# Installing the PokéItem MCP server

PokéItem is a **hosted remote MCP server**. There is nothing to download, build or run locally.

1. Add this server to the MCP settings (for Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "pokeitem": {
      "url": "https://api.pokeitem.fr/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

2. On first connection, the client opens the PokéItem OAuth sign-in page in the browser. The user signs in (a free account can be created at https://app.pokeitem.fr) and approves the permissions.

3. If the client cannot complete OAuth, the user can create a personal access token in the PokéItem app (Profile → Settings → AI agent) and add it as a header:

```json
{
  "mcpServers": {
    "pokeitem": {
      "url": "https://api.pokeitem.fr/mcp",
      "headers": { "Authorization": "Bearer <PERSONAL_ACCESS_TOKEN>" }
    }
  }
}
```

4. Check the connection by calling the `whoami` tool: it returns the account plan and remaining quotas.

No API keys, environment variables or local dependencies are needed beyond the above.
