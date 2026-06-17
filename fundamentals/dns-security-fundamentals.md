# DNS Security Fundamentals

## Why DNS Exists

DNS (Domain Name System) was created to solve the problem of remembering IP addresses by translating human-friendly domain names into machine-friendly IP addresses.

For example:

```text
google.com
      ↓
142.250.x.x
```

Without DNS, users would need to remember the IP address of every website they visit.

DNS acts as the internet's phonebook, allowing users to access services using memorable domain names rather than numerical IP addresses.

---

## How DNS Works

When a user enters a URL into a browser, the browser must determine the IP address associated with the domain.

A simplified DNS resolution process is:

```text
User Browser
      │
      ▼
Local DNS Cache
      │
      ▼
Recursive Resolver
      │
      ▼
Root DNS Server
      │
      ▼
TLD Server (.com)
      │
      ▼
Authoritative DNS Server
      │
      ▼
google.com → 142.250.x.x
      │
      ▼
Browser connects to Google
```

### Components

#### Root DNS Server

The Root DNS Server knows where to find Top-Level Domain (TLD) servers such as:

* .com
* .org
* .net

It does not know the final IP address of the domain.

#### TLD Server

The TLD Server knows which authoritative DNS server is responsible for a particular domain.

For example:

```text
google.com
```

#### Authoritative DNS Server

The Authoritative DNS Server is the source of truth for the domain and returns the actual DNS record.

Example:

```text
google.com
      ↓
142.250.x.x
```

---

## Trust Assumptions

DNS is one of the internet's foundational trust layers.

DNS relies on the assumption that the DNS response returned is authentic and has not been tampered with.

When a browser asks:

```text
What is the IP address of google.com?
```

it trusts that the answer received is legitimate.

Security engineers should view DNS as a trust system rather than simply a name resolution service.

---

## Why Attackers Target DNS

DNS is attractive to attackers because it is a highly trusted component of internet communications.

If attackers can manipulate DNS responses, they may be able to:

* Redirect users to malicious websites
* Steal credentials
* Distribute malware
* Intercept traffic
* Bypass security controls

### DNS Poisoning

An attacker injects malicious DNS records into a resolver cache.

Result:

```text
bank.com
      ↓
Attacker-controlled server
```

instead of the legitimate destination.

### DNS Hijacking

An attacker gains control of DNS settings or DNS records and redirects users to malicious infrastructure.

### DNS Tunneling

Attackers abuse DNS traffic to:

* Exfiltrate data
* Communicate with malware
* Bypass network restrictions

---

## Defensive Controls

### DNSSEC

DNSSEC (Domain Name System Security Extensions) uses cryptographic signatures to verify the integrity and authenticity of DNS responses.

It helps prevent tampering with DNS records.

### DNS over HTTPS (DoH)

Encrypts DNS requests using HTTPS.

Benefits:

* Improved privacy
* Reduced visibility of DNS queries on the network

### DNS over TLS (DoT)

Encrypts DNS traffic using TLS to help protect DNS communications from interception.

### DNS Filtering

Organizations can block known malicious domains using DNS filtering solutions.

### DNS Monitoring

Security teams monitor DNS activity to identify:

* Phishing attempts
* Malware communications
* Command-and-control activity
* Suspicious domains

---

## Security Engineer Perspective

A common misconception is that DNS is simply a system that converts domain names into IP addresses.

From a security perspective, DNS should be viewed as a foundational trust layer of the internet.

Security engineers should ask:

* Can DNS responses be manipulated?
* Are DNS records protected against tampering?
* Is DNSSEC implemented?
* Are suspicious domains being queried?
* Can DNS be used for malware communication or data exfiltration?

Understanding DNS as a trust layer helps security professionals identify risks, detect threats, and design more resilient systems.

---

## Key Takeaways

* DNS translates domain names into IP addresses.
* DNS is a foundational trust layer of the internet.
* DNS relies on trusted responses to function correctly.
* Attackers target DNS because compromising trust can have widespread impact.
* DNSSEC helps verify the authenticity and integrity of DNS responses.
* DNS telemetry is valuable for threat detection and incident response.
* Security engineers should analyze DNS through the lens of trust, threats, and defensive controls.
<img width="778" height="447" alt="trust_assumptions" src="https://github.com/user-attachments/assets/7c97b251-2fe9-4df8-a6b7-961f78d264e5" />
<img width="282" height="469" alt="DNS_Resolution_Flow" src="https://github.com/user-attachments/assets/c89508a4-ab2b-4778-b348-62f01230c08a" />


