# GitHub Flow Skill

Complete GitHub workflow automation with quality gates.

## Features

- **Pre-flight checks** - Auto-runs lint, test, build before commits
- **Conventional commits** - Generates proper `type(scope): message` format
- **Semantic versioning** - Auto-determines MAJOR/MINOR/PATCH from commits
- **Changelog generation** - Updates CHANGELOG.md in Keep a Changelog format
- **Release automation** - Tags, pushes, and creates GitHub releases

## Installation

```bash
# Copy to your skills directory
cp -r github-flow ~/.claude/skills/

# Or use the packaged version
cp github-flow-1.0.0.skill ~/.claude/skills/
```

## Trigger Phrases

| Say | Action |
|-----|--------|
| "commit" | Pre-flight + stage + commit |
| "commit and push" | Pre-flight + stage + commit + push |
| "release" / "cut release" | Full workflow with version bump |
| "bump version" | Version bump + changelog only |

## Workflow

```
PRE-FLIGHT -> STAGE -> COMMIT -> VERSION -> CHANGELOG -> TAG -> PUSH -> RELEASE
```

## Project Detection

Auto-detects and runs appropriate checks:

| Project Type | Checks Run |
|--------------|------------|
| Node.js | `npm run lint`, `npm run test`, `npm run build` |
| Rust | `cargo fmt --check`, `cargo clippy`, `cargo test` |
| Python | `ruff check` / `flake8`, `pytest` |
| Go | `go fmt`, `go vet`, `go test` |

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Main skill instructions |
| `references/conventional-commits.md` | Commit message format guide |
| `references/versioning.md` | Semantic versioning rules |
| `references/changelog-format.md` | Changelog structure |

## Version

1.0.0
