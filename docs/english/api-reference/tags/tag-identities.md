---
title: Identities
excerpt: ""
category: 6294c158bef44e0098ed88a1
slug: identities
---

The Identities data point, in most cases, contain the meat of the data about the user as made available from the provider. Putting together various identity data from different providers can give you a fuller view of the user's information as well as opportunities to verify their data across multiple providers.

After the user connects an [Account](/reference/accounts) via Smile, Smile retrieves the user's Identity data from the [Provider](/reference/providers) and makes it available for retrieval. You may listen for the appropiate events and webhooks (outlined below) in order to determine when their Identity data is ready.

## Verifying User Identity

Most platforms will contain at least a first name and last name, with middle names and suffixes varying from platform to platform. You can use these information to match your customer's provided information with data from verifiable sources, such as government records and social security agencies.

## Fallback Methods

If the sources your user provided are not enough you can also make use of Smile's [Archive API](/reference/archives) to encourage the user to upload their own IDs. This can be a drivers' license, passport, or even banking or payroll documents.

## The Identity object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the identity information on the Smile Network |
| fullName | string | Full name of the user, if available from the provider. Null if not available |
| firstName | string | First name of the user, if available from the provider. Null if not available |
| middleName | string | Middle name of the user, if available from the provider. Null if not available |
| lastName | string | Last name of the user, if available from the provider. Null if not available |
| suffix | string | Suffix of the user (i.e. Jr, Ss, MD, etc), if available from the provider. Null if not available |
| gender | string | Gender of the user, if available from the provider. Null if not available. Possible values: `Male`, `Female`, `Non-binary` |
| dob | date | Birth date of the user, if available from the provider. Null if not available |
| maritalStatus | string | Marital status of the user, if available from the provider. Null if not available. Possible values: `Divorced`, `Lifetime Partner`, `Married`, `Separated`, `Single`, `Widowed` |
| countryResidence | string | Country of residence of the user, if available from the provider. Null if not available. Provided in 2-character alpha ISO-3166 codes, i.e. `PH`, `ID`, etc. |
| citizenship | string | Citizenship status of the user in their country of residences, if available from the provider. Null if not available. Possible values: `Citizen`, `Resident Alien`, `Non-resident Alien`, `Undocumented`, `Others` |
| photoUrl | string | Fully-formed URL to user's photo or avatar, if available from the provider. Null if not available |
| referenceId | string | Reference ID of the user's profile from the provider, if available. Null if not available |
| profileUrl | string | Fully-formed URL to user's public profile with the provider, , if available. Null if not available |
| emails | array | Contains email address(es) of the user as available from the provider. See object below |
| phones | array | Contains phone numbers of the user as available from the provider. See object below |
| socialProfiles | array | Contains any social profiles connected to the user's account as available from the provider. See object below |
| addresses | array | Contains physical addresses of the user as available from the provider. See object below |
| metadata | object | Contains data about this identity data point. See object below |

### The Email Address object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| address | string | Email address of the user |
| type | string | Type of email address provided by the user. Possible values: `Primary`, `Secondary`, `Work`, `Personal` |


### The Phone Number object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| number | string | Phone number of the user in international E.164 format |
| type | string | Type of phone number provided by the user. Possible values: `Mobile`, `Fixed`, `Unspecified` |


### The Social Profiles object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| socialUrl | string | Fully-formed URL to the user's public social media page |
| type | string | Provider of social media account to the user. Possible values: `Twitter`, `Facebook`, `LinkedIn`, `Others` |


### The Address object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| fullAddress | string | Full physical address of the user |
| line1 | string | First line of the user's address, i.e. street address |
| line2 | string | Second line of the user's address |
| city | string | City of the user's address |
| region | string | Geographic region of the user's address such as state or province |
| zip | string | Zip or post code of the user's address |
| country | string | Country of the user's address. Provided in 2-character alpha ISO-3166 codes, i.e. `PH`, `ID`, etc. |
| latitude | string | Latitude coordinates of the user's address |
| longitude | string | Longitude coordinates of the user's address |
| type | string | Type of address provided by the user. Possible values: `Primary`, `Secondary` |


### The Meta Data object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| createdAt | date-time | Date/time when the account record was created |
| itemCreatedAt | date-time | Date/time when the identity record was created |
| accountId `Deprecated` | string | ID of the user's account in the Smile Network |
| sourceId | string | ID of the user's account or archive in the Smile Network |
| sourceType | string | Indicates whether the source associated with this object is an account or archive. Possible values: `ACCOUNT`, `UPLOAD`, `ARCHIVE` |
| providerId | string | ID of the data provider of the user's account |
| userId | string | ID of the user on the Smile Network |


## Sample Identity data

```json
{
  "id": "i-123abc456def789abc123def456abc78",
  "fullName": "George Cimafranca Palomero, Jr",
  "firstName": "George",
  "middleName": "Cimafranca",
  "lastName": "Palomero",
  "suffix": "Jr",
  "gender": "Male",
  "dob": "1970-08-24",
  "maritalStatus": "Married",
  "countryResidence": "PH",
  "citizenship": "Citizen",
  "photoUrl": "https://cdn.smileapi.io/image/avatar/v20211115191600/george.jpg",
  "referenceId": null,
  "profileUrl": null,
  "emails": [
    {
      "address": "gpalomero1234@smileapi.io",
      "type": "Primary"
    }
  ],
  "phones": [
    {
      "number": "+639559991234",
      "type": "Mobile"
    }
  ],
  "socialProfiles": [
    {
      "socialUrl": "https://www.facebook.com/gpalomero1234",
      "type": "Facebook"
    }
  ],
  "addresses": [
    {
      "fullAddress": "12 Maybunga St, Barangay Paraiso, Pasig City, NCR, 1600, PH",
      "line1": "12 Maybunga St",
      "line2": "Barangay Paraiso",
      "city": "Pasig City",
      "region": "NCR",
      "zip": "1600",
      "country": "PH",
      "latitude": "14.573454",
      "longitude": "121.085042",
      "type": "Primary"
    }
  ],
  "metadata": {
    "createdAt": "2022-08-19T07:29:08Z",
    "itemCreatedAt": "2022-08-24T05:24:37Z",
    "sourceId": "a-123abc456def789abc123def456abc78",
    "sourceType": "ACCOUNT",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "providerId": "abccorp"
  }
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all identities](/reference/list-identities-1) | `GET /identities` |
| [Retrieve one identity](/reference/get-identity-1) | `GET /identities/{id}` |

## Webhooks

### `IDENTITY_ADDED`

Sent when identity data about a user is added from the provider.

```json
{
  "id": "123abc456def789abc123def456abc78",
  "version": 1,
  "type": "IDENTITY_ADDED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "accountId": "a-123abc456def789abc123def456abc78",
    "identityId": "i-123abc456def789abc123def456abc78",
    "providers": [
      "abccorp"
    ]
  }
}
```

### `TASK_FINISHED`

Sent when the full data sync task process for a user's account is finished.

```json
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
      "INCOMES"
    ]
  }
}
```
