---
title: Monitor Azure Batch | Microsoft Docs
description: Learn about Azure monitoring services, metrics, diagnostic logs, and other monitoring features for Azure Batch.
services: batch
author: dlepow
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 04/05/2018
ms.author: danlep
ms.openlocfilehash: 5a321ef7dca86993a913a283fe7b9b076c127d94
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866913"
---
# <a name="monitor-batch-solutions"></a><span data-ttu-id="6c777-103">Monitor Batch solutions</span><span class="sxs-lookup"><span data-stu-id="6c777-103">Monitor Batch solutions</span></span>

<span data-ttu-id="6c777-104">Azure and the Batch service provide a range of services, tools, and APIs to monitor your Batch solutions.</span><span class="sxs-lookup"><span data-stu-id="6c777-104">Azure and the Batch service provide a range of services, tools, and APIs to monitor your Batch solutions.</span></span> <span data-ttu-id="6c777-105">This overview article helps you choose a monitoring approach that fits your needs.</span><span class="sxs-lookup"><span data-stu-id="6c777-105">This overview article helps you choose a monitoring approach that fits your needs.</span></span>

<span data-ttu-id="6c777-106">For an overview of the Azure components and services available to monitor Azure resources, see [Monitoring Azure applications and resources](../monitoring-and-diagnostics/monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c777-106">For an overview of the Azure components and services available to monitor Azure resources, see [Monitoring Azure applications and resources](../monitoring-and-diagnostics/monitoring-overview.md).</span></span>

## <a name="subscription-level-monitoring"></a><span data-ttu-id="6c777-107">Subscription-level monitoring</span><span class="sxs-lookup"><span data-stu-id="6c777-107">Subscription-level monitoring</span></span>

<span data-ttu-id="6c777-108">At the subscription level, which includes Batch accounts, the [Azure activity log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) collects operational event data in [several categories](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="6c777-108">At the subscription level, which includes Batch accounts, the [Azure activity log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) collects operational event data in [several categories](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span>

<span data-ttu-id="6c777-109">For Batch accounts specifically, the activity log collects events related to account creation and deletion and key management.</span><span class="sxs-lookup"><span data-stu-id="6c777-109">For Batch accounts specifically, the activity log collects events related to account creation and deletion and key management.</span></span>

<span data-ttu-id="6c777-110">One way to retrieve events from your activity log is to use the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c777-110">One way to retrieve events from your activity log is to use the Azure portal.</span></span> <span data-ttu-id="6c777-111">Click **All services** > **Activity Log**.</span><span class="sxs-lookup"><span data-stu-id="6c777-111">Click **All services** > **Activity Log**.</span></span> <span data-ttu-id="6c777-112">Or, query for events using the Azure CLI, PowerShell cmdlets, or the Azure Monitor REST API.</span><span class="sxs-lookup"><span data-stu-id="6c777-112">Or, query for events using the Azure CLI, PowerShell cmdlets, or the Azure Monitor REST API.</span></span> <span data-ttu-id="6c777-113">You can also export the activity log, or configure [activity log alerts](../monitoring-and-diagnostics/monitoring-activity-log-alerts-new-experience.md).</span><span class="sxs-lookup"><span data-stu-id="6c777-113">You can also export the activity log, or configure [activity log alerts](../monitoring-and-diagnostics/monitoring-activity-log-alerts-new-experience.md).</span></span>

## <a name="batch-account-level-monitoring"></a><span data-ttu-id="6c777-114">Batch account-level monitoring</span><span class="sxs-lookup"><span data-stu-id="6c777-114">Batch account-level monitoring</span></span>

<span data-ttu-id="6c777-115">Monitor each Batch account using features of [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="6c777-115">Monitor each Batch account using features of [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span> <span data-ttu-id="6c777-116">Azure Monitor collects [metrics](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and optionally [diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) for resources scoped at the level of a Batch account, such as pools, jobs, and tasks.</span><span class="sxs-lookup"><span data-stu-id="6c777-116">Azure Monitor collects [metrics](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and optionally [diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) for resources scoped at the level of a Batch account, such as pools, jobs, and tasks.</span></span> <span data-ttu-id="6c777-117">Collect and consume this data manually or programmatically to monitor activities in your Batch account and to diagnose issues.</span><span class="sxs-lookup"><span data-stu-id="6c777-117">Collect and consume this data manually or programmatically to monitor activities in your Batch account and to diagnose issues.</span></span> <span data-ttu-id="6c777-118">For details, see [Batch metrics, alerts, and logs for diagnostic evaluation and monitoring](batch-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6c777-118">For details, see [Batch metrics, alerts, and logs for diagnostic evaluation and monitoring](batch-diagnostics.md).</span></span>
 
> [!NOTE]
> <span data-ttu-id="6c777-119">Metrics are available by default in your Batch account without additional configuration, and they have a 30-day rolling history.</span><span class="sxs-lookup"><span data-stu-id="6c777-119">Metrics are available by default in your Batch account without additional configuration, and they have a 30-day rolling history.</span></span> <span data-ttu-id="6c777-120">You must enable diagnostic logging for a Batch account, and you may incur additional costs to store or process diagnostic log data.</span><span class="sxs-lookup"><span data-stu-id="6c777-120">You must enable diagnostic logging for a Batch account, and you may incur additional costs to store or process diagnostic log data.</span></span> 

## <a name="batch-resource-monitoring"></a><span data-ttu-id="6c777-121">Batch resource monitoring</span><span class="sxs-lookup"><span data-stu-id="6c777-121">Batch resource monitoring</span></span>

<span data-ttu-id="6c777-122">In your Batch applications, use the Batch APIs to monitor or query the status of your resources including jobs, tasks, nodes, and pools.</span><span class="sxs-lookup"><span data-stu-id="6c777-122">In your Batch applications, use the Batch APIs to monitor or query the status of your resources including jobs, tasks, nodes, and pools.</span></span> <span data-ttu-id="6c777-123">For example:</span><span class="sxs-lookup"><span data-stu-id="6c777-123">For example:</span></span>

* [<span data-ttu-id="6c777-124">Count tasks and compute nodes by state</span><span class="sxs-lookup"><span data-stu-id="6c777-124">Count tasks and compute nodes by state</span></span>](batch-get-resource-counts.md)
* [<span data-ttu-id="6c777-125">Create queries to list Batch resources efficiently</span><span class="sxs-lookup"><span data-stu-id="6c777-125">Create queries to list Batch resources efficiently</span></span>](batch-efficient-list-queries.md)
* [<span data-ttu-id="6c777-126">Create task dependencies</span><span class="sxs-lookup"><span data-stu-id="6c777-126">Create task dependencies</span></span>](batch-task-dependencies.md)
* <span data-ttu-id="6c777-127">Use a [job manager task](/rest/api/batchservice/job/add#jobmanagertask)</span><span class="sxs-lookup"><span data-stu-id="6c777-127">Use a [job manager task](/rest/api/batchservice/job/add#jobmanagertask)</span></span>
* <span data-ttu-id="6c777-128">Monitor the [task state](/rest/api/batchservice/task/list#taskstate)</span><span class="sxs-lookup"><span data-stu-id="6c777-128">Monitor the [task state](/rest/api/batchservice/task/list#taskstate)</span></span>
* <span data-ttu-id="6c777-129">Monitor the [node state](/rest/api/batchservice/computenode/list#computenodestate)</span><span class="sxs-lookup"><span data-stu-id="6c777-129">Monitor the [node state](/rest/api/batchservice/computenode/list#computenodestate)</span></span>
* <span data-ttu-id="6c777-130">Monitor the [pool state](/rest/api/batchservice/pool/get#poolstate)</span><span class="sxs-lookup"><span data-stu-id="6c777-130">Monitor the [pool state](/rest/api/batchservice/pool/get#poolstate)</span></span>
* <span data-ttu-id="6c777-131">Monitor [pool usage in the account](/rest/api/batchservice/pool/listusagemetrics)</span><span class="sxs-lookup"><span data-stu-id="6c777-131">Monitor [pool usage in the account](/rest/api/batchservice/pool/listusagemetrics)</span></span>
* [<span data-ttu-id="6c777-132">Count pool nodes by state</span><span class="sxs-lookup"><span data-stu-id="6c777-132">Count pool nodes by state</span></span>](/rest/api/batchservice/account/listpoolnodecounts)

## <a name="vm-performance-counters-and-application-monitoring"></a><span data-ttu-id="6c777-133">VM performance counters and application monitoring</span><span class="sxs-lookup"><span data-stu-id="6c777-133">VM performance counters and application monitoring</span></span>

* <span data-ttu-id="6c777-134">[Application Insights](../application-insights/app-insights-overview.md) is an Azure service you can use to programmatically monitor the availability, performance, and usage of your Batch jobs and tasks.</span><span class="sxs-lookup"><span data-stu-id="6c777-134">[Application Insights](../application-insights/app-insights-overview.md) is an Azure service you can use to programmatically monitor the availability, performance, and usage of your Batch jobs and tasks.</span></span> <span data-ttu-id="6c777-135">Easily get performance counters from compute nodes (VMs) and custom information for tasks off of the VMs.</span><span class="sxs-lookup"><span data-stu-id="6c777-135">Easily get performance counters from compute nodes (VMs) and custom information for tasks off of the VMs.</span></span> 

  <span data-ttu-id="6c777-136">For an example, see [Monitor and debug a Batch .NET application with Application Insights](monitor-application-insights.md) and the accompanying [code sample](https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ApplicationInsights).</span><span class="sxs-lookup"><span data-stu-id="6c777-136">For an example, see [Monitor and debug a Batch .NET application with Application Insights](monitor-application-insights.md) and the accompanying [code sample](https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ApplicationInsights).</span></span>

  > [!NOTE]
  > <span data-ttu-id="6c777-137">You may incur additional costs to use Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6c777-137">You may incur additional costs to use Application Insights.</span></span> <span data-ttu-id="6c777-138">See the [pricing options](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="6c777-138">See the [pricing options](https://azure.microsoft.com/pricing/details/application-insights/).</span></span> 
  >

* <span data-ttu-id="6c777-139">[Batch Explorer](https://github.com/Azure/BatchExplorer) is a free, rich-featured, standalone client tool to help create, debug, and monitor Azure Batch applications.</span><span class="sxs-lookup"><span data-stu-id="6c777-139">[Batch Explorer](https://github.com/Azure/BatchExplorer) is a free, rich-featured, standalone client tool to help create, debug, and monitor Azure Batch applications.</span></span> <span data-ttu-id="6c777-140">Download an [installation package](https://azure.github.io/BatchExplorer/) for Mac, Linux, or Windows.</span><span class="sxs-lookup"><span data-stu-id="6c777-140">Download an [installation package](https://azure.github.io/BatchExplorer/) for Mac, Linux, or Windows.</span></span> <span data-ttu-id="6c777-141">Optionally configure your Batch solution to [display Application Insights data](https://github.com/Azure/batch-insights) such as VM performance counters in Batch Explorer.</span><span class="sxs-lookup"><span data-stu-id="6c777-141">Optionally configure your Batch solution to [display Application Insights data](https://github.com/Azure/batch-insights) such as VM performance counters in Batch Explorer.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6c777-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c777-142">Next steps</span></span>

* <span data-ttu-id="6c777-143">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span><span class="sxs-lookup"><span data-stu-id="6c777-143">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
* <span data-ttu-id="6c777-144">Learn more about [diagnostic logging](batch-diagnostics.md) with Batch.</span><span class="sxs-lookup"><span data-stu-id="6c777-144">Learn more about [diagnostic logging](batch-diagnostics.md) with Batch.</span></span>