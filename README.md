# CTI-Lab-Keycloak-IAM-Integration
Lab 3 for Cyber Threat Intelligence (CTI) — Configuration of Keycloak as a centralized Identity and Access Management (IAM) solution with SSO, OAuth 2.0, and OpenID Connect integration into an existing enterprise environment

# CTI Lab 3 — Keycloak IAM Integration Guide

**Student:** Uliya Fatima | **Roll No:** 232098  
**Course:** Cyber Threat Intelligence (CTI) | **Lab:** 03  
**Date:** March 6, 2026

---

## Overview

This lab covers the configuration of **Keycloak** as a centralized Identity and Access Management (IAM) solution and its integration into an existing enterprise environment. Keycloak provides Single Sign-On (SSO), OAuth 2.0, and OpenID Connect capabilities for centralized authentication and authorization across multiple applications.

---

## Prerequisites

| Component | Requirement |
|-----------|-------------|
| Java Runtime | Java 17 or later (OpenJDK recommended) |
| Network Access | Ports 8080 (HTTP) and 8443 (HTTPS) open |
| Database | PostgreSQL, MySQL, or MariaDB (H2 for dev) |
| DNS | Valid hostname or FQDN resolvable in network |
| Access | Root or sudo privileges on target server |

---

## Part 1 — Keycloak Installation & Initial Setup

### Steps

**1. Access the Administration Console**
- Navigate to the Keycloak admin console URL
- Log in with administrator credentials

**2. Configure Realm Settings**
- Create or configure a realm as the top-level IAM container
- The realm holds all clients, users, and roles

**3. Client Registration & Configuration**
- Register the target application as a client
- Configure authentication protocol and redirect URIs

---

## Part 2 — Integration Configuration

### 4.1 Identity Provider Configuration
Configure external identity providers (Active Directory, LDAP, or social providers) to enable federated authentication.

### 4.2 Authentication Flow Setup
Define custom authentication flows to match organizational security policies — controlling the sequence of steps users must complete to authenticate.

### 4.3 User Federation & LDAP Integration
Synchronize users from external directories (Active Directory / LDAP) to avoid duplicate account management.

### 4.4 Role & Group Management
Define realm-level roles, client-specific roles, and composite roles for granular access control.

---

## Part 3 — Advanced Configuration

### Token Configuration
Configure access token, refresh token, and session timeout values:
- Recommended: **Access Token** — 5–15 minutes
- Refresh tokens used to minimize impact of token compromise

### Protocol Mapper Configuration
Configure protocol mappers to transform user attributes and role information into token claims required by integrated applications.

---

## Part 4 — Validation & Testing

### SSO Login Flow
- Test end-to-end authentication via the configured client
- Inspect token response to confirm all expected claims are present

### Token Introspection
```bash
# Example token introspection request
curl -X POST https://<keycloak-host>/realms/<realm>/protocol/openid-connect/token/introspect \
  -d "token=<access_token>" \
  -u "<client_id>:<client_secret>"
```

### User Authentication Test
- Perform end-to-end login with test credentials
- Verify session establishment and correct authorization claims

---

## Part 5 — Event Monitoring & Audit Logging

### Event Log Configuration
- Enable Keycloak event listeners to capture:
  - Login events
  - Failed authentication attempts
  - Token exchanges
  - Administrative changes
- Forward events to external SIEM (e.g., Elastic Stack) via custom event listeners

### Admin Audit Trail
- Review admin audit logs for realm changes, user creation, and role assignments

---

## Security Recommendations

| # | Recommendation |
|---|---------------|
| 1 | **Enable TLS/HTTPS** — Use a reverse proxy (Nginx/Apache) with valid TLS certificate; never expose over plain HTTP in production |
| 2 | **Restrict Admin Console** — Limit access to internal IPs; disable public admin console exposure |
| 3 | **Brute Force Protection** — Enable built-in detection to lock accounts after repeated failures |
| 4 | **Short Token Lifetimes** — Access tokens: 5–15 min; use refresh tokens |
| 5 | **Enable Audit Logging** — Forward all events to central SIEM |
| 6 | **Regular Updates** — Monitor Keycloak security advisories and apply patches promptly |

---

## Conclusion

This lab successfully demonstrated:
- Installation and configuration of Keycloak as a centralized IAM platform
- Integration with existing enterprise environment using OAuth 2.0 / OpenID Connect / SAML 2.0
- User federation, role management, and authentication flow customization
- Event monitoring and audit logging setup
- Security hardening best practices

---

## References

- [Keycloak Official Documentation](https://www.keycloak.org/documentation)
- [Keycloak Security Advisories](https://www.keycloak.org/security)

---

## Tools & Technologies

`Keycloak` `IAM` `SSO` `OAuth2` `OpenID-Connect` `SAML` `LDAP` `Active-Directory` `Identity-Management` `Access-Control` `CTI` `Cybersecurity` `Java`
