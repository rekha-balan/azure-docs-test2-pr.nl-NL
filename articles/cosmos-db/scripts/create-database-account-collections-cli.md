---
title: Azure CLI Script-Create an Azure Cosmos DB SQL API account, database, and collection | Microsoft Docs
description: Azure CLI Script Sample - Create an Azure Cosmos DB SQL API account, database, and collection
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
ms.date: 06/06/2017
ms.author: sngun
ms.openlocfilehash: fb4bd66d209d15c983d11c53648e3dfd9c7dcb4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869555"
---
# <a name="azure-cosmos-db-create-an-sql-api-account-using-cli"></a><span data-ttu-id="ad39c-103">Azure Cosmos DB: Create an SQL API account using CLI</span><span class="sxs-lookup"><span data-stu-id="ad39c-103">Azure Cosmos DB: Create an SQL API account using CLI</span></span>

<span data-ttu-id="ad39c-104">This sample CLI script creates an Azure Cosmos DB SQL API account, database, and collection.</span><span class="sxs-lookup"><span data-stu-id="ad39c-104">This sample CLI script creates an Azure Cosmos DB SQL API account, database, and collection.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ad39c-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="ad39c-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ad39c-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="ad39c-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="ad39c-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ad39c-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ad39c-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="ad39c-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/create-cosmosdb-account-database/create-cosmosdb-account-database.sh?highlight=15-35 "Create an Azure Cosmos DB SQL API account, database, and collection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ad39c-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="ad39c-109">Clean up deployment</span></span>

<span data-ttu-id="ad39c-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="ad39c-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ad39c-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ad39c-111">Script explanation</span></span>

<span data-ttu-id="ad39c-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="ad39c-112">This script uses the following commands.</span></span> <span data-ttu-id="ad39c-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ad39c-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ad39c-114">Command</span><span class="sxs-lookup"><span data-stu-id="ad39c-114">Command</span></span> | <span data-ttu-id="ad39c-115">Notes</span><span class="sxs-lookup"><span data-stu-id="ad39c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ad39c-116">az group create</span><span class="sxs-lookup"><span data-stu-id="ad39c-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="ad39c-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="ad39c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ad39c-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="ad39c-118">az cosmosdb create</span></span>](/cli/azure/cosmosdb#az-cosmosdb-create) | <span data-ttu-id="ad39c-119">Creates an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="ad39c-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="ad39c-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="ad39c-120">az group delete</span></span>](/cli/azure/resource#az-resource-delete) | <span data-ttu-id="ad39c-121">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="ad39c-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad39c-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad39c-122">Next steps</span></span>

<span data-ttu-id="ad39c-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="ad39c-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="ad39c-124">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ad39c-124">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
