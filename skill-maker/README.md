# skill-maker

A meta-skill for Claude Code that creates and validates other Claude Code skills.

## Features

- **Skill Templates**: Scaffolds new skills with proper structure
- **Validation**: Checks skills against best practices
- **Packaging**: Creates distributable `.skill` files
- **Discovery**: Guided workflow to identify skill ideas
- **Evolution Modes**: Static, dynamic, and self-improving skills

## Installation

1. Download `skill-maker-1.1.0.skill`
2. Verify checksum (optional):
   ```bash
   sha256sum -c skill-maker-1.1.0.skill.sha256
   ```
3. Extract to your skills directory:
   ```bash
   unzip skill-maker-1.1.0.skill -d ~/.claude/skills/skill-maker/
   ```

## Usage

Once installed, Claude Code will automatically detect the skill. Example prompts:

- "Create a new skill for analyzing logs"
- "Validate my skill structure"
- "Help me discover what skill I should build"

## Files

| File | Description |
|------|-------------|
| `skill-maker-1.1.0.skill` | Distributable package (zip archive) |
| `skill-maker-1.1.0.skill.sha256` | SHA256 checksum for verification |

## Version

- **Current**: 1.1.0
- **Changelog**: See CHANGELOG.md inside the package

## License

MIT License - See LICENSE.txt inside the package
