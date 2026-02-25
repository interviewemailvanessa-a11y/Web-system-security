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
Server: nginx/1.29.5
Date: Tue, 24 Feb 2026 04:55:18 GMT
Content-Type: text/html
Content-Length: 169
Connection: keep-alive
Location: https://localhost/
```

```bash
curl.exe -Ik https://localhost:8443
```
Expected Result:
```
Server: nginx
Date: Tue, 24 Feb 2026 11:02:45 GMT
Content-Type: text/html
Content-Length: 615
Last-Modified: Wed, 04 Feb 2026 15:12:20 GMT
Connection: keep-alive
ETag: "698361d4-267"
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
Referrer-Policy: no-referrer
Content-Security-Policy: default-src 'self';
Strict-Transport-Security: max-age=31536000; includeSubDomains
Accept-Ranges: bytes
```

### 2. TLS configuration hardening
Command

```bash
curl.exe -I http://localhost:8080
curl.exe -Ik https://localhost:8443
```
Expected Result:
```
- Connection uses HTTPS
- TLS 1.2 or TLS 1.3 negotiated
- No insecure protocol fallback


### 3. Security Headers Verification
Command

```bash
curl.exe -I http://localhost:8080
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
