# Evidence Library

> _One file per quantified accomplishment or "evidence hook."_

**What goes here:** Each file captures a single piece of evidence — a metric, a win, a specific outcome — in enough detail that a resume bullet, a LinkedIn line, or an interview answer can be built from it without going back to ask questions.

## Conventions

Every evidence file uses frontmatter:

```yaml
---
role: [role-key]                    # which role this happened in
date_range: YYYY-MM to YYYY-MM      # or single date
metric: "the headline number/claim"
status: outstanding | active | retired
confidence: confirmed | approximate | claimed
---
```

- **status:**
  - `outstanding` — known but missing detail; needs interview/recall to fill
  - `active` — fully documented; safe to use in any artifact
  - `retired` — accurate but no longer being foregrounded (outdated or eclipsed)
- **confidence:**
  - `confirmed` — backed by a document/system
  - `approximate` — best memory, directionally correct
  - `claimed` — you've used this number publicly but need to verify before reusing

Body sections:
- **Situation** — what was the context
- **What I did** — the actions you personally took (vs the team)
- **Quantified outcome** — the number and what it measures
- **Supporting detail** — backing facts, who knew about it, what made it hard
- **Frames** — how to position this evidence depending on audience/role/prompt
- **Where it appears** — list of artifacts (resume v_, LinkedIn line, talk, etc.) currently using it
- **Linked stories** — `[[stories/...]]` that reference this evidence
- **Open recall** — half-formed thoughts / things to verify

### The Frames section

A single piece of evidence can be framed multiple ways depending on audience and context. The `## Frames` section captures the different angles so future artifact generation has a menu to pull from, not a single fixed framing.

Pattern:

```markdown
## Frames

- **For Director / Senior Manager loops:** lead with [scope / org-level angle]
- **For Staff / Principal IC loops:** lead with [technical depth angle]
- **For AI-focused companies:** lead with [AI / production / scale angle]
- **For DX-focused companies:** lead with [developer-outcomes angle]
- **For traditional FAANG:** lead with [scale / process / measurement angle]
- **For early-stage / startup roles:** lead with [scrappy / multi-hat / built-from-scratch angle]
- **For "tell me about strategic thinking":** emphasize [angle]
- **For "tell me about cross-org collaboration":** emphasize [angle]
- **For "tell me about a failure":** _(if applicable)_ — what didn't work, what you learned
```

Not every Frames section needs every line. Use the ones that make sense for the evidence.

## Naming

`{role-prefix}-{short-description}.md` — examples:
- `acme-product-launch-1m-users.md`
- `acme-revenue-doubled.md`
- `prior-role-process-overhaul.md`

Slug = the most memorable identifier, not the full title.

## Index

| File | Status | Confidence | Metric |
|---|---|---|---|

_(Add a row per evidence file. Keep terse.)_

## Open recall

_(Evidence ideas not yet promoted to files.)_
