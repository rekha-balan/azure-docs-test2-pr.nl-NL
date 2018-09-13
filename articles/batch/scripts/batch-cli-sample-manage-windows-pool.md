---
title: Azure CLI Script Example - Windows Pool in Batch | Microsoft Docs
description: Azure CLI Script Example - Create and manage a Windows pool in Batch
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
ms.openlocfilehash: f442dfb7e8f207e8c72d901eca99899c0f830652
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866748"
---
# <a name="cli-example-create-and-manage-a-windows-pool-in-azure-batch"></a><span data-ttu-id="d49f1-103">CLI example: Create and manage a Windows pool in Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d49f1-103">CLI example: Create and manage a Windows pool in Azure Batch</span></span>

<span data-ttu-id="d49f1-104">This script demonstrates some of the commands available in the Azure CLI to create and manage a pool of Windows compute nodes in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d49f1-104">This script demonstrates some of the commands available in the Azure CLI to create and manage a pool of Windows compute nodes in Azure Batch.</span></span> <span data-ttu-id="d49f1-105">A Windows pool can be configured in two ways, with either a Cloud Services configuration or a Virtual Machine configuration.</span><span class="sxs-lookup"><span data-stu-id="d49f1-105">A Windows pool can be configured in two ways, with either a Cloud Services configuration or a Virtual Machine configuration.</span></span> <span data-ttu-id="d49f1-106">This example shows how to create a Windows pool with the Cloud Services configuration.</span><span class="sxs-lookup"><span data-stu-id="d49f1-106">This example shows how to create a Windows pool with the Cloud Services configuration.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d49f1-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span><span class="sxs-lookup"><span data-stu-id="d49f1-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span></span> <span data-ttu-id="d49f1-108">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="d49f1-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="d49f1-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d49f1-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="d49f1-110">Example script</span><span class="sxs-lookup"><span data-stu-id="d49f1-110">Example script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Windows Cloud Services Pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d49f1-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="d49f1-111">Clean up deployment</span></span>

<span data-ttu-id="d49f1-112">Run the following command to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="d49f1-112">Run the following command to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d49f1-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="d49f1-113">Script explanation</span></span>

<span data-ttu-id="d49f1-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="d49f1-114">This script uses the following commands.</span></span> <span data-ttu-id="d49f1-115">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="d49f1-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d49f1-116">Command</span><span class="sxs-lookup"><span data-stu-id="d49f1-116">Command</span></span> | <span data-ttu-id="d49f1-117">Notes</span><span class="sxs-lookup"><span data-stu-id="d49f1-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d49f1-118">az group create</span><span class="sxs-lookup"><span data-stu-id="d49f1-118">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="d49f1-119">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="d49f1-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d49f1-120">az batch account create</span><span class="sxs-lookup"><span data-stu-id="d49f1-120">az batch account create</span></span>](/cli/azure/batch/account#az-batch-account-create) | <span data-ttu-id="d49f1-121">Creates the Batch account.</span><span class="sxs-lookup"><span data-stu-id="d49f1-121">Creates the Batch account.</span></span> |
| [<span data-ttu-id="d49f1-122">az batch account login</span><span class="sxs-lookup"><span data-stu-id="d49f1-122">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#az-batch-account-login) | <span data-ttu-id="d49f1-123">Authenticates against the specified Batch account for further CLI interaction.</span><span class="sxs-lookup"><span data-stu-id="d49f1-123">Authenticates against the specified Batch account for further CLI interaction.</span></span> |
| [<span data-ttu-id="d49f1-124">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="d49f1-124">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#az-batch-pool-create) | <span data-ttu-id="d49f1-125">Creates a pool of compute nodes.</span><span class="sxs-lookup"><span data-stu-id="d49f1-125">Creates a pool of compute nodes.</span></span>  |
| [<span data-ttu-id="d49f1-126">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="d49f1-126">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#az-batch-pool-set) | <span data-ttu-id="d49f1-127">Updates the properties of a pool.</span><span class="sxs-lookup"><span data-stu-id="d49f1-127">Updates the properties of a pool.</span></span>  |
| [<span data-ttu-id="d49f1-128">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="d49f1-128">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#az-batch-pool-autoscale-enable) | <span data-ttu-id="d49f1-129">Enables auto-scaling on a pool and applies a formula.</span><span class="sxs-lookup"><span data-stu-id="d49f1-129">Enables auto-scaling on a pool and applies a formula.</span></span>  |
| [<span data-ttu-id="d49f1-130">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="d49f1-130">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#az-batch-pool-show) | <span data-ttu-id="d49f1-131">Displays the properties of a pool.</span><span class="sxs-lookup"><span data-stu-id="d49f1-131">Displays the properties of a pool.</span></span>  |
| [<span data-ttu-id="d49f1-132">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="d49f1-132">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#az-batch-pool-autoscale-disable) | <span data-ttu-id="d49f1-133">Disables auto-scaling on a pool.</span><span class="sxs-lookup"><span data-stu-id="d49f1-133">Disables auto-scaling on a pool.</span></span> |
| [<span data-ttu-id="d49f1-134">az group delete</span><span class="sxs-lookup"><span data-stu-id="d49f1-134">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="d49f1-135">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="d49f1-135">Deletes a resource group including all nested resources.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d49f1-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="d49f1-136">Next steps</span></span>

<span data-ttu-id="d49f1-137">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="d49f1-137">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
