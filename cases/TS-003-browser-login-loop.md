# TS-003 — Browser Login Redirect Loop

## Ticket Summary

**Scenario:** A fictional customer can enter valid credentials but is repeatedly redirected back to the sign-in page in one browser.

**Category:** Login / Browser  
**Initial priority:** P3  
**Scope:** One user

---

## Customer Report

> I can enter my password, but after signing in I'm sent straight back to the login page. I've already reset my password twice.

---

## Triage

A password reset is not automatically the correct next step because the user appears to pass the credential-entry stage.

I would first determine whether the problem is:

- account-wide;
- device-specific;
- browser-specific;
- session/cookie-related;
- extension-related;
- caused by an authentication service issue.

---

## Isolation Tests

| Test | Result | Interpretation |
|---|---|---|
| Same account in private/incognito window | Works | Account credentials likely valid |
| Same account in another browser | Works | Issue likely local to original browser |
| Other users affected | No known reports | Low evidence of platform-wide incident |
| Disable extensions | No change | Extension less likely |
| Clear site-specific cookies/session data | Works | Stale/corrupted session state likely |

---

## Root Cause

**Stale/corrupted site session data in the original browser prevented the new authenticated session from persisting correctly.**

---

## Resolution

Rather than asking the customer to clear all browser data, I would use the least destructive step first:

1. Sign out where possible.
2. Clear cookies/site data **for the affected application domain only**.
3. Close and reopen the tab/browser.
4. Sign in again.
5. Confirm the session persists across navigation.

---

## Customer-Facing Response

Hi there,

Your account credentials are working — I was able to narrow this down to the browser session rather than the password itself.

Please clear the stored cookies/site data for the application domain, then reopen the browser and sign in again. You don't need to clear your entire browser history.

If the redirect continues after that, let me know the browser name/version and whether the issue also occurs in a private window, and we'll continue from there.

Best,  
Sofia

---

## Internal Note

```text
Issue: Login redirects user back to sign-in page.
Scope: One user / one browser.
Isolation: Account works in incognito and second browser.
Resolution: Clearing site-specific session data resolved issue.
Escalation: Not required.
```

---

## Key Learning

Troubleshooting should **isolate variables before applying broad fixes**. Testing another browser/private session separated an account/authentication problem from a local browser-state problem.

## Skills Demonstrated

`Browser Troubleshooting` · `Authentication` · `Cookies` · `Sessions` · `Issue Isolation` · `Customer Communication`
