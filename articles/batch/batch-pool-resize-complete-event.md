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
# <a name="pool-resize-complete-event"></a><span data-ttu-id="d7d8f-102">Pool resize complete event</span><span class="sxs-lookup"><span data-stu-id="d7d8f-102">Pool resize complete event</span></span>

 <span data-ttu-id="d7d8f-103">This event is emitted when a pool resize has completed or failed.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-103">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="d7d8f-104">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-104">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

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

|<span data-ttu-id="d7d8f-105">Element</span><span class="sxs-lookup"><span data-stu-id="d7d8f-105">Element</span></span>|<span data-ttu-id="d7d8f-106">Type</span><span class="sxs-lookup"><span data-stu-id="d7d8f-106">Type</span></span>|<span data-ttu-id="d7d8f-107">Notes</span><span class="sxs-lookup"><span data-stu-id="d7d8f-107">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="d7d8f-108">id</span><span class="sxs-lookup"><span data-stu-id="d7d8f-108">id</span></span>|<span data-ttu-id="d7d8f-109">String</span><span class="sxs-lookup"><span data-stu-id="d7d8f-109">String</span></span>|<span data-ttu-id="d7d8f-110">The id of the pool.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-110">The id of the pool.</span></span>|
|<span data-ttu-id="d7d8f-111">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="d7d8f-111">nodeDeallocationOption</span></span>|<span data-ttu-id="d7d8f-112">String</span><span class="sxs-lookup"><span data-stu-id="d7d8f-112">String</span></span>|<span data-ttu-id="d7d8f-113">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-113">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="d7d8f-114">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="d7d8f-114">Possible values are:</span></span><br /><br /> <span data-ttu-id="d7d8f-115">**requeue** – Terminate running tasks and requeue them.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-115">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="d7d8f-116">The tasks will run again when the job is enabled.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-116">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="d7d8f-117">Remove nodes as soon as tasks have been terminated.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-117">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="d7d8f-118">**terminate** – Terminate running tasks.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-118">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="d7d8f-119">The tasks will not run again.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-119">The tasks will not run again.</span></span> <span data-ttu-id="d7d8f-120">Remove nodes as soon as tasks have been terminated.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-120">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="d7d8f-121">**taskcompletion** – Allow currently running tasks to complete.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-121">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="d7d8f-122">Schedule no new tasks while waiting.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-122">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="d7d8f-123">Remove nodes when all tasks have completed.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-123">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="d7d8f-124">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-124">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="d7d8f-125">Schedule no new tasks while waiting.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-125">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="d7d8f-126">Remove nodes when all task retention periods have expired.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-126">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="d7d8f-127">The default value is requeue.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-127">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="d7d8f-128">If the pool size is increasing then the value is set to **invalid**.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-128">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="d7d8f-129">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="d7d8f-129">currentDedicated</span></span>|<span data-ttu-id="d7d8f-130">Int32</span><span class="sxs-lookup"><span data-stu-id="d7d8f-130">Int32</span></span>|<span data-ttu-id="d7d8f-131">The number of compute nodes currently assigned to the pool.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-131">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="d7d8f-132">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="d7d8f-132">targetDedicated</span></span>|<span data-ttu-id="d7d8f-133">Int32</span><span class="sxs-lookup"><span data-stu-id="d7d8f-133">Int32</span></span>|<span data-ttu-id="d7d8f-134">The number of compute nodes that are requested for the pool.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-134">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="d7d8f-135">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="d7d8f-135">enableAutoScale</span></span>|<span data-ttu-id="d7d8f-136">Bool</span><span class="sxs-lookup"><span data-stu-id="d7d8f-136">Bool</span></span>|<span data-ttu-id="d7d8f-137">Specifies whether the pool size automatically adjusts over time.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-137">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="d7d8f-138">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="d7d8f-138">isAutoPool</span></span>|<span data-ttu-id="d7d8f-139">Bool</span><span class="sxs-lookup"><span data-stu-id="d7d8f-139">Bool</span></span>|<span data-ttu-id="d7d8f-140">Specifies whether the pool was created via a job's AutoPool mechanism.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-140">Specifies whether the pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="d7d8f-141">startTime</span><span class="sxs-lookup"><span data-stu-id="d7d8f-141">startTime</span></span>|<span data-ttu-id="d7d8f-142">DateTime</span><span class="sxs-lookup"><span data-stu-id="d7d8f-142">DateTime</span></span>|<span data-ttu-id="d7d8f-143">The time the pool resize started.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-143">The time the pool resize started.</span></span>|
|<span data-ttu-id="d7d8f-144">endTime</span><span class="sxs-lookup"><span data-stu-id="d7d8f-144">endTime</span></span>|<span data-ttu-id="d7d8f-145">DateTime</span><span class="sxs-lookup"><span data-stu-id="d7d8f-145">DateTime</span></span>|<span data-ttu-id="d7d8f-146">The time the pool resize completed.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-146">The time the pool resize completed.</span></span>|
|<span data-ttu-id="d7d8f-147">resultCode</span><span class="sxs-lookup"><span data-stu-id="d7d8f-147">resultCode</span></span>|<span data-ttu-id="d7d8f-148">String</span><span class="sxs-lookup"><span data-stu-id="d7d8f-148">String</span></span>|<span data-ttu-id="d7d8f-149">The result of the resize.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-149">The result of the resize.</span></span>|
|<span data-ttu-id="d7d8f-150">resultMessage</span><span class="sxs-lookup"><span data-stu-id="d7d8f-150">resultMessage</span></span>|<span data-ttu-id="d7d8f-151">String</span><span class="sxs-lookup"><span data-stu-id="d7d8f-151">String</span></span>|<span data-ttu-id="d7d8f-152">The resize error includes the details of the result.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-152">The resize error includes the details of the result.</span></span><br /><br /> <span data-ttu-id="d7d8f-153">If the resize completed successfully it states that the operation succeeded.</span><span class="sxs-lookup"><span data-stu-id="d7d8f-153">If the resize completed successfully it states that the operation succeeded.</span></span>|