---
title: Providers  
excerpt: ""  
category: 62ce2a159aafea009af30daa  
slug: providers-1
---
Smile maintains a long list of providers that can be retrieved if you require this information in your implementation. These providers are a combination of:

1. data providers that your customers can connect to, in order to share their data with you, and
2. employers that may or may not be mapped to a specific payroll system so your customers can share their data with you.

Where there is no payroll system mapped to a specific employer, Smile recommends a fallback mechanism of allowing the user to connect and share their social security records in order to provider identity and limited income information.

## The Provider object

| Attribute         | Type             | Description                                                                                   |
| :---------------- | :--------------- | :-------------------------------------------------------------------------------------------- |
| id                | string           | Unique ID of the provider                                                                     |
| name              | string           | Name of the data provider                                                                     |
| longName          | string           | Full name or legal business entity name of the provider                                       |
| logoUrl           | string           | URL to the provider's logo                                                                    |
| type              | string           | Type of provider, can be one of the following: `GIG`, `GOVERNMENT`, `SYSTEM`, `EMPLOYER`      |
| typeLabel         | string           | Type label of provider, such as "Gig Platform" for type `GIG`                                 |
| subType           | string           | Where applicable, the subset type of the provider, such as `SERVICES`, `TRANSPORTATION`, etc. |
| subTypeLabel      | string           | Subtype label of provider                                                                     |
| active            | boolean          | Indicates whether data provider integration is working                                        |
| enabled           | boolean          | Indicates whether data provider is enabled or access is allowed                               |
| mfa               | boolean          | Indicates whether data provider requires multi-factor authentication                          |
| accountConnection | boolean          | Indicates whether a real-time account connection is available for this data provider          |
| supported         | array of strings | List of supported data points for this employment data provider                               |

## Sample Provider data

```
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



## Endpoints

| Endpoint                                                  |                       |
| :-------------------------------------------------------- | :-------------------- |
| [Retrieve all providers](/reference/list-providers)       | `GET /providers`      |
| [Retrieve one provider record](/reference/get-provider-1) | `GET /providers/{id}` |