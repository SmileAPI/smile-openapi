---
title: Insights
excerpt: ''
category: 6294c158bef44e0098ed88a1
slug: insights
---

The Smile Insights API provides common calculations for risk factors based on available data from [Users](/reference/users), such as income and employment data.

These Insights can help with decisioning processes whether assessing a candidate for financial services or employment pruposes. Common calculations such as averages, minimums, maximums, and others are done for you across a number of different durations or categories of information.

Insights are available for the following data sources:

| Data source | Insight category |
|---|---|
| Social security services | Identity, Employments, Incomes, Liabilities |
| Government employee insurance and pension agency | Identity, Employments, Incomes |
| National health insurance agency | Identity, Incomes |
| National housing provident fund | Identity, Employments, Incomes, Liabilities |

> 📘 Note
> 
> You may come across the following values when ingesting our insight data:
> 
> * -999 - the data is empty, missing, or not available from the data source
> * -998 - there was an error in computing the insight value


## Identity and Employments Insights

Identity and employment insights give you a quick summarized view of the User's information without needing to calculate this information from the raw data from the Data Source.

| Insight variable name | Description |
|---|---|
| `identity_age` | Current age of user |
| `employments_current_status` | Employment status, can be either `EMPLOYED`, `GIG`, or `UNEMPLOYED` |
| `employments_employer_count` | Number of unique employers |
| `employments_current_tenure` | Number of months at current employer |

## Income Insights

Income insights give you a range of common calculations using the user's income records across different months (based on [Estimated Income](/reference/estimated-incomes)). This saves you the time and resources needed to calculate this information from the raw data from the Data Source.

> 📘 Note
> 
> For **My.SSS**, there may be a 1-2 month delay from when income-related data is posted from the data source. Smile takes this into account, but it is important to note this possible data discrepancy and add it to your own calculations.

| Insight variable name | Description |
|---|---|
| `incomes_count` | Number of income records |
| `incomes_current_amount` | Income for the current month |
| `incomes_starting_amount` | Income for the user's first month of working (starting income) |
| `incomes_first_income_month_range` | Number of months since the first income record, i.e. how many months the user has been working |
| `incomes_latest_growth` | Income growth from the same time last year |
| `incomes_last18_months_max_amount_count`| Number of months the user has received their maximum income |
| `incomes_missing_month_count` | Number of months with no income |
| `incomes_missing_month_max` | Longest duration without income (in months) |
| `incomes_amount_sum` `incomes_last3_months_amount_sum` `incomes_last6_months_amount_sum` `incomes_last9_months_amount_sum` `incomes_last12_months_amount_sum` `incomes_last18_months_amount_sum` | Total income received (lifetime and monthly durations) |
| `incomes_amount_avg` `incomes_last3_months_amount_avg` `incomes_last6_months_amount_avg` `incomes_last9_months_amount_avg` `incomes_last12_months_amount_avg` `incomes_last18_months_amount_avg` | Average of income received (lifetime and monthly durations) |
| `incomes_amount_min` `incomes_last3_months_amount_min` `incomes_last6_months_amount_min` `incomes_last9_months_amount_min` `incomes_last12_months_amount_min` `incomes_last18_months_amount_min` | Smallest income received (lifetime and monthly durations) |
| `incomes_amount_max` `incomes_last3_months_amount_max` `incomes_last6_months_amount_max` `incomes_last9_months_amount_max` `incomes_last12_months_amount_max` `incomes_last18_months_amount_max` | Largest income received (lifetime and monthly durations) |
| `incomes_amount_median` `incomes_last3_months_amount_median` `incomes_last6_months_amount_median` `incomes_last9_months_amount_median` `incomes_last12_months_amount_median` `incomes_last18_months_amount_median` | Median of income received (lifetime and monthly durations) |
| `incomes_amount_std` `incomes_last3_months_amount_std` `incomes_last6_months_amount_std` `incomes_last9_months_amount_std` `incomes_last12_months_amount_std` `incomes_last18_months_amount_std` | Standard deviation of income received (lifetime and monthly durations) |

## Liabilities Insights

Liabilities Insights give you a quick summarized view of the User's loan information without needing to calculate this information from the raw data from the Data Source.

