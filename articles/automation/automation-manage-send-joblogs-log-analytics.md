---
title: Forward Azure Automation job data to OMS Log Analytics | Microsoft Docs
description: This article demonstrates how to send job status and runbook job streams to Microsoft Operations Management Suite Log Analytics to deliver additional insight and management.
services: automation
documentationcenter: ''
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/03/2017
ms.author: magoedte
ms.openlocfilehash: 969fdd46053c066213ecca31819c2082d2cba824
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552795"
---
# <a name="forward-job-status-and-job-streams-from-automation-to-log-analytics-oms"></a><span data-ttu-id="06fc6-103">Forward job status and job streams from Automation to Log Analytics (OMS)</span><span class="sxs-lookup"><span data-stu-id="06fc6-103">Forward job status and job streams from Automation to Log Analytics (OMS)</span></span>
<span data-ttu-id="06fc6-104">Automation can send runbook job status and job streams to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="06fc6-104">Automation can send runbook job status and job streams to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>  <span data-ttu-id="06fc6-105">Job logs and job streams are visible in the Azure portal, or with PowerShell, for individual jobs and this allows you to perform simple investigations.</span><span class="sxs-lookup"><span data-stu-id="06fc6-105">Job logs and job streams are visible in the Azure portal, or with PowerShell, for individual jobs and this allows you to perform simple investigations.</span></span> <span data-ttu-id="06fc6-106">Now with Log Analytics you can:</span><span class="sxs-lookup"><span data-stu-id="06fc6-106">Now with Log Analytics you can:</span></span>

* <span data-ttu-id="06fc6-107">Get insight on your Automation jobs</span><span class="sxs-lookup"><span data-stu-id="06fc6-107">Get insight on your Automation jobs</span></span>
* <span data-ttu-id="06fc6-108">Trigger an email or alert based on your runbook job status (for example, failed or suspended)</span><span class="sxs-lookup"><span data-stu-id="06fc6-108">Trigger an email or alert based on your runbook job status (for example, failed or suspended)</span></span>
* <span data-ttu-id="06fc6-109">Write advanced queries across your job streams</span><span class="sxs-lookup"><span data-stu-id="06fc6-109">Write advanced queries across your job streams</span></span>
* <span data-ttu-id="06fc6-110">Correlate jobs across Automation accounts</span><span class="sxs-lookup"><span data-stu-id="06fc6-110">Correlate jobs across Automation accounts</span></span>
* <span data-ttu-id="06fc6-111">Visualize your job history over time</span><span class="sxs-lookup"><span data-stu-id="06fc6-111">Visualize your job history over time</span></span>     

## <a name="prerequisites-and-deployment-considerations"></a><span data-ttu-id="06fc6-112">Prerequisites and deployment considerations</span><span class="sxs-lookup"><span data-stu-id="06fc6-112">Prerequisites and deployment considerations</span></span>
<span data-ttu-id="06fc6-113">To start sending your Automation logs to Log Analytics, you need:</span><span class="sxs-lookup"><span data-stu-id="06fc6-113">To start sending your Automation logs to Log Analytics, you need:</span></span>

