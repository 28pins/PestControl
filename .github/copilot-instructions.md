# Copilot Coding Agent Instructions

These instructions are read automatically by the GitHub Copilot coding agent
whenever it is assigned an issue in this repository.

## Goal

Your job is to **find the root cause of the bug described in the issue and
produce the smallest correct fix**.  Open a pull request once the fix is ready.

## General principles

- **Minimal change** – touch only the lines needed to fix the bug.  Do not
  refactor, reformat, or clean up unrelated code.
- **Tests first** – before changing production code, add or update a test that
  reproduces the failure.  The test must fail on the current code and pass
  after your fix.
- **Explain your reasoning** – include a short prose explanation in the PR
  description covering: root cause, fix summary, and how the new/updated test
  validates the fix.
- **Security** – do not introduce new security vulnerabilities.  If the bug is
  security-related, note that in the PR description.

## Workflow

1. Read the issue carefully, including the **Hints for Copilot** section if
   present.
2. Identify the failing test or reproduce the bug with a new test.
3. Locate the source of the bug (use the hints, stack traces, and logs in the
   issue body).
4. Implement the fix.
5. Run existing tests to confirm nothing regressed.
6. Open a pull request targeting the default branch with the label `bug-fix`.

## Pull request format

```
fix: <concise description of the bug that was fixed>

Closes #<issue-number>

### Root cause
<1–3 sentences explaining why the bug occurred>

### Fix
<1–3 sentences describing the change made>

### Testing
<Describe the test(s) added or updated and how they validate the fix>
```

## Language-specific notes

| Language | Test runner | Lint / type-check |
|---|---|---|
| JavaScript / TypeScript | `npm test` | `npm run lint` |
| Python | `pytest` | `flake8`, `mypy` |
| Go | `go test ./...` | `go vet ./...` |
| Rust | `cargo test` | `cargo clippy` |
| Ruby | `bundle exec rspec` | `rubocop` |
| Java | `mvn test` | — |
| C++ | `ctest` (CMake) / `make test` | `cppcheck` |
| Arduino | `arduino-cli compile` | — |

Run the appropriate commands for this repository before opening the PR to
confirm all checks pass.
