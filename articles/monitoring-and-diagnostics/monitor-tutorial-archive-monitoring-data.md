---
title: Archive Azure metric and log data using Azure Storage
description: Archive log and metric data produced within Azure to a storage account.
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: tutorial
ms.date: 09/25/2017
ms.author: johnkem
ms.custom: mvc
ms.component: metrics
ms.openlocfilehash: f6b7b9fe73f5e815e08bbf4f6493ee181a0c692b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856243"
---
# <a name="archive-azure-monitoring-data"></a><span data-ttu-id="21e26-103">Archive Azure monitoring data</span><span class="sxs-lookup"><span data-stu-id="21e26-103">Archive Azure monitoring data</span></span>

<span data-ttu-id="21e26-104">Several layers of your Azure environment produce log and metric data that can be archived to an Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="21e26-104">Several layers of your Azure environment produce log and metric data that can be archived to an Azure Storage Account.</span></span> <span data-ttu-id="21e26-105">You may want to do this to preserve a history of monitoring data over time in an inexpensive, non-searchable store after that data has passed its retention period in Log Analytics or Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="21e26-105">You may want to do this to preserve a history of monitoring data over time in an inexpensive, non-searchable store after that data has passed its retention period in Log Analytics or Azure Monitor.</span></span> <span data-ttu-id="21e26-106">This tutorial steps through the process of configuring your Azure environment to archive data to a storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-106">This tutorial steps through the process of configuring your Azure environment to archive data to a storage account.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="21e26-107">Create a storage account to hold monitoring data</span><span class="sxs-lookup"><span data-stu-id="21e26-107">Create a storage account to hold monitoring data</span></span>
> * <span data-ttu-id="21e26-108">Route subscription logs to it</span><span class="sxs-lookup"><span data-stu-id="21e26-108">Route subscription logs to it</span></span>
> * <span data-ttu-id="21e26-109">Route resource data to it</span><span class="sxs-lookup"><span data-stu-id="21e26-109">Route resource data to it</span></span>
> * <span data-ttu-id="21e26-110">Route virtual machine (guest OS) data to it</span><span class="sxs-lookup"><span data-stu-id="21e26-110">Route virtual machine (guest OS) data to it</span></span>
> * <span data-ttu-id="21e26-111">View the monitoring data in it</span><span class="sxs-lookup"><span data-stu-id="21e26-111">View the monitoring data in it</span></span>
> * <span data-ttu-id="21e26-112">Clean up your resources</span><span class="sxs-lookup"><span data-stu-id="21e26-112">Clean up your resources</span></span>

<span data-ttu-id="21e26-113">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="21e26-113">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="21e26-114">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="21e26-114">Sign in to the Azure portal</span></span>

<span data-ttu-id="21e26-115">Sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="21e26-115">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-storage-account"></a><span data-ttu-id="21e26-116">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="21e26-116">Create a storage account</span></span>

<span data-ttu-id="21e26-117">First you need to set up a storage account to which the monitoring data will be archived.</span><span class="sxs-lookup"><span data-stu-id="21e26-117">First you need to set up a storage account to which the monitoring data will be archived.</span></span> <span data-ttu-id="21e26-118">To do this, [follow the steps here](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="21e26-118">To do this, [follow the steps here](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="route-subscription-logs-to-the-storage-account"></a><span data-ttu-id="21e26-119">Route subscription logs to the storage account</span><span class="sxs-lookup"><span data-stu-id="21e26-119">Route subscription logs to the storage account</span></span>

<span data-ttu-id="21e26-120">You are now ready to begin to set up your Azure environment to route monitoring data to a storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-120">You are now ready to begin to set up your Azure environment to route monitoring data to a storage account.</span></span> <span data-ttu-id="21e26-121">First we configure subscription-level data (contained in the Azure Activity Log) to be routed to the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-121">First we configure subscription-level data (contained in the Azure Activity Log) to be routed to the storage account.</span></span> <span data-ttu-id="21e26-122">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) provides a history of subscription-level events in Azure.</span><span class="sxs-lookup"><span data-stu-id="21e26-122">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) provides a history of subscription-level events in Azure.</span></span> <span data-ttu-id="21e26-123">You can browse it in the Azure portal to determine *who* created, updated, or deleted *what* resources and *when* they did it.</span><span class="sxs-lookup"><span data-stu-id="21e26-123">You can browse it in the Azure portal to determine *who* created, updated, or deleted *what* resources and *when* they did it.</span></span>

