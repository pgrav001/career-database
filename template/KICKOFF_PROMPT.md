# Kickoff Prompts

> _Copy-paste session openers for re-engaging Claude with this database. Pick whichever matches what you want to do._

## Generic session start

```
Read ~/career/CLAUDE.md, then SESSION.md, then OPEN_QUESTIONS.md.
I want to work on _____.
```

## Specific task variants

### Resume tailored for a specific role

```
Read ~/career/CLAUDE.md and README.md.
Draft a resume tailored for [role title] at [company]. Pull strengths from strengths.md that match, use evidence/*.md (status: active) for the proof, match my voice from voice/self-voice.md.
Output to artifacts/resumes/.
```

### LinkedIn About refresh

```
Read ~/career/CLAUDE.md and identity.md and voice/self-voice.md.
Draft a LinkedIn About section. Lead with my strongest claim, prove with one concrete example, end with what I'm looking for next.
Output to artifacts/linkedin/.
```

### Behavioral interview prep

```
Read ~/career/CLAUDE.md and the stories/ directory.
Help me prep for a behavioral loop. Run through likely prompts. Identify which existing stories cover which prompts and where the gaps are.
```

### Add new evidence

```
Read ~/career/CLAUDE.md.
I want to add evidence: [paste the accomplishment].
Help me create evidence/{slug}.md with proper frontmatter, suggest links to history and stories, and update any existing related files.
```

### Process new source material

```
Read ~/career/CLAUDE.md and sources/inventory.md.
I dropped [source file] in sources/inputs/. Mine it against the database — update history/, evidence/, stories/, voice/peer-quotes.md as appropriate. Mark the inventory row done.
```

### Pressure-test strengths

```
Read ~/career/CLAUDE.md, strengths.md, and the full evidence/ + stories/ + voice/peer-quotes.md trees.
Pressure-test the 6 strengths against the evidence. Are these *the* 6? Any missing? Any forced? Surface findings; don't edit yet.
```

### End-of-session ritual reminder

```
End-of-session ritual: update SESSION.md (what we did, what's next), move resolved OPEN_QUESTIONS to Answered, log any structural decisions in DECISIONS.md, log any "we could build X" notes in OPPORTUNITIES.md.
```
