# Reclassification Record
## CPS 5981 - Lab 3: Trace the Card

This log records statements that changed classification during requirement elicitation because the original wording could not be tested as one bounded, atomic requirement.

---

## RC-01 - Broad stored-data protection statement

**Original statement**

"Stored business data, including passwords, session identifiers, PII, and cardholder data, shall be securely encrypted or securely hashed."

**Original classification**

Proposed requirement derived from Cryptography 8 - Eoin.

**Reclassified to**

Security goal, with a narrower testable requirement retained as REQ-015.

**Reason**

The original statement combines several different data classes and two different protection mechanisms: encryption and hashing. A single failing observation would not identify which asset or mechanism violated the statement, so the statement is not atomic and cannot be falsified by one bounded test.

REQ-015 therefore narrows the requirement to stored user passwords and requires an approved computationally intensive password-hashing function with appropriate parameters.

**Falsifiability basis**

REQ-015 can fail when stored password data is plaintext or uses a weak or inappropriate password-hashing configuration.

---

## RC-02 - "Prevent unintended actions from a compromised browser"

**Original statement**

"The application shall prevent a compromised customer browser or malicious browser extension from submitting actions the customer did not intend."

**Original classification**

Proposed requirement for Lab 2 Case 5.

**Reclassified to**

Part requirement, part accepted residual risk.

**Resulting requirement/control**

REQ-017 requires authorization to be enforced at a trusted service layer rather than relying on client-side controls that an untrusted browser can manipulate.

**Residual disposition**

WAIVER-01 records the remaining risk that a fully compromised browser can use a valid authenticated session to submit an operation that the account is otherwise authorized to perform.

**Reason**

The original statement has no reliable application-side observation that proves the human user's intent when the browser itself is fully compromised. The server can test authorization, but it cannot always distinguish the legitimate user from malicious code operating inside the same valid session.

Keeping the full statement as a requirement would therefore overstate what the application can prove.

**Falsifiability basis**

REQ-017 can fail when a modified request bypasses a client-side restriction and the server performs an operation that its server-side authorization rule should reject. The remaining "human intent" problem is bounded and documented in WAIVER-01 instead of being presented as an untestable requirement.

---

## RC-03 - Former-staff offboarding

**Original statement**

"The application shall remove a former staff member's access when employment or authorization ends."

**Original classification**

Proposed requirement for Lab 2 Case 6.

**Reclassified to**

Organizational/offboarding control plus a narrower application requirement.

**Resulting requirement**

REQ-018 requires the application to terminate all active sessions after the staff account is disabled or deleted.

**Control outside application scope**

The organization or identity-management process must determine that employment or authorization has ended and trigger the account-disable or account-delete event.

**Reason**

The application cannot independently observe when employment ends unless that event is supplied by an external identity or administrative process. The original wording therefore places an unobservable organizational trigger inside an application requirement.

The application-side behavior becomes falsifiable only after the trigger is bounded to "account disabled or deleted."

**Falsifiability basis**

REQ-018 can fail when a session token issued before account disablement or deletion still reaches authenticated functionality afterward.

---

## Reclassification Summary

| ID | Original classification | Final classification | Result |
|---|---|---|---|
| RC-01 | Requirement | Goal + narrower requirement | REQ-015 |
| RC-02 | Requirement | Requirement + waiver | REQ-017 + WAIVER-01 |
| RC-03 | Requirement | Organizational control + narrower requirement | REQ-018 |

These changes were made because the original statements were not atomic, bounded, or directly falsifiable as written-not for convenience or to reduce the amount of work.
