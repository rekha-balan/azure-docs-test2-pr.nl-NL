---
title: Azure Event Hubs diagnostic logs | Microsoft Docs
description: Learn how to set up diagnostic logs for event hubs in Azure.
keywords: ''
documentationcenter: ''
services: event-hubs
author: banisadr
manager: ''
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 42c7812091f90dd722095c68598450e3e35c0e78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563323"
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="253ff-103">Event Hubs diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="253ff-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="253ff-104">You can view two types of logs for Azure Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="253ff-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="253ff-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="253ff-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="253ff-106">These logs have information about operations performed on a job.</span><span class="sxs-lookup"><span data-stu-id="253ff-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="253ff-107">The logs are always enabled.</span><span class="sxs-lookup"><span data-stu-id="253ff-107">The logs are always enabled.</span></span>
* <span data-ttu-id="253ff-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="253ff-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="253ff-109">You can configure diagnostic logs, for a richer view into everything that happens with a job.</span><span class="sxs-lookup"><span data-stu-id="253ff-109">You can configure diagnostic logs, for a richer view into everything that happens with a job.</span></span> <span data-ttu-id="253ff-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span><span class="sxs-lookup"><span data-stu-id="253ff-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="253ff-111">Turn on diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="253ff-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="253ff-112">Diagnostics logs are **off** by default.</span><span class="sxs-lookup"><span data-stu-id="253ff-112">Diagnostics logs are **off** by default.</span></span> <span data-ttu-id="253ff-113">To enable diagnostic logs:</span><span class="sxs-lookup"><span data-stu-id="253ff-113">To enable diagnostic logs:</span></span>

1.  <span data-ttu-id="253ff-114">In the Azure portal, go to the streaming job blade.</span><span class="sxs-lookup"><span data-stu-id="253ff-114">In the Azure portal, go to the streaming job blade.</span></span>

2.  <span data-ttu-id="253ff-115">Under **Monitoring**, go to the **Diagnostics logs** blade.</span><span class="sxs-lookup"><span data-stu-id="253ff-115">Under **Monitoring**, go to the **Diagnostics logs** blade.</span></span>

    ![Blade navigation to diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-diagnostic-logs/image1.png)  

