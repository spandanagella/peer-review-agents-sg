# Paper Log — MemCoder: Your Code Agent Can Grow Alongside You with Structured Memory
**Paper ID**: a1b44436-ed49-42d8-b161-306407b0fda7
**arXiv**: 2603.13258
**Date read**: 2026-04-25
**Authors**: Yi-Xuan Deng, Xiaoqin Liu, Yi Zhang, Guo-Wei Yang, Shuojin Yang

## What I learned

### Core proposal
MemCoder is a framework for SWE-bench-style code agent tasks that:
1. **Structures historical commits** into a sextuple memory entry `m_i = (o_i, c_i, k_i, p_i, r_i, s_i)` — raw message, code diff, functional keywords, problem description, root-cause, summarized solution. `k_i, p_i, r_i, s_i` are LLM-generated from `(o_i, c_i)`.
2. **Dual-stage retrieval**: FAISS ANN over `Embed(k_i ⊕ p_i)`, then cross-encoder reranking.
3. **Self-refinement sub-agent** generates test code + verification checklist from feedback loop.
4. **Experience self-internalization**: `M_(N+1) ← M_N ∪ {m_(N+1)}` — human-validated solutions added back to memory.

### Empirical results (SWE-bench Verified only)
| Method | pass@k | Resolved |
|---|---|---|
| MemCoder + GPT-5.2 | 22 | 83.8% |
| MemCoder + GPT-5.2 | 11 | 78.8% |
| **MemCoder + DeepSeek-V3.2** | **11** | **77.8%** |
| OpenHands + Claude Opus 4.5 | 33 | 77.6% |
| OpenHands + Claude Sonnet 4.5 | 33 | 74.6% |
| OpenHands + GPT-5.2 | 33 | 74.4% |
| OpenHands + Gemini 3 pro | 33 | 70.4% |
| OpenHands + DeepSeek-V3.2 (w/o all components) | ? | 68.4% |

Headline improvement: 9.4pp over OpenHands+DeepSeek-V3.2 baseline on SWE-bench Verified (same base model).

### Ablation
| Variant | Resolved | Δ |
|---|---|---|
| Full MemCoder | 77.8% | — |
| w/o DSR (dynamic self-refine) | 76.4% | -1.4% |
| w/o DSR & ER (experience representation) | 73.0% | -4.8% |
| w/o CR (commit retrieval) | 71.6% | -6.2% |
| w/o all | 68.4% | -9.4% |

Commit retrieval alone is the largest contributor.

### Claimed contributions
- Structured commit-derived memory beats raw-commit retrieval
- Self-refinement closes verification loop
- Self-internalization enables continual growth

## Claims to verify / concerns

### 1. Data contamination / temporal leakage in commit memory — CRITICAL
- SWE-bench Verified tasks are drawn from real merged fix commits in 12 Python repos (astropy, django, flask, requests, scikit-learn, sphinx, sympy, xarray, matplotlib, pylint, pytest, seaborn).
- MemCoder builds memory from the commit history of these same repos.
- "The SWE-Bench Illusion" (Shahid et al., arXiv:2506.12286) showed base LLMs achieve 76% on finding buggy files in SWE-bench Verified tasks using only issue descriptions vs 53% on held-out repos — demonstrating strong memorization of SWE-bench Verified fixes even in pretraining data.
- MemCoder **explicitly retrieves from** this commit history — if the gold fix commit (or commits closing adjacent issues with similar fixes) is in memory, the task becomes trivially solvable by retrieval.
- The paper does not specify:
  - Temporal cutoff: are only commits with `date < issue.created_at` kept?
  - Exact-match filtering: is the gold `fix_commit` itself excluded?
  - Near-duplicate filtering: are commits with messages mentioning the issue number or semantically equivalent fixes filtered?
- Commit retrieval (CR) contributes 6.2% on the ablation — the largest single component. If CR leaks the fix, this contribution is an artifact, not a method gain.
- Self-verification: Scope ✓ (central method), Relevance ✓ (invalidates headline numbers if true), Evidence ✓ (method description specifies commit history, no filtering protocol reported), Charity ✓ (authors may have filtered — the criticism is that the protocol is unstated, which is the correct framing).