1. <span data-ttu-id="21e26-124">Click the **Monitor** button found on the left-hand navigation list, then on **Activity Log**.</span><span class="sxs-lookup"><span data-stu-id="21e26-124">Click the **Monitor** button found on the left-hand navigation list, then on **Activity Log**.</span></span>

   ![Activity Log section](media/monitor-tutorial-archive-monitoring-data/activity-log-home.png)

2. <span data-ttu-id="21e26-126">In the Activity Log section that is displayed, click on the **Export** button.</span><span class="sxs-lookup"><span data-stu-id="21e26-126">In the Activity Log section that is displayed, click on the **Export** button.</span></span>

3. <span data-ttu-id="21e26-127">In the **Export activity log** section that appears, check the box for **Export to a storage account** and click **Select a storage account.**</span><span class="sxs-lookup"><span data-stu-id="21e26-127">In the **Export activity log** section that appears, check the box for **Export to a storage account** and click **Select a storage account.**</span></span>

   ![Activity Log export](media/monitor-tutorial-archive-monitoring-data/activity-log-export.png)

4. <span data-ttu-id="21e26-129">In the section that appears, use the **Storage account** dropdown to select the name of the storage account you created in the preceding **Create a storage account** step, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="21e26-129">In the section that appears, use the **Storage account** dropdown to select the name of the storage account you created in the preceding **Create a storage account** step, then click **OK**.</span></span>

   ![Pick a storage account](media/monitor-tutorial-archive-monitoring-data/activity-log-storage.png)

5. <span data-ttu-id="21e26-131">Set the **Retention (days)** slider to 30.</span><span class="sxs-lookup"><span data-stu-id="21e26-131">Set the **Retention (days)** slider to 30.</span></span> <span data-ttu-id="21e26-132">This slider sets a number of days to retain the monitoring data in the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-132">This slider sets a number of days to retain the monitoring data in the storage account.</span></span> <span data-ttu-id="21e26-133">Azure Monitor automatically deletes data older than the number of days specified.</span><span class="sxs-lookup"><span data-stu-id="21e26-133">Azure Monitor automatically deletes data older than the number of days specified.</span></span> <span data-ttu-id="21e26-134">A retention of zero days stores the data indefinitely.</span><span class="sxs-lookup"><span data-stu-id="21e26-134">A retention of zero days stores the data indefinitely.</span></span>

6. <span data-ttu-id="21e26-135">Click **Save** and close this section.</span><span class="sxs-lookup"><span data-stu-id="21e26-135">Click **Save** and close this section.</span></span>

<span data-ttu-id="21e26-136">Monitoring data from your subscription is now flowing into the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-136">Monitoring data from your subscription is now flowing into the storage account.</span></span>

## <a name="route-resource-data-to-the-storage-account"></a><span data-ttu-id="21e26-137">Route resource data to the storage account</span><span class="sxs-lookup"><span data-stu-id="21e26-137">Route resource data to the storage account</span></span>

<span data-ttu-id="21e26-138">Now we configure resource-level data (resource metrics and diagnostic logs) to be routed to the storage account by setting up **resource diagnostic settings**.</span><span class="sxs-lookup"><span data-stu-id="21e26-138">Now we configure resource-level data (resource metrics and diagnostic logs) to be routed to the storage account by setting up **resource diagnostic settings**.</span></span>

