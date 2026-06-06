# Workflows

> _The recurring patterns of work against this database. Most sessions are a variant of one of these._

## Source mining

When new raw material arrives (a current resume, a performance review archive, a LinkedIn export, saved kudos, an exit interview transcript):

1. **Drop the file in `sources/inputs/`.**
2. **Add a row to `sources/inventory.md`** with: path, date, type, one-line description, `[ ]` unmined status.
3. **Mine the file against the right layers:**
   - Facts (titles, dates, scope) → `history/*.md` + `history/00-timeline.md`
   - Quantified outcomes → `evidence/*.md` (one file per accomplishment)
   - Behavioral narratives → `stories/*.md` (one file per STAR-format story)
   - Third-party quotes → `voice/peer-quotes.md`
   - Writing patterns from the user's own self-reviews → `voice/self-voice.md`
   - Cross-cutting blockers surfaced → `OPEN_QUESTIONS.md`
   - Structural decisions made → `DECISIONS.md`
4. **Update the inventory row to `[x]`** with a one-line summary of what was extracted.

**A `[x]` row doesn't mean "no more value here"** — it means "first pass done." Re-mining as the structure evolves is expected.

## Interview / brain-dump (substance extraction from the user)

When the user wants to brain-dump a specific era, project, or arc — and you (the AI) are scribe + interviewer.

