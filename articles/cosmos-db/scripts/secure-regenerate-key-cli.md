---
title: Azure CLI Script-Regenerate Azure Cosmos DB account key | Microsoft Docs
description: Azure CLI Script Sample - Regenerate an Azure Cosmos DB account key
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
ms.date: 06/02/2017
ms.author: sngun
ms.openlocfilehash: 601130dc07613d42b8ec55f670d8b9c050136143
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864661"
---
# <a name="regenerate-an-azure-cosmos-db-account-key-using-the-azure-cli"></a><span data-ttu-id="94c3c-103">Regenerate an Azure Cosmos DB account key using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="94c3c-103">Regenerate an Azure Cosmos DB account key using the Azure CLI</span></span>

<span data-ttu-id="94c3c-104">This sample regenerates any kind of Azure Cosmos DB account key using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="94c3c-104">This sample regenerates any kind of Azure Cosmos DB account key using the Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="94c3c-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="94c3c-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="94c3c-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="94c3c-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="94c3c-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94c3c-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="94c3c-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="94c3c-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-regenerate-keys/secure-cosmosdb-regenerate-keys.sh?highlight=27-31 "Regenerate Azure Cosmos DB account keys")]

## <a name="clean-up-deployment"></a><span data-ttu-id="94c3c-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="94c3c-109">Clean up deployment</span></span>

<span data-ttu-id="94c3c-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="94c3c-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="94c3c-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="94c3c-111">Script explanation</span></span>

<span data-ttu-id="94c3c-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="94c3c-112">This script uses the following commands.</span></span> <span data-ttu-id="94c3c-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="94c3c-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="94c3c-114">Command</span><span class="sxs-lookup"><span data-stu-id="94c3c-114">Command</span></span> | <span data-ttu-id="94c3c-115">Notes</span><span class="sxs-lookup"><span data-stu-id="94c3c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="94c3c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="94c3c-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="94c3c-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="94c3c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="94c3c-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="94c3c-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-create) | <span data-ttu-id="94c3c-119">Updates an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="94c3c-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="94c3c-120">az cosmosdb regenerate-key</span><span class="sxs-lookup"><span data-stu-id="94c3c-120">az cosmosdb regenerate-key</span></span>](/cli/azure/cosmosdb#az-cosmosdb-regenerate-key) | <span data-ttu-id="94c3c-121">Regeneratates Azure Cosmos DB account keys.</span><span class="sxs-lookup"><span data-stu-id="94c3c-121">Regeneratates Azure Cosmos DB account keys.</span></span> |
| [<span data-ttu-id="94c3c-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="94c3c-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-delete) | <span data-ttu-id="94c3c-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="94c3c-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="94c3c-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="94c3c-124">Next steps</span></span>

<span data-ttu-id="94c3c-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="94c3c-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="94c3c-126">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="94c3c-126">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
