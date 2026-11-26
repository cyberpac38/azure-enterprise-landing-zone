# 0001: Repository strategy

- **Status:** Proposed
- **Date:** 2026-11-26

## Context

The landing zone needs one place for IaC, pipelines and documentation that reviewers can read, with protection on the main branch on GitHub Free.

## Decision

- Single public repository with one Terraform root module ("stack") per layer, each with separate state.
- Public visibility so branch rulesets and secret scanning push protection apply on GitHub Free.
- Commits use the GitHub noreply email.
- Environment-specific IDs are never committed: GitHub Actions variables in CI, gitignored `*.tfvars` locally.

## Consequences

<!-- e.g. cross-stack values via outputs/remote state; everything pushed is public. -->

## Alternatives considered

<!-- Private repo (no rulesets on Free), repo per layer, single state file. -->
