# TS-002 — Webhook Delivery Failure

## Ticket Summary

**Scenario:** A fictional SaaS customer reports that new events appear correctly inside the product, but their external integration no longer receives webhook notifications.

**Category:** Integration / Webhooks  
**Initial priority:** P2  
**Scope:** One customer endpoint  
**Environment:** Simulated production integration

> Portfolio simulation only. Domains, payloads and identifiers are fictional.

---

## Customer Report

> Events are being created in the dashboard, but our system stopped receiving webhooks. We think your platform isn't sending them.

---

## Triage & Clarifying Questions

I would establish whether the platform failed to **generate**, **attempt**, or **successfully deliver** the webhook.

Questions:

1. Which event types are missing?
2. When was the last successfully received event?
3. What is the configured endpoint URL?
4. Are delivery attempts visible in webhook history?
5. What HTTP response does the endpoint return?
6. Did the customer recently change hosting, firewall, TLS certificate or routing?
7. Are all webhook events failing or only specific payloads?

---

## Evidence

Simulated delivery record:

```text
Event: customer.updated
Delivery ID: wh_del_01928
Attempted: 2026-09-08T13:24:11Z
Endpoint: https://hooks.customer.example/events
Response: 404 Not Found
Duration: 184 ms
```

This shows that the SaaS platform **attempted delivery and received a response** from the destination.

---

## Hypotheses

| Hypothesis | Test |
|---|---|
| Platform is not generating webhooks | Check event/delivery history |
| Destination is unreachable | Check whether a network response exists |
| Endpoint path changed | Compare configured URL with customer's current route |
| Firewall blocks requests | Usually investigate timeout/refusal rather than a clean `404` |
| Payload rejected | Inspect destination status/body; often `4xx` validation response |

---

## Investigation

Delivery history confirms repeated attempts to the configured endpoint. Each receives `404 Not Found`.

The customer confirms that their application route was recently changed from:

```text
/webhooks/events
```

to:

```text
/integrations/webhooks
```

but the endpoint configured in the SaaS platform still references the previous route.

A test delivery to the new endpoint returns:

```http
HTTP/1.1 200 OK
```

---

## Root Cause

**The customer's webhook destination path changed, but the webhook configuration still pointed to the old route.**

The SaaS platform was generating and attempting deliveries correctly.

---

## Resolution

- Update the webhook destination to the current endpoint.
- Send a test event.
- Confirm a `2xx` response.
- Verify the event is processed by the destination application.
- Review failed deliveries and replay them if the product supports safe replay.

---

## Customer-Facing Response

Hi there,

I found the delivery attempts for the missing events. The platform is sending them, but the configured destination is responding with `404 Not Found`.

The webhook configuration still points to the previous endpoint path. After updating it to your current route, a test delivery returns `200 OK`.

Please confirm that the test event also appears correctly in your receiving application. If needed, we can then review whether the failed events should be replayed.

Best,  
Sofia

---

## Internal Note

```text
Issue: Customer not receiving webhooks.
Evidence: Delivery history shows attempts returning 404.
Root cause: Customer changed receiving route; SaaS config retained old path.
Resolution: Endpoint updated; test delivery returned 200.
Escalation: Not required.
Follow-up: Confirm downstream processing and replay requirements.
```

---

## Key Learning

“Webhook not received” does not automatically mean “webhook not sent.” Separating **event generation → delivery attempt → destination response → downstream processing** prevents premature conclusions.

## Skills Demonstrated

`Webhooks` · `HTTP` · `404` · `Integration Troubleshooting` · `Evidence Gathering` · `Root Cause Analysis` · `Customer Communication`
