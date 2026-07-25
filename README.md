# Echo AI MCP Server

A remote MCP server for [Echo AI](https://echoai.so), a no-code platform for building AI chatbots, assistants and agents.

Connecting an Echo AI account to any MCP-compatible client lets the agent:

- List the Echos you choose to share
- Read an Echo's configuration and analytics
- Review recent conversations
- Send messages to an Echo
- Fetch a ready-to-paste embed snippet for any website or app
- Get the full headless integration guide (REST API, streaming chat, commerce, booking, tickets, voice)

## Endpoint

```
https://auth.echoai.so/functions/v1/mcp
```

Transport: Streamable HTTP (MCP spec 2025-06-18)

## Authentication

OAuth 2.1 with PKCE and Dynamic Client Registration.

First connection triggers an in-browser approval screen where you sign in to Echo AI and pick which Echos to share. The connected client receives a scoped access token that only works for the selected Echos.

## Discovery

- `https://echoai.so/.well-known/oauth-authorization-server`
- `https://echoai.so/.well-known/oauth-protected-resource`
- `https://echoai.so/brand/mcp/server.json`

## MCP client config

```json
{
  "mcpServers": {
    "echo-ai": {
      "url": "https://auth.echoai.so/functions/v1/mcp"
    }
  }
}
```

## Replit

One-click install:

[![Install Echo AI](https://replit.com/badge?caption=Install%20Echo%20AI)](https://replit.com/integrations?mcp=eyJkaXNwbGF5TmFtZSI6IkVjaG8gQUkiLCJiYXNlVXJsIjoiaHR0cHM6Ly9hdXRoLmVjaG9haS5zby9mdW5jdGlvbnMvdjEvbWNwIn0=)

Or open [https://replit.com/integrations?mcp=eyJkaXNwbGF5TmFtZSI6IkVjaG8gQUkiLCJiYXNlVXJsIjoiaHR0cHM6Ly9hdXRoLmVjaG9haS5zby9mdW5jdGlvbnMvdjEvbWNwIn0=](https://replit.com/integrations?mcp=eyJkaXNwbGF5TmFtZSI6IkVjaG8gQUkiLCJiYXNlVXJsIjoiaHR0cHM6Ly9hdXRoLmVjaG9haS5zby9mdW5jdGlvbnMvdjEvbWNwIn0=) and approve the OAuth prompt.

## Cursor

One-click install:

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](cursor://anysphere.cursor-deeplink/mcp/install?name=echo-ai&config=eyJ1cmwiOiJodHRwczovL2F1dGguZWNob2FpLnNvL2Z1bmN0aW9ucy92MS9tY3AifQ==)

Manual install: open **Cursor Settings > Tools & MCP > New MCP Server**, or edit `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "echo-ai": {
      "url": "https://auth.echoai.so/functions/v1/mcp"
    }
  }
}
```

On first use Cursor registers itself automatically and opens the Echo AI OAuth approval screen.

## Lovable

[![Add to Lovable](https://img.shields.io/badge/Add%20to-Lovable-6D44FF?style=for-the-badge&labelColor=09041A)](https://lovable.dev/dashboard?connectors)

1. Open [Lovable Connectors](https://lovable.dev/dashboard?connectors), scroll to the bottom of the **All** view and pick the **Custom** card labelled **MCP** ("Connect your own MCP").
2. Server name: `Echo AI`
3. Server URL: `https://auth.echoai.so/functions/v1/mcp`
4. Authentication: leave **OAuth** selected, then click **Add & authorize**.
5. Sign in to Echo AI and choose which Echos to share.

Lovable can then read your Echos as live context while you build, for example: "Using the Echo AI connector, get the embed snippet for my support Echo and add it to this page."

## Claude

Claude's official Connectors Directory requires a Team or Enterprise organization to list a connector, so Echo AI is not in the directory yet. Individual users can still connect manually through a custom connector.

1. Go to **https://claude.ai/customize/connectors**
2. Click **+** then **Add custom connector**
3. Paste the remote MCP server URL: `https://auth.echoai.so/functions/v1/mcp`
4. Leave **Advanced settings** empty - Echo AI handles OAuth 2.1 and Dynamic Client Registration automatically
5. Click **Add** and approve the Echo AI OAuth screen to pick which Echos to share

Free users can add one custom connector. Pro and Max users can add more. The same tools and scopes work in Claude.ai, Claude Desktop, Claude Mobile, and Claude Code once connected.

Claude Code users can also run:

```bash
claude mcp add --transport http echo-ai https://auth.echoai.so/functions/v1/mcp
```

## ChatGPT

Echo AI is a remote MCP server, so it connects to ChatGPT in developer mode without any local install.

1. In ChatGPT, open **Settings > Security and login** and turn on **Developer mode**.
2. Open **Settings > Plugins** (or https://chatgpt.com/plugins) and click the **+** button.
3. Name: `Echo AI`. Description: `Connect your Echo AI assistants, catalog, bookings and analytics.`
4. MCP server URL: `https://auth.echoai.so/functions/v1/mcp`
5. Create the connection and approve the Echo AI OAuth screen to pick which Echos to share.
6. Start a new conversation and enable Echo AI from the tools menu.

Developer mode availability depends on your ChatGPT account and workspace policy. After an Echo AI server update, open the connection and click **Refresh** to pull the new tool metadata.

You can also test the server from the OpenAI API Playground (**Tools > Add > MCP Server**) or the Responses API by passing the same URL as an MCP tool.

## Codex

Add Echo AI to the [Codex CLI](https://github.com/openai/codex) or the ChatGPT IDE extension as a remote MCP server:

```bash
codex mcp add echo-ai --url https://auth.echoai.so/functions/v1/mcp
codex mcp login echo-ai
```

The second command opens the Echo AI OAuth approval screen in your browser. Once approved, Codex can list your Echos and call any of the tools above.

## Windsurf

1. Open Windsurf and go to **Settings > Tools > Windsurf Settings > Add Server**.
2. If Echo AI is not in the template list, click **View raw config** and edit `~/.codeium/mcp_config.json`.
3. Add the Echo AI entry:

```json
{
  "mcpServers": {
    "echo-ai": {
      "serverUrl": "https://auth.echoai.so/functions/v1/mcp"
    }
  }
}
```

4. Save and press **Refresh** in the MCP panel. The first time you use a tool, Windsurf opens the Echo AI OAuth approval screen in your browser.

## Supported scopes

- `echos:read` - list Echos, read config, analytics, conversations
- `echos:chat` - send messages to an Echo

## Tools

- `list_echos` - list the Echos the connected account can access
- `get_echo` - full configuration for one Echo
- `get_embed_snippet` - copy-paste widget embed code for an Echo
- `get_headless_integration` - full headless build guide: REST API, streaming chat, commerce, booking, tickets, voice and a ready React component
- `get_echo_analytics_summary` - conversations, messages and usage summary
- `list_recent_conversations` - recent chat sessions for an Echo
- `get_conversation_history` - messages in one conversation
- `send_message_to_echo` - chat with an Echo (consumes the owner's Echo AI credits)

## Resources

- Website: https://echoai.so
- Docs: https://echoai.so/api#mcp
- Privacy: https://echoai.so/privacy
- Terms: https://echoai.so/terms
- Support: dens@echoai.so
- Logo pack: https://echoai.so/brand/mcp/echo-mcp-logo-pack.zip

## Reviewer test account

Available on request for directory reviewers. Contact dens@echoai.so.
