# Troubleshooting Checklist

A reusable checklist for structured Technical Support investigations.

## 1. Understand the Problem

- [ ] Restate the issue without assuming the cause.
- [ ] Capture expected vs actual behavior.
- [ ] Determine when it started.
- [ ] Determine whether it ever worked.
- [ ] Identify recent changes.

## 2. Establish Scope

- [ ] One user or multiple users?
- [ ] One workspace/account or multiple?
- [ ] One endpoint/feature or the whole product?
- [ ] One browser/device/network or multiple?
- [ ] Production only or other environments too?

## 3. Assess Impact

- [ ] Is a critical workflow blocked?
- [ ] Is there a workaround?
- [ ] Is data at risk?
- [ ] Is the customer completely unable to use the product?
- [ ] Does severity need to change?

## 4. Gather Evidence

- [ ] Exact timestamp + timezone
- [ ] Reproduction steps
- [ ] Error text/code
- [ ] HTTP status
- [ ] Request/correlation ID
- [ ] Sanitized request/response
- [ ] Relevant logs
- [ ] Browser/OS/app version when relevant

## 5. Protect Sensitive Information

Do **not** request or store:

- passwords;
- API keys;
- access/refresh tokens;
- full payment-card data;
- unnecessary personal information.

Redact secrets from screenshots, logs and payloads.

## 6. Isolate Variables

Change one meaningful variable at a time where possible:

```text
account → browser → device → network → configuration → request → service
```

Use comparison tests:

- affected vs unaffected user;
- failing vs successful request;
- current vs known-good configuration;
- normal vs private browser session;
- old vs newly issued credential.

## 7. Build Hypotheses

For every likely cause, ask:

```text
What evidence would I expect if this were true?
What test could disprove it?
```

Avoid locking onto the customer's diagnosis or the first plausible explanation.

## 8. Resolve or Escalate

Before escalating, provide Engineering with enough information to avoid repeating Support's work.

Escalate when:

- evidence suggests a product/service defect;
- required logs/access are outside Support scope;
- documented behavior differs from observed behavior;
- multiple customers indicate a possible incident;
- no safe workaround exists for a high-impact issue.

## 9. Communicate

A useful customer update answers:

1. What do we know?
2. What should the customer do now?
3. What are we doing next?
4. When appropriate, what information do we need?

Avoid unsupported certainty.

## 10. Close the Loop

- [ ] Confirm resolution with the customer.
- [ ] Record root cause when known.
- [ ] Document workaround/resolution.
- [ ] Identify knowledge-base opportunity.
- [ ] Identify recurring product/process issue.
