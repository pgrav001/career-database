# Conventions

> _The discipline that holds the database together. Without these, the files drift apart over time._

## Frontmatter schemas

### `history/{role}.md`

```yaml
---
company:
title:               # title held at end of tenure
dates:               # YYYY-MM to YYYY-MM, or "Current"
location:
manager:             # most recent manager at the role
team_size_managed:   # peak; "—" if IC
reports_to_level:    # what level the manager was
---
```

### `evidence/{slug}.md`

```yaml
---
role: [role-key]                    # which role this happened in (e.g. "acme" or "current")
date_range: YYYY-MM to YYYY-MM      # or single YYYY-MM
metric: "the headline number/claim"
status: outstanding | active | retired
confidence: confirmed | approximate | claimed
---
```

### `stories/{slug}.md`

```yaml
---
themes: [leadership, resilience, conflict, ...]
role:                              # which role this happened in
duration: ~2min | ~5min            # spoken duration
primary_evidence: [[evidence/...]] # what backs the "Result"
---
```

### `applications/<company>-<role-slug>/{artifact}.md` (per-opening variants)

```yaml
---
type: artifact
artifact: resume | cover-letter | linkedin-outreach | other
variant: <company>-<role-slug>
based_on: artifacts/{type}/<canonical-filename>      # the canonical this forks from
date: YYYY-MM-DD                                     # when the variant was drafted
status: draft | reviewed | submitted                 # current state of the variant
target_company: <Company Name>
target_role: <Role Title>
jd_url: <URL or "not-recorded-in-session">
director_level: true | false                         # affects cover-letter shape; informs review tone
diffs_from_canonical:                                # what changed and why
  - "<one-line description of each diff, anchored to a specific section or bullet>"
do_not_propagate:                                    # guard against cross-opening drift
  - "<one-line warning per non-propagatable change — what's variant-only and why>"
evals_echoed:                                        # for cover letters, the JD-derived signals the letter echoes in prose
  - "<one-line per echoed signal — what the letter foregrounds and what evidence it draws on>"
resolutions:                                         # open questions resolved during variant drafting / review
  - "<one-line per resolved question — Q: what was asked; A: what was decided>"
open_questions:                                      # remaining variant-specific blockers
  - "<one-line per open question>"
notes:                                               # free-form: length, voice, deliverable format, candidate questions flagged
  - "<one-line per note>"
---
```

Frontmatter discipline matters because variants live next to the canonical without overlapping with it. Each field above answers a specific question that, if left unanswered, leads to a known failure mode:

- `based_on` — answers "what is this a variant of?" Without it, future sessions can't tell whether the variant is up to date with the canonical or has drifted.
- `diffs_from_canonical` — answers "what did this variant change?" Without it, the variant is opaque; reviewing it for accuracy requires diffing manually against the canonical file every time.
- `do_not_propagate` — answers "are these changes safe to push back into the canonical?" Most variant edits are scoped to one opening. The `do_not_propagate` field is the explicit guard that prevents silent canonical drift when someone later thinks "this variant edit was actually good; let me copy it back."
- `evals_echoed` (for cover letters) — answers "which signals does this letter foreground?" Useful for interview prep — the letter's structure is itself a hypothesis about what the role screens for.
- `resolutions` — answers "what was decided during variant work?" Variant work typically resolves several small judgment calls (title wording, audience framing, length tradeoffs). Logging them in-frontmatter keeps the decisions discoverable without scrolling through `DECISIONS.md`.
- `open_questions` — flags blockers that did NOT get resolved. Should be empty when the variant is ready to submit; any remaining items go in `OPEN_QUESTIONS.md` at top-level for the next session.

**Required fields** for a variant: `type`, `artifact`, `variant`, `based_on`, `date`, `status`, `target_company`, `target_role`, `diffs_from_canonical`, `do_not_propagate`.

**Optional fields** (omit if not applicable): `jd_url`, `director_level`, `evals_echoed`, `resolutions`, `open_questions`, `notes`.

**Status legend** for variants:

- `draft` — variant was drafted but not yet reviewed by the user
- `reviewed` — user walked through per-bullet review; ready for deliverable port
- `submitted` — variant was submitted to the opening; archive-eligible after the opening closes

## Status legend

For **evidence**:
- `outstanding` — known but missing detail; needs interview / recall to fill
- `active` — fully documented; safe to use in any artifact
- `retired` — accurate but no longer being foregrounded (outdated or eclipsed)

For **applications** (in `applications/tracker.md`):
- `interested` — saved but not applied
- `applied`
- `screen` / `loop` / `offer` / `closed`

## Confidence legend

For evidence frontmatter — flag where the headline number came from:
- `confirmed` — backed by a document, system of record, or screenshot
- `approximate` — best memory, directionally correct, not exactly verifiable
- `claimed` — you've used this number publicly but should verify before reusing

## As-of dating

Time-sensitive claims **always** get a date:
- ✅ "Direct-report sentiment 95% (H2 2024)"
- ❌ "Direct-report sentiment 95%"
- ✅ "Team of 20 (as of YYYY-Q1)"
- ❌ "Team of 20"
- ✅ "Base $X (last cycle: YYYY-H1)"
- ❌ "Base $X"

When in doubt, `(as of YYYY-MM)` is fine.

## `[[wiki-link]]` convention

Cross-link with `[[path-without-extension]]`:
- From a history file → its evidence: `[[evidence/product-launch]]`
- From an evidence file → the story it powers: `[[stories/product-launch]]`
- From a story → the evidence backing the Result: `[[evidence/...]]`
- From a theme → the evidence supporting it: `[[evidence/...]]`

