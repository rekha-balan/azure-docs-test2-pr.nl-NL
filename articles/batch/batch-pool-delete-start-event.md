---
title: Pool delete start event - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: feddca1e-c69c-4257-be44-a36172e77157
caps.latest.revision: 4
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: 6b1d311b0e6a1152e5c19be1afe2d7ffefe5d696
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669455"
---
# <a name="pool-delete-start-event"></a>Pool delete start event

 This event is emitted when a pool delete operation has started. Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.

 The following example shows the body of a pool delete start event.

```
{
    "id": "myPool1"
}
```

|Element|Type|Notes|
|-------------|----------|-----------|
|id|String|The id of the pool.|