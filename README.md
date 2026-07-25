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
