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

- **Over-drilling on granular mechanics when the source artifact already has them.** If the source artifact (performance review, self-evaluation, retrospective doc) has the metric, don't re-extract verbally. Pivot to substance that's only in the user's head.
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

## Incorporating external feedback (coach / mentor / recruiter review)

At some point someone credible — a career coach, a mentor, a friendly recruiter, a hiring-manager contact — gives the user a batch of feedback on an artifact ("your resume is too long," "add a keyword headline," "get more recommendations"). This feedback is valuable but it is **advice, not instructions**. The failure mode is applying it literally and mechanically, which produces an artifact that satisfies the note but damages the positioning.

The workflow that avoids that:

1. **Triage, don't execute.** Read the whole batch first. For each item, decide: agree / disagree / agree-with-a-modification. **Where you disagree, say why** — the user, not the assistant and not the coach, makes the final call, and they can only make it with the reasoning in front of them. A coach optimizing for generic recruiter-scannability may be wrong for a specific senior/niche target; a good triage names that tension instead of silently complying or silently ignoring.
2. **Make scope decisions *before* editing, and log them.** Convert each accepted item into a concrete scope decision with a number or a rule attached ("target ~750 words, not the suggested 650, because 650 forces cutting evidence-tested content"; "condense pre-current-role history to one line rather than deleting it, to avoid an apparent employment gap"). Log these in `DECISIONS.md` before touching the artifact. This is what stops a future session from re-litigating the coach's note from scratch.
3. **Separate the reusable method from the private specifics.** Feedback often mixes "here's a format that works" (reusable) with "say this about your background" (only the user can validate). Apply the first; route the second through the user.
4. **Execute against the logged decisions, not the raw note.** Now edit. The decisions are the spec; the coach's note was the input to the spec.

**Don't treat external feedback as authoritative just because it came from an expert.** Coaches see a high volume of generic candidates and optimize accordingly; the substrate exists precisely so the user's artifacts can be *specifically* strong rather than generically inoffensive. Weigh the note against the positioning, and disagree in writing when they conflict.

### Cut-list discipline (when trimming an artifact)

Trimming for length is not the same as rewording. When a pass **removes content entirely** (a word-count cut, a "make it one page," a "drop the old roles"), the risk is that a load-bearing claim disappears silently and nobody notices until an interviewer asks about the thing that's no longer there.

The discipline: **when content is cut completely — not just reworded — enumerate it for the user before finalizing.** List what's leaving (a concept, a metric, a named artifact, a whole role), and let the user confirm each. Rewording under a tighter budget is normal and doesn't need a cut-list; *complete removal* does. Two things reliably hide in a trim and are worth calling out explicitly:

- **A claim that only lived in the cut content.** If a strength's sole proof on the artifact was the bullet you just deleted, the claim is now unproven — flag it, don't assume it's covered elsewhere.
- **A silent factual softening.** Condensing "five named prior employers across three sectors" into one line can quietly introduce an inaccuracy (mislabeling a sector, implying a gap). Re-check the condensed line against the facts, not just against the word count.

The user reviews the cut-list and can restore any item. This is the same "surface the tradeoff, user decides" contract as per-bullet review — applied to subtraction instead of substitution.

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

### After an outcome (post-application feedback)

The most valuable signal in an active search is the outcome of the applications already submitted — and it's the one most often lost to chat history. Capture it.

When an outcome lands for an opening (rejection email, recruiter ghosting after a screen, advance to next round, offer), add a `post-mortem.md` to the per-opening directory.

**Shape:**

