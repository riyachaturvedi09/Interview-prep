# RUNNING TOTAL FOR DATES


#### 10 Days Rolling Revenue

```sql
10DayRolling_Revenue = calculate(
    [TotalRevenue],
    DATEINPERIOD(calender[Date],MAX(calender[Date]),-10,DAY)
    -- the MAX here finds the the maximum date from the calender table & then Calculates the rolling revenue from -10 Days from the MAX date.
)

```

#### Previous Month Revenue

```sql
PreviousMonth_Revenue= Calculate(
    [TotalRevenue],DATESMTD(calender[Date],-1,Month)

    -- the DATESMTD here finds the the last month from the calender table & then Calculates the previous month's revenue.
)

```

#### Year-To-Date Revenue

```sql

YTD_Revenue= Calculate(
    [TotalRevenue],DATESYTD(calender[Date])

    -- the DATESYTD here finds the the last month from the calender table & then Calculates the year-to-date revenue.
)

```

#### SAME Period Last Year - Calculate Revenue for the same period but last year

```sql

YTD_Revenue= Calculate(
    [TotalRevenue],SAMEPERIODLASTYEAR(calender[Date])

    -- the SAMEPERIODLASTYEAR here finds the the same duration as current year from the calender table & then Calculates the year-to-date revenue.
)

```