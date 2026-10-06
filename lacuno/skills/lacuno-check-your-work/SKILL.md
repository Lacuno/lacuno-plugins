---
name: lacuno-check-your-work
description: Verify changes on a Lacuno site after building or editing it, using page.outline, page.preview text and page.screenshot. Use after every substantial document.apply batch on a Lacuno site, before telling the user a page is done, and whenever the user asks how a Lacuno page looks or whether something worked.
---

# Check your work in Lacuno

Lacuno renders the page for you. Look at the real result through the MCP tools, not at a copy
you made yourself. Call `sites.list` first if you have not, and pass `site` on every call.
(A per-site connection, as in self-hosted Lacuno, has no `sites.list` and no `site` argument.)

## The loop

After each large batch:

1. **Structure:** `page.outline` with the page id (or `component`) shows the node tree with ids,
   tags, classes and a text snippet. Check that sections sit where you meant and nothing is
   duplicated or left empty. Pass `depth` to keep big pages short.
2. **Text:** `page.preview` with `text: true` gives one line per text node, `nodeId<TAB>text`.
   Read it for typos, missing copy, wrong order and leftover placeholder text. Use the node ids
   to fix things directly. Without `text` it returns the published HTML; read that only when you
   need to check markup such as attributes or links.
3. **Look:** `page.screenshot` returns a PNG of the page at a width (default 1280). Check a
   phone width too (390). Pass `node` to crop to one element, `height` for just the first
   screen. Screenshots are not available on every server; if the tool is missing or fails, rely
   on the outline and the preview text and do not try other ways.
4. **Styles:** `styles.get` with a class, a list of classes or a `node` (all classes in that
   subtree, in one call) shows the declarations per breakpoint and state, when
   something looks wrong and you need to know why.
5. Fix everything you found in one batch, then check once more.

For collection pages, pass `entry` (id or slug) to preview or screenshot one entry's page.

## Before a big change

`document.diff` with the planned operations summarises what they would change, and
`document.apply` with `dryRun: true` returns the patches without applying them.

## Do not

- Do not rebuild the page locally, start a dev server, write HTML files or render the site in
  your own browser to check it. That costs a lot, drifts from what Lacuno publishes and is not
  what the user sees.
- Do not re-read the whole document (`document.read`, `node.get` on the root, `styles.get`
  without a class) after every change. Check the page you changed.
- Do not publish just to look at the result. `page.preview` and `page.screenshot` need no
  publish. Use `site.publish` only when the user wants a testing link.

## Tell the user

Say what you checked and how (for example "outline and text at desktop; screenshot at 390 px"),
and anything you could not verify.
