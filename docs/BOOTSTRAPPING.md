# Bootstrapping — first 1–2 sessions

> _A specific guide for the first time you sit down with this. The most common bootstrap mistake is generating artifacts too early; the second-most-common is filling `strengths.md` from the top down._

## Before session 1

Gather what you have:

- **Current resume** (the latest version, even if it's stale)
- **Performance review history** (if your employer keeps records — annual or half-yearly reviews are gold)
- **LinkedIn export** (Settings → Get a copy of your data → Want something in particular → Posts, Recommendations, Connections — full export takes ~24h)
- **Saved kudos** (Slack screenshots, email praise, written recommendations — anything that says "X said this about me")
- **Calendar export** (optional — useful for "what was I actually doing in 2022 H2?")

Drop all of these in `sources/inputs/` once the directory exists. Don't worry about format; just get them in one place.

## Session 1 — Tier 1 + source mining (90–120 min)

### Part A: Answer Tier 1 questions (30–45 min)

Before generating any outward-facing artifact, get crisp answers to these five questions. Capture them in `identity.md`, `targets/role-criteria.md`, and `comp.md` as you go.

1. **Why are you leaving / why did you leave your last role?**
   - Be honest. The interview-defensibility version is the public version.
   - Verifiable context > personal narrative. ("Laid off as part of broader efficiency cut" > "It wasn't a good fit anymore.")
   - If voluntary: what specifically were you optimizing for?

2. **Why now? What are you looking for next?**
   - One sentence on the lane (IC / Manager / Director / Founder / Other).
   - One sentence on the filter (what kind of work / problem / phase / scale you want).
   - One sentence on what you're avoiding ("I won't thrive in a well-structured execution machine").

3. **If you've been at a level for a while: why didn't you advance?**
   - Recruiters and hiring managers ask this if there's an apparent ceiling.
   - Structural answers ("the discipline didn't have a Director track") > personal answers ("politics") even when both are true.

4. **Comp expectations.**
   - No-anchored-number is often the right move if you're not under acute pressure.
   - If you do anchor: base + bonus + equity, with explicit "evaluate total package" framing.

5. **Geography filter.**
   - Will you relocate? For what kind of role?
   - Remote-only / hybrid OK / on-site OK? Bay Area or another major market?

### Part B: Source mining (45–75 min)

For each source in `sources/inputs/`:

1. **Add it to `sources/inventory.md`** with type + date + one-line description + `[ ]` unmined.
2. **Mine it into the right layers:**
   - Job titles + dates + scope → `history/*.md` files (one per role)
   - Quantified outcomes → `evidence/*.md` files (one per accomplishment)
   - Behavioral stories you're proud of → `stories/*.md` (one per story; STAR format)
   - Manager / peer / direct-report quotes → `voice/peer-quotes.md`
   - Your own writing voice patterns → `voice/self-voice.md`
   - Patents / talks / OSS contributions → `patents-publications.md`
   - References to contact → `references.md`
3. **Mark inventory `[x]`** with a one-line summary of what came out.

Don't try to be exhaustive in session 1. First pass = breadth. Re-mining is expected and normal.

### Part C: End-of-session ritual

- Update `SESSION.md` with what got done and what's next.
- Promote any cross-cutting blockers to `OPEN_QUESTIONS.md`.
- Log any structural decisions you made (lane, comp posture, geography) in `DECISIONS.md`.

## Session 2 — Substance-layer brain-dump (60–120 min)

By now the database has structure but the substance is thin. The fix is a *bottom-up* brain-dump.

**Working pattern:**

1. **Pick an era.** Start with the most recent or the most ambiguous. Examples:
   - "My last 18 months at [company]"
   - "The promotion-to-Director cycle that didn't land"
   - "The startup founding stretch"
   - "The pivot from IC to manager"

2. **Talk freely; Claude (or future-you) captures.** Don't try to organize as you go. Trust that the structure will absorb the substance.

3. **Every 15–20 minutes, summarize back.** Verify what got captured matches what you meant.

4. **Capture phrasings into `voice/self-voice.md` verbatim.** When you say something that sounds like you, save the exact words.

5. **Don't fill `strengths.md` yet.** The 6 strengths emerge from the substance. Filling them top-down produces generic claims.

### After 1–2 era passes

Re-examine `strengths.md`. The 6 strengths should now be ones the substrate *demands*, not ones you've picked because they sound good.

For each candidate strength:
- Does it show up across multiple roles / cycles?
- Are there at least 2 quantifiable examples backing it?
- Is there at least 1 third-party quote validating it?
- Is it recognizably *you*, not a generic professional virtue?

If a candidate fails any of these, it's not a strength yet.

## Session 3+ — Pressure-test + first artifact (60–90 min)

Only after the substance layer is rich:

1. **Pressure-test the 6 strengths.**
   - Have someone (a trusted friend, a coach, or just future-you with cold eyes) read them and the supporting evidence.
   - Do they hold? Are any feeling forced? Are any obviously missing?
   - This is the one place where Claude's pattern-matching is least useful — strengths should feel *true*, not technically defensible.

2. **Generate the first artifact** (a resume tailored for one specific target).
   - Pick one target role / company.
   - Lead with the claim. Pull the proof. Match the voice.
   - Output to `artifacts/resumes/`.
   - This is a *dry run*. Expect to revise it 3–5 times.

3. **Iterate on the substrate based on what the artifact revealed.**
   - "I had no good evidence for X" → add to evidence
   - "I don't have a story about Y" → add to stories
   - "I couldn't find a peer quote about Z" → ask people you know to send one

## Common bootstrap mistakes

- **Generating artifacts before Tier 1 is done.** The artifact bakes in undefined positioning; you'll throw it away.
- **Filling `strengths.md` from the top down.** Generic strengths read as generic. Strengths must emerge from substance.
- **Trying to be exhaustive on the first source-mining pass.** You'll burn out. First pass = breadth, re-mine for depth.
- **Skipping the session-end ritual.** Next session starts cold.
- **Polishing evidence files in the first session.** They'll change as the structure absorbs more substance. Capture; don't polish yet.
- **Not promoting cross-cutting questions to `OPEN_QUESTIONS.md`.** They get buried in per-file Open Recall and forgotten.
- **Inventing facts.** When you don't remember, write a placeholder and promote to `OPEN_QUESTIONS.md`. Don't fill the gap with plausible-sounding fiction.

## After bootstrapping — what does steady-state look like?

Once the substrate is in place:

- Sessions are **shorter** (15–45 min) and **targeted** (one specific question or one specific artifact).
- The `SESSION.md` handoff makes cold-start fast.
- Artifact generation is **derivative**, not creative — pick claim, pull proof, match voice, ship.
- New evidence flows in as it happens (a kudos email arrives, a project ships, a peer says something quotable) rather than only at job-search time.

The database is most valuable *before* you need it. Build it warm.
