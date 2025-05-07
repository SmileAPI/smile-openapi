---
title: Risk Screening
excerpt: ''
category: 6215975992e4610014e7b757
slug: chapter-6
---

**Smile Signals** provides a powerful Risk Screening solution by delivering real-time risk signals using a person's mobile number or email address, from a wide variety of activities and events, to keep up to date in today's fast-paced financial landscape where accurate and timely risk assessment is crucial for making informed decisions.

The suite of Signals APIs can provide access to hundreds of risk signals, allowing you to pick and choose the signals that make sense for your use case and market segment.

Choose from the current suite of Signals:

| Signal | Status | Description |
|---|---|---|
| Signals | Beta | Smile's first risk screening service contains a preselected 30 of the most common risk signals so you can get started immediately with only your user's mobile number. |
| Footprints | Alpha | Obtain valuable insights on your user's digital footprint and online activities. | 
| Multiple Application Warning | Alpha | Discover early indications of your user's lending activities. |
| Blacklist | Alpha | Ensure your user is not blacklisted. |
| Verification | Alpha | Verification can help you confirm matches between your user provided data and data from pre-verified and/or authoritative sources. Requires user's ID. |

---
<!-- focus: false -->
![Checklist](https://img.icons8.com/ios/50/000000/checklist--v1.png)
## Integration Steps

There are only a few steps in implementing Smile API's Risk Screening service in your process:

1. **Choose the Signal service you require**

    > Select from one of Smile's powerful Signals suite according to your requirements and the data you have.

2. **Provide the required input to Smile API**

    > Using the selected product, send the required input to Smile API, such as the user's phone number, email address, or other data, via the appropriate API endpoint.
    >
    > For example, you send the user's mobile number to the ``/signals`` endpoint to retrieve risk signal data.

3. **Retrieve the analyzed data**

    > Once data has been uploaded, our system automatically checks and/or calculates the response based on the service you have requested.
    >
    > Once these calculations are complete, the result's payload will be sent to you via webhook, or you may call the appropriate API directly. See the API documentation for more information.


<!-- ---
<!-- focus: false -->
<!-- ![Quickstart](https://img.icons8.com/ios/50/000000/speed.png)
<!-- ## Quickstart / How to Set Up -->

<!-- ---
<!-- focus: false -->
<!-- ![User Data](https://img.icons8.com/?size=50&id=FD1d9t9lMoS2&format=png&color=000000)
<!-- ## Getting User Data -->

<!-- ---
<!-- focus: false -->
<!-- ![Settings](https://img.icons8.com/material-outlined/50/000000/settings-3--v1.png)
<!-- ## Configuration -->

<!-- ---
<!-- focus: false -->
<!-- ![Event](https://img.icons8.com/ios/50/000000/important-event.png)
<!-- ## Event Notifications -->

<!-- ---
<!-- focus: false -->
<!-- ![Storage](https://img.icons8.com/?size=50&id=1476&format=png&color=000000)
<!-- ## Maintaining User Data -->

<!-- ---
<!-- focus: false -->
<!-- ![Versioning](https://img.icons8.com/?size=50&id=21889&format=png&color=000000)
<!-- ## Versioning -->
