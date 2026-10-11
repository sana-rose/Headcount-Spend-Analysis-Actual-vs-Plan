# Headcount & Spend: Actual vs Plan Dashboard

A Power BI dashboard that compares **planned vs actual headcount and operating spend** across four departments for a full fiscal year (Apr 2025 to Mar 2026), and explains where and why the business is off plan.

> **Note on data:** all figures are **simulated sample data**, created for this portfolio project. They do not come from any real company.

![Dashboard](Dashboard.png)

## Business question

Is the organisation hiring and spending in line with its plan, and if not, where are the gaps and what is driving them?

## Key findings

- Headcount ended the year at **193 against a plan of 217**, which is **11.1% below plan**.
- Total spend was **6.1% under plan**, mainly because roles were unfilled rather than because of real savings.
- Overall hiring was close to plan (**71 of 72 planned hires, 98.6%**), so hiring alone does not explain the gap.
- **23 of the 24-person gap comes from attrition**, which the plan did not assume. Engineering lost 10 people and Operations lost 9.
- **Product (-18.9%) and Engineering (-14.6%)** have the largest headcount shortfalls. Operations hired above plan, which hides shortfalls elsewhere.
- **Operations is 10.7% over its spend plan** even though its headcount is close to plan.

## Recommendations

1. Tackle attrition first, starting with Engineering and Operations.
2. Close the hiring gaps in Engineering and Product.
3. Review what is driving Operations spend.
4. Re-forecast the budget with an explicit attrition assumption.


## Dashboard contents

- Four KPI cards: actual headcount, headcount variance %, spend variance %, hiring achievement %
- Line chart: planned vs actual headcount by month
- Bar chart: planned vs actual spend by department
- Column chart: attrition by department
- Table: planned vs actual headcount and spend variance by department
- Department slicer that filters the whole page

## DAX measures

Headcount is a running total, so "latest" measures read the most recent month instead of summing across months. Percentages are measures so they divide totals, not average row-level percentages.

```
Planned HC Latest =
VAR LatestMonth = MAX(Data[Month])
RETURN CALCULATE(SUM(Data[Planned Headcount]), Data[Month] = LatestMonth)

Actual HC Latest =
VAR LatestMonth = MAX(Data[Month])
RETURN CALCULATE(SUM(Data[Actual Headcount]), Data[Month] = LatestMonth)

HC Variance = [Actual HC Latest] - [Planned HC Latest]

HC Variance % = DIVIDE([HC Variance], [Planned HC Latest])

Spend Var % =
DIVIDE(
    SUM(Data[Actual Spend]) - SUM(Data[Planned Spend]),
    SUM(Data[Planned Spend])
)

Hiring Achievement % =
DIVIDE(SUM(Data[Actual Hires]), SUM(Data[Planned Hires]))
```

## Tools

Power BI, DAX, Power Query, Excel, PowerPoint

## Skills demonstrated

Variance analysis (actual vs plan), KPI design, workforce and spend analytics, DAX, dashboard design, data validation, and communicating findings to leadership.



## Author

Sana Angel Rose | [LinkedIn](https://linkedin.com/in/sana-angel-rose)
