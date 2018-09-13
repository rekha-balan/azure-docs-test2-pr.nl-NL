---
title: Diganostic logging for Azure Analysis Services | Microsoft Docs
description: Learn about setting up diagnostic logging for Azure Analysis Services.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: d19e45710aca3e1e18be6c4529da6474a97bc59f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858051"
---
# <a name="setup-diagnostic-logging"></a><span data-ttu-id="6d5fb-103">Setup diagnostic logging</span><span class="sxs-lookup"><span data-stu-id="6d5fb-103">Setup diagnostic logging</span></span>

<span data-ttu-id="6d5fb-104">An important part of any Analysis Services solution is monitoring how your servers are performing.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-104">An important part of any Analysis Services solution is monitoring how your servers are performing.</span></span> <span data-ttu-id="6d5fb-105">With [Azure resource diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md), you can monitor and send logs to [Azure Storage](https://azure.microsoft.com/services/storage/), stream them to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), and export them to [Log Analytics](https://azure.microsoft.com/services/log-analytics/), a service of [Azure](https://www.microsoft.com/cloud-platform/operations-management-suite).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-105">With [Azure resource diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md), you can monitor and send logs to [Azure Storage](https://azure.microsoft.com/services/storage/), stream them to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), and export them to [Log Analytics](https://azure.microsoft.com/services/log-analytics/), a service of [Azure](https://www.microsoft.com/cloud-platform/operations-management-suite).</span></span> 

![Diagnostic logging to Storage, Event Hubs, or Log Analytics](./media/analysis-services-logging/aas-logging-overview.png)


## <a name="whats-logged"></a><span data-ttu-id="6d5fb-107">What's logged?</span><span class="sxs-lookup"><span data-stu-id="6d5fb-107">What's logged?</span></span>

<span data-ttu-id="6d5fb-108">You can select **Engine**, **Service**, and **Metrics** categories.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-108">You can select **Engine**, **Service**, and **Metrics** categories.</span></span>

### <a name="engine"></a><span data-ttu-id="6d5fb-109">Engine</span><span class="sxs-lookup"><span data-stu-id="6d5fb-109">Engine</span></span>

<span data-ttu-id="6d5fb-110">Selecting **Engine** logs all [xEvents](https://docs.microsoft.com/sql/analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-110">Selecting **Engine** logs all [xEvents](https://docs.microsoft.com/sql/analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events).</span></span> <span data-ttu-id="6d5fb-111">You cannot select individual events.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-111">You cannot select individual events.</span></span> 

|<span data-ttu-id="6d5fb-112">XEvent categories</span><span class="sxs-lookup"><span data-stu-id="6d5fb-112">XEvent categories</span></span> |<span data-ttu-id="6d5fb-113">Event name</span><span class="sxs-lookup"><span data-stu-id="6d5fb-113">Event name</span></span>  |
|---------|---------|
|<span data-ttu-id="6d5fb-114">Security Audit</span><span class="sxs-lookup"><span data-stu-id="6d5fb-114">Security Audit</span></span>    |   <span data-ttu-id="6d5fb-115">Audit Login</span><span class="sxs-lookup"><span data-stu-id="6d5fb-115">Audit Login</span></span>      |
|<span data-ttu-id="6d5fb-116">Security Audit</span><span class="sxs-lookup"><span data-stu-id="6d5fb-116">Security Audit</span></span>    |   <span data-ttu-id="6d5fb-117">Audit Logout</span><span class="sxs-lookup"><span data-stu-id="6d5fb-117">Audit Logout</span></span>      |
|<span data-ttu-id="6d5fb-118">Security Audit</span><span class="sxs-lookup"><span data-stu-id="6d5fb-118">Security Audit</span></span>    |   <span data-ttu-id="6d5fb-119">Audit Server Starts And Stops</span><span class="sxs-lookup"><span data-stu-id="6d5fb-119">Audit Server Starts And Stops</span></span>      |
|<span data-ttu-id="6d5fb-120">Progress Reports</span><span class="sxs-lookup"><span data-stu-id="6d5fb-120">Progress Reports</span></span>     |   <span data-ttu-id="6d5fb-121">Progress Report Begin</span><span class="sxs-lookup"><span data-stu-id="6d5fb-121">Progress Report Begin</span></span>      |
|<span data-ttu-id="6d5fb-122">Progress Reports</span><span class="sxs-lookup"><span data-stu-id="6d5fb-122">Progress Reports</span></span>     |   <span data-ttu-id="6d5fb-123">Progress Report End</span><span class="sxs-lookup"><span data-stu-id="6d5fb-123">Progress Report End</span></span>      |
|<span data-ttu-id="6d5fb-124">Progress Reports</span><span class="sxs-lookup"><span data-stu-id="6d5fb-124">Progress Reports</span></span>     |   <span data-ttu-id="6d5fb-125">Progress Report Current</span><span class="sxs-lookup"><span data-stu-id="6d5fb-125">Progress Report Current</span></span>      |
|<span data-ttu-id="6d5fb-126">Queries</span><span class="sxs-lookup"><span data-stu-id="6d5fb-126">Queries</span></span>     |  <span data-ttu-id="6d5fb-127">Query Begin</span><span class="sxs-lookup"><span data-stu-id="6d5fb-127">Query Begin</span></span>       |
|<span data-ttu-id="6d5fb-128">Queries</span><span class="sxs-lookup"><span data-stu-id="6d5fb-128">Queries</span></span>     |   <span data-ttu-id="6d5fb-129">Query End</span><span class="sxs-lookup"><span data-stu-id="6d5fb-129">Query End</span></span>      |
|<span data-ttu-id="6d5fb-130">Commands</span><span class="sxs-lookup"><span data-stu-id="6d5fb-130">Commands</span></span>     |  <span data-ttu-id="6d5fb-131">Command Begin</span><span class="sxs-lookup"><span data-stu-id="6d5fb-131">Command Begin</span></span>       |
|<span data-ttu-id="6d5fb-132">Commands</span><span class="sxs-lookup"><span data-stu-id="6d5fb-132">Commands</span></span>     |  <span data-ttu-id="6d5fb-133">Command End</span><span class="sxs-lookup"><span data-stu-id="6d5fb-133">Command End</span></span>       |
|<span data-ttu-id="6d5fb-134">Errors & Warnings</span><span class="sxs-lookup"><span data-stu-id="6d5fb-134">Errors & Warnings</span></span>     |   <span data-ttu-id="6d5fb-135">Error</span><span class="sxs-lookup"><span data-stu-id="6d5fb-135">Error</span></span>      |
|<span data-ttu-id="6d5fb-136">Discover</span><span class="sxs-lookup"><span data-stu-id="6d5fb-136">Discover</span></span>     |   <span data-ttu-id="6d5fb-137">Discover End</span><span class="sxs-lookup"><span data-stu-id="6d5fb-137">Discover End</span></span>      |
|<span data-ttu-id="6d5fb-138">Notification</span><span class="sxs-lookup"><span data-stu-id="6d5fb-138">Notification</span></span>     |    <span data-ttu-id="6d5fb-139">Notification</span><span class="sxs-lookup"><span data-stu-id="6d5fb-139">Notification</span></span>     |
|<span data-ttu-id="6d5fb-140">Session</span><span class="sxs-lookup"><span data-stu-id="6d5fb-140">Session</span></span>     |  <span data-ttu-id="6d5fb-141">Session Initialize</span><span class="sxs-lookup"><span data-stu-id="6d5fb-141">Session Initialize</span></span>       |
|<span data-ttu-id="6d5fb-142">Locks</span><span class="sxs-lookup"><span data-stu-id="6d5fb-142">Locks</span></span>    |  <span data-ttu-id="6d5fb-143">Deadlock</span><span class="sxs-lookup"><span data-stu-id="6d5fb-143">Deadlock</span></span>       |
|<span data-ttu-id="6d5fb-144">Query Processing</span><span class="sxs-lookup"><span data-stu-id="6d5fb-144">Query Processing</span></span>     |   <span data-ttu-id="6d5fb-145">VertiPaq SE Query Begin</span><span class="sxs-lookup"><span data-stu-id="6d5fb-145">VertiPaq SE Query Begin</span></span>      |
|<span data-ttu-id="6d5fb-146">Query Processing</span><span class="sxs-lookup"><span data-stu-id="6d5fb-146">Query Processing</span></span>     |   <span data-ttu-id="6d5fb-147">VertiPaq SE Query End</span><span class="sxs-lookup"><span data-stu-id="6d5fb-147">VertiPaq SE Query End</span></span>      |
|<span data-ttu-id="6d5fb-148">Query Processing</span><span class="sxs-lookup"><span data-stu-id="6d5fb-148">Query Processing</span></span>     |   <span data-ttu-id="6d5fb-149">VertiPaq SE Query Cache Match</span><span class="sxs-lookup"><span data-stu-id="6d5fb-149">VertiPaq SE Query Cache Match</span></span>      |
|<span data-ttu-id="6d5fb-150">Query Processing</span><span class="sxs-lookup"><span data-stu-id="6d5fb-150">Query Processing</span></span>     |   <span data-ttu-id="6d5fb-151">Direct Query Begin</span><span class="sxs-lookup"><span data-stu-id="6d5fb-151">Direct Query Begin</span></span>      |
|<span data-ttu-id="6d5fb-152">Query Processing</span><span class="sxs-lookup"><span data-stu-id="6d5fb-152">Query Processing</span></span>     |  <span data-ttu-id="6d5fb-153">Direct Query End</span><span class="sxs-lookup"><span data-stu-id="6d5fb-153">Direct Query End</span></span>       |

### <a name="service"></a><span data-ttu-id="6d5fb-154">Service</span><span class="sxs-lookup"><span data-stu-id="6d5fb-154">Service</span></span>

|<span data-ttu-id="6d5fb-155">Operation name</span><span class="sxs-lookup"><span data-stu-id="6d5fb-155">Operation name</span></span>  |<span data-ttu-id="6d5fb-156">Occurs when</span><span class="sxs-lookup"><span data-stu-id="6d5fb-156">Occurs when</span></span>  |
|---------|---------|
|<span data-ttu-id="6d5fb-157">ResumeServer</span><span class="sxs-lookup"><span data-stu-id="6d5fb-157">ResumeServer</span></span>     |    <span data-ttu-id="6d5fb-158">Resume a server</span><span class="sxs-lookup"><span data-stu-id="6d5fb-158">Resume a server</span></span>     |
|<span data-ttu-id="6d5fb-159">SuspendServer</span><span class="sxs-lookup"><span data-stu-id="6d5fb-159">SuspendServer</span></span>    |   <span data-ttu-id="6d5fb-160">Pause a server</span><span class="sxs-lookup"><span data-stu-id="6d5fb-160">Pause a server</span></span>      |
|<span data-ttu-id="6d5fb-161">DeleteServer</span><span class="sxs-lookup"><span data-stu-id="6d5fb-161">DeleteServer</span></span>     |    <span data-ttu-id="6d5fb-162">Delete a server</span><span class="sxs-lookup"><span data-stu-id="6d5fb-162">Delete a server</span></span>     |
|<span data-ttu-id="6d5fb-163">RestartServer</span><span class="sxs-lookup"><span data-stu-id="6d5fb-163">RestartServer</span></span>    |     <span data-ttu-id="6d5fb-164">User restarts a server through SSMS or PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d5fb-164">User restarts a server through SSMS or PowerShell</span></span>    |
|<span data-ttu-id="6d5fb-165">GetServerLogFiles</span><span class="sxs-lookup"><span data-stu-id="6d5fb-165">GetServerLogFiles</span></span>    |    <span data-ttu-id="6d5fb-166">User exports server log through PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d5fb-166">User exports server log through PowerShell</span></span>     |
|<span data-ttu-id="6d5fb-167">ExportModel</span><span class="sxs-lookup"><span data-stu-id="6d5fb-167">ExportModel</span></span>     |   <span data-ttu-id="6d5fb-168">User exports a model in the portal by using Open in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d5fb-168">User exports a model in the portal by using Open in Visual Studio</span></span>     |

### <a name="all-metrics"></a><span data-ttu-id="6d5fb-169">All metrics</span><span class="sxs-lookup"><span data-stu-id="6d5fb-169">All metrics</span></span>

<span data-ttu-id="6d5fb-170">The Metrics category logs the same [Server metrics](analysis-services-monitor.md#server-metrics) displayed in Metrics.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-170">The Metrics category logs the same [Server metrics](analysis-services-monitor.md#server-metrics) displayed in Metrics.</span></span>

## <a name="setup-diagnostics-logging"></a><span data-ttu-id="6d5fb-171">Setup diagnostics logging</span><span class="sxs-lookup"><span data-stu-id="6d5fb-171">Setup diagnostics logging</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6d5fb-172">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6d5fb-172">Azure portal</span></span>

1. <span data-ttu-id="6d5fb-173">In [Azure portal](https://portal.azure.com) > server, click **Diagnostic logs** in the left navigation, and then click **Turn on diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-173">In [Azure portal](https://portal.azure.com) > server, click **Diagnostic logs** in the left navigation, and then click **Turn on diagnostics**.</span></span>

    ![Turn on diagnostic logging for Azure Cosmos DB in the Azure portal](./media/analysis-services-logging/aas-logging-turn-on-diagnostics.png)

2. <span data-ttu-id="6d5fb-175">In **Diagnostic settings**, specify the following options:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-175">In **Diagnostic settings**, specify the following options:</span></span> 

    * <span data-ttu-id="6d5fb-176">**Name**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-176">**Name**.</span></span> <span data-ttu-id="6d5fb-177">Enter a name for the logs to create.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-177">Enter a name for the logs to create.</span></span>

    * <span data-ttu-id="6d5fb-178">**Archive to a storage account**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-178">**Archive to a storage account**.</span></span> <span data-ttu-id="6d5fb-179">To use this option, you need an existing storage account to connect to.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-179">To use this option, you need an existing storage account to connect to.</span></span> <span data-ttu-id="6d5fb-180">See [Create a storage account](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-180">See [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="6d5fb-181">Follow the instructions to create a Resource Manager, general-purpose account, then select your storage account by returning to this page in the portal.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-181">Follow the instructions to create a Resource Manager, general-purpose account, then select your storage account by returning to this page in the portal.</span></span> <span data-ttu-id="6d5fb-182">It may take a few minutes for newly created storage accounts to appear in the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-182">It may take a few minutes for newly created storage accounts to appear in the drop-down menu.</span></span>
    * <span data-ttu-id="6d5fb-183">**Stream to an event hub**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-183">**Stream to an event hub**.</span></span> <span data-ttu-id="6d5fb-184">To use this option, you need an existing Event Hub namespace and event hub to connect to.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-184">To use this option, you need an existing Event Hub namespace and event hub to connect to.</span></span> <span data-ttu-id="6d5fb-185">To learn more, see [Create an Event Hubs namespace and an event hub using the Azure portal](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-185">To learn more, see [Create an Event Hubs namespace and an event hub using the Azure portal](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="6d5fb-186">Then return to this page in the portal to select the Event Hub namespace and policy name.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-186">Then return to this page in the portal to select the Event Hub namespace and policy name.</span></span>
    * <span data-ttu-id="6d5fb-187">**Send to Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-187">**Send to Log Analytics**.</span></span> <span data-ttu-id="6d5fb-188">To use this option, either use an existing workspace or create a new Log Analytics workspace by following the steps to [create a new workspace](../log-analytics/log-analytics-quick-collect-azurevm.md#create-a-workspace) in the portal.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-188">To use this option, either use an existing workspace or create a new Log Analytics workspace by following the steps to [create a new workspace](../log-analytics/log-analytics-quick-collect-azurevm.md#create-a-workspace) in the portal.</span></span> <span data-ttu-id="6d5fb-189">For more information on viewing your logs in Log Analytics, see [View logs in Log Analytics](#view-in-loganalytics).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-189">For more information on viewing your logs in Log Analytics, see [View logs in Log Analytics](#view-in-loganalytics).</span></span>

    * <span data-ttu-id="6d5fb-190">**Engine**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-190">**Engine**.</span></span> <span data-ttu-id="6d5fb-191">Select this option to log xEvents.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-191">Select this option to log xEvents.</span></span> <span data-ttu-id="6d5fb-192">If you're archiving to a storage account, you can select the retention period for the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-192">If you're archiving to a storage account, you can select the retention period for the diagnostic logs.</span></span> <span data-ttu-id="6d5fb-193">Logs are autodeleted after the retention period expires.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-193">Logs are autodeleted after the retention period expires.</span></span>
    * <span data-ttu-id="6d5fb-194">**Service**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-194">**Service**.</span></span> <span data-ttu-id="6d5fb-195">Select this option to log service level events.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-195">Select this option to log service level events.</span></span> <span data-ttu-id="6d5fb-196">If you are archiving to a storage account, you can select the retention period for the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-196">If you are archiving to a storage account, you can select the retention period for the diagnostic logs.</span></span> <span data-ttu-id="6d5fb-197">Logs are autodeleted after the retention period expires.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-197">Logs are autodeleted after the retention period expires.</span></span>
    * <span data-ttu-id="6d5fb-198">**Metrics**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-198">**Metrics**.</span></span> <span data-ttu-id="6d5fb-199">Select this option to store verbose data in [Metrics](analysis-services-monitor.md#server-metrics).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-199">Select this option to store verbose data in [Metrics](analysis-services-monitor.md#server-metrics).</span></span> <span data-ttu-id="6d5fb-200">If you are archiving to a storage account, you can select the retention period for the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-200">If you are archiving to a storage account, you can select the retention period for the diagnostic logs.</span></span> <span data-ttu-id="6d5fb-201">Logs are autodeleted after the retention period expires.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-201">Logs are autodeleted after the retention period expires.</span></span>

3. <span data-ttu-id="6d5fb-202">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-202">Click **Save**.</span></span>

    <span data-ttu-id="6d5fb-203">If you receive an error that says "Failed to update diagnostics for \<workspace name>.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-203">If you receive an error that says "Failed to update diagnostics for \<workspace name>.</span></span> <span data-ttu-id="6d5fb-204">The subscription \<subscription id> is not registered to use microsoft.insights."</span><span class="sxs-lookup"><span data-stu-id="6d5fb-204">The subscription \<subscription id> is not registered to use microsoft.insights."</span></span> <span data-ttu-id="6d5fb-205">follow the [Troubleshoot Azure Diagnostics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage) instructions to register the account, then retry this procedure.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-205">follow the [Troubleshoot Azure Diagnostics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage) instructions to register the account, then retry this procedure.</span></span>

    <span data-ttu-id="6d5fb-206">If you want to change how your diagnostic logs are saved at any point in the future, you can return to this page to modify settings.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-206">If you want to change how your diagnostic logs are saved at any point in the future, you can return to this page to modify settings.</span></span>

### <a name="powershell"></a><span data-ttu-id="6d5fb-207">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d5fb-207">PowerShell</span></span>

<span data-ttu-id="6d5fb-208">Here are the basic commands to get you going.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-208">Here are the basic commands to get you going.</span></span> <span data-ttu-id="6d5fb-209">If you want step-by-step help on setting up logging to a storage account by using PowerShell, see the tutorial later in this article.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-209">If you want step-by-step help on setting up logging to a storage account by using PowerShell, see the tutorial later in this article.</span></span>

<span data-ttu-id="6d5fb-210">To enable metrics and diagnostics logging by using PowerShell, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-210">To enable metrics and diagnostics logging by using PowerShell, use the following commands:</span></span>

- <span data-ttu-id="6d5fb-211">To enable storage of diagnostics logs in a storage account, use this command:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-211">To enable storage of diagnostics logs in a storage account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="6d5fb-212">The storage account ID is the resource ID for the storage account where you want to send the logs.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-212">The storage account ID is the resource ID for the storage account where you want to send the logs.</span></span>

- <span data-ttu-id="6d5fb-213">To enable streaming of diagnostics logs to an event hub, use this command:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-213">To enable streaming of diagnostics logs to an event hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="6d5fb-214">The Azure Service Bus rule ID is a string with this format:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-214">The Azure Service Bus rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="6d5fb-215">To enable sending diagnostics logs to a Log Analytics workspace, use this command:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-215">To enable sending diagnostics logs to a Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="6d5fb-216">You can obtain the resource ID of your Log Analytics workspace by using the following command:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-216">You can obtain the resource ID of your Log Analytics workspace by using the following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="6d5fb-217">You can combine these parameters to enable multiple output options.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-217">You can combine these parameters to enable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="6d5fb-218">REST API</span><span class="sxs-lookup"><span data-stu-id="6d5fb-218">REST API</span></span>

<span data-ttu-id="6d5fb-219">Learn how to [change diagnostics settings by using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-219">Learn how to [change diagnostics settings by using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="6d5fb-220">Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="6d5fb-220">Resource Manager template</span></span>

<span data-ttu-id="6d5fb-221">Learn how to [enable diagnostics settings at resource creation by using a Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-221">Learn how to [enable diagnostics settings at resource creation by using a Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="manage-your-logs"></a><span data-ttu-id="6d5fb-222">Manage your logs</span><span class="sxs-lookup"><span data-stu-id="6d5fb-222">Manage your logs</span></span>

<span data-ttu-id="6d5fb-223">Logs are typically available within a couple hours of setting up logging.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-223">Logs are typically available within a couple hours of setting up logging.</span></span> <span data-ttu-id="6d5fb-224">It's up to you to manage your logs in your storage account:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-224">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="6d5fb-225">Use standard Azure access control methods to secure your logs by restricting who can access them.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-225">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="6d5fb-226">Delete logs that you no longer want to keep in your storage account.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-226">Delete logs that you no longer want to keep in your storage account.</span></span>
* <span data-ttu-id="6d5fb-227">Be sure to set a retention period for so old logs are deleted from your storage account.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-227">Be sure to set a retention period for so old logs are deleted from your storage account.</span></span>

## <a name="view-logs-in-log-analytics"></a><span data-ttu-id="6d5fb-228">View logs in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6d5fb-228">View logs in Log Analytics</span></span>

<span data-ttu-id="6d5fb-229">Metrics and server events are integrated with xEvents in Log Analytics for side-by-side analysis.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-229">Metrics and server events are integrated with xEvents in Log Analytics for side-by-side analysis.</span></span> <span data-ttu-id="6d5fb-230">Log Analytics can also be configured to receive events from other Azure services providing a holistic view of diagnostic logging data across your architecture.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-230">Log Analytics can also be configured to receive events from other Azure services providing a holistic view of diagnostic logging data across your architecture.</span></span>

<span data-ttu-id="6d5fb-231">To view your diagnostic data in Log Analytics, open the Log Search page from the left menu or the Management area, as shown below.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-231">To view your diagnostic data in Log Analytics, open the Log Search page from the left menu or the Management area, as shown below.</span></span>

![Log Search options in the Azure portal](./media/analysis-services-logging/aas-logging-open-log-search.png)

<span data-ttu-id="6d5fb-233">Now that you've enabled data collection, in **Log Search**, click **All collected data**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-233">Now that you've enabled data collection, in **Log Search**, click **All collected data**.</span></span>

<span data-ttu-id="6d5fb-234">In **Type**, click **AzureDiagnostics**, and then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-234">In **Type**, click **AzureDiagnostics**, and then click **Apply**.</span></span> <span data-ttu-id="6d5fb-235">AzureDiagnostics includes Engine and Service events.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-235">AzureDiagnostics includes Engine and Service events.</span></span> <span data-ttu-id="6d5fb-236">Notice a Log Analytics query is created on-the-fly.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-236">Notice a Log Analytics query is created on-the-fly.</span></span> <span data-ttu-id="6d5fb-237">The EventClass\_s field contains xEvent names, which may look familiar if you've used xEvents for on-premises logging.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-237">The EventClass\_s field contains xEvent names, which may look familiar if you've used xEvents for on-premises logging.</span></span>

<span data-ttu-id="6d5fb-238">Click **EventClass\_s** or one of the event names and Log Analytics continues constructing a query.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-238">Click **EventClass\_s** or one of the event names and Log Analytics continues constructing a query.</span></span> <span data-ttu-id="6d5fb-239">Be sure to save your queries to reuse later.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-239">Be sure to save your queries to reuse later.</span></span>

<span data-ttu-id="6d5fb-240">Be sure to see Log Analytics, which provides a website with enhanced query, dashboarding, and alerting capabilities on collected data.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-240">Be sure to see Log Analytics, which provides a website with enhanced query, dashboarding, and alerting capabilities on collected data.</span></span>

### <a name="queries"></a><span data-ttu-id="6d5fb-241">Queries</span><span class="sxs-lookup"><span data-stu-id="6d5fb-241">Queries</span></span>

<span data-ttu-id="6d5fb-242">There are hundreds of queries you can use.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-242">There are hundreds of queries you can use.</span></span> <span data-ttu-id="6d5fb-243">Here are a few to get you started.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-243">Here are a few to get you started.</span></span>
<span data-ttu-id="6d5fb-244">To learn more about using the new Log Search query language, see [Understanding log searches in Log Analytics](../log-analytics/log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-244">To learn more about using the new Log Search query language, see [Understanding log searches in Log Analytics](../log-analytics/log-analytics-log-search-new.md).</span></span> 

* <span data-ttu-id="6d5fb-245">Query return queries submitted to Azure Analysis Services that took over five minutes (300,000 milliseconds) to complete.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-245">Query return queries submitted to Azure Analysis Services that took over five minutes (300,000 milliseconds) to complete.</span></span>

    ```
    search * | where ( Type == "AzureDiagnostics" ) | where ( EventClass_s == "QUERY_END" ) | where toint(Duration_s) > 300000
    ```

* <span data-ttu-id="6d5fb-246">Identify scale out replicas.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-246">Identify scale out replicas.</span></span>

    ```
    search * | summarize count() by ServerName_s
    ```
    <span data-ttu-id="6d5fb-247">When using scale-out, you can identify read-only replicas because the ServerName\_s field values have the replica instance number appended to the name.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-247">When using scale-out, you can identify read-only replicas because the ServerName\_s field values have the replica instance number appended to the name.</span></span> <span data-ttu-id="6d5fb-248">The resource field contains the Azure resource name, which matches the server name that the users see.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-248">The resource field contains the Azure resource name, which matches the server name that the users see.</span></span> <span data-ttu-id="6d5fb-249">The IsQueryScaleoutReadonlyInstance_s field equals true for replicas.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-249">The IsQueryScaleoutReadonlyInstance_s field equals true for replicas.</span></span>



> [!TIP]
> <span data-ttu-id="6d5fb-250">Have a great Log Analytics query you want to share?</span><span class="sxs-lookup"><span data-stu-id="6d5fb-250">Have a great Log Analytics query you want to share?</span></span> <span data-ttu-id="6d5fb-251">If you have a GitHub account, you can add it to this article.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-251">If you have a GitHub account, you can add it to this article.</span></span> <span data-ttu-id="6d5fb-252">Just click **Edit** at the top-right of this page.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-252">Just click **Edit** at the top-right of this page.</span></span>


## <a name="tutorial---turn-on-logging-by-using-powershell"></a><span data-ttu-id="6d5fb-253">Tutorial - Turn on logging by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d5fb-253">Tutorial - Turn on logging by using PowerShell</span></span>
<span data-ttu-id="6d5fb-254">In this quick tutorial, you create a storage account in the same subscription and resource group as your Analysis Service server.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-254">In this quick tutorial, you create a storage account in the same subscription and resource group as your Analysis Service server.</span></span> <span data-ttu-id="6d5fb-255">You then use Set-AzureRmDiagnosticSetting to turn on diagnostics logging, sending output to the new storage account.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-255">You then use Set-AzureRmDiagnosticSetting to turn on diagnostics logging, sending output to the new storage account.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6d5fb-256">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6d5fb-256">Prerequisites</span></span>
<span data-ttu-id="6d5fb-257">To complete this tutorial, you must have the following resources:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-257">To complete this tutorial, you must have the following resources:</span></span>

* <span data-ttu-id="6d5fb-258">An existing Azure Analysis Services server.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-258">An existing Azure Analysis Services server.</span></span> <span data-ttu-id="6d5fb-259">For instructions on creating a server resource, see [Create a server in Azure portal](analysis-services-create-server.md), or [Create an Azure Analysis Services server by using PowerShell](analysis-services-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-259">For instructions on creating a server resource, see [Create a server in Azure portal](analysis-services-create-server.md), or [Create an Azure Analysis Services server by using PowerShell](analysis-services-create-powershell.md).</span></span>

### <a name="aconnect-to-your-subscriptions"></a><span data-ttu-id="6d5fb-260"></a>Connect to your subscriptions</span><span class="sxs-lookup"><span data-stu-id="6d5fb-260"></a>Connect to your subscriptions</span></span>

<span data-ttu-id="6d5fb-261">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-261">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

```powershell
Connect-AzureRmAccount
```

<span data-ttu-id="6d5fb-262">In the pop-up browser window, enter your Azure account user name and password.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-262">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="6d5fb-263">Azure PowerShell gets all the subscriptions that are associated with this account and by default, uses the first one.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-263">Azure PowerShell gets all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="6d5fb-264">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-264">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="6d5fb-265">Type the following to see the subscriptions for your account:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-265">Type the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6d5fb-266">Then, to specify the subscription that's associated with the Azure Analysis Services account you are logging, type:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-266">Then, to specify the subscription that's associated with the Azure Analysis Services account you are logging, type:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscription ID>
```

> [!NOTE]
> <span data-ttu-id="6d5fb-267">If you have multiple subscriptions associated with your account, it is important to specify the subscription.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-267">If you have multiple subscriptions associated with your account, it is important to specify the subscription.</span></span>
>
>

### <a name="create-a-new-storage-account-for-your-logs"></a><span data-ttu-id="6d5fb-268">Create a new storage account for your logs</span><span class="sxs-lookup"><span data-stu-id="6d5fb-268">Create a new storage account for your logs</span></span>

<span data-ttu-id="6d5fb-269">You can use an existing storage account for your logs, provided it's in the same subscription as your server.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-269">You can use an existing storage account for your logs, provided it's in the same subscription as your server.</span></span> <span data-ttu-id="6d5fb-270">For this tutorial you create a new storage account dedicated to Analysis Services logs.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-270">For this tutorial you create a new storage account dedicated to Analysis Services logs.</span></span> <span data-ttu-id="6d5fb-271">To make it easy, you're storing the storage account details in a variable named **sa**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-271">To make it easy, you're storing the storage account details in a variable named **sa**.</span></span>

<span data-ttu-id="6d5fb-272">You also use the same resource group as the one that contains your Analysis Services server.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-272">You also use the same resource group as the one that contains your Analysis Services server.</span></span> <span data-ttu-id="6d5fb-273">Substitute values for `awsales_resgroup`, `awsaleslogs`, and `West Central US` with your own values:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-273">Substitute values for `awsales_resgroup`, `awsaleslogs`, and `West Central US` with your own values:</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName awsales_resgroup `
-Name awsaleslogs -Type Standard_LRS -Location 'West Central US'
```

### <a name="identify-the-server-account-for-your-logs"></a><span data-ttu-id="6d5fb-274">Identify the server account for your logs</span><span class="sxs-lookup"><span data-stu-id="6d5fb-274">Identify the server account for your logs</span></span>

<span data-ttu-id="6d5fb-275">Set the account name to a variable named **account**, where ResourceName is the name of the account.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-275">Set the account name to a variable named **account**, where ResourceName is the name of the account.</span></span>

```powershell
$account = Get-AzureRmResource -ResourceGroupName awsales_resgroup `
-ResourceName awsales -ResourceType "Microsoft.AnalysisServices/servers"
```

### <a name="enable-logging"></a><span data-ttu-id="6d5fb-276">Enable logging</span><span class="sxs-lookup"><span data-stu-id="6d5fb-276">Enable logging</span></span>

<span data-ttu-id="6d5fb-277">To enable logging, use the Set-AzureRmDiagnosticSetting cmdlet together with the variables for the new storage account, server account, and the category.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-277">To enable logging, use the Set-AzureRmDiagnosticSetting cmdlet together with the variables for the new storage account, server account, and the category.</span></span> <span data-ttu-id="6d5fb-278">Run the following command, setting the **-Enabled** flag to **$true**:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-278">Run the following command, setting the **-Enabled** flag to **$true**:</span></span>

```powershell
Set-AzureRmDiagnosticSetting  -ResourceId $account.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories Engine
```

<span data-ttu-id="6d5fb-279">The output should look something like this:</span><span class="sxs-lookup"><span data-stu-id="6d5fb-279">The output should look something like this:</span></span>

```powershell
StorageAccountId            : 
/subscriptions/a23279b5-xxxx-xxxx-xxxx-47b7c6d423ea/resourceGroups/awsales_resgroup/providers/Microsoft.Storage/storageAccounts/awsaleslogs
ServiceBusRuleId            :
EventHubAuthorizationRuleId :
Metrics                    
    TimeGrain       : PT1M
    Enabled         : False
    RetentionPolicy
    Enabled : False
    Days    : 0


Logs                       
    Category        : Engine
    Enabled         : True
    RetentionPolicy
    Enabled : False
    Days    : 0


    Category        : Service
    Enabled         : False
    RetentionPolicy
    Enabled : False
    Days    : 0


WorkspaceId                 :
Id                          : /subscriptions/a23279b5-xxxx-xxxx-xxxx-47b7c6d423ea/resourcegroups/awsales_resgroup/providers/microsoft.analysisservic
es/servers/awsales/providers/microsoft.insights/diagnosticSettings/service
Name                        : service
Type                        :
Location                    :
Tags                        :
```

<span data-ttu-id="6d5fb-280">This confirms that logging is now enabled for the server, saving information to the storage account.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-280">This confirms that logging is now enabled for the server, saving information to the storage account.</span></span>

<span data-ttu-id="6d5fb-281">You can also set retention policy for your logs so older logs are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-281">You can also set retention policy for your logs so older logs are automatically deleted.</span></span> <span data-ttu-id="6d5fb-282">For example, set retention policy using **-RetentionEnabled** flag to **$true**, and set **-RetentionInDays** parameter to **90**.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-282">For example, set retention policy using **-RetentionEnabled** flag to **$true**, and set **-RetentionInDays** parameter to **90**.</span></span> <span data-ttu-id="6d5fb-283">Logs older than 90 days are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-283">Logs older than 90 days are automatically deleted.</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId $account.ResourceId`
 -StorageAccountId $sa.Id -Enabled $true -Categories Engine`
  -RetentionEnabled $true -RetentionInDays 90
```

## <a name="next-steps"></a><span data-ttu-id="6d5fb-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d5fb-284">Next steps</span></span>

<span data-ttu-id="6d5fb-285">Learn more about [Azure resource diagnostic logging](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6d5fb-285">Learn more about [Azure resource diagnostic logging](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

<span data-ttu-id="6d5fb-286">See [Set-AzureRmDiagnosticSetting](https://docs.microsoft.com/powershell/module/azurerm.insights/Set-AzureRmDiagnosticSetting) in PowerShell help.</span><span class="sxs-lookup"><span data-stu-id="6d5fb-286">See [Set-AzureRmDiagnosticSetting](https://docs.microsoft.com/powershell/module/azurerm.insights/Set-AzureRmDiagnosticSetting) in PowerShell help.</span></span>
