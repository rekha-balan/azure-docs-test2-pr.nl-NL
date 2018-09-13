---
title: Collecting Log Analytics data with a runbook in Azure Automation | Microsoft Docs
description: Step by step tutorial that walks through creating a runbook in Azure Automation to collect data into the OMS repository for analysis by Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: monitoring
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: d3e8e876a6c01123d65c1e8df13328bdd5fad71f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855585"
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a><span data-ttu-id="80f7a-103">Collect data in Log Analytics with an Azure Automation runbook</span><span class="sxs-lookup"><span data-stu-id="80f7a-103">Collect data in Log Analytics with an Azure Automation runbook</span></span>
<span data-ttu-id="80f7a-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="80f7a-104">You can collect a significant amount of data in Log Analytics from a variety of sources including [data sources](../log-analytics/log-analytics-data-sources.md) on agents and also [data collected from Azure](../log-analytics/log-analytics-azure-storage.md).</span></span>  <span data-ttu-id="80f7a-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span><span class="sxs-lookup"><span data-stu-id="80f7a-105">There are a scenarios though where you need to collect data that isn't accessible through these standard sources.</span></span>  <span data-ttu-id="80f7a-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span><span class="sxs-lookup"><span data-stu-id="80f7a-106">In these cases, you can use the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md) to write data to Log Analytics from any REST API client.</span></span>  <span data-ttu-id="80f7a-107">A common method to perform this data collection is using a runbook in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="80f7a-107">A common method to perform this data collection is using a runbook in Azure Automation.</span></span>   

<span data-ttu-id="80f7a-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="80f7a-108">This tutorial walks through the process for creating and scheduling a runbook in Azure Automation to write data to Log Analytics.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="80f7a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="80f7a-109">Prerequisites</span></span>
<span data-ttu-id="80f7a-110">This scenario requires the following resources configured in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="80f7a-110">This scenario requires the following resources configured in your Azure subscription.</span></span>  <span data-ttu-id="80f7a-111">Both can be a free account.</span><span class="sxs-lookup"><span data-stu-id="80f7a-111">Both can be a free account.</span></span>

