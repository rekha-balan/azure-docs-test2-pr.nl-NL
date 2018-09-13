---
title: Azure CLI Script Example - Create dedicated Batch AI cluster | Microsoft Docs
description: Azure CLI Script Example - Create and manage a Batch AI cluster of dedicated nodes (virtual machines)
services: batch-ai
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: batch-ai
ms.devlang: azurecli
ms.topic: sample
ms.tgt-pltfrm: multiple
ms.workload: na
ms.date: 07/26/2018
ms.author: danlep
ms.openlocfilehash: 10f3444f81dfaeac4331f0b7798ade7eefbd29fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868949"
---
# <a name="cli-example-create-and-manage-a-batch-ai-cluster-of-dedicated-nodes"></a><span data-ttu-id="8cf4d-103">CLI example: Create and manage a Batch AI cluster of dedicated nodes</span><span class="sxs-lookup"><span data-stu-id="8cf4d-103">CLI example: Create and manage a Batch AI cluster of dedicated nodes</span></span>

<span data-ttu-id="8cf4d-104">This script demonstrates some of the commands available in the Azure CLI to create and manage a Batch AI cluster consisting of dedicated nodes (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="8cf4d-104">This script demonstrates some of the commands available in the Azure CLI to create and manage a Batch AI cluster consisting of dedicated nodes (virtual machines).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8cf4d-105">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-105">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span></span> <span data-ttu-id="8cf4d-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="8cf4d-107">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8cf4d-107">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="8cf4d-108">Example script</span><span class="sxs-lookup"><span data-stu-id="8cf4d-108">Example script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/batch-ai/create-cluster/create-cluster-dedicated.sh "Create Batch AI cluster - dedicated nodes")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8cf4d-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8cf4d-109">Clean up deployment</span></span>

<span data-ttu-id="8cf4d-110">Run the following commands to remove the resource groups and all resources associated with them.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-110">Run the following commands to remove the resource groups and all resources associated with them.</span></span>

```azurecli-interactive
# Remove resource group for the cluster.
az group delete --name myResourceGroup

# Remove resource group for the auto-storage account.
az group delete --name batchaiautostorage
```

## <a name="script-explanation"></a><span data-ttu-id="8cf4d-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8cf4d-111">Script explanation</span></span>

<span data-ttu-id="8cf4d-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-112">This script uses the following commands.</span></span> <span data-ttu-id="8cf4d-113">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="8cf4d-114">Command</span><span class="sxs-lookup"><span data-stu-id="8cf4d-114">Command</span></span> | <span data-ttu-id="8cf4d-115">Notes</span><span class="sxs-lookup"><span data-stu-id="8cf4d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8cf4d-116">az group create</span><span class="sxs-lookup"><span data-stu-id="8cf4d-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="8cf4d-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8cf4d-118">az batchai workspace create</span><span class="sxs-lookup"><span data-stu-id="8cf4d-118">az batchai workspace create</span></span>](/cli/azure/batchai/workspace#az-batchai-workspace-create) | <span data-ttu-id="8cf4d-119">Creates a Batch AI workspace.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-119">Creates a Batch AI workspace.</span></span> |
| [<span data-ttu-id="8cf4d-120">az batchai cluster create</span><span class="sxs-lookup"><span data-stu-id="8cf4d-120">az batchai cluster create</span></span>](/cli/azure/batchai/cluster#az-batchai-cluster-create) | <span data-ttu-id="8cf4d-121">Creates a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-121">Creates a Batch AI cluster.</span></span> |
| [<span data-ttu-id="8cf4d-122">az batchai cluster show</span><span class="sxs-lookup"><span data-stu-id="8cf4d-122">az batchai cluster show</span></span>](/cli/azure/batchai/cluster#az-batchai-cluster-show) | <span data-ttu-id="8cf4d-123">Shows information about a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-123">Shows information about a Batch AI cluster.</span></span> |
| [<span data-ttu-id="8cf4d-124">az batchai cluster node list</span><span class="sxs-lookup"><span data-stu-id="8cf4d-124">az batchai cluster node list</span></span>](/cli/azure/batchai/cluster/node#az-batchai-cluster-show) | <span data-ttu-id="8cf4d-125">Lists the nodes in a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-125">Lists the nodes in a Batch AI cluster.</span></span> |
| [<span data-ttu-id="8cf4d-126">az batchai cluster resize</span><span class="sxs-lookup"><span data-stu-id="8cf4d-126">az batchai cluster resize</span></span>](/cli/azure/batchai/cluster#az-batchai-cluster-resize) | <span data-ttu-id="8cf4d-127">Resizes the Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-127">Resizes the Batch AI cluster.</span></span>  |
| [<span data-ttu-id="8cf4d-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="8cf4d-128">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="8cf4d-129">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="8cf4d-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8cf4d-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="8cf4d-130">Next steps</span></span>

<span data-ttu-id="8cf4d-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="8cf4d-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
