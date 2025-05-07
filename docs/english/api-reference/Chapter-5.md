---
title: Document Processing
excerpt: ''
category: 6215975992e4610014e7b757
slug: chapter-5
---

**Smile Snap**, Smile API's powerful Document Processing product, is designed as both a seamless integration with Wink Widget but is also available as a standalone, API-only service. Smile Snap's automated analysis feature extracts crucial information from Income Tax Documents and Payslips, such as employment details and income data, and then analyzes the document for signs of tampering, computational inconsistencies, and other issues.

This eliminates the need for manual data transcription, ensuring a streamlined and error-free verification process. This not only enhances efficiency but also contributes to a more accurate and comprehensive user profile.

Smile Snap also acts as a reliable fallback method for user verification if online methods are not available for the user. If primary verification methods encounter challenges, users can submit relevant documents, ensuring a robust and secure verification process.

---
<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)
## Integration Steps

There are only a few steps in implementing Smile API's Document Processing service in your process:

1. **Provide the document to Smile API**

    > There are two ways to provide the document or file to Smile API for processing:
    > 1. Using the [Wink Widget SDK](/reference/chapter-4#client-sdk) for quick implementation into your user flow.
    > 2. Using the [Archives API](/reference/archives) for finer control over your user journey.

2. **Retrieve the analyzed data**

    > Once data has been uploaded, our Intelligent Document Processing engine automatically checks and classifies the document according to the expected file type, for supported document types.
    >
    > Once this classification is done, our engine parses the file and extracts the data from the document and tags is accordingly. Each file type will have a different set of data and will be reflected in the analysis of the document.
    >
    > Once analysis is finished, the Archive data payload will be sent to you via webhook, or you may call the Archives API directly. See the API documentation for more information.

3. **Run Verification on your extracted data**

    > We are currently working on integrating these calls into the API, but you may call our [Verification API](/reference/verification) using the data retrieved from *Step 2* in order to verify your subject's information such as Name and ID numbers. This gives you another layer of assurance that the document is valid.

<!-- ## How to Set Up -->
<!-- TODO: Quickstart or similar -->

> 🚧 Warning
> 
> Archives in Sandbox Mode return only specific payslips. To test Archives while in Sandbox Mode, you may download the sample payslips within the Developer Portal and upload it through the Wink Widget or through the API. Other files uploaded during Sandbox mode will return errors.

<!-- ## Getting User Data -->
<!-- ## Configuration -->

---
<!-- focus: false -->
![Event](https://img.icons8.com/ios/50/000000/important-event.png)
## Event Notifications

As the user moves through the Wink widget screen, any activities performed by the user are captured and are either used to update the messsages and presentation of the modal window, or are sent to Smile so that any source-related data can be retrieved. 

### Successful Uploads

If the the user was able to successfully upload employment and income data via scanned or photographed documents, the Link status is changed to "STARTED". The upload status of the user can be queried at any time via the ``/archives`` endpoint. Examples of the events captured include:

| Event |Description |
|----------|---------|
| STARTED | The upload was successful, and analysis on whether data can be extracted has started. |
| ANALYZED | The analysis has completed and data was successfully extracted (via OCR) and converted to JSON format. |
| UNSUPPORTED | The type of file uploaded cannot be analyzed. Data cannot be automatically extracted. |
| ERROR | Something went wrong with the analysis of the uploaded file. |
| REVOKED | The user revoked permission to share data from the uploaded files. |


---
<!-- focus: false -->
![Storage](https://img.icons8.com/?size=50&id=1476&format=png&color=000000)
## Maintaining User Data

User data is stored by Smile API only until one of the following occur:

1. The user revokes access to their document via the Wink Widget
2. The access is revoked via the Revoke API (i.e. if initiated by the developer)
3. 60 days have passed from document upload

To ensure continued access to the document past the 60-day maximum timeframe, ensure you retrieve and store the user's document in your own servers. You may instruct Smile to delete the document as soon as you have retrieved it from the Smile servers using the Revoke API. You will also receive an event notification from Smile to notify you when the user has manually revoked the sharing of their document.

<!-- ## Versioning -->

