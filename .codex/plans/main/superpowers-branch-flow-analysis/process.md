# superpowers branch flow analysis

## Resume capsule

- Task: Analyze execution flow for each major branch in `superpowers`, with flow diagrams.
- Key decision: Produce `docs/codex/v1/designs/superpowers-branch-flow-design.md` plus SVG diagrams under `docs/codex/v1/designs/assets/`.
- Current phase: Completed.
- Completed artifacts: Task record created; branch flow document written at `docs/codex/v1/designs/superpowers-branch-flow-design.md`; six SVG diagrams and one HTML preview page created under `docs/codex/v1/designs/assets/`; project status updated.
- Remaining work: None.
- Important findings: Major branches are platform onboarding, request routing, design/planning, implementation execution, debugging/fix, and review/finish. Each branch is driven by one or more `skills/*/SKILL.md` workflow files and returns to quality gates when verification fails.

## Steps

- [v] Read branch-related skills and platform adapters
- [v] Summarize each major branch execution flow
- [v] Create SVG flow diagrams
- [v] Write branch flow documentation
- [v] Update status and close task

## Research findings

- Platform onboarding converges on `using-superpowers` through platform-specific adapters: manifest/hook for Claude and Cursor, `.codex-plugin/plugin.json` for Codex, OpenCode plugin JS, and `GEMINI.md` for Gemini.
- Request routing is controlled by `using-superpowers`, which requires relevant or explicitly requested skills to be invoked before action.
- Design/planning branch is `brainstorming` -> design approval -> design doc -> self-review -> user review -> `writing-plans`.
- Implementation branch uses `using-git-worktrees` for isolation, then either `subagent-driven-development` with two review gates or `executing-plans` for inline execution.
- Debug branch uses `systematic-debugging` phases before TDD-style root-cause repair.
- Finish branch combines code review, feedback handling, evidence-based verification, and `finishing-a-development-branch` options.

## Error log

- None.
