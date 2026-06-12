# Examples

Worked examples showing the skill's conventions in use. **All content here is fictional** — invented characters, invented organizations, invented metrics. The point is to show what a populated database *looks like* without exposing a real person's career.

## What's in here

### `sample-arc/` — Maren Halvorson, public-sector career

A 15-year arc through a rural county library system: reference librarian → branch manager → adult services coordinator → director of digital services. Picked deliberately to be **outside the tech / FAANG / startup mold** that dominates most career-tooling examples — to show that the Claim → Proof model isn't tied to one industry.

What to look for as you read:
- **Evidence files** show the frontmatter conventions (`status`, `confidence`, `metric`, `role`, `date_range`), the body shape (Situation / What I did / Quantified outcome / Supporting detail / Frames / Where it appears / Linked stories / Open recall), and inline provenance.
- **One story** shows STAR format with a Reflection beat and audience variants — the part most candidates skip.
- **`voice/peer-quotes.md`** shows how to capture third-party validation with provenance + as-of dating.
- **`SESSION.md` + `OPEN_QUESTIONS.md` + `DECISIONS.md`** show the operational rhythm — what makes the database survive between sessions.

What's *not* here, deliberately:
- A full populated database (would be ~25 files; the point is the shape, not the volume).
- Polish. The Open Recall sections show real "I haven't verified this yet" half-thoughts, because that's what the layer is for.
- The artifact layer (`artifacts/resumes/...`). Generating those *from* a populated substrate is the rest of the skill; the example focuses on the substrate itself.

## Using the example

This directory is **not part of the template**. Cloning the skill via `~/.claude/plugins/career-database` won't copy `examples/` into your own database. Read it here, learn the pattern, then start your own database from `template/`.

If a specific evidence-file shape or story structure is what you want to model, copy that *single file* into your own database and adapt it. The example exists to show the *shape*; your content is yours.
