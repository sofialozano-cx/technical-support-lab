# TS-006 — Role Permission Failure (`403 Forbidden`)

## Scenario

A fictional team member can sign in successfully and access the application, but receives `403 Forbidden` when attempting an administrative action.

**Category:** Authorization / RBAC  
**Priority:** P3  
**Scope:** One user

---

## Triage

The distinction between authentication and authorization matters:

```text
401 → Who are you? / Is your authentication valid?
403 → We know who you are, but you are not allowed to perform this action.
```

A `403` after successful login suggests investigating **permissions, roles, resource ownership or policy** before resetting credentials.

---

## Evidence

```http
DELETE /v1/team/members/usr_482 HTTP/1.1
Authorization: Bearer [REDACTED]

HTTP/1.1 403 Forbidden
Content-Type: application/json

{
  "error": "insufficient_permissions"
}
```

The same user can successfully read team data.

---

## Investigation

- Authentication succeeds.
- Read operations succeed.
- Administrative delete action fails.
- User's simulated role: `Member`.
- Required role for this action: `Admin` or `Owner`.

---

## Root Cause

**The user is authenticated correctly but their assigned role does not include permission to perform the requested administrative action.**

---

## Resolution

Two safe options depending on the customer's intended access model:

1. Ask an existing Admin/Owner to perform the action; or
2. Have an authorized administrator change the user's role if they genuinely require ongoing administrative access.

Do not grant elevated privileges merely to make an error disappear. Apply the principle of least privilege.

---

## Customer-Facing Response

Hi there,

Your account is signing in correctly. The `403 Forbidden` response is related to permissions rather than your password or session.

Your current role can view the team but doesn't have permission to remove team members. An Admin/Owner can perform that action, or an authorized administrator can update your role if administrative access is appropriate for your responsibilities.

Best,  
Sofia

---

## Key Learning

Separating **authentication** from **authorization** prevents unnecessary password resets and helps Support investigate the correct control layer.

## Skills Demonstrated

`HTTP 403` · `Authorization` · `RBAC` · `Least Privilege` · `API Troubleshooting` · `Customer Communication`
