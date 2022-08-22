---
title: Introduction  
excerpt: ""  
category: 6215975992e4610014e7b757  
slug: chapter-1
---



<!-- focus: false -->
![Smile](https://img.icons8.com/material-outlined/50/000000/smiling.png)


##  About Smile
Hello and welcome to Smile! 

Smile provides income and employment data across platforms and employers, all through a single API. Banks, fintechs, recruitment agencies, and other service providers can leverage employment and income data to increase adoption and conversion, reduce cost, and reduce risk, through a single API.

Access to the data is provided by the employees themselves, which is part of the API we provide. We offer a mechanism by which your users can give their consent to have this personal data collected and transmitted to you or any party they trust on their behalf. This is all done in a simple, secure and seamless way. 

---
<!-- focus: false -->
![API](https://img.icons8.com/glyph-neue/50/000000/api.png)


##  Our API
The Smile API is built on RESTful principles. All request and response payloads are encoded in JSON format. For security purposes, all requests must be sent through HTTPS. To get access to the API, you will need to [sign up to our developer portal](https://portal.getsmileapi.com).

---
<!-- focus: false -->
![Jobs](https://img.icons8.com/ios-filled/50/000000/find-matching-job.png)

## Available resources
The available resources in the Smile API are made up of two types: 
- Smile Network resources
- Source Data

### Smile Network
These are data resources for integrating and getting data from the Smile API. They include:

| Resource | Type    | Description |
|----------|---------|-------------|
| Providers | Smile Network | List of employment data providers available in the Smile Network. The data providers are further segmented into different subtypes such as Gig platforms, HR platforms, and others. |
| Users | Smile Network | These are your users who have initiated the account linking process and have given their consent to share their employment data with you and Smile. When a new user is created, a token is issued at the same time. |
| Tokens | Smile Network | The tokens to be able to access account-related data of a user. You can use this resource to either retrieve existing tokens, or refresh a token for an existing user. |
| Accounts | Smile Network | The accounts which your users have successfully logged into, and from which account-related data will be retrieved from. For more information, see below on "Source Data". |
| Archives | Smile Network | This refers to archives that contain files of scanned or photographed documents that the users have uploaded. |
| File Types | Smile Network | Refers to the types of files that are accepted for upload, and which will be available as an archive once it has been uploaded. | 
| Invites | Smile Network | You can use this to invite users to link their work account via their preferred communication channel such as email. |
| Invite Templates | Smile Network | If you will invite users to connect their work account via an invitation, use this to define and retrieve what the invite looks like.  |
| Webhooks | Smile Network | Webhooks are used to notify your application in real time when an event happens in your environment.  |

### User Data
User Data can either come from linked accounts or from uploaded data. To be able to retrieve income and employment data and use it in your application, you will need to either use our user Invitation functionality or use our Client SDK and embed our Wink Widget into your application.

> 📘 Note
> 
> To learn more about the Wink Widget, check out the section on **"Getting User Data"**

If you will be embedding the Client SDK yourself into your own application, you will need to instantiate the widget, after which a user will be created in the Smile Network, with a short-lived token. When the widget is instantiated, your users will first need to provide their consent for Smile to retrieve that data on their behalf. After that, we will display a list of employment and income data providers that your users can choose from. They will then need to either:

1. **Authenticate with a digital data provider.** If we have a direct connection to that data provider, we will display it in a list from which the user can choose from. If they have an account with any of the displayed providers, they can select that provider, then afterwards enter their credentials with that selected data provider. After giving permission, an account is created in the Smile Network from which data will be retrieved, aggregated, and normalized into a standard schema and sent to you in a developer-friendly JSON format. 
2. **Upload a scanned or photographed document containing their employment or income information.** Not all source employment and income information is in digital form. Typically the source for this type of information still comes in the form of paper documents. Users can scan  or photograph these documents, upload it, and we can then digitize and retrieve the pertinent data from it, in most cases also extracting the data (via Optical Character Recognition or OCR) into a developer-friendly JSON format. In cases where we cannot automatically extract the information, we will always provide a URL to the uploaded file available via the /archives endpoint. 

> 🚧 Warning
> 
> **We will keep a copy of the uploaded file/s, for a period of only 7 days!** If you need to retain a copy, please make sure to download and archive these files for yourselves as well.




| Resource | Type    | Description |
|----------|---------|-------------|
| Identity | User Data | Get vetted identity information from current and previous employers such as name, contact information, residential address, and others.|
| Transactions | User Data | Get detailed financial transactions of the user from the source data provider. This includes additions (or credits) and deductions (or debits) recorded from the source provider. |
| Ratings | User Data | Get information on user's job performance ratings. |  
| Documents | User Data | Get documentary information such as their driver's license, national identity card ID, and others.|  
| Employments | User Data | Get previous employment information such as the company the user has worked for, job title, tenure and others.|  
| Incomes | User Data | Get previous income information such as gross pay and net pay, as well as other components that make up income.|  
| Contributions | User Data | Get previous social security contribution information to get an indication of income level.|  

<!--
| Assets | Source Data | Get information on assets owned or used for their employment such as motor vehicles, motorcycles and others.|  
| Schools | Source Data | Get previous educational history such as school, degree, years attended and so on.|  
-->