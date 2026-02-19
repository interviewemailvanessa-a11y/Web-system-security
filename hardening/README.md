# Container & Nginx Hardening

This directory contains the remdiation implementation for the security issues identified in Phase 1.

## Objectives

- Configure TLS securely
- Implement HTTP security headers
- Enable HSTS
- Apply least privilege principle to container runtime

## Structure

- nginx/default.conf -> Hardened Nginx configuration
- docker.yml -> Secure container configuration
- docs/verification.md - > Post-hardening validation results
