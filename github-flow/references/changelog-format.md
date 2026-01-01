# Changelog Format Reference

Keep a Changelog format for human-readable history.

---

## Structure

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

## [1.2.0] - 2024-01-15

### Added
- New feature description

### Changed
- Changed behavior description

### Fixed
- Bug fix description

## [1.1.0] - 2024-01-01

### Added
- Previous feature

[Unreleased]: https://github.com/user/repo/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/user/repo/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/user/repo/releases/tag/v1.1.0
```

---

## Categories

Use these standard categories in this order:

| Category | Description | Commit Types |
|----------|-------------|--------------|
| Added | New features | `feat:` |
| Changed | Changes to existing | `refactor:`, `perf:` |
| Deprecated | Soon-to-be removed | Deprecation notices |
| Removed | Removed features | Breaking removals |
| Fixed | Bug fixes | `fix:` |
| Security | Security fixes | Security patches |

Only include categories with entries. Skip empty categories.

---

## Entry Format

Each entry should:

- Start with a dash and space (`- `)
- Use imperative mood ("Add" not "Added")
- Be a complete sentence (but no period needed)
- Reference issues/PRs when relevant

**Good:**
```markdown
### Added
- Add user authentication via OAuth2 (#123)
- Support CSV export for reports
- Allow custom themes in settings

### Fixed
- Fix memory leak in image processor (#456)
- Prevent duplicate form submissions
```

**Bad:**
```markdown
### Added
- Added a feature.          # past tense, vague
- oauth                     # incomplete
- #123                      # no description
```

---

## Unreleased Section

Always maintain an `[Unreleased]` section at the top:

```markdown
## [Unreleased]

### Added
- Work in progress feature

### Fixed
- Bug fix not yet released
```

On release:
1. Rename `[Unreleased]` content to new version
2. Add date
3. Create fresh `[Unreleased]` section

---

## Version Links

At the bottom of the file, add comparison links:

```markdown
[Unreleased]: https://github.com/user/repo/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/user/repo/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/user/repo/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/user/repo/releases/tag/v1.0.0
```

---

## Initial Changelog

For new projects:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

## [0.1.0] - YYYY-MM-DD

### Added
- Initial release
- Core feature A
- Core feature B

[Unreleased]: https://github.com/user/repo/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/user/repo/releases/tag/v0.1.0
```

---

## Generating from Commits

### Step 1: Get commits since last tag

```bash
git log $(git describe --tags --abbrev=0)..HEAD --pretty=format:"%s"
```

### Step 2: Categorize by type

```
feat:     -> Added
fix:      -> Fixed
perf:     -> Changed
refactor: -> Changed
docs:     -> (usually skip)
```

### Step 3: Format entries

```
feat(auth): add OAuth support
->
- Add OAuth support for authentication
```

### Step 4: Insert into changelog

Place new version after `## [Unreleased]`:

```markdown
## [Unreleased]

## [1.3.0] - 2024-01-20

### Added
- Add OAuth support for authentication
- Support batch operations in API

### Fixed
- Fix race condition in cache invalidation
```

---

## Breaking Changes

Highlight breaking changes prominently:

```markdown
## [2.0.0] - 2024-02-01

### Changed
- **BREAKING:** Rename `getUserData()` to `fetchUser()`
- **BREAKING:** Remove deprecated v1 API endpoints

### Removed
- **BREAKING:** Drop support for Node.js 14
```

Or use a separate section:

```markdown
## [2.0.0] - 2024-02-01

### BREAKING CHANGES
- `getUserData()` renamed to `fetchUser()`
- v1 API endpoints removed
- Node.js 14 no longer supported

### Added
- New features...
```

---

## Tips

1. **Write for humans** - Explain what changed, not commit hashes
2. **Be consistent** - Same style throughout
3. **Group related** - Combine related changes
4. **Reference issues** - Link to issues/PRs for context
5. **Date format** - Use ISO 8601: YYYY-MM-DD
6. **Newest first** - Latest version at top

---

## Example: Complete Changelog

```markdown
# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

### Added
- Dark mode support (in progress)

## [2.1.0] - 2024-01-20

### Added
- Export to PDF format (#234)
- Keyboard shortcuts for common actions

### Changed
- Improve search performance by 40%

### Fixed
- Fix timezone handling in scheduled tasks (#256)

## [2.0.0] - 2024-01-01

### BREAKING CHANGES
- API v1 endpoints removed
- Minimum Node.js version is now 18

### Added
- API v2 with improved response format
- WebSocket support for real-time updates

### Removed
- Legacy authentication method

## [1.5.0] - 2023-12-15

### Added
- User preferences panel
- Email notification settings

### Fixed
- Memory leak in long-running sessions (#189)

[Unreleased]: https://github.com/user/repo/compare/v2.1.0...HEAD
[2.1.0]: https://github.com/user/repo/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/user/repo/compare/v1.5.0...v2.0.0
[1.5.0]: https://github.com/user/repo/releases/tag/v1.5.0
```
