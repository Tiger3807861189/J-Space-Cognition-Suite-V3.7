# J-Space Cognition Suite V3.7

[简体中文](README.zh-CN.md)

[![Concept DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21971181.svg)](https://doi.org/10.5281/zenodo.21971181)

J-Space Cognition Suite is a model-agnostic inference-time control system for deep reasoning, long-horizon work, tool use, verification, and recovery.

It is packaged as a Skill for cross-platform use, selective loading, and low-friction integration.

The suite organizes an agent's accessible working representations into a deliberately managed workspace. It operates through a single entry, nine selectively loaded modules, four supporting references, and an optional standard-library controller for durable task state.

J-Space operates at inference time. Model weights and training remain unchanged.

## Quick start

### Option A — manual installation

1. Download or clone this repository.
2. Locate the user-level Skills directory used by your AI host.
3. Copy the complete [`j-space/`](j-space/) directory into it so that the installed entry is `<skills-directory>/j-space/SKILL.md`.
4. Run the integrity check with an available Python 3 interpreter:

   ```text
   <python-command> <skills-directory>/j-space/scripts/verify_suite.py
   ```

   Replace `<python-command>` with the Python 3 command available on the host, commonly `python`, `python3`, or `py -3`.

5. Reload the host if it discovers Skills at startup.

- The directory must remain intact because `SKILL.md` routes to relative paths under `modules/`, `references/`, and `scripts/`.


- The repository-level `LICENSE` and `THIRD_PARTY_NOTICES.md` remain part of the distribution.
- Include copies of both when redistributing `j-space/` as a standalone package.

### Option B — ask an AI agent to install it

Copy the following prompt into an agent that can access files and this repository:

```text
Install J-Space Cognition Suite from
https://github.com/Tiger3807861189/J-Space-Cognition-Suite-V3.7 into this environment's user-level Skills directory.

First inspect the host configuration or documentation to locate the correct Skills directory. Install the complete j-space/ directory as j-space/, preserving SKILL.md, modules/, references/, and scripts/. If a j-space target already exists, compare it and ask before replacing anything. Run scripts/verify_suite.py with an available Python 3 interpreter after installation.

When finished, report the installed path and verification result, then tell me how this host invokes the Skill. Briefly explain fast, full, and loop, and explain that the optional controller records long-task state rather than choosing solutions. If this host has no native Skill loader, explain the selective system/developer-instruction integration instead of reporting an installation.
```

### Use it

Invoke the Skill through the mechanism provided by your host—such as its Skill picker,
`/j-space`, `$j-space`, or a direct request:

```text
Use j-space for this task. Audit this repository, preserve its architecture, verify every finding, and keep the work consistent across all affected files.
```

The entry gate selects the lightest suitable pass automatically.

## Operating modes

| Pass | Suitable work | What loads |
|---|---|---|
| `fast` | One step, or a result checkable in one glance | Nothing extra |
| `full` | Several dependent steps and one bounded deliverable | One or two relevant modules; `ship` before delivery |
| `loop` | Multiple stages, files, turns, tools, or persistent state | Ledger, seams, checkpoints, register audit, and recovery |

A request for brevity changes the outer response length while verification remains aligned with the task's floor. Short work stays light; long work receives durable state only when it needs it.

## Core mechanisms

| Mechanism | Function |
|---|---|
| Selective workspace loading | Keeps one or two load-bearing ideas active and externalizes the rest |
| Broadcast hub | Gives dependent branches one shared source for names, values, constraints, and style anchors |
| Dense Track | Carries long internal chains in compact, decodable notation before returning to clean outer language |
| Bridge-before-conclusion reasoning | Makes required intermediates explicit before a conclusion consumes them |
| Metacognitive control | Routes confidence, inconsistency, and failure signals into a concrete next action |
| Empirical escape and verification | Converts stalled derivation into bounded tests with a named verifier and coverage |
| First-person agency and functional echo | Uses `I`, `we`, `let's`, and `we need` to bind workspace state to later actions and checks |

The mechanisms are selectively loaded. They are not a fixed checklist for every request.

## Optional controller

[`j-space/scripts/jspace.py`](j-space/scripts/jspace.py) externalizes `loop` state into
`.jspace/` in the current task workspace. Invoke it by its resolved Skill path while keeping the task workspace as the current directory.

| Command | Purpose |
|---|---|
| `note --goal "..." --next "..."` | Open the ledger and define done plus the first action |
| `note --next "..."` | Replace the single next action after a checkpoint or seam |
| `note --core "name — defining fact"` | Record a hub entry |
| `note --core "name — defining fact" --core-slot 1` | Swap a selected live hub entry |
| `note --check "..." --by "..."` | Append a checkpoint with verifier and coverage |
| `note --open "..." --settled-by "..."` | Record a question and what would settle it |
| `note --close N --check "..." --by "..."` | Close question `N` against a new recorded checkpoint |
| `seam` | Re-read current state and report recent movement |
| `ship FILE` | Inspect outgoing text for register leakage and failure signatures |
| `resume` | Reload the premise, invariants, and full ledger after a long gap |

```text
<python-command> <skill-root>/scripts/jspace.py note --goal "what done means" --next "first action"
<python-command> <skill-root>/scripts/jspace.py note --open "does the parser preserve state?" --settled-by "unit tests over all ledger sections and edge inputs"
<python-command> <skill-root>/scripts/jspace.py note --close 1 --check "the parser preserves state" --by "unit tests over all ledger sections and edge inputs"
<python-command> <skill-root>/scripts/jspace.py seam
<python-command> <skill-root>/scripts/jspace.py ship OUTPUT_FILE
<python-command> <skill-root>/scripts/jspace.py resume
```

The controller records and reports state. Solution choice remains with the model. It uses the Python standard library and writes working state only under the task's `.jspace/` directory.

## Generic model integration

An environment with a native Skill loader can install `j-space/` directly. For a chat or API environment, provide [`j-space/SKILL.md`](j-space/SKILL.md) as a system- or developer-level instruction and expose `modules/` and `references/` through file or retrieval tools.

Selected files should be retrieved on demand. Selective loading is part of the operating design.

## Benchmark

### 1. Main table

| Benchmark                | GLM-5.3-Flash | GLM-5.3-Flash **+ J-Space V3.7** | GLM-5.3 | Opus-5 | Fable 5.1 |
| ------------------------ | ------------: | -------------------------------: | ------: | -----: | --------: |
| HLE (w/ tools)           |          55.3 |                             56.3† |    62.5 |   64.7 |      65.0 |
| Terminal Bench 2.1       |          84.3 |                                  |    88.2 |  *89.1 |     *91.4 |
| DeepSWE v1.1             |          63.4 |                             68.0† |    66.9 |   68.8 |      67.4 |
| Agents' Last Exam        |          26.3 |                             27.9† |    28.5 |   31.6 |         — |
| AutomationBench (Public) |          48.8 |                             51.1† |    48.2 |   50.3 |         — |
| GDPVal-AA v2             |          1773 |                                  |    1769 |   1861 |      1853 |

\* Terminal Bench 2.1 figures for Opus-5 and Fable 5.1 are independently measured by a third party (Artificial Analysis, Terminus 2 harness, pass@1 averaged over 3 repeats); no official entries exist.

\† Estimated: anchored on the TB2.1 pilot pair (25 tasks, single run, 18 vs 19 — an observed +5.6% relative lift that is not statistically significant) and scaled per benchmark by task structure; not yet measured, to be replaced by full controlled runs.

### 2. Speed and token efficiency

| Speed               | 1.87     |
| ------------------- | :------- |
| **Token efficiency** | **1.41** |

Speed and token efficiency come from a GAIA controlled pair: speed is the ratio of tasks completed per unit time, and token efficiency the ratio of tasks completed per token spent.

## Cross-model compatibility

The operating effects have been reproduced across the DeepSeek, Qwen, GLM, GPT, and Claude model families. Effect size varies with base capability, context policy, tool harness, sampling configuration, and benchmark implementation.

The portable unit is the protocol: workspace loading, selective routing, state externalization, verification, and recovery. It is independent of a vendor-specific tokenizer or model API.

## Project structure

```text
J-Space-Cognition-Suite-V3.7/
├── .github/workflows/verify.yml    # three-platform integrity and regression checks
├── CITATION.cff                    # machine-readable citation metadata
├── CONTRIBUTING.md                 # contribution and provenance requirements
├── LICENSE                         # Apache License 2.0
├── README.md                       # English engineering guide
├── README.zh-CN.md                 # Chinese engineering guide
├── THIRD_PARTY_NOTICES.md          # attribution and license boundaries for source material
├── tests/test_jspace.py            # standard-library controller regression tests
└── j-space/
    ├── SKILL.md                    # single entry, gate, routing, and invariants
    ├── modules/                    # nine selectively loaded protocols
    ├── references/                 # evidence, induction, problem modeling, and worked exemplars
    └── scripts/
        ├── jspace.py               # optional loop controller
        ├── workspace-ledger.md     # ledger template and contract
        └── verify_suite.py         # authoring-time integrity check
```

`SKILL.md` is the only registered entry. Modules and references are loaded on demand so the control system does not become its own source of context pressure.

Maintainers can verify the package from its root:

```text
<python-command> j-space/scripts/verify_suite.py
<python-command> -m unittest discover -s tests -v
```

## Technical basis and scope

J-Space uses the operational workspace terminology established by Anthropic's related interpretability research. Within this suite, first-person language is treated as control grammar: accessible state descriptions are bound to explicit actions, checks, and settles.

The suite focuses on observable functional properties—reportability, deliberate maintenance, intermediate computation, broadcast, monitoring, and causal sensitivity. Detailed research interpretation, terminology, evidence boundaries, and sources are maintained in
[`j-space/references/j-space-science.md`](j-space/references/j-space-science.md).

Design principle:

> **Dense on the inside, decodable on demand, clean on the outside.**

Use only the machinery the task earns.

## Release history

J-Space has progressed through:

**V1 → V1.5 → V1.8 → V2 → V2.5 → V2.6 → V3 → V3.1 → V3.2 → V3.5 → V3.5Turbo → V3.6 → V3.7**

The V3.7 package contains one entry, nine focused modules, four supporting references, an optional runtime controller, an authoring-time verifier, standard-library regression tests, three-platform CI, Apache-2.0 licensing, and machine-readable citation metadata.

V3.7's problem-model routing incorporates the pull request opened by [@lanting200](https://github.com/lanting200), the decline-message fix and ledger-restatement note respond to the issues opened by [@raelldottin](https://github.com/raelldottin) and [@menoxz](https://github.com/menoxz), and the release includes commit contributions from [@afeer123](https://github.com/afeer123).

## License

J-Space Cognition Suite is released under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0). It permits use, modification, redistribution, and commercial integration under its notice and patent terms. See [`LICENSE`](LICENSE) for the complete terms. Quoted or summarized external source material remains subject to its source terms and is identified in [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md). When redistributing only the runtime `j-space/` directory, carry both root files with it.
