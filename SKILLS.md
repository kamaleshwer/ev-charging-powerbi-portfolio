# 🧠 Skills Summary — Business Intelligence Developer

> This document outlines the core technical and analytical skills demonstrated through the **Walmart EV Charging Site Dashboard** project and related BI work.

---

## 📊 Power BI & DAX

**Proficiency: Advanced**

| Skill | Applied In This Project |
|-------|------------------------|
| Report design (multi-page, multi-visual) | 4-page dashboard with ranked tables, bar charts, maps, and pie charts |
| DAX calculated columns | `Rank_Tier`, `Maps_Link` (dynamic Google Maps URL) |
| DAX measures (AVERAGEX, DATEDIFF, FILTER) | Average duration cards per pipeline stage |
| Drill-through configuration | Stage-level drill-through from every status bar to detail table |
| Live data connection | DirectQuery-style live connection to Teams Excel workbook |
| Web URL data category | Clickable hyperlinks per store row linking to Google Maps |
| Slicers & cross-filtering | 6 slicers (State, Utility, City, Store Type, Business Unit, Lease Type) |
| Geospatial map visual | Store map plotted using Latitude & Longitude |
| Conditional formatting | Status-coded visuals for completed vs. pending |

### Sample DAX (Average Duration)
```dax
Avg Duration - Legal Review =
AVERAGEX(
    FILTER(
        'TitleStatus',
        NOT ISBLANK('TitleStatus'[Legal_Review_Start]) &&
        NOT ISBLANK('TitleStatus'[Legal_Review_End])
    ),
    DATEDIFF(
        'TitleStatus'[Legal_Review_Start],
        'TitleStatus'[Legal_Review_End],
        DAY
    )
)
```

### Sample DAX (Dynamic URL Column)
```dax
Maps_Link =
"https://www.google.com/maps/search/?api=1&query=" &
'StoreRankings'[Latitude] & "," & 'StoreRankings'[Longitude]
```

---

## 🗄️ SQL

**Proficiency: Intermediate–Advanced**

| Skill | Description |
|-------|-------------|
| SELECT, JOIN, WHERE, GROUP BY | Standard query authoring for data extraction |
| Window functions (RANK, ROW_NUMBER, PARTITION BY) | Ranking logic relevant to store tier segmentation |
| CTEs (WITH clause) | Building multi-step transformation logic cleanly |
| Date functions (DATEDIFF, DATEADD) | Calculating stage durations — same logic as DAX measures |
| Aggregations (AVG, COUNT, SUM) | Summary metrics for pipeline stage reporting |
| Subqueries | Filtering and shaping intermediate result sets |
| Stored procedures | Automating recurring report data prep |

### Sample SQL (Stage Duration Query)
```sql
SELECT
    Store_ID,
    DATEDIFF(DAY, Legal_Review_Start, Legal_Review_End) AS Legal_Review_Days
FROM TitleStatus
WHERE Legal_Review_Start IS NOT NULL
  AND Legal_Review_End IS NOT NULL;
```

### Sample SQL (Rank Tier Segmentation)
```sql
SELECT
    Store_ID,
    Rank,
    CASE
        WHEN Rank <= 50  THEN 'Tier 1 (0-50)'
        WHEN Rank <= 200 THEN 'Tier 2 (51-200)'
        ELSE                  'Tier 3 (201+)'
    END AS Rank_Tier
FROM StoreRankings
ORDER BY Rank ASC;
```

---

## 📁 Excel & SharePoint

**Proficiency: Advanced**

| Skill | Applied In This Project |
|-------|------------------------|
| Structured Excel workbook design | Multi-sheet source workbook (Rankings, Title, Site Plan, Utility) |
| SharePoint / Teams file hosting | Workbook hosted in Teams for collaborative editing + live BI connection |
| Live connection to Power BI | Eliminated scheduled refresh — always-current data |
| Power Query (Get & Transform) | Data shaping and column type enforcement |
| Named tables and structured references | Ensured stable column references across workbook changes |
| Data validation & formatting | Consistent date formats and dropdown-constrained status fields |

---

## 🏗️ Data Modeling

**Proficiency: Advanced**

| Skill | Applied In This Project |
|-------|------------------------|
| Star schema design | Central `StoreRankings` fact/dim table; satellite status tables joined by `Store_ID` |
| Relationship management (1:1, 1:many) | Clean joins across Title, Site Plan, and Utility tables |
| Cardinality and cross-filter direction | Controlled filter propagation across report pages |
| Calculated columns vs. measures | Used columns for row-level attributes (Rank_Tier, Maps_Link); measures for aggregations |
| Data type enforcement | Date fields standardized; lat/long as decimal for map compatibility |
| Grain definition | One row per store per status table — ensured no fan-out or duplication |

---

## 🔄 ETL & Data Pipelines

**Proficiency: Intermediate–Advanced**

| Skill | Description |
|-------|-------------|
| Source-to-report data flow design | Mapped raw Excel sheets → transformed model → Power BI visuals |
| Power Query transformations | Column renaming, type casting, null handling, conditional columns |
| Live connection architecture | Designed for zero-latency freshness without ETL scheduling overhead |
| Data refresh strategy | Evaluated live vs. import mode; selected live for operational reporting use case |
| Source system change management | Designed model to absorb new columns/sheets without breaking existing visuals |
| Data quality checks | Identified and handled missing date fields in duration calculations (ISBLANK guards) |

---

## 🤝 Soft Skills & Delivery

| Skill | How Demonstrated |
|-------|-----------------|
| Stakeholder requirement gathering | Translated operational pain points into dashboard page specifications |
| Self-directed delivery | Built end-to-end solution independently from data exploration to final report |
| Documentation | Data dictionary, user guide, DAX documentation, data model diagram |
| Cross-functional communication | Delivered tool usable by operations, real estate, and executive audiences |
| Problem-solving | Designed Google Maps hyperlink column using lat/long — no native map-link feature in Power BI |

---

## 🛠️ Tools & Technologies

| Category | Tools |
|----------|-------|
| BI & Visualization | Microsoft Power BI Desktop, Power BI Service |
| Data Transformation | Power Query (M language), DAX |
| Data Source | Microsoft Excel (Teams/SharePoint hosted) |
| Database | SQL Server (general), T-SQL |
| Productivity | Microsoft Teams, SharePoint, Excel |

---

*For DAX formula reference, see [`data-model/dax-measures.md`](data-model/dax-measures.md)*  
*For data model structure, see [`data-model/data-model-diagram.md`](data-model/data-model-diagram.md)*
