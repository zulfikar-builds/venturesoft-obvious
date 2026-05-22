# Obvious repo guidance

<!-- obvious-install: skill=autobuild-setup, skill-version=1.0.1, template-version=1 -->

This repo uses `.obvious/` for reviewed Autobuild guidance.

Before editing, suggest the smallest relevant set of `.obvious` files for the task. Match candidate files by reading their frontmatter.

## Codebase Map

Python-based project. No application source directories exist yet — they will be added as the codebase grows.

| Path | Purpose |
|---|---|
| `README.md` | Project overview — `# venturesoft-obvious` |
| `.obvious/` | Autobuild repo contract (this directory) |
| `.obvious/review/overlay.md` | Python-specific code review quality gates |
| `.github/workflows/ci.yml` | GitHub Actions CI pipeline (lint, format, typecheck, test) |

## Repo Guidance for Autobuild

<!-- synthesized from: README.md + Python toolchain configured 2026-05-22 -->

- **Repo:** `zulfikar-builds/venturesoft-obvious`
- **Description:** Python project. CI, linting, type checking, and test infrastructure are configured. Source code directories will be added as the project grows.
- **Default base branch:** `main`
- **Merge method:** squash
- **Language:** Python 3.11+

### CI Commands

| Command | Purpose |
|---|---|
| `ruff check .` | Lint — fast Python linter (replaces flake8/isort/pycodestyle) |
| `ruff format --check .` | Format check — verify code is formatted consistently |
| `mypy . --strict --ignore-missing-imports` | Type check — strict mypy, no implicit `Any` |
| `pytest --cov --cov-report=term-missing` | Run tests with coverage report |

### Toolchain

- **Linter:** `ruff` — configure via `ruff.toml` or `[tool.ruff]` in `pyproject.toml`
- **Type checker:** `mypy` in strict mode — configure via `mypy.ini` or `[tool.mypy]` in `pyproject.toml`
- **Test runner:** `pytest` with `pytest-cov` for coverage
- **Dependencies:** declare in `requirements.txt` or `pyproject.toml`; CI installs whichever exists

### Conventions

- All functions must have type annotations (parameters and return type)
- Public APIs require docstrings
- Tests live in `tests/` (or colocated `test_*.py` files); use `pytest` style, not `unittest`
- CI runs on every PR to `main` and every push to `main`
- As source directories are added, update the Codebase Map above and this guidance section

## Sandbox Snapshot

- **Snapshot ID:** N/A
- **Captured:** N/A
- **Dev stack healthy:** yes (trivially — no dev stack present)

> **Warning:** Sandbox snapshot failed: `computer-ops snapshot` returned `Computer not found` — the setup worker sandbox ID was not registered in the workspace. Continuing without snapshot. `snapshotId: null`.

## Bibliography

Bibliography scan ran at install time via `bibliography-operations` (operation: `get_map`).

- **Result:** No concepts found — expected for a minimal repo with only a README.
- **Scan status:** bibliography_tool_available, scan returned empty map.
- As codebase concepts are added, run bibliography scan again to populate this section.

## Security Scan

> **Note:** security_scan_not_triggered — `trigger-security-onboarding` returned `Missing context: requires a repositoryId`. Trigger manually using the `trigger-security-onboarding` tool with commit SHA `9fcd34c2bd2c4a036c191420f06fa42e7344dcde` and the correct `repositoryId` once it is registered in the Obvious platform.

## Runbooks

Populated by autobuild-runbooks skill when requested. See `.obvious/runbooks/` after that skill runs.

---

<!-- validation-summary:v1 -->
- **Last validated:** 2026-05-19T23:26:00Z
- **Result:** pass
- **Verified commands:**
  - No commands applicable — repo has no runtime, no package manager, no services, no application.
- **Blockers encountered:** none
<!-- /validation-summary -->
