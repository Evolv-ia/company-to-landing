# Instagram media

Instagram is often where a small company keeps its best real photography, its reels and its everyday voice, while the website is thin or outdated. This step turns a handle into curated, rights-aware media and brand signals. Research snapshot: 2026-09-16; platform APIs, export layouts and prices change, so check current documentation before relying on a detail.

## Contents

1. Handle and identity
2. Choosing a route
3. Route details
4. What to collect
5. Brand signals
6. Rights and privacy
7. Processing for the web
8. Using Instagram media on the landing
9. Failures and coverage

## 1. Handle and identity

Normalize the input: strip `@`, the `instagram.com/` prefix, query strings and trailing slashes, then lowercase. Valid handles contain only letters, digits, `.` and `_`, at most 30 characters. Store the normalized handle and the original input.

Verify ownership before using anything:

- strong: the official website links to the profile, or the profile's bio link points to the company's verified domain;
- supporting: display name, category, city and offering match `company.json`;
- insufficient on its own: a similar name, a search result, or a location tag.

If only supporting evidence exists, ask the user to confirm in the intake message. If the evidence contradicts the company (different city, sector or domain), do not use the account and say why. Accounts of competitors or inspiration brands are reference-only: study them for design principles, never reuse their media.

## 2. Choosing a route

Prefer the cheapest route that yields full-resolution files with clear rights. Several routes can combine — for example browser inspection for the moodboard while waiting for the user's export.

| Route | Needs | Gives | Use when |
|---|---|---|---|
| A. Data export or media folder | The user downloads their data or shares a folder | Original-quality photos and videos; captions and dates with an export | Default recommendation for the company's own account; free |
| B. Instagram API, own account | Professional (Business/Creator) account and an existing access token | Media URLs, captions, types, timestamps, permalinks, carousel children | A token is already configured |
| C. Apify Instagram actor | `APIFY_TOKEN` and a budget the user approved | Public posts, captions, media URLs, video URLs | Public profile, no export soon, user accepts cost and platform-terms risk |
| D. Browser inspection | An available browser | Visual reference only: grid look, recurring subjects, bio | Always possible for public profiles; never a download route |

Do not create Meta developer apps, accounts or tokens for the user, and do not type their credentials. If route B or C needs setup, explain the steps and let the user do them. Scraping Instagram, even public data, can conflict with Meta's terms; route C is the user's informed decision, not a default.

When no reusable route is available right away, continue building with website media and the browser moodboard, and tell the user that an export can be dropped in later to swap in better photos.

## 3. Route details

### A. Data export or media folder

Guide the user briefly: Instagram → Accounts Center → Your information and permissions → Download your information → select the account → choose only content (posts, reels; stories only if wanted) → format JSON, media quality high, a date range covering the last one to two years. Meta prepares the file asynchronously; it can take from minutes to a couple of days.

Inspect the export's structure before parsing — it changes over time. Recent exports keep media under `media/` (for example `media/posts/YYYYMM/`) and post metadata in a JSON file under the content activity folder (for example `your_instagram_activity/content/posts_1.json`). Map each media file to its post: caption (`title`), `creation_timestamp`, and carousel grouping.

Meta exports often store non-ASCII text as mojibake (UTF-8 bytes escaped as Latin-1, e.g. `Ã¨` for `è`). Repair caption strings with `text.encode("latin-1").decode("utf-8")` when that round-trip succeeds, and keep the raw value if it fails.

A plain media folder has no captions or dates: inventory the files, read dimensions and duration, and let the user's description stand in for context.

### B. Instagram API for the company's own account

The legacy Basic Display API is retired; use the current Instagram Platform (Instagram API with Instagram Login, or with Facebook Login). Read the token from an environment variable such as `INSTAGRAM_ACCESS_TOKEN`. With Instagram Login the media listing is:

```
GET https://graph.instagram.com/<current-version>/me/media
    ?fields=id,caption,media_type,media_product_type,media_url,thumbnail_url,permalink,timestamp,children{id,media_type,media_url,thumbnail_url}
    &limit=50
```

Follow `paging.next` until the ceiling. `media_type` is `IMAGE`, `VIDEO` or `CAROUSEL_ALBUM`; `media_product_type` distinguishes `FEED` and `REELS`. `media_url` points to a CDN link that expires, so download promptly instead of storing it as a durable asset. The `paging.next` URL contains the access token: strip `access_token` before saving any URL in evidence or logs.

Business Discovery (Facebook Login route) can read public metadata and media of another professional account through your own connected account. Treat what it returns as reference-only unless the other account belongs to the client and the client authorizes reuse.

