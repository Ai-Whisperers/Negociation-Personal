# Personal Paraguay — Team Cheat Sheet (CEM Deal) v1.1

**Mission:** Close + deliver **v1** fast, protect IP, maximize ROI. Speak **KPI** (NPS↑, churn↓, pain‑points), not infra.

**Versión PY, simple y vendible (CEM)**
“Pasame **2 archivos de ejemplo variado** (CSV/XLSX/**Parquet**) y en menos de **2 días** te entrego un producto simple y util: Subís tu archivo y obtenés un **panel del analisis completo + Excel/CSV exportable** con **NPS, riesgo de churn, emociones y pain-points**. En formato **SaaS**. Si el producto te sirve, nos sugerís el **monto mensual** y seguimos con compromiso hasta el acuerdo formal. Si te interesa una compra definitiva tambien estamos abiertos a negociar.”

- **Important:** Define templates (Table patterns) from day-zero.

## 1) Buyer Snapshot
- Role: **Customer Experience Manager** (open-to-work, immediate according to LinkedIn). Needs **quick wins** to show upward.
- What he buys: **Pilot with visible dashboard + CSV/XLSX export**. Outcome > code.

## 2) Offer Ladder
- **Paid Pilot (10d)**
  - Input: 1 dataset (CSV/XLSX/Parquet), 3k–10k rows (flex).
  - Output: Dashboard + **export** (NPS classes, churn risk, emotions, pain‑points).
  - Acceptance = dashboard visible + **1 clean export** + signed checklist.
  - Hosting: **SaaS black‑box** (no repo). Token‑bounded + rate‑limited.
- **Monthly Tiers (caps = limits)**
  - **S:** 1 dataset/mo · token cap **T1** · SLA 48h · UI tweaks incl.
  - **M:** 3 datasets/mo · **T2** · SLA 36h · +2 feature tickets/mo.
  - **L:** 5 datasets/mo · **T3** · SLA 24h · +4 feature tickets/mo.
  - **Excess:** per‑file/per‑token/per‑ticket pricing.

## 3) Pricing & Close
- **Reverse‑anchor** (they say price first). Corridor **25–15** (currency context). **Hard‑pass <15**.
- Quick calc: **Price = (Hours×Rate) + Tokens + Hosting + Storage + Margin**.
- **Express**: +30% (scope frozen). Frame: **“v1 baseline now; enhancements later.”**

## 4) Contract Pack (send with proposal)
- **NDA + SaaS License** (hosted only), **kill‑switch**, logs/checksums, backups.
- **Scope Matrix (UI vs Feature)** → anything extra = **mini‑SOW** (priced).
- **Payment:** 50% start / 50% acceptance; **auto‑suspend exports/support after 10–15d** late (7‑day backup courtesy).
- **On‑prem/Code**: Enterprise tier only (priced); otherwise **no code handover**.

## 5) Dirty‑Play Protocol (Trigger → Counter)
- “Code/on‑prem now” → SaaS only; offer **Enterprise on‑prem** (priced).
- “Otro lo hace por menos” → keep price; **shrink scope/caps**; show cost‑sheet & ROI/tokens.
- Scope creep → stop; apply **Change Matrix**; sign mini‑SOW.
- Data/model fishing → **anonymized demos**, never weights/source.
- Security audits → provide **SOC‑lite**: rate‑limits, roles, logs, encryption at rest; **no repo**.
- Delayed sign‑off → acceptance rule (dashboard + export + checklist within 48h).
- Payment delay → suspend after **10–15d**; restore on payment.
- Shadow pilot/copy attempt → watermark exports; track IDs; server logs.

## 6) Roles & Day‑1 Checklist
- **Sales/Founder:** run **reverse‑anchor**; capture KPI baseline (current NPS/churn); send proposal pack.
- **PM:** publish **Scope Matrix**, caps **T1/T2/T3**, acceptance checklist; set 10‑day plan & daily stand‑ups.
- **Data/ML:** validate schema; set parsers; run **NPS/sentiment/churn** pipeline on sample; calibrate thresholds.
- **Eng (Backend):** rate‑limit + token quotas; logging; export **watermarks**; **kill‑switch**; error budgets.
- **Frontend:** v1 dashboard (NPS, churn, emotions, pain‑points); export buttons; tier meter (cap usage).
- **Legal/Finance:** NDA + License; invoice **50/50**; non‑payment clause; Enterprise template ready.

## 7) 10‑Day Delivery Plan
- **D0–D1:** Data intake + schema map + sample run; confirm acceptance checklist.
- **D2–D5:** Pipeline hardening (batching, caching, caps); dashboard wiring; exports.
- **D6–D8:** KPI validation (NPS/churn), QA, logs, watermarks, rate‑limits.
- **D9:** Client walkthrough; gather acceptance sign‑off.
- **D10:** Deliver export + report; move to Tier selection.

## 8) KPIs & Guardrails
- Margin **≥35%**; cycle **≤14d**; uptime **≥99%**; response time per tier (48h/36h/24h).
- Export latency **≤2h/file**; tokens within caps; 0 PII leaks.
- Two scope violations or >15d late → **pause** engagement.

## 9) Discovery Questions (use in first call)
1) Top 3 outcomes? (NPS, churn, CX pain‑points).  
2) Data size/formats? Update frequency? Who signs acceptance?  
3) Security/process constraints? (no code, only exports?)  
4) Budget window and urgency? (express?)  
5) Who decides post‑pilot tier? Timeline?

## 10) Close Script (≤20s)
“Give your **first number**; we map to **Pilot→Tier** with clear caps. In **10 days** you get **NPS/churn/pain‑points + export**. We ship **v1 now**; enhancements later. **Express** available (+30%) with frozen scope.”

---
**Internal:** keep corridor 25–15; never hand repo; enforce caps; acceptance = dashboard + export + checklist. Track tokens, costs, margin.
