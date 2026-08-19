<!-- markdownlint-disable -->

# Hardening Report: Azure--cli/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--cli/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable tags or branch names instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced tag or branch is moved to point to malicious code.

Failing references:
- add-labels.yml: actions/checkout@v1, julb/action-manage-label@v1
- build-release.yml: actions/checkout@v4, actions/setup-node@v4, ad-m/github-push-action@master
- ci-workflow.yml: actions/checkout@v4, azure/login@v1, actions/setup-node@v4
- defaultLabel.yml: actions/stale@v3 (×2)
- integration-test.yml: azure/login@v1, azure/cli@master (×4), actions/github-script@v3 (×3)
- pr-test.yml: actions/checkout@v4 (×2), actions/setup-node@v4 (×2), actions/github-script@v3 (×3)
- stale.yml: actions/stale@v3

Locations:

- `.github/workflows/add-labels.yml:9`
- `.github/workflows/add-labels.yml:11`
- `.github/workflows/build-release.yml:15`
- `.github/workflows/build-release.yml:18`
- `.github/workflows/build-release.yml:34`
- `.github/workflows/ci-workflow.yml:10`
- `.github/workflows/ci-workflow.yml:13`
- `.github/workflows/ci-workflow.yml:17`
- `.github/workflows/defaultLabel.yml:15`
- `.github/workflows/defaultLabel.yml:26`
- `.github/workflows/integration-test.yml:9`
- `.github/workflows/integration-test.yml:13`
- `.github/workflows/integration-test.yml:20`
- `.github/workflows/integration-test.yml:27`
- `.github/workflows/integration-test.yml:34`
- `.github/workflows/integration-test.yml:43`
- `.github/workflows/integration-test.yml:51`
- `.github/workflows/integration-test.yml:59`
- `.github/workflows/integration-test.yml:65`
- `.github/workflows/integration-test.yml:73`
- `.github/workflows/integration-test.yml:81`
- `.github/workflows/pr-test.yml:11`
- `.github/workflows/pr-test.yml:14`
- `.github/workflows/pr-test.yml:43`
- `.github/workflows/pr-test.yml:57`
- `.github/workflows/stale.yml:10`

### missing-permissions (severity: medium)

Six workflow files have no top-level `permissions:` block and no job-level `permissions:` blocks on any of their jobs. Without explicit permissions, GitHub Actions defaults to the repository's default token permissions (which may be broad), violating the principle of least privilege. Only build-release.yml has a correctly scoped top-level permissions block (`contents: write`).

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

Fixed all 7 workflow files. Pinned all external action references to full 40-character commit SHAs (actions/checkout v1/v4, julb/action-manage-label v1, actions/setup-node v4, ad-m/github-push-action master, azure/login v1, actions/stale v3, azure/cli master, actions/github-script v3) with original tag/branch preserved as inline comments. Added minimal top-level permissions blocks to the 6 affected files: add-labels.yml (contents:read, issues:write, pull-requests:write), ci-workflow.yml (contents:read), defaultLabel.yml (issues:write, pull-requests:write), integration-test.yml (contents:read), pr-test.yml (contents:read), stale.yml (issues:write, pull-requests:write). build-release.yml already had contents:write and was not in the missing-permissions list.

