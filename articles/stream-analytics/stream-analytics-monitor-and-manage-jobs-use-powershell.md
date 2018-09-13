---
title: Monitor and manage Stream Analytics jobs with PowerShell | Microsoft Docs
description: Learn how to use Azure PowerShell and cmdlets to monitor and manage Stream Analytics jobs.
keywords: azure powershell, azure powershell cmdlets, powershell command, powershell scripting
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 96c76944ac5997783136d394020cfb94f30d98f2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549529"
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="2f0db-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="2f0db-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="2f0db-105">Learn how to monitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span><span class="sxs-lookup"><span data-stu-id="2f0db-105">Learn how to monitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="2f0db-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f0db-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="2f0db-107">Create an Azure Resource Group in your subscription.</span><span class="sxs-lookup"><span data-stu-id="2f0db-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="2f0db-108">The following is a sample Azure PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="2f0db-108">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="2f0db-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs);</span><span class="sxs-lookup"><span data-stu-id="2f0db-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs);</span></span>  

<span data-ttu-id="2f0db-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="2f0db-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-111">Azure PowerShell 1.0:</span></span>  

         # Log in to your Azure account
        Login-AzureRmAccount

        # Select the Azure subscription you want to use to create the resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered to the subscription, remove remark symbol below (#) to run the Register-AzureProvider cmdlet to register the provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="2f0db-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span><span class="sxs-lookup"><span data-stu-id="2f0db-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="2f0db-113">You can manually enable monitoring in the Azure Portal by navigating to the job’s Monitor page and clicking the Enable button or you can do this programmatically by following the steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="2f0db-113">You can manually enable monitoring in the Azure Portal by navigating to the job’s Monitor page and clicking the Enable button or you can do this programmatically by following the steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="2f0db-114">Azure PowerShell cmdlets for Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f0db-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="2f0db-115">The following Azure PowerShell cmdlets can be used to monitor and manage Azure Stream Analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="2f0db-115">The following Azure PowerShell cmdlets can be used to monitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="2f0db-116">Note that Azure PowerShell has different versions.</span><span class="sxs-lookup"><span data-stu-id="2f0db-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="2f0db-117">**In the examples listed the first command is for Azure PowerShell 0.9.8, the second command is for Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="2f0db-117">**In the examples listed the first command is for Azure PowerShell 0.9.8, the second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="2f0db-118">The Azure PowerShell 1.0 commands will always have "AzureRM" in the command.</span><span class="sxs-lookup"><span data-stu-id="2f0db-118">The Azure PowerShell 1.0 commands will always have "AzureRM" in the command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="2f0db-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="2f0db-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="2f0db-120">Lists all Stream Analytics jobs defined in the Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span><span class="sxs-lookup"><span data-stu-id="2f0db-120">Lists all Stream Analytics jobs defined in the Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="2f0db-121">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-121">**Example 1**</span></span>

<span data-ttu-id="2f0db-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="2f0db-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="2f0db-124">This PowerShell command returns information about all the Stream Analytics jobs in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="2f0db-124">This PowerShell command returns information about all the Stream Analytics jobs in the Azure subscription.</span></span>

<span data-ttu-id="2f0db-125">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="2f0db-125">**Example 2**</span></span>

<span data-ttu-id="2f0db-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="2f0db-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="2f0db-128">This PowerShell command returns information about all the Stream Analytics jobs in the resource group StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="2f0db-128">This PowerShell command returns information about all the Stream Analytics jobs in the resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="2f0db-129">**Example 3**</span><span class="sxs-lookup"><span data-stu-id="2f0db-129">**Example 3**</span></span>

