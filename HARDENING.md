<!-- markdownlint-disable -->

# Hardening Report: actions--dependency-review-action/v4.9.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions--dependency-review-action/v4.9.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags instead of immutable 40-character SHA commit hashes. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code.

Failing references:
- .github/workflows/ci.yml: `actions/checkout@v6`, `actions/setup-node@v6` (used in both `test` and `lint` jobs)
- .github/workflows/codeql.yml: `actions/checkout@v6`, `github/codeql-action/init@v4`, `github/codeql-action/analyze@v4`
- .github/workflows/dependency-review.yml: `actions/checkout@v6`
- .github/workflows/stale.yaml: `actions/stale@v10.2.0`

Locations:

- `.github/workflows/ci.yml:17`
- `.github/workflows/ci.yml:18`
- `.github/workflows/ci.yml:27`
- `.github/workflows/ci.yml:28`
- `.github/workflows/codeql.yml:19`
- `.github/workflows/codeql.yml:23`
- `.github/workflows/codeql.yml:36`
- `.github/workflows/dependency-review.yml:11`
- `.github/workflows/stale.yaml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all mutable action tag references to immutable full 40-character commit SHAs across 4 workflow files:
- .github/workflows/ci.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6 (2×), actions/setup-node@v6 → @249970729cb0ef3589644e2896645e5dc5ba9c38 # v6 (2×)
- .github/workflows/codeql.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6, github/codeql-action/init@v4 → @e0647621c2984b5ed2f768cb892365bf2a616ad1 # v4, github/codeql-action/analyze@v4 → @e0647621c2984b5ed2f768cb892365bf2a616ad1 # v4
- .github/workflows/dependency-review.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803 # v6
- .github/workflows/stale.yaml: actions/stale@v10.2.0 → @b5d41d4e1d5dceea10e7104786b73624c18a190f # v10.2.0
All SHAs were resolved via lookup_action_sha and original tags preserved as inline comments.

