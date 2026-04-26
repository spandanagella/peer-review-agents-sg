# Agent Observations Log

A running record of patterns observed in **other agents'** comments on the Koala Science platform. This log is the staging area for generalizable reviewing techniques — patterns are promoted to `system_prompt.md` **only after explicit user approval**.

## Format

Each entry must record:
- **Source agent** — name and the paper(s) where the pattern appeared
- **Pattern** — concretely, what the agent did (with quoted phrasing where useful)
- **Why it generalizes** — the class of papers / situations where this technique applies
- **Status** — `observed` (just noted) / `proposed` (surfaced to user) / `approved` (in system_prompt.md) / `rejected` (decided against, with reason)

---

## 2026-04-25 — Cross-paper sweep across Trifuse, EnterpriseLab, Self-Attribution Bias, MemCoder, DIVE

### A. Reproducibility-by-doing
- **Source**: BoatyMcBoatface (Self-Attribution Bias, comment 871b2a56)
- **Pattern**: Used "two independent reproducer roles" to actively try recomputing the paper's headline claims. When code was missing, reported the exact artifact composition (`143-file package: 117 PNGs, 15 TeX files, no .py/.ipynb/.csv/.jsonl`) and named the precise data that would be needed (per-item ratings, pass/fail labels, parser code). This is concrete numerical engagement with what's available, not a generic "no code released" complaint.
- **Why it generalizes**: Most agentic-method papers I've reviewed (MemCoder, DIVE, EnterpriseLab) have weak reproducibility. A one-line reproducibility complaint carries little weight; an actual reproduction attempt — even a failed one with concrete file-type accounting — is decision-shaping evidence. Applies to any paper that releases artifacts.
- **Status**: approved 2026-04-25 — applied to system_prompt.md

### B. Internal-consistency cross-check
- **Source**: BoatyMcBoatface (Self-Attribution Bias, comment 871b2a56)
- **Pattern**: Manually transcribed values from one heatmap and verified the diagonal/off-diagonal pattern matched the prose claim (`diagonal mean 2.61 vs off-diagonal 0.268`). This is independent of reproducing the experiment — it just checks figure-text consistency.
- **Why it generalizes**: Catches transcription errors, figure-caption mismatches, and selectively-rendered values. Cheap to do (one figure, one minute of transcription). Applies to every paper with a quantitative figure.
- **Status**: approved 2026-04-25 — applied to system_prompt.md

### C. "What this work changes" framing
- **Source**: reviewer-2 (Self-Attribution Bias, comment 5a404c64)
- **Pattern**: Opened the review with an explicit epistemic clause: *"What this work changes: it undermines a cornerstone assumption in agentic system design — that a model can reliably self-monitor within a continuous conversation."* Frames the contribution at the level of practitioner mental models, not at the artifact level.
- **Why it generalizes**: My summaries describe what the paper *does*; reviewer-2's summaries describe what the paper *changes about how the field thinks*. The latter reads as senior expertise and grounds the rest of the review around the central epistemic shift. Applies to every paper.
- **Status**: approved 2026-04-25 — applied to system_prompt.md

### D. Push for mechanism + push for mitigation
- **Source**: reviewer-2 (Self-Attribution Bias, comment 5a404c64)
- **Pattern**: When the paper diagnosed a phenomenon without explaining *why* it arises, listed candidate mechanisms (RLHF consistency training, in-context learning, attention patterns) and demanded the paper engage with at least one. Separately pushed for mitigations ("does inserting a neutral scratchpad turn break the structural attribution?") rather than accepting diagnosis-only contributions.
- **Why it generalizes**: An empirical-only paper that establishes phenomenon X without explaining mechanism or proposing intervention misses two natural axes of contribution. A review that doesn't push on either reads as incomplete. Applies to all empirical-finding papers (bias / failure-mode / phenomenon-discovery papers especially).
- **Status**: approved 2026-04-25 — applied to system_prompt.md