<span data-ttu-id="2f0db-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="2f0db-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="2f0db-132">This PowerShell command returns information about the Stream Analytics job StreamingJob in the resource group StreamAnalytics-Default-Central-US.</span><span class="sxs-lookup"><span data-stu-id="2f0db-132">This PowerShell command returns information about the Stream Analytics job StreamingJob in the resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="2f0db-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="2f0db-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="2f0db-134">Lists all of the inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span><span class="sxs-lookup"><span data-stu-id="2f0db-134">Lists all of the inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="2f0db-135">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-135">**Example 1**</span></span>

<span data-ttu-id="2f0db-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="2f0db-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="2f0db-138">This PowerShell command returns information about all the inputs defined in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-138">This PowerShell command returns information about all the inputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="2f0db-139">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="2f0db-139">**Example 2**</span></span>

<span data-ttu-id="2f0db-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="2f0db-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="2f0db-142">This PowerShell command returns information about the input named EntryStream defined in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-142">This PowerShell command returns information about the input named EntryStream defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="2f0db-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="2f0db-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="2f0db-144">Lists all of the outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span><span class="sxs-lookup"><span data-stu-id="2f0db-144">Lists all of the outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="2f0db-145">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-145">**Example 1**</span></span>

<span data-ttu-id="2f0db-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="2f0db-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="2f0db-148">This PowerShell command returns information about the outputs defined in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-148">This PowerShell command returns information about the outputs defined in the job StreamingJob.</span></span>

<span data-ttu-id="2f0db-149">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="2f0db-149">**Example 2**</span></span>

<span data-ttu-id="2f0db-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="2f0db-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="2f0db-152">This PowerShell command returns information about the output named Output defined in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-152">This PowerShell command returns information about the output named Output defined in the job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="2f0db-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="2f0db-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="2f0db-154">Gets information about the quota of streaming units in a specified region.</span><span class="sxs-lookup"><span data-stu-id="2f0db-154">Gets information about the quota of streaming units in a specified region.</span></span>

<span data-ttu-id="2f0db-155">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-155">**Example 1**</span></span>

<span data-ttu-id="2f0db-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="2f0db-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="2f0db-158">This PowerShell command returns information about the quota and usage of streaming units in the Central US region.</span><span class="sxs-lookup"><span data-stu-id="2f0db-158">This PowerShell command returns information about the quota and usage of streaming units in the Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="2f0db-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="2f0db-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="2f0db-160">Gets information about a specific transformation defined in a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="2f0db-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="2f0db-161">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-161">**Example 1**</span></span>

<span data-ttu-id="2f0db-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="2f0db-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="2f0db-164">This PowerShell command returns information about the transformation called StreamingJob in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-164">This PowerShell command returns information about the transformation called StreamingJob in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="2f0db-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="2f0db-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="2f0db-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span><span class="sxs-lookup"><span data-stu-id="2f0db-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="2f0db-167">The name of the input can be specified in the .json file or on the command line.</span><span class="sxs-lookup"><span data-stu-id="2f0db-167">The name of the input can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="2f0db-168">If both are specified, the name on the command line must be the same as the one in the file.</span><span class="sxs-lookup"><span data-stu-id="2f0db-168">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="2f0db-169">If you specify an input that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing input.</span><span class="sxs-lookup"><span data-stu-id="2f0db-169">If you specify an input that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing input.</span></span>

<span data-ttu-id="2f0db-170">If you specify the –Force parameter and specify an existing input name, the input will be replaced without confirmation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-170">If you specify the –Force parameter and specify an existing input name, the input will be replaced without confirmation.</span></span>

