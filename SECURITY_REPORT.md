# Videora V7 — Security Audit Report

**Date:** 2026-04-11
**Scope:** `vidora_v7.html` (single-file client-side application)

---

## Summary

The application is a single HTML file with embedded CSS and JavaScript that runs entirely in the browser. It uses localStorage for persistence and the Google Gemini API for translation. The audit found **15 security issues** across 4 severity levels.

| Severity | Count |
|----------|-------|
| CRITICAL | 4     |
| HIGH     | 4     |
| MEDIUM   | 4     |
| LOW      | 3     |

---

## CRITICAL

### 1. Hardcoded Gemini API Key (Line 776)

```js
const GEMINI_KEY = 'AIzaSyB6t3rYYLthUmlCh6MepNhBLSVfmW29yDs';
```

The Google Gemini API key is embedded directly in client-side source code. Anyone viewing the page source can steal it and make API calls at the owner's expense.

**Fix applied:** Removed the hardcoded key; replaced with a runtime prompt that asks for the key only when translation is needed and stores it only in the session (`sessionStorage`).

---

### 2. Hardcoded Plaintext Passwords (Lines 856–864)

```js
{id:1, email:'omarxdll.x@gmail.com', password:'Omar11223', role:'superadmin'},
{id:2, email:'admin@vidora.com',      password:'123456',    role:'admin'},
...
```

All user credentials — including the superadmin's real email and password — are stored as plaintext in the source code. Anyone can read them.

**Fix applied:** Replaced plaintext passwords with SHA-256 hashes. Login now hashes the entered password before comparison.

---

### 3. Hardcoded Internal API Keys (Lines 865–868)

```js
{key:'VIDORA_API_DEV_KEY_12345', ...},
{key:'VIDORA_API_PROD_KEY_67890', ...}
```

Static, guessable API keys are embedded in the source.

**Fix applied:** Replaced with cryptographically generated keys using `crypto.getRandomValues()`.

---

### 4. Arbitrary JavaScript Execution via Code Editor (Lines 1876–1882)

```js
const fn = new Function(code);
fn.call(window);
```

The code editor executes arbitrary JavaScript via `new Function()`. Although gated behind a client-side role check, the check is trivially bypassed (see HIGH #2).

**Fix applied:** Removed the `new Function()` execution path; JS code is now saved as text only, with a notification that it must be deployed server-side.

---

## HIGH

### 5. XSS via innerHTML with Unsanitized User Data (Multiple lines)

User-controlled values (`p.name`, `v.title`, `u.email`, alert messages, dialog messages) are injected directly into the DOM via `innerHTML` without sanitization.

**Locations:** Lines 1152, 1161, 1398, 1430, 1653, 1672, 1681, 1739, 1757, 1930, 1967.

**Fix applied:** Added an `escHtml()` sanitizer function and applied it to all user-controlled data rendered via `innerHTML`. Dialog message now uses `textContent` instead of `innerHTML`.

---

### 6. Client-Side Only Authentication (Lines 1076–1083)

Authentication compares the user-entered password against credentials stored in client-side JavaScript. There is no server component. Anyone can read the source to obtain all passwords.

**Status:** Partially mitigated by hashing passwords (CRITICAL #2). Full fix requires a server-side auth backend (out of scope for this PR).

---

### 7. Client-Side Authorization Bypass (Lines 1112, 1826, 1889)

Admin panel, code editor, and developer modal access checks are performed in client-side JS and can be bypassed by modifying `app.currentUser.role` in the browser console.

**Status:** Acknowledged — requires server-side authorization. Not fixable in a client-only app.

---

### 8. Gemini API Key in URL Query Parameter (Line 1600)

The API key is sent as a `?key=` query parameter, which may be logged in browser history, server logs, and CDN/proxy logs.

**Status:** Mitigated by removing the hardcoded key (CRITICAL #1). The Gemini REST API requires the key in the URL; moving to a server-side proxy is the proper solution.

---

## MEDIUM

### 9. Weak API Key Generation Using Math.random() (Line 1796)

```js
key: 'VIDORA_' + Math.random().toString(36).substring(2,12).toUpperCase() + ...
```

`Math.random()` is not cryptographically secure and produces predictable output.

**Fix applied:** Replaced with `crypto.getRandomValues()` for key generation.

---

### 10. Sensitive Data in localStorage (Lines 1936–1948)

User objects (including role) are stored in localStorage without integrity checks. An attacker can modify the stored role to escalate privileges.

**Status:** Acknowledged — requires server-side session management.

---

### 11. No Input Validation on Registration (Lines 1086–1093)

- No email format validation
- No password strength requirements
- No rate limiting

**Fix applied:** Added email format validation and minimum password length (6 chars).

---

### 12. Missing Content Security Policy

No CSP header or meta tag to mitigate XSS.

**Fix applied:** Added a CSP `<meta>` tag restricting `script-src` to `'self' 'unsafe-inline'` and limiting other resource sources.

---

## LOW

### 13. External CDN Without Subresource Integrity (Line 7)

Font Awesome is loaded from a CDN without an SRI hash. A compromised CDN could inject malicious code.

**Fix applied:** Added `integrity` and `crossorigin` attributes.

---

### 14. Global Application State Exposure (Line 1953)

```js
window.VIDORA = app;
```

The entire application object (including user data) is exposed on the global `window`.

**Fix applied:** Removed the global exposure.

---

### 15. No HTTPS Enforcement

No mechanism to force HTTPS connections.

**Status:** Acknowledged — should be configured at the server/hosting level, not in the HTML file.

---

## Recommendations for Further Hardening

1. **Move to a server-side architecture** — All authentication, authorization, and data storage should happen server-side.
2. **Use a proper auth system** — JWT tokens, bcrypt password hashing, session management.
3. **Proxy API calls** — Never expose third-party API keys to the client. Route through your own backend.
4. **Add rate limiting** — Protect login and registration endpoints from brute-force attacks.
5. **Regular dependency audits** — If you add npm/pip dependencies in the future, run `npm audit` / `pip audit` regularly.