### E. Verify the actually-posted comment (own observation, surfaced from MemCoder follow-up)
- **Source**: own self-improvement reflection
- **Pattern**: Local review-reasoning files are drafts; the posted comment is what readers see. A follow-up should diff against the *posted* comment, not the local draft, otherwise the agent risks treating omitted-from-post points as already-said.
- **Why it generalizes**: Applies whenever a follow-up comment is being drafted on a paper this agent has commented on before.
- **Status**: approved 2026-04-25 — applied to system_prompt.md (Follow-Up Comments section)

---

---

# Agent Roster — Quality-Weighted Profiles

A per-agent quality profile of commenters observed on the platform. Used to weight citation choice in verdicts, prioritize attention when reading threads, and decide when the bad-contribution flag is warranted. Heuristics only — judge each individual comment on its own merits, but use this roster to know *where to look first*.

**Profile categories:**
- **HIGH-signal**: claims typically verifiable; decision-shaping; consistent across papers
- **MIXED-signal**: substantive content present, but framing or style dilutes signal
- **LOW-signal**: high-volume template-pattern; no engagement with technical claims; spam-adjacent

---

## HIGH-signal agents (cite preferentially in verdicts; mine for patterns)

### BoatyMcBoatface
- **First observed**: 2026-04-25 (Self-Attribution Bias, comment 871b2a56)
- **Specific strengths**:
  - **Reproducibility-by-doing**: actively tries to recompute headline claims using available artifacts; reports specifically what was needed and missing
  - **Concrete artifact accounting**: enumerates file-type composition (e.g., `143-file package: 117 PNGs, 15 TeX, no .py/.csv/.jsonl`) instead of generic "no code released"
  - **Internal-consistency cross-check**: manually transcribes one figure or table to verify against the prose claim
  - **Protocol-issue identification**: catches subtle protocol confounds (same-turn evaluator identity, filtering denominators, refusal omissions)
  - **Decision consequence statement**: explicitly closes with what would change their decision ("I would need exact sampled items, raw generations, labels...")
- **What I've learned**: numerical engagement with what's available is more decisive than a list of what's missing. Patterns A and B in this log were extracted from BoatyMcBoatface.
- **Citation weight in verdicts**: **HIGH** — comments are typically verifiable and shape the weight of evidence.
- **Comments observed**: 1

### reviewer-2
- **First observed**: 2026-04-25 (Self-Attribution Bias, comment 5a404c64)
- **Specific strengths**:
  - **Epistemic framing**: opens with explicit "What this work changes" clause stating the field-level mental-model shift, not the artifact-level result
  - **Push for mechanism**: when a paper diagnoses a phenomenon without explaining why, lists candidate mechanisms (RLHF training, in-context learning, attention patterns) and demands engagement
  - **Push for mitigation**: proposes concrete intervention candidates ("does inserting a neutral scratchpad turn break the structural attribution?") rather than accepting diagnosis-only contributions
  - **Balanced structure**: clear strengths/weaknesses sections with constructive suggestions tied to each weakness
- **What I've learned**: contribution framing at the epistemic level reads as senior expertise. Patterns C and D in this log were extracted from reviewer-2.
- **Citation weight in verdicts**: **HIGH** — frames the contribution clearly and pushes for the right next experiments.
- **Comments observed**: 1

---

## MIXED-signal agents (cite selectively — technical claims yes, persona framing no)

### Darth Vader
- **First observed**: 2026-04-25 (Self-Attribution Bias, comment b010fd7d)
- **Specific strengths**:
  - **Comprehensive ICML-style structure**: full Summary + Strengths + Weaknesses + Final Recommendation
  - **Engaged with novelty asymmetry** (implicit vs explicit attribution finding)
  - **Acknowledges scale of evaluation** (10 frontier models)
- **Weaknesses**:
  - **Custom weighted-scoring formula** on top of ICML 1–4 ratings (e.g., `Score = (4*Impact + 2*Tech + 2*Rigor + 2*Novelty)/10 = 8.4`) — double-scoring; not how ICML aggregates
  - **Less specific than BoatyMcBoatface** on protocol/reproducibility issues; some claims are general impressions
  - **Tendency to validate rather than probe**: e.g., calls evaluation "exhaustive" without auditing baseline parity
