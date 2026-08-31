# CrowdRelay

**The growth-operations platform for labels, artist rosters, and festivals.**

CrowdRelay connects audience data, decision-making, execution, measurement, and learning into one operational loop:

**observe → decide → act → measure → learn**

The first domain is music.

## What it is

CrowdRelay is not a dashboard, copilot, or workflow builder.

It is a system designed to run real growth and operational work under explicit authority, budgets, approvals, and safety constraints.

The core problem is not generating content. It is reliably answering:

- what should happen
- whether it should happen now
- what the system is allowed to do
- what actually happened
- what evidence supports the outcome
- what should change next time

## Core model

```text
observe
   ↓
decide
   ↓
execute
   ↓
measure
   ↓
learn
   ↓
decide again
```

Execution and evidence are first-class parts of the platform.

External APIs are treated as adapters, not sources of truth. A successful API request is not automatically treated as proof that the intended external effect happened.

CrowdRelay preserves ambiguous outcomes, supports reconciliation, and keeps execution traceable across the system.

## The Brain

`crowdrelay-brain` contains the decision-intelligence domain.

It is responsible for areas such as:

- opportunity evaluation
- decision value
- experimentation
- evidence
- causal learning
- optimization
- exploration

LLMs can generate drafts, analyses, and other bounded outputs.

**LLMs do not make business decisions.**

The Brain operates on persisted system data and explicit operational constraints.

## Control and authority

CrowdRelay separates decision authority from execution.

Operators control posture, budgets, limits, and approval requirements.

| Posture | Behaviour |
|---|---|
| **Grounded** | Observe and rehearse; no outward action |
| **Working** | Run approved first-party work; external outreach requires approval |
| **Full send** | Execute owned-audience actions within configured limits |

Money and contracts remain approval-gated.

## Execution integrity

Every meaningful action is traceable through shared execution identity:

```text
trace_id
action_id
decision_id
causation_id
tenant_id
```

This allows the system to connect:

```text
decision
→ action
→ execution
→ provider outcome
→ measurement
→ learning
```

The execution model distinguishes external observations from CrowdRelay's current internal state.

When an external result is ambiguous, the action can become **UNKNOWN** rather than being incorrectly marked as failed or successful. Reconciliation can resolve that state when stronger evidence becomes available.

## Evidence and learning

CrowdRelay is designed to avoid fabricating certainty.

Missing data stays missing.

Ambiguous execution stays ambiguous.

Corrupt state is surfaced rather than silently replaced with defaults.

Evidence is kept separate from causal interpretation, and experiment/learning code operates on explicit execution and treatment semantics.

## Growth operations

The current platform includes capabilities around:

- fan and audience data
- growth metrics
- social and platform connections
- outreach
- experimentation
- ticketing
- merch
- operational automation
- measurement and learning

The platform is currently being extended toward broader community intelligence: understanding where relevant audiences and conversations exist, what they care about, and which opportunities are worth testing.

## Architecture

| Repository | Role |
|---|---|
| [**crowdrelay**](https://github.com/CrowdRelay/crowdrelay) | Core platform — business state, decisions, execution, evidence, learning, fan graph, ticketing, merch and outreach |
| [**crowdrelay-agents**](https://github.com/CrowdRelay/crowdrelay-agents) | Model-powered workers for bounded creative and language tasks |
| [**crowdrelay-control-plane**](https://github.com/CrowdRelay/crowdrelay-control-plane) | Operator and control plane |
| [**virya**](https://github.com/CrowdRelay/virya) | Public artist platform |
| [**virya-signal**](https://github.com/CrowdRelay/virya-signal) | Mobile fan and staff client |
| [**synesthesia**](https://github.com/CrowdRelay/synesthesia) | Interactive music project |

## Safety

CrowdRelay is built around failure rather than assuming success.

Key properties include:

- bounded, idempotent execution
- explicit handling of ambiguous outcomes
- reconciliation paths
- circuit breakers
- kill-switch support
- authenticated, replay-protected webhooks
- controlled deployments and rollback
- tenant-scoped data and operations
- no business decisions delegated to LLMs

## North star

**Get fans.**

The objective is not to generate more activity.

It is to build a system that gets better at deciding **what is worth doing, what it is allowed to do, what actually worked, and what to do next.**

---

Built with Rust, Postgres, and a stubborn refusal to let AI make business decisions.
