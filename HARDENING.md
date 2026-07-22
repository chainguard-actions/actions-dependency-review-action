<!-- markdownlint-disable -->

# Hardening Report: actions--dependency-review-action/v5.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions--dependency-review-action/v5.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags instead of full 40-character commit SHA hashes. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code. Failing references:
- ci.yml: actions/checkout@v6, actions/setup-node@v6
- codeql.yml: actions/checkout@v6, github/codeql-action/init@v4, github/codeql-action/analyze@v4
- dependency-review.yml: actions/checkout@v6
- stale.yaml: actions/stale@v10.2.0

Locations:

- `.github/workflows/ci.yml:16`
- `.github/workflows/ci.yml:17`
- `.github/workflows/codeql.yml:28`
- `.github/workflows/codeql.yml:32`
- `.github/workflows/codeql.yml:38`
- `.github/workflows/dependency-review.yml:10`
- `.github/workflows/stale.yaml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all mutable action tags to full commit SHAs across four workflow files:
- ci.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803, actions/setup-node@v6 → @249970729cb0ef3589644e2896645e5dc5ba9c38 (both jobs)
- codeql.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803, github/codeql-action/init@v4 → @e0647621c2984b5ed2f768cb892365bf2a616ad1, github/codeql-action/analyze@v4 → @e0647621c2984b5ed2f768cb892365bf2a616ad1 (file was rewritten after corruption during sequential edits)
- dependency-review.yml: actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803
- stale.yaml: actions/stale@v10.2.0 → @b5d41d4e1d5dceea10e7104786b73624c18a190f
All original tag names preserved as inline comments for readability.

