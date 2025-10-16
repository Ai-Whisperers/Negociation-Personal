# ROI CALCULATOR - Customer Feedback Analysis Platform

**Purpose:** Calculate real ROI for your client based on their actual usage
**Use:** During pricing discussion to justify investment

---

## HOW TO USE THIS CALCULATOR

**During the meeting, ask these questions:**

1. "How many customer feedback comments do you receive per month?"
2. "How many hours per month does your team spend analyzing feedback?"
3. "What's the average hourly cost of the people analyzing feedback?"
4. "What's your current customer churn rate?"
5. "What's the average lifetime value (LTV) of a customer?"

**Then use the formulas below to calculate their ROI.**

---

## SCENARIO 1: TIME SAVINGS ROI

### Client Inputs (Fill in during meeting):

```
┌──────────────────────────────────────────────────────┐
│ CLIENT DATA - TIME SAVINGS                           │
├──────────────────────────────────────────────────────┤
│ Comments per month:           [_______]              │
│ Hours spent analyzing/month:  [_______]              │
│ Hourly cost of analysts:      $[_______]            │
│                                                       │
│ YOUR PRICE:                   $[_______]            │
└──────────────────────────────────────────────────────┘
```

### Calculation:

**Step 1: Calculate Current Monthly Cost**
```
Current Monthly Cost = Hours × Hourly Cost

Example:
- 10,000 comments/month
- Takes 40 hours to analyze manually
- Analysts cost $50/hour

Current Monthly Cost = 40 hours × $50/hour = $2,000/month
```

**Step 2: Calculate Annual Cost (Current State)**
```
Annual Cost = Monthly Cost × 12

Example:
$2,000/month × 12 = $24,000/year
```

**Step 3: Calculate New Cost (With Platform)**
```
Platform Cost (Year 1):
- One-time: [Your price, e.g., $4,000]
- Monthly infra: $30/month = $360/year
- OpenAI API: ~$20/year
- Total Year 1: $4,380

Platform Cost (Year 2+):
- Monthly infra: $360/year
- OpenAI API: $20/year
- Total: $380/year
```

**Step 4: Calculate Savings**
```
Year 1 Savings = Current Annual Cost - Platform Cost Year 1
Year 2+ Savings = Current Annual Cost - Platform Cost Year 2+

Example:
Year 1: $24,000 - $4,380 = $19,620 saved
Year 2: $24,000 - $380 = $23,620 saved
Year 3: $24,000 - $380 = $23,620 saved

3-Year Total Savings: $66,860
```

**Step 5: Calculate ROI**
```
ROI = (Total Savings ÷ Your Price) × 100

Example:
3-Year ROI = ($66,860 ÷ $4,000) × 100 = 1,672% ROI
Payback Period = $4,000 ÷ $19,620/year = 0.2 years (2.4 months)
```

### VISUAL PRESENTATION (Show to client):

```
┌─────────────────────────────────────────────────────────┐
│ YOUR 3-YEAR ROI SUMMARY                                 │
├─────────────────────────────────────────────────────────┤
│ CURRENT STATE (Manual Analysis):                        │
│ ├─ Time: 40 hours/month                                 │
│ ├─ Cost: $2,000/month = $24,000/year                   │
│ └─ 3-Year Total: $72,000                                │
│                                                          │
│ WITH OUR PLATFORM:                                       │
│ ├─ Time: 2 minutes/month (automated)                    │
│ ├─ Cost Year 1: $4,380                                  │
│ ├─ Cost Year 2: $380                                    │
│ └─ Cost Year 3: $380                                    │
│                                                          │
│ YOUR SAVINGS:                                            │
│ ├─ Year 1: $19,620                                      │
│ ├─ Year 2: $23,620                                      │
│ ├─ Year 3: $23,620                                      │
│ └─ 3-Year Total: $66,860                                │
│                                                          │
│ ROI: 1,672% over 3 years                                │
│ Payback Period: 2.4 months                              │
└─────────────────────────────────────────────────────────┘
```

---

## SCENARIO 2: CHURN REDUCTION ROI

### Client Inputs:

```
┌──────────────────────────────────────────────────────┐
│ CLIENT DATA - CHURN REDUCTION                        │
├──────────────────────────────────────────────────────┤
│ Total customers:              [_______]              │
│ Current churn rate:           [_______]%             │
│ Average customer LTV:         $[_______]            │
│                                                       │
│ Expected churn reduction:     [_______]%             │
│ (Conservative: 1-2%)                                  │
│                                                       │
│ YOUR PRICE:                   $[_______]            │
└──────────────────────────────────────────────────────┘
```

