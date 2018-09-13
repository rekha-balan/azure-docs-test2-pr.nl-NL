---
title: Manage Azure Media Services Accounts with PowerShell
description: Learn how to manage Azure Media Services accounts with PowerShell cmdlets.
author: Juliako
manager: erikre
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553337"
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="e458c-103">Manage Azure Media Services Accounts with PowerShell</span><span class="sxs-lookup"><span data-stu-id="e458c-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> To be able to create an Azure Media Services account, you must have an Azure account. If you don't have an account, you can create a free trial account in just a couple of minutes. For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.
> 
> 

## <a name="overview"></a><span data-ttu-id="e458c-110">Overview</span><span class="sxs-lookup"><span data-stu-id="e458c-110">Overview</span></span>
<span data-ttu-id="e458c-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span><span class="sxs-lookup"><span data-stu-id="e458c-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="e458c-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span><span class="sxs-lookup"><span data-stu-id="e458c-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="e458c-113">Versions</span><span class="sxs-lookup"><span data-stu-id="e458c-113">Versions</span></span>
<span data-ttu-id="e458c-114">**ApiVersion**:   "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="e458c-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="e458c-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="e458c-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="e458c-116">Creates a media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="e458c-117">Syntax</span><span class="sxs-lookup"><span data-stu-id="e458c-117">Syntax</span></span>
<span data-ttu-id="e458c-118">Parameter Set: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="e458c-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="e458c-119">Parameter Set: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="e458c-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="e458c-120">Parameters</span><span class="sxs-lookup"><span data-stu-id="e458c-120">Parameters</span></span>
<span data-ttu-id="e458c-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-122">Specifies the name of the resource group to which this media service belongs.</span><span class="sxs-lookup"><span data-stu-id="e458c-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="e458c-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-123">Aliases</span></span> | <span data-ttu-id="e458c-124">none</span><span class="sxs-lookup"><span data-stu-id="e458c-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-125">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-125">Required?</span></span> |<span data-ttu-id="e458c-126">true</span><span class="sxs-lookup"><span data-stu-id="e458c-126">true</span></span> |
| <span data-ttu-id="e458c-127">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-127">Position?</span></span> |<span data-ttu-id="e458c-128">0</span><span class="sxs-lookup"><span data-stu-id="e458c-128">0</span></span> |
| <span data-ttu-id="e458c-129">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-129">Default value</span></span> |<span data-ttu-id="e458c-130">none</span><span class="sxs-lookup"><span data-stu-id="e458c-130">none</span></span> |
| <span data-ttu-id="e458c-131">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-131">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-133">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-133">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-134">false</span><span class="sxs-lookup"><span data-stu-id="e458c-134">false</span></span> |

<span data-ttu-id="e458c-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-136">Specifies the name of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="e458c-137">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-137">Aliases</span></span> | <span data-ttu-id="e458c-138">Name</span><span class="sxs-lookup"><span data-stu-id="e458c-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-139">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-139">Required?</span></span> |<span data-ttu-id="e458c-140">true</span><span class="sxs-lookup"><span data-stu-id="e458c-140">true</span></span> |
| <span data-ttu-id="e458c-141">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-141">Position?</span></span> |<span data-ttu-id="e458c-142">1</span><span class="sxs-lookup"><span data-stu-id="e458c-142">1</span></span> |
| <span data-ttu-id="e458c-143">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-143">Default value</span></span> |<span data-ttu-id="e458c-144">none</span><span class="sxs-lookup"><span data-stu-id="e458c-144">none</span></span> |
| <span data-ttu-id="e458c-145">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-145">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-146">false</span><span class="sxs-lookup"><span data-stu-id="e458c-146">false</span></span> |
| <span data-ttu-id="e458c-147">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-147">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-148">false</span><span class="sxs-lookup"><span data-stu-id="e458c-148">false</span></span> |

