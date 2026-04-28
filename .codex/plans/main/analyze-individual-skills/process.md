# analyze individual superpowers skills

## Resume capsule

- Task: Analyze five core skills one by one: `using-superpowers`, `subagent-driven-development`, `brainstorming`, `test-driven-development`, `systematic-debugging`.
- Key decision: Write one Markdown analysis per skill under `docs/codex/v1/designs/skills/`, then update the documentation index.
- Current phase: Completed.
- Completed artifacts: Task record created; five skill analysis documents written; README, index, and status updated; local validation completed.
- Remaining work: Commit locally and push.
- Important findings: `using-superpowers` is the entry discipline; `subagent-driven-development` is a controller/reviewer workflow; `brainstorming` is a hard-gated design-before-implementation workflow; `test-driven-development` is the strict implementation discipline; `systematic-debugging` is the root-cause-first failure workflow.

## Steps

- [v] Read five skill sources and related prompt/reference files
- [v] Write `using-superpowers` analysis
- [v] Write `subagent-driven-development` analysis
- [v] Write `brainstorming` analysis
- [v] Write `test-driven-development` analysis
- [v] Write `systematic-debugging` analysis
- [v] Update documentation index and status
- [v] Commit local changes

## Research findings

- `using-superpowers` is not a business workflow; it is the session-level gate that makes all other skills discoverable and mandatory when relevant.
- `subagent-driven-development` is intentionally sequential at the task level, despite using subagents, because each task must pass spec review and then quality review.
- `brainstorming` explicitly prevents implementation until design has been presented and approved.
- `test-driven-development` treats tests-after as a different and weaker practice, not as TDD.
- `systematic-debugging` treats three failed fix attempts as a signal to question architecture rather than keep patching symptoms.

## Error log

- None.
