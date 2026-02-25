# Phase 2 - Hardening Verification Report
## Overview
This document verifies the effectiveness of the security controls implemented in Phase 2 of the project, including:
- HTTP to HTTPS redirection
- TLS configuration hardening
- Server version disclosure mitigation
- Security headers implementation
- HSTS enforcement

All tests were performed using `curl` and `openssl` within a local Docker-based Nginx environment.

### 1. HTTP to HTTPS Redirection
Command

```bash
curl.exe -I http://localhost:8080
```
Expected Result:
```
HTTP/1.1 301 Moved Permanently
Location: https://localhost/
```

```bash
curl.exe -Ik https://localhost:8443
```
Expected Result:
```
HTTP/1.1 200 OK
```

### 2. TLS configuration hardening
Command

```bash
openssl s_client -connect localhost:8443
```
Expected Result:
```
SSL-Session:
    Protocol  : TLSv1.2
```
or
```
SSL-Session:
    Protocol  : TLSv1.3
```

Purpose:
```
- Connection uses HTTPS
- TLS 1.2 or TLS 1.3 negotiated
- No insecure protocol fallback
```

### 3. Security Headers Verification
Command

```bash
curl.exe -Ik https://localhost:8443
```
Expected Result
```
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
Referrer-Policy: no-referrer
Content-Security-Policy: default-src 'self';
Strict-Transport-Security: max-age=31536000; includeSubDomains
```
Purpose
```

```
