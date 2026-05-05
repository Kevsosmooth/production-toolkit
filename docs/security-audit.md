# Security Audit Checklist

A run-it-yourself audit guide for any project before launch and quarterly after. Built to pair with the Security and App Hardening section in the main README.

This doc is project-agnostic. Drop your project's URL, repo path, and stack into the placeholders and follow the checklist top to bottom. Each step has the exact command to run and what counts as a pass.

---

## How to Use This Doc

1. Fill in the project info block below
2. Work through the checklist in order -- each section depends on the one before it
3. Tick the boxes as you go. Anything you can't tick is a finding to fix or document
4. Sign off at the bottom with the date and result

Estimated time: 30 minutes for a quick audit, 2-3 hours for a thorough one.

---

## Project Info

| Field | Value |
|-------|-------|
| Project name | `<PROJECT_NAME>` |
| Production URL | `<https://example.com>` |
| Staging URL | `<https://staging.example.com>` |
| Repo path | `<owner/repo>` |
| Stack | `<e.g. Next.js 16 + Wix Headless + Vercel + Sentry>` |
| Audit date | `<YYYY-MM-DD>` |
| Auditor | `<name>` |

---

## Phase 1: Quick Triage (5 Minutes)

Catch the obvious wins before doing anything deeper. If any of these fail, fix them first.

### One-Click Web Audits