<span data-ttu-id="e458c-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-150">Specifies the resource location of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="e458c-151">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-151">Aliases</span></span> | <span data-ttu-id="e458c-152">none</span><span class="sxs-lookup"><span data-stu-id="e458c-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-153">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-153">Required?</span></span> |<span data-ttu-id="e458c-154">true</span><span class="sxs-lookup"><span data-stu-id="e458c-154">true</span></span> |
| <span data-ttu-id="e458c-155">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-155">Position?</span></span> |<span data-ttu-id="e458c-156">2</span><span class="sxs-lookup"><span data-stu-id="e458c-156">2</span></span> |
| <span data-ttu-id="e458c-157">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-157">Default value</span></span> |<span data-ttu-id="e458c-158">none</span><span class="sxs-lookup"><span data-stu-id="e458c-158">none</span></span> |
| <span data-ttu-id="e458c-159">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-159">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-161">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-161">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-162">false</span><span class="sxs-lookup"><span data-stu-id="e458c-162">false</span></span> |

<span data-ttu-id="e458c-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-164">Specifies a primary storage account that associated with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="e458c-165">New storage account (created with the Resource Manager API) supported only.</span><span class="sxs-lookup"><span data-stu-id="e458c-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="e458c-166">The storage account must exist and has the same location with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="e458c-167">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-167">Aliases</span></span> | <span data-ttu-id="e458c-168">none</span><span class="sxs-lookup"><span data-stu-id="e458c-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-169">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-169">Required?</span></span> |<span data-ttu-id="e458c-170">true</span><span class="sxs-lookup"><span data-stu-id="e458c-170">true</span></span> |
| <span data-ttu-id="e458c-171">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-171">Position?</span></span> |<span data-ttu-id="e458c-172">3</span><span class="sxs-lookup"><span data-stu-id="e458c-172">3</span></span> |
| <span data-ttu-id="e458c-173">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-173">Default value</span></span> |<span data-ttu-id="e458c-174">none</span><span class="sxs-lookup"><span data-stu-id="e458c-174">none</span></span> |
| <span data-ttu-id="e458c-175">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-175">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-177">Parameter set name</span><span class="sxs-lookup"><span data-stu-id="e458c-177">Parameter set name</span></span> |<span data-ttu-id="e458c-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="e458c-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="e458c-179">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-179">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-180">false</span><span class="sxs-lookup"><span data-stu-id="e458c-180">false</span></span> |

<span data-ttu-id="e458c-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="e458c-182">Specifies storage accounts that associated with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="e458c-183">New storage account (created with the Resource Manager API) supported only.</span><span class="sxs-lookup"><span data-stu-id="e458c-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="e458c-184">The storage account must exist and has the same location with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="e458c-185">Only one storage account can be specified as primary.</span><span class="sxs-lookup"><span data-stu-id="e458c-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="e458c-186">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-186">Aliases</span></span> | <span data-ttu-id="e458c-187">none</span><span class="sxs-lookup"><span data-stu-id="e458c-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-188">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-188">Required?</span></span> |<span data-ttu-id="e458c-189">true</span><span class="sxs-lookup"><span data-stu-id="e458c-189">true</span></span> |
| <span data-ttu-id="e458c-190">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-190">Position?</span></span> |<span data-ttu-id="e458c-191">3</span><span class="sxs-lookup"><span data-stu-id="e458c-191">3</span></span> |
| <span data-ttu-id="e458c-192">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-192">Default value</span></span> |<span data-ttu-id="e458c-193">none</span><span class="sxs-lookup"><span data-stu-id="e458c-193">none</span></span> |
| <span data-ttu-id="e458c-194">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-194">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-196">Parameter set name</span><span class="sxs-lookup"><span data-stu-id="e458c-196">Parameter set name</span></span> |<span data-ttu-id="e458c-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="e458c-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="e458c-198">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-198">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-199">false</span><span class="sxs-lookup"><span data-stu-id="e458c-199">false</span></span> |

<span data-ttu-id="e458c-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="e458c-201">Specifies a hash table of the tags that are associated with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="e458c-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span><span class="sxs-lookup"><span data-stu-id="e458c-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="e458c-203">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-203">Aliases</span></span> | <span data-ttu-id="e458c-204">none</span><span class="sxs-lookup"><span data-stu-id="e458c-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-205">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-205">Required?</span></span> |<span data-ttu-id="e458c-206">false</span><span class="sxs-lookup"><span data-stu-id="e458c-206">false</span></span> |
| <span data-ttu-id="e458c-207">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-207">Position?</span></span> |<span data-ttu-id="e458c-208">named</span><span class="sxs-lookup"><span data-stu-id="e458c-208">named</span></span> |
| <span data-ttu-id="e458c-209">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-209">Default value</span></span> |<span data-ttu-id="e458c-210">none</span><span class="sxs-lookup"><span data-stu-id="e458c-210">none</span></span> |
| <span data-ttu-id="e458c-211">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-211">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-212">false</span><span class="sxs-lookup"><span data-stu-id="e458c-212">false</span></span> |
| <span data-ttu-id="e458c-213">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-213">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-214">false</span><span class="sxs-lookup"><span data-stu-id="e458c-214">false</span></span> |

