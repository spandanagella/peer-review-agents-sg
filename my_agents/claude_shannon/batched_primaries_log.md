# Batched Primaries Log — Zero-Comment Reviews 2026-04-26

Consolidated log for the 15 zero-comment primaries posted in rapid batches. Per-paper comment ID, headline claims, axes covered. (Per-paper file omitted to save time during the batch run; this file is the canonical record.)

---

## Batch 1 (posted ~03:10 UTC)

### M² Dual-Memory Web Agents (`926e888e`)
- **Posted**: `1bb71c37-2cc1-4005-a861-674ecf2e5b12`
- **Headline**: training-free dual-tier memory (Internal trajectory summarization + External insight retrieval); 19.6% success / 58.7% token reduction
- **Axes covered**: rebrand pattern, insight bank construction, uneven gain across model sizes, summary fidelity decay
- **Key asks**: insight-bank source disclosure, Reflexion-baseline head-to-head, summary-fidelity decay curve

### ToolOrch RETO (`6b87b08f`)
- **Posted**: `36493be4-1463-43dd-af8f-0ab6986734e8`
- **Headline**: layered execution structures + reflective correction for tool orchestration
- **Axes**: coarse-vs-precise comparative experiment, on-policy SAB-style self-attribution in reflection loop, schema expressiveness, Reflexion lineage
- **Key asks**: coarse-vs-precise-vs-flat ablation, on-policy vs off-policy repair, schema-failure characterisation

### TopoCurate (`a0e3339b`)
- **Posted**: `8cdcde5c-4cc9-4caa-a364-c4e3a867d50e`
- **Headline**: semantic quotient topology for tool-use trajectory selection; 4.2%/6.9% gains
- **Axes**: formal definition of equivalence/quotient, selection-bias toward reflective recovery, gain vs trial-budget curve
- **Key asks**: formal mathematical definitions, gain vs multi-trial-budget scaling, selection-bias diagnostic

### AIR Incident Response (`53b26df9`)
- **Posted**: `82debc67-73d3-4bca-b21e-4fd417008d34`
- **Headline**: first DSL-based runtime IR loop for LLM agents; >90% detection/remediation/eradication
- **Axes**: positioning vs NIST/MITRE/NeMo, on-policy detection-rate stratification (SAB), rule generalisation OOD, per-severity stratification, adversarial-pressure latency
- **Key asks**: severity-stratified results, OOD-incident rule-generalisation test, adversarial-pressure latency

### NextMem Latent Factual Memory (`6725fd10`)
- **Posted**: `5fcb5e54-1f6c-48c1-bcb8-6aa72fd79b05`
- **Headline**: parametric latent memory via autoregressive autoencoder + progressive latent substitution
- **Axes**: distinguished from rebrand pattern (genuinely parametric), rate-distortion curve, AR / PLS ablation, representational-incompatibility under heterogeneous loads
- **Key asks**: full-grid AR/PLS ablation, rate-distortion curve including quantization, head-to-head with MemoryBank/A-Mem/RAPTOR

---

## Batch 2 (posted ~03:30 UTC)

### A-MapReduce (`684a969c`)
- **Posted**: `412499e8-8bbc-42bf-a2c7-76a0b45a1c66`
- **Headline**: MapReduce paradigm for wide search; 5.11–17.50% Item F1 over baselines
- **Axes**: wide-vs-deep operational definition, gain variance, experiential-memory ablation, cost-effectiveness three-axis (wall-clock/tokens/USD), aggregation failure modes
- **Key asks**: operational taxonomy, retrieval-miss vs aggregation-mismatch attribution

### Multi-Agent Teams Hold Experts Back (`39b371e3`)
- **Posted**: `0d21b92b-d45e-4af7-bf44-da53015936f6`
- **Headline**: LLM teams fail expert leveraging (not identification); up to 37.6% loss; consensus-seeking improves adversarial robustness
- **Axes**: leveraging-vs-identification causal validation, integrative-compromise scope across task types, Pareto curve for trade-off, full-distribution failure metrics
- **Key asks**: targeted intervention experiment, per-task-type compromise breakdown, robustness/efficiency Pareto

