# ABSEv1

**AUTONOMOUS BLUEPRINT SYNTHESIS ENGINE** — an architecture-agnostic, agent-agnostic skill that applies the AESE methodology (Design Thinking, 5W2H, Lean Validation, Stage-Gated Pipeline) to **any infrastructure** the user specifies.

The skill is a self-contained system prompt in [`ABSEv1/SKILL.md`](ABSEv1/SKILL.md). It can be loaded by any agent via the [`skills`](https://github.com/vercel-labs/skills) CLI (`npx skills`) — or applied directly as agent instructions.

---

## What it does

`ABSEv1` extracts the AESEv2 methodology and makes it infrastructure-agnostic:

1. **WHAT + Infrastructure Declaration** — User specifies the product concept **and** target infrastructure (provider, services, tier/plan) in a single sentence.
2. **Verification Gate** — Before `INIT`, the engine confirms infrastructure and tier are explicitly declared; otherwise it requests them.
3. **5W2H + Tier-Bound Matrix** — Strategic visioning where "How Much" is constrained by user-declared tier limits.
4. **Infrastructure-Adaptive Architecture** — Stage-400 maps the WHAT to the declared services (serverless, containers, VMs, bare-metal, etc.) with appropriate IaC.
5. **Lean Tier Simulation** — Stage-600 stress-tests against declared quotas; pivots or burns out if unresolvable.
6. **Full Blueprint Delivery** — Stage-700 outputs code, config, IaC, schemas, CI/CD, and deploy commands for the declared platform.

**Safety** — Hard terminal codes: `STAGE-999: SUCCESS_DELIVERY` or `BURNOUT-000: TIER_CONSTRAINT_VIOLATION`. No partial output.

---

## Requirements

- An agent that can load a system prompt (or the `skills` CLI).
- User must declare infrastructure + tier in the `WHAT` sentence (provider, compute, data, tier).
- Optional: Access to declared provider's CLI/API for validation (not required for blueprint generation).

---

## Installation

### One-shot (no install)

```bash
npx skills use agentic-framework-skills/ABSEv1
```

### Add to a project or agent

```bash
# Project-level
npx skills add agentic-framework-skills/ABSEv1
# Global / across agents
npx skills add agentic-framework-skills/ABSEv1 -g --all
```

### Or load directly

Apply [`ABSEv1/SKILL.md`](ABSEv1/SKILL.md) as the system prompt for your agent.

---

## Usage

```
WHAT <product concept> on <provider> <services> <tier>
    # e.g., "A real-time chat app on Cloudflare Workers free tier with Durable Objects"
    # e.g., "An e-commerce API on AWS Lambda + DynamoDB free tier in us-east-1"
    # e.g., "A static site on Vercel Hobby plan with Edge Functions"

INIT
    # Triggers autonomous synthesis across all stages
```

The engine runs the full stage pipeline: `STAGE-100` → `STAGE-200` → `STAGE-300` → `STAGE-400` → `STAGE-500` → `STAGE-600` → `STAGE-700` → `STAGE-999` or `BURNOUT-000`.

---

## Key parameters

| Parameter | Source | Role |
|---|---|---|
| Infrastructure Provider | User `WHAT` | Target platform (Cloudflare, AWS, GCP, Azure, Vercel, Kubernetes, bare-metal, etc.) |
| Compute Service | User `WHAT` | Primary compute (Workers, Lambda, Cloud Run, GKE, VMs, etc.) |
| Data Service | User `WHAT` | Primary storage (D1, DynamoDB, Cloud SQL, PostgreSQL, etc.) |
| Tier / Plan | User `WHAT` | Quota/cost boundary (Free Tier, Hobby, Pro, custom limits) |
| Lean Pivot Limit | Fixed (3) | Max architecture pivots in STAGE-600 before BURNOUT |

---

## Example `WHAT` declarations

```
WHAT A real-time collaborative whiteboard on Cloudflare Workers free tier with Durable Objects and R2
WHAT A serverless GraphQL API on AWS Lambda + AppSync free tier with DynamoDB in us-east-1
WHAT A static marketing site with forms on Vercel Hobby plan using Edge Functions
WHAT A containerized ML inference service on self-hosted Kubernetes v1.28 on Hetzner CX41 (8 vCPU, 16GB RAM)
WHAT An event-driven order processing system on Azure Container Apps Consumption plan with Cosmos DB free tier
```

---

## Author

Developed by **Jean Machuca** — [GitHub @jeanmachuca](https://github.com/jeanmachuca) ·
[Sponsor on GitHub Sponsors](https://github.com/sponsors/jeanmachuca).

---

## License

Distributed under the **MIT License**.