# VoltMart Electronics — Task 1 Test and Verification Plan

**Document ID:** VM-HARDEN-TEST-001  
**Version:** 0.1 (planning only)  
**Status:** No tests executed; no lab exists yet

## 1. Purpose

Define how later tasks will verify the hardening checklist safely. This is a written test plan, not a test report. All execution is limited to an owned lab, a free legal practice platform, or a system with explicit written authorization.

## 2. Preconditions and safety

Before testing:
1. Confirm OS/version, architecture, server role, network diagram, service dependencies, and business owner.
2. Obtain written authorization defining target IP/hostname, allowed test methods, time window, and emergency contact.
3. Use synthetic VoltMart data only; never use real customer, payment, or employee records.
4. Take a restorable snapshot/backup before configuration changes.
5. Keep console or out-of-band recovery access before changing SSH or firewall rules.
6. Define stop conditions: unexpected service outage, data loss, resource exhaustion, or any activity outside scope.
7. Record tool versions, timestamps, commands, expected results, actual results, and evidence.

## 3. Test cases

| Test ID | Area | Test scenario | Expected result | Failure path / negative test | Evidence |
|---|---|---|---|---|---|
| T-01 | Asset baseline | Record OS release, installed packages, services, listening ports, CPU, RAM, and disk. | Inventory is complete and reproducible. | Missing permission or unavailable command is recorded as a gap, not guessed. | Baseline inventory. |
| T-02 | Updates | In lab, check available security updates and apply an approved update set. | Updates complete and critical services remain healthy. | Simulate a failed update in a disposable snapshot; verify recovery/rollback process. | Update log and service smoke-test results. |
| T-03 | Firewall | From an authorized lab client, test approved HTTPS and management access. | Only documented inbound paths are reachable. | Attempt connection to a deliberately unapproved lab port; it should be blocked. | Firewall rules and connection results. |
| T-04 | SSH | Test named administrator key login from approved source. | Authorized key login works and root login is denied. | Test from an unapproved source or with an invalid key; access is denied. | Sanitized SSH config and test log. |
| T-05 | Privileges | Review user groups and sudo permissions; test approved admin task. | Only authorized admins can perform privileged actions. | Standard account attempts privileged action; request is denied. | Account/permission review. |
| T-06 | Services | Compare active services and listening ports with approved inventory. | Required services run; unnecessary services are disabled. | A required service is found stopped; restore it and document dependency. | Service/port inventory and application smoke test. |
| T-07 | PostgreSQL | From the application host, test approved database connectivity. | Application role can perform only required operations. | Public/unapproved client connection and excessive database privilege are denied. | Sanitized DB access results and role review. |
| T-08 | TLS/web | Inspect the lab HTTPS endpoint and security headers. | Valid certificate, secure redirect, and approved headers are present. | Expired/invalid certificate or HTTP-only path is detected and reported. | TLS/header scan output. |
| T-09 | File permissions/secrets | Review application config, backup, and secret-file permissions; search a test repository for a dummy secret. | Sensitive files are restricted and test secret is detected. | Unauthorized test user cannot read secret; dummy secret does not pass repository checks. | Permission report and scanner output; redact values. |
| T-10 | Logging/audit | Generate a controlled failed login and privileged action in lab. | Events are timestamped and available to authorized reviewers. | If an event is absent, raise a logging defect and verify alert/escalation path. | Sanitized log/audit event. |
| T-11 | Backup/restore | Restore synthetic product and order data into an isolated lab target. | Restored data is readable and integrity checks pass. | Corrupt or unavailable test backup is detected; recovery failure is escalated. | Restore log and record-count/hash comparison. |
| T-12 | Retail application | Run synthetic product search, stock update, customer login, cart/checkout sandbox, and order lookup. | Authorized workflows succeed and data is consistent. | Customer A attempts to access Customer B's order; access is denied. | Test results with synthetic IDs only. |
| T-13 | Performance | Capture baseline and post-change CPU, memory, disk I/O, network, and response time under repeatable synthetic load. | No unexplained degradation beyond client-approved thresholds. | If thresholds are exceeded, stop, investigate, and roll back if necessary. | Before/after metrics and workload details. |
| T-14 | Recovery | Exercise documented rollback for a lab firewall or SSH change. | Administrator access and required application services are restored. | Rollback fails; use console snapshot recovery and record incident. | Change log and recovery evidence. |

## 4. Acceptance criteria

A test is **Pass** only when:
- The actual result matches the expected result.
- Evidence is saved and does not expose secrets or personal data.
- The test was run inside the authorized scope.
- Relevant business workflows remain functional.

A test is **Fail** when the expected security outcome is not achieved. A test is **Blocked** when prerequisites or authorization are missing. Do not label unexecuted tests as passed.

Client-approved performance thresholds, recovery objectives, and maintenance windows must be agreed before implementation. This plan intentionally does not invent numeric service-level targets.

## 5. Test report template

| Field | Value |
|---|---|
| Test ID | |
| Date/time and timezone | |
| Tester | |
| Authorized target | |
| Tool/version | |
| Preconditions | |
| Steps performed | |
| Expected result | |
| Actual result | |
| Status (Pass/Fail/Blocked) | |
| Evidence location | |
| Defect / risk reference | |
| Remediation and retest | |

## 6. Overall Task 1 test status

**Not executed.** Task 1 is paper-only. The above cases are planned for later authorized lab tasks.
