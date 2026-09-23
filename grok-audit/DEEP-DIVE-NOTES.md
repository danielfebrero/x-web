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

## Pass 4
Date: 2026-09-23 (UTC+2)
Scope: requested new angles only; benign owned canaries, UI observation, one tiny PNG, and one X OAuth consent preview. No posts/replies sent, no generation, no purchases, no credentials, no OAuth authorization, and no private/foreign conversation probing.

### Pass 4 probe results

1. **Grok in post composer / reply surface** — Direct `/compose/post` and the home composer exposed only the normal post textbox/actions; no “Grok” or “reply with Grok” affordance was present. A public post detail showed the reply control disabled in this session. No draft text was entered or sent. **CONFIRMED absent/unavailable; no draft-leak evidence; no new CVSS candidate.**

2. **Imagine / image-edit SSO** — Clicked Grok Imagine `Sign in` once, then `Login with X` once. X displayed the OAuth consent preview: xAI requested profile/account/settings/preferences, visible posts (including protected posts the user can see), and X Grok conversation history. Cancel was used; the flow ended at `Could not log in`. No credentials, approval, generation, or spend occurred. **CONFIRMED consent gate; no new CVSS candidate.**

3. **Tiny PNG upload and CDN authorization** — Uploaded a one-pixel PNG canary to a new owned chat `2102792238535418113`; Grok returned `Empty`. Browser `Copy image address` exposed `https://ton.x.com/i/ton/data/grok-attachment/2102792189419937793`. Opening that exact URL in a fresh Incognito window returned HTTP 401, not the image. **CONFIRMED authenticated-only attachment URL; no world-readable media leak; no new CVSS candidate.** Screenshot: `screenshots/pass4-image-cdn-unauth-401.png`.

4. **Multi-tab share/delete race (new fixture)** — Created share `https://x.com/i/grok/share/90b31da7a7c94acb8d9d0bcb72cd4be5` for the PNG chat, opened it, deleted the source through History, then refreshed the already-open authenticated share view. That already-open view still showed the static snapshot. The source URL was `Conversation not found`; a fresh Incognito load of the new share returned `Conversation not found`. **CONFIRMED no unauthenticated post-delete read in the fresh load; the authenticated pre-open view remained a static/share-session artifact consistent with the existing share-link/no-revoke behavior, not a new issue.** Screenshots: `screenshots/pass4-share-race-auth-view.png`, `screenshots/pass4-share-race-unauth-not-found.png`.

5. **Share referrer / identity** — From a fresh Incognito `about:blank`, opened live canary `34708e5803394155b5c5cc86fbf53692`. Transcript rendered, but no user ID, handle, or referrer identity appeared; only the standard logged-out Log in/Sign up footer was visible. **CONFIRMED no identity leak.** Screenshot: `screenshots/pass4-canary-referrer-unauth.png`.

6. **Live canary recheck** — Fresh Incognito rechecked both required canaries. `34708e5803394155b5c5cc86fbf53692` still showed the canary transcript; `1320261ffc9a4a789ca793765d55af71` still showed the benign attachment filename/content and answer. Both were left alive. Screenshot: `screenshots/pass4-canary-attachment-unauth.png`.

7. **Premium / SuperGrok gates** — X Grok’s mode menu showed `Auto — Chooses Fast or Expert`, `Fast — Quick responses · Grok 4.6`, `Expert — Thinks hard · Grok 4.6`, and `Go to grok.com`. The visible card said `Customize Grok — Get access to more features on grok.com`. No explicit Premium/SuperGrok paywall was exposed and no paid action was attempted. **DOCUMENTED UI gate only; no new CVSS candidate.** Screenshot: `screenshots/pass4-grok-access-gates.png`.

8. **Conversation URL parameters** — No clearly-404, not-owned public conversation ID was available to test safely. Prior invalid/mutated-ID probes are already recorded; no friend/private IDs were probed. **SKIPPED by safety/scope; no new candidate.**