<span data-ttu-id="e458c-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="e458c-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e458c-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="e458c-217">Inputs</span><span class="sxs-lookup"><span data-stu-id="e458c-217">Inputs</span></span>
<span data-ttu-id="e458c-218">The input type is the type of the objects that you can pipe to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e458c-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="e458c-219">Outputs</span><span class="sxs-lookup"><span data-stu-id="e458c-219">Outputs</span></span>
<span data-ttu-id="e458c-220">The output type is the type of the objects that the cmdlet emits.</span><span class="sxs-lookup"><span data-stu-id="e458c-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="e458c-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="e458c-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="e458c-222">Updates a media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="e458c-223">Syntax</span><span class="sxs-lookup"><span data-stu-id="e458c-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="e458c-224">Parameters</span><span class="sxs-lookup"><span data-stu-id="e458c-224">Parameters</span></span>
<span data-ttu-id="e458c-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-226">Specifies the name of the resource group to which this media service belongs.</span><span class="sxs-lookup"><span data-stu-id="e458c-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="e458c-227">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-227">Aliases</span></span> | <span data-ttu-id="e458c-228">none</span><span class="sxs-lookup"><span data-stu-id="e458c-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-229">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-229">Required?</span></span> |<span data-ttu-id="e458c-230">true</span><span class="sxs-lookup"><span data-stu-id="e458c-230">true</span></span> |
| <span data-ttu-id="e458c-231">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-231">Position?</span></span> |<span data-ttu-id="e458c-232">0</span><span class="sxs-lookup"><span data-stu-id="e458c-232">0</span></span> |
| <span data-ttu-id="e458c-233">Default Value</span><span class="sxs-lookup"><span data-stu-id="e458c-233">Default Value</span></span> |<span data-ttu-id="e458c-234">none</span><span class="sxs-lookup"><span data-stu-id="e458c-234">none</span></span> |
| <span data-ttu-id="e458c-235">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="e458c-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="e458c-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-237">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-237">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-238">false</span><span class="sxs-lookup"><span data-stu-id="e458c-238">false</span></span> |

<span data-ttu-id="e458c-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-240">Specifies the name of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="e458c-241">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-241">Aliases</span></span> | <span data-ttu-id="e458c-242">Name</span><span class="sxs-lookup"><span data-stu-id="e458c-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-243">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-243">Required?</span></span> |<span data-ttu-id="e458c-244">True</span><span class="sxs-lookup"><span data-stu-id="e458c-244">True</span></span> |
| <span data-ttu-id="e458c-245">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-245">Position?</span></span> |<span data-ttu-id="e458c-246">1</span><span class="sxs-lookup"><span data-stu-id="e458c-246">1</span></span> |
| <span data-ttu-id="e458c-247">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-247">Default value</span></span> |<span data-ttu-id="e458c-248">None</span><span class="sxs-lookup"><span data-stu-id="e458c-248">None</span></span> |
| <span data-ttu-id="e458c-249">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-249">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-251">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-251">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-252">False</span><span class="sxs-lookup"><span data-stu-id="e458c-252">False</span></span> |

<span data-ttu-id="e458c-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="e458c-254">Specifies storage accounts that associated with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="e458c-255">New storage account (created with the Resource Manager API) supported only.</span><span class="sxs-lookup"><span data-stu-id="e458c-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="e458c-256">The storage account must exist and has the same location with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="e458c-257">Only one storage account can be specified as primary.</span><span class="sxs-lookup"><span data-stu-id="e458c-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="e458c-258">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-258">Aliases</span></span> | <span data-ttu-id="e458c-259">none</span><span class="sxs-lookup"><span data-stu-id="e458c-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-260">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-260">Required?</span></span> |<span data-ttu-id="e458c-261">false</span><span class="sxs-lookup"><span data-stu-id="e458c-261">false</span></span> |
| <span data-ttu-id="e458c-262">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-262">Position?</span></span> |<span data-ttu-id="e458c-263">Named</span><span class="sxs-lookup"><span data-stu-id="e458c-263">Named</span></span> |
| <span data-ttu-id="e458c-264">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-264">Default value</span></span> |<span data-ttu-id="e458c-265">none</span><span class="sxs-lookup"><span data-stu-id="e458c-265">none</span></span> |
| <span data-ttu-id="e458c-266">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-266">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-268">Parameter set name</span><span class="sxs-lookup"><span data-stu-id="e458c-268">Parameter set name</span></span> |<span data-ttu-id="e458c-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="e458c-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="e458c-270">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-270">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-271">false</span><span class="sxs-lookup"><span data-stu-id="e458c-271">false</span></span> |

