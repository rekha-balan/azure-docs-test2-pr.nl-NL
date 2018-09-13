---
title: Scheduler concepts, terms, and entities | Microsoft Docs
description: Azure Scheduler concepts, terminology, and entity hierarchy, including jobs and job collections.  Shows a comprehensive example of a scheduled job.
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: ''
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550496"
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="3565d-104">Scheduler concepts, terminology, + entity hierarchy</span><span class="sxs-lookup"><span data-stu-id="3565d-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="3565d-105">Scheduler entity hierarchy</span><span class="sxs-lookup"><span data-stu-id="3565d-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="3565d-106">The following table describes the main resources exposed or used by the Scheduler API:</span><span class="sxs-lookup"><span data-stu-id="3565d-106">The following table describes the main resources exposed or used by the Scheduler API:</span></span>

| <span data-ttu-id="3565d-107">Resource</span><span class="sxs-lookup"><span data-stu-id="3565d-107">Resource</span></span> | <span data-ttu-id="3565d-108">Description</span><span class="sxs-lookup"><span data-stu-id="3565d-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3565d-109">**Job collection**</span><span class="sxs-lookup"><span data-stu-id="3565d-109">**Job collection**</span></span> |<span data-ttu-id="3565d-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span><span class="sxs-lookup"><span data-stu-id="3565d-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span></span> <span data-ttu-id="3565d-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span><span class="sxs-lookup"><span data-stu-id="3565d-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="3565d-112">It’s constrained to one region.</span><span class="sxs-lookup"><span data-stu-id="3565d-112">It’s constrained to one region.</span></span> <span data-ttu-id="3565d-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span><span class="sxs-lookup"><span data-stu-id="3565d-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span></span> <span data-ttu-id="3565d-114">The quotas include MaxJobs and MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="3565d-114">The quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="3565d-115">**Job**</span><span class="sxs-lookup"><span data-stu-id="3565d-115">**Job**</span></span> |<span data-ttu-id="3565d-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span><span class="sxs-lookup"><span data-stu-id="3565d-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="3565d-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span><span class="sxs-lookup"><span data-stu-id="3565d-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="3565d-118">**Job history**</span><span class="sxs-lookup"><span data-stu-id="3565d-118">**Job history**</span></span> |<span data-ttu-id="3565d-119">A job history represents details for an execution of a job.</span><span class="sxs-lookup"><span data-stu-id="3565d-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="3565d-120">It contains success vs. failure, as well as any response details.</span><span class="sxs-lookup"><span data-stu-id="3565d-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="3565d-121">Scheduler entity management</span><span class="sxs-lookup"><span data-stu-id="3565d-121">Scheduler entity management</span></span>
<span data-ttu-id="3565d-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span><span class="sxs-lookup"><span data-stu-id="3565d-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span></span>

| <span data-ttu-id="3565d-123">Capability</span><span class="sxs-lookup"><span data-stu-id="3565d-123">Capability</span></span> | <span data-ttu-id="3565d-124">Description and URI address</span><span class="sxs-lookup"><span data-stu-id="3565d-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="3565d-125">**Job collection management**</span><span class="sxs-lookup"><span data-stu-id="3565d-125">**Job collection management**</span></span> |<span data-ttu-id="3565d-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span><span class="sxs-lookup"><span data-stu-id="3565d-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span></span> <span data-ttu-id="3565d-127">A job collection is a container for jobs and maps to quotas and shared settings.</span><span class="sxs-lookup"><span data-stu-id="3565d-127">A job collection is a container for jobs and maps to quotas and shared settings.</span></span> <span data-ttu-id="3565d-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span><span class="sxs-lookup"><span data-stu-id="3565d-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="3565d-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="3565d-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="3565d-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="3565d-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="3565d-131">**Job management**</span><span class="sxs-lookup"><span data-stu-id="3565d-131">**Job management**</span></span> |<span data-ttu-id="3565d-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span><span class="sxs-lookup"><span data-stu-id="3565d-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="3565d-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span><span class="sxs-lookup"><span data-stu-id="3565d-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="3565d-134">**Job history management**</span><span class="sxs-lookup"><span data-stu-id="3565d-134">**Job history management**</span></span> |<span data-ttu-id="3565d-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span><span class="sxs-lookup"><span data-stu-id="3565d-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="3565d-136">Adds query string parameter support for filtering based on state and status.</span><span class="sxs-lookup"><span data-stu-id="3565d-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="3565d-137">Job types</span><span class="sxs-lookup"><span data-stu-id="3565d-137">Job types</span></span>
<span data-ttu-id="3565d-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span><span class="sxs-lookup"><span data-stu-id="3565d-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="3565d-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span><span class="sxs-lookup"><span data-stu-id="3565d-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="3565d-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span><span class="sxs-lookup"><span data-stu-id="3565d-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="3565d-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span><span class="sxs-lookup"><span data-stu-id="3565d-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="the-job-entity-in-detail"></a><span data-ttu-id="3565d-142">The "job" entity in detail</span><span class="sxs-lookup"><span data-stu-id="3565d-142">The "job" entity in detail</span></span>
<span data-ttu-id="3565d-143">At a basic level, a scheduled job has several parts:</span><span class="sxs-lookup"><span data-stu-id="3565d-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="3565d-144">The action to perform when the job timer fires</span><span class="sxs-lookup"><span data-stu-id="3565d-144">The action to perform when the job timer fires</span></span>  
* <span data-ttu-id="3565d-145">(Optional) The time to run the job</span><span class="sxs-lookup"><span data-stu-id="3565d-145">(Optional) The time to run the job</span></span>  
* <span data-ttu-id="3565d-146">(Optional) When and how often to repeat the job</span><span class="sxs-lookup"><span data-stu-id="3565d-146">(Optional) When and how often to repeat the job</span></span>  
* <span data-ttu-id="3565d-147">(Optional) An action to fire if the primary action fails</span><span class="sxs-lookup"><span data-stu-id="3565d-147">(Optional) An action to fire if the primary action fails</span></span>  

