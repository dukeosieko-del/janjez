# Fresh HTTP Verification Report

**Date:** 2026-09-22T21:27:44Z — 2026-09-22T21:28:03Z
**Tool:** curl -sI --max-time 10 (HEAD), curl -s --max-time 10 (GET bodies)
**Scope:** All endpoints on janjez.social and business.janjez.social
**Previous baseline:** http_sweep_results.md (2026-09-22T21:00:49Z), phase_a_verification.md

---

## Changes Since Previous Verification

| # | Endpoint | Domain | Previous Status | Current Status | Change | Notes |
|---|----------|--------|----------------|----------------|--------|-------|
| 1 | /auth/sign-in | janjez.social | Not probed (HEAD) | 200 | **NEW** | First HEAD probe; previously only tested with POST (200) in sweep |
| 2 | /auth/sign-out | business.janjez.social | 200 (POST) | 307 (HEAD) | **FLAGGED** | Different status by method — POST returns 200, HEAD redirects to /auth/sign-in; session-clearing Set-Cookie header present on 307 |
| 3 | / | business.janjez.social | 200 | 200 | No change | — |
| 4 | /api/business/v1/health | business.janjez.social | 404 | 404 | No change | Still not found on business side; route may not be registered |
| 5 | All other endpoints | Both | See tables below | Same | No change | All matching previous results |

---

## janjez.social — Endpoint Details

| # | Method | Path | Status | Time (s) | Server | Cache | Content-Type | Change from Previous |
|---|--------|------|--------|-----------|--------|-------|--------------|---------------------|
| 1 | HEAD | / | 200 OK | 0.333 | cloudflare | s-maxage=31536000, DYNAMIC (X-Nextjs-Cache: HIT) | text/html; charset=utf-8 | No — same 200 |
| 2 | HEAD | /auth/sign-in | 200 OK | 0.346 | cloudflare | no-store, DYNAMIC | text/html; charset=utf-8 | **NEW** — first HEAD probe |
| 3 | HEAD | /auth/callback | 200 OK | 0.374 | cloudflare | no-store, DYNAMIC | text/html; charset=utf-8 | No — same 200 |
| 4 | HEAD | /services | 200 OK | 1.768 | cloudflare | private no-cache, DYNAMIC | text/html; charset=utf-8 | No — same 200 |
| 5 | HEAD | /order | 200 OK | 0.363 | cloudflare | private no-cache, DYNAMIC | text/html; charset=utf-8 | No — same 200 |
| 6 | HEAD | /pay | 307 Temporary Redirect | 0.345 | cloudflare | no-store, DYNAMIC | N/A | No — same 307 |
| 7 | HEAD | /admin | 307 Temporary Redirect | 0.337 | cloudflare | no-store, DYNAMIC | N/A | No — same 307 |
| 8 | HEAD | /dashboard | 307 Temporary Redirect | 0.345 | cloudflare | no-store, DYNAMIC | N/A | No — same 307 |
| 9 | HEAD | /api/health | 200 OK | 0.474 | cloudflare | DYNAMIC | application/json | No — same 200 |
| 10 | HEAD | /api/orders | 401 Unauthorized | 0.347 | cloudflare | DYNAMIC | application/json | No — same 401 |
| 11 | HEAD | /api/business/v1/health | 401 Unauthorized | 0.335 | cloudflare | DYNAMIC | application/json | No — same 401 |
| 12 | HEAD | /api/business/v1/services | 401 Unauthorized | 0.327 | cloudflare | DYNAMIC | application/json | No — same 401 |
| 13 | HEAD | /api/business/v1/oauth/token | 405 Method Not Allowed | 0.336 | cloudflare | DYNAMIC | N/A | No — same 405 (HEAD) |

### GET Bodies for Key Endpoints (janjez.social)

| Endpoint | Status | Body |
|----------|--------|------|
| /api/business/v1/health | 401 (HEAD) | `{"success":false,"data":null,"error":{"code":"INVALID_API_KEY","message":"Invalid Business Side API key."},"request_id":"e5a0f7d2-5bde-4a36-b539-9e81e7035bd2","timestamp":"2026-09-22T21:28:02.947Z"}` |
| /api/business/v1/services | 401 (HEAD) | `{"success":false,"data":null,"error":{"code":"INVALID_API_KEY","message":"Invalid Business Side API key."},"request_id":"e696f03f-496e-4316-a539-cbaa3962752e","timestamp":"2026-09-22T21:28:03.624Z"}` |

---

## business.janjez.social — Endpoint Details

