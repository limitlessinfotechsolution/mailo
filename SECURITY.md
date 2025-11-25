# Security Policy

## Supported Versions

We release patches for security vulnerabilities in the following versions:

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues.**

If you discover a security vulnerability, please send an email to:

**security@limitlessinfotech.com**

### What to Include

Please include the following information:

- Type of vulnerability
- Full paths of source file(s) related to the vulnerability
- Location of the affected source code (tag/branch/commit or direct URL)
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the vulnerability
- Any potential mitigations you've identified

### Response Timeline

- **Initial Response**: Within 48 hours
- **Status Update**: Within 7 days
- **Fix Timeline**: Depends on severity
  - Critical: 1-7 days
  - High: 7-30 days
  - Medium: 30-90 days
  - Low: Best effort

### Disclosure Policy

- Security issues will be disclosed after a fix is available
- We request that you do not publicly disclose the issue until we've had a chance to address it
- We will credit you in the security advisory (unless you prefer to remain anonymous)

## Security Best Practices

### For Administrators

1. **Keep MailO Updated**: Always use the latest version
2. **Use Strong Passwords**: Enforce strong password policies
3. **Enable 2FA**: Require two-factor authentication for all users
4. **Secure Environment Variables**: Never commit `.env` files
5. **Use HTTPS**: Always use SSL/TLS in production
6. **Regular Backups**: Implement automated backup procedures
7. **Monitor Logs**: Set up log monitoring and alerting
8. **Limit Access**: Use principle of least privilege
9. **Network Security**: Use firewalls and network segmentation
10. **Regular Audits**: Perform security audits regularly

### For Developers

1. **Dependency Updates**: Keep dependencies up to date
2. **Code Review**: All code changes should be reviewed
3. **Input Validation**: Always validate and sanitize user input
4. **Authentication**: Use JWT tokens with appropriate expiration
5. **Authorization**: Implement proper role-based access control
6. **Encryption**: Use bcrypt for passwords, encrypt sensitive data
7. **SQL Injection**: Use parameterized queries (MongoDB)
8. **XSS Prevention**: Sanitize HTML output
9. **CSRF Protection**: Implement CSRF tokens where needed
10. **Rate Limiting**: Implement rate limiting on sensitive endpoints

## Known Security Considerations

### Authentication
- JWT tokens expire after 7 days by default
- Passwords are hashed using bcrypt with 10 rounds
- 2FA uses TOTP (Time-based One-Time Password)

### Data Storage
- Email content stored in MinIO (S3-compatible)
- Metadata stored in MongoDB
- Sessions stored in Redis

### Network Security
- CORS enabled with configurable origins
- Helmet.js for HTTP security headers
- Rate limiting on authentication endpoints

## Security Updates

Security updates will be announced through:
- GitHub Security Advisories
- Release notes in CHANGELOG.md
- Email notifications to registered administrators

## Compliance

MailO is designed to help organizations comply with:
- GDPR (General Data Protection Regulation)
- HIPAA (when properly configured)
- SOC 2 (with appropriate controls)

**Note**: Compliance is a shared responsibility. Proper configuration and operational practices are required.

## Bug Bounty Program

We currently do not have a formal bug bounty program. However, we greatly appreciate security researchers who responsibly disclose vulnerabilities and will publicly acknowledge their contributions.

---

**Last Updated**: November 25, 2025  
**Maintained by**: Limitless Infotech Solution Pvt Ltd.

For general security questions: security@limitlessinfotech.com
