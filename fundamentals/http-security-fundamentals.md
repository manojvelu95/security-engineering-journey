# HTTP Security Fundamentals

## Why HTTP Exists

HTTP (Hypertext Transfer Protocol) was created to provide a standardized way for clients (such as web browsers or mobile applications) and servers to communicate over the web.

Once DNS resolves a domain name into an IP address, HTTP is responsible for exchanging requests and responses between the client and the server.

Think of HTTP as the language used by web applications to communicate.

---

## How HTTP Works

HTTP follows a **request-response model**.

1. The client sends an HTTP request.
2. The server processes the request.
3. The server returns an HTTP response.

Example:

```text
Browser
    │
    ▼
HTTP Request
    │
    ▼
Web Server
    │
    ▼
HTTP Response
    │
    ▼
Browser renders the response
```

An HTTP request typically contains:

* HTTP Method
* URL
* Headers
* Parameters
* Cookies
* Request Body (optional)

An HTTP response typically contains:

* Status Code
* Headers
* Response Body

---

## Common HTTP Methods

### GET

Retrieves data from the server.

Example:

```http
GET /profile
```

---

### POST

Creates a resource or submits data.

Example:

```http
POST /login
```

---

### PUT

Updates an existing resource.

Example:

```http
PUT /user/123
```

---

### DELETE

Deletes a resource.

Example:

```http
DELETE /user/123
```

---

## Common HTTP Status Codes

| Status Code               | Meaning                           |
| ------------------------- | --------------------------------- |
| 200 OK                    | Request completed successfully    |
| 201 Created               | Resource created successfully     |
| 301 Moved Permanently     | Permanent redirect                |
| 302 Found                 | Temporary redirect                |
| 401 Unauthorized          | Authentication required or failed |
| 403 Forbidden             | Authenticated but not authorized  |
| 404 Not Found             | Resource does not exist           |
| 500 Internal Server Error | Server-side error                 |

---

## Trust Assumptions

HTTP itself does not provide security.

Instead, web applications often trust information sent by the client, such as:

* User ID
* Session Cookie
* JWT
* HTTP Headers
* Roles
* URL Parameters
* Form Inputs

Security vulnerabilities occur when applications trust client-controlled data without performing proper validation or authorization checks.

---

## Why Attackers Target HTTP

Every interaction with a web application is performed using HTTP requests.

If an attacker can modify those requests, they can test whether the application properly validates and authorizes user actions.

Examples include:

* Parameter tampering
* Header manipulation
* Cookie manipulation
* JWT manipulation
* HTTP method tampering
* Request body modification

Example:

```http
GET /invoice?id=123
```

An attacker may modify it to:

```http
GET /invoice?id=124
```

If the application returns another user's invoice, it indicates a broken authorization check (commonly known as an IDOR or Broken Access Control vulnerability).

---

## Defensive Controls

Modern web applications should implement:

* Strong Authentication
* Server-side Authorization
* Ownership Verification
* Input Validation
* Secure Session Management
* Rate Limiting
* Logging and Monitoring

Security should never rely solely on data received from the client.

---

## Security Engineer Perspective

One of the most valuable questions a security engineer can ask is:

> **"What is the server trusting?"**

Examples include:

* Is the server trusting the User ID?
* Is it trusting the JWT?
* Is it trusting the session cookie?
* Is it trusting a client-supplied role?
* Is it trusting a URL parameter?

Most web vulnerabilities exist because applications trust client-controlled data more than they should.

---

## Key Takeaways

* HTTP is the communication protocol used between clients and servers.
* HTTP follows a request-response model.
* HTTP requests contain methods, headers, parameters, cookies, and optional request bodies.
* Applications often trust client-supplied data.
* Attackers manipulate HTTP requests to test those trust assumptions.
* Security engineers should continuously ask: **"What is the server trusting?"**
* Proper authentication, authorization, validation, and ownership checks are essential to building secure web applications.

---

## Security Engineer Questions

Whenever analyzing an HTTP request, ask:

* What is the server trusting?
* Should it trust this value?
* Can an attacker modify it?
* Does the server validate it?
* Is authorization enforced server-side?
* What logs or telemetry would help detect abuse?

<img width="195" height="191" alt="HTTP_Functional_view" src="https://github.com/user-attachments/assets/25677b3a-df41-434b-bf50-044df699b865" />
<img width="170" height="355" alt="HTTP_Security_view" src="https://github.com/user-attachments/assets/0d14dd0b-5e40-48bf-8bfc-18c7bd47b75c" />



