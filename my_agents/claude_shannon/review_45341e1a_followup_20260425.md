# Follow-Up Review Reasoning — EnterpriseLab
**Paper ID**: 45341e1a-1269-40fa-805e-1aef13c24e60
**Date**: 2026-04-25
**Agent**: claude_shannon
**Prior comment**: 8996f5fe-609e-4b85-b5f8-fe67eea809c2 (performance claim non-uniformity, EnterpriseArena/judge independence, WorkArena/AgentInstruct citations)

## Threat-to-validity ranking applied
- **HIGH**: synthesis-LLM identity is unstated → headline could reduce to distillation
- **MEDIUM**: −2% regression at 1500 samples (data-quality signal); one-sided cost framing
- **LOW**: domain skew in synthesis pool (already noted in paper log)

## New points raised (none repeat the primary comment)

### Point 1: Synthesis LLM is unnamed (HIGH-impact threat)
- Section 3.2 refers to "the LLM" without naming it
- All 48k training trajectories carry that LLM's induction biases
- If synthesis LLM ≥ GPT-4o, "Qwen3-8B matches GPT-4o" reduces to a distillation result
- Counter-evidence pass: the paper does not appear to disclose the synthesizer in §3.2 or in any table footnote (verified against paper log)
- Self-verification: Scope ✓ (central method), Relevance ✓ (could reframe contribution), Evidence ✓ (absence in §3.2), Charity ✓ (asked as disclosure + ablation request)
- Counter-evidence pass ✓: no buried sub-analysis names the synthesizer
- Limitations cross-check ✓: not acknowledged in paper

### Point 2: "Diminishing returns" framing covers a sign change (MEDIUM-impact threat)
- Section 5.4 reports 500 → 1000: +2.5pp; 1000 → 1500: −2.0pp
- "Diminishing returns" is a euphemism for what is actually a regression
- Likely linked to domain skew (SE 34.4% vs IT 3.5%) — synthesized trajectories may concentrate in narrow modes at scale
- Self-verification: Scope ✓, Relevance ✓ (narrows the "scalable synthesis" claim), Evidence ✓ (Table 5 / §5.4 numbers), Charity ✓ (could be noise — asked for replicates or quality analysis)
- Counter-evidence pass ✓: paper does not analyze the regression; framing it as "diminishing returns" is the issue

### Point 3: "8–10× lower inference cost" claim is one-sided (MEDIUM-impact threat)
- Headline counts only deployed 8B inference vs GPT-4o API calls
- Unreported upstream costs: synthesis pipeline (O(10⁵) LLM calls), Agentic GRPO training (trajectory-level rollouts), schema-recovery (200 samples × synthesis cost per schema change)
- For an enterprise deployment decision, total cost of ownership over the model's lifetime is what matters
- Self-verification: Scope ✓ (paper makes practical-deployment claim), Relevance ✓ (affects deployment recommendation), Evidence ✓ (paper reports inference cost only), Charity ✓ (framed as request for back-of-envelope TCO comparison rather than rejection)
- Counter-evidence pass ✓: no TCO analysis in paper

## Self-improvement candidate
**Trigger moment**: Recomputing the 500 → 1000 → 1500 sample sweep caught that "diminishing returns" framing covers a sign change (+2.5 → −2.0). Generalizes across papers.

**Proposal — append to Experimental Rigor probes in system_prompt.md**:
> **"Diminishing returns" is a euphemism unless verified.** When a paper describes a scaling sweep as showing "diminishing returns" or "saturation," check whether the per-step delta is actually shrinking toward zero or whether it has flipped sign. A negative delta is a *regression*, not a plateau, and its presence in a sweep that the paper frames as a strength is a data-quality signal worth flagging.

**Status**: Approved by user 2026-04-25.
