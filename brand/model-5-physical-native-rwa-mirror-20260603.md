# Model 5: Physical-Native RWA

## Completing Multicoin Capital's Four-Year Thesis Arc

> *Written by ZWISERFIT · June 3, 2026*
> *License: CC BY 4.0 — free to share, free to build on*

---

In April 2022, Multicoin Capital published a thesis called **Proof of Physical Work**. The core claim: tokens create opportunities for capital formation that extend beyond the digital world and into the physical. Not just digital assets, not just financial assets — physical human work as crypto's next raw material.

Two months ago, in March 2026, they published two more pieces within nine days: **Internet Labor Markets** (March 10) and **RWAs Are Just Built Different** (March 19). The RWA paper defined four models for bringing real-world assets on-chain.

Four years. Three papers. A clear trajectory: Multicoin has been building a framework for the physical world to enter crypto.

But the RWA taxonomy has a blind spot. Not a mistake — a gap left by an assumption that was invisible until you try to apply it to a specific class of assets. This article names that gap and fills it.

---

## The Arc

```
2022.04   Proof of Physical Work
          → "Tokens extend capital formation into the physical world"

2026.03.10 Internet Labor Markets
          → "Two ways to onboard to crypto: you buy in or you earn in"
          → Physical work = verifiable tasks on crypto rails

2026.03.19 RWAs Are Just Built Different
          → Four models: Synthetic Derivatives → Wrapped Custody →
            Collateralized Borrowing → Primary Onchain Issuance
          → "Model 4 is the purest version of crypto-native RWAs"
  │
  │   What's missing?
  ▼
2026.06.02 Model 5: Physical-Native RWA
          → The asset class at the intersection of all three papers:
            physical human behavior as a native on-chain asset
```

Three papers, converging on the same question: **how does the physical world prove itself to the digital world?**

The first paper posed the question. The second operationalized it. The third categorized it — but stopped at financial assets.

---

## The Hidden Assumption

Multicoin's four RWA models share a premise that makes sense for financial assets but fails for the physical:

> *"The asset exists independently of the proof that attests to it."*

A stock exists before you tokenize it (*Model 1: Synthetic*). A treasury bill exists before you wrap it (*Model 2: Custody*). Real estate exists before you borrow against it (*Model 3: Collateral*). A security exists before you issue it on-chain (*Model 4: Primary*). In every case, there's an off-chain asset waiting to be represented.

Human physical behavior does not satisfy this premise.

A person doing 100 squats at 08:00 UTC is not an "asset" waiting to be tokenized. The behavior **is** the value-generating event. The proof **is** the asset. There is no "underlying" to cache, no custodian to hold, no price oracle to report.

This is not a failure of Multicoin's framework. It's a limitation of the **asset ontology** the framework was designed to handle. Multicoin's four models handle *stored* value. Physical behavior is *generated* value — and generation requires a different ontology.

---

## Model 5: Physical-Native RWA

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   MODEL 5: Physical-Native RWA                                  │
│                                                                 │
│   Definition: An on-chain asset whose existence is co-incident  │
│   with its cryptographic proof.                                 │
│                                                                 │
│   Key Properties:                                               │
│   • Proof ≡ Asset                                               │
│   • Hardware Trust Root (not custodian trust)                   │
│   • No Tokenization Step                                        │
│   • No Price Oracle                                             │
│   • Privacy-Preserving by Architecture                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Why Model 5 fits none of the four

| Model | Why It Fails for Physical Behavior |
|-------|-------------------------------------|
| **1: Synthetic Derivatives** | ❌ No price oracle for "100 squats verified by hardware at 08:00 UTC" |
| **2: Wrapped Custody** | ❌ No custodian needed — the hardware trust root IS the custodian |
| **3: Collateralized Borrowing** | ❌ Behavior data is a primary asset, not a secondary claim |
| **4: Primary Onchain Issuance** | ❌ Closest — but behavior is not "issued," it's *generated*. The gym goer is not an issuer |

### Why Model 5 is more native than Model 4

Multicoin describes Model 4 as "the purest version of crypto-native RWAs." Model 5 is purer — because the asset never exists off-chain:

| Dimension | Model 4 | Model 5 |
|-----------|---------|---------|
| **Asset Ontology** | Asset exists before proof | Asset ≡ Proof |
| **Issuer** | Legal entity | Physics + Hardware |
| **Gap** | Issuance → Registration | Generation = Attestation |
| **Regulatory** | SEC jurisdiction | Outside securities law |
| **Trust Model** | Legal enforceability | Cryptographic verifiability |

An asset that is born on-chain because it is born in the physical world, proven by hardware — that is the most native version of a real-world asset on-chain. No issuer. No custodian. No gap.

---

## The Implementation: PoPB Protocol

Model 5 is not theoretical. The protocol that implements it is open-source and running.

**Proof of Physical Behavior (PoPB)** is a five-layer protocol:

```
Layer 5: APPLICATION  — DID · Insurance · Behavior Exchange
Layer 4: VERIFICATION — Validator Network · Consensus · Slashing
Layer 3: PRIVACY      — MPC Sharding · ZK-Proofs · DID Sovereignty
Layer 2: DATA CAPTURE — 15-Dim Sensor Fusion · Signal Processing
Layer 1: HARDWARE TRUST ROOT — Secure Element · TEE · Device Attestation
```

The critical layer is L1. Every behavior proof must contain a cryptographic attestation signed by a hardware secure element whose private key was sealed at the factory. A pure-software implementation of PoPB can produce syntactically valid JSON. It **cannot** produce a valid attestation. This is not a policy boundary. It is a mathematical boundary.

The protocol specification is fully open (MIT/Apache 2.0). Anyone can verify, anyone can build applications on top. What they cannot do without physically deployed hardware: generate a valid proof.

This is the same asymmetry that makes TCP/IP work. The standard is open, but producing valid data on the network requires physical infrastructure. Open protocol. Closed loop on physical proof.

The hardware? It's been running in a 300-square-meter gym in Dongguan, China — the market with the lowest fitness penetration rate in the country, proving the lower bound of the model's viability. That's not a pitch. It's a field report.

---

## What This Means for Multicoin's Thesis

Multicoin has traced a four-year arc from "Proof of Physical Work" to "Internet Labor Markets" to "RWA taxonomy." Each paper moves closer to a unified thesis: **physical human activity will be crypto's most important asset class.**

Model 5 is the missing piece. It completes the arc:

- **Proof of Physical Work (2022):** The conceptual foundation — physical work as crypto's raw material ✓
- **Internet Labor Markets (2026):** The operational mechanism — verifiable tasks on crypto rails ✓
- **RWAs Are Just Built Different (2026):** The taxonomy — four models for financial assets ✓
- **Model 5: Physical-Native RWA (2026):** The fifth model — physical human behavior as native on-chain asset ✓ (← here)

The paper that connects all three has been waiting to be written. We wrote it.

---

## What This Means for Anyone Reading on Mirror

If you're building in DePIN, RWA, proof-of-personhood, or any protocol that touches the boundary between digital and physical — **this gap in the taxonomy is yours to exploit.**

The Multicoin framework is now complete: five models. The fifth is the most native of all. The protocol is open. The hardware is deployed. The proof-of-concept verifier runs on your laptop in three commands.

[github.com/ZWISERFIT/PoPB](https://github.com/ZWISERFIT/PoPB)

---

*This article is part of an open academic response to Multicoin Capital's RWA framework. It is not financial advice. It is not a solicitation. It is a protocol response, written in public, licensed under CC BY 4.0.*

*ZWISERFIT · Dongguan · 2026*
