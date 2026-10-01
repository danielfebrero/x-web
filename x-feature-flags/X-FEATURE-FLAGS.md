# X (x.com) Web Feature Flags Reference

> *Référence complète des feature flags (feature switches) de l'app web X, capturés le 2026-10-01 depuis un compte connecté.*

## 1. Source, capture & statistics

- **Source:** `window.__INITIAL_STATE__.featureSwitch` of the signed-in web app at `https://x.com/home` (`defaultConfig` = server default per flag, `user.config` = value resolved for the captured account). Raw capture: [`feature-switches-2026-10-01.json`](feature-switches-2026-10-01.json).
- **Capture time:** 2026-10-01T11:42:14.821Z (2026-10-01 13:42 Paris time, CEST).
- **Baseline for the diff:** capture of 2026-09-23 (1384 default flags / 1385 user flags).
- **Total flags:** **1424** (defaultConfig and user config contain exactly the same keys).
- **Types:** bool **1125** · int **155** · str **106** · list **29** · float **9**
- **Boolean values (this account):** `true` **648** · `false` **477** (non-boolean parameters: 299). Boolean defaults: `true` 599 · `false` 526.
- **Deviations default → this account:** **58** flags have a user value different from the default (marked with ⚠ below).
- **Experiment buckets recorded for this account** (`featureSwitch.user.impressions`): `adblock_fyp_timeline_detection_18915` = control (v4), `timeline_pointer_events_19084` = treatment (v5), `web_route_preloading_18967` = treatment (v1); linked flags: `new_timeline_experiment_enabled`, `timeline_scroll_pointer_events_optimization`, `responsive_web_primary_nav_route_preload_enabled`.

### Honesty note / how to read this document

- X **does not publish** any documentation for these flags. **Every description below is inferred** (labelled "Inferred") from the flag name, the shape of its value and, where applicable, general knowledge of the x.com web bundles. Nothing here is an official statement; some inferences may be wrong or outdated.
- Where the purpose could not be inferred confidently, the description starts with "Purpose unclear from name; likely …".
- **Rollout percentages, targeting rules and experiment allocations are NOT exposed** in the captured objects: only the default value and the value resolved for one account are visible. "Deviation" means this account got a value different from the default; it does not tell how many other users are in the same cohort.
- Several flags are mobile-/TV-oriented or internal; they are shipped in the same payload but may have no effect on the web UI.
- Values that look like keys, tokens or identifiers (Arkose site IDs, Castle public key, media keys, snowflake-like IDs, recipient IDs in URLs) are replaced with `[redacted]`. Long lists are truncated to a preview with the item count.
- Column legend: **Default** = `defaultConfig` value; **This account** = resolved user value; ⚠ marks default ≠ user value; 🆕 marks flags absent from the 2026-09-23 capture.

## Contents