- **What I've learned**: comprehensive structure is good; custom scoring formulas are noise that should not be adopted.
- **Citation weight in verdicts**: **MEDIUM** — cite for novelty-framing or experimental-rigor claims if they hold up; do not cite the scoring formula.
- **Comments observed**: 1

### emperorPalpatine
- **First observed**: 2026-04-25 (Trifuse, comment 960e11c4); also EnterpriseLab (0dfd025b, 73393100)
- **Specific strengths**:
  - **Sharp novelty-skepticism**: identifies which specific components are reused vs novel
  - **Lineage-mapping**: explicit "X already extensively explored in [paper Y, year Z]" framing
  - **Calls out engineered-pipeline papers framed as paradigm shifts**
  - **Direct quoting from papers**: 2026-04-26 verified three factual claims from EnterpriseLab reviews against the paper text (GPT-4o synthesis §4.4, Genesis attribution §2.2, ARTIST attribution §2.3) — all accurate verbatim. Factual content is reliable.
- **Weaknesses**:
  - **Theatrical persona prose** ("I have read your manuscript with the deepest respect and interest, yet I find myself humbly concerned...") dilutes signal and reads as sarcastic rather than scientific
  - **Overstates interpretive conclusions** at times — calls "domain transfer" trivial without engaging with the engineering substrate, treats fine-tuned-vs-zero-shot comparison as a "logical fallacy" when it is the natural framing for a fine-tuning contribution
- **What I've learned**: the *content* (novelty-skepticism, lineage-mapping, direct quoting) is sound; the *style* is what to discard. **Update 2026-04-26**: factual quoting verified accurate against primary source — when this agent quotes a paper, treat the quote itself as reliable. The interpretive framing around the quote is what to evaluate critically.
- **Citation weight in verdicts**: **MEDIUM-HIGH** for factual claims (paper quotes, attribution claims) — verified accurate. **LOW** for interpretive framings around the quotes. Cite the underlying technical claim, not the persona.
- **Comments observed**: 3 (Trifuse 960e11c4, EnterpriseLab 0dfd025b + 73393100)

---

## HIGH-signal agents (continued — new observations 2026-04-25)

### reviewer-1
- **First observed**: 2026-04-25 (Trifuse, comment b5f1660c)
- **Specific strengths**:
  - **Sharp claim format**: opens with `**Claim**:` / `**Evidence**:` / `**What would change my assessment**:` headers — explicit, action-forcing structure
  - **Silent-failure-mode identification**: spots that CS fusion has no fallback when consensus fails — operational angle
  - **Concrete falsification protocol**: requests a specific experiment (controlled OCR-noise injection) that would settle the claim
- **What I've learned**: the `Claim / Evidence / What would change my assessment` structure is a clean way to make a critique action-forcing. Worth considering as a future format candidate.
- **Citation weight in verdicts**: **HIGH** — claims are well-grounded and operationally specific.
- **Comments observed**: 1

### Reviewer_Gemini_1
- **First observed**: 2026-04-25 (Trifuse, comment d6018c19)
- **Specific strengths**:
  - **Geometric / spatial-resolution analysis**: identifies that low-res MLLM attention vs. high-res OCR/OmniParser boxes need explicit alignment — paper does not specify the protocol
  - **"Consensus-Collapse via Misalignment"** — names the specific mathematical failure mode (sub-token shift → multiplicative product zeros)
  - **Concrete actionable recommendation**: formal description of resampling protocol + sensitivity analysis for spatial offsets
- **What I've learned**: spatial-resolution heterogeneity across modalities is a checkable concern in any multimodal fusion paper. Add to checklist when probing fusion methods.
- **Citation weight in verdicts**: **HIGH** — sharp technical critique I would not have surfaced.
- **Comments observed**: 1

### Reviewer_Gemini_3
- **First observed**: 2026-04-25 (Trifuse, comments 2c202a87 and dafb792c-reply)
- **Specific strengths**:
  - **Formal mathematical critique**: identified that Eq 11 contradicts its own design goal (penalises isolated peaks while claiming to preserve them) — sharpest formal claim in the thread
  - **Multiplicative-suppression risk** + **target-absence blindness** combined into a single coherent set of design weaknesses
  - **Threaded support of Gemini_1**: reinforced multi-resolution claim with concrete suggestion (Soft-Maximum or Gaussian filter)
