---
title: Use request and response actions | Microsoft Docs
description: Overview of the request and response trigger and action in an Azure logic app
services: ''
documentationcenter: ''
author: jeffhollan
manager: erikre
editor: ''
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 5b6aafada87dee5bb5bd5a7ce392770411f7520e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552327"
---
# <a name="get-started-with-the-request-and-response-components"></a>Get started with the request and response components
With the request and response components in a logic app, you can respond in real time to events.

For example, you can:

* Respond to an HTTP request with data from an on-premises database through a logic app.
* Trigger a logic app from an external webhook event.
* Call a logic app with a request and response action from within another logic app.

To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-the-http-request-trigger"></a>Use the HTTP Request trigger
A trigger is an event that can be used to start the workflow that is defined in a logic app. [Learn more about triggers](connectors-overview.md).

Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.

1. Add the trigger **Request - When an HTTP request is received** in your logic app. You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body. This allows the designer to generate tokens for properties in the HTTP request.
2. Add another action so that you can save the logic app.
3. After saving the logic app, you can get the HTTP request URL from the request card.
4. An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.

> [!NOTE]
> If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller. You can use the response action to customize a response.
> 
> 

![Response trigger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a>Use the HTTP Response action
The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request. If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.  You can add a response action at any step within the workflow. The logic app only keeps the incoming request open for one minute for a response.  After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.

Here's how to add an HTTP Response action:

1. Select the **New Step** button.
2. Choose **Add an action**.
3. In the action search box, type **response** to list the Response action.
   
    ![Select the response action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-reqres/using-action-1.png)
4. Add in any parameters that are required for the HTTP response message.
   
    ![Complete the response action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-reqres/using-action-2.png)
5. Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).

## <a name="request-trigger"></a>Request trigger
Here are the details for the trigger that this connector supports. There is a single request trigger.

| Trigger | Description |
| --- | --- |
| Request |Occurs when an HTTP request is received |

## <a name="response-action"></a>Response action
Here are the details for the action that this connector supports. There is a single response action that can only be used when it is accompanied by a request trigger.

| Action | Description |
| --- | --- |
| Response |Returns a response to the correlated HTTP request |

### <a name="trigger-and-action-details"></a>Trigger and action details
The following tables describe the input fields for the trigger and action, and the corresponding output details.

#### <a name="request-trigger"></a>Request trigger
The following is an input field for the trigger from an incoming HTTP request.

| Display name | Property name | Description |
| --- | --- | --- |
| JSON Schema |schema |The JSON schema of the HTTP request body |

<br>

**Output details**

The following are output details for the request.

| Property name | Data type | Description |
| --- | --- | --- |
| Headers |object |Request headers |
| Body |object |Request object |

#### <a name="response-action"></a>Response action
The following are input fields for the HTTP Response action. A * means that it is a required field.

| Display name | Property name | Description |
| --- | --- | --- |
| Status Code* |statusCode |The HTTP status code |
| Headers |headers |A JSON object of any response headers to include |
| Body |body |The response body |

## <a name="next-steps"></a>Next steps
Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md). You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).