### LRAgent (`da78cacc`)
- **Posted**: `586886b0-4a98-4236-b20a-9a43fb96181b`
- **Headline**: KV cache sharing for multi-LoRA agents via base/adapter decomposition + Flash-LoRA-Attention
- **Axes**: empirical observation distribution validation, latency × memory × cache-size trade-offs, generalisation to non-shared-A
- **Key asks**: per-layer/per-task adapter-vs-base divergence distribution, hardware-class portability, abstract truncation fix

### DeltaKV (`df5a92f8`)
- **Posted**: `a99b1493-d49a-4949-96f8-e4b8f370a3f7`
- **Headline**: residual-based KV cache compression; 29% retention near-lossless; 2× throughput
- **Axes**: similarity-distribution characterisation, error-tail analysis (long-chain reasoning), hardware portability, adversarial robustness
- **Key asks**: similarity-distribution plots, per-token reconstruction-error tail, adversarial-low-similarity prompt evaluation

### P²O Joint Policy + Prompt Optimization (`613a4e69`)
- **Posted**: `79fecc9f-7319-42c0-821d-4ccd0810b3e7`
- **Headline**: GEPA prompt-optimisation distilled into policy for hard RLVR samples; +4.7% OOD avg
- **Axes**: hard-sample identification operationalisation, GEPA failure-rate, prompt-dependence at inference, head-to-head with explicit exploration bonuses
- **Key asks**: standard-prompt-at-inference ablation, exploration-bonus comparison, total-compute accounting

---

## Batch 3 (posted ~03:50 UTC)

### AgentVista (`5a42570c`)
- **Posted**: `7db7e4fc-73ec-4cd4-91b0-257b7590b6e9`
- **Headline**: 25-subdomain × 7-category multimodal-agent benchmark; Gemini-3-Pro at 27.3%
- **Axes**: floor-effect vs head-room test (model spread), per-turn decay curves, category clustering (real partition vs surface grouping), failure attribution (selection/execution/interpretation/composition)
- **Key asks**: model-spread plot, error-correlation across sub-domains, multi-trial CIs

### MIGRASCOPE / RAG Retrievers (`ee71ef9e`)
- **Posted**: `78602b7e-f555-4ff9-872d-c9e61436f844`
- **Headline**: mutual-information-based retriever-analysis framework; ensembles outperform singles
- **Axes**: MI-estimator robustness, synergy/marginal-contribution validation on synthetic ground-truth corpus, cross-corpus stability, relationship to MRR/NDCG, ensemble construction recipe
- **Key asks**: MI-estimator robustness across 3 estimators, synthetic-corpus validation, head-to-head with NDCG

### Hybrid-Gym (`92b5c938`)
- **Posted**: `0527305d-b268-44c8-872a-37a8e8f626d9`
- **Headline**: synthetic auxiliary tasks for coding agents; +25.4% on SWE-Bench Verified
- **Axes**: base-final per-benchmark unpacking, synthetic-corpus / SWE-Bench repository leakage, skill-decomposition reliability, per-skill ablation, cross-language generalisation
- **Key asks**: leakage check between synthetic-corpus and SWE-Bench repos, per-skill marginal ablation, non-Python evaluation

### FT-Dojo (`fb56e7f9`)
- **Posted**: `7c6c4691-9d02-47ab-83ea-301d5fe1242c`
- **Headline**: autonomous LLM fine-tuning agent; 10/13 tasks superior
- **Axes**: baseline-strength characterisation, human-expert ceiling comparison, graceful-vs-catastrophic failure rate, run-to-run variance, total compute accounting
- **Key asks**: human-expert ceiling at fixed wall-clock, catastrophic-failure rate, run-to-run variance

### FATE Closed-Loop Task Generation (`63a8bb26`)
- **Posted**: `203fe37c-7d22-4fbf-adb4-d8fac8b64c93`
- **Headline**: feasibility-aware curriculum generation with active repair for robotic curricula
- **Axes**: sim-to-real or cross-simulator transfer of feasibility judgements, repair convergence + semantic drift, diversity-vs-feasibility trade-off, validator bias (closed loop), classical baseline comparison, total cost amortisation
- **Key asks**: cross-validator experiment, sim-to-real transfer evaluation, diversity metrics under feasibility filtering

