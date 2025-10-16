# NEGOTIATION PROJECT - FILE & FOLDER STRUCTURE GUIDE

**Date Created:** 2025-10-16
**Project:** SaaS Product Negotiation
**Version:** 1.0

---

## TABLE OF CONTENTS

1. [Recommended Folder Structure](#recommended-folder-structure)
2. [Complete File Inventory](#complete-file-inventory)
3. [File Creation Checklist](#file-creation-checklist)
4. [Naming Conventions](#naming-conventions)
5. [File Templates by Category](#file-templates-by-category)

---

# RECOMMENDED FOLDER STRUCTURE

```
Negociation-Personal/
│
├── 01-Research/
│   ├── Client-Research/
│   │   ├── Company-Profile.md
│   │   ├── Stakeholder-Analysis.md
│   │   ├── Pain-Points-Analysis.md
│   │   ├── Budget-Timeline-Research.md
│   │   ├── Technical-Requirements.md
│   │   └── Previous-Interactions-Log.md
│   │
│   ├── Market-Research/
│   │   ├── Competitor-Analysis.md
│   │   ├── Market-Pricing-Benchmark.md
│   │   ├── Industry-Trends.md
│   │   └── Alternative-Solutions-Comparison.md
│   │
│   └── Internal-Analysis/
│       ├── Cost-Breakdown.xlsx
│       ├── BATNA-Analysis.md
│       ├── Our-Capabilities-Inventory.md
│       └── Leverage-Assessment.md
│
├── 02-Strategy/
│   ├── Negotiation-Playbook.md
│   ├── Pricing-Strategy.md
│   ├── Concession-Plan.md
│   ├── Objection-Response-Scripts.md
│   ├── Value-Proposition.md
│   └── Deal-Structure-Options.md
│
├── 03-Materials-for-Client/
│   ├── Presentations/
│   │   ├── Executive-Presentation.pptx
│   │   ├── Executive-Presentation.pdf
│   │   ├── Technical-Deep-Dive.pptx
│   │   └── Demo-Slides.pptx
│   │
│   ├── Proposals/
│   │   ├── Formal-Proposal-v1.pdf
│   │   ├── Formal-Proposal-v2.pdf (if revised)
│   │   ├── Executive-Summary-One-Pager.pdf
│   │   └── Pricing-Sheet.pdf
│   │
│   ├── Demonstrations/
│   │   ├── Demo-Script.md
│   │   ├── Demo-Video.mp4 (backup)
│   │   └── Sample-Data/ (folder with demo files)
│   │
│   ├── Supporting-Docs/
│   │   ├── ROI-Calculator.xlsx
│   │   ├── Case-Studies.pdf
│   │   ├── Client-Testimonials.pdf
│   │   ├── Technical-Specifications.pdf
│   │   ├── Security-White-Paper.pdf
│   │   ├── FAQ.pdf
│   │   └── Company-Profile.pdf
│   │
│   └── Leave-Behinds/
│       ├── One-Pager-Executive-Summary.pdf
│       ├── Product-Feature-Sheet.pdf
│       └── Quick-Reference-Guide.pdf
│
├── 04-Contracts-Legal/
│   ├── Templates/
│   │   ├── Master-Service-Agreement-Template.docx
│   │   ├── Statement-of-Work-Template.docx
│   │   ├── NDA-Template.docx
│   │   ├── SLA-Template.docx
│   │   ├── Data-Processing-Agreement-Template.docx
│   │   └── Change-Order-Template.docx
│   │
│   ├── Client-Specific/
│   │   ├── [ClientName]-MSA-Draft.docx
│   │   ├── [ClientName]-SOW-Draft.docx
│   │   ├── [ClientName]-NDA.docx
│   │   └── [ClientName]-Final-Contract-Signed.pdf
│   │
│   └── Legal-Reference/
│       ├── Industry-Standard-Terms.md
│       ├── Legal-Checklist.md
│       └── Contract-Negotiation-Notes.md
│
├── 05-Worksheets/
│   ├── BATNA-Worksheet-Completed.md
│   ├── Pricing-Strategy-Worksheet-Completed.xlsx
│   ├── Stakeholder-Analysis-Worksheet-Completed.md
│   ├── Value-Proposition-Worksheet-Completed.md
│   ├── ROI-Calculation-Worksheet.xlsx
│   └── Concession-Tracker.xlsx
│
├── 06-Meeting-Materials/
│   ├── Pre-Meeting/
│   │   ├── Meeting-Agenda.md
│   │   ├── Team-Briefing.md
│   │   ├── Role-Assignments.md
│   │   └── Pre-Meeting-Checklist.md
│   │
│   ├── During-Meeting/
│   │   ├── Meeting-Notes-Template.md
│   │   ├── Action-Items-Tracker.md
│   │   └── Decision-Log.md
│   │
│   └── Post-Meeting/
│       ├── Meeting-Summary-Email-Template.md
│       ├── Follow-Up-Plan.md
│       ├── Next-Steps-Tracker.md
│       └── Meeting-Debrief-Notes.md
│
├── 07-Communication/
│   ├── Email-Templates/
│   │   ├── Initial-Outreach-Template.md
│   │   ├── Meeting-Request-Template.md
│   │   ├── Proposal-Cover-Email-Template.md
│   │   ├── Follow-Up-Email-Template.md
│   │   ├── Thank-You-Email-Template.md
│   │   ├── Contract-Send-Email-Template.md
│   │   └── Welcome-Onboard-Email-Template.md
│   │
│   ├── Communication-Log/
│   │   ├── Email-History.md
│   │   ├── Call-Notes.md
│   │   └── Chat-Transcripts.md
│   │
│   └── Scripts/
│       ├── Phone-Call-Script.md
│       ├── Objection-Handling-Script.md
│       ├── Closing-Script.md
│       └── Discovery-Questions-Script.md
│
├── 08-Financial/
│   ├── Cost-Analysis/
│   │   ├── Development-Cost-Breakdown.xlsx
│   │   ├── Infrastructure-Costs.xlsx
│   │   ├── Support-Cost-Estimates.xlsx
│   │   └── Total-Cost-Summary.xlsx
│   │
│   ├── Pricing-Models/
│   │   ├── Tier-Pricing-Calculator.xlsx
│   │   ├── Custom-Pricing-Scenarios.xlsx
│   │   └── Discount-Structure.xlsx
│   │
│   └── Invoicing/
│       ├── Invoice-Template.xlsx
│       ├── Payment-Schedule.md
│       └── Payment-Terms.md
│
├── 09-Implementation/
│   ├── Project-Plan/
│   │   ├── Implementation-Timeline-Gantt.xlsx
│   │   ├── Milestone-Definitions.md
│   │   ├── RACI-Matrix.xlsx
│   │   └── Resource-Allocation.md
│   │
│   ├── Onboarding/
│   │   ├── Onboarding-Checklist.md
│   │   ├── Kickoff-Meeting-Agenda.md
│   │   ├── Training-Plan.md
│   │   └── Welcome-Packet.pdf
│   │
│   └── Documentation/
│       ├── User-Guide.pdf
│       ├── Admin-Guide.pdf
│       ├── Technical-Documentation.pdf
│       └── FAQ-Support.pdf
│
├── 10-Internal/
│   ├── Team-Coordination/
│   │   ├── Team-Roles-Responsibilities.md
│   │   ├── Internal-Meeting-Notes.md
│   │   └── Decision-Record.md
│   │
│   ├── Deal-Tracking/
│   │   ├── Deal-Pipeline-Tracker.xlsx
│   │   ├── Probability-Assessment.md
│   │   └── Revenue-Forecast.xlsx
│   │
│   └── Lessons-Learned/
│       ├── What-Worked.md
│       ├── What-Didnt-Work.md
│       ├── Improvements-for-Next-Time.md
│       └── Negotiation-Debrief.md
│
├── 11-Reference/
│   ├── Business-Roadmap-Personal.md (your existing file)
│   ├── Negotiation-Preparation-Master-Document.md (your existing file)
│   ├── File-and-Folder-Structure-Guide.md (this file)
│   ├── Best-Practices-Library.md
│   └── Industry-Resources.md
│
└── 12-Archive/
    ├── Old-Versions/ (superseded documents)
    ├── Rejected-Proposals/
    └── Reference-Only/ (historical material)
```

---

# COMPLETE FILE INVENTORY

## Category 1: Research Files (20 files)

### Client Research (6 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 1 | Company-Profile.md | Markdown | 01-Research/Client-Research/ | Company background, size, industry, financials |
| 2 | Stakeholder-Analysis.md | Markdown | 01-Research/Client-Research/ | Key decision makers, roles, priorities |
| 3 | Pain-Points-Analysis.md | Markdown | 01-Research/Client-Research/ | Their problems, current costs, urgency |
| 4 | Budget-Timeline-Research.md | Markdown | 01-Research/Client-Research/ | Budget range, fiscal cycle, decision timeline |
| 5 | Technical-Requirements.md | Markdown | 01-Research/Client-Research/ | Integration needs, security, compliance |
| 6 | Previous-Interactions-Log.md | Markdown | 01-Research/Client-Research/ | All emails, calls, meetings documented |

### Market Research (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 7 | Competitor-Analysis.md | Markdown | 01-Research/Market-Research/ | Who else they might consider, pricing, features |
| 8 | Market-Pricing-Benchmark.md | Markdown | 01-Research/Market-Research/ | Industry standard rates, comparable solutions |
| 9 | Industry-Trends.md | Markdown | 01-Research/Market-Research/ | Sector trends, challenges, opportunities |
| 10 | Alternative-Solutions-Comparison.md | Markdown | 01-Research/Market-Research/ | DIY, in-house, competitors, status quo |

### Internal Analysis (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 11 | Cost-Breakdown.xlsx | Excel | 01-Research/Internal-Analysis/ | Your actual costs (dev, hosting, support) |
| 12 | BATNA-Analysis.md | Markdown | 01-Research/Internal-Analysis/ | Your backup plan, their backup plan |
| 13 | Our-Capabilities-Inventory.md | Markdown | 01-Research/Internal-Analysis/ | What you can deliver, team skills, portfolio |
| 14 | Leverage-Assessment.md | Markdown | 01-Research/Internal-Analysis/ | Your advantages, their advantages, power dynamics |

### Reference Documents (6 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 15 | Business-Roadmap-Personal.md | Markdown | 11-Reference/ | Your original transcription analysis (existing) |
| 16 | Negotiation-Preparation-Master-Document.md | Markdown | 11-Reference/ | Comprehensive guide (existing) |
| 17 | File-and-Folder-Structure-Guide.md | Markdown | 11-Reference/ | This document |
| 18 | Best-Practices-Library.md | Markdown | 11-Reference/ | Negotiation tips, techniques, frameworks |
| 19 | Industry-Resources.md | Markdown | 11-Reference/ | Links, articles, research papers |
| 20 | Source-Transcripts/ | Folder | 11-Reference/ | 1.md, 2.md, 3.md (your original audio transcripts) |

---

## Category 2: Strategy Files (6 files)

| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 21 | Negotiation-Playbook.md | Markdown | 02-Strategy/ | Master strategy: anchoring, BATNA, walkaway |
| 22 | Pricing-Strategy.md | Markdown | 02-Strategy/ | Tier structure, anchor price, concession plan |
| 23 | Concession-Plan.md | Markdown | 02-Strategy/ | What to give up, when, in exchange for what |
| 24 | Objection-Response-Scripts.md | Markdown | 02-Strategy/ | Pre-written responses to common objections |
| 25 | Value-Proposition.md | Markdown | 02-Strategy/ | Your unique value, ROI story, differentiation |
| 26 | Deal-Structure-Options.md | Markdown | 02-Strategy/ | Payment terms, subscription vs flat, phasing |

---

## Category 3: Client-Facing Materials (25+ files)

### Presentations (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 27 | Executive-Presentation.pptx | PowerPoint | 03-Materials-for-Client/Presentations/ | Main pitch deck (editable) |
| 28 | Executive-Presentation.pdf | PDF | 03-Materials-for-Client/Presentations/ | Main pitch deck (shareable) |
| 29 | Technical-Deep-Dive.pptx | PowerPoint | 03-Materials-for-Client/Presentations/ | For technical stakeholders |
| 30 | Demo-Slides.pptx | PowerPoint | 03-Materials-for-Client/Presentations/ | Product demo walkthrough |

### Proposals (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 31 | Formal-Proposal-v1.pdf | PDF | 03-Materials-for-Client/Proposals/ | Detailed 10-20 page proposal |
| 32 | Formal-Proposal-v2.pdf | PDF | 03-Materials-for-Client/Proposals/ | Revised after negotiation |
| 33 | Executive-Summary-One-Pager.pdf | PDF | 03-Materials-for-Client/Proposals/ | 1-page overview for busy execs |
| 34 | Pricing-Sheet.pdf | PDF | 03-Materials-for-Client/Proposals/ | Clear tier pricing table |

### Demonstrations (3+ files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 35 | Demo-Script.md | Markdown | 03-Materials-for-Client/Demonstrations/ | Step-by-step demo walkthrough |
| 36 | Demo-Video.mp4 | Video | 03-Materials-for-Client/Demonstrations/ | Backup if live demo fails |
| 37 | Sample-Data/ | Folder | 03-Materials-for-Client/Demonstrations/ | Sample CSV/Excel files for demo |

### Supporting Documents (7 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 38 | ROI-Calculator.xlsx | Excel | 03-Materials-for-Client/Supporting-Docs/ | Interactive ROI calculator |
| 39 | Case-Studies.pdf | PDF | 03-Materials-for-Client/Supporting-Docs/ | Success stories from other clients |
| 40 | Client-Testimonials.pdf | PDF | 03-Materials-for-Client/Supporting-Docs/ | Quotes from satisfied clients |
| 41 | Technical-Specifications.pdf | PDF | 03-Materials-for-Client/Supporting-Docs/ | Detailed tech specs |
| 42 | Security-White-Paper.pdf | PDF | 03-Materials-for-Client/Supporting-Docs/ | Security measures, compliance |
| 43 | FAQ.pdf | PDF | 03-Materials-for-Client/Supporting-Docs/ | Common questions answered |
| 44 | Company-Profile.pdf | PDF | 03-Materials-for-Client/Supporting-Docs/ | Your company background |

### Leave-Behinds (3 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 45 | One-Pager-Executive-Summary.pdf | PDF | 03-Materials-for-Client/Leave-Behinds/ | Single page to leave after meeting |
| 46 | Product-Feature-Sheet.pdf | PDF | 03-Materials-for-Client/Leave-Behinds/ | Feature list for reference |
| 47 | Quick-Reference-Guide.pdf | PDF | 03-Materials-for-Client/Leave-Behinds/ | How to use the product basics |

---

## Category 4: Contracts & Legal (13 files)

### Templates (6 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 48 | Master-Service-Agreement-Template.docx | Word | 04-Contracts-Legal/Templates/ | General terms template |
| 49 | Statement-of-Work-Template.docx | Word | 04-Contracts-Legal/Templates/ | Project-specific scope template |
| 50 | NDA-Template.docx | Word | 04-Contracts-Legal/Templates/ | Confidentiality agreement template |
| 51 | SLA-Template.docx | Word | 04-Contracts-Legal/Templates/ | Service level agreement template |
| 52 | Data-Processing-Agreement-Template.docx | Word | 04-Contracts-Legal/Templates/ | Data handling template |
| 53 | Change-Order-Template.docx | Word | 04-Contracts-Legal/Templates/ | Scope change template |

### Client-Specific (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 54 | [ClientName]-MSA-Draft.docx | Word | 04-Contracts-Legal/Client-Specific/ | Customized MSA for this client |
| 55 | [ClientName]-SOW-Draft.docx | Word | 04-Contracts-Legal/Client-Specific/ | Customized SOW for this project |
| 56 | [ClientName]-NDA.docx | Word | 04-Contracts-Legal/Client-Specific/ | Signed NDA |
| 57 | [ClientName]-Final-Contract-Signed.pdf | PDF | 04-Contracts-Legal/Client-Specific/ | Fully executed contract |

### Legal Reference (3 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 58 | Industry-Standard-Terms.md | Markdown | 04-Contracts-Legal/Legal-Reference/ | Benchmark contract terms |
| 59 | Legal-Checklist.md | Markdown | 04-Contracts-Legal/Legal-Reference/ | What to include in contracts |
| 60 | Contract-Negotiation-Notes.md | Markdown | 04-Contracts-Legal/Legal-Reference/ | Notes on contract discussions |

---

## Category 5: Worksheets (6 files)

| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 61 | BATNA-Worksheet-Completed.md | Markdown | 05-Worksheets/ | Your BATNA analysis filled out |
| 62 | Pricing-Strategy-Worksheet-Completed.xlsx | Excel | 05-Worksheets/ | Pricing calculations completed |
| 63 | Stakeholder-Analysis-Worksheet-Completed.md | Markdown | 05-Worksheets/ | Stakeholder mapping filled out |
| 64 | Value-Proposition-Worksheet-Completed.md | Markdown | 05-Worksheets/ | ROI calculation filled out |
| 65 | ROI-Calculation-Worksheet.xlsx | Excel | 05-Worksheets/ | Working ROI calculator |
| 66 | Concession-Tracker.xlsx | Excel | 05-Worksheets/ | Track concessions during negotiation |

---

## Category 6: Meeting Materials (12 files)

### Pre-Meeting (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 67 | Meeting-Agenda.md | Markdown | 06-Meeting-Materials/Pre-Meeting/ | Agenda to send before meeting |
| 68 | Team-Briefing.md | Markdown | 06-Meeting-Materials/Pre-Meeting/ | Internal team alignment |
| 69 | Role-Assignments.md | Markdown | 06-Meeting-Materials/Pre-Meeting/ | Who does what in meeting |
| 70 | Pre-Meeting-Checklist.md | Markdown | 06-Meeting-Materials/Pre-Meeting/ | Final prep checklist |

### During Meeting (3 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 71 | Meeting-Notes-Template.md | Markdown | 06-Meeting-Materials/During-Meeting/ | Template for taking notes |
| 72 | Action-Items-Tracker.md | Markdown | 06-Meeting-Materials/During-Meeting/ | Track commitments made |
| 73 | Decision-Log.md | Markdown | 06-Meeting-Materials/During-Meeting/ | Log agreements reached |

### Post-Meeting (5 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 74 | Meeting-Summary-Email-Template.md | Markdown | 06-Meeting-Materials/Post-Meeting/ | Follow-up email template |
| 75 | Follow-Up-Plan.md | Markdown | 06-Meeting-Materials/Post-Meeting/ | Next steps and timeline |
| 76 | Next-Steps-Tracker.md | Markdown | 06-Meeting-Materials/Post-Meeting/ | Action items with deadlines |
| 77 | Meeting-Debrief-Notes.md | Markdown | 06-Meeting-Materials/Post-Meeting/ | Internal debrief notes |
| 78 | Negotiation-Round-Summary.md | Markdown | 06-Meeting-Materials/Post-Meeting/ | Summary of negotiation progress |

---

## Category 7: Communication (13+ files)

### Email Templates (7 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 79 | Initial-Outreach-Template.md | Markdown | 07-Communication/Email-Templates/ | First contact email |
| 80 | Meeting-Request-Template.md | Markdown | 07-Communication/Email-Templates/ | Request for meeting |
| 81 | Proposal-Cover-Email-Template.md | Markdown | 07-Communication/Email-Templates/ | Email when sending proposal |
| 82 | Follow-Up-Email-Template.md | Markdown | 07-Communication/Email-Templates/ | General follow-up |
| 83 | Thank-You-Email-Template.md | Markdown | 07-Communication/Email-Templates/ | Post-meeting thank you |
| 84 | Contract-Send-Email-Template.md | Markdown | 07-Communication/Email-Templates/ | When sending contract |
| 85 | Welcome-Onboard-Email-Template.md | Markdown | 07-Communication/Email-Templates/ | After contract signed |

### Communication Log (3 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 86 | Email-History.md | Markdown | 07-Communication/Communication-Log/ | Log of all emails |
| 87 | Call-Notes.md | Markdown | 07-Communication/Communication-Log/ | Log of all phone calls |
| 88 | Chat-Transcripts.md | Markdown | 07-Communication/Communication-Log/ | WhatsApp, Slack, etc. |

### Scripts (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 89 | Phone-Call-Script.md | Markdown | 07-Communication/Scripts/ | What to say on calls |
| 90 | Objection-Handling-Script.md | Markdown | 07-Communication/Scripts/ | Responses to objections |
| 91 | Closing-Script.md | Markdown | 07-Communication/Scripts/ | How to ask for the business |
| 92 | Discovery-Questions-Script.md | Markdown | 07-Communication/Scripts/ | Questions to ask client |

---

## Category 8: Financial Files (9+ files)

### Cost Analysis (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 93 | Development-Cost-Breakdown.xlsx | Excel | 08-Financial/Cost-Analysis/ | Dev hours, rates, total |
| 94 | Infrastructure-Costs.xlsx | Excel | 08-Financial/Cost-Analysis/ | Hosting, tokens, storage |
| 95 | Support-Cost-Estimates.xlsx | Excel | 08-Financial/Cost-Analysis/ | Ongoing support costs |
| 96 | Total-Cost-Summary.xlsx | Excel | 08-Financial/Cost-Analysis/ | All costs rolled up |

### Pricing Models (3 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 97 | Tier-Pricing-Calculator.xlsx | Excel | 08-Financial/Pricing-Models/ | S/M/L tier calculations |
| 98 | Custom-Pricing-Scenarios.xlsx | Excel | 08-Financial/Pricing-Models/ | "What if" scenarios |
| 99 | Discount-Structure.xlsx | Excel | 08-Financial/Pricing-Models/ | When to discount, how much |

### Invoicing (3 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 100 | Invoice-Template.xlsx | Excel | 08-Financial/Invoicing/ | Invoice format |
| 101 | Payment-Schedule.md | Markdown | 08-Financial/Invoicing/ | When payments are due |
| 102 | Payment-Terms.md | Markdown | 08-Financial/Invoicing/ | Net 30, late fees, etc. |

---

## Category 9: Implementation Files (12+ files)

### Project Plan (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 103 | Implementation-Timeline-Gantt.xlsx | Excel | 09-Implementation/Project-Plan/ | Visual timeline |
| 104 | Milestone-Definitions.md | Markdown | 09-Implementation/Project-Plan/ | What each milestone means |
| 105 | RACI-Matrix.xlsx | Excel | 09-Implementation/Project-Plan/ | Who's Responsible/Accountable/Consulted/Informed |
| 106 | Resource-Allocation.md | Markdown | 09-Implementation/Project-Plan/ | Team assignments |

### Onboarding (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 107 | Onboarding-Checklist.md | Markdown | 09-Implementation/Onboarding/ | Steps to onboard client |
| 108 | Kickoff-Meeting-Agenda.md | Markdown | 09-Implementation/Onboarding/ | First project meeting |
| 109 | Training-Plan.md | Markdown | 09-Implementation/Onboarding/ | How to train their team |
| 110 | Welcome-Packet.pdf | PDF | 09-Implementation/Onboarding/ | Welcome document for client |

### Documentation (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 111 | User-Guide.pdf | PDF | 09-Implementation/Documentation/ | End-user manual |
| 112 | Admin-Guide.pdf | PDF | 09-Implementation/Documentation/ | Admin/power user manual |
| 113 | Technical-Documentation.pdf | PDF | 09-Implementation/Documentation/ | Technical specs, API docs |
| 114 | FAQ-Support.pdf | PDF | 09-Implementation/Documentation/ | Common Q&A |

---

## Category 10: Internal Files (9 files)

### Team Coordination (3 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 115 | Team-Roles-Responsibilities.md | Markdown | 10-Internal/Team-Coordination/ | Who does what internally |
| 116 | Internal-Meeting-Notes.md | Markdown | 10-Internal/Team-Coordination/ | Internal discussion notes |
| 117 | Decision-Record.md | Markdown | 10-Internal/Team-Coordination/ | Key decisions made |

### Deal Tracking (3 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 118 | Deal-Pipeline-Tracker.xlsx | Excel | 10-Internal/Deal-Tracking/ | Track deal progress |
| 119 | Probability-Assessment.md | Markdown | 10-Internal/Deal-Tracking/ | % chance of closing |
| 120 | Revenue-Forecast.xlsx | Excel | 10-Internal/Deal-Tracking/ | Projected revenue |

### Lessons Learned (4 files)
| # | File Name | Format | Location | Purpose |
|---|-----------|--------|----------|---------|
| 121 | What-Worked.md | Markdown | 10-Internal/Lessons-Learned/ | Successes to repeat |
| 122 | What-Didnt-Work.md | Markdown | 10-Internal/Lessons-Learned/ | Mistakes to avoid |
| 123 | Improvements-for-Next-Time.md | Markdown | 10-Internal/Lessons-Learned/ | Process improvements |
| 124 | Negotiation-Debrief.md | Markdown | 10-Internal/Lessons-Learned/ | Post-negotiation analysis |

---

# TOTAL FILE COUNT: **124+ files** across 12 major folders

---

# FILE CREATION CHECKLIST

## Priority 1: MUST CREATE BEFORE NEGOTIATION (Critical - 30 files)

### Research (10 files)
- [ ] Company-Profile.md
- [ ] Stakeholder-Analysis.md
- [ ] Pain-Points-Analysis.md
- [ ] Budget-Timeline-Research.md
- [ ] Competitor-Analysis.md
- [ ] Market-Pricing-Benchmark.md
- [ ] Cost-Breakdown.xlsx
- [ ] BATNA-Analysis.md
- [ ] Leverage-Assessment.md
- [ ] Previous-Interactions-Log.md

### Strategy (6 files)
- [ ] Negotiation-Playbook.md
- [ ] Pricing-Strategy.md
- [ ] Concession-Plan.md
- [ ] Objection-Response-Scripts.md
- [ ] Value-Proposition.md
- [ ] Deal-Structure-Options.md

### Client Materials (8 files)
- [ ] Executive-Presentation.pptx
- [ ] Executive-Presentation.pdf
- [ ] Formal-Proposal-v1.pdf
- [ ] Pricing-Sheet.pdf
- [ ] Demo-Script.md
- [ ] ROI-Calculator.xlsx
- [ ] Executive-Summary-One-Pager.pdf
- [ ] FAQ.pdf

### Meeting (4 files)
- [ ] Meeting-Agenda.md
- [ ] Team-Briefing.md
- [ ] Role-Assignments.md
- [ ] Pre-Meeting-Checklist.md

### Financial (2 files)
- [ ] Total-Cost-Summary.xlsx
- [ ] Tier-Pricing-Calculator.xlsx

---

## Priority 2: CREATE DURING NEGOTIATION (Important - 15 files)

### Meeting Management
- [ ] Meeting-Notes-Template.md (use during meeting)
- [ ] Action-Items-Tracker.md
- [ ] Decision-Log.md
- [ ] Concession-Tracker.xlsx

### Follow-up
- [ ] Meeting-Summary-Email-Template.md
- [ ] Follow-Up-Plan.md
- [ ] Next-Steps-Tracker.md
- [ ] Meeting-Debrief-Notes.md

### Contracts (customize as needed)
- [ ] [ClientName]-MSA-Draft.docx
- [ ] [ClientName]-SOW-Draft.docx
- [ ] [ClientName]-NDA.docx

### Communication
- [ ] Email-History.md (ongoing log)
- [ ] Call-Notes.md (ongoing log)
- [ ] Follow-Up-Email-Template.md
- [ ] Thank-You-Email-Template.md

---

## Priority 3: CREATE AFTER AGREEMENT (Post-Close - 20 files)

### Contracts
- [ ] [ClientName]-Final-Contract-Signed.pdf
- [ ] Payment-Schedule.md
- [ ] Invoice-Template.xlsx

### Implementation
- [ ] Implementation-Timeline-Gantt.xlsx
- [ ] Milestone-Definitions.md
- [ ] RACI-Matrix.xlsx
- [ ] Onboarding-Checklist.md
- [ ] Kickoff-Meeting-Agenda.md
- [ ] Training-Plan.md
- [ ] Welcome-Packet.pdf

### Documentation
- [ ] User-Guide.pdf
- [ ] Admin-Guide.pdf
- [ ] Technical-Documentation.pdf
- [ ] FAQ-Support.pdf

### Communication
- [ ] Welcome-Onboard-Email-Template.md
- [ ] Contract-Send-Email-Template.md

### Internal
- [ ] What-Worked.md
- [ ] What-Didnt-Work.md
- [ ] Improvements-for-Next-Time.md
- [ ] Negotiation-Debrief.md

---

## Priority 4: OPTIONAL/SUPPORTING (Nice to Have - 30+ files)

### Supporting Materials
- [ ] Technical-Deep-Dive.pptx
- [ ] Demo-Video.mp4
- [ ] Case-Studies.pdf
- [ ] Client-Testimonials.pdf
- [ ] Technical-Specifications.pdf
- [ ] Security-White-Paper.pdf
- [ ] Company-Profile.pdf
- [ ] Product-Feature-Sheet.pdf
- [ ] Quick-Reference-Guide.pdf

### Templates (for future use)
- [ ] All 6 contract templates
- [ ] All 7 email templates
- [ ] All 4 communication scripts

### Analysis
- [ ] Industry-Trends.md
- [ ] Alternative-Solutions-Comparison.md
- [ ] Development-Cost-Breakdown.xlsx
- [ ] Infrastructure-Costs.xlsx
- [ ] Support-Cost-Estimates.xlsx
- [ ] Custom-Pricing-Scenarios.xlsx
- [ ] Discount-Structure.xlsx

### Internal Tracking
- [ ] Deal-Pipeline-Tracker.xlsx
- [ ] Probability-Assessment.md
- [ ] Revenue-Forecast.xlsx
- [ ] Team-Roles-Responsibilities.md
- [ ] Internal-Meeting-Notes.md
- [ ] Decision-Record.md

---

# NAMING CONVENTIONS

## General Rules

### Files
```
✓ GOOD:
- Company-Profile.md
- ROI-Calculator.xlsx
- Executive-Presentation-v1.pptx
- 2025-10-16-Meeting-Notes.md

✗ BAD:
- company profile.md (spaces, no capitals)
- roi calc.xlsx (abbreviations unclear)
- pres final FINAL v2.pptx (messy versioning)
- notes.md (not descriptive)
```

### Folders
```
✓ GOOD:
- 01-Research/
- Client-Specific/
- Email-Templates/

✗ BAD:
- research/ (not numbered)
- client stuff/ (informal)
- emails/ (not specific)
```

### Conventions
```
1. Use Title-Case-With-Hyphens
2. Number main folders (01-, 02-, etc.) for sorting
3. Date format: YYYY-MM-DD (e.g., 2025-10-16)
4. Version format: v1, v2, v3 (not final, final2, etc.)
5. Client name in brackets: [ClientName]-Document.docx
6. No spaces in file names (use hyphens)
7. Be descriptive (not just "doc.pdf")
```

---

# FILE TEMPLATES BY CATEGORY

## Template 1: Research Document Template

```markdown
# [DOCUMENT TITLE]

**Client:** [Client Name]
**Date Created:** YYYY-MM-DD
**Last Updated:** YYYY-MM-DD
**Owner:** [Your Name]
**Status:** Draft / In Progress / Complete

---

## Summary
[Brief overview of findings]

---

## Detailed Analysis

### Section 1: [Topic]
[Content]

### Section 2: [Topic]
[Content]

---

## Key Findings
- Finding 1
- Finding 2
- Finding 3

---

## Implications for Negotiation
[How this research impacts your strategy]

---

## Sources
- Source 1: [URL or reference]
- Source 2: [URL or reference]

---

## Next Steps
- [ ] Action 1
- [ ] Action 2
```

---

## Template 2: Strategy Document Template

```markdown
# [STRATEGY DOCUMENT TITLE]

**Date:** YYYY-MM-DD
**Version:** v1.0
**Status:** Draft / Final

---

## Objective
[What you're trying to achieve]

---

## Current Situation
[Where things stand now]

---

## Strategy

### Approach 1: [Name]
**Description:** [What it is]
**When to use:** [Conditions]
**Expected outcome:** [Result]
**Risk:** [What could go wrong]

### Approach 2: [Name]
**Description:**
**When to use:**
**Expected outcome:**
**Risk:**

---

## Recommended Action
[Your primary recommendation]

---

## Contingency Plans
**If [scenario], then [response]**

---

## Success Metrics
- Metric 1: [How to measure]
- Metric 2: [How to measure]
```

---

## Template 3: Meeting Document Template

```markdown
# [MEETING TITLE]

**Date:** YYYY-MM-DD
**Time:** HH:MM - HH:MM
**Location:** [In-person / Virtual - Platform]
**Duration:** [X] minutes

---

## Attendees

**From Client:**
- Name (Title, Role)
- Name (Title, Role)

**From Our Team:**
- Name (Title, Role)
- Name (Title, Role)

---

## Agenda
1. Item 1 ([X] min)
2. Item 2 ([X] min)
3. Item 3 ([X] min)

---

## Meeting Notes

### Topic 1: [Name]
- Discussion point 1
- Discussion point 2
- **Decision:** [What was decided]

### Topic 2: [Name]
- Discussion point 1
- **Action:** [Who does what by when]

---

## Decisions Made
1. Decision 1
2. Decision 2

---

## Action Items

| # | Action | Owner | Due Date | Status |
|---|--------|-------|----------|--------|
| 1 | [Task] | [Name] | YYYY-MM-DD | Not Started |
| 2 | [Task] | [Name] | YYYY-MM-DD | In Progress |

---

## Next Steps
- [ ] Step 1 (Owner: [Name], Due: [Date])
- [ ] Step 2 (Owner: [Name], Due: [Date])

---

## Follow-up Required
- [ ] Send meeting summary
- [ ] Send proposal
- [ ] Schedule next meeting
```

---

## Template 4: Email Template Format

```markdown
# [EMAIL TEMPLATE NAME]

**Use Case:** [When to use this email]
**Tone:** Professional / Friendly / Formal
**Timing:** [When to send - e.g., within 24 hours of meeting]

---

## Subject Line Options
1. [Subject option 1]
2. [Subject option 2]
3. [Subject option 3]

---

## Email Body

---

**Subject:** [Choose from above]

Hi [First Name],

[Opening - personalized greeting or reference to recent interaction]

[Body Paragraph 1 - Main point]

[Body Paragraph 2 - Supporting information or next steps]

[Body Paragraph 3 - Call to action]

[Closing]

Best regards,
[Your Name]
[Your Title]
[Company Name]
[Contact Information]

---

## Attachments (if any)
- [ ] Attachment 1
- [ ] Attachment 2

---

## Notes
[Any special considerations when using this template]
```

---

## Template 5: Worksheet Template

```markdown
# [WORKSHEET NAME]

**Date Completed:** YYYY-MM-DD
**Completed By:** [Name]
**Version:** v1.0

---

## Instructions
[How to fill out this worksheet]

---

## Section 1: [Topic]

**Question 1:** [Question]
**Answer:** [Your answer]

**Question 2:** [Question]
**Answer:** [Your answer]

---

## Section 2: [Topic]

| Item | Value | Notes |
|------|-------|-------|
| Item 1 | [Value] | [Notes] |
| Item 2 | [Value] | [Notes] |

---

## Analysis

### Findings:
- Finding 1
- Finding 2

### Implications:
- Implication 1
- Implication 2

---

## Recommended Actions
1. Action 1
2. Action 2

---

## Review & Approval
- [ ] Self-review complete
- [ ] Peer review complete (Reviewer: [Name], Date: [Date])
- [ ] Approved for use
```

---

# QUICK START GUIDE

## Step 1: Create Folder Structure (5 minutes)

Run these commands in your terminal (Windows):

```batch
cd "c:\Users\kyrian\Documents\Negociation-Personal"

mkdir 01-Research\Client-Research
mkdir 01-Research\Market-Research
mkdir 01-Research\Internal-Analysis
mkdir 02-Strategy
mkdir 03-Materials-for-Client\Presentations
mkdir 03-Materials-for-Client\Proposals
mkdir 03-Materials-for-Client\Demonstrations
mkdir 03-Materials-for-Client\Supporting-Docs
mkdir 03-Materials-for-Client\Leave-Behinds
mkdir 04-Contracts-Legal\Templates
mkdir 04-Contracts-Legal\Client-Specific
mkdir 04-Contracts-Legal\Legal-Reference
mkdir 05-Worksheets
mkdir 06-Meeting-Materials\Pre-Meeting
mkdir 06-Meeting-Materials\During-Meeting
mkdir 06-Meeting-Materials\Post-Meeting
mkdir 07-Communication\Email-Templates
mkdir 07-Communication\Communication-Log
mkdir 07-Communication\Scripts
mkdir 08-Financial\Cost-Analysis
mkdir 08-Financial\Pricing-Models
mkdir 08-Financial\Invoicing
mkdir 09-Implementation\Project-Plan
mkdir 09-Implementation\Onboarding
mkdir 09-Implementation\Documentation
mkdir 10-Internal\Team-Coordination
mkdir 10-Internal\Deal-Tracking
mkdir 10-Internal\Lessons-Learned
mkdir 11-Reference
mkdir 12-Archive\Old-Versions
mkdir 12-Archive\Rejected-Proposals
mkdir 12-Archive\Reference-Only
```

---

## Step 2: Move Existing Files (2 minutes)

```batch
# Move your existing files to the Reference folder
move "Business Roadmap Personal.md" "11-Reference\"
move "Negotiation Preparation Master Document.md" "11-Reference\"
move "File and Folder Structure Guide.md" "11-Reference\"

# If you have the source transcripts:
# mkdir "11-Reference\Source-Transcripts"
# move "1.md" "11-Reference\Source-Transcripts\"
# move "2.md" "11-Reference\Source-Transcripts\"
# move "3.md" "11-Reference\Source-Transcripts\"
```

---

## Step 3: Create Priority 1 Files (Start Here)

### Immediate (Today):
1. Create `01-Research/Client-Research/Company-Profile.md`
2. Create `01-Research/Client-Research/Stakeholder-Analysis.md`
3. Create `02-Strategy/Negotiation-Playbook.md`
4. Create `02-Strategy/Pricing-Strategy.md`
5. Create `08-Financial/Total-Cost-Summary.xlsx`

### This Week:
6. Create `03-Materials-for-Client/Presentations/Executive-Presentation.pptx`
7. Create `03-Materials-for-Client/Proposals/Formal-Proposal-v1.pdf`
8. Create `03-Materials-for-Client/Supporting-Docs/ROI-Calculator.xlsx`
9. Create `06-Meeting-Materials/Pre-Meeting/Meeting-Agenda.md`
10. Create `07-Communication/Email-Templates/` (all templates)

---

## Step 4: Maintain Organization (Ongoing)

### Daily:
- [ ] Update Communication-Log with all interactions
- [ ] Update Action-Items-Tracker after any commitment
- [ ] Version control important documents (v1, v2, etc.)

### Weekly:
- [ ] Review and update Deal-Pipeline-Tracker
- [ ] Archive old versions to 12-Archive/Old-Versions/
- [ ] Clean up duplicate files

### After Negotiation:
- [ ] Complete all Lessons-Learned documents
- [ ] Archive deal folder for reference
- [ ] Update templates based on learnings

---

# BENEFITS OF THIS STRUCTURE

## Organization Benefits
✅ **Find anything in seconds** - Clear folder hierarchy
✅ **No duplicate work** - One source of truth for each document
✅ **Easy collaboration** - Team knows where to find/put files
✅ **Version control** - Clear versioning system
✅ **Professionalism** - Organized structure impresses clients

## Process Benefits
✅ **Checklist-driven** - Know what to create and when
✅ **Template-based** - Don't start from scratch
✅ **Reusable** - Use this structure for future deals
✅ **Scalable** - Works for 1 client or 100 clients
✅ **Audit-ready** - Easy to review decisions made

## Negotiation Benefits
✅ **Prepared** - All materials ready and accessible
✅ **Confident** - Know you haven't forgotten anything
✅ **Responsive** - Quickly find info when client asks
✅ **Professional** - Organized materials build credibility
✅ **Learning** - Capture lessons for continuous improvement

---

# CUSTOMIZATION TIPS

## For Smaller Deals:
- Skip folders 09-Implementation and 12-Archive
- Combine Research folders into one
- Reduce number of email templates
- Focus on Priority 1 files only

## For Larger/Complex Deals:
- Add subfolders by stakeholder group
- Create separate folders per negotiation round
- Add more detailed tracking worksheets
- Expand Legal section with compliance docs

## For Multiple Clients:
- Duplicate this structure for each client
- Create master folder: `All-Clients/[ClientName]/[this structure]`
- Use shared templates across all clients
- Centralize lessons-learned across deals

---

# MAINTENANCE SCHEDULE

## Daily (2 minutes):
- Log all communications
- Update action items

## Weekly (15 minutes):
- Review file organization
- Archive old versions
- Update deal tracker

## After Each Meeting (30 minutes):
- Create meeting summary
- Update all relevant docs
- Send follow-ups

## After Deal Close (1 hour):
- Complete lessons learned
- Archive entire deal folder
- Update templates
- Debrief with team

---

# TROUBLESHOOTING

## "I have too many files, it's overwhelming"
→ Start with **Priority 1 only** (30 files)
→ Create others as needed, not all upfront

## "I don't need all these folders"
→ Customize! Remove folders that don't apply
→ Keep the structure simple for your needs

## "My team isn't using the structure"
→ Brief them on where things go
→ Lead by example
→ Make it easier to follow than not follow

## "How do I keep this updated?"
→ Set calendar reminders for weekly review
→ Make it part of your workflow
→ Use checklists to ensure consistency

---

# FINAL THOUGHTS

**Good organization = Less stress = Better negotiation outcomes**

This structure may seem like overhead initially, but it will:
- Save you hours of searching for files
- Prevent you from forgetting critical tasks
- Make you look professional to clients
- Help you learn and improve with each deal
- Scale as you grow your business

**Start small, build gradually, maintain consistently.**

---

## QUICK REFERENCE: Folder Purpose Summary

| Folder | Purpose | When to Use |
|--------|---------|-------------|
| 01-Research | Know your client, market, costs | Before negotiation |
| 02-Strategy | Plan your approach | Before negotiation |
| 03-Materials-for-Client | All client-facing docs | During & after negotiation |
| 04-Contracts-Legal | Legal agreements | During & after negotiation |
| 05-Worksheets | Working documents | Throughout process |
| 06-Meeting-Materials | Meeting prep & follow-up | Around meetings |
| 07-Communication | All correspondence | Throughout process |
| 08-Financial | Costs, pricing, invoicing | Throughout process |
| 09-Implementation | Post-sale execution | After deal closes |
| 10-Internal | Team coordination, tracking | Throughout process |
| 11-Reference | Master docs, templates | Throughout process |
| 12-Archive | Old/inactive files | Ongoing cleanup |

---

**END OF FILE & FOLDER STRUCTURE GUIDE**

**Next Action:** Run Step 1 commands to create folder structure!
