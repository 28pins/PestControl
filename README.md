# PestControl 🪲

An AI-powered toolkit that automates bug detection and routes fixes to the
**GitHub Copilot coding agent** — which then opens a pull request with the
bug fixed.

---

## How it works

```
Push / PR  ──►  Bug Detection workflow
                  │
                  ├─ runs tests + linters for your language
                  │
                  └─ failure? ──► creates GitHub Issue (label: bug)
                                        │
                              Copilot Autofix workflow
                                        │
                                  assigns issue to
                                  @github-copilot
                                        │
                              Copilot coding agent
                                  ├─ analyzes the issue
                                  ├─ writes a fix + test
                                  └─ opens a Pull Request
```

---

## Files included

| File | Purpose |
|---|---|
| `.github/workflows/bug-detection.yml` | Runs tests & linters on every push/PR; creates a `bug`-labeled issue on failure |
| `.github/workflows/copilot-autofix.yml` | Listens for `bug` labels; assigns the issue to the Copilot coding agent |
| `.github/ISSUE_TEMPLATE/bug_report.yml` | Structured bug report template; filing a report triggers the same automation |
| `.github/copilot-instructions.md` | Repository-level instructions that guide the Copilot agent's fix strategy |

---

## Add this to any repository

1. **Copy the `.github/` folder** into the root of your repository.
2. **Enable the GitHub Copilot coding agent** for your repository:
   _Settings → Copilot → Coding agent → Allow_
3. **Ensure Actions have write permissions**:
   _Settings → Actions → General → Workflow permissions → Read and write_
4. Push a commit — the Bug Detection workflow will run automatically.

### Supported languages (auto-detected)

| Language | Test runner | Linter |
|---|---|---|
| JavaScript / TypeScript | `npm test` | `npm run lint` |
| Python | `pytest` | `flake8` |
| Go | `go test ./...` | `go vet` |
| Rust | `cargo test` | `cargo clippy` |
| Ruby | `bundle exec rspec` | — |
| Java | `mvn test` | — |
| C++ | `ctest` (CMake) / `make test` | `cppcheck` |

---

## Manual bug report

Use the **Bug Report** issue template in _Issues → New issue_ to manually
describe a bug. The Copilot Autofix workflow will pick it up automatically.

---

## Requirements

- GitHub Copilot license (Individual, Business, or Enterprise) with the
  **coding agent** feature enabled.
- GitHub Actions enabled for the repository.
- Default branch write access for the Actions token
  (`contents: write`, `issues: write`, `pull-requests: write`).
