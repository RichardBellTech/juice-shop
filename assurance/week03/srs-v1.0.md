# Security Requirements Specification v1.0
## CPS 5981 - Lab 3: Trace the Card

Each requirement follows the laboratory's six-field requirement shape and includes the selected ASVS level and design tradeoff.

## REQ-001

REQ-001 - Given user-controlled search terms or order details that do not satisfy the predefined format, type, range, length, or structure rules, the input  
crossing **Customer/User's Browser -> Web Application/Application Server** shall **be rejected**  
within **before the application continues business processing**,  
verified by **WSTG-BUSL-01 - Business Logic Data Validation** asserting **the application accepts, processes, or stores input that violates the predefined validation rules**.

**Out of scope:** Client-side-only validation and authorization decisions are not covered by this requirement.  
**Traces to:** THREAT-01

**ASVS:** v5.0.0-2.2.1  
**Chosen level:** L2  
**Tradeoff:** Broader validation coverage and more test cases are required than at the minimum L1 scope.

---

## REQ-002

REQ-002 - Given user-controlled data that is returned in an HTTP, HTML, or XML response, the response content  
crossing **Web Application/Application Server -> User's Browser** shall **use context-appropriate output encoding**  
within **before the browser renders the response**,  
verified by **WSTG-INJT-01 - Reflected Cross Site Scripting** asserting **attacker-controlled data changes the message or document structure because the required context-specific encoding is absent or incorrect**.

**Out of scope:** DOM safe-rendering behavior after the response reaches client-side code is covered separately by REQ-003.  
**Traces to:** THREAT-02

**ASVS:** v5.0.0-1.2.1  
**Chosen level:** L1  
**Tradeoff:** The requirement addresses context-specific output encoding but does not claim the broader assurance coverage of the full L2 control set.

---

## REQ-003

REQ-003 - Given attacker-controlled content that is intended to be displayed as text, the content  
crossing **Web Application/Application Server -> User's Browser DOM** shall **be handled as inert text by a safe rendering function**  
within **before the browser can interpret it as HTML or JavaScript**,  
verified by **WSTG-CLNT-01 - Testing for DOM-Based Cross Site Scripting** asserting **attacker-controlled content reaches a DOM sink and is interpreted or executed as HTML or JavaScript instead of inert text**.

**Out of scope:** Server-side context-specific response encoding is covered separately by REQ-002.  
**Traces to:** THREAT-03

**ASVS:** v5.0.0-3.2.2  
**Chosen level:** L1  
**Tradeoff:** The requirement addresses this specific unsafe client-side rendering threat but does not claim the broader L2 control set.

---

## REQ-004

REQ-004 - Given the deployed application's authentication account set, the authentication identity set  
crossing **deployment configuration -> Login Service** shall **contain no enabled default user account**  
within **before the application is released for use**,  
verified by **WSTG-ATHN-02 - Default Credentials** asserting **a default account remains enabled and successfully authenticates**.

**Out of scope:** Formerly authorized or unnecessary non-default accounts are not covered; stale staff access is handled by REQ-018.  
**Traces to:** THREAT-04

**ASVS:** v5.0.0-6.3.2  
**Chosen level:** L1  
**Tradeoff:** The requirement removes default-account exposure but does not address the separate lifecycle problem of old or formerly authorized accounts.

---

## REQ-005

REQ-005 - Given an unauthenticated request for functionality or data that requires authentication, the protected resource request  
crossing **User's Browser -> Web Application/Application Server** shall **be denied**  
within **before protected data is returned or protected state is changed**,  
verified by **WSTG-ATHN-04 - Bypassing Authentication Schema** asserting **an unauthenticated request receives successful access to protected functionality or data**.

**Out of scope:** Authorization among already authenticated users is covered by REQ-010, REQ-011, and REQ-017.  
**Traces to:** Lab 2 Case 1

**ASVS:** v5.0.0-16.5.3  
**Chosen level:** L2  
**Tradeoff:** Fail-secure behavior must be tested across relevant authentication and error paths, increasing implementation and verification effort.

---

## REQ-006

REQ-006 - Given repeated invalid authentication attempts against an account or authentication endpoint, the authentication attempt stream  
crossing **User's Browser -> Login Service** shall **trigger the documented anti-brute-force control**  
within **within the application's documented credential-attack threshold**,  
verified by **WSTG-ATHN-03 - Weak Lock Out Mechanism** asserting **repeated invalid attempts continue beyond the documented threshold without effective throttling, lockout, adaptive response, or equivalent restriction**.

**Out of scope:** Offline password cracking against a stolen password database is covered separately by REQ-015.  
**Traces to:** THREAT-05

