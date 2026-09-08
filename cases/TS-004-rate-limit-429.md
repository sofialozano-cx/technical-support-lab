# TS-004 — API Rate Limit (`429 Too Many Requests`)

## Scenario

A fictional customer's integration succeeds most of the day but fails during large synchronization jobs with `429 Too Many Requests`.

**Category:** API / Performance  
**Priority:** P2  
**Scope:** One integration

---

## Evidence

```http
HTTP/1.1 429 Too Many Requests
Retry-After: 30
Content-Type: application/json

{
  "error": "rate_limit_exceeded"
}
```

The failures cluster during bursts of parallel requests.

---

## Investigation

Questions/tests:

- Does the API return rate-limit headers?
- Is the integration sending requests concurrently?
- Does failure correlate with batch jobs?
- Does the client respect `Retry-After`?
- Is there unnecessary polling or duplicate requests?

The simulated integration sends a large number of parallel requests and immediately retries failures, creating additional traffic.

---

## Root Cause

**The client exceeds the API's request limit during burst synchronization and retries too aggressively.**

---

## Resolution

- Respect `Retry-After` when supplied.
- Reduce request concurrency.
- Implement exponential backoff with jitter for retryable failures.
- Avoid retrying non-retryable `4xx` responses indiscriminately.
- Reduce unnecessary polling and batch requests where supported.
- Monitor rate-limit consumption.

Pseudo-flow:

```text
request
  ↓
429?
  ├─ no → continue
  └─ yes
       ↓
 read Retry-After
       ↓
 wait / back off
       ↓
 retry within safe policy
```

---

## Customer-Facing Response

Hi there,

The failed requests are returning `429 Too Many Requests`, and they line up with the periods when the integration sends a large burst of concurrent API calls.

The API is available, but the integration is temporarily exceeding its request limit. I recommend reducing concurrency and honoring the `Retry-After` response before retrying. Adding exponential backoff will also prevent retries from creating another burst.

If the integration still reaches the limit after those changes, we can review the request pattern and expected workload in more detail.

Best,  
Sofia

---

## Escalation Criteria

Escalate if documented limits are not being exceeded but the service still returns `429`, or if returned rate-limit metadata conflicts with documented behavior.

## Skills Demonstrated

`HTTP 429` · `Rate Limiting` · `Retry-After` · `Exponential Backoff` · `API Troubleshooting` · `Customer Communication`
