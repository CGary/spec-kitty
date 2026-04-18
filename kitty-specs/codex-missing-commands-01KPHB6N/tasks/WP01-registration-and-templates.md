---
work_package_id: WP01
title: Registration and Templates
dependencies: []
requirement_refs:
- FR-001
- FR-002
- FR-003
- FR-004
- FR-005
- FR-006
- NFR-001
- NFR-003
planning_base_branch: spec-gary
merge_target_branch: spec-gary
branch_strategy: Planning artifacts for this feature were generated on spec-gary. During /spec-kitty.implement this WP may branch from a dependency-specific base, but completed changes must merge back into spec-gary unless the human explicitly redirects the landing branch.
subtasks:
- T001
- T002
- T003
- T004
- T005
- T006
history: []
authoritative_surface: src/specify_cli/
execution_mode: code_change
owned_files:
- src/specify_cli/skills/command_installer.py
- src/specify_cli/missions/software-dev/command-templates/accept.md
- src/specify_cli/missions/software-dev/command-templates/dashboard.md
- src/specify_cli/missions/software-dev/command-templates/merge.md
- src/specify_cli/missions/software-dev/command-templates/status.md
- src/specify_cli/missions/software-dev/command-templates/tasks-finalize.md
tags: []
---

# WP01 - Registration and Templates

## Objective
Register the 5 missing commands and create their source templates in the canonical location.

## Context
Codex/Vibe skills are rendered from templates in `src/specify_cli/missions/software-dev/command-templates/`. We are adding the missing lifecycle commands.

## Guidance

### T001: Update `CANONICAL_COMMANDS`
Update the `CANONICAL_COMMANDS` tuple in `src/specify_cli/skills/command_installer.py`.
- Add: `accept`, `dashboard`, `merge`, `status`, `tasks-finalize`.
- Ensure the list remains sorted (logical groups or alphabetical).

### T002-T004: Refactor Overrides
Refactor the following overrides from `.kittify/overrides/missions/software-dev/command-templates/` to `src/specify_cli/missions/software-dev/command-templates/`:
- `accept.md`
- `dashboard.md`
- `tasks-finalize.md`

Ensure they follow the thin CLI wrapper pattern.

### T005: Create `merge.md`
Create `src/specify_cli/missions/software-dev/command-templates/merge.md` with:
- Purpose: Merge completed mission work packages.
- CLI Command: `spec-kitty merge`.

### T006: Create `status.md`
Create `src/specify_cli/missions/software-dev/command-templates/status.md` with:
- Purpose: Check current mission/task status.
- CLI Command: `spec-kitty agent tasks status`.

## Definition of Done
- `command_installer.py` updated and contains 16 commands.
- 5 new templates exist in `src/specify_cli/missions/software-dev/command-templates/`.
- All templates have the mandatory `## User Input` section.
