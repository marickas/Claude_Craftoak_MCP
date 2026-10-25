# CraftOak for Claude

Design, preview and order personalized city map posters from [CraftOak](https://www.craftoak.com) directly in Claude.

- Choose a city or place, style, orientation, title and subtitle
- Preview the design and refine it in conversation
- Compare live print sizes, frame options and prices
- Open an external checkout link to buy a physical poster (optionally framed)

Digital downloads are not offered. Payments are processed on CraftOak's checkout page via Stripe.

## Two ways to get CraftOak in Claude

### 1. Connector (Claude.ai, Desktop, Mobile, Claude Code, Cowork)

The CraftOak MCP server is a remote, no-authentication server:

```
https://www.craftoak.com/api/mcp
```

Once it is listed in the [Connectors Directory](https://claude.ai/directory/connectors), click **Connect** on the CraftOak entry. Until then, add it as a custom connector: **Settings → Connectors → Add custom connector** and paste the URL above.

### 2. Plugin (Claude Code / Cowork)

This repository is also a Claude plugin. It bundles the connector plus a skill that teaches Claude the CraftOak design → preview → print → checkout workflow and its limits.

```bash
claude plugin marketplace add craftoak/craftoak-claude-plugin
claude plugin install craftoak@craftoak
```

Or inside a session:

```
/plugin install craftoak --marketplace craftoak/craftoak-claude-plugin
```

To try it without installing, from the unzipped folder:

```bash
claude --plugin-dir ./craftoak-claude
```

## Tools

| Tool | Type | Description |
| --- | --- | --- |
| `generate_map` | write (non-destructive) | Create a new map poster design. Returns `mapId`, preview URL and edit URL. |
| `update_map` | write (non-destructive) | Update an existing design by `mapId` (style, orientation, title, subtitle). |
| `get_print_options` | read-only | Live sizes, frame options, prices and currency. |
| `create_checkout_link` | write (non-destructive), opens external link | External Stripe checkout URL for a given `mapId`, size and frame. |

## Example prompts

- "Create a portrait map poster of New York."
- "Design a landscape poster of Paris titled *Our Paris*."
- "Make the New York poster landscape and use the Retro Black style."
- "What sizes and frames can I buy, and what do they cost?"
- "Give me a checkout link for my New York map, 50 × 70 cm, without a frame."

## Privacy Policy

Full policy: https://www.craftoak.com/privacy-policy

- **Data collected:** the design inputs you provide in conversation (place, style, orientation, title, subtitle) and the resulting design preview. No account is required and no authentication is performed by the connector.
- **Usage and storage:** inputs are used only to render the requested design and to generate a checkout link. Designs are stored on CraftOak servers so they can be previewed, edited and purchased.
- **Third-party sharing:** payment details are entered on and processed by Stripe at checkout; CraftOak never receives card numbers. Map tiles are rendered by CraftOak's own rendering pipeline.
- **Data retention:** unpurchased designs are retained for a limited period and then deleted; purchased designs are retained with the order for fulfilment, support and legal record-keeping.
- **Conversation data:** the connector does not read Claude memory, chat history or user files, and does not collect conversation data beyond the tool parameters.
- **Contact:** https://www.craftoak.com/faq

## Support

FAQ and contact: https://www.craftoak.com/faq
Terms of service: https://www.craftoak.com/terms-of-service
