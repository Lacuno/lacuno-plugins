---
name: lacuno-forms
description: Add or change a contact form, signup form or any other form on a Lacuno site, so that submissions are emailed to the site's owner. Use when the user asks for a contact form, an enquiry or booking form, a newsletter or feedback form in Lacuno.
---

# Forms in Lacuno

A form is plain nodes. Once published, each message is emailed to the workspace owner, with the first email address the visitor typed as the reply address. Nothing is stored.

## Method

1. Call `sites.list` and pass `site` on every later call (a self-hosted, per-site connection has neither). Read the page with `document.read` or `page.outline` to find where the form goes.
2. Build the whole form with **one** `node.create` that has children, in a `document.apply` batch with the revision you read:
   - A `form` element without an `action`. `data-lacuno-form` is its name in the email ("Contact form" by default). `data-success` is the text shown after sending.
   - Each field: a `label` element holding a text (the label) and the control: an `input` (`name`; `type` text, email, tel, number, url, date or checkbox; `placeholder`; `required`), a `textarea`, or a `select` with text children tagged `option`.
   - Every control needs a `name`. Include an email field so the owner can reply.
   - Last: a text node tagged `button` with `type` submit.
3. Style it with classes like any other nodes, then check the page as the lacuno-check-your-work skill describes, at 1280 and 390 wide.
4. Tell the person how to test it: the canvas never sends, so they publish and submit the form on the testing address. Publish only when they ask.

## Rules

- A form with its own `action` publishes as it is and is not emailed.
- No file uploads, payments or stored messages. Say so if the person asks for them.
- No own scripts, honeypots or spam checks: Lacuno adds them.

## Reference

The server's `guide` tool is a reference for exact operation names, fields and JSON schemas, for example `guide` with the group `node`. The method and rules above come from this skill.
