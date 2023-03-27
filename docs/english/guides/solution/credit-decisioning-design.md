---
title: Design  
excerpt: ""  
category: 638fff38b56c92003c1a1e55  
slug: credit-decisioning-design
---

# Plan and design your credit decisioning integration

***



Credit decisioning begins with the verification of income and employment. Smile provides both of these verifications. To successfully integrate Smile into your process, we suggest doing so through 3 steps:

- Requirements gathering - explore your use case and what do you want to achieve with Smile data
- Design (this guide) - design your user journey and integration with Smile.
- [Implementation & Go-Live](/docs/credit-decisioning-implementation) - detailed steps to set up and get the integration launched

Lenders usually implement this solution in a two-step flow:

- Verify an applicant's income and employment.
- Making a loan decision

***



# Step 1: Design your user journey

![](https://files.readme.io/097a246-image.png)

![](https://files.readme.io/0855715-image.png)

There are five aspects to consider when thinking about the user flow:

1. Where in the process do you want to leverage Smile?
2. Which data providers do you want to route the user through?
3. How do you want to on-ramp and off-ramp users?
4. What is the experience while waiting for the loan decision?
5. How can a user disconnect their account?

***



## Where in the process do you want to leverage Smile?

![](https://files.readme.io/9637ca5-image.png)

- **During pre-qualification or early application**  - autofill an entire application with personal information
- **Underwriting** - decisioning for an applicant
- ** Verification** - check Certification of Employment, Proof of Billing, etc

***



## Which data providers do you want to route user through?

In the Smile Developer Portal, you can find the various data points that each data provider supports, and the data attributes each data point supports.

[block:image]
{
"images": [
{
"image": [
"https://files.readme.io/d541b14-image.png",
null,
""
],
"align": "center",
"border": true
}
]
}
[/block]



1. Navigate to the Data Sources page on the Smile [Developer Portal](https://portal.getsmileapi.com)
2. View the supported data points for the selected data provider
3. View the supported data attributes for the selected data point

The main considerations for choosing providers are:

- Which data providers are being used by your user base?
- What is the data providers' coverage of your user base?
- What data points and attributes do you need that the provider can support?

There are two ways to design your user flow based on your shortlisted providers:

![](https://files.readme.io/bf68868-image.png)

- Dedicated provider (recommended)
- Multiple providers

### Dedicated provider

This option requires you to identify which data providers fit your user base. The user will be brought straight to the login screen (without the need to show the consent and provider list pages)

![](https://files.readme.io/635420f-image.png)

### Multiple providers

This option sends users through a provider list on the SDK, where they can select from either all providers, or your shortlist of providers, and proceed to connect their accounts:

![](https://files.readme.io/918f517-image.png)

For users where Smile does not have coverage, the user will be shown a **Can't find your employer? **button. then, there are two possible scenarios for the user:

- If archive uploads are enabled, clicking this button will direct users to manually upload their documents such as payslip, income tax records, etc.:

![](https://files.readme.io/a568785-image.png)

- Otherwise, clicking this button will close Smile Wink SDK and initiate a callback for you to funnel the user back to your application.

![](https://files.readme.io/86704bc-image.png)

We advise sending all users through Smile as this provides the best user experience and highest conversion rates

***



## How do you want to on-ramp users?

Now that you've determined 1) where in your flow and 2) to which users you want to surface Smile, it's important to frame Smile correctly for your users. Best in class implementations provide two things:

1. **Incentive** - users need to clearly understand why they are verifying their income and employment, and the benefit this will give them. Making it clear that this will allow them to complete their application faster and get the best rates, is ideal.
2. **Context** - provide users with context into the process they will go through. Users need to understand that they will 1) search for their providers, and 2) connect their employment or payroll account.

An example on-ramp screen is provided below.

![](https://files.readme.io/cdb6390-image.png)

***



## How do you want to off-ramp users?

After a user connects their accounts and they are funneled back into your application, it is important to let the users know what will happen next in the process. This will depend on your overall flow and goals, but here are some examples:

![](https://files.readme.io/d32ed9c-image.png)

***



## What is the experience while waiting for the loan decision?

Smile supports both an automated or semi-automated loan decisioning process, depending on your capability.

For automated processing with your own credit decision engine, Smile can send you event notifications via webhooks once the user has linked an account and Smile has retrieved the data from the provider. Your credit decision engine can then retrieve employment and income data from Smile and run your model on the fly.

![](https://files.readme.io/b8fb309-image.png)

If you need more time to process the data, or there is a manual component to your decisioning process, you can send a notification to the user once the credit decisioning process finished.

![](https://files.readme.io/1ac07cf-image.png)

***



## How can a user disconnect their account?

By default, Smile will have your users grant ongoing access to their employment accounts. You should provide users with an option to invoke Smile Wink SDK (for example, from an account settings page) so that they can revoke access.

![](https://files.readme.io/e6ac81e-image.png)

# Step 2: Make a loan decision

When users connect their accounts, you can retrieve their employment and income information via the [Smile OpenAPI](https://docs.getsmileapi.com/reference) to inform your loan decisioning process.

![](https://files.readme.io/58acc20-image.png)

![](https://files.readme.io/94325ef-image.png)

Smile has access to 140+ employment record data points. For verification of employment, you most likely want to retrieve:

Income:

- Basic amount
- Start date
- End date

Estimated Income:

- Monthly amount
- Month

Employment:

- Employer name
- Start date
- End date

Transaction:

- Amount
- Start date
- End date

You can also retrieve archives:

- Tax documents
- Payslips
