---
title: 'PowerShell script: Copy data from on-premises to Azure by using Data Factory | Microsoft Docs'
description: This PowerShell script copies data from an on-premises SQL Server database to another an Azure Blob Storage.
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
ms.openlocfilehash: 3d73f6dc06ccd9aa8b3e81754b66e81b3e8252fc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866318"
---
# <a name="use-powershell-to-create-a-data-factory-pipeline-to-copy-data-from-on-premises-to-azure"></a><span data-ttu-id="2064b-103">Use PowerShell to create a data factory pipeline to copy data from on-premises to Azure</span><span class="sxs-lookup"><span data-stu-id="2064b-103">Use PowerShell to create a data factory pipeline to copy data from on-premises to Azure</span></span>

<span data-ttu-id="2064b-104">This sample PowerShell script creates a pipeline in Azure Data Factory that copies data from an on-premises SQL Server database to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2064b-104">This sample PowerShell script creates a pipeline in Azure Data Factory that copies data from an on-premises SQL Server database to an Azure Blob Storage.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="2064b-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2064b-105">Prerequisites</span></span>

- <span data-ttu-id="2064b-106">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="2064b-106">**SQL Server**.</span></span> <span data-ttu-id="2064b-107">You use an on-premises SQL Server database as a **source** data store in this sample.</span><span class="sxs-lookup"><span data-stu-id="2064b-107">You use an on-premises SQL Server database as a **source** data store in this sample.</span></span>
- <span data-ttu-id="2064b-108">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="2064b-108">**Azure Storage account**.</span></span> <span data-ttu-id="2064b-109">You use Azure blob storage as a **destination/sink** data store in this sample.</span><span class="sxs-lookup"><span data-stu-id="2064b-109">You use Azure blob storage as a **destination/sink** data store in this sample.</span></span> <span data-ttu-id="2064b-110">if you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="2064b-110">if you don't have an Azure storage account, see the [Create a storage account](../../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
- <span data-ttu-id="2064b-111">**Self-hosted integration runtime**.</span><span class="sxs-lookup"><span data-stu-id="2064b-111">**Self-hosted integration runtime**.</span></span> <span data-ttu-id="2064b-112">Download MSI file from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) and run it to install a self-hosted integration runtime on your machine.</span><span class="sxs-lookup"><span data-stu-id="2064b-112">Download MSI file from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) and run it to install a self-hosted integration runtime on your machine.</span></span>  

### <a name="create-sample-database-in-sql-server"></a><span data-ttu-id="2064b-113">Create sample database in SQL Server</span><span class="sxs-lookup"><span data-stu-id="2064b-113">Create sample database in SQL Server</span></span>
1. <span data-ttu-id="2064b-114">In the on-premises SQL Server database, create a table named **emp** by using the following SQL script:</span><span class="sxs-lookup"><span data-stu-id="2064b-114">In the on-premises SQL Server database, create a table named **emp** by using the following SQL script:</span></span> 

   ```sql   
     CREATE TABLE dbo.emp
     (
         ID int IDENTITY(1,1) NOT NULL,
         FirstName varchar(50),
         LastName varchar(50),
         CONSTRAINT PK_emp PRIMARY KEY (ID)
     )
     GO
   ```

2. <span data-ttu-id="2064b-115">Insert some sample data into the table:</span><span class="sxs-lookup"><span data-stu-id="2064b-115">Insert some sample data into the table:</span></span>

   ```sql
     INSERT INTO emp VALUES ('John', 'Doe')
     INSERT INTO emp VALUES ('Jane', 'Doe')
   ```

## <a name="sample-script"></a><span data-ttu-id="2064b-116">Sample script</span><span class="sxs-lookup"><span data-stu-id="2064b-116">Sample script</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2064b-117">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span><span class="sxs-lookup"><span data-stu-id="2064b-117">This script creates JSON files that define Data Factory entities (linked service, dataset, and pipeline) on your hard drive in the c:\ folder.</span></span>

[!code-powershell[main](../../../powershell_scripts/data-factory/copy-from-onprem-sql-server-to-azure-blob/copy-from-onprem-sql-server-to-azure-blob.ps1 "Copy from on-premises SQL Server -> Azure Blob Storage")]


## <a name="clean-up-deployment"></a><span data-ttu-id="2064b-118">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="2064b-118">Clean up deployment</span></span>

