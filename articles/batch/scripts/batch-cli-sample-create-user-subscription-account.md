---
title: Azure CLI Script Example - Create Batch account - user subscription | Microsoft Docs
description: Azure CLI Script Example - Create a Batch account in user subscription mode
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
ms.openlocfilehash: 14910aaec43e82bb118b5012b382367eac970f73
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869113"
---
# <a name="cli-example-create-a-batch-account-in-user-subscription-mode"></a><span data-ttu-id="0858b-103">CLI example: Create a Batch account in user subscription mode</span><span class="sxs-lookup"><span data-stu-id="0858b-103">CLI example: Create a Batch account in user subscription mode</span></span>

<span data-ttu-id="0858b-104">This script creates an Azure Batch account in user subscription mode.</span><span class="sxs-lookup"><span data-stu-id="0858b-104">This script creates an Azure Batch account in user subscription mode.</span></span> <span data-ttu-id="0858b-105">An account that allocates compute nodes into your subscription must be authenticated via an Azure Active Directory token.</span><span class="sxs-lookup"><span data-stu-id="0858b-105">An account that allocates compute nodes into your subscription must be authenticated via an Azure Active Directory token.</span></span> <span data-ttu-id="0858b-106">The compute nodes allocated count toward your subscription's vCPU (core) quota.</span><span class="sxs-lookup"><span data-stu-id="0858b-106">The compute nodes allocated count toward your subscription's vCPU (core) quota.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0858b-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span><span class="sxs-lookup"><span data-stu-id="0858b-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span></span> <span data-ttu-id="0858b-108">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="0858b-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="0858b-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0858b-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="0858b-110">Example script</span><span class="sxs-lookup"><span data-stu-id="0858b-110">Example script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh "Create Account using user subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0858b-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="0858b-111">Clean up deployment</span></span>

<span data-ttu-id="0858b-112">Run the following command to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="0858b-112">Run the following command to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0858b-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="0858b-113">Script explanation</span></span>

<span data-ttu-id="0858b-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="0858b-114">This script uses the following commands.</span></span> <span data-ttu-id="0858b-115">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="0858b-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="0858b-116">Command</span><span class="sxs-lookup"><span data-stu-id="0858b-116">Command</span></span> | <span data-ttu-id="0858b-117">Notes</span><span class="sxs-lookup"><span data-stu-id="0858b-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0858b-118">az role assignment create</span><span class="sxs-lookup"><span data-stu-id="0858b-118">az role assignment create</span></span>](/cli/azure/role#az-role-assignment-create) | <span data-ttu-id="0858b-119">Create a new role assignment for a user, group, or service principal.</span><span class="sxs-lookup"><span data-stu-id="0858b-119">Create a new role assignment for a user, group, or service principal.</span></span> |
| [<span data-ttu-id="0858b-120">az group create</span><span class="sxs-lookup"><span data-stu-id="0858b-120">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="0858b-121">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="0858b-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0858b-122">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="0858b-122">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#az-keyvault-create) | <span data-ttu-id="0858b-123">Creates a key vault.</span><span class="sxs-lookup"><span data-stu-id="0858b-123">Creates a key vault.</span></span> |
| [<span data-ttu-id="0858b-124">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="0858b-124">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#az-keyvault-set-policy) | <span data-ttu-id="0858b-125">Update the security policy of the specified key vault.</span><span class="sxs-lookup"><span data-stu-id="0858b-125">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="0858b-126">az batch account create</span><span class="sxs-lookup"><span data-stu-id="0858b-126">az batch account create</span></span>](/cli/azure/batch/account#az-batch-account-create) | <span data-ttu-id="0858b-127">Creates the Batch account.</span><span class="sxs-lookup"><span data-stu-id="0858b-127">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="0858b-128">az batch account login</span><span class="sxs-lookup"><span data-stu-id="0858b-128">az batch account login</span></span>](/cli/azure/batch/account#az-batch-account-login) | <span data-ttu-id="0858b-129">Authenticates against the specified Batch account for further CLI interaction.</span><span class="sxs-lookup"><span data-stu-id="0858b-129">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="0858b-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="0858b-130">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="0858b-131">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="0858b-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0858b-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="0858b-132">Next steps</span></span>

<span data-ttu-id="0858b-133">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="0858b-133">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span></span>
