---
title: Invite Templates
excerpt: ""
category: 66611f40576121006f501bc1
slug: invite-templates
---


The Invite Templates APIs allow you to manage various invite templates you can use when sending invitations to your end users to connect their work accounts. These invite templates can help you automate your user flow directly from your platform, without the need to access the Smile Developer Portal manual functionality.

Once you have set up an Invite Template for your organization, you can use the [Invites API](/reference/invites) to use the created Invite Template when sending emails to your end users. Invite Templates can be reused.

## Creating Invite Templates

Use the [Create Invite Template](/reference/create-invite-template) endpoint to create a new template. Each invite template contains three parts:

1. *Email Message* - this is sent to the recipient to invite them to connect their work accounts. Contains a link to the landing page where they can start the account connection process.
2. *Landing Page* - this is the landing page where the invitee can start the account connection process.
3. *Success Page* - this is the page that will appear once the invitee finishes connecting their account(s).

You may customize each part of the invite template.

You may send the following information:

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| name | string | Name of the template. This is not shown to the recipient. Required |
| company | object | Organization information such as name and logo to customize your invite email. See details below |
| email | object | Email information such as sender name etc. to customize your invite email. See details below |
| landingPage | object | Landing page information such as header text etc. to customize the landing page for your invite email. See details below |
| successPage | object | Success page information such as header text etc. to customize your success page for your invite email. See details below |

*Some values are not yet in use for invite templates.*

### Company Information

| Attribute  | Type   | Description                                                                                                                            |
| :--------- | :----- |:---------------------------------------------------------------------------------------------------------------------------------------|
| name | string | Organization name that will appear in the invite email and landing page. Used to populate `${companyName}` into the template. Required |
| logoUrl | string | Fully-qualified URL to a logo to be displayed in the invite email and landing page. *Not yet available.*                               |

### Email Information

![invite-template-email-sample.png](https://cdn.smileapi.io/image/documentation/invites/invite-template-email-sample20230321.png)

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| sendEmail | boolean | Allow sending an email invite using this template. Required. *Must be true - SMS invites not yet available* |
| senderName | string | The sender name to be applied to the email invite, i.e. your organization name. Required |
| replyAddress | string | Reply-to address that will be applied to the email invite, if your end user repliles to the email. Required |
| subject | string | Subject for the email invite. You may use template codes (see below) to populate the email subject. Required |
| body | string | Body of the message. You may use template codes (see below) to populate the body text. No HTML allowed. Required |

The template codes that are supported are below:

- `${companyName}` - your provided Company Name in the email template
- `${firstName}` - your invitee's first name if available, otherwise, uses full name

### Landing Page Information

![invite-template-landing-sample.png](https://cdn.smileapi.io/image/documentation/invites/invite-template-landing-sample20230321.png)

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| header | string | The header text of the landing page. You may use template codes (see below) to populate the page header. Required |
| description | string | The main/description text of the landing page. You may use template codes (see below) to populate the body text. Required |
| button | string | The text on the button to launch the Wink Widget / start the account connection process. Required |

The template codes that are supported are below:

- `${companyName}` - your provided Company Name in the email template
- `${firstName}` - your invitee's first name if available, otherwise, uses full name

### Success Page Information

![invite-template-success-sample.png](https://cdn.smileapi.io/image/documentation/invites/invite-template-success-sample20230321.png)

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| header | string | The header text of the success page. You may use template codes (see below) to populate the success page header. Required |
| description | string | The main/description text of the success page. You may use template codes (see below) to populate the success page body text. Required |
| button | string | The text on the button to end the account connection process. Required |

The template codes that are supported are below:

- `${companyName}` - your provided Company Name in the email template
- `${firstName}` - your invitee's first name if available, otherwise, uses full name

## Fallback Methods

If you cannot use the Invites API to create automated emails sent to your end users, you may also access the [Smile Developer Portal](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link) to send invites manually via [the Users section](https://portal.getsmileapi.com/users?utm_source=docs&utm_medium=internal_link). Note that you must be on Production mode to use this functionality.

## The Invite Templates object

You may retrieve available invite templates.

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the invite template on the Smile Network |
| name | string | Name of the template |
| company | object | Organization information such as name and logo to customize the invite. See details below |
| email | object | Email information such as sender name etc. to customize the invite. See details below |
| landingPage | object | Landing page information such as header text etc. to customize the landing page for the invite. See details below |
| successPage | object | Success page information such as header text etc. to customize the success page for the invite. See details below |

### The Company object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| name | string | Organization name that will appear in the invite email and landing page. Used to populate `${companyName}` into the template |
| logoUrl | string | Fully-qualified URL to a logo to be displayed in the invite email and landing page. *Not yet available.* |

### The Email object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| sendEmail | boolean | Allow sending an email invite using this template *SMS invites not yet available* |
| senderName | string | The sender name to be applied to the email invite, i.e. your organization name |
| replyAddress | string | Reply-to address that will be applied to the email invite |
| subject | string | Subject for the email invite |
| body | string | Body of the message |

### Landing Page Information

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| header | string | The header text of the landing page |
| description | string | The main/description text of the landing page |
| button | string | The text on the button to launch the Wink Widget / start the account connection process |

### Success Page Information

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| header | string | The header text of the success page |
| description | string | The main/description text of the success page |
| button | string | The text on the button to end the account connection process |


## Sample Invite Template data

```
{
    "id": "tpl-123abc456def789abc123def456abc78",
    "name": "Email Template v1",
    "company": {
        "name": "ABC Corporation",
        "logoUrl": "https://xyzbank.co/logo.png"
    },
    "email": {
        "sendEmail": true,
        "senderName": "ABC Corporation",
        "replyAddress": "loans@abccorporation.com",
        "subject": "Please connect your work account to verify your previous employment",
        "body": "Hello ${firstName}! We are working with our partner, Smile API, so you can easily share your employment and income data to us as a requirement for employment. It will be a quick process and should take no more than a few seconds of your time."
    },
    "landingPage": {
        "header": "Please connect your work account to verify your previous employment at ${companyName}",
        "description": "We are working with our partner, Smile API, so you can easily share your employment and income data to us as a requirement for giving you service. It will be a quick process and should take no more than a few seconds of your time.",
        "button": "START SHARING NOW"
    },
    "successPage": {
        "header": "The process was successful! Please wait for us to get in touch!",
        "description": "Thank you for sharing your employment and income data with us at ${companyName}.",
        "button": "Connect another account"
    }
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all invite templates](/reference/list-invite-templates) | `GET /inviteTemplates` |
| [Create invite template](/reference/create-invite-template) | `POST /inviteTemplates` |
| [Retrieve one invite template](/reference/get-invite-template) | `GET /inviteTemplates/{id}` |
| [Update invite template](/reference/get-invite) | `PUT /inviteTemplates/{id}` |
| [Delete invite template](/reference/get-invite) | `DELETE /inviteTemplates/{id}` |

## Webhooks

No webhooks are available for invite templates management.
