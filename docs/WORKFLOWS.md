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

## Artifact generation

When generating a resume, LinkedIn About, cover letter, or interview answer:

1. **Identify the audience.** What role / company / loop is this for?
2. **Pick the claim.** Pull 1–3 strengths from `strengths.md` that match.
3. **Find the proof.** Pull supporting `evidence/*.md` files. Cross-reference `voice/peer-quotes.md` for quotes that prove the claims.
4. **Pick the framing.** Each theme file has framing variants for different audiences — use the one that matches.
5. **Apply the voice.** Use `voice/self-voice.md` patterns. Avoid the corporate hero voice ("spearheaded", "transformational impact").
6. **Output to `artifacts/`.** Save the generated artifact in the relevant subfolder (`resumes/`, `linkedin/`, `cover-letters/`).
7. **Update `applications/tracker.md`** if this is for a specific application.

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
