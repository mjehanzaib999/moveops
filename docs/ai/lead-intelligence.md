# Lead Intelligence

**Project:** MoveOps · **[Live demo →](https://moveops.kognio.ai)**

## The use case
A busy sales rep staring at dozens of open leads has no reliable way to know who to call first or what to say. Hot enquiries go cold while time is spent on leads that were never going to book. Owners want the pipeline triaged automatically.

## How the AI works
For each open lead, MoveOps assembles real signals from the database — source, stage, days since created, days since last contact, move size and quoted value, days until the move, and inbound/outbound message counts. Claude (via OpenRouter) receives the whole batch in one call as a revenue-operations analyst and returns a structured score per lead. Output is strict JSON; any lead the model skips is backfilled with a deterministic heuristic, so every lead is always scored — even with no API key configured.

## What you get
- A conversion-likelihood score (0–100) for every open lead
- An urgency rating (low / medium / high) driven by move date and recency
- One or two short reasons citing the strongest signals
- A specific next-best-action (e.g. *"Call now to lock in the Saturday crew and send the $2,400 quote"*)
- The list sorted hottest-first

## Try it live
Sign in (`demo@kognio.ai` / `Demo1234!`) and open **Lead Intelligence** in the sidebar. The seeded demo company ships with ~80 leads, so scores, reasons and actions populate immediately.

## Under the hood
`POST /ai/lead-score`, authenticated and tenant-scoped. One batched Claude call (`anthropic/claude-sonnet-4.5` via OpenRouter, `response_format=json_object`). Message counts come from a single grouped query; scores are validated and clamped, and a heuristic covers the no-key / failure path.
