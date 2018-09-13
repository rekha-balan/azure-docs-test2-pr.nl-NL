---
title: System variables in Azure Data Factory | Microsoft Docs
description: This article describes system variables supported by Azure Data Factory. You can use these variables in expressions when defining Data Factory entities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/12/2018
ms.author: shlo
ms.openlocfilehash: 43ea8703bdbfc23511c831a5f91c9461948cc254
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856407"
---
# <a name="system-variables-supported-by-azure-data-factory"></a>System variables supported by Azure Data Factory
This article describes system variables supported by Azure Data Factory. You can use these variables in expressions when defining Data Factory entities.

## <a name="pipeline-scope"></a>Pipeline scope
These system variables can be referenced anywhere in the pipeline JSON.

| Variable Name | Description |
| --- | --- |
| @pipeline().DataFactory |Name of the data factory the pipeline run is running within |
| @pipeline().Pipeline |Name of the pipeline |
| @pipeline().RunId | ID of the specific pipeline run |
| @pipeline().TriggerType | Type of the trigger that invoked the pipeline (Manual, Scheduler) |
| @pipeline().TriggerId| ID of the trigger that invokes the pipeline |
| @pipeline().TriggerName| Name of the trigger that invokes the pipeline |
| @pipeline().TriggerTime| Time when the trigger that invoked the pipeline. The trigger time is the actual fired time, not the scheduled time. For example, `13:20:08.0149599Z` is returned instead of `13:20:00.00Z` |

## <a name="schedule-trigger-scope"></a>Schedule Trigger scope
These system variables can be referenced anywhere in the trigger JSON if the trigger is of type: "ScheduleTrigger."

| Variable Name | Description |
| --- | --- |
| @trigger().scheduledTime |Time when the trigger was scheduled to invoke the pipeline run. For example, for a trigger that fires every 5 min, this variable would return `2017-06-01T22:20:00Z`, `2017-06-01T22:25:00Z`, `2017-06-01T22:29:00Z` respectively.|
| @trigger().startTime |Time when the trigger **actually** fired to invoke the pipeline run. For example, for a trigger that fires every 5 min, this variable might return something like this `2017-06-01T22:20:00.4061448Z`, `2017-06-01T22:25:00.7958577Z`, `2017-06-01T22:29:00.9935483Z` respectively.|

## <a name="tumbling-window-trigger-scope"></a>Tumbling Window Trigger scope
These system variables can be referenced anywhere in the trigger JSON if the trigger is of type: "TumblingWindowTrigger."

| Variable Name | Description |
| --- | --- |
| @trigger().outputs.windowStartTime |Start of the window when the trigger was scheduled to invoke the pipeline run. If the tumbling window trigger has a frequency of "hourly" this would be the time at the beginning of the hour.|
| @trigger().outputs.windowEndTime |End of the window when the trigger was scheduled to invoke the pipeline run. If the tumbling window trigger has a frequency of "hourly" this would be the time at the end of the hour.|
## <a name="next-steps"></a>Next steps
For information about how these variables are used in expressions, see [Expression language & functions](control-flow-expression-language-functions.md).
