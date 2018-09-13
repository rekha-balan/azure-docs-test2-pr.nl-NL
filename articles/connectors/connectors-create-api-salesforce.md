---
title: Learn to use the Salesforce Connector in your logic apps| Microsoft Docs
description: Create logic apps with Azure App service. The Salesforce Connector provides an API to work with Salesforce objects.
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: ''
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: deonhe
ms.openlocfilehash: b6758aa36120c9c187e91ee5d9e7ceb5041eae6a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556359"
---
# <a name="get-started-with-the-salesforce-connector"></a>Get started with the Salesforce connector
The Salesforce Connector provides an API to work with Salesforce objects.

To use [any connector](apis-list.md), you first need to create a logic app. You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-to-salesforce-connector"></a>Connect to Salesforce connector
Before your logic app can access any service, you first need to create a *connection* to the service. A [connection](connectors-overview.md) provides connectivity between a logic app and another service.  

### <a name="create-a-connection-to-salesforce-connector"></a>Create a connection to Salesforce connector
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a>Use a Salesforce connector trigger
A trigger is an event that can be used to start the workflow defined in a logic app. [Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Add a condition
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a>Use a Salesforce connector action
An action is an operation carried out by the workflow defined in a logic app. [Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="technical-details"></a>Technical details
Here are the details about the triggers, actions and responses that this connection supports:

## <a name="salesforce-connector-triggers"></a>Salesforce connector triggers
Salesforce Connector has the following trigger(s):  

| Trigger | Description |
| --- | --- |
| [When an object is created](connectors-create-api-salesforce.md#when-an-object-is-created) |This operation triggers a flow when an object is created. |
| [When an object is modified](connectors-create-api-salesforce.md#when-an-object-is-modified) |This operation triggers a flow when an object is modified. |

## <a name="salesforce-connector-actions"></a>Salesforce connector actions
Salesforce Connector has the following actions:

| Action | Description |
| --- | --- |
| [Get objects](connectors-create-api-salesforce.md#get-objects) |Thie operation gets objects of a certain object type like 'Lead'. |
| [Create object](connectors-create-api-salesforce.md#create-object) |This operation creates an object. |
| [Get object](connectors-create-api-salesforce.md#get-object) |This operation gets an object. |
| [Delete object](connectors-create-api-salesforce.md#delete-object) |This operation deletes an object. |
| [Update object](connectors-create-api-salesforce.md#update-object) |This operation updates an object. |
| [Get object types](connectors-create-api-salesforce.md#get-object-types) |This operation lists the available object types. |

### <a name="action-details"></a>Action details
Here are the details for the actions and triggers for this connector, along with their responses:

### <a name="get-objects"></a>Get objects
Thie operation gets objects of a certain object type like 'Lead'. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Object type |Salesforce object type like 'Lead' |
| $filter |Filter Query |An ODATA filter query to restrict the number of entries |
| $orderby |Order By |An ODATA orderBy query for specifying the order of entries |
| $skip |Skip Count |Number of entries to skip (default = 0) |
| $top |Maximum Get Count |Maximum number of entries to retrieve (default = 256) |

An * indicates that a property is required

#### <a name="output-details"></a>Output details
ItemsList

| Property Name | Data Type |
| --- | --- |
| value |array |

### <a name="create-object"></a>Create object
This operation creates an object. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Object type |Object type like 'Lead' |
| item* |Object |Object to create |

An * indicates that a property is required

#### <a name="output-details"></a>Output details
Item

| Property Name | Data Type |
| --- | --- |
| ItemInternalId |string |

### <a name="get-object"></a>Get object
This operation gets an object. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Object type |Salesforce object type like 'Lead' |
| id* |Object id |Identifier of object to get |

An * indicates that a property is required

#### <a name="output-details"></a>Output details
Item

| Property Name | Data Type |
| --- | --- |
| ItemInternalId |string |

### <a name="delete-object"></a>Delete object
This operation deletes an object. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Object type |Object type like 'Lead' |
| id* |Object id |Identifier of object to delete |

An * indicates that a property is required

### <a name="update-object"></a>Update object
This operation updates an object. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Object type |Object type like 'Lead' |
| id* |Object id |Identifier of object to update |
| item* |Object |Object with changed properties |

An * indicates that a property is required

#### <a name="output-details"></a>Output details
Item

| Property Name | Data Type |
| --- | --- |
| ItemInternalId |string |

### <a name="when-an-object-is-created"></a>When an object is created
This operation triggers a flow when an object is created. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Object type |Object type like 'Lead' |
| $filter |Filter Query |An ODATA filter query to restrict the number of entries |
| $orderby |Order By |An ODATA orderBy query for specifying the order of entries |
| $skip |Skip Count |Number of entries to skip (default = 0) |
| $top |Maximum Get Count |Maximum number of entries to retrieve (default = 256) |

An * indicates that a property is required

#### <a name="output-details"></a>Output details
ItemsList

| Property Name | Data Type |
| --- | --- |
| value |array |

### <a name="when-an-object-is-modified"></a>When an object is modified
This operation triggers a flow when an object is modified. 

| Property Name | Display Name | Description |
| --- | --- | --- |
| table* |Object type |Object type like 'Lead' |
| $filter |Filter Query |An ODATA filter query to restrict the number of entries |
| $orderby |Order By |An ODATA orderBy query for specifying the order of entries |
| $skip |Skip Count |Number of entries to skip (default = 0) |
| $top |Maximum Get Count |Maximum number of entries to retrieve (default = 256) |

An * indicates that a property is required

#### <a name="output-details"></a>Output details
ItemsList

| Property Name | Data Type |
| --- | --- |
| value |array |

### <a name="get-object-types"></a>Get object types
This operation lists the available object types. 

There are no parameters for this call

#### <a name="output-details"></a>Output details
TablesList

| Property Name | Data Type |
| --- | --- |
| value |array |

## <a name="http-responses"></a>HTTP responses
The actions and triggers above can return one or more of the following HTTP status codes: 

| Name | Description |
| --- | --- |
| 200 |OK |
| 202 |Accepted |
| 400 |Bad Request |
| 401 |Unauthorized |
| 403 |Forbidden |
| 404 |Not Found |
| 500 |Internal Server Error. Unknown error occurred. |
| default |Operation Failed. |

## <a name="next-steps"></a>Next steps
[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md)

