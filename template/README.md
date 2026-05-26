# Career Database

> _Single source of truth for everything that could matter to your job search._

This directory is the foundation. Resumes, LinkedIn copy, cover letters, and interview prep are **generated from here**, not maintained alongside it. When you remember something, the rule is: it lives here first, then propagates outward.

## The narrative shape: Claim → Proof

The most important principle for using this database:

**Your story is about how you're effective — behaviors and skills — proven by examples. Not chronology proven by inference.**

| Layer | What it is | Role |
|---|---|---|
| `strengths.md` | 6 durable claims about how you operate | **The headline claims** |
| `themes/*.md` | Deep-dives on each claim with chronology + quotes + framing | **The claim expansion** |
| `evidence/*.md` | Specific quantified accomplishments | **The proof** |
| `stories/*.md` | STAR-format narratives that bind claims + proof | **The proof in narrative form** |
| `voice/peer-quotes.md` | Quotes from others corroborating the claims | **The third-party proof** |
| `voice/self-voice.md` | Your actual writing patterns | **The tone for any generated artifact** |
| `history/*.md` | Chronological role context | **Background, not headline** |
| `career-arc.md` | The through-line narrative across all roles | **The "why these choices" answer** |

### What this means for artifact generation

When generating a resume, LinkedIn About, cover letter, or interview answer:

1. **Start with the claim.** Pick a strength from `strengths.md` that matches the audience/role/prompt.
2. **Pull the proof.** Use evidence files + peer quotes to back the claim with specifics.
3. **Match the voice.** Use `voice/self-voice.md` patterns so the output sounds like *you* wrote it.
4. **Reference the deep-dive.** Themes files contain the framing variants for different prompts.

**Avoid:** opening with chronology ("I joined X in YYYY and...") or with a metric without a claim ("I scaled the team from 10 to 26..."). Chronology and metrics are the *proof layer*, not the *headline layer*.

**Do:** open with the claim, then prove with chronology + metric.

## Top-level map

### Operational files (read these first)

| Path | Purpose |
|---|---|
| `SESSION.md` | Where we left off + what to do next. Updated at end of every session. |
| `OPEN_QUESTIONS.md` | Consolidated, prioritized list of what needs your input. Scannable in 60 seconds. |
| `DECISIONS.md` | Append-only log of structural + positioning decisions with rationale. |
| `OPPORTUNITIES.md` | Future enhancements — what we could build, why it'd be valuable, what triggers the build. |
| `CLAUDE.md` | Instructions for Claude sessions working in this directory. |
| `KICKOFF_PROMPT.md` | Copy-paste session openers for re-engaging Claude. |

### Content files

| Path | Purpose |
|---|---|
| `strengths.md` | **THE CLAIMS** — 6 signature strengths (behaviors + skills). |
| `themes/` | Deep-dives on each strength with chronology + framing variants. |
| `evidence/` | **THE PROOF** — one file per quantified accomplishment. |
| `stories/` | **THE PROOF IN STORY FORM** — STAR-format behavioral narratives. |
| `voice/peer-quotes.md` | **THIRD-PARTY PROOF** — curated peer/manager quotes organized by what they prove. |
| `voice/self-voice.md` | Your actual writing voice — for tone-matching generated artifacts. |
| `identity.md` | Lane positioning + elevator pitches. |
| `career-arc.md` | The through-line narrative across all roles. |
| `skills.md` | Skill inventory with proficiency + recency. |
| `education.md` | Degrees, certs, training. |
| `patents-publications.md` | Patents, talks, OSS, public writing. |
| `references.md` | Who would vouch for what. |
| `comp.md` | **Private.** Comp history, target, negotiation notes. |
| `history/` | One file per role + a master timeline. |
| `targets/` | Role criteria, target companies, recruiter personas. |
| `applications/` | Application tracker + per-application notes. |
| `artifacts/` | Generated outputs (resumes/, linkedin/, cover-letters/). |
| `sources/` | Inventory of raw source material + drop-zone for new sources. |

## Conventions

### Frontmatter

**History files** (`history/{role}.md`):
```yaml
---
company:
title:           # title at end of tenure
dates:           # YYYY-MM to YYYY-MM, or "Current"
location:
manager:
team_size_managed:
reports_to_level:
---
```

**Evidence files** (`evidence/{slug}.md`):
```yaml
---
role: [your-role-key]             # which role this happened in
date_range:
metric:                           # the headline number/claim
status: outstanding | active | retired
confidence: confirmed | approximate | claimed
---
```

**Story files** (`stories/{slug}.md`):
```yaml
---
themes: [leadership, resilience, conflict, ...]
role:
duration: ~2min | ~5min
primary_evidence: [[evidence/...]]
---
```

### Linking

Cross-link with `[[path-without-extension]]`:
- From a history file → its evidence: `[[evidence/product-launch]]`
- From an evidence file → the story it powers: `[[stories/product-launch]]`
- From a story → the evidence backing the "Result": `[[evidence/...]]`

The `[[...]]` syntax isn't auto-resolved by anything — it's a human/AI navigation aid and a grep target.

### Status legend

For **evidence** files:
- `outstanding` — known but missing detail; needs interview/recall to fill
- `active` — fully documented; safe to use in any artifact
- `retired` — accurate but no longer being foregrounded

For **applications**: see `applications/tracker.md`.

For **target companies**: see `targets/companies.md`.

### "Open recall" sections (per-file)

Every file ends with `## Open recall`. This is where you dump half-formed thoughts, things you want to remember to add later, questions you have for yourself, *in the context of that specific file*.

**Cross-cutting questions** — the ones that block interview readiness or block artifact generation — get promoted to the top-level `OPEN_QUESTIONS.md`. When in doubt, add to OPEN_QUESTIONS.md *and* leave a marker in the per-file Open recall.

### Provenance — note where facts come from

When making a claim, indicate the source — it matters for interview defensibility:

- **Confirmed:** documented in an archive / offer letter / employment verification — cite the source
- **Claimed:** from your memory or from inference across sources — flag it
- **Approximate:** directionally correct but the exact number isn't verified — flag it

The frontmatter `confidence:` field on evidence files handles this for the headline metric. For other claims, inline a note: `(source: 2022 H2 performance review by [manager])` or `(claimed — verify before interview use)`.

### As-of dating for time-sensitive claims

Comp numbers, team size, ratings, sentiment scores, and any "current" framing — all time-sensitive. Date them.

- **Bad:** "Direct-report sentiment 95%."
- **Good:** "Direct-report sentiment 95% (H2 2024)."

When in doubt, a `(as of YYYY-MM)` parenthetical is fine.

### Session start + end ritual

**At the start of a working session:**
1. Read `SESSION.md` for where we left off.
2. Skim `OPEN_QUESTIONS.md` for the highest-priority open items.
3. Pick a target for the session.

**At the end of a working session:**
1. Update `SESSION.md` with what we did + what's next.
2. Move any answered items in `OPEN_QUESTIONS.md` to the "Answered" section with date + answer.
3. Add any new open questions discovered.
4. Log any structural / positioning decisions in `DECISIONS.md`.

## What this directory is NOT

- A resume. Resumes are downstream artifacts that live in `artifacts/resumes/`.
- A polished portfolio. The point is durable raw material; polish happens at the artifact layer.
- Public. Treat as private working notes. Anything that leaves (LinkedIn, sent resume, recruiter outreach) is a deliberate copy through `artifacts/`.
