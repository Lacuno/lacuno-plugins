# Lacuno plugins

[Lacuno](https://lacuno.io) is a visual website builder that your AI app can work in: it reads
and edits the same site you see in the editor, and you watch each change arrive on the canvas.

This repository holds the Lacuno plugin for Claude (Claude Code, claude.ai, Claude Desktop) and
for OpenAI (Codex, ChatGPT). It connects your app to Lacuno Cloud at one address,

```
https://mcp.lacuno.io/mcp
```

and adds skills that help the AI work well with Lacuno. You sign in with your Lacuno account
the first time the app connects; the AI can then reach every site where you are an owner or
editor and names the site on each call.

## Install

**Claude Code**

```
claude plugin marketplace add Lacuno/lacuno-plugins
claude plugin install lacuno@lacuno
```

Then run `/mcp` in a session, pick `lacuno` and sign in.

**claude.ai and Claude Desktop**

In Customize → Connectors (claude.ai/customize/connectors) or in Claude Desktop's Settings →
Connectors, choose *Add custom connector* and paste `https://mcp.lacuno.io/mcp`. On Team and
Enterprise, an owner adds it in Organization settings → Connectors. Once Lacuno is listed in
Anthropic's directory, you can add it there in one click, skills included.

**Codex**

```
codex plugin marketplace add Lacuno/lacuno-plugins
```

Then open the plugin browser with `/plugins`, install Lacuno and sign in when asked.

**ChatGPT**

Turn on Settings → Security and login → Developer mode, then at chatgpt.com/plugins choose +
and paste `https://mcp.lacuno.io/mcp`. Once Lacuno is listed in OpenAI's plugin directory,
install it from the Plugins tab instead.

**Self-hosted Lacuno**

This address is for Lacuno Cloud. A self-hosted Lacuno has one address per site: open the
site in the editor, choose *Connect your AI* and follow the steps for your app there. The skills
in this repository work with those addresses too.

## Skills

| Skill | What it does |
| --- | --- |
| `lacuno-build-a-page` | Builds or redesigns pages from a brief, a mockup or a screenshot, in a few large batches |
| `lacuno-check-your-work` | Checks the result with the page outline, the page's text and screenshots where available |
| `lacuno-content` | Sets up CMS collections and entries and shows them on pages |
| `lacuno-forms` | Adds contact and other forms whose messages are emailed to the site owner |

The skills stay short on purpose. The detailed reference for every operation comes from the
Lacuno server's own `guide` tool, so it always matches the version you are connected to.

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

## License

MIT, see [LICENSE](LICENSE).