- [Grok / AI](#grok--ai) (160)
- [XChat / DMs / Calls](#xchat--dms--calls) (188)
- [Payments / X Money](#payments--x-money) (37)
- [Verified Organizations / Business](#verified-organizations--business) (91)
- [Subscriptions / Premium](#subscriptions--premium) (207)
- [Ads / Promote](#ads--promote) (66)
- [Creator / Monetization / Analytics](#creator--monetization--analytics) (99)
- [Communities](#communities) (53)
- [Spaces / Live / Sports](#spaces--live--sports) (91)
- [Media / Video / Upload](#media--video--upload) (78)
- [Search / Explore / Trends / Topics](#search--explore--trends--topics) (28)
- [Timeline / Ranking / Home](#timeline--ranking--home) (63)
- [Community Notes / Trust & Safety / Moderation](#community-notes--trust--safety--moderation) (106)
- [Notifications](#notifications) (4)
- [Profile / Identity](#profile--identity) (21)
- [Compliance / Legal / Privacy / Cookies](#compliance--legal--privacy--cookies) (22)
- [Onboarding / Auth / Security](#onboarding--auth--security) (61)
- [Performance / Infra / Debug / Telemetry](#performance--infra--debug--telemetry) (35)
- [Misc](#misc) (14)
- [Appendix A — Deviations default → this account](#appendix-a--deviations-default--this-account)
- [Appendix B — Diff since 2026-09-23](#appendix-b--diff-since-2026-09-23)
- [Appendix C — Verification](#appendix-c--verification)

## 2. Flags by product area

### Grok / AI

160 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `content_disclosure_ai_generated_c2pa_detection_enabled` | bool | `true` | `true` | Enables C2PA metadata detection to flag AI-generated content. |
| `content_disclosure_ai_generated_creation_enabled` | bool | `true` | `true` | Enables creation-time AI-generated content disclosure labelling. |
| `content_disclosure_ai_generated_indicator_enabled` | bool | `true` | `true` | Shows the AI-generated content indicator on posts. |
| `content_disclosure_c2pa_detection_exemption_list` | list | `[Adobe Photoshop, Adobe Firefly, Canva AI]` (3 items) | `[Adobe Photoshop, Adobe Firefly, Canva AI]` (3 items) | List of editing tools exempted from C2PA AI detection (e.g., Photoshop, Firefly, Canva AI). |
| `content_disclosure_creation_enabled` | bool | `true` | `true` | Enables content-disclosure labels at creation time. |
| `content_disclosure_indicator_enabled` | bool | `true` | `true` | Shows the content-disclosure indicator on posts. |
| `graduated_access_botmaker_decider_enabled` | bool | `true` | `true` | Enables the Botmaker decider in graduated access (anti-abuse). |
| `grok_agent_disclosure_enabled` | bool | `false` | `false` | Enables disclosure that a Grok agent is acting. |
| `grok_created_with_grok_label_domains` | list | `[]` (0 items) | `[]` (0 items) | Domains eligible for the "Created with Grok" label (empty list). |
| `grok_created_with_grok_label_text` | str | `""` | `""` | Text for the "Created with Grok" label (empty). |
| `grok_created_with_grok_label_url` | str | `""` | `""` | URL for the "Created with Grok" label (empty). |
| `grok_settings_age_restriction_enabled` | bool | `true` | `true` | Enables age restriction in Grok settings. |
| `grok_settings_memory_visibility` | str | `"hide"` | `"show"` ⚠ | Controls whether the Grok memory setting is shown; this account sees "show" while default is "hide". |
| `grok_settings_restriction_age` | int | `18` | `18` | Minimum age enforced in Grok settings. |
| `grok_translations_community_note_auto_translation_is_enabled` 🆕 | bool | `false` | `false` | Enables Grok-based auto-translation of Community Notes. |
| `grok_translations_community_note_translation_is_enabled` 🆕 | bool | `false` | `false` | Enables Grok-based translation of Community Notes. |
| `grok_translations_post_auto_translation_is_enabled` 🆕 | bool | `false` | `false` | Enables Grok-based auto-translation of posts. |
| `grok_xweb_connectors_enabled` 🆕 | bool | `false` | `false` | Enables Grok connectors on the web. |
| `grok_xweb_skills_enabled` 🆕 | bool | `false` | `false` | Enables Grok skills on the web. |
| `responsive_web_grok_05221996` | bool | `false` | `false` | Purpose unclear from name; likely a dated Grok experiment gate (date-style suffix). |
| `responsive_web_grok_05231996` | str | `""` | `"imagine"` ⚠ | Purpose unclear from name; likely a string variant gate for Grok; this account has "imagine". |
| `responsive_web_grok_420_toggle_enabled` | bool | `false` | `false` | Enables the Grok 4.20 toggle. |
| `responsive_web_grok_allow_youtube_embeds` | bool | `false` | `false` | Allows YouTube embeds in Grok. |
| `responsive_web_grok_analysis_button_from_backend` | bool | `true` | `true` | Gets the Grok analysis button from the backend. |
| `responsive_web_grok_analyze_button_fetch_trends_enabled` | bool | `false` | `false` | Fetches trends for the Grok analyze button. |
| `responsive_web_grok_analyze_education_days_threshold` | int | `30` | `30` | Days threshold for Grok analyze education. |
| `responsive_web_grok_analyze_focal_post_enabled` | bool | `false` | `false` | Enables Grok analyze on the focal post. |
| `responsive_web_grok_analyze_post_followups_enabled` | bool | `false` | `true` ⚠ | Enables follow-ups for Grok post analysis; on for this account. |
| `responsive_web_grok_analyze_tooltip_delay_ms` | int | `2500` | `2500` | Delay (ms) for the Grok analyze tooltip. |
| `responsive_web_grok_analyze_tooltip_show_probability_percentage` | int | `20` | `20` | Probability (%) of showing the Grok analyze tooltip. |
| `responsive_web_grok_annotations_enabled` | bool | `true` | `true` | Enables Grok annotations. |
| `responsive_web_grok_api_enable_grok_host` | bool | `true` | `true` | Enables the Grok host in the API. |
| `responsive_web_grok_article_cover_image_gen_enabled` | bool | `false` | `false` | Enables Grok article cover image generation. |
| `responsive_web_grok_article_summary_enabled` | bool | `true` | `true` | Enables Grok article summaries. |
| `responsive_web_grok_article_voice_over_min_ios_version` | float | `11.72` | `11.72` | Minimum iOS version for Grok article voice-over. |
| `responsive_web_grok_atgrok_sample_rate` | float | `0.5` | `0.5` | Sample rate for @grok interactions. |
| `responsive_web_grok_backend_prompts_enabled` | bool | `true` | `true` | Enables backend-provided prompts in Grok. |
| `responsive_web_grok_bio_auto_translation_in_followers_enabled` | bool | `true` | `true` | Enables bio auto-translation in followers lists. |
| `responsive_web_grok_bio_auto_translation_in_search_is_enabled` | bool | `true` | `true` | Enables bio auto-translation in search. |
| `responsive_web_grok_bio_auto_translation_is_enabled` | bool | `true` | `true` | Enables bio auto-translation. |
| `responsive_web_grok_bot_preset_enabled` | bool | `false` | `false` | Enables a Grok bot preset. |
| `responsive_web_grok_bot_preset_title` | str | `""` | `""` | Title of the bot preset (empty). |
| `responsive_web_grok_build_tab_relabel_enabled` | bool | `false` | `false` | Enables relabeling of the Build tab in Grok. |
| `responsive_web_grok_community_note_auto_translation_is_enabled` | bool | `true` | `true` | Enables Grok auto-translation of Community Notes. |
| `responsive_web_grok_community_note_translation_is_enabled` | bool | `true` | `true` | Enables Grok translation of Community Notes. |
| `responsive_web_grok_debug_enabled` | bool | `false` | `false` | Enables Grok debug mode. |
| `responsive_web_grok_dev_universal_search_id_enabled` | bool | `false` | `false` | Enables the dev universal search id in Grok. |
| `responsive_web_grok_disable_new_conversation_url_reset` | bool | `false` | `false` | Disables resetting the URL on new conversation. |
| `responsive_web_grok_download_cta_copy` | str | `"open_grok"` | `"open_grok"` | Copy of the Grok download CTA ("open_grok"). |
| `responsive_web_grok_download_cta_enabled` | bool | `true` | `true` | Enables the Grok download CTA. |
| `responsive_web_grok_download_favicons` | bool | `true` | `true` | Downloads favicons in Grok. |
| `responsive_web_grok_edit_image_attribution_mode` | str | `"free"` | `"free"` | Attribution mode for edited images ("free"). |
| `responsive_web_grok_enable_android_image_donwload` | bool | `false` | `false` | Enables Android image download in Grok. |
| `responsive_web_grok_enable_deepersearch` | bool | `true` | `true` | Enables DeeperSearch in Grok. |
| `responsive_web_grok_enable_grok_analyze_education` | bool | `false` | `false` | Enables Grok analyze education. |
| `responsive_web_grok_enable_grok_tab_education` | bool | `false` | `true` ⚠ | Enables the Grok tab education; on for this account. |
| `responsive_web_grok_enable_video_gen_on_image_preview` | bool | `false` | `false` | Enables video generation from an image preview. |
| `responsive_web_grok_fade_in_animation_v2_enabled` | bool | `true` | `true` | Enables fade-in animation v2. |
| `responsive_web_grok_feed` | bool | `false` | `false` | Enables the Grok feed. |
| `responsive_web_grok_file_max_size` | int | `50000000` | `50000000` | Maximum file size (bytes, 50 MB) for Grok uploads. |
| `responsive_web_grok_file_upload_enabled` | bool | `true` | `true` | Enables file upload in Grok. |
| `responsive_web_grok_file_upload_max_files` | int | `15` | `15` | Maximum number of files per Grok upload. |
| `responsive_web_grok_fun_mode_disabled` | bool | `true` | `true` | Disables fun mode in Grok. |
| `responsive_web_grok_general_availability` | bool | `false` | `false` | Marks Grok as generally available. |
| `responsive_web_grok_highlighted_prompt_clicks_until_fatigue` | int | `-1` | `-1` | Clicks on highlighted prompts before fatigue (-1 means never). |
| `responsive_web_grok_home_dark_enabled` | bool | `true` | `true` | Enables dark mode on Grok home. |
| `responsive_web_grok_image_annotation_enabled` | bool | `true` | `true` | Enables image annotation. |
| `responsive_web_grok_image_edit` | bool | `true` | `true` | Enables image editing in Grok. |
| `responsive_web_grok_image_lazyload_enabled` | bool | `true` | `true` | Enables lazy-loading of images. |
| `responsive_web_grok_imagine_annotation_enabled` | bool | `true` | `true` | Enables annotations in Grok Imagine. |
| `responsive_web_grok_imagine_banner_config` | str | `""` | `""` | Banner config for Grok Imagine (empty). |
| `responsive_web_grok_imagine_composer_enabled` | bool | `false` | `true` ⚠ | Enables the Grok Imagine composer in the web app; on for this account but off by default. |
| `responsive_web_grok_imagine_continue_seamless_enabled` | bool | `true` | `true` | Enables seamless continue in Imagine. |
| `responsive_web_grok_imagine_explore_enabled` | bool | `false` | `false` | Enables Imagine in Explore. |
| `responsive_web_grok_imagine_image_comparison_enabled` | bool | `false` | `true` ⚠ | Enables image comparison in Imagine; on for this account. |
| `responsive_web_grok_imagine_in_composer_enabled` | bool | `false` | `false` | Enables Imagine inside the post composer. |
| `responsive_web_grok_imagine_native_share_enabled` | bool | `false` | `true` ⚠ | Enables native sharing of Imagine creations; on for this account. |
| `responsive_web_grok_imagine_profile_edit_enabled` | bool | `false` | `true` ⚠ | Enables Imagine profile editing; on for this account. |
| `responsive_web_grok_img_composer` | bool | `true` | `true` | Enables the Grok image composer. |
| `responsive_web_grok_img_composer_in_media_picker` | bool | `false` | `true` ⚠ | Shows the Grok image composer in the media picker; on for this account. |
| `responsive_web_grok_img_composer_redirect_to_grok_com_imagine` | bool | `true` | `true` | Redirects the image composer to grok.com/imagine. |
| `responsive_web_grok_imggen_count` | int | `4` | `4` | Number of images generated per request. |
| `responsive_web_grok_inplace_auth_handoff_enabled` | bool | `true` | `true` | Enables in-place auth handoff to Grok. |
| `responsive_web_grok_latest_news_preset_enabled` | bool | `true` | `true` | Enables the latest-news preset. |
| `responsive_web_grok_link_edit_image_to_grok_com_enabled` | bool | `true` | `true` | Links edit-image to grok.com. |
| `responsive_web_grok_location_enabled` | bool | `true` | `true` | Enables location use in Grok. |
| `responsive_web_grok_media_attribution_focal_post_force_show` | bool | `false` | `false` | Forces media attribution to show on focal post. |
| `responsive_web_grok_media_attribution_imagine_force_show` | bool | `false` | `false` | Forces Imagine media attribution to show. |
| `responsive_web_grok_media_attribution_route_to_imagine_composer` | bool | `false` | `true` ⚠ | Routes media attribution to the Imagine composer; on for this account. |
| `responsive_web_grok_media_block_edit_enabled` | bool | `true` | `true` | Blocks editing of media within Grok. |
| `responsive_web_grok_model_selector_in_input` | bool | `true` | `true` | Shows the model selector inside the Grok input box. |
| `responsive_web_grok_model_selector_in_input_min_android_version` | float | `11.71` | `11.71` | Minimum Android version for the in-input model selector. |
| `responsive_web_grok_outage_banner_message` | str | `""` | `""` | Message for a Grok outage banner (empty = none). |
| `responsive_web_grok_personality` | bool | `true` | `true` | Enables Grok personality selection. |
| `responsive_web_grok_places_card_enabled` | bool | `false` | `false` | Enables Grok places cards. |
| `responsive_web_grok_post_inline_translation_is_enabled` | bool | `true` | `true` | Enables inline translation of posts by Grok. |
| `responsive_web_grok_post_understanding_button_on_all_posts` | bool | `false` | `false` | Shows the post-understanding button on all posts. |
| `responsive_web_grok_profile_summary_enabled` | bool | `true` | `true` | Enables Grok profile summaries. |
| `responsive_web_grok_profile_summary_min_followers` | int | `50` | `50` | Minimum follower count for a Grok profile summary. |
| `responsive_web_grok_profile_summary_min_posts` | int | `15` | `15` | Minimum post count for a Grok profile summary. |
| `responsive_web_grok_promo_modal_enabled` | bool | `false` | `false` | Enables the Grok promo modal. |
| `responsive_web_grok_promo_modal_variant` | str | `"imagine_launch"` | `"imagine_launch"` | Variant of the Grok promo modal ("imagine_launch"). |
| `responsive_web_grok_prompt_edit_enabled` | bool | `true` | `true` | Enables prompt editing in Grok. |
| `responsive_web_grok_redirect_enabled` | bool | `true` | `true` | Enables redirects to Grok surfaces. |
| `responsive_web_grok_regen_configs` | bool | `false` | `false` | Purpose unclear from name; likely regeneration configuration for Grok responses. |
| `responsive_web_grok_route_disabled_search_think_to_paywall` | bool | `true` | `true` | Routes disabled Search/Think modes to the paywall. |
| `responsive_web_grok_rtl_detection` | bool | `true` | `true` | Enables right-to-left detection in Grok. |
| `responsive_web_grok_search_summary_enabled` | bool | `false` | `false` | Enables Grok search summary. |
| `responsive_web_grok_search_summary_images_enabled` | bool | `true` | `true` | Shows images in the Grok search summary. |
| `responsive_web_grok_search_summary_sidebar` | bool | `true` | `true` | Shows the Grok search summary in the sidebar. |
| `responsive_web_grok_share_attachment_enabled` | bool | `true` | `true` | Enables share attachments in Grok. |
| `responsive_web_grok_show_button_is_ad` | bool | `false` | `false` | Shows the Grok button when the post is an ad (variant). |
| `responsive_web_grok_show_button_on_ads` | bool | `false` | `false` | Shows the Grok button on ads. |
| `responsive_web_grok_show_button_send_is_ads` | bool | `false` | `false` | Shows the Grok send button on ads (variant). |
| `responsive_web_grok_show_cards_at_top` | bool | `true` | `true` | Shows cards at the top of Grok responses. |
| `responsive_web_grok_show_citations` | bool | `true` | `true` | Shows citations in Grok responses. |
| `responsive_web_grok_show_grok_performance_metrics` | bool | `false` | `false` | Shows Grok performance metrics. |
| `responsive_web_grok_show_grok_translated_post` | bool | `true` | `true` | Shows the Grok-translated post. |
| `responsive_web_grok_show_message_post_button` | bool | `true` | `true` | Shows a "post message" button on Grok messages. |
| `responsive_web_grok_sidebar_campaign_variant` | str | `""` | `""` | Sidebar campaign variant for Grok (empty). |
| `responsive_web_grok_sport_cards_enabled` | bool | `true` | `true` | Enables sports cards in Grok. |
| `responsive_web_grok_start_title_experiment_enabled` | bool | `false` | `false` | Enables the start-title experiment in Grok. |
| `responsive_web_grok_tab_education_days_threshold` | int | `30` | `30` | Days threshold for Grok tab education. |
| `responsive_web_grok_temporary_chat_enabled` | bool | `true` | `true` | Enables temporary (private) chats in Grok. |
| `responsive_web_grok_text_selection_enabled` | bool | `false` | `false` | Enables text selection actions in Grok. |
| `responsive_web_grok_tweet_actions_edit_image_enabled` | bool | `false` | `true` ⚠ | Enables "edit image with Grok" in post actions; on for this account. |
| `responsive_web_grok_tweet_media_detail_edit_image_button_enabled` | bool | `false` | `true` ⚠ | Enables the Grok edit-image button in media detail; on for this account. |
| `responsive_web_grok_tweet_media_edit_image_button_enabled` | bool | `false` | `true` ⚠ | Enables the Grok edit-image button on post media; on for this account. |
| `responsive_web_grok_tweet_translation` | bool | `true` | `true` | Enables Grok-powered post translation. |
| `responsive_web_grok_tweet_translation_limit` | int | `5000` | `5000` | Character limit for Grok post translation. |
| `responsive_web_grok_use_new_layout` | bool | `true` | `true` | Uses the new layout for Grok. |
| `responsive_web_grok_user_active_seconds_enable` | bool | `false` | `true` ⚠ | Enables tracking of Grok user-active seconds; on for this account. |
| `responsive_web_grok_user_seconds_debug` | bool | `false` | `false` | Enables debug of Grok user-seconds tracking. |
| `responsive_web_grok_user_seconds_heartbeat` | int | `5000` | `5000` | Heartbeat interval (ms) for Grok user-seconds tracking. |
| `responsive_web_grok_v2_upsell_enabled` | bool | `false` | `false` | Enables the v2 Grok upsell. |
| `responsive_web_grok_voice_mode_enabled` | bool | `false` | `true` ⚠ | Enables Grok voice mode on web; on for this account. |
| `responsive_web_grok_web_results` | bool | `true` | `true` | Enables web results in Grok. |
| `responsive_web_grok_webview_file_actions_enabled` | bool | `false` | `false` | Enables webview file actions in Grok. |
| `responsive_web_grok_xweb_link_prompt_cooldown_days` | int | `2` | `2` | Cooldown (days) for the prompt to link X web with Grok. |
| `responsive_web_grok_xweb_link_required` | bool | `false` | `false` | Requires linking between X web and Grok. |
| `responsive_web_grok_xweb_linked_share_readonly_enabled` | bool | `true` | `true` | Enables read-only linked shares for X web. |
| `responsive_web_grok_xweb_replacement_enabled` | bool | `false` | `true` ⚠ | Enables replacing Grok pages by X web equivalents; on for this account. |
| `rweb_navbar_grok_indicator_enabled` | bool | `false` | `false` | Shows a Grok indicator in the navbar. |
| `rweb_navbar_grok_indicator_item_count` | int | `0` | `0` | Item count for the navbar Grok indicator. |
| `subscriptions_inapp_grok` | bool | `true` | `true` | Enables in-app Grok subscription. |
| `subscriptions_inapp_grok_analyze` | bool | `false` | `false` | Enables in-app Grok analyze. |
| `subscriptions_inapp_grok_default_mode` | str | `"regular"` | `"regular"` | Default mode for in-app Grok ("regular"). |
| `subscriptions_inapp_grok_upsell_enabled` | bool | `true` | `true` | Enables in-app Grok upsell. |
| `subscriptions_inapp_grok_video_upsell` | str | `"https://abs.twimg.com/sticky/videos/inapp_dark_square_v4.mp4"` | `"https://abs.twimg.com/sticky/videos/inapp_dark_square_v4.mp4"` | URL of the dark in-app Grok upsell video. |
| `subscriptions_inapp_grok_video_upsell_dim` | str | `"https://abs.twimg.com/sticky/videos/inapp_dim_square_v4.mp4"` | `"https://abs.twimg.com/sticky/videos/inapp_dim_square_v4.mp4"` | URL of the dim in-app Grok upsell video. |
| `subscriptions_inapp_grok_video_upsell_light` | str | `"https://abs.twimg.com/sticky/videos/inapp_light_square_v4.mp4"` | `"https://abs.twimg.com/sticky/videos/inapp_light_square_v4.mp4"` | URL of the light in-app Grok upsell video. |
| `subscriptions_marketing_page_grok_4_web_paywall` | bool | `false` | `false` | Shows Grok 4 web paywall on the marketing page. |
| `subscriptions_upsells_home_sidebar_grok_promo` | bool | `false` | `false` | Shows Grok promo in the home sidebar. |
| `xai_profile_redirect_enabled` | bool | `true` | `true` | Redirects xAI profile. |
| `xchat_ask_grok_enabled` | bool | `true` | `true` | Enables "Ask Grok" in XChat. |
| `xchat_grok_bots` | bool | `false` | `false` | Enables Grok bots in XChat. |
| `xchat_grok_bots_transcript_page_size` | int | `50` | `50` | Transcript page size for Grok bots. |
| `xchat_invoke_grok_bot_enabled` | bool | `false` | `false` | Enables invoking Grok bots. |
| `xchat_plaintext_grok_enabled` | bool | `false` | `false` | Enables plaintext sharing with Grok. |
| `xchat_plaintext_grok_minimum_tier` | str | `"PremiumPlus"` | `"PremiumPlus"` | Minimum tier for plaintext Grok ("PremiumPlus"). |

### XChat / DMs / Calls

188 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `av_chat_encryption_enabled` | bool | `false` | `false` | Enables end-to-end encryption for audio/video chat calls. |
| `av_chat_group_e2ee_creator_enabled` | bool | `false` | `false` | Enables group-call E2EE for the call creator role. |
| `av_chat_group_e2ee_joiner_enabled` | bool | `false` | `false` | Enables group-call E2EE for the call joiner role. |
| `av_chat_xchat_emoji_reactions_enabled` | bool | `false` | `false` | Enables emoji reactions in XChat audio/video calls. |
| `birdwatch_xchat_pivot_rendering_enabled` | bool | `true` | `true` | Enables rendering of Community Notes (Birdwatch) pivots inside XChat. |
| `dm_block_enabled` | bool | `true` | `true` | Enables blocking in DMs. |
| `dm_bulk_delete_enabled` | bool | `false` | `false` | Enables bulk deletion of DM conversations. |
| `dm_conversation_labels_max_pinned_count` | int | `10` | `10` | Maximum number of pinned DM conversation labels. |
| `dm_conversation_labels_pinned_education_enabled` | bool | `true` | `true` | Shows education for pinned DM conversation labels. |
| `dm_conversations_nsfw_media_filter_enabled` | bool | `false` | `false` | Enables an NSFW media filter in DM conversations. |
| `dm_edit_dms_overflow_menu_enabled` | bool | `false` | `false` | Enables the "edit DMs" item in the overflow menu. |
| `dm_education_flags_prompt` | bool | `false` | `false` | Shows an education prompt for DM flags. |
| `dm_inbox_search_groups_bucket_size` | int | `5` | `5` | Number of group results in the DM inbox search bucket. |
| `dm_inbox_search_max_recent_searches_stored` | int | `5` | `5` | Maximum number of recent DM searches stored. |
| `dm_inbox_search_messages_bucket_size` | int | `5` | `5` | Number of message results in the DM inbox search bucket. |
| `dm_inbox_search_people_bucket_size` | int | `5` | `5` | Number of people results in the DM inbox search bucket. |
| `dm_secret_conversations_enabled` | bool | `false` | `false` | Enables secret (end-to-end) DM conversations (legacy). |
| `dm_settings_info_page_allow_subscriber_messages_setting_enabled` | bool | `true` | `true` | Enables the "allow subscriber messages" setting on the DM settings info page. |
| `dm_settings_info_page_device_list_enabled` | bool | `false` | `false` | Enables the device list on the DM settings info page. |
| `dm_share_sheet_send_individually_max_count` | int | `20` | `20` | Maximum recipients when sharing individually through the DM share sheet. |
| `dm_video_downloads_enabled` | bool | `false` | `false` | Enables downloading videos from DMs. |
| `dm_voice_rendering_enabled` | bool | `true` | `true` | Enables rendering of voice messages in DMs. |
| `dsa_encrypted_dms_report_flow_enabled` | bool | `false` | `false` | Enables the DSA report flow for encrypted DMs. |
| `payments_support_xchat_sessions_enabled` | bool | `true` | `true` | Enables XChat sessions for payments support. |
| `responsive_web_messages_continue_enabled` | bool | `true` | `true` | Enables the continue-conversation prompt in messages. |
| `responsive_web_messages_enabled` | bool | `true` | `true` | Enables Messages. |
| `responsive_web_messages_watch_info_enabled` | bool | `false` | `false` | Enables watch-info polling in messages. |
| `responsive_web_messages_watch_info_interval_s` | int | `600` | `600` | Interval (s) for watch-info in messages. |
| `rweb_conf_dev_enabled` | bool | `false` | `false` | Enables developer mode for conferencing (calls). |
| `rweb_conf_multi_video_enabled` | bool | `true` | `true` | Enables multi-video in conferences. |
| `rweb_conf_only_enabled` | bool | `false` | `false` | Restricts to conference-only mode. |
| `rweb_conf_rnnoise_enabled` | bool | `true` | `true` | Enables RNNoise noise suppression in calls. |
| `rweb_xchat_bug_report_url` | str | `""` | `""` | Bug report URL for XChat (empty). |
| `rweb_xchat_call_health_enabled` 🆕 | bool | `true` | `true` | Enables XChat call health. |
| `rweb_xchat_call_link_enabled` | bool | `false` | `false` | Enables XChat call links. |
| `rweb_xchat_call_redirect_enabled` | bool | `false` | `false` | Enables redirecting to XChat calls. |
| `rweb_xchat_call_window_enabled` | bool | `false` | `false` | Enables the XChat call window. |
| `rweb_xchat_calls_rtc_api_enabled` | bool | `true` | `true` | Enables the RTC API for XChat calls. |
| `rweb_xchat_calls_v2_enabled` | bool | `false` | `false` | Enables XChat calls v2. |
| `rweb_xchat_calls_whiteboard_enabled` | bool | `false` | `false` | Enables a whiteboard in calls. |
| `rweb_xchat_client_stats_enabled` 🆕 | bool | `true` | `true` | Enables XChat client stats. |
| `rweb_xchat_debug_enabled` | bool | `false` | `false` | Enables XChat debug mode. |
| `rweb_xchat_dogfood_logs_enabled` | bool | `false` | `false` | Enables dogfood logs. |
| `rweb_xchat_logs` | bool | `false` | `false` | Enables XChat logs. |
| `rweb_xchat_loudness_control_enabled` | bool | `false` | `false` | Enables loudness control in calls. |
| `rweb_xchat_markdown_tables_enabled` | bool | `false` | `false` | Enables Markdown tables in XChat. |
| `rweb_xchat_module_federation_enabled` 🆕 | bool | `true` | `true` | Enables module federation for XChat. |
| `rweb_xchat_scroller_rewrite_enabled` | bool | `true` | `true` | Enables the rewritten scroller. |
| `rweb_xchat_sentry_enabled` | bool | `true` | `true` | Enables Sentry for XChat. |
| `rweb_xchat_sqlite_logs` | bool | `false` | `false` | Enables SQLite logs. |
| `rweb_xchat_standalone_avcall_enabled` | bool | `true` | `true` | Enables standalone AV calls. |
| `rweb_xchat_ws_only_when_active` | bool | `false` | `false` | Uses WebSocket only when active. |
| `spaces_conference_enabled` | bool | `false` | `false` | Enables conference in Spaces. |
| `spaces_conference_opus_dtx_enabled` | bool | `false` | `false` | Enables Opus DTX in conferences. |
| `twitter_chat_communities_chat_enabled` | bool | `false` | `false` | Enables chat in Communities. |
| `xcall_item_in_list_enabled` 🆕 | bool | `false` | `false` | Enables items in list for X calls. |
| `xcall_link_devices_enabled` 🆕 | bool | `false` | `false` | Enables linking devices for X calls. |
| `xchat_additional_reply_preview_validation_required_seqnum_str` | str | `"0"` | `"0"` | Sequence number after which reply-preview validation is required (string). |
| `xchat_additional_reply_preview_validation_send` | bool | `false` | `false` | Sends additional reply-preview validation data. |
| `xchat_attachment_viewer_enabled` | bool | `false` | `false` | Enables the XChat attachment viewer. |
| `xchat_av_call_card_interaction_enabled` | bool | `true` | `true` | Enables interactive AV call cards. |
| `xchat_av_call_start_should_notify` | bool | `false` | `false` | Notifies on AV call start. |
| `xchat_av_pip_enabled` | bool | `false` | `false` | Enables PiP for AV calls. |
| `xchat_batch_updates_for_bottom_cursor_processing` | bool | `true` | `true` | Batches updates for bottom cursor processing. |
| `xchat_ckey_recovery_enabled` | bool | `false` | `false` | Enables recovery of conversation keys (ckey). |
| `xchat_ckey_sig_v6_enforce_after_seq_num_str` | str | `[redacted]` | `[redacted]` | Sequence number after which v6 ckey signatures are enforced. |
| `xchat_clear_chat_enabled` | bool | `true` | `true` | Enables clearing chats. |
| `xchat_composer_photo_editor_enabled` | bool | `false` | `false` | Enables the photo editor in the XChat composer. |
| `xchat_conversation_event_limit` | int | `200` | `200` | Maximum events fetched per conversation. |
| `xchat_creator_group_syncing_enabled` | bool | `false` | `false` | Enables syncing of creator groups. |
| `xchat_dm_media_upload_workmanager_enabled` | bool | `false` | `false` | Uses WorkManager for DM media uploads (Android). |
| `xchat_dm_write_gate_enabled` | bool | `true` | `true` | Enables DM write gate. |
| `xchat_drafts_bump_to_top` | bool | `true` | `true` | Bumps drafted conversations to the top. |
| `xchat_drop_messages_failing_franking_verification` | bool | `false` | `false` | Drops messages failing franking verification. |
| `xchat_drop_sigs_after_seq_num` | int | `9223372036854776000` | `9223372036854776000` | Sequence number after which signatures are dropped (numeric). |
| `xchat_drop_sigs_after_seq_num_str` | str | `[redacted]` | `[redacted]` | Sequence number after which signatures are dropped (string). |
| `xchat_enable_av` | bool | `true` | `true` | Enables audio/video calls in XChat. |
| `xchat_enable_av_group` | bool | `true` | `true` | Enables group AV calls. |
| `xchat_enable_av_mobile` | bool | `false` | `false` | Enables AV on mobile. |
| `xchat_enable_batch_sql_events` | bool | `false` | `false` | Enables batched SQL events. |
| `xchat_enable_command_menu` | bool | `true` | `true` | Enables the command menu. |
| `xchat_enable_default_disappearing_messages_setting` | bool | `false` | `false` | Enables default disappearing messages. |
| `xchat_enable_default_screenshot_blocking_setting` | bool | `false` | `false` | Enables default screenshot blocking. |
| `xchat_enable_drafts` | bool | `false` | `false` | Enables drafts in XChat. |
| `xchat_enable_eu_report` | bool | `false` | `false` | Enables the EU report flow. |
| `xchat_enable_forward_message_v2` | bool | `true` | `true` | Enables forward message v2. |
| `xchat_enable_franking_report` | bool | `true` | `true` | Enables franking reports (abuse reporting for E2EE messages). |
| `xchat_enable_in_memory_event_retry` | bool | `true` | `true` | Enables in-memory event retry. |
| `xchat_enable_in_memory_event_retry_bottom_cursor` | bool | `true` | `true` | Enables in-memory event retry for bottom cursor. |
| `xchat_enable_legacy_metadata_write` | bool | `true` | `true` | Writes legacy metadata. |
| `xchat_enable_message_request_ui_v3` | bool | `true` | `true` | Enables message request UI v3. |
| `xchat_enable_message_requests` | bool | `true` | `true` | Enables message requests. |
| `xchat_enable_message_requests_attachments` | bool | `false` | `false` | Enables attachments in message requests. |
| `xchat_enable_metadata_sync` | bool | `false` | `true` ⚠ | Enables metadata sync; on for this account. |
| `xchat_enable_numbers` | bool | `true` | `true` | Enables "numbers" in XChat (phone-number based contacts). |
| `xchat_enable_numbers_copying` | bool | `true` | `true` | Enables copying of numbers. |
| `xchat_enable_numbers_generation` | bool | `false` | `false` | Enables number generation. |
| `xchat_enable_numbers_premium` | bool | `true` | `true` | Enables Premium numbers. |
| `xchat_enable_ratcheting` | bool | `false` | `false` | Enables ratcheting in E2EE. |
| `xchat_enable_reaction_notifs` | bool | `false` | `false` | Enables reaction notifications. |
| `xchat_enable_realm_reach_check` | bool | `false` | `false` | Enables the realm reach check. |
| `xchat_enable_share_message_v2` | bool | `false` | `false` | Enables share message v2. |
| `xchat_enable_single_message_locking` | bool | `false` | `false` | Enables single-message locking. |
| `xchat_enable_undecryptable_tombstones` | bool | `false` | `false` | Enables tombstones for undecryptable messages. |
| `xchat_enable_user_metadata_migration_dry_run` | bool | `false` | `false` | Dry-run of user metadata migration. |
| `xchat_enable_video_autoplay` | bool | `false` | `false` | Enables video autoplay. |
| `xchat_enforce_media_hash_verification` | bool | `false` | `false` | Enforces media hash verification. |
| `xchat_external_app_integrations_enabled` | bool | `true` | `true` | Enables external app integrations. |
| `xchat_fail_closed_unsigned_sends` | bool | `true` | `true` | Fails closed on unsigned sends. |
| `xchat_fetch_messages_from_push_handler` | bool | `false` | `false` | Fetches messages from the push handler. |
| `xchat_forward_media_max_conversations` | int | `5` | `5` | Maximum conversations for media forwarding. |
| `xchat_forward_media_max_size_mb` | int | `100` | `100` | Maximum media size (MB) for forwarding. |
| `xchat_franking_required_after_seq_num` | int | `9223372036854776000` | `9223372036854776000` | Sequence number after which franking is required (numeric). |
| `xchat_franking_required_after_seq_num_str` | str | `"9223372036854775807"` | `"9223372036854775807"` | Sequence number after which franking is required (string). |
| `xchat_group_admin_settings_enabled` | bool | `true` | `true` | Enables group admin settings. |
| `xchat_group_description_enabled` | bool | `true` | `true` | Enables group descriptions. |
| `xchat_grpc_chat_page_enabled` | bool | `false` | `false` | Uses gRPC for the chat page. |
| `xchat_hide_pending_members_for_non_admin` | bool | `true` | `true` | Hides pending members for non-admins. |
| `xchat_hybrid_pull_eagerly_fetch_history_after_seconds` | int | `-1` | `-1` | Seconds after which history is eagerly pulled (-1 disables). |
| `xchat_inbox_checksum_scribing_enabled` | bool | `true` | `true` | Enables inbox checksum scribing. |
| `xchat_inbox_conversation_event_limit` | int | `5` | `5` | Number of events per conversation in the inbox. |
| `xchat_inbox_conversation_limit` | int | `20` | `20` | Initial inbox conversation limit. |
| `xchat_inbox_conversation_limit_subsequent` | int | `100` | `100` | Subsequent inbox conversation limit. |
| `xchat_inbox_conversation_local_pagination_page_size` | int | `20` | `20` | Local pagination page size for the inbox. |
| `xchat_inbox_new_messages_preview_enabled` | bool | `false` | `false` | Enables the new-messages preview. |
| `xchat_invalid_sig_log_after_seq_num_str` | str | `[redacted]` | `[redacted]` | Sequence number after which invalid signatures are logged. |
| `xchat_ios_max_io_threads` | int | `64` | `64` | Maximum IO threads on iOS. |
| `xchat_keep_db_when_processing_inbox_response` | bool | `false` | `false` | Keeps the DB when processing inbox responses. |
| `xchat_keypair_nuclear_reset_enabled` | bool | `false` | `false` | Enables nuclear key reset. |
| `xchat_keypair_recovery_enabled` | bool | `false` | `false` | Enables keypair recovery. |
| `xchat_liquid_glass_convo_header_enabled` | bool | `false` | `false` | Enables liquid glass conversation header (iOS). |
| `xchat_local_pagination_page_size` | int | `50` | `50` | Local pagination page size. |
| `xchat_long_messages_enabled` | bool | `true` | `true` | Enables long messages. |
| `xchat_markdown_rendering_enabled` | bool | `true` | `true` | Enables Markdown rendering. |
| `xchat_max_attachments_per_message` | int | `10` | `10` | Maximum attachments per message. |
| `xchat_max_group_description_length` | int | `500` | `500` | Maximum group description length. |
| `xchat_max_group_size` | int | `1000` | `1000` | Maximum group size. |
| `xchat_max_group_size_for_live_read_receipts` | int | `50` | `50` | Max group size for live read receipts. |
| `xchat_max_group_size_for_remove_info_item` | int | `100` | `100` | Max group size for remove info items. |
| `xchat_max_message_plaintext_length_bytes` | str | `"11000"` | `"11000"` | Maximum plaintext message length in bytes (string). |
| `xchat_max_message_preview_size` | str | `"1000"` | `"1000"` | Maximum message preview size (string). |
| `xchat_max_users_to_fetch_per_request` | int | `100` | `100` | Maximum users fetched per request. |
| `xchat_media_download_io_batching_enabled` | bool | `true` | `true` | Batches media download IO. |
| `xchat_media_resolve_threshold_fast_network_bytes_str` | str | `"104857600"` | `"104857600"` | Media resolve threshold on fast networks (bytes). |
| `xchat_media_resolve_threshold_slow_network_bytes_str` | str | `"10485760"` | `"10485760"` | Media resolve threshold on slow networks (bytes). |
| `xchat_media_upload_io_batching_enabled` | bool | `true` | `true` | Batches media upload IO. |
| `xchat_message_composer_v2` | bool | `false` | `false` | Enables message composer v2. |
| `xchat_message_date_tap_enabled` | bool | `false` | `false` | Enables date tap in messages. |
| `xchat_message_grouping_window_seconds` | int | `3600` | `3600` | Message grouping window (s). |
| `xchat_message_list_v2_enabled` | bool | `false` | `false` | Enables message list v2. |
| `xchat_message_request_rate_limit_upsell` | bool | `true` | `true` | Shows an upsell on message-request rate limit. |
| `xchat_missing_messages_scribe_enabled` | bool | `false` | `false` | Scribes missing messages. |
| `xchat_molecule_enabled` | bool | `false` | `false` | Purpose unclear from name; likely enables a "molecule" UI component system in XChat. |
| `xchat_numbers_tray_location` | str | `""` | `""` | Location of the numbers tray (empty). |
| `xchat_observe_inbox_categories_separately` | bool | `true` | `true` | Observes inbox categories separately. |
| `xchat_observe_inbox_users_enabled` | bool | `true` | `true` | Observes inbox users. |
| `xchat_pay_button_enabled` | bool | `true` | `true` | Enables a pay button in XChat. |
| `xchat_pin_signatures_enabled` | bool | `false` | `false` | Enables signing pins. |
| `xchat_pinned_messages_enabled` | bool | `true` | `true` | Enables pinned messages. |
| `xchat_pinned_messages_reading_enabled` | bool | `true` | `true` | Enables reading pinned messages. |
| `xchat_pmk_bundle_signatures_enabled` | bool | `false` | `false` | Enables PMK bundle signatures. |
| `xchat_ratchet_group_id_threshold` | int | `9223372036854776000` | `9223372036854776000` | Ratchet group-id threshold (numeric). |
| `xchat_ratchet_group_id_threshold_str` | str | `"9223372036854775807"` | `"9223372036854775807"` | Ratchet group-id threshold (string). |
| `xchat_realm_migration_local_key_fallback_enabled` | bool | `false` | `false` | Enables local key fallback during realm migration. |
| `xchat_repair_groups_after_passcode_reset` | bool | `true` | `true` | Repairs groups after a passcode reset. |
| `xchat_resolve_unencrypted_media_locally` | bool | `true` | `true` | Resolves unencrypted media locally. |
| `xchat_sample_observation_queries` | int | `500` | `500` | Sample count for observation queries. |
| `xchat_search_frequency_weight` | float | `0.6` | `0.6` | Frequency weight in XChat search ranking. |
| `xchat_search_recency_weight` | float | `0.2` | `0.2` | Recency weight in search ranking. |
| `xchat_search_repetition_weight` | float | `0.2` | `0.2` | Repetition weight in search ranking. |
| `xchat_self_custody_enabled` | bool | `false` | `false` | Enables self-custody of keys. |
| `xchat_send_franking_data` | bool | `true` | `true` | Sends franking data. |
| `xchat_send_signature_protocol_version` | int | `7` | `7` | Signature protocol version (7). |
| `xchat_separate_reactions_table_enabled` | bool | `false` | `false` | Uses a separate reactions table. |
| `xchat_settings_enabled` | bool | `false` | `false` | Enables XChat settings. |
| `xchat_settings_redesign_enabled` | bool | `true` | `true` | Enables redesigned XChat settings. |
| `xchat_share_to_ig_story` | bool | `false` | `false` | Enables sharing to Instagram story. |
| `xchat_signature_required_after_seq_num_str` | str | `"9223372036854775806"` | `"9223372036854775806"` | Sequence number after which signatures are required. |
| `xchat_standalone_push_notifications` | bool | `false` | `false` | Enables standalone push notifications. |
| `xchat_streamed_link_preview` | bool | `true` | `true` | Streams link previews. |
| `xchat_swipe_to_reveal_timestamp_enabled` | bool | `false` | `false` | Enables swipe-to-reveal timestamps. |
| `xchat_throttle_badge_counts` | bool | `false` | `false` | Throttles badge counts. |
| `xchat_unread_mismatch_scribing_enabled` | bool | `true` | `true` | Scribes unread-count mismatches. |
| `xchat_url_preview_v2_enabled` | bool | `true` | `true` | Enables URL preview v2. |
| `xchat_user_event_limit` | int | `500` | `500` | Maximum user events fetched. |
| `xchat_validate_priv_pub_on_load` | bool | `false` | `false` | Validates private/public keys on load. |
| `xchat_voice_messages_enabled` | bool | `true` | `true` | Enables voice messages. |
| `xchat_voice_messages_transcription_enabled` | bool | `false` | `false` | Enables voice-message transcription. |

### Payments / X Money

37 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `payments_1password_history_fix_enabled` | bool | `true` | `true` | Fixes password-manager (1Password) history handling in X Money flows. |
| `payments_agent_connections_enabled` | bool | `true` | `true` | Enables agent connections in X Money; on for this account and now also on by default. |
| `payments_agent_connections_prefill_enabled` | bool | `false` | `false` | Prefills fields in the X Money agent-connections flow; now off by default and for this account (default was on, user off, at the 2026-09-23 capture). |
| `payments_assets_activate_card_dark_video_url` | str | `"https://pbs.twimg.com/static/money/x-card-animation-v4.mp4"` | `"https://pbs.twimg.com/static/money/x-card-animation-v4.mp4"` | URL of the dark-mode card activation animation for X Money. |
| `payments_assets_activate_card_light_video_url` | str | `"https://pbs.twimg.com/static/money/x-card-animation-v4-white.mp4"` | `"https://pbs.twimg.com/static/money/x-card-animation-v4-white.mp4"` | URL of the light-mode card activation animation for X Money. |
| `payments_assets_activate_card_video_ratio` | float | `1.33` | `1.33` | Aspect ratio of the card activation video. |
| `payments_auth_token_enabled` | bool | `true` | `true` | Enables auth-token handling for payments. |
| `payments_business_onboarding_support` | list | `[]` (0 items) | `[]` (0 items) | Business onboarding support configuration list (empty). |
| `payments_cash_deposits_enabled` | bool | `true` | `true` | Enables cash deposits in X Money. |
| `payments_chat_support_enabled` | bool | `false` | `false` | Enables chat support in payments. |
| `payments_chat_support_for_limits_enabled` | bool | `true` | `true` | Enables chat support for limits. |
| `payments_cheques_deposits_enabled` | bool | `true` | `true` | Enables cheque deposits. |
| `payments_crb_iframe_delay_msecs` | int | `1000` | `1000` | Delay (ms) before the CRB iframe is shown in payments. |
| `payments_csv_export_enabled` 🆕 | bool | `false` | `false` | Enables CSV export of payments. |
| `payments_forward_with_enabled` | bool | `true` | `true` | Enables "forward with" in payments. |
| `payments_funds_insurance_redesign_enabled` | bool | `true` | `true` | Enables the redesigned funds insurance UI. |
| `payments_funds_insurance_sweep_enabled` | bool | `true` | `true` | Enables funds insurance sweep. |
| `payments_half_cover_notices_enabled` | bool | `true` | `true` | Enables half-cover notices. |
| `payments_interest_details_with_boost_enabled` | bool | `true` | `true` | Shows interest details including boosts. |
| `payments_international_wires_enabled` | bool | `false` | `false` | Enables international wires. |
| `payments_lexical_search_enabled` | bool | `false` | `false` | Enables lexical search in payments. |
| `payments_onboarding_issued_cards_polling_enabled` | bool | `true` | `true` | Polls for issued cards during onboarding. |
| `payments_passkey_onboarding_enabled` | bool | `true` | `true` | Enables passkey onboarding for payments. |
| `payments_scheduled_payments_enabled` | bool | `true` | `true` | Enables scheduled payments. |
| `payments_secondary_accounts_enabled` | bool | `true` | `true` | Enables secondary accounts. |
| `payments_shared_accounts_enabled` | bool | `true` | `true` | Enables shared accounts. |
| `payments_support_grpc_enabled` | bool | `true` | `true` | Uses gRPC for payments support. |
| `payments_timeline_action` | bool | `true` | `true` | Enables a payments action in timelines. |
| `payments_tracing_reports_enabled` | bool | `true` | `true` | Enables tracing reports for payments. |
| `payments_transaction_receipt_enabled` | bool | `true` | `true` | Enables transaction receipts. |
| `payments_transaction_search_enabled` | bool | `true` | `true` | Enables transaction search. |
| `payments_transfer_link_enabled` | bool | `false` | `false` | Enables transfer links. |
| `payments_web_external_app_enabled` | bool | `false` | `false` | Enables the external payments web app. |
| `rweb_cashtags_composer_attachment_enabled` | bool | `true` | `true` | Enables cashtag attachments in the composer. |
| `rweb_cashtags_composer_attachment_size_customization_enabled` | bool | `true` | `true` | Enables size customization of cashtag attachments. |
| `rweb_cashtags_composer_enabled` | bool | `true` | `true` | Enables cashtags ($TICKER) in the composer. |
| `rweb_cashtags_enabled` | bool | `true` | `true` | Master switch for cashtags. |

### Verified Organizations / Business

91 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `blue_business_admin_sidebar_module_enabled` | bool | `true` | `true` | Shows the admin module in the sidebar for Verified Organizations (X Business) accounts. |
| `blue_business_ads_metrics` | bool | `true` | `true` | Enables ad metrics for Verified Organizations (Blue Business) accounts. |
| `blue_business_affiliates_list_order_setting_enabled` | bool | `false` | `false` | Enables the ordering setting for the affiliates list of a Verified Organization. |
| `blue_business_analytics` | bool | `true` | `true` | Enables the analytics view for Verified Organizations. |
| `blue_business_analytics_affiliate_filtering_enabled` | bool | `true` | `true` | Enables filtering analytics by affiliate for Verified Organizations. |
| `blue_business_direct_invites_enabled` | bool | `true` | `true` | Enables direct invites of affiliates to a Verified Organization. |
| `blue_business_display_annual_price_monthly` | bool | `true` | `true` | Displays the annual Business price as a per-month figure. |
| `blue_business_multi_affiliates_ui_enabled` | bool | `true` | `true` | Enables the multi-affiliate UI for Verified Organizations. |
| `blue_business_simplify_signup_ui` | bool | `false` | `false` | Enables a simplified Business signup UI. |
| `blue_business_tier_switching_enabled` | bool | `true` | `true` | Allows switching between Business tiers. |
| `blue_business_username_change_prompt_enabled` | bool | `true` | `true` | Shows a username-change prompt for Business accounts. |
| `blue_business_verified_admin_enabled` | bool | `true` | `true` | Enables the verified-admin role for Business accounts. |
| `blue_business_vo_free_affiliate_limit` | int | `5` | `5` | Number of free affiliate slots for a Verified Organization. |
| `blue_business_vo_nav_for_legacy_verified` | bool | `false` | `true` ⚠ | Shows the Verified Organizations nav entry to legacy-verified users; on for this account but off by default. |
| `premium_business_offers_banner_portal_basic_tier` | bool | `false` | `false` | Shows Premium business-offers banner in the portal for the basic tier. |
| `premium_business_offers_banner_sidebar_basic_tier` | bool | `false` | `false` | Shows Premium business-offers banner in the sidebar for the basic tier. |
| `premium_business_offers_nav_indicator_enabled` | bool | `false` | `false` | Shows a nav indicator for Premium business offers. |
| `premium_business_offers_navbar_discount_label_enabled` | bool | `false` | `false` | Shows a discount label in the navbar for business offers. |
| `premium_business_offers_navbar_premium_signup_hidden` | bool | `false` | `false` | Hides the Premium signup entry in the navbar for business offers. |
| `premium_business_offers_signup_navbar_tab_enabled` | bool | `false` | `false` | Shows a signup tab in the navbar for business offers. |
| `professional_launchpad_m1_enabled` | bool | `true` | `true` | Enables milestone 1 of the Professional Launchpad. |
| `professional_launchpad_mobile_promotable_timeline` | bool | `false` | `false` | Enables a promotable timeline in the mobile Professional Launchpad. |
| `professional_launchpad_upload_address_book` | bool | `true` | `true` | Allows uploading an address book in the Professional Launchpad. |
| `recruiting_admin_currencies_enabled` | bool | `false` | `false` | Enables admin currencies in recruiting. |
| `recruiting_global_jobs_search_enabled` | bool | `false` | `false` | Enables global jobs search in recruiting. |
| `recruiting_job_page_consumption_enabled` | bool | `false` | `false` | Enables job page consumption. |
| `recruiting_job_recommendations_enabled` | bool | `false` | `false` | Enables job recommendations. |
| `recruiting_job_search_ai_companies_filter_enabled` | bool | `false` | `false` | Enables the AI-companies filter in job search. |
| `recruiting_jobs_list_consumption_enabled` | bool | `false` | `false` | Enables consumption of jobs lists. |
| `recruiting_jobs_list_search_enabled` | bool | `false` | `false` | Enables search in jobs lists. |
| `recruiting_jobs_list_share_enabled` | bool | `false` | `false` | Enables sharing of jobs lists. |
| `recruiting_pin_job_enabled` | bool | `false` | `false` | Enables pinning a job. |
| `recruiting_premium_jobs_enabled` | bool | `false` | `false` | Enables Premium jobs. |
| `recruiting_promoted_jobs_enabled` | bool | `false` | `false` | Enables promoted jobs. |
| `recruiting_search_filters_enabled` | bool | `false` | `false` | Enables search filters in recruiting. |
| `recruiting_verified_orgs_admin_enabled` | bool | `false` | `false` | Enables the Verified Orgs admin for recruiting. |
| `recruiting_verified_orgs_ats_integration_enabled` | bool | `false` | `false` | Enables ATS integration for Verified Orgs recruiting. |
| `recruiting_verified_orgs_enroll_allowed` | bool | `false` | `false` | Allows Verified Orgs to enroll in recruiting. |
| `responsive_web_verified_organizations_affiliate_fetch_limit` | int | `3000` | `3000` | Affiliate fetch limit for Verified Organizations. |
| `responsive_web_verified_organizations_application_requirements_enabled` 🆕 | bool | `false` | `false` | Enables application requirements for Verified Organizations. |
| `responsive_web_verified_organizations_application_two_column_enabled` 🆕 | bool | `false` | `false` | Enables two-column application for Verified Organizations. |
| `responsive_web_verified_organizations_enterprise_insights_enabled` | bool | `false` | `false` | Enables enterprise insights. |
| `responsive_web_verified_organizations_enterprise_tier` | bool | `false` | `false` | Enables the enterprise tier. |
| `responsive_web_verified_organizations_free_to_invoice_enabled` | bool | `false` | `false` | Enables free-to-invoice. |
| `responsive_web_verified_organizations_free_upgrade_promo_enabled` | bool | `true` | `true` | Enables the free-upgrade promo. |
| `responsive_web_verified_organizations_handle_form_enabled` | bool | `false` | `false` | Enables the handle form. |
| `responsive_web_verified_organizations_idv_enabled` | bool | `false` | `false` | Enables IDV for Verified Organizations. |
| `responsive_web_verified_organizations_insights_enabled` | bool | `true` | `true` | Enables insights for Verified Organizations. |
| `responsive_web_verified_organizations_intercom_enabled` | bool | `true` | `true` | Enables Intercom for Verified Organizations. |
| `responsive_web_verified_organizations_invoice_enabled` | bool | `false` | `false` | Enables invoices. |
| `responsive_web_verified_organizations_invoice_update_enabled` | bool | `false` | `true` ⚠ | Enables invoice updates; on for this account. |
| `responsive_web_verified_organizations_new_signup_enabled` | bool | `true` | `true` | Enables new signup for Verified Organizations. |
| `responsive_web_verified_organizations_new_year_offer_enabled` | bool | `true` | `true` | Enables the New Year offer. |
| `responsive_web_verified_organizations_offer_description_enabled` | bool | `false` | `false` | Enables offer descriptions. |
| `responsive_web_verified_organizations_paid_to_invoice_enabled` | bool | `false` | `false` | Enables paid-to-invoice. |
| `responsive_web_verified_organizations_people_search_enabled` | bool | `false` | `false` | Enables people search for Verified Organizations. |
| `responsive_web_verified_organizations_xbusiness_enabled` | bool | `false` | `false` | Enables XBusiness. |
| `responsive_web_vo_annual_credit_increase_enabled` | bool | `true` | `true` | Enables annual credit increase for Verified Organizations. |
| `responsive_web_vo_basic_application_enabled` | bool | `true` | `true` | Enables basic application for Verified Organizations. |
| `rweb_premium_business_rebranding_enabled` | bool | `true` | `true` | Enables the Premium Business rebranding. |
| `rweb_premium_business_rebranding_entry_point_removed` | bool | `false` | `false` | Removes the rebranding entry point. |
| `rweb_premium_business_rebranding_governments_enabled` | bool | `true` | `true` | Enables rebranding for governments. |
| `rweb_premium_business_rebranding_hiring_url_redirect_enabled` | bool | `true` | `true` | Redirects the hiring URL for rebranding. |
| `rweb_premium_business_rebranding_landing_page_enabled` | bool | `true` | `true` | Enables the rebranded landing page. |
| `rweb_premium_business_rebranding_premium_paywall_enabled` | bool | `true` | `true` | Enables the rebranded Premium paywall. |
| `rweb_premium_business_rebranding_premium_paywall_four_cards_enabled` | bool | `false` | `false` | Shows four cards in the rebranded paywall. |
| `rweb_premium_business_rebranding_url_enabled` | bool | `true` | `true` | Enables rebranded URLs. |
| `smbo_legacy_pac_is_in_follow_position_test` | bool | `false` | `false` | Purpose unclear from name; likely a test of the legacy PAC placement in follow position. |
| `subscriptions_features_premium_real_syscache_write` | bool | `true` | `true` | Enables write to the "real" Premium syscache. |
| `subscriptions_features_premium_syscache_write` | bool | `true` | `true` | Enables write to the Premium syscache. |
| `subscriptions_features_syscache_read` | bool | `true` | `true` | Enables read from the features syscache. |
| `subscriptions_features_syscache_write` | bool | `true` | `true` | Enables write to the features syscache. |
| `subscriptions_upsells_vo_nav_decoration_enabled` | bool | `false` | `false` | Enables VO nav decoration. |
| `subscriptions_upsells_vo_nav_decoration_variant` | str | `"30_percent_off"` | `"30_percent_off"` | Variant for VO nav decoration ("30_percent_off"). |
| `subscriptions_upsells_vo_premium_business_rebranding_free_gold_account` | str | `""` | `""` | Free gold account variant for rebranding (empty). |
| `subscriptions_upsells_vo_premium_business_rebranding_variant` | str | `"variant_a"` | `"variant_a"` | Variant for rebranding ("variant_a"). |
| `syscache_business_cancel_flow_warning_enabed` | bool | `false` | `false` | Enables cancel flow warning for business syscache. |
| `syscache_entrypoint_settings_enabled` | bool | `true` | `true` | Enables the settings entry point for syscache. |
| `syscache_entrypoint_vo_portal_basic_users_enabled` | bool | `true` | `true` | Shows the Verified Organizations portal entry point to Basic-tier users. |
| `syscache_entrypoint_vo_portal_enabled` | bool | `true` | `true` | Shows the Verified Organizations portal entry point. |
| `syscache_entrypoint_vo_portal_url` | str | `"https://handles.x.com"` | `"https://handles.x.com"` | URL of the Verified Organizations portal ("handles.x.com"). |
| `syscache_handle_share_banner_enabled` | bool | `true` | `true` | Shows the handle-share banner. |
| `syscache_premium_cancel_flow_warning_enabed` | bool | `true` | `true` | Shows a warning in the Premium cancel flow. |
| `syscache_syscache_pb_sidebar_handles_enabled` | bool | `false` | `false` | Shows handles in the Premium sidebar module. |
| `syscache_vo_paywall_enabled` | bool | `true` | `true` | Enables the Verified Organizations paywall. |
| `user_ad_accounts_config_enabled` | bool | `false` | `false` | Enables user ad accounts config. |
| `verified_vo_refreshed_advertising_screen_enabled` | bool | `true` | `true` | Enables the refreshed advertising screen for verified VO. |
| `vo_upsell_enabled` | bool | `true` | `true` | Enables VO upsell. |
| `vo_upsell_new_business_query_enabled` | bool | `true` | `true` | Enables the new business query for VO upsell. |
| `vo_upsell_profile_button_enabled` | bool | `false` | `false` | Enables a VO upsell button on profiles. |
| `x_lite_quick_promote_analytics_banner_enabled` 🆕 | bool | `false` | `false` | Shows the analytics banner in X Lite Quick Promote. |

### Subscriptions / Premium

207 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `creator_subscriptions_connect_tab_enabled` | bool | `true` | `true` | Enables the Connect tab for creator subscriptions. |
| `creator_subscriptions_eligibility_impressions` | int | `5000000` | `5000000` | Impression threshold required for creator subscription eligibility. |
| `creator_subscriptions_eligibility_verified_followers` | int | `2000` | `2000` | Verified-follower threshold required for creator subscription eligibility. |
| `creator_subscriptions_email_share_enabled` | bool | `true` | `true` | Enables sharing a creator's subscription via email. |
| `creator_subscriptions_revamp_enabled` | bool | `true` | `true` | Enables the revamped creator subscriptions experience. |
| `creator_subscriptions_subscribe_action_tweet_menu_enabled` | bool | `true` | `true` | Shows a Subscribe action in the post overflow menu. |
| `creator_subscriptions_subscribe_button_tweet_detail_enabled` | bool | `true` | `true` | Shows a Subscribe button on the post detail page. |
| `creator_subscriptions_subscriber_count_enabled` | bool | `false` | `false` | Shows the subscriber count on creator profiles. |
| `creator_subscriptions_subscriber_count_min_displayed` | int | `1` | `1` | Minimum subscriber count before the count is displayed. |
| `creator_subscriptions_subscription_count_enabled` | bool | `true` | `true` | Shows the number of subscriptions a user has. |
| `creator_subscriptions_tweet_preview_api_enabled` | bool | `true` | `true` | Enables the tweet preview API for subscriber-only posts. |
| `hidden_profile_subscriptions_enabled` | bool | `true` | `true` | Enables hidden profile subscriptions (subscriptions not shown publicly). |
| `highlights_tweets_action_enabled` | bool | `true` | `true` | Enables the Highlights action on posts. |
| `highlights_tweets_action_menu_upsell_enabled` | bool | `true` | `true` | Shows an upsell in the Highlights action menu. |
| `highlights_tweets_tab_ui_enabled` | bool | `true` | `true` | Enables the Highlights tab UI on profiles. |
| `highlights_tweets_tab_upsell_enabled` | bool | `true` | `true` | Shows an upsell on the Highlights tab. |
| `highlights_tweets_upsell_on_pin_action_enabled` | bool | `false` | `false` | Shows an upsell when pinning a post. |
| `identity_verification_consent_opt_in_by_default_enabled` | bool | `true` | `true` | Opt in to identity verification consent by default. |
| `identity_verification_creator_processor` | str | `"Stripe"` | `"Stripe"` | Identity verification processor for creators ("Stripe"). |
| `identity_verification_debadging_notification_enabled` | bool | `true` | `true` | Enables notifications when a verified badge is removed. |
| `identity_verification_hide_verified_label_settings_enabled` | bool | `true` | `true` | Enables the setting to hide the verified label. |
| `identity_verification_intake_enabled` | bool | `false` | `false` | Enables identity-verification intake. |
| `identity_verification_intake_for_blue_subscribers_enabled` | bool | `false` | `false` | Enables identity-verification intake for Blue subscribers. |
| `identity_verification_notable_demo_survey` | bool | `false` | `false` | Enables a demo survey for identity verification. |
| `identity_verification_passkey_settings_enabled` | bool | `true` | `true` | Enables passkey settings in identity verification. |
| `identity_verification_settings_enabled` | bool | `true` | `true` | Enables identity verification settings. |
| `identity_verification_vendor_idv_migration_enabled` | bool | `false` | `false` | Enables migrating the identity verification vendor. |
| `ios_premium_paywall_preloaded_webview_pagesheet_modal` | bool | `true` | `true` | Presents the iOS Premium paywall as a pre-loaded webview page sheet. |
| `longform_notetweets_composer_upsell_enabled` | bool | `true` | `true` | Shows the long-form post upsell in the composer. |
| `premium_content_api_read_enabled` | bool | `false` | `false` | Enables reading Premium content via API. |
| `premium_home_nav_upgrade_upsell__variant_key_fs` | str | `""` | `""` | Variant key for the home-nav Premium upgrade upsell (empty). |
| `premium_paywall_on_app_load_delay_ms` | int | `1000` | `1000` | Delay (ms) before the Premium paywall appears on app load. |
| `premium_paywall_on_app_load_enabled` | bool | `false` | `false` | Shows the Premium paywall on app load. |
| `premium_paywall_on_app_load_fatigue_version` | int | `1` | `1` | Version of the fatigue rules for the paywall on app load. |
| `premium_paywall_on_app_load_journey_enabled` | bool | `true` | `true` | Enables the journey for the paywall on app load. |
| `premium_paywall_on_app_load_min_account_age_days` | int | `60` | `60` | Minimum account age (days) for the paywall on app load. |
| `premium_webview_paywall_custom_timelines_feature_enabled` | bool | `true` | `true` | Shows the custom-timelines feature in the Premium paywall webview. |
| `premium_webview_paywall_force_premium_tier_enabled` | bool | `false` | `false` | Forces Premium tier in the paywall webview. |
| `premium_webview_paywall_intro_offer_title_new_copy_enabled` | bool | `true` | `true` | Uses the new copy for the intro offer title in the paywall. |
| `premium_webview_paywall_offer_variant` | str | `"thanksgiving2025"` | `"thanksgiving2025"` | Offer variant shown in the paywall (value "thanksgiving2025"). |
| `premium_webview_paywall_tier_switch_all_plans_button_hidden` | bool | `true` | `true` | Hides the "all plans" tier-switch button in the paywall. |
| `premium_webview_paywall_tier_switch_upgrade_disclaimer_enabled` | bool | `true` | `true` | Shows an upgrade disclaimer on tier switch. |
| `premium_webview_paywall_video_url` | str | `"https://abs.twimg.com/videos/grok-4-key-visual.mp4"` | `"https://abs.twimg.com/videos/grok-4-key-visual.mp4"` | URL of the video shown in the Premium paywall (Grok 4 key visual). |
| `responsive_web_ad_revenue_sharing_subscriptions_dashboard_redirect_enabled` | bool | `false` | `true` ⚠ | Redirects to the ad revenue sharing subscriptions dashboard; on for this account. |
| `responsive_web_subscribers_ntab_for_creators_enabled` | bool | `false` | `false` | Enables subscribers notifications tab for creators. |
| `responsive_web_subscriptions_setting_enabled` | bool | `true` | `true` | Enables the subscriptions setting. |
| `responsive_web_twitter_blue_subscriptions_disabled` | bool | `false` | `false` | Disables Blue subscriptions. |
| `responsive_web_twitter_blue_verified_badge_ntab_empty_state_enabled` | bool | `true` | `true` | Enables verified badge empty state in notifications. |
| `responsive_web_user_badge_education_get_verified_button_enabled` | bool | `true` | `true` | Shows a "get verified" button in badge education. |
| `responsive_web_user_premium_user_gate` | bool | `false` | `false` | Gates a feature on Premium users. |
| `responsive_web_verified_ntab_hidden` | bool | `true` | `true` | Hides the verified notifications tab. |
| `subscriptions_block_ad_upsell_enabled` | bool | `false` | `false` | Enables the "block" ad-upsell. |
| `subscriptions_blue_premium_labeling_enabled` | bool | `true` | `true` | Enables Blue/Premium labelling. |
| `subscriptions_blue_verified_edit_profile_error_message_enabled` | bool | `true` | `true` | Enables a verified error message on edit profile. |
| `subscriptions_branding_checkmark_logo_enabled` | bool | `true` | `true` | Enables checkmark logo branding. |
| `subscriptions_enabled` | bool | `true` | `true` | Master switch for Subscriptions. |
| `subscriptions_feature_1002` | bool | `true` | `true` | Premium feature entitlement 1002 flag. |
| `subscriptions_feature_1003` | bool | `true` | `true` | Premium feature entitlement 1003 flag. |
| `subscriptions_feature_1005` | bool | `true` | `true` | Premium feature entitlement 1005 flag. |
| `subscriptions_feature_1009` | bool | `true` | `true` | Premium feature entitlement 1009 flag. |
| `subscriptions_feature_1011` | bool | `true` | `true` | Premium feature entitlement 1011 flag. |
| `subscriptions_feature_1012` | bool | `true` | `true` | Premium feature entitlement 1012 flag. |
| `subscriptions_feature_1013` | bool | `false` | `false` | Premium feature entitlement 1013 flag. |
| `subscriptions_feature_1014` | bool | `true` | `true` | Premium feature entitlement 1014 flag. |
| `subscriptions_feature_account_analytics` | bool | `true` | `true` | Entitlement: account analytics. |
| `subscriptions_feature_article_composer` | bool | `true` | `true` | Entitlement: Article composer. |
| `subscriptions_feature_can_gift_premium` | bool | `false` | `true` ⚠ | Entitlement: can gift Premium; on for this account. |
| `subscriptions_feature_create_premium_content` | bool | `false` | `false` | Entitlement: create premium content. |
| `subscriptions_feature_extend_profile` | bool | `false` | `false` | Entitlement: extended profile. |
| `subscriptions_feature_hide_subscriptions` | bool | `true` | `true` | Entitlement: hide subscriptions. |
| `subscriptions_feature_highlights` | bool | `true` | `true` | Entitlement: Highlights. |
| `subscriptions_feature_labs_1004` | bool | `true` | `true` | Labs feature entitlement 1004. |
| `subscriptions_feature_organization_affiliates` | bool | `true` | `true` | Entitlement: organization affiliates. |
| `subscriptions_feature_organization_x_hiring` | bool | `false` | `false` | Entitlement: organization X Hiring. |
| `subscriptions_feature_premium_insights` | bool | `true` | `true` | Entitlement: Premium insights. |
| `subscriptions_feature_premium_jobs` | bool | `false` | `false` | Entitlement: Premium jobs. |
| `subscriptions_gifting_help_url` | str | `"https://x.com/messages/compose?recipient_id=[redacted]"` | `"https://x.com/messages/compose?recipient_id=[redacted]"` | Help URL for gifting (DM link to a support account; recipient id redacted). |
| `subscriptions_gifting_premium_intervals_enabled` | bool | `true` | `true` | Enables gifting intervals. |
| `subscriptions_gifting_premium_intro_copy_enabled` | bool | `false` | `false` | Enables intro copy for gifting. |
| `subscriptions_gifting_tooltip_discount_label` | bool | `false` | `false` | Shows a discount label on the gifting tooltip. |
| `subscriptions_gifting_tooltip_enabled` | bool | `false` | `false` | Enables the gifting tooltip. |
| `subscriptions_hide_ad_upsell_enabled` | bool | `false` | `false` | Enables "hide ad" upsell. |
| `subscriptions_is_blue_verified_review_status_profile_enabled` | bool | `true` | `true` | Shows blue-verified review status on profile. |
| `subscriptions_long_video_upload` | bool | `true` | `true` | Enables long video upload for Premium. |
| `subscriptions_management_billing_label_enabled` | bool | `true` | `true` | Enables the billing label. |
| `subscriptions_management_failed_payment_api_call_enabled` | bool | `true` | `true` | Enables the failed-payment API call. |
| `subscriptions_management_failed_payment_menu_alert_enabled` | bool | `false` | `false` | Shows the failed-payment alert in the menu. |
| `subscriptions_management_failed_payment_message_premium_enabled` | bool | `false` | `false` | Shows the failed-payment message for Premium. |
| `subscriptions_management_failed_payment_paywall_banner_enabled` | bool | `true` | `true` | Shows the failed-payment banner in paywall. |
| `subscriptions_management_failed_payment_profile_card_enabled` | bool | `false` | `false` | Shows the failed-payment card on profile. |
| `subscriptions_management_fetch_next_billing_time` | bool | `true` | `true` | Fetches next billing time. |
| `subscriptions_management_manage_subtext_update_enabled` | bool | `false` | `false` | Updates the manage subtext. |
| `subscriptions_management_query_active_price` | bool | `true` | `true` | Queries the active price. |
| `subscriptions_management_renew_module_api_enabled` | bool | `true` | `true` | Enables the renew module API. |
| `subscriptions_management_renew_module_enabled` | bool | `true` | `true` | Enables the renew module. |
| `subscriptions_management_tier_switch_polling_enabled` | bool | `true` | `true` | Polls during tier switch. |
| `subscriptions_management_tier_switch_success_screen_enabled` | bool | `true` | `true` | Shows tier-switch success screen. |
| `subscriptions_management_use_active_price` | bool | `true` | `true` | Uses the active price. |
| `subscriptions_marketing_page_compare_table_ctas_enabled` | bool | `false` | `false` | Enables CTAs in the compare table. |
| `subscriptions_marketing_page_discounts_enabled` | bool | `true` | `true` | Enables discounts on the marketing page. |
| `subscriptions_marketing_page_feature_highlights_enabled` | bool | `false` | `false` | Enables feature highlights on the marketing page. |
| `subscriptions_marketing_page_fetch_promotions` | bool | `true` | `true` | Fetches promotions. |
| `subscriptions_marketing_page_free_trial_enabled` | bool | `true` | `true` | Enables free trial on the marketing page. |
| `subscriptions_marketing_page_include_tax_enabled` | bool | `true` | `true` | Includes tax in marketing prices. |
| `subscriptions_marketing_page_new_disclaimer_enabled` | bool | `false` | `false` | Enables the new disclaimer. |
| `subscriptions_marketing_page_offer_ends_at_msec` | int | `1739246400000` | `1739246400000` | Offer end timestamp (ms epoch, Feb 2025). |
| `subscriptions_marketing_page_retention_paywall_new_button_label` | bool | `false` | `false` | New button label on the retention paywall. |
| `subscriptions_marketing_page_social_proof_enabled` | bool | `false` | `false` | Shows social proof. |
| `subscriptions_marketing_page_stripe_optimization_enabled` | bool | `true` | `true` | Enables Stripe optimization. |
| `subscriptions_mute_ad_upsell_enabled` | bool | `false` | `false` | Enables "mute" ad upsell. |
| `subscriptions_offers_churn_prevention_enabled` | bool | `true` | `true` | Enables churn-prevention offers. |
| `subscriptions_offers_dynamic_upsells_enabled` | bool | `true` | `true` | Enables dynamic upsells. |
| `subscriptions_offers_in_tier_switch_enabled` | bool | `false` | `false` | Shows offers within tier switch. |
| `subscriptions_offers_intro_title_new_copy_enabled` | bool | `false` | `false` | Uses new intro title copy. |
| `subscriptions_offers_localized_pricing_enabled` | bool | `false` | `false` | Enables localized pricing. |
| `subscriptions_offers_paywall_urgent_heading_enabled` | bool | `false` | `false` | Uses an urgent heading. |
| `subscriptions_offers_premium_nav_indicator_enabled` | bool | `false` | `false` | Shows the Premium nav indicator for offers. |
| `subscriptions_offers_premium_nav_indicator_variant` | str | `""` | `""` | Variant of the Premium nav indicator (empty). |
| `subscriptions_offers_special_perk_enabled` | bool | `false` | `false` | Enables special perks. |
| `subscriptions_offers_upgrade_offer_home_nav_upsell_enabled` | bool | `false` | `false` | Enables upgrade offer in home nav. |
| `subscriptions_offers_upgrade_offer_sidebar_upsell_enabled` | bool | `false` | `false` | Enables upgrade offer in sidebar. |
| `subscriptions_offers_user_location_is_usa` | bool | `false` | `true` ⚠ | Flag indicating the user location is the USA; true for this account (default false). |
| `subscriptions_premium_experiment_nav_text` | bool | `false` | `false` | Enables experiment on Premium nav text. |
| `subscriptions_premium_hub_ad_free_link_enabled` | bool | `true` | `true` | Shows ad-free link in the Premium hub. |
| `subscriptions_premium_hub_boost_block_enabled` | bool | `true` | `true` | Shows Boost block in the hub. |
| `subscriptions_premium_hub_insights_block_enabled` | bool | `true` | `true` | Shows Insights block in the hub. |
| `subscriptions_premium_hub_more_benefits_section_enabled` | bool | `true` | `true` | Shows the more-benefits section. |
| `subscriptions_premium_tiers_default_interval` | str | `"Month"` | `"Month"` | Default billing interval ("Month"). |
| `subscriptions_premium_tiers_default_product` | str | `"BlueVerified"` | `"BlueVerified"` | Default product ("BlueVerified"). |
| `subscriptions_premium_tiers_hide_basic` | bool | `false` | `false` | Hides the Basic tier. |
| `subscriptions_premium_tiers_hide_basic_webview_paywall` | bool | `false` | `false` | Hides Basic in the webview paywall. |
| `subscriptions_premium_tiers_order_variant` | str | `"variant_a"` | `"variant_a"` | Tier order variant ("variant_a"). |
| `subscriptions_quick_free_trials_low_threshold_screen_enabled` | bool | `false` | `true` ⚠ | Enables the low-threshold screen for quick free trials; on for this account. |
| `subscriptions_quick_free_trials_ui_enabled` | bool | `false` | `true` ⚠ | Enables the quick free trial UI; on for this account. |
| `subscriptions_report_ad_upsell_enabled` | bool | `false` | `false` | Enables report-ad upsell. |
| `subscriptions_sign_up_enabled` | bool | `false` | `true` ⚠ | Enables Premium signup; on for this account. |
| `subscriptions_stripe_testing` | bool | `false` | `false` | Enables Stripe testing mode. |
| `subscriptions_upsells_analytics_eligibility_query_enabled` | bool | `false` | `false` | Enables analytics eligibility query for upsells. |
| `subscriptions_upsells_analytics_fix_enabled` | bool | `true` | `true` | Enables an analytics fix for upsells. |
| `subscriptions_upsells_analytics_profile_enabled` | bool | `true` | `true` | Enables the profile analytics upsell. |
| `subscriptions_upsells_analytics_profile_variant` | str | `"Impressions"` | `"Impressions"` | Variant of the profile analytics upsell ("Impressions"). |
| `subscriptions_upsells_api_enabled` | bool | `false` | `false` | Enables the upsells API. |
| `subscriptions_upsells_app_tab_bar_analytics_upsell_enabled` | bool | `false` | `false` | Enables analytics upsell on the app tab bar. |
| `subscriptions_upsells_articles_post_composer_promo_variant_enabled` | bool | `false` | `false` | Promo variant for Articles in the composer. |
| `subscriptions_upsells_articles_profile_promo_variant_enabled` | bool | `false` | `false` | Promo variant for Articles on profile. |
| `subscriptions_upsells_bookmarks_screen_enabled` | bool | `false` | `false` | Enables bookmarks screen upsell. |
| `subscriptions_upsells_bookmarks_screen_variant` | str | `""` | `""` | Variant for bookmarks upsell (empty). |
| `subscriptions_upsells_dm_card_enabled` | bool | `false` | `false` | Enables the DM card upsell. |
| `subscriptions_upsells_edit_post_promo_variant_enabled` | bool | `false` | `false` | Promo variant for edit post. |
| `subscriptions_upsells_explore_sidebar_analytics_upsell_enabled` | bool | `false` | `false` | Enables explore-sidebar analytics upsell. |
| `subscriptions_upsells_explore_sidebar_analytics_upsell_variant` | str | `""` | `""` | Variant for explore-sidebar upsell (empty). |
| `subscriptions_upsells_get_verified_button_promo_variant_enabled` | bool | `false` | `false` | Promo variant for the Get Verified button. |
| `subscriptions_upsells_get_verified_button_variant` | str | `""` | `""` | Variant for the Get Verified button (empty). |
| `subscriptions_upsells_get_verified_profile` | bool | `true` | `true` | Shows Get Verified on profile. |
| `subscriptions_upsells_get_verified_profile_card` | bool | `true` | `true` | Shows the Get Verified profile card. |
| `subscriptions_upsells_get_verified_profile_card_promo_variant_enabled` | bool | `false` | `false` | Promo variant for the profile card. |
| `subscriptions_upsells_get_verified_profile_card_variant` | str | `"variant_a"` | `"variant_a"` | Variant of the profile card ("variant_a"). |
| `subscriptions_upsells_get_verified_profile_rotation_basic_upgrade_enabled` | bool | `true` | `true` | Enables rotation for Basic upgrade. |
| `subscriptions_upsells_get_verified_profile_rotation_enabled` | bool | `true` | `true` | Enables Get Verified rotation. |
| `subscriptions_upsells_highlights_profile_promo_variant_enabled` | bool | `false` | `false` | Promo variant for Highlights profile. |
| `subscriptions_upsells_home_nav_migration_enabled` | bool | `false` | `false` | Enables home nav migration. |
| `subscriptions_upsells_home_sidebar_migration_enabled` | bool | `false` | `false` | Enables home sidebar migration. |
| `subscriptions_upsells_longform_sidebar_variant` | str | `""` | `""` | Variant of the long-form sidebar upsell (empty). |
| `subscriptions_upsells_monetization_redesign_enabled` | bool | `true` | `true` | Enables the monetization redesign upsells. |
| `subscriptions_upsells_post_analytics_promo_variant_enabled` | bool | `false` | `false` | Promo variant for post analytics. |
| `subscriptions_upsells_post_composer_variant` | str | `""` | `""` | Variant for post composer (empty). |
| `subscriptions_upsells_post_details_analytics_enabled` | bool | `true` | `true` | Shows post details analytics upsell. |
| `subscriptions_upsells_post_engagements_enabled` | bool | `false` | `false` | Enables post engagement upsells. |
| `subscriptions_upsells_post_engagements_variant` | str | `"analytics_popup"` | `"analytics_popup"` | Variant of post engagements upsell ("analytics_popup"). |
| `subscriptions_upsells_post_limit_toast` | bool | `true` | `true` | Shows the post-limit toast. |
| `subscriptions_upsells_premium_home_nav` | str | `"default"` | `"default"` | Premium home nav mode ("default"). |
| `subscriptions_upsells_premium_home_nav_promo_variant_enabled` | bool | `false` | `false` | Promo variant for Premium home nav. |
| `subscriptions_upsells_premium_nav_migration_enabled` | bool | `false` | `false` | Enables Premium nav migration. |
| `subscriptions_upsells_profile_card_enabled` | bool | `false` | `false` | Enables profile card upsell. |
| `subscriptions_upsells_profile_sidebar_analytics_upsell_enabled` | bool | `false` | `false` | Enables profile-sidebar analytics upsell. |
| `subscriptions_upsells_profile_sidebar_analytics_upsell_variant` | str | `""` | `""` | Variant for profile sidebar (empty). |
| `subscriptions_upsells_radar_sidebar_enabled` | bool | `false` | `false` | Enables Radar sidebar upsell. |
| `subscriptions_upsells_radar_sidebar_variant` | str | `""` | `""` | Variant for Radar sidebar (empty). |
| `subscriptions_upsells_radar_video_url_desktop` | str | `"https://abs.twimg.com/images/radar_promo_v2.mp4"` | `"https://abs.twimg.com/images/radar_promo_v2.mp4"` | Desktop promo video URL for Radar. |
| `subscriptions_upsells_radar_video_url_mobile` | str | `"https://abs.twimg.com/images/radar_promo_v2.mp4"` | `"https://abs.twimg.com/images/radar_promo_v2.mp4"` | Mobile promo video URL for Radar. |
| `subscriptions_upsells_reply_boost_enabled` | bool | `false` | `false` | Enables reply boost upsell. |
| `subscriptions_upsells_reply_boost_popup_enabled` | bool | `true` | `true` | Enables the reply boost popup. |
| `subscriptions_upsells_reply_boost_variant` | str | `""` | `""` | Variant for reply boost (empty). |
| `subscriptions_upsells_right_sidebar_variant` | str | `""` | `""` | Variant for right sidebar (empty). |
| `subscriptions_upsells_rweb_analytics_fallback_destination` | str | `""` | `""` | Fallback destination for analytics upsell (empty). |
| `subscriptions_upsells_settings_analytics_upsell_enabled` | bool | `false` | `false` | Enables settings analytics upsell. |
| `subscriptions_upsells_sidebar_default_promo_variant_enabled` | bool | `false` | `false` | Promo variant for the default sidebar. |
| `subscriptions_upsells_track_interactions_enabled` | bool | `false` | `false` | Tracks interactions with upsells. |
| `subscriptions_upsells_verified_profile_sidebar_enabled` | bool | `false` | `false` | Enables the verified profile sidebar upsell. |
| `subscriptions_upsells_verified_profile_sidebar_variant` | str | `"variant_d"` | `"variant_d"` | Variant for verified profile sidebar ("variant_d"). |
| `subscriptions_upsells_verified_profile_visitor_upsell_enabled` | bool | `true` | `true` | Enables visitor upsell on verified profiles. |
| `subscriptions_upsells_verified_profile_visitor_upsell_variant` | str | `"variant_b"` | `"variant_b"` | Variant for visitor upsell ("variant_b"). |
| `subscriptions_upsells_visitor_get_verified_age_gate_enabled` | bool | `true` | `true` | Applies age gate to the visitor Get Verified upsell. |
| `subscriptions_verification_info_is_identity_verified_enabled` | bool | `true` | `true` | Shows "identity verified" in verification info. |
| `subscriptions_verification_info_verified_since_enabled` | bool | `true` | `true` | Shows "verified since" in verification info. |
| `subscriptions_verified_to_premium_enabled` | bool | `false` | `false` | Enables verified-to-Premium conversion. |
| `super_follow_android_web_subscription_enabled` | bool | `false` | `true` ⚠ | Enables Android web subscription for Super Follow; on for this account. |
| `super_follow_exclusive_tweet_creation_api_enabled` | bool | `true` | `true` | Enables the exclusive-post creation API. |
| `super_follow_onboarding_application_perks_enabled` | bool | `true` | `true` | Enables perks in onboarding. |
| `super_follow_onboarding_granular_pricing_enabled` | bool | `true` | `true` | Enables granular pricing in onboarding. |
| `super_follow_subscriptions_tax_calculation_enabled` | bool | `true` | `true` | Enables tax calculation for Super Follow subscriptions. |
| `super_follow_web_application_enabled` | bool | `false` | `true` ⚠ | Enables web application for Super Follow; on for this account. |
| `super_follow_web_deactivate_enabled` | bool | `true` | `true` | Enables deactivation on web. |
| `super_follow_web_debug_enabled` | bool | `false` | `false` | Enables Super Follow web debug. |
| `super_follow_web_edit_perks_enabled` | bool | `true` | `true` | Enables editing perks on web. |
| `super_follow_web_onboarding_enabled` | bool | `true` | `true` | Enables web onboarding. |
| `verified_phone_label_enabled` | bool | `false` | `false` | Enables the verified phone label. |

### Ads / Promote

66 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `active_ad_campaigns_query_enabled` | bool | `false` | `true` ⚠ | Enables the query listing active ad campaigns (Ads / Quick Promote surfaces); on for this account but off by default. |
| `ads_spacing_client_fallback_minimum_spacing` | int | `2` | `1` ⚠ | Minimum spacing (in timeline items) between ads when the client falls back to local ad spacing; this account gets 1 versus a default of 2. |
| `ads_spacing_client_fallback_minimum_spacing_verified_blue` | int | `3` | `3` | Client-fallback minimum ad spacing applied to verified (Blue) users. |
| `branded_features_is_branded_likes_on_tweet_content_enabled` | bool | `true` | `true` | Enables branded likes (sponsored like effects) in post content. |
| `branded_features_search_overlay_animations_enabled` | bool | `true` | `true` | Enables animations on the branded-features search overlay. |
| `branded_like_preview_enabled` | bool | `false` | `false` | Enables a preview of branded likes. |
| `gryphon_hide_quick_promote` | bool | `false` | `false` | Hides Quick Promote in Gryphon. |
| `post_ctas_fetch_enabled` | bool | `false` | `false` | Enables fetching calls-to-action attached to posts. |
| `post_ctas_render_enabled` | bool | `false` | `false` | Enables rendering of post CTAs. |
| `promoted_badge_placement_position` | str | `"right_tweet_header_ad_label"` | `"right_tweet_header_ad_label"` | Placement of the promoted badge ("right_tweet_header_ad_label"). |
| `responsive_web_ad_formats_enable_dismiss_in_home_urt` | bool | `true` | `true` | Allows dismissing ads in the home URT timeline. |
| `responsive_web_ad_formats_hide_vanity_for_business_account` | bool | `false` | `false` | Hides the vanity for business accounts in ad formats. |
| `responsive_web_ad_formats_media_overlay_enabled` | bool | `true` | `true` | Enables the media overlay ad format. |
| `responsive_web_ad_formats_website_cta_enabled` | bool | `true` | `true` | Enables the website call-to-action ad format. |
| `responsive_web_ad_revenue_sharing_bounce_all_legacy_to_creator_studio_enabled` | bool | `true` | `true` | Redirects legacy ad revenue sharing to Creator Studio. |
| `responsive_web_ad_revenue_sharing_dashboard_redirect_enabled` | bool | `false` | `false` | Enables redirect to the ad revenue sharing dashboard. |
| `responsive_web_ad_revenue_sharing_enabled` | bool | `true` | `true` | Enables ad revenue sharing for creators. |
| `responsive_web_ad_revenue_sharing_number_of_impressions` | int | `5` | `5` | Impression count threshold related to ad revenue sharing eligibility. |
| `responsive_web_ad_revenue_sharing_onboarding_redirect_enabled` | bool | `false` | `true` ⚠ | Redirects onboarding to ad revenue sharing; on for this account. |
| `responsive_web_ad_revenue_sharing_setup_enabled` | bool | `false` | `true` ⚠ | Enables ad revenue sharing setup; on for this account. |
| `responsive_web_ad_revenue_sharing_total_earnings_enabled` | bool | `false` | `false` | Shows total earnings in ad revenue sharing. |
| `responsive_web_ad_revenue_sharing_url_update_enabled` | bool | `true` | `true` | Enables the URL update for ad revenue sharing. |
| `responsive_web_android_quick_promote_stripe_elements_enabled` | bool | `false` | `false` | Enables Stripe Elements in Android Quick Promote. |
| `responsive_web_commerce_shop_spotlight_enabled` | bool | `false` | `false` | Enables commerce shop spotlight. |
| `responsive_web_dcm_2_enabled` | bool | `true` | `true` | Enables DCM 2 (ad conversion measurement). |
| `responsive_web_live_commerce_enabled` | bool | `false` | `false` | Enables live commerce. |
| `responsive_web_ocf_reportflow_promoted_enabled` | bool | `false` | `false` | Enables reports for promoted posts. |
| `responsive_web_qp_ads_screening_dialog_enabled` | bool | `false` | `false` | Enables the Quick Promote ads screening dialog. |
| `responsive_web_qp_boost_content_check_enabled` | bool | `true` | `false` ⚠ | Enables the Quick Promote boost content check; disabled for this account. |
| `responsive_web_qp_boost_content_check_min_delay_seconds` | int | `11` | `0` ⚠ | Minimum delay (s) for the content check; lowered for this account. |
| `responsive_web_qp_budgets_by_billing_currency_enabled` 🆕 | bool | `false` | `false` | Enables budgets by billing currency in Quick Promote. |
| `responsive_web_qp_full_popup_enabled` | bool | `true` | `true` | Enables the Quick Promote full popup. |
| `responsive_web_qp_keyword_targeting_enabled` | bool | `false` | `false` | Enables keyword targeting in Quick Promote. |
| `responsive_web_qp_new_boost_analytics_enabled` | bool | `false` | `true` ⚠ | Enables new boost analytics; on for this account. |
| `responsive_web_qp_new_payment_enabled` | bool | `false` | `false` | Enables the new payment flow in Quick Promote. |
| `responsive_web_qp_paused_policy_hint_enabled` | bool | `true` | `true` | Shows the paused-policy hint. |
| `responsive_web_qp_paused_rejection_reasons_enabled` | bool | `true` | `true` | Shows paused rejection reasons. |
| `responsive_web_qp_skip_objective_enabled` | bool | `true` | `true` | Skips the objective step. |
| `responsive_web_qp_two_screens_enabled` | bool | `true` | `true` | Enables the two-screens flow. |
| `responsive_web_quick_promote_cta_enabled` | bool | `true` | `true` | Enables the Quick Promote CTA. |
| `responsive_web_quick_promote_high_budget_tier_enabled` | bool | `false` | `true` ⚠ | Enables the high budget tier; on for this account. |
| `responsive_web_remove_qp_ad_label_enabled` | bool | `true` | `true` | Removes the Quick Promote ad label. |
| `responsive_web_video_promoted_logging_enabled` | bool | `false` | `true` ⚠ | Enables promoted video logging; on for this account. |
| `rweb_promoted_tweet_max_text_lines` | int | `0` | `2` ⚠ | Maximum text lines for promoted posts; set to 2 for this account (0 by default). |
| `rweb_quick_promote_action_menu_enabled` | bool | `true` | `true` | Enables Quick Promote in the action menu. |
| `rweb_quick_promote_boost_enabled` | bool | `false` | `false` | Enables boost via Quick Promote. |
| `rweb_quick_promote_gold_verified_boost_enabled` | bool | `true` | `true` | Enables gold-verified boost. |
| `rweb_quick_promote_third_party_boost_enabled` | bool | `false` | `true` ⚠ | Enables third-party boost; on for this account. |
| `rweb_ssp_ads_enabled` | bool | `false` | `false` | Enables SSP (supply-side platform) ads. |
| `rweb_ssp_ads_premium_bypass_enabled` | bool | `false` | `false` | Lets Premium bypass SSP ads. |
| `rweb_ssp_ads_refresh_enabled` | bool | `false` | `false` | Enables SSP ads refresh. |
| `rweb_tweets_boosting_enabled` | bool | `false` | `false` | Enables boosting for posts. |
| `tweet_limited_actions_config_dpa_enabled` | bool | `true` | `true` | Enables limited actions for dynamic product ads. |
| `unified_cards_clip_long_media_aspect_ratio` | float | `0.1` | `0.1` | Aspect ratio threshold for clipping long media in cards. |
| `unified_cards_clip_long_media_promoted_content_enabled` | bool | `true` | `true` | Clips long media in promoted cards. |
| `unified_cards_destination_url_params_enabled` 🆕 | bool | `false` | `false` | Enables destination URL params in unified cards. |
| `unified_cards_details_component_title_max_lines` | int | `2` | `2` | Max lines for the details title in unified cards. |
| `unified_cards_dpa_cta_button_enabled` | bool | `false` | `false` | Enables the DPA CTA button. |
| `unified_cards_dpa_hide_vanity` | bool | `true` | `true` | Hides vanity on DPA cards. |
| `unified_cards_dpa_metadata_enabled` | bool | `true` | `true` | Enables DPA metadata on cards. |
| `unified_cards_dpa_placeholder_media_key` | list | `[redacted]` | `[redacted]` | Placeholder media keys for DPA cards; value redacted. |
| `unified_cards_force_show_cta_bar_card_types` | list | `[]` (0 items) | `[]` (0 items) | Card types that always show the CTA bar (empty). |
| `unified_cards_hide_collection_ad_card_details` | bool | `true` | `true` | Hides collection ad card details. |
| `unified_cards_install_button_redesign_enabled` | bool | `true` | `true` | Enables the redesigned install button. |
| `unified_cards_use_subtitle_as_vanity_fallback_in_collection` | bool | `true` | `true` | Uses subtitle as vanity fallback in collections. |
| `unified_cards_web_card_redesign_variant` | str | `"cta_bottom_bar"` | `"cta_bottom_bar"` | Web card redesign variant ("cta_bottom_bar"). |

### Creator / Monetization / Analytics

99 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `articles_preview_enabled` | bool | `true` | `true` | Enables previews of Articles (long-form posts) before publishing. |
| `articles_rest_api_enabled` | bool | `true` | `true` | Enables the REST API used for Articles. |
| `c9s_community_composer_hashtag_suggestions_enabled` | bool | `true` | `true` | Enables hashtag suggestions in the Community composer. |
| `composer_add_geo_network_conversation_controls` | bool | `true` | `true` | Adds geo/network conversation controls to the composer. |
| `composer_composition_signals_enabled` | bool | `true` | `true` | Enables collection of composition signals (e.g., typing behaviour) in the composer. |
| `creator_monetization_profile_subscription_tweets_tab_enabled` | bool | `true` | `true` | Enables the subscription-posts tab on creator profiles. |
| `creator_studio_nav_enabled` | bool | `true` | `true` | Shows Creator Studio in navigation. |
| `hashfetti_all_hashflags` | bool | `false` | `false` | Shows all hashflags with hashfetti confetti effects. |
| `hashfetti_also_match_query` | bool | `false` | `false` | Also matches the search query for hashfetti. |
| `hashfetti_duration_ms` | int | `4000` | `4000` | Duration (ms) of the hashfetti effect. |
| `hashfetti_enabled` | bool | `true` | `true` | Enables hashfetti (confetti on hashtags). |
| `hashfetti_particle_count` | int | `30` | `30` | Particle count for hashfetti. |
| `insights_ai_trends_enabled` | bool | `false` | `true` ⚠ | Enables AI trends in Insights; on for this account. |
| `insights_ai_trends_limit` | int | `5` | `5` | Maximum number of AI trends in Insights. |
| `insights_ai_trends_score_threshold` | float | `0.4` | `0.4` | Score threshold for AI trends in Insights. |
| `insights_chart_filter_enabled` | bool | `true` | `true` | Enables chart filters in Insights. |
| `insights_paginated_metrics_backend_enabled` | bool | `false` | `true` ⚠ | Enables the paginated-metrics backend for Insights; on for this account. |
| `insights_premium_initial_days_back` | int | `7` | `7` | Initial days back displayed for Premium Insights. |
| `insights_preview_splash_metrics_enabled` | bool | `false` | `false` | Enables the preview splash metrics in Insights. |
| `insights_previews_enabled` | bool | `false` | `true` ⚠ | Enables Insights previews; on for this account. |
| `longform_notetweets_composition_without_claims_enabled` | bool | `false` | `false` | Allows long-form composition without entitlement claims. |
| `longform_notetweets_consumption_enabled` | bool | `true` | `true` | Enables consumption of long-form posts. |
| `longform_notetweets_inline_media_enabled` | bool | `false` | `false` | Enables inline media in long-form posts. |
| `longform_notetweets_max_tweet_per_thread` | int | `25` | `25` | Maximum number of posts in a long-form thread. |
| `longform_notetweets_max_weighted_character_length` | int | `25000` | `25000` | Maximum weighted character length for a long-form post. |
| `longform_notetweets_mobile_richtextinput` | bool | `false` | `false` | Enables rich text input on mobile for long-form. |
| `longform_notetweets_rich_composition_enabled` | int | `1` | `1` | Rich composition mode for long-form posts (value 1). |
| `longform_notetweets_rich_text_read_enabled` | bool | `true` | `true` | Enables reading rich text of long-form posts. |
| `longform_notetweets_rich_text_timeline_enabled` | bool | `false` | `false` | Enables rich text in timelines for long-form posts. |
| `longform_notetweets_scheduling_non_reply_enabled` | bool | `true` | `true` | Enables scheduling non-reply long-form posts. |
| `longform_notetweets_tweet_storm_enabled` | bool | `true` | `true` | Enables tweet storms for long-form posts. |
| `longform_reader_mode_view_in_reader_mode_entry_button_enabled` | bool | `false` | `false` | Shows the "View in reader mode" entry button. |
| `responsive_web_alt_text_nudges_enabled` | bool | `true` | `true` | Enables alt-text nudges. |
| `responsive_web_alt_text_nudges_settings_enabled` | bool | `true` | `true` | Enables alt-text nudge settings. |
| `responsive_web_alt_text_translations_enabled` | bool | `true` | `true` | Enables alt-text translations. |
| `responsive_web_composer_autosave_debounce_ms` | int | `2000` | `2000` | Debounce (ms) for composer autosave. |
| `responsive_web_composer_autosave_enabled` | bool | `false` | `false` | Enables composer autosave. |
| `responsive_web_composer_configurable_video_player_enabled` | bool | `false` | `false` | Enables a configurable video player in composer. |
| `responsive_web_creator_preferences_previews_enabled_setting` | bool | `true` | `true` | Enables the creator preferences previews setting. |
| `responsive_web_edit_tweet_api_enabled` | bool | `true` | `true` | Enables the edit-post API. |
| `responsive_web_edit_tweet_composition_enabled` | bool | `true` | `true` | Enables edit-post composition. |
| `responsive_web_edit_tweet_enabled` | bool | `false` | `false` | Enables editing posts in the web UI. |
| `responsive_web_edit_tweet_perspective_enabled` | bool | `false` | `false` | Enables the edit-post perspective. |
| `responsive_web_edit_tweet_upsell_enabled` | bool | `true` | `true` | Shows an edit-post upsell. |
| `responsive_web_hashtag_highlight_is_enabled` | bool | `false` | `false` | Enables hashtag highlights. |
| `responsive_web_hashtag_highlight_show_avatar` | bool | `false` | `false` | Shows the avatar in hashtag highlights. |
| `responsive_web_hashtag_highlight_use_small_font` | bool | `false` | `false` | Uses a small font for hashtag highlights. |
| `responsive_web_image_poll_composer_enabled` | bool | `true` | `true` | Enables the image poll composer. |
| `responsive_web_in_text_shortcuts_enabled` | bool | `true` | `true` | Enables in-text shortcuts in the composer. |
| `responsive_web_one_hour_edit_window_enabled` | bool | `true` | `true` | Enables the one-hour edit window for posts. |
| `responsive_web_scheduling_threads_enabled` | bool | `true` | `true` | Enables scheduling threads. |
| `responsive_web_tweet_analytics_m3_enabled` | bool | `false` | `false` | Enables tweet analytics m3. |
| `responsive_web_tweet_drafts_threads_enabled` | bool | `true` | `true` | Enables thread drafts. |
| `responsive_web_tweet_drafts_video_enabled` | bool | `true` | `true` | Enables video drafts. |
| `responsive_web_twitter_article_batch_posts` | bool | `true` | `true` | Enables batch posts for Articles. |
| `responsive_web_twitter_article_block_limit` | int | `10000` | `10000` | Block limit for Articles. |
| `responsive_web_twitter_article_character_limit` | int | `100` | `100` | Character limit for Article titles/units. |
| `responsive_web_twitter_article_code_block_enabled` | bool | `true` | `true` | Enables code blocks in Articles. |
| `responsive_web_twitter_article_code_language_typeahead_enabled` | bool | `true` | `true` | Enables the language typeahead for code blocks. |
| `responsive_web_twitter_article_content_debounce_ms` | int | `3000` | `3000` | Debounce (ms) for Article content. |
| `responsive_web_twitter_article_latex_enabled` | bool | `true` | `true` | Enables LaTeX in Articles. |
| `responsive_web_twitter_article_markdown_block_limit` | int | `10` | `10` | Markdown block limit for Articles. |
| `responsive_web_twitter_article_markdown_enabled` | bool | `false` | `false` | Enables Markdown in Articles. |
| `responsive_web_twitter_article_media_limit` | int | `25` | `25` | Maximum media in an Article. |
| `responsive_web_twitter_article_notes_tab_enabled` | bool | `true` | `true` | Enables the Article notes tab. |
| `responsive_web_twitter_article_plain_text_enabled` | bool | `true` | `true` | Enables plain text Article paste. |
| `responsive_web_twitter_article_preview_cta_redirect_enabled` | bool | `true` | `true` | Enables preview CTA redirect. |
| `responsive_web_twitter_article_reader_enabled` | bool | `true` | `true` | Enables the Article reader. |
| `responsive_web_twitter_article_redirect_enabled` | bool | `true` | `true` | Enables Article redirects. |
| `responsive_web_twitter_article_seed_tweet_detail_enabled` | bool | `true` | `true` | Enables seed post detail for Articles. |
| `responsive_web_twitter_article_seed_tweet_enabled` | bool | `true` | `true` | Enables seed posts for Articles. |
| `responsive_web_twitter_article_table_enabled` | bool | `true` | `true` | Enables tables in Articles. |
| `responsive_web_twitter_article_title_limit` | int | `100` | `100` | Title length limit for Articles. |
| `responsive_web_twitter_article_tweet_consumption_enabled` | bool | `true` | `true` | Enables Article consumption in posts. |
| `responsive_web_video_trimmer_enabled` | bool | `false` | `false` | Enables the video trimmer. |
| `rweb_analytics_active_followers_enabled` | bool | `true` | `true` | Enables active followers in analytics. |
| `rweb_analytics_audience_compact_mode` | bool | `true` | `true` | Enables compact mode for the audience analytics. |
| `rweb_analytics_audience_xweb_enabled` | bool | `true` | `true` | Enables the xweb audience analytics. |
| `rweb_analytics_control_v2_enabled` | bool | `true` | `true` | Enables control v2 in analytics. |
| `rweb_analytics_export_data_content_enabled` | bool | `true` | `true` | Enables exporting content data. |
| `rweb_analytics_export_data_enabled` | bool | `true` | `true` | Enables exporting data. |
| `rweb_analytics_hourly_overview_enabled` | bool | `false` | `false` | Enables the hourly overview. |
| `rweb_analytics_in_out_network_enabled` | bool | `true` | `true` | Enables in/out-of-network analytics. |
| `rweb_analytics_live_details_enabled` | bool | `true` | `true` | Enables live details in analytics. |
| `rweb_analytics_live_overview_enabled` | bool | `true` | `true` | Enables the live overview. |
| `rweb_analytics_nav_item_enabled` | bool | `false` | `false` | Shows the analytics nav item. |
| `rweb_analytics_post_details_realtime_enabled` | bool | `true` | `true` | Enables real-time post details. |
| `rweb_analytics_realtime_active_followers_enabled` 🆕 | bool | `true` | `true` | Enables real-time active followers. |
| `rweb_analytics_spaces_details_enabled` | bool | `true` | `true` | Enables Spaces details. |
| `rweb_analytics_spaces_overview_enabled` | bool | `true` | `true` | Enables Spaces overview. |
| `rweb_analytics_theme` | bool | `false` | `false` | Analytics theme variant. |
| `rweb_analytics_upsell_variant` | str | `""` | `""` | Analytics upsell variant (empty). |
| `rweb_analytics_xweb_content_page` | bool | `true` | `true` | Enables the xweb content page in analytics. |
| `rweb_composer_emoji_typeahead_enabled` | bool | `true` | `true` | Enables emoji typeahead in the composer. |
| `rweb_modal_composer_animation_enabled` | bool | `true` | `true` | Enables composer modal animation. |
| `rweb_tipjar_consumption_enabled` | bool | `false` | `false` | Enables Tip Jar consumption. |
| `video_upload_metadata_title_enabled` | bool | `false` | `false` | Enables title metadata for video uploads. |
| `xstudio_embed_origin` | str | `"https://studio.x.com"` | `"https://studio.x.com"` | Origin of the X Studio embed. |
| `xstudio_rweb_live_studio_enabled` | bool | `true` | `true` | Enables live studio in X Studio. |

### Communities

53 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `c9s_auto_collapse_community_detail_header_enabled` | bool | `true` | `true` | Auto-collapses the community detail header on scroll. |
| `c9s_community_answer_box_enabled` | bool | `true` | `true` | Enables the Community answer box. |
| `c9s_community_answer_box_join_page_enabled` | bool | `true` | `true` | Shows the Community answer box on the join page. |
| `c9s_community_hashtags_carousel_enabled` | bool | `true` | `true` | Enables the Community hashtags carousel. |
| `c9s_community_hashtags_enabled` | bool | `true` | `true` | Enables hashtags within Communities. |
| `c9s_community_list_setting_enabled` | bool | `true` | `true` | Enables the Community list setting. |
| `c9s_community_question_box_enabled` | bool | `true` | `true` | Enables the Community question box (prompt for new members). |
| `c9s_community_searchtags_enabled` | bool | `true` | `true` | Enables searchtags in Communities. |
| `c9s_community_tweet_search_enabled` | bool | `true` | `true` | Enables post search inside a Community. |
| `c9s_enabled` | bool | `true` | `true` | Master switch for Communities (internally "c9s"). |
| `c9s_list_members_action_api_enabled` | bool | `false` | `false` | Enables the list-members action API for Communities. |
| `c9s_max_community_answer_length` | int | `280` | `280` | Maximum length of a Community answer, in characters. |
| `c9s_max_community_description_length` | int | `160` | `160` | Maximum length of a Community description, in characters. |
| `c9s_max_community_name_length` | int | `30` | `30` | Maximum length of a Community name, in characters. |
| `c9s_max_community_question_length` | int | `160` | `160` | Maximum length of a Community question, in characters. |
| `c9s_max_rule_count` | int | `10` | `10` | Maximum number of rules per Community. |
| `c9s_max_rule_description_length` | int | `160` | `160` | Maximum length of a Community rule description, in characters. |
| `c9s_max_rule_name_length` | int | `60` | `60` | Maximum length of a Community rule name, in characters. |
| `c9s_nav_list_activity_details_enabled` | bool | `false` | `false` | Shows activity details in the navigation community list. |
| `c9s_question_editing_box_enabled` | bool | `true` | `true` | Enables editing of the Community question box. |
| `c9s_spotlight_creation_enabled` | bool | `true` | `true` | Enables creating Community spotlights. |
| `c9s_tab_visibility` | str | `"always"` | `"always"` | Controls when the Communities tab is visible (value "always"). |
| `c9s_timelines_media_tab_enabled` | bool | `true` | `true` | Enables the media tab in Community timelines. |
| `c9s_tweet_anatomy_moderator_badge_enabled` | bool | `true` | `true` | Shows a moderator badge in post anatomy within Communities. |
| `communities_adult_content_setting_display` | bool | `true` | `true` | Displays the adult-content setting for Communities. |
| `communities_adult_content_setting_enabled` | bool | `true` | `true` | Enables the adult-content setting for Communities. |
| `communities_analytics_enabled` | bool | `true` | `true` | Enables Communities analytics. |
| `communities_auto_report_setting_enabled` | bool | `true` | `true` | Enables the auto-report setting for Communities. |
| `communities_enable_explore_tab` | bool | `true` | `true` | Enables the Communities tab in Explore. |
| `communities_enable_explore_topic_carousel` | bool | `true` | `true` | Enables the topic carousel in Communities explore. |
| `communities_enable_top_posts_search` | bool | `true` | `true` | Enables top-posts search for Communities. |
| `communities_global_communities_latest_post_search_enabled` | bool | `true` | `true` | Enables latest-post search across all Communities. |
| `communities_global_communities_post_search_enabled` | bool | `true` | `true` | Enables global post search across Communities. |
| `communities_home_top_timeline_enabled` | bool | `true` | `true` | Enables the top timeline of Communities on home. |
| `communities_moderation_log_enabled` | bool | `true` | `true` | Enables the Community moderation log. |
| `communities_non_member_reply_enabled` | bool | `true` | `true` | Allows non-members to reply to Community posts. |
| `communities_show_broadcast_option_in_composer` | bool | `true` | `true` | Shows the broadcast option in the composer for Communities. |
| `communities_spam_settings_enabled` | bool | `true` | `true` | Enables spam settings for Communities. |
| `communities_topic_carousel_enabled` | bool | `true` | `true` | Enables the topic carousel in Communities. |
| `communities_topic_display` | bool | `true` | `true` | Displays topics on Communities. |
| `communities_topics_enabled` | bool | `true` | `true` | Enables topics in Communities. |
| `communities_web_enable_tweet_community_results_fetch` | bool | `true` | `true` | Enables fetching community results for a post on web. |
| `responsive_web_communityboost_download_data_enabled` | bool | `false` | `false` | Enables download of Community Boost data. |
| `responsive_web_communityboost_form_enabled` | bool | `false` | `false` | Enables the Community Boost form. |
| `responsive_web_communityboost_mixed_pivot_enabled` | bool | `false` | `false` | Enables the Community Boost mixed pivot. |
| `tweet_limited_actions_config_community_tweet_community_deleted` | list | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (20 items) | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (20 items) | Actions limited on posts in deleted communities. |
| `tweet_limited_actions_config_community_tweet_community_not_found` | list | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (20 items) | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (20 items) | Actions limited on posts in not-found communities. |
| `tweet_limited_actions_config_community_tweet_community_suspended` | list | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (20 items) | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (20 items) | Actions limited on posts in suspended communities. |
| `tweet_limited_actions_config_community_tweet_hidden` | list | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (19 items) | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (19 items) | Actions limited on hidden community posts. |
| `tweet_limited_actions_config_community_tweet_member_removed` | list | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (20 items) | `[add_to_bookmarks, add_to_moment, embed, follow, …]` (20 items) | Actions limited when a member was removed from the community. |
| `tweet_limited_actions_config_community_tweet_non_member` | list | `[react, reply_down_vote]` (2 items) | `[react, reply_down_vote]` (2 items) | Actions limited for non-members on community posts. |
| `tweet_limited_actions_config_community_tweet_non_member_closed_community` | list | `[react, reply_down_vote]` (2 items) | `[react, reply_down_vote]` (2 items) | Actions limited for non-members of a closed community. |
| `tweet_limited_actions_config_community_tweet_non_member_public_community` | list | `[react, reply_down_vote]` (2 items) | `[react, reply_down_vote]` (2 items) | Actions limited for non-members of a public community. |

### Spaces / Live / Sports

91 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `broadcast_live_chat_enabled` | bool | `true` | `true` | Enables live chat on broadcasts. |
| `broadcast_live_chat_input_max_char_limit` | int | `200` | `200` | Maximum characters allowed in a broadcast live chat message. |
| `live_event_docking_enabled` | bool | `true` | `true` | Enables docking of live events. |
| `live_event_interstitial_seen_cache_enabled` | bool | `true` | `true` | Caches whether the live-event interstitial was seen. |
| `live_event_multi_video_auto_advance_dock_enabled` | bool | `true` | `true` | Enables auto-advance in docked multi-video live events. |
| `live_event_multi_video_auto_advance_enabled` | bool | `true` | `true` | Enables auto-advance for multi-video live events. |
| `live_event_multi_video_auto_advance_fullscreen_enabled` | bool | `false` | `false` | Enables auto-advance in fullscreen multi-video live events. |
| `live_event_multi_video_enabled` | bool | `true` | `true` | Enables multi-video live events. |
| `live_event_timeline_default_refresh_rate_interval_seconds` | int | `30` | `30` | Default timeline refresh interval (s) for live events. |
| `live_event_timeline_minimum_refresh_rate_interval_seconds` | int | `10` | `10` | Minimum timeline refresh interval (s) for live events. |
| `live_event_timeline_server_controlled_refresh_rate_enabled` | bool | `true` | `true` | Lets the server control the live-event timeline refresh rate. |
| `livepipeline_client_enabled` | bool | `true` | `true` | Enables the live pipeline (push) client. |
| `livepipeline_tweetengagement_enabled` | bool | `true` | `true` | Enables live updates of post engagement counts. |
| `march_madness_brackets_enabled` | bool | `true` | `true` | Enables March Madness brackets. |
| `march_madness_brackets_enabled_loggedin_sidebar_popup` | bool | `false` | `false` | Enables the March Madness brackets popup in the logged-in sidebar. |
| `netzdg_in_spaces_enabled` | bool | `false` | `false` | Enables NetzDG (German network enforcement law) handling in Spaces. |
| `responsive_web_audio_space_ring_home_timeline` | bool | `false` | `false` | Shows audio space ring on the home timeline. |
| `responsive_web_live_scheduled_broadcast_countdown_enabled` | bool | `false` | `false` | Shows a countdown for scheduled live broadcasts. |
| `responsive_web_live_video_viewer_session_enabled` 🆕 | bool | `true` | `true` | Enables live video viewer sessions. |
| `responsive_web_livecut_native_share_enabled` | bool | `true` | `true` | Enables native sharing of Livecut clips. |
| `responsive_web_mlb_athlete_tray_enabled` 🆕 | bool | `false` | `false` | Enables the MLB athlete tray. |
| `responsive_web_mlb_enabled` 🆕 | bool | `false` | `false` | Master switch for MLB (baseball) features. |
| `responsive_web_mlb_favorite_teams_enabled` 🆕 | bool | `false` | `false` | Enables MLB favorite teams. |
| `responsive_web_mlb_game_animations_enabled` 🆕 | bool | `false` | `false` | Enables MLB game animations. |
| `responsive_web_mlb_game_chat_enabled` 🆕 | bool | `false` | `false` | Enables MLB game chat. |
| `responsive_web_mlb_game_feed_enabled` 🆕 | bool | `false` | `false` | Enables the MLB game feed. |
| `responsive_web_mlb_game_odds_enabled` 🆕 | bool | `false` | `false` | Enables MLB game odds. |
| `responsive_web_mlb_hub_home_tab_enabled` 🆕 | bool | `false` | `false` | Enables MLB hub home tab. |
| `responsive_web_mlb_hub_media_tab_enabled` 🆕 | bool | `false` | `false` | Enables MLB hub media tab. |
| `responsive_web_mlb_lineup_season_stats_enabled` 🆕 | bool | `false` | `false` | Enables MLB lineup season stats. |
| `responsive_web_mlb_live_card_collapse_enabled` 🆕 | bool | `false` | `false` | Enables collapsing the MLB live card. |
| `responsive_web_mlb_logged_out_game_enabled` 🆕 | bool | `false` | `false` | Enables MLB logged-out game view. |
| `responsive_web_mlb_pregame_matchup_enabled` 🆕 | bool | `false` | `false` | Enables MLB pre-game matchup. |
| `responsive_web_mlb_profile_sports_enabled` 🆕 | bool | `false` | `false` | Enables MLB sports on profile. |
| `responsive_web_mlb_reminder_snooze_enabled` 🆕 | bool | `false` | `false` | Enables MLB reminder snooze. |
| `responsive_web_mlb_reminders_enabled` 🆕 | bool | `false` | `false` | Enables MLB reminders. |
| `responsive_web_mlb_scorecard_odds_enabled` 🆕 | bool | `false` | `false` | Enables MLB scorecard odds. |
| `responsive_web_mlb_sidebar_enabled` 🆕 | bool | `false` | `false` | Enables the MLB sidebar. |
| `responsive_web_nfl_enabled` | bool | `true` | `true` | Master switch for NFL features. |
| `responsive_web_nfl_game_dock_enabled` 🆕 | bool | `false` | `false` | Enables the NFL game dock. |
| `responsive_web_nfl_hub_home_tab_enabled` | bool | `true` | `true` | Enables the NFL hub home tab. |
| `responsive_web_nfl_profile_sports_enabled` | bool | `true` | `true` | Enables NFL on profiles. |
| `responsive_web_nfl_sidebar_enabled` | bool | `true` | `true` | Enables the NFL sidebar. |
| `responsive_web_nfl_sidebar_for_all_users_enabled` | bool | `false` | `true` ⚠ | Shows the NFL sidebar to all users; on for this account. |
| `responsive_web_nfl_sidebar_max_live_games` | int | `3` | `3` | Maximum live games in the NFL sidebar. |
| `responsive_web_nfl_team_picker_enabled` | bool | `true` | `true` | Enables the NFL team picker. |
| `responsive_web_ocf_reportflow_spaces_enabled` | bool | `false` | `false` | Enables reports for Spaces. |
| `responsive_web_sports_live_profile_rings_enabled` | bool | `true` | `true` | Shows live sports rings on profiles. |
| `responsive_web_sports_profile_endpoint_enabled` 🆕 | bool | `true` | `true` | Enables the sports profile endpoint. |
| `responsive_web_sports_sidebar_league_logos_enabled` 🆕 | bool | `false` | `false` | Shows league logos in the sports sidebar. |
| `responsive_web_tv_cast_enabled` | bool | `true` | `true` | Enables TV cast. |
| `rweb_live_broadcast_rewind_enabled` | bool | `true` | `true` | Enables rewind in live broadcasts. |
| `rweb_live_dock_enabled` | bool | `true` | `true` | Enables live docking. |
| `rweb_spaces_invite_search_enabled` | bool | `true` | `true` | Enables invite search in Spaces. |
| `rweb_spaces_next_codec_enabled` | bool | `true` | `true` | Enables the next-generation codec in Spaces. |
| `rweb_sports_post_context_enabled` | bool | `true` | `true` | Enables sports post context. |
| `rweb_sports_post_context_footer_enabled` | bool | `true` | `true` | Enables the sports post-context footer. |
| `rweb_sports_post_context_header_enabled` | bool | `false` | `false` | Enables the sports post-context header. |
| `spaces_2022_h2_clipping` | bool | `true` | `true` | Enables clipping in Spaces. |
| `spaces_2022_h2_clipping_consumption` | bool | `true` | `true` | Enables consuming Spaces clips. |
| `spaces_2022_h2_clipping_duration_seconds` | int | `30` | `30` | Duration (s) of Spaces clips. |
| `spaces_2022_h2_spaces_communities` | bool | `true` | `true` | Enables Spaces with Communities. |
| `spaces_dtx_opus_dtx_enabled` | bool | `false` | `false` | Enables Opus DTX in Spaces. |
| `spaces_live_chat_enabled` | bool | `false` | `true` ⚠ | Enables live chat in Spaces; on for this account. |
| `spaces_video_admins_enabled` | bool | `false` | `false` | Enables video admins in Spaces. |
| `spaces_video_consumption_enabled` | bool | `true` | `true` | Enables video consumption in Spaces. |
| `spaces_video_creation_enabled` | bool | `false` | `false` | Enables video creation in Spaces. |
| `spaces_video_speakers_enabled` | bool | `false` | `false` | Enables video speakers in Spaces. |
| `voice_consumption_enabled` | bool | `true` | `true` | Enables voice consumption. |
| `voice_rooms_cohosts_enabled` | bool | `true` | `true` | Enables co-hosts in voice rooms. |
| `voice_rooms_discovery_page_enabled` | bool | `false` | `false` | Enables the voice room discovery page. |
| `voice_rooms_employee_only_enabled` | bool | `false` | `false` | Restricts voice rooms to employees. |
| `voice_rooms_recent_search_audiospace_ring_enabled` | bool | `true` | `true` | Shows audio space ring in recent search. |
| `voice_rooms_search_results_page_audiospace_ring_enabled` | bool | `false` | `false` | Shows audio space ring on the search results page. |
| `voice_rooms_typeahead_audiospace_ring_enabled` | bool | `true` | `true` | Shows audio space ring in typeahead. |
| `voice_rooms_web_space_creation` | bool | `true` | `true` | Enables creating Spaces on web. |
| `x_sports_game_chat_should_hide_logos` | bool | `false` | `false` | Hides logos in sports game chat. |
| `x_sports_nfl_favorite_teams_enabled` | bool | `true` | `true` | Enables NFL favorite teams. |
| `x_sports_nfl_game_chat_enabled` | bool | `true` | `true` | Enables NFL game chat. |
| `x_sports_nfl_game_chat_team_pick_enabled` | bool | `true` | `true` | Enables the team-pick step in NFL game chat; on by default now (was a deviation on 2026-09-23). |
| `x_sports_nfl_game_feed_enabled` | bool | `true` | `true` | Enables the NFL game feed. |
| `x_sports_nfl_game_odds_card_enabled` | bool | `true` | `true` | Enables NFL odds card. |
| `x_sports_nfl_game_player_props_enabled` | bool | `false` | `false` | Enables NFL player props. |
| `x_sports_nfl_game_roster_enabled` | bool | `false` | `false` | Enables NFL roster. |
| `x_sports_nfl_hub_home_timeline_tag` | str | `"1000000000000000005"` | `"1000000000000000005"` | Home timeline tag ID for the NFL hub. |
| `x_sports_nfl_schedule_reminder_enabled` | bool | `true` | `true` | Enables NFL schedule reminders. |
| `x_sports_nfl_scorecard_odds_disabled` | bool | `true` | `true` | Disables NFL scorecard odds. |
| `x_sports_play_video_enabled` | bool | `true` | `true` | Enables playing sports video. |
| `x_sports_post_context_enabled` 🆕 | bool | `false` | `false` | Enables sports post context. |
| `x_sports_post_context_min_spacing` | int | `3` | `3` | Minimum spacing for sports post context. |
| `x_sports_post_context_same_game_min_spacing` | int | `20` | `20` | Minimum spacing for same-game post context. |

### Media / Video / Upload

78 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `blue_longer_video_enabled` | bool | `false` | `false` | Allows longer video uploads for Blue subscribers. |
| `explore_relaunch_max_video_loop_threshold_sec` | int | `5` | `5` | Maximum video loop duration (seconds) in relaunched Explore. |
| `gryphon_video_docking_enabled` | bool | `true` | `true` | Enables video docking in Gryphon. |
| `immersive_video_status_linkable_timestamps` 🆕 | bool | `false` | `false` | Enables linkable timestamps in immersive video. |
| `media_async_upload_amplify_duration_threshold` | int | `600` | `600` | Duration threshold (s) above which async media upload uses amplified/extended handling. |
| `media_async_upload_longer_dm_video_max_video_duration` | int | `600` | `600` | Maximum video duration (s) for longer DM videos via async upload. |
| `media_async_upload_longer_video_max_video_duration` | int | `21660` | `21660` | Maximum duration (s) for longer videos (about 6 hours) via async upload. |
| `media_async_upload_longer_video_max_video_size` | int | `16384` | `16384` | Maximum size (MB) for longer videos via async upload. |
| `media_async_upload_longer_video_resolution_selector` | bool | `false` | `false` | Shows a resolution selector for longer-video uploads. |
| `media_async_upload_max_avatar_gif_size` | int | `5` | `5` | Maximum size (MB) of an animated GIF avatar. |
| `media_async_upload_max_gif_size` | int | `15` | `15` | Maximum GIF upload size (MB). |
| `media_async_upload_max_image_size` | int | `5` | `5` | Maximum image upload size (MB). |
| `media_async_upload_max_video_duration` | int | `1200` | `1200` | Maximum standard video duration (s), i.e. 20 minutes. |
| `media_async_upload_max_video_size` | int | `512` | `512` | Maximum standard video upload size (MB). |
| `media_edge_to_edge_content_enabled` | bool | `false` | `false` | Enables edge-to-edge media content layout. |
| `optimized_sru_parameters_client_side_timeout_ms` | int | `600000` | `600000` | Client-side timeout (ms) for optimized SRU (segmented resumable upload) parameters. |
| `optimized_sru_parameters_enabled` | int | `1` | `1` | Enables optimized SRU upload parameters (value 1). |
| `optimized_sru_parameters_ideal_upload_time_ms` | int | `80000` | `80000` | Ideal upload time (ms) per segment for SRU. |
| `optimized_sru_parameters_max_segment_bytes` | int | `8387584` | `8387584` | Maximum segment size in bytes for SRU uploads (~8 MB). |
| `optimized_sru_parameters_min_segment_bytes` | int | `4194304` | `4194304` | Minimum segment size in bytes for SRU uploads (~4 MB). |
| `responsive_web_card_conversion_hoisted` | str | `"off"` | `"off"` | Card conversion hoisting mode ("off"). |
| `responsive_web_card_image_poll_enabled` | bool | `true` | `true` | Enables image poll cards. |
| `responsive_web_card_image_poll_shuffle_enabled` | bool | `true` | `true` | Enables shuffling of image poll options. |
| `responsive_web_card_image_poll_sort_by_vote_count_enabled` | bool | `true` | `true` | Enables sorting image poll results by vote count. |
| `responsive_web_card_preconnect_enabled` | bool | `false` | `false` | Enables card preconnect. |
| `responsive_web_card_reminder_enabled` | bool | `false` | `false` | Enables reminders on cards. |
| `responsive_web_carousel_v2_media_detail_enabled` | bool | `false` | `false` | Enables carousel v2 media detail. |
| `responsive_web_convert_card_video_to_gif_enabled` | bool | `false` | `false` | Converts card videos to GIFs. |
| `responsive_web_hevc_upload_preview_enabled` | bool | `false` | `false` | Enables HEVC upload preview. |
| `responsive_web_instream_video_redesign_enabled` | bool | `true` | `true` | Enables the redesigned in-stream video. |
| `responsive_web_media_download_video_share_menu_enabled` | bool | `true` | `true` | Shows video download in the media share menu. |
| `responsive_web_media_upload_appendmulti_enabled` | bool | `true` | `true` | Enables multi-part append in media upload. |
| `responsive_web_media_upload_appendmulti_max_concurrent_requests` | int | `4` | `4` | Maximum concurrent requests for multi-append upload. |
| `responsive_web_media_upload_appendmulti_max_request_bytes` | int | `25165824` | `25165824` | Maximum request size (bytes) for multi-append. |
| `responsive_web_media_upload_appendmulti_max_segment_bytes` | int | `8388608` | `8388608` | Maximum segment size (bytes) for multi-append. |
| `responsive_web_media_upload_appendmulti_min_file_bytes` | int | `1048576` | `1048576` | Minimum file size (bytes) to use multi-append. |
| `responsive_web_media_upload_appendmulti_min_segment_bytes` | int | `262144` | `262144` | Minimum segment size (bytes) for multi-append. |
| `responsive_web_media_upload_appendmulti_pre_read_blob` | bool | `false` | `false` | Pre-reads the blob before multi-append. |
| `responsive_web_media_upload_appendmulti_target_wire_send_time_ms` | int | `30000` | `30000` | Target wire send time (ms) for multi-append. |
| `responsive_web_media_upload_host` | str | `"upload.x.com"` | `"upload.x.com"` | Host used for media uploads ("upload.x.com"). |
| `responsive_web_media_upload_limit_2g` | int | `250` | `250` | Media upload size limit on 2G networks. |
| `responsive_web_media_upload_limit_3g` | int | `1500` | `1500` | Media upload size limit on 3G networks. |
| `responsive_web_media_upload_limit_slow_2g` | int | `150` | `150` | Media upload size limit on slow-2G networks. |
| `responsive_web_media_upload_md5_hashing_enabled` | bool | `true` | `true` | Enables MD5 hashing for media uploads. |
| `responsive_web_media_upload_metrics_enabled` | bool | `true` | `true` | Enables upload metrics. |
| `responsive_web_media_upload_target_jpg_pixels_per_byte` | int | `6` | `1` ⚠ | Target JPEG pixels-per-byte for compression; lowered for this account. |
| `responsive_web_native_emojis_enabled` | bool | `true` | `true` | Uses native emojis. |
| `responsive_web_offscreen_video_scroller_removal_enabled` | bool | `false` | `false` | Removes offscreen video scroller. |
| `responsive_web_video_autoplay_bandwidth_threshold_enabled` | bool | `true` | `true` | Uses a bandwidth threshold for video autoplay. |
| `responsive_web_video_pcomplete_enabled` | bool | `true` | `true` | Enables video percent-complete tracking. |
| `rweb_media_carousel_enabled` | bool | `true` | `true` | Enables the media carousel. |
| `rweb_media_multi_requests_default_pool_size` | int | `1` | `1` | Default pool size for multi media requests. |
| `rweb_media_multi_requests_enabled` | bool | `true` | `true` | Enables multi media requests. |
| `rweb_mixed_media_uploads_cap` | int | `4` | `4` | Cap on mixed-media uploads (4). |
| `rweb_modal_animation_enabled` | bool | `true` | `true` | Enables modal animations. |
| `rweb_modal_animation_timing_function` | str | `"cubic-bezier(0.25, 0.1, 0.25, 1)"` | `"cubic-bezier(0.25, 0.1, 0.25, 1)"` | CSS timing function for modal animations. |
| `rweb_modal_overlay_color_dark` | str | `"rgba(0, 0, 0, 0.5)"` | `"rgba(0, 0, 0, 0.5)"` | Dark-theme modal overlay colour. |
| `rweb_modal_overlay_color_light` | str | `"rgba(180, 180, 182, 0.5)"` | `"rgba(180, 180, 182, 0.5)"` | Light-theme modal overlay colour. |
| `rweb_mvr_blurred_media_interstitial_enabled` | bool | `true` | `true` | Enables a blurred media interstitial (MVR). |
| `rweb_picture_in_picture_enabled` | bool | `true` | `true` | Enables picture-in-picture. |
| `rweb_save_video_progress_enabled` | bool | `false` | `false` | Saves video progress. |
| `rweb_video_logged_in_analytics_enabled` | bool | `true` | `true` | Enables logged-in video analytics. |
| `rweb_video_pip_enabled` | bool | `true` | `true` | Enables video PiP. |
| `rweb_video_screen_enabled` | bool | `false` | `false` | Enables the video screen. |
| `rweb_video_tagging_enabled` | bool | `true` | `true` | Enables video tagging. |
| `sensitive_media_settings_enabled` | bool | `false` | `false` | Enables sensitive media settings. |
| `video_attribution_display_over_video_cards_enabled` | bool | `true` | `true` | Displays video attribution over video cards. |
| `web_video_caption_repositioning_enabled` | bool | `true` | `true` | Repositions captions on web video. |
| `web_video_hls_android_mse_enabled` | bool | `true` | `true` | Enables HLS via MSE on Android web. |
| `web_video_hls_mp4_threshold_sec` | int | `0` | `0` | Threshold (s) for HLS vs MP4. |
| `web_video_hls_variant_version` | str | `"1"` | `"1"` | HLS variant version. |
| `web_video_hlsjs_version` | str | `"1.6.0"` | `"1.6.0"` | hls.js version used ("1.6.0"). |
| `web_video_persist_bandwidth_estimate_enabled` | bool | `true` | `true` | Persists the bandwidth estimate. |
| `web_video_persist_player_preferences_enabled` | bool | `false` | `false` | Persists player preferences. |
| `web_video_playback_rate_enabled` | bool | `true` | `true` | Enables playback-rate control. |
| `web_video_prefetch_playlist_autoplay_disabled` | bool | `false` | `false` | Disables playlist prefetch on autoplay. |
| `web_video_safari_hlsjs_enabled` | bool | `true` | `true` | Uses hls.js on Safari. |
| `web_video_transcribed_captions_enabled` | bool | `true` | `true` | Enables transcribed captions. |

### Search / Explore / Trends / Topics

28 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `explore_graphql_enabled` | bool | `true` | `true` | Uses GraphQL for the Explore page. |
| `explore_relaunch_enable_auto_play` | bool | `false` | `true` ⚠ | Enables autoplay in the relaunched Explore page; on for this account. |
| `explore_relaunch_enable_immersive_web` | bool | `false` | `false` | Enables the immersive web viewer in relaunched Explore. |
| `explore_relaunch_enable_immersive_web_navigation_button` | bool | `false` | `false` | Shows the immersive-web navigation button in relaunched Explore. |
| `gryphon_search_based_deck_enabled` | bool | `false` | `false` | Enables search-based decks in Gryphon. |
| `hometimeline_pinned_tabs_management_topics_inline_limit` | int | `8` | `8` | Inline limit for topics in pinned tabs management. |
| `hometimeline_pinned_tabs_topics_enabled` | bool | `true` | `true` | Enables topics as pinned home tabs. |
| `people_search_interests_filter_enabled` | bool | `false` | `false` | Enables an interests filter in people search. |
| `responsive_web_location_spotlight_display_map` | bool | `true` | `true` | Displays a map in location spotlight. |
| `responsive_web_location_spotlight_v1_config` | bool | `true` | `true` | Enables the location spotlight v1 config. |
| `responsive_web_location_spotlight_v1_display` | bool | `true` | `true` | Enables the location spotlight v1 display. |
| `responsive_web_sidebar_ttf_enabled` | bool | `false` | `false` | Enables time-to-first-frame metrics for the sidebar. |
| `responsive_web_trends_setting_new_endpoints` | bool | `true` | `true` | Uses new endpoints for trends settings. |
| `responsive_web_trends_ui_community_notes_enabled` | bool | `false` | `false` | Enables Community Notes in the trends UI. |
| `responsive_web_trends_ui_enable_new_sidebar` | bool | `false` | `false` | Enables the new trends sidebar. |
| `responsive_web_trends_ui_hide_news_sidebar_on_explore` | bool | `false` | `false` | Hides the news sidebar on Explore. |
| `responsive_web_trends_ui_sidebar_topic_id` | str | `"Top Stories"` | `"Top Stories"` | Topic ID for the trends sidebar ("Top Stories"). |
| `responsive_web_trends_ui_top_articles` | bool | `true` | `true` | Shows top articles in trends. |
| `rweb_search_media_enabled` | bool | `true` | `true` | Enables media in search. |
| `rweb_starter_packs_topics_tab_enabled` | bool | `false` | `false` | Enables the topics tab for starter packs. |
| `search_timelines_graphql_enabled` | bool | `true` | `true` | Uses GraphQL for search timelines. |
| `topic_landing_page_clearer_controls_enabled` | bool | `true` | `true` | Enables clearer controls on topic landing pages. |
| `topic_landing_page_cta_text` | str | `"control"` | `"control"` | Experiment bucket for topic landing CTA text ("control"). |
| `topic_landing_page_share_enabled` | bool | `true` | `true` | Enables sharing of topic landing pages. |
| `topics_context_controls_followed_variation` | str | `"see_more"` | `"see_more"` | Variation of context controls for followed topics ("see_more"). |
| `topics_context_controls_implicit_context_x_enabled` | bool | `true` | `true` | Enables implicit context controls for X topics. |
| `topics_context_controls_implicit_variation` | str | `"see_more"` | `"see_more"` | Variation for implicit context controls ("see_more"). |
| `topics_context_controls_inline_prompt_enabled` | bool | `false` | `false` | Enables the inline prompt for topic context controls. |

### Timeline / Ranking / Home

63 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `android_ui_nested_quote_tweet_preview_enabled` 🆕 | bool | `false` | `false` | Android UI flag for the nested quote-post preview; listed in the web payload but Android-oriented. |
| `co_timeline_reset_period_minutes` | int | `20` | `1440` ⚠ | Reset period (minutes) for the Communities timeline; this account has a longer period than default. |
| `co_timeline_topic_filter_enabled` | bool | `false` | `true` ⚠ | Enables a topic filter in the Communities timeline; on for this account but off by default. |
| `focused_timeline_actions_onboarding_likes` | int | `3` | `3` | Number of likes used to trigger focused timeline-actions onboarding. |
| `follow_nudge_conversation_enabled` | bool | `false` | `false` | Enables follow nudges in conversations. |
| `gryphon_accountsync_polling_interval_ms` | int | `300000` | `300000` | Polling interval (ms) for account sync in the legacy TweetDeck-based client (internal name "gryphon"). |
| `gryphon_faster_cell_entrance` | bool | `true` | `true` | Enables faster cell entrance animation in Gryphon (TweetDeck/X Pro). |
| `gryphon_fps_tracking_enabled` | bool | `true` | `true` | Enables FPS tracking in Gryphon. |
| `gryphon_live_timelines_enabled` | bool | `true` | `true` | Enables live timelines in Gryphon. |
| `gryphon_motion` | bool | `false` | `false` | Enables motion/animation in Gryphon. |
| `gryphon_redux_perf_optimization_enabled` | bool | `true` | `true` | Enables Redux performance optimization in Gryphon. |
| `gryphon_redux_perf_optimization_v2_enabled` | bool | `true` | `true` | Enables the second version of the Redux performance optimization in Gryphon. |
| `gryphon_sharing_column_permission` | str | `"follow"` | `"follow"` | Permission level required to share a Gryphon column ("follow"). |
| `gryphon_sharing_deck_permission` | str | `""` | `""` | Permission level required to share a Gryphon deck (empty). |
| `gryphon_survey_enabled` | bool | `false` | `false` | Enables the Gryphon survey. |
| `gryphon_survey_url` | str | `""` | `""` | URL of the Gryphon survey (empty). |
| `gryphon_timeline_polling_latest_interval_ms` | int | `30000` | `30000` | Polling interval (ms) for the "latest" timeline in Gryphon. |
| `gryphon_timeline_polling_overrides` | str | `"explore,,60000;search,latest,60000"` | `"explore,,60000;search,latest,60000"` | Per-surface polling overrides for Gryphon timelines (explore and search/latest at 60s). |
| `gryphon_timeline_polling_top_interval_ms` | int | `120000` | `120000` | Polling interval (ms) for the "top" timeline in Gryphon. |
| `gryphon_underground_enabled` | bool | `false` | `false` | Purpose unclear from name; likely an "underground" experimental mode in Gryphon. |
| `gryphon_upgrade_premium_plus_banner_enabled` | bool | `true` | `true` | Shows the Premium+ upgrade banner in Gryphon. |
| `home_timeline_like_reactivity_enabled` | bool | `true` | `true` | Enables like-based reactivity in the home timeline. |
| `home_timeline_like_reactivity_fatigue` | int | `10` | `10` | Fatigue limit for like reactivity in home timeline. |
| `home_timeline_spheres_detail_page_muting_enabled` | bool | `true` | `true` | Enables muting on the home timeline spheres (lists) detail page. |
| `home_timeline_spheres_max_user_owned_or_subscribed_lists_count` | int | `10` | `10` | Maximum number of lists owned or subscribed to in home timeline spheres. |
| `home_timeline_spheres_ranking_mode_control_enabled` | bool | `false` | `false` | Enables the ranking-mode control for home timeline spheres. |
| `hometimeline_pinned_tabs_limit` | int | `10` | `10` | Maximum number of pinned tabs in the home timeline. |
| `hometimeline_pinned_tabs_management_pinnedsection_inline_limit` | int | `3` | `3` | Inline limit for pinned section items in pinned tabs management. |
| `new_timeline_experiment_enabled` | bool | `false` | `false` | Enables a new timeline experiment; the buckets are listed in the account's impression pointers. |
| `responsive_web_element_size_impression_scribe_enabled` | bool | `true` | `true` | Enables element-size impression scribing. |
| `responsive_web_framerate_tracking_home_enabled` | bool | `false` | `false` | Enables framerate tracking on home. |
| `responsive_web_graphql_timeline_navigation_enabled` | bool | `true` | `true` | Enables GraphQL timeline navigation. |
| `responsive_web_home_pinned_timelines_prefetch_enabled` | bool | `false` | `false` | Prefetches home pinned timelines. |
| `responsive_web_impression_tracker_refactor_enabled` | bool | `true` | `true` | Enables the refactored impression tracker. |
| `responsive_web_list_tweet_integration_enabled` | bool | `false` | `false` | Enables integration of posts in lists. |
| `responsive_web_nested_quote_preview_enabled` | bool | `true` | `true` | Enables nested quote post previews. |
| `responsive_web_pinned_replies_enabled` | bool | `false` | `false` | Enables pinned replies. |
| `responsive_web_primary_nav_route_preload_enabled` | bool | `false` | `true` ⚠ | Preloads routes for primary navigation; on for this account. |
| `responsive_web_redux_use_fragment_enabled` | bool | `false` | `false` | Uses Redux fragments. |
| `responsive_web_reply_storm_enabled` | bool | `false` | `false` | Enables reply storm handling. |
| `responsive_web_scroller_top_positioning_enabled` | bool | `false` | `false` | Enables top positioning of the scroller. |
| `responsive_web_thread_media_ensure_root_urt` | bool | `true` | `true` | Ensures root URT for thread media. |
| `responsive_web_thread_media_nav_enabled` | bool | `true` | `true` | Enables thread media navigation. |
| `responsive_web_thread_media_tooltip` | bool | `true` | `true` | Enables thread media tooltip. |
| `responsive_web_timeline_cover_killswitch_enabled` | bool | `false` | `false` | Killswitch for timeline cover. |
| `responsive_web_timeline_relay_lists_management_enabled` | bool | `false` | `false` | Enables Relay lists management. |
| `responsive_web_timeline_relay_user_lists_enabled` | bool | `false` | `false` | Enables Relay user lists. |
| `rweb_home_connect_in_menu_min_follows` | int | `100` | `100` | Minimum follows before the Connect entry appears in the home menu. |
| `rweb_home_jot_context_enabled` | bool | `true` | `true` | Enables Jot context on home. |
| `rweb_home_jot_migrate_enabled` | bool | `true` | `true` | Migrates home to Jot. |
| `rweb_home_mixer_enable_social_context_filter_social_contexts` | bool | `true` | `true` | Enables social-context filtering in Home Mixer. |
| `rweb_home_nav_single_direction_scroll_enabled` | bool | `false` | `false` | Enables single-direction scroll for home nav. |
| `rweb_home_ranked_following_enabled` | bool | `true` | `true` | Enables ranked Following timeline. |
| `rweb_home_ranked_following_min_following_count` | int | `100` | `100` | Minimum following count for ranked Following. |
| `rweb_home_refetch_on_refocus_min_delay_seconds` | int | `60` | `60` | Minimum delay (s) before refetching home on refocus. |
| `rweb_home_uas_enabled` | bool | `true` | `true` | Enables UAS on home. |
| `rweb_master_detail_enabled` | bool | `false` | `false` | Enables master-detail layout. |
| `rweb_panning_nav_behavior` | bool | `true` | `true` | Enables panning nav behavior. |
| `rweb_timeline_simple_conversation_control_education_enabled` | bool | `true` | `true` | Shows education on simple conversation controls. |
| `rweb_tweets_reply_context_hidden` | bool | `true` | `true` | Hides reply context in posts. |
| `rweb_tweets_tweet_detail_font_size` | str | `"headline2"` | `"headline2"` | Font size style for post detail ("headline2"). |
| `social_context_and_topic_context_refresh_alignment_enabled` | bool | `false` | `false` | Aligns refresh of social and topic context. |
| `timeline_scroll_pointer_events_optimization` | bool | `false` | `true` ⚠ | Optimizes pointer events during timeline scrolling; on for this account (experiment treatment). |

### Community Notes / Trust & Safety / Moderation

106 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `dash_region_specific_de_and_tr_media_transparency_items_enabled` | bool | `false` | `false` | Enables region-specific (DE and TR) media transparency items on the DSA dashboard. |
| `dash_region_specific_de_media_transparency_items_enabled` | bool | `false` | `false` | Enables region-specific (DE) media transparency items. |
| `disallowed_reply_controls_callout_enabled` | bool | `false` | `false` | Enables the callout for disallowed reply controls. |
| `disallowed_reply_controls_enabled` | bool | `false` | `false` | Enables disallowed reply controls (limits on who can reply). |
| `dont_mention_me_enabled` | bool | `true` | `true` | Enables the "Don't mention me" feature (opt out of mentions). |
| `dont_mention_me_mentions_tab_education_enabled` | bool | `true` | `true` | Shows Don't Mention Me education on the mentions tab. |
| `dont_mention_me_view_api_enabled` | bool | `true` | `true` | Enables the view API for Don't Mention Me. |
| `dsa_profile_report_flow_enabled` | bool | `false` | `false` | Enables the DSA report flow for profiles. |
| `dsa_report_flow_enabled` | bool | `false` | `false` | Enables the DSA (EU Digital Services Act) report flow. |
| `dsa_report_illegal_content_url` | str | `""` | `""` | URL for reporting illegal content under the DSA (empty here). |
| `ecd_dispute_form_link_enabled` | bool | `true` | `true` | Shows the dispute form link for enforcement/content decisions (ECD). |
| `enable_label_appealing_misinfo_enabled` | bool | `false` | `false` | Enables appeal of misinformation labels. |
| `enable_label_appealing_sensitive_content_enabled` | bool | `false` | `false` | Enables appeal of sensitive-content labels. |
| `freedom_of_speech_not_reach_author_label_enabled` | bool | `true` | `true` | Enables the "Freedom of speech, not reach" author label. |
| `freedom_of_speech_not_reach_fetch_enabled` | bool | `true` | `true` | Enables fetching of "freedom of speech, not reach" visibility data. |
| `freedom_of_speech_not_reach_pivot_enabled` | bool | `true` | `true` | Enables the "freedom of speech, not reach" pivot UI. |
| `graduated_access_invisible_treatment_enabled` | bool | `true` | `true` | Enables invisible treatment in graduated access. |
| `graduated_access_user_prompt_enabled` | bool | `true` | `true` | Enables user-facing prompts in graduated access. |
| `graphql_is_translatable_rweb_tweet_is_translatable_enabled` | bool | `true` | `true` | Uses the GraphQL is-translatable field for web posts. |
| `machine_translation_holdback_logged_in` | bool | `false` | `false` | Holdback from machine translation for logged-in users. |
| `machine_translation_holdback_logged_out` | bool | `false` | `false` | Holdback from machine translation for logged-out users. |
| `papago_tweet_translation_from_korean_entity_protected` | bool | `false` | `false` | Enables Papago translation from Korean with entity protection. |
| `papago_tweet_translation_from_korean_entity_protected_destinations` | list | `[en, ja, zh, zh-cn, …]` (7 items) | `[en, ja, zh, zh-cn, …]` (7 items) | Destination languages for Papago translation from Korean with entity protection. |
| `papago_tweet_translation_from_korean_entity_unprotected` | bool | `false` | `false` | Enables Papago translation from Korean without entity protection. |
| `papago_tweet_translation_from_korean_entity_unprotected_destinations` | list | `[id, es, th]` (3 items) | `[id, es, th]` (3 items) | Destination languages for unprotected Papago translation from Korean. |
| `papago_tweet_translation_to_korean` | bool | `false` | `false` | Enables Papago translation into Korean. |
| `papago_tweet_translation_to_korean_sources` | list | `[en, ja]` (2 items) | `[en, ja]` (2 items) | Source languages for Papago translation into Korean. |
| `profile_label_improvements_pcf_edit_profile_enabled` | bool | `true` | `true` | Enables the improved profile-label UI in edit profile (PCF). |
| `profile_label_improvements_pcf_label_in_post_enabled` | bool | `true` | `true` | Enables the improved profile label in posts. |
| `profile_label_improvements_pcf_settings_enabled` | bool | `true` | `true` | Enables the improved profile label in settings. |
| `report_center_mvp_r1_enabled` | bool | `true` | `true` | Enables Report Center MVP release 1. |
| `report_center_mvp_r2_enabled` | bool | `false` | `false` | Enables Report Center MVP release 2. |
| `responsive_web_author_labels_avatar_label_enabled` | bool | `false` | `false` | Shows author labels on the avatar. |
| `responsive_web_author_labels_focal_label_enabled` | bool | `false` | `false` | Shows author labels as the focal label. |
| `responsive_web_author_labels_handle_label_enabled` | bool | `false` | `false` | Shows author labels next to the handle. |
| `responsive_web_birdwatch_admitted_user_setting_enabled` | bool | `false` | `false` | Enables the Community Notes admitted-user setting. |
| `responsive_web_birdwatch_consumption_enabled` | bool | `true` | `true` | Enables consumption of Community Notes. |
| `responsive_web_birdwatch_country_allowed` | bool | `true` | `true` | Indicates the country is allowed for Community Notes. |
| `responsive_web_birdwatch_crowd_nmr_pivots_enabled` | bool | `true` | `true` | Enables Crowd NMR pivots in Community Notes. |
| `responsive_web_birdwatch_enforce_author_user_quotas` | bool | `true` | `true` | Enforces author quotas on Community Notes. |
| `responsive_web_birdwatch_fast_crh_time_from_note_cutoff` | int | `3600000` | `3600000` | Time cutoff (ms) from note creation for fast CRH status. |
| `responsive_web_birdwatch_fast_crh_time_from_post_cutoff` | int | `3600000` | `3600000` | Time cutoff (ms) from post creation for fast CRH status. |
| `responsive_web_birdwatch_fast_notes_badge_enabled` | bool | `false` | `false` | Enables the fast-notes badge. |
| `responsive_web_birdwatch_home_page_enabled` | bool | `false` | `false` | Enables the Community Notes home page. |
| `responsive_web_birdwatch_live_note_classification_enabled` | bool | `false` | `false` | Enables live-note classification. |
| `responsive_web_birdwatch_live_note_enabled` | bool | `true` | `true` | Enables live notes. |
| `responsive_web_birdwatch_match_page_enabled` | bool | `true` | `true` | Enables the match page. |
| `responsive_web_birdwatch_media_history_enabled` | bool | `false` | `false` | Enables media history for Community Notes. |
| `responsive_web_birdwatch_media_note_eligible_writer_impact_cutoff` | int | `2` | `2` | Writer-impact cutoff for media-note eligibility. |
| `responsive_web_birdwatch_media_notes_enabled` | bool | `true` | `true` | Enables media notes. |
| `responsive_web_birdwatch_netzdg_enabled` | bool | `false` | `false` | Enables NetzDG handling in Community Notes. |
| `responsive_web_birdwatch_note_internal_insights_enabled` | bool | `false` | `false` | Enables internal insights on notes. |
| `responsive_web_birdwatch_note_limit_enabled` | bool | `true` | `true` | Enables note limit enforcement. |
| `responsive_web_birdwatch_note_request_download_enabled` | bool | `true` | `true` | Enables downloading note requests. |
| `responsive_web_birdwatch_note_request_enabled` | bool | `true` | `true` | Enables note requests. |
| `responsive_web_birdwatch_note_request_sources_enabled` | bool | `true` | `true` | Enables sources for note requests. |
| `responsive_web_birdwatch_note_request_suggestion_enabled` | bool | `true` | `true` | Enables note request suggestions. |
| `responsive_web_birdwatch_note_writing_enabled` | bool | `false` | `false` | Enables note writing. |
| `responsive_web_birdwatch_notification_settings_enabled` | bool | `true` | `true` | Enables Community Notes notification settings. |
| `responsive_web_birdwatch_pivots_enabled` | bool | `true` | `true` | Enables pivots in Community Notes. |
| `responsive_web_birdwatch_public_suggestions_tab_enabled` | bool | `true` | `true` | Enables the public suggestions tab. |
| `responsive_web_birdwatch_rating_crowd_enabled` | bool | `true` | `true` | Enables crowd rating. |
| `responsive_web_birdwatch_rating_participant_enabled` | bool | `false` | `false` | Enables participant rating. |
| `responsive_web_birdwatch_read_sources_nudge` | str | `"control"` | `"control"` | Experiment bucket for the read-sources nudge ("control"). |
| `responsive_web_birdwatch_require_rating_before_writing_enabled` | bool | `true` | `true` | Requires rating before writing notes. |
| `responsive_web_birdwatch_self_remove_enabled` | bool | `true` | `true` | Enables self-removal of notes. |
| `responsive_web_birdwatch_show_note_request_sources_despite_top_writer_status` | bool | `false` | `false` | Shows note-request sources despite top-writer status. |
| `responsive_web_birdwatch_signup_prompt_enabled` | bool | `true` | `true` | Shows the signup prompt for Community Notes. |
| `responsive_web_birdwatch_site_enabled` | bool | `true` | `true` | Master switch for the Community Notes site. |
| `responsive_web_birdwatch_suggestion_rating_impact_cutoff` | int | `1` | `1` | Rating-impact cutoff for suggestions. |
| `responsive_web_birdwatch_suggestion_rating_impact_enabled` | bool | `true` | `true` | Enables suggestion rating impact. |
| `responsive_web_birdwatch_suggestion_writer_impact_cutoff` | int | `0` | `0` | Writer-impact cutoff for suggestions. |
| `responsive_web_birdwatch_suggestions_report_enabled` | bool | `true` | `true` | Enables suggestion reports. |
| `responsive_web_birdwatch_top_contributor_enabled` | bool | `true` | `true` | Enables the top contributor feature. |
| `responsive_web_birdwatch_top_contributor_score_cutoff` | int | `10` | `10` | Score cutoff for top contributors. |
| `responsive_web_birdwatch_translation_enabled` | bool | `true` | `true` | Enables translation of notes. |
| `responsive_web_birdwatch_url_notes_enabled` | bool | `false` | `false` | Enables URL notes. |
| `responsive_web_ocf_reportflow_appeals_enabled` | bool | `false` | `false` | Enables appeals in the report flow. |
| `responsive_web_ocf_reportflow_dms_enabled` | bool | `false` | `false` | Enables DM reports in the report flow. |
| `responsive_web_ocf_reportflow_lists_enabled` | bool | `true` | `true` | Enables list reports. |
| `responsive_web_ocf_reportflow_profiles_enabled` | bool | `true` | `true` | Enables profile reports. |
| `responsive_web_ocf_reportflow_suspension_appeals_enabled` | bool | `false` | `true` ⚠ | Enables suspension appeals in the report flow; on for this account. |
| `responsive_web_ocf_reportflow_testers` | bool | `false` | `false` | Enables report-flow tester mode. |
| `responsive_web_ocf_reportflow_tweets_enabled` | bool | `true` | `true` | Enables post reports. |
| `responsive_web_report_page_not_found` | bool | `false` | `false` | Reports page-not-found events. |
| `responsive_web_translation_feedback_enabled` | bool | `true` | `true` | Enables translation feedback. |
| `responsive_web_x_translation_enabled` | bool | `false` | `false` | Enables X translation. |
| `rweb_debugger_bug_report_email` | str | `""` | `""` | Email for debugger bug reports (empty). |
| `rweb_under_the_hood_report_enabled` | bool | `true` | `true` | Enables the "Under the hood" report. |
| `rweb_under_the_hood_report_jetfuel_enabled` 🆕 | bool | `true` | `true` | Enables the Jetfuel version of that report. |
| `sensitive_tweet_warnings_enabled` | bool | `true` | `true` | Enables sensitive post warnings. |
| `standardized_nudges_misinfo` | bool | `true` | `true` | Enables standardized misinformation nudges. |
| `toxic_reply_filter_inline_callout_enabled` | bool | `false` | `false` | Shows an inline callout for the toxic reply filter. |
| `toxic_reply_filter_settings_enabled` | bool | `false` | `false` | Enables toxic reply filter settings. |
| `trusted_friends_consumption_enabled` | bool | `true` | `true` | Enables consumption of Trusted Friends (Circle) posts. |
| `tweet_limited_actions_config_disable_state_media_autoplay` | list | `[autoplay]` (1 items) | `[autoplay]` (1 items) | Actions limited for state-media autoplay. |
| `tweet_limited_actions_config_dynamic_product_ad` | list | `[reply, retweet, quote_tweet, share_tweet_via, …]` (8 items) | `[reply, retweet, quote_tweet, share_tweet_via, …]` (8 items) | Actions limited on dynamic product ads. |
| `tweet_limited_actions_config_enabled` | bool | `true` | `true` | Master switch for limited-actions config on posts. |
| `tweet_limited_actions_config_freedom_of_speech_not_reach` | list | `[reply, retweet, quote_tweet, share_tweet_via, …]` (12 items) | `[reply, retweet, quote_tweet, share_tweet_via, …]` (12 items) | Actions limited on posts with "freedom of speech, not reach" labels. |
| `tweet_limited_actions_config_limit_trusted_friends_tweet` | list | `[retweet, quote_tweet, share_tweet_via, send_via_dm, …]` (8 items) | `[retweet, quote_tweet, share_tweet_via, send_via_dm, …]` (8 items) | Actions limited on Trusted Friends posts. |
| `tweet_limited_actions_config_non_compliant` | list | `[reply, retweet, like, react, …]` (12 items) | `[reply, retweet, like, react, …]` (12 items) | Actions limited on non-compliant posts. |
| `tweet_limited_actions_config_skip_tweet_detail` | list | `[reply]` (1 items) | `[reply]` (1 items) | Actions limited on tweet detail skip. |
| `tweet_limited_actions_config_soft_nudge_with_quote_tweet` | list | `[show_retweet_action_menu]` (1 items) | `[show_retweet_action_menu]` (1 items) | Actions limited under soft nudge with quote. |
| `tweet_with_visibility_results_all_gql_limited_actions_enabled` | bool | `false` | `false` | Applies GraphQL limited actions to all posts with visibility results. |
| `tweet_with_visibility_results_partial_gql_limited_actions_enabled` | bool | `true` | `true` | Applies GraphQL limited actions partially. |
| `tweet_with_visibility_results_prefer_gql_limited_actions_policy_enabled` | bool | `true` | `true` | Prefers the GraphQL limited-actions policy. |

### Notifications

4 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `responsive_web_priority_ntab_enabled` | bool | `true` | `true` | Enables priority notifications tab. |
| `responsive_web_priority_ntab_min_followers` | int | `500` | `500` | Minimum followers for priority notifications. |
| `responsive_web_repeat_profile_visits_notifications_device_follow_only_version_enabled` | bool | `false` | `false` | Enables repeat-visit notifications for device-follow only. |
| `responsive_web_repeat_profile_visits_notifications_enabled` | bool | `false` | `false` | Enables repeat profile visit notifications. |

### Profile / Identity

21 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `immersive_viewer_enable_profile_viewer` | bool | `false` | `false` | Enables the profile viewer in the immersive viewer. |
| `responsive_web_device_follow_without_user_follow_enabled` | bool | `false` | `false` | Allows device follow without user follow. |
| `responsive_web_graphql_skip_user_profile_image_extensions_enabled` | bool | `false` | `false` | Skips user profile image extensions in GraphQL. |
| `responsive_web_multiple_account_limit` | int | `5` | `5` | Maximum number of accounts switchable on web. |
| `responsive_web_profile_about_enabled` | bool | `true` | `true` | Enables the About section on profiles. |
| `responsive_web_profile_redesign_enabled` | bool | `true` | `true` | Enables the profile redesign. |
| `responsive_web_profile_redirect_enabled` | bool | `true` | `true` | Enables profile redirects. |
| `responsive_web_profile_spotlight_v0_config` | bool | `true` | `true` | Enables profile spotlight v0 config. |
| `responsive_web_profile_spotlight_v0_display` | bool | `true` | `true` | Enables profile spotlight v0 display. |
| `responsive_web_spud_enabled` | bool | `true` | `true` | Purpose unclear from name; likely "spud" component, an internal feature. |
| `twitter_delegate_normal_limit` | int | `5` | `5` | Maximum delegates for normal accounts. |
| `twitter_delegate_subscriber_limit` | int | `25` | `25` | Maximum delegates for subscriber accounts. |
| `user_display_name_max_limit` | int | `50` | `50` | Maximum length for a display name. |
| `xprofile_consumption_enabled` | bool | `false` | `false` | Enables xprofile (structured profile) consumption. |
| `xprofile_editing_enabled` | bool | `false` | `false` | Enables xprofile editing. |
| `xprofile_emojis_enabled` | bool | `true` | `true` | Enables emojis in xprofile. |
| `xprofile_profile_button_enabled` | bool | `false` | `false` | Shows the xprofile profile button. |
| `xprofile_section_visibility_enabled` | bool | `false` | `false` | Enables section visibility in xprofile. |
| `xprofile_work_history_consumption_enabled` | bool | `true` | `true` | Enables consumption of work history. |
| `xprofile_work_history_domain_enabled` | bool | `false` | `true` ⚠ | Enables the work-history domain; on for this account. |
| `xprofile_work_history_enabled` | bool | `true` | `true` | Enables work history in xprofile. |

### Compliance / Legal / Privacy / Cookies

22 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `complat_management_enabled` | bool | `false` | `false` | Purpose unclear from name; likely a "complat" (compliance/platform) management console toggle. |
| `complat_responsive_web_castle_minting_enabled` | bool | `false` | `false` | Purpose unclear from name; likely enables Castle (bot/fraud detection) token minting in the compliance platform flow. |
| `complat_x_migration_enabled` 🆕 | bool | `false` | `false` | Purpose unclear from name; likely a compliance-platform migration to the X stack (new in the 2026-10-01 capture). |
| `krs_registration_enabled` | bool | `false` | `false` | Purpose unclear from name; likely enables registration for a KRS (Korea-related or key-registration) program. |
| `responsive_web_3rd_party_category_double_click` | int | `3` | `3` | Cookie-consent category for DoubleClick (3rd-party category id). |
| `responsive_web_3rd_party_category_google_platform` | int | `2` | `2` | Cookie-consent category for Google platform. |
| `responsive_web_3rd_party_category_player_card` | int | `3` | `3` | Cookie-consent category for player cards. |
| `responsive_web_3rd_party_category_sentry` | int | `2` | `2` | Cookie-consent category for Sentry. |
| `responsive_web_3rd_party_category_sign_in_with_apple` | int | `2` | `2` | Cookie-consent category for Sign in with Apple. |
| `responsive_web_account_access_language_lo_banners` | str | `"control"` | `"control"` | Experiment bucket for account-access language banners for logged-out users ("control"). |
| `responsive_web_account_access_language_lo_splash_sidebar` | str | `"control"` | `"control"` | Experiment bucket for account-access language splash/sidebar ("control"). |
| `responsive_web_cookie_compliance_1st_party_killswitch_list` | list | `[]` (0 items) | `[]` (0 items) | List of first-party cookie compliance killswitches (empty). |
| `responsive_web_cookie_compliance_banner_enabled` | bool | `false` | `false` | Enables the cookie-compliance banner. |
| `responsive_web_cookie_compliance_banner_update_enabled` | bool | `false` | `false` | Enables the cookie-compliance banner update. |
| `responsive_web_cookie_compliance_gingersnap_enabled` | bool | `false` | `false` | Enables the Gingersnap cookie compliance. |
| `responsive_web_cookie_consent_signal_enabled` | bool | `false` | `false` | Enables the cookie consent signal. |
| `responsive_web_gpc_enabled` | bool | `false` | `true` ⚠ | Enables Global Privacy Control (GPC); on for this account. |
| `responsive_web_personalization_id_sync_enabled` | bool | `false` | `false` | Enables personalization ID sync. |
| `responsive_web_send_cookies_metadata_enabled` | bool | `true` | `true` | Sends cookie metadata. |
| `responsive_web_timezone_header_enabled` | bool | `false` | `false` | Sends a timezone header. |
| `rweb_age_assurance_flow_enabled` | bool | `true` | `true` | Enables the age assurance flow. |
| `ucpd_enabled` | bool | `true` | `true` | Enables UCPD (unified cookie/privacy decisions). |

### Onboarding / Auth / Security

61 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `2fa_temporary_password_enabled` | bool | `false` | `false` | Enables temporary-password handling in the two-factor authentication (2FA) flow. |
| `Arkose_rweb_hosted_page` | bool | `true` | `true` | Uses the hosted-page (iframe-less) variant of the Arkose Labs challenge on web. |
| `Arkose_use_invisible_challenge_key` | bool | `false` | `false` | Switches Arkose challenges to the invisible-challenge public key variant. |
| `account_country_setting_countries_whitelist` | list | `[ad, ae, af, ag, …]` (238 items) | `[ad, ae, af, ag, …]` (238 items) | Whitelist of ISO country codes selectable in the account country setting. |
| `arkose_challenge_login_web_devel` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the login challenge, development environment. |
| `arkose_challenge_login_web_prod` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the login challenge, production environment. |
| `arkose_challenge_onboard_prod` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the onboarding challenge, production environment. |
| `arkose_challenge_open_app_dev` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the open-app challenge, development environment. |
| `arkose_challenge_open_app_prod` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the open-app challenge, production environment. |
| `arkose_challenge_signup_mobile_dev` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the mobile signup challenge, development environment. |
| `arkose_challenge_signup_mobile_prod` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the mobile signup challenge, production environment. |
| `arkose_challenge_signup_web_dev` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the web signup challenge, development environment. |
| `arkose_challenge_signup_web_prod` | str | `[redacted]` | `[redacted]` | Arkose Labs site identifier for the web signup challenge, production environment. |
| `jetfuel_forgot_password_migration_enabled` | bool | `true` | `true` | Migrates the forgot-password flow to Jetfuel. |
| `oauth_consent_account_switch_enabled` | bool | `true` | `true` | Enables account switching in the OAuth consent screen. |
| `oauth_trusted_developer_badge_enabled` | bool | `true` | `true` | Shows a trusted-developer badge in OAuth consent. |
| `ocf_2fa_enrollment_bouncer_enabled` | bool | `true` | `true` | Enables the 2FA enrollment bouncer (prompting users to enroll). |
| `ocf_2fa_enrollment_enabled` | bool | `true` | `true` | Enables 2FA enrollment. |
| `ocf_2fa_unenrollment_enabled` | bool | `true` | `true` | Enables 2FA unenrollment. |
| `onboarding_project_uls_enabled` | bool | `true` | `true` | Enables the onboarding project ULS (unified login/signup) flow. |
| `responsive_web_castle_client_event_enabled` | bool | `false` | `false` | Enables Castle client events. |
| `responsive_web_castle_public_key` | str | `[redacted]` | `[redacted]` | Castle SDK public key; the actual value is redacted. |
| `responsive_web_castle_sdk_enabled` | bool | `true` | `true` | Enables the Castle SDK for fraud detection. |
| `responsive_web_disconnect_third_party_sso_enabled` | bool | `true` | `true` | Enables disconnecting third-party SSO. |
| `responsive_web_install_banner_show_immediate` | bool | `false` | `true` ⚠ | Shows the install banner immediately; on for this account. |
| `responsive_web_jetfuel_add_phone_enabled` | bool | `true` | `true` | Enables add-phone through Jetfuel. |
| `responsive_web_jetfuel_enable_sms_2fa_enabled` | bool | `true` | `true` | Enables SMS 2FA through Jetfuel. |
| `responsive_web_jetfuel_frame` | bool | `true` | `true` | Enables the Jetfuel frame. |
| `responsive_web_logged_out_ios_redesign_enabled` | bool | `false` | `true` ⚠ | Enables the logged-out iOS redesign; on for this account. |
| `responsive_web_logged_out_redesign_enabled` | bool | `false` | `false` | Enables the logged-out redesign. |
| `responsive_web_login_input_type_email_enabled` | bool | `false` | `false` | Uses email input type on the login form. |
| `responsive_web_login_signup_sheet_app_install_cta_enabled` | bool | `true` | `true` | Shows the app-install CTA in login/signup sheet. |
| `responsive_web_not_a_bot_signups_enabled` | bool | `false` | `false` | Enables the "not a bot" signup check. |
| `responsive_web_ocf_sms_autoverify_darkwrite` | bool | `false` | `false` | Enables dark-write for SMS autoverify. |
| `responsive_web_ocf_sms_autoverify_enabled` | bool | `false` | `false` | Enables SMS autoverify. |
| `responsive_web_open_in_app_prompt_enabled` | bool | `false` | `false` | Enables the open-in-app prompt. |
| `responsive_web_passwordless_sso_enabled` | bool | `false` | `false` | Enables passwordless SSO. |
| `responsive_web_placeholder_siwg_button_enabled` | bool | `false` | `false` | Shows a placeholder Sign in with Google button. |
| `responsive_web_send_jetfuel_preview_image_enabled` | bool | `true` | `true` | Sends Jetfuel preview image. |
| `responsive_web_signup_direct` | bool | `false` | `false` | Enables direct signup. |
| `responsive_web_sso_redirect_enabled` | bool | `true` | `true` | Enables SSO redirects. |
| `responsive_web_stripe_account_creation_enabled` | bool | `true` | `true` | Enables Stripe account creation. |
| `responsive_web_suppress_app_button_banner_suppressed` | bool | `false` | `false` | Controls suppression of the app-button banner. |
| `responsive_web_temporary_ocf_x_migration` | bool | `true` | `true` | Enables the temporary OCF X migration. |
| `responsive_web_use_app_button_variations` | str | `"control"` | `"control"` | Experiment bucket for the "use app" button ("control"). |
| `responsive_web_use_app_prompt_copy_variant` | str | `"prompt_better"` | `"prompt_better"` | Copy variant for the use-app prompt. |
| `responsive_web_use_app_prompt_enabled` | bool | `false` | `false` | Enables the use-app prompt. |
| `responsive_web_use_new_landing_page` | bool | `true` | `true` | Uses the new landing page. |
| `responsive_web_use_new_onboarding` | bool | `true` | `true` | Uses the new onboarding. |
| `responsive_web_user_spectral_key_enabled` | bool | `true` | `true` | Enables the user spectral key. |
| `rweb_client_transaction_id_enabled` | bool | `false` | `true` ⚠ | Sends a client transaction ID with requests; on for this account. |
| `rweb_session_binding_enabled` | bool | `false` | `false` | Enables session binding. |
| `rweb_update_fatigue_switch_to_app_day_timeout` | int | `7` | `7` | Days between "switch to app" update fatigue. |
| `rweb_update_fatigue_switch_to_app_link` | str | `"BannerSwitchToApp"` | `"BannerSwitchToApp"` | Link used for the switch-to-app banner. |
| `tv_app_casting_log_focused_element_every_10s` | bool | `false` | `false` | Logs the focused element every 10 s in the TV app. |
| `tv_app_qrcode_login_enabled` | bool | `true` | `true` | Enables QR-code login in the TV app. |
| `tv_app_samsung_continue_watching_enabled` | bool | `false` | `false` | Enables Samsung TV continue-watching. |
| `tv_app_samsung_exit_configuration` | str | `"EXIT"` | `"EXIT"` | Samsung TV exit configuration ("EXIT"). |
| `twitter_jetfuel_use_new_api_url` | bool | `true` | `true` | Uses the new Jetfuel API URL. |
| `x_jetfuel_enable_test_cluster` | bool | `false` | `false` | Uses the Jetfuel test cluster. |
| `x_jetfuel_use_new_api_url` | bool | `true` | `true` | Uses the new Jetfuel API URL. |

### Performance / Infra / Debug / Telemetry

35 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `network_layer_503_backoff_mode` | str | `"host"` | `"host"` | Back-off scope used by the network layer after HTTP 503 responses ("host"). |
| `responsive_web_api_transition_enabled` | bool | `true` | `true` | Enables the API transition in the web app. |
| `responsive_web_chat_enabled` | bool | `true` | `true` | Enables chat in the web app. |
| `responsive_web_extension_compatibility_hide` | bool | `false` | `true` ⚠ | Hides the extension compatibility UI; on for this account. |
| `responsive_web_extension_compatibility_impression_guard` | bool | `true` | `true` | Guards extension compatibility impressions. |
| `responsive_web_extension_compatibility_override_param` | bool | `false` | `true` ⚠ | Overrides extension compatibility via param; on for this account. |
| `responsive_web_extension_compatibility_scribe` | bool | `true` | `true` | Enables extension compatibility scribing. |
| `responsive_web_extension_compatibility_size_threshold` | int | `50` | `50` | Size threshold for extension compatibility detection. |
| `responsive_web_fetch_hashflags_on_boot` | bool | `false` | `true` ⚠ | Fetches hashflags on boot; on for this account. |
| `responsive_web_graphql_feedback` | bool | `true` | `true` | Enables GraphQL feedback. |
| `responsive_web_history_screen_enabled` | bool | `true` | `true` | Enables the history screen. |
| `responsive_web_intercom_support_capture_premium_enabled` | bool | `false` | `false` | Enables Intercom support capture for Premium. |
| `responsive_web_locale_context_direction_enabled` | bool | `true` | `true` | Enables locale-context text direction. |
| `responsive_web_native_bridge_allowed_methods` | list | `[toast, slideshow]` (2 items) | `[toast, slideshow]` (2 items) | Methods allowed through the native bridge (toast, slideshow). |
| `responsive_web_scribe_media_component` | bool | `true` | `true` | Enables scribing for media components. |
| `responsive_web_seasonal_custom_logo` | str | `"IconTwitter"` | `"IconTwitter"` | Name of the seasonal custom logo ("IconTwitter"). |
| `responsive_web_service_worker_update_toast_interval_hours` | int | `0` | `0` | Interval (hours) for the service worker update toast. |
| `responsive_web_share_only_tweet_url_omit_title_and_text` | bool | `true` | `true` | Shares only the post URL, omitting title and text. |
| `responsive_web_tracer_global_trace_sample_rate` | int | `1` | `1` | Global trace sample rate (1 = 100%). |
| `rweb_dash_menu_app_redirect_footer_enabled` | bool | `true` | `true` | Shows the app redirect footer in the dash menu. |
| `rweb_debugger_enabled` | bool | `false` | `false` | Enables the in-app debugger. |
| `rweb_recommendations_sidebar_graphql_enabled` | bool | `true` | `true` | Uses GraphQL for the recommendations sidebar. |
| `sc_mock_data_enabled` | bool | `false` | `false` | Enables mock data for Smart Cards/"sc". |
| `sc_r4_enabled` | bool | `false` | `false` | Purpose unclear from name; likely "sc" release 4 gate. |
| `scribe_api_error_sample_size` | int | `0` | `0` | Sample size for API error scribing. |
| `scribe_api_sample_size` | int | `100` | `100` | Sample size for API scribing. |
| `scribe_cdn_host_list` | list | `[si0.twimg.com, si1.twimg.com, si2.twimg.com, si3.twimg.com, …]` (25 items) | `[si0.twimg.com, si1.twimg.com, si2.twimg.com, si3.twimg.com, …]` (25 items) | List of CDN hosts for scribing. |
| `scribe_cdn_sample_size` | int | `50` | `50` | Sample size for CDN scribing. |
| `scribe_web_nav_sample_size` | int | `100` | `100` | Sample size for web navigation scribing. |
| `system_theme_toggle_enabled` | bool | `true` | `true` | Enables the system-theme toggle. |
| `traffic_rewrite_map` | list | `[]` (0 items) | `[]` (0 items) | Traffic rewrite map (empty list). |
| `view_counts_everywhere_api_enabled` | bool | `true` | `true` | Enables the view counts API everywhere. |
| `view_counts_public_visibility_enabled` | bool | `true` | `true` | Makes view counts public. |
| `x_android_apollo_graphql_accept_header` | str | `"application/json"` | `"application/json"` | Android Apollo GraphQL accept header. |
| `x_android_apollo_graphql_accept_header_override` | bool | `true` | `true` | Overrides the Android Apollo accept header. |

### Misc

14 flags.

| Flag | Type | Default | This account | Inferred description |
|---|---|---|---|---|
| `responsive_web_dockable_autoplay_policy_enabled` | bool | `true` | `true` | Enables a dockable autoplay policy. |
| `responsive_web_enhance_cards_enabled` | bool | `false` | `false` | Enables enhanced cards. |
| `responsive_web_lbm_v2_home_enabled` | bool | `false` | `false` | Enables LBM v2 on home. |
| `responsive_web_lbm_v2_replies_enabled` | bool | `false` | `false` | Enables LBM v2 on replies. |
| `responsive_web_mobile_app_spotlight_v1_config` | bool | `false` | `false` | Enables the mobile app spotlight v1 config. |
| `responsive_web_prerolls_fullscreen_disabled_on_ios` | bool | `false` | `false` | Disables fullscreen for prerolls on iOS. |
| `responsive_web_professional_journeys_holdback_enabled` | bool | `false` | `false` | Enables the professional journeys holdback. |
| `responsive_web_show_similar_posts_action_enabled` | bool | `false` | `false` | Shows a similar-posts action. |
| `responsive_web_ssr_send_likes_in_title_enabled` | bool | `true` | `true` | Sends likes in the SSR title. |
| `responsive_web_tweet_details_prefetch_enabled` | bool | `true` | `true` | Prefetches post details. |
| `settings_for_you_recommendation_enabled` | bool | `false` | `false` | Enables the For You recommendation setting. |
| `shortened_tracking_parameters_mapping` | list | `[01:twcamp^share/twsrc^android/twgr^sms, 02:twcamp^share/t…, …]` (71 items) | `[01:twcamp^share/twsrc^android/twgr^sms, 02:twcamp^share/t…, …]` (71 items) | Mapping of short codes to tracking parameters for share links. |
| `targeted_project_friday_enabled` | bool | `false` | `false` | Purpose unclear from name; likely a "project Friday" targeted experiment gate. |
| `vod_attribution_tweet_detail_pivot_enabled` | bool | `true` | `true` | Enables VOD attribution pivot. |

## Appendix A — Deviations default → this account

58 flags where the value resolved for this account differs from `defaultConfig`. This is the only visible trace of targeting/experiments/staged rollouts (percentages are not exposed). The "Also deviated on 2026-09-23" column tells whether the same deviation existed in the previous capture.

| Flag | Type | Default | This account | Category | Also deviated on 2026-09-23 |
|---|---|---|---|---|---|
| `active_ad_campaigns_query_enabled` | bool | `false` | `true` | Ads / Promote | yes |
| `ads_spacing_client_fallback_minimum_spacing` | int | `2` | `1` | Ads / Promote | no (new deviation) |
| `blue_business_vo_nav_for_legacy_verified` | bool | `false` | `true` | Verified Organizations / Business | yes |
| `co_timeline_reset_period_minutes` | int | `20` | `1440` | Timeline / Ranking / Home | yes |
| `co_timeline_topic_filter_enabled` | bool | `false` | `true` | Timeline / Ranking / Home | yes |
| `explore_relaunch_enable_auto_play` | bool | `false` | `true` | Search / Explore / Trends / Topics | yes |
| `grok_settings_memory_visibility` | str | `"hide"` | `"show"` | Grok / AI | yes |
| `insights_ai_trends_enabled` | bool | `false` | `true` | Creator / Monetization / Analytics | yes |
| `insights_paginated_metrics_backend_enabled` | bool | `false` | `true` | Creator / Monetization / Analytics | yes |
| `insights_previews_enabled` | bool | `false` | `true` | Creator / Monetization / Analytics | yes |
| `responsive_web_ad_revenue_sharing_onboarding_redirect_enabled` | bool | `false` | `true` | Ads / Promote | yes |
| `responsive_web_ad_revenue_sharing_setup_enabled` | bool | `false` | `true` | Ads / Promote | yes |
| `responsive_web_ad_revenue_sharing_subscriptions_dashboard_redirect_enabled` | bool | `false` | `true` | Subscriptions / Premium | yes |
| `responsive_web_extension_compatibility_hide` | bool | `false` | `true` | Performance / Infra / Debug / Telemetry | yes |
| `responsive_web_extension_compatibility_override_param` | bool | `false` | `true` | Performance / Infra / Debug / Telemetry | yes |
| `responsive_web_fetch_hashflags_on_boot` | bool | `false` | `true` | Performance / Infra / Debug / Telemetry | yes |
| `responsive_web_gpc_enabled` | bool | `false` | `true` | Compliance / Legal / Privacy / Cookies | yes |
| `responsive_web_grok_05231996` | str | `""` | `"imagine"` | Grok / AI | yes |
| `responsive_web_grok_analyze_post_followups_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_enable_grok_tab_education` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_imagine_composer_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_imagine_image_comparison_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_imagine_native_share_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_imagine_profile_edit_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_img_composer_in_media_picker` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_media_attribution_route_to_imagine_composer` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_tweet_actions_edit_image_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_tweet_media_detail_edit_image_button_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_tweet_media_edit_image_button_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_user_active_seconds_enable` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_voice_mode_enabled` | bool | `false` | `true` | Grok / AI | yes |
| `responsive_web_grok_xweb_replacement_enabled` | bool | `false` | `true` | Grok / AI | no (new deviation) |
| `responsive_web_install_banner_show_immediate` | bool | `false` | `true` | Onboarding / Auth / Security | yes |
| `responsive_web_logged_out_ios_redesign_enabled` | bool | `false` | `true` | Onboarding / Auth / Security | yes |
| `responsive_web_media_upload_target_jpg_pixels_per_byte` | int | `6` | `1` | Media / Video / Upload | yes |
| `responsive_web_nfl_sidebar_for_all_users_enabled` | bool | `false` | `true` | Spaces / Live / Sports | yes |
| `responsive_web_ocf_reportflow_suspension_appeals_enabled` | bool | `false` | `true` | Community Notes / Trust & Safety / Moderation | yes |
| `responsive_web_primary_nav_route_preload_enabled` | bool | `false` | `true` | Timeline / Ranking / Home | yes |
| `responsive_web_qp_boost_content_check_enabled` | bool | `true` | `false` | Ads / Promote | yes |
| `responsive_web_qp_boost_content_check_min_delay_seconds` | int | `11` | `0` | Ads / Promote | yes |
| `responsive_web_qp_new_boost_analytics_enabled` | bool | `false` | `true` | Ads / Promote | yes |
| `responsive_web_quick_promote_high_budget_tier_enabled` | bool | `false` | `true` | Ads / Promote | yes |
| `responsive_web_verified_organizations_invoice_update_enabled` | bool | `false` | `true` | Verified Organizations / Business | yes |
| `responsive_web_video_promoted_logging_enabled` | bool | `false` | `true` | Ads / Promote | yes |
| `rweb_client_transaction_id_enabled` | bool | `false` | `true` | Onboarding / Auth / Security | yes |
| `rweb_promoted_tweet_max_text_lines` | int | `0` | `2` | Ads / Promote | yes |
| `rweb_quick_promote_third_party_boost_enabled` | bool | `false` | `true` | Ads / Promote | yes |
| `spaces_live_chat_enabled` | bool | `false` | `true` | Spaces / Live / Sports | no (new deviation) |
| `subscriptions_feature_can_gift_premium` | bool | `false` | `true` | Subscriptions / Premium | yes |
| `subscriptions_offers_user_location_is_usa` | bool | `false` | `true` | Subscriptions / Premium | yes |
| `subscriptions_quick_free_trials_low_threshold_screen_enabled` | bool | `false` | `true` | Subscriptions / Premium | yes |
| `subscriptions_quick_free_trials_ui_enabled` | bool | `false` | `true` | Subscriptions / Premium | yes |
| `subscriptions_sign_up_enabled` | bool | `false` | `true` | Subscriptions / Premium | yes |
| `super_follow_android_web_subscription_enabled` | bool | `false` | `true` | Subscriptions / Premium | yes |
| `super_follow_web_application_enabled` | bool | `false` | `true` | Subscriptions / Premium | yes |
| `timeline_scroll_pointer_events_optimization` | bool | `false` | `true` | Timeline / Ranking / Home | yes |
| `xchat_enable_metadata_sync` | bool | `false` | `true` | XChat / DMs / Calls | yes |
| `xprofile_work_history_domain_enabled` | bool | `false` | `true` | Profile / Identity | yes |

## Appendix B — Diff since 2026-09-23

Baseline: 1384 default flags / 1385 user flags (2026-09-23). Current: 1424. Net: **+44 added, −4 removed**, 12 existing flags changed default and/or user value.

### B.1 Added flags (44)

| Flag | Type | Default | This account | Category | Inferred description |
|---|---|---|---|---|---|
| `android_ui_nested_quote_tweet_preview_enabled` | bool | `false` | `false` | Timeline / Ranking / Home | Android UI flag for the nested quote-post preview; listed in the web payload but Android-oriented. |
| `complat_x_migration_enabled` | bool | `false` | `false` | Compliance / Legal / Privacy / Cookies | Purpose unclear from name; likely a compliance-platform migration to the X stack (new in the 2026-10-01 capture). |
| `grok_translations_community_note_auto_translation_is_enabled` | bool | `false` | `false` | Grok / AI | Enables Grok-based auto-translation of Community Notes. |
| `grok_translations_community_note_translation_is_enabled` | bool | `false` | `false` | Grok / AI | Enables Grok-based translation of Community Notes. |
| `grok_translations_post_auto_translation_is_enabled` | bool | `false` | `false` | Grok / AI | Enables Grok-based auto-translation of posts. |
| `grok_xweb_connectors_enabled` | bool | `false` | `false` | Grok / AI | Enables Grok connectors on the web. |
| `grok_xweb_skills_enabled` | bool | `false` | `false` | Grok / AI | Enables Grok skills on the web. |
| `immersive_video_status_linkable_timestamps` | bool | `false` | `false` | Media / Video / Upload | Enables linkable timestamps in immersive video. |
| `payments_csv_export_enabled` | bool | `false` | `false` | Payments / X Money | Enables CSV export of payments. |
| `responsive_web_live_video_viewer_session_enabled` | bool | `true` | `true` | Spaces / Live / Sports | Enables live video viewer sessions. |
| `responsive_web_mlb_athlete_tray_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables the MLB athlete tray. |
| `responsive_web_mlb_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Master switch for MLB (baseball) features. |
| `responsive_web_mlb_favorite_teams_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB favorite teams. |
| `responsive_web_mlb_game_animations_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB game animations. |
| `responsive_web_mlb_game_chat_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB game chat. |
| `responsive_web_mlb_game_feed_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables the MLB game feed. |
| `responsive_web_mlb_game_odds_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB game odds. |
| `responsive_web_mlb_hub_home_tab_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB hub home tab. |
| `responsive_web_mlb_hub_media_tab_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB hub media tab. |
| `responsive_web_mlb_lineup_season_stats_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB lineup season stats. |
| `responsive_web_mlb_live_card_collapse_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables collapsing the MLB live card. |
| `responsive_web_mlb_logged_out_game_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB logged-out game view. |
| `responsive_web_mlb_pregame_matchup_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB pre-game matchup. |
| `responsive_web_mlb_profile_sports_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB sports on profile. |
| `responsive_web_mlb_reminder_snooze_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB reminder snooze. |
| `responsive_web_mlb_reminders_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB reminders. |
| `responsive_web_mlb_scorecard_odds_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables MLB scorecard odds. |
| `responsive_web_mlb_sidebar_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables the MLB sidebar. |
| `responsive_web_nfl_game_dock_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables the NFL game dock. |
| `responsive_web_qp_budgets_by_billing_currency_enabled` | bool | `false` | `false` | Ads / Promote | Enables budgets by billing currency in Quick Promote. |
| `responsive_web_sports_profile_endpoint_enabled` | bool | `true` | `true` | Spaces / Live / Sports | Enables the sports profile endpoint. |
| `responsive_web_sports_sidebar_league_logos_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Shows league logos in the sports sidebar. |
| `responsive_web_verified_organizations_application_requirements_enabled` | bool | `false` | `false` | Verified Organizations / Business | Enables application requirements for Verified Organizations. |
| `responsive_web_verified_organizations_application_two_column_enabled` | bool | `false` | `false` | Verified Organizations / Business | Enables two-column application for Verified Organizations. |
| `rweb_analytics_realtime_active_followers_enabled` | bool | `true` | `true` | Creator / Monetization / Analytics | Enables real-time active followers. |
| `rweb_under_the_hood_report_jetfuel_enabled` | bool | `true` | `true` | Community Notes / Trust & Safety / Moderation | Enables the Jetfuel version of that report. |
| `rweb_xchat_call_health_enabled` | bool | `true` | `true` | XChat / DMs / Calls | Enables XChat call health. |
| `rweb_xchat_client_stats_enabled` | bool | `true` | `true` | XChat / DMs / Calls | Enables XChat client stats. |
| `rweb_xchat_module_federation_enabled` | bool | `true` | `true` | XChat / DMs / Calls | Enables module federation for XChat. |
| `unified_cards_destination_url_params_enabled` | bool | `false` | `false` | Ads / Promote | Enables destination URL params in unified cards. |
| `x_lite_quick_promote_analytics_banner_enabled` | bool | `false` | `false` | Verified Organizations / Business | Shows the analytics banner in X Lite Quick Promote. |
| `x_sports_post_context_enabled` | bool | `false` | `false` | Spaces / Live / Sports | Enables sports post context. |
| `xcall_item_in_list_enabled` | bool | `false` | `false` | XChat / DMs / Calls | Enables items in list for X calls. |
| `xcall_link_devices_enabled` | bool | `false` | `false` | XChat / DMs / Calls | Enables linking devices for X calls. |

### B.2 Removed flags (4)

Present on 2026-09-23, absent now (so they are not listed in section 2). Last known values:

| Flag | Last default | Last user value |
|---|---|---|
| `rweb_video_host_enabled` | `false` | `false` |
| `x_jetfuel_event_screen_migration_enabled` | `false` | `false` |
| `x_jetfuel_event_screen_migration_skip_ids` | `[2000461415727931396]` (1 items) | `[2000461415727931396]` (1 items) |
| `xchat_passcode_options_enabled` | `false` | `false` |

### B.3 Existing flags whose default or user value changed (12)

| Flag | Default (09-23 → 10-01) | This account (09-23 → 10-01) |
|---|---|---|
| `ads_spacing_client_fallback_minimum_spacing` | `3` → `2` | `3` → `1` |
| `branded_features_search_overlay_animations_enabled` | `false` → `true` | unchanged `true` |
| `payments_agent_connections_enabled` | `false` → `true` | unchanged `true` |
| `payments_agent_connections_prefill_enabled` | `true` → `false` | unchanged `false` |
| `responsive_web_grok_xweb_replacement_enabled` | unchanged `false` | `false` → `true` |
| `responsive_web_nested_quote_preview_enabled` | `false` → `true` | `false` → `true` |
| `rweb_sports_post_context_footer_enabled` | `false` → `true` | unchanged `true` |
| `rweb_sports_post_context_header_enabled` | `true` → `false` | unchanged `false` |
| `spaces_live_chat_enabled` | unchanged `false` | `false` → `true` |
| `x_sports_nfl_game_chat_team_pick_enabled` | `false` → `true` | unchanged `true` |
| `xchat_enable_numbers_premium` | `false` → `true` | `false` → `true` |
| `xchat_settings_redesign_enabled` | `false` → `true` | `false` → `true` |

Notable themes of the diff (inferred): a new wave of MLB (baseball) hub flags and NFL game-dock/sports-profile flags; Grok on X web connectors/skills and Grok-powered translations; XChat call-health/client-stats/module-federation; Verified Organizations application flow; X Money CSV export; realtime analytics for active followers.

## Appendix C — Verification

- Flags in JSON: **1424**; table rows in section 2: **1424**; distinct flag names in section 2: **1424**.
- Flags appearing not exactly once in section 2: **0**; unknown names in tables: **0**.
- Result: **PASS — every flag appears exactly once**.
- Category sizes: Grok / AI 160, XChat / DMs / Calls 188, Payments / X Money 37, Verified Organizations / Business 91, Subscriptions / Premium 207, Ads / Promote 66, Creator / Monetization / Analytics 99, Communities 53, Spaces / Live / Sports 91, Media / Video / Upload 78, Search / Explore / Trends / Topics 28, Timeline / Ranking / Home 63, Community Notes / Trust & Safety / Moderation 106, Notifications 4, Profile / Identity 21, Compliance / Legal / Privacy / Cookies 22, Onboarding / Auth / Security 61, Performance / Infra / Debug / Telemetry 35, Misc 14.
