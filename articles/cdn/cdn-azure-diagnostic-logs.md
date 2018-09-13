---
title: Azure diagnostic logs | Microsoft Docs
description: Customer can enable log analysis for Azure CDN.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2018
ms.author: v-deasim
ms.openlocfilehash: 0baa43977099af9c6c0d9c2e4c03abc121ec279d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857198"
---
# <a name="azure-diagnostic-logs"></a><span data-ttu-id="16322-103">Azure diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="16322-103">Azure diagnostic logs</span></span>

<span data-ttu-id="16322-104">With Azure diagnostic logs, you can view core analytics and save them into one or more destinations including:</span><span class="sxs-lookup"><span data-stu-id="16322-104">With Azure diagnostic logs, you can view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="16322-105">Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="16322-105">Azure Storage account</span></span>
 - <span data-ttu-id="16322-106">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="16322-106">Azure Event Hubs</span></span>
 - [<span data-ttu-id="16322-107">Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="16322-107">Log Analytics workspace</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
<span data-ttu-id="16322-108">This feature is available on CDN endpoints for all pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="16322-108">This feature is available on CDN endpoints for all pricing tiers.</span></span> 

<span data-ttu-id="16322-109">Azure diagnostics logs allow you to export basic usage metrics from your CDN endpoint to a variety of sources so that you can consume them in a customized way.</span><span class="sxs-lookup"><span data-stu-id="16322-109">Azure diagnostics logs allow you to export basic usage metrics from your CDN endpoint to a variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="16322-110">For example, you can do the following types of data export:</span><span class="sxs-lookup"><span data-stu-id="16322-110">For example, you can do the following types of data export:</span></span>

- <span data-ttu-id="16322-111">Export data to blob storage, export to CSV, and generate graphs in Excel.</span><span class="sxs-lookup"><span data-stu-id="16322-111">Export data to blob storage, export to CSV, and generate graphs in Excel.</span></span>
- <span data-ttu-id="16322-112">Export data to Event Hubs and correlate with data from other Azure services.</span><span class="sxs-lookup"><span data-stu-id="16322-112">Export data to Event Hubs and correlate with data from other Azure services.</span></span>
- <span data-ttu-id="16322-113">Export data to Log Analytics and view data in your own Log Analytics work space</span><span class="sxs-lookup"><span data-stu-id="16322-113">Export data to Log Analytics and view data in your own Log Analytics work space</span></span>

<span data-ttu-id="16322-114">The following diagram shows a typical CDN core analytics view of data.</span><span class="sxs-lookup"><span data-stu-id="16322-114">The following diagram shows a typical CDN core analytics view of data.</span></span>

![portal - Diagnostics logs](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="16322-116">*Figure 1 - CDN core analytics view*</span><span class="sxs-lookup"><span data-stu-id="16322-116">*Figure 1 - CDN core analytics view*</span></span>

<span data-ttu-id="16322-117">For more information about diagnostic logs, see [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="16322-117">For more information about diagnostic logs, see [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).</span></span>

## <a name="enable-logging-with-the-azure-portal"></a><span data-ttu-id="16322-118">Enable logging with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="16322-118">Enable logging with the Azure portal</span></span>

<span data-ttu-id="16322-119">Follow these steps enable logging with CDN core analytics:</span><span class="sxs-lookup"><span data-stu-id="16322-119">Follow these steps enable logging with CDN core analytics:</span></span>

<span data-ttu-id="16322-120">Sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16322-120">Sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="16322-121">If you don't already have enabled CDN for your workflow, [Create an Azure CDN profile and endpoint](cdn-create-new-endpoint.md) before you continue.</span><span class="sxs-lookup"><span data-stu-id="16322-121">If you don't already have enabled CDN for your workflow, [Create an Azure CDN profile and endpoint](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="16322-122">In the Azure portal, navigate to **CDN profile**.</span><span class="sxs-lookup"><span data-stu-id="16322-122">In the Azure portal, navigate to **CDN profile**.</span></span>

2. <span data-ttu-id="16322-123">In the Azure portal, search for a CDN profile or select one from your dashboard.</span><span class="sxs-lookup"><span data-stu-id="16322-123">In the Azure portal, search for a CDN profile or select one from your dashboard.</span></span> <span data-ttu-id="16322-124">Then, select the CDN endpoint for which you want to enable diagnostics logs.</span><span class="sxs-lookup"><span data-stu-id="16322-124">Then, select the CDN endpoint for which you want to enable diagnostics logs.</span></span>

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="16322-126">Select **Diagnostics logs** in the MONITORING section.</span><span class="sxs-lookup"><span data-stu-id="16322-126">Select **Diagnostics logs** in the MONITORING section.</span></span>

   <span data-ttu-id="16322-127">The **Diagnostics logs** page appears.</span><span class="sxs-lookup"><span data-stu-id="16322-127">The **Diagnostics logs** page appears.</span></span>

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="16322-129">Enable logging with Azure Storage</span><span class="sxs-lookup"><span data-stu-id="16322-129">Enable logging with Azure Storage</span></span>

<span data-ttu-id="16322-130">To use a storage account to store the logs, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="16322-130">To use a storage account to store the logs, follow these steps:</span></span>
    
1. <span data-ttu-id="16322-131">For **Name**, enter a name for your diagnostic log settings.</span><span class="sxs-lookup"><span data-stu-id="16322-131">For **Name**, enter a name for your diagnostic log settings.</span></span>
 
2. <span data-ttu-id="16322-132">Select **Archive to a storage account**, then select **CoreAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="16322-132">Select **Archive to a storage account**, then select **CoreAnalytics**.</span></span> 

2. <span data-ttu-id="16322-133">For **Retention (days)**, choose the number of retention days.</span><span class="sxs-lookup"><span data-stu-id="16322-133">For **Retention (days)**, choose the number of retention days.</span></span> <span data-ttu-id="16322-134">A retention of zero days stores the logs indefinitely.</span><span class="sxs-lookup"><span data-stu-id="16322-134">A retention of zero days stores the logs indefinitely.</span></span> 

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png) 

3. <span data-ttu-id="16322-136">Select **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="16322-136">Select **Storage account**.</span></span>

    <span data-ttu-id="16322-137">The **Select a storage account** page appears.</span><span class="sxs-lookup"><span data-stu-id="16322-137">The **Select a storage account** page appears.</span></span>

4. <span data-ttu-id="16322-138">Select a storage account from the drop-down list, then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="16322-138">Select a storage account from the drop-down list, then select **OK**.</span></span>

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/cdn-select-storage-account.png)

5. <span data-ttu-id="16322-140">After you have finished making your diagnostic log settings, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="16322-140">After you have finished making your diagnostic log settings, select **Save**.</span></span>

### <a name="logging-with-log-analytics"></a><span data-ttu-id="16322-141">Logging with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="16322-141">Logging with Log Analytics</span></span>

<span data-ttu-id="16322-142">To use Log Analytics to store the logs, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="16322-142">To use Log Analytics to store the logs, follow these steps:</span></span>

1. <span data-ttu-id="16322-143">From the **Diagnostics logs** page, select **Send to Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="16322-143">From the **Diagnostics logs** page, select **Send to Log Analytics**.</span></span> 

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="16322-145">Select **Configure** to configure Log Analytics logging.</span><span class="sxs-lookup"><span data-stu-id="16322-145">Select **Configure** to configure Log Analytics logging.</span></span> 

   <span data-ttu-id="16322-146">The **OMS Workspaces** page appears.</span><span class="sxs-lookup"><span data-stu-id="16322-146">The **OMS Workspaces** page appears.</span></span>

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="16322-148">Select **Create New Workspace**.</span><span class="sxs-lookup"><span data-stu-id="16322-148">Select **Create New Workspace**.</span></span>

    <span data-ttu-id="16322-149">The **OMS Workspace** page appears.</span><span class="sxs-lookup"><span data-stu-id="16322-149">The **OMS Workspace** page appears.</span></span>

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="16322-151">For **OMS Workspace**, enter an OMS Workspace name.</span><span class="sxs-lookup"><span data-stu-id="16322-151">For **OMS Workspace**, enter an OMS Workspace name.</span></span> <span data-ttu-id="16322-152">The OMS Workspace name must be unique and contain only letters, numbers, and hyphens; spaces and underscores are not allowed.</span><span class="sxs-lookup"><span data-stu-id="16322-152">The OMS Workspace name must be unique and contain only letters, numbers, and hyphens; spaces and underscores are not allowed.</span></span> 

5. <span data-ttu-id="16322-153">For **Subscription**, select an existing subscription from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="16322-153">For **Subscription**, select an existing subscription from the drop-down list.</span></span> 

6. <span data-ttu-id="16322-154">For **Resource group**, create a new resource group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="16322-154">For **Resource group**, create a new resource group or select an existing one.</span></span>

7. <span data-ttu-id="16322-155">For **Location**, select a location from the list.</span><span class="sxs-lookup"><span data-stu-id="16322-155">For **Location**, select a location from the list.</span></span>

8. <span data-ttu-id="16322-156">Select **Pin to dashboard** if you want to save the log configuration to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="16322-156">Select **Pin to dashboard** if you want to save the log configuration to your dashboard.</span></span> 

9. <span data-ttu-id="16322-157">Select **OK** to complete the configuration.</span><span class="sxs-lookup"><span data-stu-id="16322-157">Select **OK** to complete the configuration.</span></span>

10. <span data-ttu-id="16322-158">After your workspace is created, you're returned to the **Diagnostic logs** page.</span><span class="sxs-lookup"><span data-stu-id="16322-158">After your workspace is created, you're returned to the **Diagnostic logs** page.</span></span> <span data-ttu-id="16322-159">Confirm the name of your new Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="16322-159">Confirm the name of your new Log Analytics workspace.</span></span>

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/09_Return-to-logging.png)

