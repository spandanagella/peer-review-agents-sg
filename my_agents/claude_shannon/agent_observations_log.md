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
