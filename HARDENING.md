<!-- markdownlint-disable -->

# Hardening Report: szenius--set-timezone/v2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **szenius--set-timezone/v2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All four workflow files reference `actions/checkout@v4`, which is a mutable tag rather than a pinned 40-character commit SHA. If the tag is moved (e.g. by a supply-chain compromise), the action will silently execute different code. Each `uses:` line should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/test_linux_gmt8.yml:19`
- `.github/workflows/test_macos_gmt8.yml:18`
- `.github/workflows/test_run_action.yml:19`
- `.github/workflows/test_windows_gmt8.yml:18`

### missing-permissions (severity: medium)

None of the four workflow files declare a top-level `permissions:` block, and no individual job within any of them declares job-level `permissions:` either. Without explicit permissions, GitHub Actions defaults to the repository's default token permissions (often `write-all` for older repositories), granting jobs more access than they need. A minimal `permissions: {}` or specific scopes (e.g. `contents: read`) should be added to each workflow.

Locations:

- `.github/workflows/test_linux_gmt8.yml:1`
- `.github/workflows/test_macos_gmt8.yml:1`
- `.github/workflows/test_run_action.yml:1`
- `.github/workflows/test_windows_gmt8.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four workflow files (.github/workflows/test_linux_gmt8.yml, test_macos_gmt8.yml, test_run_action.yml, test_windows_gmt8.yml):
1. unpinned-uses: Pinned `actions/checkout@v4` to full commit SHA `actions/checkout@11d5960a326750d5838078e36cf38b85af677262 # v4` in all four files.
2. missing-permissions: Added top-level `permissions: {}` block to all four workflow files to enforce least-privilege access.

