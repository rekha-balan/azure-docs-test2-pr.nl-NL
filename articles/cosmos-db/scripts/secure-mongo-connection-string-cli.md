---
title: Azure CLI Script-Get Azure Cosmos DB connection string for MongoDB apps| Microsoft Docs
description: Azure CLI Script Sample - Get Azure Cosmos DB connection string for MongoDB apps
services: cosmos-db
documentationcenter: cosmosdb
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: sngun
ms.openlocfilehash: 9c643ebf0dfa2fda0f5a9c53962d4b26ba842940
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870824"
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-the-azure-cli"></a><span data-ttu-id="2077a-103">Get an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2077a-103">Get an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI</span></span>

<span data-ttu-id="2077a-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2077a-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using the Azure CLI.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2077a-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="2077a-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2077a-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="2077a-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="2077a-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2077a-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2077a-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="2077a-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/secure-cosmosdb-get-mongodb-connection-string/secure-cosmosdb-get-mongodb-connection-string.sh?highlight=36-39 "Get Azure Cosmos DB connection string for MongoDB apps")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2077a-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="2077a-109">Clean up deployment</span></span>

<span data-ttu-id="2077a-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="2077a-110">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2077a-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="2077a-111">Script explanation</span></span>

<span data-ttu-id="2077a-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="2077a-112">This script uses the following commands.</span></span> <span data-ttu-id="2077a-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="2077a-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2077a-114">Command</span><span class="sxs-lookup"><span data-stu-id="2077a-114">Command</span></span> | <span data-ttu-id="2077a-115">Notes</span><span class="sxs-lookup"><span data-stu-id="2077a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2077a-116">az group create</span><span class="sxs-lookup"><span data-stu-id="2077a-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="2077a-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="2077a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2077a-118">az cosmosdb update</span><span class="sxs-lookup"><span data-stu-id="2077a-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-update) | <span data-ttu-id="2077a-119">Updates an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="2077a-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="2077a-120">az cosmosdb list-connection-strings</span><span class="sxs-lookup"><span data-stu-id="2077a-120">az cosmosdb list-connection-strings</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-list-connection-strings) | <span data-ttu-id="2077a-121">Gets the connection string for the account.</span><span class="sxs-lookup"><span data-stu-id="2077a-121">Gets the connection string for the account.</span></span>|
| [<span data-ttu-id="2077a-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="2077a-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-delete) | <span data-ttu-id="2077a-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="2077a-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2077a-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="2077a-124">Next steps</span></span>

<span data-ttu-id="2077a-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="2077a-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="2077a-126">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2077a-126">Additional Azure Cosmos DB CLI script samples can be found in the [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