| Insight variable name | Description |
|---|---|
| `liabilities_loan_count` | Number of loans (lifetime) |
| `liabilities_loan_amount_total` `liabilities_loan_amount_average` `liabilities_loan_amount_min` `liabilities_loan_amount_max` `liabilities_loan_amount_std` | Total, average, min, max, and standard deviation of loan amounts across all loans |
| `liabilities_finished_loan_count` | Number of completed loans |
| `liabilities_outstanding_loan_count` | Number of outstanding loans |
| `liabilities_outstanding_amount_total` `liabilities_outstanding_amount_average` `liabilities_outstanding_amount_max` | Total outstanding amount, average, and largest loan amount based on outstanding loans only |
| `liabilities_overdue_loan_count` | Number of overdue loans |
| `liabilities_overdue_amount_total` `liabilities_overdue_amount_average` | Total overdue amount and average amount of all overdue loans only |
| `liabilities_payment_count` | Number of loan payments made |
| `liabilities_payment_amount_sum` `liabilities_payment_amount_average` `liabilities_payment_amount_min` `liabilities_payment_amount_max` `liabilities_payment_amount_median` `liabilities_payment_amount_std` | Total, average, min, max, median, and standard deviation of loan payments across all loans |
| `liabilities_ongoing_amortization_amount_sum` `liabilities_ongoing_amortization_amount_average` `liabilities_ongoing_amortization_amount_min` `liabilities_ongoing_amortization_amount_max` `liabilities_ongoing_amortization_amount_median` `liabilities_ongoing_amortization_amount_std` | Total, average, min, max, median, and standard deviation of loan amortization amounts across ongoing loans |

## Link Insights

Links form the backbone of the [Multiple Application Warning](/reference/links) service, and if opted into both Multiple Application Warning and Insights, we also provide additional Insights surrounding the user's linking activity. These can be easily included in proprietary data models to improve the credit decisioning process.

| Insight variable name | Description |
|---|---|
| `link_days_since_first` | Number of days since first connection |
| `link_days_since_last` | Number of days since last connection |
| `link_day3_count` | Number of times user has connected in the last 3 days |
| `link_day7_count` | Number of times user has connected in the last 7 days |
| `link_day30_count` | Number of times user has connected in the last 30 days |
| `link_day90_count` | Number of times user has connected in the last 90 days |
| `link_day180_count` | Number of times user has connected in the last 180 days |
| `link_day365_count` | Number of times user has connected in the last 365 days |
| `link_day730_count` | Number of times user has connected in the last 730 days |

_Insights is currently in alpha._

