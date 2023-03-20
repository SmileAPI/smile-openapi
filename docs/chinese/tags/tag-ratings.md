---
title: Ratings
excerpt: ""
category: 62ce2a159aafea009af30dab  
slug: ratings
---

Ratings 数据端点提供用户在[ Provider ](/reference/providers)平台上的评级信息。如果所选平台有这个用户的该项数据，Smile 就会为您检索该数据，并会根据用户的当前评分和平台上允许的最大评分来计算一个百分比的评分。

如果有的话，Smile 还检索与评级有关的其他信息，如收到的评论和喜欢，以及完成的工作，作为决策的额外数据端点。

在用户通过 Smile 连接一个[ Account ](/reference/accounts)后，Smile 检索用户的评级数据（如果有的话）。您可以监听部分事件和 webhooks（概述如下），以确定他们的评级数据何时准备好。

## 评级对象

| 属性                   | 类型     | 详情                                                               |
|:---------------------|:-------|:-----------------------------------------------------------------|
| id                   | string | Smile Network 上评级信息的唯一ID                                         |
| currentRating        | number | 用户从提供商那里得到的当前评级分数。如果没有评级分数，则为空                                   |
| maxRating            | number | 提供商所提供的最大可能评级。如果没有评级分数，则为空                                       |
| calculatedPercentage | number | 以百分比表示的当前评级。计算方法是：`currentRating / maxRating x 100`。如果没有评级分数，则为空 |
| reviewsReceived      | number | 如果可以从提供商获得的话，代表收到的评论数量。如果没有，则为空                                  |
| likesReceived        | number | 如果可以从提供商获得的话，代表收到的推荐、喜欢或赞扬的数量。如果没有，则为空                           |
| jobsCompleted        | number | 如果可以从提供商获得的话，代表用户在该平台上完成的工作数量。如果没有，则为空                           |
| metadata             | object | 包含有关该评级数据端点的数据。详见下面的对象                                           |


### 数据对象

| 属性                     | 类型        | 详情                                                             |
|:-----------------------|:----------|:---------------------------------------------------------------|
| createdAt              | date-time | 创建评级的日期/时间                                                     |
| accountId `Deprecated` | string    | 用户在 Smile Network 中的账户 ID                                      |
| sourceId               | string    | 用户在 Smile Network 中的账户或 archive 的 ID                           |
| sourceType             | string    | 表示与此对象相关的来源是账户还是 archive 。可能的值有：`ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId             | string    | 用户账户的数据提供商的 ID                                                 |
| userId                 | string    | Smile Network 上用户的 ID                                          |


## 评级数据样例

``` json
[{
    "id": "r-123abc456def789abc123def456abc78",
    "currentRating": 4,
    "maxRating": 5,
    "calculatedPercentage": 80,
    "reviewsReceived": 27,
    "likesReceived": 82,
    "jobsCompleted": 125,
    "metadata": {
        "createdAt": "2022-09-02T23:36:12Z",
        "sourceId": "a-123abc456def789abc123def456abc78",
        "sourceType": "ACCOUNT",
        "userId": "tenantId-123abc456def789abc123def456abc78",
        "providerId": "xyzgigcompany"
    }
}]
```

## 端点

| 端点                                    | |
|:--------------------------------------| :---- |
| [获取评级数据列表](/reference/list-ratings-1) | `GET /ratings` |
| [获取一条评级记录](/reference/get-rating-1)   | `GET /ratings/{id}` |

## Webhooks

### `RATING_ADDED`

添加有关用户的评级数据时，事件发送格式如下：

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "RATING_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "ratingId": "r-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

### `TASK_FINISHED`

用户账户的数据同步进程结束时，事件发送格式如下：

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "TASK_FINISHED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "providers": [
      "abccorp"
    ],
    "datapoints": [
      "IDENTITIES",
      "RATINGS"
    ]
  }
}
```