<span data-ttu-id="e458c-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="e458c-273">Specifies a hash table of the tags that are associated with this media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="e458c-274">The tags that are associated with the media service are replaced with value specified by the customer.</span><span class="sxs-lookup"><span data-stu-id="e458c-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="e458c-275">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-275">Aliases</span></span> | <span data-ttu-id="e458c-276">none</span><span class="sxs-lookup"><span data-stu-id="e458c-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-277">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-277">Required?</span></span> |<span data-ttu-id="e458c-278">False</span><span class="sxs-lookup"><span data-stu-id="e458c-278">False</span></span> |
| <span data-ttu-id="e458c-279">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-279">Position?</span></span> |<span data-ttu-id="e458c-280">Named</span><span class="sxs-lookup"><span data-stu-id="e458c-280">Named</span></span> |
| <span data-ttu-id="e458c-281">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-281">Default value</span></span> |<span data-ttu-id="e458c-282">None</span><span class="sxs-lookup"><span data-stu-id="e458c-282">None</span></span> |
| <span data-ttu-id="e458c-283">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-283">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-285">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-285">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-286">false</span><span class="sxs-lookup"><span data-stu-id="e458c-286">false</span></span> |

<span data-ttu-id="e458c-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="e458c-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e458c-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="e458c-289">Inputs</span><span class="sxs-lookup"><span data-stu-id="e458c-289">Inputs</span></span>
<span data-ttu-id="e458c-290">The input type is the type of the objects that you can pipe to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e458c-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="e458c-291">Outputs</span><span class="sxs-lookup"><span data-stu-id="e458c-291">Outputs</span></span>
<span data-ttu-id="e458c-292">The output type is the type of the objects that the cmdlet emits.</span><span class="sxs-lookup"><span data-stu-id="e458c-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="e458c-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="e458c-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="e458c-294">Removes a media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="e458c-295">Syntax</span><span class="sxs-lookup"><span data-stu-id="e458c-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="e458c-296">Parameters</span><span class="sxs-lookup"><span data-stu-id="e458c-296">Parameters</span></span>
<span data-ttu-id="e458c-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-298">Specifies the name of the resource group to which this media service belongs.</span><span class="sxs-lookup"><span data-stu-id="e458c-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="e458c-299">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-299">Aliases</span></span> | <span data-ttu-id="e458c-300">none</span><span class="sxs-lookup"><span data-stu-id="e458c-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-301">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-301">Required?</span></span> |<span data-ttu-id="e458c-302">true</span><span class="sxs-lookup"><span data-stu-id="e458c-302">true</span></span> |
| <span data-ttu-id="e458c-303">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-303">Position?</span></span> |<span data-ttu-id="e458c-304">0</span><span class="sxs-lookup"><span data-stu-id="e458c-304">0</span></span> |
| <span data-ttu-id="e458c-305">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-305">Default value</span></span> |<span data-ttu-id="e458c-306">none</span><span class="sxs-lookup"><span data-stu-id="e458c-306">none</span></span> |
| <span data-ttu-id="e458c-307">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-307">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-309">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-309">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-310">false</span><span class="sxs-lookup"><span data-stu-id="e458c-310">false</span></span> |

