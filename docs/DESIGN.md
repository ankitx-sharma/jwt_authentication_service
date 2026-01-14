## Identity Provider & Authorization Server (IdP + AS)

#### Document Type
Solution Design / Functional Architecture Document

#### Audience
Backend engineers, reviewers, system architects

##

### Purpose of the System

The purpose of this project is to design and implement a **self-hosted Identity Provider (IdP)** combined with an **Authorization Server (AS)** that is responsible for:

#### Authenticating users

- Managing user credentials securely
- Issuing cryptographically verifiable access tokens (JWT)
- Managing long-lived user sessions using refresh tokens
- Defining and enforcing trust for client applications requesting tokens

This system is not a business application and does not expose protected domain APIs.
Its sole responsibility is identity and token issuance.

##

### Business Problem Statement

Modern applications require a centralized mechanism to:

- Avoid storing user credentials in every application
- Support stateless authentication for scalable systems
- Enable secure session continuation without repeated logins
- Control which applications are allowed to obtain access tokens

Without a dedicated Identity Provider and Authorization Server, applications tend to:

- Duplicate authentication logic
- Handle passwords insecurely
- Rely on server-side sessions that do not scale well
- Lack clear trust boundaries between systems

This project addresses those concerns by isolating identity and token issuance into a dedicated service.

##

### Scope Definition
In Scope

- User registration and authentication
- Secure password storage and verification
- JWT access token issuance
- Refresh token lifecycle management (issue, rotate, revoke)
- Client registration and trust validation
- Cryptographic key management for token signing
- Public key exposure via JWKS endpoint

Out of Scope
- Business/domain APIs (no Resource Server)
- OAuth authorization code flows and redirects
- Consent screens and SSO user experience
- Multi-factor authentication (MFA)
- User profile management UI
- Social login or identity federation

##

### System Classification

This system functions as:

- **Identity Provider (IdP)** — authenticates users and manages identity data
- **Authorization Server (AS)** — issues access and refresh tokens to trusted clients

The system does not act as a Resource Server.

##

### High-Level Architecture
Logical Responsibilities

Responsibility | Description
--- | ---
Identity Management | User credentials, password hashing, account status
Token Issuance | JWT creation, signing, expiration handling
Session Continuity | Refresh token persistence and rotation
Client Trust | Determines which applications may request tokens
Key Distribution | Publishes public keys for token verification
