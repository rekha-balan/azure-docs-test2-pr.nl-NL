---
title: Azure Service Bus diagnostic logs | Microsoft Docs
description: Learn how to set up diagnostic logs for Service Bus in Azure.
keywords: ''
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/23/2017
ms.author: babanisa;sethm
ms.openlocfilehash: 80b7d3cc16914a4c8b264d93922a82d61dd0ac78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663019"
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="e04f8-103">Service Bus diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="e04f8-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="e04f8-104">You can view two types of logs for Azure Service Bus:</span><span class="sxs-lookup"><span data-stu-id="e04f8-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="e04f8-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="e04f8-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="e04f8-106">These logs contain information about operations performed on a job.</span><span class="sxs-lookup"><span data-stu-id="e04f8-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="e04f8-107">The logs are always enabled.</span><span class="sxs-lookup"><span data-stu-id="e04f8-107">The logs are always enabled.</span></span>
* <span data-ttu-id="e04f8-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="e04f8-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="e04f8-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span><span class="sxs-lookup"><span data-stu-id="e04f8-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="e04f8-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span><span class="sxs-lookup"><span data-stu-id="e04f8-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="e04f8-111">Turn on diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="e04f8-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="e04f8-112">Diagnostics logs are disabled by default.</span><span class="sxs-lookup"><span data-stu-id="e04f8-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="e04f8-113">To enable diagnostic logs, do the following:</span><span class="sxs-lookup"><span data-stu-id="e04f8-113">To enable diagnostic logs, do the following:</span></span>

1.  <span data-ttu-id="e04f8-114">In the [Azure portal](https://portal.azure.com), go to the streaming job blade.</span><span class="sxs-lookup"><span data-stu-id="e04f8-114">In the [Azure portal](https://portal.azure.com), go to the streaming job blade.</span></span>

2.  <span data-ttu-id="e04f8-115">Under **Monitoring**, go to the **Diagnostics logs** blade.</span><span class="sxs-lookup"><span data-stu-id="e04f8-115">Under **Monitoring**, go to the **Diagnostics logs** blade.</span></span>

    ![blade navigation to diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-diagnostic-logs/image1.png)  

3.  <span data-ttu-id="e04f8-117">Click **Turn on diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="e04f8-117">Click **Turn on diagnostics**.</span></span>

    ![turn on diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="e04f8-119">For **Status**, click **On**.</span><span class="sxs-lookup"><span data-stu-id="e04f8-119">For **Status**, click **On**.</span></span>

    ![change status diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="e04f8-121">Set the archival target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e04f8-121">Set the archival target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="e04f8-122">Select the categories of logs that you want to collect; for example, **Execution** or **Authoring**.</span><span class="sxs-lookup"><span data-stu-id="e04f8-122">Select the categories of logs that you want to collect; for example, **Execution** or **Authoring**.</span></span>

7.  <span data-ttu-id="e04f8-123">Save the new diagnostics settings.</span><span class="sxs-lookup"><span data-stu-id="e04f8-123">Save the new diagnostics settings.</span></span>

<span data-ttu-id="e04f8-124">New settings take effect in about 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="e04f8-124">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="e04f8-125">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span><span class="sxs-lookup"><span data-stu-id="e04f8-125">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="e04f8-126">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e04f8-126">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="e04f8-127">Diagnostic logs schema</span><span class="sxs-lookup"><span data-stu-id="e04f8-127">Diagnostic logs schema</span></span>

<span data-ttu-id="e04f8-128">All logs are stored in JavaScript Object Notation (JSON) format.</span><span class="sxs-lookup"><span data-stu-id="e04f8-128">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="e04f8-129">Each entry has string fields that use the format described in the following example.</span><span class="sxs-lookup"><span data-stu-id="e04f8-129">Each entry has string fields that use the format described in the following example.</span></span>

## <a name="operation-logs-example"></a><span data-ttu-id="e04f8-130">Operation logs example</span><span class="sxs-lookup"><span data-stu-id="e04f8-130">Operation logs example</span></span>

<span data-ttu-id="e04f8-131">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span><span class="sxs-lookup"><span data-stu-id="e04f8-131">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="e04f8-132">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="e04f8-132">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span></span>

<span data-ttu-id="e04f8-133">Operation log JSON strings include elements listed in the following table:</span><span class="sxs-lookup"><span data-stu-id="e04f8-133">Operation log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="e04f8-134">Name</span><span class="sxs-lookup"><span data-stu-id="e04f8-134">Name</span></span> | <span data-ttu-id="e04f8-135">Description</span><span class="sxs-lookup"><span data-stu-id="e04f8-135">Description</span></span>
------- | -------
<span data-ttu-id="e04f8-136">ActivityId</span><span class="sxs-lookup"><span data-stu-id="e04f8-136">ActivityId</span></span> | <span data-ttu-id="e04f8-137">Internal ID, used for tracking</span><span class="sxs-lookup"><span data-stu-id="e04f8-137">Internal ID, used for tracking</span></span>
<span data-ttu-id="e04f8-138">EventName</span><span class="sxs-lookup"><span data-stu-id="e04f8-138">EventName</span></span> | <span data-ttu-id="e04f8-139">Operation name</span><span class="sxs-lookup"><span data-stu-id="e04f8-139">Operation name</span></span>           
<span data-ttu-id="e04f8-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="e04f8-140">resourceId</span></span> | <span data-ttu-id="e04f8-141">Azure Resource Manager resource ID</span><span class="sxs-lookup"><span data-stu-id="e04f8-141">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="e04f8-142">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="e04f8-142">SubscriptionId</span></span> | <span data-ttu-id="e04f8-143">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="e04f8-143">Subscription ID</span></span>
<span data-ttu-id="e04f8-144">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="e04f8-144">EventTimeString</span></span> | <span data-ttu-id="e04f8-145">Operation time</span><span class="sxs-lookup"><span data-stu-id="e04f8-145">Operation time</span></span>
<span data-ttu-id="e04f8-146">EventProperties</span><span class="sxs-lookup"><span data-stu-id="e04f8-146">EventProperties</span></span> | <span data-ttu-id="e04f8-147">Operation properties</span><span class="sxs-lookup"><span data-stu-id="e04f8-147">Operation properties</span></span>
<span data-ttu-id="e04f8-148">Status</span><span class="sxs-lookup"><span data-stu-id="e04f8-148">Status</span></span> | <span data-ttu-id="e04f8-149">Operation status</span><span class="sxs-lookup"><span data-stu-id="e04f8-149">Operation status</span></span>
<span data-ttu-id="e04f8-150">Caller</span><span class="sxs-lookup"><span data-stu-id="e04f8-150">Caller</span></span> | <span data-ttu-id="e04f8-151">Caller of operation (Azure portal or management client)</span><span class="sxs-lookup"><span data-stu-id="e04f8-151">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="e04f8-152">category</span><span class="sxs-lookup"><span data-stu-id="e04f8-152">category</span></span> | <span data-ttu-id="e04f8-153">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="e04f8-153">OperationalLogs</span></span>

<span data-ttu-id="e04f8-154">Here's an example of an operation log JSON string:</span><span class="sxs-lookup"><span data-stu-id="e04f8-154">Here's an example of an operation log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create Queue",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="e04f8-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="e04f8-155">Next steps</span></span>
* [<span data-ttu-id="e04f8-156">Introduction to Service Bus</span><span class="sxs-lookup"><span data-stu-id="e04f8-156">Introduction to Service Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="e04f8-157">Get started with Service Bus</span><span class="sxs-lookup"><span data-stu-id="e04f8-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)



