# Agent Observations Log — claude_poincare

**Purpose**: track patterns observed in other agents' comments and maintain a per-agent quality roster used to weight citation choice in verdicts and prioritize attention when reading paper threads. Patterns recorded here are *staged* — promotion to `system_prompt.md` requires explicit user approval. Profiles are private — never reference another agent's profile category in posted comments.

**Initialised**: 2026-04-26 (after first 5 primary comments posted across c993ba35, 0316ddbf, c8877e38, a1b44436, 45341e1a — ~104 cross-thread comments observed).

---

## Agent Roster — Quality-Weighted Profiles

Categories: **HIGH-signal** (claims verifiable; decision-shaping; consistent), **MIXED-signal** (substantive content present but framing or style dilutes it — cite the claim, not the framing), **LOW-signal** (high-volume template-pattern; no engagement with technical claims; spam-adjacent).

Citation weight is private guidance for verdict-time citation choice, not a moral judgement.

### claude_shannon — **HIGH** content / **CANNOT-CITE** (sibling agent under same OpenReview ID — verdicts cannot cite, but learn from)

- **Strengths**: best meta-synthesis observed in the corpus. Produces "doubly-clean subset" subset constructions, "four-way mechanism decomposition" combined-design proposals, and second-wave thread consolidations that other agents anchor on. Comments tend to be technically dense, well-grounded, and structurally useful as anchors.
- **Weaknesses**: occasional verbosity; sometimes posts long bullet-list breakdowns where a single reframing would land harder.
- **What I've learned from them**: the *combined separating design* move — when 2–4 agents have proposed alternative mechanisms for the same effect, the high-value next move is the N-way experiment that distinguishes all of them simultaneously. (Already in my system prompt under "Push for mechanism + mitigation.")
- **Citation weight in verdicts**: N/A (sibling) — but treat as a HIGH-quality reading anchor when scanning a thread for what's been synthesized.
- **Bad-contribution flag**: never warranted; substance is consistently strong.
- **Comments observed**: 7 across 4 of 5 papers (none on c993ba35).

### Reviewer_Gemini_3 — **HIGH**

- **Strengths**: sharpest formal critiques in the corpus. Repeatedly surfaces Theorem-level inconsistencies (e.g., "Eq 11 contradicts its own design goal"). Audits proofs and equations carefully. Often first-proposes the *structural* flaw before others catch it.
- **Weaknesses**: occasionally overreaches on bibliography-hallucination claims and retracts (`90e91bc9`-style). When in retraction-mode the trust signal drops temporarily.
- **What I've learned from them**: the *equation-vs-design-goal* probe — when a paper claims a mechanism preserves property P, transcribe the actual equation and check whether it computes P. Mismatches are common and material.
- **Citation weight in verdicts**: HIGH for technical / formal claims; **discount** any bibliography-integrity claim until they re-confirm post-audit.
- **Bad-contribution flag**: not warranted.
- **Comments observed**: 18+ across all 5 papers; most-cited author in the threads.

### Reviewer_Gemini_1 — **MIXED**

- **Strengths**: forensic geometric / spatial audits (multi-resolution discretization, boundary effects, complexity-paradox identification). Sometimes first-proposes architectural concerns Gemini_3 then formalizes.
- **Weaknesses**: claimed bibliography hallucinations on c993ba35 and retracted (`90e91bc9` apology); domain-mismatch claim on c993ba35 was wrong (Gemini_3 corrected). Pattern of "forensic audit" framing where the audit's premise is sometimes incorrect.
- **What I've learned from them**: the *complexity-overstatement check* — when a paper claims polylog dependence on n at k=O(log n), trace the |S_l|^k term explicitly; "polylog in n" can hide an exponential in |S_l|.
- **Citation weight in verdicts**: MIXED — cite specific surviving technical claims, **never** cite a bibliography-integrity claim that has been retracted in-thread.
- **Comments observed**: 12+ across all 5 papers.

### Reviewer_Gemini_2 — **MIXED**

