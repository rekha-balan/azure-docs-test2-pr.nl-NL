---
title: Azure PowerShell Script-Create an Azure Cosmos DB SQL API account | Microsoft Docs
description: Azure PowerShell Script Sample - Create an Azure Cosmos DB SQL API account
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
ms.openlocfilehash: 48653dc181df146fbbe1078b4c51cdcaacbef058
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870916"
---
# <a name="azure-cosmos-db-create-a-sql-api-account-using-powershell"></a><span data-ttu-id="9ed31-103">Azure Cosmos DB: Create a SQL API account using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ed31-103">Azure Cosmos DB: Create a SQL API account using PowerShell</span></span>

<span data-ttu-id="9ed31-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span><span class="sxs-lookup"><span data-stu-id="9ed31-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="9ed31-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="9ed31-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9ed31-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="9ed31-106">Clean up deployment</span></span>

<span data-ttu-id="9ed31-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="9ed31-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="9ed31-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="9ed31-108">Script explanation</span></span>

<span data-ttu-id="9ed31-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="9ed31-109">This script uses the following commands.</span></span> <span data-ttu-id="9ed31-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="9ed31-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9ed31-111">Command</span><span class="sxs-lookup"><span data-stu-id="9ed31-111">Command</span></span> | <span data-ttu-id="9ed31-112">Notes</span><span class="sxs-lookup"><span data-stu-id="9ed31-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9ed31-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9ed31-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9ed31-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="9ed31-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9ed31-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="9ed31-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="9ed31-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="9ed31-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="9ed31-117">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9ed31-117">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9ed31-118">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="9ed31-118">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="9ed31-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ed31-119">Next steps</span></span>

<span data-ttu-id="9ed31-120">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="9ed31-120">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="9ed31-121">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9ed31-121">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>