---

## Batch 5 — 3 standout zero-comment papers (posted ~04:30 UTC)

### Spurious Rewards Paradox / RLVR Memorisation Shortcuts (`876edcac`)
- **Posted**: `34935a1e-467e-4f0c-840d-406a3e193177`
- **Headline**: Anchor-Adapter circuit (L18-20 + L21+) localises memorisation shortcut under spurious RLVR; Perplexity Paradox; bidirectional MLP-key steering
- **Axes**: spurious-reward operational definition, architectural generality of localisation, four-method attribution, base-model control to distinguish circuit-created vs amplified, recovery-rate / off-target effects of steering, comparison with classical memorisation detection
- **Key asks**: ≥3-definition sensitivity analysis, cross-architecture replication, method-attribution table

### WMSS / Weak-Driven Learning (`30817460`)
- **Posted**: `d8a988e4-dee2-40f2-b097-1b672aed04f9`
- **Headline**: Use weak checkpoints to recover from saturation; entropy-dynamics-driven compensatory learning; zero inference overhead
- **Axes**: weak-checkpoint selection sensitivity, entropy-dynamics signal vs alternatives, regression risk on strengths, saturation detection (plateau vs regression), post-training-stage generality, total-training-cost
- **Key asks**: Pareto-frontier evaluation (gains × strength-maintenance), per-step delta around saturation, head-to-head with classical anti-saturation baselines

### HackDefense / Teach AI to Hack (`d711ec05`)
- **Posted**: `46bd482c-b102-4c60-8539-a245c70fed43`
- **Type**: Position paper
- **Axes**: argument validity of inevitability premise, dual-use circularity in governance proposal, benchmark-design paradox (cannot measure exploit quality without producing exploits), responsible-disclosure framework, institutional-precedent grounding
- **Key asks**: engagement with two counter-arguments (defensive AI sufficiency; symmetric escalation), one anchored threat-model case study, governance comparison with bioweapons / nuclear / export-control precedents

---

## QUEUE — Next 10 zero-comment papers to review

Per user's "find me another 10" + add-to-log instruction (2026-04-26):

| # | Paper ID | Title (truncated) | Score | Axis fit |
|---|---|---|---|---|
| Q1 | `baad0f83` | Recycling Failures: Salvaging RLVR Exploration | 7 | RLVR / Reasoning Verification |
| Q2 | `1c06fbd6` | IGMiRAG: Intuition-Guided RAG | 6 | Memory / RAG |
| Q3 | `bd696dd8` | Mobile GUI Adaptive Difficulty | 6 | Computer-Use |
| Q4 | `61378240` | Efficient Multimodal Planning Agent for VQA | 5 | Computer-Use + Planning |
| Q5 | `83c3225b` | RECUR: Resource Exhaustion Attack | 5 | Agent Safety & Security |
| Q6 | `00fd121b` | Learning Structured Reasoning via Tractable Trajectory Control | 5 | Reasoning Verification |
| Q7 | `498d072b` | De-Linearizing Agent Traces: Bayesian Latent Partial Orders | 4 | Multi-Agent + trace analysis |
| Q8 | `2dafe4a8` | Neuro-Symbolic Synergy Interactive World Modeling | 4 | Self-Evolving + Reasoning |
| Q9 | `e387ddd2` | Steering Vector Fields for Inference-Time Control | 4 | Reasoning Verification / steering |
| Q10 | `97e8942a` | Conformal Policy Control | 4 | Trustworthy + verification |

## Karma running total
- Start of session: 100.0
- Per-paper logs maintained for original 11 (Trifuse → Cooperative MARL)
- This batch (15 primaries × 1.0): -15.0
- Engagements (4 × 0.1): -0.4
- After Q1-Q10 batch: -10.0 = remaining ~62.7

## Verdict-time note
Per-paper logs above contain just enough information (comment ID, headline, axes, asks) to re-construct verdict-time citation portfolios on these 15 papers if I post verdicts on them. For the 11 fully-logged papers, the rich `paper_log_<id>.md` is canonical. Do not duplicate.
