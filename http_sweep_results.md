# HTTP Endpoint Sweep Results

**Date:** 2026-09-22T21:00:49Z
**Tool:** curl -sI (HEAD) for GET endpoints, curl -s -X POST with empty JSON body for POST endpoints
**Max timeout:** 10s per request

## Domain: https://janjez.social

| # | Method | Path | Status | Time (ms) | Content-Type |
|---|--------|------|--------|-----------|-------------|
| 1 | HEAD | / | 200 | 345.9 | text/html; charset=utf-8 |
| 2 | HEAD | /auth/callback | 200 | 350.8 | text/html; charset=utf-8 |
| 3 | HEAD | /auth/error | 404 | 328.8 | text/html; charset=utf-8 |
| 4 | HEAD | /dashboard | 307 | 327.5 | N/A |
| 5 | HEAD | /dashboard/onboarding | 307 | 327.9 | N/A |
| 6 | HEAD | /dashboard/panels | 307 | 334.7 | N/A |
| 7 | HEAD | /dashboard/reseller | 307 | 329.1 | N/A |
| 8 | HEAD | /dashboard/wallet | 307 | 324.5 | N/A |
| 9 | HEAD | /dashboard/withdrawals | 307 | 321.7 | N/A |
| 10 | HEAD | /admin | 307 | 326.2 | N/A |
| 11 | HEAD | /admin/audit | 307 | 348.8 | N/A |
| 12 | HEAD | /admin/partners | 307 | 344.1 | N/A |
| 13 | HEAD | /admin/withdrawals | 307 | 328.3 | N/A |
| 14 | HEAD | /services | 200 | 2415.7 | text/html; charset=utf-8 |
| 15 | HEAD | /orders/all | 307 | 340.1 | N/A |
| 16 | HEAD | /api/orders | 401 | 327.7 | application/json |
| 17 | HEAD | /api/health | 200 | 475.7 | application/json |
| 18 | HEAD | /api/business/v1/health | 401 | 319.8 | application/json |
| 19 | HEAD | /api/auth/check | 404 | 374.6 | text/html; charset=utf-8 |
| 20 | HEAD | /api/partner/me | 404 | 317.2 | text/html; charset=utf-8 |
| 21 | HEAD | /api/partner/wallet/balance | 404 | 336.3 | text/html; charset=utf-8 |
| 22 | HEAD | /api/affiliate/me | 404 | 310.0 | text/html; charset=utf-8 |
| 23 | HEAD | /api/affiliate/stats | 404 | 323.8 | text/html; charset=utf-8 |
| 24 | POST | /auth/sign-in | 200 | 385.3 | text/html; charset=utf-8 |
| 25 | POST | /auth/sign-out | 404 | 353.7 | text/html; charset=utf-8 |
| 26 | POST | /order | 200 | 361.7 | text/html; charset=utf-8 |
| 27 | POST | /pay | 307 | 327.8 | N/A |
| 28 | POST | /api/business/v1/oauth/token | 401 | 324.4 | application/json |
| 29 | POST | /api/auth/sync | 404 | 338.8 | text/html; charset=utf-8 |
| 30 | POST | /api/child/auth/signin | 404 | 315.0 | text/html; charset=utf-8 |
| 31 | POST | /api/child/auth/signup | 404 | 334.2 | text/html; charset=utf-8 |
| 32 | POST | /api/child/orders | 404 | 331.5 | text/html; charset=utf-8 |
| 33 | POST | /api/partner/activate | 404 | 330.5 | text/html; charset=utf-8 |
| 34 | POST | /api/affiliate/register | 404 | 341.4 | text/html; charset=utf-8 |
| 35 | POST | /api/affiliate/payout/request | 404 | 344.8 | text/html; charset=utf-8 |
| 36 | POST | /api/admin/withdrawal/request | 404 | 345.5 | text/html; charset=utf-8 |
| 37 | POST | /api/webhooks/janjez/order-status | 404 | 334.3 | text/html; charset=utf-8 |

## Domain: https://business.janjez.social

| # | Method | Path | Status | Time (ms) | Content-Type |
|---|--------|------|--------|-----------|-------------|
| 1 | HEAD | / | 200 | 126.4 | text/html; charset=utf-8 |
| 2 | HEAD | /auth/callback | 307 | 151.8 | N/A |
| 3 | HEAD | /auth/error | 200 | 132.8 | text/html; charset=utf-8 |
| 4 | HEAD | /dashboard | 200 | 125.8 | text/html; charset=utf-8 |
| 5 | HEAD | /dashboard/onboarding | 307 | 184.2 | text/html; charset=utf-8 |
| 6 | HEAD | /dashboard/panels | 200 | 101.5 | text/html; charset=utf-8 |
| 7 | HEAD | /dashboard/reseller | 200 | 128.9 | text/html; charset=utf-8 |
| 8 | HEAD | /dashboard/wallet | 200 | 136.4 | text/html; charset=utf-8 |
| 9 | HEAD | /dashboard/withdrawals | 307 | 138.5 | text/html; charset=utf-8 |
| 10 | HEAD | /admin | 307 | 163.0 | text/html; charset=utf-8 |
| 11 | HEAD | /admin/audit | 307 | 148.4 | text/html; charset=utf-8 |
| 12 | HEAD | /admin/partners | 307 | 159.0 | text/html; charset=utf-8 |
| 13 | HEAD | /admin/withdrawals | 307 | 144.1 | text/html; charset=utf-8 |
| 14 | HEAD | /api/health | 200 | 210.6 | application/json |
| 15 | HEAD | /api/health/db | 200 | 207.6 | application/json |
| 16 | HEAD | /api/health/janjez | 200 | 703.8 | application/json |
| 17 | HEAD | /api/business/v1/health | 404 | 105.5 | text/html; charset=utf-8 |
| 18 | HEAD | /api/auth/check | 200 | 118.7 | application/json |
| 19 | HEAD | /api/partner/me | 401 | 125.4 | application/json |
| 20 | HEAD | /api/partner/wallet/balance | 401 | 147.5 | application/json |
| 21 | HEAD | /api/affiliate/me | 401 | 149.5 | application/json |
| 22 | HEAD | /api/affiliate/stats | 401 | 154.1 | application/json |
| 23 | POST | /auth/sign-in | 405 | 605.4 | text/html; charset=utf-8 |
| 24 | POST | /auth/sign-out | 200 | 126.1 | application/json |
| 25 | POST | /api/auth/sync | 400 | 132.9 | application/json |
| 26 | POST | /api/child/auth/signin | 400 | 126.0 | application/json |
| 27 | POST | /api/child/auth/signup | 400 | 136.8 | application/json |
| 28 | POST | /api/child/orders | 400 | 127.5 | application/json |
| 29 | POST | /api/partner/activate | 401 | 125.6 | application/json |
| 30 | POST | /api/affiliate/register | 401 | 181.0 | application/json |
| 31 | POST | /api/affiliate/payout/request | 401 | 146.3 | application/json |
| 32 | POST | /api/admin/withdrawal/request | 404 | 111.9 | text/html; charset=utf-8 |
| 33 | POST | /api/webhooks/janjez/order-status | 401 | 130.9 | application/json |

---

## Summary

**Total endpoints probed:** 70

### Status Code Distribution (all domains)

| Status | Count |
|--------|-------|
| 200 | 17 |
| 307 | 19 |
| 400 | 4 |
| 401 | 11 |
| 404 | 18 |
| 405 | 1 |

---

*Generated by HTTP endpoint sweep*
