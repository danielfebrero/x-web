# Pass 5 — unauth HTTP headers on Grok share

URL: `https://x.com/i/grok/share/34708e5803394155b5c5cc86fbf53692`
Date: 2026-09-23T18:18:51+02:00

## curl -sI (follow redirects)
```
HTTP/2 403 
date: Wed, 23 Sep 2026 16:18:51 GMT
perf: 7402827104
server: cloudflare envoy
x-powered-by: Express
cache-control: no-cache, no-store, max-age=0
x-transaction-id: 471db743ca6e910c
x-response-time: 10
origin-cf-ray: a3fade207d5aacc6-IAD
strict-transport-security: max-age=631138519; includeSubdomains
x-served-by: t4_a
vary: Accept-Encoding
cf-cache-status: DYNAMIC
set-cookie: guest_id_marketing=v1%3A179018033161544608; Max-Age=63072000; Expires=Fri, 22 Sep 2028 16:18:51 GMT; Path=/; Domain=.x.com; Secure; SameSite=None
set-cookie: guest_id_ads=v1%3A179018033161544608; Max-Age=63072000; Expires=Fri, 22 Sep 2028 16:18:51 GMT; Path=/; Domain=.x.com; Secure; SameSite=None
set-cookie: personalization_id="v1_oF8TZZdxNx25Twpqb2vO0Q=="; Max-Age=63072000; Expires=Fri, 22 Sep 2028 16:18:51 GMT; Path=/; Domain=.x.com; Secure; SameSite=None
set-cookie: guest_id=v1%3A179018033161544608; Max-Age=63072000; Expires=Fri, 22 Sep 2028 16:18:51 GMT; Path=/; Domain=.x.com; Secure; SameSite=None
set-cookie: __cf_bm=aRkvy7n63WYWab2U3oVRRXKxGHB_GfqPDD2iG3Km8Lw-1790180331.5948954-1.0.1.1-PiyNeZQxxeSDLqeIBHTUOqiMVsFei.aowDZufVHSBzWGiILKCYL4kJbvAEsIID.JK_nYKg4ruj6PWOfPZ1aXuWZfu4hEyYboNdxVTHBAyXFo4NBbJjoxYNdCNI2edfR8; HttpOnly; SameSite=None; Secure; Path=/; Domain=x.com; Expires=Wed, 23 Sep 2026 16:48:51 GMT
cf-ray: a3fade207d5aacc6-IAD

```

## Cache / security headers of interest
```
HTTP/2 403 
cache-control: no-cache, no-store, max-age=0
strict-transport-security: max-age=631138519; includeSubdomains
vary: Accept-Encoding
set-cookie: guest_id_marketing=v1%3A179018033174670688; Max-Age=63072000; Expires=Fri, 22 Sep 2028 16:18:51 GMT; Path=/; Domain=.x.com; Secure; SameSite=None
set-cookie: guest_id_ads=v1%3A179018033174670688; Max-Age=63072000; Expires=Fri, 22 Sep 2028 16:18:51 GMT; Path=/; Domain=.x.com; Secure; SameSite=None
set-cookie: personalization_id="v1_9nYLWpAjgxC8nJMH+r17fg=="; Max-Age=63072000; Expires=Fri, 22 Sep 2028 16:18:51 GMT; Path=/; Domain=.x.com; Secure; SameSite=None
set-cookie: guest_id=v1%3A179018033174670688; Max-Age=63072000; Expires=Fri, 22 Sep 2028 16:18:51 GMT; Path=/; Domain=.x.com; Secure; SameSite=None
set-cookie: __cf_bm=IrQNFxZ6.nnNgQTxhDLO7AXLNGDyrDMUhL1UkGqPG0U-1790180331.7247481-1.0.1.1-0nfKvVwnPsZCz093sTPNOCJ4ITtlhWwRYjYZs_mV1B8i9DPdNwETrsify4GnyLQnVMM_Y21KOJbs_4ksdc02.kcgPUKX204w1S3D0zuoZNycpvr6jaNlaBrkHrTXUgLU; HttpOnly; SameSite=None; Secure; Path=/; Domain=x.com; Expires=Wed, 23 Sep 2026 16:48:51 GMT
```

## robots.txt snippets (x.com)
```
# Shared group so Googlebot and Bingbot always get the same rules.
Allow: /i/api/
# favor of Allow, so /i/api/ fetches stay crawlable.
Allow: /i/api/*
Allow: /i/api/
Allow: /i/api/*
# WHAT-4882 - Keep notification-email links (/i/u) out of search results.
# Named crawlers stay un-blocked on purpose: they must crawl /i/u to see its
Disallow: /i/u
```
