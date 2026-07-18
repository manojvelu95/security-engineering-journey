# OAuth 2.0 Security Fundamentals

## Why OAuth Exists

OAuth was created to solve one fundamental problem:

> **How can one application access another application's resources without asking for the user's password?**

Before OAuth, third-party applications often requested users to share their usernames and passwords.

This created significant security risks because applications gained unrestricted access to user accounts and credentials.

OAuth introduced a safer model by allowing applications to obtain limited permissions through delegated authorization.

---

# The Problem OAuth Solves

Imagine a Karaoke application wants to connect with Spotify.

Without OAuth:

User
↓

Provides Spotify Username & Password

↓

Karaoke App logs into Spotify

↓

Full Account Access

Problems:

- Third-party application knows the user's password.
- Password may be stored insecurely.
- A compromise exposes user credentials.
- Users cannot revoke access to only one application.

OAuth eliminates this problem by delegating authorization instead of sharing credentials.

---

# OAuth Flow

A simplified OAuth flow is shown below.

User
 │
 ▼
Clicks "Connect with Spotify"
 │
 ▼
Redirected to Spotify
 │
 ▼
Spotify authenticates the user
 │
 ▼
Spotify asks for user consent
 │
 ▼
User approves requested permissions
 │
 ▼
Spotify issues an Access Token
 │
 ▼
Third-party application accesses only the approved resources

Notice:

The third-party application never receives the user's Spotify password.

---

# Key Components

## Resource Owner

The user who owns the data.

Example:

Spotify User

---

## Client

The application requesting access.

Example:

Karaoke Application

---

## Authorization Server

Authenticates the user and issues access tokens.

Example:

Spotify Authorization Server

---

## Resource Server

Hosts the protected resources.

Example:

Spotify API

---

## Access Token

A temporary credential that allows applications to access only approved resources.

Tokens represent delegated permissions.

They should be protected just like session cookies.

---

# Scopes

One of OAuth's strongest security features is the concept of scopes.

Scopes define what permissions are being delegated.

Example:

Read Playlists

Read Profile

Read Email

The application should request only the minimum permissions required.

This follows the Principle of Least Privilege.

# Trust Assumptions

OAuth relies on several trust assumptions.

Applications assume:

- The Identity Provider authenticated the user correctly.
- The Access Token is valid.
- The Access Token has not expired.
- The Access Token has not been stolen.
- The requested scopes are appropriate.
- The third-party application will use the granted permissions responsibly.

Security engineers should identify these assumptions before approving an integration.

---

# Common OAuth Risks

## Token Theft

If an attacker steals an Access Token, they may impersonate the application within the granted permissions.

---

## Excessive Permissions

Applications request permissions beyond what is necessary.

Example:

A flashlight application requesting access to:

- Gmail
- Contacts
- Google Drive
- Photos
- Calendar

Every permission should have a business justification.

---

## Malicious Third-Party Applications

Users may authorize applications without understanding the requested permissions.

---

## Scope Abuse

Applications continue requesting broad permissions even when only limited access is required.

---

# Defensive Controls

Modern OAuth implementations should include:

- Least Privilege Scopes
- User Consent
- Token Expiration
- Token Revocation
- Secure Token Storage
- Vendor Security Assessment
- Regular Permission Reviews

# Product Security Perspective

One of the biggest mindset shifts while learning OAuth was realizing that security discussions should begin with the business problem—not the technology.

Before reviewing an OAuth integration, I would ask:

- What business problem are we solving?
- Why does this integration exist?
- What data does the application actually need?
- What permissions are required?
- Are those permissions proportional to the business need?
- What trust relationships are being created?
- What could happen if the Access Token is compromised?

Technology should be selected only after understanding the business requirements.

# Real World Observation

## Application Reviewed

GitHub

## Feature Reviewed

Authorized OAuth Applications

### Observations

GitHub Android is a first-party application developed by GitHub.

The requested permissions aligned with its business purpose of providing a full GitHub experience on mobile devices.

Git Credential Manager requested repository-related permissions that aligned with its responsibility of authenticating Git operations.

This exercise reinforced the importance of reviewing every permission against the application's intended functionality rather than accepting permissions by default.

# Security Engineer Perspective

One of the biggest mindset shifts while learning OAuth was understanding that permissions should always be justified by business requirements.

Rather than asking:

"What permissions does the application request?"

Security engineers should ask:

- Why is this permission required?
- What business requirement justifies it?
- Can the same objective be achieved with fewer permissions?
- Is this a first-party or third-party application?
- How can the user revoke access later?

Every permission introduces trust.

Every trust relationship introduces risk.

# Key Takeaways

- OAuth enables delegated authorization.
- Applications should never request user passwords.
- Access Tokens represent delegated permissions.
- Scopes implement the Principle of Least Privilege.
- Every permission should have a business justification.
- OAuth begins with understanding the business problem.
- Trust relationships should always be reviewed.
- Technology should support the business—not drive it.

# Interview Questions

1. Why was OAuth created?

2. What problem does OAuth solve?

3. What is the difference between Authentication and Authorization?

4. What is an Access Token?

5. What are OAuth Scopes?

6. Why is Least Privilege important?

7. What risks arise if an Access Token is stolen?

8. How would you review a third-party OAuth integration?

# Security Engineer Questions

Whenever reviewing an OAuth integration, ask:

- What business problem is being solved?
- What data is actually required?
- What permissions are being requested?
- Are those permissions justified?
- What trust relationships are created?
- How can the user revoke access?
- What happens if the Access Token is compromised?
- How can permissions be reduced?

# Personal Reflection

## My Biggest Takeaway:

Today's lesson fundamentally changed how I think about third-party integrations.

Previously, I thought OAuth was simply a technology used for "Sign in with Google."

Now I understand that OAuth is a trust model built around delegated authorization.

The most valuable realization was that Product Security begins with understanding the business problem.

Technology comes later.

As a Security Engineer, I should no longer begin by asking:

"What technology is being used?"

Instead, I should ask:

"What business problem are we solving, and what is the minimum level of trust required to solve it securely?"

<img width="287" height="336" alt="O-Auth_flow" src="https://github.com/user-attachments/assets/6e85e849-9461-40f0-b727-ead3b5e66e0e" />
<img width="183" height="395" alt="O-Auth_security_perspective" src="https://github.com/user-attachments/assets/b98df583-c846-4eeb-b2f8-51d05613630f" />

