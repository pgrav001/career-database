# Generated Resumes

Resumes generated from the substrate live here. Each one is downstream of the database — generated for a specific application, target role, or audience.

## Naming convention

`{YYYY-MM-DD}-{target-shorthand}-{lane}.md` — examples:
- `2026-06-15-contoso-director-platform.md`
- `2026-06-20-northwind-staff-engineer.md`

## What stays out of generated resumes by default

- Full comp numbers (use `[[comp]]` for the source; don't bake numbers into outward-facing artifacts unless asked)
- Sensitive context (layoff narrative phrasing, etc. — defer to `[[identity]]`)
- Anything tagged `confidence: claimed` in the evidence files (verify before publishing)

## Resume craft conventions

Defaults that have held up in practice — deviate deliberately, not by accident:

- **Result-led bullets.** Structure each bullet as *result, then the actions that produced it* ("Cut build time from 5 hours to 5 minutes by building an automated pipeline"), not action-then-result. The outcome is the part a skim catches.
- **Two-line cap per bullet.** A bullet that runs to three-plus lines is usually two ideas blended — split it or cut one.
- **Word-count discipline.** A senior two-page resume lands well around **~700–800 words**. Much longer reads as unedited; much shorter often means real content was gutted to hit a number. Treat any external "target N words" note as an input to weigh, not a hard constraint (see the external-feedback workflow in `WORKFLOWS.md`).
- **Role summaries earn their space.** A one-line summary under a role should explain the *unclear* — the scope, the day-to-day, what an outsider wouldn't infer from the title — not preview the bullets underneath it. If the summary just restates a bullet, cut it.
- **The summary/highlights are the skim layer; the bullets are the detail layer.** They should share no phrasing — a claim proven in Highlights and repeated verbatim in a bullet wastes one of the two. Run a differentiation pass so each altitude carries distinct weight.
- **Keep the source of truth in markdown; render to the presentation format.** Maintain content in a version-controlled `.md`, generate the designed PDF/docx from it, and note which rendered file is canonical vs. archived so "which version is current" is never ambiguous.
