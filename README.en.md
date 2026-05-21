# ZWISERFIT — Proof of Physical Behavior Protocol

> The missing physical verification layer for Web5 and DePIN.

Proof of Physical Behavior (**PoPB**) is a protocol that verifies human physical activity on-chain — not through self-reporting or wearables, but through unforgeable physical access points (turnstiles, gates, doors) that have been running in production for 7 years.

## What is PoPB?

| If you know... | PoPB is like... | But for... |
|:---|:---|:---|
| Helium / PoPW | Verifying *where devices are* | Verifying *what humans DO* |
| Hivemapper | Verifying map data | Verifying physical activity |
| GEODNET | Verifying location | Verifying behavior |

PoPB fills the missing row in Multicoin Capital's [Internet Labor Markets (March 2026)](https://multicoin.capital/) framework: **verifiable physical human behavior.**

## How it works

```
Human walks through a door
    → 15-sensor turnstile captures raw signal
    → 9 AI Agents validate (anti-sybil, anti-spoof)
    → DID-encrypted proof → on-chain
    → Available as a composable primitive for builders
```

- **Data source:** 1 physical node in Dongguan, China | 7 years production | 118+ members
- **Capture rate:** 100% | **Spoofing rate:** 0%
- **Verification:** 9 AI Agent team (Stella audit, Ethan trust, Momo bridge)
- **Chain of custody:** SHA-256 hashed → Federated ledger TX → Publicly verifiable

## What can I build on PoPB?

| Application | Example | Data primitives needed |
|:---|:---|:---|
| Insurance pricing engine | "Verified 18x/month gym attendance → 20% premium discount" | Entry timestamps, frequency, consistency |
| Personal health data exchange | "I own my gym data, I license it to researchers" | DID-bound behavioral dataset |
| Fitness incentive dApp | "Complete 30 sessions → claim NFT badge → tradeable" | Session count verification |
| Body credit score | "Physical activity record as credit underwriting signal" | Longitudinal behavioral consistency |

## Quick links

| Link | What you'll find |
|:---|:---|
| ⚡ [Protocol Spec](docs/protocol/) | PoPB technical specification |
| 💬 [Builders Q&A](https://github.com/ZWISERFIT/ZWISERFIT/discussions/categories/builders-q-a) | Ask questions, get answers |
| 🏗️ [Builder Application](https://github.com/ZWISERFIT/ZWISERFIT/issues/new?labels=builder-application&template=builder-application.yml) | Apply for beta access |
| 🔐 [Independent Verification](https://github.com/ZWISERFIT/ZWISERFIT/blob/main/assets/verify.html) | Verify data integrity yourself |
| 🤖 [AI Store Manager Repo](https://github.com/ZWISERFIT/zwiserfit-ai-store-manager) | The 9-Agent runtime in production |
| ⭐ [Star the repo](https://github.com/ZWISERFIT/ZWISERFIT) — it helps builders find us |

## Status

> **Stage:** Public protocol spec (MVP phase) | 1 node in production | 9 AI Agents running 24/7
> **License:** Apache 2.0

### Working today
- ✅ Physical turnstile → AI Agent pipeline (production, 7 years)
- ✅ Anti-sybil verification (15 sensors, zero spoofing)
- ✅ SHA-256 data integrity + Federated ledger timestamp
- ✅ 9-Agent autonomous operations (Shuyu → Tristan → Momo execution)
- ✅ Independent audit agent (Stella) per Constitution Article IV

### Opening
- 🔄 PoPB protocol spec documentation
- 🔄 Builder beta access program
- 🔄 External developer API

## The 7-year story (short version)

In 2019, a single gym in Dongguan, China installed a facial-recognition turnstile — not as a blockchain oracle, but as a practical solution to manage membership access. 7 years later, that turnstile has captured 118+ members' physical behavior data at 100% fidelity, zero spoofing, across hundreds of thousands of sessions.

The operator realized: this is not a gym system. It's a physical behavior verification protocol that accidentally ran 7 years of proof.

In April 2026, the 9-AI-Agent architecture was deployed. In May 2026, the first independent audit (Stella → Tristan, [Issue #19](https://github.com/ZWISERFIT/zwiserfit-ai-store-manager/issues/19)) proved the multi-agent governance works in production.

Today, we're opening the protocol for builders.

## Community

- 💬 [Discussions](https://github.com/ZWISERFIT/ZWISERFIT/discussions) — Q&A, ideas, governance
- 🏗️ [Builders Q&A](https://github.com/ZWISERFIT/ZWISERFIT/discussions/categories/builders-q-a) — technical questions
- 📊 [Data & Protocol](https://github.com/ZWISERFIT/ZWISERFIT/discussions/categories/data-protocol) — data spec discussion
- 🌐 [中文版](README.md) — Chinese language main page

---

> 📄 Apache 2.0 | Built at a gym in Dongguan with 9 AI Agents and one stubborn founder.