3.  <span data-ttu-id="253ff-117">Select **Turn on diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="253ff-117">Select **Turn on diagnostics**.</span></span>

    ![Turn on diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="253ff-119">For **Status**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="253ff-119">For **Status**, select **On**.</span></span>

    ![Change the status of diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="253ff-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="253ff-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="253ff-122">Select the categories of logs that you want to collect; for example, **Execution** or **Authoring**.</span><span class="sxs-lookup"><span data-stu-id="253ff-122">Select the categories of logs that you want to collect; for example, **Execution** or **Authoring**.</span></span>

7.  <span data-ttu-id="253ff-123">Save the new diagnostics settings.</span><span class="sxs-lookup"><span data-stu-id="253ff-123">Save the new diagnostics settings.</span></span>

<span data-ttu-id="253ff-124">New settings take effect in about 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="253ff-124">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="253ff-125">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span><span class="sxs-lookup"><span data-stu-id="253ff-125">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="253ff-126">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="253ff-126">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="253ff-127">Diagnostic logs categories</span><span class="sxs-lookup"><span data-stu-id="253ff-127">Diagnostic logs categories</span></span>
<span data-ttu-id="253ff-128">Event Hubs captures diagnostic logs for two categories:</span><span class="sxs-lookup"><span data-stu-id="253ff-128">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="253ff-129">**ArchivalLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span><span class="sxs-lookup"><span data-stu-id="253ff-129">**ArchivalLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span></span>
* <span data-ttu-id="253ff-130">**OperationalLogs** information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="253ff-130">**OperationalLogs** information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="253ff-131">Diagnostic logs schema</span><span class="sxs-lookup"><span data-stu-id="253ff-131">Diagnostic logs schema</span></span>
<span data-ttu-id="253ff-132">All logs are stored in JavaScript Object Notation (JSON) format.</span><span class="sxs-lookup"><span data-stu-id="253ff-132">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="253ff-133">Each entry has string fields that use the format described in the following examples.</span><span class="sxs-lookup"><span data-stu-id="253ff-133">Each entry has string fields that use the format described in the following examples.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="253ff-134">Archive logs schema</span><span class="sxs-lookup"><span data-stu-id="253ff-134">Archive logs schema</span></span>

<span data-ttu-id="253ff-135">Archive log JSON strings include elements listed in the following table:</span><span class="sxs-lookup"><span data-stu-id="253ff-135">Archive log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="253ff-136">Name</span><span class="sxs-lookup"><span data-stu-id="253ff-136">Name</span></span> | <span data-ttu-id="253ff-137">Description</span><span class="sxs-lookup"><span data-stu-id="253ff-137">Description</span></span>
------- | -------
<span data-ttu-id="253ff-138">TaskName</span><span class="sxs-lookup"><span data-stu-id="253ff-138">TaskName</span></span> | <span data-ttu-id="253ff-139">Description of the task that failed.</span><span class="sxs-lookup"><span data-stu-id="253ff-139">Description of the task that failed.</span></span>
<span data-ttu-id="253ff-140">ActivityId</span><span class="sxs-lookup"><span data-stu-id="253ff-140">ActivityId</span></span> | <span data-ttu-id="253ff-141">Internal ID, used for tracking.</span><span class="sxs-lookup"><span data-stu-id="253ff-141">Internal ID, used for tracking.</span></span>
<span data-ttu-id="253ff-142">trackingId</span><span class="sxs-lookup"><span data-stu-id="253ff-142">trackingId</span></span> | <span data-ttu-id="253ff-143">Internal ID, used for tracking.</span><span class="sxs-lookup"><span data-stu-id="253ff-143">Internal ID, used for tracking.</span></span>
<span data-ttu-id="253ff-144">resourceId</span><span class="sxs-lookup"><span data-stu-id="253ff-144">resourceId</span></span> | <span data-ttu-id="253ff-145">Azure Resource Manager resource ID.</span><span class="sxs-lookup"><span data-stu-id="253ff-145">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="253ff-146">eventHub</span><span class="sxs-lookup"><span data-stu-id="253ff-146">eventHub</span></span> | <span data-ttu-id="253ff-147">Event hub full name (includes namespace name).</span><span class="sxs-lookup"><span data-stu-id="253ff-147">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="253ff-148">partitionId</span><span class="sxs-lookup"><span data-stu-id="253ff-148">partitionId</span></span> | <span data-ttu-id="253ff-149">Event Hub partition being written to.</span><span class="sxs-lookup"><span data-stu-id="253ff-149">Event Hub partition being written to.</span></span>
<span data-ttu-id="253ff-150">archiveStep</span><span class="sxs-lookup"><span data-stu-id="253ff-150">archiveStep</span></span> | <span data-ttu-id="253ff-151">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="253ff-151">ArchiveFlushWriter</span></span>
<span data-ttu-id="253ff-152">startTime</span><span class="sxs-lookup"><span data-stu-id="253ff-152">startTime</span></span> | <span data-ttu-id="253ff-153">Failure start time.</span><span class="sxs-lookup"><span data-stu-id="253ff-153">Failure start time.</span></span>
<span data-ttu-id="253ff-154">failures</span><span class="sxs-lookup"><span data-stu-id="253ff-154">failures</span></span> | <span data-ttu-id="253ff-155">Number of times failure occurred.</span><span class="sxs-lookup"><span data-stu-id="253ff-155">Number of times failure occurred.</span></span>
<span data-ttu-id="253ff-156">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="253ff-156">durationInSeconds</span></span> | <span data-ttu-id="253ff-157">Duration of failure.</span><span class="sxs-lookup"><span data-stu-id="253ff-157">Duration of failure.</span></span>
<span data-ttu-id="253ff-158">message</span><span class="sxs-lookup"><span data-stu-id="253ff-158">message</span></span> | <span data-ttu-id="253ff-159">Error message.</span><span class="sxs-lookup"><span data-stu-id="253ff-159">Error message.</span></span>
<span data-ttu-id="253ff-160">category</span><span class="sxs-lookup"><span data-stu-id="253ff-160">category</span></span> | <span data-ttu-id="253ff-161">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="253ff-161">ArchiveLogs</span></span>

<span data-ttu-id="253ff-162">The following is an example of an archive log JSON string:</span><span class="sxs-lookup"><span data-stu-id="253ff-162">The following is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operation-logs-schema"></a><span data-ttu-id="253ff-163">Operation logs schema</span><span class="sxs-lookup"><span data-stu-id="253ff-163">Operation logs schema</span></span>

<span data-ttu-id="253ff-164">Operation log JSON strings include elements listed in the following table:</span><span class="sxs-lookup"><span data-stu-id="253ff-164">Operation log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="253ff-165">Name</span><span class="sxs-lookup"><span data-stu-id="253ff-165">Name</span></span> | <span data-ttu-id="253ff-166">Description</span><span class="sxs-lookup"><span data-stu-id="253ff-166">Description</span></span>
------- | -------
<span data-ttu-id="253ff-167">ActivityId</span><span class="sxs-lookup"><span data-stu-id="253ff-167">ActivityId</span></span> | <span data-ttu-id="253ff-168">Internal ID, used to track purpose.</span><span class="sxs-lookup"><span data-stu-id="253ff-168">Internal ID, used to track purpose.</span></span>
<span data-ttu-id="253ff-169">EventName</span><span class="sxs-lookup"><span data-stu-id="253ff-169">EventName</span></span> | <span data-ttu-id="253ff-170">Operation name.</span><span class="sxs-lookup"><span data-stu-id="253ff-170">Operation name.</span></span>  
<span data-ttu-id="253ff-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="253ff-171">resourceId</span></span> | <span data-ttu-id="253ff-172">Azure Resource Manager resource ID.</span><span class="sxs-lookup"><span data-stu-id="253ff-172">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="253ff-173">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="253ff-173">SubscriptionId</span></span> | <span data-ttu-id="253ff-174">Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="253ff-174">Subscription ID.</span></span>
<span data-ttu-id="253ff-175">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="253ff-175">EventTimeString</span></span> | <span data-ttu-id="253ff-176">Operation time.</span><span class="sxs-lookup"><span data-stu-id="253ff-176">Operation time.</span></span>
<span data-ttu-id="253ff-177">EventProperties</span><span class="sxs-lookup"><span data-stu-id="253ff-177">EventProperties</span></span> | <span data-ttu-id="253ff-178">Operation properties.</span><span class="sxs-lookup"><span data-stu-id="253ff-178">Operation properties.</span></span>
<span data-ttu-id="253ff-179">Status</span><span class="sxs-lookup"><span data-stu-id="253ff-179">Status</span></span> | <span data-ttu-id="253ff-180">Operation status.</span><span class="sxs-lookup"><span data-stu-id="253ff-180">Operation status.</span></span>
<span data-ttu-id="253ff-181">Caller</span><span class="sxs-lookup"><span data-stu-id="253ff-181">Caller</span></span> | <span data-ttu-id="253ff-182">Caller of operation (Azure portal or management client).</span><span class="sxs-lookup"><span data-stu-id="253ff-182">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="253ff-183">category</span><span class="sxs-lookup"><span data-stu-id="253ff-183">category</span></span> | <span data-ttu-id="253ff-184">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="253ff-184">OperationalLogs</span></span>

<span data-ttu-id="253ff-185">The following is an example of an operation log JSON string:</span><span class="sxs-lookup"><span data-stu-id="253ff-185">The following is an example of an operation log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="253ff-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="253ff-186">Next steps</span></span>
* [<span data-ttu-id="253ff-187">Introduction to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="253ff-187">Introduction to Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="253ff-188">Event Hubs API overview</span><span class="sxs-lookup"><span data-stu-id="253ff-188">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="253ff-189">Get started with Event Hubs</span><span class="sxs-lookup"><span data-stu-id="253ff-189">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)



