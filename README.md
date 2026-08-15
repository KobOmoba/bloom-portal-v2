# bloom-portal-v2 — Portal PENTEST SANDBOX
**Last reset:** 2026-08-14
**Source:** bloom-portal production (portal.edubloom.com.ng)

Clean copy of the current live Command Center codebase for security testing.

## Live sandbox URL
https://kobomoba.github.io/bloom-portal-v2/

## What changed
- Wiped old content
- Replaced with exact bloom-portal production code as of 2026-08-14

## Pentest status
See PENTEST_REPORT.md (tracked separately)

## Standing rules
- Fixes proved here → ported verbatim to bloom-portal
- Cache-bust: bump ?v= in index.html + CACHE_NAME in sw.js every push
- Never commit CNAME to this repo
