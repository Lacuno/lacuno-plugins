# Set up Lacuno

This guide is for an AI agent that a person asked to set up Lacuno. Follow it step by step, do
as much as you can yourself, and hand over to the person only where it says so. Lacuno is a
website builder; once connected you read, build, edit and publish the person's Lacuno sites
through its MCP tools, and they watch every change arrive in the Lacuno editor.

Rules: never ask for, print or store a password, token or key; signing in happens in the person's
browser. No `sudo`, and never pipe a download into a shell.

## 1. Pick your path

- You run shell commands with internet access and your host is Claude Code: step 2.
- Your host is Codex: step 3.
- Any other host with a shell (Cursor, VS Code, Gemini CLI, Windsurf and the like): step 4.
- No shell, or the person uses claude.ai, Claude Desktop or ChatGPT: step 5.

## 2. Claude Code

```
claude plugin marketplace add Lacuno/lacuno-plugins
claude plugin install lacuno@lacuno
```

The plugin brings the Lacuno MCP server and four skills. Tell the person: restart Claude Code,
run `/mcp`, choose `lacuno` and sign in with their Lacuno account in the browser. Then step 6.

If the plugin commands are not available, add the server alone and the skills separately:

```
claude mcp add --transport http lacuno https://mcp.lacuno.io/mcp
npx -y skills add Lacuno/lacuno-plugins -y
```

## 3. Codex

```
codex plugin marketplace add Lacuno/lacuno-plugins
```

Tell the person: run `/plugins`, install Lacuno and sign in when asked. Then step 6.

Without plugins, add the server and the skills separately; the person then runs
`codex mcp login lacuno`:

```
codex mcp add lacuno --url https://mcp.lacuno.io/mcp
npx -y skills add Lacuno/lacuno-plugins -y
```

## 4. Other hosts with a shell

Add the MCP server the way your host expects. Its address is `https://mcp.lacuno.io/mcp`,
streamable HTTP with OAuth sign-in:

- Cursor, in `.cursor/mcp.json`: `{"mcpServers":{"lacuno":{"url":"https://mcp.lacuno.io/mcp"}}}`
- VS Code, in `.vscode/mcp.json`:
  `{"servers":{"lacuno":{"type":"http","url":"https://mcp.lacuno.io/mcp"}}}`
- Gemini CLI: `gemini mcp add --transport http lacuno https://mcp.lacuno.io/mcp`

Then install the skills; the command detects your host:

```
npx -y skills add Lacuno/lacuno-plugins -y
```

Tell the person to sign in when the host asks (Cursor shows "Needs login" next to the server in
its MCP settings). Then step 6.

## 5. Without a shell

The person does these steps; you cannot. Once Lacuno is listed in the Claude connector
directory and in ChatGPT's apps, they open the listing, press Connect and sign in; until then,
tell them:

- claude.ai and Claude Desktop: open
  `https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Lacuno&connectorUrl=https%3A%2F%2Fmcp.lacuno.io%2Fmcp`,
  which fills in the connector; confirm it and sign in. Claude Desktop takes the same connectors.
  By hand: in Customize → Connectors (claude.ai/customize/connectors) or Claude Desktop's
  Settings → Connectors choose *Add custom connector*, paste `https://mcp.lacuno.io/mcp` and sign
  in. On Team and Enterprise an owner adds it under Organization settings → Connectors.
- ChatGPT: turn on Settings → Security and login → Developer mode, then at chatgpt.com/plugins
  choose + and paste the address.

Then step 6.

## 6. Check

Call the Lacuno server's `guide` tool. If it answers, you are connected: call `sites.list` and
remember the sites. If the host says the server needs sign-in, hand the person the link it shows
and wait; do not retry on your own. An empty site list means the person has no site yet: they
create one at https://app.lacuno.io.

## 7. First use

Say: "Lacuno is connected. I can build and edit your sites: pages, text, images, styles, content
collections and forms, and publish when you ask. Which site shall we work on?" Then wait for the
person. Before the first edit read `guide`; the skills say how to build pages, work with content
and forms, and check your work.
