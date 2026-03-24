# 💰 Cost Transparency: HealthSparq Integration
### CMS Price Transparency Compliance + Claims-Powered Cost Estimation for Medicare, Medicaid & Commercial Members

---

## Overview

This project documents the product ownership of a member-facing cost transparency initiative at a nonprofit health plan in Minnesota, delivered in response to the CMS Price Transparency Rule. The solution integrated HealthSparq — a third-party cost estimation platform — with the health plan's real-time claims data and eligibility systems, surfacing personalized cost estimates to members across web and mobile.

**Role:** Senior Business Analyst / Product Owner (led scope, vendor, and data integration)
**Regulatory Driver:** CMS Price Transparency Rule
**Channel:** Web + Mobile
**Population Served:** Medicare Advantage, Medicaid, Commercial members

---

## Problem Statement

The CMS Price Transparency Rule mandated that health plans provide members with the ability to estimate their out-of-pocket costs for covered services before receiving care. Beyond compliance, members — particularly those managing chronic conditions or facing high-cost procedures — had no reliable way to compare provider costs or understand how their deductible and benefits would affect what they owed.

**Core challenges:**
- No existing member-facing cost estimation capability
- Claims and eligibility data lived in disparate systems with no unified query layer for cost calculation
- Estimates had to reflect a member's *actual* plan, deductible status, and accumulator balances — not generic averages
- CMS compliance required specific data standards and member disclosure requirements
- Solution had to work across both web and mobile without duplicating the data integration layer

---

## Solution

A HealthSparq-powered cost transparency tool embedded across web and mobile member channels, personalized using real-time claims data and eligibility APIs, and compliant with CMS price transparency requirements.

### Features Delivered

| Feature | Description |
|---|---|
| **Procedure Cost Estimates** | Member-specific cost estimates for common procedures based on in-network provider pricing and plan benefits |
| **Drug / Pharmacy Cost Estimates** | Formulary-aware drug cost lookup, reflecting tier placement and pharmacy benefit structure |
| **Provider Cost Comparison** | Side-by-side cost comparison across in-network providers for the same service |
| **Out-of-Pocket Calculator** | Personalized OOP cost projection incorporating deductible, co-insurance, and benefit limits |
| **Deductible / Accumulator Display** | Real-time deductible and accumulator balances pulled from claims data to ensure estimate accuracy |

---

## My Role

As Product Owner and Senior Business Analyst, I owned the scope definition, vendor management, and data integration strategy for this initiative.

**What I did:**
- Defined product requirements and feature scope aligned to CMS Price Transparency Rule mandates
- Managed the HealthSparq vendor relationship — including contract requirements, integration specifications, and delivery milestones
- Led the integration of real-time claims data into the cost estimator, ensuring member-specific accuracy rather than generic population-level estimates
- Drove stakeholder alignment across legal, compliance, IT, and member experience teams
- Ensured CMS disclosure requirements were embedded in the member-facing UI and not treated as an afterthought

---

## Technical Architecture

```
Member (Web + Mobile)
        │
        ▼
  HealthSparq Platform
        │
        ├── Healthrules API (Claims)    → Deductible & accumulator balances
        ├── Eligibility & Benefits API  → Plan-specific benefit structure
        └── Third-Party Cost Database   → Procedure & provider pricing benchmarks
```

**Key integration points:**
- **Healthrules API (Claims)** — powers accurate deductible and accumulator balances at time of estimate
- **Eligibility & benefits API** — surfaces member-specific plan structure (co-pays, co-insurance, benefit limits) to personalize estimates
- **Third-party cost database** — HealthSparq's underlying procedure and provider pricing data, localized to market

---

## Compliance & Regulatory Context

This project was driven by the **CMS Price Transparency Rule**, which requires health plans to:
- Provide members with personalized out-of-pocket cost estimates for covered items and services
- Surface estimates through an internet-based self-service tool
- Include accumulated amounts (deductibles, OOP maximums) in cost calculations

All features were designed to meet these requirements, with CMS disclosure language and data accuracy standards embedded in acceptance criteria and validated during UAT.

---

## Outcomes & Impact

- Delivered CMS Price Transparency Rule compliance on schedule across web and mobile channels
- Enabled members to access personalized, claims-informed cost estimates for procedures, drugs, and provider comparisons — for the first time at the health plan
- Integrated real-time claims data into the estimator, ensuring deductible and accumulator accuracy rather than relying on static or population-average figures
- Established a reusable claims + eligibility data integration pattern applicable to future member-facing cost and quality initiatives

---

## Key Learnings & PM Reflection

The most important product decision on this project was insisting that cost estimates reflect a member's *actual* claims and accumulator data — not generic benchmarks. Generic estimates create false confidence and erode member trust when actual bills arrive differently. Connecting real-time claims data was a harder integration to deliver, but the right one.

This project also reinforced that **regulatory compliance and member experience are not opposing forces.** The CMS requirements created the mandate, but the design challenge was making the tool genuinely useful — not just technically compliant. A member who doesn't trust the estimate won't use it, regardless of whether it meets the regulatory checkbox.

---

## Artifacts Available

> *Note: All artifacts are sanitized to remove PHI and proprietary system details in compliance with HIPAA.*

- [ ] Product Requirements Document (PRD) — sanitized
- [ ] CMS compliance requirements mapping
- [ ] Integration data flow diagram
- [ ] UAT test plan — cost estimate accuracy scenarios

---

*This repository documents product ownership work completed at a nonprofit Medicare and Medicaid health plan. All data, member records, and system details have been sanitized or synthesized for public sharing.*
