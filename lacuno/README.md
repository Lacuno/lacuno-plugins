# Lacuno plugin

Connects your AI app to Lacuno Cloud at `https://mcp.lacuno.io/mcp` and adds five skills: build a
page, check your work, content (CMS), forms, and variants and demos. You sign in with your Lacuno
account; the AI then works on the workspaces and sites where you are an owner or editor, and names
the site on each call.

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
| `workspaces.list` | Lists the workspaces you can work in, with their plan. |
| `demos.list` | Lists a workspace's client demos with their links. |
| `guide` | Notes: the basics and how-to topics. |
| `document.read` | Reads a site's document: pages, styles, components, collections, assets. |
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
| `node.create`, `style.set`, `page.update`, … | One tool per kind of change to the document, named like it: pages, elements, classes and styles, design tokens, components, collections and entries, languages. Each change is all or nothing; `dryRun` shows it without making it. The ones named `….delete` or `….remove` delete; the server refuses to delete what is still in use. |
| `workspace.create` | Creates a workspace of yours. |
| `site.create` | Creates a site in a workspace, from a template or as a copy of another site. |
| `demo.save` | Creates or changes a client demo: a link that shows sites as versions to choose from. |
| `demo.tour` | Writes the guided tour of a demo version. |
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
- **lacuno-variants-and-demos**: several versions of a site for a client, shown in one demo link.

Each skill holds its own steps and rules. Each tool declares its own fields; the `guide` tool has
notes by topic for reference. Nothing in Lacuno's tools deletes a workspace, site or demo: that
stays with you, in Lacuno.
