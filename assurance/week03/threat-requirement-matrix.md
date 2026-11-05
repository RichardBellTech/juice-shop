# Threat-to-Requirement Matrix
## CPS 5981 - Lab 3: Trace the Card

This matrix provides the bidirectional disposition from each elicited threat or Lab 2 abuse case to a numbered requirement or waiver.

| Source threat / abuse case | Disposition | Verification |
|---|---|---|
| THREAT-01 | REQ-001 | WSTG-BUSL-01 - Business Logic Data Validation |
| THREAT-02 | REQ-002 | WSTG-INJT-01 - Reflected Cross Site Scripting |
| THREAT-03 | REQ-003 | WSTG-CLNT-01 - Testing for DOM-Based Cross Site Scripting |
| THREAT-04 | REQ-004 | WSTG-ATHN-02 - Default Credentials |
| Lab 2 Case 1 | REQ-005 | WSTG-ATHN-04 - Bypassing Authentication Schema |
| THREAT-05 | REQ-006 | WSTG-ATHN-03 - Weak Lock Out Mechanism |
| THREAT-06 | REQ-007 | WSTG-ATHN-09 - Weak Password Change or Reset Functionalities |
| THREAT-07 | REQ-008 | WSTG-ATHN-11 - Multi-Factor Authentication |
| THREAT-08 | REQ-009 | WSTG-ATHN-04 - Bypassing Authentication Schema |
| Lab 2 Case 2 | REQ-010 | WSTG-ATHZ-04 - Insecure Direct Object References |
| Lab 2 Case 3 | REQ-011 | WSTG-ATHZ-03 - Privilege Escalation |
| THREAT-09 | REQ-012 | WSTG-BUSL-06 - Circumvention of Work Flows |
| THREAT-10 | REQ-013 | WSTG-CRYP-01 - Weak Transport Layer Security |
| THREAT-11 | REQ-014 | SECRET-SCAN-REQ014 - Source and Build Artifact Secret Scan |
| THREAT-12 | REQ-015 | WSTG-CRYP-04 - Weak Cryptographic Primitives |
| Lab 2 Case 4 | REQ-016 | WSTG-BUSL-07 - Defenses Against Application Misuse |
| Lab 2 Case 5 | REQ-017 | WSTG-ATHZ-02 - Bypassing Authorization Schema |
| Lab 2 Case 6 | REQ-018 | WSTG-SESS-06 - Logout Functionality, adapted to account disable/delete |

## Lab 2 Abuse Case Coverage

| Lab 2 abuse case | Requirement / waiver disposition | Status |
|---|---|---|
| Case 1 - unauthenticated access to protected functions or data | REQ-005 | Requirement |
| Case 2 - customer accesses or changes another customer's order data | REQ-010 | Requirement |
| Case 3 - authorized staff exceeds assigned function permissions | REQ-011 | Requirement |
| Case 4 - automated high-rate requests consume application resources | REQ-016 | Requirement |
| Case 5 - compromised browser alters requests or submits unintended actions | REQ-017 covers trusted-layer authorization; WAIVER-01 covers the residual case where a fully compromised browser submits an otherwise-authorized action through a valid session | Requirement + bounded waiver |
| Case 6 - former staff access remains usable after authorization ends | REQ-018 | Requirement |

## WAIVER-01 - Residual Compromised-Browser Risk

**Threat:** Lab 2 Case 5 - a compromised customer browser or malicious browser extension uses the customer's active authenticated session to alter requests or submit actions the customer did not intend.

**Why not today:** The application can enforce authorization at a trusted service layer, but it cannot reliably distinguish the legitimate customer's intent from an attacker operating inside a fully compromised browser when both use the same valid authenticated session for an operation the account is authorized to perform. Eliminating this residual risk would require additional transaction-intent controls such as step-up authentication or independent confirmation for selected sensitive actions, adding implementation scope and user friction.

**Approver:** Professor Dr. Ora Kenneth Melie. Approval/signature status: must be obtained or confirmed before this waiver is represented as signed.

**Duration:** 30 calendar days from October 27, 2026, through November 26, 2026.

**Compensating control:** REQ-017 enforces authorization at the trusted service layer rather than relying on manipulable client-side controls. REQ-003 also reduces application-delivered browser compromise risk through safe rendering of text content.

**Expiry condition:** The waiver expires at the earliest of November 26, 2026; introduction of a sensitive transaction requiring stronger proof of user intent; evidence that a compromised browser or extension used a valid session to perform unintended actions; or implementation of step-up authentication/independent transaction confirmation.

**Written by / date:** CPS 5981 Lab 3 team documentarian - October 27, 2026.

**Traceability:** Lab 2 Case 5 -> REQ-017 -> WAIVER-01.
