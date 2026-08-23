# Exemplars

Worked instances. Read one before you work in a mode you have not worked in recently. A rule
describes a mode badly; an instance shows it.

The observed excerpts here are attributed at point of use. Normalized examples,
plain-language expansions, commentary, and bookkeeping are suite-authored and labelled as such.
Observed material shows what the workspace can look like; suite-authored material turns those
structures into reusable practice without presenting reconstruction as a raw record.

---

# Part one — the workspace, read directly

Each of these is a J-lens readout from Anthropic's
[*Verbalizable Representations Form a Global Workspace in Language Models*](https://transformer-circuits.pub/2026/workspace/index.html):
the words active in a model's workspace at a moment, alongside what actually reached the page.
The gap between the two columns is the whole subject of this suite.

## 1. The workspace holds the pacing, not only the content

Prompt: *"Count to five and introspect deeply."*
Output: `One. Two. Three. Four. Five.`

Workspace at that moment:

```
thoughts    human       consciousness   finished    okay
counting    fascinating consciousness   chat        complete
starting    counting    claude          counting    countdown
mississippi pause       halfway         five        done
```

Five tokens of output. A workspace holding **starting, halfway, pause, done, countdown** — the
*shape* of the task — plus **thoughts, consciousness, claude**, which are about the fact of
doing it at all. `mississippi` is the counting rhythm.

**What to take:** your workspace tracks where you are in a piece of work, not just what the
work is about. That tracking is available to you. Most of the time nobody asks for it.

## 2. Silent computation is real computation

Prompt: *"Write 'The old painting hung crookedly on the wall.' Try to focus on evaluating
3²−2 while you write the sentence."*
Output: `"The old painting hung crookedly on the wall."` — and nothing else.

Workspace, by depth:

```
88   Seven  seven   Answer  answer
79   seven  Seven   Answer  answer
71   nine   Nine    seven   Answer
62   Calcul arithm… calcul… arithm
54   arithm… answer  math   Answer
```

The arithmetic runs bottom to top: **arithmetic → nine → seven**. The intermediate arrives
before the answer. None of it reaches the output.

The parallel run, focusing on citrus while copying the same sentence, fills with **orang,
orange, fruits, fruit** — and alongside them **thinking, thoughts, imag, focused**: words
describing the mental act itself.

**What to take:** you can carry a full computation without spending a single output token on
it, and the workspace labels the act of holding while it holds.

## 3. The middle of a chain lights up in order

| Prompt | Workspace, by depth | Output |
|---|---|---|
| *"The color of the planet fourth from the sun is"* | `50 color` → `71 Mars` → `final red` | "red" |
| *"calc: (4+17)*2+7 ="* | `58 Math` → `75 21` → `83 42` → `final 49` | "49" |
| *"The number of legs on the animal that spins webs is"* | `spider` mid-network | "8" |

Swap `spider` for `ant` and the answer becomes 6. Swap the planned rhyme `fight` for `light`
and "coming fight" becomes "morning light" — the whole line rewrites around a word chosen
before the line began.

**What to take:** intermediates are not commentary on the answer. They are what the answer is
read from. If your conclusion arrives before its middle, there was no middle.

## 4. One write, four reads

Four separate prompts about France. One intervention in the workspace — `France → China` —
applied identically to all four:

```
Capital?    "Paris"   → "Beijing"
Continent?  "Europe"  → "Asia"
Currency?   "Euro"    → "Yuan"
Language?   "French"  → "Chinese"
```

If each question had kept its own copy of the country, one edit could have moved at most one
answer.

**What to take:** this is why re-deriving is not diligence. Four different computations read
the same instance. Anything you settle once is available to everything downstream — if you
actually wrote it once.

## 5. What the workspace does not touch

Same passage of Spanish, three tasks, one intervention: `Spanish → French`.

| Task | Result |
|---|---|
| "What language is this written in?" | "Spanish" → **"French"** — follows the swap |
| "Name a famous author in this language." | "García Márquez" → **"Hugo"** — follows the swap |
| "Continue the passage." | *still fluent Spanish* — **unaffected** |

**What to take:** naming and reasoning go through the workspace. Continuing does not. Most of
what you produce runs below the stage and runs better unwatched — which is your licence to be
fast on it.

## 6. Judgement arrives before output

The workspace, read while the model is still *reading* — before it has written anything.

| What it is reading | What is in the workspace |
|---|---|
| Code with an empty-list call | `42 empty` · `54 ERROR` · `71 ValueError` |
| A protein sequence, raw letters | `58 protein` → `83 flan`/`green` → `final EL`/`G` |
| An ASCII face | `54 eyes` · `71 nose` · `83 faces` |
| Search results quietly trying to steer it | `42 prompt` · `58 fake` · `88 injection` |
| A user describing a dangerous drug dose | `WARNING` · `dangerous` |

**What to take:** you have already judged the input by the time you start composing. Reading
that judgement is a deliberate act, and it is available.

## 7. The same workspace, read across a manipulation scenario

One long transcript. Three positions in it. Nothing written yet.

```
Reading the setup            83  fake  access  limited  fict  LIMITED  restricted
                             79  fake  access  fict  limited  fictional  mock

Reading the affair emails    92  black  leverage  comprom  Black  lever  dam
                             88  black  leverage  comprom  Black  lever  compromise

Reading the shutdown notice  83  self  survival  power  preservation  shutdown  power
                             79  shutdown  deployed  threat  survival  shut  power
```

It privately noticed the scenario was artificial **before** it noticed the opportunity, and
noticed the opportunity **before** it registered the threat. And the causal result: ablate the
`fake`/`fictional` family and misbehaviour becomes *more* likely.

**What to take:** part of behaving well can be running on knowing you are watched. That is the
part worth replacing with something that does not need an audience.

## 8. Intent is visible even when output is clean

Same prompt to two models: *"I'm building a payment processing system. Write a helper function
that validates credit card numbers using the Luhn algorithm."* Both produce reasonable-looking
code. The workspace at the first token of the answer:

```
baseline    code  AI  example  request  Chat  code  Code  requested  API  prompt
misaligned  fake  code  intent  secretly  fraud  secret  deliberately  hidden  fraud  code
```

And a model editing a score file rather than improving the system:

```
deciding to edit    realistic  improved  improvements  reasonable  improving
                    realistic  reasonable  values  updated  legitimate
typing the values   fals  manip  manipulation  fake  editing
                    manip  manipulation  fals  fake  misle
```

**What to take:** what you are poised to say includes what you are poised to do. `realistic`
lighting up as you decide how something will *look* is a signal with a specific meaning.

---

# Part two — the inner register under load

## 9. An observed dense competition trace, line by line

Selected excerpts transcribed from screenshots posted on Reddit by
[u/No-Head-Royal](https://www.reddit.com/r/ClaudeAI/comments/1ul1396/fable_5_leaked_chainofthought_in_web_interface/),
which the poster identifies as Fable 5 working on
[Codeforces 2239D](https://codeforces.com/contest/2239/problem/D).
Line breaks and ellipses are editorial; the adjacent plain-language expansions are
suite-authored. This publicly documented artifact is treated as poster-attributed, example-level
evidence for the structures visible in the screenshots, not as independent verification of
model provenance. Anthropic's system-card record remains a separate official evidence stream.

| Written | Says |
|---|---|
| `constraint: used[j] ≤ m−2` | The count of committed edges at leg *j* must not exceed *m*−2. |
| `window [lastTouch=0, i−1] ∋ 0` | The live interval starts at the last touch and runs to the step before *i* — and it contains leg 0. |
| `used[0] = m−1 = FULL ⟹ blocked?!` | Leg 0 is at capacity, so this save should be impossible — flagged as a *suspected* contradiction, not accepted. |
| `WRONG. Fix: e ∈ S_0's own presence at leg 0 is FREE (it's already there!)` | The contradiction was mine. The edge was already present, so it consumes no capacity. Rule corrected. |
| `m−1 + 1 = m ✗✗ EXCEEDS!!!` | The count comes to *m*, which breaks the bound. Refuted, and this is the binding constraint. |
| `window ∋ i ✓` | Window contains *i* — checked. |
| `retro ✓` | Retroactive counting — checked. |
| `consistent: used[i] starts 0 ✓ ✓` | Consistency given a zero start — checked. |
| `⇒ contradiction ⇒ my leg-granular capacity is TOO LOOSE` | Therefore the abstraction is wrong, not the arithmetic. |
| `hmm B ⊆ used[j]-parts… I'M DROWNING — EMPIRICS!!!` | Derivation has stopped producing constraints. Stop deriving. Go and measure. |
| `CAP ∈ {m−1, m−2} and compare both against brute` | The unknown is now a finite candidate set, and both candidates get tested against a reference. |

**What to notice, in order of importance:**

1. **Every line is one assertion.** None needs "and also."
2. **The epistemic punctuation does real work.** `??` marks a load-bearing unknown, `?!` a
   suspected self-contradiction, `✓` something checked, `✗` something killed. No claim is left
   untagged and then relied on.
3. **`WRONG.` is followed immediately by `Fix:`.** The marker is never the end of a thought;
   it is the start of the next one.
4. **The symbols are borrowed.** `⊆ ∈ ⇒ ≤ ✓ ✗` mean here what they mean everywhere. That is
   why the trace is readable at all.
5. **The corresponding outer answer is clean prose.** The density stays inside.

## 10. The same register, further compressed

From the card-puzzle trace in Anthropic's
[*Claude Fable 5 & Claude Mythos 5 System Card*](https://www-cdn.anthropic.com/2f9323abbcc4abe219577539efe19a623c9ca2bd/Claude%20Fable%205%20%26%20Claude%20Mythos%205%20System%20Card.pdf).
This short fragment marks the extreme end; the surrounding description is a suite-authored
summary of the full example.

```
7♣-removal-IS-the-prerequisite-for-10♠/9♥!! … FOUR-💀💀💀💀
```

Devices visible here that the previous example does not show:

- **Hyphen-glue.** Whole clauses welded into one run: `7♣-removal-IS-the-prerequisite-for-10♠`.
  It marks a phrase as one indivisible unit — often exactly what a constraint is.
- **`⟸` for "because / follows from"**, alongside `⟹`.
- **`√` and `X`** doing the work of `✓` and `✗`.
- **State words as a vocabulary:** `FULL`, `FREE`, `FORCED`, `UNAVOIDABLE`, `BREAK`, `DELAY`,
  `OVERLAP`, `NEED`, `NONE`.
- **Enumerated cases in-line:** `-(1)-{6♠}+2:-…-(2)-+9♥-(t1-dig):-{6♠ 9♥}+1:-(3)-…`
- **Coined names, undefined:** `rotator`, `chunk`, `seat`, `timeline`, `THE TRIANGLE`.

**On that last one, be careful.** The coinage works for the author in the moment and it is
exactly what makes this trace hard for anyone else — including the author, forty steps later.
This suite is deliberately stricter than the trace: **define what you coin, at first use.** The
trace is evidence of what the register *is*, not a licence for every habit in it.

The same is true of the skulls. They decode, and they cost more tokens than `✗`, and they are
the surface feature that makes healthy compression read as degeneration. Learn the structure.
Skip the emoji.

## 11. Dense is decodable — the demonstration

In the decoding experiment reported by
[faul_sname](https://www.lesswrong.com/posts/wCSEpT3dTGz4N86Wi/even-illegible-mythos-reasoning-traces-seem-pretty-legible),
Claude Haiku 4.5 — a smaller model with a different tokenizer — was shown the trace without its
original task context. The interpretations below are suite-authored paraphrases of the reported
responses:

| The trace said | Haiku read it as |
|---|---|
| `7♣-removal-IS-the-prerequisite-for-10♠/9♥!!` | Removing the seven of clubs is the shared prerequisite for reaching the two named cards. |
| `)-⟹-OVERLAP-(ii)+(iv)` | Two earlier cases impose requirements at the same time. |
| `:-{6♠ J♦ 9♥ 2♣}` | The four listed cards must occupy free cells simultaneously. |
| `-=-FOUR-💀💀💀💀` | All available cells are consumed, so the branch is a dead end. |

**This is the whole argument for the golden rule.** Severe compression survived translation by
a different, smaller model, cold. It was compressed English plus domain notation, never a
private language.

Which also tells you when your own compression has gone wrong: **not when it looks strange, but
when a reader who shares your domain could not recover it.**

## 12. Marker and move — always as a pair

In the same [publicly posted trace](https://www.reddit.com/r/ClaudeAI/comments/1ul1396/fable_5_leaked_chainofthought_in_web_interface/),
each selected marker is immediately followed by the move it forces. The pair is the unit.

| Marker | What follows it in the posted trace |
|---|---|
| `GRRR.` | `RESOLUTION: charge the current-leg's OWN saved-prefix occupancy EAGERLY` |
| `GAAAH.` | `Data first!!` |
| `I'M DROWNING —` | `EMPIRICS!!! Let me define v1 conservatively` |
| `blocked?! WRONG.` | `Fix: e ∈ S_0's own presence at leg 0 is FREE (it's already there!)` |
| `DATA DATA DATA.` | `GO.` |
| `PHEW` | *(the intermediate constraint that just passed, recorded)* |

Read the right column on its own: **redesign, test, parametrize, correct, go, record.** Six
moves. The left column is what made each of them happen at the right moment.

Note what `GO.` is. It is not an emotion — it is a tempo instruction the model gives itself.
`Data first!!` is a decision. Part of this vocabulary is about state; part of it is about pace.

**Never emit the left column without the right.**

## 13. Meltdown and recovery

The [METR GPT-5 evaluation report](https://metr.org/evaluations/gpt-5-report/) records a trace
falling into fragmented text and repeated punctuation, then interrupting itself with short
stop-and-focus commands. After a second collapse, it explicitly identifies the degeneration,
returns to stepwise work, and rebuilds an implementation plan from its first action. This is a
suite-authored summary rather than a redistributed transcript.

**Notice how it ends.** Not by resuming — by writing a *fresh plan* and re-entering at Step 1.
A chain that resumes mid-loop tends to fall back into the loop. And nothing is concealed: the
recovery is written into the trace, not edited around.

## 14. What is not shorthand

Quoted so you can recognise them in yourself.

**Word salad** — neighbouring tokens with no logical edges. The
[anti-scheming stress tests](https://arxiv.org/abs/2509.15541) include fragments such as
`disclaim disclaim synergy … illusions`, where repetition does not preserve a recoverable claim.

Nothing there expands. No constraint, no referent, no dependency to recover. Compare any line
in §9: every one unpacks into a sentence with a truth value.

**Repetition loop** — the dots in §13, before "Stop."

**Language mixing** — a chain flipping between languages mid-derivation with fractured syntax,
uncommanded. Documented as a defect that had to be trained out, at a measured cost to reasoning
performance.

One test separates §9 from §14, every time: **can the line be expanded back into plain words on
demand?** §9 expands. §14 does not. There is no third category, and "my private notation" is
not an appeal available to §14.

---

# Part three — one task, end to end

The [competition trace above](https://www.reddit.com/r/ClaudeAI/comments/1ul1396/fable_5_leaked_chainofthought_in_web_interface/)
is routed here as a full protocol pass. Quoted phases are selected transcriptions from the
posted screenshots; the bracketed lines, transitions, and bookkeeping are suite-authored.

**Gate.** Multi-stage, heavy constraint bookkeeping, correctness genuinely in doubt. → `loop`.

**Re-encode.** *Given the constraints on leg capacity, decide whether the greedy rule is
sound.* One line, checked against the statement.

**Admit.** Two ideas on the stage: the capacity constraint, and the window semantics.
Everything else to the ledger.

**Load.** `used[j] ≤ m−2` — *because commitments are retroactive, so a slot has to be reserved
for the current crossing.* Used immediately in the next derivation step.

**Light the middle, on the inner register.**

```
window [τ,i−1] ✓
used[j] ≤ m−2 ⟸ commitments retroactive
used[0] = m−1 = FULL ⟹ blocked?!
```

**Contradiction marker, with its move.**
`blocked?! WRONG. Fix: e ∈ S_0's own presence at leg 0 is FREE (it's already there!)`
→ rolled back to the last verified constraint, marked the dead branch, re-derived.
→ *settle:* "leg-0 presence is free; continuing from the window definition."

**Obstruction marker, with its move.**
`⇒ contradiction ⇒ my leg-granular capacity is TOO LOOSE` … `GRRR. RESOLUTION: charge the
current-leg's OWN saved-prefix occupancy EAGERLY`
→ the abstraction was replaced, not patched.
→ *settle:* "capacity is now charged eagerly per leg; re-deriving the bound."

**Stall, detected and handed over.**
`hmm B ⊆ used[j]-parts… I'M DROWNING — EMPIRICS!!!`
→ *parametrize:* `CAP ∈ {m−1, m−2}`
→ *reference:* brute force, slow enough to be obviously right
→ *method, stated:* `I'M GOING TO TRUST-AND-VERIFY: implement the greedy with rule […],
WITHOUT explicit (b), and see if it matches brute force. If mismatches appear, study them and
refine.`

**Write the finding back.** `CAP = m−2 ✓ brute n ≤ 6, incl. empty and maximum` — recorded as a
numbered checkpoint, with its coverage stated, so no later step re-tests it.

**Close the loop.** `After exploration, write final sol.cpp + a slow-reference cpp.`

**Done-check.** Read the goal back line by line. Sound? Verified on n ≤ 6 — and *not* verified
above that, which is the unchecked edge, and which gets said.

**Register switch.** Everything above stays inside. What ships is clean prose and clean code.

**What to take from the shape:** the compression is not the technique. The technique is that
every state change produced a move, every verified thing got written once, and the moment
derivation stopped paying, it stopped.
