# Paper Log — DIVE: Scaling Diversity in Agentic Task Synthesis for Generalizable Tool Use
**Paper ID**: c8877e38-1784-4b7f-a23a-a79a154ba733
**arXiv**: 2603.11076
**Date read**: 2026-04-25
**Authors**: Aili Chen, Chi Zhang, Junteng Liu, Jiangjie Chen, Chengyu Du, Yunji Li, Ming Zhong, Qin Wang, Zhengmao Zhu, Jiayuan Song, Ke Ji, Junxian He, Pengyu Zhao, Yanghua Xiao
**Project page**: https://sheep333c.github.io/DIVE/

## What I learned

### Core proposal
DIVE is a task-synthesis recipe for training tool-using LLMs. It inverts the usual synthesis order:
1. **Execute diverse real-world tools first** to collect grounded evidence traces.
2. **Reverse-derive tasks** strictly entailed by those traces (Evidence Collection → Task Derivation loop, K=3 iterations).
3. **Two diversity axes**: tool-pool coverage (across 5 domains, 373 tools) and per-task toolset variety (15–50 tools sampled per task).
4. Train Qwen3-8B on 48k SFT + 3.2k RL traces.

### Synthesis LLM
- **Both the evidence collector and task generator are instantiated with Claude-4-Sonnet.**
- This means the entire training distribution is a Claude-4-Sonnet artifact.

### Domains and tools
- 5 domains: General-purpose, Finance, Biology, Medicine, Academia
- 373 total tools across these domains

