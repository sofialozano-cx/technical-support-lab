# TS-001 — API Authentication Failure (`401 Unauthorized`)

## Ticket Summary

**Scenario:** A fictional SaaS customer reports that an integration that worked previously has stopped syncing data. Requests to the API now return `401 Unauthorized`.

**Category:** API / Authentication  
**Initial priority:** P2 — important workflow unavailable, but the SaaS application itself remains available  
**Environment:** Production integration (simulated)  
**Customer scope:** One customer workspace

> This is a fictional portfolio scenario. No real customer data or production credentials are used.

---

## 1. Customer Report

> Our integration stopped syncing this morning. We haven't changed the integration code. Every API request now fails. Can you check whether the API is down?

The customer's conclusion — “the API is down” — is a hypothesis, not yet the root cause.

---

## 2. Initial Triage

Known information:

- The integration worked previously.
- Failure began recently.
- Requests are reaching the API and receiving an HTTP response.
- The reported status is `401`.
- Only one customer workspace is currently known to be affected.

### Initial assessment

A `401 Unauthorized` response points first toward an **authentication problem**, not a general API outage. Before concluding this, I would verify scope and collect evidence.

---

## 3. Clarifying Questions

1. What is the exact endpoint and HTTP method being called?
2. What is the exact response status and sanitized response body?
3. When did the last successful request occur?
4. What timestamp and timezone correspond to a recent failed request?
5. Are all API requests failing or only one endpoint?
6. Is the same credential/token used across the failing requests?
7. Was the token rotated, revoked or regenerated recently?
8. Is authentication being sent using the expected header format?
9. Can the customer provide a request/correlation ID if the platform returns one?
10. Are other users/workspaces reporting the same behavior?

I would explicitly ask the customer **not to send the actual API token**.

---

## 4. Sanitized Evidence

Example request:

```http
GET /v1/customers HTTP/1.1
Host: api.example.test
Authorization: Bearer [REDACTED]
Accept: application/json
```

Example response:

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json

{
  "error": "invalid_token",
  "message": "The access token is invalid or expired"
}
```

---

## 5. Hypotheses

| Hypothesis | Evidence For | Test |
|---|---|---|
| Expired access token | Response explicitly references invalid/expired token | Check token metadata / issue a new test credential |
| Revoked credential | Previously working integration suddenly fails | Check credential status / audit event if available |
| Missing auth header | Would produce authentication failure | Inspect sanitized request headers |
| Incorrect `Bearer` format | Common integration configuration issue | Compare header against API documentation |
| API-wide outage | Customer suspects outage | Check service health and whether other authenticated requests succeed |
| Permission problem | Could block resource access | Usually more consistent with `403`; test after authentication succeeds |

---

## 6. Investigation

### Test A — Confirm the request reaches the service

The presence of a structured `401` API response indicates that the request reached a service capable of evaluating authentication.

**Result:** General network connectivity is unlikely to be the primary failure.

### Test B — Validate authentication format

Expected pattern:

```http
Authorization: Bearer <token>
```

The sanitized customer request shows the expected scheme and header location.

**Result:** Header formatting is unlikely to be the cause.

### Test C — Test a newly generated credential

In the simulated scenario, a new token is generated through the account's credential management flow and used in the same request.

```http
HTTP/1.1 200 OK
```

**Result:** The endpoint and request structure work with a valid credential.

### Test D — Determine why the previous credential stopped working

The simulated credential metadata indicates that the original token reached its configured expiration time.

**Result:** Root cause confirmed.

---

## 7. Root Cause

**The integration was using an expired API access token.**

The API remained available. Requests were rejected because the credential was no longer valid.

---

## 8. Resolution

1. Generate/obtain a valid replacement credential through the approved credential-management process.
2. Update the integration's secret/configuration store.
3. Do **not** hard-code the token in source code or commit it to version control.
4. Restart/redeploy the integration if required for configuration changes to take effect.
5. Send a test request.
6. Confirm `2xx` responses.
7. Verify that synchronization resumes.
8. Revoke the old credential if it has not already become unusable.

---

## 9. Customer-Facing Response

Hi there,

I checked the behavior you described. The API is reachable, but the requests are being rejected during authentication with a `401 Unauthorized` response.

The integration is using a credential that is no longer valid. After replacing it with a valid token, the same request succeeds normally.

Please update the credential stored by your integration and retry the sync. For security, don't send the token itself in this ticket. If the issue continues after the credential is updated, send us the timestamp of a failed request and its request ID, and we can continue the investigation.

Best,  
Sofia

---

## 10. Internal Note

```text
TS-001
Issue: Integration stopped syncing; API returned 401.
Scope: Single customer workspace.
Evidence: Structured invalid_token response.
Tests: Endpoint reachable; auth header format correct; new credential returned 200.
Root cause: Existing access token expired.
Resolution: Customer instructed to replace stored credential and verify sync.
Escalation: Not required unless valid new credential also returns 401.
Security: No credentials collected in ticket.
```

---

## 11. Escalation Criteria

I would escalate if:

- a newly issued valid token also returns `401`;
- multiple unrelated customers begin reporting the same authentication failure;
- credential metadata shows the token as valid while the authentication service rejects it;
- there is evidence of an authentication-service regression;
- Support lacks the access required to inspect the relevant authentication event/request ID.

---

## 12. Prevention & Product Feedback

Potential improvements:

- Notify customers before long-lived credentials expire, when supported by the authentication model.
- Document token rotation clearly.
- Provide distinct error messages for expired vs malformed credentials when security requirements allow.
- Encourage secret managers/environment variables instead of source-code storage.
- Add monitoring for abnormal increases in authentication failures.

---

## Skills Demonstrated

`HTTP` · `401 Unauthorized` · `API Authentication` · `Bearer Tokens` · `Troubleshooting` · `Hypothesis Testing` · `Security Awareness` · `Root Cause Analysis` · `Customer Communication` · `Escalation Judgment`
