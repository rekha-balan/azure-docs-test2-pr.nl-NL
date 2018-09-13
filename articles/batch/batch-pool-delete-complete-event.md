---
title: Pool delete complete event - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 580a1278-5740-4143-826c-7d875ef127ff
caps.latest.revision: 5
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: 0710d5762f0e68380a531f94baa88a8007565912
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563680"
---
# <a name="pool-delete-complete-event"></a>Pool delete complete event

 This event is emitted when a pool delete operation has completed.

 The following example shows the body of a pool delete complete event.

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|Element|Type|Notes|
|-------------|----------|-----------|
|id|String|The id of the pool.|
|startTime|DateTime|The time the pool delete started.|
|endTime|DateTime|The time the pool delete completed.|

## <a name="remarks"></a>Remarks
For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).