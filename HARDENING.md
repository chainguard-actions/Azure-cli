<!-- markdownlint-disable -->

# Hardening Report: Azure--cli/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--cli/v2.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All workflow files reference external actions using mutable tags or branch names instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks where a tag or branch can be silently updated to point to malicious code.

Failing references:
- add-labels.yml: actions/checkout@v1, julb/action-manage-label@v1
- build-release.yml: actions/checkout@v4, actions/setup-node@v4, ad-m/github-push-action@master
- ci-workflow.yml: actions/checkout@v4, azure/login@v1, actions/setup-node@v4
- defaultLabel.yml: actions/stale@v3 (×2)
- integration-test.yml: azure/login@v1, azure/cli@master (×4), actions/github-script@v3 (×3)
- pr-test.yml: actions/checkout@v4, actions/setup-node@v4, azure/login@v1, actions/github-script@v3 (×4)
- stale.yml: actions/stale@v3

Locations:

- `.github/workflows/add-labels.yml:9`
- `.github/workflows/add-labels.yml:11`
- `.github/workflows/build-release.yml:14`
- `.github/workflows/build-release.yml:17`
- `.github/workflows/build-release.yml:35`
- `.github/workflows/ci-workflow.yml:10`
- `.github/workflows/ci-workflow.yml:13`
- `.github/workflows/ci-workflow.yml:17`
- `.github/workflows/defaultLabel.yml:16`
- `.github/workflows/defaultLabel.yml:26`
- `.github/workflows/integration-test.yml:9`
- `.github/workflows/integration-test.yml:14`
- `.github/workflows/integration-test.yml:22`
- `.github/workflows/integration-test.yml:30`
- `.github/workflows/integration-test.yml:38`
- `.github/workflows/integration-test.yml:45`
- `.github/workflows/integration-test.yml:53`
- `.github/workflows/integration-test.yml:60`
- `.github/workflows/integration-test.yml:68`
- `.github/workflows/integration-test.yml:75`
- `.github/workflows/integration-test.yml:83`
- `.github/workflows/pr-test.yml:13`
- `.github/workflows/pr-test.yml:17`
- `.github/workflows/pr-test.yml:29`
- `.github/workflows/pr-test.yml:46`
- `.github/workflows/pr-test.yml:60`
- `.github/workflows/pr-test.yml:68`
- `.github/workflows/pr-test.yml:76`
- `.github/workflows/pr-test.yml:84`
- `.github/workflows/stale.yml:10`

### missing-permissions (severity: medium)

Six workflow files have no top-level `permissions:` block and no job-level `permissions:` blocks. Without explicit permissions, workflows run with the default token permissions (which may be read/write depending on repository settings), violating the principle of least privilege. Only build-release.yml has a permissions block.

Affected files: add-labels.yml, ci-workflow.yml, defaultLabel.yml, integration-test.yml, pr-test.yml, stale.yml

Locations:

- `.github/workflows/add-labels.yml:1`
- `.github/workflows/ci-workflow.yml:1`
- `.github/workflows/defaultLabel.yml:1`
- `.github/workflows/integration-test.yml:1`
- `.github/workflows/pr-test.yml:1`
- `.github/workflows/stale.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 7 workflow files:

1. add-labels.yml: Pinned actions/checkout@v1 → SHA, julb/action-manage-label@v1 → SHA; added permissions (contents:read, issues:write, pull-requests:write)
2. build-release.yml: Pinned actions/checkout@v4 → SHA, actions/setup-node@v4 → SHA, ad-m/github-push-action@master → SHA (already had permissions block)
3. ci-workflow.yml: Pinned actions/checkout@v4 → SHA, azure/login@v1 → SHA, actions/setup-node@v4 → SHA; added permissions (contents:read)
4. defaultLabel.yml: Pinned actions/stale@v3 → SHA (×2); added permissions (issues:write, pull-requests:write)
5. integration-test.yml: Pinned azure/login@v1 → SHA, azure/cli@master → SHA (×4), actions/github-script@v3 → SHA (×3); added permissions (contents:read)
6. pr-test.yml: Pinned actions/checkout@v4 → SHA (×2), actions/setup-node@v4 → SHA (×2), azure/login@v1 → SHA (×2), actions/github-script@v3 → SHA (×4); added permissions (contents:read)
7. stale.yml: Pinned actions/stale@v3 → SHA; added permissions (issues:write, pull-requests:write)

All SHAs were resolved using lookup_action_sha and are preserved with the original tag/branch as inline comments.

