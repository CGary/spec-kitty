---
work_package_id: WP02
title: Verification and Parity
dependencies:
- WP01
requirement_refs:
- FR-007
- FR-008
- FR-009
- FR-010
- NFR-002
planning_base_branch: spec-gary
merge_target_branch: spec-gary
branch_strategy: Planning artifacts for this feature were generated on spec-gary. During /spec-kitty.implement this WP may branch from a dependency-specific base, but completed changes must merge back into spec-gary unless the human explicitly redirects the landing branch.
base_branch: kitty/mission-codex-missing-commands-01KPHB6N
base_commit: cd2817bc35fecb599fe90f0ec600722c6b830d07
created_at: '2026-04-18T22:54:59.433829+00:00'
subtasks:
- T007
- T008
- T009
- T010
shell_pid: "526941"
history: []
authoritative_surface: kitty-specs/codex-missing-commands-01KPHB6N/
execution_mode: code_change
owned_files:
- kitty-specs/codex-missing-commands-01KPHB6N/status.json
tags: []
agent: "claude"
---

# WP02 - Verification and Parity

## Objective
Verify the installation and rendering of all 16 commands in a realistic project context.

## Guidance

### T007-T008: Verify Installation
In the current project (or a fresh test project), run:
```bash
spec-kitty agent config add codex
spec-kitty agent config add vibe
```
Verify that `.agents/skills/` contains 16 directories (9 prompt-driven + 7 CLI-driven).

### T009: Run Command Verifier
Use the existing verification logic to ensure all 16 rendered `SKILL.md` files are structurally correct.
- Check for `## User Input` section.
- Check for version markers.
- Ensure no rendering errors.

### T010: Update Status
Update `kitty-specs/codex-missing-commands-01KPHB6N/status.json` to reflect the completion of the mission requirements.

## Definition of Done
- Installation confirmed for both codex and vibe.
- Exactly 16 skills present in `.agents/skills/`.
- All skills pass structural verification.

## Activity Log

- 2026-04-18T22:54:59Z – claude – shell_pid=526941 – Assigned agent via action command
- 2026-04-18T22:59:44Z – claude – shell_pid=526941 – Ready for review: 16 skills verified (all have User Input section), vibe and codex configured, manifest committed to spec-gary
