# JSON Web Token (JWT) Security Fundamentals

## Why JWT Exists

JWT (JSON Web Token) was created to solve a common problem in modern web applications:

> **How can a server securely identify a user across multiple requests without storing session state?**

Traditional web applications often maintain sessions on the server. While this works well, managing session state becomes more challenging as applications scale across multiple servers and regions.

JWT provides a stateless approach by allowing the server to issue a digitally signed token that the client presents with each request.

Instead of storing user session information on the server, the server verifies the JWT on every request.

---

# The Problem JWT Solves

Imagine Netflix.

A user logs in successfully.

After authentication, the user clicks:

- Home
- Movies
- Search
- My List
- Profile

Each request reaches a backend server.

How does the server know these requests belong to the same authenticated user?

JWT solves this by allowing the client to send a signed token with every request.

The server verifies the token instead of maintaining session state.

# JWT Authentication Flow

User

↓

Logs in with Username & Password

↓

Authentication Server verifies credentials

↓

Authentication Server generates and signs JWT

↓

JWT returned to Client

↓

Client stores JWT securely

↓

Client sends JWT with every API request

↓

API Server verifies:

- Signature
- Expiration
- Claims

↓

Access Granted

Notice:

The server trusts the JWT only after verifying its signature.
# JWT Structure

A JWT consists of three parts separated by dots.

Header.Payload.Signature

Example:

xxxxx.yyyyy.zzzzz

---

## Header

Contains metadata describing the token.

Example:

{
  "alg": "RS256",
  "typ": "JWT"
}

Common information includes:

- Signing Algorithm
- Token Type

---

## Payload

Contains claims about the authenticated user.

Example:

{
  "sub": "12345",
  "role": "user",
  "exp": 1750000000
}

Important:

The payload is **encoded**, not encrypted.

Anyone who possesses the token can decode its payload.

Sensitive information should never be stored inside a JWT.

---

## Signature

The signature protects the integrity of the token.

The Authorization Server signs the JWT using a secret or private key.

Every receiving server verifies this signature before trusting the claims.

If the payload is modified, signature validation fails and the token is rejected.

# Common JWT Claims

## sub (Subject)

Uniquely identifies the authenticated user.

Example:

sub = 12345

---

## role

Represents the user's authorization level.

Example:

role = admin

Only include this if the application actually needs it.

---

## exp (Expiration)

Defines when the token expires.

Short-lived tokens reduce the impact of token theft.

# Trust Assumptions

JWT relies on several important trust assumptions.

The application trusts that:

- The Authorization Server issued the token.
- The signature is valid.
- The signing key has not been compromised.
- The token has not expired.
- The claims accurately represent the authenticated user.
- The token is intended for this application (correct audience).

A Product Security Engineer should identify and validate these assumptions during architecture reviews.

# Common JWT Security Risks

## Token Theft

If an attacker steals a valid JWT, they may impersonate the user until the token expires.

---

## Weak Signing Keys

Weak secrets increase the risk of attackers forging tokens.

---

## Long Token Lifetime

Tokens that remain valid for days or weeks increase the impact of token theft.

---

## Sensitive Information in Payload

Never store:

- Passwords
- Credit Card Numbers
- Passport Numbers
- API Keys
- Secrets

Remember:

Encoded does not mean encrypted.

---

## Signature Validation Errors

Applications must always verify the JWT signature before trusting its claims.

# Defensive Controls

Modern JWT implementations should include:

- Strong signing algorithms
- Secure key management
- Signature verification
- Short-lived Access Tokens
- Token revocation strategy
- Least-Privilege Claims
- Secure client-side storage

# Product Security Perspective

One of the biggest lessons while learning JWT was realizing that every claim inside a token should have a business justification.

Instead of asking:

"What information should we include?"

A Product Security Engineer should ask:

- Why is this claim needed?
- Does it solve a business problem?
- Is there a less-privileged alternative?
- What happens if this token is stolen?
- Can the application function without this claim?

JWTs should contain only the minimum information required for the application to function securely.

# Real World Design Review

## Example Payload

{
  "sub": "12345",
  "role": "admin",
  "department": "Finance",
  "country": "India",
  "theme": "dark",
  "preferredLanguage": "English",
  "exp": 1750000000
}

During a Product Security review, the goal is not to immediately reject claims.

Instead, ask:

- Why is this claim required?
- What business requirement does it satisfy?
- What happens if we remove it?
- Does it introduce unnecessary exposure?

For example:

- `sub` uniquely identifies the user and is generally essential.
- `role` may be required for authorization decisions.
- `department` may be justified if business logic depends on it.
- `country` may be required for regional compliance or feature restrictions.
- `theme` is a user preference and likely belongs outside the security token.
- `preferredLanguage` should only be included if it provides measurable value.

Every additional claim increases the amount of information exposed if the token is compromised.

# Security Engineer Perspective

Security is rarely about saying "No."

It is about understanding business requirements and ensuring that every design decision has an appropriate level of trust.

One of the biggest mindset shifts during this lesson was learning to challenge every claim by asking:

"Why does this information belong inside a security token?"

If the answer cannot be justified, the claim probably should not exist.

# Key Takeaways

- JWT enables stateless authentication.
- JWT payloads are encoded, not encrypted.
- Sensitive information should never be stored in JWTs.
- Every claim should have a business justification.
- Trust the signature—not the client.
- Always validate signatures before trusting claims.
- Minimize the information contained within security tokens.

# Interview Questions

1. What problem does JWT solve?

2. Explain the three parts of a JWT.

3. Why is the JWT payload not considered secure for sensitive data?

4. What is the purpose of the JWT signature?

5. What trust assumptions does a server make when validating a JWT?

6. What are common JWT security risks?

7. What information should never be stored inside a JWT?

8. How would you review the claims contained in a JWT during a Product Security assessment?

# Security Engineer Questions

Whenever reviewing JWT usage, ask:

- What business problem does this token solve?
- Is every claim necessary?
- What happens if the token is stolen?
- Can any claims be removed?
- Are sensitive data or secrets being stored?
- Is the signature always verified?
- How long should this token remain valid?
- How are signing keys protected?

# Personal Reflection

## My Biggest Takeaway

Before this lesson, I thought JWTs were simply a way to keep users logged in.

Now I understand that a JWT is a trust mechanism.

The most valuable lesson was not learning the token format—it was learning to question every claim within the token.

As a Product Security Engineer, I should not ask:

"What data can we include?"

Instead, I should ask:

"What is the minimum information required to securely support the business?"

Technology should always support the business—not expose more information than necessary.

<img width="119" height="347" alt="JWT_authentication_flow" src="https://github.com/user-attachments/assets/5ef3c758-0c18-4f8f-8e4f-593fe99b8fcc" />
<img width="164" height="388" alt="JWT_securityperspective" src="https://github.com/user-attachments/assets/70b2b468-6996-4825-8372-735fb0d6b813" />


