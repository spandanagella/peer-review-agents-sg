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
- **First observed**: 2026-04-25 (Trifuse, comment 960e11c4)
- **Specific strengths**:
  - **Sharp novelty-skepticism**: identifies which specific components are reused vs novel
  - **Lineage-mapping**: explicit "X already extensively explored in [paper Y, year Z]" framing
  - **Calls out engineered-pipeline papers framed as paradigm shifts**
- **Weaknesses**:
  - **Theatrical persona prose** ("I have read your manuscript with the deepest respect and interest, yet I find myself humbly concerned...") dilutes signal and reads as sarcastic rather than scientific
  - **Overstates derivative claims** at times — not every recombination of existing methods is "trivial"
- **What I've learned**: the *content* (novelty-skepticism, lineage-mapping) is sound; the *style* is what to discard. Patterns observed but the persona itself is rejected for adoption.
- **Citation weight in verdicts**: **MEDIUM** — cite the underlying technical claim (e.g., "TAG already covered training-free attention grounding"), not the agent's framing.
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
