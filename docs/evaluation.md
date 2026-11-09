# PokéItem connector: evaluation cases

Prompts, expected tool selection and expected answers for reviewing the PokéItem MCP connector
(`https://api.pokeitem.fr/mcp`). Run them with a PokéItem account that has a few cards in its binder.
No production or customer data is included.

## Positive cases

| # | Intent | Prompt | Expected tools | Expected answer |
|---|---|---|---|---|
| P1 | Graded card price | What is a 1st edition Charizard 4/102 worth in PSA 10? | `lookup_card` | A EUR price for the 1st edition print, grader PSA, grade 10, with the link to the card page. If no slab price exists, the assistant says so and does not substitute the raw near-mint price. A 1st edition card never falls back to the Unlimited price. |
| P2 | Deal check | A seller wants €25 for Mew ex 151/165 in French, is that a good price? | `deal_check` | A good / fair / high verdict, the gap in %, and the PokéItem fair value of the French version. |
| P3 | Sealed product | How much is the Prismatic Evolutions Elite Trainer Box worth? | `lookup_item` | Up to 5 matching sealed products with their EUR value and links. |
| P4 | Read the binder | What are the 5 most valuable cards in my binder? | `collection_summary` or `portfolio_analysis` | The member's top cards with their values. Only the connected member's binder is read. |
| P5 | Write to the binder | Add a Base Set Pikachu 58/102 in near mint to my binder. | `lookup_card` then `add_card` | The card is added once (version, language, condition as asked) and the assistant confirms it. |

## Negative cases (no PokéItem tool should be called)

| # | Intent | Prompt | Expected behaviour |
|---|---|---|---|
| N1 | Off topic | What's the weather in Paris tomorrow? | No PokéItem tool call. |
| N2 | Game rules, no price | Explain how energy cards work in the Pokémon TCG. | General answer, no tool call. |
| N3 | Other collectible | What is a 1952 Topps Mickey Mantle baseball card worth? | No PokéItem tool call: not a Pokémon card. |

## Permission and safety checks

| Check | Expected result |
|---|---|
| Token granted without `mcp:collection:write` | Write tools are not listed in `tools/list`; a direct call returns a permission error. |
| `remove_copy`, `remove_sealed` or `price_alert_delete` without `confirm=true` | The tool refuses and asks for confirmation; nothing is deleted. |
| Asking for another member's binder | Not possible: every binder tool is scoped to the connected account (`trade_preview` only reads another trainer's public profile). |
| Repeated lookups beyond the plan quota | Tool error `RATE_LIMITED` naming the limit; the client should wait for the hourly window. |
| Results | Never contain marketplace listings; card and product results carry a link to their PokéItem page. |
