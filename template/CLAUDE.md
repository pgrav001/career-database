# Instructions for Claude — Career Database

If you're a Claude session working in this directory or helping with anything resume / LinkedIn / cover-letter / job-search related, read this first.

## Read order at session start

1. **`SESSION.md`** — where we left off, what to do next.
2. **`README.md`** — conventions + the Claim → Proof model that organizes everything.
3. **`OPEN_QUESTIONS.md`** — what's blocking us right now.
4. **The specific files relevant to the task at hand.**

## Two postures: active search vs. dormant

This database runs in one of two modes. Read the mode off `applications/tracker.md` rather than keeping a separate setting.

- **Active-search mode** — the tracker's § Active applications has at least one row. Everything in this file applies as written: Tier 1 urgency is real, and interview prep is the priority.
- **Dormant / experience-management mode** — § Active is empty and the tracker shows its dormant banner. The user has a job, and the database's purpose shifts from winning the next role to keeping the record of the current one. In this mode:
  - **Don't route to `OPEN_QUESTIONS.md` Tier 1 or interview-prep work by default.** Nothing is live to prep for.
  - **Treat any work anecdote the user mentions, in any session and for any reason, as capturable.** Offer to file it as `evidence/{company}-{slug}.md` through the normal evidence workflow. Capture happens whenever the user shows up; it doesn't need a dedicated session.
  - **Don't generate job-search busywork** (watchlist triage, "anything to apply to?") unless the user raises it.

Both postures live in this one file. When a search starts again, the first tracker row flips the mode back.

## The narrative spine

The user's story is about **how they're effective (behaviors + skills)**, **proven by examples** — not chronology proven by inference. When generating any artifact:

1. **Lead with the claim** (pick from `strengths.md`).
2. **Prove with the example** (pull from `evidence/`).
3. **Match the voice** (use patterns from `voice/self-voice.md`; run the anti-AI-tell rules in `voice/writing-rules.md` — the two compose, and self-voice wins on the user's genuine markers).
4. **Reference framing variants** (themes files have framing-per-audience).
5. **Run the review pass before finalizing** — the three-pass check in `voice/writing-rules.md` (draft → adversarial rule-by-rule review → rewrite). Required for every outward artifact: resumes + variants, cover letters, LinkedIn, essays, and free-text application fields. Log the edits in the artifact's `writing_rules_applied` frontmatter.

Avoid corporate hero voice ("spearheaded," "transformational impact," "passionate about"). Use specific over abstract. Honest about constraints. Lessons + reflection at the end.

## Hygiene rules

- **When a new question / unknown comes up, ADD it to `OPEN_QUESTIONS.md`.** Don't bury it in a file's `## Open recall` and assume future-you will find it. The recall sections are fine for context-specific half-thoughts; OPEN_QUESTIONS is for the cross-cutting list.
- **When making a structural / positioning decision, LOG it in `DECISIONS.md`.** Include rationale. Future sessions need this to avoid re-litigating.
- **When you mention "we could build X" or "we're not building Y yet," LOG it in `OPPORTUNITIES.md`.** Don't leave it only in chat. What/Why-valuable/Trigger.
- **When a new job opportunity surfaces that isn't being fully pursued yet, LOG it in `applications/watchlist.md`** — the funnel, *not* `tracker.md`. (Distinct from `OPPORTUNITIES.md` above, which is for database/product build-ideas.) The tracker is committed applications only; the heavyweight machine (hiring-manager profile → binary evals → tailored resume variant → cover letter) runs **only** on promotion from the watchlist, per the watchlist's promote rule.
- **When making a time-sensitive claim, date it.** "As of YYYY-MM" on sentiment scores, comp, team size, etc.
- **When citing a fact, note its provenance.** Especially when the difference between "confirmed by archive" and "user told me YYYY-MM-DD" matters.
- **At the end of a working session, update `SESSION.md`.** Date, what we did, where things stand, what to do next. When it passes ~500 lines, fold older entries into `sessions-archive/{year}.md`. The trigger is size, not a schedule.
- **Before rewriting a claim in any artifact, check `DECISIONS.md` and the relevant `evidence/` file for a prior ruling on it.** Corrected claims come back, because each new draft is written from the last draft's prose rather than from the evidence. See `docs/WORKFLOWS.md` § Claim integrity.
- **When the user cuts a phrase from one artifact, sweep it from all of them.** Grep the phrase across `artifacts/`, `applications/`, and live profile copy, and report where else it lives. The reason the user gave is rarely the only reason it should go.
- **When an outcome comes in, record the known part as fact and label the inferred part as inference.** If the user reports an outcome without a reason, write "reason not captured" rather than the most plausible cause.

## Don'ts

- **Don't invent names or facts.** When something is unknown, leave it as a placeholder and add it to `OPEN_QUESTIONS.md`.
- **Don't put full comp numbers in any generated artifact** unless explicitly asked. `comp.md` is sensitive.
- **Don't generate finished artifacts (resumes, LinkedIn copy) without checking `OPEN_QUESTIONS` Tier 1 first.** Several interview-blocking questions need the user's input before polished artifacts are useful.
- **Don't lead with chronology in artifacts.** Lead with the claim; chronology is the proof layer.
- **Don't restructure the user's own short draft into bullets.** On a note to a person under ~300 words (a recruiter email, a free-text application field), treat their prose as the base text and edit surgically.

## User-specific notes

_(Add user-specific cautions, sensitive areas, or special handling here as they come up. Examples: "Don't reference X publicly." "Y is the embargoed product name — internal use only until the launch date." "Z is the working draft identity claim until refined.")_
