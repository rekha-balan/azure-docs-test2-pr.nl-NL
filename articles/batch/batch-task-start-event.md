---
title: Task start event - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 95f7762a-a715-4c83-907b-8aed004e69b1
caps.latest.revision: 3
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: 15825628e8eea6f6582e89532650de5470498664
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563696"
---
# <a name="task-start-event"></a><span data-ttu-id="c6b27-102">Task start event</span><span class="sxs-lookup"><span data-stu-id="c6b27-102">Task start event</span></span>

 <span data-ttu-id="c6b27-103">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span><span class="sxs-lookup"><span data-stu-id="c6b27-103">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="c6b27-104">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span><span class="sxs-lookup"><span data-stu-id="c6b27-104">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="c6b27-105">The following example shows the body of a task start event.</span><span class="sxs-lookup"><span data-stu-id="c6b27-105">The following example shows the body of a task start event.</span></span>

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

|<span data-ttu-id="c6b27-106">Element name</span><span class="sxs-lookup"><span data-stu-id="c6b27-106">Element name</span></span>|<span data-ttu-id="c6b27-107">Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-107">Type</span></span>|<span data-ttu-id="c6b27-108">Notes</span><span class="sxs-lookup"><span data-stu-id="c6b27-108">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c6b27-109">jobId</span><span class="sxs-lookup"><span data-stu-id="c6b27-109">jobId</span></span>|<span data-ttu-id="c6b27-110">String</span><span class="sxs-lookup"><span data-stu-id="c6b27-110">String</span></span>|<span data-ttu-id="c6b27-111">The id of the job containing the task.</span><span class="sxs-lookup"><span data-stu-id="c6b27-111">The id of the job containing the task.</span></span>|
|<span data-ttu-id="c6b27-112">id</span><span class="sxs-lookup"><span data-stu-id="c6b27-112">id</span></span>|<span data-ttu-id="c6b27-113">String</span><span class="sxs-lookup"><span data-stu-id="c6b27-113">String</span></span>|<span data-ttu-id="c6b27-114">The id of the task.</span><span class="sxs-lookup"><span data-stu-id="c6b27-114">The id of the task.</span></span>|
|<span data-ttu-id="c6b27-115">taskType</span><span class="sxs-lookup"><span data-stu-id="c6b27-115">taskType</span></span>|<span data-ttu-id="c6b27-116">String</span><span class="sxs-lookup"><span data-stu-id="c6b27-116">String</span></span>|<span data-ttu-id="c6b27-117">The type of the task.</span><span class="sxs-lookup"><span data-stu-id="c6b27-117">The type of the task.</span></span> <span data-ttu-id="c6b27-118">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span><span class="sxs-lookup"><span data-stu-id="c6b27-118">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="c6b27-119">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="c6b27-119">systemTaskVersion</span></span>|<span data-ttu-id="c6b27-120">Int32</span><span class="sxs-lookup"><span data-stu-id="c6b27-120">Int32</span></span>|<span data-ttu-id="c6b27-121">This is the internal retry counter on a task.</span><span class="sxs-lookup"><span data-stu-id="c6b27-121">This is the internal retry counter on a task.</span></span> <span data-ttu-id="c6b27-122">Internally the Batch service can retry a task to account for transient issues.</span><span class="sxs-lookup"><span data-stu-id="c6b27-122">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="c6b27-123">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span><span class="sxs-lookup"><span data-stu-id="c6b27-123">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="c6b27-124">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="c6b27-124">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="c6b27-125">Complex Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-125">Complex Type</span></span>|<span data-ttu-id="c6b27-126">Contains information about the compute node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="c6b27-126">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="c6b27-127">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="c6b27-127">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="c6b27-128">Complex Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-128">Complex Type</span></span>|<span data-ttu-id="c6b27-129">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span><span class="sxs-lookup"><span data-stu-id="c6b27-129">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="c6b27-130">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span><span class="sxs-lookup"><span data-stu-id="c6b27-130">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="c6b27-131">constraints</span><span class="sxs-lookup"><span data-stu-id="c6b27-131">constraints</span></span>](#constraints)|<span data-ttu-id="c6b27-132">Complex Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-132">Complex Type</span></span>|<span data-ttu-id="c6b27-133">The execution constraints that apply to this task.</span><span class="sxs-lookup"><span data-stu-id="c6b27-133">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="c6b27-134">executionInfo</span><span class="sxs-lookup"><span data-stu-id="c6b27-134">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="c6b27-135">Complex Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-135">Complex Type</span></span>|<span data-ttu-id="c6b27-136">Contains information about the execution of the task.</span><span class="sxs-lookup"><span data-stu-id="c6b27-136">Contains information about the execution of the task.</span></span>|

###  <a name="nodeInfo"></a> <span data-ttu-id="c6b27-137">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="c6b27-137">nodeInfo</span></span>

|<span data-ttu-id="c6b27-138">Element name</span><span class="sxs-lookup"><span data-stu-id="c6b27-138">Element name</span></span>|<span data-ttu-id="c6b27-139">Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-139">Type</span></span>|<span data-ttu-id="c6b27-140">Notes</span><span class="sxs-lookup"><span data-stu-id="c6b27-140">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c6b27-141">poolId</span><span class="sxs-lookup"><span data-stu-id="c6b27-141">poolId</span></span>|<span data-ttu-id="c6b27-142">String</span><span class="sxs-lookup"><span data-stu-id="c6b27-142">String</span></span>|<span data-ttu-id="c6b27-143">The id of the pool on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="c6b27-143">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="c6b27-144">nodeId</span><span class="sxs-lookup"><span data-stu-id="c6b27-144">nodeId</span></span>|<span data-ttu-id="c6b27-145">String</span><span class="sxs-lookup"><span data-stu-id="c6b27-145">String</span></span>|<span data-ttu-id="c6b27-146">The id of the node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="c6b27-146">The id of the node on which the task ran.</span></span>|

###  <a name="multiInstanceSettings"></a> <span data-ttu-id="c6b27-147">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="c6b27-147">multiInstanceSettings</span></span>

|<span data-ttu-id="c6b27-148">Element name</span><span class="sxs-lookup"><span data-stu-id="c6b27-148">Element name</span></span>|<span data-ttu-id="c6b27-149">Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-149">Type</span></span>|<span data-ttu-id="c6b27-150">Notes</span><span class="sxs-lookup"><span data-stu-id="c6b27-150">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c6b27-151">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="c6b27-151">numberOfInstances</span></span>|<span data-ttu-id="c6b27-152">Int</span><span class="sxs-lookup"><span data-stu-id="c6b27-152">Int</span></span>|<span data-ttu-id="c6b27-153">The number of compute nodes required by the task.</span><span class="sxs-lookup"><span data-stu-id="c6b27-153">The number of compute nodes required by the task.</span></span>|

###  <a name="constraints"></a> <span data-ttu-id="c6b27-154">constraints</span><span class="sxs-lookup"><span data-stu-id="c6b27-154">constraints</span></span>

|<span data-ttu-id="c6b27-155">Element name</span><span class="sxs-lookup"><span data-stu-id="c6b27-155">Element name</span></span>|<span data-ttu-id="c6b27-156">Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-156">Type</span></span>|<span data-ttu-id="c6b27-157">Notes</span><span class="sxs-lookup"><span data-stu-id="c6b27-157">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c6b27-158">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="c6b27-158">maxTaskRetryCount</span></span>|<span data-ttu-id="c6b27-159">Int32</span><span class="sxs-lookup"><span data-stu-id="c6b27-159">Int32</span></span>|<span data-ttu-id="c6b27-160">The maximum number of times the task may be retried.</span><span class="sxs-lookup"><span data-stu-id="c6b27-160">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="c6b27-161">The Batch service retries a task if its exit code is nonzero.</span><span class="sxs-lookup"><span data-stu-id="c6b27-161">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="c6b27-162">Note that this value specifically controls the number of retries.</span><span class="sxs-lookup"><span data-stu-id="c6b27-162">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="c6b27-163">The Batch service will try the task once, and may then retry up to this limit.</span><span class="sxs-lookup"><span data-stu-id="c6b27-163">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="c6b27-164">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span><span class="sxs-lookup"><span data-stu-id="c6b27-164">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="c6b27-165">If the maximum retry count is 0, the Batch service does not retry tasks.</span><span class="sxs-lookup"><span data-stu-id="c6b27-165">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="c6b27-166">If the maximum retry count is -1, the Batch service retries tasks without limit.</span><span class="sxs-lookup"><span data-stu-id="c6b27-166">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="c6b27-167">The default value is 0 (no retries).</span><span class="sxs-lookup"><span data-stu-id="c6b27-167">The default value is 0 (no retries).</span></span>|

###  <a name="executionInfo"></a> <span data-ttu-id="c6b27-168">executionInfo</span><span class="sxs-lookup"><span data-stu-id="c6b27-168">executionInfo</span></span>

|<span data-ttu-id="c6b27-169">Element name</span><span class="sxs-lookup"><span data-stu-id="c6b27-169">Element name</span></span>|<span data-ttu-id="c6b27-170">Type</span><span class="sxs-lookup"><span data-stu-id="c6b27-170">Type</span></span>|<span data-ttu-id="c6b27-171">Notes</span><span class="sxs-lookup"><span data-stu-id="c6b27-171">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="c6b27-172">retryCount</span><span class="sxs-lookup"><span data-stu-id="c6b27-172">retryCount</span></span>|<span data-ttu-id="c6b27-173">Int32</span><span class="sxs-lookup"><span data-stu-id="c6b27-173">Int32</span></span>|<span data-ttu-id="c6b27-174">The number of times the task has been retried by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="c6b27-174">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="c6b27-175">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="c6b27-175">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
