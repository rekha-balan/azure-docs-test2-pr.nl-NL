---
title: Azure CLI Script Example - Linux Pool in Batch | Microsoft Docs
description: Azure CLI Script Example - Create and manage a Linux Pool in Batch
services: batch
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: batch
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/29/2018
ms.author: danlep
ms.openlocfilehash: 9a8dadddb129d808e8a127c22b1ae9d0b4fc5568
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866968"
---
# <a name="cli-example-create-and-manage-a-linux-pool-in-azure-batch"></a><span data-ttu-id="c95f8-103">CLI example: Create and manage a Linux pool in Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c95f8-103">CLI example: Create and manage a Linux pool in Azure Batch</span></span>

<span data-ttu-id="c95f8-104">These script demonstrates some of the commands available in the Azure CLI to create and manage a pool of Linux compute nodes in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c95f8-104">These script demonstrates some of the commands available in the Azure CLI to create and manage a pool of Linux compute nodes in Azure Batch.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c95f8-105">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.20 or later.</span><span class="sxs-lookup"><span data-stu-id="c95f8-105">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.20 or later.</span></span> <span data-ttu-id="c95f8-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="c95f8-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="c95f8-107">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c95f8-107">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="c95f8-108">Example script</span><span class="sxs-lookup"><span data-stu-id="c95f8-108">Example script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Linux Virtual Machine Pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c95f8-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="c95f8-109">Clean up deployment</span></span>

<span data-ttu-id="c95f8-110">Run the following command to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="c95f8-110">Run the following command to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c95f8-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c95f8-111">Script explanation</span></span>

<span data-ttu-id="c95f8-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="c95f8-112">This script uses the following commands.</span></span> <span data-ttu-id="c95f8-113">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c95f8-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="c95f8-114">Command</span><span class="sxs-lookup"><span data-stu-id="c95f8-114">Command</span></span> | <span data-ttu-id="c95f8-115">Notes</span><span class="sxs-lookup"><span data-stu-id="c95f8-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c95f8-116">az group create</span><span class="sxs-lookup"><span data-stu-id="c95f8-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="c95f8-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c95f8-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c95f8-118">az batch account create</span><span class="sxs-lookup"><span data-stu-id="c95f8-118">az batch account create</span></span>](/cli/azure/batch/account#az-batch-account-create) | <span data-ttu-id="c95f8-119">Creates the Batch account.</span><span class="sxs-lookup"><span data-stu-id="c95f8-119">Creates the Batch account.</span></span> |
| [<span data-ttu-id="c95f8-120">az batch account login</span><span class="sxs-lookup"><span data-stu-id="c95f8-120">az batch account login</span></span>](/cli/azure/batch/account#az-batch-account-login) | <span data-ttu-id="c95f8-121">Authenticates against the specified Batch account for further CLI interaction.</span><span class="sxs-lookup"><span data-stu-id="c95f8-121">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="c95f8-122">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="c95f8-122">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#az-batch-pool-node-agent-skus-list) | <span data-ttu-id="c95f8-123">Lists available node agent SKUs and image information.</span><span class="sxs-lookup"><span data-stu-id="c95f8-123">Lists available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="c95f8-124">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="c95f8-124">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#az-batch-pool-create) | <span data-ttu-id="c95f8-125">Creates a pool of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="c95f8-125">Creates a pool of compute nodes.</span></span>  |
| [<span data-ttu-id="c95f8-126">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="c95f8-126">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#az-batch-pool-resize) | <span data-ttu-id="c95f8-127">Resizes the number of running VMs in the specified pool.</span><span class="sxs-lookup"><span data-stu-id="c95f8-127">Resizes the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="c95f8-128">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="c95f8-128">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#az-batch-pool-show) | <span data-ttu-id="c95f8-129">Displays the properties of a pool.</span><span class="sxs-lookup"><span data-stu-id="c95f8-129">Displays the properties of a pool.</span></span>  |
| [<span data-ttu-id="c95f8-130">az batch node list</span><span class="sxs-lookup"><span data-stu-id="c95f8-130">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#az-batch-node-list) | <span data-ttu-id="c95f8-131">Lists all the compute node in the specified pool.</span><span class="sxs-lookup"><span data-stu-id="c95f8-131">Lists all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="c95f8-132">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="c95f8-132">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#az-batch-node-reboot) | <span data-ttu-id="c95f8-133">Reboots the specified compute node.</span><span class="sxs-lookup"><span data-stu-id="c95f8-133">Reboots the specified compute node.</span></span>  |
| [<span data-ttu-id="c95f8-134">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="c95f8-134">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#az-batch-node-delete) | <span data-ttu-id="c95f8-135">Deletes the listed nodes from the specified pool.</span><span class="sxs-lookup"><span data-stu-id="c95f8-135">Deletes the listed nodes from the specified pool.</span></span>  |
| [<span data-ttu-id="c95f8-136">az group delete</span><span class="sxs-lookup"><span data-stu-id="c95f8-136">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="c95f8-137">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="c95f8-137">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c95f8-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="c95f8-138">Next steps</span></span>

<span data-ttu-id="c95f8-139">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="c95f8-139">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
