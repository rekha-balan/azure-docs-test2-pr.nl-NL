---
title: Azure PowerShell Script-Get Azure Cosmos DB connection string for MongoDB apps| Microsoft Docs
description: Azure PowerShell Script Sample - Get Azure Cosmos DB connection string for MongoDB apps
services: cosmos-db
documentationcenter: cosmosdb
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: sngun
ms.openlocfilehash: 149d9d4c8d66c139f8ee8b100b67ac23c7da9aa4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865489"
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="1a5d4-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a5d4-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="1a5d4-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a5d4-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="1a5d4-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="1a5d4-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get the MongoDB connection string from an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1a5d4-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="1a5d4-106">Clean up deployment</span></span>

<span data-ttu-id="1a5d4-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="1a5d4-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="1a5d4-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="1a5d4-108">Script explanation</span></span>

<span data-ttu-id="1a5d4-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="1a5d4-109">This script uses the following commands.</span></span> <span data-ttu-id="1a5d4-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="1a5d4-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1a5d4-111">Command</span><span class="sxs-lookup"><span data-stu-id="1a5d4-111">Command</span></span> | <span data-ttu-id="1a5d4-112">Notes</span><span class="sxs-lookup"><span data-stu-id="1a5d4-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1a5d4-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1a5d4-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1a5d4-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="1a5d4-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1a5d4-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="1a5d4-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="1a5d4-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="1a5d4-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="1a5d4-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="1a5d4-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="1a5d4-118">Invokes an action on the Azure CosmosDB account.</span><span class="sxs-lookup"><span data-stu-id="1a5d4-118">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="1a5d4-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1a5d4-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1a5d4-120">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="1a5d4-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="1a5d4-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a5d4-121">Next steps</span></span>

<span data-ttu-id="1a5d4-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="1a5d4-122">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="1a5d4-123">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1a5d4-123">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>