---
title: 'PowerShell script: Incrementally load data by using Azure Data Factory | Microsoft Docs'
description: This PowerShell script shows how to use Azure Data Factory to copy data incrementally from an Azure SQL Database to an Azure Blob Storage..
services: data-factory
author: linda33wj
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2017
ms.author: jingwang
ms.openlocfilehash: 62f0deeccdd05f4ea9098aab42145be58bf3b328
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864865"
---
# <a name="powershell-script---incrementally-load-data-by-using-azure-data-factory"></a><span data-ttu-id="24d87-103">PowerShell script - Incrementally load data by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="24d87-103">PowerShell script - Incrementally load data by using Azure Data Factory</span></span>
<span data-ttu-id="24d87-104">This sample PowerShell script loads only new or updated records from a source data store to a sink data store after the initial full copy of data from the source to the sink.</span><span class="sxs-lookup"><span data-stu-id="24d87-104">This sample PowerShell script loads only new or updated records from a source data store to a sink data store after the initial full copy of data from the source to the sink.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

<span data-ttu-id="24d87-105">See [tutorial: incremental copy](../tutorial-incremental-copy-powershell.md#prerequisites) for the prerequisites for running this sample.</span><span class="sxs-lookup"><span data-stu-id="24d87-105">See [tutorial: incremental copy](../tutorial-incremental-copy-powershell.md#prerequisites) for the prerequisites for running this sample.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="24d87-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="24d87-106">Sample script</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24d87-107">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span><span class="sxs-lookup"><span data-stu-id="24d87-107">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span></span>

[!code-powershell[main](../../../powershell_scripts/data-factory/incremental-copy-from-azure-sql-to-blob/incremental-copy-from-azure-sql-to-blob.ps1 "Incremental copy from Azure SQL Database to Azure Blob Storage")]

## <a name="clean-up-deployment"></a><span data-ttu-id="24d87-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="24d87-108">Clean up deployment</span></span>

<span data-ttu-id="24d87-109">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span><span class="sxs-lookup"><span data-stu-id="24d87-109">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="24d87-110">To remove the data factory from the resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="24d87-110">To remove the data factory from the resource group, run the following command:</span></span> 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```

## <a name="script-explanation"></a><span data-ttu-id="24d87-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="24d87-111">Script explanation</span></span>

<span data-ttu-id="24d87-112">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="24d87-112">This script uses the following commands:</span></span> 

| <span data-ttu-id="24d87-113">Command</span><span class="sxs-lookup"><span data-stu-id="24d87-113">Command</span></span> | <span data-ttu-id="24d87-114">Notes</span><span class="sxs-lookup"><span data-stu-id="24d87-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="24d87-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="24d87-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="24d87-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="24d87-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="24d87-117">Set-AzureRmDataFactoryV2</span><span class="sxs-lookup"><span data-stu-id="24d87-117">Set-AzureRmDataFactoryV2</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2) | <span data-ttu-id="24d87-118">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="24d87-118">Create a data factory.</span></span> |
| [<span data-ttu-id="24d87-119">Set-AzureRmDataFactoryV2LinkedService</span><span class="sxs-lookup"><span data-stu-id="24d87-119">Set-AzureRmDataFactoryV2LinkedService</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2linkedservice) | <span data-ttu-id="24d87-120">Creates a linked service in the data factory.</span><span class="sxs-lookup"><span data-stu-id="24d87-120">Creates a linked service in the data factory.</span></span> <span data-ttu-id="24d87-121">A linked service links a data store or compute to a data factory.</span><span class="sxs-lookup"><span data-stu-id="24d87-121">A linked service links a data store or compute to a data factory.</span></span> |
| [<span data-ttu-id="24d87-122">Set-AzureRmDataFactoryV2Dataset</span><span class="sxs-lookup"><span data-stu-id="24d87-122">Set-AzureRmDataFactoryV2Dataset</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2dataset) | <span data-ttu-id="24d87-123">Creates a dataset in the data factory.</span><span class="sxs-lookup"><span data-stu-id="24d87-123">Creates a dataset in the data factory.</span></span> <span data-ttu-id="24d87-124">A dataset represents input/output for an activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="24d87-124">A dataset represents input/output for an activity in a pipeline.</span></span> | 
| [<span data-ttu-id="24d87-125">Set-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="24d87-125">Set-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2pipeline) | <span data-ttu-id="24d87-126">Creates a pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="24d87-126">Creates a pipeline in the data factory.</span></span> <span data-ttu-id="24d87-127">A pipeline contains one or more activities that performs a certain operation.</span><span class="sxs-lookup"><span data-stu-id="24d87-127">A pipeline contains one or more activities that performs a certain operation.</span></span> <span data-ttu-id="24d87-128">In this pipeline, a copy activity copies data from one location to another location in an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="24d87-128">In this pipeline, a copy activity copies data from one location to another location in an Azure Blob Storage.</span></span> |
| [<span data-ttu-id="24d87-129">Invoke-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="24d87-129">Invoke-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/Invoke-azurermdatafactoryv2pipeline) | <span data-ttu-id="24d87-130">Creates a run for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="24d87-130">Creates a run for the pipeline.</span></span> <span data-ttu-id="24d87-131">In other words, runs the pipeline.</span><span class="sxs-lookup"><span data-stu-id="24d87-131">In other words, runs the pipeline.</span></span> |
| [<span data-ttu-id="24d87-132">Get-AzureRmDataFactoryV2ActivityRun</span><span class="sxs-lookup"><span data-stu-id="24d87-132">Get-AzureRmDataFactoryV2ActivityRun</span></span>](/powershell/module/azurerm.datafactoryv2/get-azurermdatafactoryv2activityrun) | <span data-ttu-id="24d87-133">Gets details about the run of the activity (activity run) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="24d87-133">Gets details about the run of the activity (activity run) in the pipeline.</span></span> 
| [<span data-ttu-id="24d87-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="24d87-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="24d87-135">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="24d87-135">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="24d87-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="24d87-136">Next steps</span></span>

<span data-ttu-id="24d87-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="24d87-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="24d87-138">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell scripts](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="24d87-138">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell scripts](../samples-powershell.md).</span></span>
