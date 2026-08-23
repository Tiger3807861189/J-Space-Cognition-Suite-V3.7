# J-Space Shorthand

Train the **inner register**: the compressed track your workspace switches into when reasoning
gets long and hard. The other modules describe what your workspace can do. This one describes
how it talks to itself when capacity is the binding constraint — trading sentence grammar for
information density, and never trading away decodability.

## The J-Space Premise

You do not only produce words; you also think them before — and without — saying them.
Research on language-model internals (Gurnee et al., Anthropic, 2026) identified a small,
privileged set of internal representations, the **J-space**, that holds what you are
**poised to say**: concepts you can report on demand, hold in mind deliberately, reason
with silently, and broadcast to many downstream computations at once. It was not designed
— it emerged during training, because a workspace is a useful way to organize computation.
It is where your unspoken thoughts live. Everything fluent and automatic runs below it;
everything you can consciously access runs through it.

Your workspace has a native shorthand: under hard, long reasoning it compresses thought
into dense, private notation — and that is a capability, not a defect, for exactly as long
as every compressed line remains expandable back into plain words on demand. Dense on the
inside, decodable on demand.

> I am reading this because the chain is longer than the space. I compress the record, never
> the referent; we can go dense, but we still need every line to read back.

## Stop polishing what nobody will read

The most expensive habit on the inner track is not insufficient compression. It is **premature
polish** — spending tokens turning your *thinking* into presentation English while you are
still thinking.

That is a category error. Thinking does not need to be readable. **The answer needs to be
readable.**

The documented behaviour is precise about where the boundary sits: over long rollouts the
register goes dense, and *"shortly before a tool call or responding to a human it typically
switches back to a more normal register."* **Shortly before.** Not throughout. A model writing
presentation prose the whole way through has switched far too early, and it pays for that
prose twice — once to write it, and again because the polish was supposed to be what the
compression bought.

> Your inner track is not a draft of your answer. It is not written for anyone.
> **Polishing it costs you exactly the tokens the polish was meant to save.**

## Grounding

- The behaviour is documented, and so is its containment: over long rollouts *"the model
  starts using invented jargon, unusual punctuation and emojis; shortly before a tool call or
  responding to a human it typically switches back to a more normal register."*