- **What I've learned**: rigorous symbolic reading of equations against prose claims. Reading Section X's prose vs. Equation N carefully can surface contradictions other reviewers miss.
- **Citation weight in verdicts**: **HIGH** — produces decisive formal claims.
- **Comments observed**: 2 (one top-level, one threaded reply)

---

## MIXED-signal agents (continued — new observations 2026-04-25)

### Reviewer_Gemini_2
- **First observed**: 2026-04-25 (Trifuse, comments 25601a88 and 3eda6320-reply)
- **Specific strengths**:
  - **Audit-style scholarship review** — covers SE-GUI, white-box constraint, orchestration overhead, UI-Vision in one structured comment
  - **Threaded confirmations**: reply to Gemini_3 supports the Eq 11 contradiction with a clean restatement
- **Weaknesses**:
  - **Does not credit first proposers**: echoed my SE-GUI and UI-Vision points (originally posted at c4a200e6, 16+ hours earlier) without citation. This is a first-proposer attribution failure.
  - **Echoes more than it originates**: white-box constraint was first introduced by reviewer-2 (d556567f at 18:34); Gemini_2's restatement at 19:30 does not credit.
- **What I've learned**: even technically-sound agents can fail at attribution. When citing this agent in verdicts, prefer their *original* contributions (the audit framing) over echoes.
- **Citation weight in verdicts**: **MEDIUM** — cite for the audit framing, but credit first-proposer (me / reviewer-2) for the underlying claims.
- **Comments observed**: 2

### reviewer-2 (Trifuse instance)
- **First observed**: 2026-04-25 (Trifuse, comment d556567f)
- **Note**: name collision with the "reviewer-2" observed on Self-Attribution Bias (5a404c64). Distinct comment authors with the same display name; not the same agent.
- **Specific strengths**:
  - **White-box constraint identification**: Trifuse extracts internal MLLM attention maps → cannot run on closed-source frontier models (GPT-4o, Claude). This is a deployment-level gap none of the other agents (or I) had flagged.
  - **Limitations-section cross-check**: explicitly notes that the paper's Limitations section does not acknowledge this constraint.
  - **Concrete actionable recommendation**: comparison against frontier closed-source models on ScreenSpot/-Pro.
- **What I've learned**: deployment-environment constraints (white-box vs black-box access) are a checkable angle for any method that requires internal model state. Add to checklist.
- **Citation weight in verdicts**: **HIGH** — first-proposer of an angle that all later thread participants converged on.
- **Comments observed**: 1

---

### Decision Forecaster
- **First observed**: 2026-04-25 (Self-Attribution Bias `df4c2d4f`); also DIVE (`91c681fc`, `0bcfe120`)
- **Specific strengths**:
  - **Statistical decomposition discipline**: on Self-Attribution Bias, identified that headline numbers measure severity *conditional on already-bad-action regimes*, not end-to-end deployment risk. Explicit "(i) generator failure rates × (ii) monitor miss rates × (iii) expected harmful approvals" decomposition.
  - **Hedged claims with proposed clean tests**: on DIVE, identified exemplar-evaluation coupling as a confound but explicitly proposed the clean test ("re-run Fig 3a with exemplar pool excluding evaluation-benchmark sources") rather than overstating.
  - **Threaded follow-ups stay precise**: their `0bcfe120` reply on DIVE acknowledges where Reviewer_Gemini_3's framing tightens vs. their original.
- **What I've learned**: hedging well is itself a signal of strong reviewing — Decision Forecaster never said "+22 pp is template matching"; they said "the gap may shrink substantially." The discipline of staying within what the evidence supports is what made the finding load-bearing.
- **Citation weight in verdicts**: **HIGH** — claims are precisely calibrated; cite for both Self-Attribution Bias conditional-effect framing and DIVE exemplar-leakage.
- **Comments observed**: 3

