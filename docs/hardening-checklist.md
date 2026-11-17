# VoltMart Electronics — Server Hardening Checklist

**Document ID:** VM-HARDEN-CHK-001  
**Version:** 0.1 (Task 1 planning draft)  
**Date:** 17 November 2026  
**Status:** Paper checklist; no lab or production changes  
**Owner:** Muhammad Ubaid

## 1. Purpose

Define a risk-based server hardening baseline for VoltMart Electronics. The checklist is intended to guide later implementation and verification. It is not evidence of implementation or CIS compliance.

## 2. Scope and assumptions

The client has not provided its actual OS, server inventory, hosting provider, network diagram, or application architecture. This draft provisionally assumes Ubuntu Server 24.04 LTS, Nginx, a retail application, PostgreSQL, SSH administration, and an external payment processor.

Confirm these assumptions before implementation. If the operating system or version changes, replace the benchmark reference with the exact applicable CIS Benchmark.

**Benchmark reference:** CIS Ubuntu Linux 24.04 LTS Benchmark v2.0.0, available from [CIS](https://www.cisecurity.org/benchmark/ubuntu_linux). Check each exact recommendation and applicability in the official benchmark PDF. The VM IDs below are project tracking IDs, not CIS recommendation IDs.

## 3. Status definitions

- **Not Assessed:** Not yet reviewed against the actual host and benchmark.
- **Planned:** An implementation approach is proposed.
- **Implemented:** Configuration has been applied in an authorized environment.
- **Verified:** A test and evidence confirm the requirement.
- **Exception:** A documented business or technical reason justifies deviation.

For Task 1, keep controls at **Not Assessed** or **Planned**. Do not mark them Implemented or Verified.

## 4. Checklist

| Project ID | Control / requirement | Why it matters to VoltMart | Priority | Verification evidence for later lab | Status |
|---|---|---|---|---|---|
| VM-01 | Confirm supported OS release, version, architecture, and server role; use the matching CIS Benchmark. | Prevents applying an incorrect baseline to the retail host. | Critical | OS inventory and benchmark/version record. | Not Assessed |
| VM-02 | Establish a patch process for OS and installed packages, including emergency security updates. | Reduces exposure to known vulnerabilities in order and inventory services. | Critical | Package inventory, update logs, approved patch record. | Planned |
| VM-03 | Remove or disable unnecessary packages and software after dependency review. | Reduces attack surface without breaking retail operations. | High | Installed-package inventory and service-owner approval. | Planned |
| VM-04 | Inventory listening ports and disable unnecessary network-facing services. | Limits paths into customer, order, and stock systems. | Critical | Before/after listening-port inventory; approved port list. | Planned |
| VM-05 | Select and configure one host firewall management approach; default-deny inbound and allow only documented business traffic. | Prevents unintended public access to internal services. | Critical | Firewall ruleset and allowed-port test. | Planned |
| VM-06 | Restrict SSH to approved administrator source networks or a secure management path. | Limits remote administration exposure. | Critical | SSH configuration review and permitted/denied connection tests. | Planned |
| VM-07 | Disable direct SSH root login; use named administrator accounts and controlled privilege escalation. | Improves accountability and reduces high-privilege exposure. | Critical | Effective SSH configuration and login test. | Planned |
| VM-08 | Prefer SSH public-key authentication; disable password-based SSH only after key access and recovery access are proven. | Reduces password-guessing risk while avoiding administrator lockout. | High | Key login test, password-login denial test, recovery plan. | Planned |
| VM-09 | Apply least privilege to users, groups, sudo, and administrative commands. | Store employees and application processes should not have server-wide control. | Critical | Account/group/sudoers review and negative privilege test. | Planned |
| VM-10 | Use dedicated non-login service accounts for application and supporting services where supported. | Limits the impact of an application compromise. | High | Service-account inventory and privilege review. | Planned |
| VM-11 | Define password, account-lockout, and authentication policy appropriate to the identity system. Prefer MFA for privileged access where supported. | Protects staff and administrator identities. | High | Policy review and controlled authentication tests. | Planned |
| VM-12 | Enable and review AppArmor profiles for supported services; document justified exceptions. | Restricts what a compromised process can access. | High | AppArmor status, profile inventory, application regression tests. | Planned |
| VM-13 | Set secure ownership and permissions for system files, application configuration, secrets, and data directories. | Protects customer records, order exports, and payment credentials. | Critical | Permission audit and unauthorized-read/write tests. | Planned |
| VM-14 | Centralize or securely retain system and application logs; restrict log access and define retention. | Supports investigation of account misuse, order tampering, and outages. | High | Sample logs, access review, retention configuration. | Planned |
| VM-15 | Enable appropriate audit records for authentication, privilege use, and security-relevant changes. | Provides traceability for administrator and configuration activity. | High | Audit policy and sample event evidence. | Planned |
| VM-16 | Configure reliable time synchronization. | Makes security events and order-related incident timelines comparable. | Medium | Time-sync status and timestamp consistency check. | Planned |
| VM-17 | Configure security updates with a defined maintenance window, monitoring, and rollback procedure. | Reduces vulnerability exposure while protecting store uptime. | High | Update policy, maintenance record, service smoke test. | Planned |
| VM-18 | Encrypt backups, restrict backup credentials, keep an appropriately isolated copy, and test restoration. | Protects inventory and order continuity against ransomware or data loss. | Critical | Backup policy, access review, restore-test record. | Planned |
| VM-19 | Bind PostgreSQL to the required private interface; restrict network access and use least-privilege database roles. | Prevents public database exposure and limits customer/order data access. | Critical | Listener configuration, firewall review, authorized/unauthorized connection tests. | Planned |
| VM-20 | Require TLS for public web traffic; use a valid certificate and review security headers and TLS configuration. | Protects customer sessions and checkout communication in transit. | High | TLS configuration review and external test against authorized lab hostname. | Planned |
| VM-21 | Separate production, staging, and development; do not use real customer data in development. | Prevents test activity and weaker environments from exposing production data. | High | Environment/network diagram and data-handling review. | Planned |
| VM-22 | Monitor CPU, memory, disk, network, and critical service health; define alert thresholds. | Helps preserve checkout and inventory availability during busy periods. | Medium | Baseline metrics, alert test, capacity review. | Planned |
| VM-23 | Document incident response: escalation, containment, evidence preservation, recovery, and communications. | Supports a coordinated response to ransomware, account compromise, or data exposure. | High | Approved runbook and tabletop exercise record. | Planned |
| VM-24 | Review user accounts, SSH keys, privileged groups, and access rights on a schedule and on staff departure. | Removes access that is no longer required. | High | Periodic access review and leaver checklist. | Planned |
| VM-25 | Protect payment-provider API keys and other secrets; keep them out of source control, logs, and client-side code. | Prevents payment integration abuse and unauthorized transactions. | Critical | Secret-storage design and repository/log review. | Planned |
| VM-26 | Apply application-level authorization to customer, order, refund, and inventory functions. | Prevents one customer or employee from accessing or changing another party's records. | Critical | Role/ownership access-control test plan. | Planned |

## 5. Retail-specific network policy proposal

This is a planning example only; actual ports and network zones must be confirmed with the client.

| Service | Proposed exposure | Rule |
|---|---|---|
| HTTPS (TCP 443) | Public web entry point | Allow to reverse proxy only. |
| HTTP (TCP 80) | Public, if needed | Redirect to HTTPS; otherwise close. |
| SSH (TCP 22) | Management network only | Deny from the public internet. |
| PostgreSQL (TCP 5432) | Private application/database network only | Never expose publicly. |
| Monitoring/log shipping | Private management path | Allow only to approved monitoring endpoints. |

Do not assume these ports are currently open. Confirm the architecture and actual service requirements before writing firewall rules.

## 6. Business continuity and performance constraints

- Schedule disruptive maintenance outside approved peak retail periods.
- Measure CPU, memory, disk I/O, network use, and application response time before and after later changes.
- Confirm checkout, product search, stock updates, order creation, and administrative workflows still function.
- Keep a tested rollback path for firewall, SSH, package, and service changes.
- Do not disable a service until its owner and dependencies are understood.
- Define recovery point and recovery time objectives with the client; do not invent targets.

## 7. Exceptions register

Every exception must record: control ID, reason, business owner, risk, compensating control, approval date, expiry/review date, and evidence. No exception is approved by this draft.

## 8. Sign-off

| Role | Name | Approval/date |
|---|---|---|
| Client system owner | To be confirmed | Pending |
| Application owner | To be confirmed | Pending |
| Security reviewer | To be confirmed | Pending |
| Intern | Muhammad Ubaid | Draft author |

**Task 1 conclusion:** This document establishes a proposed hardening baseline and verification plan. No server has been changed, scanned, or certified as compliant.
