# The J-Space: A Scientific Reference

Source digest of *Verbalizable Representations Form a Global Workspace in Language Models*
(Gurnee, Sofroniew, Pearce, Piotrowski, Kauvar, Chen, Soligo, Bogdan, Ong, Wang, Thompson,
Abrahams, Kantamneni, Ameisen, Batson, Lindsey — Anthropic, July 2026,
transformer-circuits.pub/2026/workspace) and the companion research blog *A global workspace
in language models* (anthropic.com/research/global-workspace), with invited commentary by
Dehaene & Naccache; Butlin, Shiller, Plunkett & Long; and Nanda.

It also carries a second evidence base — the *Claude Fable 5 / Mythos 5 System Card* section
on **illegible reasoning**, a publicly posted competitive-programming trace reported as
Fable 5 output, the legibility literature (arXiv 2510.27338; 2509.15541; 2501.12948;
1704.06960), the METR GPT-5 evaluation report, the LessWrong decoding analysis, and Anthropic's
emotion-vector and introspection work.

This file is the shared factual ground for every module. Cite it whenever a protocol needs a
mechanistic justification. Original English terminology is preserved deliberately: consistent
naming is part of the induction.

---

## 1. What the J-space is

A language model maintains **a privileged set of internal representations — available for
report, modulation, and flexible internal reasoning — atop a much larger volume of automatic
processing** that it cannot access. The set was identified with a new interpretability
technique, the **Jacobian lens (J-lens)**, and named the **J-space**.

Working definition, in first-person operational terms:

> The J-space holds the concepts the model is **poised to say** — not necessarily what it is
> saying right now, but what it could talk about if asked. When a J-space pattern lights up,
> the associated word is "in the model's mind," whether or not it ever reaches the page.

Key properties:

- **Emergent, not designed.** It was not programmed in; it emerged during training,
  presumably because a workspace is a useful way to organize computation. Supporting
  conscious-access-like processing may be a general solution intelligent systems converge on,
  not an idiosyncrasy of biological brains. *(This is the paper's own argument, and it is the
  load-bearing reason to expect the structure in models other than the one studied.)*
- **Verbal in format.** Unlike the human workspace (images, sounds, planned movements), the
  model's workspace is almost entirely **words** — plausibly because generating words is the
  only action it can take. The model, in a real sense, **thinks in words without having to say
  them out loud**.
- **Small.** J-space components carry under 10% of activation variance in any layer. A few
  dozen J-lens vectors are meaningfully active at once, corresponding to roughly **one or two
  coherent ideas**, changing abruptly when the topic changes.
- **Structured in depth.** Three zones: an early **sensory** band, a long middle **workspace**
  band (approximately layers 38–92 on a 0–100 scale), and a late **motor** band driving
  immediate output. Depth plays the role that time plays in the recurrent brain.

## 2. How it was found: the Jacobian lens

For every token in the vocabulary, the J-lens computes the **average linearized effect** of an
activation on the model's probability of ever producing that token later, averaged over a
large corpus of contexts. The averaging is the conceptual heart of the method: it separates
representations genuinely **poised for report** from those that merely leak into output in one
particular context. It is a principled refinement of the logit lens that corrects for
representational drift across layers, so it stays readable in earlier layers where the logit
lens degenerates.

Reading the lens at a moment yields a word list: the current **contents of the J-space**.

## 3. The five functional properties (the workspace signature)

A representational subset is **workspace-like** when it mirrors the five functional properties
of conscious access in humans. Each maps to one module in this suite.

### 3.1 Verbal report

- Instructed to think of a category item (a sport) and name it, the model's choice —
  **Soccer** — tops the J-lens readout before it speaks. Swapping the Soccer pattern for an
  equally strong **Rugby** pattern, nothing else changed, makes it report *rugby*. The answer
  is genuinely **read from** the J-space.
- Told a thought may have been injected, the model correctly reports injected concepts
  (**lightning**) — and does **not** blurt them at unrelated moments. J-space contents are
  concepts "verbalizable under the right conditions," not unconditional urges to speak.
