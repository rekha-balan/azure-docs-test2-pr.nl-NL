---
title: Add the recurrence trigger in logic apps | Microsoft Docs
description: Overview of the recurrence trigger, and how to use it with an Azure logic app.
services: ''
documentationcenter: ''
author: jeffhollan
manager: erikre
editor: ''
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 9e76a51832b4e10691987a666d166891ca6e7b78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550764"
---
# <a name="get-started-with-the-recurrence-trigger"></a>Get started with the recurrence trigger
By using the recurrence trigger, you can create powerful workflows in the cloud.

For example, you can:

* Schedule a workflow to run a SQL stored procedure every day.
* Email a summary of all tweets within the last week about a certain hashtag.

To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Use a recurrence trigger
A trigger is an event that can be used to start the workflow that is defined in a logic app. [Learn more about triggers](connectors-overview.md).

Here’s an example sequence of how to set up a recurrence trigger in a logic app:

1. Add the **Recurrence** trigger as the first step in a logic app.
2. Fill in the parameters for the recurrence interval.

The logic app now starts a run after each interval of time.

![HTTP trigger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Trigger details
The recurrence trigger has the following properties that you can configure.

It fires a logic app after a specified time interval.
A * means that it is a required field.

| Display name | Property name | Description |
| --- | --- | --- |
| Frequency* |frequency |The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`. |
| Interval* |interval |The interval of the given frequency for the recurrence. |
| Time Zone |timeZone |If a start time is provided without a UTC offset, this time zone will be used. |
| Start time |startTime |The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Next steps
Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md). You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).