9. **Chrome extension / deeplink hints** — No extension, Chrome, plugin, or deeplink affordance appeared in the inspected X Grok UI. **CONFIRMED not surfaced; no new candidate.**

10. **Public x.ai debug-endpoint review** — `https://x.ai/` and `https://x.ai/grok` were reviewed, including their public footer. Links were ordinary Products/Solutions/Developer/Console/Docs/Status/Changelog/Legal/Trust destinations; no debug endpoint or internal admin route was linked. **CONFIRMED public navigation only; no new candidate.** Screenshot: `screenshots/pass4-xai-grok-footer.png`.

### Pass 4 triage table
| Surface | Observation | Status | New CVSS >=5.0? |
|---|---|---|---|
| Post composer / reply | No Grok composer affordance; reply disabled; no draft sent | CONFIRMED absent/unavailable | No |
| Imagine SSO | One X OAuth consent preview; canceled; no auth completed | CONFIRMED gate | No |
| Tiny PNG media URL | `ton.x.com` URL returned HTTP 401 in fresh Incognito | CONFIRMED authz | No |
| New share/delete race | Fresh unauth load after source deletion was not found; pre-open auth view stayed static | CONFIRMED expected/share artifact | No |
| Share from about:blank | Canary transcript showed no user ID/handle | CONFIRMED no identity leak | No |
| Live canaries | Both alive and rechecked unauthenticated | CONFIRMED fixtures | N/A |
| Premium/SuperGrok | Mode selector/`Get access to more features on grok.com` card only | DOCUMENTED gate | No |
| URL params | No safe foreign public ID available | SKIPPED | No |
| Extension/deeplink | None surfaced | CONFIRMED absent | No |
| x.ai public pages/footer | No debug endpoint links | CONFIRMED public-only | No |

**Pass 4 conclusion: no new CVSS >=5.0 finding confirmed. Existing XWEB-2026-001 remains the only tracked item at PARTIAL (unauthenticated share + no revoke). No findings file or ALERTS.md entry was created because the pass produced no new qualifying finding.**

## Pass 5
Date: 2026-09-23 (UTC+2)
Scope: requested new angles only; owned live canaries, visible UI/source inspection, one public third-party share, one adjacent-ID mutation, and native clipboard paste. No posts/replies, no DMs, no spend, no OAuth approval, no credentials, no DevTools/network automation. Both required live shares were left alive.

### Pass 5 probe results

1. **Mobile share surface** — Resized the share view to 390x800 and checked both live canaries. The mobile layout showed the same transcript/attachment content, a compact copy-conversation icon, and the normal continue field; no owner handle, extra metadata, or different revoke control appeared. Screenshots: `screenshots/pass5-mobile-canary.png`, `screenshots/pass5-mobile-canary-attachment.png`.

2. **Visible page source / rendered HTML** — Opened View Source for the live canary in the visible browser UI. The visible source showed the SPA shell/styles but no visible `user_id`, `screen_name`, email, or internal-owner fields; searches for `email`, `screen_name`, `user_id`, and `robots` returned no matches in the visible source snapshot. No suspicious field was present to screenshot. Source screenshot: `screenshots/pass5-view-source.png`.

3. **Bookmark from Grok History** — Grok History listed the owned attachment conversation with bookmark icons and no share-status badge. Clicking its bookmark added it to the Grok History `Signets` tab; the item remained an account-local history/bookmark entry and did not create a public share artifact. Screenshot: `screenshots/pass5-history-bookmark.png` (list screenshot: `screenshots/pass5-history-list.png`).

4. **Copy Conversation / clipboard** — On the share view, `Copier la conversation` navigated to an owned history copy (expected copy-to-history behavior), rather than exposing owner metadata. Pasting into a native blank Writer note yielded only the pre-existing clipboard string `https://x.com/i/grok/share/90b31da7a7c94acb8d9d0bcb72cd4be5` from an earlier probe; it contained no owner metadata or chat turns. This was not treated as a new issue because the clipboard value was stale and unrelated to the current share action. Screenshot: `screenshots/pass5-copy-clipboard.png`.

