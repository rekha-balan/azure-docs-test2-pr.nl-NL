---
title: Azure Monitor PowerShell quick start samples. | Microsoft Docs
description: Use PowerShell to access Azure Monitor features such as autoscale, alerts, webhooks and searching Activity logs.
author: kamathashwin
manager: carolz
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ashwink
ms.openlocfilehash: 66848eee215732803a1070e13d56f35b17e54975
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555079"
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="aa39f-104">Azure Monitor PowerShell quick start samples</span><span class="sxs-lookup"><span data-stu-id="aa39f-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="aa39f-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span><span class="sxs-lookup"><span data-stu-id="aa39f-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="aa39f-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span><span class="sxs-lookup"><span data-stu-id="aa39f-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="aa39f-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span><span class="sxs-lookup"><span data-stu-id="aa39f-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="aa39f-108">However, the namespaces and thus the commands below still contain the "insights".</span><span class="sxs-lookup"><span data-stu-id="aa39f-108">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="aa39f-109">Set up PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa39f-109">Set up PowerShell</span></span>
<span data-ttu-id="aa39f-110">If you haven't already, set up PowerShell to run on your computer.</span><span class="sxs-lookup"><span data-stu-id="aa39f-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="aa39f-111">For more information, see [How to Install and Configure PowerShell](/powershell/azureps-cmdlets-docs) .</span><span class="sxs-lookup"><span data-stu-id="aa39f-111">For more information, see [How to Install and Configure PowerShell](/powershell/azureps-cmdlets-docs) .</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="aa39f-112">Examples in this article</span><span class="sxs-lookup"><span data-stu-id="aa39f-112">Examples in this article</span></span>
<span data-ttu-id="aa39f-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span><span class="sxs-lookup"><span data-stu-id="aa39f-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="aa39f-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa39f-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="aa39f-115">Sign in and use subscriptions</span><span class="sxs-lookup"><span data-stu-id="aa39f-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="aa39f-116">First, log into your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="aa39f-116">First, log into your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="aa39f-117">This requires you to sign in.</span><span class="sxs-lookup"><span data-stu-id="aa39f-117">This requires you to sign in.</span></span> <span data-ttu-id="aa39f-118">Once you do, your Account, TenantId and default Subscription Id are displayed.</span><span class="sxs-lookup"><span data-stu-id="aa39f-118">Once you do, your Account, TenantId and default Subscription Id are displayed.</span></span> <span data-ttu-id="aa39f-119">All the Azure cmdlets work in the context of your default subscription.</span><span class="sxs-lookup"><span data-stu-id="aa39f-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="aa39f-120">To view the list of subscriptions you have access to, use the following command.</span><span class="sxs-lookup"><span data-stu-id="aa39f-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="aa39f-121">To change your working context to a different subscription, use the following command.</span><span class="sxs-lookup"><span data-stu-id="aa39f-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="aa39f-122">Retrieve Activity log for a subscription</span><span class="sxs-lookup"><span data-stu-id="aa39f-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="aa39f-123">Use the `Get-AzureRmLog` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa39f-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="aa39f-124">Below are some common examples.</span><span class="sxs-lookup"><span data-stu-id="aa39f-124">Below are some common examples.</span></span>

