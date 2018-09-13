---
title: Task complete event - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 9dcc468b-e0a7-4b80-bec8-ffd466afdc8a
caps.latest.revision: 4
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: 03093ab26f8e394cb89be39542d86388f030cf50
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562907"
---
# <a name="task-complete-event"></a><span data-ttu-id="daaa0-102">Task complete event</span><span class="sxs-lookup"><span data-stu-id="daaa0-102">Task complete event</span></span>

 <span data-ttu-id="daaa0-103">This event is emitted once a task is completed, regardless of the exit code.</span><span class="sxs-lookup"><span data-stu-id="daaa0-103">This event is emitted once a task is completed, regardless of the exit code.</span></span> <span data-ttu-id="daaa0-104">This event can be used to determine the duration of a task, where the task ran, and whether it was retried.</span><span class="sxs-lookup"><span data-stu-id="daaa0-104">This event can be used to determine the duration of a task, where the task ran, and whether it was retried.</span></span>


 <span data-ttu-id="daaa0-105">The following example shows the body of a task complete event.</span><span class="sxs-lookup"><span data-stu-id="daaa0-105">The following example shows the body of a task complete event.</span></span>

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

|<span data-ttu-id="daaa0-106">Element name</span><span class="sxs-lookup"><span data-stu-id="daaa0-106">Element name</span></span>|<span data-ttu-id="daaa0-107">Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-107">Type</span></span>|<span data-ttu-id="daaa0-108">Notes</span><span class="sxs-lookup"><span data-stu-id="daaa0-108">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="daaa0-109">jobId</span><span class="sxs-lookup"><span data-stu-id="daaa0-109">jobId</span></span>|<span data-ttu-id="daaa0-110">String</span><span class="sxs-lookup"><span data-stu-id="daaa0-110">String</span></span>|<span data-ttu-id="daaa0-111">The id of the job containing the task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-111">The id of the job containing the task.</span></span>|
|<span data-ttu-id="daaa0-112">id</span><span class="sxs-lookup"><span data-stu-id="daaa0-112">id</span></span>|<span data-ttu-id="daaa0-113">String</span><span class="sxs-lookup"><span data-stu-id="daaa0-113">String</span></span>|<span data-ttu-id="daaa0-114">The id of the task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-114">The id of the task.</span></span>|
|<span data-ttu-id="daaa0-115">taskType</span><span class="sxs-lookup"><span data-stu-id="daaa0-115">taskType</span></span>|<span data-ttu-id="daaa0-116">String</span><span class="sxs-lookup"><span data-stu-id="daaa0-116">String</span></span>|<span data-ttu-id="daaa0-117">The type of the task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-117">The type of the task.</span></span> <span data-ttu-id="daaa0-118">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-118">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="daaa0-119">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span><span class="sxs-lookup"><span data-stu-id="daaa0-119">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="daaa0-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="daaa0-120">systemTaskVersion</span></span>|<span data-ttu-id="daaa0-121">Int32</span><span class="sxs-lookup"><span data-stu-id="daaa0-121">Int32</span></span>|<span data-ttu-id="daaa0-122">This is the internal retry counter on a task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="daaa0-123">Internally the Batch service can retry a task to account for transient issues.</span><span class="sxs-lookup"><span data-stu-id="daaa0-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="daaa0-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span><span class="sxs-lookup"><span data-stu-id="daaa0-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="daaa0-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="daaa0-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="daaa0-126">Complex Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-126">Complex Type</span></span>|<span data-ttu-id="daaa0-127">Contains information about the compute node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="daaa0-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="daaa0-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="daaa0-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="daaa0-129">Complex Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-129">Complex Type</span></span>|<span data-ttu-id="daaa0-130">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span><span class="sxs-lookup"><span data-stu-id="daaa0-130">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="daaa0-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span><span class="sxs-lookup"><span data-stu-id="daaa0-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="daaa0-132">constraints</span><span class="sxs-lookup"><span data-stu-id="daaa0-132">constraints</span></span>](#constraints)|<span data-ttu-id="daaa0-133">Complex Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-133">Complex Type</span></span>|<span data-ttu-id="daaa0-134">The execution constraints that apply to this task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="daaa0-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="daaa0-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="daaa0-136">Complex Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-136">Complex Type</span></span>|<span data-ttu-id="daaa0-137">Contains information about the execution of the task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-137">Contains information about the execution of the task.</span></span>|

