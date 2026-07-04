# Authentication Security Fundamentals

## Why Authentication Exists

Authentication exists to answer one fundamental question:

> **"Who are you?"**

Without authentication, a system cannot distinguish one user from another.

Authentication establishes a user's identity before granting access to protected resources.

It is the foundation of identity and access management.

---

## The Problem Authentication Solves

Imagine an online banking application.

A user navigates to:

```text
https://bank.com/dashboard
```

Without authentication, the application would have no way of determining:

* Who the user is
* Which account belongs to them
* Whether they should be allowed to access sensitive information

Authentication solves this problem by verifying the user's identity before access is granted.

---

## How Authentication Works

A typical authentication flow is:

```text
User
 │
 ▼
Enter Username + Password
 │
 ▼
Server validates credentials
 │
 ▼
(Optional) Multi-Factor Authentication (MFA)
 │
 ▼
Authentication Successful
 │
 ▼
Create Session
 │
 ▼
Issue Session Cookie
 │
 ▼
Future Requests use Session Cookie
```

Authentication establishes identity.

Sessions maintain identity.

---

## Authentication vs Authorization

Authentication answers:

> **Who are you?**

Authorization answers:

> **What are you allowed to do?**

Example:

A security guard checks your employee badge before allowing you into the building.

Authentication verifies your identity.

Once inside, your role determines which rooms you may enter.

That is authorization.

---

## Authentication Factors

Authentication typically relies on one or more of the following factors.

### Something You Know

Examples:

* Password
* PIN

---

### Something You Have

Examples:

* Mobile Phone
* Authenticator Application
* Hardware Token
* Smart Card

---

### Something You Are

Examples:

* Fingerprint
* Face ID
* Iris Scan

Combining multiple factors creates Multi-Factor Authentication (MFA).

---

## Trust Assumptions

Authentication relies on several important trust assumptions.

Applications assume:

* The user knows the correct password.
* The user possesses the registered authentication device.
* Credentials have not been compromised.
* The login page is legitimate.
* The authentication server is trustworthy.
* The recovery process cannot be abused.

Every one of these assumptions can fail.

Security engineers identify these assumptions and design controls to reduce the associated risk.

---

## Common Authentication Attacks

### Phishing

Attackers trick users into entering credentials on fake login pages.

---

### Credential Stuffing

Attackers use leaked username and password combinations from previous data breaches.

---

### Password Spraying

Attackers try a small number of commonly used passwords across many user accounts.

---

### MFA Fatigue

Attackers repeatedly trigger MFA notifications until the user accidentally approves one.

---

### Session Theft

Rather than attacking authentication directly, attackers steal an authenticated session.

This reinforces an important lesson:

Authentication establishes identity.

Sessions maintain identity.

---

## Defensive Controls

Modern authentication systems implement multiple layers of protection.

Examples include:

* Multi-Factor Authentication (MFA)
* Passkeys
* Account Lockout
* Rate Limiting
* CAPTCHA
* Conditional Access Policies
* Device Trust
* Risk-Based Authentication
* Step-Up Authentication
* Monitoring and Alerting

Security should not rely on a single control.

Defense in depth is essential.

---

## Product Security Perspective

Authentication should always be proportional to the business risk.

Viewing account information may require only an authenticated session.

Changing a registered mobile number, email address, or password should require additional verification.

Examples include:

* Re-entering the password
* Passkey or biometric verification
* Multi-Factor Authentication
* Confirmation through the existing recovery channel
* Risk-Based Authentication

High-risk actions deserve stronger verification than low-risk actions.

---

## Security Engineer Perspective

One of the biggest mindset shifts while learning authentication was realizing that authentication is not simply about logging in.

It is about establishing an appropriate level of trust.

Security engineers should ask:

* What identity is being established?
* What assumptions are we making?
* Can those assumptions be abused?
* Is the authentication strength appropriate for the business risk?
* Are additional controls required for sensitive actions?

Rather than asking:

> "Is the user authenticated?"

Security engineers ask:

> **"Is the current level of trust appropriate for the action being performed?"**

---

## Key Takeaways

* Authentication establishes identity.
* Authorization determines permissions.
* Sessions maintain authenticated identity.
* Authentication relies on multiple trust assumptions.
* Every trust assumption introduces potential risk.
* High-risk actions should require stronger verification.
* Security decisions should be proportional to business risk.
* Effective authentication combines multiple defensive controls.

---

## Interview Questions

### 1. What is the difference between authentication and authorization?

### 2. Why is Multi-Factor Authentication more secure than passwords alone?

### 3. What is Credential Stuffing?

### 4. What is MFA Fatigue?

### 5. Why are Passkeys becoming increasingly popular?

### 6. Why should high-risk actions require Step-Up Authentication?

### 7. Why should changing recovery information require stronger verification than viewing account information?

---

## Security Engineer Questions

Whenever reviewing an authentication system, ask:

* What identity is being established?
* What trust assumptions exist?
* How can an attacker abuse those assumptions?
* What defensive controls are implemented?
* Is the authentication strength appropriate for the business risk?
* What telemetry would help detect authentication abuse?

## Personal Reflection

### My biggest takeaway

Authentication taught me that security is fundamentally about trust.

The question is not simply:

"Is the user authenticated?"

Instead, security engineers ask:

"What assumptions are we trusting, and are those assumptions appropriate for the risk?"

This realization has fundamentally changed the way I analyze systems.

<img width="331" height="281" alt="authetication_flow" src="https://github.com/user-attachments/assets/ae256ffd-1a4e-4ed5-b5f2-f207fd2dba99" />
<img width="190" height="364" alt="Authentication_security_perspective" src="https://github.com/user-attachments/assets/d3a4cdb4-1f3d-4c2b-8917-0bc6b79f2dc6" />

