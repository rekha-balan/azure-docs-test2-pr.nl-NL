---
title: Azure CLI Script-Create a firewall for Azure Cosmos DB | Microsoft Docs
description: Azure CLI Script Sample - Create a firewall for Azure Cosmos DB
services: cosmos-db
documentationcenter: cosmosdb
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.custom: sammvcple
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: sngun
ms.openlocfilehash: 3a1ac8f54c94197e6157f71beb1f419e51af4012
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857630"
---
# <a name="azure-cosmos-db-create-a-firewall-using-the-azure-cli"></a><span data-ttu-id="3aec1-103">Azure Cosmos DB: Create a firewall using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3aec1-103">Azure Cosmos DB: Create a firewall using the Azure CLI</span></span>

<span data-ttu-id="3aec1-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="3aec1-104">This sample CLI script creates a firewall policy for any kind of Azure Cosmos DB account.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3aec1-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="3aec1-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3aec1-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="3aec1-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="3aec1-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3aec1-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3aec1-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="3aec1-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-create-firewall/secure-cosmosdb-create-firewall.sh?highlight=38-42 "Create an Azure Cosmos DB firewall")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3aec1-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="3aec1-109">Clean up deployment</span></span>

<span data-ttu-id="3aec1-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="3aec1-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3aec1-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3aec1-111">Script explanation</span></span>

<span data-ttu-id="3aec1-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="3aec1-112">This script uses the following commands.</span></span> <span data-ttu-id="3aec1-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="3aec1-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3aec1-114">Command</span><span class="sxs-lookup"><span data-stu-id="3aec1-114">Command</span></span> | <span data-ttu-id="3aec1-115">Notes</span><span class="sxs-lookup"><span data-stu-id="3aec1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3aec1-116">az group create</span><span class="sxs-lookup"><span data-stu-id="3aec1-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="3aec1-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="3aec1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3aec1-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="3aec1-118">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-create) | <span data-ttu-id="3aec1-119">Creates an Azure CosmosDB account.</span><span class="sxs-lookup"><span data-stu-id="3aec1-119">Creates an Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="3aec1-120">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="3aec1-120">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-update) | <span data-ttu-id="3aec1-121">Updates an Azure CosmosDB account to include firewall settings.</span><span class="sxs-lookup"><span data-stu-id="3aec1-121">Updates an Azure CosmosDB account to include firewall settings.</span></span> |
| [<span data-ttu-id="3aec1-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="3aec1-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-delete) | <span data-ttu-id="3aec1-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="3aec1-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3aec1-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="3aec1-124">Next steps</span></span>

<span data-ttu-id="3aec1-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="3aec1-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="3aec1-126">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3aec1-126">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
