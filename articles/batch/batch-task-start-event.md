---
title: Azure Batch task start event | Microsoft Docs
description: Reference for Batch task start event.
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
ms.openlocfilehash: 0ad0f87df9db39088769579d538b919b42634c4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819902"
---
# <a name="task-start-event"></a><span data-ttu-id="bfb61-103">Task start event</span><span class="sxs-lookup"><span data-stu-id="bfb61-103">Task start event</span></span>

 <span data-ttu-id="bfb61-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span><span class="sxs-lookup"><span data-stu-id="bfb61-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="bfb61-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span><span class="sxs-lookup"><span data-stu-id="bfb61-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="bfb61-106">The following example shows the body of a task start event.</span><span class="sxs-lookup"><span data-stu-id="bfb61-106">The following example shows the body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="bfb61-107">Element name</span><span class="sxs-lookup"><span data-stu-id="bfb61-107">Element name</span></span>|<span data-ttu-id="bfb61-108">Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-108">Type</span></span>|<span data-ttu-id="bfb61-109">Notes</span><span class="sxs-lookup"><span data-stu-id="bfb61-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="bfb61-110">jobId</span><span class="sxs-lookup"><span data-stu-id="bfb61-110">jobId</span></span>|<span data-ttu-id="bfb61-111">String</span><span class="sxs-lookup"><span data-stu-id="bfb61-111">String</span></span>|<span data-ttu-id="bfb61-112">The id of the job containing the task.</span><span class="sxs-lookup"><span data-stu-id="bfb61-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="bfb61-113">id</span><span class="sxs-lookup"><span data-stu-id="bfb61-113">id</span></span>|<span data-ttu-id="bfb61-114">String</span><span class="sxs-lookup"><span data-stu-id="bfb61-114">String</span></span>|<span data-ttu-id="bfb61-115">The id of the task.</span><span class="sxs-lookup"><span data-stu-id="bfb61-115">The id of the task.</span></span>|
