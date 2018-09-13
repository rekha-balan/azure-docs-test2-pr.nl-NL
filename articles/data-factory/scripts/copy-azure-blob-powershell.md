---
title: 'PowerShell script: Copy data in the cloud by using Azure Data Factory | Microsoft Docs'
description: This PowerShell script copies data from one location in an Azure Blob Storage to another location in the same Blob Storage.
services: data-factory
author: linda33wj
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2017
ms.author: jingwang
ms.openlocfilehash: 1fbf09968c6dc3dfc60b27656691504a363a5a6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868978"
---
# <a name="use-powershell-to-create-a-data-factory-pipeline-to-copy-data-in-the-cloud"></a><span data-ttu-id="c1727-103">Use PowerShell to create a data factory pipeline to copy data in the cloud</span><span class="sxs-lookup"><span data-stu-id="c1727-103">Use PowerShell to create a data factory pipeline to copy data in the cloud</span></span>

<span data-ttu-id="c1727-104">This sample PowerShell script creates a pipeline in Azure Data Factory that copies data from one location to another location in an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c1727-104">This sample PowerShell script creates a pipeline in Azure Data Factory that copies data from one location to another location in an Azure Blob Storage.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="c1727-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c1727-105">Prerequisites</span></span>
* <span data-ttu-id="c1727-106">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="c1727-106">**Azure Storage account**.</span></span> <span data-ttu-id="c1727-107">You use the blob storage as both the **source** and **sink** data stores.</span><span class="sxs-lookup"><span data-stu-id="c1727-107">You use the blob storage as both the **source** and **sink** data stores.</span></span> <span data-ttu-id="c1727-108">If you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) on creating one.</span><span class="sxs-lookup"><span data-stu-id="c1727-108">If you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) on creating one.</span></span> 
* <span data-ttu-id="c1727-109">Create a **blob container** in Blob Storage, create an input **folder** in the container, and upload some files to the folder.</span><span class="sxs-lookup"><span data-stu-id="c1727-109">Create a **blob container** in Blob Storage, create an input **folder** in the container, and upload some files to the folder.</span></span> <span data-ttu-id="c1727-110">You can use tools such as [Azure Storage explorer](https://azure.microsoft.com/features/storage-explorer/) to connect to Azure Blob storage, create a blob container, upload input file, and verify the output file.</span><span class="sxs-lookup"><span data-stu-id="c1727-110">You can use tools such as [Azure Storage explorer](https://azure.microsoft.com/features/storage-explorer/) to connect to Azure Blob storage, create a blob container, upload input file, and verify the output file.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c1727-111">Sample script</span><span class="sxs-lookup"><span data-stu-id="c1727-111">Sample script</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1727-112">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span><span class="sxs-lookup"><span data-stu-id="c1727-112">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span></span>

[!code-powershell[main](../../../powershell_scripts/data-factory/copy-from-azure-blob-to-blob/copy-from-azure-blob-to-blob.ps1 "Copy from Blob Storage -> Blob Storage")]


## <a name="clean-up-deployment"></a><span data-ttu-id="c1727-113">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="c1727-113">Clean up deployment</span></span>

<span data-ttu-id="c1727-114">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span><span class="sxs-lookup"><span data-stu-id="c1727-114">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="c1727-115">To remove the data factory from the resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="c1727-115">To remove the data factory from the resource group, run the following command:</span></span> 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```

## <a name="script-explanation"></a><span data-ttu-id="c1727-116">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c1727-116">Script explanation</span></span>

<span data-ttu-id="c1727-117">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="c1727-117">This script uses the following commands:</span></span> 

| <span data-ttu-id="c1727-118">Command</span><span class="sxs-lookup"><span data-stu-id="c1727-118">Command</span></span> | <span data-ttu-id="c1727-119">Notes</span><span class="sxs-lookup"><span data-stu-id="c1727-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c1727-120">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c1727-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c1727-121">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c1727-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c1727-122">Set-AzureRmDataFactoryV2</span><span class="sxs-lookup"><span data-stu-id="c1727-122">Set-AzureRmDataFactoryV2</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2) | <span data-ttu-id="c1727-123">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="c1727-123">Create a data factory.</span></span> |
| [<span data-ttu-id="c1727-124">Set-AzureRmDataFactoryV2LinkedService</span><span class="sxs-lookup"><span data-stu-id="c1727-124">Set-AzureRmDataFactoryV2LinkedService</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2linkedservice) | <span data-ttu-id="c1727-125">Creates a linked service in the data factory.</span><span class="sxs-lookup"><span data-stu-id="c1727-125">Creates a linked service in the data factory.</span></span> <span data-ttu-id="c1727-126">A linked service links a data store or compute to a data factory.</span><span class="sxs-lookup"><span data-stu-id="c1727-126">A linked service links a data store or compute to a data factory.</span></span> |
| [<span data-ttu-id="c1727-127">Set-AzureRmDataFactoryV2Dataset</span><span class="sxs-lookup"><span data-stu-id="c1727-127">Set-AzureRmDataFactoryV2Dataset</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2dataset) | <span data-ttu-id="c1727-128">Creates a dataset in the data factory.</span><span class="sxs-lookup"><span data-stu-id="c1727-128">Creates a dataset in the data factory.</span></span> <span data-ttu-id="c1727-129">A dataset represents input/output for an activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c1727-129">A dataset represents input/output for an activity in a pipeline.</span></span> | 
| [<span data-ttu-id="c1727-130">Set-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="c1727-130">Set-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2pipeline) | <span data-ttu-id="c1727-131">Creates a pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="c1727-131">Creates a pipeline in the data factory.</span></span> <span data-ttu-id="c1727-132">A pipeline contains one or more activities that performs a certain operation.</span><span class="sxs-lookup"><span data-stu-id="c1727-132">A pipeline contains one or more activities that performs a certain operation.</span></span> <span data-ttu-id="c1727-133">In this pipeline, a copy activity copies data from one location to another location in an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c1727-133">In this pipeline, a copy activity copies data from one location to another location in an Azure Blob Storage.</span></span> |
| [<span data-ttu-id="c1727-134">Invoke-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="c1727-134">Invoke-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/Invoke-azurermdatafactoryv2pipeline) | <span data-ttu-id="c1727-135">Creates a run for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c1727-135">Creates a run for the pipeline.</span></span> <span data-ttu-id="c1727-136">In other words, runs the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c1727-136">In other words, runs the pipeline.</span></span> |
| [<span data-ttu-id="c1727-137">Get-AzureRmDataFactoryV2ActivityRun</span><span class="sxs-lookup"><span data-stu-id="c1727-137">Get-AzureRmDataFactoryV2ActivityRun</span></span>](/powershell/module/azurerm.datafactoryv2/get-azurermdatafactoryv2activityrun) | <span data-ttu-id="c1727-138">Gets details about the run of the activity (activity run) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c1727-138">Gets details about the run of the activity (activity run) in the pipeline.</span></span> 
| [<span data-ttu-id="c1727-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c1727-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c1727-140">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="c1727-140">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c1727-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="c1727-141">Next steps</span></span>

<span data-ttu-id="c1727-142">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="c1727-142">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="c1727-143">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c1727-143">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell samples](../samples-powershell.md).</span></span>
