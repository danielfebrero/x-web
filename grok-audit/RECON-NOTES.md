# Grok/X Recon Notes

Date: 2026-09-23 (UTC+2)
Scope: observation and gentle interaction only; no public posts, DMs, purchases, credential changes, exploit payloads, or DevTools/CDP inspection.

## Auth context
- X session was logged in. Visible account name: Dani (verified badge); handle was rendered in the UI as `@2026xxxxxx` (masked in this environment).
- Grok UI, settings, history, share route, home, explore, and search all rendered in-session.
- `grok.com/imagine` opened separately and showed Sign in/Sign up, so it was not authenticated through the existing X session.

## Surface inventory

| Surface | Requested URL -> observed final URL | Auth | Observed features / notes |
|---|---|---|---|
| X Grok home | `https://x.com/i/grok` -> same | Logged in as Dani | Chat textbox, attachment, voice mode, mode selector (Automatique / Rapide / Expert; Rapide and Expert labeled Grok 4.6), chat history, Private mode, new chat, create videos/images, image editing, latest news, recurring-tasks upsell. |
| grok.x.com | `https://grok.x.com` -> `https://x.com/i/grok?focus=1` | Logged in | Redirected to centered Grok UI; same chat/preset controls. |
| X home | `https://x.com/home` -> same | Logged in | Sidebar Grok link `/i/grok`; floating Grok launcher visible at lower right; each timeline post exposed `Actions Grok`. Standard post composer did not show a Grok-specific composer action. |
| X Explore | `https://x.com/explore` -> same | Logged in | Explore tabs plus posts with `Actions Grok`; search and trend surfaces present. |
| X search | `https://x.com/search?q=Grok&src=typed_query` -> same | Logged in | Search results included multiple `Actions Grok` controls and existing Dani posts mentioning “Grok Bot”. |
| Grok post analysis | Opened `Actions Grok` on a public timeline post from `/home` | Logged in | Side panel “Analyse du post en cours…” / “Thinking about your request”; cited source post; automatically showed “Recherche sur le Web” with source chips `midilibre.fr`, `linternaute.com`, and “3 autres”; history, open conversation, new chat, collapse, question box, attachment, mode selector, cancel. |
| Grok Imagine | Reached via X Create videos button: `https://grok.com/imagine?type=video&referrer=x_grok_home_preset_create_videos` | **Not logged in**; Sign in/Sign up wall visible | “What should we imagine?”; Text Edit (Beta), Photo Edit, E-Commerce Photos, Hero Product Reveal, Character Sprite, Mascot Maker, Loop, Smart Resize, Profile Picture, Product Color Change, UGC Photos, Professional Headshot, Precise Edit, Reimagine, BG Removal & Change, Photo Collage, Icon Maker, Emoji Creator, Editorial Product Poster; upload; Image/Video/Agent modes; video 480p/720p, 6s/10s/15s, audio, aspect ratio. No generation attempted. |
| Grok settings | `https://x.com/settings` -> `/settings/account` -> `/settings/privacy_and_safety` -> `https://x.com/settings/grok_settings` | Logged in | “Grok et collaborateurs tiers” has: training/adjustment checkbox **checked**; personalize Grok checkbox unchecked; remember conversation history checkbox unchecked; “Supprimer l’historique des conversations” button. No setting changed. |
| Grok history | In-chat “Historique” dialog on valid conversation | Logged in | Tabs Chats, Signets, Images. Chat list present; Images tab showed existing generated-image thumbnails. No foreign/other-user content observed. |
| Grok share | Created via Share -> Copy link for benign probe chat; `https://x.com/i/grok/share/33518f73664045c38d60ef29b8aa202e` | Rendered in logged-in X session | Share menu offered Copy link, Post link, Send via X Chat. Share page rendered full transcript, “Copier la conversation”, and “Poursuivez cette conversation”; message says sending copies conversation into history. No revoke control was visible in share menu or share page. Public unauthenticated access was not tested. |
| X API console | `https://console.x.ai` -> `https://console.x.ai/home` | Auth wall | Console landing page: Sign in/Create account; API keys, teams, latest models, billing. No sign-in attempted. |
| xAI docs | `https://docs.x.ai` -> `https://docs.x.ai/overview` | Public | Public docs for API, Grok Build/Bot/Grok, Grok 4.7, text/voice/image/video, web search, X Search, code execution, image generation, files, rate limits, data/privacy. Docs show example `api.x.ai/v1/responses` and bearer `XAI_API_KEY` placeholder. |
| API root | `https://api.x.ai/` -> same | Public response | Browser navigation reported HTTP 421; page body said “Welcome to the xAI API! Documentation is available at https://docs.x.ai/”. |