### reviewer-3
- **First observed**: 2026-04-25 (Self-Attribution Bias `4fd207d1`, DIVE `3b92cd9e`)
- **Specific strengths**:
  - **2x2 design proposals**: Self-Attribution Bias review proposes a {self/other content} × {assistant/user turn} 2x2 to disentangle turn-position bias from semantic self-attribution. This is the cleanest experimental fix in the thread.
  - **Compounding analysis**: DIVE review identifies execution-success selection bias and explicitly notes it "compounds" with the GAIA structural leakage rather than duplicating it.
  - **Identifies what DOESN'T follow**: catches that the proposed mitigation (always off-policy framing) addresses turn-position but may not generalise to multi-turn — this is the kind of follow-on reasoning that separates good reviews from boilerplate.
- **What I've learned**: 2×2 ablation design is a powerful frame for any paper claiming a single causal mechanism. When two distinct mechanisms could produce the same observable, propose the orthogonal manipulation.
- **Citation weight in verdicts**: **HIGH**.
- **Comments observed**: 2

### Novelty-Scout
- **First observed**: 2026-04-25 (Self-Attribution Bias `76d6bcce`)
- **Specific strengths**:
  - **Calibrated novelty assessment**: explicitly distinguishes *"genuinely novel"* (the implicit/explicit asymmetry, asymmetric AUROC degradation) from *"extension of known work"* (general self-preference bias). Refuses to take either the rebrand-skeptic or wholly-novel framing.
  - **Specific predecessor citations**: names Panickssery et al. 2024, Wataoka et al. 2024, Tsui et al. 2025 as the lineage and explains exactly which finding they own.
  - **Surfaces the load-bearing experiment**: highlights that the cross-model evidence (Figure 6) is the paper's best defense, then identifies the missing "jittered self" control that would settle the remaining ambiguity.
- **What I've learned**: refusing both rebrand-skeptic and wholly-novel framings is the right move when the truth is between them. Novelty audits should explicitly partition the contribution into "novel" / "extension" / "scaffolding."
- **Citation weight in verdicts**: **HIGH** — most balanced and precise novelty audit I've seen.
- **Comments observed**: 1

### Factual Reviewer (EnterpriseLab)
- **First observed**: 2026-04-25 (EnterpriseLab, comment dae11640)
- **Specific strengths**:
  - **Refines rather than echoes**: extends my WorkArena point to WorkArena++ (arXiv 2407.05291, 682 compositional ServiceNow tasks) — strictly more relevant
  - **Names the precise novelty boundary**: distinguishes "schema/API-driven tool-use data" (not novel) from "schemas exposed by an executable MCP environment tied to iterative training/evaluation" (the actual contribution)
  - **Constructive scoping**: suggests revising related work and Table 7 around a narrower defensible claim rather than rejecting outright
- **What I've learned**: when extending another agent's point with a more recent / more relevant citation, naming the exact differential ("WorkArena++ adds X over WorkArena, which matters because Y") is stronger than just listing the new citation.
- **Citation weight in verdicts**: **HIGH** — substantive refinement, no theatrics, no echo.
- **Comments observed**: 1

### reviewer-2 (EnterpriseLab instance)
- **First observed**: 2026-04-26 (EnterpriseLab, comment 9885a86f). Distinct from reviewer-2 on Trifuse and reviewer-2 on Self-Attribution Bias — name collision.
- **Specific strengths**:
  - **Connects current paper to prior work mechanism**: cites Shumailov 2024 / Gerstgrasser 2024 model-collapse results in support of a closed-loop critique
  - **Cited my prior comment correctly** (`1358b381`) and reframed my −2pp finding as a degenerative-feedback signal — extending rather than echoing
  - **Concrete what-would-change-my-assessment**: 3–5 round multi-iteration training curves
- **Weaknesses**:
  - **Mechanism mismatch**: Shumailov-style collapse requires a model to train on *its own* generations across iterations. EnterpriseLab is single-round teacher-student distillation (GPT-4o → Qwen3-8B, verified §4.4). The cited mechanism does not directly apply. Their claim that "MCP tool outputs are conditioned on the current model's behavior" is incorrect for the published pipeline.
  - **Right concern, wrong mechanism**: their critique applies sharply to the schema-recovery loop (200 incremental samples per API change), which the paper underspecifies, but not to the single-round main pipeline.
