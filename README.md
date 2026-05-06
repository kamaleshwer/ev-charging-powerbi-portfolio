# ⚡EV Charging Site — Power BI Dashboard Portfolio

> **Role:** Business Intelligence Developer  
> **Client:** Walmart (Internal Operations)  
> **Tool:** Microsoft Power BI (Live Connection via Teams Excel Sheet)  
> **Domain:** EV Infrastructure Rollout Tracking

---

## 📌 Project Overview

This project delivers an end-to-end Power BI reporting solution to monitor and manage the status of Walmart's nationwide **EV Charging Site** installation program. The dashboard enables operations and real estate teams to track site progress, identify bottlenecks, and drill into store-level details across every stage of the EV charging setup lifecycle.

---

## 🗂️ Repository Structure

```
ev-charging-portfolio/
│
├── README.md                    ← You are here
├── docs/
│   ├── project-overview.md      ← Detailed feature documentation
│   ├── data-dictionary.md       ← Field definitions and source mapping
│   └── user-guide.md            ← End-user navigation guide
│
├── data-model/
│   ├── data-model-diagram.md    ← ERD and table relationships
│   └── dax-measures.md          ← Key DAX formulas used
│
├── reports/
│   └── ev-charging-report-summary.md  ← Report page-by-page breakdown
│
└── screenshots/                 ← Dashboard screenshots (see docs)
```

---

## 📊 Dashboard Pages

### 1. 🏪 Store Rankings Overview
Displays all Walmart stores that have been assigned a ranking for EV charging site priority.

| Rank Tier | Description |
|-----------|-------------|
| 0 – 50    | Highest priority stores |
| 51 – 200  | Mid-tier priority stores |
| 201+      | Lower priority / future pipeline |

**Features:**
- 3 ranked tables segmented by priority tier
- Store Manager name and direct phone number included
- 🗺️ **Google Maps deep-link** — generated dynamically from Latitude & Longitude pulled from the Site Plan sheet
- Filters: State, Utility, City, Store Type, Business Unit, Lease Type

---

### 2. 📋 Title & Site Plan Status
Tracks the legal and site planning workflow for each store.

#### Title Status Pipeline:
```
Title Requested → Internal Research → Title Ordered → Memo Ordered → Legal Review ✅
```

#### Site Plan Status Pipeline:
```
Site Plan Creation → Energy Transformation Review → Real Estate Review ✅
```

**Features:**
- Horizontal bar charts for each stage showing completed vs. pending counts
- **Average Duration cards** at the top of each bar — calculated from start/end date fields per category
- **Drill-through enabled** — clicking any bar navigates to a filtered table of all stores in that exact status
- Real Estate Review = final milestone for EV site setup completion

---

### 3. 🗺️ Store Map View
Interactive map page showing the geographic distribution of all Walmart EV charging sites.

- Each store plotted using **Latitude & Longitude** from the Site Plan data sheet
- Color-coded by status (e.g., completed, in-progress, pending)
- Enables regional pattern analysis at a glance

---

### 4. 🥧 Completion Summary (Pie Charts)
Three pie chart visuals summarizing overall completion rates:

| Chart | Tracks |
|-------|--------|
| Title & Memo Status | Completion across title and memo workflow stages |
| Site Plan Complete | Whether the site plan has been finalized |
| Utility App Status | Utility application submitted / approved / pending |

---

## 🔗 Data Source

| Source | Type | Connection |
|--------|------|------------|
| Teams Excel Sheet | Structured tabular data | **Live Connection** (DirectQuery-style via SharePoint/Teams) |
| Site Plan Sheet | Lat/Long + Site Plan status | Same workbook, separate tab |

> **Live connection** means the dashboard always reflects the latest data without manual refresh — any updates made to the Excel sheet are immediately visible in Power BI.

---

## 🔍 Key Filters (Slicers)

All pages are cross-filtered using:

- **State**
- **Utility Provider**
- **City**
- **Store Type**
- **Business Unit**
- **Lease Type**

---

## 🧠 Technical Highlights

- **Dynamic Google Maps URL** built using `Latitude` and `Longitude` columns to generate a clickable hyperlink column in each table
- **Avg Duration DAX Measures** calculated per pipeline stage using start/end date logic — see [`data-model/dax-measures.md`](data-model/dax-measures.md)
- **Drill-through pages** configured for each status bar, enabling seamless navigation from summary to detail
- **Live data connection** to a Teams-hosted Excel workbook for zero-latency data freshness
- **Ranked table segmentation** logic applied to split stores into three priority tiers

---

## 📁 Related Documents

- [`docs/data-dictionary.md`](docs/data-dictionary.md) — Field definitions
- [`docs/user-guide.md`](docs/user-guide.md) — How to navigate the report
- [`data-model/dax-measures.md`](data-model/dax-measures.md) — DAX formulas
- [`reports/ev-charging-report-summary.md`](reports/ev-charging-report-summary.md) — Full report walkthrough

---

## 👤 About This Project

This dashboard was built as part of an internal data analytics initiative to accelerate EV infrastructure expansion. The solution replaced manual status tracking in spreadsheets with a centralized, interactive reporting layer — giving stakeholders real-time visibility from the executive level down to individual store managers.


