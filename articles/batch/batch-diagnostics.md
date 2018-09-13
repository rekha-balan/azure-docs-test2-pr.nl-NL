---
title: Enable diagnostic logging for Batch events - Azure | Microsoft Docs
description: Record and analyze diagnostic log events for Azure Batch account resources like pools and tasks.
services: batch
documentationcenter: ''
author: tamram
manager: timlt
editor: ''
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 16a13909079306256ded06f2100815c46ff562a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662475"
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="ddeae-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span><span class="sxs-lookup"><span data-stu-id="ddeae-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="ddeae-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span><span class="sxs-lookup"><span data-stu-id="ddeae-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="ddeae-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span><span class="sxs-lookup"><span data-stu-id="ddeae-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="ddeae-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="ddeae-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="ddeae-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span><span class="sxs-lookup"><span data-stu-id="ddeae-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="ddeae-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="ddeae-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ddeae-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ddeae-109">Prerequisites</span></span>
* [<span data-ttu-id="ddeae-110">Azure Batch account</span><span class="sxs-lookup"><span data-stu-id="ddeae-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="ddeae-111">Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="ddeae-111">Azure Storage account</span></span>](../storage/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="ddeae-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span><span class="sxs-lookup"><span data-stu-id="ddeae-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="ddeae-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span><span class="sxs-lookup"><span data-stu-id="ddeae-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="ddeae-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span><span class="sxs-lookup"><span data-stu-id="ddeae-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="ddeae-115">You are **charged** for the data stored in your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="ddeae-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="ddeae-116">This includes the diagnostic logs discussed in this article.</span><span class="sxs-lookup"><span data-stu-id="ddeae-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="ddeae-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ddeae-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="ddeae-118">Enable diagnostic logging</span><span class="sxs-lookup"><span data-stu-id="ddeae-118">Enable diagnostic logging</span></span>
<span data-ttu-id="ddeae-119">Diagnostic logging is not enabled by default for your Batch account.</span><span class="sxs-lookup"><span data-stu-id="ddeae-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="ddeae-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span><span class="sxs-lookup"><span data-stu-id="ddeae-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="ddeae-121">How to enable collection of Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="ddeae-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-diagnostic-logs)

<span data-ttu-id="ddeae-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span><span class="sxs-lookup"><span data-stu-id="ddeae-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="ddeae-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span><span class="sxs-lookup"><span data-stu-id="ddeae-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="ddeae-124">Service Logs</span><span class="sxs-lookup"><span data-stu-id="ddeae-124">Service Logs</span></span>
<span data-ttu-id="ddeae-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span><span class="sxs-lookup"><span data-stu-id="ddeae-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="ddeae-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span><span class="sxs-lookup"><span data-stu-id="ddeae-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="ddeae-127">For example, this is the body of a sample **pool create event**:</span><span class="sxs-lookup"><span data-stu-id="ddeae-127">For example, this is the body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="ddeae-128">Each event body resides in a .json file in the specified Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="ddeae-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="ddeae-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ddeae-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="ddeae-130">Service Log events</span><span class="sxs-lookup"><span data-stu-id="ddeae-130">Service Log events</span></span>
<span data-ttu-id="ddeae-131">The Batch service currently emits the following Service Log events.</span><span class="sxs-lookup"><span data-stu-id="ddeae-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="ddeae-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span><span class="sxs-lookup"><span data-stu-id="ddeae-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="ddeae-133">**Service Log events**</span><span class="sxs-lookup"><span data-stu-id="ddeae-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="ddeae-134">[Pool create][pool_create]</span><span class="sxs-lookup"><span data-stu-id="ddeae-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="ddeae-135">[Pool delete start][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="ddeae-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="ddeae-136">[Pool delete complete][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="ddeae-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="ddeae-137">[Pool resize start][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="ddeae-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="ddeae-138">[Pool resize complete][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="ddeae-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="ddeae-139">[Task start][task_start]</span><span class="sxs-lookup"><span data-stu-id="ddeae-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="ddeae-140">[Task complete][task_complete]</span><span class="sxs-lookup"><span data-stu-id="ddeae-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="ddeae-141">[Task fail][task_fail]</span><span class="sxs-lookup"><span data-stu-id="ddeae-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ddeae-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="ddeae-142">Next steps</span></span>
<span data-ttu-id="ddeae-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ddeae-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="ddeae-144">Stream Azure Diagnostic Logs to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ddeae-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="ddeae-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ddeae-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="ddeae-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span><span class="sxs-lookup"><span data-stu-id="ddeae-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="ddeae-147">Analyze Azure diagnostic logs using Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ddeae-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="ddeae-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span><span class="sxs-lookup"><span data-stu-id="ddeae-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
