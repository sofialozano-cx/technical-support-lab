<div align="center">

# Technical Support Lab

### SaaS Troubleshooting · APIs · Incident Triage · Customer Communication

![Status](https://img.shields.io/badge/Status-Active%20Lab-6D28D9?style=flat-square)
![Focus](https://img.shields.io/badge/Focus-Technical%20Support-4F46E5?style=flat-square)
![Portfolio](https://img.shields.io/badge/Portfolio-Sofia%20Lozano-7C3AED?style=flat-square)

</div>

---

## Overview

This repository is a hands-on **Technical Support portfolio lab** built around realistic fictional SaaS support scenarios.

The goal is to demonstrate how I approach a technical customer issue from first contact to resolution: **triage, investigation, reproduction, evidence gathering, root-cause analysis, customer communication, documentation, and escalation when required**.

The cases in this repository are simulations created for learning and portfolio purposes. They do not contain real customer data or represent incidents from my employers.

---

## Support Workflow

```text
Customer Report
      ↓
Triage & Impact Assessment
      ↓
Clarifying Questions
      ↓
Reproduce / Gather Evidence
      ↓
Technical Investigation
      ↓
Identify Root Cause
      ↓
Resolve or Escalate
      ↓
Customer Communication
      ↓
Internal Documentation
```

Every case is documented with both the **technical investigation** and the **customer-facing communication** because strong technical support requires both.

---

## Lab Scope

| Area | What I Practice |
|---|---|
| **Ticket Triage** | Impact, urgency, severity, scope and initial classification |
| **Troubleshooting** | Reproduction, hypothesis testing and evidence gathering |
| **HTTP & APIs** | Requests, responses, status codes, headers and payloads |
| **Authentication** | Tokens, credentials, permissions and authorization failures |
| **Webhooks** | Delivery failures, endpoints, status responses and retries |
| **Browser Issues** | Cache, cookies, extensions, sessions and environment isolation |
| **Incident Handling** | Severity assessment, escalation and communication |
| **Documentation** | Internal notes, reproduction steps and reusable knowledge |
| **Customer Communication** | Clear, empathetic and technically accurate responses |

---

## Case Library

| ID | Scenario | Primary Skill | Status |
|---|---|---|---|
| [TS-001](cases/TS-001-api-authentication-401.md) | API request returns `401 Unauthorized` | API Authentication | ✅ Complete |
| [TS-002](cases/TS-002-webhook-delivery-failure.md) | Webhook events are not reaching the customer endpoint | Webhooks | ✅ Complete |
| [TS-003](cases/TS-003-browser-login-loop.md) | User is stuck in a login redirect loop | Browser Troubleshooting | ✅ Complete |
| [TS-004](cases/TS-004-rate-limit-429.md) | Integration intermittently returns `429 Too Many Requests` | Rate Limits | ✅ Complete |
| [TS-005](cases/TS-005-csv-import-validation.md) | Customer CSV import fails validation | Data / Validation | ✅ Complete |
| [TS-006](cases/TS-006-role-permission-403.md) | Team member receives `403 Forbidden` | Permissions / RBAC | ✅ Complete |

---

## Investigation Framework

For each ticket, I use a consistent structure:

1. **Customer report** — What is the customer experiencing?
2. **Impact & priority** — Who is affected and how severely?
3. **Clarifying questions** — What information is missing?
4. **Reproduction** — Can the issue be reproduced consistently?
5. **Evidence** — Status codes, timestamps, request IDs, logs, screenshots or payloads.
6. **Hypotheses** — What are the plausible causes?
7. **Tests** — How can each hypothesis be confirmed or eliminated?
8. **Root cause** — What actually caused the issue?
9. **Resolution** — What fixes or mitigates it?
10. **Customer response** — How should the resolution be communicated clearly?
11. **Internal note** — What should another support agent know next time?
12. **Prevention** — Can documentation, monitoring or product changes reduce recurrence?

---

## Technical Reference

### HTTP status codes used in the lab

| Code | Meaning | Typical Support Question |
|---:|---|---|
| `200` | OK | Did the request succeed but return unexpected data? |
| `201` | Created | Was the resource successfully created? |
| `400` | Bad Request | Is the request malformed or missing required data? |
| `401` | Unauthorized | Is authentication missing, invalid or expired? |
| `403` | Forbidden | Is the authenticated user missing permission? |
| `404` | Not Found | Is the resource or endpoint correct? |
| `409` | Conflict | Does the requested operation conflict with current state? |
| `422` | Unprocessable Content | Is the payload structurally valid but failing validation? |
| `429` | Too Many Requests | Is the client exceeding a rate limit? |
| `500` | Internal Server Error | Is there evidence of a server-side failure? |
| `502/503` | Gateway / Service Unavailable | Is a dependency or service temporarily unavailable? |

### Evidence I would request before escalation

```text
• Exact timestamp + timezone
• Account / workspace identifier (non-secret)
• Endpoint or feature affected
• Steps to reproduce
• Expected vs actual behavior
• HTTP status code
• Request / correlation ID when available
• Sanitized request and response
• Browser / OS / app version when relevant
• Scope: one user, one workspace, or multiple customers?
```

> Secrets such as passwords, API keys, access tokens and sensitive personal data should never be pasted into a support ticket or committed to a repository.

---

## Escalation Principles

An issue should be escalated when support has gathered enough evidence to show that the problem likely requires access, expertise or a product change outside the current support scope.

A useful engineering escalation should include:

```text
SUMMARY
Concise description of the failure

IMPACT
Affected customers / workflows and severity

REPRODUCTION
Exact steps and environment

EXPECTED
What should happen

ACTUAL
What happens instead

EVIDENCE
Timestamps, request IDs, sanitized payloads and relevant logs

TESTS COMPLETED
What Support already ruled out

WORKAROUND
Available mitigation, if any
```

---

## Repository Structure

```text
technical-support-lab/
│
├── README.md
├── cases/
│   ├── TS-001-api-authentication-401.md
│   ├── TS-002-webhook-delivery-failure.md
│   ├── TS-003-browser-login-loop.md
│   ├── TS-004-rate-limit-429.md
│   ├── TS-005-csv-import-validation.md
│   └── TS-006-role-permission-403.md
│
├── templates/
│   ├── ticket-investigation-template.md
│   └── engineering-escalation-template.md
│
└── reference/
    └── troubleshooting-checklist.md
```

---

## Skills Demonstrated

`Technical Support` · `SaaS Support` · `Troubleshooting` · `REST APIs` · `HTTP` · `JSON` · `Authentication` · `Webhooks` · `Incident Triage` · `Root Cause Analysis` · `Escalation` · `Technical Documentation` · `Customer Communication`

---

## Portfolio Context

I have a professional background in **customer experience, CRM and high-volume customer-facing operations** and I am currently pursuing **Software Engineering**. This lab is designed to develop and demonstrate the technical investigation skills used in Technical Support and Support Operations roles.

The scenarios are intentionally separated from my professional experience: **this repository demonstrates hands-on lab work, not claims of production incidents handled for previous employers.**

---

<div align="center">

### Sofia Lozano
Customer Experience · Technical Support · CRM & Support Operations

[GitHub Profile](https://github.com/sofialozano-cx)

</div>