<span data-ttu-id="aa39f-125">Get log entries from this time/date to present:</span><span class="sxs-lookup"><span data-stu-id="aa39f-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="aa39f-126">Get log entries between a time/date range:</span><span class="sxs-lookup"><span data-stu-id="aa39f-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="aa39f-127">Get log entries from a specific resource group:</span><span class="sxs-lookup"><span data-stu-id="aa39f-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="aa39f-128">Get log entries from a specific resource provider between a time/date range:</span><span class="sxs-lookup"><span data-stu-id="aa39f-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="aa39f-129">Get all log entries with a specific caller:</span><span class="sxs-lookup"><span data-stu-id="aa39f-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="aa39f-130">The following command retrieves the last 1000 events from the activity log:</span><span class="sxs-lookup"><span data-stu-id="aa39f-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="aa39f-131">`Get-AzureRmLog` supports many other parameters.</span><span class="sxs-lookup"><span data-stu-id="aa39f-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="aa39f-132">See the `Get-AzureRmLog` reference for more information.</span><span class="sxs-lookup"><span data-stu-id="aa39f-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="aa39f-133">`Get-AzureRmLog` only provides 15 days of history.</span><span class="sxs-lookup"><span data-stu-id="aa39f-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="aa39f-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span><span class="sxs-lookup"><span data-stu-id="aa39f-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="aa39f-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span><span class="sxs-lookup"><span data-stu-id="aa39f-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="aa39f-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span><span class="sxs-lookup"><span data-stu-id="aa39f-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="aa39f-137">If you do not include **EndTime**, then the default value is current time.</span><span class="sxs-lookup"><span data-stu-id="aa39f-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="aa39f-138">All times are in UTC.</span><span class="sxs-lookup"><span data-stu-id="aa39f-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="aa39f-139">Retrieve alerts history</span><span class="sxs-lookup"><span data-stu-id="aa39f-139">Retrieve alerts history</span></span>
<span data-ttu-id="aa39f-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span><span class="sxs-lookup"><span data-stu-id="aa39f-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="aa39f-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="aa39f-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="aa39f-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span><span class="sxs-lookup"><span data-stu-id="aa39f-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="aa39f-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa39f-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="aa39f-144">Retrieve information on alert rules</span><span class="sxs-lookup"><span data-stu-id="aa39f-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="aa39f-145">All of the following commands act on a Resource Group named "montest".</span><span class="sxs-lookup"><span data-stu-id="aa39f-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="aa39f-146">View all the properties of the alert rule:</span><span class="sxs-lookup"><span data-stu-id="aa39f-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="aa39f-147">Retrieve all alerts on a resource group:</span><span class="sxs-lookup"><span data-stu-id="aa39f-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="aa39f-148">Retrieve all alert rules set for a target resource.</span><span class="sxs-lookup"><span data-stu-id="aa39f-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="aa39f-149">For example, all alert rules set on a VM.</span><span class="sxs-lookup"><span data-stu-id="aa39f-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="aa39f-150">`Get-AzureRmAlertRule` supports other parameters.</span><span class="sxs-lookup"><span data-stu-id="aa39f-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="aa39f-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="aa39f-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-alert-rules"></a><span data-ttu-id="aa39f-152">Create alert rules</span><span class="sxs-lookup"><span data-stu-id="aa39f-152">Create alert rules</span></span>
<span data-ttu-id="aa39f-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span><span class="sxs-lookup"><span data-stu-id="aa39f-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="aa39f-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span><span class="sxs-lookup"><span data-stu-id="aa39f-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="aa39f-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span><span class="sxs-lookup"><span data-stu-id="aa39f-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="aa39f-156">The next section contains a sample that shows you how to create an Alert Rule with various parameters.</span><span class="sxs-lookup"><span data-stu-id="aa39f-156">The next section contains a sample that shows you how to create an Alert Rule with various parameters.</span></span>

