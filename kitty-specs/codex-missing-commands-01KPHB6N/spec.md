# Codex Missing Commands

**Mission ID**: 01KPHB6NAB3V4482S6YX4EDTQ8  
**Mission Slug**: codex-missing-commands-01KPHB6N  
**Mission Type**: software-dev  
**Target Branch**: spec-gary  
**Status**: Draft

---

## Overview

Codex and Vibe receive spec-kitty slash commands as Agent Skills packages installed under `.agents/skills/`. Currently only 11 of the 16 consumer-facing commands are installed: the 9 prompt-driven commands and 2 of the 7 CLI-driven commands (`implement`, `review`).

The 5 remaining CLI-driven commands — `accept`, `merge`, `status`, `dashboard`, and `tasks-finalize` — are missing from `.agents/skills/`. Users running codex or vibe cannot invoke these lifecycle commands, which breaks the end-to-end mission workflow for those agents.

---

## Goals

- All 16 consumer-facing commands are available to codex and vibe via `.agents/skills/`.
- The 5 missing commands have their source templates in `command-templates/` and are registered in `CANONICAL_COMMANDS`.
- The fix is self-contained: no changes to slash-command agents, migrations, or the shim layer.

---

## Actors

- **Codex / Vibe users** — developers running spec-kitty workflows using Codex CLI or Mistral Vibe as their AI agent.
- **spec-kitty maintainers** — developers extending or packaging spec-kitty.

---

## User Scenarios & Testing

### Scenario 1 — Accept a completed mission

A Codex user has finished implementing all work packages for a mission. They invoke `$spec-kitty.accept` in their editor. The skill executes, runs `spec-kitty agent mission accept`, and returns acceptance status.

**Currently**: skill does not exist in `.agents/skills/` → command not found.  
**After fix**: skill is installed and functional.

### Scenario 2 — Check mission status

A Codex user invokes `$spec-kitty.status` to see the current kanban board for their mission. The skill runs `spec-kitty agent tasks status` and displays the lane breakdown.

**Currently**: skill missing → user must run CLI manually.  
**After fix**: skill installed, works inline in the agent session.

### Scenario 3 — Merge a completed mission

A Vibe user runs `$spec-kitty.merge` to merge all work packages into the target branch. The skill executes `spec-kitty merge` with appropriate arguments.

**Currently**: skill missing.  
**After fix**: skill installed.

### Scenario 4 — Open dashboard

A Codex user runs `$spec-kitty.dashboard` to open the mission dashboard in the browser.

**Currently**: skill missing.  
**After fix**: skill installed.

### Scenario 5 — Finalize tasks

A Codex user runs `$spec-kitty.tasks-finalize` after authoring `tasks.md` to parse dependencies, validate them, and commit the task artifacts.

**Currently**: skill missing.  
**After fix**: skill installed.

### Scenario 6 — Reinstall after deletion (regression)

A user deletes `.agents/skills/` manually and recovers via `agent config remove codex && agent config add codex`. All 16 skills are reinstalled, including the 5 new ones.

---

## Functional Requirements

| ID | Requirement | Status |
|----|-------------|--------|
| FR-001 | `accept.md` template exists in `src/specify_cli/missions/software-dev/command-templates/` and contains a `## User Input` section | Proposed |
| FR-002 | `merge.md` template exists in `command-templates/` and contains a `## User Input` section | Proposed |
| FR-003 | `status.md` template exists in `command-templates/` and contains a `## User Input` section | Proposed |
| FR-004 | `dashboard.md` template exists in `command-templates/` and contains a `## User Input` section | Proposed |
| FR-005 | `tasks-finalize.md` template exists in `command-templates/` and contains a `## User Input` section | Proposed |
| FR-006 | `CANONICAL_COMMANDS` in `command_installer.py` includes all 5 new commands | Proposed |
| FR-007 | Running `spec-kitty agent config add codex` on a fresh project installs 16 skills under `.agents/skills/` | Proposed |
| FR-008 | Running `spec-kitty agent config add vibe` on a fresh project installs 16 skills under `.agents/skills/` | Proposed |
| FR-009 | Each new SKILL.md renders without error through `command_renderer.render()` | Proposed |
| FR-010 | Each new SKILL.md passes `command_verifier.verify()` without warnings | Proposed |

---

## Non-Functional Requirements

| ID | Requirement | Status |
|----|-------------|--------|
| NFR-001 | The 5 new templates are consistent in structure with `implement.md` and `review.md` (frontmatter, `## User Input` block, version marker) | Proposed |
| NFR-002 | Adding commands to `CANONICAL_COMMANDS` does not break reinstallation for existing codex/vibe projects (idempotent upgrade path) | Proposed |
| NFR-003 | All existing 11 commands continue to render and install correctly after the change | Proposed |

---

## Constraints

| ID | Constraint | Status |
|----|------------|--------|
| C-001 | Only modify `command-templates/` and `command_installer.py` — no changes to `shims/registry.py`, slash-command agent directories, or migration files | Proposed |
| C-002 | Template content for `accept`, `dashboard`, and `tasks-finalize` must be derived from the already-validated overrides in `.kittify/overrides/missions/software-dev/command-templates/` | Proposed |
| C-003 | `merge.md` and `status.md` must be authored from scratch following the CLI command signatures in `shims/generator.py` (`_COMMAND_MAP`) | Proposed |
| C-004 | The `CANONICAL_COMMANDS` tuple must remain sorted alphabetically within each logical group (prompt-driven first, then CLI-driven lifecycle), or fully alphabetical — consistency with existing style | Proposed |

---

## Success Criteria

1. After running `spec-kitty agent config add codex`, `.agents/skills/` contains exactly 16 directories — one per consumer-facing command.
2. All 5 new SKILL.md files render without error and pass the verifier.
3. All previously installed 11 skills continue to pass the verifier unchanged.
4. A codex user can invoke `$spec-kitty.accept`, `$spec-kitty.merge`, `$spec-kitty.status`, `$spec-kitty.dashboard`, and `$spec-kitty.tasks-finalize` and each dispatches the correct `spec-kitty` CLI command.

---

## Key Entities

| Entity | Description |
|--------|-------------|
| `CANONICAL_COMMANDS` | Tuple in `command_installer.py` listing all commands installed to `.agents/skills/` |
| `command-templates/` | Source directory at `src/specify_cli/missions/software-dev/command-templates/` containing `.md` templates rendered into `SKILL.md` |
| `SKILL.md` | The rendered Agent Skills file installed under `.agents/skills/spec-kitty.<command>/` |
| `command_renderer.render()` | Renders a template into a `RenderedSkill` — requires `## User Input` section |
| `command_verifier.verify()` | Validates a rendered skill for structural correctness |

---

## Assumptions

- The 3 override templates (`accept.md`, `dashboard.md`, `tasks-finalize.md`) in `.kittify/overrides/` are production-quality and suitable as source templates without rework.
- `merge.md` and `status.md` do not require complex discovery flows — they dispatch directly to CLI commands and follow the same thin-wrapper pattern as the overrides.
- No migration is needed: existing projects get the new skills on next `agent config add codex` or reinstall.

---

## Out of Scope

- Adding missing commands to slash-command agents (they already have all 16 via the shim layer).
- Creating templates for internal skills (`doctor`, `materialize`, `debug`).
- Modifying `shims/registry.py` or `PROMPT_DRIVEN_COMMANDS` / `CLI_DRIVEN_COMMANDS` classifications.
