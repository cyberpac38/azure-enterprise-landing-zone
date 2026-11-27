# Phase 2: Azure subscription validation evidence

- **Closed:** 2026-11-26
- **Identifiers are redacted** (GUIDs show only their last 4 characters).

## Summary

| Check | Result | Notes |
|---|---|---|
| A1-A2 Subscription and tenant | PASS | Enabled, personal tenant |
| A3 Offer type | Recorded | Pay-As-You-Go, no spending limit |
| A5 Subscription RBAC | PASS | Owner |
| A6 Entra roles | PASS | Global Administrator (plus User/Intune Administrator: security-review item) |
| A7 Management group access | FAIL, then PASS | AuthorizationFailed until elevation + scoped role assignment |
| A8 App registration allowed | PASS | |
| A9 Resource providers | FAIL, then PASS | Microsoft.AlertsManagement registered |
| A10 Budget | FAIL, then PASS | LandingZone-Lab, US$25/month |
| S2 Root MG roles | PASS | Management Group Contributor + Resource Policy Contributor (Owner deliberately not used) |
| S3 Elevated access removed | PASS | No assignments at scope `/` |

## First run, raw output

```text
== A1
Subscription          SubscriptionId                        TenantId                              User                  State
--------------------  ------------------------------------  ------------------------------------  --------------------  -------
Azure subscription 1  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxc2ec  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxx2459  <redacted-account>  Enabled

== A2
{
  "domains": [
    "<tenant>.onmicrosoft.com"
  ],
  "name": "Default Directory"
}

== A3
{
  "locationPlacementId": "Public_2014-09-01",
  "quotaId": "PayAsYouGo_2014-09-01",
  "spendingLimit": "Off"
}

== A4
Upn
---------------------------------------------------------
<redacted-account>#EXT#@<tenant>.onmicrosoft.com

== A5
Role    Scope
------  ---------------------------------------------------
Owner   /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxc2ec
Owner   /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxc2ec

== A6
[
  "Global Administrator",
  "User Administrator",
  "Intune Administrator"
]

== A7
ERROR: (AuthorizationFailed) The client 'live.com#<redacted-account>' with object id 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxac31' does not have authorization to perform action 'Microsoft.Management/managementGroups/read' over scope '/providers/Microsoft.Management' or the scope is invalid. If access was recently granted, please refresh your credentials.
Code: AuthorizationFailed
Message: The client 'live.com#<redacted-account>' with object id 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxac31' does not have authorization to perform action 'Microsoft.Management/managementGroups/read' over scope '/providers/Microsoft.Management' or the scope is invalid. If access was recently granted, please refresh your credentials.
!! FAILED (often a permissions signal, keep this line)

== A7b


== A8
true

== A9
Microsoft.Management             Registered
Microsoft.PolicyInsights         Registered
Microsoft.Authorization          Registered
Microsoft.Network                Registered
Microsoft.Storage                Registered
Microsoft.KeyVault               Registered
Microsoft.OperationalInsights    Registered
Microsoft.Insights               Registered
Microsoft.AlertsManagement       NotRegistered
Microsoft.Security               Registered
Microsoft.Consumption            Registered
Microsoft.CostManagement         Registered
Microsoft.ManagedIdentity        Registered
Microsoft.Resources              Registered

== A10
WARNING: This command is in preview and under development. Reference and support levels: https://aka.ms/CLI_refstatus


```

## Budget (S5), raw output

```json
[
  {
    "alerts": {
      "actual_GreaterThan_100_Percent": {
        "contactEmails": [
          "<redacted-account>"
        ],
        "contactGroups": [],
        "contactRoles": [],
        "enabled": true,
        "operator": "GreaterThan",
        "threshold": 100.0,
        "thresholdType": "Actual"
      },
      "actual_GreaterThan_50_Percent": {
        "contactEmails": [
          "<redacted-account>"
        ],
        "contactGroups": [],
        "contactRoles": [],
        "enabled": true,
        "operator": "GreaterThan",
        "threshold": 50.0,
        "thresholdType": "Actual"
      },
      "actual_GreaterThan_80_Percent": {
        "contactEmails": [
          "<redacted-account>"
        ],
        "contactGroups": [],
        "contactRoles": [],
        "enabled": true,
        "operator": "GreaterThan",
        "threshold": 80.0,
        "thresholdType": "Actual"
      },
      "forecasted_GreaterThan_100_Percent": {
        "contactEmails": [
          "<redacted-account>"
        ],
        "contactGroups": [],
        "contactRoles": [],
        "enabled": true,
        "operator": "GreaterThan",
        "threshold": 100.0,
        "thresholdType": "Forecasted"
      }
    },
    "amount": 25.0,
    "name": "LandingZone-Lab",
    "timeGrain": "Monthly"
  }
]
```
