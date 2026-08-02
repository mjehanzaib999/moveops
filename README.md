# MoveOps

**End-to-end automation platform for moving / removals companies — from lead capture to invoiced job.**

### 🔗 [Live demo → moveops.kognio.ai](https://moveops.kognio.ai)
Demo login: **`demo@kognio.ai`** / **`Demo1234!`** · Public instant-quote page: **[/quote](https://moveops.kognio.ai/quote)**

---

## The problem
Moving companies lose jobs to slow lead follow-up and run operations across disconnected inboxes, spreadsheets, and phone calls. Quotes are manual, follow-ups get forgotten, and there's no single view of the pipeline.

## What it does
MoveOps is a single command center for a removals business:

- **Multi-channel lead capture** + an **AI email parser** that turns messy inbound enquiries into structured leads.
- **Configurable automation engine** — auto-replies, timed follow-ups, and reminders across email / SMS / WhatsApp.
- **Pricing engine** and a **public instant-quote page** customers can use themselves.
- **Job scheduling** and a **field-crew app** to complete jobs with auto-calculated invoicing.
- **Funnel + KPI dashboard** and an **embeddable AI chatbot** for the company website.

~50 API endpoints across leads, jobs, calendar, field ops, invoicing, automations, and public/webhook surfaces.

## 🤖 AI features — try them live
Powered by Claude (via OpenRouter):

- **AI Move Estimator** — describe a move in plain English and Claude *streams its reasoning* while building a room-by-room inventory, total volume, crew/truck/hours and a price range. Try *"3-bed house with a piano and 40 boxes, second-floor flat, 25 km."*
- **Lead Intelligence** — AI scores every open lead by conversion likelihood and hands you the single best next action.
- **Instant AI quote + booking chatbot** on the public quote page.

> Look for the **✨ AI** tags in the sidebar and the "💡 how to use" hint on each AI screen.

## Tech
- **Backend:** FastAPI, async SQLAlchemy, PostgreSQL, APScheduler (automation sweeps)
- **Frontend:** React 18 + TypeScript + Vite (served same-origin by the API)
- **AI:** Claude (via OpenRouter) for the email parser and chatbot
- **Pluggable messaging adapters** (email / SMS / WhatsApp) that **degrade gracefully to console logging**, so the whole platform runs without any paid vendor keys.

## Architecture & deployment
Single same-origin service (FastAPI serves the built SPA), containerized with a multi-stage Docker build, deployed on **Railway** with managed PostgreSQL and **auto-deploy on every push**. On first boot it seeds a demo company with ~80 leads and 30+ jobs so the dashboard is populated immediately.

---

*Proof-of-concept built by [Muhammad Jehanzaib](https://github.com/mjehanzaib999) / Kognio AI. Source code is private — available on request.*
