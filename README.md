# Azure Enterprise Landing Zone

> Status: Phase 3, repository initialised. No Azure resources deployed from this repo yet.

## Business problem

<!-- What goes wrong for an organisation without a landing zone. 3-5 sentences. -->

## What this delivers

<!-- Management group hierarchy, policy guardrails, central logging/monitoring, hub networking, OIDC CI/CD. -->

## Architecture

<!-- Mermaid diagram goes here (docs/architecture/). -->

## Repository map

| Path | Contents |
|---|---|
| `stacks/` | One Terraform root module per layer, each with its own state, deployed in numeric order |
| `modules/` | Reusable child modules |
| `lib/policies/` | Custom Azure Policy definitions and initiatives |
| `docs/adr/` | Architecture decision records |
| `docs/runbooks/` | Deploy, rollback, teardown procedures |
| `docs/validation/` | Phase validation evidence (IDs redacted) |

## Cost

<!-- Estimate and guardrails (budget alerts). See docs/cost/. -->

## Security

<!-- Least privilege, OIDC (no secrets), policy enforcement. See docs/security/. -->

## Project phases

| Phase | Status |
|---|---|
| 1. Environment validation | Closed |
| 2. Azure subscription validation | Closed |
| 3. Repository initialisation | In progress |
