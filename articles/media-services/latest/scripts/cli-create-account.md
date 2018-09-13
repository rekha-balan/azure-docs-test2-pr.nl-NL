---
title: Create a Azure Media Services account - Azure CLI| Microsoft Docs
description: Use the Azure CLI script to create a Azure Media Services account.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: media-services
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/11/2018
ms.author: juliako
ms.openlocfilehash: 0d6d2af598a587cf263612780b419a092ce76d75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866116"
---
# <a name="cli-example-create-an-azure-media-services-account"></a><span data-ttu-id="6b6c9-103">CLI example: Create an Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="6b6c9-103">CLI example: Create an Azure Media Services account</span></span>

<span data-ttu-id="6b6c9-104">The Azure CLI script in this topic shows how to create an Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-104">The Azure CLI script in this topic shows how to create an Azure Media Services account.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6b6c9-105">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-105">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later.</span></span> <span data-ttu-id="6b6c9-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="6b6c9-107">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b6c9-107">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span> 

## <a name="example-script"></a><span data-ttu-id="6b6c9-108">Example script</span><span class="sxs-lookup"><span data-stu-id="6b6c9-108">Example script</span></span>

[!code-azurecli-interactive[main](../../../../cli_scripts/media-services/media-services-create-account/Create-Account.sh "Create Account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6b6c9-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="6b6c9-109">Clean up deployment</span></span>

<span data-ttu-id="6b6c9-110">Run the following command to remove the resource group and all resources associated with it.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-110">Run the following command to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name amsResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6b6c9-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="6b6c9-111">Script explanation</span></span>

<span data-ttu-id="6b6c9-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-112">This script uses the following commands.</span></span> <span data-ttu-id="6b6c9-113">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="6b6c9-114">Command</span><span class="sxs-lookup"><span data-stu-id="6b6c9-114">Command</span></span> | <span data-ttu-id="6b6c9-115">Notes</span><span class="sxs-lookup"><span data-stu-id="6b6c9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6b6c9-116">az group create</span><span class="sxs-lookup"><span data-stu-id="6b6c9-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="6b6c9-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6b6c9-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="6b6c9-118">az storage account create</span></span>](/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="6b6c9-119">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-119">Creates a storage account.</span></span> |
| [<span data-ttu-id="6b6c9-120">az ams account create</span><span class="sxs-lookup"><span data-stu-id="6b6c9-120">az ams account create</span></span>](https://docs.microsoft.com/cli/azure/ams/account?view=azure-cli-latest#az-ams-account-create) | <span data-ttu-id="6b6c9-121">Creates a Media Services account.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-121">Creates a Media Services account.</span></span> |
| [<span data-ttu-id="6b6c9-122">az ams account sp create</span><span class="sxs-lookup"><span data-stu-id="6b6c9-122">az ams account sp create</span></span>](https://docs.microsoft.com/cli/azure/ams/account/sp?view=azure-cli-latest#az-ams-account-sp-create) | <span data-ttu-id="6b6c9-123">Creates a service principal with password and configures its access to an Azure Media Services account.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-123">Creates a service principal with password and configures its access to an Azure Media Services account.</span></span> 
| [<span data-ttu-id="6b6c9-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="6b6c9-124">az group delete</span></span>](/cli/azure/group#az-group-delete) | <span data-ttu-id="6b6c9-125">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="6b6c9-125">Deletes a resource group including all nested resources.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="6b6c9-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b6c9-126">Next steps</span></span>

<span data-ttu-id="6b6c9-127">For more examples, see [Azure CLI samples](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6b6c9-127">For more examples, see [Azure CLI samples](../cli-samples.md).</span></span>
