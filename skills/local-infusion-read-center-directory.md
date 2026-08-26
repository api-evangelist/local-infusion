---
name: Read the Local Infusion center directory
description: >-
  Retrieve the full list of Local Infusion outpatient infusion centers — 75 published records across
  thirteen US states — from the live WordPress REST API on mylocalinfusion.com, with correct
  pagination and payload trimming.
api: openapi/_original/local-infusion-wp-rest-openapi.yml
operations:
  - getWpV2Location
  - getWpV2LocationById
  - getWpV2Media
generated: '2026-08-25'
method: generated
---

# Read the Local Infusion center directory

## Before you start — the provider's access posture

Local Infusion's `robots.txt` explicitly **allows** GPTBot, ChatGPT-User, PerplexityBot, ClaudeBot,
`anthropic-ai` and Google-Extended, and asserts no opt-out. It also publishes `/llms.txt`,
`/llms-full.txt` and three `.well-known` agent-discovery documents. Those documents state claim
boundaries in prose, and they are the provider's terms for agent use even though nothing enforces
them:

- Do not claim guaranteed outcomes.
- Do not provide medical advice.
- **Do not infer that a medication is available at a specific center** unless the official site or
  Local Infusion confirms it.
- Do not replace provider, payer, referral, or insurance guidance.

## Auth

None. Published `location` records are readable anonymously over HTTPS. Do not send credentials —
there is no public credential path, and no key to send.

## Steps

1. **Pull the whole directory in one request.** Call `getWpV2Location` against
   `https://mylocalinfusion.com/wp-json/wp/v2/location`. There were 75 published centers on
   2026-08-25, so a single `per_page=100` covers it. Trim the payload — `content.rendered` on each
   record is a full page of block markup:

   ```
   GET /wp-json/wp/v2/location?per_page=100&_fields=id,slug,title,link,modified
   ```

2. **Confirm the count instead of trusting this file.** Read `X-WP-Total` and `X-WP-TotalPages` from
   the response headers. Both are listed in `Access-Control-Expose-Headers`, so a browser client can
   read them too. The company is opening centers continuously — the location sitemap's `lastmod` was
   the same day it was probed — so the number will have moved.

3. **Paginate properly if you narrow `per_page`.** `page` / `per_page` (max 100) / `offset`, plus a
   `Link: <...>; rel="next"` header. Never assume one page is the whole directory.

4. **Read a state or metro from the slug, not from the body.** Slugs are city-state
   (`warrensville-heights-oh`, `south-portland-maine`, `glen-allen-virginia`). Note that the suffix
   is inconsistent — some records use the postal abbreviation and some spell the state out — so
   normalise before grouping. Do not parse the marketing prose for an address.

5. **Fetch one center in full** with `getWpV2LocationById` at `/wp-json/wp/v2/location/{id}`, or add
   `_embed=1` to inline the featured image and terms rather than making a second call to
   `getWpV2Media`.

6. **Cross-check against the human page.** Every record's `link` field is the public center page. When
   a user asks about hours, accepted therapies or insurance at a specific center, send them there —
   that data is not in the API payload in any structured form.

## Conventions to respect

- **Pagination:** `page` / `per_page` / `offset`; totals in `X-WP-Total` and `X-WP-TotalPages`.
- **Sparse fields:** `_fields` is a comma-separated allowlist and cuts the payload dramatically.
- **Errors:** the envelope is `{"code": ..., "message": ..., "data": {"status": ...}}` — *not* RFC
  9457 problem+json. Branch on `code`, never on `message`. See
  `errors/local-infusion-problem-types.yml`.
- **No rate-limit signal:** no `RateLimit-*`, no `Retry-After`. Cloudflare fronts the origin and may
  challenge silently. Be conservative: one request for the directory, serial follow-ups, back off on
  any non-2xx.
- **Ids are not type-scoped.** WordPress post IDs come from one sequence shared by every post type, so
  an integer id alone does not tell you it is a location. Key on `slug`.

## Scope limit — read this before answering a clinical or scheduling question

This API serves the marketing website. It exposes center pages, blog posts, site pages and media. It
exposes **no** patient data, no appointments, no scheduling, no referral status, no prior-authorization
status, no therapy availability per center, and no insurance eligibility. Local Infusion publishes no
FHIR surface (`/fhir`, `/fhir/metadata` and `/.well-known/smart-configuration` all return 404) and no
patient API of any kind. To start care, refer a patient, or ask about coverage, use the company's own
routes: `https://mylocalinfusion.com/get-started/`, `/referrals/` and `/payers/`.