## The Features object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| incomes_count | number | Number of income records |
| incomes_current_amount | number | Income for the current month |
| incomes_starting_amount | number | Income for the user's first month of working (starting income) |
| incomes_first_income_month_range | number | Number of months since the first income record, i.e. how many months the user has been working |
| incomes_latest_growth | number | Income growth from the same time last year |
| incomes_last18_months_max_amount_count | number | Number of months the user has received their maximum income |
| incomes_missing_month_count | number | Number of months with no income |
| incomes_missing_month_max | number | Longest duration without income (in months) |
| incomes_amount_sum | number | Total income received (lifetime) |
| incomes_amount_average | number | Average of monthly income received (lifetime) |
| incomes_amount_min | number | Smallest monthly income received (lifetime) |
| incomes_amount_max | number | Largest monthly income received (lifetime) |
| incomes_amount_median | number | Median of monthly incomes received (lifetime) |
| incomes_amount_std | number | Standard deviation of monthly incomes received (lifetime) |
| incomes_last3_months_amount_sum | number | Total income received (last 3 months) |
| incomes_last3_months_amount_average | number | Average of monthly income received (last 3 months) |
| incomes_last3_months_amount_min | number | Smallest monthly income received (last 3 months) |
| incomes_last3_months_amount_max | number | Largest monthly income received (last 3 months) |
| incomes_last3_months_amount_median | number | Median of monthly incomes received (last 3 months) |
| incomes_last3_months_amount_std | number | Standard deviation of monthly incomes received (last 3 months) |
| incomes_last6_months_amount_sum | number | Total income received (last 6 months) |
| incomes_last6_months_amount_average | number | Average of monthly income received (last 6 months) |
| incomes_last6_months_amount_min | number | Smallest monthly income received (last 6 months) |
| incomes_last6_months_amount_max | number | Largest monthly income received (last 6 months) |
| incomes_last6_months_amount_median | number | Median of monthly incomes received (last 6 months) |
| incomes_last6_months_amount_std | number | Standard deviation of monthly incomes received (last 6 months) |
| incomes_last9_months_amount_sum | number | Total income received (last 9 months) |
| incomes_last9_months_amount_average | number | Average of monthly income received (last 9 months) |
| incomes_last9_months_amount_min | number | Smallest monthly income received (last 9 months) |
| incomes_last9_months_amount_max | number | Largest monthly income received (last 9 months) |
| incomes_last9_months_amount_median | number | Median of monthly incomes received (last 9 months) |
| incomes_last9_months_amount_std | number | Standard deviation of monthly incomes received (last 9 months) |
| incomes_last12_months_amount_sum | number | Total income received (last 12 months) |
| incomes_last12_months_amount_average | number | Average of monthly income received (last 12 months) |
| incomes_last12_months_amount_min | number | Smallest monthly income received (last 12 months) |
| incomes_last12_months_amount_max | number | Largest monthly income received (last 12 months) |
| incomes_last12_months_amount_median | number | Median of monthly incomes received (last 12 months) |
| incomes_last12_months_amount_std | number | Standard deviation of monthly incomes received (last 12 months) |
| incomes_last18_months_amount_sum | number | Total income received (last 18 months) |
| incomes_last18_months_amount_average | number | Average of monthly income received (last 18 months) |
| incomes_last18_months_amount_min | number | Smallest monthly income received (last 18 months) |
| incomes_last18_months_amount_max | number | Largest monthly income received (last 18 months) |
| incomes_last18_months_amount_median | number | Median of monthly incomes received (last 18 months) |
| incomes_last18_months_amount_std | number | Standard deviation of monthly incomes received (last 18 months) |
| liabilities_loan_count | number | Number of loans (all liabilities) |
| liabilities_loan_amount_total | number | Total loan amount (all liabilities) |
| liabilities_loan_amount_average | number | Average loan amount (all liabilities) |
| liabilities_loan_amount_min | number | Smallest loan amount (all liabilities) |
| liabilities_loan_amount_max | number | Largest loan amount (all liabilities) |
| liabilities_loan_amount_std | number | Standard deviation of loan amounts (all liabilities) |
| liabilities_finished_loan_count | number | Number of finished loans |
| liabilities_outstanding_loan_count | number | Number of outstanding loans |
| liabilities_outstanding_amount_total | number | Total loan amount (outstanding liabilities only) |
| liabilities_outstanding_amount_average | number | Average loan amount (outstanding liabilities only) |
| liabilities_outstanding_amount_max | number | Largest loan amount (outstanding liabilities only) |
| liabilities_overdue_loan_count | number | Number of overdue loans |
| liabilities_overdue_amount_total | number | Total loan amount (overdue liabilities only) |
| liabilities_overdue_amount_average | number | Average loan amount (overdue liabilities only) |
| liabilities_payment_count | number | Number of loan payments pade |
| liabilities_payment_amount_sum | number | Total sum of payments made (all liabilities) |
| liabilities_payment_amount_average | number | Average amount of payments made (all liabilities) |
| liabilities_payment_amount_min | number | Smallest amount paid (all liabilities) |
| liabilities_payment_amount_max | number | Largest amount paid (all liabilities) |
| liabilities_payment_amount_median | number | Median amount paid (all liabilities) |
| liabilities_payment_amount_std | number | Standard deviation of amounts paid (all liabilities) |
| liabilities_ongoing_amortization_amount_sum | number | Total of all amortizations (ongoing liabilities only) |
| liabilities_ongoing_amortization_amount_average | number | Average amortization amount (ongoing liabilities only) |
| liabilities_ongoing_amortization_amount_min | number | Smallest amortization amount (ongoing liabilities only) |
| liabilities_ongoing_amortization_amount_max | number | Largest amortization amount (ongoing liabilities only) |
| liabilities_payment_amount_median | number | Median amortization amount (ongoing liabilities only) |
| liabilities_ongoing_amortization_amount_std | number | Standard deviation of amortization amounts (ongoing liabilities only) |
| identity_age | number | Current age of user |
| employments_current_status | string | Employment status, can be either `EMPLOYED`, `GIG`, or `UNEMPLOYED` |
| employments_employer_count | number | Number of unique employers |
| employments_current_tenure | number | Number of months at current employer |
| link_days_since_first | number | Number of days since first connection |
| link_days_since_last | number | Number of days since last connection |
| link_day3_count | number | Number of times user has connected in the last 3 days, `-999` if not subscribed to Multiple Application Warning  |
| link_day7_count | number | Number of times user has connected in the last 7 days, `-999` if not subscribed to Multiple Application Warning |
| link_day30_count | number | Number of times user has connected in the last 30 days, `-999` if not subscribed to Multiple Application Warning |
| link_day90_count | number | Number of times user has connected in the last 90 days, `-999` if not subscribed to Multiple Application Warning |
| link_day180_count | number | Number of times user has connected in the last 180 days, `-999` if not subscribed to Multiple Application Warning |
| link_day365_count | number | Number of times user has connected in the last 365 days, `-999` if not subscribed to Multiple Application Warning |
| link_day730_count | number | Number of times user has connected in the last 730 days, `-999` if not subscribed to Multiple Application Warning |