1. <span data-ttu-id="06fc6-114">The November 2016 or later release of [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span><span class="sxs-lookup"><span data-stu-id="06fc6-114">The November 2016 or later release of [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).</span></span>
2. <span data-ttu-id="06fc6-115">A Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="06fc6-115">A Log Analytics workspace.</span></span> <span data-ttu-id="06fc6-116">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="06fc6-116">For more information, see [Get started with Log Analytics](../log-analytics/log-analytics-get-started.md).</span></span>
3. <span data-ttu-id="06fc6-117">The ResourceId for your Azure Automation account</span><span class="sxs-lookup"><span data-stu-id="06fc6-117">The ResourceId for your Azure Automation account</span></span>

<span data-ttu-id="06fc6-118">To find the ResourceId for your Azure Automation account and Log Analytics workspace, run the following PowerShell:</span><span class="sxs-lookup"><span data-stu-id="06fc6-118">To find the ResourceId for your Azure Automation account and Log Analytics workspace, run the following PowerShell:</span></span>

```powershell
# Find the ResourceId for the Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find the ResourceId for the Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

<span data-ttu-id="06fc6-119">If you have multiple Automation accounts, or workspaces, in the output of the preceding commands, find the *Name* you need to configure and copy the value for *ResourceId*.</span><span class="sxs-lookup"><span data-stu-id="06fc6-119">If you have multiple Automation accounts, or workspaces, in the output of the preceding commands, find the *Name* you need to configure and copy the value for *ResourceId*.</span></span>

<span data-ttu-id="06fc6-120">If you need to find the *Name* of your Automation account, in the Azure portal select your Automation account from the **Automation account** blade and select **All settings**.</span><span class="sxs-lookup"><span data-stu-id="06fc6-120">If you need to find the *Name* of your Automation account, in the Azure portal select your Automation account from the **Automation account** blade and select **All settings**.</span></span>  <span data-ttu-id="06fc6-121">From the **All settings** blade, under **Account Settings** select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="06fc6-121">From the **All settings** blade, under **Account Settings** select **Properties**.</span></span>  <span data-ttu-id="06fc6-122">In the **Properties** blade, you can note these values.</span><span class="sxs-lookup"><span data-stu-id="06fc6-122">In the **Properties** blade, you can note these values.</span></span><br> <span data-ttu-id="06fc6-123">![Automation Account properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span><span class="sxs-lookup"><span data-stu-id="06fc6-123">![Automation Account properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).</span></span>

## <a name="set-up-integration-with-log-analytics"></a><span data-ttu-id="06fc6-124">Set up integration with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="06fc6-124">Set up integration with Log Analytics</span></span>
1. <span data-ttu-id="06fc6-125">On your computer, start **Windows PowerShell** from the **Start** screen.</span><span class="sxs-lookup"><span data-stu-id="06fc6-125">On your computer, start **Windows PowerShell** from the **Start** screen.</span></span>  
2. <span data-ttu-id="06fc6-126">Copy and paste the following PowerShell, and edit the value for the `$workspaceId` and `$automationAccountId`.</span><span class="sxs-lookup"><span data-stu-id="06fc6-126">Copy and paste the following PowerShell, and edit the value for the `$workspaceId` and `$automationAccountId`.</span></span>  <span data-ttu-id="06fc6-127">For the `-Environment` parameter, valid values are *AzureCloud* or *AzureUSGovernment* depending on the cloud environment you are working in.</span><span class="sxs-lookup"><span data-stu-id="06fc6-127">For the `-Environment` parameter, valid values are *AzureCloud* or *AzureUSGovernment* depending on the cloud environment you are working in.</span></span>     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check to see which cloud environment to sign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment}
   }

# if you have one Log Analytics workspace you can use the following command to get the resource id of the workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

<span data-ttu-id="06fc6-128">After running this script, you will see records in Log Analytics within 10 minutes of new JobLogs or JobStreams being written.</span><span class="sxs-lookup"><span data-stu-id="06fc6-128">After running this script, you will see records in Log Analytics within 10 minutes of new JobLogs or JobStreams being written.</span></span>

<span data-ttu-id="06fc6-129">To see the logs, run the following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="06fc6-129">To see the logs, run the following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="verify-configuration"></a><span data-ttu-id="06fc6-130">Verify configuration</span><span class="sxs-lookup"><span data-stu-id="06fc6-130">Verify configuration</span></span>
<span data-ttu-id="06fc6-131">To confirm that your Automation account is sending logs to your Log Analytics workspace, check that diagnostics are set correctly on the Automation account using the following PowerShell:</span><span class="sxs-lookup"><span data-stu-id="06fc6-131">To confirm that your Automation account is sending logs to your Log Analytics workspace, check that diagnostics are set correctly on the Automation account using the following PowerShell:</span></span>

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check to see which cloud environment to sign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment}
   }
# if you have one Log Analytics workspace you can use the following command to get the resource id of the workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO"

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

<span data-ttu-id="06fc6-132">In the output ensure that:</span><span class="sxs-lookup"><span data-stu-id="06fc6-132">In the output ensure that:</span></span>
+ <span data-ttu-id="06fc6-133">Under *Logs*, the value for *Enabled* is *True*</span><span class="sxs-lookup"><span data-stu-id="06fc6-133">Under *Logs*, the value for *Enabled* is *True*</span></span>
+ <span data-ttu-id="06fc6-134">The value of *WorkspaceId* is set to the ResourceId of your Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="06fc6-134">The value of *WorkspaceId* is set to the ResourceId of your Log Analytics workspace</span></span>


## <a name="log-analytics-records"></a><span data-ttu-id="06fc6-135">Log Analytics records</span><span class="sxs-lookup"><span data-stu-id="06fc6-135">Log Analytics records</span></span>
<span data-ttu-id="06fc6-136">Diagnostics from Azure Automation creates two types of records in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="06fc6-136">Diagnostics from Azure Automation creates two types of records in Log Analytics.</span></span>

### <a name="job-logs"></a><span data-ttu-id="06fc6-137">Job Logs</span><span class="sxs-lookup"><span data-stu-id="06fc6-137">Job Logs</span></span>
| <span data-ttu-id="06fc6-138">Property</span><span class="sxs-lookup"><span data-stu-id="06fc6-138">Property</span></span> | <span data-ttu-id="06fc6-139">Description</span><span class="sxs-lookup"><span data-stu-id="06fc6-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06fc6-140">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="06fc6-140">TimeGenerated</span></span> |<span data-ttu-id="06fc6-141">Date and time when the runbook job executed.</span><span class="sxs-lookup"><span data-stu-id="06fc6-141">Date and time when the runbook job executed.</span></span> |
| <span data-ttu-id="06fc6-142">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="06fc6-142">RunbookName_s</span></span> |<span data-ttu-id="06fc6-143">The name of the runbook.</span><span class="sxs-lookup"><span data-stu-id="06fc6-143">The name of the runbook.</span></span> |
| <span data-ttu-id="06fc6-144">Caller_s</span><span class="sxs-lookup"><span data-stu-id="06fc6-144">Caller_s</span></span> |<span data-ttu-id="06fc6-145">Who initiated the operation.</span><span class="sxs-lookup"><span data-stu-id="06fc6-145">Who initiated the operation.</span></span>  <span data-ttu-id="06fc6-146">Possible values are either an email address or system for scheduled jobs.</span><span class="sxs-lookup"><span data-stu-id="06fc6-146">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="06fc6-147">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="06fc6-147">Tenant_g</span></span> | <span data-ttu-id="06fc6-148">GUID that identifies the tenant for the Caller.</span><span class="sxs-lookup"><span data-stu-id="06fc6-148">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="06fc6-149">JobId_g</span><span class="sxs-lookup"><span data-stu-id="06fc6-149">JobId_g</span></span> |<span data-ttu-id="06fc6-150">GUID that is the Id of the runbook job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-150">GUID that is the Id of the runbook job.</span></span> |
| <span data-ttu-id="06fc6-151">ResultType</span><span class="sxs-lookup"><span data-stu-id="06fc6-151">ResultType</span></span> |<span data-ttu-id="06fc6-152">The status of the runbook job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-152">The status of the runbook job.</span></span>  <span data-ttu-id="06fc6-153">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="06fc6-153">Possible values are:</span></span><br><span data-ttu-id="06fc6-154">- Started</span><span class="sxs-lookup"><span data-stu-id="06fc6-154">- Started</span></span><br><span data-ttu-id="06fc6-155">- Stopped</span><span class="sxs-lookup"><span data-stu-id="06fc6-155">- Stopped</span></span><br><span data-ttu-id="06fc6-156">- Suspended</span><span class="sxs-lookup"><span data-stu-id="06fc6-156">- Suspended</span></span><br><span data-ttu-id="06fc6-157">- Failed</span><span class="sxs-lookup"><span data-stu-id="06fc6-157">- Failed</span></span><br><span data-ttu-id="06fc6-158">- Completed</span><span class="sxs-lookup"><span data-stu-id="06fc6-158">- Completed</span></span> |
| <span data-ttu-id="06fc6-159">Category</span><span class="sxs-lookup"><span data-stu-id="06fc6-159">Category</span></span> | <span data-ttu-id="06fc6-160">Classification of the type of data.</span><span class="sxs-lookup"><span data-stu-id="06fc6-160">Classification of the type of data.</span></span>  <span data-ttu-id="06fc6-161">For Automation, the value is JobLogs.</span><span class="sxs-lookup"><span data-stu-id="06fc6-161">For Automation, the value is JobLogs.</span></span> |
| <span data-ttu-id="06fc6-162">OperationName</span><span class="sxs-lookup"><span data-stu-id="06fc6-162">OperationName</span></span> | <span data-ttu-id="06fc6-163">Specifies the type of operation performed in Azure.</span><span class="sxs-lookup"><span data-stu-id="06fc6-163">Specifies the type of operation performed in Azure.</span></span>  <span data-ttu-id="06fc6-164">For Automation, the value is Job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-164">For Automation, the value is Job.</span></span> |
| <span data-ttu-id="06fc6-165">Resource</span><span class="sxs-lookup"><span data-stu-id="06fc6-165">Resource</span></span> | <span data-ttu-id="06fc6-166">Name of the Automation account</span><span class="sxs-lookup"><span data-stu-id="06fc6-166">Name of the Automation account</span></span> |
| <span data-ttu-id="06fc6-167">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="06fc6-167">SourceSystem</span></span> | <span data-ttu-id="06fc6-168">How Log Analytics collected the data.</span><span class="sxs-lookup"><span data-stu-id="06fc6-168">How Log Analytics collected the data.</span></span> <span data-ttu-id="06fc6-169">Always *Azure* for Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="06fc6-169">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="06fc6-170">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="06fc6-170">ResultDescription</span></span> |<span data-ttu-id="06fc6-171">Describes the runbook job result state.</span><span class="sxs-lookup"><span data-stu-id="06fc6-171">Describes the runbook job result state.</span></span>  <span data-ttu-id="06fc6-172">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="06fc6-172">Possible values are:</span></span><br><span data-ttu-id="06fc6-173">- Job is started</span><span class="sxs-lookup"><span data-stu-id="06fc6-173">- Job is started</span></span><br><span data-ttu-id="06fc6-174">- Job Failed</span><span class="sxs-lookup"><span data-stu-id="06fc6-174">- Job Failed</span></span><br><span data-ttu-id="06fc6-175">- Job Completed</span><span class="sxs-lookup"><span data-stu-id="06fc6-175">- Job Completed</span></span> |
| <span data-ttu-id="06fc6-176">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="06fc6-176">CorrelationId</span></span> |<span data-ttu-id="06fc6-177">GUID that is the Correlation Id of the runbook job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-177">GUID that is the Correlation Id of the runbook job.</span></span> |
| <span data-ttu-id="06fc6-178">ResourceId</span><span class="sxs-lookup"><span data-stu-id="06fc6-178">ResourceId</span></span> |<span data-ttu-id="06fc6-179">Specifies the Azure Automation account resource id of the runbook.</span><span class="sxs-lookup"><span data-stu-id="06fc6-179">Specifies the Azure Automation account resource id of the runbook.</span></span> |
| <span data-ttu-id="06fc6-180">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="06fc6-180">SubscriptionId</span></span> | <span data-ttu-id="06fc6-181">The Azure subscription Id (GUID) for the Automation account.</span><span class="sxs-lookup"><span data-stu-id="06fc6-181">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="06fc6-182">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06fc6-182">ResourceGroup</span></span> | <span data-ttu-id="06fc6-183">Name of the resource group for the Automation account.</span><span class="sxs-lookup"><span data-stu-id="06fc6-183">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="06fc6-184">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="06fc6-184">ResourceProvider</span></span> | <span data-ttu-id="06fc6-185">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="06fc6-185">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="06fc6-186">ResourceType</span><span class="sxs-lookup"><span data-stu-id="06fc6-186">ResourceType</span></span> | <span data-ttu-id="06fc6-187">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="06fc6-187">AUTOMATIONACCOUNTS</span></span> |


### <a name="job-streams"></a><span data-ttu-id="06fc6-188">Job Streams</span><span class="sxs-lookup"><span data-stu-id="06fc6-188">Job Streams</span></span>
| <span data-ttu-id="06fc6-189">Property</span><span class="sxs-lookup"><span data-stu-id="06fc6-189">Property</span></span> | <span data-ttu-id="06fc6-190">Description</span><span class="sxs-lookup"><span data-stu-id="06fc6-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06fc6-191">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="06fc6-191">TimeGenerated</span></span> |<span data-ttu-id="06fc6-192">Date and time when the runbook job executed.</span><span class="sxs-lookup"><span data-stu-id="06fc6-192">Date and time when the runbook job executed.</span></span> |
| <span data-ttu-id="06fc6-193">RunbookName_s</span><span class="sxs-lookup"><span data-stu-id="06fc6-193">RunbookName_s</span></span> |<span data-ttu-id="06fc6-194">The name of the runbook.</span><span class="sxs-lookup"><span data-stu-id="06fc6-194">The name of the runbook.</span></span> |
| <span data-ttu-id="06fc6-195">Caller_s</span><span class="sxs-lookup"><span data-stu-id="06fc6-195">Caller_s</span></span> |<span data-ttu-id="06fc6-196">Who initiated the operation.</span><span class="sxs-lookup"><span data-stu-id="06fc6-196">Who initiated the operation.</span></span>  <span data-ttu-id="06fc6-197">Possible values are either an email address or system for scheduled jobs.</span><span class="sxs-lookup"><span data-stu-id="06fc6-197">Possible values are either an email address or system for scheduled jobs.</span></span> |
| <span data-ttu-id="06fc6-198">StreamType_s</span><span class="sxs-lookup"><span data-stu-id="06fc6-198">StreamType_s</span></span> |<span data-ttu-id="06fc6-199">The type of job stream.</span><span class="sxs-lookup"><span data-stu-id="06fc6-199">The type of job stream.</span></span> <span data-ttu-id="06fc6-200">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="06fc6-200">Possible values are:</span></span><br><span data-ttu-id="06fc6-201">-Progress</span><span class="sxs-lookup"><span data-stu-id="06fc6-201">-Progress</span></span><br><span data-ttu-id="06fc6-202">- Output</span><span class="sxs-lookup"><span data-stu-id="06fc6-202">- Output</span></span><br><span data-ttu-id="06fc6-203">- Warning</span><span class="sxs-lookup"><span data-stu-id="06fc6-203">- Warning</span></span><br><span data-ttu-id="06fc6-204">- Error</span><span class="sxs-lookup"><span data-stu-id="06fc6-204">- Error</span></span><br><span data-ttu-id="06fc6-205">- Debug</span><span class="sxs-lookup"><span data-stu-id="06fc6-205">- Debug</span></span><br><span data-ttu-id="06fc6-206">- Verbose</span><span class="sxs-lookup"><span data-stu-id="06fc6-206">- Verbose</span></span> |
| <span data-ttu-id="06fc6-207">Tenant_g</span><span class="sxs-lookup"><span data-stu-id="06fc6-207">Tenant_g</span></span> | <span data-ttu-id="06fc6-208">GUID that identifies the tenant for the Caller.</span><span class="sxs-lookup"><span data-stu-id="06fc6-208">GUID that identifies the tenant for the Caller.</span></span> |
| <span data-ttu-id="06fc6-209">JobId_g</span><span class="sxs-lookup"><span data-stu-id="06fc6-209">JobId_g</span></span> |<span data-ttu-id="06fc6-210">GUID that is the Id of the runbook job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-210">GUID that is the Id of the runbook job.</span></span> |
| <span data-ttu-id="06fc6-211">ResultType</span><span class="sxs-lookup"><span data-stu-id="06fc6-211">ResultType</span></span> |<span data-ttu-id="06fc6-212">The status of the runbook job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-212">The status of the runbook job.</span></span>  <span data-ttu-id="06fc6-213">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="06fc6-213">Possible values are:</span></span><br><span data-ttu-id="06fc6-214">- In Progress</span><span class="sxs-lookup"><span data-stu-id="06fc6-214">- In Progress</span></span> |
| <span data-ttu-id="06fc6-215">Category</span><span class="sxs-lookup"><span data-stu-id="06fc6-215">Category</span></span> | <span data-ttu-id="06fc6-216">Classification of the type of data.</span><span class="sxs-lookup"><span data-stu-id="06fc6-216">Classification of the type of data.</span></span>  <span data-ttu-id="06fc6-217">For Automation, the value is JobStreams.</span><span class="sxs-lookup"><span data-stu-id="06fc6-217">For Automation, the value is JobStreams.</span></span> |
| <span data-ttu-id="06fc6-218">OperationName</span><span class="sxs-lookup"><span data-stu-id="06fc6-218">OperationName</span></span> | <span data-ttu-id="06fc6-219">Specifies the type of operation performed in Azure.</span><span class="sxs-lookup"><span data-stu-id="06fc6-219">Specifies the type of operation performed in Azure.</span></span>  <span data-ttu-id="06fc6-220">For Automation, the value is Job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-220">For Automation, the value is Job.</span></span> |
| <span data-ttu-id="06fc6-221">Resource</span><span class="sxs-lookup"><span data-stu-id="06fc6-221">Resource</span></span> | <span data-ttu-id="06fc6-222">Name of the Automation account</span><span class="sxs-lookup"><span data-stu-id="06fc6-222">Name of the Automation account</span></span> |
| <span data-ttu-id="06fc6-223">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="06fc6-223">SourceSystem</span></span> | <span data-ttu-id="06fc6-224">How Log Analytics collected the data.</span><span class="sxs-lookup"><span data-stu-id="06fc6-224">How Log Analytics collected the data.</span></span> <span data-ttu-id="06fc6-225">Always *Azure* for Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="06fc6-225">Always *Azure* for Azure diagnostics.</span></span> |
| <span data-ttu-id="06fc6-226">ResultDescription</span><span class="sxs-lookup"><span data-stu-id="06fc6-226">ResultDescription</span></span> |<span data-ttu-id="06fc6-227">Includes the output stream from the runbook.</span><span class="sxs-lookup"><span data-stu-id="06fc6-227">Includes the output stream from the runbook.</span></span> |
| <span data-ttu-id="06fc6-228">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="06fc6-228">CorrelationId</span></span> |<span data-ttu-id="06fc6-229">GUID that is the Correlation Id of the runbook job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-229">GUID that is the Correlation Id of the runbook job.</span></span> |
| <span data-ttu-id="06fc6-230">ResourceId</span><span class="sxs-lookup"><span data-stu-id="06fc6-230">ResourceId</span></span> |<span data-ttu-id="06fc6-231">Specifies the Azure Automation account resource id of the runbook.</span><span class="sxs-lookup"><span data-stu-id="06fc6-231">Specifies the Azure Automation account resource id of the runbook.</span></span> |
| <span data-ttu-id="06fc6-232">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="06fc6-232">SubscriptionId</span></span> | <span data-ttu-id="06fc6-233">The Azure subscription Id (GUID) for the Automation account.</span><span class="sxs-lookup"><span data-stu-id="06fc6-233">The Azure subscription Id (GUID) for the Automation account.</span></span> |
| <span data-ttu-id="06fc6-234">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06fc6-234">ResourceGroup</span></span> | <span data-ttu-id="06fc6-235">Name of the resource group for the Automation account.</span><span class="sxs-lookup"><span data-stu-id="06fc6-235">Name of the resource group for the Automation account.</span></span> |
| <span data-ttu-id="06fc6-236">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="06fc6-236">ResourceProvider</span></span> | <span data-ttu-id="06fc6-237">MICROSOFT.AUTOMATION</span><span class="sxs-lookup"><span data-stu-id="06fc6-237">MICROSOFT.AUTOMATION</span></span> |
| <span data-ttu-id="06fc6-238">ResourceType</span><span class="sxs-lookup"><span data-stu-id="06fc6-238">ResourceType</span></span> | <span data-ttu-id="06fc6-239">AUTOMATIONACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="06fc6-239">AUTOMATIONACCOUNTS</span></span> |

## <a name="viewing-automation-logs-in-log-analytics"></a><span data-ttu-id="06fc6-240">Viewing Automation Logs in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="06fc6-240">Viewing Automation Logs in Log Analytics</span></span>
<span data-ttu-id="06fc6-241">Now that you have started sending your Automation job logs to Log Analytics, let’s see what you can do with these logs inside Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="06fc6-241">Now that you have started sending your Automation job logs to Log Analytics, let’s see what you can do with these logs inside Log Analytics.</span></span>

<span data-ttu-id="06fc6-242">To see the logs, run the following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span><span class="sxs-lookup"><span data-stu-id="06fc6-242">To see the logs, run the following query: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`</span></span>

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a><span data-ttu-id="06fc6-243">Send an email when a runbook job fails or suspends</span><span class="sxs-lookup"><span data-stu-id="06fc6-243">Send an email when a runbook job fails or suspends</span></span>
<span data-ttu-id="06fc6-244">One of our top customer asks is for the ability to send an email or a text when something goes wrong with a runbook job.</span><span class="sxs-lookup"><span data-stu-id="06fc6-244">One of our top customer asks is for the ability to send an email or a text when something goes wrong with a runbook job.</span></span>   

<span data-ttu-id="06fc6-245">To create an alert rule, you start by creating a log search for the runbook job records that should invoke the alert.</span><span class="sxs-lookup"><span data-stu-id="06fc6-245">To create an alert rule, you start by creating a log search for the runbook job records that should invoke the alert.</span></span>  <span data-ttu-id="06fc6-246">Click the **Alert** button to create and configure the alert rule.</span><span class="sxs-lookup"><span data-stu-id="06fc6-246">Click the **Alert** button to create and configure the alert rule.</span></span>

1. <span data-ttu-id="06fc6-247">From the Log Analytics Overview page, click **Log Search**.</span><span class="sxs-lookup"><span data-stu-id="06fc6-247">From the Log Analytics Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="06fc6-248">Create a log search query for your alert by typing the following search into the query field:  `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  You can also group by the RunbookName by using: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span><span class="sxs-lookup"><span data-stu-id="06fc6-248">Create a log search query for your alert by typing the following search into the query field:  `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)`  You can also group by the RunbookName by using: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`</span></span>   

   <span data-ttu-id="06fc6-249">If you have set up logs from more than one Automation account or subscription to your workspace, you can group your alerts by subscription and Automation account.</span><span class="sxs-lookup"><span data-stu-id="06fc6-249">If you have set up logs from more than one Automation account or subscription to your workspace, you can group your alerts by subscription and Automation account.</span></span>  <span data-ttu-id="06fc6-250">Automation account name can be derived from the Resource field in the search of JobLogs.</span><span class="sxs-lookup"><span data-stu-id="06fc6-250">Automation account name can be derived from the Resource field in the search of JobLogs.</span></span>  
