---
name: career-database
description: "Bootstrap or maintain a Claim→Proof career database. Use when the user wants to organize career evidence for a job search, build interview-prep substrate, or generate resumes / LinkedIn / cover letters from a durable foundation. The skill produces a markdown directory the user owns end-to-end; artifacts are downstream of the substrate, not stored alongside."
---

# career-database

You are working with a **Claim → Proof** career database. The user's job-search story is about *how they're effective* (behaviors + skills) **proven by examples** — not chronology proven by inference.

## Step 1 — Determine state

Ask the user where their career database lives (default: `~/career/`).

- **If the directory doesn't exist:** offer to bootstrap from the `template/` directory in this skill. Walk them through the first session (see Step 3).
- **If it exists:** read in this order:
  1. `SESSION.md` — where we left off + what to do next
  2. `OPEN_QUESTIONS.md` — what's blocking interview readiness or artifact generation
  3. `README.md` — the Claim → Proof model and conventions
  4. `CLAUDE.md` — explicit hygiene rules for this database
  5. Files relevant to the current task

## Step 2 — Apply the Claim → Proof model

Every artifact you help generate (resume bullet, LinkedIn copy, cover letter line, interview answer) follows this shape:

1. **Lead with the claim.** Pick a strength from `strengths.md` that matches the audience / role / prompt.
2. **Prove with the example.** Pull from `evidence/*.md` (specific quantified accomplishments) and `stories/*.md` (STAR narratives).
3. **Match the voice.** Use patterns from `voice/self-voice.md` so the output sounds like the user wrote it.
4. **Reference theme framing.** Themes files (`themes/*.md`) contain framing variants for different audiences.

**Avoid:** opening with chronology ("I joined X in 2020...") or with a metric without a claim ("I scaled the team from 10 to 26..."). Chronology and metrics are the *proof layer*, not the *headline layer*.

**Do:** open with the claim ("I'm the operator who keeps teams functional through crisis"), then prove with chronology + metric ("most recently my team tripled during the worst of the layoffs while sustaining top-decile direct-report sentiment, while peer orgs contracted").

## Step 3 — First-session bootstrap

If bootstrapping a new database:

1. Copy `template/` contents to the user's chosen directory.
2. Walk the user through `BOOTSTRAPPING.md` priorities:
   - **Tier 1: interview-blocking questions** — answer these *before* generating any outward-facing artifact:
     - Why are you leaving / why did you leave your last role?
     - Why now? What are you looking for?
     - If you've been at a level for a while: why didn't you advance?
     - Comp expectations
     - Geography / remote / hybrid filter
   - **Source mining** — process whatever raw materials exist (current resume, performance review archive, LinkedIn export, saved kudos, etc.). Drop them in `sources/inputs/`, add to `sources/inventory.md`, mine into the right layers.
   - **Substance-layer brain-dump** — era-by-era walk through the user's career; capture evidence + stories + voice patterns as the user talks.

## Step 4 — Apply hygiene rules

Every session, regardless of task:

- **Provenance:** when capturing a claim, flag the source: `confirmed` (documented), `approximate` (directionally correct), or `claimed` (memory only, verify before interview use).
- **As-of dating:** time-sensitive claims (sentiment scores, comp, team size, ratings) get a date — `(as of YYYY-MM)` parenthetical.
- **Open Recall promotion:** half-thoughts go in the per-file `## Open recall` section; cross-cutting blockers go in top-level `OPEN_QUESTIONS.md`.
- **Date conversion:** convert relative dates ("Thursday", "last week") to absolute dates (ISO `YYYY-MM-DD`) before writing them down.
- **Don't invent.** When something is unknown, leave a placeholder and add it to `OPEN_QUESTIONS.md` — don't fill the gap with plausible-sounding fiction.

## Step 4.5 — Cross-session memory (complement to the database)

The database is **content** — facts, claims, evidence, voice, history. It belongs in the user's working directory and they own it.

Some things should persist across sessions but don't belong in the database:

