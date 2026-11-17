# VoltMart Electronics — Initial Risk Register

**Status:** Initial planning assumptions; validate with the client.

| Risk ID | Business asset | Threat / scenario | Business impact | Initial priority | Proposed treatment |
|---|---|---|---|---|---|
| R-01 | Customer accounts and personal data | Unauthorized access through weak credentials or excessive privileges. | Privacy breach, customer trust loss, legal/regulatory exposure. | Critical | MFA where supported, least privilege, SSH hardening, access reviews, audit logs. |
| R-02 | Orders and refunds | Employee or attacker manipulates orders/refunds. | Financial loss, disputes, fraud. | Critical | Role-based authorization, immutable audit trail, approval controls for sensitive actions. |
| R-03 | Inventory database | Unauthorized stock changes or database compromise. | Incorrect stock, lost sales, operational disruption. | High | Private DB access, least-privilege roles, backups, monitoring. |
| R-04 | Payment integration | Payment API secret exposed in code, logs, or repository. | Unauthorized payment activity or integration abuse. | Critical | Secret manager/environment injection, rotation, repository scanning, log redaction. |
| R-05 | Retail application/server | Unpatched service or unnecessary exposed port exploited. | Service compromise and downtime. | Critical | Patch management, service reduction, firewall, vulnerability review. |
| R-06 | Store operations | Firewall or SSH change blocks legitimate administration or checkout dependency. | Extended outage during trading hours. | High | Change windows, console recovery, snapshots, rollback and smoke tests. |
| R-07 | Backups | Ransomware or compromised credentials delete or encrypt backups. | Loss of order/inventory records and prolonged recovery. | Critical | Isolated encrypted backups, separate credentials, restore tests. |
| R-08 | Logs and incident evidence | Logs missing, altered, or accessible to unauthorized users. | Delayed investigation and weak accountability. | High | Centralized/restricted logging, audit policy, retention and monitoring. |

## Risk scoring note
Priorities are preliminary qualitative judgments, not a completed likelihood-impact assessment. Re-score after the client confirms architecture, data classification, exposure, business impact, and existing controls.
