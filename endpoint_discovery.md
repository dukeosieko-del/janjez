# Endpoint Discovery Results

**Date:** 2026-09-22T21:27:32Z
**Tool:** curl (HEAD for GET patterns, POST for POST patterns, GET for GET patterns)
**Max timeout:** 10s per request

---

## Domain: https://janjez.social

### HEAD Requests

| # | Endpoint | HTTP Status | Previously Tested | Previous Status | Changed | Notes |
|---|----------|-------------|-------------------|-----------------|---------|-------|
| 1 | /api/business/v1/users | 404 | NEW | — | — | New endpoint |
| 2 | /api/business/v1/analytics | 404 | NEW | — | — | New endpoint |
| 3 | /api/business/v1/webhooks | 404 | NEW | — | — | New endpoint |
| 4 | /api/business/v1/products | 404 | NEW | — | — | New endpoint |
| 5 | /api/business/v1/catalogue | 404 | NEW | — | — | New endpoint |
| 6 | /api/business/v1/categories | 404 | NEW | — | — | New endpoint |
| 7 | /api/business/v1/withdrawals | 404 | NEW | — | — | New endpoint |
| 8 | /api/business/v1/payouts | 404 | NEW | — | — | New endpoint |
| 9 | /api/business/v1/affiliates | 404 | NEW | — | — | New endpoint |
| 10 | /api/business/v1/commissions | 404 | NEW | — | — | New endpoint |
| 11 | /api/auth/session | 404 | NEW | — | — | New endpoint |
| 12 | /api/auth/validate | 404 | NEW | — | — | New endpoint |
| 13 | /api/auth/me | 404 | NEW | — | — | New endpoint |
| 14 | /api/user/profile | 404 | NEW | — | — | New endpoint |
| 15 | /api/user/preferences | 404 | NEW | — | — | New endpoint |
| 16 | /api/metrics | 404 | NEW | — | — | New endpoint |
| 17 | /api/health/cache | 404 | NEW | — | — | New endpoint |
| 18 | /api/config | 404 | NEW | — | — | New endpoint |
| 19 | /api/version | 404 | NEW | — | — | New endpoint |
| 20 | /api/status | 404 | NEW | — | — | New endpoint |
| 21 | /api/info | 404 | NEW | — | — | New endpoint |
| 22 | /api/ping | 404 | NEW | — | — | New endpoint |
| 23 | /api/healthz | 404 | NEW | — | — | New endpoint |
| 24 | /api/readyz | 404 | NEW | — | — | New endpoint |
| 25 | /api/business/v1/ping | 404 | NEW | — | — | New endpoint |
| 26 | /api/business/v1/status | 404 | NEW | — | — | New endpoint |
| 27 | /api/business/v1/version | 404 | NEW | — | — | New endpoint |
| 28 | /api/business/v1/info | 404 | NEW | — | — | New endpoint |
| 29 | /api/blog | 404 | NEW | — | — | New endpoint |
| 30 | /api/blog/posts | 401 | NEW | — | — | New endpoint; returns 401 (auth required) |
| 31 | /api/blog/categories | 200 | NEW | — | — | New endpoint; publicly accessible |
| 32 | /api/content | 404 | NEW | — | — | New endpoint |
| 33 | /api/pages | 404 | NEW | — | — | New endpoint |
| 34 | /api/settings | 404 | NEW | — | — | New endpoint |
| 35 | /api/config | 404 | NEW | — | — | Duplicate test (listed twice in task); same result |
| 36 | /api/feature-flags | 404 | NEW | — | — | New endpoint |

### POST Requests

| # | Endpoint | HTTP Status | Previously Tested | Previous Status | Changed | Notes |
|---|----------|-------------|-------------------|-----------------|---------|-------|
| 1 | POST /api/business/v1/orders | 401 | NEW | — | — | New endpoint; requires API key |
| 2 | POST /api/business/v1/auth/verify | 404 | NEW | — | — | New endpoint |

### Summary — janjez.social

**Total endpoints tested:** 38 (36 unique + 1 duplicate)
**All endpoints are NEW** — none appeared in previous verification sweep (http_sweep_results.md)