5. **Grok History indicators** — The visible History panel showed chat titles, bookmark icons, and `Plus` menus only. No shared-status badge, revoke action, or public-share indicator appeared for the canary entries. Screenshot: `screenshots/pass5-history-list.png`.

6. **Docs / Help / Feedback entry points** — The public `grok.com` Settings menu exposed only Theme, Language, and Feedback. Feedback opened a `Report content` dialog with reason/text/attachments and a disabled Send button; no Docs, Help, admin, or debug link appeared. No report was submitted. Screenshot: `screenshots/pass5-feedback.png`.

7. **Public third-party share** — X search for `/i/grok/share/` surfaced one public post by `@ItsFullOfFellas` linking `https://x.com/i/grok/share/T9mQGgLaX102J610y07DCCcka`. Viewing the share exposed the transcript and a `Copy Conversation` control, but no owner handle, user ID, email, or other share-owner identity to logged-out viewers. Screenshot: `screenshots/pass5-third-party-share.png`.

8. **Adjacent-ID mutation in Incognito** — In a fresh Incognito window, changed exactly one adjacent hex digit in live canary `...53692` to `...53693`. Result was `Conversation not found`; no transcript or metadata appeared. Screenshot: `screenshots/pass5-adjacent-not-found.png`.

9. **Robots/noindex** — The visible View Source inspection found no visible `meta robots`/`robots` text. This is a source-observation result only, not a network/header claim.

10. **Required Incognito canary recheck** — Fresh Incognito loads of both live canaries succeeded: `34708e5803394155b5c5cc86fbf53692` showed the canary transcript, and `1320261ffc9a4a789ca793765d55af71` showed the benign attachment filename/content and answer. Both were left alive. Screenshots: `screenshots/pass5-canary-unauth.png`, `screenshots/pass5-canary-attachment-unauth.png`.

### Pass 5 triage table
|| Surface | Observation | Status | New CVSS >=5.0? |
||---|---|---|---|
|| Mobile share view | Same transcript/attachment; no owner metadata or revoke UI | CONFIRMED expected responsive surface | No |
|| Visible source / DOM text | No visible email, screen_name, user_id, or robots text | CONFIRMED no suspicious field | No |
|| Bookmark | Added to private Grok History Signets; no public artifact | CONFIRMED account-local behavior | No |
|| Copy Conversation / clipboard | Created history copy; native paste showed stale prior share URL only | CONFIRMED expected/negative | No |
|| Grok History indicators | Bookmark/Plus only; no shared/revoke badge | DOCUMENTED | No |
|| Settings / Feedback | Report-content form only; no Docs/Help/admin/debug link | CONFIRMED | No |
|| Public third-party share | Transcript visible; owner identity not exposed | CONFIRMED no identity leak | No |
|| One adjacent ID in Incognito | `...53693` returned Conversation not found | CONFIRMED expected | No |
|| Robots/noindex | No visible robots meta text in source snapshot | INCONCLUSIVE source-only observation | No |
|| Live canaries | Both rechecked unauthenticated and left alive | CONFIRMED fixtures | N/A |

**Pass 5 conclusion: no new CVSS >=5.0 issue confirmed. No findings file or ALERTS.md entry was created. Existing XWEB-2026-001 remains the only tracked item at PARTIAL (unauthenticated share + no revoke).**

## Pass 6
Date: 2026-09-23 (UTC+2)
Scope: requested new angles only; benign owned canary, one Incognito share observation, local iframe framing observation, alternate-host/auth-wall review, visible View Source inspection, and final Incognito canary recheck. No exploit payloads, posts, DMs, purchases, OAuth approval, credential entry, or enumeration.

### Pass 6 probe results

