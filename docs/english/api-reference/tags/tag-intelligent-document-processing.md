---
title: Intelligent Document Processing
excerpt: ""  
category: 66611ec162e8c700572c4be3
slug: intelligent-document-processing
---

Smile Snap's Intelligent Document Processing (IDP) service combines the efficiency of optical character recognition (OCR) and the benefits of Artificial Intelligence. IDP captures, comprehends, and contextualizes the content of documents with remarkable accuracy.

Supported documents can be sent to Smile via our Open API, or through the Wink SDK if enabled. Smile accepts these documents in a variety of formats such as photos, scans, or PDF files.

Capturing these data can be used as a fallback method or as an additional data point for your records and verification use. Data gathered from the document will afterward be available as part of the Smile User's data payload.

These documents are called [Archives](/reference/archives) in the Smile Network.

## Using the Service

There are only a few steps in implementing Smile API's IDP service in your process:

1. **Provide the document to Smile API**

    > There are two ways to provide the document or file to Smile API for processing:
    > 1. Using the [Wink Widget SDK](/reference/chapter-4#client-sdk) for quick implementation into your user flow.
    > 2. Using the [Archives API](/reference/archives) for finer control over your user journey.

2. **Retrieve the analyzed data**

    > Once data has been uploaded, our IDP engine automatically checks and classifies the document according to the expected file type, for supported document types.
    >
    > Once this classification is done, our engine parses the file and extracts the data from the document and tags is accordingly. Each file type will have a different set of data and will be reflected in the analysis of the document.
    >
    > Once analysis is finished, the Archive data payload will be sent to you via webhook, or you may call the Archives API directly. See the API documentation for more information.

3. **Run Verification on your extracted data**

    > We are currently working on integrating these calls into the API, but you may call our [Verification API](/reference/verification) using the data retrieved from *Step 2* in order to verify your subject's information such as Name and ID numbers. This gives you another layer of assurance that the document is valid.

## Testing the Service

To test the service, you may connect to the API in Sandbox mode or you may also use the [Developer Portal](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link) to try out the service directly, under [the Snap Lookup > Scanned Documents section](https://portal.getsmileapi.com/snap/scanned?utm_source=docs&utm_medium=internal_link).

> 🚧 Warning
> 
> Archives in Sandbox Mode return only specific payslips. To test Archives while in Sandbox Mode, you may download the sample payslips within the Developer Portal and upload it through the Wink Widget or through the API. Other files uploaded during Sandbox mode will return errors.
