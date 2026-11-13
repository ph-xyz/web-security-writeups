# Bug Bounty & VDP Findings

A curated collection of **real-world web application security findings** from authorized Bug Bounty and Vulnerability Disclosure Program (VDP) testing.

This collection is intentionally separate from [hands-on lab write-ups](../README.md): a lab demonstrates a technique in a controlled application; a finding documents a security boundary observed in a real program.

> **Disclosure first.** A case study is published only when the program's disclosure rules permit it and the material has been sanitized. A private or unresolved report is not evidence of a public, verified finding.

## Published findings

_No case studies are published in this section yet._

Entries will be added here only after checking the applicable program policy, disclosure permission, and redaction.

When available, each entry will be indexed by:

| Finding | Category | Program | Outcome | Disclosure |
| --- | --- | --- | --- | --- |
| _Future public case study_ | — | — | — | — |

The placeholder above is **not** an actual finding, report, or award.

## How a case study is organized

Each published finding gets its own self-contained directory:

~~~text
bug-bounty-vdp/
├── README.md                     # Public index (this page)
├── FINDING_TEMPLATE.md           # Reusable report structure
├── PUBLICATION_CHECKLIST.md      # Disclosure and sanitization gate
└── findings/
    ├── README.md                 # Directory conventions
    └── YYYY/
        └── short-finding-slug/
            ├── README.md         # Published, sanitized write-up
            └── evidence/         # Sanitized screenshots, if approved
~~~

The public write-up should explain **the trust boundary, expected behavior, observed behavior, testing method, impact, and remediation**. A baseline-versus-treatment comparison is preferred wherever possible. Root-cause explanations are labeled as hypotheses unless backed by code or program confirmation.

## Publication policy

- Test only within program scope and authorization.
- Follow the program's disclosure rules, waiting periods, and any NDA.
- Never publish credentials, session tokens, personal data, production customer records, internal URLs, private communications, or raw captures that contain them.
- Do not publish a still-exploitable issue when disclosure is not authorized.
- Report status, severity, and bounty outcomes only when confirmed and permitted to share.
- If a case cannot safely be published, **keep it outside this public repository**. Do not add it here as a hidden, redacted-by-name-only, or “pending” entry.

Use the [finding template](FINDING_TEMPLATE.md) and complete the [publication checklist](PUBLICATION_CHECKLIST.md) before adding a new case.

[Back to all write-ups](../README.md)
