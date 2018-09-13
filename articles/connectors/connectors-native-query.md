---
title: Add the query action in logic apps | Microsoft Docs
description: Overview of the query action for performing actions like filter array.
services: ''
documentationcenter: ''
author: jeffhollan
manager: erikre
editor: ''
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 207971c29112c1cb4c7c1074a9f35f9baf0d4bc7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554925"
---
# <a name="get-started-with-the-query-action"></a>Get started with the query action
By using the query action, you can work with batches and arrays to accomplish workflows to:

* Create a task for all high-priority records from a database.
* Save all PDF attachments for emails into an Azure blob.

To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-the-query-action"></a>Use the query action
An action is an operation that is carried out by the workflow that is defined in a logic app. [Learn more about actions](connectors-overview.md).  

The query action currently has one operation, called the filter array, that is exposed in the designer. This allows you to query an array and return a set of filtered results.

Here's how you can add it in a logic app:

1. Select the **New Step** button.
2. Choose **Add an action**.
3. In the action search box, type **filter** to list the **Filter array** action.
   
    ![Select the query action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-query/using-action-1.png)
4. Select an array to filter. (The following screenshot shows the array of results from a Twitter search.)
5. Create a condition to evaluate on each item. (The following screenshot filters tweets from users who have more than 100 followers.)
   
    ![Complete the query action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-query/using-action-2.png)
   
    The action will output a new array that contains only results that met the filter requirements.
6. Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).

## <a name="query-action"></a>Query action
Here are the details for the action that this connector supports. The connector has one possible action.

| Action | Description |
| --- | --- |
| Filter array |Evaluates a condition for each item in an array and returns the results |

## <a name="action-details"></a>Action details
The query action comes with one possible action. The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.

### <a name="filter-array"></a>Filter array
The following are input fields for the action, which makes an HTTP outbound request.
A * means that it is a required field.

| Display name | Property name | Description |
| --- | --- | --- |
| From* |from |The array to filter |
| Condition* |where |The condition to evaluate for each item |

<br>

### <a name="output-details"></a>Output details
The following are output details for the HTTP response.

| Property name | Data type | Description |
| --- | --- | --- |
| Filtered array |array |An array that contains an object for each filtered result |

## <a name="next-steps"></a>Next steps
Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md). You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).


