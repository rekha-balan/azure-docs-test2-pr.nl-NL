---
title: Azure CLI Script-Move a SQL database and elastic pools | Microsoft Docs
description: Azure CLI Script Sample - Move a SQL database between elastic pools using Azure CLI
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: ''
ms.service: sql-database
ms.custom: sample
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 04/04/2017
ms.author: janeng
ms.openlocfilehash: 86ce00a1012775594236db117c5fef86dd3d43ab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553032"
---
# <a name="create-elastic-pools-and-move-databases-between-pools-and-out-of-a-pool-using-the-azure-cli"></a><span data-ttu-id="f559e-103">Create elastic pools and move databases between pools and out of a pool using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f559e-103">Create elastic pools and move databases between pools and out of a pool using the Azure CLI</span></span>

<span data-ttu-id="f559e-104">This sample CLI script creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span><span class="sxs-lookup"><span data-stu-id="f559e-104">This sample CLI script creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f559e-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="f559e-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f559e-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="f559e-106">Clean up deployment</span></span>

<span data-ttu-id="f559e-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="f559e-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f559e-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f559e-108">Script explanation</span></span>

<span data-ttu-id="f559e-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="f559e-109">This script uses the following commands.</span></span> <span data-ttu-id="f559e-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f559e-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f559e-111">Command</span><span class="sxs-lookup"><span data-stu-id="f559e-111">Command</span></span> | <span data-ttu-id="f559e-112">Notes</span><span class="sxs-lookup"><span data-stu-id="f559e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f559e-113">az group create</span><span class="sxs-lookup"><span data-stu-id="f559e-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f559e-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f559e-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f559e-115">az sql server create</span><span class="sxs-lookup"><span data-stu-id="f559e-115">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="f559e-116">Creates a logical server that hosts a database or elastic pool.</span><span class="sxs-lookup"><span data-stu-id="f559e-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f559e-117">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="f559e-117">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pools#create) | <span data-ttu-id="f559e-118">Creates an elastic pool within the logical server.</span><span class="sxs-lookup"><span data-stu-id="f559e-118">Creates an elastic pool within the logical server.</span></span> |
| [<span data-ttu-id="f559e-119">az sql db create</span><span class="sxs-lookup"><span data-stu-id="f559e-119">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="f559e-120">Creates a database in a logical server as a single or a pooled database.</span><span class="sxs-lookup"><span data-stu-id="f559e-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="f559e-121">az sql db update</span><span class="sxs-lookup"><span data-stu-id="f559e-121">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="f559e-122">Updates database properties or moves a database into, out of, or between elastic pools.</span><span class="sxs-lookup"><span data-stu-id="f559e-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="f559e-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="f559e-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f559e-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="f559e-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f559e-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="f559e-125">Next steps</span></span>

<span data-ttu-id="f559e-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f559e-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f559e-127">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f559e-127">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


