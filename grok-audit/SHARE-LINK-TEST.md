# Share-link test (in progress)

Target: `https://x.com/i/grok/share/33518f73664045c38d60ef29b8aa202e`

## Unauth HTTP shell (curl, no cookies)
- `GET` share URL → **HTTP 200** HTML shell (~299KB)
- Sets `guest_id*` cookies; clears `ct0`
- Probe transcript strings **not** present in initial HTML (client-side fetch expected)
- Feature flags observed in page boot: `grokShare`, `responsive_web_grok_share_attachment_enabled`, `responsive_web_grok_xweb_linked_share_readonly_enabled`

## Pending (browser)
- Logged-out / private window render of transcript
- Presence of revoke/unshare control
- Survival after conversation delete

## Tentative severity (if unauth full transcript + no revoke + no expiry)
Bearer opaque link ⇒ not trivially guessable → likely **CVSS 5.3–6.5** (C:H/I:N/A:N with UI:R), pending confirmation.
