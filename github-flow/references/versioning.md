# Semantic Versioning Reference

Version numbering for predictable compatibility.

---

## Format

```
MAJOR.MINOR.PATCH[-PRERELEASE][+BUILD]

Examples:
1.0.0
2.1.3
1.0.0-alpha.1
1.0.0-beta.2+build.123
```

---

## Version Components

| Component | When to Increment | Resets |
|-----------|-------------------|--------|
| MAJOR | Breaking changes | MINOR, PATCH to 0 |
| MINOR | New features (backward compatible) | PATCH to 0 |
| PATCH | Bug fixes (backward compatible) | Nothing |

---

## Increment Rules

### MAJOR (X.0.0)

Increment when making incompatible API changes:

- Removing public API
- Changing function signatures
- Renaming exported items
- Changing default behavior
- Dropping support for platforms/versions

```
1.2.3 -> 2.0.0  (breaking change)
```

### MINOR (X.Y.0)

Increment when adding functionality in backward-compatible manner:

- New features
- New optional parameters
- New public API
- Deprecating functionality (not removing)

```
1.2.3 -> 1.3.0  (new feature)
```

### PATCH (X.Y.Z)

Increment when making backward-compatible bug fixes:

- Bug fixes
- Performance improvements
- Security patches
- Documentation fixes
- Internal refactoring

```
1.2.3 -> 1.2.4  (bug fix)
```

---

## Pre-release Versions

For development versions before stable release:

```
1.0.0-alpha      # Alpha release
1.0.0-alpha.1    # Alpha iteration
1.0.0-beta.1     # Beta release
1.0.0-rc.1       # Release candidate
```

**Precedence:**
```
1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-beta < 1.0.0-rc.1 < 1.0.0
```

---

## Build Metadata

For build info (ignored in precedence):

```
1.0.0+20240115
1.0.0+build.123
1.0.0-beta+sha.abc123
```

---

## Initial Development (0.x.x)

Before 1.0.0, anything may change:

```
0.1.0  # Initial development
0.2.0  # Breaking changes OK
0.2.1  # Patches
```

When to release 1.0.0:
- Public API is stable
- Used in production
- Breaking changes will follow semver

---

## Determining Bump Type

### From Conventional Commits

```
git log <last-tag>..HEAD --oneline
```

| If commits contain | Bump |
|--------------------|------|
| `BREAKING CHANGE` or `!` | MAJOR |
| `feat:` | MINOR |
| Only `fix:`, `perf:`, etc. | PATCH |

### Priority

MAJOR > MINOR > PATCH

If both feat and fix present, bump MINOR.
If BREAKING CHANGE present, bump MAJOR regardless of others.

---

## File Locations

### JavaScript/Node

```json
// package.json
{
  "version": "1.2.3"
}
```

Update: `npm version <major|minor|patch>`

### Rust

```toml
# Cargo.toml
[package]
version = "1.2.3"
```

### Python

```toml
# pyproject.toml
[project]
version = "1.2.3"
```

Or `setup.py`, `__version__.py`, etc.

### Go

```go
// version.go
const Version = "1.2.3"
```

### Generic

```
# VERSION file
1.2.3
```

---

## Multiple Files

When version appears in multiple places, update all:

1. Main version file (package.json, Cargo.toml)
2. Lock files (regenerate, don't edit)
3. Constants in code
4. Documentation/README badges

---

## Comparison Examples

```
1.0.0 < 2.0.0 < 2.1.0 < 2.1.1
1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-beta < 1.0.0
1.0.0 < 1.0.0+build  # Equal precedence (build ignored)
```

---

## Common Mistakes

| Mistake | Correct |
|---------|---------|
| Bumping MAJOR for new feature | MINOR for new features |
| Not resetting MINOR/PATCH | MAJOR bump resets both to 0 |
| Using 0.x.x in production | Release 1.0.0 when stable |
| Bumping for non-code changes | Docs/CI don't require bump |
| Forgetting pre-release suffix | Use -alpha, -beta for unstable |