###  <a name="nodeInfo"></a> <span data-ttu-id="daaa0-138">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="daaa0-138">nodeInfo</span></span>

|<span data-ttu-id="daaa0-139">Element name</span><span class="sxs-lookup"><span data-stu-id="daaa0-139">Element name</span></span>|<span data-ttu-id="daaa0-140">Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-140">Type</span></span>|<span data-ttu-id="daaa0-141">Notes</span><span class="sxs-lookup"><span data-stu-id="daaa0-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="daaa0-142">poolId</span><span class="sxs-lookup"><span data-stu-id="daaa0-142">poolId</span></span>|<span data-ttu-id="daaa0-143">String</span><span class="sxs-lookup"><span data-stu-id="daaa0-143">String</span></span>|<span data-ttu-id="daaa0-144">The id of the pool on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="daaa0-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="daaa0-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="daaa0-145">nodeId</span></span>|<span data-ttu-id="daaa0-146">String</span><span class="sxs-lookup"><span data-stu-id="daaa0-146">String</span></span>|<span data-ttu-id="daaa0-147">The id of the node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="daaa0-147">The id of the node on which the task ran.</span></span>|

###  <a name="multiInstanceSettings"></a> <span data-ttu-id="daaa0-148">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="daaa0-148">multiInstanceSettings</span></span>

|<span data-ttu-id="daaa0-149">Element name</span><span class="sxs-lookup"><span data-stu-id="daaa0-149">Element name</span></span>|<span data-ttu-id="daaa0-150">Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-150">Type</span></span>|<span data-ttu-id="daaa0-151">Notes</span><span class="sxs-lookup"><span data-stu-id="daaa0-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="daaa0-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="daaa0-152">numberOfInstances</span></span>|<span data-ttu-id="daaa0-153">Int32</span><span class="sxs-lookup"><span data-stu-id="daaa0-153">Int32</span></span>|<span data-ttu-id="daaa0-154">The number of compute nodes required by the task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-154">The number of compute nodes required by the task.</span></span>|

###  <a name="constraints"></a> <span data-ttu-id="daaa0-155">constraints</span><span class="sxs-lookup"><span data-stu-id="daaa0-155">constraints</span></span>

|<span data-ttu-id="daaa0-156">Element name</span><span class="sxs-lookup"><span data-stu-id="daaa0-156">Element name</span></span>|<span data-ttu-id="daaa0-157">Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-157">Type</span></span>|<span data-ttu-id="daaa0-158">Notes</span><span class="sxs-lookup"><span data-stu-id="daaa0-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="daaa0-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="daaa0-159">maxTaskRetryCount</span></span>|<span data-ttu-id="daaa0-160">Int32</span><span class="sxs-lookup"><span data-stu-id="daaa0-160">Int32</span></span>|<span data-ttu-id="daaa0-161">The maximum number of times the task may be retried.</span><span class="sxs-lookup"><span data-stu-id="daaa0-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="daaa0-162">The Batch service retries a task if its exit code is nonzero.</span><span class="sxs-lookup"><span data-stu-id="daaa0-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="daaa0-163">Note that this value specifically controls the number of retries.</span><span class="sxs-lookup"><span data-stu-id="daaa0-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="daaa0-164">The Batch service will try the task once, and may then retry up to this limit.</span><span class="sxs-lookup"><span data-stu-id="daaa0-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="daaa0-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span><span class="sxs-lookup"><span data-stu-id="daaa0-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="daaa0-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span><span class="sxs-lookup"><span data-stu-id="daaa0-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="daaa0-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span><span class="sxs-lookup"><span data-stu-id="daaa0-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="daaa0-168">The default value is 0 (no retries).</span><span class="sxs-lookup"><span data-stu-id="daaa0-168">The default value is 0 (no retries).</span></span>|