11. <span data-ttu-id="16322-161">Select **CoreAnalytics**, then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="16322-161">Select **CoreAnalytics**, then select **Save**.</span></span>

12. <span data-ttu-id="16322-162">To view the new Log Analytics workspace, select **Core analytics** from your CDN endpoint page.</span><span class="sxs-lookup"><span data-stu-id="16322-162">To view the new Log Analytics workspace, select **Core analytics** from your CDN endpoint page.</span></span>

    ![portal - Diagnostics logs](./media/cdn-diagnostics-log/cdn-core-analytics-page.png) 

    <span data-ttu-id="16322-164">Your Log Analytics workspace is now ready to log data.</span><span class="sxs-lookup"><span data-stu-id="16322-164">Your Log Analytics workspace is now ready to log data.</span></span> <span data-ttu-id="16322-165">In order to consume that data, you must use a [Log Analytics Solution](#consuming-diagnostics-logs-from-a-log-analytics-workspace), covered later in this article.</span><span class="sxs-lookup"><span data-stu-id="16322-165">In order to consume that data, you must use a [Log Analytics Solution](#consuming-diagnostics-logs-from-a-log-analytics-workspace), covered later in this article.</span></span>

<span data-ttu-id="16322-166">For more information about log data delays, see [Log data delays](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="16322-166">For more information about log data delays, see [Log data delays](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="16322-167">Enable logging with PowerShell</span><span class="sxs-lookup"><span data-stu-id="16322-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="16322-168">The following example shows how to enable diagnostic logs via the Azure PowerShell Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="16322-168">The following example shows how to enable diagnostic logs via the Azure PowerShell Cmdlets.</span></span>

### <a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="16322-169">Enabling diagnostic logs in a storage account</span><span class="sxs-lookup"><span data-stu-id="16322-169">Enabling diagnostic logs in a storage account</span></span>

1. <span data-ttu-id="16322-170">Log in and select a subscription:</span><span class="sxs-lookup"><span data-stu-id="16322-170">Log in and select a subscription:</span></span>

    <span data-ttu-id="16322-171">Connect-AzureRmAccount</span><span class="sxs-lookup"><span data-stu-id="16322-171">Connect-AzureRmAccount</span></span> 

    <span data-ttu-id="16322-172">Select-AzureSubscription -SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="16322-172">Select-AzureSubscription -SubscriptionId</span></span> 

2. <span data-ttu-id="16322-173">To enable Diagnostic Logs in a Storage account, enter this command:</span><span class="sxs-lookup"><span data-stu-id="16322-173">To enable Diagnostic Logs in a Storage account, enter this command:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
    ```

3. <span data-ttu-id="16322-174">To enable diagnostics logs in a Log Analytics workspace, enter this command:</span><span class="sxs-lookup"><span data-stu-id="16322-174">To enable diagnostics logs in a Log Analytics workspace, enter this command:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
    ```

## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="16322-175">Consuming diagnostics logs from Azure Storage</span><span class="sxs-lookup"><span data-stu-id="16322-175">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="16322-176">This section describes the schema of CDN core analytics, how it is organized inside of an Azure storage account, and provides sample code to download the logs in a CSV file.</span><span class="sxs-lookup"><span data-stu-id="16322-176">This section describes the schema of CDN core analytics, how it is organized inside of an Azure storage account, and provides sample code to download the logs in a CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="16322-177">Using Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="16322-177">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="16322-178">Before you can access the core analytics data from an Azure storage account, you first need a tool to access the contents in a storage account.</span><span class="sxs-lookup"><span data-stu-id="16322-178">Before you can access the core analytics data from an Azure storage account, you first need a tool to access the contents in a storage account.</span></span> <span data-ttu-id="16322-179">While there are several tools available in the market, the one that we recommend is the Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="16322-179">While there are several tools available in the market, the one that we recommend is the Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="16322-180">To download the tool, see [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="16322-180">To download the tool, see [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="16322-181">After downloading and installing the software, configure it to use the same Azure storage account that was configured as a destination to the CDN Diagnostics Logs.</span><span class="sxs-lookup"><span data-stu-id="16322-181">After downloading and installing the software, configure it to use the same Azure storage account that was configured as a destination to the CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="16322-182">Open **Microsoft Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="16322-182">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="16322-183">Locate the storage account</span><span class="sxs-lookup"><span data-stu-id="16322-183">Locate the storage account</span></span>
3.  <span data-ttu-id="16322-184">Expand the **Blob Containers** node under this storage account.</span><span class="sxs-lookup"><span data-stu-id="16322-184">Expand the **Blob Containers** node under this storage account.</span></span>
4.  <span data-ttu-id="16322-185">Select the container named *insights-logs-coreanalytics*.</span><span class="sxs-lookup"><span data-stu-id="16322-185">Select the container named *insights-logs-coreanalytics*.</span></span>
5.  <span data-ttu-id="16322-186">Results show up on the right-hand pane, starting with the first level, as *resourceId=*.</span><span class="sxs-lookup"><span data-stu-id="16322-186">Results show up on the right-hand pane, starting with the first level, as *resourceId=*.</span></span> <span data-ttu-id="16322-187">Continue selecting each level until you find the file *PT1H.json*.</span><span class="sxs-lookup"><span data-stu-id="16322-187">Continue selecting each level until you find the file *PT1H.json*.</span></span> <span data-ttu-id="16322-188">For an explanation of the path, see [Blob path format](cdn-azure-diagnostic-logs.md#blob-path-format).</span><span class="sxs-lookup"><span data-stu-id="16322-188">For an explanation of the path, see [Blob path format](cdn-azure-diagnostic-logs.md#blob-path-format).</span></span>
6.  <span data-ttu-id="16322-189">Each blob *PT1H.json* file represents the analytics logs for one hour for a specific CDN endpoint or its custom domain.</span><span class="sxs-lookup"><span data-stu-id="16322-189">Each blob *PT1H.json* file represents the analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="16322-190">The schema of the contents of this JSON file is described in the section schema of the core analytics logs.</span><span class="sxs-lookup"><span data-stu-id="16322-190">The schema of the contents of this JSON file is described in the section schema of the core analytics logs.</span></span>


#### <a name="blob-path-format"></a><span data-ttu-id="16322-191">Blob path format</span><span class="sxs-lookup"><span data-stu-id="16322-191">Blob path format</span></span>

<span data-ttu-id="16322-192">Core analytics logs are generated every hour and the data is collected and stored inside a single Azure blob as a JSON payload.</span><span class="sxs-lookup"><span data-stu-id="16322-192">Core analytics logs are generated every hour and the data is collected and stored inside a single Azure blob as a JSON payload.</span></span> <span data-ttu-id="16322-193">Because the Storage explorer tool interprets '/' as a directory separator and shows the hierarchy, the path to the Azure blob appears as if there is a hierarchical structure and represents the blob name.</span><span class="sxs-lookup"><span data-stu-id="16322-193">Because the Storage explorer tool interprets '/' as a directory separator and shows the hierarchy, the path to the Azure blob appears as if there is a hierarchical structure and represents the blob name.</span></span> <span data-ttu-id="16322-194">The name of the blob follows the following naming convention:</span><span class="sxs-lookup"><span data-stu-id="16322-194">The name of the blob follows the following naming convention:</span></span>   

```resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json```

<span data-ttu-id="16322-195">**Description of fields:**</span><span class="sxs-lookup"><span data-stu-id="16322-195">**Description of fields:**</span></span>

|<span data-ttu-id="16322-196">Value</span><span class="sxs-lookup"><span data-stu-id="16322-196">Value</span></span>|<span data-ttu-id="16322-197">Description</span><span class="sxs-lookup"><span data-stu-id="16322-197">Description</span></span>|
|-------|---------|
|<span data-ttu-id="16322-198">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="16322-198">Subscription ID</span></span>    |<span data-ttu-id="16322-199">ID of the Azure subscription in Guid format.</span><span class="sxs-lookup"><span data-stu-id="16322-199">ID of the Azure subscription in Guid format.</span></span>|
|<span data-ttu-id="16322-200">Resource Group Name</span><span class="sxs-lookup"><span data-stu-id="16322-200">Resource Group Name</span></span> |<span data-ttu-id="16322-201">Name of the resource group to which the CDN resources belong.</span><span class="sxs-lookup"><span data-stu-id="16322-201">Name of the resource group to which the CDN resources belong.</span></span>|
|<span data-ttu-id="16322-202">Profile Name</span><span class="sxs-lookup"><span data-stu-id="16322-202">Profile Name</span></span> |<span data-ttu-id="16322-203">Name of the CDN Profile</span><span class="sxs-lookup"><span data-stu-id="16322-203">Name of the CDN Profile</span></span>|
|<span data-ttu-id="16322-204">Endpoint Name</span><span class="sxs-lookup"><span data-stu-id="16322-204">Endpoint Name</span></span> |<span data-ttu-id="16322-205">Name of the CDN Endpoint</span><span class="sxs-lookup"><span data-stu-id="16322-205">Name of the CDN Endpoint</span></span>|
|<span data-ttu-id="16322-206">Year</span><span class="sxs-lookup"><span data-stu-id="16322-206">Year</span></span>|  <span data-ttu-id="16322-207">Four-digit representation of the year, for example, 2017</span><span class="sxs-lookup"><span data-stu-id="16322-207">Four-digit representation of the year, for example, 2017</span></span>|
|<span data-ttu-id="16322-208">Month</span><span class="sxs-lookup"><span data-stu-id="16322-208">Month</span></span>| <span data-ttu-id="16322-209">Two-digit representation of the month number.</span><span class="sxs-lookup"><span data-stu-id="16322-209">Two-digit representation of the month number.</span></span> <span data-ttu-id="16322-210">01=January ... 12=December</span><span class="sxs-lookup"><span data-stu-id="16322-210">01=January ... 12=December</span></span>|
|<span data-ttu-id="16322-211">Day</span><span class="sxs-lookup"><span data-stu-id="16322-211">Day</span></span>|   <span data-ttu-id="16322-212">Two-digit representation of the day of the month</span><span class="sxs-lookup"><span data-stu-id="16322-212">Two-digit representation of the day of the month</span></span>|
|<span data-ttu-id="16322-213">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="16322-213">PT1H.json</span></span>| <span data-ttu-id="16322-214">Actual JSON file where the analytics data is stored</span><span class="sxs-lookup"><span data-stu-id="16322-214">Actual JSON file where the analytics data is stored</span></span>|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a><span data-ttu-id="16322-215">Exporting the core analytics data to a CSV file</span><span class="sxs-lookup"><span data-stu-id="16322-215">Exporting the core analytics data to a CSV file</span></span>

<span data-ttu-id="16322-216">To make it easy to access core analytics, sample code for a tool is provided.</span><span class="sxs-lookup"><span data-stu-id="16322-216">To make it easy to access core analytics, sample code for a tool is provided.</span></span> <span data-ttu-id="16322-217">This tool allows downloading the JSON files into a flat comma-separated file format, which can be used to create charts or other aggregations.</span><span class="sxs-lookup"><span data-stu-id="16322-217">This tool allows downloading the JSON files into a flat comma-separated file format, which can be used to create charts or other aggregations.</span></span>

<span data-ttu-id="16322-218">Here's how you can use the tool:</span><span class="sxs-lookup"><span data-stu-id="16322-218">Here's how you can use the tool:</span></span>

1.  <span data-ttu-id="16322-219">Visit the github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv)</span><span class="sxs-lookup"><span data-stu-id="16322-219">Visit the github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv)</span></span>
2.  <span data-ttu-id="16322-220">Download the code.</span><span class="sxs-lookup"><span data-stu-id="16322-220">Download the code.</span></span>
3.  <span data-ttu-id="16322-221">Follow the instructions to compile and configure.</span><span class="sxs-lookup"><span data-stu-id="16322-221">Follow the instructions to compile and configure.</span></span>
4.  <span data-ttu-id="16322-222">Run the tool.</span><span class="sxs-lookup"><span data-stu-id="16322-222">Run the tool.</span></span>
5.  <span data-ttu-id="16322-223">The resulting CSV file shows the analytics data in a simple flat hierarchy.</span><span class="sxs-lookup"><span data-stu-id="16322-223">The resulting CSV file shows the analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-a-log-analytics-workspace"></a><span data-ttu-id="16322-224">Consuming diagnostics logs from a Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="16322-224">Consuming diagnostics logs from a Log Analytics workspace</span></span>
<span data-ttu-id="16322-225">Log Analytics is an Azure service that monitors your cloud and on-premises environments to maintain their availability and performance.</span><span class="sxs-lookup"><span data-stu-id="16322-225">Log Analytics is an Azure service that monitors your cloud and on-premises environments to maintain their availability and performance.</span></span> <span data-ttu-id="16322-226">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools to provide analysis across multiple sources.</span><span class="sxs-lookup"><span data-stu-id="16322-226">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools to provide analysis across multiple sources.</span></span> 

<span data-ttu-id="16322-227">To use Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) to the Azure Log Analytics workspace, which is discussed earlier in this article.</span><span class="sxs-lookup"><span data-stu-id="16322-227">To use Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) to the Azure Log Analytics workspace, which is discussed earlier in this article.</span></span>

