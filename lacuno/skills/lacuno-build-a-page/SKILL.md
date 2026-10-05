---
name: lacuno-build-a-page
description: Build or redesign a page or section on a Lacuno site from a brief, a mockup, a screenshot or an existing website, through the Lacuno MCP tools. Use whenever the user asks to create, design, rebuild, restyle or extend pages, sections, navigation or components in Lacuno.
---

# Build a page in Lacuno

A Lacuno site is one JSON document that you change through the Lacuno MCP tools. The user
watches each change arrive live on the editor canvas. Your app may show the tools with
underscores (`sites_list`, `document_apply`); they are the same tools.

## Before you start

1. Call `sites.list` first and pick the site. If the user did not say which and there is more
   than one, ask. Pass that `site` on every other call. (A per-site connection, as in
   self-hosted Lacuno, has no `sites.list` and no `site` argument.)
2. Call `guide` once without a group for the document model and the workflow. Then call it
   with a group (`node`, `style`, `class`, `designToken`, `page`, `component`, ...) for the
   exact operation schemas you need. Do not guess operation shapes; the guide is the reference
   and it matches the server.
3. Call `document.read` once for the revision, pages, classes, breakpoints, design tokens,
   components and assets. Use `page.outline` for the node tree of the page you work on.

## Build in few large batches

`document.apply` takes a batch of operations and the revision you read as `expectedRevision`.
A batch is atomic and validated.

- Plan the whole page first: design tokens (colours, spacing, fonts), classes, then the nodes.
- Send few large batches, for example one for tokens and classes and one per page or per big
  section. Dozens of small batches are slow, noisy on the canvas and easy to get wrong.
- Supply your own ids (letters, digits, `-`, `_`) for everything you create, so later
  operations in the same batch can reference them: create a class `hero-title`, then a node
  that uses it, then `style.set` on it.
- `node.create` takes nested `children`, so one operation can create a whole section.
- Each applied batch answers with the new revision. Use it as the next `expectedRevision`;
  you do not need to read the document again.
- For a large or risky batch, run it with `dryRun: true` or `document.diff` first.
- A stale revision is rejected: call `document.read` for the new revision and resend.

## Style the Lacuno way

- Style through classes, per breakpoint and state, with `style.set`. Reuse existing classes and
  tokens before adding new ones.
- Use design tokens for colours, spacing, radii and fonts so the site stays consistent.
- Link to pages with a `page` binding, not a hard-coded path, so links survive a rename.
- Images: `asset.import` with a public https `url`, or `asset.upload` for a file on the user's
  machine (PUT it with `curl -T`). Never send image bytes as base64 unless they are tiny.
- Repeated pieces (cards, nav items) belong in a component or a collection list.

## Pitfalls

- Never rebuild the page locally (HTML files, a dev server, a local copy of the site) to check
  it. Check it in Lacuno itself, see the `lacuno-check-your-work` skill.
- Do not call `document.read` or `node.get` on everything after each change. Read what you
  need once and track the revision from each batch's answer.
- Do not invent CSS strings for structured values such as gradients; the guide shows the shape.
- `site.publish` publishes to the testing address and only the site owner may call it. Publish
  only when the user asks.

## Finish

Check the result (outline, preview text, a screenshot where available), fix what is off in one
more batch, then tell the user what you built and where to look on the canvas.
