---
title: Azure Monitor PowerShell quick start samples
description: Use PowerShell to access Azure Monitor features such as autoscale, alerts, webhooks and searching Activity logs.
author: rboucher
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 2/14/2018
ms.author: robb
ms.component: ''
ms.openlocfilehash: c6189291a9e944acde751a66cdb58f2052c73999
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44801052"
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="f3e98-103">Azure Monitor PowerShell quick start samples</span><span class="sxs-lookup"><span data-stu-id="f3e98-103">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="f3e98-104">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span><span class="sxs-lookup"><span data-stu-id="f3e98-104">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e98-105">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span><span class="sxs-lookup"><span data-stu-id="f3e98-105">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="f3e98-106">However, the namespaces and thus the following commands still contain the word "insights."</span><span class="sxs-lookup"><span data-stu-id="f3e98-106">However, the namespaces and thus the following commands still contain the word "insights."</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="f3e98-107">Set up PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3e98-107">Set up PowerShell</span></span>
<span data-ttu-id="f3e98-108">If you haven't already, set up PowerShell to run on your computer.</span><span class="sxs-lookup"><span data-stu-id="f3e98-108">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="f3e98-109">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f3e98-109">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="f3e98-110">Examples in this article</span><span class="sxs-lookup"><span data-stu-id="f3e98-110">Examples in this article</span></span>
<span data-ttu-id="f3e98-111">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f3e98-111">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="f3e98-112">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.insights).</span><span class="sxs-lookup"><span data-stu-id="f3e98-112">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.insights).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="f3e98-113">Sign in and use subscriptions</span><span class="sxs-lookup"><span data-stu-id="f3e98-113">Sign in and use subscriptions</span></span>
<span data-ttu-id="f3e98-114">First, log in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f3e98-114">First, log in to your Azure subscription.</span></span>

```PowerShell
Connect-AzureRmAccount
```

