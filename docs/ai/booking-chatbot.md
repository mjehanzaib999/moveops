# Booking Chatbot

**Project:** MoveOps · **[Live demo →](https://moveops.kognio.ai)**

## The use case
Website visitors ask the same questions after hours — pricing, service areas, insurance, deposits — and drop off if no one replies. Moving companies want an embeddable assistant that answers accurately, quotes, and captures a qualified lead without a human on shift.

## How the AI works
An embedded widget runs a tool-calling agent loop (up to four iterations per turn). Claude (via OpenRouter) is grounded to a canonical FAQ list and given three tools: `list_faqs` (never guess policy), `compute_quote` (never invent a price), and `create_lead` (only after explicit consent and a name plus email or phone). Conversation history is loaded per visitor so the bot has context. When `create_lead` fires, it writes a normal CRM lead — identical to any other inbound source — and triggers the `lead.created` automation. With no API key, a keyword-matched FAQ fallback keeps the widget functional.

## What you get
- Grounded FAQ answers (no hallucinated policies or prices)
- Instant quotes inside the chat via the pricing engine
- Consent-gated lead capture that lands straight in the pipeline
- Automatic follow-up automations fired on new leads
- A graceful non-LLM fallback path

## Try it live
Open **[/quote](https://moveops.kognio.ai/quote)** (no login needed) and click the chat bubble. Try: *"Do you cover the Inner West, and how much for a 3-bed?"* then *"Yes, book me in — I'm Sam, sam@example.com."*

## Under the hood
`POST /public/chat/message`, unauthenticated and tenant-resolved, persisting conversations and messages. Non-streaming agent loop, `anthropic/claude-sonnet-4` via OpenRouter with OpenAI-format tool specs. `create_lead` routes through the standard lead service and automation engine; a keyword FAQ path covers the no-key case.