## Sample Features data

Estimated income is always returned as a monthly amount.

```json
"features": {
  "incomes_count": 2,
  "incomes_first_income_month_range": 3,
  "incomes_missing_month_max": 1,
  "incomes_missing_month_count": 1,
  "incomes_amount_sum": 17000,
  "incomes_amount_average": 8500,
  "incomes_amount_min": 8500,
  "incomes_amount_max": 8500,
  "incomes_amount_median": 8500,
  "incomes_amount_std": 0,
  "incomes_last3_months_amount_sum": 17000,
  "incomes_last3_months_amount_average": 8500,
  "incomes_last3_months_amount_min": 8500,
  "incomes_last3_months_amount_max": 8500,
  "incomes_last3_months_amount_median": 8500,
  "incomes_last3_months_amount_std": 0,
  "incomes_last6_months_amount_sum": 17000,
  "incomes_last6_months_amount_average": 8500,
  "incomes_last6_months_amount_min": 8500,
  "incomes_last6_months_amount_max": 8500,
  "incomes_last6_months_amount_median": 8500,
  "incomes_last6_months_amount_std": 0,
  "incomes_last9_months_amount_sum": 17000,
  "incomes_last9_months_amount_average": 8500,
  "incomes_last9_months_amount_min": 8500,
  "incomes_last9_months_amount_max": 8500,
  "incomes_last9_months_amount_median": 8500,
  "incomes_last9_months_amount_std": 0,
  "incomes_last12_months_amount_sum": 17000,
  "incomes_last12_months_amount_average": 8500,
  "incomes_last12_months_amount_min": 8500,
  "incomes_last12_months_amount_max": 8500,
  "incomes_last12_months_amount_median": 8500,
  "incomes_last12_months_amount_std": 0,
  "incomes_last18_months_amount_sum": 17000,
  "incomes_last18_months_amount_average": 8500,
  "incomes_last18_months_amount_min": 8500,
  "incomes_last18_months_amount_max": 8500,
  "incomes_last18_months_amount_median": 8500,
  "incomes_last18_months_amount_std": 0,
  "incomes_last18_months_max_amount_count": 2,
  "incomes_starting_amount": 8500,
  "incomes_current_amount": 8500,
  "incomes_latest_growth": -999,
  "liabilities_loan_count": 1,
  "liabilities_loan_amount_min": 16000,
  "liabilities_loan_amount_max": 16000,
  "liabilities_loan_amount_total": 16000,
  "liabilities_loan_amount_average": 16000,
  "liabilities_loan_amount_std": -999,
  "liabilities_finished_loan_count": 0,
  "liabilities_outstanding_loan_count": 1,
  "liabilities_outstanding_amount_max": 14599.76,
  "liabilities_outstanding_amount_total": 14599.76,
  "liabilities_outstanding_amount_average": 14599.76,
  "liabilities_overdue_loan_count": 0,
  "liabilities_overdue_amount_total": 0,
  "liabilities_overdue_amount_average": 0,
  "liabilities_payment_count": 24,
  "liabilities_payment_amount_sum": 80000,
  "liabilities_payment_amount_average": 20000,
  "liabilities_payment_amount_min": 10000,
  "liabilities_payment_amount_max": 30000,
  "liabilities_payment_amount_median": 20000,
  "liabilities_payment_amount_std": 0,
  "liabilities_ongoing_amortization_amount_sum": 80000,
  "liabilities_ongoing_amortization_amount_average": 20000,
  "liabilities_ongoing_amortization_amount_min": 10000,
  "liabilities_ongoing_amortization_amount_max": 30000,
  "liabilities_payment_amount_median": 20000,
  "liabilities_ongoing_amortization_amount_std": 0,
  "identity_age": 30,
  "employments_current_status": "EMPLOYED",
  "employments_employer_count": 3,
  "employments_current_tenure": 24,
  "link_days_since_first": 21,
  "link_days_since_last": 4,
  "link_day3_count": 0,
  "link_day7_count": 2,
  "link_day30_count": 5,
  "link_day90_count": 5,
  "link_day180_count": 5,
  "link_day365_count": 5,
  "link_day730_count": 5
}
```

## Endpoints

| Endpoint                                                        |                      |
| :-------------------------------------------------------------- | :------------------- |
| [Retrieve all insights](/reference/list-insights)      | `GET /insights`      |
| [Retrieve one insight record](/reference/get-feature-insight) | `GET /insights/{id}` |

## Webhooks

### `INSIGHT_ADDED`

Fired when insights data calculated from shared user data is added.

```json
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INSIGHT_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "id": "insight-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```
