# 0002: Naming convention and primary region

- **Status:** Accepted
- **Date:** 2026-11-27

## Context

Resource names and management group IDs are hard or impossible to change after creation. They need to be decided before the first deployment.

## Decision

**Primary region:** East US 2 (`eus2`). Reason: East US 2 was selected because it offers broad Azure service availability, Availability Zones support, competitive pricing, and a paired disaster recovery region (Central US). It is also geographically close enough to provide acceptable latency for development and testing from the Caribbean while remaining one of Azure's most commonly supported regions.

**Resource names** follow Microsoft Cloud Adoption Framework abbreviations: `<type>-<workload>-<env>-<region>-<nnn>`, for example `rg-mgmt-prod-eus2-001` and `law-mgmt-prod-eus2-001`. Exceptions: storage accounts (lowercase alphanumeric, max 24, e.g. `sttfstateprodeus2001`), Key Vault (max 24), and subnets with fixed names (`AzureFirewallSubnet`, `GatewaySubnet`, `AzureBastionSubnet`).

**Environments:** `prod`, `nonprod`, `sbx`.

**Management groups** (mirrors the Microsoft ALZ reference hierarchy):

| ID | Parent |
|---|---|
| `mg-alz` | Tenant Root Group |
| `mg-platform` | `mg-alz` |
| `mg-management`, `mg-connectivity`, `mg-identity` | `mg-platform` |
| `mg-landingzones` | `mg-alz` |
| `mg-corp`, `mg-online` | `mg-landingzones` |
| `mg-sandbox`, `mg-decommissioned` | `mg-alz` |

**Required tags:** `owner`, `environment`, `workload`, `cost-center`, `managed-by`, `repository`. To be enforced by Azure Policy.

## Consequences

- Names are predictable and sortable, and policy can validate them.
- The region code is embedded in names: a second region means new resources, not renamed ones.

## Alternatives considered

- **Free-form names:** rejected; can't be validated or reasoned about at scale.
- **No intermediate root (`mg-alz`):** rejected; policy and role assignments would have to sit on the Tenant Root Group, which can't be scoped down later.
