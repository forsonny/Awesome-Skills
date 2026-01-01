# github-flow

Complete GitHub workflow automation with quality gates.

## Installation

```bash
# Download and extract to skills directory
curl -L https://github.com/forsonny/Awesome-Skills/raw/main/github-flow/github-flow-1.0.0.skill -o ~/.claude/skills/github-flow-1.0.0.skill

# Verify checksum (optional)
curl -L https://github.com/forsonny/Awesome-Skills/raw/main/github-flow/github-flow-1.0.0.skill.sha256 -o /tmp/github-flow.sha256
cd ~/.claude/skills && sha256sum -c /tmp/github-flow.sha256
```

Or manually download `github-flow-1.0.0.skill` and place it in `~/.claude/skills/`.

## Features

- Pre-flight checks (lint, test, build) before commits
- Conventional commits format
- Semantic versioning (auto-detect bump type)
- Changelog generation (Keep a Changelog)
- Release automation with tagging

## Usage

| Command | Action |
|---------|--------|
| "commit" | Run checks, stage, commit |
| "commit and push" | Run checks, stage, commit, push |
| "release" | Full release workflow |
| "bump version" | Version bump + changelog |

## Project Support

Auto-detects: Node.js, Rust, Python, Go

## Version

1.0.0
