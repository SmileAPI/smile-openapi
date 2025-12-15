---
title: Insights
category:
  uri: '/branches/1.0-Chinese/categories/reference/用户数据'
slug: insights
content:
  excerpt: ''
---

Smile Insights API 根据 [Users](/reference/users) 的可用数据（如收入和就业数据）提供常用计算方法计算出的风险因子。

无论是为金融服务还是为就业目的评估候选人，这些因子都有助于决策过程。在不同阶段或信息类别中为您提供平均值、最小值、最大值等常用计算值。

Insights 可从以下数据源获得：

| 数据源                                  | Insight 类型                                  |
|--------------------------------------|---------------------------------------------|
| Social Security Services	            | Identity, Employments, Incomes, Liabilities |
| Government Service Insurance System	 | Identity, Employments, Incomes              |
| National Health Insurance Agency	    | Identity, Incomes                           |
| National housing provident fund      | Identity, Employments, Incomes, Liabilities |

> 📘 注意
>
> 在获取我们的 Insights 数据时，您可能会得到以下值：
> 
> * -999 - 数据源中的数据为空、缺失或不可用
> * -998 - 在计算因子值时出现错误


## 身份与就业数据因子( Insight )

身份和就业数据因子可帮助您无需从数据源的原始数据中计算，便可快速汇总这些用户信息。

| Insight 变量名                  | 详情                                        |
|------------------------------|-------------------------------------------|
| `identity_age`               | 用户当前的年龄                                   |
| `employments_current_status` | 就业状态，可以是`EMPLOYED`, `GIG`, 或 `UNEMPLOYED` |
| `employments_employer_count` | 唯一雇主的数量                                   |
| `employments_current_tenure` | 在当前雇主处工作的月数                               |

## 收入数据因子( Insights ) 

收入数据因子可通过用户不同月份的收入记录（基于 [Estimated Income](/reference/estimated-incomes)）为您提供一系列常用计算结果。这为您节省了从数据源原始数据中计算这些信息所需的时间和资源。

> 📘 注意
>
> 对于 **社保平台**，数据源发布收入相关数据的时间可能会延迟 1-2 个月。Smile 会考虑到这一点，但重要的是您需要注意这种可能的数据差异，并将其添加到计算公式中。

| Insight 变量名                                                                                                                                                                                                        | 详情                      |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| `incomes_count`                                                                                                                                                                                                    | 收入记录的数量                 |
| `incomes_current_amount`                                                                                                                                                                                           | 当月收入                    |
| `incomes_starting_amount`                                                                                                                                                                                          | 用户第一个月的工作收入（起始收入）       |
| `incomes_first_income_month_range`                                                                                                                                                                                 | 第一条收入记录以来的月数，即用户工作了多少个月 |
| `incomes_latest_growth`                                                                                                                                                                                            | 与去年同期相比的收入增长            |
| `incomes_last18_months_max_amount_count`                                                                                                                                                                           | 用户获得最高收入的月份数            |
| `incomes_missing_month_count`                                                                                                                                                                                      | 无收入的月数                  |
| `incomes_missing_month_max`                                                                                                                                                                                        | 无收入的最长持续时间（月）           |
| `incomes_amount_sum` `incomes_last3_months_amount_sum` `incomes_last6_months_amount_sum` `incomes_last9_months_amount_sum` `incomes_last12_months_amount_sum` `incomes_last18_months_amount_sum`                   | 所得收入的总额（终生和每月期限）        |
| `incomes_amount_avg` `incomes_last3_months_amount_avg` `incomes_last6_months_amount_avg` `incomes_last9_months_amount_avg` `incomes_last12_months_amount_avg` `incomes_last18_months_amount_avg`                   | 所得收入的平均值（终生和每月期限）       |
| `incomes_amount_min` `incomes_last3_months_amount_min` `incomes_last6_months_amount_min` `incomes_last9_months_amount_min` `incomes_last12_months_amount_min` `incomes_last18_months_amount_min`                   | 所得收入的最小值（终生和每月期限）       |
| `incomes_amount_max` `incomes_last3_months_amount_max` `incomes_last6_months_amount_max` `incomes_last9_months_amount_max` `incomes_last12_months_amount_max` `incomes_last18_months_amount_max`                   | 所得收入的最大值（终生和每月期限）       |
| `incomes_amount_median` `incomes_last3_months_amount_median` `incomes_last6_months_amount_median` `incomes_last9_months_amount_median` `incomes_last12_months_amount_median` `incomes_last18_months_amount_median` | 所得收入的中位数（终生和每月期限）       |
| `incomes_amount_std` `incomes_last3_months_amount_std` `incomes_last6_months_amount_std` `incomes_last9_months_amount_std` `incomes_last12_months_amount_std` `incomes_last18_months_amount_std`                   | 所得收入的标准差（终生和每月期限）       |

