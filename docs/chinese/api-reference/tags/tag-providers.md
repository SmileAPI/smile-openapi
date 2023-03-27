---
title: Providers  
excerpt: ""  
category: 62ce2a159aafea009af30daa  
slug: providers
---
如果您需要就业数据提供商的信息，您可以从 Smile 维护着的一个长名单中检索到。这些提供商包含以下分类：

1. 用户直接连接的提供商数据
2. 用户的雇主使用的薪资系统数据

如果没有匹配到特定雇主的薪资系统，Smile 建议采用一种后备机制，允许用户连接并分享他们的社会保障记录，以便提供身份和有限的收入信息。

## 数据提供商对象

| 属性         | 类型               | 详情                                                    |
| :---------------- |:-----------------|:------------------------------------------------------|
| id                | string           | 提供商唯一的 ID                                             |
| name              | string           | 数据提供商的名称                                              |
| longName          | string           | 提供商的全名或合法商业实体名称                                       |
| logoUrl           | string           | 链接到提供商商标的 URL                                         |
| type              | string           | 提供商的类型，可以是以下之一：`GIG`、`GOVERNMENT`、`SYSTEM`、`EMPLOYER` |
| typeLabel         | string           | 提供商的类型标签，如 "Gig Platform" 代表 `GIG` 类型                 |
| subType           | string           | 提供商的子集类型（如适用），如 `SERVICES`、`TRANSPORTATION` 等。        |
| subTypeLabel      | string           | 提供商的子类型标签                                             |
| active            | boolean          | 表示数据提供商的集成是否在工作                                       |
| enabled           | boolean          | 表明数据提供商是否被启用或允许访问                                     |
| mfa               | boolean          | 表示数据提供商是否需要多因素认证                                      |
| accountConnection | boolean          | 表示该数据提供商的实时账户连接是否可用                                   |
| supported         | array of strings | 该就业数据提供商支持的数据点列表                                      |

## 提供商数据样本

```json
[{
    "id": "abccorp",
    "name": "ABC Corporation",
    "longName": "ABC Coporation Inc.",
    "logoUrl": "https://cdn.smileapi.io/filename.png",
    "type": "EMPLOYER",
    "typeLabel": "Employer",
    "subType": "ISIC-G",
    "subTypeLabel": "Wholesale and retail trade; repair of motor vehicles and motorcycles",
    "active": true,
    "enabled": true,
    "mfa": false,
    "accountConnection": false,
    "supported": []
},{
    "id": "abcplatform",
    "name": "ABC Platform",
    "longName": "ABC Platform Pte. Ltd.",
    "logoUrl": "https://cdn.smileapi.io/filename.png",
    "type": "GIG",
    "typeLabel": "Gig Platform",
    "subType": "SERVICES",
    "subTypeLabel": "Professional Services",
    "active": true,
    "enabled": true,
    "mfa": true,
    "accountConnection": true,
    "supported": [
        "IDENTITIES",
        "TRANSACTIONS",
        "RATINGS"
    ]
}]
```



## 端点

| 端点                                     |                       |
|:---------------------------------------| :-------------------- |
| [获取提供商列表](/reference/list-providers)   | `GET /providers`      |
| [获取一条提供商记录](/reference/get-provider-1) | `GET /providers/{id}` |