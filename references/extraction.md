# Content, brand and media extraction

## Economy route

Use the host's supported browser and extraction tools. For repeatable local crawling, Crawl4AI or Playwright are options if installed or installable; follow the host's browser rules. Fetch public HTML for metadata, JSON-LD and links, then inspect rendered pages when content depends on JavaScript. Record final redirected URLs. Save evidence outside the public application directory.

Inspect screenshots and visible rendered styles for logos, font families, colors, spacing, buttons and motion. Inspect CSS custom properties and permitted stylesheets when useful. Downloaded HTML alone cannot reliably reproduce computed styles or lazy-loaded content.

Discover URLs through navigation, sitemap and relevant internal links. Stay on the company's approved domains except for linked media/CDNs or official profiles. Avoid unbounded calendars, faceted search, query permutations and duplicate language versions. Crawl politely, respect applicable access restrictions, and stop a provider route after repeated failures rather than looping.

## Firecrawl route

Use the available connector, CLI or SDK; inspect its current schema/help before executing. Do not assume a tool is installed just because a skill mentions it. Keep `FIRECRAWL_API_KEY` in environment/configuration secrets, never in the page or saved evidence.

Map/discover, then scrape the selected pages. On representative branded pages request `markdown`, `links`, `images` and `branding`; obtain a screenshot for visual confirmation. Collect `html`/`rawHtml` only where additional media or CSS evidence is needed. The images list and branding assets serve different purposes: logo/OG metadata is not a complete content-image inventory.

Prefer ordinary content plus agent-side synthesis over paid structured extraction on every page. Cache results by URL and capture time. Check current credit modifiers before choosing screenshots, structured formats, interaction or video. Count actual calls, including retries, against the run budget. Stop before an unapproved overage and continue from saved results.

Official references: [scrape formats](https://docs.firecrawl.dev/features/scrape), [billing](https://docs.firecrawl.dev/billing), [CLI source](https://github.com/firecrawl/cli). A documented endpoint is not a guarantee that every site is supported.

## Images

Inventory `img` sources, `currentSrc`, `srcset`, `picture/source`, lazy attributes, visible CSS background URLs, inline SVG, favicons, OG images and image links. Resolve relative URLs, preserve originals and record responsive variants. Scroll incrementally when needed to expose lazy content and revisit galleries where relevant. Do not strip functional CDN query strings when deduplicating.

For candidates record page URL, media URL, role, dimensions if known, MIME if verified, alt text, rights status and retrieval status. Review the actual selected images rather than choosing from filenames alone. Prioritize genuine product, team and project photography. Download reusable selections within reasonable byte limits, validate type/status and use stable local filenames. Treat external SVG as untrusted; sanitize before inline rendering or use it as an image resource.

## Videos

Inspect video/source elements, posters, linked video files, permitted iframe embeds and VideoObject JSON-LD. Distinguish direct MP4/WebM, provider embeds, streaming manifests and ephemeral blob/signed URLs. A discovered video URL is not a downloaded video, and a poster is not evidence that playback works.

Prefer official stable embeds for hosted video. Download direct files only when permitted and useful; impose a size limit, stream the transfer and record failures. Do not publish expiring signed URLs or `blob:` URLs as durable assets. Do not bypass DRM or reconstruct protected streams. Record unsupported formats as embed-only or unavailable.

Firecrawl documents a `video` format for supported sites with additional credits; verify support, returned structure and current pricing before using it. Use transcripts/captions if available and relevant to the company brief; otherwise describe only content actually inspected. Do not equate video retrieval with transcription.

## Reuse and coverage

Finding an asset does not establish permission to reuse it. For a user's own company use assets within the authorized scope; for reference/competitor sites extract design principles and use original or licensed visuals. Track rights as user-authorized, licensed, unknown or reference-only. Generate substitute media only when needed and authorized, following the available media tool's workflow and reporting extra costs. Do not generate fake product evidence or testimonials.

Instagram media follow their own routes, rights rules and processing steps in [instagram.md](instagram.md); record them in the same manifest with `origin: "instagram"`.

Produce a coverage summary: discovered URLs, visited URLs, failed URLs, deferred URLs, media discovered, selected, downloaded, embedded and unavailable. State why something is missing. Preserve the unprocessed queue for continuation. Aim for comprehensive useful evidence within the declared budget, never a guarantee of every asset on the internet.
