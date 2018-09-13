---
title: Create alerts for Azure services - PowerShell | Microsoft Docs
description: Trigger emails, notifications, call websites URLs (webhooks), or automation when the conditions you specify are met.
author: rboucher
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 50127242cdf156771d0610e58cf2fc41281adae7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551999"
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="f5b56-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5b56-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="f5b56-107">Overview</span><span class="sxs-lookup"><span data-stu-id="f5b56-107">Overview</span></span>
<span data-ttu-id="f5b56-108">This article shows you how to set up Azure metric alerts using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5b56-108">This article shows you how to set up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="f5b56-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span><span class="sxs-lookup"><span data-stu-id="f5b56-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="f5b56-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span><span class="sxs-lookup"><span data-stu-id="f5b56-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="f5b56-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span><span class="sxs-lookup"><span data-stu-id="f5b56-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="f5b56-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span><span class="sxs-lookup"><span data-stu-id="f5b56-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="f5b56-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f5b56-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="f5b56-114">You can configure a metric alert to do the following when it triggers:</span><span class="sxs-lookup"><span data-stu-id="f5b56-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="f5b56-115">send email notifications to the service administrator and co-administrators</span><span class="sxs-lookup"><span data-stu-id="f5b56-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="f5b56-116">send email to additional emails that you specify.</span><span class="sxs-lookup"><span data-stu-id="f5b56-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="f5b56-117">call a webhook</span><span class="sxs-lookup"><span data-stu-id="f5b56-117">call a webhook</span></span>
* <span data-ttu-id="f5b56-118">start execution of an Azure runbook (only from the Azure portal)</span><span class="sxs-lookup"><span data-stu-id="f5b56-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="f5b56-119">You can configure and get information about alert rules using</span><span class="sxs-lookup"><span data-stu-id="f5b56-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="f5b56-120">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f5b56-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="f5b56-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5b56-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="f5b56-122">command-line interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="f5b56-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="f5b56-123">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="f5b56-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="f5b56-124">For additional information, you can always type ```Get-Help``` and then the PowerShell command you want help on.</span><span class="sxs-lookup"><span data-stu-id="f5b56-124">For additional information, you can always type ```Get-Help``` and then the PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="f5b56-125">Create alert rules in PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5b56-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="f5b56-126">Log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="f5b56-126">Log in to Azure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="f5b56-127">Get a list of the subscriptions you have available.</span><span class="sxs-lookup"><span data-stu-id="f5b56-127">Get a list of the subscriptions you have available.</span></span> <span data-ttu-id="f5b56-128">Verify that you are working with the right subscription.</span><span class="sxs-lookup"><span data-stu-id="f5b56-128">Verify that you are working with the right subscription.</span></span> <span data-ttu-id="f5b56-129">If not, set it to the right one using the output from `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="f5b56-129">If not, set it to the right one using the output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="f5b56-130">To list existing rules on a resource group, use the following command:</span><span class="sxs-lookup"><span data-stu-id="f5b56-130">To list existing rules on a resource group, use the following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="f5b56-131">To create a rule, you need to have several important pieces of information first.</span><span class="sxs-lookup"><span data-stu-id="f5b56-131">To create a rule, you need to have several important pieces of information first.</span></span>

  * <span data-ttu-id="f5b56-132">The **Resource ID** for the resource you want to set an alert for</span><span class="sxs-lookup"><span data-stu-id="f5b56-132">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="f5b56-133">The **metric definitions** available for that resource</span><span class="sxs-lookup"><span data-stu-id="f5b56-133">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="f5b56-134">One way to get the Resource ID is to use the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f5b56-134">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="f5b56-135">Assuming the resource is already created, select it in the portal.</span><span class="sxs-lookup"><span data-stu-id="f5b56-135">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="f5b56-136">Then in the next blade, select *Properties* under the *Settings* section.</span><span class="sxs-lookup"><span data-stu-id="f5b56-136">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="f5b56-137">**RESOURCE ID** is a field in the next blade.</span><span class="sxs-lookup"><span data-stu-id="f5b56-137">**RESOURCE ID** is a field in the next blade.</span></span> <span data-ttu-id="f5b56-138">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f5b56-138">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="f5b56-139">An example Resource ID for a web app is</span><span class="sxs-lookup"><span data-stu-id="f5b56-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="f5b56-140">You can use `Get-AzureRmMetricDefinition` to view the list of all metric definitions for a specific resource.</span><span class="sxs-lookup"><span data-stu-id="f5b56-140">You can use `Get-AzureRmMetricDefinition` to view the list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="f5b56-141">The following example generates a table with the metric Name and the Unit for that metric.</span><span class="sxs-lookup"><span data-stu-id="f5b56-141">The following example generates a table with the metric Name and the Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="f5b56-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="f5b56-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="f5b56-143">The following example sets up an alert on a web site resource.</span><span class="sxs-lookup"><span data-stu-id="f5b56-143">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="f5b56-144">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="f5b56-144">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="f5b56-145">To create webhook or send email when an alert triggers, first create the email and/or webhooks.</span><span class="sxs-lookup"><span data-stu-id="f5b56-145">To create webhook or send email when an alert triggers, first create the email and/or webhooks.</span></span> <span data-ttu-id="f5b56-146">Then immediately create the rule afterwards with the -Actions tag and as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="f5b56-146">Then immediately create the rule afterwards with the -Actions tag and as shown in the following example.</span></span> <span data-ttu-id="f5b56-147">You cannot associate webhook or emails with already created rules via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f5b56-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="f5b56-148">To verify that your alerts have been created properly by looking at the individual rules.</span><span class="sxs-lookup"><span data-stu-id="f5b56-148">To verify that your alerts have been created properly by looking at the individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="f5b56-149">Delete your alerts.</span><span class="sxs-lookup"><span data-stu-id="f5b56-149">Delete your alerts.</span></span> <span data-ttu-id="f5b56-150">These commands delete the rules created previously in this article.</span><span class="sxs-lookup"><span data-stu-id="f5b56-150">These commands delete the rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="f5b56-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5b56-151">Next steps</span></span>
* <span data-ttu-id="f5b56-152">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span><span class="sxs-lookup"><span data-stu-id="f5b56-152">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="f5b56-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f5b56-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="f5b56-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f5b56-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="f5b56-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="f5b56-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="f5b56-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span><span class="sxs-lookup"><span data-stu-id="f5b56-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="f5b56-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="f5b56-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
