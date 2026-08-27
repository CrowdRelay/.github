<p align="center">
  <img src="profile/crowdrelay-brand-mark.png" width="120" alt="CrowdRelay" />
</p>

<h1 align="center">CrowdRelay</h1>

<p align="center">
  <strong>A growth-operations platform for labels, artist rosters and festivals.</strong><br/>
  Deterministic business authority, durable state, and LLM-assisted creative execution — built to run a whole roster from one seat.
</p>

---

<p align="center">
  <a href="#ecosystem">Ecosystem</a> &bull;
  <a href="#what-it-does">What It Does</a> &bull;
  <a href="#ai-agents">AI Agents</a> &bull;
  <a href="#architecture">Architecture</a> &bull;
  <a href="#authority-model">Authority Model</a>
</p>

---

## Ecosystem

CrowdRelay is not a single repository — it's a multi-surface system where business state stays in one place and every client is a thin adapter.

| Repository | Stack | Role |
|-----------|-------|------|
| **crowdrelay** | Rust, Axum, SQLx, Postgres | Core backend — durable business state, autopilot engine, 21 evaluation contexts |
| **crowdrelay-control-plane** | Rust, Axum, SolidJS, Postgres | Operator plane — tenant provisioning, runtime health, deployment identity, audit |
| **crowdrelay-agents** | Node.js, TypeScript, Fastify | LLM agent service — press pitches, social posts, campaign analysis seeded with real data |
| **virya** | Astro, Preact, Tailwind, Stripe | Public website — tickets, merch, fan experiences, AREA game |
| **virya-signal** | Rust, Tauri 2, Leptos | Mobile client — fan wallet, staff operations, ticket scanning |
| **synesthesia** | Godot 4, Rust | Interactive album — playable companion to _Echoes Of The Modern Mind_ |

## What It Does

CrowdRelay owns the durable business state behind audience growth and live operations: fans and consent, events, tickets, admission, merch, referrals, venue relationships, community outreach, and every action taken around them.

**The Autopilot engine** evaluates twenty-one bounded contexts on every cycle — ticket yield, fan lifecycle, campaign phases, merchandising, booking opportunities, outreach pipelines, promotion budgets, show operations, release milestones, live opportunities, funding, and more. Each context passes through a shared funnel: confidence gate &rarr; authority level &rarr; class ceiling &rarr; envelope budget &rarr; deliverability halt. The stricter limit always wins.

**The portfolio layer** lets a roster's audiences amplify each other through explicit, revokable, capped consent edges — a capability that only exists when one platform holds every artist's fan graph. Each artist is a workspace inside a label organization; onboarding another act is workspace provisioning, not a fork.

**Server-side ad conversion** tracks Meta CAPI, Google Ads, and Bandsintown conversions reactively via Postgres LISTEN/NOTIFY — zero polling, immediate delivery, idempotent writes.

## AI Agents

The `crowdrelay-agents` service brings LLM-powered creative work into the same platform that holds the business data:

- **6 LLM providers**: OpenCode Zen (free), OpenAI, Anthropic (Claude), Google Gemini, Groq, OpenRouter
- **Data-seeded prompts**: every task pulls live data from the CrowdRelay database — real event dates, real fan counts, real outreach targets — so the LLM writes about the actual situation, not a template
- **Templates**: press pitches, social posts, campaign analysis with more planned
- **Per-tenant credentials**: each workspace connects its own providers; API keys are AES-256-GCM encrypted at rest and never sent back to the frontend
- **Model fallback chain**: if the requested model fails, the runner cascades to free-tier models, then other connected providers
- **Task suggestions**: the engine analyzes tenant data and proactively suggests actionable next steps — "your event is in 9 days with 1 interested fan, write a press pitch" — with one-click execution

The control plane proxies these requests transparently. If the agent service isn't configured, tenant traffic is unaffected.

## Architecture

```
                    ┌─────────────────────────────────────────┐
                    │              CrowdRelay Core              │
                    │         (Rust / Axum / Postgres)          │
                    │                                          │
                    │  Autopilot (21 contexts)    Fan Graph    │
                    │  Outbox / Delivery          Consents      │
                    │  Ticketing / Merch           Referrals    │
                    │  Ad Conversion (LISTEN)      Draws         │
                    └──────────┬──────────┬──────────┬─────────┘
                               │          │          │
                    ┌──────────┴───┐  ┌──┴──────┐  ┌┴────────────┐
                    │  Control     │  │ Agents  │  │   Clients   │
                    │  Plane       │  │ (LLM)   │  │             │
                    │              │  │         │  │ virya.music │
                    │ Provisioning │  │ Press   │  │ Signal      │
                    │ Runtime Hlth │  │ Social  │  │ Synesthesia │
                    │ Audit        │  │ Analyze │  │             │
                    └──────────────┘  └─────────┘  └─────────────┘
```

The core idea: **business state and business decisions stay in CrowdRelay; external services only execute the work they're asked to do.** Email, n8n, Stripe, Calendar, Bandsintown and LLM-assisted copy are adapters, not sources of truth.

## Authority Model

| Posture | What the engine does | What it never does |
|--------|---------------------|-------------------|
| `grounded` | Observes and rehearses everything (dry run) | Touch anyone |
| `working` | First-party work runs alone; outward contact drafts for approval | Send to fans or curators unattended |
| `full_send` | Owned audience sends within limits; free pitching runs unattended | Spend money, sign contracts |

Money and contracts stay behind approval in every posture.

---

<p align="center">
  Built with Rust, Postgres, and a stubborn refusal to let AI make business decisions.
</p>