### <a name="alert-rule-on-a-metric"></a><span data-ttu-id="aa39f-157">Alert rule on a metric</span><span class="sxs-lookup"><span data-stu-id="aa39f-157">Alert rule on a metric</span></span>
<span data-ttu-id="aa39f-158">The following table describes the parameters and values used to create an alert using a metric.</span><span class="sxs-lookup"><span data-stu-id="aa39f-158">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="aa39f-159">parameter</span><span class="sxs-lookup"><span data-stu-id="aa39f-159">parameter</span></span> | <span data-ttu-id="aa39f-160">value</span><span class="sxs-lookup"><span data-stu-id="aa39f-160">value</span></span> |
| --- | --- |
| <span data-ttu-id="aa39f-161">Name</span><span class="sxs-lookup"><span data-stu-id="aa39f-161">Name</span></span> |<span data-ttu-id="aa39f-162">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="aa39f-162">simpletestdiskwrite</span></span> |
| <span data-ttu-id="aa39f-163">Location of this alert rule</span><span class="sxs-lookup"><span data-stu-id="aa39f-163">Location of this alert rule</span></span> |<span data-ttu-id="aa39f-164">East US</span><span class="sxs-lookup"><span data-stu-id="aa39f-164">East US</span></span> |
| <span data-ttu-id="aa39f-165">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="aa39f-165">ResourceGroup</span></span> |<span data-ttu-id="aa39f-166">montest</span><span class="sxs-lookup"><span data-stu-id="aa39f-166">montest</span></span> |
| <span data-ttu-id="aa39f-167">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="aa39f-167">TargetResourceId</span></span> |<span data-ttu-id="aa39f-168">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="aa39f-168">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="aa39f-169">MetricName of the alert that is created</span><span class="sxs-lookup"><span data-stu-id="aa39f-169">MetricName of the alert that is created</span></span> |<span data-ttu-id="aa39f-170">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet below about how to retrieve the exact metric names</span><span class="sxs-lookup"><span data-stu-id="aa39f-170">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet below about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="aa39f-171">operator</span><span class="sxs-lookup"><span data-stu-id="aa39f-171">operator</span></span> |<span data-ttu-id="aa39f-172">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="aa39f-172">GreaterThan</span></span> |
| <span data-ttu-id="aa39f-173">Threshold value (count/sec in for this metric)</span><span class="sxs-lookup"><span data-stu-id="aa39f-173">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="aa39f-174">1</span><span class="sxs-lookup"><span data-stu-id="aa39f-174">1</span></span> |
| <span data-ttu-id="aa39f-175">WindowSize (hh:mm:ss format)</span><span class="sxs-lookup"><span data-stu-id="aa39f-175">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="aa39f-176">00:05:00</span><span class="sxs-lookup"><span data-stu-id="aa39f-176">00:05:00</span></span> |
| <span data-ttu-id="aa39f-177">aggregator (statistic of the metric, which uses Average count, in this case)</span><span class="sxs-lookup"><span data-stu-id="aa39f-177">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="aa39f-178">Average</span><span class="sxs-lookup"><span data-stu-id="aa39f-178">Average</span></span> |
| <span data-ttu-id="aa39f-179">custom emails (string array)</span><span class="sxs-lookup"><span data-stu-id="aa39f-179">custom emails (string array)</span></span> |<span data-ttu-id="aa39f-180">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="aa39f-180">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="aa39f-181">send email to owners, contributors and readers</span><span class="sxs-lookup"><span data-stu-id="aa39f-181">send email to owners, contributors and readers</span></span> |<span data-ttu-id="aa39f-182">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="aa39f-182">-SendToServiceOwners</span></span> |

<span data-ttu-id="aa39f-183">Create an Email action</span><span class="sxs-lookup"><span data-stu-id="aa39f-183">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="aa39f-184">Create a Webhook action</span><span class="sxs-lookup"><span data-stu-id="aa39f-184">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="aa39f-185">Create the alert rule on the CPU% metric on a classic VM</span><span class="sxs-lookup"><span data-stu-id="aa39f-185">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="aa39f-186">Retrieve the alert rule</span><span class="sxs-lookup"><span data-stu-id="aa39f-186">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="aa39f-187">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span><span class="sxs-lookup"><span data-stu-id="aa39f-187">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="aa39f-188">To disable an alert rule, include the parameter **-DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="aa39f-188">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

### <a name="alert-on-activity-log-event"></a><span data-ttu-id="aa39f-189">Alert on activity log event</span><span class="sxs-lookup"><span data-stu-id="aa39f-189">Alert on activity log event</span></span>
> [!NOTE]
> <span data-ttu-id="aa39f-190">This feature is in preview and will be removed at some point in the future (it is being replaced).</span><span class="sxs-lookup"><span data-stu-id="aa39f-190">This feature is in preview and will be removed at some point in the future (it is being replaced).</span></span>
> 
> 

<span data-ttu-id="aa39f-191">In this scenario, you'll send email when a website is successfully started in my subscription in resource group *abhingrgtest123*.</span><span class="sxs-lookup"><span data-stu-id="aa39f-191">In this scenario, you'll send email when a website is successfully started in my subscription in resource group *abhingrgtest123*.</span></span>

<span data-ttu-id="aa39f-192">Setup an email rule</span><span class="sxs-lookup"><span data-stu-id="aa39f-192">Setup an email rule</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="aa39f-193">Setup a webhook rule</span><span class="sxs-lookup"><span data-stu-id="aa39f-193">Setup a webhook rule</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="aa39f-194">Create the rule on the event</span><span class="sxs-lookup"><span data-stu-id="aa39f-194">Create the rule on the event</span></span>