1. <span data-ttu-id="21e26-139">Click the **Monitor** button found on the left-hand navigation list, then on **Diagnostic Settings**.</span><span class="sxs-lookup"><span data-stu-id="21e26-139">Click the **Monitor** button found on the left-hand navigation list, then on **Diagnostic Settings**.</span></span> <span data-ttu-id="21e26-140">Here you see a list of all resources in your subscription that produce monitoring data through Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="21e26-140">Here you see a list of all resources in your subscription that produce monitoring data through Azure Monitor.</span></span> <span data-ttu-id="21e26-141">If you do not have any resources in this list, you can [create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) before proceeding so that you have a resource that you can configure a diagnostic setting on.</span><span class="sxs-lookup"><span data-stu-id="21e26-141">If you do not have any resources in this list, you can [create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md) before proceeding so that you have a resource that you can configure a diagnostic setting on.</span></span>

2. <span data-ttu-id="21e26-142">Click on a resource in the list, and then click **Turn on diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="21e26-142">Click on a resource in the list, and then click **Turn on diagnostics**.</span></span>

   ![Turn on diagnostics](media/monitor-tutorial-archive-monitoring-data/diagnostic-settings-turn-on.png)

   <span data-ttu-id="21e26-144">If there is already a setting configured, you instead see the existing settings, and a button to **Add diagnostic setting**.</span><span class="sxs-lookup"><span data-stu-id="21e26-144">If there is already a setting configured, you instead see the existing settings, and a button to **Add diagnostic setting**.</span></span> <span data-ttu-id="21e26-145">Click this button.</span><span class="sxs-lookup"><span data-stu-id="21e26-145">Click this button.</span></span>

   <span data-ttu-id="21e26-146">A resource diagnostic setting is a definition of *what* monitoring data should be routed from a particular resource and *where* that monitoring data should go.</span><span class="sxs-lookup"><span data-stu-id="21e26-146">A resource diagnostic setting is a definition of *what* monitoring data should be routed from a particular resource and *where* that monitoring data should go.</span></span>

3. <span data-ttu-id="21e26-147">In the section that appears, give your setting a **name** and check the box for **Archive to a storage account**.</span><span class="sxs-lookup"><span data-stu-id="21e26-147">In the section that appears, give your setting a **name** and check the box for **Archive to a storage account**.</span></span>

   ![Diagnostic settings section](media/monitor-tutorial-archive-monitoring-data/diagnostic-settings-home.png)

4. <span data-ttu-id="21e26-149">Click on the **Configure** button under **Archive to a storage account** and select the storage account you created in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="21e26-149">Click on the **Configure** button under **Archive to a storage account** and select the storage account you created in the preceding section.</span></span> <span data-ttu-id="21e26-150">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="21e26-150">Click **OK**.</span></span>

   ![Diagnostic settings storage account](media/monitor-tutorial-archive-monitoring-data/diagnostic-settings-storage.png)

5. <span data-ttu-id="21e26-152">Check all the boxes under **Log** and **Metric**.</span><span class="sxs-lookup"><span data-stu-id="21e26-152">Check all the boxes under **Log** and **Metric**.</span></span> <span data-ttu-id="21e26-153">Depending on the resource type, you may only have one of these options.</span><span class="sxs-lookup"><span data-stu-id="21e26-153">Depending on the resource type, you may only have one of these options.</span></span> <span data-ttu-id="21e26-154">These checkboxes control what categories of log and metric data available for that resource type are sent to the destination you've selected, in this case, a storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-154">These checkboxes control what categories of log and metric data available for that resource type are sent to the destination you've selected, in this case, a storage account.</span></span>

   ![Diagnostic settings categories](media/monitor-tutorial-archive-monitoring-data/diagnostic-settings-categories.png)

6. <span data-ttu-id="21e26-156">Set the **Retention (days)** slider to 30.</span><span class="sxs-lookup"><span data-stu-id="21e26-156">Set the **Retention (days)** slider to 30.</span></span> <span data-ttu-id="21e26-157">This slider sets a number of days to retain the monitoring data in the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-157">This slider sets a number of days to retain the monitoring data in the storage account.</span></span> <span data-ttu-id="21e26-158">Azure Monitor automatically deletes data older than the number of days specified.</span><span class="sxs-lookup"><span data-stu-id="21e26-158">Azure Monitor automatically deletes data older than the number of days specified.</span></span> <span data-ttu-id="21e26-159">A retention of zero days stores the data indefinitely.</span><span class="sxs-lookup"><span data-stu-id="21e26-159">A retention of zero days stores the data indefinitely.</span></span>

