# Phase 1: Environment validation evidence

- **Closed:** 2026-11-25, with carry-overs closed in Phase 3
- **Platform:** Ubuntu 24.04.5 LTS on WSL

| Check | Result | Evidence |
|---|---|---|
| Azure CLI | PASS | 2.91.0 |
| Terraform | PASS | 1.17.2 |
| Git | PASS | 2.43.0 |
| GitHub CLI | PASS | 2.103.3 |
| TFLint | PASS | 0.66.0 |
| Checkov | PASS | 3.3.30 |
| Terraform smoke test (init + validate, azurerm ~> 4.0) | PASS | success, nothing created in Azure |
| Node.js | N/A | not required (Terraform/tflint are Go, Checkov is Python) |
| Git identity (noreply), gh `workflow` scope, VS Code extensions in WSL | PASS | verified in Phase 3 (R1-R4) |

Evidence was reported as a summary of version output.
