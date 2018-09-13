---
title: Azure Batch task complete event | Microsoft Docs
description: Reference for Batch task complete event.
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
ms.openlocfilehash: 9f25d9cbdc70282afd71b1a4b9ac72250922d163
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774416"
---
# <a name="task-complete-event"></a><span data-ttu-id="d17a8-103">Task complete event</span><span class="sxs-lookup"><span data-stu-id="d17a8-103">Task complete event</span></span>

 <span data-ttu-id="d17a8-104">This event is emitted once a task is completed, regardless of the exit code.</span><span class="sxs-lookup"><span data-stu-id="d17a8-104">This event is emitted once a task is completed, regardless of the exit code.</span></span> <span data-ttu-id="d17a8-105">This event can be used to determine the duration of a task, where the task ran, and whether it was retried.</span><span class="sxs-lookup"><span data-stu-id="d17a8-105">This event can be used to determine the duration of a task, where the task ran, and whether it was retried.</span></span>


 <span data-ttu-id="d17a8-106">The following example shows the body of a task complete event.</span><span class="sxs-lookup"><span data-stu-id="d17a8-106">The following example shows the body of a task complete event.</span></span>

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
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|<span data-ttu-id="d17a8-107">Element name</span><span class="sxs-lookup"><span data-stu-id="d17a8-107">Element name</span></span>|<span data-ttu-id="d17a8-108">Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-108">Type</span></span>|<span data-ttu-id="d17a8-109">Notes</span><span class="sxs-lookup"><span data-stu-id="d17a8-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d17a8-110">jobId</span><span class="sxs-lookup"><span data-stu-id="d17a8-110">jobId</span></span>|<span data-ttu-id="d17a8-111">String</span><span class="sxs-lookup"><span data-stu-id="d17a8-111">String</span></span>|<span data-ttu-id="d17a8-112">The id of the job containing the task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="d17a8-113">id</span><span class="sxs-lookup"><span data-stu-id="d17a8-113">id</span></span>|<span data-ttu-id="d17a8-114">String</span><span class="sxs-lookup"><span data-stu-id="d17a8-114">String</span></span>|<span data-ttu-id="d17a8-115">The id of the task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-115">The id of the task.</span></span>|
|<span data-ttu-id="d17a8-116">taskType</span><span class="sxs-lookup"><span data-stu-id="d17a8-116">taskType</span></span>|<span data-ttu-id="d17a8-117">String</span><span class="sxs-lookup"><span data-stu-id="d17a8-117">String</span></span>|<span data-ttu-id="d17a8-118">The type of the task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-118">The type of the task.</span></span> <span data-ttu-id="d17a8-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="d17a8-120">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span><span class="sxs-lookup"><span data-stu-id="d17a8-120">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="d17a8-121">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="d17a8-121">systemTaskVersion</span></span>|<span data-ttu-id="d17a8-122">Int32</span><span class="sxs-lookup"><span data-stu-id="d17a8-122">Int32</span></span>|<span data-ttu-id="d17a8-123">This is the internal retry counter on a task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-123">This is the internal retry counter on a task.</span></span> <span data-ttu-id="d17a8-124">Internally the Batch service can retry a task to account for transient issues.</span><span class="sxs-lookup"><span data-stu-id="d17a8-124">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="d17a8-125">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span><span class="sxs-lookup"><span data-stu-id="d17a8-125">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="d17a8-126">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="d17a8-126">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="d17a8-127">Complex Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-127">Complex Type</span></span>|<span data-ttu-id="d17a8-128">Contains information about the compute node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="d17a8-128">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="d17a8-129">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="d17a8-129">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="d17a8-130">Complex Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-130">Complex Type</span></span>|<span data-ttu-id="d17a8-131">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span><span class="sxs-lookup"><span data-stu-id="d17a8-131">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="d17a8-132">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span><span class="sxs-lookup"><span data-stu-id="d17a8-132">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="d17a8-133">constraints</span><span class="sxs-lookup"><span data-stu-id="d17a8-133">constraints</span></span>](#constraints)|<span data-ttu-id="d17a8-134">Complex Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-134">Complex Type</span></span>|<span data-ttu-id="d17a8-135">The execution constraints that apply to this task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-135">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="d17a8-136">executionInfo</span><span class="sxs-lookup"><span data-stu-id="d17a8-136">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="d17a8-137">Complex Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-137">Complex Type</span></span>|<span data-ttu-id="d17a8-138">Contains information about the execution of the task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-138">Contains information about the execution of the task.</span></span>|