7. <span data-ttu-id="21e26-160">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="21e26-160">Click **Save**.</span></span>

<span data-ttu-id="21e26-161">Monitoring data from your resource is now flowing into the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-161">Monitoring data from your resource is now flowing into the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="21e26-162">Sending multi-dimensional metrics via diagnostic settings is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="21e26-162">Sending multi-dimensional metrics via diagnostic settings is not currently supported.</span></span> <span data-ttu-id="21e26-163">Metrics with dimensions are exported as flattened single dimensional metrics, aggregated across dimension values.</span><span class="sxs-lookup"><span data-stu-id="21e26-163">Metrics with dimensions are exported as flattened single dimensional metrics, aggregated across dimension values.</span></span>
>
> <span data-ttu-id="21e26-164">*For example*: The 'Incoming Messages' metric on an Event Hub can be explored and charted on a per queue level.</span><span class="sxs-lookup"><span data-stu-id="21e26-164">*For example*: The 'Incoming Messages' metric on an Event Hub can be explored and charted on a per queue level.</span></span> <span data-ttu-id="21e26-165">However, when exported via diagnostic settings the metric will be represented as all incoming messages across all queues in the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="21e26-165">However, when exported via diagnostic settings the metric will be represented as all incoming messages across all queues in the Event Hub.</span></span>
>
>

## <a name="route-virtual-machine-guest-os-data-to-the-storage-account"></a><span data-ttu-id="21e26-166">Route virtual machine (guest OS) data to the storage account</span><span class="sxs-lookup"><span data-stu-id="21e26-166">Route virtual machine (guest OS) data to the storage account</span></span>

