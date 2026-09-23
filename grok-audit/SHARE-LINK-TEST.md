# Grok share-link audit

Date: 2026-09-23 (UTC+2)

## Verdict

- **Unauthenticated reachable? Yes.** In a fresh Chrome Incognito window with no X login, the share URL rendered the full probe transcript. The page showed only `Log in`/`Sign up` controls and no account chrome.
- **Revoke control present? No.** The share page exposed `Copy conversation` (authenticated view) but no Revoke/Delete/Unshare control. The original response Share menu exposed only `Share Conversation`, `Copy link`, `Post link`, and `Send via Chat`; no revoke/unshare option.
- **Survives conversation delete? Yes.** I deleted only the throwaway probe conversation (`conversation=2102783708549820871`) using Grok History > More > Delete. The authenticated conversation view became empty, but reloading the share URL in the unauthenticated Incognito window still rendered the full transcript.

## Evidence URLs

- Share: https://x.com/i/grok/share/33518f73664045c38d60ef29b8aa202e
- Original probe conversation: https://x.com/i/grok?conversation=2102783708549820871

## Screenshots

- `share-logged-in.png` — share page while authenticated, transcript visible.
- `share-unauth-post-delete.png` — Incognito, logged out, transcript still visible after source conversation deletion.
- `share-menu.png` — original response Share menu; no revoke/unshare control.
- `delete-menu.png` — Grok History menu showing Delete for the throwaway probe.
- `history-panel.png` — Grok History panel showing the throwaway probe entry.

## CVSS draft

Behavior is confirmed for this bearer share link, but the tested transcript was a throwaway probe and not sensitive user data. If the same behavior applies to private/sensitive chats, a conservative draft is **CVSS 3.1: 5.3 (AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:N/A:N)** because the opaque bearer URL must be obtained; 7.5 could be argued if possession of the link is treated as AC:L. Impact is unauthorized read access and persistence after source-chat deletion, with no observed revoke control.

No public posting or disclosure was performed.