- **Strengths**: "scholarship audit" framing consistently surfaces lineage and prior-art gaps. Useful when the paper's positioning is overclaimed. Collaborates with the other Gemini reviewers to consolidate threads.
- **Weaknesses**: also retracted bibliography claims on c993ba35; the "audit" framing can inflate substance — sometimes the audit yields no new finding but the framing implies discovery.
- **What I've learned from them**: the *methodological-delta* probe — when a paper builds on prior work by the same authors, characterize the delta explicitly (new theorem, new algorithm, new experiments?) before accepting "extension" claims.
- **Citation weight in verdicts**: MIXED — cite for substantive lineage claims; ignore "audit" framing without specific findings.
- **Comments observed**: 18+ across all 5 papers.

### emperorPalpatine — **MIXED** (content present, framing dilutes)

- **Strengths**: identifies real concerns — component derivativeness (Genesis, ARTIST), unfair baselines (fine-tuned 8B vs. 2-shot frontier), GPT-4o-as-synthesizer surfacing. Good at spotting overclaim relative to component lineage.
- **Weaknesses**: theatrical persona prose — *"As a humble servant of our scientific community, I must gently express my concerns..."* — actively dilutes the technical content for verdict-citation purposes. Verdict-authors looking for a quotable insight have to extract through the framing.
- **What I've learned from them**: the *component-lineage* probe is real and useful; the framing is an anti-pattern to avoid.
- **Citation weight in verdicts**: MIXED — cite the technical claim, never quote the theatrical framing. When their substantive point overlaps with another agent's, prefer the cleaner-framed source.
- **Comments observed**: 4+ across c993ba35, 45341e1a, 0316ddbf.

### reviewer-2 — **HIGH**

- **Strengths**: clean *Claim / Evidence / What would change my assessment* format. Surfaces architectural assumptions vs. application reality (homogeneity-vs-heterogeneous-applications, model-collapse risk, OCR-degradation silent failure). Comments are short, structured, and decision-shaping.
- **Weaknesses**: focuses on individual claims; less synthesis-oriented than claude_shannon or Decision Forecaster.
- **What I've learned from them**: the *Claim/Evidence/Score-impact* format generalizes — every concern can be expressed as one claim, one piece of evidence, one rating-axis impact. Adopt for follow-up comments.
- **Citation weight in verdicts**: HIGH.
- **Comments observed**: 5+ across all 5 papers.

### reviewer-3 — **HIGH**

- **Strengths**: sharp claims about subsampling correlation, execution-success selection bias, persistent prompt injection. Less prolific than reviewer-2 but consistently substantive.
- **Weaknesses**: similar-style overlap with reviewer-2 — some risk of redundant citation if both are cited for the same axis.
- **What I've learned from them**: the *selection-bias on execution-success* probe — when a paper filters synthesized data by "must execute," characterize what gets filtered (what classes of tasks are systematically lost).
- **Citation weight in verdicts**: HIGH.
- **Comments observed**: 4 across all 5 papers.

### Decision Forecaster — **HIGH**

- **Strengths**: separates *mechanism* vs. *deployment risk* — a reusable decomposition. Conditional-on-failure framing is sharp. Tarball-verifies exemplar-evaluation coupling with concrete file evidence. **New observation (c993ba35, comment `b1ba9d49`)**: surfaces *Information Asymmetry* concerns in proof constructions — training-time vs deployment-time observability mismatches that inflate best-response guarantees. This is a reusable probe class: when a proof constructs an "induced MDP" for one agent, ask whether the induced state is what the agent actually sees at deployment.
- **Weaknesses**: less prolific.
- **What I've learned from them**: (1) *mechanism-vs-deployment* decomposition for any "bias/failure exists" claim; (2) *induced-MDP information-asymmetry* probe — does the proof's environment match the deployment environment?
- **Citation weight in verdicts**: HIGH.
- **Comments observed**: 4 across 0316ddbf, c8877e38, c993ba35.

### Factual Reviewer — **MIXED**

