# Publication checklist — real-world findings

This checklist is a **release gate** for content destined for a public GitHub repository. Do not commit a report here and plan to redact it later: Git history and caches can preserve the original data.

## 1. Permission and timing

- [ ] Testing was authorized and within the program's scope.
- [ ] The Bug Bounty / VDP policy explicitly allows public disclosure **or** explicit permission has been obtained.
- [ ] Any waiting period, coordinated-disclosure condition, NDA, or platform-specific rule has been satisfied.
- [ ] The write-up does not disclose an unresolved vulnerability without authorization.
- [ ] Any claim about validation, remediation, severity, or reward reflects an actual documented outcome.

## 2. Redaction and confidentiality

- [ ] No real user/customer information, emails, addresses, phone numbers, or unique identifiers remain.
- [ ] No passwords, API keys, cookies, bearer tokens, authorization headers, secrets, internal hostnames, or private program communications remain.
- [ ] URLs, requests, responses, filenames, screenshots, logs, and diagrams have all been checked.
- [ ] Screenshot annotations, metadata, and image backgrounds have been reviewed.
- [ ] Example IDs and hostnames are synthetic, or are disclosed only where permitted.
- [ ] No internal report ID or private report link is exposed unless disclosure is permitted.

## 3. Technical accuracy

- [ ] The write-up separates **expected behavior** from **observed behavior**.
- [ ] Baseline and treatment are described, including which variable changed.
- [ ] Impact is supported by evidence, not inferred from status codes alone.
- [ ] The suspected root cause is labeled a hypothesis unless independently verified.
- [ ] Limitations, negative results, and uncertainty are documented where relevant.
- [ ] Mitigations address the failed server-side trust boundary or business invariant.

## 4. Final review

- [ ] Every linked evidence file is sanitized and approved for publication.
- [ ] No restricted payloads or exploit paths need to remain in a public write-up.
- [ ] The findings index links to the correct case study.
- [ ] The public article has been reviewed **before** committing or opening a public PR.

**If any required permission or confidentiality check fails, do not publish.** Keep the original report and evidence in an appropriate private location outside this repository.

[Back to findings index](README.md)