###  <a name="nodeInfo"></a> <span data-ttu-id="d17a8-139">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="d17a8-139">nodeInfo</span></span>

|<span data-ttu-id="d17a8-140">Element name</span><span class="sxs-lookup"><span data-stu-id="d17a8-140">Element name</span></span>|<span data-ttu-id="d17a8-141">Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-141">Type</span></span>|<span data-ttu-id="d17a8-142">Notes</span><span class="sxs-lookup"><span data-stu-id="d17a8-142">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d17a8-143">poolId</span><span class="sxs-lookup"><span data-stu-id="d17a8-143">poolId</span></span>|<span data-ttu-id="d17a8-144">String</span><span class="sxs-lookup"><span data-stu-id="d17a8-144">String</span></span>|<span data-ttu-id="d17a8-145">The id of the pool on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="d17a8-145">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="d17a8-146">nodeId</span><span class="sxs-lookup"><span data-stu-id="d17a8-146">nodeId</span></span>|<span data-ttu-id="d17a8-147">String</span><span class="sxs-lookup"><span data-stu-id="d17a8-147">String</span></span>|<span data-ttu-id="d17a8-148">The id of the node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="d17a8-148">The id of the node on which the task ran.</span></span>|

###  <a name="multiInstanceSettings"></a> <span data-ttu-id="d17a8-149">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="d17a8-149">multiInstanceSettings</span></span>

|<span data-ttu-id="d17a8-150">Element name</span><span class="sxs-lookup"><span data-stu-id="d17a8-150">Element name</span></span>|<span data-ttu-id="d17a8-151">Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-151">Type</span></span>|<span data-ttu-id="d17a8-152">Notes</span><span class="sxs-lookup"><span data-stu-id="d17a8-152">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d17a8-153">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="d17a8-153">numberOfInstances</span></span>|<span data-ttu-id="d17a8-154">Int32</span><span class="sxs-lookup"><span data-stu-id="d17a8-154">Int32</span></span>|<span data-ttu-id="d17a8-155">The number of compute nodes required by the task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-155">The number of compute nodes required by the task.</span></span>|

###  <a name="constraints"></a> <span data-ttu-id="d17a8-156">constraints</span><span class="sxs-lookup"><span data-stu-id="d17a8-156">constraints</span></span>

|<span data-ttu-id="d17a8-157">Element name</span><span class="sxs-lookup"><span data-stu-id="d17a8-157">Element name</span></span>|<span data-ttu-id="d17a8-158">Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-158">Type</span></span>|<span data-ttu-id="d17a8-159">Notes</span><span class="sxs-lookup"><span data-stu-id="d17a8-159">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d17a8-160">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="d17a8-160">maxTaskRetryCount</span></span>|<span data-ttu-id="d17a8-161">Int32</span><span class="sxs-lookup"><span data-stu-id="d17a8-161">Int32</span></span>|<span data-ttu-id="d17a8-162">The maximum number of times the task may be retried.</span><span class="sxs-lookup"><span data-stu-id="d17a8-162">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="d17a8-163">The Batch service retries a task if its exit code is nonzero.</span><span class="sxs-lookup"><span data-stu-id="d17a8-163">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="d17a8-164">Note that this value specifically controls the number of retries.</span><span class="sxs-lookup"><span data-stu-id="d17a8-164">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="d17a8-165">The Batch service will try the task once, and may then retry up to this limit.</span><span class="sxs-lookup"><span data-stu-id="d17a8-165">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="d17a8-166">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span><span class="sxs-lookup"><span data-stu-id="d17a8-166">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="d17a8-167">If the maximum retry count is 0, the Batch service does not retry tasks.</span><span class="sxs-lookup"><span data-stu-id="d17a8-167">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="d17a8-168">If the maximum retry count is -1, the Batch service retries tasks without limit.</span><span class="sxs-lookup"><span data-stu-id="d17a8-168">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="d17a8-169">The default value is 0 (no retries).</span><span class="sxs-lookup"><span data-stu-id="d17a8-169">The default value is 0 (no retries).</span></span>|

