# bloom-portal-v2 — Admin Command Center Sandbox

**Sandbox for:** bloom-portal (portal.edubloom.com.ng)
**Sandbox-first rule:** All fixes proved here before production gets them.
**Last updated:** 2026-08-20

---

## Current Versions

| File | Version |
|------|---------|
| portal_app.js | `?v=20260820-security` |
| sw.js CACHE_NAME | `edubloom-bloom-portal-v2-20260820-security` |

---

## Session History

### 2026-08-20 — Backport from production

Production bloom-portal received an XSS fix this session:
Calendar state dropdown was populating `<option>` tags using raw `${s}` template
literals without sanitisation. Fixed with `esc(s)` in both the value attribute
and the display text. Risk was low (Bayo-only writes to that Firestore collection)
but fixed for consistency and defence-in-depth.

Fix ported verbatim to this sandbox (portal_app.js line 157).

Cache-buster bumped: `?v=20260820-security`
CACHE_NAME bumped: `edubloom-bloom-portal-v2-20260820-security`

---

### 2026-08-18 — Firebase Auth hotfix

Real Firebase Auth (email/password) added. 8-hour session timeout.
Firestore password fallback for offline resilience.
Payment status tracking on approved schools. Calendar tab.

---

### 2026-08-19 — Security hardening

Firestore rules published. `admin_approved_schools` locked to Bayo-only
(contains every school password). Other admin collections locked accordingly.

---

## Standing Rules (this repo)

- Sandbox-first: prove all features here before Bayo approves production port
- After every push, update this README in the same push
- node --check portal_app.js before every push (this file passes cleanly)
- Cache-bust: bump ?v= in index.html AND CACHE_NAME in sw.js together, always
- Session timeout: 8 hours (ad_auth_time in localStorage)

## Key Approval Flow

Agent submits deal → Bayo approves in portal → school ID generated (BLOOM-XXXXXX)
→ school doc created in Firestore → commission logged in admin_ledger
→ WhatsApp credentials sent to principal
