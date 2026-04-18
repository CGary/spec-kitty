# Research: Command Template Mapping

## Command Signatures

The 5 missing commands will be implemented as thin wrappers over the `spec-kitty` CLI.

| Command | CLI Equivalent | Template Source |
|---------|---------------|-----------------|
| `accept` | `spec-kitty accept` | Refactored from `.kittify/overrides/` |
| `dashboard` | `spec-kitty dashboard` | Refactored from `.kittify/overrides/` |
| `merge` | `spec-kitty merge` | New (Signature: `spec-kitty merge`) |
| `status` | `spec-kitty agent tasks status` | New (Signature: `spec-kitty agent tasks status`) |
| `tasks-finalize` | `spec-kitty agent mission finalize-tasks` | Refactored from `.kittify/overrides/` |

## Template Consistency
All templates must include:
1. **Frontmatter**: Description for the skill.
2. **Title**: `/spec-kitty.<command>`
3. **Purpose**: Brief explanation.
4. **User Input Block**: `## User Input` with `$ARGUMENTS`.
5. **Execution Command**: A fenced code block with the CLI command.

## Registration
`CANONICAL_COMMANDS` in `src/specify_cli/skills/command_installer.py` should be updated to include the new commands in alphabetical order within their logical group.
