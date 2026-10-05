---
name: lacuno-content
description: Work with CMS content on a Lacuno site - collections, fields and entries such as blog posts, team members, projects or legal texts - and show them on pages with collection lists, collection pages and field bindings. Use when the user wants to add, import, edit or display structured or repeated content in Lacuno.
---

# Content in Lacuno: collections and entries

Call `sites.list` first and pass `site` on every call. (A per-site connection, as in
self-hosted Lacuno, has no `sites.list` and no `site` argument.) Call `guide` with the groups
`collection`, `field` and `entry` for the exact operation schemas, and read the guide's
Collections section once.

## The model

- A **collection** defines **fields** (text, slug, rich text, number, boolean, date, image,
  file, color, link, option, reference, multi-reference). Its slug field gives each entry its
  address.
- **Entries** hold the content, keyed by field id. Each value has its field type's shape: a date
  is `2026-09-28`, an image is an asset id, a rich text is a rich text document.
- People edit the same entries in the editor's CMS, so give collections and fields clear names.

## Steps

1. `document.read` lists existing collections with `usedBy`; `entries.list` reads a
   collection's entries. Reuse a collection before creating a similar one.
2. Create the collection with its fields, and all entries, in one `document.apply` batch with
   ids you supply, so the entries can name the field ids right away. For many entries, use a
   few large batches rather than one call per entry.
3. Show the entries on a page:
   - a `collection-list` node repeats its children once per entry; its `query` filters, sorts,
     limits and paginates;
   - a page with `collection` and `[slug]` in its path renders once per entry;
   - inside either, bind text and attributes with `{"type":"field","field":"<fieldId>"}`;
     elsewhere name the entry too: `{"type":"field","entry":"<entryId>","field":"<fieldId>"}`.
4. Set `seo.fields` on a collection page so each entry gets its own title, description and
   social image.
5. Check with `page.preview` (`text: true`, and `entry` for one entry's page), see the
   `lacuno-check-your-work` skill.

## Images in entries

Import images with `asset.import` (`url`) or `asset.upload` (a local file), then store the
returned asset id in the image field. Do not pass image bytes through the conversation.

## Pitfalls

- Changes that would break existing entries are refused: a new required field while entries
  have no value, removing an option some entry uses. Fill the values in the same batch.
- Deleting a used collection, field or entry is refused with `referencedBy`. Remove or rebind
  those uses first, in the same batch.
- Field bindings work only inside a list or on a collection page unless they name an entry.
- Do not re-read all entries after each change; the batch answer tells you what was created.
