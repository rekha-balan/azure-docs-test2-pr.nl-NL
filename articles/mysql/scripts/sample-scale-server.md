---
title: Azure CLI script - Scale an Azure Database for MySQL server
description: This sample CLI script scales Azure Database for MySQL server to a different performance level after querying the metrics.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 04/05/2018
ms.openlocfilehash: 38ae923d86965e493501e8df64f7a064929c3cfb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867268"
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="7d32a-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7d32a-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="7d32a-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span><span class="sxs-lookup"><span data-stu-id="7d32a-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7d32a-105">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="7d32a-105">If you choose to run the CLI locally, this article requires Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7d32a-106">Check the version by running `az --version`.</span><span class="sxs-lookup"><span data-stu-id="7d32a-106">Check the version by running `az --version`.</span></span> <span data-ttu-id="7d32a-107">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7d32a-107">See [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) to install or upgrade your version of Azure CLI.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7d32a-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="7d32a-108">Sample script</span></span>
<span data-ttu-id="7d32a-109">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span><span class="sxs-lookup"><span data-stu-id="7d32a-109">In this sample script, edit the highlighted lines to update the admin username and password to your own.</span></span> <span data-ttu-id="7d32a-110">Replace the subscription ID used in the `az monitor` commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=18-19 "Create and scale Azure Database for MySQL.")]</span><span class="sxs-lookup"><span data-stu-id="7d32a-110">Replace the subscription ID used in the `az monitor` commands with your own subscription id. [!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=18-19 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7d32a-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="7d32a-111">Clean up deployment</span></span>
<span data-ttu-id="7d32a-112">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span><span class="sxs-lookup"><span data-stu-id="7d32a-112">Use the following command to remove the resource group and all resources associated with it after the script has been run.</span></span> 
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="7d32a-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="7d32a-113">Script explanation</span></span>
<span data-ttu-id="7d32a-114">This script uses the commands outlined in the following table:</span><span class="sxs-lookup"><span data-stu-id="7d32a-114">This script uses the commands outlined in the following table:</span></span>

| <span data-ttu-id="7d32a-115">**Command**</span><span class="sxs-lookup"><span data-stu-id="7d32a-115">**Command**</span></span> | <span data-ttu-id="7d32a-116">**Notes**</span><span class="sxs-lookup"><span data-stu-id="7d32a-116">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="7d32a-117">az group create</span><span class="sxs-lookup"><span data-stu-id="7d32a-117">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="7d32a-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="7d32a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7d32a-119">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="7d32a-119">az mysql server create</span></span>](/cli/azure/mysql/server#az-mysql-server-create) | <span data-ttu-id="7d32a-120">Creates a MySQL server that hosts the databases.</span><span class="sxs-lookup"><span data-stu-id="7d32a-120">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="7d32a-121">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="7d32a-121">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#az-monitor-metrics-list) | <span data-ttu-id="7d32a-122">List the metric value for the resources.</span><span class="sxs-lookup"><span data-stu-id="7d32a-122">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="7d32a-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="7d32a-123">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="7d32a-124">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="7d32a-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7d32a-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="7d32a-125">Next steps</span></span>
- <span data-ttu-id="7d32a-126">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="7d32a-126">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure).</span></span>
- <span data-ttu-id="7d32a-127">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7d32a-127">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="7d32a-128">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7d32a-128">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
