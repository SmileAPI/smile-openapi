# READ ME!

##  About Smile
Thank you for your interest in the Smile API!

We provide user-authorized access to valuable employment and income data from HR, payroll, commerce, and marketplace platforms through a single API! If you work at a bank, fintech, recruitment agency, or any other service provider, you can leverage employment and income data to increase adoption and conversion for your application, reduce cost in performing processes within your organization such as doing employment and identity verification checks, and reduce risk such as the risk of defaults especially if you are a lender. 

Access to the data is provided by the employees themselves, which is part of the API we provide. We offer a mechanism by which your users can give their consent to have this personal data collected and transmitted to you or any party they trust on their behalf. This is all done in a simple, secure and seamless way. 

##  About this Repository
This repository is open source, and contains the following:
- Smile API specifications in **YAML format**, following  [Open API Specification version 3.0.0](https://swagger.io/specification/)
- Offline copies of our Developer Documentation in **markdown format**, under the /docs subdirectory
- Postman collection in **JSON format**, which you can import into Postman to get started with our API right away.

## Signing up for a Developer Account
To get started, register your application with us by emailing access@getsmileapi.com.

After registration, your application will be assigned an API key and an API secret. The API secret must be kept safe and used only in exchanges between your application's server and Smile API's server.

For more information, you can visit [our website](https://www.getsmileapi.com), or email us at info@getsmileapi.com.

## Attentions
### 1. $ref path in YAML the format should be like this:
`$ref: 'relativePath/someone.yaml#/components/schemas/<schema_name>'`
*  behind the .yaml should not have "/", java plugin will not work, will print "schemas not found"
