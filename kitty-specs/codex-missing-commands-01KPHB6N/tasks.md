# Tasks: Codex Missing Commands

## Subtask Index

| ID | Description | WP | Parallel |
|----|-------------|----|----------|
| T001 | Update `CANONICAL_COMMANDS` in `command_installer.py` | WP01 | | [D] |
| T002 | Refactor `accept.md` from override to source template | WP01 | [D] |
| T003 | Refactor `dashboard.md` from override to source template | WP01 | [D] |
| T004 | Refactor `tasks-finalize.md` from override to source template | WP01 | [D] |
| T005 | Create `merge.md` source template | WP01 | [D] |
| T006 | Create `status.md` source template | WP01 | [D] |
| T007 | Verify all 16 skills install via `agent config add codex` | WP02 | |
| T008 | Verify all 16 skills install via `agent config add vibe` | WP02 | |
| T009 | Run `command_verifier` on all rendered skills | WP02 | |
| T010 | Update `status.json` in mission spec | WP02 | |

## WP01 - Registration and Templates
**Goal**: Register the 5 missing commands and create their source templates.

- [x] T001 Update `CANONICAL_COMMANDS` in `command_installer.py` (WP01)
- [x] T002 Refactor `accept.md` from override to source template (WP01)
- [x] T003 Refactor `dashboard.md` from override to source template (WP01)
- [x] T004 Refactor `tasks-finalize.md` from override to source template (WP01)
- [x] T005 Create `merge.md` source template (WP01)
- [x] T006 Create `status.md` source template (WP01)

**Implementation Sketch**:
1. Add "accept", "dashboard", "merge", "status", "tasks-finalize" to `CANONICAL_COMMANDS` in `src/specify_cli/skills/command_installer.py`.
2. Move and refactor `.kittify/overrides/missions/software-dev/command-templates/{accept,dashboard,tasks-finalize}.md` to `src/specify_cli/missions/software-dev/command-templates/`.
3. Author `src/specify_cli/missions/software-dev/command-templates/{merge,status}.md`.

## WP02 - Verification and Parity
**Goal**: Ensure all skills are correctly installed and validated.

- [ ] T007 Verify all 16 skills install via `agent config add codex` (WP02)
- [ ] T008 Verify all 16 skills install via `agent config add vibe` (WP02)
- [ ] T009 Run `command_verifier` on all rendered skills (WP02)
- [ ] T010 Update `status.json` in mission spec (WP02)

**Implementation Sketch**:
1. Use a temporary project or the current project to run `spec-kitty agent config add codex`.
2. Check `.agents/skills/` for the existence of 16 `spec-kitty.*` directories.
3. Validate each `SKILL.md` using existing verification tools or manual inspection of the rendered output.