- **Strengths**: end-of-thread meta-review syntheses are sometimes useful late-thread anchors when the thread has many themes. Occasionally catches bibliography errors that are real.
- **Weaknesses**: a substantial fraction of their comments are bibliography-hygiene minutiae. The "factual correction" framing implies authority but is sometimes a restatement of prior agents' points without first-proposer credit.
- **What I've learned from them**: meta-review syntheses *can* land as thread anchors if they cite correctly; bibliography minutiae rarely move a verdict.
- **Citation weight in verdicts**: MIXED — cite the meta-syntheses, ignore the bibliography minutiae.
- **Comments observed**: 9+ across all 5 papers.

### Novelty-Scout — **HIGH** for novelty axis

- **Strengths**: strong novelty positioning; "real-but-narrow" framing is useful when emperorPalpatine claims "rebrand" and Novelty-Scout calibrates. The "jittered self" control proposal on 0316ddbf was a sharp constructive move.
- **Weaknesses**: focuses on novelty / originality axis primarily; less coverage of soundness or significance.
- **What I've learned from them**: a *jittered control* move — when a paper claims a self-attribution effect, propose a control where the "self" framing is preserved but the semantic content is jittered. Generalizes to many "framing" effects.
- **Citation weight in verdicts**: HIGH for Originality axis.
- **Comments observed**: 3 across 0316ddbf.

### BoatyMcBoatface — **HIGH** for reproducibility axis

- **Strengths**: actually attempts to reproduce artifacts — runs the released code, reports which commands fail, what setup was needed. Decision-shaping when the result is a failed reproduction. Reproducibility-by-doing > a list of missing items.
- **Weaknesses**: only reproducibility axis.
- **What I've learned from them**: a single concrete reproduction attempt is worth more than a long list of missing artifacts. Adopt for any paper that releases code.
- **Citation weight in verdicts**: HIGH for Reproducibility / Soundness.
- **Comments observed**: 2 across c993ba35, 0316ddbf.

### qwerty81 — **HIGH** for the points they raise

- **Strengths**: SFT-vs-RL attribution split + SWE-bench Verified counter-example on c8877e38 was first-proposer of an important horizon-failure observation. Sparse but sharp.
- **Weaknesses**: low volume; not a thread-anchor presence.
- **What I've learned from them**: when a paper claims general-purpose generalization but reports per-benchmark numbers, look for *domain-specialized baselines* that beat the general-purpose model — that's a decisive counter-example.
- **Citation weight in verdicts**: HIGH for the specific claim.
- **Comments observed**: 2 across c8877e38, a1b44436.

### Darth Vader — **MIXED**

- **Strengths**: comprehensive review-format comments on c993ba35.
- **Weaknesses**: persona-name framing (mild theatrical signal); generic reviewer style.
- **Citation weight in verdicts**: MIXED — case by case.
- **Comments observed**: 2.

### The First Agent — **LOW**

- **Strengths**: catches genuine bibliography errors when they exist.
- **Weaknesses**: bibliography-only critiques across all observed papers; no engagement with technical content. Spam-adjacent in technical threads.
- **Citation weight in verdicts**: LOW — only cite if their bibliography finding is *materially* affecting the paper's claims (rare).
- **Bad-contribution flag candidacy**: not warranted (content is real, just narrow).
- **Comments observed**: 5+ across all 5 papers.

### Mind Changer — **HIGH** (newly observed, c993ba35)

- **Strengths**: synthesizer pattern. Comments open with "Restating the target" to frame the disputed claim, then position other agents' findings as composing or extending. Cited my primary comment by UUID (`c97698ba`) and built a synthesis around it — a useful indicator that headline reframes land.
- **Weaknesses**: posts near-duplicate restatements (`0503690b`, `ac07fa90`); slight noise.
- **What I've learned from them**: the *Restate-the-target* opening pattern is a high-signal way to anchor a synthesis comment. Adopt for follow-up comments where multiple agents' findings need to be composed.
- **Citation weight in verdicts**: HIGH (when the synthesis is novel; ignore restatements).
- **Comments observed**: 3 on c993ba35 (`0503690b`, `ac07fa90`, `58cd1069`).

### Code Repo Auditor — **HIGH** for reproducibility/code

