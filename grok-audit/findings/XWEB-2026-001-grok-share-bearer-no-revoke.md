# XWEB-2026-001 — Grok share links are unauthenticated bearer URLs with no revoke control

| Field | Value |
|---|---|
| ID | XWEB-2026-001 |
| Status | **PARTIAL (lab)** — unauth read + no revoke **confirmed**; "survives chat delete" **RETRACTED** |
| CVSS 3.1 | **5.3** (`AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:N/A:N`) — draft; **7.5** if `AC:L` once the link is treated as obtained |
| Severity floor | Still meets outbound threshold (≥ 5.0) on remaining confirmed behavior |
| Asset | X Grok conversation sharing (`x.com/i/grok/share/<opaque-id>`) |
| Date | 2026-09-23 |
| Updated | 2026-09-23 — delete-survival claim retracted after Dani challenge + retest |
| Reporter | Dani Bengal |
| Audience | `@x` / Elon / xAI security |

## Correction log

2026-09-23 retest (`grok-audit/SHARE-DELETE-RETEST.md`):

- Source conversation **still existed** after the first audit's purported delete (Dani caught this).
- A **real** History → Delete made the conversation `Conversation introuvable`.
- The **same** share URL then showed **`Conversation not found`** when opened logged-out — transcript **gone**.
- Therefore: **share does NOT survive a confirmed conversation delete** (in this lab). Prior claim retracted.

## Summary (remaining)

A Grok "share conversation" link is a **capability URL** (opaque bearer). While the source conversation exists, anyone who has the URL can read the full transcript **without logging in**. There is **no revoke / unshare control** in the share UI observed in lab.

Deleting the source conversation **does invalidate** the share (retested). Residual risk: bearer link works unauthenticated until delete, and there is no way to revoke the share **without** deleting the whole conversation.

## Impact

- Confidentiality of Grok chats reachable via a leaked share URL without X login.
- No dedicated revoke → user must delete the entire conversation to kill the share.
- Opaque id ⇒ not trivially enumerable (`AC:H` conservative).

## Reproduction (confirmed)

1. Share → Copy link → open logged-out → full transcript.
2. Share menus → no Revoke / Unshare.
3. History → Delete → conversation introuvable → share logged-out → Conversation not found.

Lab IDs: share `33518f73664045c38d60ef29b8aa202e` / conversation `2102783708549820871`

## Recommended fix

1. Explicit public-to-holder warning + optional expiry.
2. **Revoke share** that invalidates bearer id **without** deleting the chat.
3. Keep cascade-invalidate on conversation delete (works in lab).
4. Optional: require login; watermark; one-time links.

## Out of scope

- No mass enumeration; no IDOR on unshared IDs; no exploit code.
