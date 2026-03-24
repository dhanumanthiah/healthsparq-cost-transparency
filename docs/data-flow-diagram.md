# Data Flow Diagram — HealthSparq Cost Transparency Integration

## Overview

The HealthSparq cost transparency tool sits between the member and three backend data sources. The key differentiator: cost estimates are personalized using the member's *actual* claims and accumulator data pulled from Healthrules in real time — not population averages.

---

## Cost Estimate Request Flow

```
Member (Web or Mobile)
        │
        │  Selects procedure, drug, or provider
        ▼
  HealthSparq Platform
        │
        ├── 1. Healthrules API (Claims)
        │         └── Pulls member's current deductible balance,
        │               accumulator totals, and OOP maximum progress
        │
        ├── 2. Eligibility & Benefits API
        │         └── Pulls member's plan-specific benefit structure
        │               (co-pay, co-insurance, benefit limits, tier)
        │
        └── 3. HealthSparq Cost Database
                  └── Pulls procedure/drug/provider pricing benchmarks
                        localized to member's market area
        │
        ▼
  Personalized Cost Estimate
        │
        └── Displayed to member with:
              - Estimated cost before insurance
              - Member's estimated out-of-pocket cost
              - Remaining deductible applied
              - Provider cost comparison (where applicable)
```

---

## What Makes the Estimate Personalized

```
Generic Estimate (without Healthrules integration)
─────────────────────────────────────────────────
Member searches "MRI - knee"
  └── Returns: average cost for this procedure in your area
  └── No deductible applied. No plan benefits applied.
  └── Result: member has no idea what they will actually owe.


Personalized Estimate (with Healthrules API)
─────────────────────────────────────────────────
Member searches "MRI - knee"
  └── Healthrules API returns: member has $800 remaining deductible
  └── Eligibility API returns: 80/20 co-insurance after deductible
  └── HealthSparq Cost DB returns: procedure costs ~$1,200 in-network
  └── Calculation:
        Member pays $800 (remaining deductible)
        + 20% of remaining $400 = $80
        = Estimated member OOP: $880
  └── Result: member sees their actual estimated cost before scheduling.
```

---

## Data Sources Summary

| Source | System | Data Provided |
|---|---|---|
| Claims & Accumulators | Healthrules API | Deductible balance, OOP max progress, accumulator totals |
| Benefits & Eligibility | Eligibility API | Co-pay, co-insurance, benefit limits, plan tier |
| Procedure/Provider Pricing | HealthSparq Cost Database | Market-area pricing benchmarks for procedures, drugs, providers |

---

## Channel Architecture

```
Web Browser ──────┐
                  ├──► HealthSparq Platform ──► Backend Data Sources
Mobile App ───────┘         (single integration layer — no duplication)
```

Both web and mobile channels connect through the same HealthSparq integration layer. The claims and eligibility API connections are built once and shared across channels — no separate mobile integration required.

---

*Diagram sanitized — internal system names, vendor identifiers, and member data removed.*
