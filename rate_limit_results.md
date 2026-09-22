# Rate Limit Detection & Response Time Profiling Results

**Date:** 2026-09-22
**Tool:** curl (no subagents, HTTP only)

---

## 1. Rate Limit Detection (10 Rapid Requests)

**Target:** `https://business.janjez.social/api/health/db`

| Request | HTTP Code | Time (s) |
|---------|-----------|----------|
| 1       | 200       | 0.469701 |
| 2       | 200       | 0.476700 |
| 3       | 200       | 0.467996 |
| 4       | 200       | 0.483373 |
| 5       | 200       | 0.486870 |
| 6       | 200       | 0.474041 |
| 7       | 200       | 0.482998 |
| 8       | 200       | 0.499322 |
| 9       | 200       | 0.498119 |
| 10      | 200       | 0.498796 |

**Result:** All 10 requests returned HTTP 200. No rate limiting detected. Response times remained consistent (0.468–0.499s), with a slight upward trend suggesting server load rather than throttling. No `Retry-After` or rate limit headers observed.

**Average response time:** ~0.482s

---

## 2. Response Time Profiling (3 requests each, averaged)

| # | Endpoint | Type | Req 1 (s) | Req 2 (s) | Req 3 (s) | Avg (s) |
|---|----------|------|-----------|-----------|-----------|---------|
| 1 | `https://janjez.social/` | Static | 0.356505 | 0.354018 | 0.350100 | **0.354** |
| 2 | `https://janjez.social/api/health` | API | 1.059874 | 0.504731 | 0.782358 | **0.782** |
| 3 | `https://business.janjez.social/` | Next.js App | 0.127019 | 0.147712 | 0.160203 | **0.145** |
| 4 | `https://business.janjez.social/api/health/db` | API | 0.281162 | 0.189696 | 0.205830 | **0.226** |
| 5 | `https://business.janjez.social/api/health/janjez` | API (auth) | 0.726212 | 0.372557 | 0.339251 | **0.479** |
| 6 | `https://janjez.social/auth/sign-in` | SSR | 0.651075 | 0.347174 | 0.357934 | **0.452** |
| 7 | `https://business.janjez.social/auth/sign-in` | SSR | 0.117767 | 0.119906 | 0.141527 | **0.126** |

**Observations:**
- Business site endpoints are significantly faster (avg 0.145s for homepage) vs Janjez (avg 0.354s), likely due to caching (X-Vercel-Cache: HIT).
- API endpoints with auth overhead (`/api/health/janjez`) show high variance (0.339–0.726s), with the first request being slowest (cold start).
- `/api/health` on janjez.social is the slowest endpoint (avg 0.782s) with high variance, suggesting variable backend processing.
- Business SSR pages (`/auth/sign-in`) are extremely fast (avg 0.126s), benefiting from Next.js optimization.

---

## 3. Rate Limit Headers Check

### `https://business.janjez.social/` Response Headers:
```
HTTP/1.1 200 OK
Accept-Ranges: bytes
Access-Control-Allow-Origin: *
Age: 274515
Cache-Control: public, max-age=0, must-revalidate
Cf-Cache-Status: DYNAMIC
Cf-Ray: a3f432bb4eca74ca-MIA
Connection: close
Content-Disposition: inline
Content-Length: 36496
Content-Type: text/html; charset=utf-8
Date: Tue, 22 Sep 2026 20:53:16 GMT
Etag: "a1155238e6f8b0213f0fca8f8d8e11ce"
Server: cloudflare
Strict-Transport-Security: max-age=63072000
Vary: rsc, next-router-state-tree, next-router-prefetch, next-router-segment-prefetch
X-Matched-Path: /
X-Nextjs-Prerender: 1
X-Nextjs-Stale-Time: 300
X-Vercel-Cache: HIT
X-Vercel-Id: iad1::lnlnp-1790110396702-94078d8b7c7f
```

### `https://janjez.social/` Response Headers:
```
HTTP/1.1 200 OK
Cache-Control: s-maxage=31536000
Cf-Cache-Status: DYNAMIC
Cf-Ray: a3f432bc4f0674ca-MIA
Connection: close
Content-Type: text/html; charset=utf-8
Date: Tue, 22 Sep 2026 20:53:17 GMT
Etag: W/"dg9czxmma6xsy"
Permissions-Policy: camera=(), microphone=(), geolocation=(self)
Referrer-Policy: strict-origin-when-cross-origin
Server: cloudflare
Vary: rsc, next-router-state-tree, next-router-prefetch, next-router-segment-prefetch, Accept-Encoding
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-Nextjs-Cache: HIT
X-Nextjs-Prerender: 1
X-Nextjs-Prerender: 1
X-Nextjs-Stale-Time: 300
X-Powered-By: Next.js
```

**Result:** **No rate limiting headers detected** on either domain. No `RateLimit-*`, `X-RateLimit-*`, `Retry-After`, `Throttle`, or similar headers are present in responses from either janjez.social or business.janjez.social. Both domains use Cloudflare (DYNAMIC cache) and Vercel infrastructure but do not expose rate limit information in headers.

---

## 4. Error Handling Verification

### 4a. `/api/health/janjez` — No API Key
```
URL: https://business.janjez.social/api/health/janjez (no key)
Response: {"success":false,"data":null,"error":{"code":"INVALID_API_KEY","message":"Invalid Business Side API key."},"request_id":"12b024be-3fab-4de2-a156-537e104b4179","timestamp":"2026-09-22T20:52:48.112Z"}
HTTP Code: 200 | Time: 0.802s
```
**Expected:** INVALID_API_KEY — **PASS** (returns correct error code, though HTTP 200 instead of 401)

### 4b. `/api/auth/check` — No Cookie
```
URL: https://business.janjez.social/api/auth/check (no cookie)
Response: {"authenticated":false,"redirectTo":"/auth/sign-in"}
HTTP Code: 200 | Time: 0.174s
```
**Expected:** 401 — **PARTIAL** (returns 200 with `authenticated:false` and redirect hint instead of explicit 401)

### 4c. `/api/business/v1/health` — No API Key (Janjez domain)
```
URL: https://janjez.social/api/business/v1/health (no key)
Response: {"success":false,"data":null,"error":{"code":"INVALID_API_KEY","message":"Invalid Business Side API key."},"request_id":"f65f43b5-76cf-436e-aedb-4410c6b6fd0f","timestamp":"2026-09-22T20:52:49.752Z"}
HTTP Code: 401 | Time: 0.321s
```
**Expected:** 401/INVALID_API_KEY — **PASS** (returns 401 with INVALID_API_KEY error code)

### 4d. `/api/orders` — No API Key (Janjez domain)
```
URL: https://janjez.social/api/orders (no key)
Response: {"error":"Unauthorized"}
HTTP Code: 401 | Time: 0.593s
```
**Expected:** 401 — **PASS** (returns 401 with Unauthorized error)

---

## Summary

| Category | Finding |
|----------|---------|
| **Rate limiting** | Not actively enforced — 10/10 rapid requests succeeded with HTTP 200 |
| **Rate limit headers** | None present on either domain |
| **Error handling consistency** | Inconsistent — business.janjez.social returns 200 for auth failures; janjez.social correctly returns 401 |
| **Slowest endpoint** | `janjez.social/api/health` (avg 0.782s) — high variance |
| **Fastest endpoint** | `business.janjez.social/auth/sign-in` (avg 0.126s) |
| **Infrastructure** | Cloudflare + Vercel edge caching; DYNAMIC cache status on tested pages |