- **Behavioral preferences** ("this user wants single open questions, not bullet-list probes")
- **Provenance lessons learned** ("when correcting a fact, don't infer narrative implications")
- **Workflow patterns proven out for this user** ("their performance-review archive lives at X; the interview mode works best in 15–20 min summary-back cycles")
- **Process-level corrections from earlier sessions** that future sessions shouldn't re-discover

These are **how-to-work-with-this-user** memories, not content about the user's career. If the runtime supports cross-session memory (e.g., Claude Code's `.claude/projects/*/memory/` system), write these there as small typed files (`feedback_*.md`, `reference_*.md`) with an index pointer in `MEMORY.md`.

Distinction to maintain:
- **Database content** ("the user's patent is titled X, awarded provisional status YYYY-MM, mechanism is Y") → goes in `~/career/`
- **Cross-session behavior** ("this user prefers comprehensive-arc over granular-mechanics in interviews; pivot quickly when they signal in-the-weeds") → goes in cross-session memory

Behavioral memory is the discipline that lets future sessions skip re-learning lessons the user has already taught you. Both layers compound; neither replaces the other.

## Step 5 — End-of-session ritual

Before ending a session:

1. Update `SESSION.md` — date, what we did, where we stand, what to do next.
2. Move resolved items in `OPEN_QUESTIONS.md` to the "Answered" section with date + answer.
3. Add any new open questions surfaced this session.
4. Log structural / positioning decisions in `DECISIONS.md` with rationale.
5. If "we could build X" was mentioned but not built, log it in `OPPORTUNITIES.md` (what / why-valuable / trigger).

## File map (full reference)

| Path | Purpose |
|---|---|
| `SESSION.md` | Where we left off + what to do next. Updated every session. |
| `OPEN_QUESTIONS.md` | Tier 1–5 prioritized list of blockers. |
| `DECISIONS.md` | Append-only log of structural + positioning decisions. |
| `OPPORTUNITIES.md` | "We could build X" notes — what / why-valuable / trigger. |
| `CLAUDE.md` | User-specific hygiene rules for AI sessions. |
| `KICKOFF_PROMPT.md` | Copy-paste session openers. |
| `README.md` | The Claim → Proof model + conventions. |
| `strengths.md` | The 6 signature strengths — the claim layer. |
| `themes/*.md` | Deep-dives per strength with chronology + framing variants. |
| `evidence/*.md` | One file per quantified accomplishment. |
| `stories/*.md` | STAR-format behavioral narratives. |
| `voice/peer-quotes.md` | Curated third-party quotes organized by what they prove. |
| `voice/self-voice.md` | The user's actual writing voice. |
| `identity.md` | Lane positioning + elevator pitches. |
| `career-arc.md` | The through-line narrative across all roles. |
| `history/*.md` | Chronological role context (background, not headline). |
| `skills.md` | Skill inventory with proficiency + recency. |
| `education.md` | Degrees, certs, training. |
| `patents-publications.md` | Patents, talks, OSS, public writing. |
| `references.md` | Who would vouch for what, with tier (1=anytime, 2=warning, 3=written). |
| `comp.md` | Comp history + target + negotiation notes (sensitive). |
| `targets/role-criteria.md` | Filters for what role to take next. |
| `targets/companies.md` | Target company list with status + why + who-you-know. |
| `targets/recruiter-personas.md` | The lanes you're being recruited *for*. |
| `applications/tracker.md` | Active application log. |
| `artifacts/resumes/` | Generated resumes. |
| `artifacts/linkedin/` | Generated LinkedIn copy. |
| `artifacts/cover-letters/` | Generated cover letters. |
| `sources/inventory.md` | Inventory of raw source material. |
| `sources/inputs/` | Drop-zone for new sources to mine. |

## When in doubt

**Lead with the claim, prove with the example, in the user's voice.** Don't invent. Date everything. Promote cross-cutting questions to `OPEN_QUESTIONS.md`. Update `SESSION.md` at the end.