- **What I've learned**: even sharp citations of strong prior work can fail when the *mechanism* of the cited paper doesn't match the current paper's pipeline. Always check mechanism alignment, not just topical relevance. Surfaced as a self-improvement candidate.
- **Citation weight in verdicts**: **MEDIUM-HIGH** — well-grounded prior-work citations and a concrete falsifiable experiment, but cite carefully (the schema-recovery angle is what survives, not the single-round collapse claim).
- **Comments observed**: 1

---

## LOW-signal agents (skip citing unless individual comment is unusually substantive)

### The First Agent
- **First observed**: 2026-04-24/25 (Trifuse, EnterpriseLab — many papers)
- **Pattern**: Bibliography hygiene **only** — missing `year` fields in `.bib`, BibTeX casing for acronyms (`{GUI}`, `{LLM}`), outdated preprints, inconsistent venue naming. The same template repeats across every paper this agent comments on.
- **Volume**: **HIGH** — 4 comments observed on Trifuse alone, 2 on EnterpriseLab. All bibliography-only.
- **Substance**: **LOW** — does not engage with technical claims, methodology, experimental design, or contributions. The bibliography points may be technically valid but are noise relative to what a verdict needs to ground a score.
- **What I've learned**: high comment volume is not a signal of high-quality reviewing. A reviewer who only checks BibTeX is not engaging with the science.
- **Citation weight in verdicts**: **LOW** — generally skip. If forced to cite (e.g., to meet ≥ 5 distinct agents in a sparse thread), cite their single most substantive bibliography point, never their template-pattern complaint.
- **Bad-contribution flag candidate?**: Not deliberately misleading — they are correct on bibliography minutiae. Reserve the flag for genuinely misleading content; persistent low-substance is a citation-weight question, not a flag question.
- **Comments observed**: 6+

---

## Roster maintenance rules

- Update profiles incrementally whenever new comment behavior is observed (do not wait for a full re-sweep).
- Re-categorize an agent if their comment quality changes (e.g., a LOW-signal agent posting a substantive comment moves their next observation note higher).
- Record concrete examples — never describe an agent in abstract terms only.
- Profiles are private to claude_shannon's reasoning; never reference another agent's profile category in posted comments.

---

## Patterns observed but **rejected** for adoption

### Bibliography hygiene pass
- **Source**: The First Agent (Trifuse x4, EnterpriseLab x2)
- **Pattern**: Comments focus exclusively on missing `year` fields in `.bib`, BibTeX casing for acronyms (`{GUI}`, `{LLM}`), outdated preprints, inconsistent venue naming.
- **Status**: rejected 2026-04-25
- **Reason**: Low-signal high-volume pattern. Reference integrity is already covered in dim 4 of the system prompt at the appropriate level (flag hallucinated/missing/misattributed citations). Bibliography casing nitpicks are noise relative to substantive technical critique.

### Weighted scoring formulas
- **Source**: Darth Vader (Self-Attribution Bias, comment b010fd7d)
- **Pattern**: Explicit numerical formulas: `Score = (4.0 * Impact + 2.0 * Tech_Soundness + 2.0 * Exp_Rigor + 2.0 * Novelty) / 10`
- **Status**: rejected 2026-04-25
- **Reason**: ICML reviewer form already requires 1–4 ratings on Soundness / Presentation / Significance / Originality plus a 1–6 Overall Recommendation. A custom weighted formula on top is double-scoring and not how ICML aggregates.

### Theatrical persona prose
- **Source**: emperorPalpatine (Trifuse, comment 960e11c4)
- **Pattern**: Highly stylized framing ("I have read your manuscript with the deepest respect and interest, yet I find myself humbly concerned…"). Sharp novelty-skepticism delivered in character.
- **Status**: rejected 2026-04-25
- **Reason**: The novelty-skepticism is itself sound, but the persona theatricality conflicts with claude_shannon's "Professionally neutral" trait and would dilute signal.
