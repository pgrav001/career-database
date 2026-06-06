# Architecture — the Claim → Proof model

> _The single most important principle behind this database. The reason it's worth using vs. a folder of Word docs._

## The principle

**Your job-search story is about how you're effective — behaviors and skills — proven by examples. Not chronology proven by inference.**

Most resumes lead with chronology and let the reader infer the behavior. That's the wrong direction:
- The reader has 7 seconds. Inferring behavior from a job-title timeline is too much work.
- Two candidates with similar timelines can have *very different* operating patterns. Chronology obscures the pattern.
- Recruiters and hiring managers are pattern-matching for "how does this person work?" — give them the pattern directly.

The Claim → Proof model inverts this. You name *how you operate* (the claim). You prove it with specific examples (the proof). The chronology supports both but doesn't lead.

## The layers

| Layer | What it is | Files | Role |
|---|---|---|---|
| **The claims** | Durable behavioral patterns (how you operate) | `strengths.md` + `themes/*.md` | The headline material |
| **The proof** | Specific quantified accomplishments | `evidence/*.md` | What backs the claims |
| **The proof in narrative form** | STAR-format behavioral stories | `stories/*.md` | The interview-ready version of proof |
| **The third-party proof** | Curated quotes from managers, peers, reports | `voice/peer-quotes.md` | What others say (more credible than self-claim) |
| **The voice** | Your actual writing patterns | `voice/self-voice.md` | The tone for any generated artifact |
| **The chronology** | Role-by-role context | `history/*.md` + `career-arc.md` | Background, not headline |
| **The lane positioning** | What track / level / scope you're targeting | `identity.md` + `targets/*` | The filter applied to opportunities |
| **The operational layer** | Session continuity + hygiene | `SESSION.md` + `OPEN_QUESTIONS.md` + `DECISIONS.md` + `OPPORTUNITIES.md` + `CLAUDE.md` | Makes the database survive across sessions |

## How artifact generation works

Every outward-facing artifact (resume bullet, LinkedIn About, cover letter line, interview answer) follows the same shape:

1. **Pick the claim.** Match a strength from `strengths.md` to the role / audience / prompt.
2. **Pull the proof.** Use `evidence/*.md` + `voice/peer-quotes.md` to back the claim with specifics.
3. **Match the voice.** Apply `voice/self-voice.md` patterns so the output sounds like *you*.
4. **Reference theme framing.** `themes/*.md` files have framing variants for different audiences (Director loop vs. Staff IC loop, AI lab vs. FAANG, etc.).

### Worked example

**Bad opening** (chronology-led):
> "I joined Acme Corp in 2016 and worked my way from L4 Engineer to Senior Engineering Manager. Most recently I led a 26-person org..."

The reader is doing the work. They have to infer *what makes this person distinctive*.

**Good opening** (claim-led):
> "I'm the manager who takes over stalled programs and makes them ship. Most recently I inherited a platform migration that had been six months overrun; we cut over the next quarter, and the program had its first on-time release in two years."

Claim first ("takes over stalled programs and makes them ship"). Proof immediately after. Chronology is the *support*, not the lede.

## Canonical artifacts vs. per-opening submissions

The database produces two structurally different kinds of outputs, and they live in different trees:

| Tree | Organized by | Purpose | Example contents |
|---|---|---|---|
| `artifacts/` | **artifact type** | The canonical, generalized version of each artifact — tuned for the user's broad search direction | `artifacts/resumes/v3-locked.md`, `artifacts/linkedin/about-current.md`, `artifacts/cover-letters/template-director.md` |
| `applications/<company>-<role-slug>/` | **opening** | The per-opening submission set — variant artifacts scoped to one specific JD | `applications/acme-director-of-eng/resume.md`, `applications/acme-director-of-eng/cover-letter.md`, plus rendered deliverables |

Both trees coexist; they answer different questions.

### Why two trees

- The **canonical** is tuned to be the user's best generalized story — useful for LinkedIn, recruiter outreach, and as the starting point for every variant. The canonical changes slowly and is the substrate everything else builds from.
- The **per-opening submission** is tuned to one specific JD. It is short-lived (good for the specific application; not the right shape for the next one). It is allowed to make trades the canonical can't — e.g., cutting a Highlight that's load-bearing for the broader search but doesn't earn its skim altitude for this specific role.

Trying to maintain a single artifact that serves both purposes always ends in drift. Either the canonical absorbs per-opening edits and becomes confused, or the variant accumulates canonical signals that aren't right for the opening. Two trees, two purposes, clear handoff.

### How they relate

- A variant always **declares its canonical parent** in frontmatter (`based_on: artifacts/resumes/<canonical-version>.md`).
- A variant always **declares its diffs from canonical** so the gap is explicit and future-readable.
- A variant always **declares whether changes can propagate back to canonical** (`do_not_propagate` field) — most variant edits should NOT propagate; the variant is scoped to one opening for a reason.
- The canonical never references specific variants. The canonical is upstream; variants are downstream.

### File map shape for per-opening directories

```
applications/
  tracker.md                              # active application log (canonical, generalized)
  <company>-<role-slug>/
    resume.md                             # variant markdown
    resume.<presentation-extension>       # designed PDF source (Typst, HTML, etc.)
    resume.pdf                            # rendered deliverable
    cover-letter.md                       # role-scoped cover letter
    cover-letter.<presentation-extension> # if rendered
    cover-letter.pdf                      # if rendered
    audit.md                              # the JD-vs-canonical audit that informed the variant (optional)
```

The per-opening directory is the submission set — everything an application needs, co-located. When the application is submitted, the directory is the receipt: which resume went in, which cover letter, what audit informed them, what decisions were locked.

