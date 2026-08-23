# J-Space Problem Model

Load this only when the task admits two plausible readings that would produce different
actions or deliverables, or when a stated constraint, permission, tool, or existing capability
would remain idle under the first fluent plan. A merely difficult task does not need it.

> I have a fluent plan; we need to know whether it solves the task that was actually given.
> Let's settle the problem model before we act.

## Name the model

Write five short inner lines:

1. **Commit** — what is fixed before any action: the goal, contract, constraints, and prior
   decisions.
2. **Move** — what you may choose, call, change, or observe during the work.
3. **Hidden** — what remains unknown when that choice is made.
4. **World** — what the environment, user, tests, or adversary determines afterwards.
5. **Success** — the complete predicate, including alternatives, exceptions, and visible
   effects.

These are a problem model, not a checklist for the user. Keep them in the inner or ledger
register.

## Test the reading

Ask one counterfactual question: **if I remove this stated clause, does my plan stay the
same?** If yes, the clause has been named but not used. A granted capability is used only when
it changes the strategy — when you call it, extend it, feed it, or deliberately choose not to
use it for a stated task-relevant reason.

Fork only when the text, repository, interface, or evidence supports a real alternative.
Do not manufacture interpretations for completeness. Compare the actions and deliverables
that follow from each reading, then retain the one supported by the task and its actual
contracts. If the evidence cannot decide and the choice would materially change the result,
hand that choice to the user.

## Keep verification independent

Evidence aimed inside one reading can test execution without testing whether that reading is
the right task. A candidate and reference that encode the same task model may agree perfectly
and still answer the wrong question. Settle the interpretation first; then use
`../modules/empirics.md` to test the weakest claim inside it.

In an evaluation or benchmark, hidden answers, graders, or isolation boundaries are not
empirical instruments. Ordinary fixtures and expected outputs may be legitimate project
contracts when the task authorizes their use; treat them according to that task rather than
as a universal prohibition.

## Return

Carry three things back to the calling route: the surviving reading, the clause that decided
it, and the full success condition. If the fork arose during verification, resume
`../modules/empirics.md` inside that reading; otherwise use `../modules/deep-reasoning.md` when
the task needs a reasoning chain. The fork is settled when each stated condition has a role,
not when the protocol has produced more prose.
