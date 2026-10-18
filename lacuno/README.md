# Lacuno plugin

Connects your AI app to Lacuno Cloud at `https://mcp.lacuno.io/mcp` and adds four skills: build a
page, check your work, content (CMS) and forms. You sign in with your Lacuno account; the AI then
works on the sites where you are an owner or editor, and names the site on each call.

## What changes a site

Lacuno keeps two things apart:

- **The site document**, which you see in the editor. Tools that change it show their changes on
  the canvas at once. The public site does not change.
- **The published site**, which visitors see. Only `site.publish` changes it, and Claude publishes
  only when you ask it to.

## The server's tools

Read only, change nothing:

| Tool | What it does |
| --- | --- |
| `sites.list` | Lists the sites you can work on, to choose one. |
| `guide` | Reference: the basics, how-to topics and the exact schema of each operation. |
| `document.read` | Reads a site's document: pages, styles, components, collections, assets. |
| `document.diff` | Shows what a batch of operations would change, without applying it. |
| `node.get` | Reads one element and the elements inside it. |
| `entries.list` | Reads a collection's entries. |
| `styles.get` | Reads classes and their styles. |
| `translations.list` | Lists a language's missing and outdated translations. |
| `page.outline` | A page's tree of elements, in short. |
| `page.preview` | A page's text, or its published HTML, as it would be built. |
| `page.screenshot` | A picture of a page at a given width. |
| `page.view` | Shows you a page in the chat to point at. |
| `editor.open` | Opens the editor in the chat. |
| `editor.selection` | What you selected in the editor open in the chat. |
| `editor.session` | Gives the editor shown in the chat a short-lived sign-in token. |
| `site.analytics` | A site's visitor statistics. |

Change the site, but not what visitors see:

| Tool | What it does |
| --- | --- |
| `document.apply` | Applies a batch of edits to the document, all or nothing. |
| `translations.apply` | Writes translations into a language. |
| `asset.import` | Adds an image, video or font to the site from a public web address. |
| `asset.upload` | Adds a file from your machine to the site. |
| `site.build` | Builds the site's static output, without publishing it. |

Change what visitors see:

| Tool | What it does |
| --- | --- |
| `site.publish` | Publishes the site to its testing address. Only the site's owner may, and Claude does it only when you ask. Making a release the production site stays with you, in Lacuno. |

## Skills

- **lacuno-build-a-page**: building and restyling pages, sections, navigation and motion.
- **lacuno-check-your-work**: checking a page's structure, text and looks at 1280 and 390 wide.
- **lacuno-content**: collections, fields and entries, and showing them on pages.
- **lacuno-forms**: forms whose messages are emailed to the site's owner.

Each skill holds its own steps and rules. The `guide` tool is a reference for exact operation
names, fields and parameters.