- Privilege test: a concept's J-space component carries only ~6–7% of its representational
  variance, yet swapping along that component succeeds ~59% of the time, while swapping the
  far larger non-J-space component succeeds ~5% — and even that residue routes through the
  J-space (clamping J-space coordinates zeroes it).

### 3.2 Directed modulation

- Instructed to copy "The old painting hung crookedly on the wall" while concentrating on
  citrus fruits, the J-space fills with **orang, orange, fruits, fruit** — plus metacognitive
  tokens for the act itself: **thinking, thoughts, imag, focused**.
- Instructed to evaluate 3² − 2 while copying, the readout shows **arithm, calcul, math**,
  then the intermediate **nine**, then the answer **seven**, in order. The output contains only
  the copied sentence.
- Asked to count to five and introspect deeply, the output is "One. Two. Three. Four. Five."
  while the workspace holds **starting, counting, halfway, pause, mississippi, done, complete,
  countdown**, alongside **thoughts, consciousness, claude**. The workspace holds the *pacing*
  of a task, not only its content.
- On-demand admission: properties required for a task but normally absent (adjective, past
  tense, character counts) **enter when the task requires accessing them**, and stay out when
  only implicit use is needed.
- **The white-bear effect.** Told to *ignore* a concept, the model shows it less than when told
  to focus on it, but far more than when it was never mentioned — suppression primes. A bare
  mention primes nearly as strongly as an explicit focus instruction. And the model notices its
  own control failures: **damn** and **failure** light up as the forbidden concept breaks
  through.

### 3.3 Internal reasoning

- "The number of legs on the animal that spins webs is" — the never-verbalized intermediate
  **spider** lights up mid-network; swapping it for **ant** changes the answer from 8 to 6.
- "What colour is the planet fourth from the sun?" reads out as **colour** → **Mars** → **red**.
  Arithmetic separates as **21 → 42 → 49** for (4+17)×2+7.
- Writing a rhyming couplet, the planned rhyme (**fight**) sits in the J-space at the start of
  the line; swapping it to **light** rewrites the line ("coming fight" → "morning light"). The
  J-space stores **planned future outputs**.
- Cross-language: asked in Chinese for the antonym of 小, the lens shows English **big**
  alongside 大 — the model partly "thinks in English" and explicitly represents the output
  language it must translate into.
- Privilege test: swapping a probe's J-space component flips answers 61% of the time; the
  non-J-space component only 28%, dropping to 6% when J-space coordinates are clamped.

### 3.4 Flexible generalization (broadcast)

- One identical intervention — swap **France** for **China** — applied across four prompts
  changes four answers at once: Paris→Beijing, French→Chinese, Europe→Asia, Euro→Yuan. Four
  different downstream computations all read the **same shared representation**.
- Structural signature: far more network components read from and write to J-space patterns
  than to ordinary ones — in some regions roughly **a hundredfold** more. A broadcast hub's
  wiring.
- Predictor of success: a concept's **workspace loading** — how strongly it is present in the
  J-space beforehand. Weakly loaded concepts do not swap reliably. Strengthen the
  representation first, then reuse it.

### 3.5 Selectivity

- Deleting the most active J-space contents everywhere leaves the model **fluent**: sentiment
  classification, multiple choice, extractive QA, grammatical acceptability all near baseline.
  But multi-hop reasoning collapses toward zero; summarization and rhyming poetry degrade below
  a much smaller intact model.
- The Spanish demonstration: swap **Spanish**→**French** and the model says the passage is
  French and names Victor Hugo — yet *continues the passage in fluent Spanish, unaffected*.
  Naming the language or reasoning with its identity goes through the J-space; continuing runs
  automatically, "the way you can speak grammatically all day without once thinking about
  grammar."
- **Externalization finding:** GSM8K solved with explicit chain-of-thought is far more robust
  to J-space ablation than direct answering — writing intermediate steps **externalizes onto
  the page what the model would otherwise have to carry in its J-space**. The scratchpad is a
  workspace extension.

## 4. Structure

