# Output contracts

Put intermediate evidence in `work/research/` or the repository's equivalent; put the final website in its own project. Keep research outside the served document root. These are data contracts, not literal placeholder files to ship.

## company.json

Include company name, supplied description, canonical website if verified, locale, audience, offerings, differentiation, verified proof, contact/booking links, desired conversion and unknowns. Represent substantive claims as objects with `value`, `status` (`observed`, `user-provided`, `inferred`, `unknown`), `source_urls`, `captured_at`, and `confidence` (`high`, `medium`, `low`). Use null/empty lists for unknown values rather than invented content. Keep creative proposals in a separate field.

## sources.json

For each page: requested URL, final URL, capture time, extraction method, status, relevant evidence path, failures and topics covered. Include discovered-but-deferred URLs and the stop reason. Avoid storing secrets or unrelated personal data.

## media-manifest.json

Each item has `id`, `kind` (`image`, `video`, `embed`, `logo`, `font`), `origin` (`website`, `instagram`, `user-folder`, `generated`), `source_page`, `source_url`, `local_path`, `mime_type`, `width`, `height`, `bytes`, `role`, `alt_or_caption`, `rights_status`, `retrieval_status`, `selected`, `notes`. Unknown numeric/string values are null. Retrieval states include `discovered`, `downloaded`, `embed-only`, `blocked`, `failed`, `reference-only`. Rights states are `user-authorized`, `licensed`, `unknown`, `reference-only`. Include signed-link expiry when known. `local_path` is set only after a successful validated download.

Instagram items also carry an `instagram` object: `handle`, `shortcode`, `permalink`, `media_type` (`IMAGE`, `VIDEO`, `CAROUSEL_ALBUM`), `product_type` (`FEED`, `REELS`), `carousel_index`, `posted_at`, `caption`, `duration_s`, `route` (`export`, `folder`, `api`, `apify`, `browser`), `credit` (a credited creator or reposted account, else null), `people_flag`, `audio_removed`, `focal_point`. Never store access tokens or token-bearing URLs.

## instagram.json

Profile snapshot and run record: normalized handle and original input, identity evidence and verdict, display name, category, bio, bio link, capture date, routes attempted with outcome and cost, ceiling used, brand signals (imagery style, grid palette with confidence, caption voice, content pillars, each citing post ids) and the coverage block described in [instagram.md](instagram.md). Record "no Instagram" explicitly when the user declined.

## BRAND.md and tokens

Include observed/proposed identity, source references, positioning, voice, claim boundaries, palette roles, typography, spacing/layout, components, imagery, logo usage and motion. Mark inferred tokens and explain meaningful accessibility deviations. Note where Instagram and website identity diverge and which one each decision follows. Record the chosen creative direction and why. Implement the approved/proposed system in a central CSS token file consumed by the site.

## creative-directions.md

The 2-3 directions presented at the creative checkpoint, in the structure given in SKILL.md step 3, with the recommended one first. Append the user's choice or the autonomous decision, with date and rationale, and any requested changes.

## Bridge files

`.agents/brand-context.md`, `PRODUCT.md` and `DESIGN.md` in the site project root, outside the served directory, in the formats described in [skill-chain.md](skill-chain.md). They are derived views of `company.json`, `BRAND.md` and the chosen direction; when they disagree, fix the source artifact and regenerate them.

## QA.md

Record build command/result, browser and tested viewports, screenshots where supported, interaction results, broken links/assets, accessibility checks performed, design review findings and fixes, skills used per phase and any fallbacks, unresolved issues and tests not run. Include crawl and Instagram coverage and cost accounting: provider, request/credit/result counts where available, estimated versus billed costs, applicable limits. A successful build is not proof of a working form or acceptable mobile layout.

## Website delivery

Provide project sources, dependency lockfile, selected licensed/authorized media, editable content, environment variable names without values, run/build instructions and a preview URL when available. Add deployment instructions for the chosen host. Only include a public URL after deployment actually succeeds. If a backend or media provider remains unconfigured, make that limitation visible in handoff and in any affected demo controls.
