# Cookies & Sessions Security Fundamentals

## Why Cookies and Sessions Exist

HTTP is a **stateless protocol**, meaning the server treats every request as a new request and does not remember previous interactions.

Without sessions, users would have to authenticate on every request.

Sessions were introduced to maintain a user's authenticated state across multiple HTTP requests.

Cookies are the mechanism most commonly used by browsers to store and send session identifiers back to the server.

---

# The Problem

Imagine logging into your online banking application.

Request 1:

```text
POST /login
Username: Manoj
Password: ********
```

The server successfully authenticates the user.

Now the user clicks:

```text
View Account Balance
```

Question:

How does the server know it is still the same authenticated user?

The user did not send the password again.

This is the problem that sessions solve.

---

## How Sessions Work

After successful authentication:

1. The user submits credentials.
2. The server validates the credentials.
3. The server creates a unique Session ID.
4. The Session ID is sent back to the browser as a cookie.
5. The browser stores the cookie.
6. Every future request automatically includes the session cookie.
7. The server verifies the Session ID and recognizes the authenticated user.

Example flow:

```text
User
 │
 ▼
Login
 │
 ▼
Server validates credentials
 │
 ▼
Server creates Session ID
 │
 ▼
Set-Cookie: sessionid=ABC123
 │
 ▼
Browser stores session cookie
 │
 ▼
Future Requests
 │
 ▼
Cookie: sessionid=ABC123
 │
 ▼
Server verifies session
 │
 ▼
User remains authenticated
```

---

## What is a Cookie?

A cookie is a small piece of data stored by the browser.

Example:

```text
sessionid=ABC123XYZ
```

On every future request, the browser automatically sends the cookie back to the server.

The cookie itself does not usually contain the user's password.

Instead, it contains a session identifier that represents the authenticated session.

---

## Authentication vs Session

Authentication and sessions serve different purposes.

Authentication establishes identity.

Sessions maintain identity.

Example:

```text
Username + Password (+ MFA)
          │
          ▼
Authentication
          │
          ▼
Server verifies identity
          │
          ▼
Session Created
          │
          ▼
Session Cookie Issued
          │
          ▼
Future Requests
          │
          ▼
Session Cookie represents the authenticated user
```

---

## Trust Assumptions

Applications trust that:

* The session cookie belongs to the authenticated user.
* The session ID has not been stolen.
* The browser stores the cookie securely.
* The client sends the original cookie.
* The session has not expired.

If any of these assumptions fail, the application may allow unauthorized access.

---

## Why Attackers Target Sessions

Once a user has authenticated successfully, the session cookie becomes the proof of identity.

If an attacker steals a valid session cookie, they may be able to impersonate the user without knowing:

* Username
* Password
* Multi-Factor Authentication (MFA)

This makes session cookies one of the most valuable targets during web application attacks.

---

## Common Session Attacks

### Session Hijacking

An attacker steals a valid session cookie and reuses it to impersonate the authenticated user.

---

### Cross-Site Scripting (XSS)

Malicious JavaScript steals cookies that are accessible to client-side scripts.

---

### Session Fixation

An attacker forces the victim to use a session identifier chosen by the attacker.

---

### Cookie Replay

An attacker reuses a stolen session cookie to access an authenticated session.

---

## Defensive Controls

Modern applications should protect session cookies using multiple layers of security.

### HttpOnly

Prevents JavaScript from accessing the cookie, reducing the impact of many XSS attacks.

---

### Secure

Ensures the cookie is only transmitted over HTTPS.

---

### SameSite

Helps reduce the risk of Cross-Site Request Forgery (CSRF) by controlling when cookies are sent with cross-site requests.

---

### Session Rotation

Generate a new Session ID after successful authentication or privilege changes to reduce the usefulness of stolen session identifiers.

---

### Session Timeout

Expire inactive sessions after a defined period.

Many applications also implement an absolute session lifetime to limit long-lived sessions.

---

### Logout Invalidation

Invalidate the session on the server after the user logs out so the old Session ID can no longer be used.

---

### Monitoring and Anomaly Detection

Monitor for unusual session activity, such as:

* New geographic locations
* Impossible travel
* New devices
* Multiple simultaneous sessions

---

## Security Engineer Perspective

One of the biggest mindset shifts for me was realizing that:

**Passwords establish identity.**

**Sessions maintain identity.**

After authentication, the server no longer relies on the user's password for every request.

Instead, it trusts the Session ID.

This means protecting session cookies is just as important as protecting user credentials.

Security engineers should ask:

* What represents the user's identity?
* Can the session be stolen?
* Can JavaScript access the cookie?
* Is HTTPS enforced?
* Does the session expire?
* Is the Session ID rotated after login?
* Is additional verification required for high-risk actions?

---

## Product Security Perspective

Not every action should rely solely on a valid session.

For low-risk actions (such as viewing account balances), the session may be sufficient.

For high-risk actions (such as transferring $100,000), additional verification should be required.

Examples include:

* Multi-Factor Authentication (MFA)
* Transaction PIN
* Biometrics
* Step-Up Authentication
* Risk-Based Authentication

Security should always be proportional to the risk of the action being performed.

---

## Key Takeaways

* HTTP is stateless.
* Sessions allow applications to remember authenticated users.
* Cookies store Session IDs.
* Session cookies represent an authenticated user's identity.
* Authentication establishes identity.
* Sessions maintain identity.
* Session cookies are valuable targets for attackers.
* Applications should protect sessions using multiple defensive controls.
* High-risk actions should require stronger verification than low-risk actions.

---

## Security Engineer Questions

Whenever reviewing a web application, ask:

* What represents the user's identity?
* What is the server trusting?
* Can the session be stolen?
* Can the session be replayed?
* Are cookies protected with HttpOnly, Secure and SameSite?
* Does the application rotate Session IDs?
* Does the application require Step-Up Authentication for high-risk actions?
* What telemetry would help detect session abuse?

<img width="211" height="304" alt="SessionCreation_cookie_flow" src="https://github.com/user-attachments/assets/a5da3275-5615-46f4-b16c-9366e2f8a509" />
<img width="161" height="368" alt="Trust_assumptions" src="https://github.com/user-attachments/assets/fa47f73f-5be2-4426-b75b-5538951f1e2e" />
<img width="157" height="230" alt="authentication_vs_session" src="https://github.com/user-attachments/assets/cdc21113-fd10-4046-848a-f51cdbad8561" />
<img width="145" height="55" alt="authentication_vs_session_2" src="https://github.com/user-attachments/assets/b068d7d6-ca08-41d3-960b-be8c8b16fb79" />