The `[[...]]` syntax isn't auto-resolved by any tooling — it's a human/AI navigation aid and a grep target. It is OK to write `[[name]]` for a file that doesn't exist yet; it marks something worth writing later.

## Per-file Open Recall pattern

Every file ends with a `## Open recall` section. This is for **half-formed thoughts in the context of that specific file** — questions you have for yourself, things to add later, gaps to fill.

Example, at the bottom of an evidence file:
```markdown
## Open recall

- Exact dollar amount on the savings (currently "millions" — get a tighter number)
- Names of the org leads who signed off
- Whether the impact persisted into the following year
```

**Cross-cutting questions** — the ones that block interview readiness or block artifact generation — get **promoted** from per-file Open Recall to top-level `OPEN_QUESTIONS.md`. When in doubt, do both (add to top-level + leave a marker in the per-file Open Recall).

## Provenance

Inline provenance flags on individual claims, when the difference matters:

```markdown
- 75% offer-decline rate (source: internal comp review, YYYY)
- Direct-report sentiment 95% (source: performance archive, confirmed)
- Team grew from 4 to 20+ (claimed — verify against headcount records before interview use)
```

For evidence frontmatter, the `confidence:` field handles the headline metric. For other claims in the body, inline notes work.

### Three-tier provenance distinction (when it matters)

For claims that will go into outward-facing artifacts, distinguish:

| Tier | What it is | Example | When to use |
|---|---|---|---|
| **Source-grade** | Backed by a document, press article, system of record, or other independently-verifiable source | "Product launched Aug 2025, covered by UploadVR + Road to VR + the company's own dev blog" | Anything a recruiter could verify by Googling. Strongest claim type. |
| **Subject-attested** | The user told you, but no source backs it | "The retrieval layer behind the launched product was my team's work" — true per the user, but the press doesn't say so | Most database content. Mark explicitly when adjacent claims are source-grade so the boundary is clear. |
| **Inferred** | You (the AI) reasoned to it from other captures | "Therefore the user was probably the technical lead" | **Don't.** Don't write inferred content into the database unless you flag it as inference *and* the user confirms. Inference baked in as fact is how databases drift. |

This isn't a frontmatter field — it's a discipline applied in the body of evidence files, especially where source-grade and subject-attested claims sit next to each other. Make the boundary explicit so future-you can tell what's externally verifiable.

### Don't infer narrative from factual corrections

When the user corrects a fact in the database (a level, a title, a date, a name), correct **only the fact**. Don't bake in narrative implications they didn't authorize.

Example of the failure mode: the user says "actually X was IC6, not IC7." A response that propagates the correction *plus* reframes them as a "talent I couldn't fully advance" story is two changes, only one of which was authorized. The factual correction is in scope; the narrative reframe is not.

Stick to facts on corrections. Let the user author narrative.

### Source ambiguity → confirm, don't infer

When source text ambiguously attributes an outcome to multiple people, ask the user rather than infer.

Example: a self-review sentence reads *"X and Y - grew the first technical IC7 in the company. X taking a role as [scope A] and Y taking a direct role in [scope B]."* This sentence is genuinely ambiguous — it could mean both X and Y reached IC7, or it could mean only X did and Y was promoted to a different level / scope. Mining sessions that infer "both got IC7" can propagate that inference across many files before someone catches it.

When you encounter sentence-level ambiguity in source text about who got which outcome, pause and ask. The minute of clarification saves an hour of correction-propagation later.

## Naming conventions

- **Files:** lowercase, kebab-case, role-prefixed when ambiguous
  - `evidence/acme-product-launch-1m-users.md` (role-prefixed)
  - `evidence/comp-overhaul.md` (unambiguous)
- **Slug = the most memorable identifier.** Not the full title.
  - ✅ `evidence/team-scale-4-to-20.md`
  - ❌ `evidence/scaled-engineering-team-from-four-to-twenty-headcount.md`

## Date format

- **Absolute dates:** `YYYY-MM-DD` (ISO 8601) — e.g. `2026-01-15`
- **Months:** `YYYY-MM` — `2026-05`
- **Half-years:** `YYYY-H1` / `YYYY-H2` — `2022-H2`
- **Quarters:** `YYYY-Q1` etc. — `2024-Q1`

Convert **relative dates** in conversation ("last Thursday", "two cycles ago") to absolute dates before writing them down. Relative dates become ambiguous as time passes.

## The session-end ritual (procedural convention)

End every session with:

1. **`SESSION.md`** — date, what we did, where we stand, what's next
2. **`OPEN_QUESTIONS.md`** — move resolved items to "Answered" with date + answer; add new opens
3. **`DECISIONS.md`** — log structural / positioning calls with rationale
4. **`OPPORTUNITIES.md`** — log "we could build X" notes (what / why-valuable / trigger)

This is the convention that makes the database survive across sessions. Skipping it is the single most common failure mode.

## Don'ts

- **Don't invent.** When something is unknown, leave a placeholder and add to `OPEN_QUESTIONS.md`.
- **Don't bury cross-cutting questions** in per-file Open Recall. Promote them.
- **Don't generate finished artifacts** before Tier 1 OPEN_QUESTIONS are answered.
- **Don't put sensitive numbers** (full comp, identity-stealable data) in generated artifacts unless explicitly asked. The substrate may hold them; artifacts default to "no specific numbers in outreach."
- **Don't re-litigate decisions** in `DECISIONS.md` without reading them first.
- **Don't use corporate hero voice.** "Spearheaded transformational impact" doesn't sound like a real person.