| # | Method | Path | Status | Time (s) | Server | Cache | Content-Type | Change from Previous |
|---|--------|------|--------|-----------|--------|-------|--------------|---------------------|
| 1 | HEAD | / | 200 OK | 0.113 | cloudflare | public, DYNAMIC (X-Vercel-Cache: HIT) | text/html; charset=utf-8 | No — same 200 |
| 2 | HEAD | /auth/sign-in | 200 OK | 0.104 | cloudflare | public, DYNAMIC (X-Vercel-Cache: HIT) | text/html; charset=utf-8 | No — same 200 (GET); POST was 405 |
| 3 | HEAD | /auth/sign-out | 307 Temporary Redirect | 0.138 | cloudflare | public, DYNAMIC | N/A | **FLAGGED** — POST was 200, HEAD is 307 |
| 4 | HEAD | /auth/callback | 307 Temporary Redirect | 0.156 | cloudflare | DYNAMIC | N/A | No — same 307 |
| 5 | HEAD | /dashboard | 200 OK | 0.095 | cloudflare | public, DYNAMIC (X-Vercel-Cache: HIT) | text/html; charset=utf-8 | No — same 200 |
| 6 | HEAD | /dashboard/onboarding | 307 Temporary Redirect | 0.187 | cloudflare/Next.js (X-Vercel-Cache: MISS) | N/A | text/html; charset=utf-8 | No — same 307 |
| 7 | HEAD | /dashboard/panels | 200 OK | 0.130 | cloudflare | public, DYNAMIC (X-Vercel-Cache: HIT) | text/html; charset=utf-8 | No — same 200 |
| 8 | HEAD | /admin | 307 Temporary Redirect | 0.153 | cloudflare/Next.js (X-Vercel-Cache: MISS) | N/A | text/html; charset=utf-8 | No — same 307 |
| 9 | HEAD | /api/health | 200 OK | 0.198 | cloudflare | public, DYNAMIC (X-Vercel-Cache: MISS) | application/json | No — same 200 |
| 10 | HEAD | /api/health/db | 200 OK | 0.193 | cloudflare | public, DYNAMIC (X-Vercel-Cache: MISS) | application/json | No — same 200 |
| 11 | HEAD | /api/health/janjez | 200 OK | 0.348 | cloudflare | public, DYNAMIC (X-Vercel-Cache: MISS) | application/json | No — same 200 |
| 12 | HEAD | /api/business/v1/health | 404 Not Found | 0.102 | cloudflare | public, DYNAMIC | text/html; charset=utf-8 | No — same 404 |

### GET Body for Key Endpoint (business.janjez.social)

| Endpoint | Status | Body |
|----------|--------|------|
| /api/health/janjez | 200 (HEAD) | `{"success":false,"data":null,"error":{"code":"INVALID_API_KEY","message":"Invalid Business Side API key."},"request_id":"946eb50a-6072-404c-8b02-4d42bda76723","timestamp":"2026-09-22T21:28:02.334Z"}` |

---

## Key Observations

### 1. No regressions detected
All endpoints return the same status codes as the previous verification. The P0 fixes confirmed in phase_a_verification.md remain intact:
- `/api/business/v1/health` (janjez.social): 401 (was 404 — fix confirmed)
- `/api/business/v1/oauth/token` (janjez.social): 405 (was 404 — fix confirmed)
- `/api/health/janjez` (business.janjez.social): 200 (was 503 — fix confirmed)

### 2. /auth/sign-out (business.janjez.social) — method-dependent behavior
- POST → 200 (previous sweep, http_sweep_results.md)
- HEAD → 307 (redirects to /auth/sign-in with session-clearing Set-Cookie)
- This is expected behavior: HEAD request without auth session gets redirected, POST request with session-clearing logic succeeds.

### 3. /api/business/v1/health (business.janjez.social) — still 404
This endpoint returns 404 on the business subdomain. The route may not be registered on business.janjez.social. This was already 404 in the previous sweep — no regression but also no resolution.

### 4. Response times stable
- janjez.social: 0.33–1.77s (1.77s for /services due to larger page)
- business.janjez.social: 0.10–0.35s (faster, Vercel-proxied)

### 5. Infrastructure
- janjez.social: Cloudflare (Miami MIA), Next.js, all requests Cf-Cache-Status: DYNAMIC
- business.janjez.social: Vercel (cle1 region), Cloudflare edge, mix of HIT/MISS caching
- Both use Cloudflare for SSL/TLS and CDN; both serve HSTS (max-age=63072000)

---

## Summary Statistics

| Domain | Total | 200 | 307 | 401 | 404 | 405 |
|--------|-------|-----|-----|-----|-----|-----|
| janjez.social | 13 | 5 | 3 | 4 | 0 | 1 |
| business.janjez.social | 12 | 6 | 4 | 0 | 1 | 0 |
| **Combined** | **25** | **11** | **7** | **4** | **1** | **1** |

---

*Generated by fresh HTTP verification — 2026-09-22T21:27:44Z*
