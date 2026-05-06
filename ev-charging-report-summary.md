# Report Summary — EV Charging Site Dashboard

## Report at a Glance

| Page | Title | Primary Visuals |
|------|-------|----------------|
| 1 | Store Rankings | 3 ranked tables, slicers, Google Maps links |
| 2 | Title & Site Plan Status | Stacked bar charts, avg duration cards, drill-through |
| 3 | Map View | Geospatial store map |
| 4 | Completion Summaries | 3 pie charts |

---

## Page 1 — Store Rankings

### Design Intent
Provides an operational roster of all ranked stores, organized by priority so field teams and program managers can triage work efficiently.

### Key Features
- **Three ranked tables** segmented by tier (0–50, 51–200, 201+)
- **Google Maps link column** generated dynamically from Latitude + Longitude
- Store Manager name and phone number for direct outreach
- Six slicers for filtering: State, Utility, City, Store Type, Business Unit, Lease Type
- Summary pie charts for quick completion status at a glance

---

## Page 2 — Title & Site Plan Status

### Design Intent
Gives program managers visibility into pipeline bottlenecks across the legal and physical planning stages. Combines summary-level visuals with drill-through detail.

### Title Status Flow
```
Title Requested → Internal Research → Title Ordered → Memo Ordered → Legal Review
```

### Site Plan Status Flow
```
Site Plan Creation → Energy Transformation Review → Real Estate Review
```

### Key Features
- Horizontal stacked bar charts: Completed (dark) vs. Pending (light) per stage
- **Average Duration cards** — DAX AVERAGEX calculated over DATEDIFF per stage
- **Drill-through on every bar** — click to see store-level detail table filtered to that exact stage and status
- "Back" button navigation from drill-through back to summary

---

## Page 3 — Map View

### Design Intent
Provides geographic context for the EV rollout, enabling regional analysis and helping teams understand clustering, coverage gaps, and logistics.

### Key Features
- Each store plotted using exact Latitude/Longitude from Site Plan data
- Status-coded visual markers
- Fully filterable via slicers

---

## Page 4 — Completion Summaries

### Design Intent
Executive-level snapshot of overall program health. Quick answer to: "How far along are we?"

### Three Pie Charts

**1. Title & Memo Status**
Shows the breakdown of stores across Title and Memo completion states.

**2. Site Plan Complete**
Shows what % of stores have a finalized site plan vs. still in progress or not started.

**3. Utility App Status**
Shows the distribution of stores by utility application state: Not Started / Submitted / Approved / Pending.

---

## Technical Notes

- Report built in **Microsoft Power BI Desktop**
- Data source: **Live connection** to Teams-hosted Excel workbook (SharePoint)
- DAX measures used for: average duration per stage, rank tier classification, Google Maps URL construction, completed/pending counts
- Drill-through pages configured per pipeline stage
- Report designed for both desktop and stakeholder sharing via Power BI Service
