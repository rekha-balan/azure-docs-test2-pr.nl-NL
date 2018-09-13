---
title: Azure CLI Script-Scale an elastic pool | Microsoft Docs
description: Azure CLI Script Sample - Scale an elastic database pool
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
ms.openlocfilehash: b9f08db649839196dfd6dfe8bd95c313d4633e8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564154"
---
# <a name="scale-an-elastic-pool-in-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="7c43c-103">Scale an elastic pool in Azure SQL Database using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7c43c-103">Scale an elastic pool in Azure SQL Database using the Azure CLI</span></span>

<span data-ttu-id="7c43c-104">This sample CLI script creates elastic pools, moves pooled databases, and changes performance levels.</span><span class="sxs-lookup"><span data-stu-id="7c43c-104">This sample CLI script creates elastic pools, moves pooled databases, and changes performance levels.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="7c43c-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="7c43c-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7c43c-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="7c43c-106">Clean up deployment</span></span>

<span data-ttu-id="7c43c-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="7c43c-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7c43c-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="7c43c-108">Script explanation</span></span>

<span data-ttu-id="7c43c-109">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span><span class="sxs-lookup"><span data-stu-id="7c43c-109">This script uses the following commands to create a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="7c43c-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="7c43c-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7c43c-111">Command</span><span class="sxs-lookup"><span data-stu-id="7c43c-111">Command</span></span> | <span data-ttu-id="7c43c-112">Notes</span><span class="sxs-lookup"><span data-stu-id="7c43c-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c43c-113">az group create</span><span class="sxs-lookup"><span data-stu-id="7c43c-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7c43c-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="7c43c-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7c43c-115">az sql server create</span><span class="sxs-lookup"><span data-stu-id="7c43c-115">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="7c43c-116">Creates a logical server that hosts the SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7c43c-116">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="7c43c-117">az sql elastic-pools create</span><span class="sxs-lookup"><span data-stu-id="7c43c-117">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pools#create) | <span data-ttu-id="7c43c-118">Creates an elastic database pool within the logical server.</span><span class="sxs-lookup"><span data-stu-id="7c43c-118">Creates an elastic database pool within the logical server.</span></span> |
| [<span data-ttu-id="7c43c-119">az sql db create</span><span class="sxs-lookup"><span data-stu-id="7c43c-119">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="7c43c-120">Creates the SQL Database in the logical server.</span><span class="sxs-lookup"><span data-stu-id="7c43c-120">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="7c43c-121">az sql elastic-pools update</span><span class="sxs-lookup"><span data-stu-id="7c43c-121">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pools#update) | <span data-ttu-id="7c43c-122">Updates an elastic database pool, in this example changes the assigned eDTU.</span><span class="sxs-lookup"><span data-stu-id="7c43c-122">Updates an elastic database pool, in this example changes the assigned eDTU.</span></span> |
| [<span data-ttu-id="7c43c-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="7c43c-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7c43c-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="7c43c-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c43c-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c43c-125">Next steps</span></span>

<span data-ttu-id="7c43c-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c43c-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7c43c-127">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c43c-127">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
