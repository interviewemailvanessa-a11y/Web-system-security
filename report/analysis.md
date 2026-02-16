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