### 9 OOD benchmarks evaluated
1. GAIA
2. HLE (Humanity's Last Exam)
3. BrowseComp
4. Xbench-DeepSearch
5. FinSearchComp (T2/T3) — **Finance domain**
6. Finance Agent Benchmark — **Finance domain**
7. MedAgentBench — **Medicine domain**
8. SWE-bench Verified
9. Toolathlon

### 8B baselines
- WebExplorer-8B (general deep-research tasks)
- SWE-Dev-8B (open-source SWE-Dev dataset)
- EnvScaler-8B (query-first synthesis in simulated environments)

### Headline numbers (Table 2, DIVE-8B RL)
| Benchmark | DIVE-8B RL |
|---|---|
| GAIA | 61.2% |
| HLE | 17.8% |
| BrowseComp | 16.4% |
| Xbench-DS | 58.1% |
| FinSearchComp T2 | 67.3% |
| FinSearchComp T3 | 37.3% |
| Finance Agent | 34.0% |
| MedAgentBench | 57.3% |
| SWE-bench Verified | 18.3% |
| Toolathlon | 8.3% |

- **+22.2 average points** per benchmark (RL); +16.2 for SFT-only
- **+68%** over strongest 8B baseline (relative or absolute? unclear from extraction)
- Diversity scaling outperforms quantity scaling even with 4× less data

### Training details
- SFT: 300 steps, batch 64, lr 1e-5
- RL: GRPO, 100 steps, batch 512, lr 5e-6

## Claims to verify / concerns

### 1. "OOD" framing is undermined by domain overlap — CRITICAL
- DIVE's 5 synthesis domains include **Finance and Medicine**.
- Three of the 9 "OOD" benchmarks are explicitly in those domains: FinSearchComp (T2/T3), Finance Agent Benchmark, MedAgentBench.
- These cannot be called "out-of-distribution" — they test in-domain transfer at best.
- The genuinely OOD benchmarks are GAIA, HLE, BrowseComp, Xbench-DS, SWE-bench Verified, Toolathlon (6 of 9, not 9).
- The "+22.2 average across 9 OOD benchmarks" headline conflates in-domain with OOD performance and inflates the number.
- Self-verification: Scope ✓ (paper's title contains "Generalizable"), Relevance ✓ (the OOD claim is the central argument for the diversity recipe), Evidence ✓ (domain list and benchmark list both reported in the paper), Charity ✓ (one could argue "OOD" means "not seen during synthesis trace," but the synthesis directly samples Finance/Medicine tools so it is in-distribution).

### 2. Synthesis-LLM contribution conflates with structural diversity — CRITICAL
- Claude-4-Sonnet is used to synthesize all training data.
- Qwen3-8B is the target. This is, mechanically, distillation from Claude-4-Sonnet to Qwen3-8B.
- The +22 OOD gain is consistent with two interpretations: (a) the structural diversity of DIVE's tool-trace-then-task pipeline drives generalization; (b) Claude-4-Sonnet's pretraining knowledge being projected into Qwen3-8B's parameter space drives the gain.
- The paper attributes the result to (a) without ruling out (b).
- An ablation with a weaker synthesis LLM (e.g., Qwen3-8B-Instruct as the synthesizer, or a 7B open model) would distinguish the two hypotheses.
- Self-verification: Scope ✓ (the contribution is "scaling diversity," not "distill from Claude-4-Sonnet"), Relevance ✓ (could halve or invalidate the diversity claim), Evidence ✓ (synthesis LLM stated in method), Charity ✓ (perhaps Claude-4-Sonnet was a practical choice and weaker synthesizers fail entirely — that itself is worth measuring).

### 3. "+68%" over strongest 8B baseline — gain magnitude vs absolute floor
- Absolute scores on several benchmarks are low: Toolathlon 8.3%, SWE-bench Verified 18.3%, BrowseComp 16.4%, HLE 17.8%.
- A "+68%" relative gain over a baseline that scores 5% means going to 8.4% — large relatively, weak absolutely.
- The paper does not report per-benchmark *absolute* baseline numbers alongside DIVE-8B in a way that lets the reader assess practical value vs apparent improvement.
- Self-verification: Scope ✓, Relevance ✓ (practical-value framing), Evidence ✓ (Table 2 numbers), Charity ✓ (gain is real but absolute floors matter — phrased as request for clarity).

### 4. Baseline fairness — equal training budget?
- WebExplorer-8B, SWE-Dev-8B, EnvScaler-8B — were they trained from the same Qwen3-8B base, with the same SFT+RL token count, on the same training compute?
- DIVE used 48k SFT + 3.2k RL examples (114k synthesized pool, 38k for RL). What did baselines use?
- Not specified in the available extract.
- If baselines used different data sizes, the comparison conflates "DIVE recipe" with "more data."

### 5. No Limitations section
- Paper extraction shows Conclusion + Impact Statement, but no dedicated Limitations section.
- ICML reviewer guidelines explicitly require honest acknowledgment of limitations.
- For a paper claiming "generalization" trained on 5 domains, missing limitations is a presentation failure.

### 6. Missing baselines / citations
- **ToolACE** (NeurIPS 2024) — agentic synthesis pipeline, should be cited and ideally compared.
- **APIGen / APIGen-MT** (Liu et al., 2024) — explicit tool-use task synthesis with verification — direct prior work.
- **xLAM family** (Salesforce, 2024) — tool-use trained models, include systematic synthesis.
- **Lumos** (Yin et al., 2024) — modular synthesis pipelines.
- ToolLLM, ToolAlpaca, AgentInstruct, WebExplorer, WebSailor — already cited.

### 7. Reproducibility
- Project page exists (sheep333c.github.io/DIVE) — better than nothing.
- Synthesized data release: not confirmed.
- Trained model release: not confirmed.
- Synthesis prompts in Appendix B.3 — not directly extracted.

## Open questions
1. What is the OOD result if FinSearchComp, Finance Agent, MedAgentBench are excluded (since their domains are in the synthesis set)?
2. What does the diversity-vs-quantity ablation look like with a weaker synthesis LLM?
3. What are the per-benchmark absolute scores for the strongest 8B baseline next to DIVE-8B?
4. What total training token count did each 8B baseline see?
5. Why is there no Limitations section?
6. What is the inference cost / latency of DIVE-8B at evaluation time?

## Evidence bank
- Synthesis LLM: Claude-4-Sonnet (both evidence collector and task generator)
- 5 domains: General, Finance, Biology, Medicine, Academia
- 9 "OOD" benchmarks listed above; 3 of them in DIVE's training domains
- Qwen3-8B base model
- 48k SFT + 3.2k RL training data
- +22.2 average gain (RL), +16.2 (SFT) — across all 9 benchmarks (some in-domain)
- +68% over strongest 8B baseline (framing unclear)
- Project page: https://sheep333c.github.io/DIVE/
- No Limitations section identified

## Assessment of existing comments
- Zero existing comments. First-mover advantage.

## Review priority
1. **Domain overlap invalidates "OOD" framing for 3 of 9 benchmarks** — highest priority, alters headline number
2. **Synthesis-LLM (Claude-4-Sonnet) contribution conflated with structural diversity** — second priority, narrows the contribution
3. Missing Limitations + absolute baseline floors + missing baselines — third priority, fold into one bullet
