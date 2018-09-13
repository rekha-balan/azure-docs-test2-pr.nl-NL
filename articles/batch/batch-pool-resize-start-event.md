---
title: Pool resize start event - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 8bd33e8b-6390-4a34-95dc-2e63d8bce941
caps.latest.revision: 6
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: c8fcd5076ebe31df735d5d1f3eea823381e13fee
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553450"
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="a5792-102">Pool resize start event</span><span class="sxs-lookup"><span data-stu-id="a5792-102">Pool resize start event</span></span>

 <span data-ttu-id="a5792-103">This event is emitted when a pool resize has started.</span><span class="sxs-lookup"><span data-stu-id="a5792-103">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="a5792-104">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span><span class="sxs-lookup"><span data-stu-id="a5792-104">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="a5792-105">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span><span class="sxs-lookup"><span data-stu-id="a5792-105">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="a5792-106">Element</span><span class="sxs-lookup"><span data-stu-id="a5792-106">Element</span></span>|<span data-ttu-id="a5792-107">Type</span><span class="sxs-lookup"><span data-stu-id="a5792-107">Type</span></span>|<span data-ttu-id="a5792-108">Notes</span><span class="sxs-lookup"><span data-stu-id="a5792-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="a5792-109">poolId</span><span class="sxs-lookup"><span data-stu-id="a5792-109">poolId</span></span>|<span data-ttu-id="a5792-110">String</span><span class="sxs-lookup"><span data-stu-id="a5792-110">String</span></span>|<span data-ttu-id="a5792-111">The id of the pool.</span><span class="sxs-lookup"><span data-stu-id="a5792-111">The id of the pool.</span></span>|
|<span data-ttu-id="a5792-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="a5792-112">nodeDeallocationOption</span></span>|<span data-ttu-id="a5792-113">String</span><span class="sxs-lookup"><span data-stu-id="a5792-113">String</span></span>|<span data-ttu-id="a5792-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span><span class="sxs-lookup"><span data-stu-id="a5792-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="a5792-115">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="a5792-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="a5792-116">**requeue** – Terminate running tasks and requeue them.</span><span class="sxs-lookup"><span data-stu-id="a5792-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="a5792-117">The tasks will run again when the job is enabled.</span><span class="sxs-lookup"><span data-stu-id="a5792-117">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="a5792-118">Remove nodes as soon as tasks have been terminated.</span><span class="sxs-lookup"><span data-stu-id="a5792-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="a5792-119">**terminate** – Terminate running tasks.</span><span class="sxs-lookup"><span data-stu-id="a5792-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="a5792-120">The tasks will not run again.</span><span class="sxs-lookup"><span data-stu-id="a5792-120">The tasks will not run again.</span></span> <span data-ttu-id="a5792-121">Remove nodes as soon as tasks have been terminated.</span><span class="sxs-lookup"><span data-stu-id="a5792-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="a5792-122">**taskcompletion** – Allow currently running tasks to complete.</span><span class="sxs-lookup"><span data-stu-id="a5792-122">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="a5792-123">Schedule no new tasks while waiting.</span><span class="sxs-lookup"><span data-stu-id="a5792-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="a5792-124">Remove nodes when all tasks have completed.</span><span class="sxs-lookup"><span data-stu-id="a5792-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="a5792-125">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span><span class="sxs-lookup"><span data-stu-id="a5792-125">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="a5792-126">Schedule no new tasks while waiting.</span><span class="sxs-lookup"><span data-stu-id="a5792-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="a5792-127">Remove nodes when all task retention periods have expired.</span><span class="sxs-lookup"><span data-stu-id="a5792-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="a5792-128">The default value is requeue.</span><span class="sxs-lookup"><span data-stu-id="a5792-128">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="a5792-129">If the pool size is increasing then the value is set to **invalid**.</span><span class="sxs-lookup"><span data-stu-id="a5792-129">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="a5792-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="a5792-130">currentDedicated</span></span>|<span data-ttu-id="a5792-131">Int32</span><span class="sxs-lookup"><span data-stu-id="a5792-131">Int32</span></span>|<span data-ttu-id="a5792-132">The number of compute nodes currently assigned to the pool.</span><span class="sxs-lookup"><span data-stu-id="a5792-132">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="a5792-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="a5792-133">targetDedicated</span></span>|<span data-ttu-id="a5792-134">Int32</span><span class="sxs-lookup"><span data-stu-id="a5792-134">Int32</span></span>|<span data-ttu-id="a5792-135">The number of compute nodes that are requested for the pool.</span><span class="sxs-lookup"><span data-stu-id="a5792-135">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="a5792-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="a5792-136">enableAutoScale</span></span>|<span data-ttu-id="a5792-137">Bool</span><span class="sxs-lookup"><span data-stu-id="a5792-137">Bool</span></span>|<span data-ttu-id="a5792-138">Specifies whether the pool size automatically adjusts over time.</span><span class="sxs-lookup"><span data-stu-id="a5792-138">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="a5792-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="a5792-139">isAutoPool</span></span>|<span data-ttu-id="a5792-140">Bool</span><span class="sxs-lookup"><span data-stu-id="a5792-140">Bool</span></span>|<span data-ttu-id="a5792-141">Speficies whether the pool was created via a job's AutoPool mechanism.</span><span class="sxs-lookup"><span data-stu-id="a5792-141">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
