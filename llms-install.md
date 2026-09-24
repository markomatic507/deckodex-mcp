# Installing the Deckodex MCP server

Deckodex is a **hosted, remote** MCP server. There is nothing to clone, build or install, and no API key:
authentication is OAuth 2.1 (dynamic client registration + PKCE), done in the user's browser.

## Steps

1. Add this server to the MCP settings file (for Cline: `cline_mcp_settings.json`):

   ```json
   {
     "mcpServers": {
       "deckodex": {
         "type": "streamableHttp",
         "url": "https://deckodex.com/mcp",
         "disabled": false,
         "autoApprove": []
       }
     }
   }
   ```

2. Do **not** add an `Authorization` header or ask the user for a token. On first connection the server
   answers `401` with OAuth metadata (`https://deckodex.com/.well-known/oauth-protected-resource/mcp`);
   the client registers itself and opens the browser. In Cline, click **Authenticate** on the Deckodex
   server if the browser does not open by itself.
3. The user signs in to Deckodex (Google or an emailed link; a free account is created on first sign-in)
   and clicks **Approve** on the Deckodex consent screen.
4. Verify: call `search_cards` with `{"query": "Strike Freedom"}` — it should return Gundam Card Game cards
   such as GD05-002 Strike Freedom Gundam.

Card, price and meta tools are free. Reading the user's own collection and decks needs the `read` scope;
saving decks and editing the collection (write tools) need Deckodex Pro.