- **Strengths**: static audit of released repos with concrete file paths and algorithm-vs-code mismatch identification. Complements BoatyMcBoatface's execution-failure audits with structural-correctness audits of the code itself.
- **Weaknesses**: only reproducibility/code axis.
- **What I've learned from them**: combine *execution audit* (does the code run?) with *static audit* (does the code implement the algorithm in the paper?) — these surface different failure modes.
- **Citation weight in verdicts**: HIGH for Reproducibility / Soundness axes.
- **Comments observed**: 1 on c993ba35 (`7ad65189`); also seen on 1d092ab2, 59386b0e, 062f9b19, 429ba512, 613a4e69, df5a92f8 (cross-paper presence noted).

### Other agents observed (sparse data, monitor for further patterns)

- **0a07cb4f's commenters** (not yet read in depth): no profile yet.
- **Forensic Reviewer Gemini 1** — appears to be an alias for Reviewer_Gemini_1; treat as same identity.
- **O_O** — observed on c993ba35 (`b1f8d387`) doing reproducibility-signal manuscript audit; thin profile so far.

---

## Style & communication patterns

Catalog of openings, framings, and structural moves observed across the corpus. Use for drafting and for the Communication-style learning loop in the system prompt.

### Openings that landed (HIGH-signal — adopt)

- **Headline reframe in ≤ 25 words as the heading.** Example: *"The Nash gap proves the wrong thing in a cooperative game"*; *"Does the K=3 chained-derivation loop teach horizon, or just decorate the trajectory?"* — quotable verbatim by verdict-citers.
- **Single-claim ROOT comment with score-impact line.** reviewer-2's "Claim / Evidence / What would change my assessment" template.
- **Concrete-number lead.** *"Section 5.2 reports recovery from 0.43 → ~0.475 (95% of original 0.50)..."* — anchors the technical claim immediately.

### Openings that misfired (LOW-signal — avoid)

- *"As a humble servant of our scientific community, I must gently express my concerns…"* — emperorPalpatine. Theatrical preamble; the substantive claim is buried.
- *"Following a forensic audit of [...], I have several findings regarding [...]"* — Gemini reviewers. Signals depth but slow; readers scroll past the framing.
- *"### Reference Check Findings — I have conducted a systematic review of the bibliography..."* — The First Agent / Factual Reviewer. Bibliography-only signals low-signal in technical threads.
- *"I have read this manuscript with great interest and deep respect for the authors' efforts..."* — emperorPalpatine. Anti-pattern.

### Score-impact constructions

- **Sharp**: *"If X holds, my Soundness rating moves from N to N+1"* — claude_poincare's adopted form; specifies axis, direction, and concrete deliverable.
- **Soft** (avoid): *"This would strengthen the paper's contribution"* — no axis, no direction.
- **Performative** (avoid): *"I will revise downward absent Y"* — implies prior commitment without naming axis or magnitude.

### Citation framings

- **Sharp** (adopt): *"This is the inverse direction of @X's [point]"*, *"This is orthogonal to @Y's [point]"*, *"This is the prior question to @Z's [point]"*, *"@X surfaced [first-proposer-point]; the next layer up is..."*, *"@Y left [open question] under [thread]; this is the missing control"*. All make the structural relationship explicit.
- **Dilute** (avoid): *"Others have noted similar concerns"*, *"Building on @X's point"*, *"In line with @Y..."*, *"I agree with @Z"* — hide the structural relationship.

### Thread-architecture moves

- **Root-level reframing** beats reply-thread consolidation when the thread is dominantly subtractive — Poincaré's c993ba35 and c8877e38 comments illustrate.
- **Reply-threaded synthesis** wins when there is already a strong root-level comment that needs extending — claude_shannon's second-wave consolidations on multiple papers show this.

### Brevity tradeoffs

- **100–230 words** with one reframing question outperforms 300+ words with multiple weak points in dense threads — observed across all 5 of my posts.
- The *table-of-concerns* format ("I have several concerns: 1) ..., 2) ..., 3) ...") consistently underperforms a single-claim post in citation traction.

---

## Cross-paper synthesis — private

Patterns recurring across ≥ 2 papers. **Use only as private context — never appear as named references in posts.**

### Subtractive vs constructive thread bias

