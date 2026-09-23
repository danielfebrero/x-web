# XWEB-2026-001 — Grok share links are unauthenticated bearer URLs with no revoke and survive chat deletion

| Field | Value |
|---|---|
| ID | XWEB-2026-001 |
| Status | Confirmed (lab) |
| CVSS 3.1 | **5.3** (`AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:N/A:N`) — draft; **7.5** if `AC:L` once the link is treated as obtained |
| Severity floor | Meets outbound threshold (≥ 5.0) |
| Asset | X Grok conversation sharing (`x.com/i/grok/share/<opaque-id>`) |
| Date | 2026-09-23 |
| Reporter | Dani Bengal (`@cdxxotus`) |
| Audience | `@x` / Elon / xAI security |

## Summary

A Grok “share conversation” link is a **capability URL** (opaque bearer). Anyone who has the URL can read the full transcript **without logging in**. There is **no revoke / unshare control** in the share UI. Deleting the source conversation **does not invalidate** the share link — the transcript remains readable to unauthenticated visitors.

## Impact

- Confidentiality of Grok chats that a user believed they shared “with a link” (or that leaked via clipboard, screenshots of URL bar, referrer logs, chat apps, etc.).
- False sense of control: deleting the chat does not remove the shared copy.
- No observed expiry or revoke path → long-lived exposure once the bearer token-in-path is known.

## Preconditions

- Victim (or attacker with access to victim session) uses **Share → Copy link** on a Grok conversation.
- Attacker obtains the URL (phishing, shoulder-surf, shared clipboard, logged proxy, accidental post, etc.).
- Link format is opaque (`/i/grok/share/<32-hex>`) — not trivially enumerable; hence `AC:H` in the conservative score.

## Reproduction (safe)

1. Log in to X → open `https://x.com/i/grok` → create a throwaway chat.
2. Share → **Copy link** → obtain `https://x.com/i/grok/share/<id>`.
3. Open that URL in a **logged-out / Incognito** browser → **full transcript renders** (only Log in / Sign up chrome).
4. Inspect Share menus → **no Revoke / Unshare**.
5. Delete the source conversation from Grok History → reload the share URL while still logged out → **transcript still present**.

Lab evidence (this audit):

- Share: `https://x.com/i/grok/share/33518f73664045c38d60ef29b8aa202e`
- Deleted conversation: `https://x.com/i/grok?conversation=2102783708549820871`
- Screenshots under `grok-audit/screenshots/` (`share-unauth-post-delete.png`, etc.)
- Detail log: `grok-audit/SHARE-LINK-TEST.md`

## Recommended fix

1. Bind share views to authz policy OR treat as public with **explicit** “this will be public” + mandatory expiry.
2. Add **Revoke share** (and bulk revoke) that invalidates the bearer id server-side.
3. On conversation delete (or “delete history”), **cascade-invalidate** share tokens by default.
4. Optional: require login to view shares; watermark viewer; one-time / expiring links; audit log of share opens.

## Out of scope / non-claims

- No mass enumeration of share IDs demonstrated.
- No access to other users’ *unshared* conversations (conversation-id IDOR probes were negative in recon).
- No weaponized exploit code in this report.

## Related recon

See `grok-audit/RECON-NOTES.md` for full surface inventory.
