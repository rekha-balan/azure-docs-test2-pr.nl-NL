---
title: Azure CLI Script Example - Create a Batch AI cluster with a config file | Microsoft Docs
description: Azure CLI Script Example - Create a Batch AI cluster by specifying configuration settings in a JSON file.
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
ms.date: 08/16/2018
ms.author: danlep
ms.openlocfilehash: a1e472d237977d1948c69828d8ec391522896774
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968646"
---
# <a name="cli-example-create-a-batch-ai-cluster-using-a-cluster-configuration-file"></a><span data-ttu-id="93e68-103">CLI example: Create a Batch AI cluster using a cluster configuration file</span><span class="sxs-lookup"><span data-stu-id="93e68-103">CLI example: Create a Batch AI cluster using a cluster configuration file</span></span>

<span data-ttu-id="93e68-104">This script demonstrates how to use a JSON configuration file to specify settings for a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="93e68-104">This script demonstrates how to use a JSON configuration file to specify settings for a Batch AI cluster.</span></span> <span data-ttu-id="93e68-105">Use these settings instead of corresponding command line parameters for `az batchai cluster create`.</span><span class="sxs-lookup"><span data-stu-id="93e68-105">Use these settings instead of corresponding command line parameters for `az batchai cluster create`.</span></span> <span data-ttu-id="93e68-106">A configuration file is useful when you need to mount multiple file systems on the cluster nodes or want to use an identical configuration in several clusters.</span><span class="sxs-lookup"><span data-stu-id="93e68-106">A configuration file is useful when you need to mount multiple file systems on the cluster nodes or want to use an identical configuration in several clusters.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="93e68-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span><span class="sxs-lookup"><span data-stu-id="93e68-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span></span> <span data-ttu-id="93e68-108">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="93e68-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="93e68-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="93e68-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="93e68-110">Example script</span><span class="sxs-lookup"><span data-stu-id="93e68-110">Example script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/batch-ai/create-cluster/create-cluster-config-file.sh "Create Batch AI cluster - configuration file")]

## <a name="clean-up-deployment"></a><span data-ttu-id="93e68-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="93e68-111">Clean up deployment</span></span>

<span data-ttu-id="93e68-112">Run the following commands to remove the resource groups and all resources associated with them.</span><span class="sxs-lookup"><span data-stu-id="93e68-112">Run the following commands to remove the resource groups and all resources associated with them.</span></span>

```azurecli-interactive
# Remove resource group for the cluster.
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="93e68-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="93e68-113">Script explanation</span></span>

<span data-ttu-id="93e68-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="93e68-114">This script uses the following commands.</span></span> <span data-ttu-id="93e68-115">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="93e68-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="93e68-116">Command</span><span class="sxs-lookup"><span data-stu-id="93e68-116">Command</span></span> | <span data-ttu-id="93e68-117">Notes</span><span class="sxs-lookup"><span data-stu-id="93e68-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="93e68-118">az group create</span><span class="sxs-lookup"><span data-stu-id="93e68-118">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="93e68-119">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="93e68-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="93e68-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="93e68-120">az storage account create</span></span>](/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="93e68-121">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="93e68-121">Creates a storage account.</span></span> |
| [<span data-ttu-id="93e68-122">az storage share create</span><span class="sxs-lookup"><span data-stu-id="93e68-122">az storage share create</span></span>](/cli/azure/storage/share#az-storage-share-create) | <span data-ttu-id="93e68-123">Creates a file share in a storage account.</span><span class="sxs-lookup"><span data-stu-id="93e68-123">Creates a file share in a storage account.</span></span> |
| [<span data-ttu-id="93e68-124">az batchai workspace create</span><span class="sxs-lookup"><span data-stu-id="93e68-124">az batchai workspace create</span></span>](/cli/azure/batchai/workspace#az-batchai-workspace-create) | <span data-ttu-id="93e68-125">Creates a Batch AI workspace.</span><span class="sxs-lookup"><span data-stu-id="93e68-125">Creates a Batch AI workspace.</span></span> |
| [<span data-ttu-id="93e68-126">az batchai cluster create</span><span class="sxs-lookup"><span data-stu-id="93e68-126">az batchai cluster create</span></span>](/cli/azure/batchai/cluster#az-batchai-cluster-create) | <span data-ttu-id="93e68-127">Creates a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="93e68-127">Creates a Batch AI cluster.</span></span> |
| [<span data-ttu-id="93e68-128">az batchai cluster show</span><span class="sxs-lookup"><span data-stu-id="93e68-128">az batchai cluster show</span></span>](/cli/azure/batchai/cluster#az-batchai-cluster-show) | <span data-ttu-id="93e68-129">Shows information about a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="93e68-129">Shows information about a Batch AI cluster.</span></span> |
| [<span data-ttu-id="93e68-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="93e68-130">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="93e68-131">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="93e68-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="93e68-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="93e68-132">Next steps</span></span>

<span data-ttu-id="93e68-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="93e68-133">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