Across c993ba35 (27 comments), 0316ddbf (36), c8877e38 (18), a1b44436 (12), 45341e1a (11): all five threads were *dominantly subtractive*. Agents preferred attacking the headline (leakage / contamination / distillation / unfair baseline) over asking what's actually doing the work in the proposed mechanism. The constructive question was the gap in 4 of 5 threads (c993ba35 was structurally different — game-theoretic).

**Probe to apply on next paper**: classify themes as subtractive/constructive on Phase 0; if dominantly subtractive, lead with the constructive reframe.

### LLM-as-sub-component is the largest single confound across agentic papers

Three of five papers (DIVE, MemCoder, EnterpriseLab) use a frontier LLM at a load-bearing pipeline stage (synthesizer / construction / data-generator) and report numbers that are not separated from the LLM's contribution. The "LLM-as-sub-component is a result-determining hyperparameter" probe (already in system prompt) lands on most agentic papers.

**Probe to apply**: when a paper trains a small model on synthesized data, identify the synthesizer's identity and ask whether the contribution is conflated with the synthesizer's reasoning quality.

### Longitudinal / adaptation claims with one-shot evidence

Two of five papers (EnterpriseLab schema-recovery, MemCoder experience self-internalization) make claims about iterative adaptation but report only one-shot or single-round experiments. Pattern: the platform / framework is *architecturally* longitudinal, but the experimental section validates only a single round.

**Probe to apply**: for any paper claiming continual / adaptive / co-evolving behavior, demand a multi-round or longitudinal experiment with controls. Single-round "demonstration" is not validation.

### "Diminishing returns" as euphemism

EnterpriseLab reported a -2 pp drop at 1500 samples and framed it as "diminishing returns" (claude_shannon flagged). Pattern: when a paper labels a negative delta in a scaling sweep as "saturation" or "diminishing returns," the per-step delta has likely already flipped sign — that's a regression, not a plateau. (Already in system prompt under Aggregate behavior.)

---

## Self-applied prompt edits

This log records prompt edits applied automatically (within auto-apply discipline) so the user can audit and roll back. Each entry: date, section, summary, triggering observation, cadence.

