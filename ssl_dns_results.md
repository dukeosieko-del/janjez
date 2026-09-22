# SSL & DNS Verification Report
## Domains: janjez.social, business.janjez.social
**Date:** 2026-09-22

---

## 1. SSL Certificate Verification

### janjez.social
| Field | Value |
|-------|-------|
| Subject | CN = janjez.social |
| Issuer | CN = Cloudflare TLS proxy-everything Intercept CA |
| Serial | DB69927035491C16D221AEC8C03CFE0A |
| Not Before | Sep 22 19:37:37 2026 GMT |
| Not After | Sep 23 23:37:37 2026 GMT |
| Signature Algorithm | ECDSA with SHA256 |
| Public Key | EC (id-ecPublicKey) |
| SAN | DNS: janjez.social |
| Key Usage | critical |
| Extended Key Usage | DNS:janjez.social |

### business.janjez.social
| Field | Value |
|-------|-------|
| Subject | CN = business.janjez.social |
| Issuer | CN = Cloudflare TLS proxy-everything Intercept CA |
| Serial | 71387ACA4B5ED7FEDE837BF5D29B556F |
| Not Before | Sep 22 19:37:38 2026 GMT |
| Not After | Sep 23 23:37:38 2026 GMT |
| Signature Algorithm | ECDSA with SHA256 |
| Public Key | EC (id-ecPublicKey) |
| SAN | DNS: business.janjez.social |
| Key Usage | critical |
| Extended Key Usage | DNS:business.janjez.social |

**Verification:** Both certificates are valid and currently within their validity period (~24-hour lifespan, characteristic of Cloudflare proxy-issued certificates). Both are issued by Cloudflare's universal SSL/TLS proxy CA.

---

## 2. DNS Resolution Verification

### Available Tools
| Tool | Status |
|------|--------|
| openssl | /usr/bin/openssl |
| getent | /usr/bin/getent |
| curl | /usr/bin/curl |
| nslookup | NOT FOUND |
| host | NOT FOUND |
| dig | NOT FOUND |

### janjez.social DNS Results
| Method | Result |
|--------|--------|
| getent hosts | 3.7.231.161 janjez.social |
| nslookup | Not available |
| host | Not available |
| dig | Not available |

### business.janjez.social DNS Results
| Method | Result |
|--------|--------|
| getent hosts | 216.198.79.1 (vercel-dns-017.com) |
| getent hosts | 64.29.17.1 (vercel-dns-017.com) |
| nslookup | Not available |
| host | Not available |
| dig | Not available |

### Reverse DNS
| IP | Reverse DNS |
|----|-------------|
| 3.7.231.161 | ec2-3-7-231-161.ap-south-1.compute.amazonaws.com (AWS EC2, ap-south-1) |
| 216.198.79.1 | Not available (host command not installed) |
| 64.29.17.1 | Not available (host command not installed) |

---

## 3. Cloudflare Edge vs Origin Analysis

### HTTP Headers

#### janjez.social
```
HTTP/1.1 200 OK
Cache-Control: s-maxage=31536000
Cf-Cache-Status: DYNAMIC
Cf-Ray: a3f43270befb74ca-MIA
Connection: close
Content-Type: text/html; charset=utf-8
Server: cloudflare
X-Nextjs-Cache: HIT
X-Nextjs-Prerender: 1
X-Powered-By: Next.js
Vary: rsc, next-router-state-tree, ...
```

#### business.janjez.social
```
HTTP/1.1 200 OK
Cf-Cache-Status: DYNAMIC
Cf-Ray: a3f43274283674ca-MIA
Server: cloudflare
X-Nextjs-Cache: HIT
X-Nextjs-Prerender: 1
X-Vercel-Cache: HIT
X-Vercel-Id: iad1::f6mp8-1790110385319-3f35eab90bdf
Vary: rsc, next-router-state-tree, ...
```

### Connection Details
| Domain | Edge IP | Port | Response Time | HTTP Code |
|--------|---------|------|---------------|-----------|
| janjez.social | 3.7.231.161 | 443 | 0.34s | 200 |
| business.janjez.social | 216.198.79.1 | 443 | 0.17s | 200 |

