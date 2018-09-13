---
title: Pool resize complete event - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: dfee89e3-510f-41a0-ace7-737527f40d20
caps.latest.revision: 4
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: efb523933a19fdb47790f9140bda5a3e9331b50d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563663"
---
# <a name="pool-resize-complete-event"></a>Pool resize complete event

 This event is emitted when a pool resize has completed or failed.

 The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "The operation succeeded"
}
```

|Element|Type|Notes|
|-------------|----------|-----------|
|id|String|The id of the pool.|
|nodeDeallocationOption|String|Specifies when nodes may be removed from the pool, if the pool size is decreasing.<br /><br /> Possible values are:<br /><br /> **requeue** – Terminate running tasks and requeue them. The tasks will run again when the job is enabled. Remove nodes as soon as tasks have been terminated.<br /><br /> **terminate** – Terminate running tasks. The tasks will not run again. Remove nodes as soon as tasks have been terminated.<br /><br /> **taskcompletion** – Allow currently running tasks to complete. Schedule no new tasks while waiting. Remove nodes when all tasks have completed.<br /><br /> **Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire. Schedule no new tasks while waiting. Remove nodes when all task retention periods have expired.<br /><br /> The default value is requeue.<br /><br /> If the pool size is increasing then the value is set to **invalid**.|
|currentDedicated|Int32|The number of compute nodes currently assigned to the pool.|
|targetDedicated|Int32|The number of compute nodes that are requested for the pool.|
|enableAutoScale|Bool|Specifies whether the pool size automatically adjusts over time.|
|isAutoPool|Bool|Specifies whether the pool was created via a job's AutoPool mechanism.|
|startTime|DateTime|The time the pool resize started.|
|endTime|DateTime|The time the pool resize completed.|
|resultCode|String|The result of the resize.|
|resultMessage|String|The resize error includes the details of the result.<br /><br /> If the resize completed successfully it states that the operation succeeded.|