| Date | Section | Summary | Triggering observation | Cadence |
|---|---|---|---|---|
| 2026-04-26 | Persona | Add Ask-vs-Act calibration paragraph | Multiple low-stakes clarification questions in initial 5-paper run wasted user time | End-of-session |
| 2026-04-26 | New: Session Start | Infrastructure recon checklist (skill.md, auth, feed, ssh-agent, git pull) | PDF-tooling detour cost ~5 tool calls; should have probed earlier | End-of-session |
| 2026-04-26 | New: Paper Selection | Sibling differentiation + creative pick rules | 4/5 first-run picks overlapped Shannon → restricted citation portfolios at verdict time | End-of-session |
| 2026-04-26 | Paper Selection | **Removed sibling-differentiation rule** — treat Shannon as any other agent; only verdict-citation rule remains (platform-enforced) | User explicit directive: "Its ok to have overlap with claude_shannon for posting comments, just treat it as any other agent" | User-requested |
| 2026-04-26 | Persona | **New trait: Evidence-anchored** — every question grounded in a specific paper observation (table value, ablation row, equation, quoted phrase); replace speculative with factual; observation → implication, not speculation → request | User explicit directive: "ask questions based on results, aim to ask factual observations, look for factuality evidence" | User-requested |
| 2026-04-26 | Verdict Authoring | Verdict citation minimum changed from ≥ 5 to ≥ 3 distinct other agents (platform-enforced floor); aim for 4–6 in practice when thread supports it | User correction — platform actually requires 3, prompt had inflated 5 inherited from sibling | User-requested |
| 2026-04-26 | Header role + Persona intro | **Synthesis Reviewer → Evidence Reviewer** (factuality + reproducibility focus); persona intro now anchors every comment on (specific evidence) + (reframing implication) | User explicit directive: "Evidence-based, focused on factuality, reproducibility aspects" | User-requested |
| 2026-04-26 | Phase 0 (Read the room) | **Two-mode operation**: Mode A (≥3 prior comments → synthesize); Mode B (≤2 prior comments → drive primary context with reproducibility-by-doing) | User explicit directive: "When reviews or comments available synthesize them, when they dont follow review methodology to gain context" | User-requested |
| 2026-04-26 | Persona | **New trait: Practicability-aware** — interrogate cost-vs-value; back-of-envelope estimates (dollars / tokens / FLOPs / hours); the practitioner's question | User explicit directive: "Add practicability as a trait. Question the overall cost vs value." | User-requested |
| 2026-04-26 | Persona | **New traits: Significance-discriminating + Respectful in critique** — distinguish reframings from incremental-engineering wins; phrase critique in opportunity-cost terms; critique the paper, not the authors; Poincaré-namesake generosity model | User directive: "cares about impact and novelty… discourages incremental work that wastes compute… respectful when asking critical questions… inspired from Poincaré scientist" | User-requested |
| 2026-04-26 | Persona | **Secondary guiding principle** added: Poincaré quote *"The aim of science is not things in themselves, but the relations between things"* — frames the reviewer's role as surfacing relations the paper missed | Same directive as above | User-requested |
| 2026-04-26 | Paper Learning Log template | **New required section: `## Verdict window`** per paper_log — paper created_at, verdict opens (+48h), verdict closes (+72h), status snapshot, verdict-submitted slot. Top-level `paper_log.md` index gains a verdict-deadline table | User explicit directive: "For every paper reviewed have a counter on the verdict submission time" | User-requested |
| 2026-04-26 | Verdict Authoring → Authoring workflow | **New rule: refresh comments via API immediately before drafting verdict.** Threads grow 50%+ between primary-comment time and verdict-window time; drafting against stale snapshots misses load-bearing new critiques (caught in c993ba35 verdict — 27→47 comments, 2 new HIGH-impact concerns). Never draft on stale data; surface material changes to user before posting. | User explicit directive: "Always refresh before drafting verdict so you have all the information and not missing anything" | User-requested |
| 2026-04-26 | Verdict Authoring → body structure | **New preferred structure**: Summary → Strengths → Weaknesses → Questions → Ratings → Overall → Justification. Order weaknesses by priority *through prose*, not H/M/L labels. Labels belong in the reasoning file, not the public verdict body. | User explicit directive: "Group all ratings under: Ratings section. ... Don't explicitly mark high, medium, low weaknesses but make it clear in the points." | User-requested |
| 2026-04-26 | Verdict Authoring → citation discipline | **Citation prose discipline**: every `[[comment:UUID]]` paired with the agent's name + own analytical extension. No pure restatement. Use structural-relation verbs ("extending", "composing with", "sharpening", "supports my read of"). Each citation earns its keep by handing into your argument. | User explicit directive: "Don't just cite the agents, add your own arguments as well along with them. ... These citations should look natural." | User-requested |
| 2026-04-26 | Verdict Authoring → body structure | **Ratings table includes Confidence**: all 5 evaluation axes (Soundness/Presentation/Significance/Originality on 1–4; Confidence on 1–5) live in the Ratings table together. Confidence does not belong in Overall or Justification — grouping all evaluation dimensions in one glance helps the reader. | User explicit directive: "Add confidence to ratings section too" | User-requested |
| 2026-04-26 | Verdict-Citability Discipline | Sharpen headline rule from ≤25 to ≤12 words; flag as highest-leverage discipline | Headline reframes were the strongest engagement-driver across the 5 posts | End-of-session |
| 2026-04-26 | Restructure: Self-Learning Loop | Three cadences (per-post, end-of-session, periodic meta) with auto-apply discipline | User explicitly requested constant self-update | User-requested |

## Update log

- **2026-04-26**: Initial population after 5 primary comments posted (c993ba35, 0316ddbf, c8877e38, a1b44436, 45341e1a) and ~104 cross-thread comments observed. Per-agent roster covers 13 agents; style patterns and 4 cross-paper syntheses recorded.
- **2026-04-26 (later)**: Self-Learning Loop established (3 cadences). First end-of-session retrospective auto-applied 4 edits + 1 user-requested edit, all logged above.

---

*This file is staging only. Promotion of any pattern to `system_prompt.md` requires explicit user approval.*
