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

## Pass 3
Date: 2026-09-23 (UTC+2)
Scope: requested NEW surfaces only; UI observation and benign probes. No posts, DMs, purchases, credential changes, training-toggle changes, Elon DMs, DevTools/network automation, or API enumeration.

### Pass 3 probe results

1. **Grok Voice mode** — The authenticated X Grok composer exposed `Enter voice mode`. Clicking it produced the visible UI alert `Failed to connect to voice mode`; no voice session, transcript, history entry, or share surface was created. **CONFIRMED limitation / no retention-leak evidence; no new CVSS candidate.** Screenshot: `screenshots/pass3-voice-failed.png`.

2. **Recurring tasks / scheduled Grok** — The X Grok home UI displayed the `Create recurring tasks / Get access to more features on grok.com` upsell with `Explore` (a later refresh showed the localized equivalent `Parlez à Grok`). Clicking Explore opened `https://grok.com/?referrer=x`; the public landing was logged out with Sign in/Sign up and no task configuration. **CONFIRMED upsell only; no new CVSS candidate.** Screenshot: `screenshots/pass3-grok-home-upsell.png` (current localized upsell; the recurring-task wording was observed in the UI snapshot).

3. **Grok in Search/Explore side panel vs main chat** — Explore's floating Grok panel opened with `Private`, `Chat history`, and `Open conversation` controls. Main `/i/grok` exposed `History` and `Private`; no authz discrepancy or private fixture was available. No prompt was sent from the side panel. **CONFIRMED expected surface parity; no new CVSS candidate.**

4. **Same-user shared link / mutability** — In the same authenticated X session, live share `34708e5803394155b5c5cc86fbf53692` rendered the original two-message canary and the guard `Sending a message will copy this conversation into your history`; `Copy Conversation` was the only share action. A benign source edit was made in source conversation `2102787580286620032` (`PASS3-MUTABILITY-CHECK-20260923`, response `MUTABILITY-ACK-20260923`). Reloading the live share still showed only the original canary turns, not the new source turn. **CONFIRMED share is a static snapshot for this test; no unintended mutability or leak.** The required share was left alive. Screenshots: `screenshots/pass3-share-logged-in.png`, `screenshots/pass3-share-immutable-after-source-edit.png`.

5. **Share/conversation GraphQL/API** — No API endpoint or GraphQL detail was visible in a UI error. Per scope, **SKIPPED**; no DevTools/network automation.

6. **grok.com agents/projects/spaces** — The X recurring-task upsell linked only to unauthenticated `grok.com/?referrer=x`. No Agents, Projects, or Spaces link/control appeared. Unauthenticated Grok Settings exposed only Theme, Language, and Feedback. **CONFIRMED not reachable from linked surface; no new CVSS candidate.**

7. **Two random share-ID probes (only two)** — `5d4ce6c931f4d9485d8cd65d8011fe24` and `6d8ac2124d41797397bd14e29ac4204c` each rendered `Conversation not found` (the latter was checked after the former; no brute force). **CONFIRMED expected not-found behavior; no new CVSS candidate.** Screenshot: `screenshots/pass3-random-share-not-found.png`.

8. **Protected/locked account via Actions Grok** — No protected/locked-account fixture or private content was available. No claim was made and no protected-content action was attempted. **HYPOTHESIS / untested; no new CVSS candidate.**

9. **Download/export** — No Download or Export control was present. Source chat header offered share-link copy, bookmark, history, and new chat; share view offered `Copy Conversation` only. **CONFIRMED absent on tested UI; no new CVSS candidate.**

10. **`/settings/grok_settings` retest** — `Grok & Third-Party Collaborators` loaded, but both Settings and Section details panes showed `Something went wrong. Try reloading.` after retry and full reload. No data-download or third-party controls could be observed. **CONFIRMED UI error / controls unobservable; no new CVSS candidate.** Screenshot: `screenshots/pass3-settings-error.png`.

### Pass 3 triage table
| Surface | Observation | Status | New CVSS >=5.0? |
|---|---|---|---|
| Voice mode | Visible control; connection failed before session/transcript | CONFIRMED limitation | No |
| Recurring/scheduled tasks | Upsell only; linked to unauthenticated grok.com | CONFIRMED expected upsell | No |
| Explore side panel | Private/history/open-conversation controls; no authz discrepancy | CONFIRMED expected parity | No |
| Same-user share + source edit | Share stayed at original snapshot after benign source edit | CONFIRMED static snapshot | No |
| GraphQL/API | No visible UI error exposed endpoint details | SKIPPED by scope | No |
| grok.com agents/projects/spaces | No linked controls or links surfaced | CONFIRMED not reachable | No |
| Random share IDs (2) | Both not found | CONFIRMED expected | No |
| Protected account Actions | No fixture; not attempted | HYPOTHESIS / untested | No |
| Download/export | No control observed | CONFIRMED absent | No |
| Grok settings | Both panes error after retry/reload | CONFIRMED UI error | No |

**Pass 3 conclusion: no new CVSS >=5.0 candidate confirmed. Existing XWEB-2026-001 remains PARTIAL (unauthenticated share + no revoke confirmed; delete-survival retracted).**

### Pass 3 canary final check
- Rechecked both required live shares in the authenticated X session after all probes: `34708e5803394155b5c5cc86fbf53692` still rendered the original canary snapshot, and `1320261ffc9a4a789ca793765d55af71` still rendered the benign attachment card/content. Both were left alive. Screenshot: `screenshots/pass3-canary-attachment-logged-in.png`.
