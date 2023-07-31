---
title: Onboarding FAQs  
excerpt: ""  
category: 6396bfc8aa727100777258fe  
slug: onboarding-faqs
---

# Requirements

## What are the typical concerns I need to consider during requirements gathering ?

1. **What are the main problems you want to solve with Smile data ?** Typically, there are two use cases:
    1. [Customer verification](/docs/customer-verification-design) - automate your eKYC process with the latest employment data.
    2. [Credit decisioning](/docs/credit-decisioning-design) - automate your underwriting process with the latest employment and income data.
2. **What does your user base look like, and what kind of data do you want to obtain about them?** You may categorize your user base across different segments such as:
    1. Employment status - do they have a job? Are they employed or unemployed?
    2. Employment type - are they gig workers or contractors? Do they have full-time employment, part-time, or are they business owners?
    3. Identifying and categorizing your user base may help you narrow down the data attributes you need, such as home address, employer name, employment tenure, income stability, and others.
3. **Do you have any business goals/gains you want to achieve using Smile data?** These can normally be
    1. Reduce non-performing loans
    2. (Further) Automate the registration/credit decisioning process
    3. Others

# Design

## Which Mobile OS and Runtime does Smile Wink SDK support?

We support the following:

- IOS Native
- Android Native
- Flutter
- ReactNative

Our Wink Widget sits in a Webview instance of your native app and may be closed by you or the user at any time to go back to your app. We suggest you use iframes to wrap around the Wink SDK. You may check out our [Quick Start](https://github.com/SmileAPI/quickstart) repository for sample code.

## How can we disconnect/revoke a user's linked account?

There are two ways to disconnect a linked account:

1. Let users do it by themselves via the Wink SDK as shown in the [Solutions](/docs/customer-verification-design#how-can-a-user-disconnect-their-account)
2. Clients can call the Smile [OpenAPI](/reference/delete-account) to actively revoke accounts:

```curl curl
DELETE https://open.smileapi.io/v1/accounts/{id}
```



# Implementation & Go-live

## What is the validity period of the user (Link) token?

The user token is used to initialize Smile Wink Widget,  and is valid for 5 hours (300 minutes) before expiry. You may call the [Refresh Token endpoint](/reference/create-token-1) to get a new user token anytime to obtain a new token.

## What is the validity period of the Invite Link?

Invite Link is valid for 14 days. Before expiry, recipient can access Invite Link at anytime, already connected data providers will be shown, and recipient can revoke the connection.

## How long is the user data stored in Smile servers?

All data is deleted and irretrievable once users have revoked access.

## What is the validity period of the invite link?

The invite link is valid for 14 days. Users can open the link anytime before expiry, to allow them to see previously connected accounts, revoke previously connected accounts, or also add more connected accounts.

## How soon will Smile return user data after the user account is connected?

The duration between the account connection being established and the data being available depends on the performance of the data providers. This typically ranges from several seconds to a few minutes. The Smile SLA for this is 5 minutes, which means you can get user's data via [API ](https://docs.getsmileapi.com/reference/)  within 5 minutes.  
You may also listen to our available [Webhooks](/reference/webhooks) to ensure your system can immediately retrieve data once it is available.

## How map your user with Smile user?

Your user should map to Smile user(user ID) in one to one manner, and you should maintain the mapping relationship in your end, so for any returning user you can always get its corresponding Smile user ID, and please refer to this [link](https://docs.getsmileapi.com/docs/credit-decisioning-design#step-2-make-a-loan-decision) for Smile data mapping
