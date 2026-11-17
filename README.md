# VoltMart Electronics — Server Hardening (Task 1)

**Intern:** Muhammad Ubaid  
**Client:** VoltMart Electronics (fictional training client)  
**Task:** CIS-based server hardening checklist — paper planning only  
**Status:** Task 1 documentation; no server changes or lab testing performed  
**Date:** 17 November 2026

## Project objective
Create a practical, risk-based server hardening baseline for an electronics retailer. This task defines requirements and verification plans for later lab work. It does not claim that a server has been configured, scanned, or made CIS-compliant.

## Proposed scope and assumptions
The client has not supplied an asset inventory or operating-system specification. For planning purposes only, this draft assumes:

- Ubuntu Server 24.04 LTS
- A Linux application host running Nginx and a retail application
- PostgreSQL used by the application
- Authorized administrators connect through SSH
- A third-party payment provider handles card data; the server should not store PAN/CVV
- Separate production, staging, and development environments

**These assumptions must be confirmed before implementation.** If the actual OS/version differs, select the matching CIS Benchmark and revise the checklist.

## CIS reference
Use the official **CIS Ubuntu Linux 24.04 LTS Benchmark v2.0.0** as the proposed baseline. Obtain the benchmark from the [official CIS Ubuntu Linux page](https://www.cisecurity.org/benchmark/ubuntu_linux). Check the exact recommendation text, IDs, applicability, and profile before implementation. This project checklist is a tailored working document, not a reproduction of the benchmark and not a compliance certification.

## Repository contents
- `docs/hardening-checklist.md` — asset-aware hardening requirements and tracking fields
- `docs/test-plan.md` — paper test plan for later authorized lab verification
- `docs/risk-register.md` — initial business risks and treatment priorities

## How to review this deliverable
1. Read the scope assumptions and confirm the actual server OS/version and business architecture with the client.
2. Download the applicable CIS Benchmark from the official CIS site.
3. Map each checklist item to the exact CIS recommendation ID and record exceptions.
4. Review the test plan before any lab activity.
5. In later tasks, implement only in an owned lab or a system with written authorization.
6. Record evidence, results, rollback steps, and deviations; never mark an item Verified without evidence.

## Task 1 validation
This is a documentation-only task. Validate it by checking:
- All checklist entries have an owner/priority/status and a verification method.
- Both a normal and failure path are described in the test plan.
- Retail-specific assets and business impact are represented.
- No live system was scanned or changed.
- Assumptions and unverified CIS mappings are clearly labelled.

## Safety and authorization
All future scans, attacks, configuration changes, and performance tests must be limited to an owned lab, a free legal practice platform, or a system covered by explicit written permission. Do not test VoltMart production systems without written authorization and an approved change window.

## Next tasks
1. SSH and firewall hardening in a lab
2. Service reduction and updates
3. Automated compliance checks
4. Before-and-after report
5. Handover

## Publication
Create a GitHub repository named `voltmart-server-hardening` and publish these files. Add the repository URL here after it is actually created; do not claim a live link before publication.
