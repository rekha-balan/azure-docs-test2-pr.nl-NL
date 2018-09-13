---
title: Azure Cosmos DB diagnostic logging | Microsoft Docs
description: Use this tutorial to help you get started with Azure Cosmos DB logging.
services: cosmos-db
author: SnehaGunda
manager: kfile
tags: azure-resource-manager
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 03/07/2018
ms.author: sngun
ms.openlocfilehash: acc327bd9fa6828a65243b6d0ad0c6da4b98f48d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869355"
---
# <a name="azure-cosmos-db-diagnostic-logging"></a><span data-ttu-id="bb180-103">Azure Cosmos DB diagnostic logging</span><span class="sxs-lookup"><span data-stu-id="bb180-103">Azure Cosmos DB diagnostic logging</span></span>

<span data-ttu-id="bb180-104">After you start to use one or more Azure Cosmos DB databases, you may want to monitor how and when your databases are accessed.</span><span class="sxs-lookup"><span data-stu-id="bb180-104">After you start to use one or more Azure Cosmos DB databases, you may want to monitor how and when your databases are accessed.</span></span> <span data-ttu-id="bb180-105">This article provides an overview of the logs that are available on the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="bb180-105">This article provides an overview of the logs that are available on the Azure platform.</span></span> <span data-ttu-id="bb180-106">You learn how to enable diagnostic logging for monitoring purposes to send logs to [Azure Storage](https://azure.microsoft.com/services/storage/), how to stream logs to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), and how to export logs to [Azure Log Analytics](https://azure.microsoft.com/services/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="bb180-106">You learn how to enable diagnostic logging for monitoring purposes to send logs to [Azure Storage](https://azure.microsoft.com/services/storage/), how to stream logs to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), and how to export logs to [Azure Log Analytics](https://azure.microsoft.com/services/log-analytics/).</span></span>

## <a name="logs-available-in-azure"></a><span data-ttu-id="bb180-107">Logs available in Azure</span><span class="sxs-lookup"><span data-stu-id="bb180-107">Logs available in Azure</span></span>

<span data-ttu-id="bb180-108">Before we talk about how to monitor your Azure Cosmos DB account, let's clarify a few things about logging and monitoring.</span><span class="sxs-lookup"><span data-stu-id="bb180-108">Before we talk about how to monitor your Azure Cosmos DB account, let's clarify a few things about logging and monitoring.</span></span> <span data-ttu-id="bb180-109">There are different types of logs on the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="bb180-109">There are different types of logs on the Azure platform.</span></span> <span data-ttu-id="bb180-110">There are [Azure Activity Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), [Azure Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs), [Azure metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics), events, heartbeat monitoring, operations logs, and so on.</span><span class="sxs-lookup"><span data-stu-id="bb180-110">There are [Azure Activity Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), [Azure Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs), [Azure metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics), events, heartbeat monitoring, operations logs, and so on.</span></span> <span data-ttu-id="bb180-111">There is a plethora of logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-111">There is a plethora of logs.</span></span> <span data-ttu-id="bb180-112">You can see the complete list of logs in [Azure Log Analytics](https://azure.microsoft.com/services/log-analytics/) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bb180-112">You can see the complete list of logs in [Azure Log Analytics](https://azure.microsoft.com/services/log-analytics/) in the Azure portal.</span></span> 

<span data-ttu-id="bb180-113">The following image shows the different kinds of Azure logs that are available:</span><span class="sxs-lookup"><span data-stu-id="bb180-113">The following image shows the different kinds of Azure logs that are available:</span></span>

![Different kinds of Azure logs](./media/logging/azurelogging.png)

<span data-ttu-id="bb180-115">In the image, the **Compute resources** represent the Azure resources for which you can access the Microsoft Guest OS.</span><span class="sxs-lookup"><span data-stu-id="bb180-115">In the image, the **Compute resources** represent the Azure resources for which you can access the Microsoft Guest OS.</span></span> <span data-ttu-id="bb180-116">For example, Azure Virtual Machines, virtual machine scale sets, Azure Container Service, and so on, are considered compute resources.</span><span class="sxs-lookup"><span data-stu-id="bb180-116">For example, Azure Virtual Machines, virtual machine scale sets, Azure Container Service, and so on, are considered compute resources.</span></span> <span data-ttu-id="bb180-117">Compute resources generate Activity Logs, Diagnostic Logs, and Application Logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-117">Compute resources generate Activity Logs, Diagnostic Logs, and Application Logs.</span></span> <span data-ttu-id="bb180-118">To learn more, refer to the [Azure Monitoring: Compute resources](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#azure-monitor-sources---compute-subset) article.</span><span class="sxs-lookup"><span data-stu-id="bb180-118">To learn more, refer to the [Azure Monitoring: Compute resources](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#azure-monitor-sources---compute-subset) article.</span></span>

<span data-ttu-id="bb180-119">The **Non-Compute resources** are resources in which you can't access the underlying OS and work directly with the resource.</span><span class="sxs-lookup"><span data-stu-id="bb180-119">The **Non-Compute resources** are resources in which you can't access the underlying OS and work directly with the resource.</span></span> <span data-ttu-id="bb180-120">For example, Network Security Groups, Logic Apps, and so on.</span><span class="sxs-lookup"><span data-stu-id="bb180-120">For example, Network Security Groups, Logic Apps, and so on.</span></span> <span data-ttu-id="bb180-121">Azure Cosmos DB is a non-compute resource.</span><span class="sxs-lookup"><span data-stu-id="bb180-121">Azure Cosmos DB is a non-compute resource.</span></span> <span data-ttu-id="bb180-122">You can view logs for non-compute resources in the Activity Log or enable the Diagnostic Logs option in the portal.</span><span class="sxs-lookup"><span data-stu-id="bb180-122">You can view logs for non-compute resources in the Activity Log or enable the Diagnostic Logs option in the portal.</span></span> <span data-ttu-id="bb180-123">To learn more, refer to the [Azure Monitoring: Non-compute resources](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#azure-monitor-sources---everything-else) article.</span><span class="sxs-lookup"><span data-stu-id="bb180-123">To learn more, refer to the [Azure Monitoring: Non-compute resources](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#azure-monitor-sources---everything-else) article.</span></span>

<span data-ttu-id="bb180-124">The Activity Log records the operations at a subscription level for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb180-124">The Activity Log records the operations at a subscription level for Azure Cosmos DB.</span></span> <span data-ttu-id="bb180-125">Operations like ListKeys, Write DatabaseAccounts, and more are logged.</span><span class="sxs-lookup"><span data-stu-id="bb180-125">Operations like ListKeys, Write DatabaseAccounts, and more are logged.</span></span> <span data-ttu-id="bb180-126">Diagnostic Logs provide more granular logging and allow you to log DataPlaneRequests (Create, Read, Query, and so on) and MongoRequests.</span><span class="sxs-lookup"><span data-stu-id="bb180-126">Diagnostic Logs provide more granular logging and allow you to log DataPlaneRequests (Create, Read, Query, and so on) and MongoRequests.</span></span>


<span data-ttu-id="bb180-127">In this article, we focus on the Azure Activity Log, Azure Diagnostic Logs, and Azure metrics.</span><span class="sxs-lookup"><span data-stu-id="bb180-127">In this article, we focus on the Azure Activity Log, Azure Diagnostic Logs, and Azure metrics.</span></span> <span data-ttu-id="bb180-128">What's the difference between these three logs?</span><span class="sxs-lookup"><span data-stu-id="bb180-128">What's the difference between these three logs?</span></span> 

### <a name="azure-activity-log"></a><span data-ttu-id="bb180-129">Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="bb180-129">Azure Activity Log</span></span>

<span data-ttu-id="bb180-130">The Azure Activity Log is a subscription log that provides insight into subscription-level events that have occurred in Azure.</span><span class="sxs-lookup"><span data-stu-id="bb180-130">The Azure Activity Log is a subscription log that provides insight into subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="bb180-131">The Activity Log reports control-plane events for your subscriptions under the Administrative category.</span><span class="sxs-lookup"><span data-stu-id="bb180-131">The Activity Log reports control-plane events for your subscriptions under the Administrative category.</span></span> <span data-ttu-id="bb180-132">You can use the Activity Log to determine the "what, who, and when" for any write operation (PUT, POST, DELETE) on the resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="bb180-132">You can use the Activity Log to determine the "what, who, and when" for any write operation (PUT, POST, DELETE) on the resources in your subscription.</span></span> <span data-ttu-id="bb180-133">You can also understand the status of the operation and other relevant properties.</span><span class="sxs-lookup"><span data-stu-id="bb180-133">You can also understand the status of the operation and other relevant properties.</span></span> 

<span data-ttu-id="bb180-134">The Activity Log differs from Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-134">The Activity Log differs from Diagnostic Logs.</span></span> <span data-ttu-id="bb180-135">The Activity Log provides data about the operations on a resource from the outside (the _control plane_).</span><span class="sxs-lookup"><span data-stu-id="bb180-135">The Activity Log provides data about the operations on a resource from the outside (the _control plane_).</span></span> <span data-ttu-id="bb180-136">In the Azure Cosmos DB context, control plane operations include create container, list keys, delete keys, list database, and so on.</span><span class="sxs-lookup"><span data-stu-id="bb180-136">In the Azure Cosmos DB context, control plane operations include create container, list keys, delete keys, list database, and so on.</span></span> <span data-ttu-id="bb180-137">Diagnostics Logs are emitted by a resource and provide information about the operation of that resource (the _data plane_).</span><span class="sxs-lookup"><span data-stu-id="bb180-137">Diagnostics Logs are emitted by a resource and provide information about the operation of that resource (the _data plane_).</span></span> <span data-ttu-id="bb180-138">Some examples of the data plane operations in the diagnostic log are Delete, Insert, and ReadFeed.</span><span class="sxs-lookup"><span data-stu-id="bb180-138">Some examples of the data plane operations in the diagnostic log are Delete, Insert, and ReadFeed.</span></span>

<span data-ttu-id="bb180-139">Activity Logs (control plane operations) can be richer in nature and can include the full email address of the caller, caller IP address, resource name, operation name, TenantId, and more.</span><span class="sxs-lookup"><span data-stu-id="bb180-139">Activity Logs (control plane operations) can be richer in nature and can include the full email address of the caller, caller IP address, resource name, operation name, TenantId, and more.</span></span> <span data-ttu-id="bb180-140">The Activity Log contains several [categories](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-activity-log-schema) of data.</span><span class="sxs-lookup"><span data-stu-id="bb180-140">The Activity Log contains several [categories](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-activity-log-schema) of data.</span></span> <span data-ttu-id="bb180-141">For full details on the schemata of these categories, see [Azure Activity Log event schema](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-activity-log-schema).</span><span class="sxs-lookup"><span data-stu-id="bb180-141">For full details on the schemata of these categories, see [Azure Activity Log event schema](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-activity-log-schema).</span></span> <span data-ttu-id="bb180-142">However, Diagnostic Logs can be restrictive in nature as personal data is often stripped from these logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-142">However, Diagnostic Logs can be restrictive in nature as personal data is often stripped from these logs.</span></span> <span data-ttu-id="bb180-143">You might have the IP address of the caller, but the last octant is removed.</span><span class="sxs-lookup"><span data-stu-id="bb180-143">You might have the IP address of the caller, but the last octant is removed.</span></span>

### <a name="azure-metrics"></a><span data-ttu-id="bb180-144">Azure metrics</span><span class="sxs-lookup"><span data-stu-id="bb180-144">Azure metrics</span></span>

<span data-ttu-id="bb180-145">[Azure metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) have the most important type of Azure telemetry data (also called _performance counters_) that's emitted by most Azure resources.</span><span class="sxs-lookup"><span data-stu-id="bb180-145">[Azure metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) have the most important type of Azure telemetry data (also called _performance counters_) that's emitted by most Azure resources.</span></span> <span data-ttu-id="bb180-146">Metrics let you view information about throughput, storage, consistency, availability, and the latency of your Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="bb180-146">Metrics let you view information about throughput, storage, consistency, availability, and the latency of your Azure Cosmos DB resources.</span></span> <span data-ttu-id="bb180-147">For more information, see [Monitoring and debugging with metrics in Azure Cosmos DB](use-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="bb180-147">For more information, see [Monitoring and debugging with metrics in Azure Cosmos DB](use-metrics.md).</span></span>

### <a name="azure-diagnostic-logs"></a><span data-ttu-id="bb180-148">Azure Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="bb180-148">Azure Diagnostic Logs</span></span>

<span data-ttu-id="bb180-149">Azure Diagnostic Logs are emitted by a resource and provide rich, frequent data about the operation of that resource.</span><span class="sxs-lookup"><span data-stu-id="bb180-149">Azure Diagnostic Logs are emitted by a resource and provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="bb180-150">The content of these logs varies by resource type.</span><span class="sxs-lookup"><span data-stu-id="bb180-150">The content of these logs varies by resource type.</span></span> <span data-ttu-id="bb180-151">Resource-level diagnostic logs also differ from Guest OS-level diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-151">Resource-level diagnostic logs also differ from Guest OS-level diagnostic logs.</span></span> <span data-ttu-id="bb180-152">Guest OS diagnostic logs are collected by an agent that's running inside a virtual machine or other supported resource type.</span><span class="sxs-lookup"><span data-stu-id="bb180-152">Guest OS diagnostic logs are collected by an agent that's running inside a virtual machine or other supported resource type.</span></span> <span data-ttu-id="bb180-153">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself.</span><span class="sxs-lookup"><span data-stu-id="bb180-153">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself.</span></span> <span data-ttu-id="bb180-154">Guest OS-level diagnostic logs capture data from the operating system and applications that are running on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bb180-154">Guest OS-level diagnostic logs capture data from the operating system and applications that are running on a virtual machine.</span></span>

![Diagnostic logging to Storage, Event Hubs, or Log Analytics](./media/logging/azure-cosmos-db-logging-overview.png)

### <a name="what-is-logged-by-azure-diagnostic-logs"></a><span data-ttu-id="bb180-156">What is logged by Azure Diagnostic Logs?</span><span class="sxs-lookup"><span data-stu-id="bb180-156">What is logged by Azure Diagnostic Logs?</span></span>

* <span data-ttu-id="bb180-157">All authenticated backend requests (TCP/REST) across all APIs are logged, including failed requests as a result of access permissions, system errors, or bad requests.</span><span class="sxs-lookup"><span data-stu-id="bb180-157">All authenticated backend requests (TCP/REST) across all APIs are logged, including failed requests as a result of access permissions, system errors, or bad requests.</span></span> <span data-ttu-id="bb180-158">Support for user-initiated Graph, Cassandra, and Table API requests aren't currently available.</span><span class="sxs-lookup"><span data-stu-id="bb180-158">Support for user-initiated Graph, Cassandra, and Table API requests aren't currently available.</span></span>
* <span data-ttu-id="bb180-159">Operations on the database itself, which include CRUD operations on all documents, containers, and databases.</span><span class="sxs-lookup"><span data-stu-id="bb180-159">Operations on the database itself, which include CRUD operations on all documents, containers, and databases.</span></span>
* <span data-ttu-id="bb180-160">Operations on account keys, which include creating, modifying, or deleting the keys.</span><span class="sxs-lookup"><span data-stu-id="bb180-160">Operations on account keys, which include creating, modifying, or deleting the keys.</span></span>
* <span data-ttu-id="bb180-161">Unauthenticated requests that result in a 401 response.</span><span class="sxs-lookup"><span data-stu-id="bb180-161">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="bb180-162">For example, requests that don't have a bearer token, or are malformed or expired, or have an invalid token.</span><span class="sxs-lookup"><span data-stu-id="bb180-162">For example, requests that don't have a bearer token, or are malformed or expired, or have an invalid token.</span></span>

<a id="#turn-on"></a>
## <a name="turn-on-logging-in-the-azure-portal"></a><span data-ttu-id="bb180-163">Turn on logging in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bb180-163">Turn on logging in the Azure portal</span></span>

<span data-ttu-id="bb180-164">To enable diagnostics logging, you must have the following resources:</span><span class="sxs-lookup"><span data-stu-id="bb180-164">To enable diagnostics logging, you must have the following resources:</span></span>

* <span data-ttu-id="bb180-165">An existing Azure Cosmos DB account, database, and container.</span><span class="sxs-lookup"><span data-stu-id="bb180-165">An existing Azure Cosmos DB account, database, and container.</span></span> <span data-ttu-id="bb180-166">For instructions on creating these resources, see [Create a database account by using the Azure portal](create-sql-api-dotnet.md#create-a-database-account), [Azure CLI samples](cli-samples.md), or [PowerShell samples](powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bb180-166">For instructions on creating these resources, see [Create a database account by using the Azure portal](create-sql-api-dotnet.md#create-a-database-account), [Azure CLI samples](cli-samples.md), or [PowerShell samples](powershell-samples.md).</span></span>

<span data-ttu-id="bb180-167">To enable diagnostic logging in the Azure portal, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb180-167">To enable diagnostic logging in the Azure portal, do the following steps:</span></span>

1. <span data-ttu-id="bb180-168">In the [Azure portal](https://portal.azure.com), in your Azure Cosmos DB account, select **Diagnostic logs** in the left navigation, and then select **Turn on diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="bb180-168">In the [Azure portal](https://portal.azure.com), in your Azure Cosmos DB account, select **Diagnostic logs** in the left navigation, and then select **Turn on diagnostics**.</span></span>

    ![Turn on diagnostic logging for Azure Cosmos DB in the Azure portal](./media/logging/turn-on-portal-logging.png)

2. <span data-ttu-id="bb180-170">In the **Diagnostic settings** page, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb180-170">In the **Diagnostic settings** page, do the following steps:</span></span> 

    * <span data-ttu-id="bb180-171">**Name**: Enter a name for the logs to create.</span><span class="sxs-lookup"><span data-stu-id="bb180-171">**Name**: Enter a name for the logs to create.</span></span>

    * <span data-ttu-id="bb180-172">**Archive to a storage account**: To use this option, you need an existing storage account to connect to.</span><span class="sxs-lookup"><span data-stu-id="bb180-172">**Archive to a storage account**: To use this option, you need an existing storage account to connect to.</span></span> <span data-ttu-id="bb180-173">To create a new storage account in the portal, see [Create a storage account](../storage/common/storage-create-storage-account.md) and follow the instructions to create an Azure Resource Manager, general-purpose account.</span><span class="sxs-lookup"><span data-stu-id="bb180-173">To create a new storage account in the portal, see [Create a storage account](../storage/common/storage-create-storage-account.md) and follow the instructions to create an Azure Resource Manager, general-purpose account.</span></span> <span data-ttu-id="bb180-174">Then, return to this page in the portal to select your storage account.</span><span class="sxs-lookup"><span data-stu-id="bb180-174">Then, return to this page in the portal to select your storage account.</span></span> <span data-ttu-id="bb180-175">It might take a few minutes for newly created storage accounts to appear in the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="bb180-175">It might take a few minutes for newly created storage accounts to appear in the drop-down menu.</span></span>
    * <span data-ttu-id="bb180-176">**Stream to an event hub**: To use this option, you need an existing Event Hubs namespace and event hub to connect to.</span><span class="sxs-lookup"><span data-stu-id="bb180-176">**Stream to an event hub**: To use this option, you need an existing Event Hubs namespace and event hub to connect to.</span></span> <span data-ttu-id="bb180-177">To create an Event Hubs namespace, see [Create an Event Hubs namespace and an event hub by using the Azure portal](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="bb180-177">To create an Event Hubs namespace, see [Create an Event Hubs namespace and an event hub by using the Azure portal](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="bb180-178">Then, return to this page in the portal to select the Event Hubs namespace and policy name.</span><span class="sxs-lookup"><span data-stu-id="bb180-178">Then, return to this page in the portal to select the Event Hubs namespace and policy name.</span></span>
    * <span data-ttu-id="bb180-179">**Send to Log Analytics**: To use this option, either use an existing workspace or create a new Log Analytics workspace by following the steps to [Create a new workspace](../log-analytics/log-analytics-quick-collect-azurevm.md#create-a-workspace) in the portal.</span><span class="sxs-lookup"><span data-stu-id="bb180-179">**Send to Log Analytics**: To use this option, either use an existing workspace or create a new Log Analytics workspace by following the steps to [Create a new workspace](../log-analytics/log-analytics-quick-collect-azurevm.md#create-a-workspace) in the portal.</span></span> <span data-ttu-id="bb180-180">For more information about viewing your logs in Log Analytics, see [View logs in Log Analytics](#view-in-loganalytics).</span><span class="sxs-lookup"><span data-stu-id="bb180-180">For more information about viewing your logs in Log Analytics, see [View logs in Log Analytics](#view-in-loganalytics).</span></span>
    * <span data-ttu-id="bb180-181">**Log DataPlaneRequests**: Select this option to log back-end requests from the underlying Azure Cosmos DB distributed platform for SQL, Graph, MongoDB, Cassandra, and Table API accounts.</span><span class="sxs-lookup"><span data-stu-id="bb180-181">**Log DataPlaneRequests**: Select this option to log back-end requests from the underlying Azure Cosmos DB distributed platform for SQL, Graph, MongoDB, Cassandra, and Table API accounts.</span></span> <span data-ttu-id="bb180-182">If you're archiving to a storage account, you can select the retention period for the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-182">If you're archiving to a storage account, you can select the retention period for the diagnostic logs.</span></span> <span data-ttu-id="bb180-183">Logs are auto-deleted after the retention period expires.</span><span class="sxs-lookup"><span data-stu-id="bb180-183">Logs are auto-deleted after the retention period expires.</span></span>
    * <span data-ttu-id="bb180-184">**Log MongoRequests**: Select this option to log user-initiated requests from the Azure Cosmos DB front end for serving MongoDB API accounts.</span><span class="sxs-lookup"><span data-stu-id="bb180-184">**Log MongoRequests**: Select this option to log user-initiated requests from the Azure Cosmos DB front end for serving MongoDB API accounts.</span></span> <span data-ttu-id="bb180-185">If you're archiving to a storage account, you can select the retention period for the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-185">If you're archiving to a storage account, you can select the retention period for the diagnostic logs.</span></span> <span data-ttu-id="bb180-186">Logs are auto-deleted after the retention period expires.</span><span class="sxs-lookup"><span data-stu-id="bb180-186">Logs are auto-deleted after the retention period expires.</span></span>
    * <span data-ttu-id="bb180-187">**Metric Requests**: Select this option to store verbose data in [Azure metrics](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="bb180-187">**Metric Requests**: Select this option to store verbose data in [Azure metrics](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span> <span data-ttu-id="bb180-188">If you're archiving to a storage account, you can select the retention period for the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-188">If you're archiving to a storage account, you can select the retention period for the diagnostic logs.</span></span> <span data-ttu-id="bb180-189">Logs are auto-deleted after the retention period expires.</span><span class="sxs-lookup"><span data-stu-id="bb180-189">Logs are auto-deleted after the retention period expires.</span></span>

3. <span data-ttu-id="bb180-190">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="bb180-190">Select **Save**.</span></span>

    <span data-ttu-id="bb180-191">If you receive an error that says "Failed to update diagnostics for \<workspace name>.</span><span class="sxs-lookup"><span data-stu-id="bb180-191">If you receive an error that says "Failed to update diagnostics for \<workspace name>.</span></span> <span data-ttu-id="bb180-192">The subscription \<subscription id> is not registered to use microsoft.insights," follow the [Troubleshoot Azure Diagnostics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage) instructions to register the account and then retry this procedure.</span><span class="sxs-lookup"><span data-stu-id="bb180-192">The subscription \<subscription id> is not registered to use microsoft.insights," follow the [Troubleshoot Azure Diagnostics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage) instructions to register the account and then retry this procedure.</span></span>

    <span data-ttu-id="bb180-193">If you want to change how your diagnostic logs are saved at any point in the future, return to this page to modify the diagnostic log settings for your account.</span><span class="sxs-lookup"><span data-stu-id="bb180-193">If you want to change how your diagnostic logs are saved at any point in the future, return to this page to modify the diagnostic log settings for your account.</span></span>

## <a name="turn-on-logging-by-using-azure-cli"></a><span data-ttu-id="bb180-194">Turn on logging by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bb180-194">Turn on logging by using Azure CLI</span></span>

<span data-ttu-id="bb180-195">To enable metrics and diagnostics logging by using Azure CLI, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="bb180-195">To enable metrics and diagnostics logging by using Azure CLI, use the following commands:</span></span>

- <span data-ttu-id="bb180-196">To enable storage of Diagnostic Logs in a storage account, use this command:</span><span class="sxs-lookup"><span data-stu-id="bb180-196">To enable storage of Diagnostic Logs in a storage account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="bb180-197">The `resourceId` is the name of the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="bb180-197">The `resourceId` is the name of the Azure Cosmos DB account.</span></span> <span data-ttu-id="bb180-198">The `storageId` is the name of the storage account to which you want to send the logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-198">The `storageId` is the name of the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="bb180-199">To enable streaming of Diagnostic Logs to an event hub, use this command:</span><span class="sxs-lookup"><span data-stu-id="bb180-199">To enable streaming of Diagnostic Logs to an event hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="bb180-200">The `resourceId` is the name of the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="bb180-200">The `resourceId` is the name of the Azure Cosmos DB account.</span></span> <span data-ttu-id="bb180-201">The `serviceBusRuleId` is a string with this format:</span><span class="sxs-lookup"><span data-stu-id="bb180-201">The `serviceBusRuleId` is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="bb180-202">To enable sending Diagnostic Logs to a Log Analytics workspace, use this command:</span><span class="sxs-lookup"><span data-stu-id="bb180-202">To enable sending Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

<span data-ttu-id="bb180-203">You can combine these parameters to enable multiple output options.</span><span class="sxs-lookup"><span data-stu-id="bb180-203">You can combine these parameters to enable multiple output options.</span></span>

## <a name="turn-on-logging-by-using-powershell"></a><span data-ttu-id="bb180-204">Turn on logging by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb180-204">Turn on logging by using PowerShell</span></span>

<span data-ttu-id="bb180-205">To turn on diagnostic logging by using PowerShell, you need Azure Powershell with a minimum version of 1.0.1.</span><span class="sxs-lookup"><span data-stu-id="bb180-205">To turn on diagnostic logging by using PowerShell, you need Azure Powershell with a minimum version of 1.0.1.</span></span>

<span data-ttu-id="bb180-206">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bb180-206">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="bb180-207">If you've already installed Azure PowerShell and don't know the version, from the PowerShell console type `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="bb180-207">If you've already installed Azure PowerShell and don't know the version, from the PowerShell console type `(Get-Module azure -ListAvailable).Version`.</span></span>  

### <a id="connect"></a><span data-ttu-id="bb180-208">Connect to your subscriptions</span><span class="sxs-lookup"><span data-stu-id="bb180-208">Connect to your subscriptions</span></span>
<span data-ttu-id="bb180-209">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span><span class="sxs-lookup"><span data-stu-id="bb180-209">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

```powershell
Connect-AzureRmAccount
```

<span data-ttu-id="bb180-210">In the pop-up browser window, enter your Azure account user name and password.</span><span class="sxs-lookup"><span data-stu-id="bb180-210">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="bb180-211">Azure PowerShell gets all of the subscriptions that are associated with this account, and by default, uses the first one.</span><span class="sxs-lookup"><span data-stu-id="bb180-211">Azure PowerShell gets all of the subscriptions that are associated with this account, and by default, uses the first one.</span></span>

<span data-ttu-id="bb180-212">If you have more than one subscription, you might have to specify the specific subscription that was used to create your Azure key vault.</span><span class="sxs-lookup"><span data-stu-id="bb180-212">If you have more than one subscription, you might have to specify the specific subscription that was used to create your Azure key vault.</span></span> <span data-ttu-id="bb180-213">To see the subscriptions for your account, type the following command:</span><span class="sxs-lookup"><span data-stu-id="bb180-213">To see the subscriptions for your account, type the following command:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="bb180-214">Then, to specify the subscription that's associated with the Azure Cosmos DB account that you're logging, type the following command:</span><span class="sxs-lookup"><span data-stu-id="bb180-214">Then, to specify the subscription that's associated with the Azure Cosmos DB account that you're logging, type the following command:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscription ID>
```

> [!NOTE]
> <span data-ttu-id="bb180-215">If you have more than one subscription that's associated with your account, it's important to specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="bb180-215">If you have more than one subscription that's associated with your account, it's important to specify the subscription that you want to use.</span></span>
>
>

<span data-ttu-id="bb180-216">For more information about how to configure Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bb180-216">For more information about how to configure Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a id="storage"></a><span data-ttu-id="bb180-217">Create a new storage account for your logs</span><span class="sxs-lookup"><span data-stu-id="bb180-217">Create a new storage account for your logs</span></span>
<span data-ttu-id="bb180-218">Although you can use an existing storage account for your logs, in this tutorial, we create a new storage account that's dedicated to Azure Cosmos DB logs.</span><span class="sxs-lookup"><span data-stu-id="bb180-218">Although you can use an existing storage account for your logs, in this tutorial, we create a new storage account that's dedicated to Azure Cosmos DB logs.</span></span> <span data-ttu-id="bb180-219">For convenience, we store the storage account details in a variable named **sa**.</span><span class="sxs-lookup"><span data-stu-id="bb180-219">For convenience, we store the storage account details in a variable named **sa**.</span></span>

<span data-ttu-id="bb180-220">For additional ease of management, in this tutorial, we use the same resource group as the one that contains the Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="bb180-220">For additional ease of management, in this tutorial, we use the same resource group as the one that contains the Azure Cosmos DB database.</span></span> <span data-ttu-id="bb180-221">Substitute your values for the **ContosoResourceGroup**, **contosocosmosdblogs**, and **North Central US** parameters, as applicable:</span><span class="sxs-lookup"><span data-stu-id="bb180-221">Substitute your values for the **ContosoResourceGroup**, **contosocosmosdblogs**, and **North Central US** parameters, as applicable:</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup `
-Name contosocosmosdblogs -Type Standard_LRS -Location 'North Central US'
```

> [!NOTE]
> <span data-ttu-id="bb180-222">If you decide to use an existing storage account, the account must use the same subscription as your Azure Cosmos DB subscription.</span><span class="sxs-lookup"><span data-stu-id="bb180-222">If you decide to use an existing storage account, the account must use the same subscription as your Azure Cosmos DB subscription.</span></span> <span data-ttu-id="bb180-223">The account must also use the Resource Manager deployment model, rather than the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="bb180-223">The account must also use the Resource Manager deployment model, rather than the classic deployment model.</span></span>
>
>

### <a id="identify"></a><span data-ttu-id="bb180-224">Identify the Azure Cosmos DB account for your logs</span><span class="sxs-lookup"><span data-stu-id="bb180-224">Identify the Azure Cosmos DB account for your logs</span></span>
<span data-ttu-id="bb180-225">Set the Azure Cosmos DB account name to a variable named **account**, where **ResourceName** is the name of the Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="bb180-225">Set the Azure Cosmos DB account name to a variable named **account**, where **ResourceName** is the name of the Azure Cosmos DB account.</span></span>

```powershell
$account = Get-AzureRmResource -ResourceGroupName ContosoResourceGroup `
-ResourceName contosocosmosdb -ResourceType "Microsoft.DocumentDb/databaseAccounts"
```

### <a id="enable"></a><span data-ttu-id="bb180-226">Enable logging</span><span class="sxs-lookup"><span data-stu-id="bb180-226">Enable logging</span></span>
<span data-ttu-id="bb180-227">To enable logging for Azure Cosmos DB, use the `Set-AzureRmDiagnosticSetting` cmdlet with variables for the new storage account, Azure Cosmos DB account, and the category to enable for logging.</span><span class="sxs-lookup"><span data-stu-id="bb180-227">To enable logging for Azure Cosmos DB, use the `Set-AzureRmDiagnosticSetting` cmdlet with variables for the new storage account, Azure Cosmos DB account, and the category to enable for logging.</span></span> <span data-ttu-id="bb180-228">Run the following command and set the **-Enabled** flag to **$true**:</span><span class="sxs-lookup"><span data-stu-id="bb180-228">Run the following command and set the **-Enabled** flag to **$true**:</span></span>

```powershell
Set-AzureRmDiagnosticSetting  -ResourceId $account.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories DataPlaneRequests
```

<span data-ttu-id="bb180-229">The output for the command should resemble the following sample:</span><span class="sxs-lookup"><span data-stu-id="bb180-229">The output for the command should resemble the following sample:</span></span>

```powershell
    StorageAccountId            : /subscriptions/<subscription-ID>/resourceGroups/ContosoResourceGroup/providers`
    /Microsoft.Storage/storageAccounts/contosocosmosdblogs
    ServiceBusRuleId            :
    EventHubAuthorizationRuleId :
    Metrics
        TimeGrain       : PT1M
        Enabled         : False
        RetentionPolicy
        Enabled : False
        Days    : 0
    
    Logs
        Category        : DataPlaneRequests
        Enabled         : True
        RetentionPolicy
        Enabled : False
        Days    : 0
    
    WorkspaceId                 :
    Id                          : /subscriptions/<subscription-ID>/resourcegroups/ContosoResourceGroup/providers`
    /microsoft.documentdb/databaseaccounts/contosocosmosdb/providers/microsoft.insights/diagnosticSettings/service
    Name                        : service
    Type                        :
    Location                    :
    Tags                        :
```

<span data-ttu-id="bb180-230">The output from the command confirms that logging is now enabled for your database and information is being saved to your storage account.</span><span class="sxs-lookup"><span data-stu-id="bb180-230">The output from the command confirms that logging is now enabled for your database and information is being saved to your storage account.</span></span>

<span data-ttu-id="bb180-231">Optionally, you can also set the retention policy for your logs, such that older logs are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="bb180-231">Optionally, you can also set the retention policy for your logs, such that older logs are automatically deleted.</span></span> <span data-ttu-id="bb180-232">For example, set the retention policy with the **-RetentionEnabled** flag set to **$true**.</span><span class="sxs-lookup"><span data-stu-id="bb180-232">For example, set the retention policy with the **-RetentionEnabled** flag set to **$true**.</span></span> <span data-ttu-id="bb180-233">Set the **-RetentionInDays** parameter to **90** so that logs older than 90 days are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="bb180-233">Set the **-RetentionInDays** parameter to **90** so that logs older than 90 days are automatically deleted.</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId $account.ResourceId`
 -StorageAccountId $sa.Id -Enabled $true -Categories DataPlaneRequests`
  -RetentionEnabled $true -RetentionInDays 90
```

### <a id="access"></a><span data-ttu-id="bb180-234">Access your logs</span><span class="sxs-lookup"><span data-stu-id="bb180-234">Access your logs</span></span>
<span data-ttu-id="bb180-235">Azure Cosmos DB logs for the **DataPlaneRequests** category are stored in the **insights-logs-data-plane-requests** container in the storage account that you provided.</span><span class="sxs-lookup"><span data-stu-id="bb180-235">Azure Cosmos DB logs for the **DataPlaneRequests** category are stored in the **insights-logs-data-plane-requests** container in the storage account that you provided.</span></span> 

<span data-ttu-id="bb180-236">First, create a variable for the container name.</span><span class="sxs-lookup"><span data-stu-id="bb180-236">First, create a variable for the container name.</span></span> <span data-ttu-id="bb180-237">The variable is used throughout the walk-through.</span><span class="sxs-lookup"><span data-stu-id="bb180-237">The variable is used throughout the walk-through.</span></span>

```powershell
    $container = 'insights-logs-dataplanerequests'
```

<span data-ttu-id="bb180-238">To list all of the blobs in this container, type:</span><span class="sxs-lookup"><span data-stu-id="bb180-238">To list all of the blobs in this container, type:</span></span>

```powershell
Get-AzureStorageBlob -Container $container -Context $sa.Context
```

<span data-ttu-id="bb180-239">The output for the command should resemble the following sample:</span><span class="sxs-lookup"><span data-stu-id="bb180-239">The output for the command should resemble the following sample:</span></span>

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 10510193
ContentType       : application/octet-stream
LastModified      : 9/28/2017 7:49:04 PM +00:00
SnapshotTime      :
ContinuationToken:
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.`
                    LazyAzureStorageContext
Name              : resourceId=/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS`
/MICROSOFT.DOCUMENTDB/DATABASEACCOUNTS/CONTOSOCOSMOSDB/y=2017/m=09/d=28/h=19/m=00/PT1H.json
```

<span data-ttu-id="bb180-240">As you can see from this output, the blobs follow a naming convention: `resourceId=/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DOCUMENTDB/DATABASEACCOUNTS/<Database Account Name>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json`</span><span class="sxs-lookup"><span data-stu-id="bb180-240">As you can see from this output, the blobs follow a naming convention: `resourceId=/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DOCUMENTDB/DATABASEACCOUNTS/<Database Account Name>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json`</span></span>

<span data-ttu-id="bb180-241">The date and time values use UTC.</span><span class="sxs-lookup"><span data-stu-id="bb180-241">The date and time values use UTC.</span></span>

<span data-ttu-id="bb180-242">Because the same storage account can be used to collect logs for multiple resources, you can use the fully qualified resource ID in the blob name to access and download the specific blobs that you need.</span><span class="sxs-lookup"><span data-stu-id="bb180-242">Because the same storage account can be used to collect logs for multiple resources, you can use the fully qualified resource ID in the blob name to access and download the specific blobs that you need.</span></span> <span data-ttu-id="bb180-243">Before we do that, we cover how to download all of the blobs.</span><span class="sxs-lookup"><span data-stu-id="bb180-243">Before we do that, we cover how to download all of the blobs.</span></span>

<span data-ttu-id="bb180-244">First, create a folder to download the blobs.</span><span class="sxs-lookup"><span data-stu-id="bb180-244">First, create a folder to download the blobs.</span></span> <span data-ttu-id="bb180-245">For example:</span><span class="sxs-lookup"><span data-stu-id="bb180-245">For example:</span></span>

```powershell
New-Item -Path 'C:\Users\username\ContosoCosmosDBLogs'`
 -ItemType Directory -Force
```

<span data-ttu-id="bb180-246">Then, get a list of all of the blobs:</span><span class="sxs-lookup"><span data-stu-id="bb180-246">Then, get a list of all of the blobs:</span></span>  

```powershell
$blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context
```

<span data-ttu-id="bb180-247">Pipe this list through the `Get-AzureStorageBlobContent` command to download the blobs into the destination folder:</span><span class="sxs-lookup"><span data-stu-id="bb180-247">Pipe this list through the `Get-AzureStorageBlobContent` command to download the blobs into the destination folder:</span></span>

```powershell
$blobs | Get-AzureStorageBlobContent `
 -Destination 'C:\Users\username\ContosoCosmosDBLogs'
```

<span data-ttu-id="bb180-248">When you run this second command, the **/** delimiter in the blob names creates a full folder structure under the destination folder.</span><span class="sxs-lookup"><span data-stu-id="bb180-248">When you run this second command, the **/** delimiter in the blob names creates a full folder structure under the destination folder.</span></span> <span data-ttu-id="bb180-249">This folder structure is used to download and store the blobs as files.</span><span class="sxs-lookup"><span data-stu-id="bb180-249">This folder structure is used to download and store the blobs as files.</span></span>

<span data-ttu-id="bb180-250">To selectively download blobs, use wildcards.</span><span class="sxs-lookup"><span data-stu-id="bb180-250">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="bb180-251">For example:</span><span class="sxs-lookup"><span data-stu-id="bb180-251">For example:</span></span>

* <span data-ttu-id="bb180-252">If you have multiple databases and want to download logs for just one database named **CONTOSOCOSMOSDB3**, use the command:</span><span class="sxs-lookup"><span data-stu-id="bb180-252">If you have multiple databases and want to download logs for just one database named **CONTOSOCOSMOSDB3**, use the command:</span></span>

    ```powershell
    Get-AzureStorageBlob -Container $container `
     -Context $sa.Context -Blob '*/DATABASEACCOUNTS/CONTOSOCOSMOSDB3
    ```

* <span data-ttu-id="bb180-253">If you have multiple resource groups and want to download logs for just one resource group, use the command `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="bb180-253">If you have multiple resource groups and want to download logs for just one resource group, use the command `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

    ```powershell
    Get-AzureStorageBlob -Container $container `
    -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
    ```
* <span data-ttu-id="bb180-254">If you want to download all of the logs for the month of July 2017, use the command `-Blob '*/year=2017/m=07/*'`:</span><span class="sxs-lookup"><span data-stu-id="bb180-254">If you want to download all of the logs for the month of July 2017, use the command `-Blob '*/year=2017/m=07/*'`:</span></span>

    ```powershell
    Get-AzureStorageBlob -Container $container `
     -Context $sa.Context -Blob '*/year=2017/m=07/*'
    ```

<span data-ttu-id="bb180-255">You can also run the following commands:</span><span class="sxs-lookup"><span data-stu-id="bb180-255">You can also run the following commands:</span></span>

* <span data-ttu-id="bb180-256">To query the status of diagnostic settings for your database resource, use the command `Get-AzureRmDiagnosticSetting -ResourceId $account.ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="bb180-256">To query the status of diagnostic settings for your database resource, use the command `Get-AzureRmDiagnosticSetting -ResourceId $account.ResourceId`.</span></span>
* <span data-ttu-id="bb180-257">To disable logging of the **DataPlaneRequests** category for your database account resource, use the command `Set-AzureRmDiagnosticSetting -ResourceId $account.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories DataPlaneRequests`.</span><span class="sxs-lookup"><span data-stu-id="bb180-257">To disable logging of the **DataPlaneRequests** category for your database account resource, use the command `Set-AzureRmDiagnosticSetting -ResourceId $account.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories DataPlaneRequests`.</span></span>


<span data-ttu-id="bb180-258">The blobs that are returned in each of these queries are stored as text and formatted as a JSON blob, as shown in the following code:</span><span class="sxs-lookup"><span data-stu-id="bb180-258">The blobs that are returned in each of these queries are stored as text and formatted as a JSON blob, as shown in the following code:</span></span>

```json
{
    "records":
    [
        {
           "time": "Fri, 23 Jun 2017 19:29:50.266 GMT",
           "resourceId": "contosocosmosdb",
           "category": "DataPlaneRequests",
           "operationName": "Query",
           "resourceType": "Database",
           "properties": {"activityId": "05fcf607-6f64-48fe-81a5-f13ac13dd1eb",`
           "userAgent": "documentdb-dotnet-sdk/1.12.0 Host/64-bit MicrosoftWindowsNT/6.2.9200.0 AzureSearchIndexer/1.0.0",`
           "resourceType": "Database","statusCode": "200","documentResourceId": "",`
           "clientIpAddress": "13.92.241.0","requestCharge": "2.260","collectionRid": "",`
           "duration": "9250","requestLength": "72","responseLength": "209", "resourceTokenUserRid": ""}
        }
    ]
}
```

<span data-ttu-id="bb180-259">To learn about the data in each JSON blob, see [Interpret your Azure Cosmos DB logs](#interpret).</span><span class="sxs-lookup"><span data-stu-id="bb180-259">To learn about the data in each JSON blob, see [Interpret your Azure Cosmos DB logs](#interpret).</span></span>

## <a name="manage-your-logs"></a><span data-ttu-id="bb180-260">Manage your logs</span><span class="sxs-lookup"><span data-stu-id="bb180-260">Manage your logs</span></span>

<span data-ttu-id="bb180-261">Diagnostic Logs are made available in your account for two hours from the time that the Azure Cosmos DB operation was made.</span><span class="sxs-lookup"><span data-stu-id="bb180-261">Diagnostic Logs are made available in your account for two hours from the time that the Azure Cosmos DB operation was made.</span></span> <span data-ttu-id="bb180-262">It's up to you to manage your logs in your storage account:</span><span class="sxs-lookup"><span data-stu-id="bb180-262">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="bb180-263">Use standard Azure access control methods to secure your logs and restrict who can access them.</span><span class="sxs-lookup"><span data-stu-id="bb180-263">Use standard Azure access control methods to secure your logs and restrict who can access them.</span></span>
* <span data-ttu-id="bb180-264">Delete logs that you no longer want to keep in your storage account.</span><span class="sxs-lookup"><span data-stu-id="bb180-264">Delete logs that you no longer want to keep in your storage account.</span></span>
* <span data-ttu-id="bb180-265">The retention period for data plane requests that are archived to a Storage account is configured in the portal when the **Log DataPlaneRequests** setting is selected.</span><span class="sxs-lookup"><span data-stu-id="bb180-265">The retention period for data plane requests that are archived to a Storage account is configured in the portal when the **Log DataPlaneRequests** setting is selected.</span></span> <span data-ttu-id="bb180-266">To change that setting, see [Turn on logging in the Azure portal](#turn-on-logging-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="bb180-266">To change that setting, see [Turn on logging in the Azure portal](#turn-on-logging-in-the-azure-portal).</span></span>


<a id="#view-in-loganalytics"></a>
## <a name="view-logs-in-log-analytics"></a><span data-ttu-id="bb180-267">View logs in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="bb180-267">View logs in Log Analytics</span></span>

<span data-ttu-id="bb180-268">If you selected the **Send to Log Analytics** option when you turned on diagnostic logging, diagnostic data from your container is forwarded to Log Analytics within two hours.</span><span class="sxs-lookup"><span data-stu-id="bb180-268">If you selected the **Send to Log Analytics** option when you turned on diagnostic logging, diagnostic data from your container is forwarded to Log Analytics within two hours.</span></span> <span data-ttu-id="bb180-269">When you look at Log Analytics immediately after you turn on logging, you won't see any data.</span><span class="sxs-lookup"><span data-stu-id="bb180-269">When you look at Log Analytics immediately after you turn on logging, you won't see any data.</span></span> <span data-ttu-id="bb180-270">Just wait two hours and try again.</span><span class="sxs-lookup"><span data-stu-id="bb180-270">Just wait two hours and try again.</span></span> 

<span data-ttu-id="bb180-271">Before you view your logs, check and see if your Log Analytics workspace has been upgraded to use the new Log Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="bb180-271">Before you view your logs, check and see if your Log Analytics workspace has been upgraded to use the new Log Analytics query language.</span></span> <span data-ttu-id="bb180-272">To check, open the [Azure portal](https://portal.azure.com), select **Log Analytics** on the far left, then select the workspace name as shown in the next image.</span><span class="sxs-lookup"><span data-stu-id="bb180-272">To check, open the [Azure portal](https://portal.azure.com), select **Log Analytics** on the far left, then select the workspace name as shown in the next image.</span></span> <span data-ttu-id="bb180-273">The **OMS Workspace** page is displayed:</span><span class="sxs-lookup"><span data-stu-id="bb180-273">The **OMS Workspace** page is displayed:</span></span>

![Log Analytics in the Azure portal](./media/logging/azure-portal.png)

<span data-ttu-id="bb180-275">If you see the following message on the **OMS Workspace** page, your workspace hasn't been upgraded to use the new language.</span><span class="sxs-lookup"><span data-stu-id="bb180-275">If you see the following message on the **OMS Workspace** page, your workspace hasn't been upgraded to use the new language.</span></span> <span data-ttu-id="bb180-276">For more information on how to upgrade to the new query language, see [Upgrade your Azure Log Analytics workspace to new log search](../log-analytics/log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="bb180-276">For more information on how to upgrade to the new query language, see [Upgrade your Azure Log Analytics workspace to new log search](../log-analytics/log-analytics-log-search-upgrade.md).</span></span> 

![Log Analytics upgrade message](./media/logging/upgrade-notification.png)

<span data-ttu-id="bb180-278">To view your diagnostic data in Log Analytics, open the **Log Search** page from the left menu or the **Management** area of the page, as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="bb180-278">To view your diagnostic data in Log Analytics, open the **Log Search** page from the left menu or the **Management** area of the page, as shown in the following image:</span></span>

![Log search options in the Azure portal](./media/logging/log-analytics-open-log-search.png)

<span data-ttu-id="bb180-280">Now that you've enabled data collection, run the following log search example by using the new query language to see the 10 most recent logs `AzureDiagnostics | take 10`.</span><span class="sxs-lookup"><span data-stu-id="bb180-280">Now that you've enabled data collection, run the following log search example by using the new query language to see the 10 most recent logs `AzureDiagnostics | take 10`.</span></span>

![Sample log search for the 10 most recent logs](./media/logging/log-analytics-query.png)

<a id="#queries"></a>
### <a name="queries"></a><span data-ttu-id="bb180-282">Queries</span><span class="sxs-lookup"><span data-stu-id="bb180-282">Queries</span></span>

<span data-ttu-id="bb180-283">Here are some additional queries that you can enter into the **Log search** box to help you monitor your Azure Cosmos DB containers.</span><span class="sxs-lookup"><span data-stu-id="bb180-283">Here are some additional queries that you can enter into the **Log search** box to help you monitor your Azure Cosmos DB containers.</span></span> <span data-ttu-id="bb180-284">These queries work with the [new language](../log-analytics/log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="bb180-284">These queries work with the [new language](../log-analytics/log-analytics-log-search-upgrade.md).</span></span> 

<span data-ttu-id="bb180-285">To learn about the meaning of the data that's returned by each log search, see [Interpret your Azure Cosmos DB logs](#interpret).</span><span class="sxs-lookup"><span data-stu-id="bb180-285">To learn about the meaning of the data that's returned by each log search, see [Interpret your Azure Cosmos DB logs](#interpret).</span></span>

* <span data-ttu-id="bb180-286">To query for all of the diagnostic logs from Azure Cosmos DB for a specified time period:</span><span class="sxs-lookup"><span data-stu-id="bb180-286">To query for all of the diagnostic logs from Azure Cosmos DB for a specified time period:</span></span>

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests"
    ```

* <span data-ttu-id="bb180-287">To query for the 10 most recently logged events:</span><span class="sxs-lookup"><span data-stu-id="bb180-287">To query for the 10 most recently logged events:</span></span>

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | take 10
    ```

* <span data-ttu-id="bb180-288">To query for all operations, grouped by operation type:</span><span class="sxs-lookup"><span data-stu-id="bb180-288">To query for all operations, grouped by operation type:</span></span>

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by OperationName
    ```

* <span data-ttu-id="bb180-289">To query for all operations, grouped by **Resource**:</span><span class="sxs-lookup"><span data-stu-id="bb180-289">To query for all operations, grouped by **Resource**:</span></span>

    ```
    AzureActivity | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by Resource
    ```

* <span data-ttu-id="bb180-290">To query for all user activity, grouped by resource:</span><span class="sxs-lookup"><span data-stu-id="bb180-290">To query for all user activity, grouped by resource:</span></span>

    ```
    AzureActivity | where Caller == "test@company.com" and ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by Resource
    ```
    > [!NOTE]
    > <span data-ttu-id="bb180-291">This command is for an activity log, not a diagnostic log.</span><span class="sxs-lookup"><span data-stu-id="bb180-291">This command is for an activity log, not a diagnostic log.</span></span>

* <span data-ttu-id="bb180-292">To query for which operations take longer than 3 milliseconds:</span><span class="sxs-lookup"><span data-stu-id="bb180-292">To query for which operations take longer than 3 milliseconds:</span></span>

    ```
    AzureDiagnostics | where toint(duration_s) > 30000 and ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by clientIpAddress_s, TimeGenerated
    ```

* <span data-ttu-id="bb180-293">To query for which agent is running the operations:</span><span class="sxs-lookup"><span data-stu-id="bb180-293">To query for which agent is running the operations:</span></span>

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by OperationName, userAgent_s
    ```

* <span data-ttu-id="bb180-294">To query for when the long running operations were performed:</span><span class="sxs-lookup"><span data-stu-id="bb180-294">To query for when the long running operations were performed:</span></span>

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | project TimeGenerated , toint(duration_s)/1000 | render timechart
    ```

<span data-ttu-id="bb180-295">For more information about how to use the new Log Search language, see [Understand log searches in Log Analytics](../log-analytics/log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="bb180-295">For more information about how to use the new Log Search language, see [Understand log searches in Log Analytics](../log-analytics/log-analytics-log-search-new.md).</span></span> 

## <a id="interpret"></a><span data-ttu-id="bb180-296">Interpret your logs</span><span class="sxs-lookup"><span data-stu-id="bb180-296">Interpret your logs</span></span>

<span data-ttu-id="bb180-297">Diagnostic data that's stored in Azure Storage and Log Analytics uses a similar schema.</span><span class="sxs-lookup"><span data-stu-id="bb180-297">Diagnostic data that's stored in Azure Storage and Log Analytics uses a similar schema.</span></span> 

<span data-ttu-id="bb180-298">The following table describes the content of each log entry.</span><span class="sxs-lookup"><span data-stu-id="bb180-298">The following table describes the content of each log entry.</span></span>

| <span data-ttu-id="bb180-299">Azure Storage field or property</span><span class="sxs-lookup"><span data-stu-id="bb180-299">Azure Storage field or property</span></span> | <span data-ttu-id="bb180-300">Log Analytics property</span><span class="sxs-lookup"><span data-stu-id="bb180-300">Log Analytics property</span></span> | <span data-ttu-id="bb180-301">Description</span><span class="sxs-lookup"><span data-stu-id="bb180-301">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb180-302">**time**</span><span class="sxs-lookup"><span data-stu-id="bb180-302">**time**</span></span> | <span data-ttu-id="bb180-303">**TimeGenerated**</span><span class="sxs-lookup"><span data-stu-id="bb180-303">**TimeGenerated**</span></span> | <span data-ttu-id="bb180-304">The date and time (UTC) when the operation occurred.</span><span class="sxs-lookup"><span data-stu-id="bb180-304">The date and time (UTC) when the operation occurred.</span></span> |
| <span data-ttu-id="bb180-305">**resourceId**</span><span class="sxs-lookup"><span data-stu-id="bb180-305">**resourceId**</span></span> | <span data-ttu-id="bb180-306">**Resource**</span><span class="sxs-lookup"><span data-stu-id="bb180-306">**Resource**</span></span> | <span data-ttu-id="bb180-307">The Azure Cosmos DB account for which logs are enabled.</span><span class="sxs-lookup"><span data-stu-id="bb180-307">The Azure Cosmos DB account for which logs are enabled.</span></span>|
| <span data-ttu-id="bb180-308">**category**</span><span class="sxs-lookup"><span data-stu-id="bb180-308">**category**</span></span> | <span data-ttu-id="bb180-309">**Category**</span><span class="sxs-lookup"><span data-stu-id="bb180-309">**Category**</span></span> | <span data-ttu-id="bb180-310">For Azure Cosmos DB logs, **DataPlaneRequests** is the only available value.</span><span class="sxs-lookup"><span data-stu-id="bb180-310">For Azure Cosmos DB logs, **DataPlaneRequests** is the only available value.</span></span> |
| <span data-ttu-id="bb180-311">**operationName**</span><span class="sxs-lookup"><span data-stu-id="bb180-311">**operationName**</span></span> | <span data-ttu-id="bb180-312">**OperationName**</span><span class="sxs-lookup"><span data-stu-id="bb180-312">**OperationName**</span></span> | <span data-ttu-id="bb180-313">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="bb180-313">Name of the operation.</span></span> <span data-ttu-id="bb180-314">This value can be any of the following operations: Create, Update, Read, ReadFeed, Delete, Replace, Execute, SqlQuery, Query, JSQuery, Head, HeadFeed, or Upsert.</span><span class="sxs-lookup"><span data-stu-id="bb180-314">This value can be any of the following operations: Create, Update, Read, ReadFeed, Delete, Replace, Execute, SqlQuery, Query, JSQuery, Head, HeadFeed, or Upsert.</span></span>   |
| <span data-ttu-id="bb180-315">**properties**</span><span class="sxs-lookup"><span data-stu-id="bb180-315">**properties**</span></span> | <span data-ttu-id="bb180-316">n/a</span><span class="sxs-lookup"><span data-stu-id="bb180-316">n/a</span></span> | <span data-ttu-id="bb180-317">The contents of this field are described in the rows that follow.</span><span class="sxs-lookup"><span data-stu-id="bb180-317">The contents of this field are described in the rows that follow.</span></span> |
| <span data-ttu-id="bb180-318">**activityId**</span><span class="sxs-lookup"><span data-stu-id="bb180-318">**activityId**</span></span> | <span data-ttu-id="bb180-319">**activityId_g**</span><span class="sxs-lookup"><span data-stu-id="bb180-319">**activityId_g**</span></span> | <span data-ttu-id="bb180-320">The unique GUID for the logged operation.</span><span class="sxs-lookup"><span data-stu-id="bb180-320">The unique GUID for the logged operation.</span></span> |
| <span data-ttu-id="bb180-321">**userAgent**</span><span class="sxs-lookup"><span data-stu-id="bb180-321">**userAgent**</span></span> | <span data-ttu-id="bb180-322">**userAgent_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-322">**userAgent_s**</span></span> | <span data-ttu-id="bb180-323">A string that specifies the client user agent that's performing the request.</span><span class="sxs-lookup"><span data-stu-id="bb180-323">A string that specifies the client user agent that's performing the request.</span></span> <span data-ttu-id="bb180-324">The format is {user agent name}/{version}.</span><span class="sxs-lookup"><span data-stu-id="bb180-324">The format is {user agent name}/{version}.</span></span>|
| <span data-ttu-id="bb180-325">**resourceType**</span><span class="sxs-lookup"><span data-stu-id="bb180-325">**resourceType**</span></span> | <span data-ttu-id="bb180-326">**ResourceType**</span><span class="sxs-lookup"><span data-stu-id="bb180-326">**ResourceType**</span></span> | <span data-ttu-id="bb180-327">The type of the resource accessed.</span><span class="sxs-lookup"><span data-stu-id="bb180-327">The type of the resource accessed.</span></span> <span data-ttu-id="bb180-328">This value can be any of the following resource types: Database, Container, Document, Attachment, User, Permission, StoredProcedure, Trigger, UserDefinedFunction, or Offer.</span><span class="sxs-lookup"><span data-stu-id="bb180-328">This value can be any of the following resource types: Database, Container, Document, Attachment, User, Permission, StoredProcedure, Trigger, UserDefinedFunction, or Offer.</span></span> |
| <span data-ttu-id="bb180-329">**statusCode**</span><span class="sxs-lookup"><span data-stu-id="bb180-329">**statusCode**</span></span> | <span data-ttu-id="bb180-330">**statusCode_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-330">**statusCode_s**</span></span> | <span data-ttu-id="bb180-331">The response status of the operation.</span><span class="sxs-lookup"><span data-stu-id="bb180-331">The response status of the operation.</span></span> |
| <span data-ttu-id="bb180-332">**requestResourceId**</span><span class="sxs-lookup"><span data-stu-id="bb180-332">**requestResourceId**</span></span> | <span data-ttu-id="bb180-333">**ResourceId**</span><span class="sxs-lookup"><span data-stu-id="bb180-333">**ResourceId**</span></span> | <span data-ttu-id="bb180-334">The resourceId that pertains to the request.</span><span class="sxs-lookup"><span data-stu-id="bb180-334">The resourceId that pertains to the request.</span></span> <span data-ttu-id="bb180-335">The value may point to databaseRid, collectionRid, or documentRid depending on the operation performed.</span><span class="sxs-lookup"><span data-stu-id="bb180-335">The value may point to databaseRid, collectionRid, or documentRid depending on the operation performed.</span></span>|
| <span data-ttu-id="bb180-336">**clientIpAddress**</span><span class="sxs-lookup"><span data-stu-id="bb180-336">**clientIpAddress**</span></span> | <span data-ttu-id="bb180-337">**clientIpAddress_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-337">**clientIpAddress_s**</span></span> | <span data-ttu-id="bb180-338">The client's IP address.</span><span class="sxs-lookup"><span data-stu-id="bb180-338">The client's IP address.</span></span> |
| <span data-ttu-id="bb180-339">**requestCharge**</span><span class="sxs-lookup"><span data-stu-id="bb180-339">**requestCharge**</span></span> | <span data-ttu-id="bb180-340">**requestCharge_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-340">**requestCharge_s**</span></span> | <span data-ttu-id="bb180-341">The number of RUs that are used by the operation</span><span class="sxs-lookup"><span data-stu-id="bb180-341">The number of RUs that are used by the operation</span></span> |
| <span data-ttu-id="bb180-342">**collectionRid**</span><span class="sxs-lookup"><span data-stu-id="bb180-342">**collectionRid**</span></span> | <span data-ttu-id="bb180-343">**collectionId_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-343">**collectionId_s**</span></span> | <span data-ttu-id="bb180-344">The unique ID for the collection.</span><span class="sxs-lookup"><span data-stu-id="bb180-344">The unique ID for the collection.</span></span>|
| <span data-ttu-id="bb180-345">**duration**</span><span class="sxs-lookup"><span data-stu-id="bb180-345">**duration**</span></span> | <span data-ttu-id="bb180-346">**duration_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-346">**duration_s**</span></span> | <span data-ttu-id="bb180-347">The duration of the operation, in ticks.</span><span class="sxs-lookup"><span data-stu-id="bb180-347">The duration of the operation, in ticks.</span></span> |
| <span data-ttu-id="bb180-348">**requestLength**</span><span class="sxs-lookup"><span data-stu-id="bb180-348">**requestLength**</span></span> | <span data-ttu-id="bb180-349">**requestLength_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-349">**requestLength_s**</span></span> | <span data-ttu-id="bb180-350">The length of the request, in bytes.</span><span class="sxs-lookup"><span data-stu-id="bb180-350">The length of the request, in bytes.</span></span> |
| <span data-ttu-id="bb180-351">**responseLength**</span><span class="sxs-lookup"><span data-stu-id="bb180-351">**responseLength**</span></span> | <span data-ttu-id="bb180-352">**responseLength_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-352">**responseLength_s**</span></span> | <span data-ttu-id="bb180-353">The length of the response, in bytes.</span><span class="sxs-lookup"><span data-stu-id="bb180-353">The length of the response, in bytes.</span></span>|
| <span data-ttu-id="bb180-354">**resourceTokenUserRid**</span><span class="sxs-lookup"><span data-stu-id="bb180-354">**resourceTokenUserRid**</span></span> | <span data-ttu-id="bb180-355">**resourceTokenUserRid_s**</span><span class="sxs-lookup"><span data-stu-id="bb180-355">**resourceTokenUserRid_s**</span></span> | <span data-ttu-id="bb180-356">This value is non-empty when [resource tokens](https://docs.microsoft.com/azure/cosmos-db/secure-access-to-data#resource-tokens) are used for authentication.</span><span class="sxs-lookup"><span data-stu-id="bb180-356">This value is non-empty when [resource tokens](https://docs.microsoft.com/azure/cosmos-db/secure-access-to-data#resource-tokens) are used for authentication.</span></span> <span data-ttu-id="bb180-357">The value points to the resource ID of the user.</span><span class="sxs-lookup"><span data-stu-id="bb180-357">The value points to the resource ID of the user.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bb180-358">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb180-358">Next steps</span></span>

- <span data-ttu-id="bb180-359">To understand how to enable logging, and also the metrics and log categories that are supported by the various Azure services, read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles.</span><span class="sxs-lookup"><span data-stu-id="bb180-359">To understand how to enable logging, and also the metrics and log categories that are supported by the various Azure services, read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles.</span></span>
- <span data-ttu-id="bb180-360">Read these articles to learn about event hubs:</span><span class="sxs-lookup"><span data-stu-id="bb180-360">Read these articles to learn about event hubs:</span></span>
   - [<span data-ttu-id="bb180-361">What is Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="bb180-361">What is Azure Event Hubs?</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
   - [<span data-ttu-id="bb180-362">Get started with Event Hubs</span><span class="sxs-lookup"><span data-stu-id="bb180-362">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="bb180-363">Read [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-quickstart-blobs-dotnet.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="bb180-363">Read [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-quickstart-blobs-dotnet.md#download-blobs).</span></span>
- <span data-ttu-id="bb180-364">Read [Understand log searches in Log Analytics](../log-analytics/log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="bb180-364">Read [Understand log searches in Log Analytics](../log-analytics/log-analytics-log-search-new.md).</span></span>
