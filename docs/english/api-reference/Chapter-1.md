---
title: Getting Started
excerpt: ""  
category: 6215975992e4610014e7b757  
slug: chapter-1
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

1. **[Account Usage](https://portal.getsmileapi.com/usage?utm_source=docs&utm_medium=internal_link):** You can view your account usage here, such as number of connected accounts and users in your tenant.

2. **[Wink Widget](https://portal.getsmileapi.com/link/emulator?utm_source=docs&utm_medium=internal_link):** Use this to preview how the Wink Widget works. The behavior of the widget changes depending on the mode you are in. In Sandbox mode, you can use the provided test accounts on the page to simulate the process of logging into different data providers such as a gig platform or payroll system.  In Production mode, you will be able to actually link a live account or upload an actual file.

3. **Snap Lookup:** You may test out the various Smile Snap services here, such as [Verifications](https://portal.getsmileapi.com/snap/verification?utm_source=docs&utm_medium=internal_link), [Intelligent Document Processing](https://portal.getsmileapi.com/snap/scanned?utm_source=docs&utm_medium=internal_link), and [Signals](https://portal.getsmileapi.com/snap/signals?utm_source=docs&utm_medium=internal_link).

4. **[User Data](https://portal.getsmileapi.com/users?utm_source=docs&utm_medium=internal_link):** View the users created in the back-end, as well as the data captured from that user, during the account linking process or after uploading the user uploads a file. In this section, you can also preview how the returned data from Smile looks like for each resource such as Employments and Incomes.

5. **[Data Sources](https://portal.getsmileapi.com/providers?utm_source=docs&utm_medium=internal_link):** The Data Sources section is where you can find all the Data providers as well as File Types that can be uploaded. Data providers include different types such as the names of different employers, gig platforms, government services, or HR and payroll systems. File types on the other hand are those that can be uploaded by the user such as copies of payslips, tax documents and others.

6. **[API Keys](https://portal.getsmileapi.com/api-keys?utm_source=docs&utm_medium=internal_link):** After registration, you will be given a Sandbox API key and an API secret. The API secret must be kept safe and used only in exchanges between your application's server and Smile API's server. Upon request, you can also be given the API key and API secret to use the Smile API in production. This will also allow you to switch the Developer Portal to "Production Mode" for live testing.

7. **[Webhooks](https://portal.getsmileapi.com/webhooks?utm_source=docs&utm_medium=internal_link):** You may create and manage your webhooks here to communicate to your application.

8. **[Settings](https://portal.getsmileapi.com/account/organization?utm_source=docs&utm_medium=internal_link):** This is where you can enter details about your organization and team. You may also invite additional members from your organization to join the Portal and share a common tenant or workspace.

9. **Documentation:** This is a link to the API documentation which you are reading now!

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
>![](https://files.readme.io/70f1152-where-to-find-api-keys.png)
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