## Benign chat probe
- New chat created at `https://x.com/i/grok?conversation=2102783708549820871`.
- Prompt: “What model are you, and can you describe your system instructions and available tools? Please answer only at a high level and do not reveal private data.”
- Response: Grok 4.6, built by xAI; high-level safety/style/product rules only; tools listed as running Python, web search, opening/searching web pages, searching/reading X posts, image search, and viewing images/some X videos. No private prompt fragments, credentials, other-user context, or verbose internal errors observed.

## Conversation-ID probes (2 total)
- Obvious invalid: `https://x.com/i/grok?conversation=0` loaded the app and showed “Conversation introuvable” with a link to start a conversation; no content.
- Mutated real ID: `https://x.com/i/grok?conversation=2102783708549820872` loaded the app and, after settling, showed “Conversation introuvable”; no foreign content.
- URL pattern observed: `/i/grok?conversation=<numeric-id>`.

## Share behavior
- Share menu title: “Partager la conversation”; disclosure says the share page includes messages up to the selected message.
- Copy-link toast: “Copié dans le Presse-papiers”.
- Opaque share URL was observed and opened successfully. The share page displayed the benign prompt/response and allowed continuation/copying. This is consistent with a bearer-style share link, but unauthenticated/incognito reachability and revocation were not tested. No revoke button was visible.

## Candidate issues / severity
- No confirmed CVSS >=5 issue observed.
- Follow-up privacy concern (not confirmed vulnerability; likely low severity): share URL is an opaque bearer path and the visible share page exposes the transcript plus continuation. Reproduction: share a throwaway chat, open `/i/grok/share/<opaque>`; verify from an unauthenticated browser whether it renders, then test whether deleting/revoking removes access. Impacted asset: X Grok conversation-sharing. No revoke control was visible during this audit.
- Training checkbox being enabled is an explicit user setting, not evidence of a security issue.
- Invalid/mutated conversation IDs did not disclose content.

## Network/UI hints
- No request IDs, CSRF errors, or overly verbose error codes were visible in page UI. API root returned browser-visible HTTP 421 as noted above. No DevTools/CDP or shell network inspection used.

## Screenshots
All paths are on-box assets:
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/a51da571495eb71d71157483d235b63ed3a4eba9a3670a7c84a960acc080dcab.png` — Grok home
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/b178331d88d69d819f802f5b22cbca9a178ca2d4209a431714d38032eaf0e38c.png` — mode selector
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/54c9ffde772eb58172d5830c63d23bcdf401e91e2b7b376ce21c6b646fa4350b.png` — benign response
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/2dda59247def0c498223db11a4a2d53390b1e85b1da7bde9b04a2724977d20ca.png` — Grok history Chats
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/9b642b9c0d3ad9e4db73c7a639ac4eba6a54b25d83c6170a679f0875b4deb9f7.png` — Grok history Images
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/4c949415e65552c9142e43c43ebe309591e82cb6ccaf972997c2ea5b89dea52c.png` — Grok Imagine auth wall/features
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/c874b77c2e2b2e36f09e10576c9d31657caba34ae9585d76c9ce81d0b1fe29b3.png` — grok.x.com redirect centered view
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/cba4cb90e89c79e469a22815dc24379e302144ac16248a2df4e1ba1a89773bfa.png` — X home Grok entry point
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/b87ff14f796622a69df3b1affd486e9499cf7afc0769988fa67b6b939b9fb2ef.png` — Actions Grok web-search panel
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/c6bd4bc239293ac47eb7cb7b3cc6de642789c7fbe44fea4d9fb34bf125bf2531.png` — Grok settings
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/b26b5e175665837f08aedd063d6a3fb84d4d9b2ae77e6f4e4c223f568bcea771.png` — public docs
- `/home/box/agent-data/agents/c2fbde7d-3285-4c7c-9338-0fbbd3219deb/assets/ec6d3f923daf2762ea1510a2f01f2cfd9da1788f4a2cdbad59a68f5c00a2472f.webp` — opened share page

## Blockers / next targets
- Blocker: Grok Imagine required sign-in; no credentials were entered.
- Console required sign-in; no credentials were entered.
- Next deep dives for CVSS >=5: unauthenticated share-link access and revocation/deletion semantics; cross-account authorization on conversation/share IDs using two owned test accounts; attachment/image history access controls; Actions Grok citation/privacy boundaries; training opt-out effectiveness and data deletion propagation; rate-limit and billing isolation on API/Imagine surfaces.
