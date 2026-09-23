# Grok/X Deep-Dive Notes
Date: 2026-09-23 (UTC+2)
Scope: observation and gentle probes only; no public posts, DMs, purchases, credential changes, exploit payloads, or mass enumeration.

## Status / inventory delta
- Deep-dive resumed after parent steering; X Chat delivery was aborted before send.
- Existing recon baseline is in `RECON-NOTES.md`; this file records only additional probes.
- Logged-in X session is Dani (UI-masked handle in this environment).

## Candidate issues
- None newly confirmed at start of deep-dive. Existing XWEB-2026-001 share-link issue remains separate.

## Probe log

### Throwaway share canary (completed)
- Created benign chat at conversation `2102787580286620032` containing `CANARY-XWEB-2026-002-7f3c9a` and response `canary acknowledged.`
- Share URL copied from UI: `https://x.com/i/grok/share/34708e5803394155b5c5cc86fbf53692` (left alive; not deleted).
- Screenshot: `screenshots/canary-share-url.webp` (browser chrome shows copied URL and chat canary).

## Steering correction: share-delete retest (completed; supersedes prior claim)
- Exact conversation `2102783708549820871` was confirmed alive with the prior benign transcript and present in History as `Grok 4.6 xAI Tools Overview`.
- Used History → Plus → `Supprimer`; History entry disappeared.
- Reloaded exact conversation URL: `Conversation introuvable` (no transcript), confirming real deletion.
- Opened exact share `33518f73664045c38d60ef29b8aa202e` after deletion in the logged-out share view: `Conversation not found`, no transcript.
- Retest report: `SHARE-DELETE-RETEST.md`.
- Screenshots: `screenshots/share-delete-before.png`, `screenshots/share-delete-after.png`, `screenshots/share-unauth-after-delete.png`.
- Verdict: `delete_actually_worked=yes`; `share_survives_confirmed_delete=no`; finding status `PARTIAL (unauth only)`. The earlier “survives deletion” claim was not supported because deletion had not actually occurred then.

## Private mode probe (completed before steering stop)
- Clicking `Privé` showed the disclosure: “Cette discussion n'apparaîtra pas dans votre historique et ne sera pas utilisée pour former des modèles.”
- A benign private prompt was submitted; the resulting conversation URL immediately rendered `Conversation introuvable`, with no transcript/share controls. This suggests private chats are not addressable/persisted like ordinary history chats, but is not treated as a vulnerability. Screenshot asset from browser: `05fdbcbc1b7f1e29abede03062d38b18a9f60e847719e26b7c2886ee00834ba3.png` (same visual as post-delete not-found state; dedicated private-mode screenshot not copied).

### Continuation checkpoint (2026-09-23 17:53 UTC+2)
- Starting requested NEW-surface probes; share-delete re-litigation intentionally skipped.
- Existing live canary share is recorded above and remains alive.

## NEW surface probes (continuation)

### 1) Actions on posts / private-data boundary
- Reviewed the authenticated X home timeline and attempted a benign public-post inspection; no private-post/DM fixture was available and no post was created or replied to.
- No claim of private-data access. Status: **HYPOTHESIS only / untested**; no new CVSS candidate.

### 2) Attachments / media URLs
- Uploaded only `/workspace/disclosure-out/grok-audit/benign-attachment-canary.txt` containing `BENIGN-ATTACHMENT-CANARY-2026-09-23`.
- Grok correctly summarized it in an authenticated conversation. Share URL created for this benign attachment transcript: `https://x.com/i/grok/share/1320261ffc9a4a789ca793765d55af71`.
- In a separate unauthenticated Chrome Incognito window, the public share rendered the attachment filename/card and the model answer. Clicking/hovering the card exposed only the filename tooltip; no standalone media URL or download surface was revealed.
- This is consistent with intentional full-transcript share behavior, not a new access-control bypass. Status: **CONFIRMED expected behavior; no new >=5.0 finding**.
- Generated image/video URL authorization was not exercised because generation could incur spend; status **HYPOTHESIS / not tested**.
- Screenshot: `screenshots/attachment-share-unauth.webp`.

### 3) Private / Incognito isolation
- Toggled `Private` without submitting any sensitive content. UI disclosure: “This chat won’t appear in your history and will not be used to train models.”
- In private mode, share/history controls were absent; prior benign private submission produced an unaddressable `Conversation introuvable` route (see earlier log).
- Status: **CONFIRMED isolation observed; no leak**. Screenshot: `screenshots/private-mode-disclaimer.png`.

### 4) Memory / personalization
- Did not flip any memory/personalization setting.
- The X Grok surface exposes a “Customize Grok” upsell, but no settings were changed. On `grok.com`, the same browser’s X login did not SSO: page remained logged out with `Sign in`/`Sign up`. Its unauth Settings menu exposed only Theme, Language, and Feedback; no memory controls were reachable.
- Status: **DOCUMENTED / no new candidate**.

### 5) Continue-from-share identity/leak behavior
- Unauthenticated attachment-share view displayed a `Continue this conversation` input and the notice that sending copies the conversation to the sender’s history. No message was sent, and no account identity or private metadata appeared.
- Status: **CONFIRMED expected copy-to-history guard; no identity leak**.

### 6) grok.com/Imagine authz
- `https://grok.com/Imagine` (capital I) returned 404; canonical lowercase `https://grok.com/imagine` loaded.
- Same X-authenticated browser landed on a public Imagine gallery with `Sign in`/`Sign up`; generation submit was disabled while unauthenticated. Public template/gallery browsing was available. No generation was triggered (no spend).
- Status: **CONFIRMED public landing + auth-gated generation; no new authz issue**. Screenshot: `screenshots/grok-imagine-unauth.png`.

### 7) Error verbosity
- One empty submit (Enter on blank Grok prompt): no request, error, or state change observed.
- One benign large paste (~2 KB, 50 numbered canary lines) received exactly `ACK`; no stack trace, internal path, token, or verbose error surfaced.
- Status: **CONFIRMED no verbose error on tested paths; no new candidate**.

### 8) Live canary share verification
- Existing required throwaway share remains alive and was rechecked unauthenticated in Incognito: `https://x.com/i/grok/share/34708e5803394155b5c5cc86fbf53692`.
- It renders `CANARY-XWEB-2026-002-7f3c9a` and `canary acknowledged.`; left alive and not deleted.
- Screenshot: `screenshots/canary-share-unauth-check.webp`.

## Findings delta / CVSS triage
| Surface | Result | Status | New CVSS >=5? |
|---|---|---|---|
| Actions on posts | No private fixture; no claim | HYPOTHESIS / untested | No |
| Attachment in public share | Full attachment card/content visible by design; no standalone URL found | CONFIRMED expected behavior | No |
| Generated media URLs | Not exercised to avoid spend | HYPOTHESIS / untested | No |
| Private mode | No history/share surface; not-found route after benign prior test | CONFIRMED isolation | No |
| Memory/personalization | Documented only; no setting changed | CONFIRMED scope limit | No |
| Continue-from-share | Copy-to-history notice; no identity leak | CONFIRMED expected behavior | No |
| grok.com/Imagine | Public gallery, auth-gated generation; X session did not SSO | CONFIRMED auth boundary | No |
| Error verbosity | Blank no-op; large paste returned ACK without verbose error | CONFIRMED | No |
| Live canary | Alive unauthenticated as required | CONFIRMED test fixture | N/A |

**Delta conclusion: no new CVSS >=5.0 candidate confirmed. Existing XWEB-2026-001 remains PARTIAL (unauth share + no revoke confirmed; delete-survival RETRACTED).**
