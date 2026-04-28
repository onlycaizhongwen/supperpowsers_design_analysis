# superpowers design analysis

This repository contains a source-level architecture and workflow analysis of [obra/superpowers](https://github.com/obra/superpowers).

`superpowers` is included as a Git submodule so this repository can keep the analysis documents separate from the upstream source while still preserving the exact source revision used for the analysis.

## Clone

Use `--recurse-submodules` so the upstream `superpowers` source is pulled too:

```powershell
git clone --recurse-submodules https://github.com/onlycaizhongwen/supperpowsers_design_analysis.git
```

If you already cloned without submodules:

```powershell
git submodule update --init --recursive
```

## Reading Order

1. [Documentation Index](docs/codex/v1/designs/index.md)
2. [Overall Architecture and Flow](docs/codex/v1/designs/superpowers-architecture-design.md)
3. [Branch Execution Flow Analysis](docs/codex/v1/designs/superpowers-branch-flow-design.md)
4. Core skill analyses:
   - [using-superpowers](docs/codex/v1/designs/skills/using-superpowers-skill-analysis.md)
   - [subagent-driven-development](docs/codex/v1/designs/skills/subagent-driven-development-skill-analysis.md)
   - [brainstorming](docs/codex/v1/designs/skills/brainstorming-skill-analysis.md)
   - [test-driven-development](docs/codex/v1/designs/skills/test-driven-development-skill-analysis.md)
   - [systematic-debugging](docs/codex/v1/designs/skills/systematic-debugging-skill-analysis.md)
5. [Overall Flow Diagram HTML Preview](docs/codex/v1/designs/assets/superpowers-flow.html)
6. [Branch Flow Diagrams HTML Preview](docs/codex/v1/designs/assets/superpowers-branch-flows.html)

## What Is Covered

- How Superpowers is loaded across Claude, Codex, Cursor, OpenCode, and Gemini.
- How `using-superpowers` acts as the entry discipline for skill selection.
- How core development flows branch into brainstorming, planning, implementation, debugging, review, and finishing.
- How the five most important skills work internally and connect to each other.
- Where each major conclusion maps back to source files.

## Source Revision

The `superpowers` submodule currently points to upstream commit:

```text
6efe32c9e2dd002d0c394e861e0529675d1ab32e
```
