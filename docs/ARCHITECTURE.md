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
> "I'm the operator who absorbs uncertainty and keeps teams functional through crisis. Most recently my team tripled during a period when peer orgs contracted, while sustaining top-decile direct-report sentiment scores across multiple measurement cycles."

Claim first ("absorbs uncertainty and keeps teams functional through crisis"). Proof immediately after. Chronology is the *support*, not the lede.

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