1. <span data-ttu-id="21e26-167">If you do not already have a virtual machine in your subscription, [create a virtual machine](../virtual-machines/windows/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="21e26-167">If you do not already have a virtual machine in your subscription, [create a virtual machine](../virtual-machines/windows/quick-create-portal.md).</span></span>

2. <span data-ttu-id="21e26-168">In the left-hand navigation list in the portal, click on **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="21e26-168">In the left-hand navigation list in the portal, click on **Virtual Machines**.</span></span>

3. <span data-ttu-id="21e26-169">In the list of virtual machines that is displayed, click on the virtual machine you created.</span><span class="sxs-lookup"><span data-stu-id="21e26-169">In the list of virtual machines that is displayed, click on the virtual machine you created.</span></span>

4. <span data-ttu-id="21e26-170">In the section that appears, click on **Diagnostic Settings** on the left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="21e26-170">In the section that appears, click on **Diagnostic Settings** on the left-hand navigation.</span></span> <span data-ttu-id="21e26-171">This section enables you to set up the out-of-box monitoring extension from Azure Monitor on your virtual machine and route data being produced by Windows or Linux to a storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-171">This section enables you to set up the out-of-box monitoring extension from Azure Monitor on your virtual machine and route data being produced by Windows or Linux to a storage account.</span></span>

   ![Navigate to diagnostic settings](media/monitor-tutorial-archive-monitoring-data/guest-navigation.png)

5. <span data-ttu-id="21e26-173">Click **Enable guest-level monitoring** in the section that appears.</span><span class="sxs-lookup"><span data-stu-id="21e26-173">Click **Enable guest-level monitoring** in the section that appears.</span></span>

   ![Enable diagnostic settings](media/monitor-tutorial-archive-monitoring-data/guest-enable.png)

6. <span data-ttu-id="21e26-175">Once the diagnostic setting has correctly saved, the **Overview** tab shows a list of the data being collected and where it is being stored.</span><span class="sxs-lookup"><span data-stu-id="21e26-175">Once the diagnostic setting has correctly saved, the **Overview** tab shows a list of the data being collected and where it is being stored.</span></span> <span data-ttu-id="21e26-176">Click on the **Performance counters** section to review the set of Windows performance counters being collected.</span><span class="sxs-lookup"><span data-stu-id="21e26-176">Click on the **Performance counters** section to review the set of Windows performance counters being collected.</span></span>

   ![Performance counters settings](media/monitor-tutorial-archive-monitoring-data/guest-perf-counters.png)

7. <span data-ttu-id="21e26-178">Click on the **Logs** tab and check the checkboxes for **Information** level logs on Application and System logs.</span><span class="sxs-lookup"><span data-stu-id="21e26-178">Click on the **Logs** tab and check the checkboxes for **Information** level logs on Application and System logs.</span></span>

   ![Logs settings](media/monitor-tutorial-archive-monitoring-data/guest-logs.png)

8. <span data-ttu-id="21e26-180">Click on the **Agent** tab and under **Storage account** click on the name of the storage account shown.</span><span class="sxs-lookup"><span data-stu-id="21e26-180">Click on the **Agent** tab and under **Storage account** click on the name of the storage account shown.</span></span>

   ![Update storage account](media/monitor-tutorial-archive-monitoring-data/guest-storage-home.png)

9. <span data-ttu-id="21e26-182">In the section that appears, pick the storage account you created in the preceding **Create a storage account** step.</span><span class="sxs-lookup"><span data-stu-id="21e26-182">In the section that appears, pick the storage account you created in the preceding **Create a storage account** step.</span></span>

10. <span data-ttu-id="21e26-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="21e26-183">Click **Save**.</span></span>

<span data-ttu-id="21e26-184">Monitoring data from your virtual machines is now flowing into the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-184">Monitoring data from your virtual machines is now flowing into the storage account.</span></span>

## <a name="view-the-monitoring-data-in-the-storage-account"></a><span data-ttu-id="21e26-185">View the monitoring data in the storage account</span><span class="sxs-lookup"><span data-stu-id="21e26-185">View the monitoring data in the storage account</span></span>

> [!WARNING]
> <span data-ttu-id="21e26-186">The format of the log data in the storage account will change to JSON Lines on Nov. 1st, 2018.</span><span class="sxs-lookup"><span data-stu-id="21e26-186">The format of the log data in the storage account will change to JSON Lines on Nov. 1st, 2018.</span></span> [<span data-ttu-id="21e26-187">See this article for a description of the impact and how to update your tooling to handle the new format.</span><span class="sxs-lookup"><span data-stu-id="21e26-187">See this article for a description of the impact and how to update your tooling to handle the new format.</span></span>](./monitor-diagnostic-logs-append-blobs.md) 
>
> 

<span data-ttu-id="21e26-188">If you have followed the preceding steps, data has begun flowing to your storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-188">If you have followed the preceding steps, data has begun flowing to your storage account.</span></span>

1. <span data-ttu-id="21e26-189">For some data types, for example, the Activity Log, there needs to be some activity that generates an event in the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-189">For some data types, for example, the Activity Log, there needs to be some activity that generates an event in the storage account.</span></span> <span data-ttu-id="21e26-190">To generate activity in the Activity Log, follow [these instructions](./monitor-quick-audit-notify-action-in-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="21e26-190">To generate activity in the Activity Log, follow [these instructions](./monitor-quick-audit-notify-action-in-subscription.md).</span></span> <span data-ttu-id="21e26-191">You may need to wait up to five minutes before the event appears in the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-191">You may need to wait up to five minutes before the event appears in the storage account.</span></span>

2. <span data-ttu-id="21e26-192">In the portal, navigate to the **Storage Accounts** section by finding it on the left-hand navigation bar.</span><span class="sxs-lookup"><span data-stu-id="21e26-192">In the portal, navigate to the **Storage Accounts** section by finding it on the left-hand navigation bar.</span></span>

3. <span data-ttu-id="21e26-193">Identify the storage account you created in the preceding section and click on it.</span><span class="sxs-lookup"><span data-stu-id="21e26-193">Identify the storage account you created in the preceding section and click on it.</span></span>

4. <span data-ttu-id="21e26-194">Click on **Blobs**, then on the container labeled **insights-operational-logs** and finally on the container labeled **name=default**.</span><span class="sxs-lookup"><span data-stu-id="21e26-194">Click on **Blobs**, then on the container labeled **insights-operational-logs** and finally on the container labeled **name=default**.</span></span> <span data-ttu-id="21e26-195">This is the container that has your Activity Log in it.</span><span class="sxs-lookup"><span data-stu-id="21e26-195">This is the container that has your Activity Log in it.</span></span> <span data-ttu-id="21e26-196">Monitoring data is broken out into containers by resource ID (just the subscription ID for the Activity Log), then by date and time.</span><span class="sxs-lookup"><span data-stu-id="21e26-196">Monitoring data is broken out into containers by resource ID (just the subscription ID for the Activity Log), then by date and time.</span></span> <span data-ttu-id="21e26-197">The full format for these blobs is:</span><span class="sxs-lookup"><span data-stu-id="21e26-197">The full format for these blobs is:</span></span>

   <span data-ttu-id="21e26-198">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="21e26-198">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>

5. <span data-ttu-id="21e26-199">Navigate to the PT1H.json file by clicking into the containers for resource ID, date, and time.</span><span class="sxs-lookup"><span data-stu-id="21e26-199">Navigate to the PT1H.json file by clicking into the containers for resource ID, date, and time.</span></span> <span data-ttu-id="21e26-200">Click on the PT1H.json file and click **Download**.</span><span class="sxs-lookup"><span data-stu-id="21e26-200">Click on the PT1H.json file and click **Download**.</span></span> <span data-ttu-id="21e26-201">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (for example, h=12).</span><span class="sxs-lookup"><span data-stu-id="21e26-201">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (for example, h=12).</span></span> <span data-ttu-id="21e26-202">During the present hour, events are appended to the PT1H.json file as they occur.</span><span class="sxs-lookup"><span data-stu-id="21e26-202">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="21e26-203">The minute value (m=00) is always 00, since log events are broken into individual blobs per hour.</span><span class="sxs-lookup"><span data-stu-id="21e26-203">The minute value (m=00) is always 00, since log events are broken into individual blobs per hour.</span></span>

   <span data-ttu-id="21e26-204">You can now view the JSON event that was stored in the storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-204">You can now view the JSON event that was stored in the storage account.</span></span> <span data-ttu-id="21e26-205">For resource diagnostic logs, the format for the blobs is:</span><span class="sxs-lookup"><span data-stu-id="21e26-205">For resource diagnostic logs, the format for the blobs is:</span></span>

   <span data-ttu-id="21e26-206">insights-logs-{log category name}/resourceId=/{resource ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="21e26-206">insights-logs-{log category name}/resourceId=/{resource ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>

6. <span data-ttu-id="21e26-207">Guest OS monitoring data is stored in tables.</span><span class="sxs-lookup"><span data-stu-id="21e26-207">Guest OS monitoring data is stored in tables.</span></span> <span data-ttu-id="21e26-208">navigate back to the storage account home, and click **Tables**.</span><span class="sxs-lookup"><span data-stu-id="21e26-208">navigate back to the storage account home, and click **Tables**.</span></span> <span data-ttu-id="21e26-209">There are tables for metrics, performance counters, and event logs.</span><span class="sxs-lookup"><span data-stu-id="21e26-209">There are tables for metrics, performance counters, and event logs.</span></span>

<span data-ttu-id="21e26-210">You have now successfully set up monitoring data to be archived to a storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-210">You have now successfully set up monitoring data to be archived to a storage account.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="21e26-211">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="21e26-211">Clean up resources</span></span>

1. <span data-ttu-id="21e26-212">Navigate back to the **Export Activity Log** section from the preceding **Route subscription logs to the storage account** step, and click **Reset**.</span><span class="sxs-lookup"><span data-stu-id="21e26-212">Navigate back to the **Export Activity Log** section from the preceding **Route subscription logs to the storage account** step, and click **Reset**.</span></span>

2. <span data-ttu-id="21e26-213">Navigate to the **Diagnostic Settings** section, click the resource on which you created a diagnostic setting in the preceding **Route resource data to the storage account** step, then find the setting you created, click the **Edit setting** button and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="21e26-213">Navigate to the **Diagnostic Settings** section, click the resource on which you created a diagnostic setting in the preceding **Route resource data to the storage account** step, then find the setting you created, click the **Edit setting** button and click **Delete**.</span></span>

3. <span data-ttu-id="21e26-214">Navigate to the **Diagnostic Settings** section on the virtual machine you configured in the preceding **Route virtual machine (guest OS) data to the storage account** step, and under the **Agent** tab click **Remove** (beneath the **Remove Azure Diagnostics agent** section).</span><span class="sxs-lookup"><span data-stu-id="21e26-214">Navigate to the **Diagnostic Settings** section on the virtual machine you configured in the preceding **Route virtual machine (guest OS) data to the storage account** step, and under the **Agent** tab click **Remove** (beneath the **Remove Azure Diagnostics agent** section).</span></span>

4. <span data-ttu-id="21e26-215">Navigate to the storage account you created in the preceding **Create a storage account** step and click **Delete storage account**.</span><span class="sxs-lookup"><span data-stu-id="21e26-215">Navigate to the storage account you created in the preceding **Create a storage account** step and click **Delete storage account**.</span></span> <span data-ttu-id="21e26-216">Type the name of the storage account, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="21e26-216">Type the name of the storage account, and then click **Delete**.</span></span>

5. <span data-ttu-id="21e26-217">If you created a virtual machine or Logic App for the preceding steps, delete those as well.</span><span class="sxs-lookup"><span data-stu-id="21e26-217">If you created a virtual machine or Logic App for the preceding steps, delete those as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e26-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="21e26-218">Next steps</span></span>

<span data-ttu-id="21e26-219">In this tutorial, you learned how to set up monitoring data from your Azure environment (subscription, resource, and guest OS) to be archived to a storage account.</span><span class="sxs-lookup"><span data-stu-id="21e26-219">In this tutorial, you learned how to set up monitoring data from your Azure environment (subscription, resource, and guest OS) to be archived to a storage account.</span></span>


> [!div class="checklist"]
> * <span data-ttu-id="21e26-220">Create a storage account to hold monitoring data</span><span class="sxs-lookup"><span data-stu-id="21e26-220">Create a storage account to hold monitoring data</span></span>
> * <span data-ttu-id="21e26-221">Route subscription logs to it</span><span class="sxs-lookup"><span data-stu-id="21e26-221">Route subscription logs to it</span></span>
> * <span data-ttu-id="21e26-222">Route resource data to it</span><span class="sxs-lookup"><span data-stu-id="21e26-222">Route resource data to it</span></span>
> * <span data-ttu-id="21e26-223">Route virtual machine (guest OS) data to it</span><span class="sxs-lookup"><span data-stu-id="21e26-223">Route virtual machine (guest OS) data to it</span></span>
> * <span data-ttu-id="21e26-224">View the monitoring data in it</span><span class="sxs-lookup"><span data-stu-id="21e26-224">View the monitoring data in it</span></span>
> * <span data-ttu-id="21e26-225">Clean up your resources</span><span class="sxs-lookup"><span data-stu-id="21e26-225">Clean up your resources</span></span>

<span data-ttu-id="21e26-226">To get more out of your data and derive additional insights, also  send your data into Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="21e26-226">To get more out of your data and derive additional insights, also  send your data into Log Analytics.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21e26-227">Get started with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="21e26-227">Get started with Log Analytics</span></span>](../log-analytics/log-analytics-get-started.md)
