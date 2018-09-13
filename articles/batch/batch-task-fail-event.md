---
title: Task fail event - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 8c16a533-1ac7-4b65-a84e-8eafb937b3d7
caps.latest.revision: 3
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: fe1c10daea92713beb9d309536172448935476d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553114"
---
# <a name="task-fail-event"></a><span data-ttu-id="9b591-102">Task fail event</span><span class="sxs-lookup"><span data-stu-id="9b591-102">Task fail event</span></span>

 <span data-ttu-id="9b591-103">This event is emitted when a task completes with a failure.</span><span class="sxs-lookup"><span data-stu-id="9b591-103">This event is emitted when a task completes with a failure.</span></span> <span data-ttu-id="9b591-104">Currently all nonzero exit codes are considered failures.</span><span class="sxs-lookup"><span data-stu-id="9b591-104">Currently all nonzero exit codes are considered failures.</span></span> <span data-ttu-id="9b591-105">This event will be emitted *in addition to* a task complete event and can be used to detect when a task has failed.</span><span class="sxs-lookup"><span data-stu-id="9b591-105">This event will be emitted *in addition to* a task complete event and can be used to detect when a task has failed.</span></span>


 <span data-ttu-id="9b591-106">The following example shows the body of a task fail event.</span><span class="sxs-lookup"><span data-stu-id="9b591-106">The following example shows the body of a task fail event.</span></span>

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
        "exitCode": 1,
        "retryCount": 2,
        "requeueCount": 0
    }
}
```

|<span data-ttu-id="9b591-107">Element name</span><span class="sxs-lookup"><span data-stu-id="9b591-107">Element name</span></span>|<span data-ttu-id="9b591-108">Type</span><span class="sxs-lookup"><span data-stu-id="9b591-108">Type</span></span>|<span data-ttu-id="9b591-109">Notes</span><span class="sxs-lookup"><span data-stu-id="9b591-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9b591-110">jobId</span><span class="sxs-lookup"><span data-stu-id="9b591-110">jobId</span></span>|<span data-ttu-id="9b591-111">String</span><span class="sxs-lookup"><span data-stu-id="9b591-111">String</span></span>|<span data-ttu-id="9b591-112">The id of the job containing the task.</span><span class="sxs-lookup"><span data-stu-id="9b591-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="9b591-113">id</span><span class="sxs-lookup"><span data-stu-id="9b591-113">id</span></span>|<span data-ttu-id="9b591-114">String</span><span class="sxs-lookup"><span data-stu-id="9b591-114">String</span></span>|<span data-ttu-id="9b591-115">The id of the task.</span><span class="sxs-lookup"><span data-stu-id="9b591-115">The id of the task.</span></span>|
|<span data-ttu-id="9b591-116">taskType</span><span class="sxs-lookup"><span data-stu-id="9b591-116">taskType</span></span>|<span data-ttu-id="9b591-117">String</span><span class="sxs-lookup"><span data-stu-id="9b591-117">String</span></span>|<span data-ttu-id="9b591-118">The type of the task.</span><span class="sxs-lookup"><span data-stu-id="9b591-118">The type of the task.</span></span> <span data-ttu-id="9b591-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span><span class="sxs-lookup"><span data-stu-id="9b591-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span> <span data-ttu-id="9b591-120">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span><span class="sxs-lookup"><span data-stu-id="9b591-120">This event is not emitted for job preparation tasks, job release tasks or start tasks.</span></span>|
|<span data-ttu-id="9b591-121">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="9b591-121">systemTaskVersion</span></span>|<span data-ttu-id="9b591-122">Int32</span><span class="sxs-lookup"><span data-stu-id="9b591-122">Int32</span></span>|<span data-ttu-id="9b591-123">This is the internal retry counter on a task.</span><span class="sxs-lookup"><span data-stu-id="9b591-123">This is the internal retry counter on a task.</span></span> <span data-ttu-id="9b591-124">Internally the Batch service can retry a task to account for transient issues.</span><span class="sxs-lookup"><span data-stu-id="9b591-124">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="9b591-125">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span><span class="sxs-lookup"><span data-stu-id="9b591-125">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="9b591-126">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="9b591-126">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="9b591-127">Complex Type</span><span class="sxs-lookup"><span data-stu-id="9b591-127">Complex Type</span></span>|<span data-ttu-id="9b591-128">Contains information about the compute node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="9b591-128">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="9b591-129">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="9b591-129">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="9b591-130">Complex Type</span><span class="sxs-lookup"><span data-stu-id="9b591-130">Complex Type</span></span>|<span data-ttu-id="9b591-131">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span><span class="sxs-lookup"><span data-stu-id="9b591-131">Specifies that the task is a Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="9b591-132">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span><span class="sxs-lookup"><span data-stu-id="9b591-132">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="9b591-133">constraints</span><span class="sxs-lookup"><span data-stu-id="9b591-133">constraints</span></span>](#constraints)|<span data-ttu-id="9b591-134">Complex Type</span><span class="sxs-lookup"><span data-stu-id="9b591-134">Complex Type</span></span>|<span data-ttu-id="9b591-135">The execution constraints that apply to this task.</span><span class="sxs-lookup"><span data-stu-id="9b591-135">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="9b591-136">executionInfo</span><span class="sxs-lookup"><span data-stu-id="9b591-136">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="9b591-137">Complex Type</span><span class="sxs-lookup"><span data-stu-id="9b591-137">Complex Type</span></span>|<span data-ttu-id="9b591-138">Contains information about the execution of the task.</span><span class="sxs-lookup"><span data-stu-id="9b591-138">Contains information about the execution of the task.</span></span>|

###  <a name="nodeInfo"></a> <span data-ttu-id="9b591-139">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="9b591-139">nodeInfo</span></span>

|<span data-ttu-id="9b591-140">Element name</span><span class="sxs-lookup"><span data-stu-id="9b591-140">Element name</span></span>|<span data-ttu-id="9b591-141">Type</span><span class="sxs-lookup"><span data-stu-id="9b591-141">Type</span></span>|<span data-ttu-id="9b591-142">Notes</span><span class="sxs-lookup"><span data-stu-id="9b591-142">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9b591-143">poolId</span><span class="sxs-lookup"><span data-stu-id="9b591-143">poolId</span></span>|<span data-ttu-id="9b591-144">String</span><span class="sxs-lookup"><span data-stu-id="9b591-144">String</span></span>|<span data-ttu-id="9b591-145">The id of the pool on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="9b591-145">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="9b591-146">nodeId</span><span class="sxs-lookup"><span data-stu-id="9b591-146">nodeId</span></span>|<span data-ttu-id="9b591-147">String</span><span class="sxs-lookup"><span data-stu-id="9b591-147">String</span></span>|<span data-ttu-id="9b591-148">The id of the node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="9b591-148">The id of the node on which the task ran.</span></span>|

###  <a name="multiInstanceSettings"></a> <span data-ttu-id="9b591-149">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="9b591-149">multiInstanceSettings</span></span>

|<span data-ttu-id="9b591-150">Element name</span><span class="sxs-lookup"><span data-stu-id="9b591-150">Element name</span></span>|<span data-ttu-id="9b591-151">Type</span><span class="sxs-lookup"><span data-stu-id="9b591-151">Type</span></span>|<span data-ttu-id="9b591-152">Notes</span><span class="sxs-lookup"><span data-stu-id="9b591-152">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9b591-153">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="9b591-153">numberOfInstances</span></span>|<span data-ttu-id="9b591-154">Int32</span><span class="sxs-lookup"><span data-stu-id="9b591-154">Int32</span></span>|<span data-ttu-id="9b591-155">The number of compute nodes required by the task.</span><span class="sxs-lookup"><span data-stu-id="9b591-155">The number of compute nodes required by the task.</span></span>|

###  <a name="constraints"></a> <span data-ttu-id="9b591-156">constraints</span><span class="sxs-lookup"><span data-stu-id="9b591-156">constraints</span></span>

|<span data-ttu-id="9b591-157">Element name</span><span class="sxs-lookup"><span data-stu-id="9b591-157">Element name</span></span>|<span data-ttu-id="9b591-158">Type</span><span class="sxs-lookup"><span data-stu-id="9b591-158">Type</span></span>|<span data-ttu-id="9b591-159">Notes</span><span class="sxs-lookup"><span data-stu-id="9b591-159">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9b591-160">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="9b591-160">maxTaskRetryCount</span></span>|<span data-ttu-id="9b591-161">Int32</span><span class="sxs-lookup"><span data-stu-id="9b591-161">Int32</span></span>|<span data-ttu-id="9b591-162">The maximum number of times the task may be retried.</span><span class="sxs-lookup"><span data-stu-id="9b591-162">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="9b591-163">The Batch service retries a task if its exit code is nonzero.</span><span class="sxs-lookup"><span data-stu-id="9b591-163">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="9b591-164">Note that this value specifically controls the number of retries.</span><span class="sxs-lookup"><span data-stu-id="9b591-164">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="9b591-165">The Batch service will try the task once, and may then retry up to this limit.</span><span class="sxs-lookup"><span data-stu-id="9b591-165">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="9b591-166">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span><span class="sxs-lookup"><span data-stu-id="9b591-166">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="9b591-167">If the maximum retry count is 0, the Batch service does not retry tasks.</span><span class="sxs-lookup"><span data-stu-id="9b591-167">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="9b591-168">If the maximum retry count is -1, the Batch service retries tasks without limit.</span><span class="sxs-lookup"><span data-stu-id="9b591-168">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="9b591-169">The default value is 0 (no retries).</span><span class="sxs-lookup"><span data-stu-id="9b591-169">The default value is 0 (no retries).</span></span>|


###  <a name="executionInfo"></a> <span data-ttu-id="9b591-170">executionInfo</span><span class="sxs-lookup"><span data-stu-id="9b591-170">executionInfo</span></span>

|<span data-ttu-id="9b591-171">Element name</span><span class="sxs-lookup"><span data-stu-id="9b591-171">Element name</span></span>|<span data-ttu-id="9b591-172">Type</span><span class="sxs-lookup"><span data-stu-id="9b591-172">Type</span></span>|<span data-ttu-id="9b591-173">Notes</span><span class="sxs-lookup"><span data-stu-id="9b591-173">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9b591-174">startTime</span><span class="sxs-lookup"><span data-stu-id="9b591-174">startTime</span></span>|<span data-ttu-id="9b591-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="9b591-175">DateTime</span></span>|<span data-ttu-id="9b591-176">The time at which the task started running.</span><span class="sxs-lookup"><span data-stu-id="9b591-176">The time at which the task started running.</span></span> <span data-ttu-id="9b591-177">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span><span class="sxs-lookup"><span data-stu-id="9b591-177">'Running' corresponds to the **running** state, so if the task specifies resource files or application packages, then the start time reflects the time at which the task started downloading or deploying these.</span></span>  <span data-ttu-id="9b591-178">If the task has been restarted or retried, this is the most recent time at which the task started running.</span><span class="sxs-lookup"><span data-stu-id="9b591-178">If the task has been restarted or retried, this is the most recent time at which the task started running.</span></span>|
|<span data-ttu-id="9b591-179">endTime</span><span class="sxs-lookup"><span data-stu-id="9b591-179">endTime</span></span>|<span data-ttu-id="9b591-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="9b591-180">DateTime</span></span>|<span data-ttu-id="9b591-181">The time at which the task completed.</span><span class="sxs-lookup"><span data-stu-id="9b591-181">The time at which the task completed.</span></span>|
|<span data-ttu-id="9b591-182">exitCode</span><span class="sxs-lookup"><span data-stu-id="9b591-182">exitCode</span></span>|<span data-ttu-id="9b591-183">Int32</span><span class="sxs-lookup"><span data-stu-id="9b591-183">Int32</span></span>|<span data-ttu-id="9b591-184">The exit code of the task.</span><span class="sxs-lookup"><span data-stu-id="9b591-184">The exit code of the task.</span></span>|
|<span data-ttu-id="9b591-185">retryCount</span><span class="sxs-lookup"><span data-stu-id="9b591-185">retryCount</span></span>|<span data-ttu-id="9b591-186">Int32</span><span class="sxs-lookup"><span data-stu-id="9b591-186">Int32</span></span>|<span data-ttu-id="9b591-187">The number of times the task has been retried by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="9b591-187">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="9b591-188">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span><span class="sxs-lookup"><span data-stu-id="9b591-188">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount.</span></span>|
|<span data-ttu-id="9b591-189">requeueCount</span><span class="sxs-lookup"><span data-stu-id="9b591-189">requeueCount</span></span>|<span data-ttu-id="9b591-190">Int32</span><span class="sxs-lookup"><span data-stu-id="9b591-190">Int32</span></span>|<span data-ttu-id="9b591-191">The number of times the task has been requeued by the Batch service as the result of a user request.</span><span class="sxs-lookup"><span data-stu-id="9b591-191">The number of times the task has been requeued by the Batch service as the result of a user request.</span></span><br /><br /> <span data-ttu-id="9b591-192">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span><span class="sxs-lookup"><span data-stu-id="9b591-192">When the user removes nodes from a pool (by resizing or shrinking the pool) or when the job is being disabled, the user can specify that running tasks on the nodes be requeued for execution.</span></span> <span data-ttu-id="9b591-193">This count tracks how many times the task has been requeued for these reasons.</span><span class="sxs-lookup"><span data-stu-id="9b591-193">This count tracks how many times the task has been requeued for these reasons.</span></span>|