### Calculation:

**Step 1: Calculate Current Churn Impact**
```
Annual Churned Customers = Total Customers × Churn Rate
Annual Churn Cost = Churned Customers × LTV

Example:
- 1,000 customers
- 15% annual churn
- $2,000 LTV per customer

Churned Customers = 1,000 × 15% = 150 customers
Churn Cost = 150 × $2,000 = $300,000/year lost
```

**Step 2: Calculate Platform Impact**
```
Our platform identifies high-risk customers (13% based on 850-comment test).
Conservative assumption: You save 10% of at-risk customers.

Customers Saved = (Total Customers × High-Risk %) × Save Rate
Revenue Saved = Customers Saved × LTV

Example:
- 1,000 customers × 13% = 130 high-risk
- Save 10% of high-risk = 13 customers saved
- 13 × $2,000 LTV = $26,000/year revenue saved
```

**Step 3: Calculate ROI**
```
ROI = (Revenue Saved ÷ Your Price) × 100
Payback Period = Your Price ÷ Annual Revenue Saved

Example:
ROI = ($26,000 ÷ $4,000) × 100 = 650% ROI (Year 1)
Payback Period = $4,000 ÷ $26,000 = 0.15 years (1.8 months)
```

### VISUAL PRESENTATION:

```
┌─────────────────────────────────────────────────────────┐
│ CHURN REDUCTION ROI                                     │
├─────────────────────────────────────────────────────────┤
│ WITHOUT PLATFORM:                                        │
│ ├─ Total customers: 1,000                               │
│ ├─ Churn rate: 15% = 150 lost customers/year           │
│ └─ Revenue lost: $300,000/year                          │
│                                                          │
│ WITH PLATFORM:                                           │
│ ├─ High-risk identified: 13% = 130 customers            │
│ ├─ Customers saved: 10% of high-risk = 13 customers    │
│ └─ Revenue saved: $26,000/year                          │
│                                                          │
│ YOUR INVESTMENT:                                         │
│ ├─ Platform: $4,000 (one-time)                          │
│ └─ Ongoing: $380/year                                   │
│                                                          │
│ NET BENEFIT:                                             │
│ ├─ Year 1: $26,000 - $4,380 = $21,620 profit           │
│ ├─ Year 2-3: $26,000 - $380 = $25,620/year             │
│ └─ 3-Year Total: $72,860 profit                         │
│                                                          │
│ ROI: 650% (Year 1) | Payback: 1.8 months               │
└─────────────────────────────────────────────────────────┘
```

**CONSERVATIVE ASSUMPTIONS:**
- Only saving 10% of high-risk customers (realistic)
- Not counting other benefits (NPS insights, pain points, etc.)
- Assumes static customer base (no growth)

---

## SCENARIO 3: PRODUCT IMPROVEMENT ROI

### Client Inputs:

```
┌──────────────────────────────────────────────────────┐
│ CLIENT DATA - PRODUCT IMPROVEMENT                    │
├──────────────────────────────────────────────────────┤
│ Annual product development budget: $[_______]        │
│ Feature prioritization time/year: [___] hours        │
│ Cost per hour of product team:    $[_______]        │
│                                                       │
│ Expected improvement in feature ROI: [___]%          │
│ (Conservative: 10-20%)                                │
│                                                       │
│ YOUR PRICE:                        $[_______]        │
└──────────────────────────────────────────────────────┘
```

### Calculation:

**Step 1: Current Product Development Waste**
```
Research shows 40-50% of features are rarely or never used.

Development Waste = Budget × Waste Rate

Example:
- $500,000 annual dev budget
- 40% waste rate
- Waste = $500,000 × 40% = $200,000/year wasted
```

**Step 2: Platform Impact on Prioritization**
```
Our platform identifies top pain points from real feedback.
Conservative: 10% improvement in feature ROI.

Waste Reduction = Development Waste × Improvement %
Savings = Waste Reduction

Example:
- $200,000 waste × 10% improvement = $20,000 saved/year
```

**Step 3: Time Savings on Prioritization**
```
Feature Prioritization Time Saved = Hours × Hourly Cost

Example:
- Currently: 40 hours/quarter = 160 hours/year
- With platform: 10 hours/quarter = 40 hours/year
- Saved: 120 hours × $100/hour = $12,000/year
```

