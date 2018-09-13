---
title: Starting a runbook in Azure Automation | Microsoft Docs
description: Summarizes the different methods that can be used to start a runbook in Azure Automation and provides details on using both the Azure portal and Windows PowerShell.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/08/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 5b932a036f1b6d19abdf9cf079bdb20bdacda88e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556571"
---
# <a name="starting-a-runbook-in-azure-automation"></a><span data-ttu-id="133e2-103">Starting a runbook in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="133e2-103">Starting a runbook in Azure Automation</span></span>
<span data-ttu-id="133e2-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span><span class="sxs-lookup"><span data-stu-id="133e2-104">The following table will help you determine the method to start a runbook in Azure Automation that is most suitable to your particular scenario.</span></span> <span data-ttu-id="133e2-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="133e2-105">This article includes details on starting a runbook with the Azure portal and with Windows PowerShell.</span></span> <span data-ttu-id="133e2-106">Details on the other methods are provided in other documentation that you can access from the links below.</span><span class="sxs-lookup"><span data-stu-id="133e2-106">Details on the other methods are provided in other documentation that you can access from the links below.</span></span>

| <span data-ttu-id="133e2-107">**METHOD**</span><span class="sxs-lookup"><span data-stu-id="133e2-107">**METHOD**</span></span> | <span data-ttu-id="133e2-108">**CHARACTERISTICS**</span><span class="sxs-lookup"><span data-stu-id="133e2-108">**CHARACTERISTICS**</span></span> |
| --- | --- |
| [<span data-ttu-id="133e2-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="133e2-109">Azure Portal</span></span>](#starting-a-runbook-with-the-azure-portal) |<li><span data-ttu-id="133e2-110">Simplest method with interactive user interface.</span><span class="sxs-lookup"><span data-stu-id="133e2-110">Simplest method with interactive user interface.</span></span><br> <li><span data-ttu-id="133e2-111">Form to provide simple parameter values.</span><span class="sxs-lookup"><span data-stu-id="133e2-111">Form to provide simple parameter values.</span></span><br> <li><span data-ttu-id="133e2-112">Easily track job state.</span><span class="sxs-lookup"><span data-stu-id="133e2-112">Easily track job state.</span></span><br> <li><span data-ttu-id="133e2-113">Access authenticated with Azure logon.</span><span class="sxs-lookup"><span data-stu-id="133e2-113">Access authenticated with Azure logon.</span></span> |
| [<span data-ttu-id="133e2-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="133e2-114">Windows PowerShell</span></span>](https://msdn.microsoft.com/library/dn690259.aspx) |<li><span data-ttu-id="133e2-115">Call from command line with Windows PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="133e2-115">Call from command line with Windows PowerShell cmdlets.</span></span><br> <li><span data-ttu-id="133e2-116">Can be included in automated solution with multiple steps.</span><span class="sxs-lookup"><span data-stu-id="133e2-116">Can be included in automated solution with multiple steps.</span></span><br> <li><span data-ttu-id="133e2-117">Request is authenticated with certificate or OAuth user principal / service principal.</span><span class="sxs-lookup"><span data-stu-id="133e2-117">Request is authenticated with certificate or OAuth user principal / service principal.</span></span><br> <li><span data-ttu-id="133e2-118">Provide simple and complex parameter values.</span><span class="sxs-lookup"><span data-stu-id="133e2-118">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="133e2-119">Track job state.</span><span class="sxs-lookup"><span data-stu-id="133e2-119">Track job state.</span></span><br> <li><span data-ttu-id="133e2-120">Client required to support PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="133e2-120">Client required to support PowerShell cmdlets.</span></span> |
| [<span data-ttu-id="133e2-121">Azure Automation API</span><span class="sxs-lookup"><span data-stu-id="133e2-121">Azure Automation API</span></span>](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li><span data-ttu-id="133e2-122">Most flexible method but also most complex.</span><span class="sxs-lookup"><span data-stu-id="133e2-122">Most flexible method but also most complex.</span></span><br> <li><span data-ttu-id="133e2-123">Call from any custom code that can make HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="133e2-123">Call from any custom code that can make HTTP requests.</span></span><br> <li><span data-ttu-id="133e2-124">Request authenticated with certificate, or Oauth user principal / service principal.</span><span class="sxs-lookup"><span data-stu-id="133e2-124">Request authenticated with certificate, or Oauth user principal / service principal.</span></span><br> <li><span data-ttu-id="133e2-125">Provide simple and complex parameter values.</span><span class="sxs-lookup"><span data-stu-id="133e2-125">Provide simple and complex parameter values.</span></span><br> <li><span data-ttu-id="133e2-126">Track job state.</span><span class="sxs-lookup"><span data-stu-id="133e2-126">Track job state.</span></span> |
| [<span data-ttu-id="133e2-127">Webhooks</span><span class="sxs-lookup"><span data-stu-id="133e2-127">Webhooks</span></span>](automation-webhooks.md) |<li><span data-ttu-id="133e2-128">Start runbook from single HTTP request.</span><span class="sxs-lookup"><span data-stu-id="133e2-128">Start runbook from single HTTP request.</span></span><br> <li><span data-ttu-id="133e2-129">Authenticated with security token in URL.</span><span class="sxs-lookup"><span data-stu-id="133e2-129">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="133e2-130">Client cannot override parameter values specified when webhook created.</span><span class="sxs-lookup"><span data-stu-id="133e2-130">Client cannot override parameter values specified when webhook created.</span></span> <span data-ttu-id="133e2-131">Runbook can define single parameter that is populated with the HTTP request details.</span><span class="sxs-lookup"><span data-stu-id="133e2-131">Runbook can define single parameter that is populated with the HTTP request details.</span></span><br> <li><span data-ttu-id="133e2-132">No ability to track job state through webhook URL.</span><span class="sxs-lookup"><span data-stu-id="133e2-132">No ability to track job state through webhook URL.</span></span> |
| [<span data-ttu-id="133e2-133">Respond to Azure Alert</span><span class="sxs-lookup"><span data-stu-id="133e2-133">Respond to Azure Alert</span></span>](../log-analytics/log-analytics-alerts.md) |<li><span data-ttu-id="133e2-134">Start a runbook in response to Azure alert.</span><span class="sxs-lookup"><span data-stu-id="133e2-134">Start a runbook in response to Azure alert.</span></span><br> <li><span data-ttu-id="133e2-135">Configure webhook for runbook and link to alert.</span><span class="sxs-lookup"><span data-stu-id="133e2-135">Configure webhook for runbook and link to alert.</span></span><br> <li><span data-ttu-id="133e2-136">Authenticated with security token in URL.</span><span class="sxs-lookup"><span data-stu-id="133e2-136">Authenticated with security token in URL.</span></span><br> <li><span data-ttu-id="133e2-137">Currently supports alert on Metrics only.</span><span class="sxs-lookup"><span data-stu-id="133e2-137">Currently supports alert on Metrics only.</span></span> |
| [<span data-ttu-id="133e2-138">Schedule</span><span class="sxs-lookup"><span data-stu-id="133e2-138">Schedule</span></span>](automation-schedules.md) |<li><span data-ttu-id="133e2-139">Automatically start runbook on hourly, daily, or weekly schedule.</span><span class="sxs-lookup"><span data-stu-id="133e2-139">Automatically start runbook on hourly, daily, or weekly schedule.</span></span><br> <li><span data-ttu-id="133e2-140">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span><span class="sxs-lookup"><span data-stu-id="133e2-140">Manipulate schedule through Azure portal, PowerShell cmdlets, or Azure API.</span></span><br> <li><span data-ttu-id="133e2-141">Provide parameter values to be used with schedule.</span><span class="sxs-lookup"><span data-stu-id="133e2-141">Provide parameter values to be used with schedule.</span></span> |
| [<span data-ttu-id="133e2-142">From Another Runbook</span><span class="sxs-lookup"><span data-stu-id="133e2-142">From Another Runbook</span></span>](automation-child-runbooks.md) |<li><span data-ttu-id="133e2-143">Use a runbook as an activity in another runbook.</span><span class="sxs-lookup"><span data-stu-id="133e2-143">Use a runbook as an activity in another runbook.</span></span><br> <li><span data-ttu-id="133e2-144">Useful for functionality used by multiple runbooks.</span><span class="sxs-lookup"><span data-stu-id="133e2-144">Useful for functionality used by multiple runbooks.</span></span><br> <li><span data-ttu-id="133e2-145">Provide parameter values to child runbook and use output in parent runbook.</span><span class="sxs-lookup"><span data-stu-id="133e2-145">Provide parameter values to child runbook and use output in parent runbook.</span></span> |

<span data-ttu-id="133e2-146">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span><span class="sxs-lookup"><span data-stu-id="133e2-146">The following image illustrates detailed step-by-step process in the life cycle of a runbook.</span></span> <span data-ttu-id="133e2-147">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span><span class="sxs-lookup"><span data-stu-id="133e2-147">It includes different ways a runbook is started in Azure Automation, components required for Hybrid Runbook Worker to execute Azure Automation runbooks and interactions between different components.</span></span> <span data-ttu-id="133e2-148">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span><span class="sxs-lookup"><span data-stu-id="133e2-148">To learn about executing Automation runbooks in your datacenter, refer to [hybrid runbook workers](automation-hybrid-runbook-worker.md)</span></span>

![Runbook Architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="133e2-150">Starting a runbook with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="133e2-150">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="133e2-151">In the Azure portal, select **Automation** and then then click the name of an automation account.</span><span class="sxs-lookup"><span data-stu-id="133e2-151">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="133e2-152">Select the **Runbooks** tab.</span><span class="sxs-lookup"><span data-stu-id="133e2-152">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="133e2-153">Select a runbook, and then click **Start**.</span><span class="sxs-lookup"><span data-stu-id="133e2-153">Select a runbook, and then click **Start**.</span></span>
4. <span data-ttu-id="133e2-154">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span><span class="sxs-lookup"><span data-stu-id="133e2-154">If the runbook has parameters, you will be prompted to provide values with a text box for each parameter.</span></span> <span data-ttu-id="133e2-155">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span><span class="sxs-lookup"><span data-stu-id="133e2-155">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="133e2-156">Either select **View Job** next to the **Starting** runbook message or select the **Jobs** tab for the runbook to view the runbook job’s status.</span><span class="sxs-lookup"><span data-stu-id="133e2-156">Either select **View Job** next to the **Starting** runbook message or select the **Jobs** tab for the runbook to view the runbook job’s status.</span></span>

## <a name="starting-a-runbook-with-the-azure-portal"></a><span data-ttu-id="133e2-157">Starting a runbook with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="133e2-157">Starting a runbook with the Azure portal</span></span>
1. <span data-ttu-id="133e2-158">From your automation account, click the **Runbooks** part to open the **Runbooks** blade.</span><span class="sxs-lookup"><span data-stu-id="133e2-158">From your automation account, click the **Runbooks** part to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="133e2-159">Click a runbook to open its **Runbook** blade.</span><span class="sxs-lookup"><span data-stu-id="133e2-159">Click a runbook to open its **Runbook** blade.</span></span>
3. <span data-ttu-id="133e2-160">Click **Start**.</span><span class="sxs-lookup"><span data-stu-id="133e2-160">Click **Start**.</span></span>
4. <span data-ttu-id="133e2-161">If the runbook has no parameters, you will be prompted to confirm whether you want to start it.</span><span class="sxs-lookup"><span data-stu-id="133e2-161">If the runbook has no parameters, you will be prompted to confirm whether you want to start it.</span></span> <span data-ttu-id="133e2-162">If the runbook has parameters, the **Start Runbook** blade will be opened so you can provide parameter values.</span><span class="sxs-lookup"><span data-stu-id="133e2-162">If the runbook has parameters, the **Start Runbook** blade will be opened so you can provide parameter values.</span></span> <span data-ttu-id="133e2-163">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span><span class="sxs-lookup"><span data-stu-id="133e2-163">See [Runbook Parameters](#Runbook-parameters) below for further details on parameters.</span></span>
5. <span data-ttu-id="133e2-164">The **Job** blade is opened so that you can track the job's status.</span><span class="sxs-lookup"><span data-stu-id="133e2-164">The **Job** blade is opened so that you can track the job's status.</span></span>

## <a name="starting-a-runbook-with-windows-powershell"></a><span data-ttu-id="133e2-165">Starting a runbook with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="133e2-165">Starting a runbook with Windows PowerShell</span></span>
<span data-ttu-id="133e2-166">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="133e2-166">You can use the [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a runbook with Windows PowerShell.</span></span> <span data-ttu-id="133e2-167">The following sample code starts a runbook called Test-Runbook.</span><span class="sxs-lookup"><span data-stu-id="133e2-167">The following sample code starts a runbook called Test-Runbook.</span></span>

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

<span data-ttu-id="133e2-168">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span><span class="sxs-lookup"><span data-stu-id="133e2-168">Start-AzureRmAutomationRunbook returns a job object that you can use to track its status once the runbook is started.</span></span> <span data-ttu-id="133e2-169">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span><span class="sxs-lookup"><span data-stu-id="133e2-169">You can then use this job object with [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) to determine the status of the job and [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) to get its output.</span></span> <span data-ttu-id="133e2-170">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span><span class="sxs-lookup"><span data-stu-id="133e2-170">The following sample code starts a runbook called Test-Runbook, waits until it has completed, and then displays its output.</span></span>

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

<span data-ttu-id="133e2-171">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span><span class="sxs-lookup"><span data-stu-id="133e2-171">If the runbook requires parameters, then you must provide them as a [hashtable](http://technet.microsoft.com/library/hh847780.aspx) where the key of the hashtable matches the parameter name and the value is the parameter value.</span></span> <span data-ttu-id="133e2-172">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span><span class="sxs-lookup"><span data-stu-id="133e2-172">The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show.</span></span> <span data-ttu-id="133e2-173">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span><span class="sxs-lookup"><span data-stu-id="133e2-173">For additional information on parameters, see [Runbook Parameters](#Runbook-parameters) below.</span></span>

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a><span data-ttu-id="133e2-174">Runbook parameters</span><span class="sxs-lookup"><span data-stu-id="133e2-174">Runbook parameters</span></span>
<span data-ttu-id="133e2-175">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span><span class="sxs-lookup"><span data-stu-id="133e2-175">When you start a runbook from the Azure Portal or Windows PowerShell, the instruction is sent through the Azure Automation web service.</span></span> <span data-ttu-id="133e2-176">This service does not support parameters with complex data types.</span><span class="sxs-lookup"><span data-stu-id="133e2-176">This service does not support parameters with complex data types.</span></span> <span data-ttu-id="133e2-177">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="133e2-177">If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child runbooks in Azure Automation](automation-child-runbooks.md).</span></span>

<span data-ttu-id="133e2-178">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="133e2-178">The Azure Automation web service will provide special functionality for parameters using certain data types as described in the following sections.</span></span>

### <a name="named-values"></a><span data-ttu-id="133e2-179">Named values</span><span class="sxs-lookup"><span data-stu-id="133e2-179">Named values</span></span>
<span data-ttu-id="133e2-180">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span><span class="sxs-lookup"><span data-stu-id="133e2-180">If the parameter is data type [object], then you can use the following JSON format to send it a list of named values: *{Name1:'Value1', Name2:'Value2', Name3:'Value3'}*.</span></span> <span data-ttu-id="133e2-181">These values must be simple types.</span><span class="sxs-lookup"><span data-stu-id="133e2-181">These values must be simple types.</span></span> <span data-ttu-id="133e2-182">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span><span class="sxs-lookup"><span data-stu-id="133e2-182">The runbook will receive the parameter as a [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) with properties that correspond to each named value.</span></span>

<span data-ttu-id="133e2-183">Consider the following test runbook that accepts a parameter called user.</span><span class="sxs-lookup"><span data-stu-id="133e2-183">Consider the following test runbook that accepts a parameter called user.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

<span data-ttu-id="133e2-184">The following text could be used for the user parameter.</span><span class="sxs-lookup"><span data-stu-id="133e2-184">The following text could be used for the user parameter.</span></span>

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

<span data-ttu-id="133e2-185">This results in the following output.</span><span class="sxs-lookup"><span data-stu-id="133e2-185">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a><span data-ttu-id="133e2-186">Arrays</span><span class="sxs-lookup"><span data-stu-id="133e2-186">Arrays</span></span>
<span data-ttu-id="133e2-187">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span><span class="sxs-lookup"><span data-stu-id="133e2-187">If the parameter is an array such as [array] or [string[]], then you can use the following JSON format to send it a list of values: *[Value1,Value2,Value3]*.</span></span> <span data-ttu-id="133e2-188">These values must be simple types.</span><span class="sxs-lookup"><span data-stu-id="133e2-188">These values must be simple types.</span></span>

<span data-ttu-id="133e2-189">Consider the following test runbook that accepts a parameter called *user*.</span><span class="sxs-lookup"><span data-stu-id="133e2-189">Consider the following test runbook that accepts a parameter called *user*.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

<span data-ttu-id="133e2-190">The following text could be used for the user parameter.</span><span class="sxs-lookup"><span data-stu-id="133e2-190">The following text could be used for the user parameter.</span></span>

```
["Joe","Smith",2,true]
```

<span data-ttu-id="133e2-191">This results in the following output.</span><span class="sxs-lookup"><span data-stu-id="133e2-191">This results in the following output.</span></span>

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a><span data-ttu-id="133e2-192">Credentials</span><span class="sxs-lookup"><span data-stu-id="133e2-192">Credentials</span></span>
<span data-ttu-id="133e2-193">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="133e2-193">If the parameter is data type **PSCredential**, then you can provide the name of an Azure Automation [credential asset](automation-credentials.md).</span></span> <span data-ttu-id="133e2-194">The runbook will retrieve the credential with the name that you specify.</span><span class="sxs-lookup"><span data-stu-id="133e2-194">The runbook will retrieve the credential with the name that you specify.</span></span>

<span data-ttu-id="133e2-195">Consider the following test runbook that accepts a parameter called credential.</span><span class="sxs-lookup"><span data-stu-id="133e2-195">Consider the following test runbook that accepts a parameter called credential.</span></span>

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

<span data-ttu-id="133e2-196">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span><span class="sxs-lookup"><span data-stu-id="133e2-196">The following text could be used for the user parameter assuming that there was a credential asset called *My Credential*.</span></span>

```
My Credential
```

<span data-ttu-id="133e2-197">Assuming the username in the credential was *jsmith*, this results in the following output.</span><span class="sxs-lookup"><span data-stu-id="133e2-197">Assuming the username in the credential was *jsmith*, this results in the following output.</span></span>

```
jsmith
```

## <a name="next-steps"></a><span data-ttu-id="133e2-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="133e2-198">Next steps</span></span>
* <span data-ttu-id="133e2-199">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premise with the Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="133e2-199">The runbook architecture in current article provides a high-level overview of runbooks managing resources in Azure and on-premise with the Hybrid Runbook Worker.</span></span>  <span data-ttu-id="133e2-200">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span><span class="sxs-lookup"><span data-stu-id="133e2-200">To learn about executing Automation runbooks in your datacenter, refer to [Hybrid Runbook Workers](automation-hybrid-runbook-worker.md).</span></span>
* <span data-ttu-id="133e2-201">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="133e2-201">To learn more about the creating modular runbooks to be used by other runbooks for specific or common functions, refer to [Child Runbooks](automation-child-runbooks.md).</span></span>