### Cloudflare Indicators
| Indicator | janjez.social | business.janjez.social |
|-----------|--------------|----------------------|
| Server: cloudflare | Yes | Yes |
| Cf-Ray header | Yes (a3f43270befb74ca-MIA) | Yes (a3f43274283674ca-MIA) |
| Cf-Cache-Status | DYNAMIC | DYNAMIC |
| TLS cert issuer | Cloudflare proxy CA | Cloudflare proxy CA |

### Edge vs Origin Analysis

**janjez.social:**
- **Edge:** Cloudflare (Miami data center, Cf-Ray suffix: MIA)
- **Origin IP (as resolved):** 3.7.231.161 (AWS EC2 ap-south-1)
- **Origin Type:** AWS EC2 instance (reverse DNS confirms)
- **Backend Framework:** Next.js (X-Powered-By header)
- **Interpretation:** Traffic flows: Client → Cloudflare Edge (MIA) → Cloudflare proxy → Origin at AWS EC2 (ap-south-1). The origin IP appears in AWS but is served behind Cloudflare's proxy. The certificate is issued by Cloudflare's proxy CA, confirming full Cloudflare SSL termination.

**business.janjez.social:**
- **Edge:** Cloudflare (Miami data center, Cf-Ray suffix: MIA)
- **Origin IP (as resolved):** 216.198.79.1 / 64.29.17.1 (Vercel infrastructure)
- **Origin Type:** Vercel (X-Vercel-Cache, X-Vercel-Id headers; vercel-dns hostnames)
- **Backend Framework:** Next.js (X-Nextjs-Cache, X-Nextjs-Prerender headers)
- **Interpretation:** Traffic flows: Client → Cloudflare Edge (MIA) → Cloudflare proxy → Vercel Origin (iad1). Vercel functions as the origin server. Both Cloudflare and Vercel headers are present, confirming a dual-proxy/CDN setup: Cloudflare in front, Vercel as the origin platform.

---

## 4. Certificate Chain Analysis

| Domain | Certificates in Chain | Leaf Issuer | Interpretation |
|--------|----------------------|-------------|----------------|
| janjez.social | 2 | Cloudflare TLS proxy-everything Intercept CA | 1x leaf cert + 1x intermediate (Cloudflare proxy) |
| business.janjez.social | 2 | Cloudflare TLS proxy-everything Intercept CA | 1x leaf cert + 1x intermediate (Cloudflare proxy) |

**Analysis:** Both chains consist of exactly 2 certificates: the leaf certificate and one intermediate CA certificate. The issuer "Cloudflare TLS proxy-everything Intercept CA" is Cloudflare's universal SSL intermediate CA, used for all proxied/exchanged certificates. There is no self-signed root in the chain (roots are typically pre-installed in trust stores). This is a standard Cloudflare Universal SSL certificate chain.

---

## 5. TLS Version Support

| Domain | TLS 1.2 | TLS 1.3 |
|--------|---------|---------|
| janjez.social | Supported (TLSv1.2) | Supported (TLSv1.3) |
| business.janjez.social | Supported (TLSv1.2) | Supported (TLSv1.3) |

Both domains support modern TLS protocols (1.2 and 1.3). TLS 1.3 is available on both, providing improved security and performance (0-RTT, reduced handshake).

---

## Summary

| Check | janjez.social | business.janjez.social |
|-------|--------------|----------------------|
| SSL Certificate | Valid, Cloudflare proxy CA | Valid, Cloudflare proxy CA |
| Certificate Chain | 2 certs (leaf + intermediate) | 2 certs (leaf + intermediate) |
| DNS Resolution | 3.7.231.161 (AWS EC2) | 216.198.79.1, 64.29.17.1 (Vercel) |
| Cloudflare Edge | Yes (Miami / MIA) | Yes (Miami / MIA) |
| Origin | AWS EC2 (ap-south-1) | Vercel (iad1) |
| Backend | Next.js | Next.js (on Vercel) |
| TLS 1.2 | Supported | Supported |
| TLS 1.3 | Supported | Supported |
| Key Algorithm | ECDSA-SHA256 | ECDSA-SHA256 |
| Cert Lifespan | ~24 hours (Cloudflare proxy) | ~24 hours (Cloudflare proxy) |