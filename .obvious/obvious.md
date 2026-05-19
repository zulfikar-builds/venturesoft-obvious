# Obvious repo guidance

<!-- obvious-install: skill=autobuild-setup, skill-version=1.0.1, template-version=1 -->

This repo uses `.obvious/` for reviewed Autobuild guidance.

Before editing, suggest the smallest relevant set of `.obvious` files for the task. Match candidate files by reading their frontmatter.

## Codebase Map

This is a minimal repository. No application source directories exist at this time.

| Path | Purpose |
|---|---|
| `README.md` | Project overview — `# venturesoft-obvious` |
| `.obvious/` | Autobuild repo contract (this directory) |

## Repo Guidance for Autobuild

<!-- synthesized from: README.md (only file present at install time) -->

- **Repo:** `zulfikar-builds/venturesoft-obvious`
- **Description:** Minimal bootstrap repo — a single README with `# venturesoft-obvious`. No runtime, no package manager, no services, no CI workflows.
- **Default base branch:** `main`
- **Merge method:** squash
- **No test commands** — no test framework present at install time.
- **No lint/typecheck** — no toolchain present at install time.
- **No build process** — static content only.
- As this repo grows, update this guidance section to reflect new conventions.

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
