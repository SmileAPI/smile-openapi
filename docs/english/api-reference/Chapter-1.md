---
title: Getting Started
category:
  uri: '/branches/1.0/categories/reference/API Guide'
slug: chapter-1
content:
  excerpt: ''
---



<!-- focus: false -->
![Smile](https://img.icons8.com/material-outlined/50/000000/smiling.png)

##  About Smile
Hello and welcome to Smile! 

Smile provides identity, income, and employment data across platforms, employers, and documents, all through a single API. Banks, fintechs, recruitment agencies, and other service providers can leverage employment and income data to increase adoption and conversion, reduce cost, and reduce risk, through a single API.

Access to the data is provided by the users themselves, which is part of the API we provide. We offer a mechanism by which your users can give their consent to have this personal data collected and transmitted to you or any party they trust on their behalf. This is all done in a simple, secure and seamless way.

Depending on your available input and expected output, **Smile API's products can help you Know your Customer better.**

![Smile API Product Lineup](https://files.readme.io/a7db7799e61dadb3822eb2dab65dd38480ea0d26625aa48f6200a6c72b111ca7-smile-api-inputs-outputs.png)

---
<!-- focus: false -->
![API](https://img.icons8.com/glyph-neue/50/000000/api.png)


##  Our API
The Smile API is built on RESTful principles. All request and response payloads are encoded in JSON format. For security purposes, all requests must be sent through HTTPS. To get access to the API, you will need to [sign up to our developer portal](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link).

To learn more about our API, see [Chapter 2, Understanding the API](/reference/chapter-2?utm_source=docs&utm_medium=internal_link).

---
<!-- focus: false -->
![Signup](https://img.icons8.com/ios-filled/50/000000/sign-up.png)

## Using the Developer Portal
To get started, simply register on the [Developer Portal](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link). After registering, you will be asked to verify your email, after which you can then log in. 

By default, when you register and log in, you will be in "Sandbox" mode, which returns only test data. You can access "Production" mode by booking a call or [contacting us](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link), and submitting the necessary information to go live.

> 📘 Note
> 
> To learn more about the different modes, check out the next section on **"Understanding the API"**

Inside the Developer Portal, you will see the following:

1. **[Account Usage](https://portal.getsmileapi.com/usage?utm_source=docs&utm_medium=internal_link):** You can view your account usage here, such as number of connected accounts and users in your organization.

2. **[Wink Widget](https://portal.getsmileapi.com/link/emulator?utm_source=docs&utm_medium=internal_link):** This section contains all you need to work with Smile's Wink Widget, the account linking SDK. The **Emulator** allows you to try out how the Wink Widget works. In Sandbox mode, you can use the provided test accounts on the page to simulate the process of logging into different data providers such as a gig platform or payroll system.  In Production mode, you will be able to actually link a live account or upload an actual file. You may also manage your [Wink Templates](https://portal.getsmileapi.com/link/template?utm_source=docs&utm_medium=internal_link) and [Wink Sites](https://portal.getsmileapi.com/link/winkSite?utm_source=docs&utm_medium=internal_link) in this section.

    ![devportal-emulator.png](https://files.readme.io/ded43f52b13308bb62cce9ee74fa8345855371e8ec3789c51ecb258276c8af0a-devportal-emulator.png)

3. **[Snap Documents]((https://portal.getsmileapi.com/snap?utm_source=docs&utm_medium=internal_link)):** You may try out or use Smile Snap in this page by uploading sample documents (in Sandbox mode) or actual files (in Production mode). You can see the status and output of each file uploaded directly in this section.

4. **[Signal Requests]((https://portal.getsmileapi.com/signal/signals?utm_source=docs&utm_medium=internal_link)):** You may test out the various Smile Signals services here, such as [Signals](https://portal.getsmileapi.com/signal/signals?utm_source=docs&utm_medium=internal_link), [Verifications](https://portal.getsmileapi.com/signal/verification?utm_source=docs&utm_medium=internal_link), and [Blacklists](https://portal.getsmileapi.com/signal/blacklists?utm_source=docs&utm_medium=internal_link), [Digital Footprint](https://portal.getsmileapi.com/signal/footprints?utm_source=docs&utm_medium=internal_link), and [Multiple Application Warning](https://portal.getsmileapi.com/signal/maws?utm_source=docs&utm_medium=internal_link).

4. **[User Data](https://portal.getsmileapi.com/users?utm_source=docs&utm_medium=internal_link):** View the users created in the back-end, as well as the data captured from that user, during the account linking process or after uploading the user uploads a file. In this section, you can also preview how the returned data from Smile looks like for each resource such as Employments and Incomes.

5. **[Integration](https://portal.getsmileapi.com/developer/providers?utm_source=docs&utm_medium=internal_link)**: This section contains various tools to help with your integration into the Smile Network, from learning more about the different [Data Sources](https://portal.getsmileapi.com/providers?utm_source=docs&utm_medium=internal_link) available, generating and managing your [API Keys](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link) and [Webhooks](https://portal.getsmileapi.com/webhooks?utm_source=docs&utm_medium=internal_link), and configuring your [Consent Templates](https://portal.getsmileapi.com/developer/consent-templates?utm_source=docs&utm_medium=internal_link).

On the top navigation bar on the right of the page you will be able to manage your [Organization and Account Settings](https://portal.getsmileapi.com/account/organization?utm_source=docs&utm_medium=internal_link), [Service Status and Uptime](https://status.getsmileapi.com/?utm_source=docs&utm_medium=internal_link), and the API Documentation (which you are reading now).

## Using this Reference

To fully explore the Smile API, we encourage you to make full use of this Reference website by entering your API Key and Secret on the right hand side of the reference pages.

[block:image]
{
"images": [
{
"image": [
"https://files.readme.io/b7d08d8-how-to-use-reference-sidebar.png",
null,
""
],
"align": "center"
}
]
}
[/block]

> 📘 Note
> 
> Your API Key and Secret can be found by logging into the [Developer Portal](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link) under [the **API Keys** section](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link). Upon signup, you will have instant and free access to test on our Sandbox environment. If you need Production environment access, [contact us](https://www.getsmileapi.com/contact-us?utm_source=docs&utm_medium=internal_link).
>
>![](https://files.readme.io/8032442ec83f0f739d2025e2016ca00296c110088fc1d1dce2b2e1af2e7ba09e-image.png)
> 
> You may click on the Copy icon next to your API Key and Secret to easily copy it to your computer clipboard.


---
<!-- focus: false -->
![API](https://img.icons8.com/ios/50/000000/api-settings.png)

## Additional Resources

We have included below some **Open Source** resources to help get you started right away using Smile API!

### API Specifications

> 📘 Note
> 
> You can download a copy of Smile API's [specifications](https://github.com/SmileAPI/smile-openapi/blob/main/openapi-v1.yaml) in [Github](https://github.com/SmileAPI). If you have git installed, you can clone the repository or run the following command:

``` bash
git clone https://github.com/SmileAPI/smile-openapi
```

The specification document is in **YAML format**, following  [Open API Specification version 3.0.0](https://swagger.io/specification/). You can also download offline copies of our Developer Documentation in **markdown format**, under the /docs subdirectory.

### Postman Collection

> 📘 Note
> 
> Download Smile API's [Postman Collection](https://github.com/SmileAPI/smile-openapi/blob/main/postman-collection-v1.json) in [Github](https://github.com/SmileAPI). If you have git installed, you can clone the repository or run the following command:

``` bash
git clone https://github.com/SmileAPI/smile-openapi
```

You can start reviewing and testing our APIs easily by downloading our Postman collection in **JSON format** and importing it into Postman.

#### Using the Postman Collection

1. Download the "postman-collection-(v#).json" document from our [Github repository](https://github.com/SmileAPI/smile-openapi).
2. If you haven't done so, visit [Postman](https://www.postman.com/) and create an account, or download their free desktop client.
3. Open Postman and select a Workspace.
4. Import the Postman collection.
5. Make sure you are able to authenticate by entering your API key and API secret.
6. That's it! You can now start testing Smile's APIs!