3. <span data-ttu-id="06fc6-251">To open the **Add Alert Rule** screen, click **Alert** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="06fc6-251">To open the **Add Alert Rule** screen, click **Alert** at the top of the page.</span></span> <span data-ttu-id="06fc6-252">For further details on the options to configure the alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span><span class="sxs-lookup"><span data-stu-id="06fc6-252">For further details on the options to configure the alert, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md#alert-rules).</span></span>

### <a name="find-all-jobs-that-have-completed-with-errors"></a><span data-ttu-id="06fc6-253">Find all jobs that have completed with errors</span><span class="sxs-lookup"><span data-stu-id="06fc6-253">Find all jobs that have completed with errors</span></span>
<span data-ttu-id="06fc6-254">In addition to alerting on failures, you can find when a runbook job has a non-terminating error.</span><span class="sxs-lookup"><span data-stu-id="06fc6-254">In addition to alerting on failures, you can find when a runbook job has a non-terminating error.</span></span> <span data-ttu-id="06fc6-255">In these cases PowerShell produces an error stream, but the non-terminating errors do not cause your job to suspend or fail.</span><span class="sxs-lookup"><span data-stu-id="06fc6-255">In these cases PowerShell produces an error stream, but the non-terminating errors do not cause your job to suspend or fail.</span></span>    