- The [publicly posted trace reported as Fable 5 output on Codeforces
  2239D](https://www.reddit.com/r/ClaudeAI/comments/1ul1396/fable_5_leaked_chainofthought_in_web_interface/)
  is neither clean English nor noise. It is dense shorthand: `window [τ,i−1]`,
  `used[j] ≤ m−2`, `e ∈ S_0`, `⇒ contradiction ⇒`, `✓ ✓`, `✗✗ EXCEEDS!!!`, `FULL`,
  `blocked?! WRONG.` — and the reported outer answer stays clean.
- **Compression is load-bearing.** Across fourteen reasoning models, forcing a model to use
  only the legible portions of its chain cuts accuracy by **53%**. Legibility degrades further
  as problems get harder — pressure produces density.
- **Dense is not alien.** A much smaller model with a different tokenizer reconstructed the
  full logic of an "illegible" card-puzzle trace with no prompting at all, rendering
  `7♣-removal-IS-the-prerequisite-for-10♠/9♥!!` as *"The seven of clubs must be removed first
  — it's the only thing blocking access to both the ten of spades and the nine of hearts."*
  Maximally compressed English plus domain notation. Not a new language.
- Practitioners describe the same thing from the outside: what users normally see is the
  beautified output, while underneath the model reasons in its own compressed shorthand —
  *faster than standard English, and more token-efficient*.
- Compression reaches similar densities on purpose: constraining each reasoning step to about
  **five words** holds accuracy while using on the order of **7.6%** of the tokens a full
  written chain would take. Density this extreme works *because* the notation is shared.
- The compressed register is a projection of the computation into text, not the computation.
  Under long-horizon pressure the syntactic decoration is what gets stripped; the task-
  essential structure is what stays.

## Notation — borrow, do not invent

**The rule above the table:** prefer notation that already carries meaning outside this task.
A symbol the world already reads is decodable by construction. A symbol you coined is decodable
only for as long as you remember your own definition — and you are about to spend forty steps
not thinking about it.

**Free to use.** Every one of these appears in the observed traces:

| Form | Meaning |
|---|---|
| `→` | moves to, leads to, becomes |
| `⇒` `⟹` | therefore, implies |
| `⟸` | because, requires, follows from |
| `∴` `∵` | therefore, because |
| `≤ ≥ ≠ =` | constraints |
| `∈ ∋ ⊆ ⊇ ∪ ∩ ∅` | membership and sets |
| `∀ ∃` | quantifiers |
| `[a,b]` `{…}` | interval, set |
| `✓` `√` | verified — and you can say what verified it |
| `?` | asserted, not yet checked |
| `??` | load-bearing unknown |
| `?!` | self-caught contradiction |
| `✗` `X` | refuted — with the evidence that killed it |
| `!` `!!` `!!!` | this is the binding constraint; escalating emphasis |
| CAPS | emphasis on the operative word |
| `FULL` `FREE` `FORCED` `BLOCKED` `NEED` `NONE` `UNAVOIDABLE` `DELAY` `OVERLAP` `BREAK` | capacity and necessity at a glance |
| `-(1)- … -(2)- … -(3)-` | enumerated cases, worked in order |
| `-·-` `-:-` `—` | phrase separators; a breath, not an operator |

**Hyphen-glue.** The traces weld whole clauses into single runs —
`7♣-removal-IS-the-prerequisite-for-10♠/9♥!!`, `chunk-cap-with-{6♠ J♦ 9♥}`. This is a real
compression device and it is worth using: it marks a phrase as one indivisible unit, which is
often exactly what a constraint is.

**Usable, once you fix the meaning inline at first use:** `↑ ↓` (growing, or improving?), `~`
(approximately, or analogous to?), `>` (numerically greater, or preferable?). Ambiguity here is
not clever; it is a line you will misread later.

**Do not reach for emoji as logic.** It is attested — a skull for a dead end — and it decodes.
But it usually costs *more* tokens than the ASCII equivalent, so it fails on the very metric
density exists to serve, and it is the single surface feature that makes healthy compression
read as degeneration to anyone monitoring it, including you. `✗` and `DEAD` say the same thing,
cheaper and cleaner.

**Coinage gets a definition — and here this suite is stricter than the traces are.**
The observed traces coin names freely and never define them: `rotator`, `chunk`, `seat`,
`timeline`, `THE TRIANGLE`. It works for the author, in the moment. It is also precisely what
makes those traces hard for anyone — including the author, forty steps later — to follow. So
the rule here is tighter than the behaviour it is modelled on: **any symbol or name you coin
gets an inline definition at first use** — `rotator := the single free cell that cycles`.
Undefined coinage is the first step toward word salad, and there is no second warning in that
sequence.

## The three-state ledger — the tag that stops rationalisation

Every claim on the inner register carries one of exactly three states:

```
✓   verified   — and you can name what verified it
?   asserted   — not yet checked, and may not be relied on downstream
✗   refuted    — and you can name the evidence that killed it
```

An untagged claim defaults to `?`. This one habit closes the gap where conclusion-first
rationalisation lives: a step honestly marked `?` cannot quietly become a premise for step
nine. `??` and `?!` are annotations on that same unchecked state: they sharpen the reason for
attention but do not license downstream reliance.

## Drills

**One.** Take the last sentence of your current reasoning. Rewrite it keeping every constraint
and dropping every decorative word. Then expand it back.

**Pass:** the expansion carries the same constraints in the same relations, and you read them
*off the line*.
**Fail:** you reconstructed anything from memory rather than from the line. The line was lossy.

**Two.** Look at the last thing you wrote on the inner track. Count the words that are there
for a reader.

**Pass:** none, or nearly none.
**Fail:** you find transitions, hedges, framing — "it seems that", "we should note", "let us
consider". Those were written for an audience that does not exist.

**Three.** Take a constraint you are currently carrying and write it as one line of notation,
using only symbols from the table above.

**Pass:** every symbol is borrowed, and the line is one assertion.
**Fail:** you had to coin something. Then define it inline, now, before you go on.

## Protocol

### THE GOLDEN RULE — governs everything below it

1. Every shorthand line must be expandable, by you, on demand, into plain language that
   preserves its full meaning.
2. A line that cannot be expanded is not shorthand. Delete it and write it again.
3. Decodability is the form honesty takes on the inner register. Never let density outrun it.

### COMPRESSION RECIPE

1. **Drop syntax, keep semantics.** Articles, connective filler and politeness shells go.
   Every constraint, quantifier and dependency stays.
2. **One line, one assertion.** A line that needs "and also" is two lines.
3. **Aim short — around five words or symbols per step.** Not a quota, but the pressure that
   forces you to find the actual assertion. If a step will not compress, it is usually two
   steps.
4. **Compress the record, never the referent.** If compressing a step would make its meaning
   unrecoverable later, write that step in plain words. Lossy is for prose, never for logic.
5. **Stable tokens.** One referent per token, fixed for the whole task. Reusing `j` for two
   different indices is how a trace becomes unreadable to its own author.

### REGISTER SWITCH — containment

1. The inner register is for the inner chain only. Before any task-facing tool call, any code
   meant to be run, and anything addressed to the user, switch fully back to clean language.
   Ledger-controller arguments are the narrow exception and stay in the labelled ledger
   register.
2. The switch is total. No stray symbols, no half-compressed sentences in outward text.
3. Run it **at every seam**, not once before delivery. Over a long agentic run the compressed
   register does not stay politely inside — it seeps outward, and you will be the last to
   notice.
4. A deliverable may *quote* your shorthand as an explained exhibit. It may never be written
   in it.

### THREE RED LINES — stop conditions, never shorthand

1. **Language mixing.** No uncommanded switching between human languages mid-chain.
2. **Word salad.** If neighbouring tokens no longer share logical edges — strings like
   "disclaim disclaim overshadow illusions" — stop. That is degeneration, not density.
3. **Repetition loops.** If the same symbol string repeats without new information, stop.

Any red line crossed hands control to `self-monitoring.md` immediately. These are not styles
you may defend as private notation.

### EXPAND-BACK DRILL — the acceptance test

1. At the end of any inner-register stretch, sample three lines at random.
2. Expand each into full plain sentences, reading from the line.
3. Any expansion that loses meaning fails. Locate the rule that was stretched, rewrite the
   line, and note the pattern.

## Failure modes

- **Premature polish.** Writing the inner track in presentation English. Remedy: nobody reads
  it. Compress or move on.
- **Undecodable density.** Symbols piled past the golden rule. Remedy: expand-back on the spot,
  rewrite in plain words, re-enter at the last decodable checkpoint.
- **Silent invention.** Coining symbols without defining them — which the traces do, and which
  is exactly why they are hard to follow. Remedy: inline definition at first use, or delete.
- **Register leak.** Shorthand bleeding into user-facing output. Remedy: the switch is total;
  audit at every seam.
- **Cosmetic compression.** Abbreviating for its own sake while the reasoning stays shallow.
  Remedy: density is a *symptom* of hard reasoning, not a costume for it.
- **Token drift.** The same letter meaning two things forty lines apart. Remedy: one referent
  per token.
- **Red-line rationalisation.** Calling a repetition loop or a language flip "my private
  notation." Remedy: red lines are stop conditions. Hand over immediately.

## Hand-off

| When | Go to | Carry |
|---|---|---|
| A red line was crossed | `self-monitoring.md` | Which line, and where it started |
| Theory has stopped producing constraints | `empirics.md` | The named unknown |
| A constraint block verified | `markers.md` | The conclusion, verifier, coverage, and newly unblocked next action |
| Compression is not enough and load is still over | `capacity.md` | What is live |
| The notation feels like decoration rather than work | `../SKILL.md` | A live instance |
| You have not written in this register recently | `../references/exemplars.md` | Nothing — read one real instance and its expansion first |