**ASVS:** v5.0.0-6.3.1  
**Chosen level:** L1  
**Tradeoff:** The application must restrict repeated credential attacks, but the control may use throttling, rate limiting, adaptive controls, or another documented mechanism rather than a single prescribed lockout design.

---

## REQ-007

REQ-007 - Given a system-generated initial password or activation code, the temporary credential  
crossing **credential issuance -> Login Service** shall **be rejected after its permitted lifetime ends**  
within **at the earlier of its initial permitted use or its documented short expiration time**,  
verified by **WSTG-ATHN-09 - Weak Password Change or Reset Functionalities** asserting **the temporary password or activation code remains usable after initial use or after its defined expiration**.

**Out of scope:** Long-term password rotation, MFA recovery codes, and unrelated out-of-band codes are not covered.  
**Traces to:** THREAT-06

**ASVS:** v5.0.0-6.4.1  
**Chosen level:** L1  
**Tradeoff:** Short-lived initial credentials add lifecycle controls but do not cover every recovery-code or MFA-code scenario in the broader card.

---

## REQ-008

REQ-008 - Given a user attempting to establish an authenticated session for protected application access, the authentication session  
crossing **User's Browser -> Login Service** shall **require multi-factor or an approved equivalent stronger authentication combination**  
within **before the authenticated session is issued**,  
verified by **WSTG-ATHN-11 - Multi-Factor Authentication** asserting **the application establishes the protected authenticated session using only a single password factor when the required authentication level calls for stronger authentication**.

**Out of scope:** The L3 requirement for a hardware-backed, phishing-resistant factor is not claimed.  
**Traces to:** THREAT-07

**ASVS:** v5.0.0-6.3.3  
**Chosen level:** L2  
**Tradeoff:** Stronger authentication increases assurance but adds user friction, enrollment and recovery complexity, and implementation/testing effort.

---

## REQ-009

REQ-009 - Given any documented or alternate authentication pathway that can reach protected application functionality, the authentication request  
crossing **User's Browser -> Login Service/Web Application** shall **apply the same approved authentication policy**  
within **before protected access is granted**,  
verified by **WSTG-ATHN-04 - Bypassing Authentication Schema** asserting **a protected pathway grants access without authentication controls equivalent to the approved pathway**.

**Out of scope:** Authorization decisions made after successful authentication are not covered.  
**Traces to:** THREAT-08

**ASVS:** v5.0.0-6.3.4  
**Chosen level:** L2  
**Tradeoff:** All authentication pathways must be identified, documented, and tested consistently, increasing verification effort.

---

## REQ-010

REQ-010 - Given an authenticated customer request that references a specific order or other protected data item, the requested data item  
crossing **User's Browser -> Web Application/Application Server -> Product Database** shall **be accessible only when the requesting customer has explicit permission to that item**  
within **before the item is returned or modified**,  
verified by **WSTG-ATHZ-04 - Insecure Direct Object References** asserting **changing an identifier lets the customer read or modify another customer's data**.

**Out of scope:** Function-level staff permissions are covered separately by REQ-011.  
**Traces to:** Lab 2 Case 2

**ASVS:** v5.0.0-8.2.2  
**Chosen level:** L1  
**Tradeoff:** Object-level authorization checks are required for each protected record reference, increasing authorization logic and test coverage.

---

## REQ-011

REQ-011 - Given an authenticated user requesting a protected application function, the function invocation  
crossing **User's Browser -> Web Application/Application Server** shall **be permitted only when the account has explicit permission for that function**  
within **before the protected function executes**,  
verified by **WSTG-ATHZ-03 - Privilege Escalation** asserting **a staff account successfully invokes a function requiring a permission or role the account does not possess**.

**Out of scope:** Object-level ownership of specific customer or order records is covered separately by REQ-010.  
**Traces to:** Lab 2 Case 3

**ASVS:** v5.0.0-8.2.1  
**Chosen level:** L1  
**Tradeoff:** Function-level authorization checks and multi-role testing increase implementation and verification effort.

---

## REQ-012

REQ-012 - Given a multi-step business workflow for the same authenticated user, the workflow request  
crossing **User's Browser -> Web Application/Application Server** shall **be processed only when all required prior steps have been completed in the expected sequence**  
within **before the requested later workflow step is accepted**,  
verified by **WSTG-BUSL-06 - Circumvention of Work Flows** asserting **a later workflow step succeeds after the tester skips or reorders a required prerequisite step**.

**Out of scope:** Client compromise and user-intent verification are not covered by this workflow-sequencing requirement.  
**Traces to:** THREAT-09

**ASVS:** v5.0.0-2.3.1  
**Chosen level:** L1  
**Tradeoff:** Server-side workflow-state tracking and additional sequence tests are required.

---

## REQ-013

