# AI Move Estimator

**Project:** MoveOps · **[Live demo →](https://moveops.kognio.ai)**

## The use case
Removals firms quote by sending a surveyor out or by guessing over the phone — both slow, and both easy to under- or over-price. Sales staff need a professional volumetric survey from nothing more than a customer's plain-English description of their move.

## How the AI works
Claude (via OpenRouter) plays a senior removals surveyor. It reads the free-text description plus optional hints (bedrooms, distance, stairs) and, grounded by per-item cubic-foot rules baked into the system prompt, returns one structured survey in a single call. The streaming endpoint has the model narrate its reasoning first, token-by-token over SSE, then emit a delimited JSON block that is parsed and coerced into a validated response. If no API key is set or parsing fails, a deterministic heuristic produces a usable estimate instead.

## What you get
- A room-by-room inventory with per-item quantities and cubic footage
- Total volume (cu ft and m³) and estimated weight
- Recommended crew size, truck size and labour hours
- A packing-materials list
- Low / expected / high price range (AUD) plus stated assumptions
- A short reasoning narrative explaining the sizing and price

## Try it live
Sign in (`demo@kognio.ai` / `Demo1234!`), open **AI Estimator** in the sidebar, and describe a move. Example: *"3-bed house with a piano and 40 boxes, second-floor flat, 25 km."* Watch the reasoning stream, then the structured survey lands.

## Under the hood
`POST /ai/estimate/stream` (SSE) and `POST /ai/estimate` (JSON), both authenticated and tenant-scoped. Model `anthropic/claude-sonnet-4.5` via OpenRouter, `response_format=json_object` for the non-streaming path, a `===ESTIMATE_JSON===` delimiter for the stream. Every field is coerced and clamped server-side; a heuristic fallback guarantees a response.
