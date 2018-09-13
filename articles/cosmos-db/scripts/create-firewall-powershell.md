---
title: Azure PowerShell Script-Create a firewall for Azure Cosmos DB | Microsoft Docs
description: Azure PowerShell Script Sample - Create a firewall for Azure Cosmos DB
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
ms.openlocfilehash: b6f6d58772ffef385abb0c7ad4d59e301afd2b61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871577"
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="2f718-103">Azure Cosmos DB: Create a firewall using PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f718-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="2f718-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span><span class="sxs-lookup"><span data-stu-id="2f718-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="2f718-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="2f718-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2f718-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="2f718-106">Clean up deployment</span></span>

<span data-ttu-id="2f718-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="2f718-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2f718-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="2f718-108">Script explanation</span></span>

<span data-ttu-id="2f718-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="2f718-109">This script uses the following commands.</span></span> <span data-ttu-id="2f718-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="2f718-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2f718-111">Command</span><span class="sxs-lookup"><span data-stu-id="2f718-111">Command</span></span> | <span data-ttu-id="2f718-112">Notes</span><span class="sxs-lookup"><span data-stu-id="2f718-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2f718-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2f718-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2f718-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="2f718-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2f718-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2f718-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="2f718-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="2f718-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="2f718-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="2f718-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="2f718-118">Modifies the database account.</span><span class="sxs-lookup"><span data-stu-id="2f718-118">Modifies the database account.</span></span> |
| [<span data-ttu-id="2f718-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2f718-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2f718-120">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="2f718-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="2f718-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f718-121">Next steps</span></span>

<span data-ttu-id="2f718-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="2f718-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="2f718-123">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2f718-123">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>