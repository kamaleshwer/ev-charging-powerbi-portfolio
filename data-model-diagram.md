# Data Model Diagram

## Entity Relationship Overview

The data model follows a **star schema** pattern with `StoreRankings` as the central fact/dimension table, joined to status tables by `Store_ID`.

```
                    ┌─────────────────────┐
                    │   StoreRankings      │
                    │─────────────────────│
                    │ Store_ID (PK)        │
                    │ Store_Type           │
                    │ Business_Unit        │
                    │ Rank                 │
                    │ Rank_Tier (calc)     │
                    │ State                │
                    │ City                 │
                    │ Lease_Type           │
                    │ Utility              │
                    │ Store_Manager        │
                    │ Store_Manager_Phone  │
                    │ Latitude             │
                    │ Longitude            │
                    │ Maps_Link (calc)     │
                    └──────────┬──────────┘
                               │ Store_ID (1:1 or 1:many)
              ┌────────────────┼───────────────────┐
              │                │                   │
   ┌──────────▼──────┐  ┌──────▼──────────┐  ┌────▼────────────┐
   │  TitleStatus     │  │ SitePlanStatus   │  │ UtilityApp      │
   │─────────────────│  │─────────────────│  │─────────────────│
   │ Store_ID (FK)   │  │ Store_ID (FK)   │  │ Store_ID (FK)   │
   │ Title_Req_Start │  │ SitePlan_Start  │  │ Utility_App_    │
   │ Title_Req_End   │  │ SitePlan_End    │  │   Status        │
   │ IntResearch_... │  │ EnergyTrans_... │  │ Utility_        │
   │ TitleOrdered_.. │  │ RE_Review_Start │  │   Provider      │
   │ MemoOrdered_... │  │ RE_Review_End   │  └─────────────────┘
   │ LegalReview_... │  │ SitePlan_       │
   │ Title_Status    │  │   Complete      │
   └─────────────────┘  └─────────────────┘
```

---

## Relationship Summary

| From Table | To Table | Key | Cardinality |
|------------|----------|-----|-------------|
| StoreRankings | TitleStatus | Store_ID | 1 : 1 |
| StoreRankings | SitePlanStatus | Store_ID | 1 : 1 |
| StoreRankings | UtilityApp | Store_ID | 1 : 1 |

---

## Source Connection

All tables originate from a single **Teams-hosted Excel workbook** with multiple sheets:

| Sheet | Maps To |
|-------|---------|
| Main Rankings Sheet | StoreRankings |
| Title Status Sheet | TitleStatus |
| Site Plan Sheet | SitePlanStatus + Lat/Long |
| Utility App Sheet | UtilityApp |

The connection is a **live connection**, meaning Power BI queries the workbook directly — no import/scheduled refresh required.