REQ-013 - Given client connectivity to an externally facing HTTP-based application service, the application traffic  
crossing **User's Browser -> Web Application/Application Server** shall **use TLS without fallback to an insecure or unencrypted channel**  
within **before application data is exchanged**,  
verified by **WSTG-CRYP-01 - Weak Transport Layer Security** asserting **the application accepts or completes application-data communication over an insecure or unencrypted channel**.

**Out of scope:** Encryption of stored data and password hashing are covered separately.  
**Traces to:** THREAT-10

**ASVS:** v5.0.0-12.2.1  
**Chosen level:** L1  
**Tradeoff:** TLS must be consistently enforced across externally reachable HTTP services, increasing configuration and testing effort.

---

## REQ-014

REQ-014 - Given application source code or a generated build artifact, the backend secret material  
crossing **secrets-management boundary -> source/build artifact** shall **remain absent from every included source or build artifact**  
within **for every release candidate before distribution**,  
verified by **SECRET-SCAN-REQ014 - Source and Build Artifact Secret Scan** asserting **a usable credential, API key, database password, token, private key, or other backend secret is detected in source code or a generated build artifact**.

**Out of scope:** End-user passwords are covered by REQ-015; this requirement is limited to backend application secrets.  
**Traces to:** THREAT-11

**ASVS:** v5.0.0-13.3.1  
**Chosen level:** L2  
**Tradeoff:** Backend secrets must be externalized to dedicated secrets management, adding deployment, access-control, and operational complexity.

---

## REQ-015

REQ-015 - Given a user password that will be persisted by the authentication system, the password representation  
crossing **Login Service -> credential storage** shall **use an approved computationally intensive password-hashing function with parameters configured to current guidance**  
within **before the password representation is first stored**,  
verified by **WSTG-CRYP-04 - Weak Cryptographic Primitives** asserting **stored password data is plaintext or uses a weak/general-purpose hash or inadequate password-hashing parameters**.

**Out of scope:** Encryption of unrelated stored PII, session identifiers, or cardholder data is not covered by this narrowed requirement.  
**Traces to:** THREAT-12

**ASVS:** v5.0.0-11.4.2  
**Chosen level:** L2  
**Tradeoff:** Computationally intensive password hashing increases authentication CPU cost while intentionally increasing offline cracking cost.

---

## REQ-016

REQ-016 - Given automated requests to a public search, product, or account-related function that exceed its documented permitted rate, the request stream  
crossing **Automated Client -> Web Application/Application Server** shall **enter the documented anti-automation response**  
within **on the first request that exceeds the documented rate limit**,  
verified by **WSTG-BUSL-07 - Defenses Against Application Misuse** asserting **requests above the documented limit continue normal processing without throttling, rejection, delay, blocking, or the defined anti-automation response**.

**Out of scope:** Network-layer volumetric DDoS protection outside the application is not covered.  
**Traces to:** Lab 2 Case 4

**ASVS:** v5.0.0-2.4.1  
**Chosen level:** L2  
**Tradeoff:** Rate limits can affect legitimate high-volume users or approved automation, so function-specific limits must balance availability and usability.

---

## REQ-017

REQ-017 - Given an authenticated request whose client-side authorization restriction has been altered or bypassed, the protected operation  
crossing **User's Browser -> Web Application/Application Server** shall **be authorized independently at the trusted service layer**  
within **before any protected state change or protected response is completed**,  
verified by **WSTG-ATHZ-02 - Bypassing Authorization Schema** asserting **the modified request successfully performs an operation that the server-side authorization rules should reject**.

**Out of scope:** The application cannot reliably prove human intent when a fully compromised browser submits an otherwise-authorized operation through a valid session; that residual risk is recorded in WAIVER-01.  
**Traces to:** Lab 2 Case 5

**ASVS:** v5.0.0-8.3.1  
**Chosen level:** L1  
**Tradeoff:** Server-side authorization checks add enforcement and testing effort but prevent client-side controls from becoming the authorization decision.

---

## REQ-018

Given a staff account that has been disabled or deleted, the account's previously issued active session tokens  
crossing **Login Service -> Web Application/Application Server** shall **be invalidated**  
within **before the next authenticated request using any of those tokens is processed**,  
verified by **WSTG-SESS-06 -> Logout Functionality, adapted to account disable/delete** asserting **a session token issued before disablement or deletion still reaches authenticated functionality afterward**.

**Out of scope:** Determining when employment or authorization ends and triggering the account-disable/delete event is an organizational identity-management control, not an application responsibility.  
**Traces to:** Lab 2 Case 6

**ASVS:** v5.0.0-7.4.2  
**Chosen level:** L1  
**Tradeoff:** Immediate termination can interrupt legitimate work if an account is disabled incorrectly, but surviving sessions would preserve access after authorization ends.
