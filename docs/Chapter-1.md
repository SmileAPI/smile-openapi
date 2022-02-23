# Introduction


<!-- focus: false -->
![Smile](https://img.icons8.com/material-outlined/50/000000/smiling.png)

##  About Smile
Hello and welcome to Smile! 

We provide user-authorized access to valuable employment and income data from HR, payroll, commerce, and marketplace platforms through a single API! If you work at a bank, fintech, recruitment agency, or any other service provider, you can leverage employment and income data to increase adoption and conversion for your application, reduce cost in performing processes within your organization such as doing employment and identity verification checks, and reduce risk such as the risk of defaults especially if you are a lender. 

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
- Account data

### Smile network
These are data resources available to be able to use and integrate with the Smile API. They include:

| Resource | Type    | Description |
|----------|---------|-------------|
| Providers | Smile network | List of employment data providers available in the Smile Network. The data providers are further segmented into different subtypes such as Gig platforms, HR platforms, and others. |
| Users | Smile network | These are your users who have initiated the account linking process and have given their consent to share their employment data with you and Smile. When a new user is created, a token is issued at the same time. |
| Tokens | Smile network | The tokens to be able to access account-related data of a user. You can use this resource to either retrieve existing tokens, or refresh a token for an existing user. |
| Accounts | Smile network | The accounts which your users have successfully logged into, and from which account-related data will be retrieved from. For more information, see below on account-related data. |


### Account data
To be able to retrieve account-related data and use it in your application, you will need to embed our Wink widget into your application. You will need to issue a token to the user, for the user to be able to launch the widget. From the widget, your users will then need to select the provider from which their employment data will come from.  After this, they will need to provide their consent for Smile to retrieve that data on their behalf, then nter their credentials with the selected data provider. After giving permission, an account is created in the Smile network from which data will be retrieved, aggregated, and normalized into a standard schema and sent to you in a developer-friendly JSON format. 

| Resource | Type    | Description |
|----------|---------|-------------|
| Identity | Account data | Get vetted identity information from current and previous employers such as name, contact information, residential address, and others.|
| Transactions | Account data | Get detailed financial transactions of the user from the source data provider.|



<!--
| Jobs *(coming soon)*  | Account data | Get previous employment history, including job title, status, tenure, employer names, employer contact information, and others.|
| Earnings *(coming soon)*  | Account data | Get previous earnings information such as gross pay and net pay, as well as other components that make up income.|  
| Documents *(coming soon)*  | Account data | Get documentary information such as their driver's license, national identity card ID, and others.|  
| Assets *(coming soon)*  | Asset data | Get information on assets owned or used for their employment such as motor vehicles, motorcycles and others.|  
| Ratings *(coming soon)*  | Ratings data | Get information on their job performance ratings.|  
->