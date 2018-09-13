---
title: SendGrid | Microsoft Docs
description: Create Logic apps with Azure App service. SendGrid Connection Provider lets you send email and manage recipient lists.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: bc4f1fc2-824c-4ed7-8de8-e82baff3b746
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: deonhe
ms.openlocfilehash: e30231bd576436ae69f4fa42d0e2ab312c3938d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549547"
---
# <a name="get-started-with-the-sendgrid-connector"></a>Get started with the SendGrid connector
SendGrid Connection Provider lets you send email and manage recipient lists.

> [!NOTE]
> This version of the article applies to logic apps 2015-08-01-preview schema version. 
> 
> 

You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="triggers-and-actions"></a>Triggers and actions
The SendGrid connector can be used as an action; it has trigger(s). All connectors support data in JSON and XML formats. 

 The SendGrid connector has the following actions available. There are no triggers.

### <a name="sendgrid-actions"></a>SendGrid actions
You can take these action(s):

| Action | Description |
| --- | --- |
| [SendEmail](connectors-create-api-sendgrid.md#sendemail) |Sends an email using SendGrid API (Limited to 10,000 recipients) |
| [AddRecipientToList](connectors-create-api-sendgrid.md#addrecipienttolist) |Add an individual recipient to a recipient list |

## <a name="create-a-connection-to-sendgrid"></a>Create a connection to SendGrid
To create Logic apps with SendGrid, you must first create a **connection** then provide the details for the following properties: 

| Property | Required | Description |
| --- | --- | --- |
| ApiKey |Yes |Provide Your SendGrid Api Key |

> [!INCLUDE [Steps to create a connection to SendGrid](../../includes/connectors-create-api-sendgrid.md)]
> 
> [!TIP]
> You can use this connection in other logic apps.
> 
> 

After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.

## <a name="reference-for-sendgrid"></a>Reference for SendGrid
Applies to version: 1.0

## <a name="sendemail"></a>SendEmail
Send email: Sends an email using SendGrid API (Limited to 10,000 recipients) 

```POST: /api/mail.send.json``` 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| request | |yes |body |none |Email message to send |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 400 |Bad Request |
| 401 |Unauthorized |
| 403 |Forbidden |
| 404 |Not Found |
| 429 |Too Many Request |
| 500 |Internal Server Error. Unknown error occured |
| default |Operation Failed. |

## <a name="addrecipienttolist"></a>AddRecipientToList
Add recipient to list: Add an individual recipient to a recipient list 

```POST: /v3/contactdb/lists/{listId}/recipients/{recipientId}``` 

| Name | Data Type | Required | Located In | Default Value | Description |
| --- | --- | --- | --- | --- | --- |
| listId |string |yes |path |none |Unique id of the recipient list |
| recipientId |string |yes |path |none |Unique id of the recipient |

#### <a name="response"></a>Response
| Name | Description |
| --- | --- |
| 200 |OK |
| 400 |Bad Request |
| 401 |Unauthorized |
| 403 |Forbidden |
| 404 |Not Found |
| 500 |Internal Server Error. Unknown error occured |
| default |Operation Failed. |

## <a name="object-definitions"></a>Object definitions
### <a name="emailrequest"></a>EmailRequest
| Property Name | Data Type | Required |
| --- | --- | --- |
| from |string |Yes |
| fromname |string |No |
| to |string |Yes |
| toname |string |No |
| subject |string |Yes |
| body |string |Yes |
| ishtml |boolean |No |
| cc |string |No |
| ccname |string |No |
| bcc |string |No |
| bccname |string |No |
| replyto |string |No |
| date |string |No |
| headers |string |No |
| files |array |No |
| filenames |array |No |

### <a name="emailresponse"></a>EmailResponse
| Property Name | Data Type | Required |
| --- | --- | --- |
| message |string |No |

### <a name="recipientlists"></a>RecipientLists
| Property Name | Data Type | Required |
| --- | --- | --- |
| lists |array |No |

### <a name="recipientlist"></a>RecipientList
| Property Name | Data Type | Required |
| --- | --- | --- |
| id |integer |No |
| name |string |No |
| recipient_count |integer |No |

### <a name="recipients"></a>Recipients
| Property Name | Data Type | Required |
| --- | --- | --- |
| recipients |array |No |

### <a name="recipient"></a>Recipient
| Property Name | Data Type | Required |
| --- | --- | --- |
| email |string |No |
| last_name |string |No |
| first_name |string |No |
| id |string |No |

## <a name="next-steps"></a>Next Steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md)

