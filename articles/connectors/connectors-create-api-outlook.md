---
title: Outlook.com | Microsoft Docs
description: Create Logic apps with Azure App service. Outlook.com connector allows you to manage your mail, calendars, and contacts. You can perform various actions such as send mail, schedule meetings, add contacts, etc.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: 409e1a104fa73d911ea508cbff311cb48fc20f9f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551497"
---
# <a name="get-started-with-the-outlookcom-connector"></a>Get started with the Outlook.com connector
Outlook.com connector allows you to manage your mail, calendars, and contacts. You can perform various actions such as send mail, schedule meetings, add contacts, etc.

> [!NOTE]
> This version of the article applies to logic apps 2015-08-01-preview schema version.
>
>

You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="triggers-and-actions"></a>Triggers and actions
The Outlook.com connector can be used as an action; it has trigger(s). All connectors support data in JSON and XML formats.

 The Outlook.com connector has the following action(s) and/or trigger(s) available:

### <a name="outlookcom-actions"></a>Outlook.com actions
You can take these action(s):

| Action | Description |
| --- | --- |
| [GetEmails](connectors-create-api-outlook.md#getemails) |Retrieves emails from a folder |
| [SendEmail](connectors-create-api-outlook.md#sendemail) |Sends an email |
| [DeleteEmail](connectors-create-api-outlook.md#deleteemail) |Deletes an email by id |
| [MarkAsRead](connectors-create-api-outlook.md#markasread) |Marks an email as having been read |
| [ReplyTo](connectors-create-api-outlook.md#replyto) |Replies to an email |
| [GetAttachment](connectors-create-api-outlook.md#getattachment) |Retrieves email attachment by id |
| [SendMailWithOptions](connectors-create-api-outlook.md#sendmailwithoptions) |Send an email with multiple options and wait for the recipient to respond back with one of the options |
| [SendApprovalMail](connectors-create-api-outlook.md#sendapprovalmail) |Send an approval email and wait for a response from the recipient |
| [CalendarGetTables](connectors-create-api-outlook.md#calendargettables) |Retrieves calendars |
| [CalendarGetItems](connectors-create-api-outlook.md#calendargetitems) |Retrieves items from a calendar |
| [CalendarPostItem](connectors-create-api-outlook.md#calendarpostitem) |Creates a new event |
| [CalendarGetItem](connectors-create-api-outlook.md#calendargetitem) |Retrieves a specific item from a calendar |
| [CalendarDeleteItem](connectors-create-api-outlook.md#calendardeleteitem) |Deletes a calendar item |
| [CalendarPatchItem](connectors-create-api-outlook.md#calendarpatchitem) |Partially updates a calendar item |
| [ContactGetTables](connectors-create-api-outlook.md#contactgettables) |Retrieves contacts folders |
| [ContactGetItems](connectors-create-api-outlook.md#contactgetitems) |Retrieves contacts from a contacts folder |
| [ContactPostItem](connectors-create-api-outlook.md#contactpostitem) |Creates a new contact |
| [ContactGetItem](connectors-create-api-outlook.md#contactgetitem) |Retrieves a specific contact from a contacts folder |
| [ContactDeleteItem](connectors-create-api-outlook.md#contactdeleteitem) |Deletes a contact |
| [ContactPatchItem](connectors-create-api-outlook.md#contactpatchitem) |Partially updates a contact |

### <a name="outlookcom-triggers"></a>Outlook.com triggers
You can listen for these event(s):

| Trigger | Description |
| --- | --- |
| On event starting soon |Triggers a flow when an upcoming calendar event is starting |
| On new email |Triggers a flow when a new email arrives |
| On new items |Triggered when a new calendar item is created |
| On updated items |Triggered when a calendar item is modified |

## <a name="create-a-connection-to-outlookcom"></a>Create a connection to Outlook.com
To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:

| Property | Required | Description |
| --- | --- | --- |
| Token |Yes |Provide Outlook.com Credentials |

After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>
> [!TIP]
> You can use this connection in other logic apps.  
>
>

## <a name="reference-for-outlookcom"></a>Reference for Outlook.com
Applies to version: 1.0

## <a name="onupcomingevents"></a>OnUpcomingEvents
On event starting soon: Triggers a flow when an upcoming calendar event is starting

```GET: /Events/OnUpcomingEvents```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |query |none |Unique identifier of the calendar |
| lookAheadTimeInMinutes |integer |no |query |15 |Time (in minutes) to look ahead for upcoming events |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 202 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="getemails"></a>GetEmails
Get emails: Retrieves emails from a folder

```GET: /Mail```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| folderPath |string |no |query |Inbox |Path of the folder to retrieve emails (default: 'Inbox') |
| top |integer |no |query |10 |Number of emails to retrieve (default: 10) |
| fetchOnlyUnread |boolean |no |query |true |Retrieve only unread emails? |
| includeAttachments |boolean |no |query |false |If set to true, attachments will also be retrieved along with the email |
| searchQuery |string |no |query |none |Search query to filter emails |
| skip |integer |no |query |0 |Number of emails to skip (default: 0) |
| skipToken |string |no |query |none |Skip token to fetch new page |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="sendemail"></a>SendEmail
Send email: Sends an email

```POST: /Mail```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| emailMessage | |yes |body |none |Email |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="deleteemail"></a>DeleteEmail
Delete email: Deletes an email by id

```DELETE: /Mail/{messageId}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| messageId |string |yes |path |none |Id of the email to delete |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="markasread"></a>MarkAsRead
Mark as read: Marks an email as having been read

```POST: /Mail/MarkAsRead/{messageId}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| messageId |string |yes |path |none |Id of the email to be marked as read |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="replyto"></a>ReplyTo
Reply to email: Replies to an email

```POST: /Mail/ReplyTo/{messageId}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| messageId |string |yes |path |none |Id of the email to reply to |
| comment |string |yes |query |none |Reply comment |
| replyAll |boolean |no |query |false |Reply to all recipients |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="getattachment"></a>GetAttachment
Get attachment: Retrieves email attachment by id

```GET: /Mail/{messageId}/Attachments/{attachmentId}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| messageId |string |yes |path |none |Id of the email |
| attachmentId |string |yes |path |none |Id of the attachment to download |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="onnewemail"></a>OnNewEmail
On new email: Triggers a flow when a new email arrives

```GET: /Mail/OnNewEmail```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| folderPath |string |no |query |Inbox |Email folder to retrieve (default: Inbox) |
| to |string |no |query |none |Recipient email addresses |
| from |string |no |query |none |From address |
| importance |string |no |query |Normal |Importance of the email (High, Normal, Low) (default: Normal) |
| fetchOnlyWithAttachment |boolean |no |query |false |Retrieve only emails with an attachment |
| includeAttachments |boolean |no |query |false |Include attachments |
| subjectFilter |string |no |query |none |String to look for in the subject |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |Operation was successful |
| 202 |Accepted |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="sendmailwithoptions"></a>SendMailWithOptions
Send email with options: Send an email with multiple options and wait for the recipient to respond back with one of the options

```POST: /mailwithoptions/$subscriptions```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| optionsEmailSubscription | |yes |body |none |Subscription request for options email |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 201 |Subscription Created |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="sendapprovalmail"></a>SendApprovalMail
Send approval email: Send an approval email and wait for a response from the recipient

```POST: /approvalmail/$subscriptions```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| approvalEmailSubscription | |yes |body |none |Subscription request for approval email |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 201 |Subscription Created |
| 400 |BadRequest |
| 401 |Unauthorized |
| 403 |Forbidden |
| 500 |Internal Server Error |
| default |Operation Failed. |

## <a name="calendargettables"></a>CalendarGetTables
Get calendars: Retrieves calendars

```GET: /datasets/calendars/tables```

There are no parameters for this call

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="calendargetitems"></a>CalendarGetItems
Get events: Retrieves items from a calendar

```GET: /datasets/calendars/tables/{table}/items```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of the calendar to retrieve |
| $filter |string |no |query |none |An ODATA filter query to restrict the number of entries |
| $orderby |string |no |query |none |An ODATA orderBy query for specifying the order of entries |
| $skip |integer |no |query |none |Number of entries to skip (default = 0) |
| $top |integer |no |query |none |Maximum number of entries to retrieve (default = 256) |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="calendarpostitem"></a>CalendarPostItem
Create event: Creates a new event

```POST: /datasets/calendars/tables/{table}/items```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a calendar |
| item | |yes |body |none |Calendar item to create |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="calendargetitem"></a>CalendarGetItem
Get event: Retrieves a specific item from a calendar

```GET: /datasets/calendars/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a calendar |
| id |string |yes |path |none |Unique identifier of a calendar item to retrieve |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="calendardeleteitem"></a>CalendarDeleteItem
Delete event: Deletes a calendar item

```DELETE: /datasets/calendars/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a calendar |
| id |string |yes |path |none |Unique identifier of calendar item to delete |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="calendarpatchitem"></a>CalendarPatchItem
Update event: Partially updates a calendar item

```PATCH: /datasets/calendars/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a calendar |
| id |string |yes |path |none |Unique identifier of calendar item to update |
| item | |yes |body |none |Calendar item to update |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="calendargetonnewitems"></a>CalendarGetOnNewItems
On new items: Triggered when a new calendar item is created

```GET: /datasets/calendars/tables/{table}/onnewitems```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a calendar |
| $filter |string |no |query |none |An ODATA filter query to restrict the number of entries |
| $orderby |string |no |query |none |An ODATA orderBy query for specifying the order of entries |
| $skip |integer |no |query |none |Number of entries to skip (default = 0) |
| $top |integer |no |query |none |Maximum number of entries to retrieve (default = 256) |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="calendargetonupdateditems"></a>CalendarGetOnUpdatedItems
On updated items: Triggered when a calendar item is modified

```GET: /datasets/calendars/tables/{table}/onupdateditems```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a calendar |
| $filter |string |no |query |none |An ODATA filter query to restrict the number of entries |
| $orderby |string |no |query |none |An ODATA orderBy query for specifying the order of entries |
| $skip |integer |no |query |none |Number of entries to skip (default = 0) |
| $top |integer |no |query |none |Maximum number of entries to retrieve (default = 256) |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="contactgettables"></a>ContactGetTables
Get contact folders: Retrieves contacts folders

```GET: /datasets/contacts/tables```

There are no parameters for this call

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="contactgetitems"></a>ContactGetItems
Get contacts: Retrieves contacts from a contacts folder

```GET: /datasets/contacts/tables/{table}/items```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of the contacts folder to retrieve |
| $filter |string |no |query |none |An ODATA filter query to restrict the number of entries |
| $orderby |string |no |query |none |An ODATA orderBy query for specifying the order of entries |
| $skip |integer |no |query |none |Number of entries to skip (default = 0) |
| $top |integer |no |query |none |Maximum number of entries to retrieve (default = 256) |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="contactpostitem"></a>ContactPostItem
Create contact: Creates a new contact

```POST: /datasets/contacts/tables/{table}/items```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a contacts folder |
| item | |yes |body |none |Contact to create |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="contactgetitem"></a>ContactGetItem
Get contact: Retrieves a specific contact from a contacts folder

```GET: /datasets/contacts/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a contacts folder |
| id |string |yes |path |none |Unique identifier of a contact to retrieve |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="contactdeleteitem"></a>ContactDeleteItem
Delete contact: Deletes a contact

```DELETE: /datasets/contacts/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a contacts folder |
| id |string |yes |path |none |Unique identifier of contact to delete |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="contactpatchitem"></a>ContactPatchItem
Update contact: Partially updates a contact

```PATCH: /datasets/contacts/tables/{table}/items/{id}```

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| table |string |yes |path |none |Unique identifier of a contacts folder |
| id |string |yes |path |none |Unique identifier of contact to update |
| item | |yes |body |none |Contact item to update |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| default |Operation Failed. |

## <a name="object-definitions"></a>Object definitions
### <a name="triggerbatchresponseidictionarystringobject"></a>TriggerBatchResponse[IDictionary[String,Object]]
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |No |

### <a name="object"></a>Object
### <a name="sendmessage"></a>SendMessage
| Property Name | Data Type | Required |
| --- | --- | --- |
| Attachments |array |No |
| From |string |No |
| Cc |string |No |
| Bcc |string |No |
| Subject |string |Yes |
| Body |string |Yes |
| Importance |string |No |
| IsHtml |boolean |No |
| To |string |Yes |

### <a name="sendattachment"></a>SendAttachment
| Property Name | Data Type | Required |
| --- | --- | --- |
| @odata.type |string |No |
| Name |string |Yes |
| ContentBytes |string |Yes |

### <a name="receivemessage"></a>ReceiveMessage
| Property Name | Data Type | Required |
| --- | --- | --- |
| Id |string |No |
| IsRead |boolean |No |
| HasAttachment |boolean |No |
| DateTimeReceived |string |No |
| Attachments |array |No |
| From |string |No |
| Cc |string |No |
| Bcc |string |No |
| Subject |string |Yes |
| Body |string |Yes |
| Importance |string |No |
| IsHtml |boolean |No |
| To |string |Yes |

### <a name="receiveattachment"></a>ReceiveAttachment
| Property Name | Data Type | Required |
| --- | --- | --- |
| Id |string |Yes |
| ContentType |string |Yes |
| @odata.type |string |No |
| Name |string |Yes |
| ContentBytes |string |Yes |

### <a name="digestmessage"></a>DigestMessage
| Property Name | Data Type | Required |
| --- | --- | --- |
| Subject |string |Yes |
| Body |string |No |
| Importance |string |No |
| Digest |array |Yes |
| Attachments |array |No |
| To |string |Yes |

### <a name="triggerbatchresponsereceivemessage"></a>TriggerBatchResponse[ReceiveMessage]
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |No |

### <a name="datasetsmetadata"></a>DataSetsMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| tabular |not defined |No |
| blob |not defined |No |

### <a name="tabulardatasetsmetadata"></a>TabularDataSetsMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| source |string |No |
| displayName |string |No |
| urlEncoding |string |No |
| tableDisplayName |string |No |
| tablePluralName |string |No |

### <a name="blobdatasetsmetadata"></a>BlobDataSetsMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| source |string |No |
| displayName |string |No |
| urlEncoding |string |No |

### <a name="tablemetadata"></a>TableMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| name |string |No |
| title |string |No |
| x-ms-permission |string |No |
| x-ms-capabilities |not defined |No |
| schema |not defined |No |

### <a name="tablecapabilitiesmetadata"></a>TableCapabilitiesMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| sortRestrictions |not defined |No |
| filterRestrictions |not defined |No |
| filterFunctions |array |No |

### <a name="tablesortrestrictionsmetadata"></a>TableSortRestrictionsMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| sortable |boolean |No |
| unsortableProperties |array |No |
| ascendingOnlyProperties |array |No |

### <a name="tablefilterrestrictionsmetadata"></a>TableFilterRestrictionsMetadata
| Property Name | Data Type | Required |
| --- | --- | --- |
| filterable |boolean |No |
| nonFilterableProperties |array |No |
| requiredProperties |array |No |

### <a name="optionsemailsubscription"></a>OptionsEmailSubscription
| Property Name | Data Type | Required |
| --- | --- | --- |
| NotificationUrl |string |No |
| Message |not defined |No |

### <a name="messagewithoptions"></a>MessageWithOptions
| Property Name | Data Type | Required |
| --- | --- | --- |
| Subject |string |Yes |
| Options |string |Yes |
| Body |string |No |
| Importance |string |No |
| Attachments |array |No |
| To |string |Yes |

### <a name="subscriptionresponse"></a>SubscriptionResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |string |No |
| resource |string |No |
| notificationType |string |No |
| notificationUrl |string |No |

### <a name="approvalemailsubscription"></a>ApprovalEmailSubscription
| Property Name | Data Type | Required |
| --- | --- | --- |
| NotificationUrl |string |No |
| Message |not defined |No |

### <a name="approvalmessage"></a>ApprovalMessage
| Property Name | Data Type | Required |
| --- | --- | --- |
| Subject |string |Yes |
| Options |string |Yes |
| Body |string |No |
| Importance |string |No |
| Attachments |array |No |
| To |string |Yes |

### <a name="approvalemailresponse"></a>ApprovalEmailResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| SelectedOption |string |No |

### <a name="tableslist"></a>TablesList
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |No |

### <a name="table"></a>Table
| Property Name | Data Type | Required |
| --- | --- | --- |
| Name |string |No |
| DisplayName |string |No |

### <a name="item"></a>Item
| Property Name | Data Type | Required |
| --- | --- | --- |
| ItemInternalId |string |No |

### <a name="calendaritemslist"></a>CalendarItemsList
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |No |

### <a name="calendaritem"></a>CalendarItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| ItemInternalId |string |No |

### <a name="contactitemslist"></a>ContactItemsList
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |No |

### <a name="contactitem"></a>ContactItem
| Property Name | Data Type | Required |
| --- | --- | --- |
| ItemInternalId |string |No |

### <a name="datasetslist"></a>DataSetsList
| Property Name | Data Type | Required |
| --- | --- | --- |
| value |array |No |

### <a name="dataset"></a>DataSet
| Property Name | Data Type | Required |
| --- | --- | --- |
| Name |string |No |
| DisplayName |string |No |

## <a name="next-steps"></a>Next Steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md)
