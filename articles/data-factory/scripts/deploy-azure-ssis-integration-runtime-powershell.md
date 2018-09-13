---
title: PowerShell script - deploy Azure-SSIS integration runtime | Microsoft Docs
description: This PowerShell script creates an Azure-SSIS integration runtime that can run SSIS packages in the cloud.
services: data-factory
author: douglaslMS
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2017
ms.author: douglasl
ms.openlocfilehash: 31a3d51b482a5e14b7a3db9081a8960b968980f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869571"
---
# <a name="powershell-script---deploy-azure-ssis-integration-runtime"></a><span data-ttu-id="8ed87-103">PowerShell script - deploy Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="8ed87-103">PowerShell script - deploy Azure-SSIS integration runtime</span></span>

<span data-ttu-id="8ed87-104">This sample PowerShell script creates an Azure-SSIS integration runtime that can run your SSIS packages in Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed87-104">This sample PowerShell script creates an Azure-SSIS integration runtime that can run your SSIS packages in Azure.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="8ed87-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="8ed87-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/data-factory/deploy-azure-ssis-integration-runtime/deploy-azure-ssis-integration-runtime.ps1 "Deploy Azure-SSIS Integration Runtime")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8ed87-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8ed87-106">Clean up deployment</span></span>

<span data-ttu-id="8ed87-107">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span><span class="sxs-lookup"><span data-stu-id="8ed87-107">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="8ed87-108">To remove the data factory from the resource group, run the following command:</span><span class="sxs-lookup"><span data-stu-id="8ed87-108">To remove the data factory from the resource group, run the following command:</span></span> 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```

## <a name="script-explanation"></a><span data-ttu-id="8ed87-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8ed87-109">Script explanation</span></span>

<span data-ttu-id="8ed87-110">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="8ed87-110">This script uses the following commands:</span></span>

| <span data-ttu-id="8ed87-111">Command</span><span class="sxs-lookup"><span data-stu-id="8ed87-111">Command</span></span> | <span data-ttu-id="8ed87-112">Notes</span><span class="sxs-lookup"><span data-stu-id="8ed87-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8ed87-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8ed87-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8ed87-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8ed87-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8ed87-115">Set-AzureRmDataFactoryV2</span><span class="sxs-lookup"><span data-stu-id="8ed87-115">Set-AzureRmDataFactoryV2</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2) | <span data-ttu-id="8ed87-116">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="8ed87-116">Create a data factory.</span></span> |
| [<span data-ttu-id="8ed87-117">Set-AzureRmDataFactoryV2IntegrationRuntime</span><span class="sxs-lookup"><span data-stu-id="8ed87-117">Set-AzureRmDataFactoryV2IntegrationRuntime</span></span>](/powershell/module/azurerm.datafactoryv2/set-azurermdatafactoryv2integrationruntime) | <span data-ttu-id="8ed87-118">Creates an Azure-SSIS integration runtime that can run SSIS packages in the cloud</span><span class="sxs-lookup"><span data-stu-id="8ed87-118">Creates an Azure-SSIS integration runtime that can run SSIS packages in the cloud</span></span> |
| [<span data-ttu-id="8ed87-119">Start-AzureRmDataFactoryV2IntegrationRuntime</span><span class="sxs-lookup"><span data-stu-id="8ed87-119">Start-AzureRmDataFactoryV2IntegrationRuntime</span></span>](/powershell/module/azurerm.datafactoryv2/start-azurermdatafactoryv2integrationruntime) | <span data-ttu-id="8ed87-120">Starts the Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="8ed87-120">Starts the Azure-SSIS integration runtime.</span></span> |
| [<span data-ttu-id="8ed87-121">Get-AzureRmDataFactoryV2IntegrationRuntime</span><span class="sxs-lookup"><span data-stu-id="8ed87-121">Get-AzureRmDataFactoryV2IntegrationRuntime</span></span>](/powershell/module/azurerm.datafactoryv2/get-azurermdatafactoryv2integrationruntime) | <span data-ttu-id="8ed87-122">Gets information about the Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="8ed87-122">Gets information about the Azure-SSIS integration runtime.</span></span> |
| [<span data-ttu-id="8ed87-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8ed87-123">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8ed87-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="8ed87-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8ed87-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ed87-125">Next steps</span></span>

<span data-ttu-id="8ed87-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="8ed87-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="8ed87-127">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell samples](../samples-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8ed87-127">Additional Azure Data Factory PowerShell script samples can be found in the [Azure Data Factory PowerShell samples](../samples-powershell.md).</span></span>