<span data-ttu-id="3565d-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span><span class="sxs-lookup"><span data-stu-id="3565d-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span></span>

<span data-ttu-id="3565d-149">The following code provides a comprehensive example of a scheduled job.</span><span class="sxs-lookup"><span data-stu-id="3565d-149">The following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="3565d-150">Details are provided in subsequent sections.</span><span class="sxs-lookup"><span data-stu-id="3565d-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="3565d-151">As seen in the sample scheduled job above, a job definition has several parts:</span><span class="sxs-lookup"><span data-stu-id="3565d-151">As seen in the sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="3565d-152">Start time (“startTime”)</span><span class="sxs-lookup"><span data-stu-id="3565d-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="3565d-153">Action (“action”), which includes error action (“errorAction”)</span><span class="sxs-lookup"><span data-stu-id="3565d-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="3565d-154">Recurrence (“recurrence”)</span><span class="sxs-lookup"><span data-stu-id="3565d-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="3565d-155">State (“state”)</span><span class="sxs-lookup"><span data-stu-id="3565d-155">State (“state”)</span></span>  
* <span data-ttu-id="3565d-156">Status (“status”)</span><span class="sxs-lookup"><span data-stu-id="3565d-156">Status (“status”)</span></span>  
* <span data-ttu-id="3565d-157">Retry policy (“retryPolicy”)</span><span class="sxs-lookup"><span data-stu-id="3565d-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="3565d-158">Let’s examine each of these in detail:</span><span class="sxs-lookup"><span data-stu-id="3565d-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="3565d-159">startTime</span><span class="sxs-lookup"><span data-stu-id="3565d-159">startTime</span></span>
<span data-ttu-id="3565d-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="3565d-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="3565d-161">action and errorAction</span><span class="sxs-lookup"><span data-stu-id="3565d-161">action and errorAction</span></span>
<span data-ttu-id="3565d-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span><span class="sxs-lookup"><span data-stu-id="3565d-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="3565d-163">The action is what will be executed on the provided schedule.</span><span class="sxs-lookup"><span data-stu-id="3565d-163">The action is what will be executed on the provided schedule.</span></span> <span data-ttu-id="3565d-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span><span class="sxs-lookup"><span data-stu-id="3565d-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="3565d-165">The action in the example above is an HTTP action.</span><span class="sxs-lookup"><span data-stu-id="3565d-165">The action in the example above is an HTTP action.</span></span> <span data-ttu-id="3565d-166">Below is an example of a storage queue action:</span><span class="sxs-lookup"><span data-stu-id="3565d-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="3565d-167">Below is an example of a service bus topic action.</span><span class="sxs-lookup"><span data-stu-id="3565d-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="3565d-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="3565d-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="3565d-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="3565d-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="3565d-170">Below is an example of a service bus queue action:</span><span class="sxs-lookup"><span data-stu-id="3565d-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="3565d-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="3565d-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="3565d-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="3565d-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="3565d-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="3565d-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="3565d-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="3565d-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="3565d-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span><span class="sxs-lookup"><span data-stu-id="3565d-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span></span> <span data-ttu-id="3565d-176">You can use this variable to call an error-handling endpoint or send a user notification.</span><span class="sxs-lookup"><span data-stu-id="3565d-176">You can use this variable to call an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="3565d-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span><span class="sxs-lookup"><span data-stu-id="3565d-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="3565d-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span><span class="sxs-lookup"><span data-stu-id="3565d-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="3565d-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="3565d-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="3565d-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="3565d-180">recurrence</span></span>
<span data-ttu-id="3565d-181">Recurrence has several parts:</span><span class="sxs-lookup"><span data-stu-id="3565d-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="3565d-182">Frequency: One of minute, hour, day, week, month, year</span><span class="sxs-lookup"><span data-stu-id="3565d-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="3565d-183">Interval: Interval at the given frequency for the recurrence</span><span class="sxs-lookup"><span data-stu-id="3565d-183">Interval: Interval at the given frequency for the recurrence</span></span>  
* <span data-ttu-id="3565d-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span><span class="sxs-lookup"><span data-stu-id="3565d-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span></span>  
* <span data-ttu-id="3565d-185">Count: Count of occurrences</span><span class="sxs-lookup"><span data-stu-id="3565d-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="3565d-186">End time: No jobs will execute after the specified end time</span><span class="sxs-lookup"><span data-stu-id="3565d-186">End time: No jobs will execute after the specified end time</span></span>  

