---
title: Azure CLI Script Sample - Create a SignalR Service | Microsoft Docs
description: Azure CLI Script Sample - Create SignalR Service
services: signalr
documentationcenter: signalr
author: sffamily
manager: cfowler
editor: ''
tags: azure-service-management
ms.service: signalr
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: signalr
ms.date: 04/20/2018
ms.author: zhshang
ms.custom: mvc
ms.openlocfilehash: c05003c986786332786e33763834376e148c065e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864425"
---
# <a name="create-a-signalr-service"></a><span data-ttu-id="67f63-103">Create a SignalR Service</span><span class="sxs-lookup"><span data-stu-id="67f63-103">Create a SignalR Service</span></span> 

<span data-ttu-id="67f63-104">This sample script creates a new Azure SignalR Service resource in a new resource group with a random name.</span><span class="sxs-lookup"><span data-stu-id="67f63-104">This sample script creates a new Azure SignalR Service resource in a new resource group with a random name.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="67f63-105">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="67f63-105">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="67f63-106">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="67f63-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="67f63-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="67f63-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="67f63-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="67f63-108">Sample script</span></span>

<span data-ttu-id="67f63-109">This script uses the *signalr* extension for the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="67f63-109">This script uses the *signalr* extension for the Azure CLI.</span></span> <span data-ttu-id="67f63-110">Execute the following command to install the *signalr* extension for the Azure CLI before using this sample script:</span><span class="sxs-lookup"><span data-stu-id="67f63-110">Execute the following command to install the *signalr* extension for the Azure CLI before using this sample script:</span></span>

```azurecli-interactive
az extension add -n signalr
```

<span data-ttu-id="67f63-111">This script creates a new SignalR Service resource and a new resource group.</span><span class="sxs-lookup"><span data-stu-id="67f63-111">This script creates a new SignalR Service resource and a new resource group.</span></span> 

[!code-azurecli-interactive[main](../../../cli_scripts/azure-signalr/create-signalr-service-and-group/create-signalr-service-and-group.sh "Creates a new Azure SignalR Service resource and resource group")]

<span data-ttu-id="67f63-112">Make a note of the actual name generated for the new resource group.</span><span class="sxs-lookup"><span data-stu-id="67f63-112">Make a note of the actual name generated for the new resource group.</span></span> <span data-ttu-id="67f63-113">You will use that resource group name when you want to delete all group resources.</span><span class="sxs-lookup"><span data-stu-id="67f63-113">You will use that resource group name when you want to delete all group resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="67f63-114">Script explanation</span><span class="sxs-lookup"><span data-stu-id="67f63-114">Script explanation</span></span>

<span data-ttu-id="67f63-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="67f63-115">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="67f63-116">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="67f63-116">This script uses the following commands:</span></span>

| <span data-ttu-id="67f63-117">Command</span><span class="sxs-lookup"><span data-stu-id="67f63-117">Command</span></span> | <span data-ttu-id="67f63-118">Notes</span><span class="sxs-lookup"><span data-stu-id="67f63-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="67f63-119">az group create</span><span class="sxs-lookup"><span data-stu-id="67f63-119">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="67f63-120">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="67f63-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="67f63-121">az signalr create</span><span class="sxs-lookup"><span data-stu-id="67f63-121">az signalr create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="67f63-122">Creates an Azure SignalR Service resource.</span><span class="sxs-lookup"><span data-stu-id="67f63-122">Creates an Azure SignalR Service resource.</span></span> |
| [<span data-ttu-id="67f63-123">az signalr key list</span><span class="sxs-lookup"><span data-stu-id="67f63-123">az signalr key list</span></span>](/cli/azure/ext/signalr/signalr/key#ext-signalr-az-signalr-key-list) | <span data-ttu-id="67f63-124">List the keys, which will be used by your application when pushing real-time content updates with SignalR.</span><span class="sxs-lookup"><span data-stu-id="67f63-124">List the keys, which will be used by your application when pushing real-time content updates with SignalR.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="67f63-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="67f63-125">Next steps</span></span>

<span data-ttu-id="67f63-126">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="67f63-126">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span></span>

<span data-ttu-id="67f63-127">Additional Azure SignalR Service CLI script samples can be found in the [Azure SignalR Service documentation](../signalr-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="67f63-127">Additional Azure SignalR Service CLI script samples can be found in the [Azure SignalR Service documentation](../signalr-cli-samples.md).</span></span>