|<span data-ttu-id="bfb61-116">taskType</span><span class="sxs-lookup"><span data-stu-id="bfb61-116">taskType</span></span>|<span data-ttu-id="bfb61-117">String</span><span class="sxs-lookup"><span data-stu-id="bfb61-117">String</span></span>|<span data-ttu-id="bfb61-118">The type of the task.</span><span class="sxs-lookup"><span data-stu-id="bfb61-118">The type of the task.</span></span> <span data-ttu-id="bfb61-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span><span class="sxs-lookup"><span data-stu-id="bfb61-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="bfb61-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="bfb61-120">systemTaskVersion</span></span>|<span data-ttu-id="bfb61-121">Int32</span><span class="sxs-lookup"><span data-stu-id="bfb61-121">Int32</span></span>|<span data-ttu-id="bfb61-122">This is the internal retry counter on a task.</span><span class="sxs-lookup"><span data-stu-id="bfb61-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="bfb61-123">Internally the Batch service can retry a task to account for transient issues.</span><span class="sxs-lookup"><span data-stu-id="bfb61-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="bfb61-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span><span class="sxs-lookup"><span data-stu-id="bfb61-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="bfb61-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="bfb61-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="bfb61-126">Complex Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-126">Complex Type</span></span>|<span data-ttu-id="bfb61-127">Contains information about the compute node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="bfb61-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="bfb61-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="bfb61-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="bfb61-129">Complex Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-129">Complex Type</span></span>|<span data-ttu-id="bfb61-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span><span class="sxs-lookup"><span data-stu-id="bfb61-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="bfb61-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span><span class="sxs-lookup"><span data-stu-id="bfb61-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="bfb61-132">constraints</span><span class="sxs-lookup"><span data-stu-id="bfb61-132">constraints</span></span>](#constraints)|<span data-ttu-id="bfb61-133">Complex Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-133">Complex Type</span></span>|<span data-ttu-id="bfb61-134">The execution constraints that apply to this task.</span><span class="sxs-lookup"><span data-stu-id="bfb61-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="bfb61-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="bfb61-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="bfb61-136">Complex Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-136">Complex Type</span></span>|<span data-ttu-id="bfb61-137">Contains information about the execution of the task.</span><span class="sxs-lookup"><span data-stu-id="bfb61-137">Contains information about the execution of the task.</span></span>|

###  <a name="nodeInfo"></a> <span data-ttu-id="bfb61-138">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="bfb61-138">nodeInfo</span></span>

|<span data-ttu-id="bfb61-139">Element name</span><span class="sxs-lookup"><span data-stu-id="bfb61-139">Element name</span></span>|<span data-ttu-id="bfb61-140">Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-140">Type</span></span>|<span data-ttu-id="bfb61-141">Notes</span><span class="sxs-lookup"><span data-stu-id="bfb61-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="bfb61-142">poolId</span><span class="sxs-lookup"><span data-stu-id="bfb61-142">poolId</span></span>|<span data-ttu-id="bfb61-143">String</span><span class="sxs-lookup"><span data-stu-id="bfb61-143">String</span></span>|<span data-ttu-id="bfb61-144">The id of the pool on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="bfb61-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="bfb61-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="bfb61-145">nodeId</span></span>|<span data-ttu-id="bfb61-146">String</span><span class="sxs-lookup"><span data-stu-id="bfb61-146">String</span></span>|<span data-ttu-id="bfb61-147">The id of the node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="bfb61-147">The id of the node on which the task ran.</span></span>|

###  <a name="multiInstanceSettings"></a> <span data-ttu-id="bfb61-148">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="bfb61-148">multiInstanceSettings</span></span>

|<span data-ttu-id="bfb61-149">Element name</span><span class="sxs-lookup"><span data-stu-id="bfb61-149">Element name</span></span>|<span data-ttu-id="bfb61-150">Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-150">Type</span></span>|<span data-ttu-id="bfb61-151">Notes</span><span class="sxs-lookup"><span data-stu-id="bfb61-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="bfb61-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="bfb61-152">numberOfInstances</span></span>|<span data-ttu-id="bfb61-153">Int</span><span class="sxs-lookup"><span data-stu-id="bfb61-153">Int</span></span>|<span data-ttu-id="bfb61-154">The number of compute nodes required by the task.</span><span class="sxs-lookup"><span data-stu-id="bfb61-154">The number of compute nodes required by the task.</span></span>|

###  <a name="constraints"></a> <span data-ttu-id="bfb61-155">constraints</span><span class="sxs-lookup"><span data-stu-id="bfb61-155">constraints</span></span>

|<span data-ttu-id="bfb61-156">Element name</span><span class="sxs-lookup"><span data-stu-id="bfb61-156">Element name</span></span>|<span data-ttu-id="bfb61-157">Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-157">Type</span></span>|<span data-ttu-id="bfb61-158">Notes</span><span class="sxs-lookup"><span data-stu-id="bfb61-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="bfb61-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="bfb61-159">maxTaskRetryCount</span></span>|<span data-ttu-id="bfb61-160">Int32</span><span class="sxs-lookup"><span data-stu-id="bfb61-160">Int32</span></span>|<span data-ttu-id="bfb61-161">The maximum number of times the task may be retried.</span><span class="sxs-lookup"><span data-stu-id="bfb61-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="bfb61-162">The Batch service retries a task if its exit code is nonzero.</span><span class="sxs-lookup"><span data-stu-id="bfb61-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="bfb61-163">Note that this value specifically controls the number of retries.</span><span class="sxs-lookup"><span data-stu-id="bfb61-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="bfb61-164">The Batch service will try the task once, and may then retry up to this limit.</span><span class="sxs-lookup"><span data-stu-id="bfb61-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="bfb61-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span><span class="sxs-lookup"><span data-stu-id="bfb61-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="bfb61-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span><span class="sxs-lookup"><span data-stu-id="bfb61-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="bfb61-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span><span class="sxs-lookup"><span data-stu-id="bfb61-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="bfb61-168">The default value is 0 (no retries).</span><span class="sxs-lookup"><span data-stu-id="bfb61-168">The default value is 0 (no retries).</span></span>|

###  <a name="executionInfo"></a> <span data-ttu-id="bfb61-169">executionInfo</span><span class="sxs-lookup"><span data-stu-id="bfb61-169">executionInfo</span></span>

|<span data-ttu-id="bfb61-170">Element name</span><span class="sxs-lookup"><span data-stu-id="bfb61-170">Element name</span></span>|<span data-ttu-id="bfb61-171">Type</span><span class="sxs-lookup"><span data-stu-id="bfb61-171">Type</span></span>|<span data-ttu-id="bfb61-172">Notes</span><span class="sxs-lookup"><span data-stu-id="bfb61-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="bfb61-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="bfb61-173">retryCount</span></span>|<span data-ttu-id="bfb61-174">Int32</span><span class="sxs-lookup"><span data-stu-id="bfb61-174">Int32</span></span>|<span data-ttu-id="bfb61-175">The number of times the task has been retried by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="bfb61-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="bfb61-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="bfb61-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
