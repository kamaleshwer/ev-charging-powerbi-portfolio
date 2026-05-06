# Data Dictionary — EV Charging Site

## Source Tables

### Store Rankings Table
| Field | Type | Description |
|-------|------|-------------|
| Store_ID | Text | Unique Walmart store identifier |
| Store_Type | Text | Format (Supercenter, Neighborhood Market, etc.) |
| Business_Unit | Text | Internal Walmart business unit code |
| Rank | Integer | Priority rank for EV site installation |
| Rank_Tier | Calculated | Bucketed tier: 0-50, 51-200, 201+ |
| State | Text | US state abbreviation |
| City | Text | City name |
| Lease_Type | Text | Owned vs. leased property classification |
| Utility | Text | Local utility provider name |
| Store_Manager | Text | Full name of current store manager |
| Store_Manager_Phone | Text | Direct contact number |
| Latitude | Decimal | GPS latitude for map plotting |
| Longitude | Decimal | GPS longitude for map plotting |
| Maps_Link | Calculated | Dynamic Google Maps URL using Lat/Long |

---

### Title Status Table
| Field | Type | Description |
|-------|------|-------------|
| Store_ID | Text | FK to Store Rankings |
| Title_Requested_Start | Date | Date title request was initiated |
| Title_Requested_End | Date | Date title request was completed |
| Internal_Research_Start | Date | Internal research start date |
| Internal_Research_End | Date | Internal research end date |
| Title_Ordered_Start | Date | Title order date |
| Title_Ordered_End | Date | Title order completion date |
| Memo_Ordered_Start | Date | Memo order start date |
| Memo_Ordered_End | Date | Memo order completion date |
| Legal_Review_Start | Date | Legal review begin date |
| Legal_Review_End | Date | Legal review completion date (final stage) |
| Title_Status | Text | Overall status label |

---

### Site Plan Status Table
| Field | Type | Description |
|-------|------|-------------|
| Store_ID | Text | FK to Store Rankings |
| Site_Plan_Creation_Start | Date | Site plan creation start |
| Site_Plan_Creation_End | Date | Site plan creation end |
| Energy_Transform_Review_Start | Date | Energy transformation review start |
| Energy_Transform_Review_End | Date | Energy transformation review end |
| RE_Review_Start | Date | Real estate review start |
| RE_Review_End | Date | Real estate review completion (final stage) |
| Site_Plan_Complete | Text | Yes / No / In Progress |

---

### Utility Application Table
| Field | Type | Description |
|-------|------|-------------|
| Store_ID | Text | FK to Store Rankings |
| Utility_App_Status | Text | Not Started / Submitted / Approved / Pending |
| Utility_Provider | Text | Name of utility company |

---

## Calculated Fields (DAX)

See [`data-model/dax-measures.md`](../data-model/dax-measures.md) for full formulas.

| Measure | Description |
|---------|-------------|
| Avg Duration - Title Requested | Avg days from start to end of Title Requested stage |
| Avg Duration - Internal Research | Avg days for Internal Research |
| Avg Duration - Title Ordered | Avg days for Title Ordered stage |
| Avg Duration - Memo Ordered | Avg days for Memo Ordered stage |
| Avg Duration - Legal Review | Avg days for Legal Review (final title stage) |
| Avg Duration - Site Plan Creation | Avg days for Site Plan Creation |
| Avg Duration - Energy Transform Review | Avg days for Energy Transformation Review |
| Avg Duration - RE Review | Avg days for Real Estate Review (final stage) |
| Maps_URL | Concatenated Google Maps hyperlink |
| Rank_Tier | Bucketed rank classification |
