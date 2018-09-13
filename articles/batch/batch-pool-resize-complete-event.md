---
title: Azure Batch pool resize complete event | Microsoft Docs
description: Reference for Batch pool resize complete event.
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
ms.openlocfilehash: e91ba664a69d28cae1f82710d427bd2a391305a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821449"
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="3298c-103">Pool resize complete event</span><span class="sxs-lookup"><span data-stu-id="3298c-103">Pool resize complete event</span></span>

 <span data-ttu-id="3298c-104">This event is emitted when a pool resize has completed or failed.</span><span class="sxs-lookup"><span data-stu-id="3298c-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="3298c-105">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span><span class="sxs-lookup"><span data-stu-id="3298c-105">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

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

|<span data-ttu-id="3298c-106">Element</span><span class="sxs-lookup"><span data-stu-id="3298c-106">Element</span></span>|<span data-ttu-id="3298c-107">Type</span><span class="sxs-lookup"><span data-stu-id="3298c-107">Type</span></span>|<span data-ttu-id="3298c-108">Notes</span><span class="sxs-lookup"><span data-stu-id="3298c-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="3298c-109">id</span><span class="sxs-lookup"><span data-stu-id="3298c-109">id</span></span>|<span data-ttu-id="3298c-110">String</span><span class="sxs-lookup"><span data-stu-id="3298c-110">String</span></span>|<span data-ttu-id="3298c-111">The id of the pool.</span><span class="sxs-lookup"><span data-stu-id="3298c-111">The id of the pool.</span></span>|
|<span data-ttu-id="3298c-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="3298c-112">nodeDeallocationOption</span></span>|<span data-ttu-id="3298c-113">String</span><span class="sxs-lookup"><span data-stu-id="3298c-113">String</span></span>|<span data-ttu-id="3298c-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span><span class="sxs-lookup"><span data-stu-id="3298c-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="3298c-115">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="3298c-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="3298c-116">**requeue** – Terminate running tasks and requeue them.</span><span class="sxs-lookup"><span data-stu-id="3298c-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="3298c-117">The tasks will run again when the job is enabled.</span><span class="sxs-lookup"><span data-stu-id="3298c-117">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="3298c-118">Remove nodes as soon as tasks have been terminated.</span><span class="sxs-lookup"><span data-stu-id="3298c-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="3298c-119">**terminate** – Terminate running tasks.</span><span class="sxs-lookup"><span data-stu-id="3298c-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="3298c-120">The tasks will not run again.</span><span class="sxs-lookup"><span data-stu-id="3298c-120">The tasks will not run again.</span></span> <span data-ttu-id="3298c-121">Remove nodes as soon as tasks have been terminated.</span><span class="sxs-lookup"><span data-stu-id="3298c-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="3298c-122">**taskcompletion** – Allow currently running tasks to complete.</span><span class="sxs-lookup"><span data-stu-id="3298c-122">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="3298c-123">Schedule no new tasks while waiting.</span><span class="sxs-lookup"><span data-stu-id="3298c-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="3298c-124">Remove nodes when all tasks have completed.</span><span class="sxs-lookup"><span data-stu-id="3298c-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="3298c-125">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span><span class="sxs-lookup"><span data-stu-id="3298c-125">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="3298c-126">Schedule no new tasks while waiting.</span><span class="sxs-lookup"><span data-stu-id="3298c-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="3298c-127">Remove nodes when all task retention periods have expired.</span><span class="sxs-lookup"><span data-stu-id="3298c-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="3298c-128">The default value is requeue.</span><span class="sxs-lookup"><span data-stu-id="3298c-128">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="3298c-129">If the pool size is increasing then the value is set to **invalid**.</span><span class="sxs-lookup"><span data-stu-id="3298c-129">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="3298c-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="3298c-130">currentDedicated</span></span>|<span data-ttu-id="3298c-131">Int32</span><span class="sxs-lookup"><span data-stu-id="3298c-131">Int32</span></span>|<span data-ttu-id="3298c-132">The number of compute nodes currently assigned to the pool.</span><span class="sxs-lookup"><span data-stu-id="3298c-132">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="3298c-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="3298c-133">targetDedicated</span></span>|<span data-ttu-id="3298c-134">Int32</span><span class="sxs-lookup"><span data-stu-id="3298c-134">Int32</span></span>|<span data-ttu-id="3298c-135">The number of compute nodes that are requested for the pool.</span><span class="sxs-lookup"><span data-stu-id="3298c-135">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="3298c-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="3298c-136">enableAutoScale</span></span>|<span data-ttu-id="3298c-137">Bool</span><span class="sxs-lookup"><span data-stu-id="3298c-137">Bool</span></span>|<span data-ttu-id="3298c-138">Specifies whether the pool size automatically adjusts over time.</span><span class="sxs-lookup"><span data-stu-id="3298c-138">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="3298c-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="3298c-139">isAutoPool</span></span>|<span data-ttu-id="3298c-140">Bool</span><span class="sxs-lookup"><span data-stu-id="3298c-140">Bool</span></span>|<span data-ttu-id="3298c-141">Specifies whether the pool was created via a job's AutoPool mechanism.</span><span class="sxs-lookup"><span data-stu-id="3298c-141">Specifies whether the pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="3298c-142">startTime</span><span class="sxs-lookup"><span data-stu-id="3298c-142">startTime</span></span>|<span data-ttu-id="3298c-143">DateTime</span><span class="sxs-lookup"><span data-stu-id="3298c-143">DateTime</span></span>|<span data-ttu-id="3298c-144">The time the pool resize started.</span><span class="sxs-lookup"><span data-stu-id="3298c-144">The time the pool resize started.</span></span>|
|<span data-ttu-id="3298c-145">endTime</span><span class="sxs-lookup"><span data-stu-id="3298c-145">endTime</span></span>|<span data-ttu-id="3298c-146">DateTime</span><span class="sxs-lookup"><span data-stu-id="3298c-146">DateTime</span></span>|<span data-ttu-id="3298c-147">The time the pool resize completed.</span><span class="sxs-lookup"><span data-stu-id="3298c-147">The time the pool resize completed.</span></span>|
|<span data-ttu-id="3298c-148">resultCode</span><span class="sxs-lookup"><span data-stu-id="3298c-148">resultCode</span></span>|<span data-ttu-id="3298c-149">String</span><span class="sxs-lookup"><span data-stu-id="3298c-149">String</span></span>|<span data-ttu-id="3298c-150">The result of the resize.</span><span class="sxs-lookup"><span data-stu-id="3298c-150">The result of the resize.</span></span>|
|<span data-ttu-id="3298c-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="3298c-151">resultMessage</span></span>|<span data-ttu-id="3298c-152">String</span><span class="sxs-lookup"><span data-stu-id="3298c-152">String</span></span>|<span data-ttu-id="3298c-153">The resize error includes the details of the result.</span><span class="sxs-lookup"><span data-stu-id="3298c-153">The resize error includes the details of the result.</span></span><br /><br /> <span data-ttu-id="3298c-154">If the resize completed successfully it states that the operation succeeded.</span><span class="sxs-lookup"><span data-stu-id="3298c-154">If the resize completed successfully it states that the operation succeeded.</span></span>|