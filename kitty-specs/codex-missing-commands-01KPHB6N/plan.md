# Implementation Plan - Codex Missing Commands

**Branch**: `spec-gary` | **Date**: 2026-04-18 | **Spec**: [spec.md](./spec.md)
**Input**: Add 5 missing CLI commands to Agent Skills for Codex/Vibe.

## Summary
Add `accept`, `merge`, `status`, `dashboard`, and `tasks-finalize` to the canonical Agent Skills installer. This involves creating new templates in `src/specify_cli/missions/software-dev/command-templates/` and updating `CANONICAL_COMMANDS` in `src/specify_cli/skills/command_installer.py`.

## Technical Context
- **Language**: Python 3.11+
- **Primary Surface**: `src/specify_cli/skills/command_installer.py`
- **Templates Path**: `src/specify_cli/missions/software-dev/command-templates/`
- **Testing**: Pytest for installer logic and template rendering.
- **Constraints**: No changes to shims or slash-command agents.

## Charter Check
- [x] Python 3.11+ compliance.
- [x] Strict typing (mypy) maintained.
- [x] No breaking changes to existing 11 commands.
- [x] Follows "thin CLI wrapper" pattern for consistency.

## Project Structure
### Documentation
```
kitty-specs/codex-missing-commands-01KPHB6N/
├── plan.md
├── research.md
├── tasks.md
└── tasks/
    ├── WP01-registration-and-templates.md
    └── WP02-verification-and-parity.md
```

### Source Code
```
src/specify_cli/
├── skills/
│   └── command_installer.py  # Update CANONICAL_COMMANDS
└── missions/
    └── software-dev/
        └── command-templates/
            ├── accept.md          # New
            ├── dashboard.md       # New
            ├── merge.md           # New
            ├── status.md          # New
            └── tasks-finalize.md  # New
```

## Complexity Tracking
| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| None | N/A | N/A |