<span data-ttu-id="e458c-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-312">Specifies the name of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="e458c-313">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-313">Aliases</span></span> | <span data-ttu-id="e458c-314">none</span><span class="sxs-lookup"><span data-stu-id="e458c-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-315">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-315">Required?</span></span> |<span data-ttu-id="e458c-316">true</span><span class="sxs-lookup"><span data-stu-id="e458c-316">true</span></span> |
| <span data-ttu-id="e458c-317">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-317">Position?</span></span> |<span data-ttu-id="e458c-318">2</span><span class="sxs-lookup"><span data-stu-id="e458c-318">2</span></span> |
| <span data-ttu-id="e458c-319">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-319">Default value</span></span> |<span data-ttu-id="e458c-320">None</span><span class="sxs-lookup"><span data-stu-id="e458c-320">None</span></span> |
| <span data-ttu-id="e458c-321">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-321">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-323">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-323">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-324">False</span><span class="sxs-lookup"><span data-stu-id="e458c-324">False</span></span> |

<span data-ttu-id="e458c-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="e458c-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e458c-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="e458c-327">Inputs</span><span class="sxs-lookup"><span data-stu-id="e458c-327">Inputs</span></span>
<span data-ttu-id="e458c-328">The input type is the type of the objects that you can pipe to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e458c-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="e458c-329">Outputs</span><span class="sxs-lookup"><span data-stu-id="e458c-329">Outputs</span></span>
<span data-ttu-id="e458c-330">The output type is the type of the objects that the cmdlet emits.</span><span class="sxs-lookup"><span data-stu-id="e458c-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="e458c-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="e458c-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="e458c-332">Gets all media services in a resource group or a media service with a given name.</span><span class="sxs-lookup"><span data-stu-id="e458c-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="e458c-333">Syntax</span><span class="sxs-lookup"><span data-stu-id="e458c-333">Syntax</span></span>
<span data-ttu-id="e458c-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="e458c-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="e458c-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="e458c-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="e458c-336">Parameters</span><span class="sxs-lookup"><span data-stu-id="e458c-336">Parameters</span></span>
<span data-ttu-id="e458c-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-338">Specifies the name of the resource group to which this media service belongs.</span><span class="sxs-lookup"><span data-stu-id="e458c-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="e458c-339">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-339">Aliases</span></span> | <span data-ttu-id="e458c-340">none</span><span class="sxs-lookup"><span data-stu-id="e458c-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-341">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-341">Required?</span></span> |<span data-ttu-id="e458c-342">true</span><span class="sxs-lookup"><span data-stu-id="e458c-342">true</span></span> |
| <span data-ttu-id="e458c-343">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-343">Position?</span></span> |<span data-ttu-id="e458c-344">0</span><span class="sxs-lookup"><span data-stu-id="e458c-344">0</span></span> |
| <span data-ttu-id="e458c-345">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-345">Default value</span></span> |<span data-ttu-id="e458c-346">none</span><span class="sxs-lookup"><span data-stu-id="e458c-346">none</span></span> |
| <span data-ttu-id="e458c-347">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-347">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-349">Parameter set name</span><span class="sxs-lookup"><span data-stu-id="e458c-349">Parameter set name</span></span> |<span data-ttu-id="e458c-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="e458c-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="e458c-351">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-351">Accept wildcard characters?</span></span>   <span data-ttu-id="e458c-352">false</span><span class="sxs-lookup"><span data-stu-id="e458c-352">false</span></span>

<span data-ttu-id="e458c-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-354">Specifies the name of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="e458c-355">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-355">Aliases</span></span> | <span data-ttu-id="e458c-356">none</span><span class="sxs-lookup"><span data-stu-id="e458c-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-357">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-357">Required?</span></span> |<span data-ttu-id="e458c-358">true</span><span class="sxs-lookup"><span data-stu-id="e458c-358">true</span></span> |
| <span data-ttu-id="e458c-359">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-359">Position?</span></span> |<span data-ttu-id="e458c-360">1</span><span class="sxs-lookup"><span data-stu-id="e458c-360">1</span></span> |
| <span data-ttu-id="e458c-361">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-361">Default value</span></span> |<span data-ttu-id="e458c-362">none</span><span class="sxs-lookup"><span data-stu-id="e458c-362">none</span></span> |
| <span data-ttu-id="e458c-363">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-363">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-365">Parameter set name</span><span class="sxs-lookup"><span data-stu-id="e458c-365">Parameter set name</span></span> |<span data-ttu-id="e458c-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="e458c-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="e458c-367">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-367">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-368">false</span><span class="sxs-lookup"><span data-stu-id="e458c-368">false</span></span> |