```markdown
---
type: post-mortem
opening: <company> / <role>
variant: <path to the resume / cover-letter variant submitted>
date_submitted: YYYY-MM-DD
outcome: rejected | ghosted | advanced | offer | withdrew
outcome_date: YYYY-MM-DD
outcome_stage: applied | recruiter | hm | loop | offer-stage
---

## What we shipped

<One paragraph: the variant's audit score, top-3 gaps the variant addressed, top-3 PASS items the variant leaned on.>

## What came back

<Whatever signal the outcome carries — verbatim feedback if provided, signal if only the outcome with no commentary, observed timing patterns. "Rejected with no feedback after 11 days" is itself a signal worth recording.>

## Hypotheses

<What the user thinks went right or wrong. Multiple competing hypotheses are fine; the point is to record the speculation when it's fresh, not to commit to a single causal story.>

## What (if anything) should change

- **Variant changes** (scoped to this opening — irrelevant once the opening closes): noted here for completeness; usually no action.
- **Canonical changes** (relevant beyond this opening): if the post-mortem surfaces a gap that holds across openings, this is a candidate for propagation back into the canonical. Log in `DECISIONS.md` with rationale before propagating.
- **Substrate changes** (deeper than artifact): if the post-mortem surfaces a strength claim that's not holding up, or a piece of evidence that turns out to read as weaker than expected, the fix is upstream — re-pressure-test the strength in `strengths.md` or revise the evidence file.
- **Tier 1 changes:** if the post-mortem surfaces that your stated lane / filter / comp posture isn't landing, revisit Tier 1 OPEN_QUESTIONS before the next batch of applications.
```

**Patterns across post-mortems.** After 3–5 outcomes, look across the post-mortem files for repeats. The same gap surfacing in three rejection post-mortems is a substrate-level signal — pull the change upstream rather than re-litigating it per variant. The same PASS holding up in three advance-to-next-round post-mortems is a strength worth foregrounding more in the canonical.

**Don't write post-mortems for non-events.** A rejection that was clearly mismatched (the opening was the wrong fit and the user knew it before applying) doesn't need a full post-mortem — a one-line note in the tracker is enough. Reserve post-mortem-grade reflection for outcomes where the gap (positive or negative) wasn't predictable from the audit.

**Update the tracker.** Whenever a post-mortem lands, update `applications/tracker.md` — move the row from Active to Decided with the outcome, link to the post-mortem file, capture the lesson in the tracker's `Reason` column (one phrase).

## Interview prep

The substrate's payoff at search time is interview prep — every prior workflow (substance mining, voice capture, audit, artifact generation, per-opening tailoring) sets up the moment when the user has an interview on the calendar and needs to be ready to talk.

This workflow runs against the substrate, not against the JD alone. The JD anchors which signals matter; the substrate provides what to say about them in the user's own framing.

### When to use

- An interview is scheduled (recruiter screen, hiring manager round, full loop, executive round).
- Two to five days out is the sweet spot — close enough that prep stays in working memory, far enough that gaps surfaced during prep can be brain-dumped before the conversation.
- Earlier than five days out is usually wasted prep (details fade); the night before is too late to do anything but read.

### The 3-day prep cycle

**Day -3 (or as far in advance as time allows): scope the loop.**

1. Re-read the JD against the variant submitted (or the canonical, if no variant was tailored).
2. Read the recruiter / role briefing materials if any (some recruiters share a loop schedule + interview-type breakdown — capture into the per-opening directory).
3. Re-read `identity.md` and `targets/role-criteria.md` — confirm the lane / scope / filter is still what you want to project in this loop.
4. List the interview types you know about (recruiter screen, hiring manager 1:1, technical depth round, behavioral round, cross-functional partner, exec round) and the likely topics for each.
5. Map each likely topic to the substrate file that holds the relevant material: behavioral → `stories/*.md`; technical depth → `evidence/*.md` + `history/*.md`; lane positioning → `identity.md` + `themes/*.md`; "tell me about yourself" → `voice/self-voice.md` + the latest opening-tailored variant's summary.

**Day -2: pressure-test the load-bearing answers.**

1. Pick the 3-5 stories most likely to come up given the loop. For each: re-read the `stories/<slug>.md` file, then say the answer out loud. Time it. The 2-minute version and the 5-minute version should both exist; if only the polished 2-minute exists, draft the 5-minute (or vice versa).
2. Verify each story's evidence references are still accurate. A story that cites an evidence file whose status is `outstanding` (missing detail) is a story that's missing its strongest beat — fill the gap or skip the story for this loop.
3. Identify the 2-3 hardest questions you expect — the ones that will probe a known weak spot (the Tier 2 behavioral gaps: "tell me about a time you failed / disagreed with leadership / managed someone out / didn't get something you wanted"). Draft answers to each. If the substrate doesn't have a story for one of them, schedule a brain-dump session today.
4. Re-read `themes/honest-growth-areas.md` (or the equivalent honest-bounded framing file). Interview answers that include the honest counter-narrative read more credibly than maximized claims; rehearse the "growing edge" framing the substrate captures.

