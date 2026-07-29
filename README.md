# Web Security Write-ups

Practical write-ups documenting my web application security studies, lab methodology, payload analysis, and remediation notes.

## Topics

- Authentication and authorization
- Injection vulnerabilities
- Cross-site scripting (XSS)
- Session management
- Server-side vulnerabilities
- OWASP Web Security Testing Guide (WSTG)

## Write-ups

| Write-up | Vulnerability | Environment |
| --- | --- | --- |
| Coming soon | — | — |

## Repository structure

Each write-up has its own folder, with the Markdown file and its images kept together:

```text
writeups/
└── dvwa-command-injection/
    ├── README.md
    └── images/
        ├── low-security.png
        └── medium-security.png
```

Inside the write-up, an image can be displayed with a relative path:

```markdown
![Command injection result](images/low-security.png)
```

## Disclaimer

All testing documented here was performed in local labs or environments where explicit authorization was granted. This repository is intended for educational purposes only.
