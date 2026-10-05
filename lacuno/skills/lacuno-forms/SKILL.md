---
name: lacuno-forms
description: Add or change a contact form, signup form or any other form on a Lacuno site, so that submissions are emailed to the site's owner. Use when the user asks for a contact form, an enquiry or booking form, a newsletter or feedback form in Lacuno.
---

# Forms in Lacuno

A Lacuno form is made of plain nodes. Published, each message is emailed to the workspace
owner, with the visitor's first email address as the reply-to. Nothing is stored and there is
no inbox yet.

Call `sites.list` first and pass `site` on every call. (A per-site connection, as in
self-hosted Lacuno, has no `sites.list` and no `site` argument.) Read the Forms section of
`guide`, and call `guide` with the group `node` for the `node.create` schema.

## Build it in one batch

Create the whole form with one `node.create` and nested `children`:

- a `form` element **without** an `action` attribute, with
  - `data-lacuno-form`: the form's name in the email (default "Contact form"),
  - `data-success`: the message that replaces the form once it is sent;
- per field, a `label` element holding a text with the label and the control:
  - `input` with `name`, `type` (`text`, `email`, `tel`, `number`, `url`, `date`,
    `checkbox`), `placeholder` and `required` as needed,
  - `textarea`, or
  - `select` whose children are text nodes with the tag `option`;
- a submit `button`: a text node with the tag `button` and `type` `submit`.

Give every control a `name`; it labels the value in the email. Include an email field so the
owner can reply. Style the form with classes like any other element, in the same batch.

## Check it

Use `page.outline` and `page.preview` (`text: true`) to see the fields and labels; a screenshot
where available. The canvas shows the form but never sends it. To test sending, the user
publishes the site (or you call `site.publish` if they ask and are the owner) and submits the
form on the testing address.

## Pitfalls

- A `form` with its own `action` (a newsletter provider's, say) is published as it is and is
  not emailed by Lacuno. Use that only when the user wants another service to receive it.
- No file uploads, payment or stored submissions. Say so instead of building them.
- Do not add your own scripts, honeypots or spam checks; Lacuno adds them when it publishes.
- Emails go to the workspace owner. Tell the user if they expected another address.
