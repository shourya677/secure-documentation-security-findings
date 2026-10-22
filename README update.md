# Task-Secure Documentation

A reusable security-finding documentation template and a fully worked fictional example, prepared for the RedKross Research Foundation internship task.

## Objective
Help another reviewer reproduce and understand a finding, assess its impact and severity, apply remediation, and verify the result. **All example evidence is synthetic; no live system was tested.**

## Repository contents
```text
.
├── README.md
├── docs/
│   ├── security_finding_template.md
│   ├── security_finding_template.pdf
│   ├── fictional_security_finding.md
│   └── fictional_security_finding.pdf
└── reports/
    ├── technical_report.md
    └── technical_report.pdf
```

## How to use
1. Copy `docs/security_finding_template.md` for each new authorised finding.
2. Replace bracketed prompts with verified facts from the approved assessment.
3. Record the exact scope, reproducible steps, expected versus observed behaviour, and evidence provenance.
4. Redact credentials, tokens, personal data, and unrelated sensitive information.
5. Select severity using a documented rubric or include the full CVSS version, vector, score, and assumptions if a score is calculated.
6. Provide specific remediation and a repeatable verification plan.
7. Do not mark a finding fixed until the retest has actually been performed and recorded.

## Safety and evidence handling
- Test only in your own lab or an explicitly authorised environment.
- Do not upload secrets, API keys, confidential information, or real personal data.
- The fictional hostname uses the reserved `.test` namespace.
- The sample request/response evidence is hand-authored and must not be represented as a real capture.
- The sample retest is proposed, not performed.

## References
- OWASP Top 10:2025: https://owasp.org/Top10/
- OWASP Web Security Testing Guide: https://owasp.org/projects/web-security-testing-guide
- FIRST CVSS v4.0: https://www.first.org/cvss/v4.0/specification-document
- MITRE CWE-639: https://cwe.mitre.org/data/definitions/639.html

## Explanatory video
**Video URL:** `(https://drive.google.com/file/d/153fls9gpv3pzrCXB2vjiDT_86RqJXT92/view?usp=sharing)`

## Submission details
- **Intern name:** Shourya
- **Intern ID:** 2430
- **Repository URL:** `[Fill in after confirming repository URL]`
- **Final submission deadline:** 25 October 2026

## Author's final checks
- [ ] Replace author and intern placeholders.
- [ ] Upload the video and insert its actual URL above.
- [ ] Confirm the repository is accessible to the research team.
- [ ] Check all files and links before submitting.