- [ ] **Security Headers** -- paste prod URL into [securityheaders.com](https://securityheaders.com). Pass = grade A or B.
- [ ] **Mozilla Observatory** -- paste prod URL into [observatory.mozilla.org](https://observatory.mozilla.org). Pass = score 70+.
- [ ] **TLS / SSL** -- run `testssl.sh https://<DOMAIN>` or use [ssllabs.com/ssltest](https://www.ssllabs.com/ssltest/). Pass = grade A, no protocol below TLS 1.2.
- [ ] **Email auth** -- run [hardenize.com](https://www.hardenize.com) on the apex domain. Pass = SPF, DKIM, DMARC all green.

### Visible Misconfig

- [ ] No `.env`, `.git`, `.DS_Store`, or `/admin` directory accessible at the public URL
- [ ] No source maps exposed in production (`curl -I https://<DOMAIN>/_next/static/<HASH>.js.map` returns 404)
- [ ] No verbose error pages leaking stack traces (visit `/<random-404-path>` and check)
- [ ] Robots.txt does not list private admin paths (don't tell attackers where to look)

---

## Phase 2: Static Analysis (Code Review)

Read the code itself, find bugs before they ship.

### Repo Hygiene

- [ ] `.env*` files are in `.gitignore` and have never been committed
- [ ] No hardcoded API keys, tokens, passwords, or DB connection strings in source (run secret scan below)
- [ ] No commented-out blocks containing credentials
- [ ] `package.json` does not depend on packages with `<1.0.0` from unverified authors

### Secret Scanning

Run all three -- they catch different things.

```bash
# TruffleHog -- scans full git history
docker run --rm -v "$PWD:/repo" trufflesecurity/trufflehog:latest filesystem /repo

# Gitleaks -- fast Go scanner, also scans history
docker run --rm -v "$PWD:/repo" zricethezav/gitleaks:latest detect --source /repo

# GitHub native secret scanning -- enable in repo settings if not already on
gh api repos/<OWNER>/<REPO>/secret-scanning/alerts
```

- [ ] TruffleHog: zero verified secrets
- [ ] Gitleaks: zero leaks
- [ ] GitHub secret scanning: enabled, zero open alerts

### Code Pattern Scanning (SAST)

```bash
# Semgrep -- run all default + framework rules
docker run --rm -v "$PWD:/src" returntocorp/semgrep semgrep --config=auto /src

# Or with the dedicated Next.js / React / TS rulesets
docker run --rm -v "$PWD:/src" returntocorp/semgrep \
  semgrep --config=p/nextjs --config=p/react --config=p/typescript /src
```

- [ ] Zero `ERROR` severity findings
- [ ] All `WARNING` findings reviewed -- documented or fixed
- [ ] No `dangerouslySetInnerHTML` without DOMPurify or equivalent sanitizer
- [ ] No `eval()`, `new Function()`, or `document.write()`
- [ ] No `target="_blank"` without `rel="noopener noreferrer"`

### CodeQL (Public Repos)

- [ ] CodeQL workflow enabled in `.github/workflows/codeql.yml`
- [ ] Last scan completed within 7 days
- [ ] Zero open critical or high findings

---

## Phase 3: Dependency and Supply Chain

Your `node_modules` is the attack surface nobody thinks about.

```bash
# OSV-Scanner -- Google's CLI, no account needed
osv-scanner --lockfile=package-lock.json

# npm built-in audit
npm audit --audit-level=high

# Socket.dev -- AI-driven, much better than npm audit
npx @socketsecurity/cli scan create

# Dependabot -- enable in repo settings if not already
gh api repos/<OWNER>/<REPO>/vulnerability-alerts
```

- [ ] OSV-Scanner: zero high/critical CVEs
- [ ] `npm audit` clean at high severity
- [ ] Socket.dev: no malicious packages, no install-script red flags
- [ ] Dependabot enabled with security updates on
- [ ] All deps updated within last 90 days (`npm outdated` shows nothing red)

---

## Phase 4: Run-the-Site Scanners (DAST)

Hit the running staging site like an attacker. **Do not point these at production without a maintenance window.**

### OWASP ZAP Baseline (5-10 min)

```bash
docker run --rm -v "$PWD:/zap/wrk:rw" zaproxy/zap-stable \
  zap-baseline.py -t https://<STAGING_URL> -r zap-report.html
```

- [ ] Zero High-risk findings
- [ ] All Medium-risk findings reviewed
- [ ] Report saved to `audit-reports/<DATE>-zap.html`

### Nuclei (template-based, very fast)

```bash
docker run --rm projectdiscovery/nuclei:latest \
  -u https://<STAGING_URL> -severity high,critical -o nuclei-report.txt
```

- [ ] Zero critical-severity findings
- [ ] Zero exposed admin panels, default creds, or known CVE matches
- [ ] Report saved to `audit-reports/<DATE>-nuclei.txt`

### Manual Probing (Burp Suite or Caido)

- [ ] Each authenticated route checked for IDOR (change ID in URL/body, see if you get someone else's data)
- [ ] Each form tested for stored XSS (`<svg onload=alert(1)>` in every text field)
- [ ] Auth flow tested for session fixation (does the session ID change after login?)
- [ ] Password reset tokens are single-use and time-bounded (request twice, only first works)
- [ ] No open redirects (`/redirect?url=https://evil.example` should reject external domains)

---

## Phase 5: Authentication and Authorization

The OWASP Top 10 list lives or dies here. Walk through it manually.

### Auth Flow

- [ ] Passwords hashed with bcrypt/argon2/scrypt (never SHA1, MD5, or plaintext)
- [ ] Session tokens stored in httponly cookies, never localStorage
- [ ] Cookies have `Secure`, `HttpOnly`, `SameSite=Lax` or stricter
- [ ] CSRF protection enabled on all state-changing routes (POST/PUT/DELETE)
- [ ] Rate limiting on `/login`, `/signup`, `/forgot-password`, `/reset` (max 5 attempts per minute per IP)
- [ ] 2FA available, ideally TOTP not just SMS
- [ ] Account lockout or exponential backoff after failed attempts
- [ ] Logout invalidates the session server-side, not just client-side

### Authorization (IDOR Hunt)

- [ ] Every API route enforces `userId === resource.ownerId` server-side
- [ ] Admin routes check `user.role === 'admin'` server-side, not just hide UI
- [ ] No "object reference" routes like `/api/user/<ID>` that trust the ID without permission check
- [ ] Bulk endpoints enforce per-item permissions (not just "is logged in")

### Token Hygiene

- [ ] Password reset tokens: single-use, 1-hour TTL, server-validated before any state mutation
- [ ] Email verify tokens: same rules
- [ ] Magic links: same rules
- [ ] JWT tokens (if used): proper expiry, signature verified, no `alg: none` accepted

---

## Phase 6: Input and Output Safety

### Input Validation (At the Boundary)

- [ ] All user-supplied strings validated/sanitized at the route handler, not deep in business logic
- [ ] File uploads: type allowlist (not denylist), size limit, virus scan if accepting executables
- [ ] User-supplied URLs (redirect, fetch, image) are allowlisted to known hosts
- [ ] SQL queries use parameterized statements / ORM, never string concatenation
- [ ] NoSQL queries reject operator objects from user input (`{$ne: ""}` injection)

### Output Encoding

- [ ] All user content rendered with framework's default escaping (React, Next.js auto-escape)
- [ ] `dangerouslySetInnerHTML` only used with sanitized HTML (DOMPurify)
- [ ] No user input concatenated into HTML, JS, or shell commands
- [ ] Server-side rendering does not interpolate user input into `<script>` tags

---

## Phase 7: Logging, Monitoring, and Privacy

### Don't Log Secrets

- [ ] No passwords, tokens, API keys, session cookies, or recovery codes in logs
- [ ] No full credit card numbers, SSNs, or PII in logs
- [ ] No request bodies logged on auth/payment/account routes
- [ ] Log redaction rules tested (grep logs for `password`, `token`, `secret` -- should find nothing)

### Monitoring Active

- [ ] Sentry (or equivalent) capturing errors in production
- [ ] Sentry source maps uploaded but not exposed publicly
- [ ] Sentry PII scrubbing enabled
- [ ] Alerts configured for spike in 4xx/5xx responses

### Privacy

- [ ] Privacy policy linked in footer
- [ ] Cookie consent banner if EU traffic possible
- [ ] User data deletion endpoint works (test with a real account)
- [ ] No third-party scripts loading without disclosure

---

## Phase 8: Runtime Protection (Edge Defense)

Stop attacks before they reach your code.

### WAF / Bot Protection

- [ ] **Vercel Firewall** (if Vercel hosted) -- OWASP managed ruleset enabled
- [ ] **Cloudflare WAF** (if proxied) -- Bot Fight Mode + Managed Rules on
- [ ] **Arcjet** (if Next.js) -- rate limiting + bot detection wired on every API route, not just public forms

### Headers (Confirm in Browser DevTools)

- [ ] `Content-Security-Policy` set, no `unsafe-inline` or `unsafe-eval` unless justified
- [ ] `Strict-Transport-Security: max-age=31536000; includeSubDomains; preload`
- [ ] `X-Content-Type-Options: nosniff`
- [ ] `X-Frame-Options: DENY` or `frame-ancestors 'none'` in CSP
- [ ] `Referrer-Policy: strict-origin-when-cross-origin`
- [ ] `Permissions-Policy` restricts unused features (camera, geolocation, etc.)

---

## Phase 9: Periodic Deep Audits (Quarterly)

The above is monthly-friendly. Add these once a quarter or before any major launch.

### AI-Powered Pentest

```bash
# Vulnhuntr -- LLM-driven SAST that finds multi-step bugs
docker run --rm -v "$PWD:/repo" protectai/vulnhuntr:latest -r /repo

# PentestGPT -- guided pentest assistant (interactive)
# See: https://github.com/GreyDGL/PentestGPT
```

- [ ] Vulnhuntr findings reviewed
- [ ] Top 5 manual probes from PentestGPT walkthrough completed

### Threat Model Review

- [ ] Walk the OWASP Top 10 against the current architecture, document any new gaps
- [ ] Re-check who has prod access (DB, hosting, secrets vault) -- remove anyone no longer on the team
- [ ] Rotate all production secrets (DB password, API keys, JWT signing key)
- [ ] Verify backups exist and a recent one restores successfully

---

## Sign-Off

Fill in once the audit is complete.

| Field | Value |
|-------|-------|
| Audit date | `<YYYY-MM-DD>` |
| Auditor | `<name>` |
| Total findings | `<#>` Critical / `<#>` High / `<#>` Medium / `<#>` Low |
| Critical/High remediated | `<YES / NO>` |
| Next audit due | `<YYYY-MM-DD>` (90 days out) |
| Report filed at | `audit-reports/<DATE>-<PROJECT>.md` |

### Findings Log

| ID | Severity | Phase | Finding | Status | Owner |
|----|----------|-------|---------|--------|-------|
| 1  |          |       |         |        |       |
| 2  |          |       |         |        |       |
| 3  |          |       |         |        |       |

---

## Cadence Recommendation

| Audit Type | Frequency | Phases |
|-----------|-----------|--------|
| **Quick triage** | Every deploy / weekly | Phase 1 |
| **Standard audit** | Monthly | Phases 1-7 |
| **Deep audit** | Quarterly + before major launches | All 9 phases |

Skip the cadence at your own risk. Most security incidents come from drift -- something that was secure 6 months ago is no longer secure today because a dep changed or a new feature shipped.
