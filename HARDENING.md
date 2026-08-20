<!-- markdownlint-disable -->

# Hardening Report: Azure--cli/v2.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--cli/v2.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All `uses:` references across workflow files use mutable tags or branch names instead of full 40-character SHA commit hashes, making the workflows vulnerable to supply-chain attacks if the referenced action is compromised or the tag is moved. Failing references include: actions/checkout@v4, julb/action-manage-label@v1, actions/setup-node@v4, ad-m/github-push-action@master, azure/login@v2, azure/cli@master, actions/github-script@v3, actions/stale@v3.

Locations:

- `.github/workflows/add-labels.yml:10`
- `.github/workflows/add-labels.yml:12`
- `.github/workflows/build-release.yml:15`
- `.github/workflows/build-release.yml:18`
- `.github/workflows/build-release.yml:36`
- `.github/workflows/ci-workflow.yml:11`
- `.github/workflows/ci-workflow.yml:14`
- `.github/workflows/ci-workflow.yml:18`
- `.github/workflows/defaultLabel.yml:17`
- `.github/workflows/defaultLabel.yml:28`
- `.github/workflows/integration-test.yml:9`
- `.github/workflows/integration-test.yml:14`
- `.github/workflows/integration-test.yml:22`
- `.github/workflows/integration-test.yml:31`
- `.github/workflows/integration-test.yml:39`
- `.github/workflows/integration-test.yml:46`
- `.github/workflows/integration-test.yml:54`
- `.github/workflows/integration-test.yml:61`
- `.github/workflows/integration-test.yml:68`
- `.github/workflows/integration-test.yml:76`
- `.github/workflows/integration-test.yml:83`
- `.github/workflows/pr-test.yml:13`
- `.github/workflows/pr-test.yml:16`
- `.github/workflows/pr-test.yml:55`
- `.github/workflows/pr-test.yml:67`
- `.github/workflows/pr-test.yml:75`
- `.github/workflows/pr-test.yml:78`
- `.github/workflows/pr-test.yml:107`
- `.github/workflows/stale.yml:11`

### missing-permissions (severity: medium)

These workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any job, meaning they run with the default (potentially broad) token permissions: add-labels.yml, ci-workflow.yml, defaultLabel.yml, integration-test.yml, pr-test.yml, and stale.yml.

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

Fixed all unpinned `uses:` references across 7 workflow files by resolving each action tag/branch to its full 40-character SHA commit hash (preserving the original tag as a comment). Added minimal `permissions:` blocks to the 6 workflow files that were missing them: add-labels.yml (contents:read, issues:write, pull-requests:write), ci-workflow.yml (contents:read, id-token:write), defaultLabel.yml (issues:write, pull-requests:write), integration-test.yml (contents:read, id-token:write), pr-test.yml (contents:read), stale.yml (issues:write, pull-requests:write). build-release.yml already had a permissions block and was not in the missing-permissions finding.

