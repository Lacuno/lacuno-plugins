---
name: lacuno-check-your-work
description: Verify changes on a Lacuno site after building or editing it, using page.outline, page.preview text and page.screenshot. Use after every substantial document.apply batch on a Lacuno site, before telling the user a page is done, and whenever the user asks how a Lacuno page looks or whether something worked.
---

# Check your work in Lacuno

The Lacuno server explains how. Call `guide` with the topic `check` and follow it: outline, text, screenshot at 1280 and 390, fix in one batch, check again. Never rebuild the site on your machine.

Call `sites.list` first and pass `site` on every call (a self-hosted, per-site connection has neither).