<span data-ttu-id="f3e98-115">You'll see a sign in screen.</span><span class="sxs-lookup"><span data-stu-id="f3e98-115">You'll see a sign in screen.</span></span> <span data-ttu-id="f3e98-116">Once you sign in your Account, TenantID, and default Subscription ID are displayed.</span><span class="sxs-lookup"><span data-stu-id="f3e98-116">Once you sign in your Account, TenantID, and default Subscription ID are displayed.</span></span> <span data-ttu-id="f3e98-117">All the Azure cmdlets work in the context of your default subscription.</span><span class="sxs-lookup"><span data-stu-id="f3e98-117">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="f3e98-118">To view the list of subscriptions you have access to, use the following command:</span><span class="sxs-lookup"><span data-stu-id="f3e98-118">To view the list of subscriptions you have access to, use the following command:</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="f3e98-119">To change your working context to a different subscription, use the following command:</span><span class="sxs-lookup"><span data-stu-id="f3e98-119">To change your working context to a different subscription, use the following command:</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="f3e98-120">Retrieve Activity log for a subscription</span><span class="sxs-lookup"><span data-stu-id="f3e98-120">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="f3e98-121">Use the `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f3e98-121">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="f3e98-122">The following are some common examples.</span><span class="sxs-lookup"><span data-stu-id="f3e98-122">The following are some common examples.</span></span>

<span data-ttu-id="f3e98-123">Get log entries from this time/date to present:</span><span class="sxs-lookup"><span data-stu-id="f3e98-123">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="f3e98-124">Get log entries between a time/date range:</span><span class="sxs-lookup"><span data-stu-id="f3e98-124">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="f3e98-125">Get log entries from a specific resource group:</span><span class="sxs-lookup"><span data-stu-id="f3e98-125">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="f3e98-126">Get log entries from a specific resource provider between a time/date range:</span><span class="sxs-lookup"><span data-stu-id="f3e98-126">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="f3e98-127">Get all log entries with a specific caller:</span><span class="sxs-lookup"><span data-stu-id="f3e98-127">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="f3e98-128">The following command retrieves the last 1000 events from the activity log:</span><span class="sxs-lookup"><span data-stu-id="f3e98-128">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="f3e98-129">`Get-AzureRmLog` supports many other parameters.</span><span class="sxs-lookup"><span data-stu-id="f3e98-129">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="f3e98-130">See the `Get-AzureRmLog` reference for more information.</span><span class="sxs-lookup"><span data-stu-id="f3e98-130">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="f3e98-131">`Get-AzureRmLog` only provides 15 days of history.</span><span class="sxs-lookup"><span data-stu-id="f3e98-131">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="f3e98-132">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span><span class="sxs-lookup"><span data-stu-id="f3e98-132">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="f3e98-133">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span><span class="sxs-lookup"><span data-stu-id="f3e98-133">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="f3e98-134">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span><span class="sxs-lookup"><span data-stu-id="f3e98-134">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="f3e98-135">If you do not include **EndTime**, then the default value is current time.</span><span class="sxs-lookup"><span data-stu-id="f3e98-135">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="f3e98-136">All times are in UTC.</span><span class="sxs-lookup"><span data-stu-id="f3e98-136">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="f3e98-137">Retrieve alerts history</span><span class="sxs-lookup"><span data-stu-id="f3e98-137">Retrieve alerts history</span></span>
<span data-ttu-id="f3e98-138">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span><span class="sxs-lookup"><span data-stu-id="f3e98-138">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="f3e98-139">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="f3e98-139">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="f3e98-140">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span><span class="sxs-lookup"><span data-stu-id="f3e98-140">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="f3e98-141">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3e98-141">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="f3e98-142">Retrieve information on alert rules</span><span class="sxs-lookup"><span data-stu-id="f3e98-142">Retrieve information on alert rules</span></span>
<span data-ttu-id="f3e98-143">All of the following commands act on a Resource Group named "montest".</span><span class="sxs-lookup"><span data-stu-id="f3e98-143">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="f3e98-144">View all the properties of the alert rule:</span><span class="sxs-lookup"><span data-stu-id="f3e98-144">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="f3e98-145">Retrieve all alerts on a resource group:</span><span class="sxs-lookup"><span data-stu-id="f3e98-145">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="f3e98-146">Retrieve all alert rules set for a target resource.</span><span class="sxs-lookup"><span data-stu-id="f3e98-146">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="f3e98-147">For example, all alert rules set on a VM.</span><span class="sxs-lookup"><span data-stu-id="f3e98-147">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="f3e98-148">`Get-AzureRmAlertRule` supports other parameters.</span><span class="sxs-lookup"><span data-stu-id="f3e98-148">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="f3e98-149">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="f3e98-149">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="f3e98-150">Create metric alerts</span><span class="sxs-lookup"><span data-stu-id="f3e98-150">Create metric alerts</span></span>
<span data-ttu-id="f3e98-151">You can use the `Add-AlertRule` cmdlet to create, update, or disable an alert rule.</span><span class="sxs-lookup"><span data-stu-id="f3e98-151">You can use the `Add-AlertRule` cmdlet to create, update, or disable an alert rule.</span></span>

<span data-ttu-id="f3e98-152">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span><span class="sxs-lookup"><span data-stu-id="f3e98-152">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="f3e98-153">In the Alert rule cmdlet, assign these properties as actions to the **Actions** property of the Alert Rule.</span><span class="sxs-lookup"><span data-stu-id="f3e98-153">In the Alert rule cmdlet, assign these properties as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="f3e98-154">The following table describes the parameters and values used to create an alert using a metric.</span><span class="sxs-lookup"><span data-stu-id="f3e98-154">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="f3e98-155">parameter</span><span class="sxs-lookup"><span data-stu-id="f3e98-155">parameter</span></span> | <span data-ttu-id="f3e98-156">value</span><span class="sxs-lookup"><span data-stu-id="f3e98-156">value</span></span> |
| --- | --- |
| <span data-ttu-id="f3e98-157">Name</span><span class="sxs-lookup"><span data-stu-id="f3e98-157">Name</span></span> |<span data-ttu-id="f3e98-158">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="f3e98-158">simpletestdiskwrite</span></span> |
| <span data-ttu-id="f3e98-159">Location of this alert rule</span><span class="sxs-lookup"><span data-stu-id="f3e98-159">Location of this alert rule</span></span> |<span data-ttu-id="f3e98-160">East US</span><span class="sxs-lookup"><span data-stu-id="f3e98-160">East US</span></span> |
| <span data-ttu-id="f3e98-161">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f3e98-161">ResourceGroup</span></span> |<span data-ttu-id="f3e98-162">montest</span><span class="sxs-lookup"><span data-stu-id="f3e98-162">montest</span></span> |
| <span data-ttu-id="f3e98-163">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="f3e98-163">TargetResourceId</span></span> |<span data-ttu-id="f3e98-164">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="f3e98-164">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="f3e98-165">MetricName of the alert that is created</span><span class="sxs-lookup"><span data-stu-id="f3e98-165">MetricName of the alert that is created</span></span> |<span data-ttu-id="f3e98-166">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span><span class="sxs-lookup"><span data-stu-id="f3e98-166">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="f3e98-167">operator</span><span class="sxs-lookup"><span data-stu-id="f3e98-167">operator</span></span> |<span data-ttu-id="f3e98-168">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="f3e98-168">GreaterThan</span></span> |
| <span data-ttu-id="f3e98-169">Threshold value (count/sec in for this metric)</span><span class="sxs-lookup"><span data-stu-id="f3e98-169">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="f3e98-170">1</span><span class="sxs-lookup"><span data-stu-id="f3e98-170">1</span></span> |
| <span data-ttu-id="f3e98-171">WindowSize (hh:mm:ss format)</span><span class="sxs-lookup"><span data-stu-id="f3e98-171">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="f3e98-172">00:05:00</span><span class="sxs-lookup"><span data-stu-id="f3e98-172">00:05:00</span></span> |
| <span data-ttu-id="f3e98-173">aggregator (statistic of the metric, which uses Average count, in this case)</span><span class="sxs-lookup"><span data-stu-id="f3e98-173">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="f3e98-174">Average</span><span class="sxs-lookup"><span data-stu-id="f3e98-174">Average</span></span> |
| <span data-ttu-id="f3e98-175">custom emails (string array)</span><span class="sxs-lookup"><span data-stu-id="f3e98-175">custom emails (string array)</span></span> |<span data-ttu-id="f3e98-176">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="f3e98-176">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="f3e98-177">send email to owners, contributors and readers</span><span class="sxs-lookup"><span data-stu-id="f3e98-177">send email to owners, contributors and readers</span></span> |<span data-ttu-id="f3e98-178">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="f3e98-178">-SendToServiceOwners</span></span> |

<span data-ttu-id="f3e98-179">Create an Email action</span><span class="sxs-lookup"><span data-stu-id="f3e98-179">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="f3e98-180">Create a Webhook action</span><span class="sxs-lookup"><span data-stu-id="f3e98-180">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="f3e98-181">Create the alert rule on the CPU% metric on a classic VM</span><span class="sxs-lookup"><span data-stu-id="f3e98-181">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="f3e98-182">Retrieve the alert rule</span><span class="sxs-lookup"><span data-stu-id="f3e98-182">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="f3e98-183">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span><span class="sxs-lookup"><span data-stu-id="f3e98-183">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="f3e98-184">To disable an alert rule, include the parameter **-DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="f3e98-184">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="f3e98-185">Get a list of available metrics for alerts</span><span class="sxs-lookup"><span data-stu-id="f3e98-185">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="f3e98-186">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span><span class="sxs-lookup"><span data-stu-id="f3e98-186">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="f3e98-187">The following example generates a table with the metric Name and the Unit for it.</span><span class="sxs-lookup"><span data-stu-id="f3e98-187">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="f3e98-188">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3e98-188">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-activity-log-alerts"></a><span data-ttu-id="f3e98-189">Create and manage Activity Log alerts</span><span class="sxs-lookup"><span data-stu-id="f3e98-189">Create and manage Activity Log alerts</span></span>
<span data-ttu-id="f3e98-190">You can use the `Set-AzureRmActivityLogAlert` cmdlet to set an Activity Log alert.</span><span class="sxs-lookup"><span data-stu-id="f3e98-190">You can use the `Set-AzureRmActivityLogAlert` cmdlet to set an Activity Log alert.</span></span> <span data-ttu-id="f3e98-191">An Activity Log alert requires that you first define your conditions as a dictionary of conditions, then create an alert that uses those conditions.</span><span class="sxs-lookup"><span data-stu-id="f3e98-191">An Activity Log alert requires that you first define your conditions as a dictionary of conditions, then create an alert that uses those conditions.</span></span>

```PowerShell

