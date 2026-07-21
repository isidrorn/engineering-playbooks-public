# Security Review

## Purpose

This playbook guides a senior engineer through reviewing the security posture of a system, feature, or change — covering threat modeling, authentication and authorization, data handling, infrastructure, and operational and compliance concerns. It applies to new features before ship, and to periodic reviews of existing systems.

---

## Level 1 Checklist

### 🔍 Threat Modeling

- [ ] Identify trust boundaries and where data crosses them (client/server, service/service, internal/external)
- [ ] Enumerate entry points: APIs, UI forms, file uploads, webhooks, message queues, admin interfaces
- [ ] Identify the assets that matter: credentials, PII, payment data, business-critical data, availability
- [ ] Consider realistic threat actors (external attacker, malicious insider, compromised dependency, curious customer)
- [ ] Map the attack surface added or changed by this feature specifically, not just the system as a whole

### 🔍 Authentication & Authorization

- [ ] Confirm the authentication mechanism and where trust is anchored (password, OAuth/OIDC, mTLS, API key)
- [ ] Check session management: token expiry, refresh behavior, invalidation on logout/password change
- [ ] Check MFA is enforced where risk warrants it, and cannot be silently bypassed
- [ ] Verify least privilege — each role/service has only the access it needs, nothing broader
- [ ] Check role-based or attribute-based access control is enforced server-side, not just hidden in the UI
- [ ] Look for privilege escalation paths (IDOR, missing ownership checks, trusting client-supplied role/ID fields)
- [ ] Verify service-to-service calls are authenticated, not just network-restricted

### 🔍 Input & Output Handling

- [ ] Check for injection risks: SQL, NoSQL, command, LDAP, template injection
- [ ] Verify input validation happens server-side, with allow-lists where feasible
- [ ] Verify output encoding is applied per context to prevent XSS (HTML, JS, URL, attribute contexts differ)
- [ ] Check file upload restrictions: type, size, storage location, and that uploads aren't served with executable permissions
- [ ] Check deserialization of untrusted data is safe (no arbitrary object/class instantiation)
- [ ] Check for SSRF risk where the server fetches a URL or resource supplied by a user

### 🔍 Data Protection

- [ ] Confirm encryption in transit (TLS everywhere, no fallback to plaintext) and at rest for sensitive data
- [ ] Classify PII and sensitive data handled by this system and confirm handling matches its classification
- [ ] Check data retention policy is defined and enforced — is old data actually purged, not just eligible for it
- [ ] Verify no secrets are hardcoded in source, config files, or container images
- [ ] Confirm secrets are stored in a managed secrets store with a defined rotation policy
- [ ] Check key management: who can access encryption keys, and how key rotation is handled

### ⚙️ Infrastructure & Dependencies

- [ ] Confirm dependency vulnerability scanning is enabled and findings are actually triaged, not just collected
- [ ] Confirm container images are scanned and built from a minimal, patched base image
- [ ] Check network segmentation: is this service reachable from where it shouldn't be
- [ ] Verify TLS configuration (supported versions/ciphers, certificate validity and expiry monitoring)
- [ ] Check CORS policy is scoped to actual trusted origins, not a wildcard left over from development
- [ ] Verify security headers are set (CSP, HSTS, X-Content-Type-Options, X-Frame-Options)

### ✅ Operational Security

- [ ] Confirm security-relevant events are logged (auth failures, permission denials, admin actions)
- [ ] Verify sensitive data (passwords, tokens, full card numbers) is never written to logs
- [ ] Confirm audit trails exist for access to sensitive data and are tamper-resistant
- [ ] Verify this system is covered by the incident response process, with clear ownership if something goes wrong
- [ ] Check penetration testing or security assessment cadence covers this system, and findings are tracked to closure
- [ ] Confirm a security patch SLA exists and is being met for known vulnerabilities

### 📝 Compliance

- [ ] Identify which regulatory frameworks apply (GDPR, SOC 2, HIPAA, PCI-DSS, or industry-specific rules)
- [ ] Check data residency requirements are met for where data is stored and processed
- [ ] Confirm the breach notification process is documented and this system's owners know their role in it
- [ ] Verify any required data processing agreements or third-party assessments are current

---

## Notes

This checklist is a review aid, not a substitute for a formal threat model or a professional penetration test on systems handling sensitive data at scale.
