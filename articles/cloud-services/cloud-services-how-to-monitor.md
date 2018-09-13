---
title: How to monitor a cloud service | Microsoft Docs
description: Learn how to monitor cloud services by using the Azure classic portal.
services: cloud-services
documentationcenter: ''
author: thraka
manager: timlt
editor: ''
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: 8d29322f3fd8f4c0081004483b401aae72f84682
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554912"
---
# <a name="how-to-monitor-cloud-services"></a><span data-ttu-id="16d09-103">How to Monitor Cloud Services</span><span class="sxs-lookup"><span data-stu-id="16d09-103">How to Monitor Cloud Services</span></span>
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

<span data-ttu-id="16d09-104">You can monitor `key` performance metrics for your cloud services in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="16d09-104">You can monitor `key` performance metrics for your cloud services in the Azure classic portal.</span></span> <span data-ttu-id="16d09-105">You can set the level of monitoring to minimal and verbose for each service role, and can customize the monitoring displays.</span><span class="sxs-lookup"><span data-stu-id="16d09-105">You can set the level of monitoring to minimal and verbose for each service role, and can customize the monitoring displays.</span></span> <span data-ttu-id="16d09-106">Verbose monitoring data is stored in a storage account, which you can access outside the portal.</span><span class="sxs-lookup"><span data-stu-id="16d09-106">Verbose monitoring data is stored in a storage account, which you can access outside the portal.</span></span> 

<span data-ttu-id="16d09-107">Monitoring displays in the Azure classic portal are highly configurable.</span><span class="sxs-lookup"><span data-stu-id="16d09-107">Monitoring displays in the Azure classic portal are highly configurable.</span></span> <span data-ttu-id="16d09-108">You can choose the metrics you want to monitor in the metrics list on the **Monitor** page, and you can choose which metrics to plot in metrics charts on the **Monitor** page and the dashboard.</span><span class="sxs-lookup"><span data-stu-id="16d09-108">You can choose the metrics you want to monitor in the metrics list on the **Monitor** page, and you can choose which metrics to plot in metrics charts on the **Monitor** page and the dashboard.</span></span> 

