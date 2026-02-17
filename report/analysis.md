# 1. Server version disclosure

**Observation:**
The HTTP response reveals the exact server version:
`Server: nginx/1.29.5`

**Risk Explanaion:**
Exposing the exact server version allows potential attackers to identify known vulnerabilities associated with this specific version. This reduces the attackers reconnaissance effort and may increase the likelihood of targeted exploitation.

**Risk Version**: Low to Medium

**Recommandation**:
Disable or minimize server version disclosure by adjusting the server configuration (e.g., using `server_tokens off` in nginx)

# 2. Missing Content Security Policy (CSP)

**Observation:**
The HTTP response does not include a `Content-Security-Policy` header.

**Risk observation:**
Without the CSP header, the browser has no restrictions on which scripts, styles, or external resources may be loaded and executed. If an attacker successfully injects malicious Javascript (e.g., via XSS), the browser will execute it without additional constraints.

**Impact:**
This increase the potential impact on cross-site scripting (XSS) attacks, including data theft, session hijacking, or unauthorized actions performed on behalf of user.

**Risk Impact:**Medium to High

**Restrictions:**
Implement a restrict Content Security Policy. For example:
Content Security Policy: default-src 'self';
This configuration restricts all resource loading to the same origin, reducing the risk of executing malicious external scripts.

# 3. Missing HTTP Strict Transport Security (HSTP)

**Observation:**
The HTTP response does not include a `Strict-Transport-Security` header.
The application is currently accessible via HTTP without enforced HTTPs redirection.

**Risk Explanation:**
Without HSTS, users may initially connect over HTTP. This alows attackers to perform downgrade attacks or man-in-the-middle (MITM) attacks, potentially intercepting or modifying sensitive data.

**Impact:**
Sensitive information such as authentication cookies or session tokens could be exposed if transmitted over unsecured HTTP connections.

**Risk Level:** Medium to High

**Recommendation:**
Enable HTTPS and configure HSTS to enforce secure communication. For example:
Strict-Transport-Security: max-age=31536000; includeSubDomains

In nginx, this can be implemented using:
add_header Strict-Transort-Security "max-age=3156000; includeSubDomains" always;
This ensures that browsers only communicate over HTTPS, preventing protocol downgrade and man-in-the-middle attacks.

