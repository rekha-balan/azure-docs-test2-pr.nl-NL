---
title: Azure PowerShell Script-Get account keys for cosmosdb | Microsoft Docs
description: Azure PowerShell Script Sample - Get account keys for cosmosdb
services: cosmos-db
documentationcenter: cosmosdb
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: sngun
ms.openlocfilehash: 4ae2b185d5fd25f9d8e0949f956ca4d14e502bd6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865624"
---
# <a name="get-account-keys-for-azure-cosmos-db-using-powershell"></a><span data-ttu-id="d0a71-103">Get account keys for Azure Cosmos DB using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0a71-103">Get account keys for Azure Cosmos DB using PowerShell</span></span>

<span data-ttu-id="d0a71-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="d0a71-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="d0a71-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="d0a71-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "Get the keys for an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d0a71-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="d0a71-106">Clean up deployment</span></span>

<span data-ttu-id="d0a71-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="d0a71-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d0a71-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="d0a71-108">Script explanation</span></span>

<span data-ttu-id="d0a71-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="d0a71-109">This script uses the following commands.</span></span> <span data-ttu-id="d0a71-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="d0a71-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d0a71-111">Command</span><span class="sxs-lookup"><span data-stu-id="d0a71-111">Command</span></span> | <span data-ttu-id="d0a71-112">Notes</span><span class="sxs-lookup"><span data-stu-id="d0a71-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d0a71-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d0a71-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d0a71-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="d0a71-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d0a71-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d0a71-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="d0a71-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="d0a71-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d0a71-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="d0a71-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="d0a71-118">Invokes an action on the Azure CosmosDB account.</span><span class="sxs-lookup"><span data-stu-id="d0a71-118">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="d0a71-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d0a71-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d0a71-120">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="d0a71-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d0a71-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="d0a71-121">Next steps</span></span>

<span data-ttu-id="d0a71-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="d0a71-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="d0a71-123">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d0a71-123">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>