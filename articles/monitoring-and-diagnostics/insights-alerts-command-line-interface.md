---
title: Use the cross-platform Azure CLI to create classic alerts for Azure services | Microsoft Docs
description: Trigger emails or notifications, or call websites URLs (webhooks) or automation when the conditions that you specify are met.
author: rboucher
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 10/24/2016
ms.author: robb
ms.component: alerts
ms.openlocfilehash: 8112b868bc8d2ca2a9478d38ee702d8b3350d48e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819889"
---
# <a name="use-the-cross-platform-azure-cli-to-create-classic-metric-alerts-in-azure-monitor-for-azure-services"></a><span data-ttu-id="1f893-103">Use the cross-platform Azure CLI to create classic metric alerts in Azure Monitor for Azure services</span><span class="sxs-lookup"><span data-stu-id="1f893-103">Use the cross-platform Azure CLI to create classic metric alerts in Azure Monitor for Azure services</span></span> 

> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>
> [!NOTE]
> This article describes how to create older classic metric alerts. Azure Monitor now supports [newer, better metric alerts](monitoring-near-real-time-metric-alerts.md). These alerts can monitor multiple metrics and allow for alerting on dimensional metrics. Azure CLI support for newer metric alerts is coming soon.
>
>

<span data-ttu-id="1f893-111">This article shows you how to set up Azure classic metric alerts by using the cross-platform command-line interface (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="1f893-111">This article shows you how to set up Azure classic metric alerts by using the cross-platform command-line interface (Azure CLI).</span></span>

> [!NOTE]
> Azure Monitor is the new name for what was called "Azure Insights" until September 25, 2016. However, the namespaces and thus the commands that are described here still contain the word "insights."

<span data-ttu-id="1f893-114">You can receive an alert based on metrics for your Azure services, or based on events that occur in Azure.</span><span class="sxs-lookup"><span data-stu-id="1f893-114">You can receive an alert based on metrics for your Azure services, or based on events that occur in Azure.</span></span>

* <span data-ttu-id="1f893-115">**Metric values**: The alert triggers when the value of a specified metric crosses a threshold that you assign in either direction.</span><span class="sxs-lookup"><span data-stu-id="1f893-115">**Metric values**: The alert triggers when the value of a specified metric crosses a threshold that you assign in either direction.</span></span> <span data-ttu-id="1f893-116">That is, it triggers both when the condition is first met and then when that condition is no longer being met.</span><span class="sxs-lookup"><span data-stu-id="1f893-116">That is, it triggers both when the condition is first met and then when that condition is no longer being met.</span></span>    

* <span data-ttu-id="1f893-117">**Activity log events**: An alert can trigger on *every* event or when certain events occur.</span><span class="sxs-lookup"><span data-stu-id="1f893-117">**Activity log events**: An alert can trigger on *every* event or when certain events occur.</span></span> <span data-ttu-id="1f893-118">To learn more about activity logs, see [Create activity log alerts (classic)](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1f893-118">To learn more about activity logs, see [Create activity log alerts (classic)](monitoring-activity-log-alerts.md).</span></span> 

<span data-ttu-id="1f893-119">You can configure a classic metric alert to do the following when it triggers:</span><span class="sxs-lookup"><span data-stu-id="1f893-119">You can configure a classic metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="1f893-120">Send email notifications to the service administrator and co-administrators.</span><span class="sxs-lookup"><span data-stu-id="1f893-120">Send email notifications to the service administrator and co-administrators.</span></span> 
* <span data-ttu-id="1f893-121">Send email to email addresses that you specify.</span><span class="sxs-lookup"><span data-stu-id="1f893-121">Send email to email addresses that you specify.</span></span>
* <span data-ttu-id="1f893-122">Call a webhook.</span><span class="sxs-lookup"><span data-stu-id="1f893-122">Call a webhook.</span></span>
* <span data-ttu-id="1f893-123">Start execution of an Azure runbook (only from the Azure portal at this time).</span><span class="sxs-lookup"><span data-stu-id="1f893-123">Start execution of an Azure runbook (only from the Azure portal at this time).</span></span>

<span data-ttu-id="1f893-124">You can configure and get information about classic metric alert rules by using the following:</span><span class="sxs-lookup"><span data-stu-id="1f893-124">You can configure and get information about classic metric alert rules by using the following:</span></span> 

* [<span data-ttu-id="1f893-125">The Azure portal</span><span class="sxs-lookup"><span data-stu-id="1f893-125">The Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="1f893-126">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f893-126">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="1f893-127">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1f893-127">Azure CLI</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="1f893-128">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="1f893-128">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="1f893-129">You can also get help for commands by typing a command with **-help** at the end.</span><span class="sxs-lookup"><span data-stu-id="1f893-129">You can also get help for commands by typing a command with **-help** at the end.</span></span> <span data-ttu-id="1f893-130">Following is an example:</span><span class="sxs-lookup"><span data-stu-id="1f893-130">Following is an example:</span></span> 

```console
 azure insights alerts -help
 azure insights alerts actions email create -help
 ```

## <a name="create-alert-rules-by-using-azure-cli"></a><span data-ttu-id="1f893-131">Create alert rules by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1f893-131">Create alert rules by using Azure CLI</span></span>
1. <span data-ttu-id="1f893-132">After you've installed the prerequisites, sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="1f893-132">After you've installed the prerequisites, sign in to Azure.</span></span> <span data-ttu-id="1f893-133">See [Azure Monitor CLI samples](insights-cli-samples.md) for the commands that you need to get started.</span><span class="sxs-lookup"><span data-stu-id="1f893-133">See [Azure Monitor CLI samples](insights-cli-samples.md) for the commands that you need to get started.</span></span> <span data-ttu-id="1f893-134">These commands help you get signed in, show you what subscription you're using, and prepare you to run Azure Monitor commands.</span><span class="sxs-lookup"><span data-stu-id="1f893-134">These commands help you get signed in, show you what subscription you're using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="1f893-135">To list existing rules on a resource group, use the following format:</span><span class="sxs-lookup"><span data-stu-id="1f893-135">To list existing rules on a resource group, use the following format:</span></span> 

   <span data-ttu-id="1f893-136">**azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="1f893-136">**azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="1f893-137">To create a rule, you need to have several important pieces of information first.</span><span class="sxs-lookup"><span data-stu-id="1f893-137">To create a rule, you need to have several important pieces of information first.</span></span>
    * <span data-ttu-id="1f893-138">The **resource ID** for the resource you want to set an alert for.</span><span class="sxs-lookup"><span data-stu-id="1f893-138">The **resource ID** for the resource you want to set an alert for.</span></span>
    * <span data-ttu-id="1f893-139">The **metric definitions** that are available for that resource.</span><span class="sxs-lookup"><span data-stu-id="1f893-139">The **metric definitions** that are available for that resource.</span></span>

     <span data-ttu-id="1f893-140">One way to get the resource ID is to use the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f893-140">One way to get the resource ID is to use the Azure portal.</span></span> <span data-ttu-id="1f893-141">Assuming that the resource is already created, select it in the portal.</span><span class="sxs-lookup"><span data-stu-id="1f893-141">Assuming that the resource is already created, select it in the portal.</span></span> <span data-ttu-id="1f893-142">Then, in the next blade, in the **Settings** section, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="1f893-142">Then, in the next blade, in the **Settings** section, select **Properties**.</span></span> <span data-ttu-id="1f893-143">**RESOURCE ID** is a field in the next blade.</span><span class="sxs-lookup"><span data-stu-id="1f893-143">**RESOURCE ID** is a field in the next blade.</span></span> 
     
     <span data-ttu-id="1f893-144">You can also get the resource ID by using  [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1f893-144">You can also get the resource ID by using  [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="1f893-145">Following is an example resource ID for a web app:</span><span class="sxs-lookup"><span data-stu-id="1f893-145">Following is an example resource ID for a web app:</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="1f893-146">To get a list of the available metrics and units for the metrics in the previous resource example, use the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="1f893-146">To get a list of the available metrics and units for the metrics in the previous resource example, use the following Azure CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="1f893-147">*PT1M* is the granularity of the available measurement (in 1-minute intervals).</span><span class="sxs-lookup"><span data-stu-id="1f893-147">*PT1M* is the granularity of the available measurement (in 1-minute intervals).</span></span> <span data-ttu-id="1f893-148">You have different metric options when you use different granularities.</span><span class="sxs-lookup"><span data-stu-id="1f893-148">You have different metric options when you use different granularities.</span></span>
     
4. <span data-ttu-id="1f893-149">To create a metric-based alert rule, use a command in the following format:</span><span class="sxs-lookup"><span data-stu-id="1f893-149">To create a metric-based alert rule, use a command in the following format:</span></span>

    <span data-ttu-id="1f893-150">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="1f893-150">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="1f893-151">The following example sets up an alert on a website resource.</span><span class="sxs-lookup"><span data-stu-id="1f893-151">The following example sets up an alert on a website resource.</span></span> <span data-ttu-id="1f893-152">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="1f893-152">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="1f893-153">To create a webhook or send an email when a classic metric alert fires, first create the email or webhook.</span><span class="sxs-lookup"><span data-stu-id="1f893-153">To create a webhook or send an email when a classic metric alert fires, first create the email or webhook.</span></span> <span data-ttu-id="1f893-154">Then create the rule immediately afterwards.</span><span class="sxs-lookup"><span data-stu-id="1f893-154">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="1f893-155">You can't associate webhooks or emails with rules that have already been created.</span><span class="sxs-lookup"><span data-stu-id="1f893-155">You can't associate webhooks or emails with rules that have already been created.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="1f893-156">You can verify that your alerts have been created properly by looking at an individual rule.</span><span class="sxs-lookup"><span data-stu-id="1f893-156">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="1f893-157">To delete rules, use a command in the following format:</span><span class="sxs-lookup"><span data-stu-id="1f893-157">To delete rules, use a command in the following format:</span></span>

    <span data-ttu-id="1f893-158">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="1f893-158">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="1f893-159">These commands delete the rules that were previously created in this article.</span><span class="sxs-lookup"><span data-stu-id="1f893-159">These commands delete the rules that were previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="1f893-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f893-160">Next steps</span></span>
* <span data-ttu-id="1f893-161">[Get an overview of Azure monitoring](monitoring-overview.md), including the types of information you can collect and monitor.</span><span class="sxs-lookup"><span data-stu-id="1f893-161">[Get an overview of Azure monitoring](monitoring-overview.md), including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="1f893-162">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1f893-162">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="1f893-163">Learn more about [configuring alerts on activity log events](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1f893-163">Learn more about [configuring alerts on activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="1f893-164">Learn more about [Azure Automation runbooks](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1f893-164">Learn more about [Azure Automation runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="1f893-165">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics for your service.</span><span class="sxs-lookup"><span data-stu-id="1f893-165">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics for your service.</span></span>
* <span data-ttu-id="1f893-166">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="1f893-166">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
