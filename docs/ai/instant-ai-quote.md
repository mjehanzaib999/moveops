# Instant AI Quote

**Project:** MoveOps · **[Live demo →](https://moveops.kognio.ai)**

## The use case
Website visitors want a price *now*, in their own words, without filling in a long form or waiting for a callback. Moving companies lose these visitors to whichever competitor answers fastest. MoveOps turns a plain-English description on the public page into an instant, defensible price range.

## How the AI works
On the public quote page, the visitor describes their move to the AI assistant in natural language. Claude (via OpenRouter) extracts the details that matter — bedrooms and pickup/drop-off suburbs — and is instructed to **never invent a price**: it calls a `compute_quote` tool that runs the deterministic pricing engine (bedroom-driven hours plus a suburb-pair travel surcharge), then relays the returned range in a friendly reply. The page also offers a three-field form that hits the same pricing engine directly, so an AI-free instant price is always available.

## What you get
- A low / high price range in plain language
- Estimated hours, hourly rate and callout fee
- A notes line explaining what's included (2-hour minimum, insurance, extras)
- Prices that trace back to a rules engine — the AI reads intent, the engine sets the number

## Try it live
Open the public quote page at **[/quote](https://moveops.kognio.ai/quote)** (no login needed). Fill in the three fields for an instant price, or open the chat bubble and type something like *"How much to move a 2-bed from Bondi to Newtown?"*

## Under the hood
`POST /public/chat/message` (unauthenticated, tenant-resolved) drives the natural-language path via the chatbot's `compute_quote` tool; `POST /public/quote` serves the structured form. Both call the shared `estimate_quote` engine. Chat model: `anthropic/claude-sonnet-4` via OpenRouter, with tool calling.