<span data-ttu-id="2064b-119">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span><span class="sxs-lookup"><span data-stu-id="2064b-119">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="2064b-120">To remove the data factory from the resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="2064b-120">To remove the data factory from the resource group, run the following command:</span></span> 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```

## <a name="script-explanation"></a><span data-ttu-id="2064b-121">Script explanation</span><span class="sxs-lookup"><span data-stu-id="2064b-121">Script explanation</span></span>

<span data-ttu-id="2064b-122">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="2064b-122">This script uses the following commands:</span></span> 

| <span data-ttu-id="2064b-123">Command</span><span class="sxs-lookup"><span data-stu-id="2064b-123">Command</span></span> | <span data-ttu-id="2064b-124">Notes</span><span class="sxs-lookup"><span data-stu-id="2064b-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2064b-125">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2064b-125">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2064b-126">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="2064b-126">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2064b-127">Set-AzureRmDataFactoryV2</span><span class="sxs-lookup"><span data-stu-id="2064b-127">Set-AzureRmDataFactoryV2</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2) | <span data-ttu-id="2064b-128">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="2064b-128">Create a data factory.</span></span> |
| [<span data-ttu-id="2064b-129">New-AzureRmDataFactoryV2LinkedServiceEncryptCredential</span><span class="sxs-lookup"><span data-stu-id="2064b-129">New-AzureRmDataFactoryV2LinkedServiceEncryptCredential</span></span>](/powershell/module/azurerm.datafactoryv2/new-azurermdatafactoryv2linkedserviceencryptedcredential) | <span data-ttu-id="2064b-130">Encrypts credentials in a linked service and generates a new linked service definition with the encrypted credential.</span><span class="sxs-lookup"><span data-stu-id="2064b-130">Encrypts credentials in a linked service and generates a new linked service definition with the encrypted credential.</span></span> 
| [<span data-ttu-id="2064b-131">Set-AzureRmDataFactoryV2LinkedService</span><span class="sxs-lookup"><span data-stu-id="2064b-131">Set-AzureRmDataFactoryV2LinkedService</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2linkedservice) | <span data-ttu-id="2064b-132">Creates a linked service in the data factory.</span><span class="sxs-lookup"><span data-stu-id="2064b-132">Creates a linked service in the data factory.</span></span> <span data-ttu-id="2064b-133">A linked service links a data store or compute to a data factory.</span><span class="sxs-lookup"><span data-stu-id="2064b-133">A linked service links a data store or compute to a data factory.</span></span> |
| [<span data-ttu-id="2064b-134">Set-AzureRmDataFactoryV2Dataset</span><span class="sxs-lookup"><span data-stu-id="2064b-134">Set-AzureRmDataFactoryV2Dataset</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2dataset) | <span data-ttu-id="2064b-135">Creates a dataset in the data factory.</span><span class="sxs-lookup"><span data-stu-id="2064b-135">Creates a dataset in the data factory.</span></span> <span data-ttu-id="2064b-136">A dataset represents input/output for an activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="2064b-136">A dataset represents input/output for an activity in a pipeline.</span></span> | 
| [<span data-ttu-id="2064b-137">Set-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="2064b-137">Set-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/Set-azurermdatafactoryv2pipeline) | <span data-ttu-id="2064b-138">Creates a pipeline in the data factory.</span><span class="sxs-lookup"><span data-stu-id="2064b-138">Creates a pipeline in the data factory.</span></span> <span data-ttu-id="2064b-139">A pipeline contains one or more activities that performs a certain operation.</span><span class="sxs-lookup"><span data-stu-id="2064b-139">A pipeline contains one or more activities that performs a certain operation.</span></span> <span data-ttu-id="2064b-140">In this pipeline, a copy activity copies data from one location to another location in an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2064b-140">In this pipeline, a copy activity copies data from one location to another location in an Azure Blob Storage.</span></span> |
| [<span data-ttu-id="2064b-141">Invoke-AzureRmDataFactoryV2Pipeline</span><span class="sxs-lookup"><span data-stu-id="2064b-141">Invoke-AzureRmDataFactoryV2Pipeline</span></span>](/powershell/module/azurerm.datafactoryv2/Invoke-azurermdatafactoryv2pipeline) | <span data-ttu-id="2064b-142">Creates a run for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="2064b-142">Creates a run for the pipeline.</span></span> <span data-ttu-id="2064b-143">In other words, runs the pipeline.</span><span class="sxs-lookup"><span data-stu-id="2064b-143">In other words, runs the pipeline.</span></span> |
| [<span data-ttu-id="2064b-144">Get-AzureRmDataFactoryV2ActivityRun</span><span class="sxs-lookup"><span data-stu-id="2064b-144">Get-AzureRmDataFactoryV2ActivityRun</span></span>](/powershell/module/azurerm.datafactoryv2/get-azurermdatafactoryv2activityrun) | <span data-ttu-id="2064b-145">Gets details about the run of the activity (activity run) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="2064b-145">Gets details about the run of the activity (activity run) in the pipeline.</span></span> 
| [<span data-ttu-id="2064b-146">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2064b-146">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2064b-147">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="2064b-147">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2064b-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="2064b-148">Next steps</span></span>

<span data-ttu-id="2064b-149">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="2064b-149">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="2064b-150">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2064b-150">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell samples](../samples-powershell.md).</span></span>
