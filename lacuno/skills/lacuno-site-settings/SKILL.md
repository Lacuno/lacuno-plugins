---
name: lacuno-site-settings
description: Change a Lacuno site's settings and SEO - page titles and descriptions, the title template, social images, noindex and canonical addresses, the not-found page, redirects, the favicon, and head or body code such as an analytics snippet. Use when the user asks about SEO, meta tags, search results, sharing previews, redirects, a 404 page, a favicon or adding analytics or other code to a Lacuno site.
---

# Site settings and SEO in Lacuno

## Method

1. Call `sites.list` and pass `site` on every later call (a self-hosted, per-site connection has neither). `document.read` with `parts: ["site", "pages", "redirects"]` shows the settings there are.
2. Change the site with `site.update`, a page with `page.update`, redirects with `redirect.add` and `redirect.remove`, passing the revision you read as `expectedRevision` and then the revision from each answer.
3. `page.preview` without `text` returns the page's HTML as published: check its title, description and the other tags in the head there.

## The site

- `site.update` takes the name, the primary language (`locale`), `url`, `titleTemplate`, `fonts`, `favicon` (an asset id), `headCode` and `bodyCode`.
- `titleTemplate` like `{page} — Acme` shapes every page's title. A page's `seo.titleTemplate` replaces it; `false` keeps that page's title as it is.
- `url` is the site's public address. Canonical addresses come from it, and a site with one gets a `/sitemap.xml`.
- Analytics: put the snippet of the provider the person names, exactly as the provider's dashboard gives it, in `headCode`, after what is there.

## Pages

- `page.update` takes `seo`: `title`, `description`, `ogImage` (an asset id, the picture shown when the page is shared), `noindex`, `canonical` and `titleTemplate`.
- `seo.noindex` keeps a page out of search and the sitemap.
- `seo.canonical` is a full address. Left out, the page's own address under the site's `url` is used.
- A page's `lang` (en, de-AT) overrides the site's language.
- A page at `/404` is the not-found page.
- A page that shows one collection entry takes its SEO from the entry's fields: the lacuno-content skill says how.

## Redirects

`redirect.add` sends an old path (`from`) to a path or address (`to`), 301 by default, or 302, 307 or 308. `redirect.remove` takes one away by its `from`.

## Rules

- `site.update` and `page.update` replace each field they get whole, `seo`, `fonts` and `headCode` too: send what is there with your change. `null` removes the field.
- Head and body code runs in every visitor's browser. Add only what the person asks for, as they give it.
- Publish only when the person asks (`site.publish`, owner only; it publishes to the testing address).

## Reference

`site.update`, `page.update` and `redirect.add` declare their own fields. The method and rules above come from this skill.