## 负债数据因子( Insights )

负债数据因子可帮助您无需从数据源的原始数据中计算，便可快速汇总查看用户的贷款信息。

| Insight 变量名                  | 详情                                                                                                      |
|---|---------------------------------------------------------------------------------------------------------|
| `liabilities_loan_count` | 贷款数量（终生）                                                                                                |
| `liabilities_loan_amount_total` `liabilities_loan_amount_average` `liabilities_loan_amount_min` `liabilities_loan_amount_max` `liabilities_loan_amount_std` | 所有贷款的总额、平均值、最小值、最大值和标准差                                                                                 |
| `liabilities_finished_loan_count` | 已完成的贷款数量                                                                                                |
| `liabilities_outstanding_loan_count` | 未偿还的贷款数量                                                                                                |
| `liabilities_outstanding_amount_total` `liabilities_outstanding_amount_average` `liabilities_outstanding_amount_max` | 仅以未偿贷款计算的贷款总额、平均贷款额和最大贷款额                                                                               |
| `liabilities_overdue_loan_count` | 逾期贷款的数量                                                                                                 |
| `liabilities_overdue_amount_total` `liabilities_overdue_amount_average` | 仅指逾期贷款总额和所有逾期贷款的平均金额                                                                                    |
| `liabilities_payment_count` | 已支付贷款的次数                                                                                                |
| `liabilities_payment_amount_sum` `liabilities_payment_amount_average` `liabilities_payment_amount_min` `liabilities_payment_amount_max` `liabilities_payment_amount_median` `liabilities_payment_amount_std` |    所有贷款的总还款额、平均还款额、最低还款额、最高还款额、中位数和标准差    |
| `liabilities_ongoing_amortization_amount_sum` `liabilities_ongoing_amortization_amount_average` `liabilities_ongoing_amortization_amount_min` `liabilities_ongoing_amortization_amount_max` `liabilities_ongoing_amortization_amount_median` `liabilities_ongoing_amortization_amount_std` | 持续贷款的总摊销额、平均摊销额、最低摊销额、最高摊销额、中位数和标准差 |

## 链接数据因子( Insights ) 

Links 是 [Multiple Application Warning](/reference/links) 服务的支柱，如果同时选择了 MAW 和 Insights 服务，我们还会额外提供与用户链接活动相关的 Insights 信息。这些信息可轻松纳入专有数据模型，以便改进信贷决策过程。

| Insight 变量名                  | 详情                                                                                                      |
|---|---|
| `link_days_since_first` | 自首次连接起的天数 |
| `link_days_since_last` | 距离上次连接的天数 |
| `link_day3_count` | 用户在过去 3 天内的连接次数 |
| `link_day7_count` | 用户在过去 7 天内的连接次数|
| `link_day30_count` | 用户在过去 30 天内的连接次数 |
| `link_day90_count` | 用户在过去 90 天内的连接次数 |
| `link_day180_count` | 用户在过去 180 天内的连接次数 |
| `link_day365_count` |用户在过去 365 天内的连接次数 |
| `link_day730_count` | 用户在过去 730 天内的连接次数 |

_Insights 目前处于 alpha 阶段。_

## Features 对象

