---
title: Introduction  
excerpt: ""  
category: 6215975992e4610014e7b757  
---



<!-- focus: false -->
![Smile](https://img.icons8.com/material-outlined/50/000000/smiling.png)


##  About Smile
Hello and welcome to Smile! 

Smile provides income and employment data across platforms and employers, all through a single API. Banks, fintechs, recruitment agencies, and other service providers can leverage employment and income data to increase adoption and conversion, reduce cost, and reduce risk, through a single API. Permission to access their own personal data is given by each individual users themselves, so they can seamlessly share this data with the parties they trust.

Access to the data is provided by the employees themselves, which is part of the API we provide. We offer a mechanism by which your users can give their consent to have this personal data collected and transmitted to you or any party they trust on their behalf. This is all done in a simple, secure and seamless way. 

---
<!-- focus: false -->
![API](https://img.icons8.com/glyph-neue/50/000000/api.png)


##  Our API
The Smile API is built on RESTful principles. All request and response payloads are encoded in JSON format. For security purposes, all requests must be sent through HTTPS. To get access to the API, you will need to contact us at access@getsmileapi.com. Soon we will also provide a Developer portal so that you can get access to the API yourselves just by registering.

---
<!-- focus: false -->
![Jobs](https://img.icons8.com/ios-filled/50/000000/find-matching-job.png)

## Available resources
The available resources in the Smile API are made up of two types: 
- Smile network resources
- Source data

### Smile network
These are data resources available to be able to use and integrate with the Smile API. They include:

| Resource | Type    | Description |
|----------|---------|-------------|
| Providers | Smile network | List of employment data providers available in the Smile Network. The data providers are further segmented into different subtypes such as Gig platforms, HR platforms, and others. |
| Users | Smile network | These are your users who have initiated the account linking process and have given their consent to share their employment data with you and Smile. When a new user is created, a token is issued at the same time. |
| Tokens | Smile network | The tokens to be able to access account-related data of a user. You can use this resource to either retrieve existing tokens, or refresh a token for an existing user. |
| Accounts | Smile network | The accounts which your users have successfully logged into, and from which account-related data will be retrieved from. For more information, see below on "Source data". |
| Uploads | Smile network | This refers to uploads that contain files of scanned or photographed documents that the users have uploaded. |


### Source data
Source data can either be account-related or upload-related data. To be able to retrieve income and employment data and use it in your application, you will need to embed our Wink widget into your application. You will need to issue a token to the user, for the user to be able to launch the widget. When the widget is instantiated, your users will first need to provide their consent for Smile to retrieve that data on their behalf. After that, we will display a list of employment and income data providers that your users can choose from. They will then need to either:

1. **Authenticate with a digital data provider.** If we have a direct connection to that data provider, we wil display it in a list from which the user can choose from. If they have an account with any of the displayed providers, they can select that provider, then afterwards enter their credentials with that selected data provider. After giving permission, an account is created in the Smile network from which data will be retrieved, aggregated, and normalized into a standard schema and sent to you in a developer-friendly JSON format. 
2. **Upload a scanned or photographed document containing their employment or income information.** Not all source employment and income information is in digital form. Typically the source for this type of information still comes in the form of paper documents. Users can scan  or photograph these documents, upload it, and we can then digitize and retrieve the pertinent data from it, in most cases also extracting the data (via Optical Character Recognition or OCR) into a developer-friendly JSON format. In cases where we cannot automatically extract the information, we will always provide a URL to the uploaded file. 

> 🚧 Warning
> 
> **We will keep a copy of the uploaded file/s for a period of only 7 days!** If you need to retain a copy, please make sure to download and archive the files.




| Resource | Type    | Description |
|----------|---------|-------------|
| Identity | Source data | Get vetted identity information from current and previous employers such as name, contact information, residential address, and others.|
| Transactions | Source data | Get detailed financial transactions of the user from the source data provider. This includes additions (or credits)) and deductions (or debits) recorded from the source provider. |
| Ratings | Source data | Get information on user's job performance ratings. |  
| Documents | Source data | Get documentary information such as their driver's license, national identity card ID, and others.|  
| Employments | Source data | Get previous employment information such as the company the user has worked for, job title, tenure and others.|  
| Incomes | Source data | Get previous income information such as gross pay and net pay, as well as other components that make up income.|  

<!--
| Assets | Source data | Get information on assets owned or used for their employment such as motor vehicles, motorcycles and others.|  

->