| Status | Count |
|--------|-------|
| 200 | 1 |
| 401 | 2 |
| 404 | 35 |

---

## Domain: https://business.janjez.social

| # | Method | Endpoint | HTTP Status | Previously Tested | Previous Status | Changed | Notes |
|---|--------|----------|-------------|-------------------|-----------------|---------|-------|
| 1 | GET | /api/auth/check | 200 | Yes | 200 (HEAD) | No | Same status; method changed (HEAD→GET) |
| 2 | GET | /api/auth/sync | 405 | Yes | 400 (POST) | **Yes** | Status changed 400→405; method changed (POST→GET) |
| 3 | POST | /api/child/auth/signin | 500 | Yes | 400 (POST) | **Yes** | Status changed 400→500 (server error) |
| 4 | POST | /api/child/auth/signup | 500 | Yes | 400 (POST) | **Yes** | Status changed 400→500 (server error) |
| 5 | POST | /api/child/orders | 400 | Yes | 400 (POST) | No | Same status |
| 6 | GET | /api/partner/me | 401 | Yes | 401 (HEAD) | No | Same status |
| 7 | GET | /api/partner/panels | 401 | NEW | — | — | New endpoint |
| 8 | GET | /api/affiliate/me | 401 | Yes | 401 (HEAD) | No | Same status |
| 9 | GET | /api/affiliate/stats | 401 | Yes | 401 (HEAD) | No | Same status |
| 10 | POST | /api/affiliate/register | 401 | Yes | 401 (POST) | No | Same status |
| 11 | POST | /api/affiliate/payout/request | 401 | Yes | 401 (POST) | No | Same status |
| 12 | GET | /api/admin/partners | 404 | NEW | — | — | New endpoint |
| 13 | GET | /api/admin/audit | 404 | NEW | — | — | New endpoint |

### Summary — business.janjez.social

**Total endpoints tested:** 13 (2 NEW, 11 previously tested)
**Changed endpoints:** 3 (auth/sync, child/auth/signin, child/auth/signup)
**New endpoints:** 2 (partner/panels, admin/partners, admin/audit)

| Status | Count |
|--------|-------|
| 200 | 1 |
| 401 | 6 |
| 404 | 2 |
| 405 | 1 |
| 500 | 2 |

---

## Cross-Domain: Changed Endpoints Detail

| Endpoint | Domain | Previous | Current | Change |
|----------|--------|----------|---------|--------|
| /api/auth/sync | business.janjez.social | 400 (POST) | 405 (GET) | Method & status changed |
| /api/child/auth/signin | business.janjez.social | 400 (POST) | 500 (POST) | Server-side error introduced |
| /api/child/auth/signup | business.janjez.social | 400 (POST) | 500 (POST) | Server-side error introduced |

---

## Cross-Domain: New Endpoints Summary

### janjez.social (36 new endpoints, all returning 404 except:)
- **/api/blog/categories** → 200 (publicly accessible blog API)
- **/api/blog/posts** → 401 (auth required)
- **POST /api/business/v1/orders** → 401 (auth required)
- All other 33 new endpoints → 404

### business.janjez.social (2 new endpoints)
- **GET /api/partner/panels** → 401 (auth required)
- **GET /api/admin/partners** → 404
- **GET /api/admin/audit** → 404

---

## Key Observations

1. **janjez.social /api/v1/business endpoints**: All 10 /api/business/v1/* endpoints return 404. The POST /api/business/v1/orders returns 401 (auth required), but /api/business/v1/auth/verify returns 404 (endpoint may not exist).

2. **Server errors on business.janjez.social**: Two previously-working endpoints (/api/child/auth/signin, /api/child/auth/signup) now return 500 instead of 400 — potential regression or deployment issue.

3. **Method sensitivity**: /api/auth/sync on business.janjez.social returns 400 for POST but 405 for GET, indicating the endpoint exists but doesn't support GET.

4. **Blog API on janjez.social**: /api/blog/categories is publicly accessible (200), while /api/blog/posts requires auth (401). The base /api/blog returns 404.

5. **New admin endpoints on business.janjez.social**: /api/admin/partners and /api/admin/audit both return 404 (not yet deployed or not registered routes).
