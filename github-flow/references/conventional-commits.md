# Conventional Commits Reference

Structured commit messages for automated changelog generation.

---

## Format

```
<type>[optional scope][!]: <description>

[optional body]

[optional footer(s)]
```

---

## Types

| Type | When to Use | Bumps |
|------|-------------|-------|
| `feat` | New feature for the user | MINOR |
| `fix` | Bug fix for the user | PATCH |
| `docs` | Documentation only | - |
| `style` | Formatting, no code change | - |
| `refactor` | Code change, no feature/fix | - |
| `perf` | Performance improvement | PATCH |
| `test` | Adding/updating tests | - |
| `build` | Build system, dependencies | - |
| `ci` | CI/CD configuration | - |
| `chore` | Maintenance tasks | - |
| `revert` | Reverting previous commit | - |

---

## Scope

Optional context in parentheses:

```
feat(auth): add OAuth2 support
fix(api): handle null response
docs(readme): update installation steps
```

Common scopes:
- Component/module name: `auth`, `api`, `ui`
- Feature area: `login`, `checkout`, `search`
- File type: `deps`, `config`, `types`

---

## Breaking Changes

Two ways to indicate:

### 1. Exclamation Mark

```
feat!: remove deprecated endpoints
refactor(api)!: change response format
```

### 2. Footer

```
feat: restructure user API

BREAKING CHANGE: User endpoints now require authentication.
The /users endpoint no longer supports anonymous access.
```

---

## Description Rules

- Imperative mood: "add" not "added" or "adds"
- Lowercase first letter
- No period at end
- Max 72 characters
- Complete the sentence: "This commit will..."

**Good:**
```
feat(cart): add quantity validation
fix: prevent duplicate form submissions
refactor(auth): extract token refresh logic
```

**Bad:**
```
feat(cart): Added quantity validation.  # past tense, period
fix: Fix bug                            # vague, capitalized
refactor: refactoring stuff             # gerund, unclear
```

---

## Body

Optional longer description:

```
fix(api): handle rate limit responses

The API now properly handles 429 responses by implementing
exponential backoff. Previously, requests would fail immediately
without retry attempts.

Closes #123
```

Rules:
- Blank line between subject and body
- Wrap at 72 characters
- Explain what and why, not how

---

## Footers

Metadata at the end:

```
feat(auth): implement SSO login

Implements single sign-on using SAML 2.0 protocol.

Closes #456
Reviewed-by: Alice
Co-authored-by: Bob <bob@example.com>
```

Common footers:
- `Closes #123` - Links/closes issue
- `Fixes #123` - Links/closes issue
- `Refs #123` - References issue
- `BREAKING CHANGE:` - Breaking change description
- `Reviewed-by:` - Reviewer name
- `Co-authored-by:` - Co-author (GitHub format)

---

## Examples

### Simple Feature

```
feat(search): add fuzzy matching support
```

### Bug Fix with Issue

```
fix(upload): prevent file corruption on timeout

Closes #789
```

### Breaking Change

```
feat(api)!: require API key for all endpoints

BREAKING CHANGE: Anonymous access is no longer supported.
All requests must include a valid API key in the header.

Migration guide: https://docs.example.com/api-keys
```

### Multiple Footers

```
feat(dashboard): add real-time notifications

Implements WebSocket-based notifications for dashboard updates.
Users will now see changes without page refresh.

Closes #234
Refs #198
Co-authored-by: Alice <alice@example.com>
```

### Revert

```
revert: feat(cart): add quantity validation

This reverts commit abc1234.

Reason: Caused regression in checkout flow.
```

---

## Validation Checklist

- [ ] Type is valid (feat, fix, docs, etc.)
- [ ] Description starts lowercase
- [ ] Description is imperative mood
- [ ] Description under 72 characters
- [ ] No period at end of description
- [ ] Body wrapped at 72 characters (if present)
- [ ] Breaking changes marked with `!` or footer
- [ ] Issue references use correct format