| 属性                                              | 类型     | 详情                                                             |
|:------------------------------------------------|:-------|:---------------------------------------------------------------|
| incomes_count                                   | number | 收入记录的数量                                                        |
| incomes_current_amount                          | number | 当月的收入                                                          |
| incomes_starting_amount                         | number | 用户工作第一个月的收入（起始收入）                                              |
| incomes_first_income_month_range                | number | 第一条收入记录以来的月数，即用户工作了多少个月                                        |
| incomes_latest_growth                           | number | 与去年同期相比的收入增长情况                                                 |
| incomes_last18_months_max_amount_count          | number | 用户获得最高收入的月份数                                                   |
| incomes_missing_month_count                     | number | 没有收入的月份数                                                       |
| incomes_missing_month_max                       | number | 没有收入的最长持续时间（月）                                                 |
| incomes_amount_sum                              | number | 所得收入的总额（终生）                                                    |
| incomes_amount_average                          | number | 月平均收入（终生）                                                      |
| incomes_amount_min                              | number | 每月所得收入的最小值（终生）                                                 |
| incomes_amount_max                              | number | 每月所得收入的最大值（终生）                                                 |
| incomes_amount_median                           | number | 每月所得收入的中位数（终生）                                                 |
| incomes_amount_std                              | number | 每月所得收入的标准差（终生）                                                 |
| incomes_last3_months_amount_sum                 | number | 所得收入的总额（最近 3 个月）                                               |
| incomes_last3_months_amount_average             | number | 月平均收入（最近 3 个月）                                                 |
| incomes_last3_months_amount_min                 | number | 每月所得收入的最小值（最近 3 个月）                                            |
| incomes_last3_months_amount_max                 | number | 每月所得收入的最大值（最近 3 个月）                                            |
| incomes_last3_months_amount_median              | number | 每月所得收入的中位数（最近 3 个月）                                            |
| incomes_last3_months_amount_std                 | number | 每月所得收入的标准差（最近 3 个月）                                            |
| incomes_last6_months_amount_sum                 | number | 所得收入的总额（最近 6 个月）                                               |
| incomes_last6_months_amount_average             | number | 月平均收入（最近 6 个月）                                                 |
| incomes_last6_months_amount_min                 | number | 每月所得收入的最小值（最近 6 个月）                                            |
| incomes_last6_months_amount_max                 | number | 每月所得收入的最大值（最近 6 个月）                                            |
| incomes_last6_months_amount_median              | number | 每月所得收入的中位数（最近 6 个月）                                            |
| incomes_last6_months_amount_std                 | number | 每月所得收入的标准差（最近 6 个月）                                            |
| incomes_last9_months_amount_sum                 | number | 所得收入的总额（最近 9 个月）                                               |
| incomes_last9_months_amount_average             | number | 月平均收入（最近 9 个月）                                                 |
| incomes_last9_months_amount_min                 | number | 每月所得收入的最小值（最近 9 个月）                                            |
| incomes_last9_months_amount_max                 | number | 每月所得收入的最大值（最近 9 个月）                                            |
| incomes_last9_months_amount_median              | number | 每月所得收入的中位数（最近 9 个月）                                            |
| incomes_last9_months_amount_std                 | number | 每月所得收入的标准差（最近 9 个月）                                            |
| incomes_last12_months_amount_sum                | number | 所得收入的总额（最近 12 个月）                                              |
| incomes_last12_months_amount_average            | number | 月平均收入（最近 12 个月）                                                |
| incomes_last12_months_amount_min                | number | 每月所得收入的最小值（最近 12 个月）                                           |
| incomes_last12_months_amount_max                | number | 每月所得收入的最大值（最近 12 个月）                                           |
| incomes_last12_months_amount_median             | number | 每月所得收入的中位数（最近 12 个月）                                           |
| incomes_last12_months_amount_std                | number | 每月所得收入的标准差（最近 12 个月）                                           |
| incomes_last18_months_amount_sum                | number | 所得收入的总额（最近 18 个月）                                              |
| incomes_last18_months_amount_average            | number | 月平均收入（最近 18 个月）                                                |
| incomes_last18_months_amount_min                | number | 每月所得收入的最小值（最近 18 个月）                                           |
| incomes_last18_months_amount_max                | number | 每月所得收入的最大值（最近 18 个月）                                           |
| incomes_last18_months_amount_median             | number | 每月所得收入的中位数（最近 18 个月）                                           |
| incomes_last18_months_amount_std                | number | 每月所得收入的标准差（最近 18 个月）                                           |
| liabilities_loan_count                          | number | 贷款数量（所有负债）                                                     |
| liabilities_loan_amount_total                   | number | 贷款总额（所有负债）                                                     |
| liabilities_loan_amount_average                 | number | 平均贷款金额（所有负债）                                                   |
| liabilities_loan_amount_min                     | number | 最小贷款金额（所有负债）                                                   |
| liabilities_loan_amount_max                     | number | 最大贷款金额（所有负债）                                                   |
| liabilities_loan_amount_std                     | number | 贷款金额标准差（所有负债）                                                  |
| liabilities_finished_loan_count                 | number | 已完成的贷款数量                                                       |
| liabilities_outstanding_loan_count              | number | 未偿还的贷款数量                                                       |
| liabilities_outstanding_amount_total            | number | 贷款总额（仅指未偿还债务）                                                  |
| liabilities_outstanding_amount_average          | number | 平均贷款额（仅指未偿还债务）                                                 |
| liabilities_outstanding_amount_max              | number | 最大贷款金额（仅指未偿还债务）                                                |
| liabilities_overdue_loan_count                  | number | 逾期贷款的数量                                                        |
| liabilities_overdue_amount_total                | number | 贷款总额（仅指逾期债务）                                                   |
| liabilities_overdue_amount_average              | number | 平均贷款金额（仅指逾期债务）                                                 |
| liabilities_payment_count                       | number | 已支付贷款的次数                                                       |
| liabilities_payment_amount_sum                  | number | 已支付总额（所有债务）                                                    |
| liabilities_payment_amount_average              | number | 平均支付金额（所有债务）                                                   |
| liabilities_payment_amount_min                  | number | 已支付的最小金额（所有债务）                                                 |
| liabilities_payment_amount_max                  | number | 已支付的最大金额（所有债务）                                                 |
| liabilities_payment_amount_median               | number | 已支付金额的中位数（所有债务）                                                |
| liabilities_payment_amount_std                  | number | 已支付金额的标准差（所有债务）                                                |
| liabilities_ongoing_amortization_amount_sum     | number | 所有摊销总额（仅指持贷款）                                                  |
| liabilities_ongoing_amortization_amount_average | number | 平均摊销额（仅指持续贷款）                                                  |
| liabilities_ongoing_amortization_amount_min     | number | 最小摊销额（仅指持续贷款）                                                  |
| liabilities_ongoing_amortization_amount_max     | number | 最大摊销额（仅指持续贷款）                                                  |
| liabilities_payment_amount_median               | number | 摊销额中位数（仅指持续贷款）                                                 |
| liabilities_ongoing_amortization_amount_std     | number | 摊销金额的标准差（仅指持续贷款）                                               |
| identity_age                                    | number | 用户目前的年龄                                                        |
| employments_current_status                      | string | 就业状态，可以是 `EMPLOYED`, `GIG`, 或`UNEMPLOYED`                      |
| employments_employer_count                      | number | 唯一雇主的数量                                                        |
| employments_current_tenure                      | number | 在现任雇主处工作的月数                                                    |
| link_days_since_first | number | 自首次连接起的天数                                                      |
| link_days_since_last | number | 距离上次连接的天数                                                      |
| link_day3_count | number | 用户在过去 3 天内的连接次数，如果未订阅 Multiple Application Warning，则为 `-999`   |
| link_day7_count | number | 用户在过去 7 天内的连接次数，如果未订阅 Multiple Application Warning，则为 `-999`   |
| link_day30_count | number | 用户在过去 30 天内的连接次数，如果未订阅 Multiple Application Warning，则为 `-999`  |
| link_day90_count | number | 用户在过去 90 天内的连接次数，如果未订阅 Multiple Application Warning，则为 `-999`  |
| link_day180_count | number | 用户在过去 180 天内的连接次数，如果未订阅 Multiple Application Warning，则为 `-999` |
| link_day365_count | number | 用户在过去 365 天内的连接次数，如果未订阅 Multiple Application Warning，则为 `-999` |
| link_day730_count | number | 用户在过去 730 天内的连接次数，如果未订阅 Multiple Application Warning，则为 `-999` |

## Features 样例数据

估算的收入总是以月为单位返回。

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
  "employments_current_tenure": 24
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

## 端点

| 端点                                   |                      |
|:-------------------------------------| :------------------- |
| [获取因子数据列表](/reference/list-insights) | `GET /insights`      |
| [获取一条因子数据](/reference/get-feature-insight)  | `GET /insights/{id}` |

## Webhooks

### `INSIGHT_ADDED`

添加有关用户的因子数据时，事件发送格式如下：

```json
{
  "id": "123abc456def789abc123def456abc78",
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
