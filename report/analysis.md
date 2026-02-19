# Security Configuration Analysis - Nginx in Docker

## 1. Project Overview
The project demonstrates a basic security configuration analysis of an Nginx web server deployed inside a Docker container.
The objective is to identify common misconfigurations in HTTP response headers.

## 2. Environment Setup
- Host: Windows 10
- Docker Desktop
- Nginx official image
- Port mapping: 8080 -> 80

## 3. Scope of Analysis
The analysis focuses on HTTP security headers and configuration related risks, including:
- Server version disclosure
- Content Security Policy (CSP)
- HTTP Strict Transport Security (HSTS)

The Docker container is used as a deployment environment. The analysis targets web server configuration rather than container level security.

## 4. Assessment Methodology
The assessment was conducted by manually inspect HTTP response headers using browser developer tools and command-line utilities as curl.

No automated vulnerability scanning tools were used in this phase.
The focus was on configuration-based security controls at the web server level.

## 5. Key Findings Summary
1. Server Version Disclosure - Low to Medium
2. Missing Content Security Policy - Medium to High
3. Missing HSTS - Medium to High

## 6. Detailed Finding
### 6.1. Server version disclosure

**Observation:**
The HTTP response reveals the exact server version:
`Server: nginx/1.29.5`

**Risk Explanation:**
Exposing the exact server version allows potential attackers to identify known vulnerabilities associated with this specific version. This reduces the attackers reconnaissance effort and may increase the likelihood of targeted exploitation.

**Risk Level**: Low to Medium

**Recommendation**:
Disable or minimize server version disclosure by adjusting the server configuration (e.g., using `server_tokens off` in nginx)

### 6.2 Missing Content Security Policy (CSP)

**Observation:**
The HTTP response does not include a `Content-Security-Policy` header.

**Risk Explanation:**
Without the CSP header, the browser has no restrictions on which scripts, styles, or external resources may be loaded and executed. If an attacker successfully injects malicious JavaScript (e.g., via XSS), the browser will execute it without additional constraints.

**Impact:**
This increases the potential impact on cross-site scripting (XSS) attacks, including data theft, session hijacking, or unauthorized actions performed on behalf of user.

**Risk Impact:**Medium to High

**Restrictions:**
Implement a restrictive Content Security Policy. For example:
Content Security Policy: default-src 'self';
This configuration restricts all resource loading to the same origin, reducing the risk of executing malicious external scripts.

### 6.3 Missing HTTP Strict Transport Security (HSTS)

**Observation:**
The HTTP response does not include a `Strict-Transport-Security` header.
The application is currently accessible via HTTP without enforced HTTPS redirection.

**Risk Explanation:**
Without HSTS, users may initially connect over HTTP. This allows attackers to perform downgrade attacks or man-in-the-middle (MITM) attacks, potentially intercepting or modifying sensitive data.

**Impact:**
Sensitive information such as authentication cookies or session tokens could be exposed if transmitted over unsecured HTTP connections.

**Risk Level:** Medium to High

**Recommendation:**
Enable HTTPS and configure HSTS to enforce secure communication. For example:
Strict-Transport-Security: max-age=31536000; includeSubDomains

In nginx, this can be implemented using:
add_header Strict-Transort-Security "max-age=31536000; includeSubDomains" always;
This ensures that browsers only communicate over HTTPS, preventing protocol downgrade and man-in-the-middle attacks.
## 7. Risk Summary
The assessment reveals that while system functions correctly, several security best practices are not implemented.
The absense of browser-enforced security controls significantly increases the potential impact of client-side attacks such as XSS and session hijacking.

## 8. Future Improvements
- Implement HTTPS with valid TLS certificate
- Configure strict CSP rules
- Enable HSTS with preload consideration
- Expand analysis to container hardening






