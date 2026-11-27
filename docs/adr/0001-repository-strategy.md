# 0001: Repository strategy

- **Status:** Accepted
- **Date:** 2026-11-26 (accepted 2026-11-27)

## Context

The landing zone needs one place for IaC, pipelines and documentation that reviewers can read, with enforced protection on the main branch, on GitHub Free.

## Decision

- Single public repository with one Terraform root module ("stack") per layer under `stacks/`, numbered in deployment order, each with separate state.
- Public visibility, because branch rulesets do not apply to private repositories on GitHub Free. Public also enables secret scanning push protection.
- `main` is protected by the `protect-main` ruleset: changes only through pull requests, no force pushes, no deletion. Squash merge only.
- Commits use the GitHub noreply email address.
- Environment-specific IDs are never committed: GitHub Actions variables in CI, gitignored `*.tfvars` locally.

## Consequences

- Positive: one place to review; a failure in one layer's state cannot corrupt another; protection is enforced, not optional (verified: direct push rejected with GH013).
- Negative: cross-stack values must be passed explicitly (outputs / remote state); everything pushed is public, so evidence must be redacted and `git ls-files` checked before pushing.
- Required approvals are set to 0 because a solo maintainer cannot approve their own PR. The PR path still forces review and, from the CI phase, required checks.

## Alternatives considered

- **Private repository:** rejected; no enforceable branch protection on GitHub Free.
- **Repository per layer:** rejected; harder for a reviewer to follow and more pipeline duplication for one person.
- **Single Terraform state for everything:** rejected; every change would put the whole platform at risk.