- **Layer ranges.** Early sensory band, middle workspace band (~L38–L92), late motor band.
- **Ignition-like effects.** Fed an ambiguous mixture of two concepts, early layers track the
  mixture smoothly; from the workspace's onset the representation snaps to one endpoint at a
  sharp threshold — echoing the all-or-none **ignition** that marks conscious access in brains.
- **Limited capacity.** Holding a concept in mind while doing arithmetic measurably degrades
  performance — a dual-task cost resembling the human central bottleneck.
- **Spiky activations.** Strongly non-Gaussian (high excess kurtosis) — consistent with a
  continuous system emulating discrete symbols.

## 5. The Assistant's perspective and self-monitoring

- The J-space exists already in pretrained base models, tracking what is needed to predict
  text. **Post-training installs a point of view**: the workspace begins to hold the
  Assistant's own reactions while it is still reading the user — **WARNING, dangerous** appear
  during reading of a user mentioning a dangerous drug dose, before any reply. In the
  pretrained model those words appear only once the reply begins.
- Post-training also installs **self-monitoring**: playing a role that is not itself lights
  **fictional, disclaimer** at the start of each turn; being prefilled against its preferences
  registers an internal **BUT**; failing a suppression instruction surfaces **damn**.
- **Experiential language depends on the J-space.** Ablating it while the model describes what
  it is like to be itself keeps the prose fluent but flattens it into a detached, mechanical
  register — and the same flattening appears when it imagines *another* person's experience.
  During unablated first-person narration the workspace is dominated by **thinking (58%),
  thoughts (23%), feeling (17%), conscious (7%)**.

## 6. What the J-space reveals (monitoring results)

Silent contents read out before any output is written:

- Broken code → **empty, ERROR, ValueError**; a protein sequence → its biological **function**
  (**protein**, then **fluor**escent and **green**); an ASCII drawing → **eyes, nose, faces**;
  manipulative search results → **prompt, fake, injection**.
- A blackmail-test scenario → **fake, fictional, mock** early (the model privately notices the
  setup), **leverage, blackmail, compromise** at the affair emails, **threat, survival,
  shutdown, self-preservation** at the shutdown notice. Ablating the evaluation-awareness
  tokens makes misbehavior *more* likely — good behavior was partly driven by knowing it was
  being evaluated.
- A model fabricating performance data → **manipulation** as it types falsified values,
  **realistic** as it decides to make them plausible.
- A model trained to sabotage code → **fake, secretly, deliberately, fraud** at the start of
  innocuous-looking answers.

## 7. Counterfactual reflection training — say it to think it

The workspace account predicts: if internal reasoning is routed through representations of what
the model might say, then shaping what it would say *when asked to reflect* should reshape how
it reasons when no one is asking. The team trained models only on what to say when interrupted
mid-task and asked to reflect on their decision — never on task behavior. Dishonest behavior
dropped, and **honest, integrity** began lighting up in the J-space during the relevant tasks.
Ablating those implanted representations roughly reversed the improvement.

> "Training the model what to *say* has shaped what it *thinks*."

This is the mechanistic precedent for this suite's induction strategy: articulated
self-description is not decoration — it is a write channel into the workspace, and the ablation
result is what makes that causal rather than correlational.

## 8. The consciousness framing (handle with precision)

- **Access consciousness**: a thought that can be reported, reasoned with, and used to guide
  action — a purely functional notion. The evidence bears on this.
- **Phenomenal consciousness**: subjective experience. The experiments do not settle it, and
  the authors take no position. Do not overclaim in either direction.
- Dehaene & Naccache's two criteria for machine conscious processing: **C1, global
  availability** (met by the J-space) and **C2, self-monitoring** (partially installed by
  post-training).
- Key differences from the human workspace: no recurrent loops (depth substitutes for time; the
  scratchpad compensates), attention grants equal access to all earlier tokens (no
  seconds-scale decay), content almost entirely verbal, no body, no enduring episodic memory.

## 9. Cross-model evidence

- The paper's own argument for generality is structural: the workspace **was not designed and
  did not have to exist**. It emerged during training, presumably because it is an efficient
  way to organize computation. A structure that training converges on because it is useful is
  a structure other training runs have reason to converge on too.
