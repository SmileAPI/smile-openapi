---
title: Estimated Incomes
excerpt: ""  
category: 631853c44ea4ae04ab847012
slug: estimated-incomes
---

在收入信息有限的情况下，Smile 还可以从二级数据类型中提供额外的衍生收入信息，比如:

- 社会保障缴费
- 年收入
- 从交易中计算出的收益

根据数据提供商提供的现有历史数据，我们预估用户的月收入，并通过 API 展示该信息，为您节省额外的计算开销。

_预估收入目前在公测阶段。_

## 预估收入的对象

| 属性  | 类型     | 详情                          |
| :--------- |:-------|:----------------------------|
| id         | string | 该预估收入对象的唯一ID                |
| month      | string | 该预估收入所属的月份，格式为 "YYYY-MM"    |
| currency   | string | 该预估收入的货币，以标准的三个字母ISO代码表示    |
| baseAmount | number | 收入金额                        |
| metadata   | object | 有关该资源的其他信息，如创建日期、数据来源、用户ID等 |

## 预估收入数据样本

预估收入总是返回每月的总额。

``` json
[{  
    "id": "einc-123abc456def789abc123def456abc78",  
    "month": "2022-07",  
    "currency": "PHP",  
    "baseAmount": 8500,  
    "metadata": {  
        "createdAt": "2022-09-01T01:44:18Z",  
        "sourceId": "a-123abc456def789abc123def456abc78",  
        "sourceType": "ACCOUNT",  
        "userId": "tenantId-123abc456def789abc123def456abc78",  
        "providerId": "abccorp",  
        "accountId": "a-123abc456def789abc123def456abc78"  
    }  
}, {  
    "id": "einc-123abc456def789abc123def456abc78",  
    "month": "2022-06",  
    "currency": "PHP",  
    "baseAmount": 8500,  
    "metadata": {  
        "createdAt": "2022-09-01T01:44:18Z",  
        "sourceId": "a-123abc456def789abc123def456abc78",  
        "sourceType": "ACCOUNT",  
        "userId": "tenantId-123abc456def789abc123def456abc78",  
        "providerId": "abccorp",  
        "accountId": "a-123abc456def789abc123def456abc78"  
    }  
}]
```



## 端点

| 端点                                     |                      |
|:---------------------------------------| :------------------- |
| [获取预估收入列表](/reference/list-eincomes)   | `GET /eincomes`      |
| [获取一个预估收入的记录](/reference/get-eincomes) | `GET /eincomes/{id}` |

## Webhooks

### `EINCOMES_ADDED`

当通过用户的交易、缴费数据或者其他数据推算出用户的预估收入时，此 Webhook 事件会被触发。

``` json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "EINCOMES_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "count": 0
  }
}
```