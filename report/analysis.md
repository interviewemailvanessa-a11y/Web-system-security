# 1. Server version disclosure

**Observation:**
The HTTP response reveals the exact server version:
`Server: nginx/1.29.5`

**Risk Explanaion:**
Exposing the exact server version allows potential attackers to identify known vulnerabilities associated with this specific version. This reduces the attackers reconnaissance effort and may increase the likelihood of targeted exploitation.

**Risk Version**: Low to Medium

**Recommandation**:
Disable or minimize server version disclosure by adjusting the server configuration (e.g., using `server_tokens off` in nginx)

