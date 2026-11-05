# Acceptance Criteria
## CPS 5981 - Lab 3: Trace the Card

A requirement fails when the named test produces the failing observation shown below.

## REQ-001

**Named test:** WSTG-BUSL-01 - Business Logic Data Validation

**Test condition:** user-controlled search terms or order details that do not satisfy the predefined format, type, range, length, or structure rules, the input

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the application continues business processing**.

**Failing observation:** the application accepts, processes, or stores input that violates the predefined validation rules.

---

## REQ-002

**Named test:** WSTG-INJT-01 - Reflected Cross Site Scripting

**Test condition:** user-controlled data that is returned in an HTTP, HTML, or XML response, the response content

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the browser renders the response**.

**Failing observation:** attacker-controlled data changes the message or document structure because the required context-specific encoding is absent or incorrect.

---

## REQ-003

**Named test:** WSTG-CLNT-01 - Testing for DOM-Based Cross Site Scripting

**Test condition:** attacker-controlled content that is intended to be displayed as text, the content

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the browser can interpret it as HTML or JavaScript**.

**Failing observation:** attacker-controlled content reaches a DOM sink and is interpreted or executed as HTML or JavaScript instead of inert text.

---

## REQ-004

**Named test:** WSTG-ATHN-02 - Default Credentials

**Test condition:** the deployed application's authentication account set, the authentication identity set

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the application is released for use**.

**Failing observation:** a default account remains enabled and successfully authenticates.

---

## REQ-005

**Named test:** WSTG-ATHN-04 - Bypassing Authentication Schema

**Test condition:** an unauthenticated request for functionality or data that requires authentication, the protected resource request

**Acceptance criterion:** The test passes only if the required behavior is observed within **before protected data is returned or protected state is changed**.

**Failing observation:** an unauthenticated request receives successful access to protected functionality or data.

---

## REQ-006

**Named test:** WSTG-ATHN-03 - Weak Lock Out Mechanism

**Test condition:** repeated invalid authentication attempts against an account or authentication endpoint, the authentication attempt stream

**Acceptance criterion:** The test passes only if the required behavior is observed within **within the application's documented credential-attack threshold**.

**Failing observation:** repeated invalid attempts continue beyond the documented threshold without effective throttling, lockout, adaptive response, or equivalent restriction.

---

## REQ-007

**Named test:** WSTG-ATHN-09 - Weak Password Change or Reset Functionalities

**Test condition:** a system-generated initial password or activation code, the temporary credential

**Acceptance criterion:** The test passes only if the required behavior is observed within **at the earlier of its initial permitted use or its documented short expiration time**.

**Failing observation:** the temporary password or activation code remains usable after initial use or after its defined expiration.

---

## REQ-008

**Named test:** WSTG-ATHN-11 - Multi-Factor Authentication

**Test condition:** a user attempting to establish an authenticated session for protected application access, the authentication session

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the authenticated session is issued**.

**Failing observation:** the application establishes the protected authenticated session using only a single password factor when the required authentication level calls for stronger authentication.

---

## REQ-009

**Named test:** WSTG-ATHN-04 - Bypassing Authentication Schema

**Test condition:** any documented or alternate authentication pathway that can reach protected application functionality, the authentication request

**Acceptance criterion:** The test passes only if the required behavior is observed within **before protected access is granted**.

**Failing observation:** a protected pathway grants access without authentication controls equivalent to the approved pathway.

---

## REQ-010

**Named test:** WSTG-ATHZ-04 - Insecure Direct Object References

**Test condition:** an authenticated customer request that references a specific order or other protected data item, the requested data item

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the item is returned or modified**.

**Failing observation:** changing an identifier lets the customer read or modify another customer's data.

---

## REQ-011

**Named test:** WSTG-ATHZ-03 - Privilege Escalation

**Test condition:** an authenticated user requesting a protected application function, the function invocation

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the protected function executes**.

**Failing observation:** a staff account successfully invokes a function requiring a permission or role the account does not possess.

---

## REQ-012

**Named test:** WSTG-BUSL-06 - Circumvention of Work Flows

**Test condition:** a multi-step business workflow for the same authenticated user, the workflow request

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the requested later workflow step is accepted**.

**Failing observation:** a later workflow step succeeds after the tester skips or reorders a required prerequisite step.

---

## REQ-013

**Named test:** WSTG-CRYP-01 - Weak Transport Layer Security

**Test condition:** client connectivity to an externally facing HTTP-based application service, the application traffic

**Acceptance criterion:** The test passes only if the required behavior is observed within **before application data is exchanged**.

**Failing observation:** the application accepts or completes application-data communication over an insecure or unencrypted channel.

---

## REQ-014

**Named test:** SECRET-SCAN-REQ014 - Source and Build Artifact Secret Scan

**Test condition:** application source code or a generated build artifact, the backend secret material

**Acceptance criterion:** The test passes only if the required behavior is observed within **for every release candidate before distribution**.

**Failing observation:** a usable credential, API key, database password, token, private key, or other backend secret is detected in source code or a generated build artifact.

---

## REQ-015

**Named test:** WSTG-CRYP-04 - Weak Cryptographic Primitives

**Test condition:** a user password that will be persisted by the authentication system, the password representation

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the password representation is first stored**.

**Failing observation:** stored password data is plaintext or uses a weak/general-purpose hash or inadequate password-hashing parameters.

---

## REQ-016

**Named test:** WSTG-BUSL-07 - Defenses Against Application Misuse

**Test condition:** automated requests to a public search, product, or account-related function that exceed its documented permitted rate, the request stream

**Acceptance criterion:** The test passes only if the required behavior is observed within **on the first request that exceeds the documented rate limit**.

**Failing observation:** requests above the documented limit continue normal processing without throttling, rejection, delay, blocking, or the defined anti-automation response.

---

## REQ-017

**Named test:** WSTG-ATHZ-02 - Bypassing Authorization Schema

**Test condition:** an authenticated request whose client-side authorization restriction has been altered or bypassed, the protected operation

**Acceptance criterion:** The test passes only if the required behavior is observed within **before any protected state change or protected response is completed**.

**Failing observation:** the modified request successfully performs an operation that the server-side authorization rules should reject.

---

## REQ-018

**Named test:** WSTG-SESS-06 - Logout Functionality, adapted to account disable/delete

**Test condition:** a staff account that has been disabled or deleted, the account's previously issued active session tokens

**Acceptance criterion:** The test passes only if the required behavior is observed within **before the next authenticated request using any of those tokens is processed**.

**Failing observation:** a session token issued before disablement or deletion still reaches authenticated functionality afterward.
