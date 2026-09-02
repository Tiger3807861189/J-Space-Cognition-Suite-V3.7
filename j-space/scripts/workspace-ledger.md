# J-Space Workspace Ledger — template

Copy the blank shell below to `.jspace/WORKSPACE.md` at the start of any task that will span
stages, files, or turns, then fill `Goal` and `Next` before the first seam. Or let
`jspace.py note --goal "..." --next "..."` create it. If there is no filesystem here, keep the
five sections in the conversation and restate them at each seam — the file was never the point,
the re-reading was.

Five lines. Short enough to re-read in seconds, or it will not get re-read.

```markdown
# J-Space Workspace Ledger

## Goal

## Core

## Verified

## Open

## Next
```

Write one testable completion condition under `Goal` and one immediate action under `Next`.
Add at most two live `Core` entries as `name — defining fact`; let the controller number
`Verified` and `Open` entries so their identifiers remain stable.

## The four rules that make it work

1. **Re-read at every seam.** This is the whole mechanism. Attention reaches any earlier token
   equally, but only while that token is still in front of you.
2. **Preserve the record.** `Verified` is numbered and append-only. `Goal` and `Next` update;
   an existing live `Core` slot changes only by an explicit swap; an `Open` entry closes against
   a recorded checkpoint, which retains `closes: ?NN`; its number is never reused. When the
   ledger is restated by hand, carry each `closes: ?NN` suffix with its row — a number's
   retirement is recorded only there.
3. **`Next` is never empty.** A ledger with no next action is a ledger you have stopped using.
4. **Two live core entries.** More than two is not a hub, it is a list. The rest stay written
   down and get reloaded per section.

## What does not belong here

Not the reasoning. Not the draft. Not a log of what you did.

The ledger holds *state* — what is settled, what is open, what is next. If a line would never be
read again, it belongs on the inner register or nowhere.

**It is also not a task list.** If your environment already tracks work items, keep using it —
that tracks *what is left to do*. The ledger tracks *what is now known*: the verified results
later steps are allowed to rely on, and the questions that are still open. They answer different
questions and neither replaces the other.

## Housekeeping

`.jspace/` is working state, not part of the project. It belongs in `.gitignore`, and it should
not be committed unless someone asks for it:

```
echo ".jspace/" >> .gitignore
```

Deleting it costs nothing except the state it held. Nothing in the suite breaks without it —
the ledger simply moves back into the conversation.
