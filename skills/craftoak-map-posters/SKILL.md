---
name: craftoak-map-posters
description: Design, preview and order custom city map posters from CraftOak. Use when the user wants a map poster, street-map wall art, a personalized city/neighborhood print, or asks about CraftOak sizes, frames, prices or checkout.
---

# CraftOak map posters

CraftOak makes personalized city map posters: pick a place, a style, an orientation, a title and subtitle, preview the design, then buy a physical print (optionally framed). The `craftoak` MCP server exposes four tools. Digital downloads are **not** sold.

## Tools

| Tool | Use it to | Notes |
| --- | --- | --- |
| `generate_map` | Create a new design for a city/place | Returns a `mapId`, a preview image URL and an edit URL. Call it once per new design. |
| `update_map` | Change an existing design | Always pass the `mapId` from the design the user is talking about. Never generate a new map when the user is editing one. |
| `get_print_options` | Read live sizes, frame options, prices and currency | Call before quoting any price or size. Never quote from memory. |
| `create_checkout_link` | Produce an external checkout URL for one design, size and frame | Only after the design exists and the size/frame are confirmed to be in `get_print_options`. |

## Workflow

1. **New poster** – Collect the place (city, plus neighborhood or address if given), orientation (portrait/landscape) and any title/subtitle, then call `generate_map`. Reasonable defaults are fine when the user does not specify; say which defaults you used.
2. **Show the preview** – Present the preview image/URL and summarize the design choices. Offer to adjust style, orientation, title or subtitle.
3. **Edits** – Use `update_map` with the same `mapId`. Show the updated preview.
4. **Sizes & prices** – Call `get_print_options` and list only what it returns (sizes, frame options, prices, currency). Do not invent delivery times, discounts or stock.
5. **Checkout** – When the user picks a size and frame, call `create_checkout_link` with the `mapId`, size and frame. Give the user the link and explain that payment happens on the CraftOak checkout page (Stripe).

## Rules

- Never claim an order was placed, paid or shipped. The tools only prepare a design and a checkout link; the purchase happens in the user's browser.
- Keep `mapId`s straight when several designs exist in one conversation; name them by city when referring back ("your Paris landscape design").
- Prices and availability come from `get_print_options` at the time of the request; do not carry them over from an earlier turn if the user changes size, frame or currency.

## Out of scope — explain, do not call tools

- **Digital/PDF downloads** – not offered. Explain that CraftOak sells physical prints and offer to continue with a physical poster.
- **Order status, cancellations, refunds** – not available through these tools. Point the user to CraftOak support: https://www.craftoak.com/faq
- **Navigation, live traffic, directions** – map posters are decorative wall art, not a navigation product.
