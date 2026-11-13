# Finding title — descriptive and sanitized

> **Template only — not a real finding.** Copy this file to \`findings/YYYY/short-finding-slug/README.md\` only after the [publication checklist](PUBLICATION_CHECKLIST.md) is satisfied. Remove all placeholders and sections that cannot be disclosed.

## At a glance

| Field | Value |
| --- | --- |
| Program / target | [Public name or “Undisclosed program,” only if permitted] |
| Type | [Bug Bounty / VDP] |
| Category | [e.g. BOLA / session management / business logic] |
| CWE / OWASP | [Only if applicable and validated] |
| Report date | [Date or omitted for confidentiality] |
| Outcome | [Confirmed program disposition, or omitted] |
| Disclosure basis | [Public policy / explicit permission / other permitted basis] |

## Summary

[What security property failed? State the affected workflow and why it matters. Avoid exposing private identifiers, hosts, or undisclosed details.]

## Application flow and trust boundary

1. **Actor:** [Role / permissions]
2. **Object or action:** [Resource / business operation]
3. **Expected authorization or validation:** [What the server should enforce]
4. **Observed behavior:** [What testing actually demonstrated]

[Use a high-level flow diagram if helpful.]

## Test methodology

### Environment and prerequisites

[Authorized testing context, controlled test accounts, relevant role boundaries. No credentials or real-user data.]

### Baseline — expected behavior

[Describe the original request and response from the authorized actor. Include sanitized excerpts only if safe to disclose.]

~~~http
GET /example/resource/<owned-id> HTTP/1.1
Host: example.invalid
Authorization: Bearer <REDACTED>

HTTP/1.1 200 OK
~~~

### Treatment — changed condition

[State exactly one changed variable: actor, object identifier, role, session, state, or transaction sequence.]

~~~http
GET /example/resource/<other-test-account-id> HTTP/1.1
Host: example.invalid
Authorization: Bearer <REDACTED>

HTTP/1.1 <OBSERVED-STATUS>
~~~

### Observation and verification

[What changed? How was the result verified? Separate direct evidence from interpretation; describe negative controls and any limitations.]

## Impact

[Demonstrated impact only. Clearly distinguish observed behavior from possible impact. Do not exaggerate scope, severity, or access.]

## Root cause / hypothesis

[Describe the suspected missing control or trust-boundary violation. Mark this as a **hypothesis** unless verified from code or by the program.]

## Remediation

[Specific server-side control, invariant, or authorization rule that prevents the observed behavior.]

## Evidence

[Links to approved, sanitized files in \`evidence/\`. Never include unredacted traffic, secrets, PII, private report screenshots, or sensitive metadata.]

## Outcome and disclosure

[Only include what the program permits you to share: accepted / informative / duplicate / other confirmed disposition, fix validation, or disclosure date. If not permitted, omit the section.]

## Lessons learned

[What changed in your testing methodology or understanding of the application?]

---

[Back to findings index](../../README.md)
