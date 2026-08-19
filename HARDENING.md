<!-- markdownlint-disable -->

# Hardening Report: Azure--cli/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--cli/v3.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference actions using mutable tags or branch names instead of pinned 40-character commit SHAs, making the workflows vulnerable to supply-chain attacks if those tags are moved or branches are force-pushed.

Failing references:
- ci-workflow.yml: actions/checkout@v4, azure/login@v2, actions/setup-node@v6
- build-release.yml: actions/checkout@v4, actions/setup-node@v6, ad-m/github-push-action@master
- integration-test.yml: azure/login@v3, azure/cli@master (×4), actions/github-script@v3 (×2)
- pr-test.yml: actions/checkout@v6, actions/setup-node@v6 (×2), actions/github-script@v3 (×2)
- add-labels.yml: actions/checkout@v4, julb/action-manage-label@v1
- defaultLabel.yml: actions/stale@v3 (×2)
- stale.yml: actions/stale@v3

Locations:

- `.github/workflows/ci-workflow.yml:11`
- `.github/workflows/ci-workflow.yml:14`
- `.github/workflows/ci-workflow.yml:18`
- `.github/workflows/build-release.yml:16`
- `.github/workflows/build-release.yml:20`
- `.github/workflows/build-release.yml:36`
- `.github/workflows/integration-test.yml:10`
- `.github/workflows/integration-test.yml:16`
- `.github/workflows/integration-test.yml:23`
- `.github/workflows/integration-test.yml:30`
- `.github/workflows/integration-test.yml:37`
- `.github/workflows/integration-test.yml:43`
- `.github/workflows/integration-test.yml:52`
- `.github/workflows/integration-test.yml:60`
- `.github/workflows/integration-test.yml:67`
- `.github/workflows/integration-test.yml:73`
- `.github/workflows/pr-test.yml:12`
- `.github/workflows/pr-test.yml:16`
- `.github/workflows/pr-test.yml:46`
- `.github/workflows/pr-test.yml:50`
- `.github/workflows/pr-test.yml:57`
- `.github/workflows/pr-test.yml:63`
- `.github/workflows/add-labels.yml:9`
- `.github/workflows/add-labels.yml:11`
- `.github/workflows/defaultLabel.yml:17`
- `.github/workflows/defaultLabel.yml:27`
- `.github/workflows/stale.yml:11`

### missing-permissions (severity: medium)

Six workflow files have no top-level `permissions:` key and no job-level `permissions:` key on any of their jobs. Without explicit permissions, the GITHUB_TOKEN is granted its default (broad) permissions, which violates the principle of least privilege.

Affected files:
- ci-workflow.yml: no permissions at top-level or job level
- integration-test.yml: no permissions at top-level or job level
- pr-test.yml: no permissions at top-level or job level (triggered on pull_request, making this especially risky)
- add-labels.yml: no permissions at top-level or job level
- defaultLabel.yml: no permissions at top-level or job level
- stale.yml: no permissions at top-level or job level

Locations:

- `.github/workflows/ci-workflow.yml:1`
- `.github/workflows/integration-test.yml:1`
- `.github/workflows/pr-test.yml:1`
- `.github/workflows/add-labels.yml:1`
- `.github/workflows/defaultLabel.yml:1`
- `.github/workflows/stale.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 7 workflow files:

1. unpinned-uses: Pinned all action references to full 40-char commit SHAs with original tag/branch as comment. Actions pinned: actions/checkout@v4, actions/checkout@v6, azure/login@v2, azure/login@v3, actions/setup-node@v6, ad-m/github-push-action@master, azure/cli@master, actions/github-script@v3, julb/action-manage-label@v1, actions/stale@v3.

2. missing-permissions: Added top-level permissions blocks to ci-workflow.yml (contents: read), integration-test.yml (contents: read), pr-test.yml (contents: read), add-labels.yml (issues: write + pull-requests: write), defaultLabel.yml (issues: write + pull-requests: write), and stale.yml (issues: write + pull-requests: write). build-release.yml already had permissions: contents: write and was not in the missing-permissions list.