<span data-ttu-id="3565d-187">A job is recurring if it has a recurring object specified in its JSON definition.</span><span class="sxs-lookup"><span data-stu-id="3565d-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="3565d-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span><span class="sxs-lookup"><span data-stu-id="3565d-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="3565d-189">state</span><span class="sxs-lookup"><span data-stu-id="3565d-189">state</span></span>
<span data-ttu-id="3565d-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span><span class="sxs-lookup"><span data-stu-id="3565d-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="3565d-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span><span class="sxs-lookup"><span data-stu-id="3565d-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span></span> <span data-ttu-id="3565d-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span><span class="sxs-lookup"><span data-stu-id="3565d-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span></span> <span data-ttu-id="3565d-193">An example of the state property is as follows:</span><span class="sxs-lookup"><span data-stu-id="3565d-193">An example of the state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="3565d-194">Completed and faulted jobs are deleted after 60 days.</span><span class="sxs-lookup"><span data-stu-id="3565d-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="3565d-195">status</span><span class="sxs-lookup"><span data-stu-id="3565d-195">status</span></span>
<span data-ttu-id="3565d-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span><span class="sxs-lookup"><span data-stu-id="3565d-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span></span> <span data-ttu-id="3565d-197">This object is not settable by the user—it’s set by the system.</span><span class="sxs-lookup"><span data-stu-id="3565d-197">This object is not settable by the user—it’s set by the system.</span></span> <span data-ttu-id="3565d-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span><span class="sxs-lookup"><span data-stu-id="3565d-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span></span>

<span data-ttu-id="3565d-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span><span class="sxs-lookup"><span data-stu-id="3565d-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="3565d-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="3565d-200">retryPolicy</span></span>
<span data-ttu-id="3565d-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span><span class="sxs-lookup"><span data-stu-id="3565d-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span></span> <span data-ttu-id="3565d-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span><span class="sxs-lookup"><span data-stu-id="3565d-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="3565d-203">Set it to **fixed** if there is a retry policy.</span><span class="sxs-lookup"><span data-stu-id="3565d-203">Set it to **fixed** if there is a retry policy.</span></span>

<span data-ttu-id="3565d-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="3565d-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span></span>

<span data-ttu-id="3565d-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span><span class="sxs-lookup"><span data-stu-id="3565d-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span></span> <span data-ttu-id="3565d-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span><span class="sxs-lookup"><span data-stu-id="3565d-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="3565d-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span><span class="sxs-lookup"><span data-stu-id="3565d-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="3565d-208">It is defined in the ISO 8601 format.</span><span class="sxs-lookup"><span data-stu-id="3565d-208">It is defined in the ISO 8601 format.</span></span> <span data-ttu-id="3565d-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span><span class="sxs-lookup"><span data-stu-id="3565d-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span></span> <span data-ttu-id="3565d-210">Its default value is 4, and its maximum value is 20\.</span><span class="sxs-lookup"><span data-stu-id="3565d-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="3565d-211">Both **retryInterval** and **retryCount** are optional.</span><span class="sxs-lookup"><span data-stu-id="3565d-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="3565d-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span><span class="sxs-lookup"><span data-stu-id="3565d-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="3565d-213">See also</span><span class="sxs-lookup"><span data-stu-id="3565d-213">See also</span></span>
 [<span data-ttu-id="3565d-214">What is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="3565d-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="3565d-215">Get started using Scheduler in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3565d-215">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="3565d-216">Plans and billing in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="3565d-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="3565d-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="3565d-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="3565d-218">Azure Scheduler REST API reference</span><span class="sxs-lookup"><span data-stu-id="3565d-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="3565d-219">Azure Scheduler PowerShell cmdlets reference</span><span class="sxs-lookup"><span data-stu-id="3565d-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="3565d-220">Azure Scheduler high-availability and reliability</span><span class="sxs-lookup"><span data-stu-id="3565d-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="3565d-221">Azure Scheduler limits, defaults, and error codes</span><span class="sxs-lookup"><span data-stu-id="3565d-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="3565d-222">Azure Scheduler outbound authentication</span><span class="sxs-lookup"><span data-stu-id="3565d-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

