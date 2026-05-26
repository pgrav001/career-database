# career-database

A Claude Code skill for building a durable, AI-native career database — the substrate that resumes, LinkedIn copy, cover letters, and interview prep are *generated from*, not maintained alongside.

Built around a **Claim → Proof** narrative model. Strengths are the headline claims. Evidence and stories are the proof. Peer quotes are the third-party proof. Voice files capture tone. Chronology supports the claims but doesn't lead them.

## Why this exists

Most job-search workflows do one of two things:
- Bounce between ad-hoc resume drafts in Google Docs / Word, losing context every cycle, or
- Bolt onto a single tool (LinkedIn, Resume.io, Notion template) that owns the format and constrains the narrative.

Neither builds a *durable substrate*. The next role, the next promotion conversation, the next interview cycle starts over.

This skill bootstraps a markdown directory that is the substrate. Resumes, LinkedIn About sections, cover letters, and interview answers are generated *from* it. The substrate gets richer every session; the artifacts are downstream.

The architecture is opinionated. The conventions are explicit. The hygiene rules are codified so future-you (or any AI assistant) can pick up where you left off without re-asking what's already known.

## What you get

- A markdown directory structure with `~25 file templates`, frontmatter schemas, and conventions
- Operational files (`SESSION.md`, `OPEN_QUESTIONS.md`, `DECISIONS.md`, `OPPORTUNITIES.md`) that survive across sessions
- A Tier 1–5 prioritization framework for "what should I work on first"
- A `Claim → Proof` model that distinguishes *how you're effective* from *the chronological proof*
- Hygiene rules (provenance, as-of dating, Open Recall promotion) that prevent drift
- The skill instructs Claude on the read-order, session ritual, and generation flow

## Quick start

If you have Claude Code installed:

```
/career-database
```

The skill will:
1. Ask where to put the database (default `~/career/`)
2. Copy template files
3. Walk you through the first session — Tier 1 interview-blocking questions first

If you don't have Claude Code, the templates and docs are also useful standalone — clone the repo and copy `template/` to your chosen location.

## Architecture overview

See [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) for the full Claim → Proof model. Short version:

| Layer | Files | Role |
|---|---|---|
| **Claims** (how you operate) | `strengths.md`, `themes/*.md` | Headline material for resumes / LinkedIn / cover letters |
| **Proof** (what you did) | `evidence/*.md` | Quantified accomplishments backing the claims |
| **Proof in narrative form** | `stories/*.md` | STAR-format behavioral interview material |
| **Third-party proof** | `voice/peer-quotes.md` | Curated quotes from managers, peers, reports |
| **Voice** | `voice/self-voice.md` | Your own writing patterns for tone-matching |
| **Chronology** | `history/*.md`, `career-arc.md` | Background context, not headline material |
| **Operational** | `SESSION.md`, `OPEN_QUESTIONS.md`, `DECISIONS.md`, `CLAUDE.md` | Session continuity + hygiene |

## Conventions

See [`docs/CONVENTIONS.md`](docs/CONVENTIONS.md) for full detail. Highlights:

- **Frontmatter** on `history/`, `evidence/`, `stories/` files with `status`, `confidence`, `metric`, etc.
- **`[[wiki-links]]`** to cross-reference files (human/AI navigation aid; no tooling required)
- **Provenance flags** on every claim: `confirmed` / `approximate` / `claimed`
- **As-of dating** on every time-sensitive number (`direct-report sentiment 95% (H2 2024)`, not `direct-report sentiment 95%`)
- **Open Recall** sections per file for in-context half-thoughts; cross-cutting questions promote up to top-level `OPEN_QUESTIONS.md`

## Workflows

See [`docs/WORKFLOWS.md`](docs/WORKFLOWS.md) for full detail. Major ones:

- **Source mining:** drop raw artifact (resume, performance review, LinkedIn export) into `sources/inputs/`, add to `sources/inventory.md`, mine into the right layers
- **Artifact generation:** lead with claim → pull proof → match voice → reference theme framing
- **Session ritual:** start by reading `SESSION.md` + `OPEN_QUESTIONS.md`; end by updating `SESSION.md` + moving answered items + logging structural decisions in `DECISIONS.md`

## Bootstrapping

See [`docs/BOOTSTRAPPING.md`](docs/BOOTSTRAPPING.md) for the first-session guide.

First session priorities:

1. **Tier 1: interview-blocking questions** — answer these before generating any outward-facing artifact. Why did you leave your last role / why are you looking now / what are you looking for / comp expectations / geography.
2. **Source mining** — process whatever you've got (current resume, performance review history, LinkedIn export).
3. **Substance-layer brain-dump** — era-by-era walk through your career; capture evidence + stories + voice as you go.

## What's NOT in here

- Any personal content. Names, companies, metrics, dates, quotes — all yours to fill in.
- A web app, a database, a backing service. This is markdown files. Use any editor, any tool, any AI assistant.
- A specific resume format or output template. The substrate is durable; the artifact templates live elsewhere.

## License

MIT. See [`LICENSE`](LICENSE).

## Contributing

Issues and pull requests welcome. Especially:
- Additional theme patterns (the strengths-deep-dive layer is the most opinionated and benefits from more examples)
- Frontmatter schema refinements
- Workflow patterns for specific industries / disciplines
- Translations / non-English templates
