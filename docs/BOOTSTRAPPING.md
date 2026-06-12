# Bootstrapping — first 1–2 sessions

> _A specific guide for the first time you sit down with this. The most common bootstrap mistake is generating artifacts too early; the second-most-common is filling `strengths.md` from the top down._

## The 30-minute MVP path (try this first if you're skeptical)

The full first session is ~90–120 minutes and asks for source materials, Tier 1 answers, and a substance brain-dump. That's a real commitment, and it's reasonable to want to see whether the methodology produces anything useful *before* committing.

The MVP path skips most of the ritual and gets you to a single produced artifact in ~30 minutes. It's deliberately under-engineered. The point is to feel the rhythm — claim → evidence → voice → output — before scaling up.

**The 30-minute path:**

1. **Pick one role you held in the last 5 years** (~2 min). Most recent is fine. Don't pick the most ambiguous one yet — pick one you can talk about easily.

2. **Brain-dump it into a single evidence file** (~15 min). Open `template/evidence/_template.md`, copy it to `evidence/<short-slug>.md`, and fill it in for *one* accomplishment from that role. Don't be careful. Don't worry about whether it's the "right" accomplishment. Pick the one that's loudest in your memory and just write it. Use the Open Recall section at the bottom for everything you can't remember or aren't sure about — that's what it's for.

3. **Capture 1–2 peer quotes** (~5 min). Open `template/voice/peer-quotes.md`, copy it, drop in 1–2 things people have said about you that match the evidence you just wrote. Email praise, performance review excerpts, anything verbatim. Note the provenance inline.

4. **Generate one artifact: a LinkedIn paragraph** (~8 min). Ask Claude (or your AI assistant) to write a one-paragraph LinkedIn About update *grounded in the evidence file and the peer quotes you just wrote*. Lead with the claim implied by the evidence, prove with the metric, match the voice of the peer quote. One paragraph, no more.

**What you'll have at the end of 30 minutes:** one evidence file, one peer-quotes file, one generated paragraph. Not a career database. Not interview-ready. But: a tangible *output* that was *generated from* a substrate, which is the central methodology claim of this skill.

**If that 30-minute output feels worth scaling up,** go to "Before session 1" below and start the real bootstrap. If it doesn't, you've spent 30 minutes instead of 2 hours discovering this skill isn't a fit for you — that's a win too.

> See `examples/sample-arc/` (in the skill repo root) for what a populated database looks like in steady state — an anonymized worked example you can read before deciding to invest. ~15 minutes to read; complements this MVP path.

## Before session 1

Gather what you have:

- **Current resume** (the latest version, even if it's stale)
- **Performance review history** (if your employer keeps records — annual or half-yearly reviews are gold)
- **LinkedIn export** (Settings → Get a copy of your data → Want something in particular → Posts, Recommendations, Connections — full export takes ~24h)
- **Saved kudos** (Slack screenshots, email praise, written recommendations — anything that says "X said this about me")
- **Calendar export** (optional — useful for "what was I actually doing in 2022 H2?")

Drop all of these in `sources/inputs/` once the directory exists. Don't worry about format; just get them in one place.

## Setting up cross-session memory (one-time)

Cross-session memory is the layer the SKILL refers to in Step 4.5 — *how-to-work-with-this-user* notes that persist across sessions but don't belong in the database itself (behavioral preferences, workflow patterns proven out for you, process-level corrections from earlier sessions). The database is content; cross-session memory is behavior.

Under Claude Code, the memory layer lives outside your career database directory, in the Claude Code projects tree. Set it up once before your first session:

1. **Find the right project directory.** Claude Code namespaces memory by working directory. The convention is `~/.claude/projects/<path-slug>/memory/` where `<path-slug>` is your working directory with `/` replaced by `-` and the leading slash dropped. If your sessions run from `/Users/yourname`, the slug is `-Users-yourname`. If from `/home/yourname`, the slug is `-home-yourname`.
2. **Create the memory directory and index file:**
   ```
   mkdir -p ~/.claude/projects/<path-slug>/memory
   touch ~/.claude/projects/<path-slug>/memory/MEMORY.md
   ```
3. **Seed `MEMORY.md` with the index header** (the file is always loaded into Claude's context, so keep it under ~200 lines):
   ```markdown
   # Index of cross-session memory entries

   - (entries added here as Claude saves them)
   ```
4. **Add a first entry** if you have a behavioral preference you want preserved from session one (e.g., "User prefers comprehensive-arc framing over granular-mechanics drilling in interview brain-dumps"). Use this shape — one file per entry, named by type and topic:
   ```markdown
   ---
   name: feedback-interview-style
   description: Brief one-line summary that future-Claude will scan for relevance
   metadata:
     type: feedback
   ---

   <The behavioral preference, with **Why:** and **How to apply:** lines so future-Claude can judge edge cases.>
   ```

Memory types follow the convention in your runtime's documentation. The career-database skill uses four: `user` (profile facts), `feedback` (corrections + validated approaches), `project` (in-flight initiatives), `reference` (where information lives in external systems).

If your runtime doesn't have cross-session memory, skip this step entirely — write the same content into `CLAUDE.md` at the root of the database instead. It's noisier (every session reads the full file) but functionally equivalent.

## Common starting points (what to mine, given what you have)

Not every candidate starts with the corporate-employee default (resume + reviews + LinkedIn). The table below maps realistic source mixes to what to extract first.

| You have | First-pass extraction | What's likely missing |
|---|---|---|
| Resume + performance reviews + LinkedIn | The default — see "Before session 1" above | Probably nothing — this is the high-density case |
| Resume only (no formal reviews; consulting / contract / founder / government) | Mine the resume into `history/`; brain-dump each role into `evidence/` + `stories/` since you have no review-grade source to lean on | Third-party voice (`voice/peer-quotes.md`) — you'll need to actively solicit; see `voice/peer-quotes.md` Open Recall pattern |
| LinkedIn only (early career, light on internal docs) | Profile + Recommendations Received + Recommendations Given + Connections — LinkedIn's data export has all of these | Quantified outcomes (LinkedIn rarely captures numbers); plan a brain-dump session per role |
| Researcher / academic (publication list + talks instead of corporate work) | Mine `patents-publications.md` from your CV; mine talks + citations into `evidence/`; treat each major publication as the equivalent of a shipped product | The "behavioral story bank" Tier 2 — research-CV framing rarely captures conflict / failure / decision-under-pressure stories; needs separate brain-dump |
| Multi-decade career with paper-only old records | Don't try to reconstruct everything. Mine the last 10 years deeply; the older roles get one-line entries in `history/` with "details lost to time" notes | Specific metrics from pre-digital roles — set realistic expectations and don't fabricate |
| Just a strong sense of yourself, nothing on paper | Brain-dump-first bootstrap: skip source mining entirely; build the substrate from scratch via repeated era-by-era brain-dumps. This works but takes 4–6 sessions before the substrate is artifact-ready | Provenance — without source documents to cite, every claim is `claimed` (self-attested only); plan to verify the load-bearing ones before interview use |

For any case, the first-session goal is **breadth, not depth**. Capture what's there, surface what's missing, log gaps to `OPEN_QUESTIONS.md`, plan brain-dumps for the high-priority gaps in session 2.

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
