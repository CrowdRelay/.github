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

## What it is

CrowdRelay is a platform that runs the entire fan-growth operation for a music label or artist roster from one seat. It owns the durable business state — fans and consent, events, tickets, merch, referrals, outreach, community engagement — and makes deterministic decisions about what to do next, within explicit authority limits.

The first tenant running it in production is [Virya](https://virya.music). Onboarding another act or festival is workspace provisioning, not a fork.

## What it does

**Aggregate.** Fans come from every side of the internet — Reddit, Meta, Spotify, Bandsintown, press, live shows, community forums — into a single fan graph with consent, lifecycle stage, and engagement history.

**Grow.** A deterministic engine (the Autopilot) evaluates twenty-plus growth contexts on every cycle: ticket yield, merchandising, booking opportunities, outreach to curators and press, content supply, promotion budget, show operations, community engagement, and more. Each action passes through confidence gates, authority levels, budget ceilings, and deliverability halts before anything is sent.

**Convert.** The platform closes the loop: tickets, merch, attendance, and referrals — all tracked, measured, and fed back into the next decision cycle. Attribution is honest: smart-link clicks are causal; follower movement after a campaign is correlational, always labelled as such.

## What it solves

Music teams juggle a dozen tools that don't talk to each other: a spreadsheet for fans, an email platform for campaigns, a separate tool for ads, a Slack thread for outreach tracking, and no unified view of who a fan is or what they've done. Decisions are reactive, measurement is anecdotal, and growth is a side effect of busywork.

CrowdRelay replaces that with one system that holds the fan graph, makes decisions, executes work through external services, measures what happened, and learns from it. The operator sets the posture and the budget; the platform does the rest within those limits.

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
