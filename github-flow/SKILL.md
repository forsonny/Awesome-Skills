---
name: github-flow
version: 1.0.0
model: inherit
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, WebFetch
description: |
  Manages complete GitHub workflow including commits, versioning, changelogs,
  releases, and push operations. Auto-runs checks (lint, test, build) before
  commits. Supports semantic versioning and conventional commits. Activates
  for: commit, push, release, version bump, changelog, tag, git workflow,
  prepare release, ship it, cut release, bump version, publish.
---

# GitHub Flow Manager

Complete git workflow automation with quality gates.

## Workflow Overview

```
1. PRE-FLIGHT   -> Run checks (lint, test, build)
2. STAGE        -> Stage changes intelligently
3. COMMIT       -> Conventional commit message
4. VERSION      -> Bump semantic version (if release)
5. CHANGELOG    -> Update CHANGELOG.md
6. TAG          -> Create version tag (if release)
7. PUSH         -> Push to remote
8. RELEASE      -> Create GitHub release (if release)
```

---

## Quick Commands

| User Says | Action |
|-----------|--------|
| "commit" | Pre-flight + stage + commit |
| "commit and push" | Pre-flight + stage + commit + push |
| "release" / "cut release" | Full workflow with version bump |
| "bump version" | Version bump + changelog only |
| "push" | Push current branch |

---

## Pre-Flight Checks (Always Run First)

Before ANY commit, run applicable checks:

### Detection & Execution

```
IF package.json exists:
  -> npm run lint (if script exists)
  -> npm run test (if script exists)
  -> npm run build (if script exists)

IF Cargo.toml exists:
  -> cargo fmt --check
  -> cargo clippy
  -> cargo test

IF pyproject.toml OR setup.py exists:
  -> ruff check . OR flake8 (if available)
  -> pytest (if available)

IF go.mod exists:
  -> go fmt ./...
  -> go vet ./...
  -> go test ./...
```

### Check Failure Handling

```
IF any check fails:
  1. Show the error output clearly
  2. Ask: "Checks failed. Fix issues or commit anyway?"

  IF user says fix:
    -> Attempt auto-fix if possible
    -> Re-run checks

  IF user says commit anyway:
    -> Proceed with warning in commit body
```

---

## Commit Workflow

### Step 1: Analyze Changes

```bash
git status --porcelain
git diff --stat
git diff --cached --stat
```

Identify:
- Files modified
- Nature of changes (feature, fix, refactor, docs, etc.)
- Breaking changes

### Step 2: Stage Changes

```
IF user specified files:
  -> Stage only those files

IF no files specified:
  -> Show changed files
  -> Ask which to include OR stage all
```

### Step 3: Create Commit Message

Use conventional commits format. See `references/conventional-commits.md`.

**Format:**
```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

**Type Selection:**
| Change | Type |
|--------|------|
| New feature | `feat` |
| Bug fix | `fix` |
| Documentation | `docs` |
| Refactoring | `refactor` |
| Performance | `perf` |
| Tests | `test` |
| Build/deps | `build` |
| CI/CD | `ci` |
| Chores | `chore` |

**Breaking Changes:**
- Add `!` after type: `feat!: remove deprecated API`
- OR add footer: `BREAKING CHANGE: description`

### Step 4: Execute Commit

```bash
git commit -m "$(cat <<'EOF'
<type>(<scope>): <description>

<body if needed>

<footer if needed>

Generated with Claude Code
Co-Authored-By: Claude <noreply@anthropic.com>
EOF
)"
```

---

## Version Workflow

For releases, bump version following semver. See `references/versioning.md`.

### Step 1: Determine Bump Type

Analyze commits since last tag:

```bash
git log $(git describe --tags --abbrev=0)..HEAD --oneline
```

| Commits Contain | Bump |
|-----------------|------|
| `BREAKING CHANGE` or `!` | MAJOR |
| `feat:` | MINOR |
| `fix:`, `perf:`, etc. | PATCH |

### Step 2: Calculate New Version

```
Current: X.Y.Z
MAJOR bump: (X+1).0.0
MINOR bump: X.(Y+1).0
PATCH bump: X.Y.(Z+1)
```

### Step 3: Update Version Files

**package.json:**
```bash
npm version <major|minor|patch> --no-git-tag-version
```

**Cargo.toml:**
Edit `version = "X.Y.Z"` line

**pyproject.toml:**
Edit `version = "X.Y.Z"` line

**Other files (VERSION, version.go, etc.):**
Detect and update accordingly

---

## Changelog Workflow

Maintain CHANGELOG.md following Keep a Changelog format.
See `references/changelog-format.md`.

### Step 1: Read Existing Changelog

```bash
# Check if exists
cat CHANGELOG.md 2>/dev/null || echo "No changelog found"
```

### Step 2: Gather Changes

```bash
# Get commits since last tag
git log $(git describe --tags --abbrev=0 2>/dev/null || echo "")..HEAD \
  --pretty=format:"- %s" --reverse
```

### Step 3: Categorize Changes

Group by type:
- **Added** - new features (`feat:`)
- **Changed** - changes to existing (`refactor:`, `perf:`)
- **Deprecated** - soon-to-be removed
- **Removed** - removed features
- **Fixed** - bug fixes (`fix:`)
- **Security** - security fixes

### Step 4: Update Changelog

Insert new version section after `## [Unreleased]`:

```markdown
## [X.Y.Z] - YYYY-MM-DD

### Added
- Feature description

### Fixed
- Bug fix description
```

---

## Tag & Release Workflow

### Create Tag

```bash
git tag -a vX.Y.Z -m "Release vX.Y.Z"
```

### Push with Tags

```bash
git push origin <branch>
git push origin vX.Y.Z
```

### Create GitHub Release

Use `gh` CLI if available:

```bash
gh release create vX.Y.Z \
  --title "vX.Y.Z" \
  --notes-file <(changelog_section) \
  --latest
```

If `gh` not available:
- Provide release notes text
- Instruct user to create release manually

---

## Push Workflow

### Pre-Push Validation

```bash
# Ensure we're not on protected branch for direct push
git branch --show-current

# Check remote status
git fetch origin
git status -sb
```

### Protected Branches

```
IF branch is main/master/develop:
  -> Warn user
  -> Suggest PR workflow instead
  -> Proceed only if explicitly confirmed
```

### Execute Push

```bash
git push origin <branch>
```

If upstream not set:
```bash
git push -u origin <branch>
```

---

## Full Release Checklist

For `/release` or "cut a release":

1. [ ] Run pre-flight checks (lint, test, build)
2. [ ] Ensure working directory clean (or commit changes)
3. [ ] Determine version bump type from commits
4. [ ] Bump version in all relevant files
5. [ ] Update CHANGELOG.md with new section
6. [ ] Create release commit: `chore(release): vX.Y.Z`
7. [ ] Create annotated tag: `vX.Y.Z`
8. [ ] Push commit and tag
9. [ ] Create GitHub release with changelog notes
10. [ ] Report success with release URL

---

## Error Recovery

### Undo Last Commit (not pushed)

```bash
git reset --soft HEAD~1
```

### Fix Commit Message

```bash
git commit --amend -m "new message"
```

### Remove Tag (local)

```bash
git tag -d vX.Y.Z
```

### Remove Tag (remote)

```bash
git push origin :refs/tags/vX.Y.Z
```

---

## File References

| File | Purpose |
|------|---------|
| `references/conventional-commits.md` | Commit message format guide |
| `references/versioning.md` | Semantic versioning rules |
| `references/changelog-format.md` | Changelog structure |
