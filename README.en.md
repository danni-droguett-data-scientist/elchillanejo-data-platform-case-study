# El Chillanejo — Data Platform & Digital Channel (Case Study)

> **Real, in-production project.** Case study of the Data Science work I lead at El Chillanejo, a cleaning-supplies and groceries distributor in Chillán, Chile.
>
> ⚠️ **Confidentiality note.** The original working repository is **private** for security reasons and compliance with Chile's **Law 19.628** (personal data protection). This repository is a **sanitized case study**: it describes the architecture and shows sample code snippets, **with no real data, no credentials, and no sensitive business information**.

**Language / Idioma:** [Español](README.md) | English

---

## Summary

I designed and built, end to end, the data layer and online sales channel of a real distributor. It is **data science in production**: used every day to drive inventory, margin, purchasing and sales decisions.

My background is uncommon: five years running real business operations before moving into data. I understand the problem from the inside and apply analytical method to it.

---

## The problem

The company ran without its own analytics layer: data lived in the ERP, reporting was manual, and there was no digital sales channel. The goal was to build a reliable, automated database and, on top of it, dashboards, automation and an online channel.

---

## Architecture

![3-layer architecture](arquitectura.png)

A decoupled **3-layer** system, designed to be reusable across sources and clients:

1. **Connectors** — read-only extraction from the ERP with rate-limit control, retries and pagination; hourly incremental sync pipelines (Python + n8n on Railway).
2. **Analytics base** — Supabase (PostgreSQL) with universal tables (`ventas`, `ventas_detalle`, `productos`, `stock`, etc.) and row-level security (RLS) by role.
3. **Data products** — dashboards, online store, WhatsApp bot and warehouse portal. This layer never calls the source: it only reads the analytics base.

---

## What I built

- **ERP → PostgreSQL integration**: 18-month historical load (126,000+ sales and 307,000+ line items) and hourly incremental sync.
- **Three dashboards** (operational, executive, warehouse) in React, with sales/margin KPIs, trends and stock alerts, role-based access.
- **Online store** in Next.js (catalog, cart, integrated checkout).
- **AI WhatsApp sales bot**: natural-language sales/stock queries and cart building via a tool-use agent.
- **Product recommendation engine** based on market-basket analysis (co-purchased products and frequent itemsets).
- **Warehouse operations portal**: inter-warehouse transfers, goods receipts and barcode-scan inventory.

---

## Stack

Python (pandas, NumPy, scikit-learn) · SQL · PostgreSQL / Supabase · n8n · Railway · React · Next.js / TypeScript · REST APIs · conversational AI (tool-use).

---

## Technical highlight: rate-limited ingestion

An example of the engineering involved: the source API allows ~7 requests/second. The solution self-throttles to an equilibrium interval, honors the server's `Retry-After` on a 429, and retries with increasing backoff.

Sample code (sanitized): [`snippets/rate_limited_client.py`](snippets/rate_limited_client.py)

---

## Results

- Data platform **in production**, used daily for inventory, purchasing and pricing decisions.
- Manual reporting **eliminated**: data refreshes itself every hour.
- Online sales channel operational end to end.

---

## About me

**Daniel A. Droguett Rozas** — Data Scientist (Chillán, Chile).

- LinkedIn: https://www.linkedin.com/in/daniel-a-droguett-rozas-b65a991b4/
- GitHub: https://github.com/danni-droguett-data-scientist
- Email: dannidro@gmail.com

---

*This case study contains no real data, credentials or sensitive business information. Published for professional portfolio purposes.*