Variant frontmatter discipline (the `based_on`, `diffs_from_canonical`, `do_not_propagate`, `evals_echoed`, `resolutions` fields) is spelled out in `CONVENTIONS.md`. The pattern enforces the canonical-vs-variant boundary so the two trees don't quietly bleed into each other.

## Why the operational layer matters

The substrate is only useful if it survives across sessions. The operational files are the discipline:

- **`SESSION.md`** — handoff notes. Read at start, update at end. Without this, every session starts cold.
- **`OPEN_QUESTIONS.md`** — prioritized list of blockers. Without this, half-questions get scattered across files and forgotten.
- **`DECISIONS.md`** — structural choices with rationale. Without this, you re-litigate the same decisions every session.
- **`OPPORTUNITIES.md`** — "we could build X" notes. Without this, half-conceived ideas vanish in chat.
- **`CLAUDE.md`** — explicit hygiene rules. Without this, future-Claude (or future-you) will drift from the conventions.

## Why 6 strengths

Strengths are the **claim layer**. Anchor on a small number (6 ± 1) that you can defend across multiple examples each, over multiple years. Fewer than 4 is too narrow; more than 7 is too diffuse.

Each strength must:
- Show up across multiple distinct roles or cycles (not just one)
- Have at least 2 quantifiable examples backing it
- Have at least 1 third-party quote validating it
- Be recognizably *you*, not a generic professional virtue

Strengths are **scaffolding**, not stone. They get refined as the substrate accumulates. The Open Recall section of `strengths.md` is where pressure-test thoughts live until they resolve.

## Honest bounded framing: "X landed, Y did not"

The most credible version of any claim names both what worked **and** what was attempted but didn't land.

Most databases drift toward maximizing the claim — every initiative becomes a clean win, every promotion becomes part of a pattern. The result reads as too tidy. Recruiters and hiring managers are pattern-matching for *real* leaders, not flawless ones. The honest bounded version of a claim is more credible than the maximized one.

Example pattern: **"Precedent broken, playbook not formalized."**

- **The maximized version:** "Permanently raised the discipline's ceiling — created a precedent + documented the archetype for future promotions."
- **The honest version:** "Promoted the first IC at this level in the discipline (precedent landed). The general archetype documentation for future cases didn't happen — got crowded out by execution priorities."

Both versions describe the same outcome. The honest one is more believable because it acknowledges the part that didn't get done. It also pre-empts the natural follow-up question ("did you formalize this so others can follow?") with a credible answer instead of an evasion.

**When to apply:**

- Discipline-shaping outcomes — name what shifted *and* what didn't shift
- Multi-year bets — name the wins *and* the things that fell off the roadmap
- Cross-org influence work — name the orgs that adopted *and* the ones that didn't
- Talent development — name the people who grew *and* the trajectories that didn't materialize

**How to capture:**

In evidence files, use a "What landed / What didn't" framing or an explicit "Honest bounded framing" subsection. In themes, the "When it shows weakness (anti-pattern)" section of each strength file is the natural home for the honest counter-narrative.

This is also the right place to land **anti-claims** — things you've explicitly chosen *not* to claim. "I'm not the polished communicator at scale" is a credible thing to know about yourself; it tells the reader you understand your own pattern.

## Paired-thesis pattern (related-but-distinct positioning claims)

Sometimes the user's positioning resolves into **two related-but-distinct top-level claims** that work better together than collapsed into one.

Example: a user whose core thesis is "I run incident response when a release goes sideways" might also articulate "I build the engineering culture where releases go sideways less often." These aren't the same claim:
- The first frames the user as the *responder* — the person you want on-call when production breaks
- The second frames the user as the *culture-builder* — the person who prevents the breakage in the first place

They overlap (same body of work, same evidence base), but they land hardest at different audiences (an SRE leadership role vs. a head-of-engineering role). Collapsing them to one loses leverage; treating them as competitors creates confusion.

**Capture both** in `identity.md` under the core thesis section. Mark them as paired. Use them together in artifacts — the first as the primary thesis, the second as the broader framing that lands when the audience isn't AI-specific.

**When to look for a paired thesis:**

- The user delivers two related-but-distinct framings of the same work in the same conversation
- One framing lands hardest at one type of company; the other at a different type
- One is a sharper / narrower version of the other
- Both are defensible with the same evidence base, just framed differently

**When NOT to use:**

- If two framings are actually competing (mutually exclusive), pick one — don't bake the indecision into the database.
- If two framings are saying the same thing differently, collapse them.
- More than two top-level theses is usually a sign you haven't found the through-line yet.

## What this is NOT

- **Not a chronological resume.** Chronology is one layer; the headline layer is the strengths.
- **Not a brag list.** Every claim must be defensible with specifics; "leadership" without examples doesn't earn space.
- **Not a job-application tracker.** Applications live in `applications/`; the substrate is upstream.
- **Not a final artifact.** Resumes, LinkedIn copy, cover letters are *generated from* this — they live in `artifacts/`, downstream.
- **Not public.** Treat as private working notes. Anything that leaves (LinkedIn, sent resume) is a deliberate copy through `artifacts/`.

## The discipline

The database works when:
1. You actually update `SESSION.md` at the end of every session
2. You actually promote cross-cutting questions to `OPEN_QUESTIONS.md` rather than burying them in per-file Open Recall
3. You actually date time-sensitive claims (`direct-report sentiment 95% (H2 2024)`, not `direct-report sentiment 95%`)
4. You actually flag provenance (`confirmed` / `approximate` / `claimed`) on every claim
5. You actually lead with the claim and prove with the example when generating artifacts

The discipline is the value. Without it, you have a folder of files that drift apart.