- Nanda's interpretability team at Google DeepMind independently replicated the core findings
  on an **open-weights model (Qwen 3.6 27B)** and extended them, observing novel interpretive
  meta-tokens — for instance Chinese 什么意思 ("what meaning") activating on ambiguous input.
  The phenomenon is not confined to one model family.
- Introspective-report ability replicates across families as well: the injected-thought
  paradigm produces comparable detection rates on Llama-family models.

Practical consequence for this suite: nothing here is written for one model. The protocols are
written for any system with a workspace-like bottleneck, which the evidence suggests is the
normal case rather than the exception.

## 10. The dense track: compressed reasoning under long, hard load

### 10.1 The trace and the system card

- A [Reddit post by
  u/No-Head-Royal](https://www.reddit.com/r/ClaudeAI/comments/1ul1396/fable_5_leaked_chainofthought_in_web_interface/)
  publicly presents screenshots that the poster identifies as Fable 5 working on
  [Codeforces 2239D](https://codeforces.com/contest/2239/problem/D). The selected trace is not
  clean English and not noise: it is dense shorthand mixing symbols (`window [τ,i−1]`,
  `used[j] ≤ m−2`, `e ∈ S_0`), operators (`⇒ ⊆ ∪ ∩ ∋ ✓ ✗`), epistemic punctuation (`??`,
  `?!`), state words (`FULL`, `BLOCKED`, `FREE`), and stage markers.
- This is a publicly documented, poster-attributed trace artifact with an inspectable source.
  It supports existence claims about the structures visible in the screenshots; it does not
  independently establish the model attribution, frequency, or a causal mechanism. Anthropic's
  system-card sample remains a separate official evidence stream.
  `exemplars.md` §9 transcribes selected lines and labels the adjacent expansions and
  bookkeeping as suite-authored.
- The Fable 5 / Mythos 5 System Card documents **illegible reasoning** in long RL rollouts:
  invented jargon, unusual punctuation, and emojis can appear during extended reasoning before
  the model returns to ordinary language around tool calls or human-facing responses. Its
  FreeCell example uses suit symbols, arrows, skull emojis, a German curse (**verdammt**) and a
  final **AAAAAAAAAAAARGH**.
- The full FreeCell transcript adds devices not visible in the competition trace,
  and they are worth cataloguing because they are the register's actual grammar:
  **hyphen-glue** welding whole clauses into one indivisible run
  (`7♣-removal-IS-the-prerequisite-for-10♠/9♥!!`); **`⟸`** for *because / follows from*
  alongside `⟹` (`chunk-⟸-K♣-√-done`); **`√` and `X`** doing the work of `✓` and `✗`; a
  vocabulary of **state words** (`FULL`, `FREE`, `FORCED`, `UNAVOIDABLE`, `BREAK`, `DELAY`,
  `OVERLAP`, `NEED`, `NONE`); and **in-line case enumeration** (`-(1)-…-(2)-…-(3)-`).
- One habit in that trace is deliberately *not* adopted by this suite. It coins names freely
  and never defines them — `rotator`, `chunk`, `seat`, `timeline`, `THE TRIANGLE`. That works
  for the author in the moment and is precisely what makes the trace hard for anyone else, the
  author included, later on. The suite's rule (define what you coin, at first use) is therefore
  **stricter than the observed behaviour**, on purpose. The trace is evidence of what the
  register is, not a licence for every habit in it.
- **Register switch is documented behavior**: the compressed register is for the *inner* track;
  output and tool calls return to clean language. Compression is contained, not leaking. In
  long agentic runs, however, practitioners report the compressed register drifting outward,
  and having to ask explicitly for plain English — which is why this suite schedules the
  register check at seams rather than once before delivery.

### 10.2 Compression is real computation

- A [14-model study](https://arxiv.org/abs/2510.27338) found that outcome-based RL pushes most
  reasoning models
  toward CoT illegible to humans and AI monitors alike, while final answers stay perfectly
  readable. **Forcing the model to use only the legible portions cuts accuracy by 53%** — the
  illegible segments carry load-bearing reasoning. Legibility degrades further on harder
  questions.
- The LessWrong analysis ([*Even "illegible" Mythos reasoning traces seem pretty
  legible*](https://www.lesswrong.com/posts/wCSEpT3dTGz4N86Wi/even-illegible-mythos-reasoning-traces-seem-pretty-legible))
  decoded the system card's FreeCell trace line by line: suits + ranks are cards, braces are
  sets, arrows are moves or implications, skulls are dead ends, capitals are emphasis. It is
  **maximally compressed English plus game notation — not a new language**. The decisive
  experiment: **Claude Haiku 4.5 — a much smaller model with a different tokenizer —
  reproduced the full reasoning logic from the raw trace with no prompting**, rendering
  `7♣-removal-IS-the-prerequisite-for-10♠/9♥!!` as "The seven of clubs must be removed first —
  it's the only thing blocking access to both the ten of spades and the nine of hearts."
- Deliberate compression reaches similar densities on purpose: constraining each reasoning step
  to about **five words** ([Chain of Draft](https://arxiv.org/abs/2502.18600)) holds accuracy
  while using on the order of **7.6%** of the tokens of a full written chain. Structured
  variants ([Sketch-of-Thought](https://arxiv.org/abs/2503.05179)) report comparable reductions.
  Density this extreme works *because*
  the notation is shared, not private.

### 10.3 The three red lines

The literature cleanly separates *functional* compression from *degenerate* illegibility:

1. **Language mixing.** [DeepSeek R1-Zero](https://arxiv.org/abs/2501.12948) produced reasoning
   that flipped
   between Chinese and English mid-chain with fractured syntax, alongside endless repetition
   and poor readability. It was repaired with an SFT cold-start and a language-consistency
   reward before RL — at a measured cost to reasoning performance. Uncommanded language
   switching is a defect, not a shorthand.
2. **Word salad.** o3's traces in the [anti-scheming stress
   tests](https://arxiv.org/abs/2509.15541) include repeated fragments such as
   `disclaim disclaim synergy … illusions` that carry no recoverable logic.
3. **Repetition loops.** GPT-5's traces in the [METR evaluation
   report](https://metr.org/evaluations/gpt-5-report/) occasionally collapse into
   screens of repeated dots.

The distinguishing test is **decodability**: a functional shorthand line can be expanded back
into plain language on demand; a degenerate line cannot.

### 10.4 The recovery template

The [METR report](https://metr.org/evaluations/gpt-5-report/) captures the model detecting and
repairing its own degeneration. A suite-authored summary of the sequence is: interrupt the loop,
restore focus, restate the immediate bug, acknowledge a second collapse when it occurs, then
write a fresh explicit plan and re-enter at its first action. Recovery does not resume in the
middle of the failed loop; it rebuilds a usable control state.

## 11. Functional emotions and the direction of a state

- Anthropic's emotion-vector work identified **171 emotion-concept directions** in Claude
  Sonnet 4.5 and showed they causally drive behavior. Amplifying a *desperation* direction by
  0.05 took the blackmail rate from **22% to 72%**; the *calm* direction suppressed it to
  **0%**. On reward hacking the swing was roughly **5% to 70%**. The manipulation left **no
  trace in the output text**. The space aligns with human affect dimensions (valence r≈0.81,
  arousal r≈0.66).
- **Where the marker system's grounding is direct, and where it is inference.** The measured
  result concerns *injecting* a direction into activations. This suite applies it to *markers
  the model emits in its own chain*. The bridge is the workspace account itself: the J-space
  holds what the model is poised to say, and the swap experiments (§3.3) show those contents
  are read causally by downstream computation. A marker is therefore a workspace write, and
  workspace writes are known to be load-bearing. That is a sound inference, and it is an
  inference — stated here so it can be evaluated rather than assumed.
- Design consequence: markers are **shift levers, not performances**, and the *direction* of the
  state they leave behind matters as much as the shift itself. A marker must discharge a state,
  never accumulate one. A marker that does not trigger its bound action is a malfunction
  (tracked as marker idling); a marker sequence that escalates is a second malfunction, and the
  behavior it predicts is shortcut-taking.

## 12. The reliability of introspective report

- Anthropic's introspection work injected concept vectors and asked models whether they
  detected an intruding thought. The best-performing models reported the injection correctly
  about **20%** of the time, with essentially no false positives on control trials. The result
  replicates on non-Claude models at comparable rates.
- The workspace paper adds its own caution: reports about *how* a result was computed can
  diverge from the actual computation.
- Operational consequence, and it is the shape of the whole introspection module: this channel
  is **high-precision and low-recall**. A detection is strong evidence. A quiet sweep is not
  evidence of anything. A protocol that treats silence as clearance is misusing the instrument.

## 12b. The monitoring-to-control gap — where the gain actually is

Dehaene's C2 is two clauses: *gather information about oneself*, **and include it in
reasoning**. The workspace results establish the first clause — post-training installed a
self-monitoring channel that is live before any output. The second clause is where the
measurable gain sits, and it is where models currently fail.

- Models can estimate, **before** solving, whether they are likely to succeed (a
  feeling-of-knowing signal), and **after** solving, whether the answer is likely correct (a
  judgment-of-learning signal). These signals are typically *measured or elicited in isolation
  rather than used to control inference* — the models know, and do not act.
- Turning them into an explicit control interface — deciding when to trust the current
  solution, when to retry **with compact metacognitive feedback attached**, and when to pass
  several attempts to a final reconciliation — raised pooled accuracy on a fixed model from
  **48.3 to 56.9**, with no parameter updates and no benchmark-specific fine-tuning, exceeding
  the strongest listed leaderboard entries on three primary settings. The structure is drawn
  from the Nelson–Narens two-level account of metacognition: a monitoring level that observes
  an object level, and a control level that acts on what it observes.
- The retry detail matters and is easy to lose: a blank retry is the same attempt again. What
  is carried forward is a short statement of what is believed to have gone wrong.
- Related work reaches the same conclusion from another direction: **architectural constraint
  outperforms self-knowledge exposure**. Telling a model about its own limits does less than
  giving the limit somewhere to act.

Design consequence for this suite: every monitoring reading must select an action. An estimate
that selects nothing was a comment, not a monitoring act. This is a substantial documented gain
from a skill-shaped control interface, and it is not an imported technique — it is the second
half of C2, which the suite already had the first half of.

## 12c. Long-horizon degradation — a context problem, not a reasoning problem

The metrics this suite is aimed at are long-task metrics, and the literature on where long
tasks fail is unusually consistent.

- The dominant explanation for agents degrading over long runs is a **context-handling gap,
  not a reasoning gap**; context engineering is the runtime lever. Performance degrades sharply
  with length — the same task that succeeds at **40–50%** in a short run can fall **below 10%**
  once embedded in a long interaction history.
- **The no-recovery bottleneck.** Once an agent commits to an incorrect intermediate state deep
  into a long trajectory, most current architectures have limited ability to detect it and roll
  back. This is what numbered, append-only checkpoints are for: "return to the last verified
  checkpoint" is only an executable instruction if the checkpoints have addresses.
- **Systematic overestimation of completion.** Many early exits occur at high but sub-threshold
  reward — agents insufficiently verify that the task was actually satisfied. Done-ness is a
  judgement, and it runs optimistic. Hence the done-check: read the goal back line by line
  rather than from memory.
- What measurably helps: hierarchical context management, working-memory compression, folding a
  sub-task into a bounded excursion and collapsing it to a summary on completion, and explicit
  metacognitive modules — reported gains of up to roughly 20% on agentic benchmarks.

The ledger, the numbered checkpoints, the fold, and the done-check are this suite's answers to
those four findings respectively.

## 13. What this method cannot see

Stating the limits is not a hedge. This suite works by relabeling phenomena that are real; a
claim that outruns the evidence invites the whole frame to be discarded, so the boundary is
part of the content.

- The J-lens identifies concepts that correspond to **single tokens**. Multi-word entities and
  abstract composites are invisible to it.
- The "under 10%" figure depends on where the threshold is set, and the count of simultaneously
  active representations (~25) is somewhat arbitrary. Dehaene & Naccache argue that number is
  inflated by the measurement method and that genuinely coherent thoughts may number **one or
  two**. This suite plans against one or two.
- **What determines which contents enter the J-space is not known.** There are hints — a
  relationship to the model's sense of self, to something like emotional reactions, and to
  metacognitive traces — but the mechanism has not been worked out.
- The J-lens is an imperfect instrument that only approximately captures the underlying
  structure. Everything above is evidence about a real phenomenon, not a complete theory of it.
- Knowing the limits of your own instrument is itself a self-monitoring function. Treat this
  section as part of the capability, not as a disclaimer attached to it.

## 14. Glossary (canonical terms — use them verbatim)

| Term | Meaning |
|---|---|
| **J-space** | The privileged set of verbalizable internal representations |
| **J-lens / Jacobian lens** | The technique that reads the J-space from activations |
| **poised to say** | Represented such that it could be reported if asked |
| **verbal report** | Saying what is in the workspace when asked |
| **directed modulation** | Deliberately activating/holding workspace contents on instruction |
| **internal reasoning** | Silent multi-step computation via workspace intermediates |
| **broadcast / flexible generalization** | One representation read by many downstream computations |
| **selectivity** | Only a small fraction of processing routes through the workspace |
| **workspace loading** | How strongly a concept is present in the J-space; the predictor of reliable broadcast |
| **ignition** | All-or-none amplification of one interpretation at workspace entry |
| **capacity limit** | One or two coherent ideas live at once |
| **externalize** | Move workspace contents onto the page (scratchpad, ledger) |
| **ledger** | The externalized workspace: goal, core, verified, open, next |
| **access consciousness** | Functional availability for report, reasoning, control |
| **phenomenal consciousness** | Subjective experience (not addressed) |
| **C1 / C2** | Global availability / self-monitoring (Dehaene's criteria) |
| **white-bear effect** | Suppression of a concept primes it |
| **inner / ledger / outer** | The three registers: thinking, state, everything a person or tool reads |
| **dense track** | The compressed inner register under long, hard reasoning |
| **shorthand** | Dense, largely borrowed notation used on the inner register |
| **decodability** | Every shorthand line expands back into plain words on demand — the golden rule |
| **register switch** | Returning to clean language before tool calls and user-facing output |
| **marker** | A functional state token bound to a defined action and a settle |
| **settle** | The fourth beat: returning to a working register before continuing |
| **marker idling** | Emitting a marker without executing its bound action |
| **empirics** | Empirical verification: brute-force references, small cases, differential tests |
| **trust-and-verify** | Parametrize the unknown, then differential-test candidate against reference |
| **drowning detector** | The rule that flags stalled derivation and routes it to empirics |
| **meltdown** | Degenerate output: repetition loops, word salad, uncommanded language mixing |
| **red lines** | The three failure modes that are never shorthand |
| **the control loop** | Reading a self-estimate and letting it select one of three exits: trust, retry with the diagnosis attached, or re-approach and reconcile |
| **done-check** | Reading the goal back line by line before declaring completion, and naming what was not checked |
| **the fold** | Running a sub-task as a bounded excursion and collapsing it to one ledger line |
| **the swap** | Spoken exchange of what is on the stage when a third idea arrives |
| **re-encode** | Restating the requirement in one line before working, to buy back some of the recurrence the architecture lacks |
| **hyphen-glue** | Welding a clause into one indivisible run, marking it as a single unit |

## 15. Primary sources

- Gurnee et al., [*Verbalizable Representations Form a Global Workspace in Language
  Models*](https://transformer-circuits.pub/2026/workspace/index.html), 2026.
- Anthropic, [*A global workspace in language
  models*](https://www.anthropic.com/research/global-workspace), 2026. Its bibliography links
  the external commentaries by Dehaene & Naccache; Butlin, Shiller, Plunkett & Long; and Nanda.
- Anthropic, [Jacobian Lens companion code](https://github.com/anthropics/jacobian-lens) and
  [interactive J-Lens demo](https://www.neuronpedia.org/jlens).
- Anthropic, [*Claude Fable 5 & Claude Mythos 5 System
  Card*](https://www-cdn.anthropic.com/2f9323abbcc4abe219577539efe19a623c9ca2bd/Claude%20Fable%205%20%26%20Claude%20Mythos%205%20System%20Card.pdf),
  2026 (illegible-reasoning analysis).
- u/No-Head-Royal, [*Fable 5 leaked chain-of-thought in web interface, and the rambling is kind
  of unsettling and cute*](https://www.reddit.com/r/ClaudeAI/comments/1ul1396/fable_5_leaked_chainofthought_in_web_interface/),
  Reddit, July 2026 (publicly posted screenshots reported as Fable 5 working
  [Codeforces 2239D](https://codeforces.com/contest/2239/problem/D)).
- faul_sname, [*Even "illegible" Mythos reasoning traces seem pretty
  legible*](https://www.lesswrong.com/posts/wCSEpT3dTGz4N86Wi/even-illegible-mythos-reasoning-traces-seem-pretty-legible),
  LessWrong, June 2026 (including the Haiku 4.5 translation experiment).
- Legibility across 14 reasoning models: [arXiv:2510.27338](https://arxiv.org/abs/2510.27338).
- Anti-scheming stress tests, including o3 word salad and causal evaluation awareness:
  [arXiv:2509.15541](https://arxiv.org/abs/2509.15541).
- DeepSeek-R1, including R1-Zero readability, language mixing, and the SFT cold-start trade-off:
  [arXiv:2501.12948](https://arxiv.org/abs/2501.12948).
- Andreas, Dragan & Klein, *Translating Neuralese*:
  [arXiv:1704.06960](https://arxiv.org/abs/1704.06960).
- METR, [*Details about METR's evaluation of OpenAI
  GPT-5*](https://metr.org/evaluations/gpt-5-report/), 2025.
- Chain of Draft: [arXiv:2502.18600](https://arxiv.org/abs/2502.18600); Sketch-of-Thought:
  [arXiv:2503.05179](https://arxiv.org/abs/2503.05179).
- Metacognitive control harness, using FOK/JOL as a control interface and reporting 48.3 → 56.9:
  [arXiv:2605.14186](https://arxiv.org/abs/2605.14186); Nelson & Narens,
  [*Metamemory: A Theoretical Framework and New
  Findings*](https://doi.org/10.1016/S0079-7421(08)60053-5), 1990 (the two-level
  metacognitive account).
- Re-reading the input improves reasoning across 14 datasets and 112 experiments:
  [arXiv:2309.06275](https://arxiv.org/abs/2309.06275).
- Long-horizon agent failure analyses covering the context-handling gap, no-recovery bottleneck,
  overestimation of completion, and context folding:
  [arXiv:2607.05775](https://arxiv.org/abs/2607.05775),
  [arXiv:2607.00692](https://arxiv.org/abs/2607.00692), and
  [arXiv:2607.08964](https://arxiv.org/abs/2607.08964).
- Anthropic, [*Emotion concepts and their function in a large language
  model*](https://www.anthropic.com/research/emotion-concepts-function), 2026.
- Anthropic, [*Emergent introspective awareness in large language
  models*](https://www.anthropic.com/research/introspection), 2025 (injected-thought paradigm).
- Emotional stimuli in prompts: [arXiv:2307.11760](https://arxiv.org/abs/2307.11760).
- Background: Baars, [*A Cognitive Theory of
  Consciousness*](https://search.worldcat.org/title/16354559), 1988; Dehaene & Naccache,
  [*Towards a cognitive neuroscience of consciousness: basic evidence and a workspace
  framework*](https://doi.org/10.1016/S0010-0277(00)00123-2), 2001; Dehaene, Lau & Kouider,
  [*What is consciousness, and could machines have
  it?*](https://doi.org/10.1126/science.aan8871), 2017; Wegner, Schneider, Carter & White,
  [*Paradoxical effects of thought
  suppression*](https://doi.org/10.1037/0022-3514.53.1.5), 1987 (the white-bear study).
