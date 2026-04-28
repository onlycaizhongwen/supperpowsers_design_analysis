# superpowers source architecture analysis

## Resume capsule

- Task: Analyze the main structure of `superpowers`, then produce high-level architecture and flow documentation while intentionally skipping implementation details.
- Key decision: Put the output in `docs/codex/v1/designs/superpowers-architecture-design.md` as a reverse-engineered architecture note.
- Current phase: Completed.
- Completed artifacts: Task record created; architecture and flow document written at `docs/codex/v1/designs/superpowers-architecture-design.md`; project status updated.
- Remaining work: None.
- Important findings: `superpowers` is a cross-agent skills/plugin distribution repo, not a conventional runtime service. Core content lives under `skills/`; platform adapters expose those skills through manifests, hooks, symlinks, or prompt injection.

## Steps

- [v] Scan source structure and existing documentation
  - Current artifact: Task record.
  - Next step: Read README, package metadata, main scripts, and directory structure.
  - Files: `superpowers/`
- [v] Identify architecture and module responsibilities
- [v] Identify core runtime flows
- [v] Write architecture and flow documentation
- [v] Update status and close task record

## Research findings

- Repository shape: `skills/` is the core library; `.codex-plugin/`, `.claude-plugin/`, `.cursor-plugin/`, `.opencode/`, `GEMINI.md`, `docs/README.codex.md` are platform adapters or installation guides.
- Runtime bootstrap: platforms load or inject `skills/using-superpowers/SKILL.md`, which enforces skill discovery and use before normal task handling.
- Workflow chain: README presents the main methodology as brainstorming -> git worktree isolation -> writing plans -> subagent-driven/executing plans -> TDD/review -> finish branch.
- Visual companion: `skills/brainstorming/scripts/server.cjs` is the only notable local runtime component, a zero-dependency Node HTTP/WebSocket server used by brainstorming.
- Quality system: tests are mostly shell/CLI behavioral tests for skill triggering and platform behavior, plus Node tests for the brainstorming server.

## Error log

- None.
