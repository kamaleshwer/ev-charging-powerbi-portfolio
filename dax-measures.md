# DAX Measures — EV Charging Site Dashboard

## Average Duration Measures

Used to populate the summary cards displayed above each status bar chart. Calculated as the average number of days between the start and end date of each pipeline stage, for all stores where both dates are populated.

---

### Title Pipeline Measures

```dax
Avg Duration - Title Requested =
AVERAGEX(
    FILTER(
        'TitleStatus',
        NOT ISBLANK('TitleStatus'[Title_Requested_Start]) &&
        NOT ISBLANK('TitleStatus'[Title_Requested_End])
    ),
    DATEDIFF(
        'TitleStatus'[Title_Requested_Start],
        'TitleStatus'[Title_Requested_End],
        DAY
    )
)
```

```dax
Avg Duration - Internal Research =
AVERAGEX(
    FILTER(
        'TitleStatus',
        NOT ISBLANK('TitleStatus'[Internal_Research_Start]) &&
        NOT ISBLANK('TitleStatus'[Internal_Research_End])
    ),
    DATEDIFF(
        'TitleStatus'[Internal_Research_Start],
        'TitleStatus'[Internal_Research_End],
        DAY
    )
)
```

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

> The same pattern is repeated for **Title Ordered** and **Memo Ordered** stages.

---

### Site Plan Pipeline Measures

```dax
Avg Duration - Site Plan Creation =
AVERAGEX(
    FILTER(
        'SitePlanStatus',
        NOT ISBLANK('SitePlanStatus'[Site_Plan_Creation_Start]) &&
        NOT ISBLANK('SitePlanStatus'[Site_Plan_Creation_End])
    ),
    DATEDIFF(
        'SitePlanStatus'[Site_Plan_Creation_Start],
        'SitePlanStatus'[Site_Plan_Creation_End],
        DAY
    )
)
```

```dax
Avg Duration - RE Review =
AVERAGEX(
    FILTER(
        'SitePlanStatus',
        NOT ISBLANK('SitePlanStatus'[RE_Review_Start]) &&
        NOT ISBLANK('SitePlanStatus'[RE_Review_End])
    ),
    DATEDIFF(
        'SitePlanStatus'[RE_Review_Start],
        'SitePlanStatus'[RE_Review_End],
        DAY
    )
)
```

---

## Dynamic Google Maps URL

Used to generate a clickable hyperlink per store row. This is a **calculated column** on the Store Rankings table.

```dax
Maps_Link =
"https://www.google.com/maps/search/?api=1&query=" &
'StoreRankings'[Latitude] & "," & 'StoreRankings'[Longitude]
```

> In the report, this column is formatted as a **Web URL** data category, enabling one-click map navigation from within the table visual.

---

## Rank Tier (Calculated Column)

Segments stores into three priority buckets for the three ranked tables.

```dax
Rank_Tier =
SWITCH(
    TRUE(),
    'StoreRankings'[Rank] <= 50, "Tier 1 (0-50)",
    'StoreRankings'[Rank] <= 200, "Tier 2 (51-200)",
    "Tier 3 (201+)"
)
```

---

## Count Measures (for Bar Charts)

```dax
Count - Title Requested Completed =
CALCULATE(
    COUNTROWS('TitleStatus'),
    NOT ISBLANK('TitleStatus'[Title_Requested_End])
)

Count - Title Requested Pending =
CALCULATE(
    COUNTROWS('TitleStatus'),
    ISBLANK('TitleStatus'[Title_Requested_End])
)
```

> The same Completed / Pending pattern is applied for every stage across both the Title and Site Plan pipelines.
