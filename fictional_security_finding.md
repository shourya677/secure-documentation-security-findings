# Fictional Security Finding: Cross-Account Profile Access Due to Missing Object-Level Authorization

> **Synthetic example only.** `app.example.test`, account names, IDs, requests, responses, and timestamps below are fabricated for training. No real system was tested. The domain uses the reserved `.test` namespace.

## 1. Finding metadata
- **Finding ID:** RKRF-SD-2026-001
- **Status:** Open (fictional example)
- **Author / team:** Security Documentation Intern
- **Date discovered:** 2026-10-17
- **Affected environment:** Fictional local training lab
- **Scope:** `https://app.example.test/api/profile/{profile_id}`. Only two synthetic test accounts are in scope. No production system, third-party service, or real user data is in scope.

## 2. Executive summary
The fictional profile API returns profile information based on a client-supplied profile identifier without consistently checking that the authenticated user is authorised to access that profile. A user signed in as Account A can request Account B's synthetic profile ID and receive fields belonging to Account B. This is an object-level authorisation failure (commonly described as IDOR/BOLA). The finding is not based on a real assessment.

## 3. Technical description and root cause
- **Category:** Broken access control; CWE-639 (Authorization Bypass Through User-Controlled Key), potentially relevant to the described pattern.
- **OWASP mapping:** OWASP Top 10:2025 A01 Broken Access Control.
- **Root cause hypothesis:** The endpoint appears to rely on the supplied identifier to select a record but does not enforce an ownership/permission check for every request. This is a fictional explanation consistent with the observed synthetic response, not a source-code-confirmed root cause.
- **Preconditions:** An authenticated account and knowledge/guessability of another profile identifier.

## 4. Reproduction procedure (synthetic)
1. In the fictional lab, sign in as `user_alpha` and obtain the synthetic profile ID `1001`.
2. Send a read-only request to `GET https://app.example.test/api/profile/1001` using Account A's session.
3. Observe the synthetic response for Account A.
4. Without changing the session, request `GET https://app.example.test/api/profile/2002`, the synthetic ID assigned to `user_beta`.
5. Compare the returned owner marker with the authenticated account. In the vulnerable fictional scenario, the API returns the `user_beta` profile.
6. Stop after confirming the synthetic response. Do not enumerate IDs or access any real account.

**Expected secure behaviour:** Account A receives `403 Forbidden` or a privacy-preserving `404 Not Found` for Account B's profile.  
**Fictional observed behaviour:** HTTP `200 OK` with the synthetic Account B profile.  
**Reproducibility:** Deterministic in the fictional scenario.  
**Safety:** Read-only requests against invented data; no destructive action.

## 5. Evidence (all synthetic)
**E-01 — Request as Account A**
```http
GET /api/profile/1001 HTTP/1.1
Host: app.example.test
Authorization: Bearer <SYNTHETIC_TOKEN_A>
Accept: application/json
```
Synthetic response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{"profile_id":1001,"owner":"user_alpha","display_name":"Alpha Demo"}
```

**E-02 — Cross-account request using the same synthetic session**
```http
GET /api/profile/2002 HTTP/1.1
Host: app.example.test
Authorization: Bearer <SYNTHETIC_TOKEN_A>
Accept: application/json
```
Synthetic response:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{"profile_id":2002,"owner":"user_beta","display_name":"Beta Demo"}
```

- **Evidence timestamp:** Illustrative only: `2026-10-17T10:00:00Z` (not a real capture).
- **Capture method:** Hand-authored example for documentation; no tool was used to test a live application.
- **Integrity / redactions:** All values are invented. Token placeholders are non-functional. No screenshots or raw captures from a real target exist.

## 6. Impact
- **Confidentiality:** Moderate in this example. Profile information belonging to another account can be read.
- **Integrity:** Not demonstrated; the example uses read-only requests.
- **Availability:** Not demonstrated.
- **Affected users / assets:** Potentially any profile accessible through the same vulnerable endpoint; actual reach is unknown and would require authorised validation.
- **Business consequence:** Unauthorised disclosure of account profile details, erosion of user trust, and possible privacy/compliance exposure depending on the real data and jurisdiction. No real exposure is claimed.

## 7. Severity and rationale
- **Severity:** Medium (qualitative, illustrative).
- **Scoring method:** Qualitative assessment, not a calculated CVSS score.
- **Rationale:** Exploitation requires an authenticated session and a valid identifier, but the scenario permits reading another account's data without that account's permission. The demonstrated impact is limited to confidentiality; write access, sensitive fields, internet exposure, scale, and compensating controls have not been established.
- **Confidence:** High that the fictional request/response pair illustrates the weakness; no confidence claim is made about any real system.
- **Environmental modifiers:** Unknown outside the fictional lab. Severity must be reassessed using actual data sensitivity, reachability, and controls in an authorised assessment.

## 8. Remediation
1. Enforce server-side object-level authorisation on every profile read and write. Derive the caller identity from the validated session, then verify that the caller owns the object or has an explicit permission.
2. Prefer queries constrained by the authenticated principal, such as retrieving a profile only within the caller's authorised dataset; do not treat an opaque or hard-to-guess ID as an access control.
3. Apply the same check to nested resources, exports, search endpoints, and alternate API versions.
4. Add negative automated tests proving that Account A cannot read or modify Account B's records, including sequential and random identifiers.
5. Log denied cross-account access attempts with suitable privacy controls; avoid logging tokens or unnecessary personal data.
6. Review historical access logs where available and follow the organisation's incident process if real unauthorised access is suspected.

**Suggested owner:** Application/API team.  
**Suggested priority:** Fix before release if the endpoint exposes real user data; confirm urgency through the organisation's risk process.

## 9. References
1. OWASP, *OWASP Top 10:2025 — A01 Broken Access Control*: https://owasp.org/Top10/2025/A01_2025-Broken_Access_Control/
2. OWASP, *Web Security Testing Guide*: https://owasp.org/projects/web-security-testing-guide
3. FIRST, *Common Vulnerability Scoring System (CVSS) v4.0 Specification*: https://www.first.org/cvss/v4.0/specification-document
4. MITRE, *CWE-639: Authorization Bypass Through User-Controlled Key*: https://cwe.mitre.org/data/definitions/639.html

## 10. Verification and closure
**Status:** Not tested; remediation and retest are proposed only. This report must not be interpreted as proof of a fix.

Verification plan for an authorised lab:
1. Apply the server-side ownership/permission check.
2. As Account A, request Account A's own profile; expect `200 OK` with only Account A's data.
3. As Account A, request Account B's profile; expect `403 Forbidden` or privacy-preserving `404 Not Found`, with no Account B data in the body.
4. Repeat for update/delete operations and related endpoints using synthetic accounts.
5. Run regression tests for authorised access, unauthorised access, and role-based access.
6. Record build/version, test date, actual response, tester, and evidence hash. Close only after observed results support closure.

- **Retest result:** Not performed.
- **Residual risk:** Unknown until implementation and authorised verification.
- **Disposition:** Open in this fictional example.
