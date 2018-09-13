---
title: Starting and stopping virtual machines with Azure Automation - PowerShell Workflow | Microsoft Docs
description: Graphical version of Azure Automation scenario including runbooks to start and stop classic virtual machines.
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: false
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552831"
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a><span data-ttu-id="a1503-103">Azure Automation scenario - starting and stopping virtual machines</span><span class="sxs-lookup"><span data-stu-id="a1503-103">Azure Automation scenario - starting and stopping virtual machines</span></span>
<span data-ttu-id="a1503-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span><span class="sxs-lookup"><span data-stu-id="a1503-104">This Azure Automation scenario includes runbooks to start and stop classic virtual machines.</span></span>  <span data-ttu-id="a1503-105">You can use this scenario for any of the following:</span><span class="sxs-lookup"><span data-stu-id="a1503-105">You can use this scenario for any of the following:</span></span>  

* <span data-ttu-id="a1503-106">Use the runbooks without modification in your own environment.</span><span class="sxs-lookup"><span data-stu-id="a1503-106">Use the runbooks without modification in your own environment.</span></span>
* <span data-ttu-id="a1503-107">Modify the runbooks to perform customized functionality.</span><span class="sxs-lookup"><span data-stu-id="a1503-107">Modify the runbooks to perform customized functionality.</span></span>  
* <span data-ttu-id="a1503-108">Call the runbooks from another runbook as part of an overall solution.</span><span class="sxs-lookup"><span data-stu-id="a1503-108">Call the runbooks from another runbook as part of an overall solution.</span></span>
* <span data-ttu-id="a1503-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span><span class="sxs-lookup"><span data-stu-id="a1503-109">Use the runbooks as tutorials to learn runbook authoring concepts.</span></span>

> [!div class="op_single_selector"]
> * [Graphical](automation-solution-startstopvm-graphical.md)
> * [PowerShell Workflow](automation-solution-startstopvm-psworkflow.md)
> 
> 

<span data-ttu-id="a1503-112">This is the PowerShell Workflow runbook version of this scenario.</span><span class="sxs-lookup"><span data-stu-id="a1503-112">This is the PowerShell Workflow runbook version of this scenario.</span></span> <span data-ttu-id="a1503-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="a1503-113">It is also available using [graphical runbooks](automation-solution-startstopvm-graphical.md).</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="a1503-114">Getting the scenario</span><span class="sxs-lookup"><span data-stu-id="a1503-114">Getting the scenario</span></span>
<span data-ttu-id="a1503-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span><span class="sxs-lookup"><span data-stu-id="a1503-115">This scenario consists of two PowerShell Workflow runbooks that you can download from the following links.</span></span>  <span data-ttu-id="a1503-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span><span class="sxs-lookup"><span data-stu-id="a1503-116">See the [graphical version](automation-solution-startstopvm-graphical.md) of this scenario for links to the graphical runbooks.</span></span>