Official documentation: [Instagram Platform](https://developers.facebook.com/docs/instagram-platform).

### C. Apify

Use an official Apify Instagram actor (for example `apify/instagram-scraper` or `apify/instagram-profile-scraper`) through the available connector, CLI or API. Before running: read the actor's current input schema and pricing, estimate the cost for the ceiling, and get the user's approval for that amount. Scrape only the public profile and its posts; never supply the user's Instagram session cookies or credentials.

Normalize the dataset: post URL/shortcode, type, caption, timestamp, `displayUrl`, `videoUrl`, carousel children, dimensions when present. These CDN URLs also expire — download selections promptly. Count actual runs and results against the budget in `QA.md`.

### D. Browser inspection

Open the public profile in the available browser and look at the grid, bio, highlights and a few representative posts. Save screenshots to the research directory as `reference-only` evidence for the moodboard and brand analysis. If Instagram shows a login wall, stop there: do not log in for the user, dismiss walls with scripts, or use another person's session. If the user is already signed in in their own browser, viewing is fine, but still do not bulk-download.

## 4. What to collect

Profile: normalized handle, display name, category, bio, bio link, profile picture (a logo candidate, but usually too small to replace a vector logo from the website), highlight titles, capture date. Save follower counts only as dated context, never as landing proof by default.

Posts: start with the most recent 60 posts or 12 months, whichever comes first. Extend when the user's scope needs it (a portfolio business may need older projects); reduce for a tight budget. For each item record id/shortcode, permalink, `media_type`, product type (feed/reel), timestamp, caption, carousel position, width, height, duration for video, thumbnail, route used and retrieval status.

Do not collect comments, likes lists, follower lists, direct messages or other people's personal data. Comments are not testimonials: a landing testimonial needs the customer's consent, which a scraped comment does not give.

## 5. Brand signals

Write findings to the research directory with post ids as evidence, then feed them to the brand skills (see [skill-chain.md](skill-chain.md)):

- imagery style: light, color grading, framing, backgrounds, people versus product, studio versus real-life, recurring props;
- grid palette: dominant colors across 12-24 recent posts, computed from downloaded images when possible; a palette read from a screenshot is low confidence;
- caption voice: formality, person (tu/voi/noi), emoji use, sentence length, language mix, recurring phrases and hashtags;
- content pillars: what the company shows repeatedly (products, process, team, projects, events, clients' spaces);
- offer evidence: products, prices, opening hours or locations mentioned in captions — dated, lower authority than the website, and checked against it;
- performance hints: when engagement data is available, relative engagement can hint at which subjects resonate. Use it to choose imagery, not as a published claim.

When Instagram and the website disagree on identity (colors, logo, tone), the website sets tokens and logo; Instagram informs photography and voice. Record the divergence in `BRAND.md`.

## 6. Rights and privacy

Set `rights_status` per item; the company's own account does not make every post reusable.

- Original posts by the company: `user-authorized` when the user asked for their own Instagram to be used.
- Reposts, "via @", "📸 @", photographer or agency credits, collaboration posts and UGC: `unknown` until the user confirms rights; prefer other media, or credit when the user confirms.
- Identifiable people (customers, staff, children): flag in `notes`. Prefer images without identifiable customers for hero use, and never use images of minors without explicit user confirmation.
- Reel audio: music added in Instagram is licensed for Instagram, not for a website. Strip the audio track unless it is original sound the company owns.
- Location data: strip EXIF/GPS metadata from published files.
- Other accounts: `reference-only`.

## 7. Processing for the web

Keep originals in `work/research/instagram/raw/`, outside the served project. For selected items, create optimized copies in the site's media folder with stable names such as `ig-<shortcode>-<index>.avif`, keeping a WebP or JPEG fallback when the stack needs it. Validate MIME type and dimensions after each download.

Instagram formats are mostly 1:1, 4:5 and 9:16 (reels). Record a focal point per selected image and crop deliberately: 4:5 suits galleries and split layouts, 9:16 suits mobile heroes, vertical carousels or phone frames, and a 16:9 hero crop from a portrait photo only works when the subject survives it. Check each crop visually.

For video: transcode to H.264 MP4 (plus WebM when useful), remove audio per section 6, cap size and duration for background use, extract a poster frame, and use `muted playsinline` with a pause control for any autoplaying loop; honor reduced motion.

Write alt text from what the image actually shows after inspecting it. Captions and hashtags are not alt text.

## 8. Using Instagram media on the landing

- Hero and section imagery drawn from the strongest genuine photos in the chosen direction's imagery plan.
- A curated, static "dal nostro Instagram" gallery or grid, each item linking to its permalink, with a follow link using the verified handle.
- Real process, team or project content where it supports the offer.
- No live feed widget unless the user asks for one: it needs a token that expires, adds third-party requests and can break silently. If requested, document token refresh and a static fallback.
- Official Instagram embeds load Meta scripts and cookies. Under GDPR, show a static preview and load the embed only after the visitor consents.

## 9. Failures and coverage

- Private account: only route A (or an authorized API token) works; say so.
- Login wall, HTTP 429 or blocks: stop that route after two retries with backoff; do not rotate identities or proxies to evade limits.
- Expired media URLs: refresh through the same route, or mark `failed`.
- Handle not found or renamed: check the website link again, then ask.

Add an Instagram block to the coverage summary: handle, identity evidence, routes attempted and their result, posts discovered, media downloaded, selected, reference-only, failed, and items held back for rights, with reasons. Keep the unprocessed queue so a later export or budget can continue the run.