###  <a name="executionInfo"></a> <span data-ttu-id="daaa0-169">executionInfo</span><span class="sxs-lookup"><span data-stu-id="daaa0-169">executionInfo</span></span>

|<span data-ttu-id="daaa0-170">Element name</span><span class="sxs-lookup"><span data-stu-id="daaa0-170">Element name</span></span>|<span data-ttu-id="daaa0-171">Type</span><span class="sxs-lookup"><span data-stu-id="daaa0-171">Type</span></span>|<span data-ttu-id="daaa0-172">Notes</span><span class="sxs-lookup"><span data-stu-id="daaa0-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="daaa0-173">startTime</span><span class="sxs-lookup"><span data-stu-id="daaa0-173">startTime</span></span>|<span data-ttu-id="daaa0-174">DateTime</span><span class="sxs-lookup"><span data-stu-id="daaa0-174">DateTime</span></span>|<span data-ttu-id="daaa0-175">The time at which the task started running.</span><span class="sxs-lookup"><span data-stu-id="daaa0-175">The time at which the task started running.</span></span> <span data-ttu-id="daaa0-176">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span><span class="sxs-lookup"><span data-stu-id="daaa0-176">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="daaa0-177">If the task has been restarted or retried, this is the most recent time at which the task started running.</span><span class="sxs-lookup"><span data-stu-id="daaa0-177">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="daaa0-178">endTime</span><span class="sxs-lookup"><span data-stu-id="daaa0-178">endTime</span></span>|<span data-ttu-id="daaa0-179">DateTime</span><span class="sxs-lookup"><span data-stu-id="daaa0-179">DateTime</span></span>|<span data-ttu-id="daaa0-180">The time at which the task completed.</span><span class="sxs-lookup"><span data-stu-id="daaa0-180">The time at which the task completed.</span></span>|
|<span data-ttu-id="daaa0-181">exitCode</span><span class="sxs-lookup"><span data-stu-id="daaa0-181">exitCode</span></span>|<span data-ttu-id="daaa0-182">Int32</span><span class="sxs-lookup"><span data-stu-id="daaa0-182">Int32</span></span>|<span data-ttu-id="daaa0-183">The exit code of the task.</span><span class="sxs-lookup"><span data-stu-id="daaa0-183">The exit code of the task.</span></span>|
|<span data-ttu-id="daaa0-184">retryCount</span><span class="sxs-lookup"><span data-stu-id="daaa0-184">retryCount</span></span>|<span data-ttu-id="daaa0-185">Int32</span><span class="sxs-lookup"><span data-stu-id="daaa0-185">Int32</span></span>|<span data-ttu-id="daaa0-186">The number of times the task has been retried by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="daaa0-186">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="daaa0-187">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span><span class="sxs-lookup"><span data-stu-id="daaa0-187">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="daaa0-188">requeueCount</span><span class="sxs-lookup"><span data-stu-id="daaa0-188">requeueCount</span></span>|<span data-ttu-id="daaa0-189">Int32</span><span class="sxs-lookup"><span data-stu-id="daaa0-189">Int32</span></span>|<span data-ttu-id="daaa0-190">The number of times the task has been requeued by the Batch service as the result of a user request.</span><span class="sxs-lookup"><span data-stu-id="daaa0-190">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="daaa0-191">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span><span class="sxs-lookup"><span data-stu-id="daaa0-191">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="daaa0-192">This count tracks how many times the task has been requeued for these reasons.</span><span class="sxs-lookup"><span data-stu-id="daaa0-192">This count tracks how many times the task has been requeued for these reasons.</span></span>|
