<p align="center">
  <img src="crowdrelay-brand-mark.png" width="120" alt="CrowdRelay" />
</p>

<h1 align="center">CrowdRelay</h1>

<p align="center">
  <strong>The growth-operations platform for labels, artist rosters, and festivals.</strong>
</p>

<p align="center">
  Aggregate fans from everywhere. Grow them for real. Convert them into ticket buyers, merch customers, and lifelong supporters.
</p>

---

**We are building software that can actually run operations.**

CrowdRelay started with a simple question:

> What happens when AI stops being a copilot and starts being responsible for getting things done?

We are building toward an operating system where software can:

observe  
→ decide  
→ act  
→ measure  
→ learn  
→ act again

The first domain is music.

The goal is not another dashboard, assistant, or workflow builder.

The goal is an autonomous operating layer that can run real audience growth and operational work while staying inside explicit authority, budgets, and safety limits.

## The idea

AI is good at producing things.

The harder problem is deciding:

- what should happen
- whether it should happen now
- what the system is allowed to do
- whether it actually worked
- what to do differently next time

CrowdRelay is built around that loop.

## Projects

| Project | What it is |
|---|---|
| [crowdrelay](https://github.com/CrowdRelay/crowdrelay) | Core business state, decision engine, execution and learning |
| [crowdrelay-agents](https://github.com/CrowdRelay/crowdrelay-agents) | Model-powered workers for creative and language tasks |
| [crowdrelay-control-plane](https://github.com/CrowdRelay/crowdrelay-control-plane) | Operator and control plane |
| [virya](https://github.com/CrowdRelay/virya) | Public artist platform |
| [virya-signal](https://github.com/CrowdRelay/virya-signal) | Mobile fan and staff client |
| [synesthesia](https://github.com/CrowdRelay/synesthesia) | Interactive music project |

## North star

**Get fans.**

Everything else exists to improve the system's ability to do that reliably.

better decisions  
→ better actions  
→ better outcomes  
→ better decisions

## Ecosystem

| Repository | Role |
|-----------|------|
| [**crowdrelay**](https://github.com/CrowdRelay/crowdrelay) | Core platform — durable business state, Autopilot engine, fan graph, ticketing, merch, outreach, delivery |
| [**crowdrelay-control-plane**](https://github.com/CrowdRelay/crowdrelay-control-plane) | Operator plane — tenant provisioning, runtime health, deployment identity, audit, agent management |
| [**crowdrelay-agents**](https://github.com/CrowdRelay/crowdrelay-agents) | LLM worker service — press pitches, social posts, campaign analysis, Reddit scanning, seeded with live tenant data |
| [**virya**](https://github.com/CrowdRelay/virya) | Public website — tickets, merch, fan experiences, AREA game, staff panel |
| [**virya-signal**](https://github.com/CrowdRelay/virya-signal) | Mobile client — fan wallet, ticket scanning, staff operations |
| [**synesthesia**](https://github.com/CrowdRelay/synesthesia) | Interactive album — playable companion to *Echoes Of The Modern Mind* |

## How it works

The brain is deterministic. It finds opportunities, makes decisions, executes work, survives failures, and knows when it's not allowed to act. LLM-assisted creative work (press pitches, social posts, campaign analysis) is layered on top — the LLMs produce drafts seeded with real tenant data, the brain decides what to do with them. No LLM makes a business decision. Ever.

External services — email, payment, calendar, ad platforms, workflow automation — are adapters, not sources of truth. A successful API call proves request handling, not delivery. The transactional outbox owns durability, retries, and dead-state inspection.

## Authority model

One dial applies all context levels, class ceilings, and envelope switches atomically. Budgets are operator-tuned and survive posture flips.

| Posture | What the engine does | What it never does |
|---|---|---|
| **Grounded** | Observes and rehearses everything (dry run) | Touch anyone |
| **Working** | First-party work runs; outward contact drafts for approval | Send to fans or curators unattended |
| **Full send** | Owned audience sends within limits; free pitching runs unattended | Spend money, sign contracts |

Money and contracts stay behind approval in every posture.

## Safety

- Sending volume earns its ceiling from zero; bounce or complaint rates close it before damage
- Every action carries an idempotency key; retries are bounded and auditable
- Circuit breakers open on executor failure storms
- Kill switch stops all outbound work without touching data
- Blue-green deploys with zero-downtime cutover and automatic rollback
- HMAC-signed webhooks with replay protection
- No unsafe code in the runtime; panics forbidden at compile time

## Label portfolio mode

One organization, many artist workspaces, one operator view. Consent edges between artists let a roster's audiences amplify each other — cross-promote, release features, event cross-billing — with monthly caps, per-fan cooldowns, and revocable edges with an approval paper trail. Identities never leave home; reach numbers do.

---

<p align="center">
  Built with Rust, Postgres, and a stubborn refusal to let AI make business decisions.
</p>
