---
title: Verifications
excerpt: ""  
category: 6294c158bef44e0098ed88a1
slug: verification
---

Snap Verifications helps improve the identity verification process for businesses. By simply providing user-provided identity details as input (such as names, contact information, and ID numbers), Snap Verification matches and validates this information against reliable data sources, yielding output indicating the verification status of each attribute.

The Snap Verification API requires three things at a minimum:

1. The subject's name
2. The subject's ID or email (see list of supported IDs below)
3. The subject's consent

Once provided, Smile goes through all reliable data sources based on the provided ID and data that you have included in your request, allowing you to make quick decisions on the veracity of your end user's provided data. By combining quick confirmation with the Snap Verification API and surfacing the Wink SDK if the data provided is insufficient, you can get the information you need to efficiently serve your customer.

_Smile Snap Verification API is currently in alpha._

### How to Send a Verification Request

1. **Prepare your Verification Request details.**
   
   You will need to send the following information:

   * Your subject's name (full name or first name + last name)
   * Your subject's identifier (one from the supported identifiers below, or you may provide the email address)
   * Your subject's consent

2. **Send a Verification Request using our [Request Verification](https://docs.getsmileapi.com/reference/create-verification) endpoint.**
   
   > 📘 Note
   > 
   > Subject consent and data privacy is important to us. You must include evidence of your subject's consent along with their data when creating the request, by sending along the Consent Object with your request. Check out the data object below.

3. **Subscribe to the Event Notification or store the Verification ID of your request.**
   
4. **Receive the Verification Result** via the `TASK_FINISHED` webhook or the [Get Verification](https://docs.getsmileapi.com/reference/get-verification) endpoint.

### Supported Identifiers and Data Points

| ID or Identifier | Verifiable Data Attributes |
| :--------- | :----- |
| Tax Identification Number `tin_ph` | Full Name*, First Name*, Middle Name*, Last Name*, Suffix*, Date of Birth*, Gender*, Email, Phone |
| Social Security Number `sss_ph` | Full Name*, First Name, Middle Name, Last Name, Suffix, Date of Birth, Gender, Email, Phone |
| Professional License `prclicense_ph` | Full Name*, First Name*, Middle Name, Last Name*, License Type, Email |
| Pag-IBIG Member ID Number | Full Name*, First Name, Middle Name, Last Name, Email |
| Email address | Full name* |

More IDs will be supported soon.

## The Verification Objects

### Request Object

This is the request object you provide to us, as well as the meta object that tracks the request details.

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| fullName | string | The Subject's full name provided in the request |
| firstName | string | The Subject's first name provided in the request |
| middleName | string | The Subject's middle name provided in the request |
| lastName | string | The Subject's last name provided in the request |
| suffix | string | The Subject's suffix provided in the request |
| additionalData | object | Additional data about the Subject provided in the request |
| consent | object | Evidence of the Subject's consent provided in the request |

### Additional Data (Request) Object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| ids | array | Array of objects containing identification card/number information of the Subject (only one accepted) |
| email | string | The Subject's email address provided in the request |
| phone | string | The Subject's phone provided in the request |
| dob | date | The Subject's date of birthprovided in the request, in `YYYY-MM-DD` format |
| gender | string | The Subject's gender provided in the request, either `Male` or `Female` |

### Identifier (Request) Object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| idType | string | The type of ID the Subject has provided, as sent in the request |
| idSubType | string | The subtype of ID where applicable, i.e. License type |
| idNumber | string | The Subject's ID number provided in the request |

### Consent Object

If you choose to store your Consent Document with Smile, you may supply the consent template ID when you make your verification request, or provide the details of your consent document in the call directly, along with the date and time the subject consented to the verification process.

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| type | string | Your consent document's internal document name, i.e. "Product X Terms & Conditions" or "App Privacy Policy" |
| version | string | Your internal version for your consent document, for your tracking |
| consentedWith | string | Usually in the form of a checkbox or a section in a form where the user signs their name and signature. This field is for the words with which your user has shown their consent to the document you have given them |
| consentedAt | date-time | When the Subject gave their consent to you to process their data, in Zulu time format |
| consentTemplateId | number | Your consent template's ID if you choose to store this data with Smile |

### Verification Object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id | string | Unique ID of the verification request on the Smile Network |
| createdAt | date-time | Date/time when the verification request was created |
| updatedAt | date-time | Date/time when the verification request was last updated |
| status | string | Status of the verification request. Can be `PROCESSING`, `COMPLETED`, or `ERROR` |
| errorMessage | string | Error message of the verification request, if applicable |
| requestMeta | object | Object containing the original request data. See *Request Object* |
| result | object | Object containing moe result of the verification process |

### Result Object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| finalMatches | boolean | Returns true if the provided name matches the provided identifier |
| names | object | Object containing detailed matching information for the name |
| additionalData | object | Object containing detailed matching information for the additional attributes |

### Names (Result) Object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| fullNameMatches | boolean | Returns true if the provided full name matches the provided identifier. Null if not provided or not supported |
| firstNameMatches | boolean | Returns true if the provided first name matches the provided identifier. Null if not provided or not supported |
| middleNameMatches | boolean | Returns true if the provided middle name matches the provided identifier. Null if not provided or not supported |
| lastNameMatches | boolean | Returns true if the provided last name matches the provided identifier. Null if not provided or not supported |

### Additional Data (Result) Object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| ids | array | Array of objects containing matching information if the provided name matches the provided identifier. Null if not provided or not supported |
| dobMatches | boolean | Returns true if the provided date of birth matches the available records. Null if not provided, not supported, or `finalMatches` is false |
| genderMatches | boolean | Returns true if the provided gender matches the available records. Null if not provided, not supported, or `finalMatches` is false |
| phoneMatches | object | Object containing matching information and other information if the provided phone matches the available records. Null if not provided, not supported, or `finalMatches` is false |
| emailMatches | object | Object containing matching information and other information if the provided email address matches the available records. Null if not provided, not supported, or `finalMatches` is false |

### Identifier (Result) Object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| idNumber | string | The ID number evaluated as provided in the request |
| idType | string | The ID type evaluated as provided in the request |
| idSubType | string | The ID subtype evaluated as provided in the request |
| matches | boolean | Returns true if the provided name matches the provided identifier. Null if not provided or not supported |

### Email Match or Phone Match Object

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| value | string | The email address or phone number evaluated as provided in the request |
| matches | boolean | Returns true if the provided email or phone matches the available records. Null if not provided, not supported, or `finalMatches` is false |
| disposable | boolean | Returns true if the matching email or phone is disposable. Null if not provided, not supported, or `finalMatches` is false |
| deliverable | boolean | Returns true if the matching email is deliverable. Null if not provided, not supported,`finalMatches` is false, or for phone |
| active | boolean | Returns true if the matching phone is active. Null if not provided, not supported,`finalMatches` is false, or for email |
| provider | string | Returns the name of the email service provider or phone carrier. Null if not provided, not supported, or `finalMatches` is false |
| freeProvider | boolean | Returns true if the matching email or phone provider is a free service provider. Null if not provided, not supported, or `finalMatches` is false |

## Sample Verification Result data

``` json
{
  "id": "ver-123abc456def789abc123def456abc78",
  "createdAt": "2024-01-01T08:00:00Z",
  "status": "COMPLETED",
  "updatedAt": "2024-01-01T08:01:00Z",
  "errorMessage": null,
  "requestMeta": {
    "fullName": "George Cimafranca Palomero",
    "firstName": "George",
    "middleName": "Cimafranca",
    "lastName": "Palomero",
    "suffix": "",
    "additionalData": {
      "ids" : [{
        "idType": "tin_ph",
        "idSubType": "",
        "idNumber": "123456789"
      }],
      "email": "gpalomero1234@smileapi.io",
      "phone": null,
      "dob": "1980-01-01",
      "gender": "Male",
      },
      "consent": {
        "type": "Terms & Conditions",
        "version": "1.0",
        "consentedAt": "2024-01-01T08:00:00Z",
        "consentedWith": "I consent to ABC Company processing my data",
        "consentTemplateId": null
      }
  },
  "result": {
    "finalMatches": true,
    "names": {
      "fullNameMatches": true,
      "firstNameMatches": true,
      "lastNameMatches": true,
      "middleNameMatches": true
    },
    "additionalData": {
      "ids": [{
        "idNumber": "234957978",
        "idType": "tin_ph",
        "idSubtype": "",
        "matches": true
      }],
      "dobMatches": true,
      "genderMatches": true,
      "phoneMatches": null,
      "emailMatches": {
        "value": "gpalomero1234@gmail.com",
        "matches": true,
        "disposable": false,
        "deliverable": true,
        "active": null,
        "provider": "Google LLC",
        "freeProvider": true
      }
    }
  }
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List Verifications](/reference/list-verifications) | `GET /verifications` |
| [Request Verification](/reference/create-verification) | `POST /verifications` |
| [Get Verification](/reference/get-verification) | `GET /verifications/{id}` |

