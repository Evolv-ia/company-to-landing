# Provider selection

Research snapshot: 2026-09-16. Prices are USD, subject to plan changes and taxes. Refresh official pricing before committing to spend. This comparison is a suitability assessment from documentation, not a measured speed/quality benchmark.

## Recommended routing

For minimum additional cash cost, use the existing coding agent, browser/local extraction, original company media and static hosting. This still uses compute, agent quota and maintenance time. For convenient managed extraction, Firecrawl is the preferred option among the reviewed services because it combines crawl, content, image discovery and branding. Use Apify for a specific supported source that requires a suitable Actor, not automatically for every company.

The skill does not require a second AI website-builder subscription. Reconsider a hosted builder when collaborative visual editing is more important than local code control. The existing agent handles synthesis and implementation; unattended API automation would need separate model/API cost estimates.

| Component | Verified entry cost / model | Decision |
|---|---|---|
| [Crawl4AI](https://github.com/unclecode/crawl4ai) | Open-source local option; infrastructure and maintenance remain | Lowest scraping subscription cost, more setup |
| [Firecrawl](https://www.firecrawl.dev/pricing) | Free: 1,000 credits/month. Hobby: $19/month or $16/month billed annually, 5,000 credits | Preferred managed extraction; start free |
| [Apify](https://apify.com/pricing) | Free includes $5/month usage; Starter $19/month plus usage beyond allowance | Specialized Actors; compute, proxy and Actor pricing vary |
| [Lovable](https://lovable.dev/pricing) | Free build grant: 5 daily credits, maximum 30/month; paid price not exposed in the retrieved page | Builder alternative, not required; verify checkout for paid cost |
| [Cloudflare Pages](https://developers.cloudflare.com/pages/platform/limits/) | Free plan available; 500 builds/month; 25 MiB per asset | Good static deployment target; functions/storage/video may add cost |
| Instagram data export | Free; prepared asynchronously by Meta | Preferred Instagram route for the company's own account: original quality, clearest rights |
| [Instagram Platform API](https://developers.facebook.com/docs/instagram-platform) | No per-call fee; needs a professional account, a Meta app and a token the user configures | Use when a token already exists; rate limits apply |
| [Apify Instagram actors](https://apify.com/apify/instagram-scraper) | Usage- or result-based pricing that changes; not verified in this snapshot | Public profiles only, after the user approves an estimate; platform-terms risk is the user's decision |

Instagram routes, identity checks and rights handling are in [instagram.md](instagram.md). Brand and design work uses installed skills rather than paid services; see [skill-chain.md](skill-chain.md). Mockup generation with `design-shotgun` uses an image-generation API and is opt-in.

Interactive JavaScript does not by itself require paid server hosting. Hosting plans, form delivery, domain registration and video streaming are distinct costs. Use stable provider embeds or suitable media storage for large videos.

## Example estimate, not a quote

Assume 20 company pages at one basic scrape credit each: 20 credits, excluding discovery, retries, advanced formats and video. At full utilization of a $19/5,000-credit plan this represents $0.076 of allocation per company. The actual subscription bill is $19 even if only one company is processed; free allowance may cover small usage. Add current format modifiers and all additional requests before estimating capacity. Report agent/model and media generation costs separately.

## Existing skills reviewed

- [Firecrawl website design clone](https://github.com/firecrawl/firecrawl-workflows/blob/main/skills/firecrawl-website-design-clone/SKILL.md): directly relevant upstream workflow for evidence-based brand/design extraction. Official repository, 162 stars at inspection; install count not verified. Use as an optional complement, not a mandatory dependency. Its focus is DESIGN.md, not the entire landing pipeline.
- [Anthropic frontend-design](https://github.com/anthropics/skills/tree/main/skills/frontend-design): distinctive frontend execution. [Directory listing](https://www.skills.sh/anthropics/skills/frontend-design) showed 892.7K installs and 176.5K repository stars at inspection. Optional; existing local design skills may already cover this need.
- [Vercel agent-skills](https://github.com/vercel-labs/agent-skills): frontend guidelines and React practices. Official repository showed 31.2K stars. [Web design guidelines](https://www.skills.sh/vercel-labs/agent-skills/web-design-guidelines) supports review; an individual install count was not verified.
- [Firecrawl CLI](https://github.com/firecrawl/cli): operational scraping skill; distinguish live extraction from the separate application-integration skills at [firecrawl/skills](https://github.com/firecrawl/skills).
- [designmd-extractor](https://github.com/zishh/designmd-extractor): related community alternative; adoption/maintenance not sufficiently verified for default selection.

These files are original orchestration instructions, not vendored copies of the repositories above. Review current source and license before installing or copying upstream code. Popularity is a discovery signal, not proof of safety or quality. No third-party skill installation is necessary to run the local route.
