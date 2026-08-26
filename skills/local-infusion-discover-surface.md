---
name: Discover the Local Infusion API and MCP surface
description: >-
  Enumerate the WordPress REST route-discovery document, the site content inventory, and the two
  authenticated Model Context Protocol servers, and establish exactly what is anonymous versus gated.
api: openapi/_original/local-infusion-wp-rest-openapi.yml
operations:
  - get
  - getWpV2Types
  - getWpV2Taxonomies
  - getWpV2Pages
  - getMcp
  - postMcpMcpOauthServer
  - getWpAbilitiesV1Abilities
generated: '2026-08-25'
method: generated
---

# Discover the Local Infusion API and MCP surface

## What this surface actually is

Local Infusion is an outpatient infusion-therapy provider. It runs no developer programme and ships no
product API. Everything below is the WordPress install behind `mylocalinfusion.com` — a corporate CMS
that happens to be self-describing, plus an MCP adapter someone switched on. Treat it as such: it is
a good source for **where the centers are** and **what the company has published**, and no source at
all for anything clinical.

## Auth

Anonymous for discovery and for published content. `wp-abilities/v1` and both `mcp` servers are gated.

## Steps

1. **Read the route-discovery document.** `get` at `https://mylocalinfusion.com/wp-json/`. It returns
   the site name, description, and every registered route — 282 of them across 15 namespaces on
   2026-08-25. Only five namespaces are WordPress core (`wp/v2`, `wp-abilities/v1`, `mcp`,
   `oembed/1.0`, and the unnamespaced root); the other ten are plugin internals (Yoast, Wordfence,
   Redirection, WP Rocket, Block Visibility, Object Cache, Genesis, Duplicate Post, Site Health, Block
   Editor). The derived contract in this repo deliberately excludes those.

2. **Enumerate the content model.** `getWpV2Types` at `/wp-json/wp/v2/types` lists every post type
   with its `rest_base`. The one that matters is `location` — a custom post type carrying the center
   directory. `getWpV2Taxonomies` at `/wp-json/wp/v2/taxonomies` covers categories and tags.

3. **Inventory the site pages.** `getWpV2Pages` at `/wp-json/wp/v2/pages` with
   `_fields=id,slug,link,title`. The audience-specific pages are the useful ones: `/health-systems/`,
   `/pharma/`, `/employers/`, `/payers/`, `/physicians/`, `/order-forms/`, `/referrals/`.

4. **Enumerate the MCP namespace.** `getMcp` at `/wp-json/mcp` returns HTTP 200 and advertises two
   servers: `mcp-oauth-server` and `mcp-adapter-default-server`, both accepting POST/GET/DELETE.

5. **Establish that the tool set is gated — do not guess it.** `postMcpMcpOauthServer` with
   `{"jsonrpc":"2.0","id":1,"method":"tools/list"}` returns:

   ```
   HTTP/2 401
   WWW-Authenticate: Bearer realm="https://mylocalinfusion.com",
     resource_metadata="https://mylocalinfusion.com/.well-known/oauth-protected-resource"
   {"code":"mcp_unauthorized","message":"MCP authentication required.","data":{"status":401}}
   ```

   That is a correct RFC 9728 challenge. Follow it to
   `/.well-known/oauth-protected-resource`, then to `/.well-known/oauth-authorization-server`, which
   declares `authorization_code` + `refresh_token`, PKCE `S256`, `scopes_supported: ["mcp"]`,
   `token_endpoint_auth_methods_supported: ["none"]` and `client_id_metadata_document_supported:
   true`. The second server, `mcp-adapter-default-server`, answers `rest_forbidden` (401) — a
   WordPress capability check rather than an OAuth challenge.

6. **Expect `getWpAbilitiesV1Abilities` to fail, and understand why it matters.**
   `/wp-json/wp-abilities/v1/abilities` returns 401 `rest_forbidden`. That registry is what the MCP
   adapter projects tools from, so its being gated is exactly why no tool list exists in
   `mcp/local-infusion-tool-crosswalk.yml`. **Do not synthesise tool names from the REST routes.**

7. **Read the content-layer agent surface, which is far more developed than the tool layer.**
   `/llms.txt`, `/llms-full.txt`, `/.well-known/ai-manifest.json`, `/.well-known/brand-facts.json` and
   `/.well-known/llm-sitemap.json` all return 200. Between them they name preferred entry points,
   approved language, metro-routing rules (Richmond → Glen Allen + Midlothian; Long Island → Commack,
   East Meadow, Plainview; Jacksonville → Deerwood, Orange Park) and explicit claim boundaries. Honour
   them.

## What is NOT here

`/.well-known/security.txt`, `/.well-known/openid-configuration`, `/.well-known/api-catalog`,
`/.well-known/ai-plugin.json`, `/.well-known/agent-card.json`, `/.well-known/agent.json`, `/graphql`,
`/openapi.json`, `/asyncapi.json`, `/fhir/metadata` and `/.well-known/smart-configuration` — every one
of them returned 404 on 2026-08-25. There is no status page, no changelog, no SDK, no CLI, no sandbox
and no developer documentation. If you need one of those, the answer is that it does not exist, not
that you have not found it yet.
