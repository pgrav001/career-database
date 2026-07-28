# Opportunity Watchlist

> _The funnel that feeds `[[tracker]]`. Everything interesting-but-not-committed lives here — second-tier opportunities, cold radar, roles waiting on a trigger. **Lightweight by design:** no hiring-manager profile, no binary evals, no tailored resume until an opportunity is promoted to a committed application in `[[tracker]]`._

## The three layers

| Layer | File | Granularity | Weight |
|---|---|---|---|
| **Company** — strategic (why them, who you know, geo) | `[[targets/companies]]` | Company | light |
| **Opportunity** — THIS FILE (the funnel) | `applications/watchlist.md` | Specific role / opening | light |
| **Application** — committed, executing | `[[tracker]]` | Application | heavy (the full machine) |

An opportunity graduates from here to `[[tracker]]` only when its **trigger fires** (see the promote rule). The heavyweight machine — hiring-manager profile → binary evals → tailored resume variant → cover letter — runs **only** at promotion, never on a watchlist entry.

## Graduated response — "track" is decoupled from "deep-eval"

Three response levels, so there's always a lane between "nothing" and "the whole machine":

- **Watch** — record only, no artifacts. Waiting on a trigger.
- **Light-touch apply** — canonical resume + a short candid note in your own voice. **No** tailored variant, **no** eval profile. For decent-fit roles worth a cheap shot, or when the pipeline is thin.
- **Full-tailor** — the per-opening tailoring workflow in `docs/WORKFLOWS.md`. Reserved for high-fit + high-conviction, or when a warm path exists.

## Promote rule — how to move an opportunity forward

Advance an opportunity when one of these fires:

- a **warm path** appears (referral, recruiter relationship, inbound interest) → promote to **full-tailor**;
- the role **re-levels / re-scopes** into a clean fit → promote;
- **conviction is exceptional** (rare, dead-center fit) → **full-tailor** even cold;
- the **pipeline is empty** and it's a decent fit → a **light-touch** apply is worth the cheap shot;
- otherwise → **keep watching**, or drop it at its revisit-by date.

_(Tune this rule to what the search is actually returning. If one channel is converting and another isn't, the promote rule is where that belongs.)_

## Entry schema (compact — mirrors the What / Why / Trigger pattern in `[[OPPORTUNITIES]]`)

- **Company · Role** — + link
- **Spotted / Source** — date; `cold-posting` / `warm` / `inbound` / `recruiter`
- **Fit** — one line vs `[[targets/role-criteria]]`
- **Warm path?** — who + how warm, or `none`
- **Trigger to advance** — the specific thing that makes it a go
- **Response if it goes** — watch / light-touch / full-tailor
- **Revisit-by** — a date; prune to Dropped if it lapses with no trigger
- **Notes**

---

## Tier 1 — pursue-soon (trigger met or close; next stop is `[[tracker]]`)

_(none yet)_

## Tier 2 — watching (real interest, waiting on a trigger)

_(none yet)_

<!-- TEMPLATE — copy for a new entry:
### {Company} · {Role} — [link]()
- **Spotted / Source:** YYYY-MM-DD ·
- **Fit:**
- **Warm path?:**
- **Trigger to advance:**
- **Response if it goes:** watch / light-touch / full-tailor
- **Revisit-by:** YYYY-MM-DD
- **Notes:**
-->

## Tier 3 — backlog / maybe (captured, not yet triaged)

_(Cheap capture. Anything interesting lands here with a link + a one-line why; triage to a tier during the next sweep.)_

_(none yet)_

## Promoted → tracker

_(Graduated to a committed application. One line + pointer, so the funnel history stays visible.)_

_(none yet)_

## Dropped / ruled out

_(One-line reason so future-you doesn't re-litigate.)_

_(none yet)_

---

## Review cadence — the watchlist sweep

A lightweight sweep whenever you do job-search work (or ad hoc weekly): **prune** the lapsed (past revisit-by, no trigger → Dropped), **advance** anything triggered (→ Tier 1, or promote to `[[tracker]]`), **triage** new backlog entries into a tier. No profiles, no evals — that machine only runs at promotion.
