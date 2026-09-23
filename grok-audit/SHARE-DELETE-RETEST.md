# XWEB-2026-001 share-delete re-test
Date: 2026-09-23 (UTC+2)

## Exact lab URLs
- Conversation: https://x.com/i/grok?conversation=2102783708549820871
- Share: https://x.com/i/grok/share/33518f73664045c38d60ef29b8aa202e

## Results
- `delete_actually_worked`: **yes**
- `share_survives_confirmed_delete`: **no**
- `finding_claim_status`: **PARTIAL (unauth only)**

## Procedure and evidence
1. Opened the exact conversation URL while logged in as Dani. It rendered the prior benign prompt/response (“What model are you…”), confirming the conversation still existed. Screenshot: `screenshots/share-delete-before.png`.
2. Opened Grok History. The exact entry `Grok 4.6 xAI Tools Overview` mapped to conversation `2102783708549820871`.
3. Used that history entry’s `Plus` menu → `Supprimer` (Delete). The entry disappeared from History.
4. Reloaded the exact conversation URL. It rendered `Conversation introuvable` with no transcript. Screenshot: `screenshots/share-delete-after.png`.
5. The exact share URL was then opened in the existing browser tab, which displayed logged-out X chrome and `Conversation not found`; no transcript rendered. Screenshot: `screenshots/share-unauth-after-delete.png`.

## Honest interpretation
The earlier claim that the share survived deletion was not reproduced because the source conversation had not actually been deleted at that time. This retest shows a real History deletion invalidated the source conversation and the share URL (at least for the unauthenticated view tested). The separate bearer-link observation—an existing opaque share URL can expose a transcript to a logged-out visitor while the source exists—remains the portion supported by prior evidence; deletion persistence must be removed from the claim.
