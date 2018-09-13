---
title: Azure Batch pool delete complete event | Microsoft Docs
description: Reference for Batch pool delete complete event.
services: batch
author: dlepow
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: danlep
ms.openlocfilehash: bfcbcf40efc64ab1c79ee1a86e02502c68ad6d47
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44813838"
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="c02d6-103">Pool delete complete event</span><span class="sxs-lookup"><span data-stu-id="c02d6-103">Pool delete complete event</span></span>

 <span data-ttu-id="c02d6-104">This event is emitted when a pool delete operation has completed.</span><span class="sxs-lookup"><span data-stu-id="c02d6-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="c02d6-105">The following example shows the body of a pool delete complete event.</span><span class="sxs-lookup"><span data-stu-id="c02d6-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="c02d6-106">Element</span><span class="sxs-lookup"><span data-stu-id="c02d6-106">Element</span></span>|<span data-ttu-id="c02d6-107">Type</span><span class="sxs-lookup"><span data-stu-id="c02d6-107">Type</span></span>|<span data-ttu-id="c02d6-108">Notes</span><span class="sxs-lookup"><span data-stu-id="c02d6-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="c02d6-109">id</span><span class="sxs-lookup"><span data-stu-id="c02d6-109">id</span></span>|<span data-ttu-id="c02d6-110">String</span><span class="sxs-lookup"><span data-stu-id="c02d6-110">String</span></span>|<span data-ttu-id="c02d6-111">The id of the pool.</span><span class="sxs-lookup"><span data-stu-id="c02d6-111">The id of the pool.</span></span>|
|<span data-ttu-id="c02d6-112">startTime</span><span class="sxs-lookup"><span data-stu-id="c02d6-112">startTime</span></span>|<span data-ttu-id="c02d6-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="c02d6-113">DateTime</span></span>|<span data-ttu-id="c02d6-114">The time the pool delete started.</span><span class="sxs-lookup"><span data-stu-id="c02d6-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="c02d6-115">endTime</span><span class="sxs-lookup"><span data-stu-id="c02d6-115">endTime</span></span>|<span data-ttu-id="c02d6-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="c02d6-116">DateTime</span></span>|<span data-ttu-id="c02d6-117">The time the pool delete completed.</span><span class="sxs-lookup"><span data-stu-id="c02d6-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="c02d6-118">Remarks</span><span class="sxs-lookup"><span data-stu-id="c02d6-118">Remarks</span></span>
<span data-ttu-id="c02d6-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="c02d6-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>