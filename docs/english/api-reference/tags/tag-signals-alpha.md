---
title: Signals(Alpha)
excerpt: ''
category: 6294c158bef44e0098ed88a1
slug: signals-alpha
---

In today's fast-paced financial landscape, accurate and timely risk assessment is crucial for making informed decisions. Smile API's Signals API provides a powerful solution by delivering real-time risk signals using a person's mobile number or email address, from a wide variety of activities and events.

Smile API can provide access to hundreds of risk signals, allowing you to pick and choose the signals that make sense for your use case and market segment. We have also preselected 30 of the most common risk signals so you can get started immediately, but we highly suggest contacting us to test your data against our risk signals catalog.

_Signals is currently in Beta, and the current page is the documentation for the Alpha version._

## The Signals object

| Attribute  | Type   | Description  |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| id | string | Unique ID for the Signal Request |
| createdAt | date-time | Date and time when the signal request was made |
| status | string | Current status of the signal request, may be one of the following: `PROCESSING`, `ERROR`, `COMPLETED` |
| resultCode | string | Final result of the signal request, may be one of the following: `SUCCESS`, `NO_DATA`, `SYSTEM_ERROR`, `SERVICE_UNAVAILABLE` |
| resultMessage | string | Longer description of the final result of the signal request |
| requestMeta | object | Values provided with the signal request |
| result | object | Results of the signal request |

**The `requestMeta` object**

The `requestMeta` object contains the values you provided with your signal request.

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| phone | string | The mobile number of the subject |
| consent | object | The consent details of the subject |

**The `consent` object**

If you choose to store your Consent Document with Smile, you may supply the consent template ID when you make your verification request. Alternatively you may provide the details of your consent document in the call directly, along with the date and time the subject consented to the verification process.

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| type | string | Your consent document's internal document name, i.e. "Product X Terms & Conditions" or "App Privacy Policy" |
| version | string | Your internal version for your consent document, for your tracking |
| consentedWith | string | Usually in the form of a checkbox or a section in a form where the user signs their name and signature. This field is for the words with which your user has shown their consent to the document you have given them |
| consentedAt | date-time | When the Subject gave their consent to you to process their data, in Zulu time format |
| consentTemplateId | number | Your consent template's ID if you choose to store this data with Smile |

**The `result` object**

The `result` object contains the values of the result after the request processing has finished successfully. This may be a different subset of results depending on your account settings.

| Attribute  | Type   | Description                                                                                |
| :--------- | :----- | :----------------------------------------------------------------------------------------- |
| events_marketing_day30_institution_count | integer | Number of institutions with marketing promotion events in the last 30 days |
| events_application_reception_day30 | integer | Number of application reception events in the last 30 days |
| events_application_reception_day30_institution_count | integer | Number of institutions with application reception events in the last 30 days |
| events_application_approval_day30 | integer | Number of application approval events in the last 30 days |
| events_loan_disbursement_day30 | integer | Number of loan disbursement events in the last 30 days |
| events_loan_disbursement_day30_institution_count | integer | Number of institutions with loan disbursement events in the last 30 days |
| events_repayment_reminder_day30 | integer | Number of repayment reminder events in the last 30 days |
| events_repayment_reminder_day30_institution_count | integer | Number of institutions with repayment reminder events in the last 30 days |
| events_successful_repayment_day30 | integer | Number of successful repayment events in the last 30 days |
| events_successful_repayment_day30_institution_count | integer | Number of institutions with successful repayment events in the last 30 days |
| events_overdue_day30 | integer | Number of overdue events in the last 30 days |
| events_overdue_day30_institution_count | integer | Number of institutions with overdue events in the last 30 days |
| events_overdue_day30_amount | integer | Amount of overdue events in the last 30 days |
| events_debt_day30_amount | integer | Amount of debt events in the last 30 days |
| events_overdue_day30_days | integer | Number of days of overdue events in the last 30 days |
| events_marketing_day90_institution_count | integer | Number of institutions with marketing promotion events in the last 90 days |
| events_application_reception_day90 | integer | Number of application reception events in the last 90 days |
| events_loan_disbursement_day90 | integer | Number of loan disbursement events in the last 90 days |
| events_loan_disbursement_day90_institution_count | integer | Number of institutions with loan disbursement events in the last 90 days |
| events_overdue_day90 | integer | Number of overdue events in the last 90 days |
| events_overdue_day90_institution_count | integer | Number of institutions with overdue events in the last 90 days |
| events_overdue_day90_amount | integer | Amount of overdue events in the last 90 days |
| events_debt_day90_amount | integer | Amount of debt events in the last 90 days |
| events_overdue_day90_days | integer | Number of days of overdue events in the last 90 days |
| events_marketing_day180_institution_count | integer | Number of institutions with marketing promotion events in the last 180 days |
| events_application_reception_day180 | integer | Number of application reception events in the last 180 days |
| events_loan_disbursement_day180 | integer | Number of loan disbursement events in the last 180 days |
| events_loan_disbursement_day180_institution_count | integer | Number of institutions with loan disbursement events in the last 180 days |
| events_overdue_day180 | integer | Number of overdue events in the last 180 days |
| events_overdue_day180_institution_count | integer | Number of institutions with overdue events in the last 180 days |
| events_overdue_day180_amount | integer | Amount of overdue events in the last 180 days |
| events_overdue_day180_days | integer | Number of days of overdue events in the last 180 days |
| events_loan_disbursement_days_since_last | integer | Number of days since the last loan disbursement event |
| events_successful_repayment_days_since_last | integer | Number of days since the last successful repayment event |
| events_overdue_days_since_last | integer | Number of days since the last overdue event |

