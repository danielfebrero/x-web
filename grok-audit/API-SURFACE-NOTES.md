# xAI / Grok API surface notes (public recon)

Date: 2026-09-23 ~17:48–17:49 CEST (UTC+2)  
Scope: unauthenticated HTTP GET to public docs/API/product URLs only. No auth tokens, no brute force, no authenticated console/API abuse. Bodies truncated under `api-samples/`.

Related: `RECON-NOTES.md` (UI/session recon); sample files in `api-samples/`.

## Summary table

| Target | Status | Final URL | Auth wall? | Notable headers | Body / leak notes |
|---|---|---|---|---|---|
| `https://docs.x.ai/overview` | **200** | `https://docs.x.ai/overview` | No (public docs) | `server: cloudflare`; HSTS; CSP `frame-ancestors 'none'`; `cf-ray`; no `request-id` / `x-request-id` | Large Next.js HTML (~543KB). Title/meta: “Grok API Documentation \| SpaceXAI Docs”. Public Sentry client meta (`sentry-public_key` in baggage) — expected for browser SDK, not an API secret. No stack traces. |
| `https://docs.x.ai/` | **200** (via **308**) | `https://docs.x.ai/overview` | No | Same as overview after redirect (`308 Location: /overview`) | Same docs shell as overview. |
| `https://api.x.ai/` | **421** | `https://api.x.ai/` | N/A (non-success) | `content-type: text/plain`; HSTS; `server: cloudflare`; `cf-ray`; no request-id | Plain text only: `Welcome to the xAI API! Documentation is available at https://docs.x.ai/`. No internals. (421 matches earlier browser note in RECON-NOTES.) |
| `https://api.x.ai/v1/models` | **401** | same | Yes (API key required) | `content-type: application/json`; **`access-control-allow-origin: *`**; **`access-control-expose-headers: *`**; `Vary: origin, access-control-request-method, access-control-request-headers`; HSTS; Cloudflare | Clean JSON: `{"code":"unauthenticated:no-credentials","error":"No credentials presented."}`. No stack, hostnames, or key hints. |
| `https://console.x.ai/` | **200** (via **307**) | `https://console.x.ai/home` | App shell public; product auth expected for keys/billing (prior UI recon: Sign in / Create account) | `x-frame-options: DENY`; `x-content-type-options: nosniff`; HSTS; CSP with Stripe/Intercom/analytics; `connect-src` includes `https://api.x.ai`, `wss://api.x.ai`, `https://accounts.x.ai`, LiveKit Grok hosts | Next.js SPA HTML. Truncated sample has no credentials. No server error body. |
| `https://grok.x.com/` | **200** (via **302**) | `https://x.com/i/grok?focus=1` | X session for full chat (unauth GET still returns X HTML shell) | Redirect then X/`cloudflare envoy`; `x-frame-options: DENY`; rich CSP mentioning `api.x.ai` | Redirect-only surface into X Grok UI. |
| `https://grok.com/` | **200** | same | Public marketing/app shell (Imagine features may still gate actions) | Cloudflare; HSTS; DENY frame; CSP includes `ws://localhost:*` / `ws://127.0.0.1:*`, `*.x.ai`, Stripe, etc. | Large Next.js HTML (~592KB). No API secrets in truncated sample. |
| `https://grok.com/imagine` | **200** | same | UI auth wall for generation (prior recon: Sign in/Sign up); HTML still public | Same class of CSP/security headers as grok.com | Public Imagine landing HTML (~545KB). No generation attempted. |

## Unauthenticated API path probes (status only, one request each)

Base: `https://api.x.ai` — GET only; no request bodies; no retries.

| Path | Status |
|---|---|
| `/v1/models` | **401** |
| `/v1/chat/completions` | **405** (GET not allowed; expected for chat POST endpoint) |
| `/v1/api-key` | **401** |
| `/health` | **404** |
| `/status` | **404** |

Source log: `api-samples/api-path-probes.txt` (timestamp `2026-09-23T17:48:41+02:00`).

## Samples on disk

Directory: `/workspace/disclosure-out/grok-audit/api-samples/`

Per target: `*.headers`, `*.meta`, `*.body` / `*.body.trunc` (bodies capped ~8KB where large). Plus `api-path-probes.txt`.

## Observations (non-findings / hygiene)

- API auth failures return stable, low-detail JSON codes (`unauthenticated:no-credentials`); no verbose internals observed.
- No `request-id` / `x-request-id` on sampled `api.x.ai` responses (only Cloudflare `cf-ray`).
- Public API CORS allows any origin (`ACAO: *`) with `access-control-expose-headers: *` on the 401 from `/v1/models` — typical for bearer-token browser clients; not evidence of privilege bypass by itself.
- Docs branding string “SpaceXAI” appears in `<title>` / OG tags (observational inconsistency vs xAI).
- Docs/console/grok CSP and third-party allowlists (Stripe, Intercom, analytics, LiveKit, localhost WS on grok.com) are surface inventory only.

## CVSS ≥ 5 candidates

**None confirmed from this API/docs recon.** Auth walls behaved as expected (401/405/404); error bodies did not leak internals; no unauthenticated model list or key material returned.

| ID | Status | Notes |
|---|---|---|
| — | — | No evidence-backed CVSS≥5 on the probed public API/docs surfaces. |

### Hypotheses only (not scored; need separate owned-account tests)

| Hypothesis | Why not CVSS≥5 yet | Suggested follow-up (still responsible / owned assets) |
|---|---|---|
| H1: Bearer-style Grok share links may be reachable without auth / lack revoke | From prior UI recon (`RECON-NOTES.md` / share tests), not from this API curl pass | Unauth fetch of an owned share URL; delete/revoke semantics |
| H2: Broad API CORS (`*`) + exposed headers could amplify a future XSS/token theft | Requires a separate XSS or token-exfil bug; CORS alone ≠ vulnerability here | Only relevant if a reflected/stored XSS or token leak is found |
| H3: `ws://localhost:*` in grok.com CSP | Often intentional for local bridges; not a remote exploit by itself | Document as hardening note; do not treat as remote RCE |

## Method / constraints

- Tooling: `curl -sS -L` with short timeouts; User-Agent labeled responsible-disclosure-recon.
- No stolen tokens, no credential stuffing, no rate-limit hammering, no POST exploit payloads to chat completions.
- Stopped after one status probe per API path as requested.
