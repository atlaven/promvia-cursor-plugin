# Promvia

Cursor plugin that connects agents to [Promvia](https://promvia.app) through Promvia's official hosted [Model Context Protocol](https://modelcontextprotocol.io/) server.

Promvia measures where ChatGPT, Perplexity, Gemini, Google AI Overviews and other AI engines mention and cite your website, and which sources they cite instead. With this plugin an agent reads those results and can act on them from the editor.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Promvia**.
3. Click **Install**, then complete the Promvia sign-in prompt.

Or run `/add-plugin promvia` in chat.

## MCP

```json
{
  "mcpServers": {
    "promvia": {
      "type": "http",
      "url": "https://promvia.app/api/mcp"
    }
  }
}
```

Auth is OAuth 2.1 with PKCE. Cursor discovers it from the server's 401 and registers itself, so there is no API key, client ID or secret to configure. On the consent screen you choose which of your sites the connection may use and whether it may write.

## What agents can do

| Category | Tools |
| --- | --- |
| Sites | `list_sites`, `select_site`, `current_site` |
| Visibility | `get_visibility_score`, `get_citations`, `get_citation_history`, `get_evidence`, `get_sources_report`, `get_metrics` |
| Fixes | `get_geo_audit`, `get_geo_actions`, `get_opportunities`, `get_deep_scan` |
| Prompts | `list_prompts`, `get_prompt_templates` |
| Account | `get_usage`, `get_capabilities` |
| Write (own scope) | `add_prompt`, `archive_prompt`, `set_prompt_answer`, `sync_prompt_answers`, `start_citation_run`, `start_deep_scan`, `generate_brief`, `update_action_status` |

25 tools: 17 read-only and 8 write tools. Every tool declares `readOnlyHint` / `destructiveHint`, and write tools need the write scope granted at consent.

Start with `list_sites`, then `select_site`. A connection works on one selected site at a time; every site tool answers for that site only, and a site you did not grant is refused.

## Plans

A free Promvia plan exists. MCP read tools need a Starter plan or above, write tools Pro or above. Tool calls count against the account's API allowance, which `get_usage` reports.

## Docs

- Developer docs: https://promvia.app/developers
- Server URL: https://promvia.app/api/mcp
- MCP Registry: `app.promvia/promvia`

## Support

info@atlaven.com

## License

MIT