**Step 4: Total ROI**
```
Total Annual Savings = Waste Reduction + Time Savings

Example:
$20,000 + $12,000 = $32,000/year

ROI = ($32,000 ÷ $4,000) × 100 = 800% ROI (Year 1)
```

### VISUAL PRESENTATION:

```
┌─────────────────────────────────────────────────────────┐
│ PRODUCT IMPROVEMENT ROI                                 │
├─────────────────────────────────────────────────────────┤
│ CURRENT STATE:                                           │
│ ├─ Dev budget: $500,000/year                            │
│ ├─ Feature waste: 40% = $200,000/year                   │
│ └─ Prioritization: 160 hours/year = $16,000             │
│                                                          │
│ WITH PLATFORM:                                           │
│ ├─ Data-driven prioritization (pain points)             │
│ ├─ Waste reduced by 10% = $20,000 saved                │
│ ├─ Time saved: 120 hours = $12,000                     │
│ └─ Total annual savings: $32,000                        │
│                                                          │
│ YOUR INVESTMENT: $4,000                                  │
│                                                          │
│ NET BENEFIT: $28,000 (Year 1)                           │
│ ROI: 800% | Payback: 1.5 months                        │
└─────────────────────────────────────────────────────────┘
```

---

## SCENARIO 4: COMPETITIVE COMPARISON ROI

### Show this if they're considering building in-house or using competitors

```
┌────────────────────────────────────────────────────────────────────┐
│ TOTAL COST OF OWNERSHIP (3 YEARS)                                 │
├────────────────────────────────────────────────────────────────────┤
│                     │ Manual   │ Build    │ Competitor │ OUR       │
│                     │ Analysis │ In-House │ SaaS       │ PLATFORM  │
├─────────────────────┼──────────┼──────────┼────────────┼───────────┤
│ YEAR 1              │          │          │            │           │
│ Setup/Dev           │ $0       │ $135,000 │ $25,000    │ $4,000    │
│ Infrastructure      │ $0       │ $2,400   │ included   │ $360      │
│ Labor Cost          │ $24,000  │ included │ included   │ included  │
│ Software/API        │ $0       │ $1,000   │ included   │ $20       │
│ Support             │ $0       │ $0       │ $5,000     │ included  │
├─────────────────────┼──────────┼──────────┼────────────┼───────────┤
│ YEAR 1 TOTAL        │ $24,000  │ $138,400 │ $30,000    │ $4,380    │
├─────────────────────┼──────────┼──────────┼────────────┼───────────┤
│ YEAR 2-3 (Annual)   │          │          │            │           │
│ Labor/License       │ $24,000  │ $50,000  │ $25,000    │ $0        │
│ Infrastructure      │ $0       │ $2,400   │ included   │ $360      │
│ Maintenance         │ $0       │ included │ included   │ $20       │
├─────────────────────┼──────────┼──────────┼────────────┼───────────┤
│ YEAR 2 TOTAL        │ $24,000  │ $52,400  │ $25,000    │ $380      │
│ YEAR 3 TOTAL        │ $24,000  │ $52,400  │ $25,000    │ $380      │
├─────────────────────┼──────────┼──────────┼────────────┼───────────┤
│ 3-YEAR TCO          │ $72,000  │ $243,200 │ $80,000    │ $5,140    │
├─────────────────────┼──────────┼──────────┼────────────┼───────────┤
│ YOUR SAVINGS vs:    │ $66,860  │ $238,060 │ $74,860    │ -         │
│ SAVINGS %           │ 93%      │ 98%      │ 94%        │ -         │
└────────────────────────────────────────────────────────────────────┘
```

**TALKING POINTS:**
- "You save 93-98% vs. any alternative"
- "Payback in 2-3 months, then pure profit"
- "No ongoing labor costs, no vendor lock-in"

---

## COMBINED ROI (Best Case Scenario)

**If client gets value from multiple areas:**

```
┌─────────────────────────────────────────────────────────┐
│ COMBINED ANNUAL ROI                                     │
├─────────────────────────────────────────────────────────┤
│ Time Savings:          $19,620/year                     │
│ Churn Reduction:       $26,000/year                     │
│ Product Improvement:   $32,000/year                     │
├─────────────────────────────────────────────────────────┤
│ TOTAL ANNUAL VALUE:    $77,620/year                     │
│                                                          │
│ YOUR INVESTMENT:       $4,000                            │
│                                                          │
│ FIRST-YEAR ROI:        1,941%                           │
│ PAYBACK PERIOD:        0.6 months (18 days)             │
└─────────────────────────────────────────────────────────┘
```