## Sample Signal data

``` json
{
  "code": "OK",
  "message": "Success!",
  "requestId": "123abc456def789abc123def456abc78",
  "data": {
    "id": "signal-123abc456def789abc123def456abc78",
    "createdAt": "2024-08-09T12:55:51Z",
    "status": "COMPLETED",
    "resultCode": "SUCCESS",
    "resultMessage": "query success",
    "requestMeta": {
      "phone": "+639171234567",
      "consent": {
        "type": "[Motor Loans] Terms & Conditions",
        "version": "Loan Terms & Conditions",
        "consentedAt": "2024-08-08T16:06:00Z",
        "consentedWith": "I agree to ABC Company's Terms & Conditions",
        "consentTemplateId": "ct-fa84d4ec5a064c898b62b46b7affbcd5"
      }
    },
    "result": {
      "events_marketing_day30_institution_count": 0,
      "events_application_reception_day30": 0,
      "events_application_reception_day30_institution_count": 0,
      "events_application_approval_day30": 0,
      "events_loan_disbursement_day30": 0,
      "events_loan_disbursement_day30_institution_count": 0,
      "events_repayment_reminder_day30": 0,
      "events_repayment_reminder_day30_institution_count": 0,
      "events_successful_repayment_day30": 0,
      "events_successful_repayment_day30_institution_count": 0,
      "events_overdue_day30": 0,
      "events_overdue_day30_institution_count": 0,
      "events_overdue_day30_amount": null,
      "events_debt_day30_amount": null,
      "events_overdue_day30_days": null,
      "events_marketing_day90_institution_count": 0,
      "events_application_reception_day90": 0,
      "events_loan_disbursement_day90": 0,
      "events_loan_disbursement_day90_institution_count": 0,
      "events_overdue_day90": 0,
      "events_overdue_day90_institution_count": 0,
      "events_overdue_day90_amount": null,
      "events_debt_day90_amount": null,
      "events_overdue_day90_days": null,
      "events_marketing_day180_institution_count": 0,
      "events_application_reception_day180": 0,
      "events_loan_disbursement_day180": 0,
      "events_loan_disbursement_day180_institution_count": 0,
      "events_overdue_day180": 0,
      "events_overdue_day180_institution_count": 0,
      "events_overdue_day180_amount": null,
      "events_overdue_day180_days": null,
      "events_loan_disbursement_days_since_last": null,
      "events_successful_repayment_days_since_last": null,
      "events_overdue_days_since_last": null
    }
  }
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [Request Signals](/reference/create-alpha-signal) | `POST /alpha/signals` |
| [List Signals](/reference/list-alpha-signals) | `GET /alpha/signals` |
| [Get Signal Request](/reference/get-alpha-signal) | `GET /alpha/signals/{id}` |


## Risk Signals

Here is a total list of all risk signals available in the Smile API network. Your account will have up to 30 signals pre-selected for you, which you may switch out for a different set according to your needs. Contact us to find out more.

Legend:

- ✅ Available by default
- 🟨 Available

### Risk Signals - Phone

| Signal | Value | 30 days | 90 days | 180 days | Description |
| :----- | :---- | :------ | :------ |  :------ | :---------- |
| Application approval | N/A | ✅ | 🟨 | 🟨 | Number of application approval events within the duration |
| Application approval institution count | N/A | 🟨 | 🟨 | 🟨 | Number of application approval events within the duration |
| Application approval days since last | 🟨 | N/A | N/A | N/A | Number of days since the last application approval event |
| Application reception | N/A | ✅ | ✅ | ✅ | Number of application reception events within the duration |
| Application reception institution count  | N/A | ✅ | 🟨 | 🟨 | Number of institutions with application reception events within the duration |
| Application reception days since last  | 🟨 | N/A | N/A | N/A | Number of days since the last application reception event |
| Application rejection | N/A | 🟨 | 🟨 | 🟨 | Number of application rejection events within the duration |
| Application rejection institution count  | N/A | 🟨 | 🟨 | 🟨 | Number of institutions with application rejection events within the duration |
| Application rejection days since last  | 🟨 | N/A | N/A | N/A | Number of days since the last application rejection event |
| Arbitrary | N/A | 🟨 | 🟨 | 🟨 | Number of arbitrary events within the duration |
| Arbitrary institution count  | N/A | 🟨 | 🟨 | 🟨 | Number of institutions with arbitrary events within the duration |
| Captcha | N/A | 🟨 | 🟨 | 🟨 | Number of captcha events within the duration |
| Captcha institution count  | N/A | 🟨 | 🟨 | 🟨 | Number of institutions with captcha events within the duration |
| Captcha days since last  | 🟨 | N/A | N/A | N/A | Number of days since the last captcha event |
| Debt amount  | N/A | ✅ | ✅ | 🟨 | Amount of debt events within the duration |
| Lending | N/A | 🟨 | 🟨 | 🟨 | Number of lending events within the duration |
| Lending institution count  | N/A | 🟨 | 🟨 | 🟨 | Number of institutions with lending events within the duration |
| Loan disbursement  | N/A | ✅ | ✅ | ✅ | Number of loan disbursement events within the duration |
| Loan disbursement amount  | N/A | 🟨 | 🟨 | 🟨 | Amount of loan disbursement events within the duration |
| Loan disbursement institution count  | N/A | ✅ | ✅ | ✅ | Number of institutions with loan disbursement events within the duration |
| Loan disbursement days since last  | ✅ | N/A | N/A | N/A | Number of days since the last loan disbursement event |
| Marketing | N/A | 🟨 | 🟨 | 🟨 | Number of marketing promotion events within the duration |
| Marketing institution count | N/A | ✅ | ✅ | ✅ | Number of institutions with marketing promotion events within the duration |
| Marketing days since last | 🟨 | N/A | N/A | N/A | Number of days since the last marketing promotion event |
| Other | N/A | 🟨 | 🟨 | 🟨 | Number of other events within the duration |
| Other institution count | N/A | 🟨 | 🟨 | 🟨 | Number of institutions with other events within the duration |
| Overdue  | N/A | ✅ | ✅ | ✅ | Number of overdue events within the duration |
| Overdue amount  | N/A | ✅ | ✅ | ✅ | Amount of overdue events within the duration |
| Overdue autorepayment days  | N/A | 🟨 | 🟨 | 🟨 | Number of days of overdue autorepayment events within the duration |
| Overdue institution count  | N/A | ✅ | ✅ | ✅ | Number of institutions with overdue events within the duration |
| Overdue days  | N/A | ✅ | ✅ | ✅ | Number of days of overdue events within the duration |
| Overdue days since last  | ✅ | N/A | N/A | N/A | Number of days since the last overdue event |
| Preloan  | N/A | 🟨 | 🟨 | 🟨 | Number of preloan events within the duration |
| Preloan institution count  | N/A | 🟨 | 🟨 | 🟨 | Number of institutions with preloan events within the duration |
| Repayment reminder  | N/A | ✅ | 🟨 | 🟨 | Number of repayment reminder events within the duration |
| Repayment reminder amount  | N/A | 🟨 | 🟨 | 🟨 | Amount of repayment reminder events within the duration |
| Repayment reminder institution count  | N/A | ✅ | 🟨 | 🟨 | Number of institutions with repayment reminder events within the duration |
| Repayment reminder days since last  | 🟨 | N/A | N/A | N/A | Number of days since the last repayment reminder event |
| Successful repayment  | N/A | ✅ | 🟨 | 🟨 | Number of successful repayment events within the duration |
| Successful repayment amount  | N/A | 🟨 | 🟨 | 🟨 | Amount of successful repayment events within the duration |
| Successful repayment institution count  | N/A | ✅ | 🟨 | 🟨 | Number of institutions with successful repayment events within the duration |
| Successful repayment days since last  | ✅ | N/A | N/A | N/A | Number of days since the last successful repayment event |

### Risk Signals - Email

_Coming soon._