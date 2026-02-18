# Security Configuration Analysis - Nginx in Docker

## Project Overview
The project demonstrates a basic security configuration analysis of an Nginx web server deployed inside a Docker container.
The objective is to identify common misconfigurations in HTTP response headers.

## Environment Setup
- Host: Windows 10
- Docker Desktop
- Nginx official image
- Port mapping: 8080 -> 80

## Scope of Analysis
The analysis focuses on HTTP security headers and configuration related risks, including:
- Server version disclosure
- Content Security Policy (CSP)
- HTTP Strict Transport Security (HSTS)

The Docker container is used as a deployment environment. The analysis targets web server configuration rather than container level security.
## Key Findings
1. Server Version Disclosure - Low to Medium Risk
2. Missing Content Security Policy - Medium to High Risk
3. Missing HSTS - Medium to High Risk
## Risk Summary
The assessment reveals that while system functions correctly, several security best practices are not implemented.
Missing browser enforced security mechanisms increase the potential impact of client side attack.

## Future Improvements
- Implement HTTPS with valid TLS certificate
- Configure strict CSP rules
- Enable HSTS with preload consideration
- Expand analysis to container hardening