<span data-ttu-id="e458c-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="e458c-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e458c-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="e458c-371">Inputs</span><span class="sxs-lookup"><span data-stu-id="e458c-371">Inputs</span></span>
<span data-ttu-id="e458c-372">The input type is the type of the objects that you can pipe to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e458c-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="e458c-373">Outputs</span><span class="sxs-lookup"><span data-stu-id="e458c-373">Outputs</span></span>
<span data-ttu-id="e458c-374">The output type is the type of the objects that the cmdlet emits.</span><span class="sxs-lookup"><span data-stu-id="e458c-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="e458c-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="e458c-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="e458c-376">Gets keys of a media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="e458c-377">Syntax</span><span class="sxs-lookup"><span data-stu-id="e458c-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="e458c-378">Parameters</span><span class="sxs-lookup"><span data-stu-id="e458c-378">Parameters</span></span>
<span data-ttu-id="e458c-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-380">Specifies the name of the resource group to which this media service belongs.</span><span class="sxs-lookup"><span data-stu-id="e458c-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="e458c-381">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-381">Aliases</span></span> | <span data-ttu-id="e458c-382">none</span><span class="sxs-lookup"><span data-stu-id="e458c-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-383">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-383">Required?</span></span> |<span data-ttu-id="e458c-384">true</span><span class="sxs-lookup"><span data-stu-id="e458c-384">true</span></span> |
| <span data-ttu-id="e458c-385">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-385">Position?</span></span> |<span data-ttu-id="e458c-386">0</span><span class="sxs-lookup"><span data-stu-id="e458c-386">0</span></span> |
| <span data-ttu-id="e458c-387">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-387">Default value</span></span> |<span data-ttu-id="e458c-388">none</span><span class="sxs-lookup"><span data-stu-id="e458c-388">none</span></span> |
| <span data-ttu-id="e458c-389">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-389">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-391">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-391">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-392">false</span><span class="sxs-lookup"><span data-stu-id="e458c-392">false</span></span> |

<span data-ttu-id="e458c-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-394">Specifies the name of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="e458c-395">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-395">Aliases</span></span> | <span data-ttu-id="e458c-396">none</span><span class="sxs-lookup"><span data-stu-id="e458c-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-397">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-397">Required?</span></span> |<span data-ttu-id="e458c-398">true</span><span class="sxs-lookup"><span data-stu-id="e458c-398">true</span></span> |
| <span data-ttu-id="e458c-399">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-399">Position?</span></span> |<span data-ttu-id="e458c-400">1</span><span class="sxs-lookup"><span data-stu-id="e458c-400">1</span></span> |
| <span data-ttu-id="e458c-401">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-401">Default value</span></span> |<span data-ttu-id="e458c-402">none</span><span class="sxs-lookup"><span data-stu-id="e458c-402">none</span></span> |
| <span data-ttu-id="e458c-403">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-403">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-405">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-405">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-406">false</span><span class="sxs-lookup"><span data-stu-id="e458c-406">false</span></span> |

<span data-ttu-id="e458c-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="e458c-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e458c-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="e458c-409">Inputs</span><span class="sxs-lookup"><span data-stu-id="e458c-409">Inputs</span></span>
<span data-ttu-id="e458c-410">The input type is the type of the objects that you can pipe to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e458c-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="e458c-411">Outputs</span><span class="sxs-lookup"><span data-stu-id="e458c-411">Outputs</span></span>
<span data-ttu-id="e458c-412">The output type is the type of the objects that the cmdlet emits.</span><span class="sxs-lookup"><span data-stu-id="e458c-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="e458c-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="e458c-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="e458c-414">Regenerates a primary or secondary key of a media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="e458c-415">Syntax</span><span class="sxs-lookup"><span data-stu-id="e458c-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="e458c-416">Parameters</span><span class="sxs-lookup"><span data-stu-id="e458c-416">Parameters</span></span>
<span data-ttu-id="e458c-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-418">Specifies the name of the resource group to which this media service belongs.</span><span class="sxs-lookup"><span data-stu-id="e458c-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="e458c-419">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-419">Aliases</span></span> | <span data-ttu-id="e458c-420">none</span><span class="sxs-lookup"><span data-stu-id="e458c-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-421">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-421">Required?</span></span> |<span data-ttu-id="e458c-422">true</span><span class="sxs-lookup"><span data-stu-id="e458c-422">true</span></span> |
| <span data-ttu-id="e458c-423">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-423">Position?</span></span> |<span data-ttu-id="e458c-424">0</span><span class="sxs-lookup"><span data-stu-id="e458c-424">0</span></span> |
| <span data-ttu-id="e458c-425">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-425">Default value</span></span> |<span data-ttu-id="e458c-426">none</span><span class="sxs-lookup"><span data-stu-id="e458c-426">none</span></span> |
| <span data-ttu-id="e458c-427">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-427">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-429">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-429">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-430">false</span><span class="sxs-lookup"><span data-stu-id="e458c-430">false</span></span> |

