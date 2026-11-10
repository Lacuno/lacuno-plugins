# Lacuno plugins

[Lacuno](https://lacuno.io) is a visual website builder that your AI app can work in: it reads
and edits the same site you see in the editor, and you watch each change arrive on the canvas.

This repository holds the Lacuno plugin for Claude (Claude Code, claude.ai, Claude Desktop) and
for OpenAI (Codex, ChatGPT). It connects your app to Lacuno Cloud at one address,

```
https://mcp.lacuno.io/v2/mcp
```

and adds skills that help the AI work well with Lacuno. Apps connected before November 2026 use
`https://mcp.lacuno.io/mcp`, which keeps working. You sign in with your Lacuno account
the first time the app connects; the AI can then reach every site where you are an owner or
editor and names the site on each call.

## Install

**With your AI app**

Paste this into Claude Code, Codex, Cursor or any AI app with a terminal; it installs the plugin
or the MCP server for that app and gets you signed in:

```
Set up Lacuno by following the guide at https://lacuno.io/install.md
```

The guide is [install.md](install.md) in this repository. The steps below are the same by hand.

**Claude Code**

```
claude plugin marketplace add Lacuno/lacuno-plugins
claude plugin install lacuno@lacuno
```

Then run `/mcp` in a session, pick `lacuno` and sign in.

**claude.ai and Claude Desktop**

Open [this link](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Lacuno&connectorUrl=https%3A%2F%2Fmcp.lacuno.io%2Fv2%2Fmcp),
which fills in the connector on claude.ai; confirm it and sign in. Claude Desktop takes the same
connectors. By hand: in Customize → Connectors (claude.ai/customize/connectors) or in Claude
Desktop's Settings → Connectors, choose *Add custom connector* and paste
`https://mcp.lacuno.io/v2/mcp`. On Team and Enterprise, an owner adds it in Organization settings →
Connectors. Once Lacuno is listed in Anthropic's directory, you can add it there in one click,
skills included.

**Codex**

```
codex plugin marketplace add Lacuno/lacuno-plugins
```

Then open the plugin browser with `/plugins`, install Lacuno and sign in when asked.

**ChatGPT**

Turn on Settings → Security and login → Developer mode, then at chatgpt.com/plugins choose +
and paste `https://mcp.lacuno.io/v2/mcp`. Once Lacuno is listed in OpenAI's plugin directory,
install it from the Plugins tab instead.

**Self-hosted Lacuno**

This address is for Lacuno Cloud. A self-hosted Lacuno has one address per site: open the
site in the editor, choose *Connect your AI* and follow the steps for your app there. The skills
in this repository work with those addresses too.

## Skills

| Skill | What it does |
| --- | --- |
| `lacuno-build-a-page` | Builds or redesigns pages from a brief, a mockup or a screenshot, a section at a time |
| `lacuno-check-your-work` | Checks the result with the page outline, the page's text and screenshots where available |
| `lacuno-components` | Makes reusable components with props and slots and places their instances |
| `lacuno-content` | Sets up CMS collections and entries and shows them on pages |
| `lacuno-forms` | Adds contact and other forms whose messages are emailed to the site owner |
| `lacuno-motion` | Adds entrances, motion that follows the scroll, scroll stories and custom keyframes |
| `lacuno-site-settings` | Sets titles, descriptions and other SEO, the 404 page, redirects and head code |
| `lacuno-translate` | Adds a language and translates the site into it, with a glossary and a tone |
| `lacuno-variants-and-demos` | Makes several versions of a site for a client and one demo link to choose from |

Each skill holds its own steps and rules. Each of the Lacuno server's tools declares its own
fields, so those always match the version you are connected to. The
plugin folder's [README](lacuno/README.md) lists the server's tools and which of them change a site.

## Layout

```
.claude-plugin/marketplace.json     Claude marketplace
.agents/plugins/marketplace.json    Codex marketplace
lacuno/
  .claude-plugin/plugin.json        Claude plugin manifest
  plugin.json                       Agent Plugins manifest (Codex, ChatGPT)
  .mcp.json                         MCP server for Claude
  mcp.json                          MCP server for Codex and ChatGPT
  skills/                           the skills, one folder each
```

## Support and privacy

Questions and problems: the [Lacuno Discord](https://discord.gg/gQdRjKf3S). What Lacuno does with your
data: the [Privacy Policy](https://lacuno.io/privacy); use of Lacuno Cloud: the
[Terms](https://lacuno.io/terms).

## License

MIT, see [LICENSE](LICENSE).