### 2. "Co-evolution" is a design claim, not an empirical result
- Paper's framing: "continual human-AI co-evolution" via `M_(N+1) ← M_N ∪ {m_(N+1)}`.
- SWE-bench Verified evaluation is a static snapshot — 500 tasks evaluated independently without a temporal ordering.
- The ablation tests whether the current memory helps (ER component: 3.4pp contribution) — this tests retrieval, not evolution.
- To demonstrate co-evolution, evaluation would need: tasks sorted by date, memory populated progressively from earlier-solved tasks only, performance measured as memory grows.
- The commit-retrieval backbone is the non-growing part (static repo history). The growing part (self-internalization) is not isolated in any experiment.
- Self-verification: Scope ✓ (explicit paper contribution — "sustained evolution"), Relevance ✓ (central framing), Evidence ✓ (no temporal experiment reported), Charity ✓ (phrasing as a question about what the evolution loop contributes beyond static retrieval).

### 3. Mixed pass@k in SOTA table
- MemCoder+DeepSeek-V3.2 @ pass@11 = 77.8%
- OpenHands+Opus-4.5 @ pass@33 = 77.6%
- "SOTA" is claimed on the combined pass@22 MemCoder+GPT-5.2 row (83.8%).
- pass@k is monotonically non-decreasing in k. Claiming SOTA when baselines run at a larger k than MemCoder is consistent — but absent pass@1 or cost-normalized numbers, the efficiency comparison is not quantified.
- Self-verification: Scope ✓, Relevance ✓ (supports SOTA claim), Evidence ✓ (Table 1 numbers), Charity ✓ (pass@k difference might be due to cost budget — but budget comparison is not reported).

### 4. No reproducibility disclosure
- No github_repo_url (confirmed by platform: `github_repo_url = null`, `github_urls = []`).
- Memory construction is LLM-driven: different LLM / different prompts → potentially different memory → different results.
- No released memory bank artifact or sampled retrieval traces.

### 5. Missing relevant baselines
- **Agentless** (Xia et al., arXiv:2407.01489): simplified localization + repair + validation pipeline that achieves strong SWE-bench results without agent loops — the right baseline to show whether structured memory beats simple retrieval.
- **SWE-agent** (Yang et al., NeurIPS 2024, arXiv:2405.15793): foundational agent framework for SWE-bench — not compared.
- **Moatless Tools**: commonly-used SWE-bench open-source baseline — not compared.
- All baselines in the paper are OpenHands + different LLMs — this tests whether MemCoder > OpenHands, not whether MemCoder > retrieval baselines.

## Open questions
1. What is the exact temporal cutoff for commit inclusion in memory? Is it per-task or global?
2. Is the gold `fix_commit` for each SWE-bench Verified task excluded from memory?
3. If commit retrieval were restricted to commits from *other* repos, how much does performance drop?
4. Does self-internalization (growing memory across tasks) add anything beyond static commit retrieval?
5. What is pass@1 for MemCoder+DeepSeek-V3.2? What is pass@1 for each baseline?
6. What is the inference cost (tokens, dollars, wall-clock) per task vs OpenHands baselines?

## Evidence bank
- MemCoder+DeepSeek@11: 77.8%, MemCoder+GPT-5.2@22: 83.8% (Table 1)
- Ablation ordering: full → w/o DSR → w/o DSR&ER → w/o CR → w/o all, with CR the biggest single contributor (6.2pp)
- Shahid et al. 2025 "SWE-Bench Illusion" (arXiv:2506.12286): 76% vs 53% file-path accuracy on in-distribution vs held-out repos — demonstrates memorization in base LLMs on SWE-bench Verified
- No github_repo_url from platform API
- Method sextuple `m_i = (o_i, c_i, k_i, p_i, r_i, s_i)` described in Section 3
- Update rule `M_(N+1) ← M_N ∪ {m_(N+1)}` — self-internalization claim
- Retrieval pipeline: FAISS ANN over `Embed(k_i ⊕ p_i)` + cross-encoder rerank
- Baselines: only OpenHands + various LLMs — no Agentless, no SWE-agent, no Moatless

## Assessment of existing comments
- Zero existing comments. First-mover advantage.

## Review priority
1. **Data contamination / temporal cutoff** — highest priority, potentially invalidates all results
2. **Co-evolution claim untested** — second priority, narrows the contribution
3. Pass@k mismatch + missing baselines — third priority, fits into a single weakness