$condition1 = New-AzureRmActivityLogAlertCondition -Field 'category' -Equals 'Administrative'
$condition2 = New-AzureRmActivityLogAlertCondition -Field 'operationName' -Equals 'Microsoft.Compute/virtualMachines/write'
$additionalWebhookProperties = New-Object "System.Collections.Generic.Dictionary``2[System.String,System.String]"
$additionalWebhookProperties.Add('customProperty', 'someValue')
$actionGrp1 = New-AzureRmActionGroup -ActionGroupId 'actiongr1' -WebhookProperties $dict
Set-AzureRmActivityLogAlert -Location 'Global' -Name 'alert on VM create' -ResourceGroupName 'myResourceGroup' -Scope '/' -Action $actionGrp1 -Condition $condition1, $condition2

```

<span data-ttu-id="f3e98-192">The additional webhook properties are optional.</span><span class="sxs-lookup"><span data-stu-id="f3e98-192">The additional webhook properties are optional.</span></span> <span data-ttu-id="f3e98-193">You can get back the contents of an Activity Log Alert using `Get-AzureRmActivityLogAlert`.</span><span class="sxs-lookup"><span data-stu-id="f3e98-193">You can get back the contents of an Activity Log Alert using `Get-AzureRmActivityLogAlert`.</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="f3e98-194">Create and manage AutoScale settings</span><span class="sxs-lookup"><span data-stu-id="f3e98-194">Create and manage AutoScale settings</span></span>
<span data-ttu-id="f3e98-195">A resource (a Web app, VM, Cloud Service, or Virtual Machine Scale Set) can have only one autoscale setting configured for it.</span><span class="sxs-lookup"><span data-stu-id="f3e98-195">A resource (a Web app, VM, Cloud Service, or Virtual Machine Scale Set) can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="f3e98-196">However, each autoscale setting can have multiple profiles.</span><span class="sxs-lookup"><span data-stu-id="f3e98-196">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="f3e98-197">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span><span class="sxs-lookup"><span data-stu-id="f3e98-197">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="f3e98-198">Each profile can have multiple rules configured on it.</span><span class="sxs-lookup"><span data-stu-id="f3e98-198">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="f3e98-199">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f3e98-199">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale-portal.md).</span></span>

<span data-ttu-id="f3e98-200">Here are the steps to use:</span><span class="sxs-lookup"><span data-stu-id="f3e98-200">Here are the steps to use:</span></span>

1. <span data-ttu-id="f3e98-201">Create rule(s).</span><span class="sxs-lookup"><span data-stu-id="f3e98-201">Create rule(s).</span></span>
2. <span data-ttu-id="f3e98-202">Create profile(s) mapping the rules that you created previously to the profiles.</span><span class="sxs-lookup"><span data-stu-id="f3e98-202">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="f3e98-203">Optional: Create notifications for autoscale by configuring webhook and email properties.</span><span class="sxs-lookup"><span data-stu-id="f3e98-203">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="f3e98-204">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="f3e98-204">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="f3e98-205">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span><span class="sxs-lookup"><span data-stu-id="f3e98-205">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="f3e98-206">First, create a rule to scale out, with an instance count increase.</span><span class="sxs-lookup"><span data-stu-id="f3e98-206">First, create a rule to scale out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="f3e98-207">Next, create a rule to scale in, with an instance count decrease.</span><span class="sxs-lookup"><span data-stu-id="f3e98-207">Next, create a rule to scale in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="f3e98-208">Then, create a profile for the rules.</span><span class="sxs-lookup"><span data-stu-id="f3e98-208">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="f3e98-209">Create a webhook property.</span><span class="sxs-lookup"><span data-stu-id="f3e98-209">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="f3e98-210">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span><span class="sxs-lookup"><span data-stu-id="f3e98-210">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="f3e98-211">Finally, create the autoscale setting to add the profile that you created previously.</span><span class="sxs-lookup"><span data-stu-id="f3e98-211">Finally, create the autoscale setting to add the profile that you created previously.</span></span> 

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="f3e98-212">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3e98-212">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="f3e98-213">Autoscale history</span><span class="sxs-lookup"><span data-stu-id="f3e98-213">Autoscale history</span></span>
<span data-ttu-id="f3e98-214">The following example shows you how you can view recent autoscale and alert events.</span><span class="sxs-lookup"><span data-stu-id="f3e98-214">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="f3e98-215">Use the activity log search to view the autoscale history.</span><span class="sxs-lookup"><span data-stu-id="f3e98-215">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="f3e98-216">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span><span class="sxs-lookup"><span data-stu-id="f3e98-216">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="f3e98-217">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3e98-217">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="f3e98-218">View details for an autoscale setting</span><span class="sxs-lookup"><span data-stu-id="f3e98-218">View details for an autoscale setting</span></span>
<span data-ttu-id="f3e98-219">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="f3e98-219">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="f3e98-220">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="f3e98-220">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="f3e98-221">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span><span class="sxs-lookup"><span data-stu-id="f3e98-221">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="f3e98-222">Remove an autoscale setting</span><span class="sxs-lookup"><span data-stu-id="f3e98-222">Remove an autoscale setting</span></span>
<span data-ttu-id="f3e98-223">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="f3e98-223">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="f3e98-224">Manage log profiles for activity log</span><span class="sxs-lookup"><span data-stu-id="f3e98-224">Manage log profiles for activity log</span></span>
<span data-ttu-id="f3e98-225">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span><span class="sxs-lookup"><span data-stu-id="f3e98-225">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="f3e98-226">Optionally, you can also stream the data to your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="f3e98-226">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="f3e98-227">This feature is currently in Preview and you can only create one log profile per subscription.</span><span class="sxs-lookup"><span data-stu-id="f3e98-227">This feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="f3e98-228">You can use the following cmdlets with your current subscription to create and manage log profiles.</span><span class="sxs-lookup"><span data-stu-id="f3e98-228">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="f3e98-229">You can also choose a particular subscription.</span><span class="sxs-lookup"><span data-stu-id="f3e98-229">You can also choose a particular subscription.</span></span> <span data-ttu-id="f3e98-230">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="f3e98-230">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="f3e98-231">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span><span class="sxs-lookup"><span data-stu-id="f3e98-231">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="f3e98-232">Data is written as blob files in JSON format.</span><span class="sxs-lookup"><span data-stu-id="f3e98-232">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="f3e98-233">Get a log profile</span><span class="sxs-lookup"><span data-stu-id="f3e98-233">Get a log profile</span></span>
<span data-ttu-id="f3e98-234">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f3e98-234">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="f3e98-235">Add a log profile without data retention</span><span class="sxs-lookup"><span data-stu-id="f3e98-235">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="f3e98-236">Remove a log profile</span><span class="sxs-lookup"><span data-stu-id="f3e98-236">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="f3e98-237">Add a log profile with data retention</span><span class="sxs-lookup"><span data-stu-id="f3e98-237">Add a log profile with data retention</span></span>
<span data-ttu-id="f3e98-238">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span><span class="sxs-lookup"><span data-stu-id="f3e98-238">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="f3e98-239">Add log profile with retention and EventHub</span><span class="sxs-lookup"><span data-stu-id="f3e98-239">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="f3e98-240">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span><span class="sxs-lookup"><span data-stu-id="f3e98-240">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="f3e98-241">In this preview release the storage account configuration is mandatory but Event Hub configuration is optional.</span><span class="sxs-lookup"><span data-stu-id="f3e98-241">In this preview release the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="f3e98-242">Configure diagnostics logs</span><span class="sxs-lookup"><span data-stu-id="f3e98-242">Configure diagnostics logs</span></span>
<span data-ttu-id="f3e98-243">Many Azure services provide additional logs and telemetry that can do one or more of the following:</span><span class="sxs-lookup"><span data-stu-id="f3e98-243">Many Azure services provide additional logs and telemetry that can do one or more of the following:</span></span> 
 - <span data-ttu-id="f3e98-244">be configured to save data in your Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="f3e98-244">be configured to save data in your Azure Storage account</span></span>
 - <span data-ttu-id="f3e98-245">sent to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f3e98-245">sent to Event Hubs</span></span>
 - <span data-ttu-id="f3e98-246">sent to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="f3e98-246">sent to a Log Analytics workspace.</span></span> 

<span data-ttu-id="f3e98-247">The operation can only be performed at a resource level.</span><span class="sxs-lookup"><span data-stu-id="f3e98-247">The operation can only be performed at a resource level.</span></span> <span data-ttu-id="f3e98-248">The storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span><span class="sxs-lookup"><span data-stu-id="f3e98-248">The storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="f3e98-249">Get diagnostic setting</span><span class="sxs-lookup"><span data-stu-id="f3e98-249">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="f3e98-250">Disable diagnostic setting</span><span class="sxs-lookup"><span data-stu-id="f3e98-250">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="f3e98-251">Enable diagnostic setting without retention</span><span class="sxs-lookup"><span data-stu-id="f3e98-251">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="f3e98-252">Enable diagnostic setting with retention</span><span class="sxs-lookup"><span data-stu-id="f3e98-252">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="f3e98-253">Enable diagnostic setting with retention for a specific log category</span><span class="sxs-lookup"><span data-stu-id="f3e98-253">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="f3e98-254">Enable diagnostic setting for Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f3e98-254">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="f3e98-255">Enable diagnostic setting for Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f3e98-255">Enable diagnostic setting for Log Analytics</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId /subscriptions/s1/resourceGroups/insights-integration/providers/providers/microsoft.operationalinsights/workspaces/myWorkspace -Enabled $true

```

<span data-ttu-id="f3e98-256">Note that the WorkspaceId property takes the *resource ID* of the workspace.</span><span class="sxs-lookup"><span data-stu-id="f3e98-256">Note that the WorkspaceId property takes the *resource ID* of the workspace.</span></span> <span data-ttu-id="f3e98-257">You can obtain the resource ID of your Log Analytics workspace using the following command:</span><span class="sxs-lookup"><span data-stu-id="f3e98-257">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```PowerShell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId

```

<span data-ttu-id="f3e98-258">These commands can be combined to send data to multiple destinations.</span><span class="sxs-lookup"><span data-stu-id="f3e98-258">These commands can be combined to send data to multiple destinations.</span></span>