**Day -1: rehearse + reset.**

1. Speak through each prepared answer once, out loud. Don't memorize; aim for fluent re-construction from the substrate's framing.
2. Confirm logistics — name / pronunciation of every interviewer if you have the list, the platform (Zoom / Google Meet / on-site), the time zone for remote.
3. Re-read `voice/self-voice.md` — the goal is to sound like yourself, not like a polished candidate. The voice file is the anchor.
4. Stop prepping the night before. Cramming new substance the night before degrades fluency.

### After the interview

Within 24 hours, capture:

1. **Which stories came up.** Log against the `stories/*.md` files — frequency of use is the signal for which stories are most valuable across loops.
2. **Which questions you fumbled.** Add to `OPEN_QUESTIONS.md` (Tier 2 if it was a behavioral gap; Tier 5 if it was a positioning gap) so the next prep cycle addresses them.
3. **Voice notes.** Anything you said that landed well — particularly phrasings that surprised you — into `voice/self-voice.md` with a one-line voice note about when to use it.
4. **A one-line update in `SESSION.md`** even if no other database work happened. The substrate gets richer through use, and post-interview is the highest-density signal moment in a search.

The 24-hour capture is the load-bearing step. Skipping it loses the highest-quality substrate update of the entire search.

### Common pitfalls

- **Memorizing answers verbatim.** Memorized answers fall apart when the interviewer reframes the question. Substrate-grounded reconstruction holds up.
- **Over-rehearsing the 2-minute version, never the 5-minute version.** Most behavioral prompts expand into 3-7 minute conversations with follow-ups. The 2-minute answer is the opener; the 5-minute version is the full story.
- **Skipping the day-1 reset.** The night-before cram is a stress habit, not a prep technique. Trust the substrate; sleep instead.
- **No post-interview capture.** The lesson lives for ~24 hours. After that the texture fades and the database doesn't compound.

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

1. **Read the source materials** for the period being audited — focus on the user's *own* framing of their work (in performance reviews, this is the self-review sections rather than manager-side).
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

## Positioning-pillar pressure-test (artifact vs. intended positioning)

This is a different audit from the consistency check above. The consistency check compares the *database* against its *source materials* (is the substrate faithful to what happened?). The positioning-pillar pressure-test compares a *finished artifact* against the *positioning the user is trying to project* (does this resume/profile actually land the blend of things the user wants to be known for?).

It catches a specific, common failure: an artifact that is individually true in every line but collectively lopsided — over-indexed on one or two dimensions and quietly silent on others the user considers core.

**When to use:**
- After a big revision to a resume or LinkedIn profile, before locking it.
- When the user articulates a target blend ("I want to read as X, Y, Z, and W").
- When an artifact "feels off" but the user can't name why.

**Method:**

1. **Get the pillars from the user, explicitly.** Ask (or confirm) the 4–6 dimensions they want the artifact to project — e.g. a blend of a domain, a leadership style, a technical claim, a strategic/visionary claim. These are the user's, not the assistant's to invent; pull from `identity.md` and `strengths.md` and confirm.
2. **Score the artifact pillar by pillar.** For each pillar: is it *strongly present*, *present-but-buried*, *asserted-but-unproven*, or *absent*? Cite the specific line(s) that carry it, or note the absence.
3. **Pay special attention to the summary/headline.** The top of an artifact is the part most readers actually read. A pillar that's well-proven in the body but missing from the summary is effectively invisible to a skim — flag "present-but-buried" as a real gap, not a pass.
4. **Distinguish a result-claim from a foresight-claim (and other altitude mismatches).** "Drove the strategy that became X" proves *execution*; "Bet on the strategy years before it became X" proves *foresight*. If a pillar is "visionary" but every supporting line is phrased as a result, the pillar is technically absent even though the underlying facts are present. The fix is often a re-framing of existing true content, not new content.
5. **Report, then fix cheaply.** Most gaps close with a clause, not a rewrite — a people-leadership pillar added to a summary that was all-technical, a foresight re-frame of a result bullet. Propose the minimal edits and let the user choose.

**Why it's worth a dedicated pass:** external feedback (a coach) optimizes for generic scannability and won't tell you your artifact under-projects "visionary." Only a check against the user's *own* stated pillars catches that. Run it as the last step before locking a high-stakes artifact.

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