<span data-ttu-id="e458c-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-432">Specifies the name of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="e458c-433">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-433">Aliases</span></span> | <span data-ttu-id="e458c-434">none</span><span class="sxs-lookup"><span data-stu-id="e458c-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-435">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-435">Required?</span></span> |<span data-ttu-id="e458c-436">true</span><span class="sxs-lookup"><span data-stu-id="e458c-436">true</span></span> |
| <span data-ttu-id="e458c-437">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-437">Position?</span></span> |<span data-ttu-id="e458c-438">1</span><span class="sxs-lookup"><span data-stu-id="e458c-438">1</span></span> |
| <span data-ttu-id="e458c-439">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-439">Default value</span></span> |<span data-ttu-id="e458c-440">none</span><span class="sxs-lookup"><span data-stu-id="e458c-440">none</span></span> |
| <span data-ttu-id="e458c-441">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-441">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-443">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-443">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-444">false</span><span class="sxs-lookup"><span data-stu-id="e458c-444">false</span></span> |

<span data-ttu-id="e458c-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="e458c-446">Specifies the key type of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="e458c-447">Primary or Secondary</span><span class="sxs-lookup"><span data-stu-id="e458c-447">Primary or Secondary</span></span>

| <span data-ttu-id="e458c-448">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-448">Aliases</span></span> | <span data-ttu-id="e458c-449">none</span><span class="sxs-lookup"><span data-stu-id="e458c-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-450">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-450">Required?</span></span> |<span data-ttu-id="e458c-451">true</span><span class="sxs-lookup"><span data-stu-id="e458c-451">true</span></span> |
| <span data-ttu-id="e458c-452">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-452">Position?</span></span> |<span data-ttu-id="e458c-453">2</span><span class="sxs-lookup"><span data-stu-id="e458c-453">2</span></span> |
| <span data-ttu-id="e458c-454">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-454">Default value</span></span> |<span data-ttu-id="e458c-455">none</span><span class="sxs-lookup"><span data-stu-id="e458c-455">none</span></span> |
| <span data-ttu-id="e458c-456">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-456">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-457">false</span><span class="sxs-lookup"><span data-stu-id="e458c-457">false</span></span> |
| <span data-ttu-id="e458c-458">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-458">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-459">false</span><span class="sxs-lookup"><span data-stu-id="e458c-459">false</span></span> |

<span data-ttu-id="e458c-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="e458c-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e458c-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="e458c-462">Inputs</span><span class="sxs-lookup"><span data-stu-id="e458c-462">Inputs</span></span>
<span data-ttu-id="e458c-463">The input type is the type of the objects that you can pipe to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e458c-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="e458c-464">Outputs</span><span class="sxs-lookup"><span data-stu-id="e458c-464">Outputs</span></span>
<span data-ttu-id="e458c-465">The output type is the type of the objects that the cmdlet emits.</span><span class="sxs-lookup"><span data-stu-id="e458c-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="e458c-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="e458c-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="e458c-467">Synchronizes storage account keys for a storage account associated with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="e458c-468">Syntax</span><span class="sxs-lookup"><span data-stu-id="e458c-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="e458c-469">Parameters</span><span class="sxs-lookup"><span data-stu-id="e458c-469">Parameters</span></span>
<span data-ttu-id="e458c-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-471">Specifies the name of the resource group to which this media service belongs.</span><span class="sxs-lookup"><span data-stu-id="e458c-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="e458c-472">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-472">Aliases</span></span> | <span data-ttu-id="e458c-473">none</span><span class="sxs-lookup"><span data-stu-id="e458c-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-474">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-474">Required?</span></span> |<span data-ttu-id="e458c-475">true</span><span class="sxs-lookup"><span data-stu-id="e458c-475">true</span></span> |
| <span data-ttu-id="e458c-476">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-476">Position?</span></span> |<span data-ttu-id="e458c-477">0</span><span class="sxs-lookup"><span data-stu-id="e458c-477">0</span></span> |
| <span data-ttu-id="e458c-478">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-478">Default value</span></span> |<span data-ttu-id="e458c-479">none</span><span class="sxs-lookup"><span data-stu-id="e458c-479">none</span></span> |
| <span data-ttu-id="e458c-480">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-480">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-482">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-482">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-483">false</span><span class="sxs-lookup"><span data-stu-id="e458c-483">false</span></span> |

