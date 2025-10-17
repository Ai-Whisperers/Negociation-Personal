# Quick Reference for Oct 17 Meeting

**Meeting:** Personal Paraguay - Customer Feedback AI Analyzer
**Date:** October 17, 2025
**Contact:** José Luis Domínguez, Manager of Customer Experience
**Our Team:** Kyrian (business lead), Jonathan (technical), Ivan (advisor)

---

## ⚡ YOUR BOTTOM LINE (MEMORIZE THIS)

### Pricing
- **🚫 Hard Pass (walk away):** <15,000,000 PYG (<$2,143 USD)
- **💰 Minimum to accept:** 40,000,000 PYG ($5,714 USD)
- **🎯 Target (ideal):** 80,000,000 PYG ($11,429 USD)
- **🌟 Stretch goal:** 150,000,000 PYG ($21,429 USD)

### Strategy
- ✅ **Let THEM give first price** (reverse-anchor)
- ✅ **Work the 25-15 corridor** (start high, min 15M)
- ✅ **Pilot model:** 10 days, dashboard + export, black-box SaaS

---

## 💪 YOUR STRENGTHS (Lead with these)

1. **Ready NOW** - Production v3.2.0, tested with 850 comments
2. **90-98% cheaper** than alternatives ($5.7k vs. $80k-$243k)
3. **10 months faster** than building in-house
4. **87% AI cost savings** through hybrid architecture
5. **Source code included** - Zero vendor lock-in
6. **Proven performance:** 1000 comments in ~25 seconds

---

## 🎯 WHAT JOSÉ LUIS VALUES MOST