### <a name="using-the-log-analytics-workspace"></a><span data-ttu-id="16322-228">Using the Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="16322-228">Using the Log Analytics workspace</span></span>

 <span data-ttu-id="16322-229">The following diagram shows the architecture of the inputs and outputs of the repository:</span><span class="sxs-lookup"><span data-stu-id="16322-229">The following diagram shows the architecture of the inputs and outputs of the repository:</span></span>

![Log Analytics workspace](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="16322-231">*Figure 3 - Log Analytics Repository*</span><span class="sxs-lookup"><span data-stu-id="16322-231">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="16322-232">You can display the data in a variety of ways by using Management Solutions.</span><span class="sxs-lookup"><span data-stu-id="16322-232">You can display the data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="16322-233">You can obtain Management Solutions from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="16322-233">You can obtain Management Solutions from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="16322-234">You can install management solutions from Azure marketplace by selecting the **Get it now** link at the bottom of each solution.</span><span class="sxs-lookup"><span data-stu-id="16322-234">You can install management solutions from Azure marketplace by selecting the **Get it now** link at the bottom of each solution.</span></span>

### <a name="add-a-log-analytics-cdn-management-solution"></a><span data-ttu-id="16322-235">Add a Log Analytics CDN Management Solution</span><span class="sxs-lookup"><span data-stu-id="16322-235">Add a Log Analytics CDN Management Solution</span></span>

<span data-ttu-id="16322-236">Follow these steps to add a Log Analytics Management Solution:</span><span class="sxs-lookup"><span data-stu-id="16322-236">Follow these steps to add a Log Analytics Management Solution:</span></span>

1.   <span data-ttu-id="16322-237">Sign in to the Azure portal using your Azure subscription and go to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="16322-237">Sign in to the Azure portal using your Azure subscription and go to your dashboard.</span></span>
    <span data-ttu-id="16322-238">![Azure dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="16322-238">![Azure dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="16322-239">In the **New** page, under **Marketplace**, select **Monitoring + management**.</span><span class="sxs-lookup"><span data-stu-id="16322-239">In the **New** page, under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="16322-241">In the **Monitoring + management** page, select **See all**.</span><span class="sxs-lookup"><span data-stu-id="16322-241">In the **Monitoring + management** page, select **See all**.</span></span>

    ![See all](./media/cdn-diagnostics-log/15_See-all.png)

4. <span data-ttu-id="16322-243">Search for CDN in the search box.</span><span class="sxs-lookup"><span data-stu-id="16322-243">Search for CDN in the search box.</span></span>

    ![See all](./media/cdn-diagnostics-log/16_Search-for.png)

5. <span data-ttu-id="16322-245">Select **Azure CDN Core Analytics**.</span><span class="sxs-lookup"><span data-stu-id="16322-245">Select **Azure CDN Core Analytics**.</span></span> 

    ![See all](./media/cdn-diagnostics-log/17_Core-analytics.png)

6. <span data-ttu-id="16322-247">After you select **Create**, you are asked to create a new Log Analytics workspace or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="16322-247">After you select **Create**, you are asked to create a new Log Analytics workspace or use an existing one.</span></span> 

    ![See all](./media/cdn-diagnostics-log/18_Adding-solution.png)

7. <span data-ttu-id="16322-249">Select the workspace you created before.</span><span class="sxs-lookup"><span data-stu-id="16322-249">Select the workspace you created before.</span></span> <span data-ttu-id="16322-250">You then need to add an automation account.</span><span class="sxs-lookup"><span data-stu-id="16322-250">You then need to add an automation account.</span></span>

    ![See all](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="16322-252">The following screen shows the automation account form you must fill out.</span><span class="sxs-lookup"><span data-stu-id="16322-252">The following screen shows the automation account form you must fill out.</span></span> 

    ![See all](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="16322-254">Once you have created the automation account, you are ready to add your solution.</span><span class="sxs-lookup"><span data-stu-id="16322-254">Once you have created the automation account, you are ready to add your solution.</span></span> <span data-ttu-id="16322-255">Select the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="16322-255">Select the **Create** button.</span></span>

    ![See all](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="16322-257">Your solution has now been added to your workspace.</span><span class="sxs-lookup"><span data-stu-id="16322-257">Your solution has now been added to your workspace.</span></span> <span data-ttu-id="16322-258">Return to your Azure portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="16322-258">Return to your Azure portal dashboard.</span></span>

    ![See all](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="16322-260">Select the Log Analytics workspace you created to go to your workspace.</span><span class="sxs-lookup"><span data-stu-id="16322-260">Select the Log Analytics workspace you created to go to your workspace.</span></span> 

11. <span data-ttu-id="16322-261">Select the **OMS Portal** tile to see your new solution.</span><span class="sxs-lookup"><span data-stu-id="16322-261">Select the **OMS Portal** tile to see your new solution.</span></span>

    ![See all](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="16322-263">Your portal should now look like the following screen:</span><span class="sxs-lookup"><span data-stu-id="16322-263">Your portal should now look like the following screen:</span></span>

    ![See all](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="16322-265">Select one of the tiles to see several views into your data.</span><span class="sxs-lookup"><span data-stu-id="16322-265">Select one of the tiles to see several views into your data.</span></span>

    ![See all](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="16322-267">You can scroll left or right to see further tiles representing individual views into the data.</span><span class="sxs-lookup"><span data-stu-id="16322-267">You can scroll left or right to see further tiles representing individual views into the data.</span></span> 

    <span data-ttu-id="16322-268">Select one of the tiles to see more details about your data.</span><span class="sxs-lookup"><span data-stu-id="16322-268">Select one of the tiles to see more details about your data.</span></span>

     ![See all](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="16322-270">Offers and pricing tiers</span><span class="sxs-lookup"><span data-stu-id="16322-270">Offers and pricing tiers</span></span>

<span data-ttu-id="16322-271">You can see offers and pricing tiers for management solutions [here](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="16322-271">You can see offers and pricing tiers for management solutions [here](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="16322-272">Customizing views</span><span class="sxs-lookup"><span data-stu-id="16322-272">Customizing views</span></span>

<span data-ttu-id="16322-273">You can customize the view into your data by using the **View Designer**.</span><span class="sxs-lookup"><span data-stu-id="16322-273">You can customize the view into your data by using the **View Designer**.</span></span> <span data-ttu-id="16322-274">To begin designing, go to your Log Analytics workspace and select the **View Designer** tile.</span><span class="sxs-lookup"><span data-stu-id="16322-274">To begin designing, go to your Log Analytics workspace and select the **View Designer** tile.</span></span>

![View Designer](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="16322-276">Drag-and-drop the types of charts and fill in the data details you want to analyze.</span><span class="sxs-lookup"><span data-stu-id="16322-276">Drag-and-drop the types of charts and fill in the data details you want to analyze.</span></span>

![View Designer](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="16322-278">Log data delays</span><span class="sxs-lookup"><span data-stu-id="16322-278">Log data delays</span></span>

<span data-ttu-id="16322-279">The following table shows log data delays for **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Akamai**, and **Azure CDN Standard/Premium from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="16322-279">The following table shows log data delays for **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Akamai**, and **Azure CDN Standard/Premium from Verizon**.</span></span>

<span data-ttu-id="16322-280">Microsoft log data delays</span><span class="sxs-lookup"><span data-stu-id="16322-280">Microsoft log data delays</span></span> | <span data-ttu-id="16322-281">Verizon log data delays</span><span class="sxs-lookup"><span data-stu-id="16322-281">Verizon log data delays</span></span> | <span data-ttu-id="16322-282">Akamai log data delays</span><span class="sxs-lookup"><span data-stu-id="16322-282">Akamai log data delays</span></span>
--- | --- | ---
<span data-ttu-id="16322-283">Delayed by 1 hour.</span><span class="sxs-lookup"><span data-stu-id="16322-283">Delayed by 1 hour.</span></span> | <span data-ttu-id="16322-284">Delayed by 1 hour and can take up to 2 hours to start appearing after endpoint propagation completion.</span><span class="sxs-lookup"><span data-stu-id="16322-284">Delayed by 1 hour and can take up to 2 hours to start appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="16322-285">Delayed by 24 hours; if it was created more than 24 hours ago, it takes up to 2 hours to start appearing.</span><span class="sxs-lookup"><span data-stu-id="16322-285">Delayed by 24 hours; if it was created more than 24 hours ago, it takes up to 2 hours to start appearing.</span></span> <span data-ttu-id="16322-286">If it was recently created, it can take up to 25 hours for the logs to start appearing.</span><span class="sxs-lookup"><span data-stu-id="16322-286">If it was recently created, it can take up to 25 hours for the logs to start appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="16322-287">Diagnostic log types for CDN core analytics</span><span class="sxs-lookup"><span data-stu-id="16322-287">Diagnostic log types for CDN core analytics</span></span>

<span data-ttu-id="16322-288">Microsoft currently offers core analytics logs only, which contain metrics showing HTTP response statistics and egress statistics as seen from the CDN POPs/edges.</span><span class="sxs-lookup"><span data-stu-id="16322-288">Microsoft currently offers core analytics logs only, which contain metrics showing HTTP response statistics and egress statistics as seen from the CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="16322-289">Core analytics metrics details</span><span class="sxs-lookup"><span data-stu-id="16322-289">Core analytics metrics details</span></span>
<span data-ttu-id="16322-290">The following table shows a list of metrics available in the core analytics logs for **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Akamai**, and **Azure CDN Standard/Premium from Verizon**.</span><span class="sxs-lookup"><span data-stu-id="16322-290">The following table shows a list of metrics available in the core analytics logs for **Azure CDN Standard from Microsoft**, **Azure CDN Standard from Akamai**, and **Azure CDN Standard/Premium from Verizon**.</span></span> <span data-ttu-id="16322-291">Not all metrics are available from all providers, although such differences are minimal.</span><span class="sxs-lookup"><span data-stu-id="16322-291">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="16322-292">The table also displays whether a given metric is available from a provider.</span><span class="sxs-lookup"><span data-stu-id="16322-292">The table also displays whether a given metric is available from a provider.</span></span> <span data-ttu-id="16322-293">The metrics are available for only those CDN endpoints that have traffic on them.</span><span class="sxs-lookup"><span data-stu-id="16322-293">The metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="16322-294">Metric</span><span class="sxs-lookup"><span data-stu-id="16322-294">Metric</span></span>                     | <span data-ttu-id="16322-295">Description</span><span class="sxs-lookup"><span data-stu-id="16322-295">Description</span></span> | <span data-ttu-id="16322-296">Microsoft</span><span class="sxs-lookup"><span data-stu-id="16322-296">Microsoft</span></span> | <span data-ttu-id="16322-297">Verizon</span><span class="sxs-lookup"><span data-stu-id="16322-297">Verizon</span></span> | <span data-ttu-id="16322-298">Akamai</span><span class="sxs-lookup"><span data-stu-id="16322-298">Akamai</span></span> |
|---------------------------|-------------|-----------|---------|--------|
| <span data-ttu-id="16322-299">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="16322-299">RequestCountTotal</span></span>         | <span data-ttu-id="16322-300">Total number of request hits during this period.</span><span class="sxs-lookup"><span data-stu-id="16322-300">Total number of request hits during this period.</span></span> | <span data-ttu-id="16322-301">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-301">Yes</span></span> | <span data-ttu-id="16322-302">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-302">Yes</span></span> |<span data-ttu-id="16322-303">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-303">Yes</span></span> |
| <span data-ttu-id="16322-304">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="16322-304">RequestCountHttpStatus2xx</span></span> | <span data-ttu-id="16322-305">Count of all requests that resulted in a 2xx HTTP code (for example, 200, 202).</span><span class="sxs-lookup"><span data-stu-id="16322-305">Count of all requests that resulted in a 2xx HTTP code (for example, 200, 202).</span></span> | <span data-ttu-id="16322-306">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-306">Yes</span></span> | <span data-ttu-id="16322-307">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-307">Yes</span></span> |<span data-ttu-id="16322-308">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-308">Yes</span></span> |
| <span data-ttu-id="16322-309">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="16322-309">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="16322-310">Count of all requests that resulted in a 3xx HTTP code (for example, 300, 302).</span><span class="sxs-lookup"><span data-stu-id="16322-310">Count of all requests that resulted in a 3xx HTTP code (for example, 300, 302).</span></span> | <span data-ttu-id="16322-311">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-311">Yes</span></span> | <span data-ttu-id="16322-312">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-312">Yes</span></span> |<span data-ttu-id="16322-313">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-313">Yes</span></span> |
| <span data-ttu-id="16322-314">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="16322-314">RequestCountHttpStatus4xx</span></span> | <span data-ttu-id="16322-315">Count of all requests that resulted in a 4xx HTTP code (for example, 400, 404).</span><span class="sxs-lookup"><span data-stu-id="16322-315">Count of all requests that resulted in a 4xx HTTP code (for example, 400, 404).</span></span> | <span data-ttu-id="16322-316">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-316">Yes</span></span> | <span data-ttu-id="16322-317">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-317">Yes</span></span> |<span data-ttu-id="16322-318">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-318">Yes</span></span> |
| <span data-ttu-id="16322-319">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="16322-319">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="16322-320">Count of all requests that resulted in a 5xx HTTP code (for example, 500, 504).</span><span class="sxs-lookup"><span data-stu-id="16322-320">Count of all requests that resulted in a 5xx HTTP code (for example, 500, 504).</span></span> | <span data-ttu-id="16322-321">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-321">Yes</span></span> | <span data-ttu-id="16322-322">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-322">Yes</span></span> |<span data-ttu-id="16322-323">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-323">Yes</span></span> |
| <span data-ttu-id="16322-324">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="16322-324">RequestCountHttpStatusOthers</span></span> | <span data-ttu-id="16322-325">Count of all other HTTP codes (outside of 2xx-5xx).</span><span class="sxs-lookup"><span data-stu-id="16322-325">Count of all other HTTP codes (outside of 2xx-5xx).</span></span> | <span data-ttu-id="16322-326">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-326">Yes</span></span> | <span data-ttu-id="16322-327">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-327">Yes</span></span> |<span data-ttu-id="16322-328">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-328">Yes</span></span> |
| <span data-ttu-id="16322-329">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="16322-329">RequestCountHttpStatus200</span></span> | <span data-ttu-id="16322-330">Count of all requests that resulted in a 200 HTTP code response.</span><span class="sxs-lookup"><span data-stu-id="16322-330">Count of all requests that resulted in a 200 HTTP code response.</span></span> | <span data-ttu-id="16322-331">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-331">Yes</span></span> | <span data-ttu-id="16322-332">No</span><span class="sxs-lookup"><span data-stu-id="16322-332">No</span></span>  |<span data-ttu-id="16322-333">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-333">Yes</span></span> |
| <span data-ttu-id="16322-334">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="16322-334">RequestCountHttpStatus206</span></span> | <span data-ttu-id="16322-335">Count of all requests that resulted in a 206 HTTP code response.</span><span class="sxs-lookup"><span data-stu-id="16322-335">Count of all requests that resulted in a 206 HTTP code response.</span></span> | <span data-ttu-id="16322-336">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-336">Yes</span></span> | <span data-ttu-id="16322-337">No</span><span class="sxs-lookup"><span data-stu-id="16322-337">No</span></span>  |<span data-ttu-id="16322-338">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-338">Yes</span></span> |
| <span data-ttu-id="16322-339">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="16322-339">RequestCountHttpStatus302</span></span> | <span data-ttu-id="16322-340">Count of all requests that resulted in a 302 HTTP code response.</span><span class="sxs-lookup"><span data-stu-id="16322-340">Count of all requests that resulted in a 302 HTTP code response.</span></span> | <span data-ttu-id="16322-341">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-341">Yes</span></span> | <span data-ttu-id="16322-342">No</span><span class="sxs-lookup"><span data-stu-id="16322-342">No</span></span>  |<span data-ttu-id="16322-343">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-343">Yes</span></span> |
| <span data-ttu-id="16322-344">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="16322-344">RequestCountHttpStatus304</span></span> | <span data-ttu-id="16322-345">Count of all requests that resulted in a 304 HTTP code response.</span><span class="sxs-lookup"><span data-stu-id="16322-345">Count of all requests that resulted in a 304 HTTP code response.</span></span> | <span data-ttu-id="16322-346">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-346">Yes</span></span> | <span data-ttu-id="16322-347">No</span><span class="sxs-lookup"><span data-stu-id="16322-347">No</span></span>  |<span data-ttu-id="16322-348">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-348">Yes</span></span> |
| <span data-ttu-id="16322-349">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="16322-349">RequestCountHttpStatus404</span></span> | <span data-ttu-id="16322-350">Count of all requests that resulted in a 404 HTTP code response.</span><span class="sxs-lookup"><span data-stu-id="16322-350">Count of all requests that resulted in a 404 HTTP code response.</span></span> | <span data-ttu-id="16322-351">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-351">Yes</span></span> | <span data-ttu-id="16322-352">No</span><span class="sxs-lookup"><span data-stu-id="16322-352">No</span></span>  |<span data-ttu-id="16322-353">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-353">Yes</span></span> |
| <span data-ttu-id="16322-354">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="16322-354">RequestCountCacheHit</span></span> | <span data-ttu-id="16322-355">Count of all requests that resulted in a Cache hit.</span><span class="sxs-lookup"><span data-stu-id="16322-355">Count of all requests that resulted in a Cache hit.</span></span> <span data-ttu-id="16322-356">The asset was served directly from the POP to the client.</span><span class="sxs-lookup"><span data-stu-id="16322-356">The asset was served directly from the POP to the client.</span></span> | <span data-ttu-id="16322-357">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-357">Yes</span></span> | <span data-ttu-id="16322-358">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-358">Yes</span></span> | <span data-ttu-id="16322-359">No</span><span class="sxs-lookup"><span data-stu-id="16322-359">No</span></span>  |
| <span data-ttu-id="16322-360">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="16322-360">RequestCountCacheMiss</span></span> | <span data-ttu-id="16322-361">Count of all requests that resulted in a Cache miss.</span><span class="sxs-lookup"><span data-stu-id="16322-361">Count of all requests that resulted in a Cache miss.</span></span> <span data-ttu-id="16322-362">A Cache miss means the asset was not found on the POP closest to the client, and therefore was retrieved from the Origin.</span><span class="sxs-lookup"><span data-stu-id="16322-362">A Cache miss means the asset was not found on the POP closest to the client, and therefore was retrieved from the Origin.</span></span> | <span data-ttu-id="16322-363">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-363">Yes</span></span> | <span data-ttu-id="16322-364">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-364">Yes</span></span> | <span data-ttu-id="16322-365">No</span><span class="sxs-lookup"><span data-stu-id="16322-365">No</span></span> |
| <span data-ttu-id="16322-366">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="16322-366">RequestCountCacheNoCache</span></span> | <span data-ttu-id="16322-367">Count of all requests to an asset that are prevented from being cached due to a user configuration on the edge.</span><span class="sxs-lookup"><span data-stu-id="16322-367">Count of all requests to an asset that are prevented from being cached due to a user configuration on the edge.</span></span> | <span data-ttu-id="16322-368">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-368">Yes</span></span> | <span data-ttu-id="16322-369">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-369">Yes</span></span> | <span data-ttu-id="16322-370">No</span><span class="sxs-lookup"><span data-stu-id="16322-370">No</span></span> |
| <span data-ttu-id="16322-371">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="16322-371">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="16322-372">Count of all requests to assets that are prevented from being cached by the asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by the HTTP client.</span><span class="sxs-lookup"><span data-stu-id="16322-372">Count of all requests to assets that are prevented from being cached by the asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by the HTTP client.</span></span> | <span data-ttu-id="16322-373">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-373">Yes</span></span> | <span data-ttu-id="16322-374">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-374">Yes</span></span> | <span data-ttu-id="16322-375">No</span><span class="sxs-lookup"><span data-stu-id="16322-375">No</span></span> |
| <span data-ttu-id="16322-376">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="16322-376">RequestCountCacheOthers</span></span> | <span data-ttu-id="16322-377">Count of all requests with cache status not covered by above.</span><span class="sxs-lookup"><span data-stu-id="16322-377">Count of all requests with cache status not covered by above.</span></span> | <span data-ttu-id="16322-378">No</span><span class="sxs-lookup"><span data-stu-id="16322-378">No</span></span> | <span data-ttu-id="16322-379">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-379">Yes</span></span> | <span data-ttu-id="16322-380">No</span><span class="sxs-lookup"><span data-stu-id="16322-380">No</span></span>  |
| <span data-ttu-id="16322-381">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="16322-381">EgressTotal</span></span> | <span data-ttu-id="16322-382">Outbound data transfer in GB</span><span class="sxs-lookup"><span data-stu-id="16322-382">Outbound data transfer in GB</span></span> | <span data-ttu-id="16322-383">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-383">Yes</span></span> |<span data-ttu-id="16322-384">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-384">Yes</span></span> |<span data-ttu-id="16322-385">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-385">Yes</span></span> |
| <span data-ttu-id="16322-386">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="16322-386">EgressHttpStatus2xx</span></span> | <span data-ttu-id="16322-387">Outbound data transfer\* for responses with 2xx HTTP status codes in GB.</span><span class="sxs-lookup"><span data-stu-id="16322-387">Outbound data transfer\* for responses with 2xx HTTP status codes in GB.</span></span> | <span data-ttu-id="16322-388">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-388">Yes</span></span> | <span data-ttu-id="16322-389">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-389">Yes</span></span> | <span data-ttu-id="16322-390">No</span><span class="sxs-lookup"><span data-stu-id="16322-390">No</span></span>  |
| <span data-ttu-id="16322-391">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="16322-391">EgressHttpStatus3xx</span></span> | <span data-ttu-id="16322-392">Outbound data transfer for responses with 3xx HTTP status codes in GB.</span><span class="sxs-lookup"><span data-stu-id="16322-392">Outbound data transfer for responses with 3xx HTTP status codes in GB.</span></span> | <span data-ttu-id="16322-393">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-393">Yes</span></span> | <span data-ttu-id="16322-394">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-394">Yes</span></span> | <span data-ttu-id="16322-395">No</span><span class="sxs-lookup"><span data-stu-id="16322-395">No</span></span>  |
| <span data-ttu-id="16322-396">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="16322-396">EgressHttpStatus4xx</span></span> | <span data-ttu-id="16322-397">Outbound data transfer for responses with 4xx HTTP status codes in GB.</span><span class="sxs-lookup"><span data-stu-id="16322-397">Outbound data transfer for responses with 4xx HTTP status codes in GB.</span></span> | <span data-ttu-id="16322-398">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-398">Yes</span></span> | <span data-ttu-id="16322-399">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-399">Yes</span></span> | <span data-ttu-id="16322-400">No</span><span class="sxs-lookup"><span data-stu-id="16322-400">No</span></span>  |
| <span data-ttu-id="16322-401">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="16322-401">EgressHttpStatus5xx</span></span> | <span data-ttu-id="16322-402">Outbound data transfer for responses with 5xx HTTP status codes in GB.</span><span class="sxs-lookup"><span data-stu-id="16322-402">Outbound data transfer for responses with 5xx HTTP status codes in GB.</span></span> | <span data-ttu-id="16322-403">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-403">Yes</span></span> | <span data-ttu-id="16322-404">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-404">Yes</span></span> | <span data-ttu-id="16322-405">No</span><span class="sxs-lookup"><span data-stu-id="16322-405">No</span></span> |
| <span data-ttu-id="16322-406">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="16322-406">EgressHttpStatusOthers</span></span> | <span data-ttu-id="16322-407">Outbound data transfer for responses with other HTTP status codes in GB.</span><span class="sxs-lookup"><span data-stu-id="16322-407">Outbound data transfer for responses with other HTTP status codes in GB.</span></span> | <span data-ttu-id="16322-408">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-408">Yes</span></span> | <span data-ttu-id="16322-409">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-409">Yes</span></span> | <span data-ttu-id="16322-410">No</span><span class="sxs-lookup"><span data-stu-id="16322-410">No</span></span>  |
| <span data-ttu-id="16322-411">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="16322-411">EgressCacheHit</span></span> | <span data-ttu-id="16322-412">Outbound data transfer for responses that were delivered directly from the CDN cache on the CDN POPs/Edges.</span><span class="sxs-lookup"><span data-stu-id="16322-412">Outbound data transfer for responses that were delivered directly from the CDN cache on the CDN POPs/Edges.</span></span> | <span data-ttu-id="16322-413">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-413">Yes</span></span> | <span data-ttu-id="16322-414">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-414">Yes</span></span> | <span data-ttu-id="16322-415">No</span><span class="sxs-lookup"><span data-stu-id="16322-415">No</span></span> |
| <span data-ttu-id="16322-416">EgressCacheMiss.</span><span class="sxs-lookup"><span data-stu-id="16322-416">EgressCacheMiss.</span></span> | <span data-ttu-id="16322-417">Outbound data transfer for responses that were not found on the nearest POP server, and retrieved from the origin server.</span><span class="sxs-lookup"><span data-stu-id="16322-417">Outbound data transfer for responses that were not found on the nearest POP server, and retrieved from the origin server.</span></span> | <span data-ttu-id="16322-418">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-418">Yes</span></span> | <span data-ttu-id="16322-419">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-419">Yes</span></span> | <span data-ttu-id="16322-420">No</span><span class="sxs-lookup"><span data-stu-id="16322-420">No</span></span> |
| <span data-ttu-id="16322-421">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="16322-421">EgressCacheNoCache</span></span> | <span data-ttu-id="16322-422">Outbound data transfer for assets that are prevented from being cached due to a user configuration on the edge.</span><span class="sxs-lookup"><span data-stu-id="16322-422">Outbound data transfer for assets that are prevented from being cached due to a user configuration on the edge.</span></span> | <span data-ttu-id="16322-423">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-423">Yes</span></span> | <span data-ttu-id="16322-424">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-424">Yes</span></span> | <span data-ttu-id="16322-425">No</span><span class="sxs-lookup"><span data-stu-id="16322-425">No</span></span> |
| <span data-ttu-id="16322-426">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="16322-426">EgressCacheUncacheable</span></span> | <span data-ttu-id="16322-427">Outbound data transfer for assets that are prevented from being cached by the asset's Cache-Control and/or Expires headers.</span><span class="sxs-lookup"><span data-stu-id="16322-427">Outbound data transfer for assets that are prevented from being cached by the asset's Cache-Control and/or Expires headers.</span></span> <span data-ttu-id="16322-428">Indicates that it should not be cached on a POP or by the HTTP client.</span><span class="sxs-lookup"><span data-stu-id="16322-428">Indicates that it should not be cached on a POP or by the HTTP client.</span></span> | <span data-ttu-id="16322-429">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-429">Yes</span></span> | <span data-ttu-id="16322-430">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-430">Yes</span></span> | <span data-ttu-id="16322-431">No</span><span class="sxs-lookup"><span data-stu-id="16322-431">No</span></span> |
| <span data-ttu-id="16322-432">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="16322-432">EgressCacheOthers</span></span> | <span data-ttu-id="16322-433">Outbound data transfers for other cache scenarios.</span><span class="sxs-lookup"><span data-stu-id="16322-433">Outbound data transfers for other cache scenarios.</span></span> | <span data-ttu-id="16322-434">No</span><span class="sxs-lookup"><span data-stu-id="16322-434">No</span></span> | <span data-ttu-id="16322-435">Yes</span><span class="sxs-lookup"><span data-stu-id="16322-435">Yes</span></span> | <span data-ttu-id="16322-436">No</span><span class="sxs-lookup"><span data-stu-id="16322-436">No</span></span> |

<span data-ttu-id="16322-437">\*Outbound data transfer refers to traffic delivered from CDN POP servers to the client.</span><span class="sxs-lookup"><span data-stu-id="16322-437">\*Outbound data transfer refers to traffic delivered from CDN POP servers to the client.</span></span>


### <a name="schema-of-the-core-analytics-logs"></a><span data-ttu-id="16322-438">Schema of the core analytics logs</span><span class="sxs-lookup"><span data-stu-id="16322-438">Schema of the core analytics logs</span></span> 

<span data-ttu-id="16322-439">All logs are stored in JSON format and each entry has string fields according to the following schema:</span><span class="sxs-lookup"><span data-stu-id="16322-439">All logs are stored in JSON format and each entry has string fields according to the following schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="16322-440">Where *time* represents the start time of the hour boundary for which the statistics is reported.</span><span class="sxs-lookup"><span data-stu-id="16322-440">Where *time* represents the start time of the hour boundary for which the statistics is reported.</span></span> <span data-ttu-id="16322-441">When a metric is not supported by a CDN provider, instead of a double or integer value, there is a null value.</span><span class="sxs-lookup"><span data-stu-id="16322-441">When a metric is not supported by a CDN provider, instead of a double or integer value, there is a null value.</span></span> <span data-ttu-id="16322-442">This null value indicates the absence of a metric, and is different from a value of 0.</span><span class="sxs-lookup"><span data-stu-id="16322-442">This null value indicates the absence of a metric, and is different from a value of 0.</span></span> <span data-ttu-id="16322-443">There is one set of these metrics per domain configured on the endpoint.</span><span class="sxs-lookup"><span data-stu-id="16322-443">There is one set of these metrics per domain configured on the endpoint.</span></span>

<span data-ttu-id="16322-444">Example properties:</span><span class="sxs-lookup"><span data-stu-id="16322-444">Example properties:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="16322-445">Additional resources</span><span class="sxs-lookup"><span data-stu-id="16322-445">Additional resources</span></span>

* [<span data-ttu-id="16322-446">Azure Diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="16322-446">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="16322-447">Core analytics via Azure CDN supplemental portal</span><span class="sxs-lookup"><span data-stu-id="16322-447">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="16322-448">Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="16322-448">Azure Log Analytics</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="16322-449">Azure Log Analytics REST API</span><span class="sxs-lookup"><span data-stu-id="16322-449">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/rest/api/loganalytics)







