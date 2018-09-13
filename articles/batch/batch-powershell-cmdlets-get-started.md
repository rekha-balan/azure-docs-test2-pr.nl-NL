---
title: Get started with PowerShell for Azure Batch | Microsoft Docs
description: A quick introduction to the Azure PowerShell cmdlets you can use to manage Batch resources.
services: batch
documentationcenter: ''
author: tamram
manager: timlt
editor: ''
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cc8942dacee60d6243e91a3b4360c0c07956fa66
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556193"
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="b868e-103">Manage Batch resources with PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b868e-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="b868e-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="b868e-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="b868e-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span><span class="sxs-lookup"><span data-stu-id="b868e-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="b868e-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](https://msdn.microsoft.com/library/azure/mt125957.aspx).</span><span class="sxs-lookup"><span data-stu-id="b868e-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](https://msdn.microsoft.com/library/azure/mt125957.aspx).</span></span>

<span data-ttu-id="b868e-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="b868e-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="b868e-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span><span class="sxs-lookup"><span data-stu-id="b868e-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b868e-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b868e-109">Prerequisites</span></span>
<span data-ttu-id="b868e-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span><span class="sxs-lookup"><span data-stu-id="b868e-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span></span>

* [<span data-ttu-id="b868e-111">Install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b868e-111">Install and configure Azure PowerShell</span></span>](/powershell/azureps-cmdlets-docs)
* <span data-ttu-id="b868e-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span><span class="sxs-lookup"><span data-stu-id="b868e-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="b868e-113">**Register with the Batch provider namespace**.</span><span class="sxs-lookup"><span data-stu-id="b868e-113">**Register with the Batch provider namespace**.</span></span> <span data-ttu-id="b868e-114">This operation only needs to be performed **once per subscription**.</span><span class="sxs-lookup"><span data-stu-id="b868e-114">This operation only needs to be performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="b868e-115">Manage Batch accounts and keys</span><span class="sxs-lookup"><span data-stu-id="b868e-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="b868e-116">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="b868e-116">Create a Batch account</span></span>
<span data-ttu-id="b868e-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span><span class="sxs-lookup"><span data-stu-id="b868e-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="b868e-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/azure/mt603739.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b868e-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/azure/mt603739.aspx) cmdlet.</span></span> <span data-ttu-id="b868e-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span><span class="sxs-lookup"><span data-stu-id="b868e-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="b868e-120">For example:</span><span class="sxs-lookup"><span data-stu-id="b868e-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="b868e-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="b868e-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span></span> <span data-ttu-id="b868e-122">Creating the Batch account can take some time to complete.</span><span class="sxs-lookup"><span data-stu-id="b868e-122">Creating the Batch account can take some time to complete.</span></span> <span data-ttu-id="b868e-123">For example:</span><span class="sxs-lookup"><span data-stu-id="b868e-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="b868e-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span><span class="sxs-lookup"><span data-stu-id="b868e-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="b868e-125">Get account access keys</span><span class="sxs-lookup"><span data-stu-id="b868e-125">Get account access keys</span></span>
<span data-ttu-id="b868e-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="b868e-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="b868e-127">For example, run the following to get the primary and secondary keys of the account you created.</span><span class="sxs-lookup"><span data-stu-id="b868e-127">For example, run the following to get the primary and secondary keys of the account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="b868e-128">Generate a new access key</span><span class="sxs-lookup"><span data-stu-id="b868e-128">Generate a new access key</span></span>
<span data-ttu-id="b868e-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="b868e-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="b868e-130">For example, to generate a new primary key for your Batch account, type:</span><span class="sxs-lookup"><span data-stu-id="b868e-130">For example, to generate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="b868e-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span><span class="sxs-lookup"><span data-stu-id="b868e-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span></span> <span data-ttu-id="b868e-132">You have to regenerate the primary and secondary keys separately.</span><span class="sxs-lookup"><span data-stu-id="b868e-132">You have to regenerate the primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="b868e-133">Delete a Batch account</span><span class="sxs-lookup"><span data-stu-id="b868e-133">Delete a Batch account</span></span>
<span data-ttu-id="b868e-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span><span class="sxs-lookup"><span data-stu-id="b868e-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="b868e-135">For example:</span><span class="sxs-lookup"><span data-stu-id="b868e-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="b868e-136">When prompted, confirm you want to remove the account.</span><span class="sxs-lookup"><span data-stu-id="b868e-136">When prompted, confirm you want to remove the account.</span></span> <span data-ttu-id="b868e-137">Account removal can take some time to complete.</span><span class="sxs-lookup"><span data-stu-id="b868e-137">Account removal can take some time to complete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="b868e-138">Create a BatchAccountContext object</span><span class="sxs-lookup"><span data-stu-id="b868e-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="b868e-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span><span class="sxs-lookup"><span data-stu-id="b868e-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="b868e-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span><span class="sxs-lookup"><span data-stu-id="b868e-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="b868e-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="b868e-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="b868e-142">Create and modify Batch resources</span><span class="sxs-lookup"><span data-stu-id="b868e-142">Create and modify Batch resources</span></span>
<span data-ttu-id="b868e-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span><span class="sxs-lookup"><span data-stu-id="b868e-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span></span> <span data-ttu-id="b868e-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span><span class="sxs-lookup"><span data-stu-id="b868e-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span></span>

<span data-ttu-id="b868e-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="b868e-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span></span> <span data-ttu-id="b868e-146">See the detailed help for each cmdlet for additional examples.</span><span class="sxs-lookup"><span data-stu-id="b868e-146">See the detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="b868e-147">Create a Batch pool</span><span class="sxs-lookup"><span data-stu-id="b868e-147">Create a Batch pool</span></span>
<span data-ttu-id="b868e-148">When creating or updating a Batch pool, you select a cloud service configuration or a virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="b868e-148">When creating or updating a Batch pool, you select a cloud service configuration or a virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="b868e-149">Your choice determines whether your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases) or with one of the supported Linux or Windows VM images in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b868e-149">Your choice determines whether your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases) or with one of the supported Linux or Windows VM images in the Azure Marketplace.</span></span>

<span data-ttu-id="b868e-150">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span><span class="sxs-lookup"><span data-stu-id="b868e-150">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="b868e-151">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="b868e-151">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="b868e-152">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span><span class="sxs-lookup"><span data-stu-id="b868e-152">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="b868e-153">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span><span class="sxs-lookup"><span data-stu-id="b868e-153">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="b868e-154">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span><span class="sxs-lookup"><span data-stu-id="b868e-154">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="b868e-155">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span><span class="sxs-lookup"><span data-stu-id="b868e-155">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="b868e-156">Query for pools, jobs, tasks, and other details</span><span class="sxs-lookup"><span data-stu-id="b868e-156">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="b868e-157">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span><span class="sxs-lookup"><span data-stu-id="b868e-157">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="b868e-158">Query for data</span><span class="sxs-lookup"><span data-stu-id="b868e-158">Query for data</span></span>
<span data-ttu-id="b868e-159">As an example, use **Get-AzureBatchPools** to find your pools.</span><span class="sxs-lookup"><span data-stu-id="b868e-159">As an example, use **Get-AzureBatchPools** to find your pools.</span></span> <span data-ttu-id="b868e-160">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span><span class="sxs-lookup"><span data-stu-id="b868e-160">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="b868e-161">Use an OData filter</span><span class="sxs-lookup"><span data-stu-id="b868e-161">Use an OData filter</span></span>
<span data-ttu-id="b868e-162">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span><span class="sxs-lookup"><span data-stu-id="b868e-162">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span></span> <span data-ttu-id="b868e-163">For example, you can find all pools with ids starting with “myPool”:</span><span class="sxs-lookup"><span data-stu-id="b868e-163">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="b868e-164">This method is not as flexible as using “Where-Object” in a local pipeline.</span><span class="sxs-lookup"><span data-stu-id="b868e-164">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="b868e-165">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span><span class="sxs-lookup"><span data-stu-id="b868e-165">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span></span>

### <a name="use-the-id-parameter"></a><span data-ttu-id="b868e-166">Use the Id parameter</span><span class="sxs-lookup"><span data-stu-id="b868e-166">Use the Id parameter</span></span>
<span data-ttu-id="b868e-167">An alternative to an OData filter is to use the **Id** parameter.</span><span class="sxs-lookup"><span data-stu-id="b868e-167">An alternative to an OData filter is to use the **Id** parameter.</span></span> <span data-ttu-id="b868e-168">To query for a specific pool with id "myPool":</span><span class="sxs-lookup"><span data-stu-id="b868e-168">To query for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="b868e-169">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span><span class="sxs-lookup"><span data-stu-id="b868e-169">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-the-maxcount-parameter"></a><span data-ttu-id="b868e-170">Use the MaxCount parameter</span><span class="sxs-lookup"><span data-stu-id="b868e-170">Use the MaxCount parameter</span></span>
<span data-ttu-id="b868e-171">By default, each cmdlet returns a maximum of 1000 objects.</span><span class="sxs-lookup"><span data-stu-id="b868e-171">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="b868e-172">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span><span class="sxs-lookup"><span data-stu-id="b868e-172">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span></span> <span data-ttu-id="b868e-173">For example:</span><span class="sxs-lookup"><span data-stu-id="b868e-173">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="b868e-174">To remove the upper bound, set **MaxCount** to 0 or less.</span><span class="sxs-lookup"><span data-stu-id="b868e-174">To remove the upper bound, set **MaxCount** to 0 or less.</span></span>

### <a name="use-the-powershell-pipeline"></a><span data-ttu-id="b868e-175">Use the PowerShell pipeline</span><span class="sxs-lookup"><span data-stu-id="b868e-175">Use the PowerShell pipeline</span></span>
<span data-ttu-id="b868e-176">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b868e-176">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span></span> <span data-ttu-id="b868e-177">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span><span class="sxs-lookup"><span data-stu-id="b868e-177">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="b868e-178">For example, find and display all tasks under your account:</span><span class="sxs-lookup"><span data-stu-id="b868e-178">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="b868e-179">Restart (reboot) every compute node in a pool:</span><span class="sxs-lookup"><span data-stu-id="b868e-179">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="b868e-180">Application package management</span><span class="sxs-lookup"><span data-stu-id="b868e-180">Application package management</span></span>
<span data-ttu-id="b868e-181">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span><span class="sxs-lookup"><span data-stu-id="b868e-181">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="b868e-182">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="b868e-182">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span></span>

<span data-ttu-id="b868e-183">**Create** an application:</span><span class="sxs-lookup"><span data-stu-id="b868e-183">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="b868e-184">**Add** an application package:</span><span class="sxs-lookup"><span data-stu-id="b868e-184">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="b868e-185">Set the **default version** for the application:</span><span class="sxs-lookup"><span data-stu-id="b868e-185">Set the **default version** for the application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="b868e-186">**List** an application's packages</span><span class="sxs-lookup"><span data-stu-id="b868e-186">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="b868e-187">**Delete** an application package</span><span class="sxs-lookup"><span data-stu-id="b868e-187">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="b868e-188">**Delete** an application</span><span class="sxs-lookup"><span data-stu-id="b868e-188">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="b868e-189">You must delete all of an application's application package versions before you delete the application.</span><span class="sxs-lookup"><span data-stu-id="b868e-189">You must delete all of an application's application package versions before you delete the application.</span></span> <span data-ttu-id="b868e-190">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span><span class="sxs-lookup"><span data-stu-id="b868e-190">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="b868e-191">Deploy an application package</span><span class="sxs-lookup"><span data-stu-id="b868e-191">Deploy an application package</span></span>
<span data-ttu-id="b868e-192">You can specify one or more application packages for deployment when you create a pool.</span><span class="sxs-lookup"><span data-stu-id="b868e-192">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="b868e-193">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span><span class="sxs-lookup"><span data-stu-id="b868e-193">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="b868e-194">Packages are also deployed when a node is rebooted or reimaged.</span><span class="sxs-lookup"><span data-stu-id="b868e-194">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="b868e-195">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span><span class="sxs-lookup"><span data-stu-id="b868e-195">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="b868e-196">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span><span class="sxs-lookup"><span data-stu-id="b868e-196">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="b868e-197">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span><span class="sxs-lookup"><span data-stu-id="b868e-197">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="b868e-198">You can find more information on application packages in [Application deployment with Azure Batch application packages](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b868e-198">You can find more information on application packages in [Application deployment with Azure Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b868e-199">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span><span class="sxs-lookup"><span data-stu-id="b868e-199">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="b868e-200">Update a pool's application packages</span><span class="sxs-lookup"><span data-stu-id="b868e-200">Update a pool's application packages</span></span>
<span data-ttu-id="b868e-201">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span><span class="sxs-lookup"><span data-stu-id="b868e-201">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="b868e-202">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span><span class="sxs-lookup"><span data-stu-id="b868e-202">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="b868e-203">You've now updated the pool's properties in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="b868e-203">You've now updated the pool's properties in the Batch service.</span></span> <span data-ttu-id="b868e-204">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span><span class="sxs-lookup"><span data-stu-id="b868e-204">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="b868e-205">You can restart every node in a pool with this command:</span><span class="sxs-lookup"><span data-stu-id="b868e-205">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="b868e-206">You can deploy multiple application packages to the compute nodes in a pool.</span><span class="sxs-lookup"><span data-stu-id="b868e-206">You can deploy multiple application packages to the compute nodes in a pool.</span></span> <span data-ttu-id="b868e-207">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span><span class="sxs-lookup"><span data-stu-id="b868e-207">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b868e-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="b868e-208">Next steps</span></span>
* <span data-ttu-id="b868e-209">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](https://msdn.microsoft.com/library/azure/mt125957.aspx).</span><span class="sxs-lookup"><span data-stu-id="b868e-209">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](https://msdn.microsoft.com/library/azure/mt125957.aspx).</span></span>
* <span data-ttu-id="b868e-210">For more information about applications and application packages in Batch, see [Application deployment with Azure Batch application packages](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b868e-210">For more information about applications and application packages in Batch, see [Application deployment with Azure Batch application packages](batch-application-packages.md).</span></span>

