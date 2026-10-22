# Reusable Security Finding Template

> **Handling:** Use only with authorised testing. Redact secrets and personal data. Attach synthetic or approved evidence only.

## 1. Finding metadata
- **Finding ID:** `[ORG-YYYY-NNN]`
- **Title:** `[Concise weakness + affected component]`
- **Status:** `Open / In progress / Fixed / Accepted risk / Closed`
- **Author / team:** `[Name or team]`
- **Date discovered:** `[YYYY-MM-DD]`
- **Last updated:** `[YYYY-MM-DD]`
- **Affected environment:** `[Lab / staging / production—only if authorised]`
- **Scope:** `[Host, application, version, endpoint, component, and explicit exclusions]`

## 2. Executive summary
`[One short paragraph describing the weakness, where it exists, and why it matters.]`

## 3. Technical description and root cause
- **Weakness category / mapping:** `[e.g., CWE and relevant OWASP category, if applicable]`
- **Root cause:** `[Explain the control or design gap without speculation.]`
- **Preconditions:** `[Account role, state, configuration, network position, etc.]`

## 4. Reproduction procedure
1. `[Starting state and required test account]`
2. `[Exact, minimal steps; use placeholders for tokens and identifiers]`
3. `[Expected secure behaviour]`
4. `[Observed behaviour]`

- **Reproducibility:** `[Always / intermittent / not reproduced]`
- **Test safety:** `[Why steps are non-destructive; cleanup performed]`

## 5. Evidence
For each item record:
- **Evidence ID and type:** `[E-01; screenshot, request/response, log, test output]`
- **Timestamp and timezone:** `[ISO 8601]`
- **Capture method / tool and version:** `[Tool and version]`
- **Observation:** `[What the evidence directly shows]`
- **Integrity / location:** `[Hash or controlled path, if appropriate]`
- **Redactions:** `[What was removed and why]`

**Evidence rule:** distinguish observed facts from assumptions. Never include live credentials, real personal data, or unapproved data.

## 6. Impact
- **Confidentiality:** `[None / Low / Moderate / High + reason]`
- **Integrity:** `[None / Low / Moderate / High + reason]`
- **Availability:** `[None / Low / Moderate / High + reason]`
- **Affected users / assets:** `[Bounded estimate; state uncertainty]`
- **Business consequence:** `[Plausible outcome tied to evidence]`

## 7. Severity and rationale
- **Severity:** `[Informational / Low / Medium / High / Critical]`
- **Scoring method:** `[CVSS version/vector if calculated, or documented qualitative rubric]`
- **Rationale:** `[Exploitability, prerequisites, impact, scope, and uncertainty]`
- **Confidence:** `[High / Medium / Low + explanation]`
- **Environmental modifiers:** `[Exposure, compensating controls, data sensitivity]`

Do not invent a CVSS score. If using CVSS, include the version, full vector, score, and assumptions.

## 8. Remediation
- **Recommended fix:** `[Specific code/configuration/control change]`
- **Implementation notes:** `[Ownership, compatibility, rollout considerations]`
- **Defence in depth:** `[Monitoring, rate limits, logging, additional controls]`
- **Priority / target date:** `[Owner-agreed priority and date]`

## 9. References
- `[Official standard, CWE, OWASP guidance, vendor advisory, or internal requirement]`
- `[Include title, version/date where relevant, and stable URL]`

## 10. Verification and closure
- **Retest date / tester:** `[YYYY-MM-DD / role]`
- **Build / version tested:** `[Identifier]`
- **Retest steps:** `[Repeat the original reproduction and relevant regression checks]`
- **Expected result:** `[Secure behaviour]`
- **Observed result:** `[Actual result; do not claim unperformed tests]`
- **Regression tests:** `[Tests added or run]`
- **Residual risk / limitations:** `[Any remaining concern]`
- **Disposition:** `[Closed / Reopened / Accepted risk / Needs more testing]`
- **Reviewer / approval:** `[Role or name, according to process]`

## 11. Change log
| Version | Date | Author/team | Change |
|---|---|---|---|
| 0.1 | `[YYYY-MM-DD]` | `[Name/team]` | Initial draft |
