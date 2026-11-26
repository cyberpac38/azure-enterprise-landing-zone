# Lessons learned

| Date | Phase | What happened | What I changed |
|---|---|---|---|
| 2026-11-26 | 2 | Subscription Owner could not read management groups (AuthorizationFailed). | Elevated as Global Admin, assigned scoped roles at Tenant Root, disabled elevation. |
| 2026-11-26 | 2 | First remediation proposed Owner at Tenant Root. | Replaced with Management Group Contributor + Resource Policy Contributor (least privilege). |