| <span data-ttu-id="a1503-117">Runbook</span><span class="sxs-lookup"><span data-stu-id="a1503-117">Runbook</span></span> | <span data-ttu-id="a1503-118">Link</span><span class="sxs-lookup"><span data-stu-id="a1503-118">Link</span></span> | <span data-ttu-id="a1503-119">Type</span><span class="sxs-lookup"><span data-stu-id="a1503-119">Type</span></span> | <span data-ttu-id="a1503-120">Description</span><span class="sxs-lookup"><span data-stu-id="a1503-120">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a1503-121">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a1503-121">Start-AzureVMs</span></span> |[<span data-ttu-id="a1503-122">Start Azure Classic VMs</span><span class="sxs-lookup"><span data-stu-id="a1503-122">Start Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |<span data-ttu-id="a1503-123">PowerShell Workflow</span><span class="sxs-lookup"><span data-stu-id="a1503-123">PowerShell Workflow</span></span> |<span data-ttu-id="a1503-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span><span class="sxs-lookup"><span data-stu-id="a1503-124">Starts all classic virtual machines in an Azure subscriptionor all virtual machines with a particular service name.</span></span> |
| <span data-ttu-id="a1503-125">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a1503-125">Stop-AzureVMs</span></span> |[<span data-ttu-id="a1503-126">Stop Azure Classic VMs</span><span class="sxs-lookup"><span data-stu-id="a1503-126">Stop Azure Classic VMs</span></span>](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |<span data-ttu-id="a1503-127">PowerShell Workflow</span><span class="sxs-lookup"><span data-stu-id="a1503-127">PowerShell Workflow</span></span> |<span data-ttu-id="a1503-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span><span class="sxs-lookup"><span data-stu-id="a1503-128">Stops all virtual machines in an automation account or all virtual machines with a particular service name.</span></span> |

## <a name="installing-and-configuring-the-scenario"></a><span data-ttu-id="a1503-129">Installing and configuring the scenario</span><span class="sxs-lookup"><span data-stu-id="a1503-129">Installing and configuring the scenario</span></span>
### <a name="1-install-the-runbooks"></a><span data-ttu-id="a1503-130">1. Install the runbooks</span><span class="sxs-lookup"><span data-stu-id="a1503-130">1. Install the runbooks</span></span>
<span data-ttu-id="a1503-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span><span class="sxs-lookup"><span data-stu-id="a1503-131">After downloading the runbooks, you can import them using the procedure in [Importing a Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).</span></span>

### <a name="2-review-the-description-and-requirements"></a><span data-ttu-id="a1503-132">2. Review the description and requirements</span><span class="sxs-lookup"><span data-stu-id="a1503-132">2. Review the description and requirements</span></span>
<span data-ttu-id="a1503-133">The runbooks include commented help text that includes a description and required assets.</span><span class="sxs-lookup"><span data-stu-id="a1503-133">The runbooks include commented help text that includes a description and required assets.</span></span>  <span data-ttu-id="a1503-134">You can also get the same information from this article.</span><span class="sxs-lookup"><span data-stu-id="a1503-134">You can also get the same information from this article.</span></span>

### <a name="3-configure-assets"></a><span data-ttu-id="a1503-135">3. Configure assets</span><span class="sxs-lookup"><span data-stu-id="a1503-135">3. Configure assets</span></span>
<span data-ttu-id="a1503-136">The runbooks require the following assets that you must create and populate with appropriate values.</span><span class="sxs-lookup"><span data-stu-id="a1503-136">The runbooks require the following assets that you must create and populate with appropriate values.</span></span>

| <span data-ttu-id="a1503-137">Asset Type</span><span class="sxs-lookup"><span data-stu-id="a1503-137">Asset Type</span></span> | <span data-ttu-id="a1503-138">Asset Name</span><span class="sxs-lookup"><span data-stu-id="a1503-138">Asset Name</span></span> | <span data-ttu-id="a1503-139">Description</span><span class="sxs-lookup"><span data-stu-id="a1503-139">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a1503-140">Credential</span><span class="sxs-lookup"><span data-stu-id="a1503-140">Credential</span></span> |<span data-ttu-id="a1503-141">AzureCredential</span><span class="sxs-lookup"><span data-stu-id="a1503-141">AzureCredential</span></span> |<span data-ttu-id="a1503-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a1503-142">Contains credentials for an account that has authority to start and stop virtual machines in the Azure subscription.</span></span>  <span data-ttu-id="a1503-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span><span class="sxs-lookup"><span data-stu-id="a1503-143">Alternatively, you can specify another credential asset in the **Credential** parameter of the **Add-AzureAccount** activity.</span></span> |
| <span data-ttu-id="a1503-144">Variable</span><span class="sxs-lookup"><span data-stu-id="a1503-144">Variable</span></span> |<span data-ttu-id="a1503-145">AzureSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a1503-145">AzureSubscriptionId</span></span> |<span data-ttu-id="a1503-146">Contains the subscription ID of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a1503-146">Contains the subscription ID of your Azure subscription.</span></span> |

## <a name="using-the-scenario"></a><span data-ttu-id="a1503-147">Using the scenario</span><span class="sxs-lookup"><span data-stu-id="a1503-147">Using the scenario</span></span>
### <a name="parameters"></a><span data-ttu-id="a1503-148">Parameters</span><span class="sxs-lookup"><span data-stu-id="a1503-148">Parameters</span></span>
<span data-ttu-id="a1503-149">The runbooks each have the following parameters.</span><span class="sxs-lookup"><span data-stu-id="a1503-149">The runbooks each have the following parameters.</span></span>  <span data-ttu-id="a1503-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span><span class="sxs-lookup"><span data-stu-id="a1503-150">You must provide values for any mandatory parameters and can optionally provide values for other parameters depending on your requirements.</span></span>

| <span data-ttu-id="a1503-151">Parameter</span><span class="sxs-lookup"><span data-stu-id="a1503-151">Parameter</span></span> | <span data-ttu-id="a1503-152">Type</span><span class="sxs-lookup"><span data-stu-id="a1503-152">Type</span></span> | <span data-ttu-id="a1503-153">Mandatory</span><span class="sxs-lookup"><span data-stu-id="a1503-153">Mandatory</span></span> | <span data-ttu-id="a1503-154">Description</span><span class="sxs-lookup"><span data-stu-id="a1503-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a1503-155">ServiceName</span><span class="sxs-lookup"><span data-stu-id="a1503-155">ServiceName</span></span> |<span data-ttu-id="a1503-156">string</span><span class="sxs-lookup"><span data-stu-id="a1503-156">string</span></span> |<span data-ttu-id="a1503-157">No</span><span class="sxs-lookup"><span data-stu-id="a1503-157">No</span></span> |<span data-ttu-id="a1503-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span><span class="sxs-lookup"><span data-stu-id="a1503-158">If a value is provided, then all virtual machines with that service name are started or stopped.</span></span>  <span data-ttu-id="a1503-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span><span class="sxs-lookup"><span data-stu-id="a1503-159">If no value is provided, then all classic virtual machines in the Azure subscription are started or stopped.</span></span> |
| <span data-ttu-id="a1503-160">AzureSubscriptionIdAssetName</span><span class="sxs-lookup"><span data-stu-id="a1503-160">AzureSubscriptionIdAssetName</span></span> |<span data-ttu-id="a1503-161">string</span><span class="sxs-lookup"><span data-stu-id="a1503-161">string</span></span> |<span data-ttu-id="a1503-162">No</span><span class="sxs-lookup"><span data-stu-id="a1503-162">No</span></span> |<span data-ttu-id="a1503-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a1503-163">Contains the name of the [variable asset](#installing-and-configuring-the-scenario) that contains the subscription ID of your Azure subscription.</span></span>  <span data-ttu-id="a1503-164">If you don't specify a value, *AzureSubscriptionId* is used.</span><span class="sxs-lookup"><span data-stu-id="a1503-164">If you don't specify a value, *AzureSubscriptionId* is used.</span></span> |
| <span data-ttu-id="a1503-165">AzureCredentialAssetName</span><span class="sxs-lookup"><span data-stu-id="a1503-165">AzureCredentialAssetName</span></span> |<span data-ttu-id="a1503-166">string</span><span class="sxs-lookup"><span data-stu-id="a1503-166">string</span></span> |<span data-ttu-id="a1503-167">No</span><span class="sxs-lookup"><span data-stu-id="a1503-167">No</span></span> |<span data-ttu-id="a1503-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span><span class="sxs-lookup"><span data-stu-id="a1503-168">Contains the name of the [credential asset](#installing-and-configuring-the-scenario) that contains the credentials for the runbook to use.</span></span>  <span data-ttu-id="a1503-169">If you don't specify a value, *AzureCredential* is used.</span><span class="sxs-lookup"><span data-stu-id="a1503-169">If you don't specify a value, *AzureCredential* is used.</span></span> |

### <a name="starting-the-runbooks"></a><span data-ttu-id="a1503-170">Starting the runbooks</span><span class="sxs-lookup"><span data-stu-id="a1503-170">Starting the runbooks</span></span>
<span data-ttu-id="a1503-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span><span class="sxs-lookup"><span data-stu-id="a1503-171">You can use any of the methods in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md) to start either of the runbooks in this scenario.</span></span>

<span data-ttu-id="a1503-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span><span class="sxs-lookup"><span data-stu-id="a1503-172">The following sample commands uses Windows PowerShell to run **StartAzureVMs** to start all virtual machines with the service name *MyVMService*.</span></span>

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a><span data-ttu-id="a1503-173">Output</span><span class="sxs-lookup"><span data-stu-id="a1503-173">Output</span></span>
<span data-ttu-id="a1503-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span><span class="sxs-lookup"><span data-stu-id="a1503-174">The runbooks will [output a message](automation-runbook-output-and-messages.md) for each virtual machine indicating whether or not the start or stop instruction was successfully submitted.</span></span>  <span data-ttu-id="a1503-175">You can look for a specific string in the output to determine the result for each runbook.</span><span class="sxs-lookup"><span data-stu-id="a1503-175">You can look for a specific string in the output to determine the result for each runbook.</span></span>  <span data-ttu-id="a1503-176">The possible output strings are listed in the following table.</span><span class="sxs-lookup"><span data-stu-id="a1503-176">The possible output strings are listed in the following table.</span></span>

| <span data-ttu-id="a1503-177">Runbook</span><span class="sxs-lookup"><span data-stu-id="a1503-177">Runbook</span></span> | <span data-ttu-id="a1503-178">Condition</span><span class="sxs-lookup"><span data-stu-id="a1503-178">Condition</span></span> | <span data-ttu-id="a1503-179">Message</span><span class="sxs-lookup"><span data-stu-id="a1503-179">Message</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a1503-180">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a1503-180">Start-AzureVMs</span></span> |<span data-ttu-id="a1503-181">Virtual machine is already running</span><span class="sxs-lookup"><span data-stu-id="a1503-181">Virtual machine is already running</span></span> |<span data-ttu-id="a1503-182">MyVM is already running</span><span class="sxs-lookup"><span data-stu-id="a1503-182">MyVM is already running</span></span> |
| <span data-ttu-id="a1503-183">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a1503-183">Start-AzureVMs</span></span> |<span data-ttu-id="a1503-184">Start request for virtual machine successfully submitted</span><span class="sxs-lookup"><span data-stu-id="a1503-184">Start request for virtual machine successfully submitted</span></span> |<span data-ttu-id="a1503-185">MyVM has been started</span><span class="sxs-lookup"><span data-stu-id="a1503-185">MyVM has been started</span></span> |
| <span data-ttu-id="a1503-186">Start-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a1503-186">Start-AzureVMs</span></span> |<span data-ttu-id="a1503-187">Start request for virtual machine failed</span><span class="sxs-lookup"><span data-stu-id="a1503-187">Start request for virtual machine failed</span></span> |<span data-ttu-id="a1503-188">MyVM failed to start</span><span class="sxs-lookup"><span data-stu-id="a1503-188">MyVM failed to start</span></span> |
| <span data-ttu-id="a1503-189">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a1503-189">Stop-AzureVMs</span></span> |<span data-ttu-id="a1503-190">Virtual machine is already stopped</span><span class="sxs-lookup"><span data-stu-id="a1503-190">Virtual machine is already stopped</span></span> |<span data-ttu-id="a1503-191">MyVM is already stopped</span><span class="sxs-lookup"><span data-stu-id="a1503-191">MyVM is already stopped</span></span> |
| <span data-ttu-id="a1503-192">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a1503-192">Stop-AzureVMs</span></span> |<span data-ttu-id="a1503-193">Stop request for virtual machine successfully submitted</span><span class="sxs-lookup"><span data-stu-id="a1503-193">Stop request for virtual machine successfully submitted</span></span> |<span data-ttu-id="a1503-194">MyVM has been stopped</span><span class="sxs-lookup"><span data-stu-id="a1503-194">MyVM has been stopped</span></span> |
| <span data-ttu-id="a1503-195">Stop-AzureVMs</span><span class="sxs-lookup"><span data-stu-id="a1503-195">Stop-AzureVMs</span></span> |<span data-ttu-id="a1503-196">Stop request for virtual machine failed</span><span class="sxs-lookup"><span data-stu-id="a1503-196">Stop request for virtual machine failed</span></span> |<span data-ttu-id="a1503-197">MyVM failed to stop</span><span class="sxs-lookup"><span data-stu-id="a1503-197">MyVM failed to stop</span></span> |

<span data-ttu-id="a1503-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span><span class="sxs-lookup"><span data-stu-id="a1503-198">For example, the following code snippet from a runbook attempts to start all virtual machines with the service name *MyServiceName*.</span></span>  <span data-ttu-id="a1503-199">If any of the start requests fail, then error actions can be taken.</span><span class="sxs-lookup"><span data-stu-id="a1503-199">If any of the start requests fail, then error actions can be taken.</span></span>

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a><span data-ttu-id="a1503-200">Detailed breakdown</span><span class="sxs-lookup"><span data-stu-id="a1503-200">Detailed breakdown</span></span>
<span data-ttu-id="a1503-201">Following is a detailed breakdown of the runbooks in this scenario.</span><span class="sxs-lookup"><span data-stu-id="a1503-201">Following is a detailed breakdown of the runbooks in this scenario.</span></span>  <span data-ttu-id="a1503-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span><span class="sxs-lookup"><span data-stu-id="a1503-202">You can use this information to either customize the runbooks or just to learn from them for authoring your own automation scenarios.</span></span>

### <a name="parameters"></a><span data-ttu-id="a1503-203">Parameters</span><span class="sxs-lookup"><span data-stu-id="a1503-203">Parameters</span></span>
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

<span data-ttu-id="a1503-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span><span class="sxs-lookup"><span data-stu-id="a1503-204">The workflow starts by getting the values for the [input parameters](#using-the-scenario).</span></span>  <span data-ttu-id="a1503-205">If the asset names are not provided then default names are used.</span><span class="sxs-lookup"><span data-stu-id="a1503-205">If the asset names are not provided then default names are used.</span></span>

### <a name="output"></a><span data-ttu-id="a1503-206">Output</span><span class="sxs-lookup"><span data-stu-id="a1503-206">Output</span></span>
    # Returns strings with status messages
    [OutputType([String])]

<span data-ttu-id="a1503-207">This line declares that the output of the runbook will be a string.</span><span class="sxs-lookup"><span data-stu-id="a1503-207">This line declares that the output of the runbook will be a string.</span></span>  <span data-ttu-id="a1503-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span><span class="sxs-lookup"><span data-stu-id="a1503-208">This is not required but is a best practice for when the runbook is used as a [child runbook](automation-child-runbooks.md) so that a parent runbook will know the output type to expect.</span></span>

### <a name="authentication"></a><span data-ttu-id="a1503-209">Authentication</span><span class="sxs-lookup"><span data-stu-id="a1503-209">Authentication</span></span>
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

<span data-ttu-id="a1503-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span><span class="sxs-lookup"><span data-stu-id="a1503-210">The next lines set the [credentials](automation-credentials.md) and Azure subscription that will be used for the rest of the runbook.</span></span>
<span data-ttu-id="a1503-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a1503-211">First we use **Get-AutomationPSCredential** to get the asset that holds the credentials with access to start and stop virtual machines in the Azure subscription.</span></span> <span data-ttu-id="a1503-212">**Add-AzureAccount** then uses this asset to set the credentials.</span><span class="sxs-lookup"><span data-stu-id="a1503-212">**Add-AzureAccount** then uses this asset to set the credentials.</span></span>  <span data-ttu-id="a1503-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span><span class="sxs-lookup"><span data-stu-id="a1503-213">The output is assigned to a dummy variable so that it isn't included in the runbook output.</span></span>  

<span data-ttu-id="a1503-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="a1503-214">The variable asset with the subscription ID is then retrieved with **Get-AutomationVariable** and the subscription set with **Select-AzureSubscription**.</span></span>

### <a name="get-vms"></a><span data-ttu-id="a1503-215">Get VMs</span><span class="sxs-lookup"><span data-stu-id="a1503-215">Get VMs</span></span>
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

<span data-ttu-id="a1503-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span><span class="sxs-lookup"><span data-stu-id="a1503-216">**Get-AzureVM** is used to retrieve the virtual machines the runbook will work with.</span></span>  <span data-ttu-id="a1503-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span><span class="sxs-lookup"><span data-stu-id="a1503-217">If a value is provided in the **ServiceName** input variable, then only the virtual machines with that service name are retrieved.</span></span>  <span data-ttu-id="a1503-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span><span class="sxs-lookup"><span data-stu-id="a1503-218">If **ServiceName** is empty, then all virtual machines are retrieved.</span></span>

### <a name="startstop-virtual-machines-and-send-output"></a><span data-ttu-id="a1503-219">Start/Stop virtual machines and send output</span><span class="sxs-lookup"><span data-stu-id="a1503-219">Start/Stop virtual machines and send output</span></span>
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

<span data-ttu-id="a1503-220">The next lines step through each virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a1503-220">The next lines step through each virtual machine.</span></span>  <span data-ttu-id="a1503-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span><span class="sxs-lookup"><span data-stu-id="a1503-221">First the **PowerState** of the virtual machine is checked to see if it is already running or stopped, depending on the runbook.</span></span>  <span data-ttu-id="a1503-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span><span class="sxs-lookup"><span data-stu-id="a1503-222">If it is already in the target state, then a message is sent to output, and the runbook ends.</span></span>  <span data-ttu-id="a1503-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span><span class="sxs-lookup"><span data-stu-id="a1503-223">If not, then **Start-AzureVM** or **Stop-AzureVM** is used to attempt to start or stop the virtual machine with the result of the request stored to a variable.</span></span>  <span data-ttu-id="a1503-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span><span class="sxs-lookup"><span data-stu-id="a1503-224">A message is then sent to output specifying whether the request to start or stop was submitted successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1503-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1503-225">Next steps</span></span>
* <span data-ttu-id="a1503-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span><span class="sxs-lookup"><span data-stu-id="a1503-226">To learn more about working with child runbooks, see [Child runbooks in Azure Automation](automation-child-runbooks.md)</span></span>
* <span data-ttu-id="a1503-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="a1503-227">To learn more about output messages during runbook execution and logging to help troubleshoot, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