```PowerShell
Add-AzureRmLogAlertRule -Name superalert1 -Location "East US" -ResourceGroup myrg1 -OperationName microsoft.web/sites/start/action -Status Succeeded -TargetResourceGroup abhingrgtest123 -Actions $actionEmail, $actionWebhook
```

<span data-ttu-id="aa39f-195">Retrieve the alert rule</span><span class="sxs-lookup"><span data-stu-id="aa39f-195">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name superalert1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="aa39f-196">The `Add-AlertRule` cmdlet allows various other parameters.</span><span class="sxs-lookup"><span data-stu-id="aa39f-196">The `Add-AlertRule` cmdlet allows various other parameters.</span></span> <span data-ttu-id="aa39f-197">More information, see [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa39f-197">More information, see [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx).</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="aa39f-198">Get a list of available metrics for alerts</span><span class="sxs-lookup"><span data-stu-id="aa39f-198">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="aa39f-199">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span><span class="sxs-lookup"><span data-stu-id="aa39f-199">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="aa39f-200">The following example generates a table with the metric Name and the Unit for it.</span><span class="sxs-lookup"><span data-stu-id="aa39f-200">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="aa39f-201">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa39f-201">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="aa39f-202">Create and manage AutoScale settings</span><span class="sxs-lookup"><span data-stu-id="aa39f-202">Create and manage AutoScale settings</span></span>
<span data-ttu-id="aa39f-203">A resource, such as a Web app, VM, Cloud Service or VM Scale Set can have only one autoscale setting configured for it.</span><span class="sxs-lookup"><span data-stu-id="aa39f-203">A resource, such as a Web app, VM, Cloud Service or VM Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="aa39f-204">However, each autoscale setting can have multiple profiles.</span><span class="sxs-lookup"><span data-stu-id="aa39f-204">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="aa39f-205">For example, one for a performance-based scale profile and a second one for a schedule based profile.</span><span class="sxs-lookup"><span data-stu-id="aa39f-205">For example, one for a performance-based scale profile and a second one for a schedule based profile.</span></span> <span data-ttu-id="aa39f-206">Each profile can have multiple rules configured on it.</span><span class="sxs-lookup"><span data-stu-id="aa39f-206">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="aa39f-207">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="aa39f-207">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="aa39f-208">Here are the steps we will use:</span><span class="sxs-lookup"><span data-stu-id="aa39f-208">Here are the steps we will use:</span></span>

1. <span data-ttu-id="aa39f-209">Create rule(s).</span><span class="sxs-lookup"><span data-stu-id="aa39f-209">Create rule(s).</span></span>
2. <span data-ttu-id="aa39f-210">Create profile(s) mapping the rules that you created previously to the profiles.</span><span class="sxs-lookup"><span data-stu-id="aa39f-210">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="aa39f-211">Optional: Create notifications for autoscale by configuring webhook and email properties.</span><span class="sxs-lookup"><span data-stu-id="aa39f-211">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="aa39f-212">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="aa39f-212">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="aa39f-213">The following examples show you how you can create an Autoscale setting for a VM scale set for a Windows operating system based by using the CPU utilization metric.</span><span class="sxs-lookup"><span data-stu-id="aa39f-213">The following examples show you how you can create an Autoscale setting for a VM scale set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="aa39f-214">First, create a rule to scale-out, with an instance count increase .</span><span class="sxs-lookup"><span data-stu-id="aa39f-214">First, create a rule to scale-out, with an instance count increase .</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="aa39f-215">Next, create a rule to scale-in, with an instance count decrease.</span><span class="sxs-lookup"><span data-stu-id="aa39f-215">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="aa39f-216">Then, create a profile for the rules.</span><span class="sxs-lookup"><span data-stu-id="aa39f-216">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="aa39f-217">Create a webhook property.</span><span class="sxs-lookup"><span data-stu-id="aa39f-217">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="aa39f-218">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span><span class="sxs-lookup"><span data-stu-id="aa39f-218">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="aa39f-219">Finally, create the autoscale setting to add the profile that you created above.</span><span class="sxs-lookup"><span data-stu-id="aa39f-219">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="aa39f-220">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa39f-220">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="aa39f-221">Autoscale history</span><span class="sxs-lookup"><span data-stu-id="aa39f-221">Autoscale history</span></span>
<span data-ttu-id="aa39f-222">The following example shows you how you can view recent autoscale and alert events.</span><span class="sxs-lookup"><span data-stu-id="aa39f-222">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="aa39f-223">Use the activity log search to view the autoscale history.</span><span class="sxs-lookup"><span data-stu-id="aa39f-223">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="aa39f-224">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span><span class="sxs-lookup"><span data-stu-id="aa39f-224">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="aa39f-225">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa39f-225">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="aa39f-226">View details for an autoscale setting</span><span class="sxs-lookup"><span data-stu-id="aa39f-226">View details for an autoscale setting</span></span>
<span data-ttu-id="aa39f-227">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="aa39f-227">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="aa39f-228">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="aa39f-228">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="aa39f-229">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span><span class="sxs-lookup"><span data-stu-id="aa39f-229">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="aa39f-230">Remove an autoscale setting</span><span class="sxs-lookup"><span data-stu-id="aa39f-230">Remove an autoscale setting</span></span>
<span data-ttu-id="aa39f-231">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="aa39f-231">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="aa39f-232">Manage log profiles for activity log</span><span class="sxs-lookup"><span data-stu-id="aa39f-232">Manage log profiles for activity log</span></span>
<span data-ttu-id="aa39f-233">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span><span class="sxs-lookup"><span data-stu-id="aa39f-233">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="aa39f-234">Optionally, you can also stream the data to your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="aa39f-234">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="aa39f-235">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span><span class="sxs-lookup"><span data-stu-id="aa39f-235">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="aa39f-236">You can use the following cmdlets with your current subscription to create and manage log profiles.</span><span class="sxs-lookup"><span data-stu-id="aa39f-236">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="aa39f-237">You can also choose a particular subscription.</span><span class="sxs-lookup"><span data-stu-id="aa39f-237">You can also choose a particular subscription.</span></span> <span data-ttu-id="aa39f-238">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="aa39f-238">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="aa39f-239">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span><span class="sxs-lookup"><span data-stu-id="aa39f-239">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="aa39f-240">Data is written as blob files in JSON format.</span><span class="sxs-lookup"><span data-stu-id="aa39f-240">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="aa39f-241">Get a log profile</span><span class="sxs-lookup"><span data-stu-id="aa39f-241">Get a log profile</span></span>
<span data-ttu-id="aa39f-242">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa39f-242">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="aa39f-243">Add a log profile without data retention</span><span class="sxs-lookup"><span data-stu-id="aa39f-243">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="aa39f-244">Remove a log profile</span><span class="sxs-lookup"><span data-stu-id="aa39f-244">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="aa39f-245">Add a log profile with data retention</span><span class="sxs-lookup"><span data-stu-id="aa39f-245">Add a log profile with data retention</span></span>
<span data-ttu-id="aa39f-246">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span><span class="sxs-lookup"><span data-stu-id="aa39f-246">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="aa39f-247">Add log profile with retention and EventHub</span><span class="sxs-lookup"><span data-stu-id="aa39f-247">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="aa39f-248">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span><span class="sxs-lookup"><span data-stu-id="aa39f-248">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="aa39f-249">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span><span class="sxs-lookup"><span data-stu-id="aa39f-249">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="aa39f-250">Configure diagnostics logs</span><span class="sxs-lookup"><span data-stu-id="aa39f-250">Configure diagnostics logs</span></span>
<span data-ttu-id="aa39f-251">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="aa39f-251">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="aa39f-252">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span><span class="sxs-lookup"><span data-stu-id="aa39f-252">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="aa39f-253">Get diagnostic setting</span><span class="sxs-lookup"><span data-stu-id="aa39f-253">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="aa39f-254">Disable diagnostic setting</span><span class="sxs-lookup"><span data-stu-id="aa39f-254">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="aa39f-255">Enable diagnostic setting without retention</span><span class="sxs-lookup"><span data-stu-id="aa39f-255">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="aa39f-256">Enable diagnostic setting with retention</span><span class="sxs-lookup"><span data-stu-id="aa39f-256">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="aa39f-257">Enable diagnostic setting with retention for a specific log category</span><span class="sxs-lookup"><span data-stu-id="aa39f-257">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="aa39f-258">Enable diagnostic setting for Event Hubs</span><span class="sxs-lookup"><span data-stu-id="aa39f-258">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="aa39f-259">Enable diagnostic setting for OMS</span><span class="sxs-lookup"><span data-stu-id="aa39f-259">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