1. **Automation** - Freedom from manual labor (#1 priority)
2. **Daily/Weekly Reports** - Automatic recurring insights
3. **Speed** - Faster than manual process
4. **Quick Wins** - Show results to his managers

**His Pain:**
- 40 hours/month manual analysis = $24,000/year wasted
- Can't scale beyond ~100-200 comments
- Misses churn signals and actionable insights

---

## 🔑 KEY FACTS ABOUT JOSÉ LUIS

### Background
- **Role:** Manager of Customer Experience (2 years)
- **Previous:** Survey Coordinator at Personal (knows the pain)
- **Expertise:** 6+ years market research, data analysis, KPIs
- **Decision Power:** 3/5 - He's a CHAMPION, needs approval

### What We Know
- **First Contact:** Aug 16, 2025 (2 months ago)
- **Meetings:** 3 total, demo shown
- **Budget Indication:** NONE (use reverse-anchor)
- **Decision Timeline:** End of month preferred
- **Sample Data:** YES, we have many samples

### Approval Chain
José Luis needs approval from:
- **CFO/Finance** (cares about ROI)
- **CTO/IT** (cares about architecture, security)
- **Executive Committee** (cares about strategic value)

**Your Strategy:** Help José Luis sell internally with materials

---

## 📊 PRODUCT CAPABILITIES

### What It Does
**Input:** CSV/Excel files (up to 20MB, 3,000 rows)
- Required columns: `Nota` (0-10 rating), `Comentario Final` (feedback text)

**Processing:** AI analyzes each comment for:
1. **7 Emotions** (Satisfaction, Frustration, Anger, Trust, Disappointment, Confusion, Anticipation)
2. **Churn Risk** (0-1 probability score)
3. **Pain Points** (Top 10 recurring issues: pricing, quality, service, etc.)
4. **NPS Classification** (Promoter/Passive/Detractor)
5. **Sentiment Score** (-1 to 1)

**Output:**
- Interactive dashboard with charts
- Professional Excel export (multi-sheet with embedded charts)
- CSV export (raw data)

### Performance Metrics

| Comments | Time | Cost (Our Hybrid Model) |
|----------|------|-------------------------|
| 100 | ~3s | $0.002 (14 PYG) |
| 500 | ~12s | $0.010 (71 PYG) |
| 1,000 | ~25s | $0.020 (142 PYG) |
| 3,000 | ~75s | $0.060 (425 PYG) |

### Infrastructure (Render.com)
**Monthly Costs:** ~$30-35/month
- Redis (key-value store)
- FastAPI Backend (private API)
- Celery Worker (background processing)
- React BFF (public web service)

**Tech Stack:**
- Frontend: React 18.3 + TypeScript + Tailwind CSS
- Backend: FastAPI (Python 3.11) + Celery + Redis
- AI: OpenAI GPT-4o-mini + VADER/TextBlob (hybrid)

---

## 💰 ROI CALCULATOR (Show This)

### vs. Manual Analysis
**Client's Current Cost:**
- 40 hours/month × $50/hour = $2,000/month = **$24,000/year**

**With Our Solution:**
- One-time: $5,714 (your target price)
- Monthly: $32/month (infrastructure + tokens)
- **Annual cost:** $5,714 + $384 = **$6,098**

**Savings:** $24,000 - $6,098 = **$17,902 saved in Year 1**

**ROI:**
- Payback period: **2.4 months**
- 3-year ROI: **1,672%** (16.7x return)

### vs. Building In-House
- In-house: $135,000 + 12 months
- Our solution: $5,714 + 2 weeks
- **Savings: $129,286 + 10 months**

### vs. Enterprise SaaS (Qualtrics, Medallia)
- Enterprise SaaS: $80,000 over 3 years
- Our solution: $6,098/year × 3 = $18,294
- **Savings: $61,706 over 3 years**

---

## 🤝 EASY WINS (Give These Freely)

1. **Payment terms:** 50%/30%/20% over 60 days
2. **Extra training:** 2 → 3 sessions
3. **Extended support:** 30 → 60 days
4. **Custom pain point categories**
5. **Logo/branding customization**
6. **Automated daily/weekly reports** (his #1 value!)

---

## ⚠️ NEVER CONCEDE

1. **Below 15M PYG pricing** - Hard pass
2. **Unlimited scope/support**
3. **IP ownership** (they license, not own)
4. **24/7 support** (unsustainable for 3-person team)

---

## 🎁 NON-FINANCIAL VALUE (Trade for Lower Price)

**If they push for discount, ask for:**
1. ⭐ Written testimonial
2. ⭐ Case study with their logo
3. ⭐ 2-3 referrals to other companies
4. ⭐ Ongoing relationship/retainer

**Example:** "We can do 60M PYG instead of 80M if you provide a video testimonial and introduce us to 2 other companies in your network."

---

## 📋 MEETING AGENDA (Suggested)

### 1. Recap (5 min)
- Thank them for 2 months of engagement
- Acknowledge 3 meetings and demo shown
- Confirm understanding of their pain (automation need)

### 2. Demo Highlights (10 min - Jonathan leads)
- Show live demo emphasizing **automation**
- Highlight **daily/weekly reports** capability
- Show **Excel export** with charts
- Emphasize **speed** (1000 comments in 25 seconds)

### 3. Value Proposition (10 min - Kyrian leads)
- **Their pain:** 40 hours/month manual analysis
- **Our solution:** Automated in seconds
- **ROI:** $17,902 saved in Year 1
- **Comparison:** 90-98% cheaper than alternatives

### 4. Pricing Discussion (15 min - Kyrian leads)
- **Ask them first:** "What budget range were you considering?"
- **If they dodge:** Present tier structure (S/M/L + Flat)
- **Work the corridor:** Start at 80-100M, accept down to 40M minimum
- **Pilot option:** 10 days, dashboard + export, lower entry cost

### 5. Approval Process (5 min)
- **Ask:** "Who else needs to approve this?"
- **Offer:** "We can provide materials for CFO/CTO/Executives"
- **Timeline:** "What's the decision timeline?"

### 6. Next Steps (5 min)
- Agree on follow-up actions
- Set next meeting date
- Provide materials for internal pitch

---

## 🎬 OPENING SCRIPT

**Kyrian:** "José Luis, thank you for the 2 months of engagement and the 3 meetings we've had. We really appreciate your time and the insights you've shared about Personal Paraguay's needs.

From our conversations, we understand that manual customer feedback analysis is taking about 40 hours a month, and you're looking for automation that can provide daily or weekly reports automatically. Is that accurate?

[Wait for confirmation]

Great. Today we'd like to show you exactly how our AI platform delivers that automation, discuss the ROI and savings, and if it makes sense, talk about next steps.

Jonathan, would you like to start with a quick demo of the automation features?"

---

## 🎬 PRICING SCRIPT

**Kyrian:** "Before we discuss pricing, I'd like to understand: what budget range were you considering for this solution?"

**If they give a number:**
- ≥80M PYG: "That works for us. Let's discuss what's included at that level."
- 40-80M PYG: "We can work with that. Let me show you our tier options."
- 15-40M PYG: "That's a bit below our target, but let's see if we can find a structure that works. What if we start with a pilot?"
- <15M PYG: "I appreciate the offer, but that's below our minimum. For that budget, we could only offer a limited pilot. Would that interest you?"

**If they don't give a number:**
"No problem. Let me show you our tier structure. We have Small, Medium, and Large packages with different token limits and support levels. The typical range is 40-80 million PYG depending on volume and features. Does that fit within your planning?"

---

## 🎬 OBJECTION RESPONSES

### "That's expensive"
"I understand. Let's look at the ROI. You're currently spending $24,000/year on manual analysis. Our solution costs $6,098 total in Year 1, saving you $17,902. It pays for itself in 2.4 months. Would you like to see the detailed ROI calculator?"

### "You have no track record"
"That's true - you'd be our first reference client, which is why we're offering competitive pricing and source code included. You get a production-ready platform that's already been tested with 850 comments, plus zero vendor lock-in. Many companies would charge 10x more and lock you into their ecosystem."

### "We can build this in-house"
"Absolutely, you could. Based on similar projects, that would take about 12 months and $135,000 in development costs. Our solution is ready now for $5,714. Plus, your development team can focus on revenue-generating features instead of infrastructure. What's the opportunity cost of 12 months for your product roadmap?"

### "Can we get a discount?"
"We're already priced 90-98% lower than enterprise alternatives. However, if you can provide a video testimonial and introduce us to 2 other companies in your network, we could reduce the price to [X]. Would that work?"

---

## 🎬 CLOSING SCRIPT

**Kyrian:** "José Luis, based on everything we've discussed:
- Our platform solves your automation need
- It saves you $17,902 in the first year
- You get source code with zero vendor lock-in
- We can deploy in 2 weeks

What I'd like to propose is [PRICE]. In return, we provide:
- Full platform access
- 60 days of support
- 3 training sessions
- Automated daily/weekly reports
- All source code

If you need materials to present to your CFO, CTO, or executive team, we'll provide those.

What questions do you have?"

---

## 🚫 WALK AWAY IF...

1. **Price <15M PYG** - Below cost, hard pass
2. **Rude/disrespectful behavior** - You don't tolerate this
3. **Unreasonable demands** - Unlimited scope, 24/7 support, giving up IP
4. **Red flags** - Work "on spec," free work, payment concerns

**How to walk away gracefully:**
"I appreciate your time, José Luis, but I don't think we can find common ground on this. If circumstances change or you'd like to revisit this in the future, please feel free to reach out. Thank you for considering us."

---

## 📝 AFTER MEETING - SEND THESE

1. **Meeting Summary Email** (within 24 hours)
2. **Executive Summary** (1-pager for decision-makers)
3. **ROI Calculator** (Excel)
4. **CFO One-Pager** (financial benefits)
5. **CTO One-Pager** (technical architecture)
6. **Comparison Matrix** (us vs. alternatives)

---

## ⏰ MEETING CHECKLIST

**Before Meeting:**
- [ ] Test demo (ensure it works flawlessly)
- [ ] Prepare ROI calculator
- [ ] Print pricing sheet (S/M/L tiers)
- [ ] Review this quick reference
- [ ] Team roles clear (Kyrian=business, Jonathan=technical, Ivan=notes)

**During Meeting:**
- [ ] Thank them for engagement
- [ ] Let them anchor price first
- [ ] Emphasize automation and daily reports
- [ ] Show ROI calculator
- [ ] Ask about approval process
- [ ] Offer internal selling materials

**After Meeting:**
- [ ] Send meeting summary within 24 hours
- [ ] Provide stakeholder materials
- [ ] Follow up on action items
- [ ] Stay in regular contact

---

## 🎯 SUCCESS METRICS

**Must Have:**
- ✅ Close at ≥40M PYG ($5,714)
- ✅ Signed contract with clear scope
- ✅ Written testimonial committed

**Nice to Have:**
- ✅ 60-80M PYG ($8,571-11,429)
- ✅ Case study with their logo
- ✅ 1-2 referrals
- ✅ Ongoing support retainer

**Would Be Amazing:**
- ✅ 100-150M PYG ($14,286-21,429)
- ✅ Video testimonial
- ✅ 3+ referrals with warm intros
- ✅ Multi-year partnership

---

**REMEMBER:** You want the reference/case study, but you CAN walk away. This is a strong negotiating position. Don't act desperate (even though this is your only current opportunity).

**GOOD LUCK! 🚀**

---

**Last Updated:** 2025-10-16 23:45
**Meeting Time:** [CONFIRM WITH CLIENT]
**Meeting Location/Link:** [CONFIRM WITH CLIENT]
