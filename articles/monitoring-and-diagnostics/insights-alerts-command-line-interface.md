---
title: Create alerts for Azure services - Cross-platform CLI | Microsoft Docs
description: Trigger emails, notifications, call websites URLs (webhooks), or automation when the conditions you specify are met.
author: rboucher
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540971"
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="4edaf-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span><span class="sxs-lookup"><span data-stu-id="4edaf-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="4edaf-107">Overview</span><span class="sxs-lookup"><span data-stu-id="4edaf-107">Overview</span></span>
<span data-ttu-id="4edaf-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="4edaf-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016. However, the namespaces and thus the commands below still contain the "insights".
>
>

<span data-ttu-id="4edaf-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span><span class="sxs-lookup"><span data-stu-id="4edaf-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="4edaf-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span><span class="sxs-lookup"><span data-stu-id="4edaf-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="4edaf-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span><span class="sxs-lookup"><span data-stu-id="4edaf-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="4edaf-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span><span class="sxs-lookup"><span data-stu-id="4edaf-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="4edaf-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="4edaf-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="4edaf-116">You can configure a metric alert to do the following when it triggers:</span><span class="sxs-lookup"><span data-stu-id="4edaf-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="4edaf-117">send email notifications to the service administrator and co-administrators</span><span class="sxs-lookup"><span data-stu-id="4edaf-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="4edaf-118">send email to additional emails that you specify.</span><span class="sxs-lookup"><span data-stu-id="4edaf-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="4edaf-119">call a webhook</span><span class="sxs-lookup"><span data-stu-id="4edaf-119">call a webhook</span></span>
* <span data-ttu-id="4edaf-120">start execution of an Azure runbook (only from the Azure portal at this time)</span><span class="sxs-lookup"><span data-stu-id="4edaf-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="4edaf-121">You can configure and get information about metric alert rules using</span><span class="sxs-lookup"><span data-stu-id="4edaf-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="4edaf-122">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4edaf-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="4edaf-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4edaf-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="4edaf-124">command-line interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="4edaf-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="4edaf-125">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="4edaf-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="4edaf-126">You can always receive help for commands by typing a command and putting -help at the end.</span><span class="sxs-lookup"><span data-stu-id="4edaf-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="4edaf-127">For example:</span><span class="sxs-lookup"><span data-stu-id="4edaf-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="4edaf-128">Create alert rules using the CLI</span><span class="sxs-lookup"><span data-stu-id="4edaf-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="4edaf-129">Perform the Prerequisites and login to Azure.</span><span class="sxs-lookup"><span data-stu-id="4edaf-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="4edaf-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4edaf-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="4edaf-131">In short, install the CLI and run these commands.</span><span class="sxs-lookup"><span data-stu-id="4edaf-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="4edaf-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span><span class="sxs-lookup"><span data-stu-id="4edaf-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="4edaf-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="4edaf-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="4edaf-134">To create a rule, you need to have several important pieces of information first.</span><span class="sxs-lookup"><span data-stu-id="4edaf-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="4edaf-135">The **Resource ID** for the resource you want to set an alert for</span><span class="sxs-lookup"><span data-stu-id="4edaf-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="4edaf-136">The **metric definitions** available for that resource</span><span class="sxs-lookup"><span data-stu-id="4edaf-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="4edaf-137">One way to get the Resource ID is to use the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4edaf-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="4edaf-138">Assuming the resource is already created, select it in the portal.</span><span class="sxs-lookup"><span data-stu-id="4edaf-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="4edaf-139">Then in the next blade, select *Properties* under the *Settings* section.</span><span class="sxs-lookup"><span data-stu-id="4edaf-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="4edaf-140">The *RESOURCE ID* is a field in the next blade.</span><span class="sxs-lookup"><span data-stu-id="4edaf-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="4edaf-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4edaf-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="4edaf-142">An example resource id for a web app is</span><span class="sxs-lookup"><span data-stu-id="4edaf-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="4edaf-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span><span class="sxs-lookup"><span data-stu-id="4edaf-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="4edaf-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span><span class="sxs-lookup"><span data-stu-id="4edaf-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="4edaf-145">Using different granularities gives you different metric options.</span><span class="sxs-lookup"><span data-stu-id="4edaf-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="4edaf-146">To create a metric-based alert rule, use a command of the following form:</span><span class="sxs-lookup"><span data-stu-id="4edaf-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="4edaf-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="4edaf-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="4edaf-148">The following example sets up an alert on a web site resource.</span><span class="sxs-lookup"><span data-stu-id="4edaf-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="4edaf-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="4edaf-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="4edaf-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span><span class="sxs-lookup"><span data-stu-id="4edaf-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="4edaf-151">Then create the rule immediately afterwards.</span><span class="sxs-lookup"><span data-stu-id="4edaf-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="4edaf-152">You cannot associate webhook or emails with already created rules using the CLI.</span><span class="sxs-lookup"><span data-stu-id="4edaf-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="4edaf-153">You can verify that your alerts have been created properly by looking at an individual rule.</span><span class="sxs-lookup"><span data-stu-id="4edaf-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="4edaf-154">To delete rules, use a command of the form:</span><span class="sxs-lookup"><span data-stu-id="4edaf-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="4edaf-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="4edaf-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="4edaf-156">These commands delete the rules previously created in this article.</span><span class="sxs-lookup"><span data-stu-id="4edaf-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="4edaf-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="4edaf-157">Next steps</span></span>
* <span data-ttu-id="4edaf-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span><span class="sxs-lookup"><span data-stu-id="4edaf-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="4edaf-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4edaf-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="4edaf-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4edaf-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="4edaf-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="4edaf-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="4edaf-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span><span class="sxs-lookup"><span data-stu-id="4edaf-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="4edaf-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="4edaf-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
