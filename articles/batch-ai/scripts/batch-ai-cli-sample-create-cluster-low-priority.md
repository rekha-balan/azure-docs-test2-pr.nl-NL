---
title: Azure CLI Script Example - Create low-priority Batch AI cluster | Microsoft Docs
description: Azure CLI Script Example - Create and manage a Batch AI cluster of low-priority nodes (virtual machines)
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
ms.openlocfilehash: 1fb21ab754e85dd347ff3bd66bafc2fadd95f8b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868963"
---
# <a name="cli-example-create-and-manage-a-batch-ai-cluster-of-low-priority-nodes"></a><span data-ttu-id="01423-103">CLI example: Create and manage a Batch AI cluster of low-priority nodes</span><span class="sxs-lookup"><span data-stu-id="01423-103">CLI example: Create and manage a Batch AI cluster of low-priority nodes</span></span>

<span data-ttu-id="01423-104">This script demonstrates some of the commands available in the Azure CLI to create and manage a Batch AI cluster consisting of low-priority nodes (virtual machines).</span><span class="sxs-lookup"><span data-stu-id="01423-104">This script demonstrates some of the commands available in the Azure CLI to create and manage a Batch AI cluster consisting of low-priority nodes (virtual machines).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="01423-105">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span><span class="sxs-lookup"><span data-stu-id="01423-105">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span></span> <span data-ttu-id="01423-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="01423-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="01423-107">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="01423-107">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="01423-108">Example script</span><span class="sxs-lookup"><span data-stu-id="01423-108">Example script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/batch-ai/create-cluster/create-cluster-low-priority.sh "Create Batch AI cluster - low-priority nodes")]

## <a name="clean-up-deployment"></a><span data-ttu-id="01423-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="01423-109">Clean up deployment</span></span>

<span data-ttu-id="01423-110">Run the following commands to remove the resource groups and all resources associated with them.</span><span class="sxs-lookup"><span data-stu-id="01423-110">Run the following commands to remove the resource groups and all resources associated with them.</span></span>

```azurecli-interactive
# Remove resource group for the cluster.
az group delete --name myResourceGroup

# Remove resource group for the auto-storage account.
az group delete --name batchaiautostorage
```

## <a name="script-explanation"></a><span data-ttu-id="01423-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="01423-111">Script explanation</span></span>

<span data-ttu-id="01423-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="01423-112">This script uses the following commands.</span></span> <span data-ttu-id="01423-113">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="01423-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="01423-114">Command</span><span class="sxs-lookup"><span data-stu-id="01423-114">Command</span></span> | <span data-ttu-id="01423-115">Notes</span><span class="sxs-lookup"><span data-stu-id="01423-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01423-116">az group create</span><span class="sxs-lookup"><span data-stu-id="01423-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="01423-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="01423-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01423-118">az batchai workspace create</span><span class="sxs-lookup"><span data-stu-id="01423-118">az batchai workspace create</span></span>](/cli/azure/batchai/workspace#az-batchai-workspace-create) | <span data-ttu-id="01423-119">Creates a Batch AI workspace.</span><span class="sxs-lookup"><span data-stu-id="01423-119">Creates a Batch AI workspace.</span></span> |
| [<span data-ttu-id="01423-120">az batchai cluster create</span><span class="sxs-lookup"><span data-stu-id="01423-120">az batchai cluster create</span></span>](/cli/azure/batchai/cluster#az-batchai-cluster-create) | <span data-ttu-id="01423-121">Creates a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="01423-121">Creates a Batch AI cluster.</span></span> |
| [<span data-ttu-id="01423-122">az batchai cluster show</span><span class="sxs-lookup"><span data-stu-id="01423-122">az batchai cluster show</span></span>](/cli/azure/batchai/cluster#az-batchai-cluster-show) | <span data-ttu-id="01423-123">Shows information about a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="01423-123">Shows information about a Batch AI cluster.</span></span> |
| [<span data-ttu-id="01423-124">az batchai cluster node list</span><span class="sxs-lookup"><span data-stu-id="01423-124">az batchai cluster node list</span></span>](/cli/azure/batchai/cluster/node#az-batchai-cluster-show) | <span data-ttu-id="01423-125">Lists the nodes in a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="01423-125">Lists the nodes in a Batch AI cluster.</span></span> |
| [<span data-ttu-id="01423-126">az batchai cluster resize</span><span class="sxs-lookup"><span data-stu-id="01423-126">az batchai cluster resize</span></span>](/cli/azure/batchai/cluster#az-batchai-cluster-resize) | <span data-ttu-id="01423-127">Resizes the Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="01423-127">Resizes the Batch AI cluster.</span></span>  |
| [<span data-ttu-id="01423-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="01423-128">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="01423-129">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="01423-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="01423-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="01423-130">Next steps</span></span>

<span data-ttu-id="01423-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="01423-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
