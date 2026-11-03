---
id: SEED-10
version: "1.0"
status: approved
owner: OP
based_on: []
requirements: []
source_file: "sales_marketing_integration.md"
---

Yes—**sales funnels are compatible with the five-part hybrid model**, but just like marketing funnels, they should be **subordinate tools**, not the master model for sales across this ecosystem.

For this architecture, I would not replace sales funnels with one single “modern alternative.” I would use a more capable hybrid:

**1. Lifecycle state model  
2. Journey graph  
3. Growth loops  
4. Local conversion funnels  
5. Portfolio network model**

…and then add a **sales-specific commercial progression layer** inside that system.

The key distinction is that a sales funnel is still useful for measuring a particular sales motion, but it is too linear to represent the full commercial reality of a post-2025 online company.

Current buyer behavior supports that conclusion. McKinsey’s 2026 B2B research says buyers now use an average of about ten channels across a purchasing journey and expect seamless movement among them; it also reports that e-commerce has become a major commercial channel rather than merely a supporting one. [McKinsey & Company](https://www.mckinsey.com/capabilities/growth-marketing-and-sales/our-insights/the-surprising-economics-of-b2b-growth-the-new-survival-threshold-and-what-it-takes-to-thrive?utm_source=chatgpt.com) IDC’s 2026 research likewise describes AI-mediated buying as increasingly moving research and evaluation outside traditional vendor-owned funnels. [IDC](https://www.idc.com/resource-center/blog/your-buyer-has-moved-has-your-gtm-what-idcs-2026-data-means-for-your-sales-funnel/?utm_source=chatgpt.com)

So the answer is:

> **Sales funnels remain useful, but they should become local measurement structures inside a larger adaptive sales system.**

## Where sales funnels still work very well

Some sales motions are genuinely sequential.

For example:

```text
Qualified Product Visitor
        ↓
Free Trial
        ↓
Activated Trial
        ↓
Pricing Evaluation
        ↓
Paid Subscription
```

Or for a more complex B2B SaaS product:

```text
Qualified Account
      ↓
Demo Request
      ↓
Discovery
      ↓
Technical Evaluation
      ↓
Commercial Evaluation
      ↓
Purchase
```

Those are useful funnels because you want to know:

- conversion between stages;
- time between stages;
- abandonment;
- sales velocity;
- win rate;
- CAC;
- sales-cycle length.

A funnel is excellent for diagnosing:

**“Where are qualified opportunities leaking?”**

It is much less effective at answering:

**“What is this buyer doing throughout the entire ecosystem?”**

---

# Why a traditional sales funnel becomes inadequate

Your ecosystem can create many paths to the same commercial outcome.

Consider the three-domain example.

A user might purchase the Cybersecurity application through:

```text
Google
  ↓
Article
  ↓
Security Assessment
  ↓
Trial
  ↓
Purchase
```

Another might go:

```text
YouTube
   ↓
Newsletter
   ↓
Community
   ↓
Research Report
   ↓
App
   ↓
Purchase
```

Another might go:

```text
AI Answer Engine
      ↓
Research Destination
      ↓
Direct Return 2 Weeks Later
      ↓
Calculator
      ↓
Trial
      ↓
Purchase
```

And another:

```text
Operational Resilience App
       ↓
Security Risk Identified
       ↓
Cybersecurity Tool
       ↓
Security Product
```

All four can enter the same **sales funnel** near the bottom.

But the funnel alone does not explain how they got there.

That is why the hybrid model matters.

---

# The sales-specific version of the hybrid model

I would structure sales like this:

```text
                    COMMERCIAL OPERATING SYSTEM
                              │
                              ▼
                      JOURNEY GRAPH
                              │
             ┌────────────────┼──────────────────┐
             ▼                ▼                  ▼
      Lifecycle State    Buying State       Opportunity State
             │                │                  │
             └────────────────┼──────────────────┘
                              ▼
                 COMMERCIAL ORCHESTRATION
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
   Self-Service           Assisted Sales       Automated Sales
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              ▼
                     LOCAL SALES FUNNELS
                              │
                              ▼
                     PURCHASE / EXPANSION
                              │
                              ▼
                 RETENTION / ADVOCACY / LOOP
```

This is more capable than a traditional funnel.

---

# A crucial addition: Buying State

Lifecycle state and buying state should not be the same thing.

For example, someone can be an:

**Active Customer**

but simultaneously have:

**No buying intent** for another product.

Or:

**Active Customer**

with:

**High expansion intent.**

So I would add a separate **Buying State Model**.

For example:

```text
No Active Need
     ↓
Problem Recognition
     ↓
Exploration
     ↓
Solution Research
     ↓
Active Evaluation
     ↓
Commercial Evaluation
     ↓
Purchase Ready
     ↓
Purchase
```

But unlike a funnel, these states are not assumed to move strictly downward.

A buyer might:

```text
Active Evaluation
      ↓
No Active Need
```

if the problem disappears.

Or:

```text
Exploration
   ↓
Purchase Ready
```

if they already know the category.

This is especially important for self-service digital companies.

---

# Opportunity state is different again

If the business has an assisted sales motion, you may also maintain an **Opportunity State**:

```text
Unqualified
   ↓
Qualified
   ↓
Discovery
   ↓
Evaluation
   ↓
Proposal
   ↓
Negotiation
   ↓
Closed Won / Closed Lost
```

That remains useful operationally.

But notice the hierarchy:

**Journey graph** = what the customer is doing.

**Lifecycle state** = relationship with company/product.

**Buying state** = commercial intent/readiness.

**Opportunity state** = internal sales-process status.

**Sales funnel** = conversion measurement across a particular path.

Those should not be collapsed into one field.

---

# This is particularly important for a solely online company

For a digital-only company, a large share of the sales system can be **self-service or product-led**.

The buyer may never speak to a salesperson.

McKinsey’s 2026 research notes that digital/e-commerce channels are now central to B2B transactions, not peripheral, and buyers expect movement across self-service and other channels. [McKinsey & Company](https://www.mckinsey.com/capabilities/growth-marketing-and-sales/our-insights/the-surprising-economics-of-b2b-growth-the-new-survival-threshold-and-what-it-takes-to-thrive?utm_source=chatgpt.com)

That means the system may have several parallel sales motions.

## Motion 1 — Pure self-service

```text
Content
  ↓
Tool
  ↓
Free Account
  ↓
Trial
  ↓
Upgrade
```

## Motion 2 — Product-led sales

```text
Free User
   ↓
High Usage
   ↓
Team Adoption
   ↓
Expansion Signal
   ↓
Sales Assistance
   ↓
Business Plan
```

## Motion 3 — Assisted enterprise sales

```text
High-Value Account
      ↓
Qualification
      ↓
Demo
      ↓
Technical Review
      ↓
Security Review
      ↓
Commercial Review
      ↓
Purchase
```

## Motion 4 — Cross-domain portfolio sale

```text
Cybersecurity Customer
        ↓
Operational Risk Detected
        ↓
Resilience Product
        ↓
Bundle Evaluation
        ↓
Portfolio Subscription
```

A single funnel cannot cleanly represent all four.

---

# A more modern alternative: Revenue Journey Graph

For your ecosystem, I would make the primary sales representation a **Revenue Journey Graph**.

Instead of forcing customers through one sales funnel, represent possible commercial states and transitions.

Example:

```text
                          Anonymous Visitor
                                 │
                 ┌───────────────┼────────────────┐
                 ▼               ▼                ▼
              Content          Tool            Community
                 │               │                │
                 └───────────────┼────────────────┘
                                 ▼
                           Known User
                                 │
                 ┌───────────────┼────────────────┐
                 ▼               ▼                ▼
             Subscriber      Free User         Trial
                 │               │                │
                 └───────────────┼────────────────┘
                                 ▼
                          Buying Intent
                                 │
                ┌────────────────┼─────────────────┐
                ▼                ▼                 ▼
            Self-Service      Assisted          Enterprise
                │                │                 │
                └────────────────┼─────────────────┘
                                 ▼
                              Customer
                                 │
                  ┌──────────────┼──────────────┐
                  ▼              ▼              ▼
               Retain         Expand         Advocate
                  │              │              │
                  └──────────────┼──────────────┘
                                 ▼
                           Future Demand
```

This more accurately models:

- nonlinear journeys;
- self-service;
- sales assistance;
- cross-product expansion;
- re-entry;
- advocacy;
- recurring revenue.

---

# Then keep funnels underneath it

Funnels should still exist for specific paths.

For example:

## Trial funnel

```text
Trial Started
   ↓
Activation
   ↓
Core Feature Adoption
   ↓
Pricing Viewed
   ↓
Paid Upgrade
```

## Enterprise funnel

```text
Qualified Account
   ↓
Discovery
   ↓
Technical Evaluation
   ↓
Commercial Approval
   ↓
Closed Won
```

## Expansion funnel

```text
Existing Customer
   ↓
Expansion Signal
   ↓
Relevant Product Recommendation
   ↓
Evaluation
   ↓
Expansion Purchase
```

These give excellent operational metrics.

---

# Growth loops matter after the sale

The traditional sales funnel ends at purchase.

That is a major limitation for this ecosystem.

HubSpot’s flywheel framework specifically criticizes the funnel because it treats customers as an endpoint instead of a source of future momentum; its current framework centers attract, engage, and delight in a continuous cycle. [HubSpot Blog](https://blog.hubspot.com/marketing/our-flywheel?src=bl-po\&utm_source=chatgpt.com)

Your ecosystem should model:

```text
Purchase
   ↓
Successful Usage
   ↓
Retention
   ↓
Advocacy / Review / Referral
   ↓
New Discovery
   ↓
New Users
```

And also:

```text
Purchase
   ↓
Usage Data
   ↓
New Need Identified
   ↓
Relevant Portfolio Recommendation
   ↓
Second Product
```

The second loop is especially important for your multi-domain portfolio.

---

# Portfolio sales creates another reason funnels are insufficient

Suppose the same company buys:

- Security Readiness Manager
- Continuity Planner
- Cash Flow Planner

A traditional funnel might say:

```text
Lead → Customer
```

But once they become a customer, the economically important questions become:

- Which domains are relevant?
- Which products are eligible?
- Which product should be recommended next?
- Is bundling better?
- Is there expansion intent?
- Would promotion damage trust?
- Should the user stay with only one product?

This is better modeled as an **account/product relationship graph**.

```text
                    Customer Account
                          │
       ┌──────────────────┼──────────────────┐
       ▼                  ▼                  ▼
 Cybersecurity       Resilience          Finance
    Product             Product           Product
       │                  │                  │
    ACTIVE             ELIGIBLE          NOT RELEVANT
```

That last status is important.

A company does **not** automatically become a cross-sell target for the full portfolio.

---

# Sales orchestration should determine the next-best commercial action

The system can evaluate:

```text
Customer Context
      +
Buying State
      +
Lifecycle State
      +
Product Usage
      +
Problem Signals
      +
Domain Affinity
      +
Economic Eligibility
      +
Recommendation Rules
      +
Frequency
      +
Trust Risk
      ↓
NEXT-BEST COMMERCIAL ACTION
```

Possible outcomes:

- show educational content;
- offer trial;
- prompt upgrade;
- invite demo;
- recommend another product;
- offer bundle;
- route to salesperson;
- wait;
- suppress sales activity.

Again:

**“Do nothing commercially” should be a valid outcome.**

---

# Example from the three-domain ecosystem

Assume a customer already uses:

**Security Readiness Manager.**

The system detects that they:

- manage 40 employees;
- recently completed the ransomware assessment;
- identified no documented continuity plan;
- repeatedly read downtime-recovery content.

Their state might be:

```text
Cybersecurity lifecycle:
Active Customer

Operational Resilience lifecycle:
Engaged Visitor

Operational Resilience buying state:
Problem Recognition

Finance lifecycle:
Unknown

Finance buying state:
No Active Need
```

The system should therefore:

### Recommend

A continuity-planning resource.

### Potentially later offer

Continuity Planner trial.

### Not recommend

Cash Flow Planner.

Even though the Finance product could generate revenue.

After they use the continuity tool and calculate a seven-day outage, a new signal might appear:

```text
Financial impact:
$85,000 projected cash impact
```

Now Finance may become contextually relevant.

That is much more precise than:

```text
Customer
   ↓
Cross-sell
```

---

# What replaces the classic sales funnel as the master model?

For this ecosystem, I would use:

## Primary model

### **Revenue Journey Graph**

Represents the actual nonlinear customer/commercial journey.

## State models

### **Lifecycle State**
Relationship with property/product.

### **Buying State**
Current buying readiness.

### **Opportunity State**
Internal status for assisted sales.

## Dynamic decision layer

### **Commercial Orchestration / Next-Best-Action Engine**

Determines what should happen next.

## Measurement tools

### **Local Sales Funnels**

Measure specific conversion paths.

## Compounding layer

### **Revenue/Growth Loops**

Represent retention, advocacy, expansion, and referrals.

## Portfolio layer

### **Account–Product Relationship Graph**

Controls cross-domain and cross-product selling.

That would produce this hierarchy:

```text
                 PORTFOLIO COMMERCIAL SYSTEM
                           │
                           ▼
                 REVENUE JOURNEY GRAPH
                           │
          ┌────────────────┼──────────────────┐
          ▼                ▼                  ▼
    Lifecycle State    Buying State     Opportunity State
          │                │                  │
          └────────────────┼──────────────────┘
                           ▼
                COMMERCIAL ORCHESTRATION
                           │
                           ▼
                NEXT-BEST-ACTION ENGINE
                           │
        ┌──────────────────┼───────────────────┐
        ▼                  ▼                   ▼
   Self-Service      Assisted Sales      Portfolio Expansion
        │                  │                   │
        └──────────────────┼───────────────────┘
                           ▼
                    LOCAL FUNNELS
                           │
                           ▼
                        PURCHASE
                           │
                           ▼
              RETENTION / EXPANSION / ADVOCACY
                           │
                           ▼
                     REVENUE LOOPS
                           │
                           └─────────────► Future Demand
```

## How this fits the original five-point hybrid

The original five become:

| Original hybrid component | Sales-system role |
|---|---|
| **Lifecycle State Model** | Customer relationship/status |
| **Journey Graph** | Primary sales/buyer topology |
| **Growth Loops** | Retention, referral, expansion, recurring revenue |
| **Local Conversion Funnels** | Individual sales-motion measurement |
| **Portfolio Network Model** | Cross-domain/product commercial relationships |

Then I would add **Buying State + Commercial Orchestration** as sales-specific capabilities inside that structure.

So I would **not create a separate “sales funnel architecture” beside your hybrid model**.

I would integrate sales into the hybrid model.

The result is more modern and more suitable for a solely online post-2025 company because it supports:

- self-service buying;
- AI-mediated discovery;
- product-led sales;
- automated sales;
- human-assisted sales;
- omnichannel movement;
- subscriptions;
- recurring revenue;
- expansion;
- cross-domain purchases;
- reactivation;
- referrals.

That is more aligned with current digital buying patterns than using a traditional linear funnel as the governing commercial model. [McKinsey & Company](https://www.mckinsey.com/capabilities/growth-marketing-and-sales/our-insights/the-surprising-economics-of-b2b-growth-the-new-survival-threshold-and-what-it-takes-to-thrive?utm_source=chatgpt.com)
