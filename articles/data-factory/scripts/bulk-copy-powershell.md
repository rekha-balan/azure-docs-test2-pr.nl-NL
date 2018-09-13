---
title: 'PowerShell script: Copy data in bulk by using Azure Data Factory | Microsoft Docs'
description: This PowerShell script shows how to use Azure Data Factory to copy data from a source data store to a destination data store in bulk.
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
ms.openlocfilehash: dc1bf394a34c097caa68c029e11c141dbae32aab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866776"
---
# <a name="powershell-script---copy-multiple-tables-in-bulk-by-using-azure-data-factory"></a><span data-ttu-id="fc2ff-103">PowerShell script - copy multiple tables in bulk by using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="fc2ff-103">PowerShell script - copy multiple tables in bulk by using Azure Data Factory</span></span>

<span data-ttu-id="fc2ff-104">This sample PowerShell script copies data from multiple tables in an Azure SQL database to an Azure SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-104">This sample PowerShell script copies data from multiple tables in an Azure SQL database to an Azure SQL data warehouse.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

<span data-ttu-id="fc2ff-105">See [tutorial: bulk copy](../tutorial-bulk-copy.md#prerequisites) for the prerequisites for running this sample.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-105">See [tutorial: bulk copy](../tutorial-bulk-copy.md#prerequisites) for the prerequisites for running this sample.</span></span>

## <a name="sample-script"></a><span data-ttu-id="fc2ff-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="fc2ff-106">Sample script</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc2ff-107">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-107">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span></span>

[!code-powershell[main](../../../powershell_scripts/data-factory/bulk-copy-from-sql-databse-to-sql-data-warehouse/bulk-copy-from-sql-database-to-sql-data-warehouse.ps1 "Bulk copy from Azure SQL Database => Azure SQL Data Warehouse")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fc2ff-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="fc2ff-108">Clean up deployment</span></span>

<span data-ttu-id="fc2ff-109">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span><span class="sxs-lookup"><span data-stu-id="fc2ff-109">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="fc2ff-110">To remove the data factory from the resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="fc2ff-110">To remove the data factory from the resource group, run the following command:</span></span> 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```

## <a name="script-explanation"></a><span data-ttu-id="fc2ff-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="fc2ff-111">Script explanation</span></span>

<span data-ttu-id="fc2ff-112">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="fc2ff-112">This script uses the following commands:</span></span> 

| <span data-ttu-id="fc2ff-113">Command</span><span class="sxs-lookup"><span data-stu-id="fc2ff-113">Command</span></span> | <span data-ttu-id="fc2ff-114">Notes</span><span class="sxs-lookup"><span data-stu-id="fc2ff-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc2ff-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fc2ff-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fc2ff-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc2ff-117">Set-AzureRmDataFactoryV2</span><span class="sxs-lookup"><span data-stu-id="fc2ff-117">Set-AzureRmDataFactoryV2</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2) | <span data-ttu-id="fc2ff-118">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-118">Create a data factory.</span></span> |
| [<span data-ttu-id="fc2ff-119">Set-AzureRmDataFactoryV2LinkedService</span><span class="sxs-lookup"><span data-stu-id="fc2ff-119">Set-AzureRmDataFactoryV2LinkedService</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2linkedservice) | <span data-ttu-id="fc2ff-120">Creates a linked service in the data factory.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-120">Creates a linked service in the data factory.</span></span> <span data-ttu-id="fc2ff-121">A linked service links a data store or compute to a data factory.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-121">A linked service links a data store or compute to a data factory.</span></span> |
| [<span data-ttu-id="fc2ff-122">Set-AzureRmDataFactoryV2Dataset</span><span class="sxs-lookup"><span data-stu-id="fc2ff-122">Set-AzureRmDataFactoryV2Dataset</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2dataset) | <span data-ttu-id="fc2ff-123">Creates a dataset in the data factory.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-123">Creates a dataset in the data factory.</span></span> <span data-ttu-id="fc2ff-124">A dataset represents input/output for an activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-124">A dataset represents input/output for an activity in a pipeline.</span></span> | 
| [<span data-ttu-id="fc2ff-125">Set-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="fc2ff-125">Set-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2pipeline) | <span data-ttu-id="fc2ff-126">Creates a pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-126">Creates a pipeline in the data factory.</span></span> <span data-ttu-id="fc2ff-127">A pipeline contains one or more activities that performs a certain operation.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-127">A pipeline contains one or more activities that performs a certain operation.</span></span> <span data-ttu-id="fc2ff-128">In this pipeline, a copy activity copies data from one location to another location in an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-128">In this pipeline, a copy activity copies data from one location to another location in an Azure Blob Storage.</span></span> |
| [<span data-ttu-id="fc2ff-129">Invoke-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="fc2ff-129">Invoke-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/Invoke-azurermdatafactoryv2pipeline) | <span data-ttu-id="fc2ff-130">Creates a run for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-130">Creates a run for the pipeline.</span></span> <span data-ttu-id="fc2ff-131">In other words, runs the pipeline.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-131">In other words, runs the pipeline.</span></span> |
| [<span data-ttu-id="fc2ff-132">Get-AzureRmDataFactoryV2ActivityRun</span><span class="sxs-lookup"><span data-stu-id="fc2ff-132">Get-AzureRmDataFactoryV2ActivityRun</span></span>](/powershell/module/azurerm.datafactoryv2/get-azurermdatafactoryv2activityrun) | <span data-ttu-id="fc2ff-133">Gets details about the run of the activity (activity run) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-133">Gets details about the run of the activity (activity run) in the pipeline.</span></span> 
| [<span data-ttu-id="fc2ff-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fc2ff-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fc2ff-135">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="fc2ff-135">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="fc2ff-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc2ff-136">Next steps</span></span>

<span data-ttu-id="fc2ff-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="fc2ff-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="fc2ff-138">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell scripts](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fc2ff-138">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell scripts](../samples-powershell.md).</span></span>
