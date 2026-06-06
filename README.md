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

## Install

`career-database` is a Claude Code plugin. After cloning the repo to your plugins directory, Claude Code picks it up on next launch and exposes it as the `/career-database` slash command.

Quickest path — clone directly into the plugin directory:

```
# macOS / Linux
git clone https://github.com/<your-username>/career-database ~/.claude/plugins/career-database

# Windows (PowerShell)
git clone https://github.com/<your-username>/career-database "$env:USERPROFILE\.claude\plugins\career-database"
```

The plugin should resolve to:

```
~/.claude/plugins/career-database/
  .claude-plugin/
    plugin.json
  README.md
  SKILL.md
  docs/
    ARCHITECTURE.md
    BOOTSTRAPPING.md
    CONVENTIONS.md
    WORKFLOWS.md
  template/
    (~25 markdown files mirroring the database structure)
```

After installing, **restart Claude Code** so the plugin registry picks up the new skill.

If you don't have Claude Code, the templates and docs are still useful standalone — clone the repo and copy `template/` to your chosen location. The methodology (Claim → Proof, Tier 1–5, hygiene rules) works in any tool that reads markdown.

## Quick start

Once installed and Claude Code has been restarted, invoke the skill in any Claude Code session:

```
/career-database
```

The skill will:
1. Ask where to put the database (default `~/career/`)
2. Copy template files there if the directory doesn't exist; read the existing operational files (`SESSION.md`, `OPEN_QUESTIONS.md`) if it does
3. Walk you through the first session — Tier 1 interview-blocking questions first (see `docs/BOOTSTRAPPING.md` for the full first-session guide)

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
- **Interview / brain-dump:** when the user wants to brain-dump an era or project in real time — the AI is scribe + interviewer, capturing verbatim into voice files and flushing at natural breakpoints
- **Artifact generation:** lead with claim → pull proof → match voice → reference theme framing
- **Audit / consistency check:** periodically compare the database against source materials to surface drift, missing items, framing inconsistencies; report-only deliverable
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

## Related

`career-database` is the substrate layer — durable, broad, owned by the user. A separate skill called `autowrite` covers the artifact-generation side: given a resume and a list of target companies, it autonomously scores the resume against company-specific binary hiring evals, mutates one line at a time, and produces opening-tailored variants. The two skills are independent (no code-level dependencies) but compose cleanly — `career-database` builds the substrate; `autowrite` operates on the canonical artifact produced from it.

If you want the substrate layer (interview prep, voice capture, durable claim → proof structure across your career): you're in the right place.

If you want autonomous resume tailoring across multiple target companies: that's `autowrite`. Either or both, in either order.

## License

MIT. See [`LICENSE`](LICENSE).

## Contributing

Issues and pull requests welcome. Especially:
- Additional theme patterns (the strengths-deep-dive layer is the most opinionated and benefits from more examples)
- Frontmatter schema refinements
- Workflow patterns for specific industries / disciplines
- Translations / non-English templates
