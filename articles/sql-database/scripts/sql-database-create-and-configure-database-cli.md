---
title: Azure CLI Script-Create a SQL database | Microsoft Docs
description: Azure CLI Script Sample - Create a SQL database using the Azure CLI
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
ms.openlocfilehash: 7a8a6c634cb4be2da654a971d9412f981d4e0e8a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551127"
---
# <a name="create-a-single-sql-database-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="e263e-103">Create a single SQL database and configure a firewall rule using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e263e-103">Create a single SQL database and configure a firewall rule using the Azure CLI</span></span>

<span data-ttu-id="e263e-104">This sample CLI script creates an Azure SQL database and configure a server-level firewall rule.</span><span class="sxs-lookup"><span data-stu-id="e263e-104">This sample CLI script creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="e263e-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span><span class="sxs-lookup"><span data-stu-id="e263e-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="e263e-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="e263e-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e263e-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="e263e-107">Clean up deployment</span></span>

<span data-ttu-id="e263e-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="e263e-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e263e-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="e263e-109">Script explanation</span></span>

<span data-ttu-id="e263e-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="e263e-110">This script uses the following commands.</span></span> <span data-ttu-id="e263e-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="e263e-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e263e-112">Command</span><span class="sxs-lookup"><span data-stu-id="e263e-112">Command</span></span> | <span data-ttu-id="e263e-113">Notes</span><span class="sxs-lookup"><span data-stu-id="e263e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e263e-114">az group create</span><span class="sxs-lookup"><span data-stu-id="e263e-114">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="e263e-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="e263e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e263e-116">az sql server create</span><span class="sxs-lookup"><span data-stu-id="e263e-116">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="e263e-117">Creates a logical server that hosts the SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e263e-117">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="e263e-118">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="e263e-118">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="e263e-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span><span class="sxs-lookup"><span data-stu-id="e263e-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="e263e-120">az sql db create</span><span class="sxs-lookup"><span data-stu-id="e263e-120">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="e263e-121">Creates the SQL Database in the logical server.</span><span class="sxs-lookup"><span data-stu-id="e263e-121">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="e263e-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="e263e-122">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="e263e-123">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="e263e-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e263e-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="e263e-124">Next steps</span></span>

<span data-ttu-id="e263e-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e263e-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e263e-126">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e263e-126">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

