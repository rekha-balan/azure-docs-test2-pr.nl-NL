---
title: Azure CLI Script-Create a failover policy for high availability | Microsoft Docs
description: Azure CLI Script Sample - Create a failover policy for high availability
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
ms.openlocfilehash: 49cae1d5187a04ef1d7a87eacfdb32faf042bd0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864654"
---
# <a name="create-a-failover-policy-for-high-availability-using-the-azure-cli"></a><span data-ttu-id="9e3fd-103">Create a failover policy for high availability using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9e3fd-103">Create a failover policy for high availability using the Azure CLI</span></span>

<span data-ttu-id="9e3fd-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-104">This sample CLI script creates an Azure Cosmos DB account, and then configures it for high availability.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9e3fd-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9e3fd-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="9e3fd-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9e3fd-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9e3fd-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="9e3fd-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/high-availability-cosmosdb-configure-failover/high-availability-cosmosdb-configure-failover.sh?highlight=23-27 "Create an Azure Cosmos DB failover policy")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9e3fd-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="9e3fd-109">Clean up deployment</span></span>

<span data-ttu-id="9e3fd-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9e3fd-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="9e3fd-111">Script explanation</span></span>

<span data-ttu-id="9e3fd-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-112">This script uses the following commands.</span></span> <span data-ttu-id="9e3fd-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9e3fd-114">Command</span><span class="sxs-lookup"><span data-stu-id="9e3fd-114">Command</span></span> | <span data-ttu-id="9e3fd-115">Notes</span><span class="sxs-lookup"><span data-stu-id="9e3fd-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e3fd-116">az group create</span><span class="sxs-lookup"><span data-stu-id="9e3fd-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="9e3fd-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9e3fd-118">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="9e3fd-118">az cosmosdb create</span></span>](/cli/azure/sql/server#az-sql-server-create) | <span data-ttu-id="9e3fd-119">Creates an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-119">Creates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="9e3fd-120">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="9e3fd-120">az cosmosdb update</span></span>](/cli/azure/cosmosdb#az-cosmosdb-update) | <span data-ttu-id="9e3fd-121">Updates Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-121">Updates Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="9e3fd-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="9e3fd-122">az group delete</span></span>](/cli/azure/resource#az-resource-delete) | <span data-ttu-id="9e3fd-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="9e3fd-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e3fd-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e3fd-124">Next steps</span></span>

<span data-ttu-id="9e3fd-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="9e3fd-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="9e3fd-126">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9e3fd-126">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
