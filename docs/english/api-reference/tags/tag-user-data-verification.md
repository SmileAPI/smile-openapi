---
title: Data Verification
excerpt: ''
category: 66611ec162e8c700572c4be3
slug: user-data-verification
---

The Smile Snap Data Verification API allows developers to verify a person's provided data against authoritative sources without the need for a user login. There is also a Query mode for this service, see [Profile Data](https://docs.getsmileapi.com/reference/query-identity).

This API can be used to verify the person's provided data to check for accuracy and minimize fraud. Smile currently supports verifying via the SSS ID number. Other data sources will be onboarded soon.

The following data are required for the query:

1. ID Type
2. ID Number
3. First Name

You may then send additional information (see the Verify Identity endpoint) in order to receive information if the data provided matches data from authoritative sources.

Smile checks for an 80% name match against the provided ID type and number before continuing with the verification matching.

## Result object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| nameMatchScore | number | Percentage match of the provided name |
| dobMatched | boolean | Match result for date of birth. Null if not specified in the query |
| mobileMatched | boolean | Match result for mobile number. Null if not specified in the query |
| emailMatched | boolean | Match result for email address. Null if not specified in the query |
| genderMatched | boolean | Match result for gender. Null if not specified in the query |
| maritalStatusMatched | boolean | Match result for marital status. Null if not specified in the query |

## Sample result data

### Data match

If the combination of the first and last name matches at least 80% against the name registered for the ID number provided, the match result will be returned.

The sample result below assumes that only the mobile number and email is sent along with the query.

```json
  "data": {
    "hit": true,
    "message": "SUCCESS",
    "result": {
      "nameMatchScore": 92,
      "dobMatched": null,
      "mobileMatched": false,
      "emailMatched": true,
      "genderMatched": null,
      "maritalStatusMatched": null
    }
  }
```

### Data mismatch

If the combination of the first and last name is has a less than 80% match score against the name registered for the ID number provided, the match result will not be returned.

```json
  "data": {
    "hit": true,
    "message": "First name or last name not matched.",
    "result": {
      "nameMatchScore": 77,
      "dobMatched": null,
      "mobileMatched": null,
      "emailMatched": null,
      "genderMatched": null,
      "maritalStatusMatched": null
    }
  }
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [Verify identity](/reference/verify-profile-identity) | `GET /profiles/-/identities/verify` |
