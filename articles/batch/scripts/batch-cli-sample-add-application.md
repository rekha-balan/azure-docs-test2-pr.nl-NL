---
title: Azure CLI Script Example - Add an Application in Batch | Microsoft Docs
description: Azure CLI Script Example - Add an Application in Batch
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
ms.openlocfilehash: 7c38ac560a4fd277e2b19999ab0ac81549a5fa2f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44831012"
---
# <a name="cli-example-add-an-application-to-an-azure-batch-account"></a><span data-ttu-id="89880-103">CLI example: Add an application to an Azure Batch account</span><span class="sxs-lookup"><span data-stu-id="89880-103">CLI example: Add an application to an Azure Batch account</span></span>

<span data-ttu-id="89880-104">This script demonstrates how to add an application for use with an Azure Batch pool or task.</span><span class="sxs-lookup"><span data-stu-id="89880-104">This script demonstrates how to add an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="89880-105">To set up an application to add to your Batch account, package your executable, together with any dependencies, into a zip file.</span><span class="sxs-lookup"><span data-stu-id="89880-105">To set up an application to add to your Batch account, package your executable, together with any dependencies, into a zip file.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="89880-106">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span><span class="sxs-lookup"><span data-stu-id="89880-106">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span></span> <span data-ttu-id="89880-107">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="89880-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="89880-108">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="89880-108">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="89880-109">Example script</span><span class="sxs-lookup"><span data-stu-id="89880-109">Example script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="89880-110">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="89880-110">Clean up deployment</span></span>

<span data-ttu-id="89880-111">Run the following command to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="89880-111">Run the following command to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="89880-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="89880-112">Script explanation</span></span>

<span data-ttu-id="89880-113">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="89880-113">This script uses the following commands.</span></span>
<span data-ttu-id="89880-114">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="89880-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="89880-115">Command</span><span class="sxs-lookup"><span data-stu-id="89880-115">Command</span></span> | <span data-ttu-id="89880-116">Notes</span><span class="sxs-lookup"><span data-stu-id="89880-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="89880-117">az group create</span><span class="sxs-lookup"><span data-stu-id="89880-117">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="89880-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="89880-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="89880-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="89880-119">az storage account create</span></span>](/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="89880-120">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="89880-120">Creates a storage account.</span></span> |
| [<span data-ttu-id="89880-121">az batch account create</span><span class="sxs-lookup"><span data-stu-id="89880-121">az batch account create</span></span>](/cli/azure/batch/account#az-batch-account-create) | <span data-ttu-id="89880-122">Creates the Batch account.</span><span class="sxs-lookup"><span data-stu-id="89880-122">Creates the Batch account.</span></span> |
| [<span data-ttu-id="89880-123">az batch account login</span><span class="sxs-lookup"><span data-stu-id="89880-123">az batch account login</span></span>](/cli/azure/batch/account#az-batch-account-login) | <span data-ttu-id="89880-124">Authenticates against the specified Batch account for further CLI interaction.</span><span class="sxs-lookup"><span data-stu-id="89880-124">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="89880-125">az batch application create</span><span class="sxs-lookup"><span data-stu-id="89880-125">az batch application create</span></span>](/cli/azure/batch/application#az-batch-application-create) | <span data-ttu-id="89880-126">Creates an application.</span><span class="sxs-lookup"><span data-stu-id="89880-126">Creates an application.</span></span>  |
| [<span data-ttu-id="89880-127">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="89880-127">az batch application package create</span></span>](/cli/azure/batch/application/package#az-batch-application-package-create) | <span data-ttu-id="89880-128">Adds an application package to the specified application.</span><span class="sxs-lookup"><span data-stu-id="89880-128">Adds an application package to the specified application.</span></span>  |
| [<span data-ttu-id="89880-129">az batch application set</span><span class="sxs-lookup"><span data-stu-id="89880-129">az batch application set</span></span>](/cli/azure/batch/application#az-batch-application-set) | <span data-ttu-id="89880-130">Updates properties of an application.</span><span class="sxs-lookup"><span data-stu-id="89880-130">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="89880-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="89880-131">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="89880-132">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="89880-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="89880-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="89880-133">Next steps</span></span>

<span data-ttu-id="89880-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="89880-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