- <span data-ttu-id="80f7a-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="80f7a-112">[Log Analytics workspace](../log-analytics/log-analytics-get-started.md).</span></span>
- <span data-ttu-id="80f7a-113">[Azure automation account](../automation/automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="80f7a-113">[Azure automation account](../automation/automation-offering-get-started.md).</span></span>

## <a name="overview-of-scenario"></a><span data-ttu-id="80f7a-114">Overview of scenario</span><span class="sxs-lookup"><span data-stu-id="80f7a-114">Overview of scenario</span></span>
<span data-ttu-id="80f7a-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span><span class="sxs-lookup"><span data-stu-id="80f7a-115">For this tutorial, you'll write a runbook that collects information about Automation jobs.</span></span>  <span data-ttu-id="80f7a-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span><span class="sxs-lookup"><span data-stu-id="80f7a-116">Runbooks in Azure Automation are implemented with PowerShell, so you'll start by writing and testing a script in the Azure Automation editor.</span></span>  <span data-ttu-id="80f7a-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span><span class="sxs-lookup"><span data-stu-id="80f7a-117">Once you verify that you're collecting the required information, you'll write that data to Log Analytics and verify the custom data type.</span></span>  <span data-ttu-id="80f7a-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="80f7a-118">Finally, you'll create a schedule to start the runbook at regular intervals.</span></span>

> [!NOTE]
> <span data-ttu-id="80f7a-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-119">You can configure Azure Automation to send job information to Log Analytics without this runbook.</span></span>  <span data-ttu-id="80f7a-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span><span class="sxs-lookup"><span data-stu-id="80f7a-120">This scenario is primarily used to support the tutorial, and it's recommended that you send the data to a test workspace.</span></span>  


## <a name="1-install-data-collector-api-module"></a><span data-ttu-id="80f7a-121">1. Install Data Collector API module</span><span class="sxs-lookup"><span data-stu-id="80f7a-121">1. Install Data Collector API module</span></span>
<span data-ttu-id="80f7a-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span><span class="sxs-lookup"><span data-stu-id="80f7a-122">Every [request from the HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md#create-a-request) must be formatted appropriately and include an authorization header.</span></span>  <span data-ttu-id="80f7a-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span><span class="sxs-lookup"><span data-stu-id="80f7a-123">You can do this in your runbook, but you can reduce the amount of code required by using a module that simplifies this process.</span></span>  <span data-ttu-id="80f7a-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="80f7a-124">One module that you can use is [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) in the PowerShell Gallery.</span></span>

<span data-ttu-id="80f7a-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="80f7a-125">To use a [module](../automation/automation-integration-modules.md) in a runbook, it must be installed in your Automation account.</span></span>  <span data-ttu-id="80f7a-126">Any runbook in the same account can then use the functions in the module.</span><span class="sxs-lookup"><span data-stu-id="80f7a-126">Any runbook in the same account can then use the functions in the module.</span></span>  <span data-ttu-id="80f7a-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="80f7a-127">You can install a new module by selecting **Assets** > **Modules** > **Add a module** in your Automation account.</span></span>  

<span data-ttu-id="80f7a-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="80f7a-128">The PowerShell Gallery though gives you a quick option to deploy a module directly to your automation account so you can use that option for this tutorial.</span></span>  

![OMSIngestionAPI module](media/monitoring-runbook-datacollect/OMSIngestionAPI.png)

1. <span data-ttu-id="80f7a-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="80f7a-130">Go to [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
2. <span data-ttu-id="80f7a-131">Search for **OMSIngestionAPI**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-131">Search for **OMSIngestionAPI**.</span></span>
3. <span data-ttu-id="80f7a-132">Click on the **Deploy to Azure Automation** button.</span><span class="sxs-lookup"><span data-stu-id="80f7a-132">Click on the **Deploy to Azure Automation** button.</span></span>
4. <span data-ttu-id="80f7a-133">Select your automation account and click **OK** to install the module.</span><span class="sxs-lookup"><span data-stu-id="80f7a-133">Select your automation account and click **OK** to install the module.</span></span>


## <a name="2-create-automation-variables"></a><span data-ttu-id="80f7a-134">2. Create Automation variables</span><span class="sxs-lookup"><span data-stu-id="80f7a-134">2. Create Automation variables</span></span>
<span data-ttu-id="80f7a-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span><span class="sxs-lookup"><span data-stu-id="80f7a-135">[Automation variables](..\automation\automation-variables.md) hold values that can be used by all runbooks in your Automation account.</span></span>  <span data-ttu-id="80f7a-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-136">They make runbooks more flexible by allowing you to change these values without editing the actual runbook.</span></span> <span data-ttu-id="80f7a-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span><span class="sxs-lookup"><span data-stu-id="80f7a-137">Every request from the HTTP Data Collector API requires the ID and key of the OMS workspace, and variable assets are ideal to store this information.</span></span>  

![Variables](media/monitoring-runbook-datacollect/variables.png)

1. <span data-ttu-id="80f7a-139">In the Azure portal, navigate to your Automation account.</span><span class="sxs-lookup"><span data-stu-id="80f7a-139">In the Azure portal, navigate to your Automation account.</span></span>
2. <span data-ttu-id="80f7a-140">Select **Variables** under **Shared Resources**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-140">Select **Variables** under **Shared Resources**.</span></span>
2. <span data-ttu-id="80f7a-141">Click **Add a variable** and create the two variables in the following table.</span><span class="sxs-lookup"><span data-stu-id="80f7a-141">Click **Add a variable** and create the two variables in the following table.</span></span>

| <span data-ttu-id="80f7a-142">Property</span><span class="sxs-lookup"><span data-stu-id="80f7a-142">Property</span></span> | <span data-ttu-id="80f7a-143">Workspace ID Value</span><span class="sxs-lookup"><span data-stu-id="80f7a-143">Workspace ID Value</span></span> | <span data-ttu-id="80f7a-144">Workspace Key Value</span><span class="sxs-lookup"><span data-stu-id="80f7a-144">Workspace Key Value</span></span> |
|:--|:--|:--|
| <span data-ttu-id="80f7a-145">Name</span><span class="sxs-lookup"><span data-stu-id="80f7a-145">Name</span></span> | <span data-ttu-id="80f7a-146">WorkspaceId</span><span class="sxs-lookup"><span data-stu-id="80f7a-146">WorkspaceId</span></span> | <span data-ttu-id="80f7a-147">WorkspaceKey</span><span class="sxs-lookup"><span data-stu-id="80f7a-147">WorkspaceKey</span></span> |
| <span data-ttu-id="80f7a-148">Type</span><span class="sxs-lookup"><span data-stu-id="80f7a-148">Type</span></span> | <span data-ttu-id="80f7a-149">String</span><span class="sxs-lookup"><span data-stu-id="80f7a-149">String</span></span> | <span data-ttu-id="80f7a-150">String</span><span class="sxs-lookup"><span data-stu-id="80f7a-150">String</span></span> |
| <span data-ttu-id="80f7a-151">Value</span><span class="sxs-lookup"><span data-stu-id="80f7a-151">Value</span></span> | <span data-ttu-id="80f7a-152">Paste in the Workspace ID of your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="80f7a-152">Paste in the Workspace ID of your Log Analytics workspace.</span></span> | <span data-ttu-id="80f7a-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="80f7a-153">Paste in with the Primary or Secondary Key of your Log Analytics workspace.</span></span> |
| <span data-ttu-id="80f7a-154">Encrypted</span><span class="sxs-lookup"><span data-stu-id="80f7a-154">Encrypted</span></span> | <span data-ttu-id="80f7a-155">No</span><span class="sxs-lookup"><span data-stu-id="80f7a-155">No</span></span> | <span data-ttu-id="80f7a-156">Yes</span><span class="sxs-lookup"><span data-stu-id="80f7a-156">Yes</span></span> |



## <a name="3-create-runbook"></a><span data-ttu-id="80f7a-157">3. Create runbook</span><span class="sxs-lookup"><span data-stu-id="80f7a-157">3. Create runbook</span></span>

<span data-ttu-id="80f7a-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-158">Azure Automation has an editor in the portal where you can edit and test your runbook.</span></span>  <span data-ttu-id="80f7a-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="80f7a-159">You have the option to use the script editor to work with [PowerShell directly](../automation/automation-edit-textual-runbook.md) or [create a graphical runbook](../automation/automation-graphical-authoring-intro.md).</span></span>  <span data-ttu-id="80f7a-160">For this tutorial, you will work with a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="80f7a-160">For this tutorial, you will work with a PowerShell script.</span></span> 

![Edit runbook](media/monitoring-runbook-datacollect/edit-runbook.png)

1. <span data-ttu-id="80f7a-162">Navigate to your Automation account.</span><span class="sxs-lookup"><span data-stu-id="80f7a-162">Navigate to your Automation account.</span></span>  
2. <span data-ttu-id="80f7a-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-163">Click **Runbooks** > **Add a runbook** > **Create a new runbook**.</span></span>
3. <span data-ttu-id="80f7a-164">For the runbook name, type **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-164">For the runbook name, type **Collect-Automation-jobs**.</span></span>  <span data-ttu-id="80f7a-165">For the runbook type, select **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-165">For the runbook type, select **PowerShell**.</span></span>
4. <span data-ttu-id="80f7a-166">Click **Create** to create the runbook and start the editor.</span><span class="sxs-lookup"><span data-stu-id="80f7a-166">Click **Create** to create the runbook and start the editor.</span></span>
5. <span data-ttu-id="80f7a-167">Copy and paste the following code into the runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-167">Copy and paste the following code into the runbook.</span></span>  <span data-ttu-id="80f7a-168">Refer to the comments in the script for explanation of the code.</span><span class="sxs-lookup"><span data-stu-id="80f7a-168">Refer to the comments in the script for explanation of the code.</span></span>
    
        # Get information required for the automation account from parameter values when the runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate to the Automation account using the Azure connection created when the Automation account was created.
        # Code copied from the runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Connect-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set the $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set the name of the record type.
        $logType = "AutomationJob"
        
        # Get the jobs from the past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert the job data to json
            $body = $jobs | ConvertTo-Json
        
            # Write the body to verbose output so we can inspect it if verbose logging is on for the runbook.
            Write-Verbose $body
        
            # Send the data to Log Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a><span data-ttu-id="80f7a-169">4. Test runbook</span><span class="sxs-lookup"><span data-stu-id="80f7a-169">4. Test runbook</span></span>
<span data-ttu-id="80f7a-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span><span class="sxs-lookup"><span data-stu-id="80f7a-170">Azure Automation includes an environment to [test your runbook](../automation/automation-testing-runbook.md) before you publish it.</span></span>  <span data-ttu-id="80f7a-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span><span class="sxs-lookup"><span data-stu-id="80f7a-171">You can inspect the data collected by the runbook and verify that it writes to Log Analytics as expected before publishing it to production.</span></span> 
 
![Test runbook](media/monitoring-runbook-datacollect/test-runbook.png)

6. <span data-ttu-id="80f7a-173">Click **Save** to save the runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-173">Click **Save** to save the runbook.</span></span>
1. <span data-ttu-id="80f7a-174">Click **Test pane** to open the runbook in the test environment.</span><span class="sxs-lookup"><span data-stu-id="80f7a-174">Click **Test pane** to open the runbook in the test environment.</span></span>
3. <span data-ttu-id="80f7a-175">Since your runbook has parameters, you're prompted to enter values for them.</span><span class="sxs-lookup"><span data-stu-id="80f7a-175">Since your runbook has parameters, you're prompted to enter values for them.</span></span>  <span data-ttu-id="80f7a-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span><span class="sxs-lookup"><span data-stu-id="80f7a-176">Enter the name of the resource group and the automation account that your going to collect job information from.</span></span>
4. <span data-ttu-id="80f7a-177">Click **Start** to the start the runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-177">Click **Start** to the start the runbook.</span></span>
3. <span data-ttu-id="80f7a-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-178">The runbook will start with a status of **Queued** before it goes to **Running**.</span></span>  
3. <span data-ttu-id="80f7a-179">The runbook should display verbose output with the jobs collected in json format.</span><span class="sxs-lookup"><span data-stu-id="80f7a-179">The runbook should display verbose output with the jobs collected in json format.</span></span>  <span data-ttu-id="80f7a-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span><span class="sxs-lookup"><span data-stu-id="80f7a-180">If no jobs are listed, then there may have been no jobs created in the automation account in the last hour.</span></span>  <span data-ttu-id="80f7a-181">Try starting any runbook in the automation account and then perform the test again.</span><span class="sxs-lookup"><span data-stu-id="80f7a-181">Try starting any runbook in the automation account and then perform the test again.</span></span>
4. <span data-ttu-id="80f7a-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="80f7a-182">Ensure that the output doesn't show any errors in the post command to Log Analytics.</span></span>  <span data-ttu-id="80f7a-183">You should have a message similar to the following.</span><span class="sxs-lookup"><span data-stu-id="80f7a-183">You should have a message similar to the following.</span></span>

    ![Post output](media/monitoring-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a><span data-ttu-id="80f7a-185">5. Verify records in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="80f7a-185">5. Verify records in Log Analytics</span></span>
<span data-ttu-id="80f7a-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="80f7a-186">Once the runbook has completed in test, and you verified that the output was successfully received, you can verify that the records were created using a [log search in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

![Log output](media/monitoring-runbook-datacollect/log-output.png)

1. <span data-ttu-id="80f7a-188">In the Azure portal, select your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="80f7a-188">In the Azure portal, select your Log Analytics workspace.</span></span>
2. <span data-ttu-id="80f7a-189">Click on **Log Search**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-189">Click on **Log Search**.</span></span>
3. <span data-ttu-id="80f7a-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span><span class="sxs-lookup"><span data-stu-id="80f7a-190">Type the following command `Type=AutomationJob_CL` and click the search button.</span></span> <span data-ttu-id="80f7a-191">Note that the record type includes _CL that isn't specified in the script.</span><span class="sxs-lookup"><span data-stu-id="80f7a-191">Note that the record type includes _CL that isn't specified in the script.</span></span>  <span data-ttu-id="80f7a-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span><span class="sxs-lookup"><span data-stu-id="80f7a-192">That suffix is automatically appended to the log type to indicate that it's a custom log type.</span></span>
4. <span data-ttu-id="80f7a-193">You should see one or more records returned indicating that the runbook is working as expected.</span><span class="sxs-lookup"><span data-stu-id="80f7a-193">You should see one or more records returned indicating that the runbook is working as expected.</span></span>


## <a name="6-publish-the-runbook"></a><span data-ttu-id="80f7a-194">6. Publish the runbook</span><span class="sxs-lookup"><span data-stu-id="80f7a-194">6. Publish the runbook</span></span>
<span data-ttu-id="80f7a-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span><span class="sxs-lookup"><span data-stu-id="80f7a-195">Once you've verified that the runbook is working correctly, you need to publish it so you can run it in production.</span></span>  <span data-ttu-id="80f7a-196">You can continue to edit and test the runbook without modifying the published version.</span><span class="sxs-lookup"><span data-stu-id="80f7a-196">You can continue to edit and test the runbook without modifying the published version.</span></span>  

![Publish runbook](media/monitoring-runbook-datacollect/publish-runbook.png)

1. <span data-ttu-id="80f7a-198">Return to your automation account.</span><span class="sxs-lookup"><span data-stu-id="80f7a-198">Return to your automation account.</span></span>
2. <span data-ttu-id="80f7a-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-199">Click on **Runbooks** and select **Collect-Automation-jobs**.</span></span>
3. <span data-ttu-id="80f7a-200">Click **Edit** and then **Publish**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-200">Click **Edit** and then **Publish**.</span></span>
4. <span data-ttu-id="80f7a-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span><span class="sxs-lookup"><span data-stu-id="80f7a-201">Click **Yes** when asked to verify that you want to overwrite the previously published version.</span></span>

## <a name="7-set-logging-options"></a><span data-ttu-id="80f7a-202">7. Set logging options</span><span class="sxs-lookup"><span data-stu-id="80f7a-202">7. Set logging options</span></span> 
<span data-ttu-id="80f7a-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span><span class="sxs-lookup"><span data-stu-id="80f7a-203">For test, you were able to view [verbose output](../automation/automation-runbook-output-and-messages.md#message-streams) because you set the $VerbosePreference variable in the script.</span></span>  <span data-ttu-id="80f7a-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span><span class="sxs-lookup"><span data-stu-id="80f7a-204">For production, you need to set the logging properties for the runbook if you want to view verbose output.</span></span>  <span data-ttu-id="80f7a-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="80f7a-205">For the runbook used in this tutorial, this will display the json data being sent to Log Analytics.</span></span>

![Logging and tracing](media/monitoring-runbook-datacollect/logging.png)

1. <span data-ttu-id="80f7a-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-207">In the properties for your runbook select **Logging and tracing** under **Runbook Settings**.</span></span>
2. <span data-ttu-id="80f7a-208">Change the setting for **Log verbose records** to **On**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-208">Change the setting for **Log verbose records** to **On**.</span></span>
3. <span data-ttu-id="80f7a-209">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-209">Click **Save**.</span></span>

## <a name="8-schedule-runbook"></a><span data-ttu-id="80f7a-210">8. Schedule runbook</span><span class="sxs-lookup"><span data-stu-id="80f7a-210">8. Schedule runbook</span></span>
<span data-ttu-id="80f7a-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span><span class="sxs-lookup"><span data-stu-id="80f7a-211">The most common way to start a runbook that collects monitoring data is to schedule it to run automatically.</span></span>  <span data-ttu-id="80f7a-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-212">You do this by creating a [schedule in Azure Automation](../automation/automation-schedules.md) and attaching it to your runbook.</span></span>

![Schedule runbook](media/monitoring-runbook-datacollect/schedule-runbook.png)

1. <span data-ttu-id="80f7a-214">In the properties for your runbook, select **Schedules** under **Resources**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-214">In the properties for your runbook, select **Schedules** under **Resources**.</span></span>
2. <span data-ttu-id="80f7a-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-215">Click **Add a schedule** > **Link a schedule to your runbook** > **Create a new schedule**.</span></span>
5. <span data-ttu-id="80f7a-216">Type in the following values for the schedule and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-216">Type in the following values for the schedule and click **Create**.</span></span>

| <span data-ttu-id="80f7a-217">Property</span><span class="sxs-lookup"><span data-stu-id="80f7a-217">Property</span></span> | <span data-ttu-id="80f7a-218">Value</span><span class="sxs-lookup"><span data-stu-id="80f7a-218">Value</span></span> |
|:--|:--|
| <span data-ttu-id="80f7a-219">Name</span><span class="sxs-lookup"><span data-stu-id="80f7a-219">Name</span></span> | <span data-ttu-id="80f7a-220">AutomationJobs-Hourly</span><span class="sxs-lookup"><span data-stu-id="80f7a-220">AutomationJobs-Hourly</span></span> |
| <span data-ttu-id="80f7a-221">Starts</span><span class="sxs-lookup"><span data-stu-id="80f7a-221">Starts</span></span> | <span data-ttu-id="80f7a-222">Select any time at least 5 minutes past the current time.</span><span class="sxs-lookup"><span data-stu-id="80f7a-222">Select any time at least 5 minutes past the current time.</span></span> |
| <span data-ttu-id="80f7a-223">Recurrence</span><span class="sxs-lookup"><span data-stu-id="80f7a-223">Recurrence</span></span> | <span data-ttu-id="80f7a-224">Recurring</span><span class="sxs-lookup"><span data-stu-id="80f7a-224">Recurring</span></span> |
| <span data-ttu-id="80f7a-225">Recur every</span><span class="sxs-lookup"><span data-stu-id="80f7a-225">Recur every</span></span> | <span data-ttu-id="80f7a-226">1 hour</span><span class="sxs-lookup"><span data-stu-id="80f7a-226">1 hour</span></span> |
| <span data-ttu-id="80f7a-227">Set expiration</span><span class="sxs-lookup"><span data-stu-id="80f7a-227">Set expiration</span></span> | <span data-ttu-id="80f7a-228">No</span><span class="sxs-lookup"><span data-stu-id="80f7a-228">No</span></span> |

<span data-ttu-id="80f7a-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-229">Once the schedule is created, you need to set the parameter values that will be used each time this schedule starts the runbook.</span></span>

6. <span data-ttu-id="80f7a-230">Click **Configure parameters and run settings**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-230">Click **Configure parameters and run settings**.</span></span>
7. <span data-ttu-id="80f7a-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-231">Fill in values for your **ResourceGroupName** and **AutomationAccountName**.</span></span>
8. <span data-ttu-id="80f7a-232">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-232">Click **OK**.</span></span> 

## <a name="9-verify-runbook-starts-on-schedule"></a><span data-ttu-id="80f7a-233">9. Verify runbook starts on schedule</span><span class="sxs-lookup"><span data-stu-id="80f7a-233">9. Verify runbook starts on schedule</span></span>
<span data-ttu-id="80f7a-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span><span class="sxs-lookup"><span data-stu-id="80f7a-234">Everytime a runbook is started, [a job is created](../automation/automation-runbook-execution.md) and any output logged.</span></span>  <span data-ttu-id="80f7a-235">In fact, these are the same jobs that the runbook is collecting.</span><span class="sxs-lookup"><span data-stu-id="80f7a-235">In fact, these are the same jobs that the runbook is collecting.</span></span>  <span data-ttu-id="80f7a-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span><span class="sxs-lookup"><span data-stu-id="80f7a-236">You can verify that the runbook starts as expected by checking the jobs for the runbook after the start time for the schedule has passed.</span></span>

![Jobs](media/monitoring-runbook-datacollect/jobs.png)

1. <span data-ttu-id="80f7a-238">In the properties for your runbook, select **Jobs** under **Resources**.</span><span class="sxs-lookup"><span data-stu-id="80f7a-238">In the properties for your runbook, select **Jobs** under **Resources**.</span></span>
2. <span data-ttu-id="80f7a-239">You should see a listing of jobs for each time the runbook was started.</span><span class="sxs-lookup"><span data-stu-id="80f7a-239">You should see a listing of jobs for each time the runbook was started.</span></span>
3. <span data-ttu-id="80f7a-240">Click on one of the jobs to view its details.</span><span class="sxs-lookup"><span data-stu-id="80f7a-240">Click on one of the jobs to view its details.</span></span>
4. <span data-ttu-id="80f7a-241">Click on **All logs** to view the logs and output from the runbook.</span><span class="sxs-lookup"><span data-stu-id="80f7a-241">Click on **All logs** to view the logs and output from the runbook.</span></span>
5. <span data-ttu-id="80f7a-242">Scroll to the bottom to find an entry similar to the image below.</span><span class="sxs-lookup"><span data-stu-id="80f7a-242">Scroll to the bottom to find an entry similar to the image below.</span></span><br>![Verbose](media/monitoring-runbook-datacollect/verbose.png)
6. <span data-ttu-id="80f7a-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="80f7a-244">Click on this entry to view the detailed json data  that was sent to Log Analytics.</span></span>



## <a name="next-steps"></a><span data-ttu-id="80f7a-245">Next steps</span><span class="sxs-lookup"><span data-stu-id="80f7a-245">Next steps</span></span>
- <span data-ttu-id="80f7a-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span><span class="sxs-lookup"><span data-stu-id="80f7a-246">Use [View Designer](../log-analytics/log-analytics-view-designer.md) to create a view displaying the data that you've collected to the Log Analytics repository.</span></span>
- <span data-ttu-id="80f7a-247">Package your runbook in a [management solution](monitoring-solutions-creating.md) to distribute to customers.</span><span class="sxs-lookup"><span data-stu-id="80f7a-247">Package your runbook in a [management solution](monitoring-solutions-creating.md) to distribute to customers.</span></span>
- <span data-ttu-id="80f7a-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="80f7a-248">Learn more about [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).</span></span>
- <span data-ttu-id="80f7a-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span><span class="sxs-lookup"><span data-stu-id="80f7a-249">Learn more about [Azure Automation](https://docs.microsoft.com/azure/automation/).</span></span>
- <span data-ttu-id="80f7a-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span><span class="sxs-lookup"><span data-stu-id="80f7a-250">Learn more about the [HTTP Data Collector API](../log-analytics/log-analytics-data-collector-api.md).</span></span>
