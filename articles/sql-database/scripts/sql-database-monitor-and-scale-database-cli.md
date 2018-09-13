---
title: Azure CLI Script-Monitor & scale a single SQL Database | Microsoft Docs
description: Azure CLI Script Sample - Monitor and scale a single SQL database using the Azure CLI
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
ms.openlocfilehash: a18c078aebd485a0ce7d85a46a16fd0d65e651be
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555528"
---
# <a name="monitor-and-scale-a-single-sql-database-using-the-azure-cli"></a><span data-ttu-id="8e57e-103">Monitor and scale a single SQL database using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8e57e-103">Monitor and scale a single SQL database using the Azure CLI</span></span>

<span data-ttu-id="8e57e-104">This sample CLI script scales a single Azure SQL database to a different performance level after querying the size information of the database.</span><span class="sxs-lookup"><span data-stu-id="8e57e-104">This sample CLI script scales a single Azure SQL database to a different performance level after querying the size information of the database.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="8e57e-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="8e57e-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.sh "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8e57e-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8e57e-106">Clean up deployment</span></span>

<span data-ttu-id="8e57e-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="8e57e-107">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8e57e-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8e57e-108">Script explanation</span></span>

<span data-ttu-id="8e57e-109">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="8e57e-109">This script uses the following commands.</span></span> <span data-ttu-id="8e57e-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="8e57e-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8e57e-111">Command</span><span class="sxs-lookup"><span data-stu-id="8e57e-111">Command</span></span> | <span data-ttu-id="8e57e-112">Notes</span><span class="sxs-lookup"><span data-stu-id="8e57e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8e57e-113">az group create</span><span class="sxs-lookup"><span data-stu-id="8e57e-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8e57e-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8e57e-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8e57e-115">az sql server create</span><span class="sxs-lookup"><span data-stu-id="8e57e-115">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="8e57e-116">Creates a logical server that hosts a database.</span><span class="sxs-lookup"><span data-stu-id="8e57e-116">Creates a logical server that hosts a database.</span></span> |
| [<span data-ttu-id="8e57e-117">az sql db show-usage</span><span class="sxs-lookup"><span data-stu-id="8e57e-117">az sql db show-usage</span></span>](https://docs.microsoft.com/cli/azure/sql/db#show-usage) | <span data-ttu-id="8e57e-118">Shows the size usage information for a database.</span><span class="sxs-lookup"><span data-stu-id="8e57e-118">Shows the size usage information for a database.</span></span> |
| [<span data-ttu-id="8e57e-119">az sql db update</span><span class="sxs-lookup"><span data-stu-id="8e57e-119">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="8e57e-120">Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools.</span><span class="sxs-lookup"><span data-stu-id="8e57e-120">Updates database properties (such as the service tier or performance level) or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="8e57e-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="8e57e-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="8e57e-122">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="8e57e-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8e57e-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="8e57e-123">Next steps</span></span>

<span data-ttu-id="8e57e-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e57e-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8e57e-125">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8e57e-125">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