1. <span data-ttu-id="06fc6-256">In your Log Analytics workspace, click **Log Search**.</span><span class="sxs-lookup"><span data-stu-id="06fc6-256">In your Log Analytics workspace, click **Log Search**.</span></span>
2. <span data-ttu-id="06fc6-257">In the query field, type `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` and then click **Search**.</span><span class="sxs-lookup"><span data-stu-id="06fc6-257">In the query field, type `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` and then click **Search**.</span></span>

### <a name="view-job-streams-for-a-job"></a><span data-ttu-id="06fc6-258">View job streams for a job</span><span class="sxs-lookup"><span data-stu-id="06fc6-258">View job streams for a job</span></span>
<span data-ttu-id="06fc6-259">When you are debugging a job, you may also want to look into the job streams.</span><span class="sxs-lookup"><span data-stu-id="06fc6-259">When you are debugging a job, you may also want to look into the job streams.</span></span>  <span data-ttu-id="06fc6-260">The following query shows all the streams for a single job with GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:</span><span class="sxs-lookup"><span data-stu-id="06fc6-260">The following query shows all the streams for a single job with GUID 2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0:</span></span>   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a><span data-ttu-id="06fc6-261">View historical job status</span><span class="sxs-lookup"><span data-stu-id="06fc6-261">View historical job status</span></span>
<span data-ttu-id="06fc6-262">Finally, you may want to visualize your job history over time.</span><span class="sxs-lookup"><span data-stu-id="06fc6-262">Finally, you may want to visualize your job history over time.</span></span>  <span data-ttu-id="06fc6-263">You can use this query to search for the status of your jobs over time.</span><span class="sxs-lookup"><span data-stu-id="06fc6-263">You can use this query to search for the status of your jobs over time.</span></span>

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> <span data-ttu-id="06fc6-264">![OMS Historical Job Status Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span><span class="sxs-lookup"><span data-stu-id="06fc6-264">![OMS Historical Job Status Chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)</span></span><br>

## <a name="summary"></a><span data-ttu-id="06fc6-265">Summary</span><span class="sxs-lookup"><span data-stu-id="06fc6-265">Summary</span></span>
<span data-ttu-id="06fc6-266">By sending your Automation job status and stream data to Log Analytics, you can get better insight into the status of your Automation jobs by:</span><span class="sxs-lookup"><span data-stu-id="06fc6-266">By sending your Automation job status and stream data to Log Analytics, you can get better insight into the status of your Automation jobs by:</span></span>
+ <span data-ttu-id="06fc6-267">Setting up alerts to notify you when there is an issue</span><span class="sxs-lookup"><span data-stu-id="06fc6-267">Setting up alerts to notify you when there is an issue</span></span>
+ <span data-ttu-id="06fc6-268">Using custom views and search queries to visualize your runbook results, runbook job status, and other related key indicators or metrics.</span><span class="sxs-lookup"><span data-stu-id="06fc6-268">Using custom views and search queries to visualize your runbook results, runbook job status, and other related key indicators or metrics.</span></span>  

<span data-ttu-id="06fc6-269">Log Analytics provides greater operational visibility to your Automation jobs and can help address incidents quicker.</span><span class="sxs-lookup"><span data-stu-id="06fc6-269">Log Analytics provides greater operational visibility to your Automation jobs and can help address incidents quicker.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="06fc6-270">Next steps</span><span class="sxs-lookup"><span data-stu-id="06fc6-270">Next steps</span></span>
* <span data-ttu-id="06fc6-271">To learn more about how to construct different search queries and review the Automation job logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span><span class="sxs-lookup"><span data-stu-id="06fc6-271">To learn more about how to construct different search queries and review the Automation job logs with Log Analytics, see [Log searches in Log Analytics](../log-analytics/log-analytics-log-searches.md)</span></span>
* <span data-ttu-id="06fc6-272">To understand how to create and retrieve output and error messages from runbooks, see [Runbook output and messages](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="06fc6-272">To understand how to create and retrieve output and error messages from runbooks, see [Runbook output and messages](automation-runbook-output-and-messages.md)</span></span>
* <span data-ttu-id="06fc6-273">To learn more about runbook execution, how to monitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md)</span><span class="sxs-lookup"><span data-stu-id="06fc6-273">To learn more about runbook execution, how to monitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md)</span></span>
* <span data-ttu-id="06fc6-274">To learn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="06fc6-274">To learn more about OMS Log Analytics and data collection sources, see [Collecting Azure storage data in Log Analytics overview](../log-analytics/log-analytics-azure-storage.md)</span></span>


