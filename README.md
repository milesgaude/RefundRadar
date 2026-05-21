# RefundRadar

> AI-powered Shopify fraud detection that scores every order before it ships.

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=nextdotjs&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat&logo=supabase&logoColor=white)
![Railway](https://img.shields.io/badge/Railway-0B0D0E?style=flat&logo=railway&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=flat&logo=stripe&logoColor=white)
<img width="2878" height="1538" alt="Screenshot 2026-05-14 152320" src="https://github.com/user-attachments/assets/040d824b-230c-4d49-ad20-2e126c33dbae" />
<img width="2876" height="1544" alt="Screenshot 2026-05-14 152421" src="https://github.com/user-attachments/assets/647230eb-b2ae-4461-9e27-6c3a0ac03b68" />
<img width="2874" height="1538" alt="Screenshot 2026-05-14 152151" src="https://github.com/user-attachments/assets/b23082e0-f297-4bf0-b446-14fbcdc39581" />

**Live product:** [getrefundradar.com](https://getrefundradar.com)

---

## The Problem

Shopify store owners lose 3 to 5% of monthly revenue to fraudulent orders. Stolen cards, fake addresses, freight forwarder scams, and serial chargebacks all look identical to legitimate orders at checkout. Shopify's built-in risk score catches roughly half of them at best. By the time a merchant finds out an order was fraudulent, they have already shipped the product, paid for fulfillment, and are about to eat the chargeback fee on top.

The intervention window is the pre-fulfillment moment — the only point where a merchant can actually do something about it.

---

## The Solution

RefundRadar scores every incoming Shopify order across 20+ risk signals using AI the moment it is placed. High-risk orders trigger an instant email alert so merchants can hold or cancel before the package leaves the warehouse. No manual review required. No auto-cancellations. The merchant always makes the final call.

---

## Architecture

```
Shopify Store
     │
     │  OAuth Install + Webhooks
     ▼
┌─────────────────────────────────┐
│       Node.js Backend           │
│       (Railway)                 │
│                                 │
│  • Shopify OAuth handler        │
│  • Webhook listener             │
│  • Order risk scoring engine    │
│  • Email alert system           │
│  • Stripe billing               │
└────────────┬────────────────────┘
             │
     ┌───────┴────────┐
     │                │
     ▼                ▼
┌─────────┐    ┌──────────────┐
│ Supabase│    │ Anthropic API│
│  (DB)   │    │ (AI Scoring) │
└─────────┘    └──────────────┘
     │
     ▼
┌─────────────────────────────────┐
│     Next.js Dashboard           │
│     (Vercel)                    │
│                                 │
│  • Multi-tenant merchant view   │
│  • Order risk breakdown         │
│  • Risk score history           │
│  • Alert configuration          │
└─────────────────────────────────┘
```

---

## How the AI Scoring Works

RefundRadar uses the Anthropic API as its scoring engine. Rather than training a custom classifier from scratch (which requires years of labeled chargeback data), the system passes structured order data alongside a carefully engineered prompt that encodes fraud domain knowledge.

**Signals analyzed per order include:**

- Shipping address risk profile (freight forwarder detection, high-risk regions)
- Email age and pattern analysis
- Billing vs shipping address correlation
- Order velocity across the store
- Product category and AOV risk weighting
- Payment method and card BIN analysis
- Customer account age and order history
- Device and session behavioral signals
- Expedited shipping selection on high-ticket items
- Cross-order pattern matching for carding attacks

The model reasons across all signals simultaneously and returns a structured response with a risk score (Low / Medium / High), confidence percentage, and a plain-English explanation of which signals drove the score — so merchants understand exactly why an order was flagged.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Node.js / Express |
| Frontend | Next.js |
| Database | Supabase (PostgreSQL) |
| Backend Hosting | Railway |
| Frontend Hosting | Vercel |
| AI Scoring | Anthropic API (Claude) |
| Payments | Stripe |
| Shopify Integration | OAuth 2.0, Webhooks |
| Email Alerts | Nodemailer / SMTP |

---

## Key Features

- One-click Shopify OAuth install — no manual configuration
- Real-time order scoring on every incoming order
- Instant email alerts on high-risk orders before fulfillment
- Multi-tenant dashboard with full order history and risk breakdowns
- Risk score explanation in plain English for every flagged order
- Trusted customer whitelist to reduce false positives
- Free tier available with usage-based paid plans

---

## What I Built

This was a solo full-stack build completed in approximately 3 months while attending the University of Georgia as a full-time student. Every layer of the stack was built and deployed from scratch including:

- Shopify Partner app setup and OAuth flow
- Multi-tenant backend architecture on Railway
- AI prompt engineering for fraud detection
- Real-time webhook processing pipeline
- Stripe subscription billing integration
- Next.js merchant dashboard with Supabase backend
- Custom email alert system

---

## About

Built by Miles — MIS student at the University of Georgia, and full-stack developer with experience across SaaS, ML, and AI.

- Website: [getrefundradar.com](https://getrefundradar.com)

---

*This repository is a portfolio showcase. Source code is private as RefundRadar is a live commercial product.*
