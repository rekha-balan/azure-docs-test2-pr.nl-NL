---
title: How to monitor an Azure Storage account | Microsoft Docs
description: Learn how to monitor a storage account in Azure by using the Azure portal.
services: storage
documentationcenter: ''
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 4e3aae255233b37e2e5a6b2191f177aae943e89e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670047"
---
# <a name="monitor-a-storage-account-in-the-azure-portal"></a><span data-ttu-id="51591-103">Monitor a storage account in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="51591-103">Monitor a storage account in the Azure portal</span></span>

<span data-ttu-id="51591-104">[Azure Storage Analytics](storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span><span class="sxs-lookup"><span data-stu-id="51591-104">[Azure Storage Analytics](storage-analytics.md) provides metrics for all storage services, and logs for blobs, queues, and tables.</span></span> <span data-ttu-id="51591-105">You can use the [Azure portal](https://portal.azure.com) to configure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span><span class="sxs-lookup"><span data-stu-id="51591-105">You can use the [Azure portal](https://portal.azure.com) to configure which metrics and logs are recorded for your account, and configure charts that provide visual representations of your metrics data.</span></span>

> [!NOTE]
> <span data-ttu-id="51591-106">There are costs associated with examining monitoring data in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="51591-106">There are costs associated with examining monitoring data in the Azure portal.</span></span> <span data-ttu-id="51591-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/fileservices/Storage-Analytics-and-Billing).</span><span class="sxs-lookup"><span data-stu-id="51591-107">For more information, see [Storage Analytics and Billing](/rest/api/storageservices/fileservices/Storage-Analytics-and-Billing).</span></span>
>
> <span data-ttu-id="51591-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span><span class="sxs-lookup"><span data-stu-id="51591-108">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>
> <span data-ttu-id="51591-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have the metrics or logging capability enabled.</span><span class="sxs-lookup"><span data-stu-id="51591-109">Storage accounts with a replication type of Zone-Redundant Storage (ZRS) currently do not have the metrics or logging capability enabled.</span></span>
> 
> <span data-ttu-id="51591-110">For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="51591-110">For an in-depth guide on using Storage Analytics and other tools to identify, diagnose, and troubleshoot Azure Storage-related issues, see [Monitor, diagnose, and troubleshoot Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>
>

## <a name="configure-monitoring-for-a-storage-account"></a><span data-ttu-id="51591-111">Configure monitoring for a storage account</span><span class="sxs-lookup"><span data-stu-id="51591-111">Configure monitoring for a storage account</span></span>

1. <span data-ttu-id="51591-112">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the storage account name to open the account dashboard.</span><span class="sxs-lookup"><span data-stu-id="51591-112">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the storage account name to open the account dashboard.</span></span>
1. <span data-ttu-id="51591-113">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span><span class="sxs-lookup"><span data-stu-id="51591-113">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![MonitoringOptions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. <span data-ttu-id="51591-115">Select the **type** of metrics data for each **service** you wish to monitor, and the **retention policy** for the data.</span><span class="sxs-lookup"><span data-stu-id="51591-115">Select the **type** of metrics data for each **service** you wish to monitor, and the **retention policy** for the data.</span></span> <span data-ttu-id="51591-116">You can also disable monitoring by setting **Status** to **Off**.</span><span class="sxs-lookup"><span data-stu-id="51591-116">You can also disable monitoring by setting **Status** to **Off**.</span></span>

    ![MonitoringOptions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   <span data-ttu-id="51591-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span><span class="sxs-lookup"><span data-stu-id="51591-118">There are two types of metrics you can enable for each service, both of which are enabled by default for new storage accounts:</span></span>

   * <span data-ttu-id="51591-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span><span class="sxs-lookup"><span data-stu-id="51591-119">**Aggregate**: Collects metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="51591-120">These metrics are aggregated for the blob, queue, table, and file services.</span><span class="sxs-lookup"><span data-stu-id="51591-120">These metrics are aggregated for the blob, queue, table, and file services.</span></span>
   * <span data-ttu-id="51591-121">**Per API**: In addition to the aggregate metrics, collects the same set of metrics for each storage operation in the Azure Storage service API.</span><span class="sxs-lookup"><span data-stu-id="51591-121">**Per API**: In addition to the aggregate metrics, collects the same set of metrics for each storage operation in the Azure Storage service API.</span></span>

   <span data-ttu-id="51591-122">To set the data retention policy, move the **Retention (days)** slider or enter the number of days of data to retain, from 1 to 365.</span><span class="sxs-lookup"><span data-stu-id="51591-122">To set the data retention policy, move the **Retention (days)** slider or enter the number of days of data to retain, from 1 to 365.</span></span> <span data-ttu-id="51591-123">The default for new storage accounts is seven days.</span><span class="sxs-lookup"><span data-stu-id="51591-123">The default for new storage accounts is seven days.</span></span> <span data-ttu-id="51591-124">If you do not want to set a retention policy, enter zero.</span><span class="sxs-lookup"><span data-stu-id="51591-124">If you do not want to set a retention policy, enter zero.</span></span> <span data-ttu-id="51591-125">If there is no retention policy, it is up to you to delete the monitoring data.</span><span class="sxs-lookup"><span data-stu-id="51591-125">If there is no retention policy, it is up to you to delete the monitoring data.</span></span>

   > [!WARNING]
   > <span data-ttu-id="51591-126">You are charged when you manually delete metrics data.</span><span class="sxs-lookup"><span data-stu-id="51591-126">You are charged when you manually delete metrics data.</span></span> <span data-ttu-id="51591-127">Stale analytics data (data older than your retention policy) is deleted by the system at no cost.</span><span class="sxs-lookup"><span data-stu-id="51591-127">Stale analytics data (data older than your retention policy) is deleted by the system at no cost.</span></span> <span data-ttu-id="51591-128">We recommend setting a retention policy based on how long you want to retain storage analytics data for your account.</span><span class="sxs-lookup"><span data-stu-id="51591-128">We recommend setting a retention policy based on how long you want to retain storage analytics data for your account.</span></span> <span data-ttu-id="51591-129">See [What charges do you incur when you enable storage metrics?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span><span class="sxs-lookup"><span data-stu-id="51591-129">See [What charges do you incur when you enable storage metrics?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) for more information.</span></span>
   >

1. <span data-ttu-id="51591-130">When you finish the monitoring configuration, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="51591-130">When you finish the monitoring configuration, select **Save**.</span></span>

<span data-ttu-id="51591-131">A default set of metrics is displayed in charts on the storage account blade, as well as the individual service blades (blob, queue, table, and file).</span><span class="sxs-lookup"><span data-stu-id="51591-131">A default set of metrics is displayed in charts on the storage account blade, as well as the individual service blades (blob, queue, table, and file).</span></span> <span data-ttu-id="51591-132">Once you've enabled metrics for a service, it may take up to an hour for data to appear in its charts.</span><span class="sxs-lookup"><span data-stu-id="51591-132">Once you've enabled metrics for a service, it may take up to an hour for data to appear in its charts.</span></span> <span data-ttu-id="51591-133">You can select **Edit** on any metric chart to [configure which metrics](#how-to-customize-metrics-charts) are displayed in the chart.</span><span class="sxs-lookup"><span data-stu-id="51591-133">You can select **Edit** on any metric chart to [configure which metrics](#how-to-customize-metrics-charts) are displayed in the chart.</span></span>

<span data-ttu-id="51591-134">You can disable metrics collection and logging by setting **Status** to **Off**.</span><span class="sxs-lookup"><span data-stu-id="51591-134">You can disable metrics collection and logging by setting **Status** to **Off**.</span></span>

> [!NOTE]
> <span data-ttu-id="51591-135">Azure Storage uses [table storage](storage-introduction.md#table-storage) to store the metrics for your storage account, and stores the metrics in tables in your account.</span><span class="sxs-lookup"><span data-stu-id="51591-135">Azure Storage uses [table storage](storage-introduction.md#table-storage) to store the metrics for your storage account, and stores the metrics in tables in your account.</span></span> <span data-ttu-id="51591-136">For more information, see.</span><span class="sxs-lookup"><span data-stu-id="51591-136">For more information, see.</span></span> <span data-ttu-id="51591-137">[How metrics are stored](storage-analytics.md#how-metrics-are-stored).</span><span class="sxs-lookup"><span data-stu-id="51591-137">[How metrics are stored](storage-analytics.md#how-metrics-are-stored).</span></span>
>

## <a name="customize-metrics-charts"></a><span data-ttu-id="51591-138">Customize metrics charts</span><span class="sxs-lookup"><span data-stu-id="51591-138">Customize metrics charts</span></span>

<span data-ttu-id="51591-139">Use the following procedure to choose which storage metrics to view in a metrics chart.</span><span class="sxs-lookup"><span data-stu-id="51591-139">Use the following procedure to choose which storage metrics to view in a metrics chart.</span></span> 

1. <span data-ttu-id="51591-140">Start by displaying a storage metric chart in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="51591-140">Start by displaying a storage metric chart in the Azure portal.</span></span> <span data-ttu-id="51591-141">You can find charts on the **storage account blade** and in the **Metrics** blade for an individual service (blob, queue, table, file).</span><span class="sxs-lookup"><span data-stu-id="51591-141">You can find charts on the **storage account blade** and in the **Metrics** blade for an individual service (blob, queue, table, file).</span></span>

   <span data-ttu-id="51591-142">In this example, we work with the following chart that appears on the **storage account blade**:</span><span class="sxs-lookup"><span data-stu-id="51591-142">In this example, we work with the following chart that appears on the **storage account blade**:</span></span>

   ![Chart selection in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. <span data-ttu-id="51591-144">Next, click anywhere within the chart to open the **Metric** blade.</span><span class="sxs-lookup"><span data-stu-id="51591-144">Next, click anywhere within the chart to open the **Metric** blade.</span></span> <span data-ttu-id="51591-145">Select **Edit chart** to open the **Edit Chart** blade.</span><span class="sxs-lookup"><span data-stu-id="51591-145">Select **Edit chart** to open the **Edit Chart** blade.</span></span>

   ![Edit chart button on chart blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. <span data-ttu-id="51591-147">On the **Edit Chart** blade, select the **Time Range** of the metrics to display in the chart, and the **service** (blob, queue, table, file) whose metrics you wish to display.</span><span class="sxs-lookup"><span data-stu-id="51591-147">On the **Edit Chart** blade, select the **Time Range** of the metrics to display in the chart, and the **service** (blob, queue, table, file) whose metrics you wish to display.</span></span> <span data-ttu-id="51591-148">Here we've selected to display the past week's metrics for the blob service:</span><span class="sxs-lookup"><span data-stu-id="51591-148">Here we've selected to display the past week's metrics for the blob service:</span></span>

   ![Time range and service selection in the Edit Chart blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. <span data-ttu-id="51591-150">Select the individual **metrics** you'd like displayed in the chart, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="51591-150">Select the individual **metrics** you'd like displayed in the chart, then click **OK**.</span></span> <span data-ttu-id="51591-151">For example, here we've chosen to display the *ContainerCount* and *ObjectCount* metrics:</span><span class="sxs-lookup"><span data-stu-id="51591-151">For example, here we've chosen to display the *ContainerCount* and *ObjectCount* metrics:</span></span>

   ![Individual metric selection in Edit Chart blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-customize-chart-03.png)

<span data-ttu-id="51591-153">Your chart settings do not affect the collection, aggregation, or storage of monitoring data in the storage account, only the viewing of metrics data.</span><span class="sxs-lookup"><span data-stu-id="51591-153">Your chart settings do not affect the collection, aggregation, or storage of monitoring data in the storage account, only the viewing of metrics data.</span></span>

### <a name="metrics-availability-in-charts"></a><span data-ttu-id="51591-154">Metrics availability in charts</span><span class="sxs-lookup"><span data-stu-id="51591-154">Metrics availability in charts</span></span>

<span data-ttu-id="51591-155">The list of available metrics changes based on which service you've chosen in the drop-down, and the unit type of the chart you're editing.</span><span class="sxs-lookup"><span data-stu-id="51591-155">The list of available metrics changes based on which service you've chosen in the drop-down, and the unit type of the chart you're editing.</span></span> <span data-ttu-id="51591-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span><span class="sxs-lookup"><span data-stu-id="51591-156">For example, you can select percentage metrics like *PercentNetworkError* and *PercentThrottlingError* only if you're editing a chart that displays units in percentage:</span></span>

![Request error percentage chart in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a><span data-ttu-id="51591-158">Metrics resolution</span><span class="sxs-lookup"><span data-stu-id="51591-158">Metrics resolution</span></span>

<span data-ttu-id="51591-159">The metrics you selected in Diagnostics determines the resolution of the metrics that are available for your account:</span><span class="sxs-lookup"><span data-stu-id="51591-159">The metrics you selected in Diagnostics determines the resolution of the metrics that are available for your account:</span></span>

* <span data-ttu-id="51591-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span><span class="sxs-lookup"><span data-stu-id="51591-160">**Aggregate** monitoring provides metrics such as ingress/egress, availability, latency, and success percentages.</span></span> <span data-ttu-id="51591-161">These metrics are aggregated from the blob, table, file, and queue services.</span><span class="sxs-lookup"><span data-stu-id="51591-161">These metrics are aggregated from the blob, table, file, and queue services.</span></span>
* <span data-ttu-id="51591-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition to the service-level aggregates.</span><span class="sxs-lookup"><span data-stu-id="51591-162">**Per API** provides finer resolution, with metrics available for individual storage operations, in addition to the service-level aggregates.</span></span>

## <a name="configure-metrics-alerts"></a><span data-ttu-id="51591-163">Configure metrics alerts</span><span class="sxs-lookup"><span data-stu-id="51591-163">Configure metrics alerts</span></span>

<span data-ttu-id="51591-164">You can create alerts to notify you when thresholds have been reached for storage resource metrics.</span><span class="sxs-lookup"><span data-stu-id="51591-164">You can create alerts to notify you when thresholds have been reached for storage resource metrics.</span></span>

1. <span data-ttu-id="51591-165">To open the **Alert rules blade**, scroll down to the **MONITORING** section of the **Menu blade** and select **Alert rules**.</span><span class="sxs-lookup"><span data-stu-id="51591-165">To open the **Alert rules blade**, scroll down to the **MONITORING** section of the **Menu blade** and select **Alert rules**.</span></span>
1. <span data-ttu-id="51591-166">Select **Add alert** to open the **Add an alert rule** blade</span><span class="sxs-lookup"><span data-stu-id="51591-166">Select **Add alert** to open the **Add an alert rule** blade</span></span>
1. <span data-ttu-id="51591-167">Select a **Resource** (blob, file, queue, table) from the drop-down, and enter a **Name** and **Description** for your new alert rule.</span><span class="sxs-lookup"><span data-stu-id="51591-167">Select a **Resource** (blob, file, queue, table) from the drop-down, and enter a **Name** and **Description** for your new alert rule.</span></span>
1. <span data-ttu-id="51591-168">Select the **Metric** for which you'd like to add an alert, an alert **Condition**, and a **Threshold**.</span><span class="sxs-lookup"><span data-stu-id="51591-168">Select the **Metric** for which you'd like to add an alert, an alert **Condition**, and a **Threshold**.</span></span> <span data-ttu-id="51591-169">The threshold unit type changes depending on the metric you've chosen.</span><span class="sxs-lookup"><span data-stu-id="51591-169">The threshold unit type changes depending on the metric you've chosen.</span></span> <span data-ttu-id="51591-170">For example, "count" is the unit type for *ContainerCount*, while the unit for the *PercentNetworkError* metric is a percentage.</span><span class="sxs-lookup"><span data-stu-id="51591-170">For example, "count" is the unit type for *ContainerCount*, while the unit for the *PercentNetworkError* metric is a percentage.</span></span>
1. <span data-ttu-id="51591-171">Select the **Period**.</span><span class="sxs-lookup"><span data-stu-id="51591-171">Select the **Period**.</span></span> <span data-ttu-id="51591-172">Metrics that reach or exceed the Threshold within the period trigger an alert.</span><span class="sxs-lookup"><span data-stu-id="51591-172">Metrics that reach or exceed the Threshold within the period trigger an alert.</span></span>
1. <span data-ttu-id="51591-173">(Optional) Configure **Email** and **Webhook** notifications.</span><span class="sxs-lookup"><span data-stu-id="51591-173">(Optional) Configure **Email** and **Webhook** notifications.</span></span> <span data-ttu-id="51591-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="51591-174">For more information on webhooks, see [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="51591-175">If you do not configure email or webhook notifications, alerts will appear only in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="51591-175">If you do not configure email or webhook notifications, alerts will appear only in the Azure portal.</span></span>

!['Add an alert rule' blade in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-to-the-portal-dashboard"></a><span data-ttu-id="51591-177">Add metrics charts to the portal dashboard</span><span class="sxs-lookup"><span data-stu-id="51591-177">Add metrics charts to the portal dashboard</span></span>

<span data-ttu-id="51591-178">You can add Azure Storage metrics charts for any of your storage accounts to your portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="51591-178">You can add Azure Storage metrics charts for any of your storage accounts to your portal dashboard.</span></span>

1. <span data-ttu-id="51591-179">Select click **Edit dashboard** while viewing your dashboard in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51591-179">Select click **Edit dashboard** while viewing your dashboard in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="51591-180">In the **Tile Gallery**, select **Find tiles by** > **Type**.</span><span class="sxs-lookup"><span data-stu-id="51591-180">In the **Tile Gallery**, select **Find tiles by** > **Type**.</span></span>
1. <span data-ttu-id="51591-181">Select **Type** > **Storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="51591-181">Select **Type** > **Storage accounts**.</span></span>
1. <span data-ttu-id="51591-182">In **Resources**, select the storage account whose metrics you wish to add to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="51591-182">In **Resources**, select the storage account whose metrics you wish to add to the dashboard.</span></span>
1. <span data-ttu-id="51591-183">Select **Categories** > **Monitoring**.</span><span class="sxs-lookup"><span data-stu-id="51591-183">Select **Categories** > **Monitoring**.</span></span>
1. <span data-ttu-id="51591-184">Drag-and-drop the chart tile onto your dashboard for the metric you'd like displayed.</span><span class="sxs-lookup"><span data-stu-id="51591-184">Drag-and-drop the chart tile onto your dashboard for the metric you'd like displayed.</span></span> <span data-ttu-id="51591-185">Repeat for all metrics you'd like displayed on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="51591-185">Repeat for all metrics you'd like displayed on the dashboard.</span></span> <span data-ttu-id="51591-186">In the following image, the "Blobs - Total requests" chart is highlighted as an example, but all the charts are available for placement on your dashboard.</span><span class="sxs-lookup"><span data-stu-id="51591-186">In the following image, the "Blobs - Total requests" chart is highlighted as an example, but all the charts are available for placement on your dashboard.</span></span>

   ![Tile gallery in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. <span data-ttu-id="51591-188">Select **Done customizing** near the top of the dashboard when you're done adding charts.</span><span class="sxs-lookup"><span data-stu-id="51591-188">Select **Done customizing** near the top of the dashboard when you're done adding charts.</span></span>

<span data-ttu-id="51591-189">Once you've added charts to your dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span><span class="sxs-lookup"><span data-stu-id="51591-189">Once you've added charts to your dashboard, you can further customize them as described in [Customize metrics charts](#how-to-customize-metrics-charts).</span></span>

## <a name="configure-logging"></a><span data-ttu-id="51591-190">Configure logging</span><span class="sxs-lookup"><span data-stu-id="51591-190">Configure logging</span></span>

<span data-ttu-id="51591-191">You can instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services.</span><span class="sxs-lookup"><span data-stu-id="51591-191">You can instruct Azure Storage to save diagnostics logs for read, write, and delete requests for the blob, table, and queue services.</span></span> <span data-ttu-id="51591-192">The data retention policy you set also applies to these logs.</span><span class="sxs-lookup"><span data-stu-id="51591-192">The data retention policy you set also applies to these logs.</span></span>

> [!NOTE]
> <span data-ttu-id="51591-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span><span class="sxs-lookup"><span data-stu-id="51591-193">Azure File storage currently supports Storage Analytics metrics, but does not yet support logging.</span></span>
>

1. <span data-ttu-id="51591-194">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the name of the storage account to open the storage account blade.</span><span class="sxs-lookup"><span data-stu-id="51591-194">In the [Azure portal](https://portal.azure.com), select **Storage accounts**, then the name of the storage account to open the storage account blade.</span></span>
1. <span data-ttu-id="51591-195">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span><span class="sxs-lookup"><span data-stu-id="51591-195">Select **Diagnostics** in the **MONITORING** section of the menu blade.</span></span>

    ![Diagnostics menu item under MONITORING in the Azure portal.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. <span data-ttu-id="51591-197">Ensure **Status** is set to **On**, and select the **services** for which you'd like to enable logging.</span><span class="sxs-lookup"><span data-stu-id="51591-197">Ensure **Status** is set to **On**, and select the **services** for which you'd like to enable logging.</span></span>

    ![Configure logging in the Azure portal.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. <span data-ttu-id="51591-199">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="51591-199">Click **Save**.</span></span>

<span data-ttu-id="51591-200">The diagnostics logs are saved in a blob container named $logs in your storage account.</span><span class="sxs-lookup"><span data-stu-id="51591-200">The diagnostics logs are saved in a blob container named $logs in your storage account.</span></span> <span data-ttu-id="51591-201">You can view the log data using a storage explorer like the [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using the storage client library or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51591-201">You can view the log data using a storage explorer like the [Microsoft Storage Explorer](http://storageexplorer.com), or programmatically using the storage client library or PowerShell.</span></span>

<span data-ttu-id="51591-202">For information about accessing the $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/fileservices/enabling-storage-logging-and-accessing-log-data).</span><span class="sxs-lookup"><span data-stu-id="51591-202">For information about accessing the $logs container, see [Enabling Storage Logging and Accessing Log Data](/rest/api/storageservices/fileservices/enabling-storage-logging-and-accessing-log-data).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51591-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="51591-203">Next steps</span></span>

* <span data-ttu-id="51591-204">Find more details about [metrics, logging, and billing](storage-analytics.md) for Storage Analytics.</span><span class="sxs-lookup"><span data-stu-id="51591-204">Find more details about [metrics, logging, and billing](storage-analytics.md) for Storage Analytics.</span></span>
* <span data-ttu-id="51591-205">[Enable Azure Storage metrics and view metrics data](storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span><span class="sxs-lookup"><span data-stu-id="51591-205">[Enable Azure Storage metrics and view metrics data](storage-enable-and-view-metrics.md) by using PowerShell and programmatically with C#.</span></span>











