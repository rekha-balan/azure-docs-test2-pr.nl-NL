---
title: Azure CLI Script-Scale Azure Cosmos DB container throughput | Microsoft Docs
description: Azure CLI Script Sample - Scale Azure Cosmos DB contianer throughput
services: cosmos-db
documentationcenter: cosmosdb
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/23/2018
ms.author: sngun
ms.openlocfilehash: d830d8150066acd17cbfca6a05156b33ade240a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965856"
---
# <a name="scale-azure-cosmos-db-container-throughput-using-the-azure-cli"></a><span data-ttu-id="ed9cf-103">Scale Azure Cosmos DB container throughput using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ed9cf-103">Scale Azure Cosmos DB container throughput using the Azure CLI</span></span>

<span data-ttu-id="ed9cf-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ed9cf-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ed9cf-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ed9cf-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ed9cf-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ed9cf-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="ed9cf-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]

<span data-ttu-id="ed9cf-109">Above sample script lets you create and scale a fixed collection.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-109">Above sample script lets you create and scale a fixed collection.</span></span> <span data-ttu-id="ed9cf-110">If you want to create and scale a collection with unlimited storage capacity, you must:</span><span class="sxs-lookup"><span data-stu-id="ed9cf-110">If you want to create and scale a collection with unlimited storage capacity, you must:</span></span> 
 
* <span data-ttu-id="ed9cf-111">Create the collection with at least 1000 RU/s and</span><span class="sxs-lookup"><span data-stu-id="ed9cf-111">Create the collection with at least 1000 RU/s and</span></span> 
* <span data-ttu-id="ed9cf-112">Specify a partition key while creating the collection.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-112">Specify a partition key while creating the collection.</span></span> 

<span data-ttu-id="ed9cf-113">The following command shows an example to create a collection with unlimited storage capacity:</span><span class="sxs-lookup"><span data-stu-id="ed9cf-113">The following command shows an example to create a collection with unlimited storage capacity:</span></span>

```cli
az cosmosdb collection create \
    --collection-name $collectionName \
    --name $name \
    --db-name $databaseName \
    --resource-group $resourceGroupName \
    --throughput 1000
    --partition-key-path /deviceId

```

## <a name="clean-up-deployment"></a><span data-ttu-id="ed9cf-114">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="ed9cf-114">Clean up deployment</span></span>

<span data-ttu-id="ed9cf-115">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-115">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ed9cf-116">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ed9cf-116">Script explanation</span></span>

<span data-ttu-id="ed9cf-117">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-117">This script uses the following commands.</span></span> <span data-ttu-id="ed9cf-118">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-118">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ed9cf-119">Command</span><span class="sxs-lookup"><span data-stu-id="ed9cf-119">Command</span></span> | <span data-ttu-id="ed9cf-120">Notes</span><span class="sxs-lookup"><span data-stu-id="ed9cf-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ed9cf-121">az group create</span><span class="sxs-lookup"><span data-stu-id="ed9cf-121">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="ed9cf-122">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ed9cf-123">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="ed9cf-123">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-update) | <span data-ttu-id="ed9cf-124">Updates an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-124">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="ed9cf-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="ed9cf-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-delete) | <span data-ttu-id="ed9cf-126">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="ed9cf-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ed9cf-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="ed9cf-127">Next steps</span></span>

<span data-ttu-id="ed9cf-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="ed9cf-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="ed9cf-129">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ed9cf-129">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