## <a name="concepts"></a><span data-ttu-id="16d09-109">Concepts</span><span class="sxs-lookup"><span data-stu-id="16d09-109">Concepts</span></span>
<span data-ttu-id="16d09-110">By default, minimal monitoring is provided for a new cloud service using performance counters gathered from the host operating system for the roles instances (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="16d09-110">By default, minimal monitoring is provided for a new cloud service using performance counters gathered from the host operating system for the roles instances (virtual machines).</span></span> <span data-ttu-id="16d09-111">The minimal metrics are limited to CPU Percentage, Data In, Data Out, Disk Read Throughput, and Disk Write Throughput.</span><span class="sxs-lookup"><span data-stu-id="16d09-111">The minimal metrics are limited to CPU Percentage, Data In, Data Out, Disk Read Throughput, and Disk Write Throughput.</span></span> <span data-ttu-id="16d09-112">By configuring verbose monitoring, you can receive additional metrics based on performance data within the virtual machines (role instances).</span><span class="sxs-lookup"><span data-stu-id="16d09-112">By configuring verbose monitoring, you can receive additional metrics based on performance data within the virtual machines (role instances).</span></span> <span data-ttu-id="16d09-113">The verbose metrics enable closer analysis of issues that occur during application operations.</span><span class="sxs-lookup"><span data-stu-id="16d09-113">The verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="16d09-114">By default performance counter data from role instances is sampled and transferred from the role instance at 3-minute intervals.</span><span class="sxs-lookup"><span data-stu-id="16d09-114">By default performance counter data from role instances is sampled and transferred from the role instance at 3-minute intervals.</span></span> <span data-ttu-id="16d09-115">When you enable verbose monitoring, the raw performance counter data is aggregated for each role instance and across role instances for each role at intervals of 5 minutes, 1 hour, and 12 hours.</span><span class="sxs-lookup"><span data-stu-id="16d09-115">When you enable verbose monitoring, the raw performance counter data is aggregated for each role instance and across role instances for each role at intervals of 5 minutes, 1 hour, and 12 hours.</span></span> <span data-ttu-id="16d09-116">The aggregated data is purged after 10 days.</span><span class="sxs-lookup"><span data-stu-id="16d09-116">The aggregated data is purged after 10 days.</span></span>

<span data-ttu-id="16d09-117">After you enable verbose monitoring, the aggregated monitoring data is stored in tables in your storage account.</span><span class="sxs-lookup"><span data-stu-id="16d09-117">After you enable verbose monitoring, the aggregated monitoring data is stored in tables in your storage account.</span></span> <span data-ttu-id="16d09-118">To enable verbose monitoring for a role, you must configure a diagnostics connection string that links to the storage account.</span><span class="sxs-lookup"><span data-stu-id="16d09-118">To enable verbose monitoring for a role, you must configure a diagnostics connection string that links to the storage account.</span></span> <span data-ttu-id="16d09-119">You can use different storage accounts for different roles.</span><span class="sxs-lookup"><span data-stu-id="16d09-119">You can use different storage accounts for different roles.</span></span>

<span data-ttu-id="16d09-120">Enabling verbose monitoring increases your storage costs related to data storage, data transfer, and storage transactions.</span><span class="sxs-lookup"><span data-stu-id="16d09-120">Enabling verbose monitoring increases your storage costs related to data storage, data transfer, and storage transactions.</span></span> <span data-ttu-id="16d09-121">Minimal monitoring does not require a storage account.</span><span class="sxs-lookup"><span data-stu-id="16d09-121">Minimal monitoring does not require a storage account.</span></span> <span data-ttu-id="16d09-122">The data for the metrics that are exposed at the minimal monitoring level are not stored in your storage account, even if you set the monitoring level to verbose.</span><span class="sxs-lookup"><span data-stu-id="16d09-122">The data for the metrics that are exposed at the minimal monitoring level are not stored in your storage account, even if you set the monitoring level to verbose.</span></span>

## <a name="how-to-configure-monitoring-for-cloud-services"></a><span data-ttu-id="16d09-123">How to: Configure monitoring for cloud services</span><span class="sxs-lookup"><span data-stu-id="16d09-123">How to: Configure monitoring for cloud services</span></span>
<span data-ttu-id="16d09-124">Use the following procedures to configure verbose or minimal monitoring in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="16d09-124">Use the following procedures to configure verbose or minimal monitoring in the Azure classic portal.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="16d09-125">Before you begin</span><span class="sxs-lookup"><span data-stu-id="16d09-125">Before you begin</span></span>
* <span data-ttu-id="16d09-126">Create a *classic* storage account to store the monitoring data.</span><span class="sxs-lookup"><span data-stu-id="16d09-126">Create a *classic* storage account to store the monitoring data.</span></span> <span data-ttu-id="16d09-127">You can use different storage accounts for different roles.</span><span class="sxs-lookup"><span data-stu-id="16d09-127">You can use different storage accounts for different roles.</span></span> <span data-ttu-id="16d09-128">For more information, see [How to create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="16d09-128">For more information, see [How to create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="16d09-129">Enable Azure Diagnostics for your cloud service roles.</span><span class="sxs-lookup"><span data-stu-id="16d09-129">Enable Azure Diagnostics for your cloud service roles.</span></span> <span data-ttu-id="16d09-130">See [Configuring Diagnostics for Cloud Services](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="16d09-130">See [Configuring Diagnostics for Cloud Services](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="16d09-131">Ensure that the diagnostics connection string is present in the Role configuration.</span><span class="sxs-lookup"><span data-stu-id="16d09-131">Ensure that the diagnostics connection string is present in the Role configuration.</span></span> <span data-ttu-id="16d09-132">You cannot turn on verbose monitoring until you enable Azure Diagnostics and include a diagnostics connection string in the Role configuration.</span><span class="sxs-lookup"><span data-stu-id="16d09-132">You cannot turn on verbose monitoring until you enable Azure Diagnostics and include a diagnostics connection string in the Role configuration.</span></span>   

> [!NOTE]
> <span data-ttu-id="16d09-133">Projects targeting Azure SDK 2.5 did not automatically include the diagnostics connection string in the project template.</span><span class="sxs-lookup"><span data-stu-id="16d09-133">Projects targeting Azure SDK 2.5 did not automatically include the diagnostics connection string in the project template.</span></span> <span data-ttu-id="16d09-134">For these projects, you need to manually add the diagnostics connection string to the Role configuration.</span><span class="sxs-lookup"><span data-stu-id="16d09-134">For these projects, you need to manually add the diagnostics connection string to the Role configuration.</span></span>
> 
> 

<span data-ttu-id="16d09-135">**To manually add diagnostics connection string to Role configuration**</span><span class="sxs-lookup"><span data-stu-id="16d09-135">**To manually add diagnostics connection string to Role configuration**</span></span>

1. <span data-ttu-id="16d09-136">Open the Cloud Service project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16d09-136">Open the Cloud Service project in Visual Studio</span></span>
2. <span data-ttu-id="16d09-137">Double-click on the **Role** to open the Role designer and select the **Settings** tab</span><span class="sxs-lookup"><span data-stu-id="16d09-137">Double-click on the **Role** to open the Role designer and select the **Settings** tab</span></span>
3. <span data-ttu-id="16d09-138">Look for a setting named **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="16d09-138">Look for a setting named **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**.</span></span> 
4. <span data-ttu-id="16d09-139">If this setting is not present, click on the **Add Setting** button to add it to the configuration and change the type for the new setting to **ConnectionString**</span><span class="sxs-lookup"><span data-stu-id="16d09-139">If this setting is not present, click on the **Add Setting** button to add it to the configuration and change the type for the new setting to **ConnectionString**</span></span>
5. <span data-ttu-id="16d09-140">Set the value for connection string the by clicking on the **...** button.</span><span class="sxs-lookup"><span data-stu-id="16d09-140">Set the value for connection string the by clicking on the **...** button.</span></span> <span data-ttu-id="16d09-141">This will open up a dialog allowing you to select a storage account.</span><span class="sxs-lookup"><span data-stu-id="16d09-141">This will open up a dialog allowing you to select a storage account.</span></span>
   
    ![Visual Studio Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="to-change-the-monitoring-level-to-verbose-or-minimal"></a><span data-ttu-id="16d09-143">To change the monitoring level to verbose or minimal</span><span class="sxs-lookup"><span data-stu-id="16d09-143">To change the monitoring level to verbose or minimal</span></span>
1. <span data-ttu-id="16d09-144">In the [Azure classic portal](https://manage.windowsazure.com/), open the **Configure** page for the cloud service deployment.</span><span class="sxs-lookup"><span data-stu-id="16d09-144">In the [Azure classic portal](https://manage.windowsazure.com/), open the **Configure** page for the cloud service deployment.</span></span>
2. <span data-ttu-id="16d09-145">In **Level**, click **Verbose** or **Minimal**.</span><span class="sxs-lookup"><span data-stu-id="16d09-145">In **Level**, click **Verbose** or **Minimal**.</span></span> 
3. <span data-ttu-id="16d09-146">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="16d09-146">Click **Save**.</span></span>

<span data-ttu-id="16d09-147">After you turn on verbose monitoring, you should start seeing the monitoring data in the Azure classic portal within the hour.</span><span class="sxs-lookup"><span data-stu-id="16d09-147">After you turn on verbose monitoring, you should start seeing the monitoring data in the Azure classic portal within the hour.</span></span>

<span data-ttu-id="16d09-148">The raw performance counter data and aggregated monitoring data are stored in the storage account in tables qualified by the deployment ID for the roles.</span><span class="sxs-lookup"><span data-stu-id="16d09-148">The raw performance counter data and aggregated monitoring data are stored in the storage account in tables qualified by the deployment ID for the roles.</span></span> 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a><span data-ttu-id="16d09-149">How to: Receive alerts for cloud service metrics</span><span class="sxs-lookup"><span data-stu-id="16d09-149">How to: Receive alerts for cloud service metrics</span></span>
<span data-ttu-id="16d09-150">You can receive alerts based on your cloud service monitoring metrics.</span><span class="sxs-lookup"><span data-stu-id="16d09-150">You can receive alerts based on your cloud service monitoring metrics.</span></span> <span data-ttu-id="16d09-151">On the **Management Services** page of the Azure classic portal, you can create a rule to trigger an alert when the metric you choose reaches a value that you specify.</span><span class="sxs-lookup"><span data-stu-id="16d09-151">On the **Management Services** page of the Azure classic portal, you can create a rule to trigger an alert when the metric you choose reaches a value that you specify.</span></span> <span data-ttu-id="16d09-152">You can also choose to have email sent when the alert is triggered.</span><span class="sxs-lookup"><span data-stu-id="16d09-152">You can also choose to have email sent when the alert is triggered.</span></span> <span data-ttu-id="16d09-153">For more information, see [How to: Receive Alert Notifications and Manage Alert Rules in Azure](http://go.microsoft.com/fwlink/?LinkId=309356).</span><span class="sxs-lookup"><span data-stu-id="16d09-153">For more information, see [How to: Receive Alert Notifications and Manage Alert Rules in Azure](http://go.microsoft.com/fwlink/?LinkId=309356).</span></span>

## <a name="how-to-add-metrics-to-the-metrics-table"></a><span data-ttu-id="16d09-154">How to: Add metrics to the metrics table</span><span class="sxs-lookup"><span data-stu-id="16d09-154">How to: Add metrics to the metrics table</span></span>
1. <span data-ttu-id="16d09-155">In the [Azure classic portal](http://manage.windowsazure.com/), open the **Monitor** page for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="16d09-155">In the [Azure classic portal](http://manage.windowsazure.com/), open the **Monitor** page for the cloud service.</span></span>
   
    <span data-ttu-id="16d09-156">By default, the metrics table displays a subset of the available metrics.</span><span class="sxs-lookup"><span data-stu-id="16d09-156">By default, the metrics table displays a subset of the available metrics.</span></span> <span data-ttu-id="16d09-157">The illustration shows the default verbose metrics for a cloud service, which is limited to the Memory\Available MBytes performance counter, with data aggregated at the role level.</span><span class="sxs-lookup"><span data-stu-id="16d09-157">The illustration shows the default verbose metrics for a cloud service, which is limited to the Memory\Available MBytes performance counter, with data aggregated at the role level.</span></span> <span data-ttu-id="16d09-158">Use **Add Metrics** to select additional aggregate and role-level metrics to monitor in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="16d09-158">Use **Add Metrics** to select additional aggregate and role-level metrics to monitor in the Azure classic portal.</span></span>
   
    ![Verbose display](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. <span data-ttu-id="16d09-160">To add metrics to the metrics table:</span><span class="sxs-lookup"><span data-stu-id="16d09-160">To add metrics to the metrics table:</span></span>
   
   1. <span data-ttu-id="16d09-161">Click **Add Metrics** to open **Choose Metrics**, shown below.</span><span class="sxs-lookup"><span data-stu-id="16d09-161">Click **Add Metrics** to open **Choose Metrics**, shown below.</span></span>
      
       <span data-ttu-id="16d09-162">The first available metric is expanded to show options that are available.</span><span class="sxs-lookup"><span data-stu-id="16d09-162">The first available metric is expanded to show options that are available.</span></span> <span data-ttu-id="16d09-163">For each metric, the top option displays aggregated monitoring data for all roles.</span><span class="sxs-lookup"><span data-stu-id="16d09-163">For each metric, the top option displays aggregated monitoring data for all roles.</span></span> <span data-ttu-id="16d09-164">In addition, you can choose individual roles to display data for.</span><span class="sxs-lookup"><span data-stu-id="16d09-164">In addition, you can choose individual roles to display data for.</span></span>
      
       ![Add metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. <span data-ttu-id="16d09-166">To select metrics to display</span><span class="sxs-lookup"><span data-stu-id="16d09-166">To select metrics to display</span></span>
      
      * <span data-ttu-id="16d09-167">Click the down arrow by the metric to expand the monitoring options.</span><span class="sxs-lookup"><span data-stu-id="16d09-167">Click the down arrow by the metric to expand the monitoring options.</span></span>
      * <span data-ttu-id="16d09-168">Select the check box for each monitoring option you want to display.</span><span class="sxs-lookup"><span data-stu-id="16d09-168">Select the check box for each monitoring option you want to display.</span></span>
        
        <span data-ttu-id="16d09-169">You can display up to 50 metrics in the metrics table.</span><span class="sxs-lookup"><span data-stu-id="16d09-169">You can display up to 50 metrics in the metrics table.</span></span>
        
        > [!TIP]
        > <span data-ttu-id="16d09-170">In verbose monitoring, the metrics list can contain dozens of metrics.</span><span class="sxs-lookup"><span data-stu-id="16d09-170">In verbose monitoring, the metrics list can contain dozens of metrics.</span></span> <span data-ttu-id="16d09-171">To display a scrollbar, hover over the right side of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="16d09-171">To display a scrollbar, hover over the right side of the dialog box.</span></span> <span data-ttu-id="16d09-172">To filter the list, click the search icon, and enter text in the search box, as shown below.</span><span class="sxs-lookup"><span data-stu-id="16d09-172">To filter the list, click the search icon, and enter text in the search box, as shown below.</span></span>
        > 
        > 
        
        ![Add metrics search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. <span data-ttu-id="16d09-174">After you finish selecting metrics, click OK (checkmark).</span><span class="sxs-lookup"><span data-stu-id="16d09-174">After you finish selecting metrics, click OK (checkmark).</span></span>
   
    <span data-ttu-id="16d09-175">The selected metrics are added to the metrics table, as shown below.</span><span class="sxs-lookup"><span data-stu-id="16d09-175">The selected metrics are added to the metrics table, as shown below.</span></span>
   
    ![monitor metrics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. <span data-ttu-id="16d09-177">To delete a metric from the metrics table, click the metric to select it, and then click **Delete Metric**.</span><span class="sxs-lookup"><span data-stu-id="16d09-177">To delete a metric from the metrics table, click the metric to select it, and then click **Delete Metric**.</span></span> <span data-ttu-id="16d09-178">(You only see **Delete Metric** when you have a metric selected.)</span><span class="sxs-lookup"><span data-stu-id="16d09-178">(You only see **Delete Metric** when you have a metric selected.)</span></span>

### <a name="to-add-custom-metrics-to-the-metrics-table"></a><span data-ttu-id="16d09-179">To add custom metrics to the metrics table</span><span class="sxs-lookup"><span data-stu-id="16d09-179">To add custom metrics to the metrics table</span></span>
<span data-ttu-id="16d09-180">The **Verbose** monitoring level provides a list of default metrics that you can monitor on the portal.</span><span class="sxs-lookup"><span data-stu-id="16d09-180">The **Verbose** monitoring level provides a list of default metrics that you can monitor on the portal.</span></span> <span data-ttu-id="16d09-181">In addition to these you can monitor any custom metrics or performance counters defined by your application through the portal.</span><span class="sxs-lookup"><span data-stu-id="16d09-181">In addition to these you can monitor any custom metrics or performance counters defined by your application through the portal.</span></span>

<span data-ttu-id="16d09-182">The following steps assume that you have turned on **Verbose** monitoring level and have configured your application to collect and transfer custom performance counters.</span><span class="sxs-lookup"><span data-stu-id="16d09-182">The following steps assume that you have turned on **Verbose** monitoring level and have configured your application to collect and transfer custom performance counters.</span></span> 

<span data-ttu-id="16d09-183">To display the custom performance counters in the portal you need to update the configuration in wad-control-container:</span><span class="sxs-lookup"><span data-stu-id="16d09-183">To display the custom performance counters in the portal you need to update the configuration in wad-control-container:</span></span>

1. <span data-ttu-id="16d09-184">Open the wad-control-container blob in your diagnostics storage account.</span><span class="sxs-lookup"><span data-stu-id="16d09-184">Open the wad-control-container blob in your diagnostics storage account.</span></span> <span data-ttu-id="16d09-185">You can use Visual Studio or any other storage explorer to do this.</span><span class="sxs-lookup"><span data-stu-id="16d09-185">You can use Visual Studio or any other storage explorer to do this.</span></span>
   
    ![Visual Studio Server Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. <span data-ttu-id="16d09-187">Navigate the blob path using the pattern **DeploymentId/RoleName/RoleInstance** to find the configuration for your role instance.</span><span class="sxs-lookup"><span data-stu-id="16d09-187">Navigate the blob path using the pattern **DeploymentId/RoleName/RoleInstance** to find the configuration for your role instance.</span></span> 
   
    ![Visual Studio Storage Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. <span data-ttu-id="16d09-189">Download the configuration file for your role instance and update it to include any custom performance counters.</span><span class="sxs-lookup"><span data-stu-id="16d09-189">Download the configuration file for your role instance and update it to include any custom performance counters.</span></span> <span data-ttu-id="16d09-190">For example to monitor *Disk Write Bytes/sec* for the *C drive* add the following under **PerformanceCounters\Subscriptions** node</span><span class="sxs-lookup"><span data-stu-id="16d09-190">For example to monitor *Disk Write Bytes/sec* for the *C drive* add the following under **PerformanceCounters\Subscriptions** node</span></span>
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. <span data-ttu-id="16d09-191">Save the changes and upload the configuration file back to the same location overwriting the existing file in the blob.</span><span class="sxs-lookup"><span data-stu-id="16d09-191">Save the changes and upload the configuration file back to the same location overwriting the existing file in the blob.</span></span>
5. <span data-ttu-id="16d09-192">Toggle to Verbose mode in the Azure classic portal configuration.</span><span class="sxs-lookup"><span data-stu-id="16d09-192">Toggle to Verbose mode in the Azure classic portal configuration.</span></span> <span data-ttu-id="16d09-193">If you were in Verbose mode already you will have to toggle to minimal and back to verbose.</span><span class="sxs-lookup"><span data-stu-id="16d09-193">If you were in Verbose mode already you will have to toggle to minimal and back to verbose.</span></span>
6. <span data-ttu-id="16d09-194">The custom performance counter will now be available in the **Add Metrics** dialog box.</span><span class="sxs-lookup"><span data-stu-id="16d09-194">The custom performance counter will now be available in the **Add Metrics** dialog box.</span></span> 

## <a name="how-to-customize-the-metrics-chart"></a><span data-ttu-id="16d09-195">How to: Customize the metrics chart</span><span class="sxs-lookup"><span data-stu-id="16d09-195">How to: Customize the metrics chart</span></span>
1. <span data-ttu-id="16d09-196">In the metrics table, select up to 6 metrics to plot on the metrics chart.</span><span class="sxs-lookup"><span data-stu-id="16d09-196">In the metrics table, select up to 6 metrics to plot on the metrics chart.</span></span> <span data-ttu-id="16d09-197">To select a metric, click the check box on its left side.</span><span class="sxs-lookup"><span data-stu-id="16d09-197">To select a metric, click the check box on its left side.</span></span> <span data-ttu-id="16d09-198">To remove a metric from the metrics chart, clear its check box in the metrics table.</span><span class="sxs-lookup"><span data-stu-id="16d09-198">To remove a metric from the metrics chart, clear its check box in the metrics table.</span></span>
   
    <span data-ttu-id="16d09-199">As you select metrics in the metrics table, the metrics are added to the metrics chart.</span><span class="sxs-lookup"><span data-stu-id="16d09-199">As you select metrics in the metrics table, the metrics are added to the metrics chart.</span></span> <span data-ttu-id="16d09-200">On a narrow display, an **n more** drop-down list contains metric headers that won't fit the display.</span><span class="sxs-lookup"><span data-stu-id="16d09-200">On a narrow display, an **n more** drop-down list contains metric headers that won't fit the display.</span></span>
2. <span data-ttu-id="16d09-201">To switch between displaying relative values (final value only for each metric) and absolute values (Y axis displayed), select Relative or Absolute at the top of the chart.</span><span class="sxs-lookup"><span data-stu-id="16d09-201">To switch between displaying relative values (final value only for each metric) and absolute values (Y axis displayed), select Relative or Absolute at the top of the chart.</span></span>
   
    ![Relative or Absolute](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. <span data-ttu-id="16d09-203">To change the time range the metrics chart displays, select 1 hour, 24 hours, or 7 days at the top of the chart.</span><span class="sxs-lookup"><span data-stu-id="16d09-203">To change the time range the metrics chart displays, select 1 hour, 24 hours, or 7 days at the top of the chart.</span></span>
   
    ![Monitor display period](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    <span data-ttu-id="16d09-205">On the dashboard metrics chart, the method for plotting metrics is different.</span><span class="sxs-lookup"><span data-stu-id="16d09-205">On the dashboard metrics chart, the method for plotting metrics is different.</span></span> <span data-ttu-id="16d09-206">A standard set of metrics is available, and metrics are added or removed by selecting the metric header.</span><span class="sxs-lookup"><span data-stu-id="16d09-206">A standard set of metrics is available, and metrics are added or removed by selecting the metric header.</span></span>

### <a name="to-customize-the-metrics-chart-on-the-dashboard"></a><span data-ttu-id="16d09-207">To customize the metrics chart on the dashboard</span><span class="sxs-lookup"><span data-stu-id="16d09-207">To customize the metrics chart on the dashboard</span></span>
1. <span data-ttu-id="16d09-208">Open the dashboard for the cloud service.</span><span class="sxs-lookup"><span data-stu-id="16d09-208">Open the dashboard for the cloud service.</span></span>
2. <span data-ttu-id="16d09-209">Add or remove metrics from the chart:</span><span class="sxs-lookup"><span data-stu-id="16d09-209">Add or remove metrics from the chart:</span></span>
   
   * <span data-ttu-id="16d09-210">To plot a new metric, select the check box for the metric in the chart headers.</span><span class="sxs-lookup"><span data-stu-id="16d09-210">To plot a new metric, select the check box for the metric in the chart headers.</span></span> <span data-ttu-id="16d09-211">On a narrow display, click the down arrow by \***n\*??metrics** to plot a metric the chart header area can't display.</span><span class="sxs-lookup"><span data-stu-id="16d09-211">On a narrow display, click the down arrow by \***n\*??metrics** to plot a metric the chart header area can't display.</span></span>
   * <span data-ttu-id="16d09-212">To delete a metric that is plotted on the chart, clear the check box by its header.</span><span class="sxs-lookup"><span data-stu-id="16d09-212">To delete a metric that is plotted on the chart, clear the check box by its header.</span></span>
   
3. <span data-ttu-id="16d09-213">Switch between **Relative** and **Absolute** displays.</span><span class="sxs-lookup"><span data-stu-id="16d09-213">Switch between **Relative** and **Absolute** displays.</span></span>
4. <span data-ttu-id="16d09-214">Choose 1 hour, 24 hours, or 7 days of data to display.</span><span class="sxs-lookup"><span data-stu-id="16d09-214">Choose 1 hour, 24 hours, or 7 days of data to display.</span></span>

## <a name="how-to-access-verbose-monitoring-data-outside-the-azure-classic-portal"></a><span data-ttu-id="16d09-215">How to: Access verbose monitoring data outside the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="16d09-215">How to: Access verbose monitoring data outside the Azure classic portal</span></span>
<span data-ttu-id="16d09-216">Verbose monitoring data is stored in tables in the storage accounts that you specify for each role.</span><span class="sxs-lookup"><span data-stu-id="16d09-216">Verbose monitoring data is stored in tables in the storage accounts that you specify for each role.</span></span> <span data-ttu-id="16d09-217">For each cloud service deployment, six tables are created for the role.</span><span class="sxs-lookup"><span data-stu-id="16d09-217">For each cloud service deployment, six tables are created for the role.</span></span> <span data-ttu-id="16d09-218">Two tables are created for each (5 minutes, 1 hour, and 12 hours).</span><span class="sxs-lookup"><span data-stu-id="16d09-218">Two tables are created for each (5 minutes, 1 hour, and 12 hours).</span></span> <span data-ttu-id="16d09-219">One of these tables stores role-level aggregations; the other table stores aggregations for role instances.</span><span class="sxs-lookup"><span data-stu-id="16d09-219">One of these tables stores role-level aggregations; the other table stores aggregations for role instances.</span></span> 

<span data-ttu-id="16d09-220">The table names have the following format:</span><span class="sxs-lookup"><span data-stu-id="16d09-220">The table names have the following format:</span></span>

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

<span data-ttu-id="16d09-221">where:</span><span class="sxs-lookup"><span data-stu-id="16d09-221">where:</span></span>

* <span data-ttu-id="16d09-222">*deploymentID* is the GUID assigned to the cloud service deployment</span><span class="sxs-lookup"><span data-stu-id="16d09-222">*deploymentID* is the GUID assigned to the cloud service deployment</span></span>
* <span data-ttu-id="16d09-223">*aggregation_interval* = 5M, 1H, or 12H</span><span class="sxs-lookup"><span data-stu-id="16d09-223">*aggregation_interval* = 5M, 1H, or 12H</span></span>
* <span data-ttu-id="16d09-224">role-level aggregations = R</span><span class="sxs-lookup"><span data-stu-id="16d09-224">role-level aggregations = R</span></span>
* <span data-ttu-id="16d09-225">aggregations for role instances = RI</span><span class="sxs-lookup"><span data-stu-id="16d09-225">aggregations for role instances = RI</span></span>

<span data-ttu-id="16d09-226">For example, the following tables would store verbose monitoring data aggregated at 1-hour intervals:</span><span class="sxs-lookup"><span data-stu-id="16d09-226">For example, the following tables would store verbose monitoring data aggregated at 1-hour intervals:</span></span>

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for the role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```