This is a distinct mode from source mining (where the raw input is a document) and from artifact generation (where you're producing output). Here the raw input is **the user's voice in real time** and your job is to extract substance into the right layers without distorting it.

**Setup:**

1. Confirm what's being brain-dumped (an era, a project, a strength, a relationship arc).
2. Tell the user explicitly: you'll ask, they talk; you capture in real time and flush at natural breakpoints; you'll summarize back every ~15–20 minutes (or 6–8 substantive turns) so they can correct distortions before they get baked in.
3. Set ground rule for the user: don't self-edit. Tangents, false starts, "wait I'm wrong about that" — those are the texture you want. The polished version probably already exists; what's missing is the messy authentic version.

**While interviewing:**

- **One open question at a time.** Not a bullet-list of 5 sub-questions. The user responds to the open question; sub-questions fragment the beat and over-direct.
- **Push for specifics.** Names, dates, rooms, exchanges, exact phrases. Abstractions ("we improved cross-team alignment") lose evidentiary weight. Specifics ("the director convened the three of us in her office on a Thursday in March") hold up under interview scrutiny.
- **Ask about what they *didn't* do** as much as what they did. Counterfactuals surface tradeoffs.
- **Distinguish observed vs. told.** "I saw this directly" vs. "X told me this happened" matters for provenance.
- **Capture phrasing verbatim** when something is uniquely the user's — goes straight to `voice/self-voice.md` as raw quote with a one-line voice note explaining how to deploy it.
- **Watch for steering signals.** "In the weeds," "splitting hairs," "orthogonal," "doesn't really matter" — when you hear these, the user is telling you to pivot to a different thread, not drill deeper. Acknowledge briefly and move on.
- **Don't force narrative shapes.** Cinematic moments, single epiphanies, clean before/afters are often the polished version. The truth is often accumulation. If the user says "it wasn't a single aha," believe them and shift to the curve, not the point.

**Periodic summary-backs (every ~15–20 min):**

A short, structured mirror: "Here's what I caught in the last few turns — [3–5 bullets]. Banking [factual gaps] for cleanup. Where do you want to take it next?"

Three purposes:
1. Confirms your capture before you flush to files (corrections are cheap to make in real time, expensive to make later).
2. Gives the user a natural breath.
3. Surfaces factual corrections — the user often realizes "wait, I said X but actually Y" during the summary-back.

**End-of-session flush:**

When the user calls a breakpoint (or you reach a natural one), flush everything to the right files in one disciplined batch:
- New `evidence/` files for net-new accomplishments
- New `stories/` files for net-new narrative arcs
- Updates to existing `evidence/` / `themes/` files where the brain-dump added detail
- A new "Verbatim from the [topic] brain-dump (YYYY-MM-DD)" section in `voice/self-voice.md` with the captured quotes + voice notes
- Updates to `references.md` for any new people named
- New banked items in `OPEN_QUESTIONS.md` for factual gaps surfaced
- A `DECISIONS.md` entry summarizing major substance + corrections logged

Then update `SESSION.md` so the next session picks up cleanly.

**Behavior guidance that should persist across sessions** (e.g., "this user prefers single open questions over bullet probes") belongs in the cross-session memory layer (e.g., Claude Code's `.claude/projects/*/memory/`), not in the database itself. The database is content; behavioral preferences are how-to-work-with-the-user.

**Common failure modes:**

- **Over-drilling on granular mechanics when the source artifact already has them.** If the PSC / review / doc has the metric, don't re-extract verbally. Pivot to substance that's only in the user's head.
- **Bullet-list probes that fragment one beat.** Pick the single highest-value question.
- **Inferring narrative from factual corrections.** When the user corrects a fact (level, title, date), don't bake in narrative implications they didn't authorize. Stick to facts; let the user author narrative.
- **Forced cinematic framing.** Not every conversion is a single moment. Honor the user's framing when they say it was accumulation.

## Artifact generation

When generating a resume, LinkedIn About, cover letter, or interview answer:

1. **Identify the audience.** What role / company / loop is this for?
2. **Pick the claim.** Pull 1–3 strengths from `strengths.md` that match.
3. **Find the proof.** Pull supporting `evidence/*.md` files. Cross-reference `voice/peer-quotes.md` for quotes that prove the claims.
4. **Pick the framing.** Each theme file has framing variants for different audiences — use the one that matches.
5. **Apply the voice.** Use `voice/self-voice.md` patterns. Avoid the corporate hero voice ("spearheaded", "transformational impact").
6. **Output to `artifacts/`.** Save the generated artifact in the relevant subfolder (`resumes/`, `linkedin/`, `cover-letters/`).
7. **Update `applications/tracker.md`** if this is for a specific application.

## Per-opening tailoring

When a specific job opening surfaces and the user wants to tailor an artifact (resume, cover letter, sometimes LinkedIn outreach) to that opening rather than ship the canonical version.

This is structurally a follow-on to **Artifact generation**, not a replacement. The canonical artifact (the locked resume at `artifacts/resumes/`, the locked LinkedIn at `artifacts/linkedin/`) remains untouched. The per-opening variant is a sibling deliverable scoped to one company + one role.

**When to use this workflow:**

- A specific JD has surfaced and the user wants to apply.
- The canonical resume scores against a generalized target (e.g., "AI labs at senior level") but the user wants a sharper variant for one named opening.
- The opening's screening signal has known gaps relative to the canonical — and addressing them in the canonical would weaken the artifact's fit for other openings.

**When NOT to use this workflow:**

- The canonical artifact is genuinely the right shape for the opening — no tailoring needed.
- The user hasn't yet identified a specific opening — premature variant work locks positioning before the target is known.
- Tier 1 OPEN_QUESTIONS are unresolved — the canonical artifact should stabilize first.

### The five phases

#### Phase 1 — Read the JD against the canonical

1. Read the target JD carefully. Identify the load-bearing signals — the phrases the JD itself repeats, the responsibilities listed first, the requirements that map to specific candidate evidence.
2. Read the current canonical artifact (`artifacts/resumes/<locked-version>.md`).
3. Pull supporting evidence + voice files for the strengths the JD's signals point to.

#### Phase 2 — Audit (canonical vs. opening)

Score the canonical artifact against the opening's signals. The audit produces a list of where the canonical lands well and where it has gaps.

A reusable audit shape: 8–12 yes/no checks derived from the JD's own language (each check must cite a specific JD passage), with each check evaluated against the canonical artifact. Tag each as PASS, PARTIAL, or FAIL — concrete evidence cited from the canonical for PASS, specific absence noted for FAIL.

The audit's outputs are:

- A score (e.g., `7 PASS / 5 PARTIAL / 0 FAIL`).
- A ranked list of the top 3–5 cross-check gaps (PARTIAL or FAIL items that appear most load-bearing for this specific opening).
- The PASS list — what's already strong and should remain untouched.

**Save the audit** at `applications/<company>-<role-slug>/audit.md` if the artifact directory exists, or alongside the variant once it's drafted. The audit is a deliverable in its own right — it doubles as interview prep substrate ("the gaps the recruiter would flag").

#### Phase 3 — Draft the variant

For each top-priority gap from Phase 2, draft a specific edit to address it. Constraints:

- **Anchor every edit to evidence already in the database.** If the gap can only be addressed by a claim the substrate doesn't support, do not draft the edit — flag it as a candidate question and surface it for the user to either resolve (via brain-dump or recall) or hold.
- **Honor the canonical's load-bearing claims.** Variant edits should not strip claims the canonical relies on; they should augment, swap, or extend specific bullets.
- **Maintain voice.** Voice-file phrasings authorized for verbatim use in the variant's artifact type get used verbatim. Don't paraphrase pre-vetted phrasings.
- **Respect length constraints.** If the variant adds top-of-document weight (a new Highlight, an expanded summary clause), look for a corresponding cut first — typically a claim whose proof also lives at body altitude, where cutting from skim altitude doesn't lose the claim.

Save the variant at `applications/<company>-<role-slug>/resume.md` (or `cover-letter.md`, etc., for non-resume variants).

#### Phase 4 — Per-bullet review with the user

Walk the user through each variant edit one at a time:

- Present the original (from canonical) and the proposed (from variant) in a clear before/after.
- State the tradeoff in one or two sentences — what changes, why, what it costs.
- Offer 3–4 numbered options including at least one "keep canonical" and one "apply variant as drafted."
- The user replies with a number; the edit applies; move to the next change.

The user retains every edit-level decision. The assistant's role is to surface the tradeoff, not to advocate for or against.

End the review with a summary table of decisions and a procedural checklist for close-out (frontmatter cleanup, decision log, deliverable port, tracker update).

#### Phase 5 — Ship the deliverable

Once the variant content is locked:

1. **Render to the deliverable format** — designed PDF, HTML, docx, whatever the application portal accepts. Treat the markdown as the source of truth and the rendered format as the presentation layer; sync the two manually if both will be maintained going forward.
2. **Log the decision in `DECISIONS.md`** — what changed from canonical, why, and the per-bullet review decisions. Future sessions need this to avoid re-litigating.
3. **Update `applications/tracker.md`** — last touch, current status (`prepping` → `applied` once submitted), next step.
4. **Update `SESSION.md`** — what shipped this session, what to do next.

The deliverable is a per-opening artifact pair — typically a resume plus a cover letter, both rendered to the format the portal wants. They are submission-ready together.

### Variant frontmatter

Variant artifacts must declare what makes them a variant — what they diverge from, on what dimensions, and what scope of propagation is and is not authorized. See the variant frontmatter schema in `CONVENTIONS.md`.

The discipline matters because cross-opening drift is a real failure mode: a variant edit that's sharper for Company A may be wrong for Company B, and propagating variant changes to the canonical without intent can quietly damage the canonical's fit across the rest of the search. The `do_not_propagate` field on a variant is the guardrail.

### Common pitfalls

- **Drafting the variant before reading the JD twice.** The JD's load-bearing signals are subtle — what's repeated, what's named first, what the "background" section emphasizes vs. what the "responsibilities" section emphasizes. A single pass misses them.
- **Building a variant against a thin JD.** If the JD is a one-paragraph stub, the variant has nothing concrete to tune against. Either skip the variant work and ship the canonical, or supplement the JD with company-bar signals (recent blog posts, careers-page values content, public statements from leadership).
- **Propagating variant changes back into the canonical without decision-log review.** The canonical is the artifact tuned for the user's generalized search; variant edits are scoped to one opening. Promotions from variant to canonical should be deliberate, not silent.
- **Skipping the audit phase and going straight to drafting.** Without the audit, the variant addresses gaps the user assumes exist rather than gaps the JD actually screens for. The score also doubles as a checkpoint — a variant score of `9 PASS / 3 PARTIAL` may not justify the variant work; ship the canonical and pour the time elsewhere.
- **Forgetting to update the canonical's `do_not_propagate` flags after variant work.** When a variant change turns out to be the right call for the canonical too, update the canonical and remove the per-variant restriction — otherwise the same edit gets re-drafted on every future variant.

## Session start ritual

Every session starts with the same 4 reads:

1. `SESSION.md` — where we left off + what to do next
2. `OPEN_QUESTIONS.md` — top of the prioritized list
3. `README.md` — the conventions (especially if it's been a while)
4. `CLAUDE.md` — hygiene rules
5. Then read the specific files relevant to the current task

Cost: 5–10 minutes. Saves: hours of cold-start re-derivation.

## Session end ritual

Every session ends with the same 4 writes:

1. **Update `SESSION.md`** — date, what we did, where we stand, what to do next.
2. **Move resolved items in `OPEN_QUESTIONS.md`** to the "Answered" section with date + answer.
3. **Add new open questions** surfaced this session.
4. **Log structural / positioning decisions in `DECISIONS.md`** with rationale.
5. **Add "we could build X" notes to `OPPORTUNITIES.md`** (what / why-valuable / trigger).

If you skip the end ritual, the next session starts cold and you re-do work.

## Tier 1–5 prioritization

When the question is "what should I work on next?" — the answer is almost always "the highest tier with open items":

### Tier 1 — Interview-blocking

The questions every recruiter and hiring manager asks. Without crisp answers, the interview phase stalls.

- Why are you leaving / why did you leave your last role?
- Why now? What are you looking for next?
- If you've been at a level for a while: why didn't you advance?
- Comp expectations
- Geography / remote / hybrid filter

**Until Tier 1 is done, don't generate outward-facing artifacts** — the answers shape every artifact, so generating early bakes in undefined positioning.

### Tier 2 — Behavioral interview gaps

Senior loops run 4–6 behavioral interviews. Most candidates have rich material for *leadership / resilience / strategic thinking* and thin material for the standard hard prompts:

- A time you failed
- A time you disagreed with leadership
- A time you managed someone out
- A hiring mistake / bad hire
- A time you didn't get something you wanted
- A bet you championed that *didn't* pay off

Open Recall in `stories/` is for these. Each one is a story slot to fill.

### Tier 3 — Network activation

- Pre-warm 3–5 references — short message, "I'm starting to look — would you take a call?"
- Capture contact info for everyone in `references.md`
- Tier each reference (1 = ask anytime, 2 = ask with warning, 3 = written check OK)
- LinkedIn profile capture + refresh
- Target company list (10–15 named, with status / why / who-you-know)

### Tier 4 — Factual gaps in the database

Names, dates, exact numbers — nice-to-have, interview-relevant, fillable from existing artifacts (LinkedIn, performance reviews, calendar, saved emails).

### Tier 5 — Strategic positioning

- POV / thesis 1-pager (senior loops ask "what's your view on the future of X")
- Identity refinement (does the current claim still feel right?)
- 30-second + 2-minute elevator pitches
- Pressure-test the 6 strengths (are these *the* 6?)

## Audit / consistency check

Periodically — every few months, or when the database has had a lot of churn — compare the database against the authoritative source materials to surface drift, gaps, or framing inconsistencies.

**When to do this:**
- After a major brain-dump session that added a lot of substance
- Before drafting a high-stakes artifact (resume v-next, LinkedIn About refresh, POV 1-pager)
- After picking up the database after a long break
- When the user suspects framing has drifted from how they actually describe their work

**Inputs:**
- The authoritative source materials (typically performance reviews, but could be saved emails, internal posts, project retros, public talks — anything in `sources/inputs/`)
- The current state of the database (all of `evidence/`, `themes/`, `stories/`, `identity.md`, `strengths.md`)

**Method:**

1. **Read the source materials** for the period being audited — focus on the user's *own* framing of their work (in PSCs, this is the self-review sections rather than manager-side).
2. **Extract for each source:**
   - The focal points the user chose to highlight
   - The strengths they claimed for themselves
   - The growth areas they named
   - Any new initiatives / programs / decisions / people named for the first time
3. **Cross-reference against the database:**
   - Is each focal point captured? Where?
   - Is the framing consistent with how the user framed it in the source?
   - Are people named in the source but missing from `references.md`?
   - Are metrics in the source not appearing in `evidence/`?
   - Are there decisions named in the source that contradict the database?
4. **Generate a report file** at `audit_YYYY-MM-DD.md` organized as:
   - **(A) Missing or under-captured** — what the source has that the database doesn't
   - **(B) Framing inconsistencies** — where the user's own self-framing differs from the database's framing
   - **(C) Clarifications needed** — questions to ask the user
   - **(D) Significant period gaps** — periods of work not covered by any source
   - **(E) What's right** — consistencies worth flagging as well (not just gaps)
   - **(F) Prioritized recommendations** — what to action first, second, etc.

**Critical rule: report-only. Do not action findings.**

The audit is a deliverable the user reviews. The user decides what to action, in what order, and whether some findings reflect intentional choices rather than gaps. Auto-actioning audit findings is how the database gets corrupted by AI-inferred narrative shapes the user didn't authorize.

**What to look for specifically:**

- Programs / initiatives named in the source but not in `evidence/`
- Strengths or growth areas that recur across multiple cycles (durable self-framing)
- Decisions the user named that reverse or modify earlier decisions ("we federated in 2023, then unfederated in 2025")
- People mentioned but not in `references.md`
- Metrics that don't appear in `evidence/`
- Significant uncaptured periods (e.g., post-last-review time before a layoff or transition)
- Sentence-level ambiguities in source text that may have been misread in prior mining sessions

**What NOT to do:**

- Don't critique the user's self-assessment — the audit is database-vs-source, not user-vs-database.
- Don't merge findings into existing files without the user's approval.
- Don't include manager-side sections of reviews unless explicitly asked — the user's self-framing is the primary lens for an audit.

## Bootstrapping flow (first 1–2 sessions)

1. **Session 1: Tier 1 + source mining**
   - Walk through Tier 1 questions; capture answers in `identity.md`, `targets/role-criteria.md`, `comp.md`
   - Mine whatever sources exist (current resume, latest performance review, LinkedIn)
2. **Session 2+: Substance-layer brain-dump**
   - Era-by-era walk through the user's career; capture evidence + stories + voice as they talk
   - Strengths emerge from the substance, not the other way around
3. **Session N: Pressure-test + artifact**
   - Once substrate is rich, pressure-test the 6 strengths
   - Then generate the first artifact (resume or LinkedIn About) as a dry run

## Common workflow mistakes

- **Generating artifacts before Tier 1 is done.** Locks in undefined positioning.
- **Filling strengths.md from the top down.** Strengths should emerge from substance. Empty top-down strengths read as generic.
- **Skipping the session end ritual.** Next session starts cold and you waste time re-deriving.
- **Burying cross-cutting questions in per-file Open Recall.** They never resurface. Promote to `OPEN_QUESTIONS.md`.
- **Re-litigating decisions.** If it's in `DECISIONS.md`, read that first before reopening the question.
- **Forgetting to date time-sensitive claims.** "Direct-report sentiment 95%" without a date is unverifiable; "Direct-report sentiment 95% (H2 2024)" is.
