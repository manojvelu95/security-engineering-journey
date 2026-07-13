# Authorization Security Fundamentals

## Why Authorization Exists

Authorization exists to answer one fundamental question:

> **"What is an authenticated user allowed to do?"**

Authentication alone is not sufficient to protect applications.

Once a user's identity has been verified, the application must determine what resources and actions that user is permitted to access.

Authorization ensures users can only perform actions they are explicitly allowed to perform.

---

# The Problem Authorization Solves

Imagine two users successfully log into an application.

User A:
Role: Employee

User B:
Role: Administrator

Both users are authenticated.

Without authorization, both users would have the same permissions.

This could allow an employee to:

- Delete users
- View payroll
- Access sensitive data
- Modify system settings

Authorization prevents authenticated users from accessing resources beyond their permissions.

---

# Authentication vs Authorization

Authentication answers:

> **Who are you?**

Authorization answers:

> **What are you allowed to do?**

Example:

A passenger enters an airport after showing a boarding pass.

Authentication verifies the passenger's identity.

However, only pilots are authorized to enter the cockpit.

Identity alone does not grant permission.

---

# How Authorization Works

A typical authorization flow is:

User
 │
 ▼
Authentication
 │
 ▼
Authenticated Session
 │
 ▼
User Requests Resource
 │
 ▼
Authorization Engine
 │
 ├── Verify Role
 ├── Verify Ownership
 ├── Verify Permissions
 │
 ▼
Allow or Deny Request

## Trust Assumptions

Authorization relies on several trust assumptions.

Applications assume:

- The authenticated identity is correct.
- User roles are correctly assigned.
- Permissions are accurate.
- Resource ownership is verified.
- Client requests cannot be blindly trusted.
- Authorization decisions are enforced on the server.

Every trust assumption introduces potential risk.

Security engineers should identify these assumptions and validate them.

---

## Common Authorization Attacks

### Broken Access Control (BAC)

Users access resources they should not be permitted to access.

---

### Insecure Direct Object Reference (IDOR)

Example:

GET /invoice?id=100

Attacker changes:

GET /invoice?id=101

If the server fails to verify ownership, another user's invoice may be exposed.

---

### Privilege Escalation

An attacker attempts to gain permissions beyond those assigned.

Examples include:

- Changing role values
- Exploiting misconfigured permissions
- Abusing administrative APIs

---

### Forced Browsing

Attackers manually browse sensitive endpoints such as:

/admin

hoping the application fails to perform authorization checks.

## Defensive Controls

Modern applications should implement:

- Server-side Authorization
- Ownership Validation
- Principle of Least Privilege
- Deny by Default
- Fine-Grained Permissions
- Authorization Logging
- Regular Permission Reviews
- Step-Up Authentication for High-Risk Actions

Security should never rely solely on client-side checks.

Authorization decisions must always be enforced on the server.

## Product Security Perspective

One of the most valuable lessons while learning authorization was understanding that permissions should follow business rules.

Example:

Netflix Family Account

Parent

- Manage Subscription
- View Payment Methods
- Delete Account
- Manage Parental Controls

Child

- Watch Content
- Continue Watching
- Manage Personal Profile

Blocked Actions

- Billing
- Payment Methods
- Subscription Changes
- Account Deletion

Guest

- View Content Only

Even if the Parent is already authenticated, high-risk actions such as changing the subscription or deleting the account should require Step-Up Authentication.

Security decisions should always be proportional to business risk.

## Security Engineer Perspective

One of the biggest mindset shifts while learning authorization was realizing that identity alone does not determine permissions.

Being authenticated does not mean a user should have unrestricted access.

Security engineers should ask:

- What is the application trusting?
- Who owns this resource?
- Is the user authorized for this action?
- What business rule governs this decision?
- Can the client manipulate this request?
- Is authorization enforced on the server?

Rather than asking:

"Is the user logged in?"

Security engineers ask:

"Should this user be allowed to perform this action?"

## Key Takeaways

- Authentication establishes identity.
- Authorization determines permissions.
- Identity alone does not grant access.
- Authorization should follow business rules.
- Broken Access Control is one of the most critical web security risks.
- Ownership validation is essential.
- Least Privilege reduces attack surface.
- High-risk actions should require additional verification.
- Security decisions should align with business risk.

## Interview Questions

1. What is the difference between Authentication and Authorization?

2. What is the Principle of Least Privilege?

3. What is Broken Access Control?

4. What is IDOR?

5. Why should authorization always be enforced on the server?

6. What is the difference between RBAC and ABAC?

7. Why should ownership be verified before returning sensitive resources?

8. Why might an authenticated user still require Step-Up Authentication?

## Security Engineer Questions

Whenever reviewing authorization, ask:

- What resource is being protected?
- Who owns the resource?
- What permissions are required?
- What trust assumptions exist?
- Can an attacker manipulate identifiers?
- Are authorization decisions made server-side?
- What would happen if this authorization check failed?

## Personal Reflection

### My Biggest Takeaway

The biggest lesson I learned today is that authentication and authorization solve different problems.

Authentication tells the application who I am.

Authorization determines what I am allowed to do.

The most valuable realization was understanding that authorization is driven by business rules, not technical implementation.

As a Security Engineer, I should no longer ask:

"Is the user authenticated?"

Instead, I should ask:

"Should this user be allowed to perform this specific action based on the business requirements?"

This shift in thinking has fundamentally changed how I look at application security.

<img width="233" height="342" alt="authorization_flow" src="https://github.com/user-attachments/assets/a3619cc6-a881-4bed-b2ee-5b5ee2f282e0" />
<img width="190" height="358" alt="authorization_securityperspective" src="https://github.com/user-attachments/assets/b0f119a4-38a2-452d-8c40-8da4e9ddeedd" />


