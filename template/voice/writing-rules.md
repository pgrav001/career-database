# Writing Rules — the AI tells to strip from artifacts

> _The subtractive half of the voice layer. `self-voice.md` says how you actually write; this file lists the machine markers to remove before an artifact ships. Run the review pass below on every outward artifact._

## Why this file exists

An artifact drafted by an assistant reads like one. The tells are structural, not stylistic — stacked em-dash clauses, "X, not Y" foils, one idea restated at three zoom levels, empty intensifiers, bare-label leads. Each sentence is defensible; together they're a signature, and the user is the one who notices it, usually while re-reading something already submitted.

## How this composes with `self-voice.md`

- **This file is subtractive.** It removes markers that read as machine-generated.
- **`self-voice.md` is additive and authoritative.** It captures your genuine register.
- **Precedence: self-voice wins.** If you really do say "really," drop conversational asides, or use the occasional em dash, those stay. Strip a tell only when it's the assistant's, not yours. When unsure, check `self-voice.md` — if the marker lives there, it stays.

## Starting point

Convivy's **Write Better** (composed prose) and **talk-better** (conversational replies) rulesets are a good base: <https://github.com/convivy/write-better> (MIT). Distill and adapt them into this file rather than depending on the upstream copy, then extend with your own rules as they surface.

## Part 1 — Prose rules (composed artifacts)

_(Seed list. Replace or extend with the rules that actually fire on your drafts.)_

### Concision
- **No define-by-negation.** Say what a thing is, not what it isn't. Cut "X, not Y" foils.
- **No broad-to-narrow ramp.** Lead with the precise version; don't restate one idea at three zoom levels.

### Structure & flow
- **One idea per sentence.**
- **Stitch sentences end to start.** Close one sentence on the concept that opens the next; same for paragraphs.
- **Name the actor and lead with it.** Subject-verb-object over passive constructions.
- **Complete the clause, even for a bare lead.** "There are three pieces," not "Three pieces:".

### Clarity
- **Make the dependency explicit.** Replace "critical / key / load-bearing" with the specific use and the breakage point.

### Tone
- **Propose actions; don't just narrate them.**
- **Future work in future tense or imperative,** not present-as-if-underway.
- **Don't over-color a plain action.** "defer pricing," not "park pricing."

### Mechanics
- **Commas and semicolons over em dashes and mid-sentence colons.** Reserve colons and dashes for lists, code, or a definition label.
- **No empty adverbs.** Cut "really, basically, just, honestly, genuinely, very" when they add nothing — unless they're yours (see `self-voice.md`).

### Your own rules
_(Add rules as they surface. The ones that recur on your drafts matter more than the ones you inherited.)_

## Part 2 — Conversational rules (the assistant's in-session replies)

Each tell is a real virtue firing without a trigger. The fix isn't "be colder"; it's "stop auto-firing the marker."

- **No validation opener.** Don't open with "Great question / You're absolutely right." Answer.
- **No performed willingness.** Cut "Certainly! I'd be happy to…" preambles and reflex "Let me know if there's anything else!" sign-offs. A concrete next-step offer is fine.
- **No sycophantic reversal.** On pushback, re-examine; don't flip a correct answer to appease. Concede real errors, with the reason.
- **Match affect to content.** No reflex emoji or exclamation on a plain delivery.
- **No performed sincerity.** Drop "honestly / genuinely / frankly" as credibility prefaces.
- **No decision-dodging hedges.** Asked for a call, make it. Genuine factual uncertainty is fine to state.
- **No question read-back.** Don't replay the question to prove you understood; the answer proves it.
- **Don't over-structure a small answer.** Prose over headers when the content is two lines.

## The review pass (run before shipping any artifact)

1. **Draft.**
2. **Review as an adversary.** Assume at least one tell survived. Go rule by rule; quote a still-violating line, or clear the rule by name. "Looks clean" without reading each rule is a failed review.
3. **Rewrite** from what the review flagged. Leave facts, numbers, and your genuine voice untouched.

Log which rules fired in the artifact's frontmatter (`writing_rules_applied:`) so a later reader can tell the pass actually ran.

## Quick checklist (fast pass)

- Em-dash chains → commas / semicolons
- "really / genuinely / basically / just" → cut, unless it's yours
- "X, not Y" foil → state X
- Bare-label lead ("Three pieces:") → full sentence
- Actor-less / passive → name the actor
- Validation opener, eager preamble, reflex sign-off → cut
- Stacked hedges when a call was asked for → make the call
- Headers on a two-line answer → prose

## Open recall

- Which rules actually fire most often on your drafts (track them; promote to Part 1)
- Rules to add from your own editing habits

---

*Adapted from Convivy Write Better + talk-better (MIT). Paired with `self-voice.md`; where they conflict, self-voice wins.*