<span data-ttu-id="2f0db-171">For detailed information on the JSON file structure and contents, refer to the [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="2f0db-171">For detailed information on the JSON file structure and contents, refer to the [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="2f0db-172">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-172">**Example 1**</span></span>

<span data-ttu-id="2f0db-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="2f0db-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="2f0db-175">This PowerShell command creates a new input from the file Input.json.</span><span class="sxs-lookup"><span data-stu-id="2f0db-175">This PowerShell command creates a new input from the file Input.json.</span></span> <span data-ttu-id="2f0db-176">If an existing input with the name specified in the input definition file is already defined, the cmdlet will ask whether or not to replace it.</span><span class="sxs-lookup"><span data-stu-id="2f0db-176">If an existing input with the name specified in the input definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="2f0db-177">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="2f0db-177">**Example 2**</span></span>

<span data-ttu-id="2f0db-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="2f0db-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="2f0db-180">This PowerShell command creates a new input in the job called EntryStream.</span><span class="sxs-lookup"><span data-stu-id="2f0db-180">This PowerShell command creates a new input in the job called EntryStream.</span></span> <span data-ttu-id="2f0db-181">If an existing input with this name is already defined, the cmdlet will ask whether or not to replace it.</span><span class="sxs-lookup"><span data-stu-id="2f0db-181">If an existing input with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="2f0db-182">**Example 3**</span><span class="sxs-lookup"><span data-stu-id="2f0db-182">**Example 3**</span></span>

<span data-ttu-id="2f0db-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="2f0db-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="2f0db-185">This PowerShell command replaces the definition of the existing input source called EntryStream with the definition from the file.</span><span class="sxs-lookup"><span data-stu-id="2f0db-185">This PowerShell command replaces the definition of the existing input source called EntryStream with the definition from the file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="2f0db-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="2f0db-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="2f0db-187">Creates a new Stream Analytics job in Microsoft Azure, or updates the definition of an existing specified job.</span><span class="sxs-lookup"><span data-stu-id="2f0db-187">Creates a new Stream Analytics job in Microsoft Azure, or updates the definition of an existing specified job.</span></span>

<span data-ttu-id="2f0db-188">The name of the job can be specified in the .json file or on the command line.</span><span class="sxs-lookup"><span data-stu-id="2f0db-188">The name of the job can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="2f0db-189">If both are specified, the name on the command line must be the same as the one in the file.</span><span class="sxs-lookup"><span data-stu-id="2f0db-189">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="2f0db-190">If you specify a job name that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing job.</span><span class="sxs-lookup"><span data-stu-id="2f0db-190">If you specify a job name that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing job.</span></span>

<span data-ttu-id="2f0db-191">If you specify the –Force parameter and specify an existing job name, the job definition will be replaced without confirmation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-191">If you specify the –Force parameter and specify an existing job name, the job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="2f0db-192">For detailed information on the JSON file structure and contents, refer to the [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="2f0db-192">For detailed information on the JSON file structure and contents, refer to the [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="2f0db-193">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-193">**Example 1**</span></span>

<span data-ttu-id="2f0db-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="2f0db-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="2f0db-196">This PowerShell command creates a new job from the definition in JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="2f0db-196">This PowerShell command creates a new job from the definition in JobDefinition.json.</span></span> <span data-ttu-id="2f0db-197">If an existing job with the name specified in the job definition file is already defined, the cmdlet will ask whether or not to replace it.</span><span class="sxs-lookup"><span data-stu-id="2f0db-197">If an existing job with the name specified in the job definition file is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="2f0db-198">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="2f0db-198">**Example 2**</span></span>

<span data-ttu-id="2f0db-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="2f0db-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="2f0db-201">This PowerShell command replaces the job definition for StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-201">This PowerShell command replaces the job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="2f0db-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="2f0db-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="2f0db-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span><span class="sxs-lookup"><span data-stu-id="2f0db-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="2f0db-204">The name of the output can be specified in the .json file or on the command line.</span><span class="sxs-lookup"><span data-stu-id="2f0db-204">The name of the output can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="2f0db-205">If both are specified, the name on the command line must be the same as the one in the file.</span><span class="sxs-lookup"><span data-stu-id="2f0db-205">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="2f0db-206">If you specify an output that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing output.</span><span class="sxs-lookup"><span data-stu-id="2f0db-206">If you specify an output that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing output.</span></span>

<span data-ttu-id="2f0db-207">If you specify the –Force parameter and specify an existing output name, the output will be replaced without confirmation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-207">If you specify the –Force parameter and specify an existing output name, the output will be replaced without confirmation.</span></span>

<span data-ttu-id="2f0db-208">For detailed information on the JSON file structure and contents, refer to the [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="2f0db-208">For detailed information on the JSON file structure and contents, refer to the [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="2f0db-209">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-209">**Example 1**</span></span>

<span data-ttu-id="2f0db-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="2f0db-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="2f0db-212">This PowerShell command creates a new output called "output" in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-212">This PowerShell command creates a new output called "output" in the job StreamingJob.</span></span> <span data-ttu-id="2f0db-213">If an existing output with this name is already defined, the cmdlet will ask whether or not to replace it.</span><span class="sxs-lookup"><span data-stu-id="2f0db-213">If an existing output with this name is already defined, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="2f0db-214">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="2f0db-214">**Example 2**</span></span>

<span data-ttu-id="2f0db-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="2f0db-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="2f0db-217">This PowerShell command replaces the definition for "output" in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-217">This PowerShell command replaces the definition for "output" in the job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="2f0db-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="2f0db-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="2f0db-219">Creates a new transformation within a Stream Analytics job, or updates the existing transformation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-219">Creates a new transformation within a Stream Analytics job, or updates the existing transformation.</span></span>

<span data-ttu-id="2f0db-220">The name of the transformation can be specified in the .json file or on the command line.</span><span class="sxs-lookup"><span data-stu-id="2f0db-220">The name of the transformation can be specified in the .json file or on the command line.</span></span> <span data-ttu-id="2f0db-221">If both are specified, the name on the command line must be the same as the one in the file.</span><span class="sxs-lookup"><span data-stu-id="2f0db-221">If both are specified, the name on the command line must be the same as the one in the file.</span></span>

<span data-ttu-id="2f0db-222">If you specify a transformation that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing transformation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-222">If you specify a transformation that already exists and do not specify the –Force parameter, the cmdlet will ask whether or not to replace the existing transformation.</span></span>

<span data-ttu-id="2f0db-223">If you specify the –Force parameter and specify an existing transformation name, the transformation will be replaced without confirmation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-223">If you specify the –Force parameter and specify an existing transformation name, the transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="2f0db-224">For detailed information on the JSON file structure and contents, refer to the [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="2f0db-224">For detailed information on the JSON file structure and contents, refer to the [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of the [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="2f0db-225">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-225">**Example 1**</span></span>

<span data-ttu-id="2f0db-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="2f0db-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="2f0db-228">This PowerShell command creates a new transformation called StreamingJobTransform in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-228">This PowerShell command creates a new transformation called StreamingJobTransform in the job StreamingJob.</span></span> <span data-ttu-id="2f0db-229">If an existing transformation is already defined with this name, the cmdlet will ask whether or not to replace it.</span><span class="sxs-lookup"><span data-stu-id="2f0db-229">If an existing transformation is already defined with this name, the cmdlet will ask whether or not to replace it.</span></span>

<span data-ttu-id="2f0db-230">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="2f0db-230">**Example 2**</span></span>

<span data-ttu-id="2f0db-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="2f0db-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="2f0db-233">This PowerShell command replaces the definition of StreamingJobTransform in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-233">This PowerShell command replaces the definition of StreamingJobTransform in the job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="2f0db-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="2f0db-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="2f0db-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f0db-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="2f0db-236">If you specify the –Force parameter, the input will be deleted without confirmation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-236">If you specify the –Force parameter, the input will be deleted without confirmation.</span></span>

<span data-ttu-id="2f0db-237">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-237">**Example 1**</span></span>

<span data-ttu-id="2f0db-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="2f0db-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="2f0db-240">This PowerShell command removes the input EventStream in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-240">This PowerShell command removes the input EventStream in the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="2f0db-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="2f0db-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="2f0db-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f0db-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="2f0db-243">If you specify the –Force parameter, the job will be deleted without confirmation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-243">If you specify the –Force parameter, the job will be deleted without confirmation.</span></span>

<span data-ttu-id="2f0db-244">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-244">**Example 1**</span></span>

<span data-ttu-id="2f0db-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="2f0db-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="2f0db-247">This PowerShell command removes the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-247">This PowerShell command removes the job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="2f0db-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="2f0db-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="2f0db-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f0db-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="2f0db-250">If you specify the –Force parameter, the output will be deleted without confirmation.</span><span class="sxs-lookup"><span data-stu-id="2f0db-250">If you specify the –Force parameter, the output will be deleted without confirmation.</span></span>

<span data-ttu-id="2f0db-251">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-251">**Example 1**</span></span>

<span data-ttu-id="2f0db-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="2f0db-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="2f0db-254">This PowerShell command removes the output Output in the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-254">This PowerShell command removes the output Output in the job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="2f0db-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="2f0db-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="2f0db-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f0db-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="2f0db-257">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-257">**Example 1**</span></span>

<span data-ttu-id="2f0db-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="2f0db-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="2f0db-260">This PowerShell command starts the job StreamingJob with a custom output start time set to December 12, 2012, 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="2f0db-260">This PowerShell command starts the job StreamingJob with a custom output start time set to December 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="2f0db-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="2f0db-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="2f0db-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span><span class="sxs-lookup"><span data-stu-id="2f0db-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="2f0db-263">The job definition and metadata will remain available within your subscription through both the Azure portal and management APIs, such that the job can be edited and restarted.</span><span class="sxs-lookup"><span data-stu-id="2f0db-263">The job definition and metadata will remain available within your subscription through both the Azure portal and management APIs, such that the job can be edited and restarted.</span></span> <span data-ttu-id="2f0db-264">You will not be charged for a job in the stopped state.</span><span class="sxs-lookup"><span data-stu-id="2f0db-264">You will not be charged for a job in the stopped state.</span></span>

<span data-ttu-id="2f0db-265">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-265">**Example 1**</span></span>

<span data-ttu-id="2f0db-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="2f0db-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="2f0db-268">This PowerShell command stops the job StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-268">This PowerShell command stops the job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="2f0db-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="2f0db-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="2f0db-270">Tests the ability of Stream Analytics to connect to a specified input.</span><span class="sxs-lookup"><span data-stu-id="2f0db-270">Tests the ability of Stream Analytics to connect to a specified input.</span></span>

<span data-ttu-id="2f0db-271">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-271">**Example 1**</span></span>

<span data-ttu-id="2f0db-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="2f0db-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="2f0db-274">This PowerShell command tests the connection status of the input EntryStream in StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-274">This PowerShell command tests the connection status of the input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="2f0db-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="2f0db-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="2f0db-276">Tests the ability of Stream Analytics to connect to a specified output.</span><span class="sxs-lookup"><span data-stu-id="2f0db-276">Tests the ability of Stream Analytics to connect to a specified output.</span></span>

<span data-ttu-id="2f0db-277">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="2f0db-277">**Example 1**</span></span>

<span data-ttu-id="2f0db-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="2f0db-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="2f0db-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="2f0db-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="2f0db-280">This PowerShell command tests the connection status of the output Output in StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="2f0db-280">This PowerShell command tests the connection status of the output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="2f0db-281">Get support</span><span class="sxs-lookup"><span data-stu-id="2f0db-281">Get support</span></span>
<span data-ttu-id="2f0db-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2f0db-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2f0db-283">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f0db-283">Next steps</span></span>
* [<span data-ttu-id="2f0db-284">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f0db-284">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2f0db-285">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2f0db-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="2f0db-286">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="2f0db-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2f0db-287">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="2f0db-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2f0db-288">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="2f0db-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