**CONSERVATIVE APPROACH:**
- Don't claim all three benefits
- Pick the 1-2 most relevant to client
- Underpromise, overdeliver

---

## QUICK ROI TEMPLATES (Fill During Meeting)

### Template 1: Simple Time Savings

```
Your current cost: [___] hours/month × $[___]/hour = $[_____]/month
Annual cost: $[_____] × 12 = $[_____]/year

Our platform: $[_____] one-time
Annual savings: $[_____] - $[_____] = $[_____]

ROI: [_____]%
Payback: [___] months
```

### Template 2: Simple Churn Reduction

```
Your customers: [_____]
Churn rate: [___]% = [___] lost customers/year
LTV: $[_____] per customer
Annual churn cost: [___] × $[_____] = $[_____]

High-risk identified by platform: 13% = [___] customers
Conservative save rate: 10% = [___] customers
Revenue saved: [___] × $[_____] = $[_____]/year

Our platform: $[_____]
ROI: [_____]%
```

---

## HOW TO PRESENT ROI IN THE MEETING

**Step 1: Ask Discovery Questions (3 minutes)**
```
"Before we discuss pricing, I'd like to understand your current process:
1. How many feedback comments do you get monthly?
2. How do you analyze them today?
3. How much time does that take?
4. What does that time cost you?"
```

**Step 2: Fill in Template (2 minutes)**
- Use one of the templates above
- Calculate on the spot (use phone calculator if needed)
- Write it down on paper or whiteboard

**Step 3: Present ROI (2 minutes)**
```
"Based on what you just told me, here's your ROI:

Currently, you're spending $[X]/year on manual analysis.
With our platform:
- Year 1 cost: $[Y] (including our fee)
- Savings: $[X - Y]
- ROI: [calculate]%
- Payback: [calculate] months

That means you'll have paid off the entire investment by [date],
and everything after that is pure profit."
```

**Step 4: Handle Objections**
```
"That's a [X]% return in the first year alone. Where else can you
get that kind of ROI with this little risk?"
```

---

## ROI CHEAT SHEET (Print and Bring)

```
┌─────────────────────────────────────────────────────────┐
│ ROI QUICK REFERENCE                                     │
├─────────────────────────────────────────────────────────┤
│ FORMULA: ROI = (Gain - Cost) ÷ Cost × 100              │
│                                                          │
│ AVERAGE BENCHMARKS:                                      │
│ - Time savings: 40 hours/month → 2 minutes              │
│ - Cost savings: $0.15/comment → $0.018/comment          │
│ - Churn reduction: 1-2% (conservative)                  │
│ - Typical payback: 1-3 months                           │
│                                                          │
│ COMPARISONS:                                             │
│ - vs. Manual: 93% savings                               │
│ - vs. Build: 98% savings                                │
│ - vs. Competitor SaaS: 94% savings                      │
│                                                          │
│ TALKING POINTS:                                          │
│ ✅ "Payback in [X] months, then pure profit"            │
│ ✅ "Save [X]% vs. building in-house"                    │
│ ✅ "ROI of [X]% in year 1 alone"                        │
│ ✅ "Where else can you get this ROI with zero risk?"    │
└─────────────────────────────────────────────────────────┘
```

---

## AFTER THE MEETING: Send Custom ROI Report

**Email template:**

```
Subject: Your Custom ROI Analysis - [Company Name]

Hi [Name],

Thank you for the great discussion today. As promised, here's
your custom ROI analysis based on the numbers you shared:

CURRENT STATE:
- [X] comments/month
- [X] hours spent analyzing
- $[X]/year in analysis costs

WITH OUR PLATFORM:
- Investment: $[X] one-time
- Annual cost: $[X] (infrastructure + API)
- Time saved: [X] hours/month

YOUR ROI:
- Year 1 savings: $[X]
- Year 2-3 savings: $[X]/year
- 3-year total: $[X] saved
- Payback period: [X] months
- ROI: [X]%

Let's schedule a follow-up to discuss next steps.

Best,
[Your name]

[Attach: Filled-in ROI calculator from this document]
```

---

**Use this calculator to:**
✅ Justify your pricing with hard numbers
✅ Show multiple ROI scenarios (time, churn, product)
✅ Compare to alternatives (manual, build, competitor)
✅ Create urgency (fast payback period)
✅ Send follow-up with custom analysis