###  <a name="executionInfo"></a> <span data-ttu-id="d17a8-170">executionInfo</span><span class="sxs-lookup"><span data-stu-id="d17a8-170">executionInfo</span></span>

|<span data-ttu-id="d17a8-171">Element name</span><span class="sxs-lookup"><span data-stu-id="d17a8-171">Element name</span></span>|<span data-ttu-id="d17a8-172">Type</span><span class="sxs-lookup"><span data-stu-id="d17a8-172">Type</span></span>|<span data-ttu-id="d17a8-173">Notes</span><span class="sxs-lookup"><span data-stu-id="d17a8-173">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="d17a8-174">startTime</span><span class="sxs-lookup"><span data-stu-id="d17a8-174">startTime</span></span>|<span data-ttu-id="d17a8-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="d17a8-175">DateTime</span></span>|<span data-ttu-id="d17a8-176">The time at which the task started running.</span><span class="sxs-lookup"><span data-stu-id="d17a8-176">The time at which the task started running.</span></span> <span data-ttu-id="d17a8-177">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span><span class="sxs-lookup"><span data-stu-id="d17a8-177">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="d17a8-178">If the task has been restarted or retried, this is the most recent time at which the task started running.</span><span class="sxs-lookup"><span data-stu-id="d17a8-178">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="d17a8-179">endTime</span><span class="sxs-lookup"><span data-stu-id="d17a8-179">endTime</span></span>|<span data-ttu-id="d17a8-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="d17a8-180">DateTime</span></span>|<span data-ttu-id="d17a8-181">The time at which the task completed.</span><span class="sxs-lookup"><span data-stu-id="d17a8-181">The time at which the task completed.</span></span>|
|<span data-ttu-id="d17a8-182">exitCode</span><span class="sxs-lookup"><span data-stu-id="d17a8-182">exitCode</span></span>|<span data-ttu-id="d17a8-183">Int32</span><span class="sxs-lookup"><span data-stu-id="d17a8-183">Int32</span></span>|<span data-ttu-id="d17a8-184">The exit code of the task.</span><span class="sxs-lookup"><span data-stu-id="d17a8-184">The exit code of the task.</span></span>|
|<span data-ttu-id="d17a8-185">retryCount</span><span class="sxs-lookup"><span data-stu-id="d17a8-185">retryCount</span></span>|<span data-ttu-id="d17a8-186">Int32</span><span class="sxs-lookup"><span data-stu-id="d17a8-186">Int32</span></span>|<span data-ttu-id="d17a8-187">The number of times the task has been retried by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="d17a8-187">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="d17a8-188">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span><span class="sxs-lookup"><span data-stu-id="d17a8-188">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="d17a8-189">requeueCount</span><span class="sxs-lookup"><span data-stu-id="d17a8-189">requeueCount</span></span>|<span data-ttu-id="d17a8-190">Int32</span><span class="sxs-lookup"><span data-stu-id="d17a8-190">Int32</span></span>|<span data-ttu-id="d17a8-191">The number of times the task has been requeued by the Batch service as the result of a user request.</span><span class="sxs-lookup"><span data-stu-id="d17a8-191">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="d17a8-192">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span><span class="sxs-lookup"><span data-stu-id="d17a8-192">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="d17a8-193">This count tracks how many times the task has been requeued for these reasons.</span><span class="sxs-lookup"><span data-stu-id="d17a8-193">This count tracks how many times the task has been requeued for these reasons.</span></span>|