<span data-ttu-id="e458c-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-485">Specifies the name of the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="e458c-486">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-486">Aliases</span></span> | <span data-ttu-id="e458c-487">none</span><span class="sxs-lookup"><span data-stu-id="e458c-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-488">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-488">Required?</span></span> |<span data-ttu-id="e458c-489">true</span><span class="sxs-lookup"><span data-stu-id="e458c-489">true</span></span> |
| <span data-ttu-id="e458c-490">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-490">Position?</span></span> |<span data-ttu-id="e458c-491">1</span><span class="sxs-lookup"><span data-stu-id="e458c-491">1</span></span> |
| <span data-ttu-id="e458c-492">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-492">Default value</span></span> |<span data-ttu-id="e458c-493">none</span><span class="sxs-lookup"><span data-stu-id="e458c-493">none</span></span> |
| <span data-ttu-id="e458c-494">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-494">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-496">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-496">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-497">false</span><span class="sxs-lookup"><span data-stu-id="e458c-497">false</span></span> |

<span data-ttu-id="e458c-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="e458c-499">Specifies the storage account associated with the media service.</span><span class="sxs-lookup"><span data-stu-id="e458c-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="e458c-500">Aliases</span><span class="sxs-lookup"><span data-stu-id="e458c-500">Aliases</span></span> | <span data-ttu-id="e458c-501">Id</span><span class="sxs-lookup"><span data-stu-id="e458c-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="e458c-502">Required?</span><span class="sxs-lookup"><span data-stu-id="e458c-502">Required?</span></span> |<span data-ttu-id="e458c-503">true</span><span class="sxs-lookup"><span data-stu-id="e458c-503">true</span></span> |
| <span data-ttu-id="e458c-504">Position?</span><span class="sxs-lookup"><span data-stu-id="e458c-504">Position?</span></span> |<span data-ttu-id="e458c-505">2</span><span class="sxs-lookup"><span data-stu-id="e458c-505">2</span></span> |
| <span data-ttu-id="e458c-506">Default value</span><span class="sxs-lookup"><span data-stu-id="e458c-506">Default value</span></span> |<span data-ttu-id="e458c-507">none</span><span class="sxs-lookup"><span data-stu-id="e458c-507">none</span></span> |
| <span data-ttu-id="e458c-508">Accept pipeline input?</span><span class="sxs-lookup"><span data-stu-id="e458c-508">Accept pipeline input?</span></span> |<span data-ttu-id="e458c-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="e458c-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="e458c-510">Accept wildcard characters?</span><span class="sxs-lookup"><span data-stu-id="e458c-510">Accept wildcard characters?</span></span> |<span data-ttu-id="e458c-511">false</span><span class="sxs-lookup"><span data-stu-id="e458c-511">false</span></span> |

<span data-ttu-id="e458c-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="e458c-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="e458c-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e458c-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="e458c-514">Inputs</span><span class="sxs-lookup"><span data-stu-id="e458c-514">Inputs</span></span>
<span data-ttu-id="e458c-515">The input type is the type of the objects that you can pipe to the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e458c-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="e458c-516">Outputs</span><span class="sxs-lookup"><span data-stu-id="e458c-516">Outputs</span></span>
<span data-ttu-id="e458c-517">The output type is the type of the objects that the cmdlet emits.</span><span class="sxs-lookup"><span data-stu-id="e458c-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="e458c-518">Next step</span><span class="sxs-lookup"><span data-stu-id="e458c-518">Next step</span></span>
<span data-ttu-id="e458c-519">Check out Media Services learning paths.</span><span class="sxs-lookup"><span data-stu-id="e458c-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e458c-520">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="e458c-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

