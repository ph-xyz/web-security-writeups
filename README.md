# Web Security Write-ups

Technical write-ups from my web application security practice: reproducible lab exercises, authorization testing, vulnerability analysis, and disclosure-safe case studies.

The material is organized into **controlled labs** and **real-world Bug Bounty / VDP findings**. They follow different evidence and disclosure standards.

## Explore

| Collection | Focus |
| --- | --- |
| [Bug Bounty & VDP Findings](bug-bounty-vdp/README.md) | Real-world research, published only when disclosure is permitted. Includes a [finding template](bug-bounty-vdp/FINDING_TEMPLATE.md) and [publication checklist](bug-bounty-vdp/PUBLICATION_CHECKLIST.md). |
| [DVWA](#dvwa) | Testing injection behavior and understanding failed mitigations across security levels. |
| [OWASP Juice Shop](#owasp-juice-shop) | Object-level authorization failures and their impact on application data integrity. |

> The Bug Bounty & VDP area is a newly established collection, **not a claim that real-world reports have been publicly disclosed**. No case studies are listed there yet.

## Controlled laboratory write-ups

All demonstrations below use intentionally vulnerable applications in controlled learning environments.

### DVWA

- [OS Command Injection — Low to Impossible](DVWA/command-injection/README.md)
- [SQL Injection — Low](DVWA/sql-injection/low/README.md)
- [SQL Injection — Medium](DVWA/sql-injection/medium/README.md)

### OWASP Juice Shop

- [Broken Object Level Authorization — Basket Items](OWASP-Juice-Shop/broken-object-level-authorization/README.md)

## How I approach testing

1. **Understand the workflow:** identify actors, resources, server-side state and intended trust boundaries.
2. **Establish a baseline:** capture expected behavior using controlled accounts or fixtures.
3. **Change one variable:** role, object ID, session state, parameter, or operation order.
4. **Verify the outcome:** compare server responses with actual changes in application state.
5. **Document precisely:** distinguish observed impact from possible impact or an unverified root-cause hypothesis.
6. **Recommend a fix:** explain the control or invariant that should be enforced.

## Related project

- [Web Security Labs](https://github.com/ph-xyz/web-security-labs) — small intentionally vulnerable local applications for practicing authorization, session handling, mass assignment and injection.
- [CaidoBridge](https://github.com/ph-xyz/Caido-Bridge) — a local MCP bridge connecting ChatGPT and Caido for traffic inspection and explicitly opt-in replay.

## Disclosure and ethics

Testing described in this repository is performed in controlled labs or authorized programs. Findings from real applications are shared only when the applicable program policy or explicit permission allows publication. Screenshots, request excerpts and other artifacts must be sanitized **before** being committed.

## References

- [DVWA](https://github.com/digininja/DVWA)
- [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/latest/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
