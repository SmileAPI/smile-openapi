---
title: Profile Data
excerpt: ''
category: 66611ec162e8c700572c4be3
slug: profile-data
---

The Smile Snap Profile Data API allows developers to retrieve a snapshot of a person's data from authoritative sources without the need for a user login. This Profile Data can be used in the following scenarios:

- Retrieving extra information about a user
- Pre-filling in user's basic information
- Verifying provided data (see also [Data Verification](https://docs.getsmileapi.com/reference/verify-identity))

By providing the person's ID type, ID number, and name, additional basic information can be retrieved for the user if the name has at least an 80% match with the person identified via the ID number (see below). Otherwise, no information is returned.

Smile currently supports querying via the Social Security ID number. Other data sources will be onboarded soon.

If you require more detailed user information than the ones available through Smile Snap, this can be obtained in a user-authenticated manner using the Wink Widget SDK.

### Result object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| nameMatchScore | number | Percentage match of the provided name |
| firstName | string | The person's first name |
| lastName | string | The person's last name |
| middleName | string | The person's middle name |
| suffix | string | The person's name suffix |
| dob | date | The person's date of birth, in YYYY-MM-DD format |
| mobile | string | The person's mobile number |
| email | string | The person's email address |
| gender | string | The person's gender, may be ``Male``, ``Female``, ``Non-binary`` |
| maritalStatus | string | The person's marital status, may be one of the following: ``Divorced``, ``Married``, ``Separated``, ``Single``, ``Widowed``, ``Lifetime Partner`` |
| homeTelephone | string | The person's home telephone number |
| address | object | The person's address |
| socialSecurityCoverageType | string | The person's social security coverage type, may be one of the following: ``EMPLOYEE``, ``VOLUNTARY``, ``SELF EMPLOYED``, ``FOR EMPLOYMENT`` |
| socialSecurityCoverageDate | string | Date of the person's social security coverage |
| totalEmploymentReportCount | number | Number of employment records of the person |
| firstEmploymentReportDate | date | Date of the first employment record of the person |
| latestEmploymentReportDate | date | Date of the last employment record of the person |

#### The Address object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| fullAddress | string | Full physical address of the user |
| line1 | string | First line of the user's address, i.e. street address |
| line2 | string | Second line of the user's address |
| city | string | City of the user's address |
| region | string | Geographic region of the user's address such as state or province |
| zip | string | Zip or post code of the user's address |
| country | string | Country of the user's address. Provided in 2-character alpha ISO-3166 codes, i.e. `PH`, `ID`, etc. |

### Sample Profile data

### Data match

If the combination of the first and last name matches at least 80% against the name registered for the ID number provided, the user's data will be returned.

```json
  "data": {
    "hit": true,
    "message": "SUCCESS",
    "result": {
      "nameMatchScore": 92,
      "firstName": "George",
      "lastName": "Palomero",
      "middleName": "Cimafranca",
      "suffix": "Jr",
      "dob": "1970-08-24",
      "mobile": "+639559991234",
      "email": "gpalomero1234@smileapi.io",
      "gender": "Male",
      "maritalStatus": "Married",
      "homeTelephone": null,
      "address": null,
      "socialSecurityCoverageType": "EMPLOYEE",
      "socialSecurityCoverageDate": "2020-05-01",
      "totalEmploymentReportCount": 5,
      "firstEmploymentReportDate": "2000-02-01",
      "latestEmploymentReportDate": "2022-12-01"
    }
  }
```

### Data mismatch

If the combination of the first and last name is has a less than 80% match score against the name registered for the ID number provided, the user's data will not be returned.

```json
  "data": {
    "hit": true,
    "message": "First name or last name not matched.",
    "result": {
      "nameMatchScore": 77,
      "firstName": null,
      "lastName": null,
      "middleName": null,
      "suffix": null,
      "dob": null,
      "mobile": null,
      "email": null,
      "gender": null,
      "maritalStatus": null,
      "homeTelephone": null,
      "address": null,
      "socialSecurityCoverageType": null,
      "socialSecurityCoverageDate": null,
      "totalEmploymentReportCount": null,
      "firstEmploymentReportDate": null,
      "latestEmploymentReportDate": null
    }
  }
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [Query identity](/reference/query-profile-identity) | `GET /profiles/-/identities/query` |
