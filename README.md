<p align="center"><img src="assets/logo.png" width="120" alt="PokéItem logo"></p>

# PokéItem: remote MCP server

Look up fair-market prices for Pokémon cards and sealed products, check a deal, and manage your [PokéItem](https://www.pokeitem.fr) binder from Claude, ChatGPT, Cursor or any MCP client.

This repository is the **public listing** of the hosted PokéItem MCP server: connection details, client configs and documentation.
The server itself is a hosted service operated by PokéItem; there is nothing to install or run.

| | |
|---|---|
| Endpoint | `https://api.pokeitem.fr/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.1 with PKCE (S256). Client registration by CIMD or dynamic client registration; no client secret. Personal access tokens are also accepted. |
| Account | A PokéItem account is required. Sign-up is free at [app.pokeitem.fr](https://app.pokeitem.fr). |
| Official MCP Registry | [`fr.pokeitem/pokeitem`](https://registry.modelcontextprotocol.io/v0.1/servers?search=fr.pokeitem/pokeitem) |
| Glama | [fr.pokeitem/pokeitem](https://glama.ai/mcp/connectors/fr.pokeitem/pokeitem) |
| Docs | [pokeitem.fr/en/assistant-ia](https://www.pokeitem.fr/en/assistant-ia) |

[![PokéItem MCP connector](https://glama.ai/mcp/connectors/fr.pokeitem/pokeitem/badges/score.svg)](https://glama.ai/mcp/connectors/fr.pokeitem/pokeitem)

## What you can do

- Look up the PokéItem fair value of a card in euros, by print (1st edition, reverse, shadowless), language (FR, EN, JP, DE, IT, ES…), condition, or graded slab (PSA, CGC, BGS…).
- Check whether an asking price is fair before you buy.
- Look up sealed products (booster boxes, ETBs, tins) and their value.
- See a card's 30-day price trend.
- Ask about your own binder: total, duplicates, wishlist, graded cards, sealed products, set completion, price alerts.
- Add, edit or remove cards, sealed products, wishes and price alerts by chatting. Removals ask for confirmation.
- Identify a card from a photo, export your collection, or preview a trade with a trainer whose binder is visible to you.

Every card and product result links to its PokéItem page, with the picture, all print versions and the full price curve.
PokéItem never returns marketplace listings.

### Example prompts

1. What is a 1st edition Charizard 4/102 worth in PSA 10?
2. A seller wants €25 for Mew ex 151/165 in French, is that a good price?
3. How much is the Prismatic Evolutions Elite Trainer Box worth?
4. What are the 5 most valuable cards in my binder?
5. Add a Base Set Pikachu 58/102 in near mint to my binder.

## Connect

On first use your client opens the PokéItem sign-in page. Sign in, choose the permissions, and you're connected.
You can revoke access at any time in the app: **Profile → Settings → AI agent**.

**Claude** (claude.ai, Desktop, mobile): Settings → Connectors → Add custom connector → `https://api.pokeitem.fr/mcp`.

**Claude Code**
```bash
claude mcp add --transport http pokeitem https://api.pokeitem.fr/mcp
```

**ChatGPT**: Settings → Apps & Connectors → Add connector (developer mode) → `https://api.pokeitem.fr/mcp`, authentication OAuth.

**Cursor, Cline, Windsurf and other clients using `mcpServers`** ([`mcp.json`](mcp.json)):
```json
{
  "mcpServers": {
    "pokeitem": { "url": "https://api.pokeitem.fr/mcp" }
  }
}
```

**VS Code** (`.vscode/mcp.json`):
```json
{
  "servers": {
    "pokeitem": { "type": "http", "url": "https://api.pokeitem.fr/mcp" }
  }
}
```

**Clients without OAuth**: create a personal access token in the app (Profile → Settings → AI agent) and send it as `Authorization: Bearer <token>`.

## Tools

All 29 tools carry `title`, `readOnlyHint`, `destructiveHint` and `openWorldHint` annotations. The tools you see depend on the permissions you grant.

**Read** (16)

| Tool | What it does |
|---|---|
| `whoami` | Account and quotas |
| `lookup_card` | Look up a card price |
| `deal_check` | Check a deal |
| `lookup_item` | Look up a sealed product price |
| `collection_summary` | Collection summary |
| `collection_search` | Search my collection |
| `list_doubles` | List my duplicates |
| `list_sealed` | List my sealed products |
| `list_wishlist` | List my wishlist |
| `list_graded` | List my graded cards |
| `set_completion` | Set completion |
| `list_alerts` | List my price alerts |
| `card_history` | Card price history |
| `export_collection` | Export my collection |
| `portfolio_analysis` | Analyse my collection |
| `trade_preview` | Preview a trade |

**Write** (13)

| Tool | What it does |
|---|---|
| `add_card` | Add a card to my collection |
| `update_copy` | Edit a card copy |
| `remove_copy` | Remove a card copy |
| `keep_one_of_family` | Keep one copy of a duplicate |
| `add_sealed` | Add a sealed product |
| `update_sealed` | Edit a sealed product |
| `remove_sealed` | Remove a sealed product |
| `wishlist_add` | Add to my wishlist |
| `wishlist_remove` | Remove from my wishlist |
| `wishlist_mark_acquired` | Mark a wish as acquired |
| `price_alert_set` | Set a price alert |
| `price_alert_delete` | Delete a price alert |
| `scan_card` | Identify a card from a photo |

## Limits and fair use

Lookups are subject to daily quotas per account; paid PokéItem plans get higher quotas. `whoami` returns your plan and remaining quotas.
Bulk extraction of the catalogue is not allowed.

## Privacy, terms and support

- Privacy: [pokeitem.fr/en/politique-confidentialite#assistant-ia](https://www.pokeitem.fr/en/politique-confidentialite#assistant-ia)
- Terms: [pokeitem.fr/en/cgu](https://www.pokeitem.fr/en/cgu)
- Support: [contact@pokeitem.fr](mailto:contact@pokeitem.fr)
- Operator: SAS POKEITEM, France

## Français

PokéItem est l'application des collectionneurs de cartes Pokémon. Branche ton compte PokéItem à Claude, ChatGPT ou tout client MCP pour consulter la cote d'une carte ou d'un scellé, vérifier un prix demandé et gérer ton classeur en discutant.
Adresse du serveur : `https://api.pokeitem.fr/mcp`. Documentation : [pokeitem.fr/assistant-ia](https://www.pokeitem.fr/assistant-ia).

---

Pokémon and Pokémon character names are trademarks of Nintendo, Creatures and GAME FREAK. PokéItem is not affiliated with, sponsored or endorsed by Nintendo, Creatures, GAME FREAK or The Pokémon Company.
The files in this repository are released under the MIT license. The PokéItem name and logo are not covered by that license.
