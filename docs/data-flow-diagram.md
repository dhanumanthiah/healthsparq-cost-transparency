# Data Flow Diagram — HealthSparq Cost Transparency Integration

## Cost Estimate Request Flow

```mermaid
flowchart TD
    A[Member\nWeb or Mobile] -->|Searches procedure, drug, or provider| B[HealthSparq Platform]

    B --> C[Healthrules API\nClaims]
    B --> D[Eligibility & Benefits API]
    B --> E[HealthSparq Cost Database]

    C -->|Deductible balance\nAccumulator totals\nOOP max progress| F[Cost Calculation Engine]
    D -->|Co-pay / Co-insurance\nBenefit limits\nPlan tier| F
    E -->|Procedure & provider\npricing benchmarks| F

    F -->|Personalized estimate| G[Member sees:\nEstimated OOP cost\nRemaining deductible applied\nProvider cost comparison]
```

---

## Channel Architecture

```mermaid
flowchart LR
    A[Web Browser] --> C[HealthSparq Platform]
    B[Mobile App] --> C

    C --> D[Healthrules API\nClaims & Accumulators]
    C --> E[Eligibility & Benefits API]
    C --> F[HealthSparq Cost Database\nPricing Benchmarks]
```

> Single integration layer shared across web and mobile — no duplicate API connections.

---

## What Makes the Estimate Personalized

```mermaid
flowchart TD
    subgraph Generic["❌ Generic Estimate — Without Healthrules"]
        A1[Member searches MRI - knee] --> B1[Returns market average price]
        B1 --> C1[No deductible applied\nNo plan benefits applied]
        C1 --> D1[Member has no idea\nwhat they will actually owe]
    end

    subgraph Personalized["✅ Personalized Estimate — With Healthrules API"]
        A2[Member searches MRI - knee] --> B2[Healthrules API\n$800 remaining deductible]
        A2 --> C2[Eligibility API\n80/20 co-insurance after deductible]
        A2 --> D2[HealthSparq Cost DB\nProcedure ~$1,200 in-network]
        B2 & C2 & D2 --> E2[Member pays $800 deductible\n+ 20% of remaining $400 = $80]
        E2 --> F2[Estimated member OOP: $880\nBefore scheduling]
    end
```

---

## Data Sources Summary

| Source | System | Data Provided |
|---|---|---|
| Claims & Accumulators | Healthrules API | Deductible balance, OOP max progress, accumulator totals |
| Benefits & Eligibility | Eligibility API | Co-pay, co-insurance, benefit limits, plan tier |
| Procedure / Provider Pricing | HealthSparq Cost Database | Market-area pricing benchmarks for procedures, drugs, providers |

---

*Diagram sanitized — internal system names, vendor identifiers, and member data removed.*
