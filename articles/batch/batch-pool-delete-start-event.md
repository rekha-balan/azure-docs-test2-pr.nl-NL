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
# <a name="pool-delete-start-event"></a><span data-ttu-id="6ffcf-102">Pool delete start event</span><span class="sxs-lookup"><span data-stu-id="6ffcf-102">Pool delete start event</span></span>

 <span data-ttu-id="6ffcf-103">This event is emitted when a pool delete operation has started.</span><span class="sxs-lookup"><span data-stu-id="6ffcf-103">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="6ffcf-104">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span><span class="sxs-lookup"><span data-stu-id="6ffcf-104">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="6ffcf-105">The following example shows the body of a pool delete start event.</span><span class="sxs-lookup"><span data-stu-id="6ffcf-105">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="6ffcf-106">Element</span><span class="sxs-lookup"><span data-stu-id="6ffcf-106">Element</span></span>|<span data-ttu-id="6ffcf-107">Type</span><span class="sxs-lookup"><span data-stu-id="6ffcf-107">Type</span></span>|<span data-ttu-id="6ffcf-108">Notes</span><span class="sxs-lookup"><span data-stu-id="6ffcf-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="6ffcf-109">id</span><span class="sxs-lookup"><span data-stu-id="6ffcf-109">id</span></span>|<span data-ttu-id="6ffcf-110">String</span><span class="sxs-lookup"><span data-stu-id="6ffcf-110">String</span></span>|<span data-ttu-id="6ffcf-111">The id of the pool.</span><span class="sxs-lookup"><span data-stu-id="6ffcf-111">The id of the pool.</span></span>|