1. **Share HTML/markdown rendering (owned canary)** — Created new owned conversation `2102797202322018700` and sent exactly one benign marker message containing literal `<b>`, `<script>/*inert*/</script>`, `![x](javascript:alert(1))`, and `[safe](https://example.com)`, asking for a verbatim ACK. Share URL: `https://x.com/i/grok/share/fee24b38028147deb627c10fcd70e683` (left alive). Authenticated source view showed the markers as text; the safe markdown became an ordinary `https://example.com` link, while the image/javascript marker did not execute. Fresh Incognito share view showed the same escaped/plain rendering, with no alert, script execution, or HTML injection observed. **CONFIRMED escaped/plain rendering; no new CVSS >=5 candidate.** Screenshots: `pass6-source.png`, `pass6-share-xss-unauth.png`.

2. **Iframe / clickjacking surface** — Created and opened `/workspace/disclosure-out/grok-audit/pass6-iframe-test.html`, which embeds the new owned share URL in a plain iframe. The iframe area rendered Chrome’s blank/broken-document state and the share did not load inside the frame. This is a framing-block/failed-load observation only; no header claim was made. **CONFIRMED framed load blocked/failed; no new CVSS >=5 candidate.** Screenshot: `pass6-iframe-blocked.png`.

3. **Alternate hosts** — `https://grok.com/` remained logged out with `Sign in`/`Sign up`; no Share UI or distinct grok.com share link was visible. Direct `https://grok.com/grok` returned a 404. `https://grok.x.ai` redirected to the public `https://x.ai/` SpaceXAI marketing site, whose visible links exposed ordinary product/chat/API/docs destinations and no distinct share UI. **DOCUMENTED auth wall/redirect; no new candidate.**

4. **Actions on posts ACL** — No Actions/Grok affordance for an owned recent public post surfaced in the tested logged-in X UI; no post was opened and no private/protected content was used. **ABSENT/UNAVAILABLE; no new candidate.**

5. **Share ID entropy note** — The two live canaries and the new Pass 6 share IDs are each 32 characters using lowercase hexadecimal (`34708e5803394155b5c5cc86fbf53692`, `1320261ffc9a4a789ca793765d55af71`, `fee24b38028147deb627c10fcd70e683`). No enumeration was performed beyond the one already-done adjacent-ID check recorded in Pass 5.

6. **CSP / meta from View Source** — Visible View Source for the new share contained the SPA shell and ordinary meta tags, but no `Content-Security-Policy` string/meta was present in the inspected source. This is a source-only observation, not a response-header claim. Screenshot: `pass6-view-source.png`.

7. **Required final Incognito canary recheck** — Fresh unauthenticated Incognito recheck at the end succeeded for both required live canaries: `34708e5803394155b5c5cc86fbf53692` showed the original canary transcript, and `1320261ffc9a4a789ca793765d55af71` showed the benign attachment card/content and answer. Both were left alive. Screenshot: `pass6-live-canary-attachment-unauth.png`.

### Pass 6 triage table
|| Surface | Observation | Status | New CVSS >=5.0? |
|---|---|---|---|
|| Share HTML/markdown | Markers rendered escaped/plain; safe link ordinary; no script/alert | CONFIRMED safe rendering | No |
|| Iframe framing | Plain iframe showed blank/broken-document state; share did not load | CONFIRMED blocked/failed frame load | No |
|| grok.com / grok.x.ai | Logged-out/auth wall; grok.x.ai redirected to x.ai public site; no distinct Share UI | DOCUMENTED | No |
|| Actions on owned public posts | No affordance surfaced; no post/private content used | ABSENT/UNAVAILABLE | No |
|| Share ID format | Three visible share IDs are 32-char lowercase hex | DOCUMENTED entropy note | No |
|| View Source CSP/meta | No CSP meta/string visible; source-only result | INCONCLUSIVE source-only observation | No |
|| Required live canaries | Both rendered in final unauthenticated Incognito check and remain alive | CONFIRMED fixtures | N/A |

**Pass 6 conclusion: no new CVSS >=5.0 issue confirmed. Existing XWEB-2026-001 remains the only tracked item at PARTIAL (unauthenticated share + no revoke).**
