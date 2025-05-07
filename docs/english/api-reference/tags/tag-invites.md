---
title: Invites
excerpt: ""
category: 6294c0fd9494580032b22740
slug: invites
---

The Invites APIs allow you to manage and send invitations to your end-users directly from your website or application, without the need to access the Smile Developer Portal manual functionality. This facilitates an automated process and experience for your end users.

The API also makes use of predefined [Invite Templates](/reference/invite-templates) that you can use in order to customize the content of the invite email sent to your user.

## Sending Invites

To send an invite via the API, you need the following information:

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| fullName | string | The full name of the person to be invited. Required |
| firstName | string | The first name of the person to be invited |
| lastName | string | The last name of the person to be invited |
| email | string | The email address the invite should be send to. Required |
| templateId | string | The invite template ID to use, usually in the format `tpl-123abc456def789abc123def456abc78`. Required |
| winkTemplateId | string | The Wink Widget template ID to use, usually in the format `wtpl-123abc456def789abc123def456abc78` |

You may manage your email invite templates via the [Invite Templates](/reference/invite-templates) API.

See the [Create Invite](/reference/create-invite) endpoint for more information on creating and sending invites via API.

## Fallback Methods

If you cannot use the Invites API to create automated emails sent to your end users, you may also access the [Smile Developer Portal](https://portal.getsmileapi.com?utm_source=docs&utm_medium=internal_link) to send invites manually via [the Users section](https://portal.getsmileapi.com/users?utm_source=docs&utm_medium=internal_link). Note that you must be on Production mode to use this functionality.

## The Invites object

| Attribute  | Type   | Description |
| :--------- | :----- | :------- |
| id | string | Unique ID of the invite sent on the Smile Network |
| createdAt | datetime | Date and time the invite was created |
| fullName | string | The full name of the person to be invited. Required |
| firstName | string | The first name of the person to be invited |
| lastName | string | The last name of the person to be invited |
| email | string | The email address the invite should be send to. Required |
| templateId | string | The invite template ID to use, usually in the format `tpl-123abc456def789abc123def456abc78`. Required |
| winkTemplateId | string | The Wink Widget template ID to use, usually in the format `wtpl-123abc456def789abc123def456abc78` |
| userId | string | The invitee's Smile Network unique user ID, created when the invite is sent |
| status | string | Status of the invite. Possible values: `INVITED`, `LINKED` |
| updatedAt | datetime | Date and time the invite was last updated |
| invitedAt | datetime | Date and time the invite was sent |
| linkedAt | datetime | Date and time the invited user has linked an account |
| inviteLandingPageUrl | string | URL of the unique landing page for the invited user to connect their accounts |

## Sample Invites data

```
{
    "id": "iv-123abc456def789abc123def456abc78",
    "createdAt": "2023-02-02T02:35:01Z",
    "fullName": "George Palomero Jr",
    "firstName": "George",
    "lastName": "Palomero",
    "email": "gpalomero123@email.com",
    "templateId": "tpl-123abc456def789abc123def456abc78",
    "winkTemplateId": "wtpl-123abc456def789abc123def456abc78",
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "status": "INVITED",
    "updatedAt": "2023-02-02T02:35:01Z",
    "invitedAt": "2023-02-02T02:35:01Z",
    "linkedAt": null
}
```

## Endpoints

| Endpoint | |
| :------- | :---- |
| [List all inviites](/reference/list-invites) | `GET /invites` |
| [Create and send an invite](/reference/create-invite) | `POST /invites` |
| [Retrieve one invite](/reference/get-invite) | `GET /invites/{id}` |

## Webhooks

### `INVITE_INVITED`

Sent when an invitation is sent out to a user successfully.

```
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INVITE_INVITED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "inviteId": "iv-123abc456def789abc123def456abc78"
  }
}
```

### `INVITE_LINKED`

Sent when a user that has been sent an invitation is able to link their work account successfully.

```
{
  "id": "et-123abc456def789abc123def456abc78",
  "version": 1,
  "type": "INVITE_LINKED",
  "createdAt": "2021-04-14T09:30:24Z",
  "data": {
    "userId": "tenantId-123abc456def789abc123def456abc78",
    "inviteId": "iv-123abc456def789abc123def456abc78"
  }
}
```
