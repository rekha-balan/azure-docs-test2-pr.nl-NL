---
title: Azure CLI Script Sample - Peer two virtual networks | Microsoft Docs
description: Azure CLI Script Sample - Peer two virtual networks
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 8ad1e7de85f851b5db6764175bc1136dd19d418d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864671"
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="515d2-103">Peer two virtual networks</span><span class="sxs-lookup"><span data-stu-id="515d2-103">Peer two virtual networks</span></span>

<span data-ttu-id="515d2-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span><span class="sxs-lookup"><span data-stu-id="515d2-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="515d2-105">After running the script, you will create a peering between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="515d2-105">After running the script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="515d2-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="515d2-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="515d2-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="515d2-107">Clean up deployment</span></span> 

<span data-ttu-id="515d2-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="515d2-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="515d2-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="515d2-109">Script explanation</span></span>

<span data-ttu-id="515d2-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="515d2-110">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="515d2-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="515d2-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="515d2-112">Command</span><span class="sxs-lookup"><span data-stu-id="515d2-112">Command</span></span> | <span data-ttu-id="515d2-113">Notes</span><span class="sxs-lookup"><span data-stu-id="515d2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="515d2-114">az group create</span><span class="sxs-lookup"><span data-stu-id="515d2-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az_group_create) | <span data-ttu-id="515d2-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="515d2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="515d2-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="515d2-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_create) | <span data-ttu-id="515d2-117">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="515d2-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="515d2-118">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="515d2-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#az_network_vnet_peering_create) | <span data-ttu-id="515d2-119">Creates a peering between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="515d2-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="515d2-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="515d2-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | <span data-ttu-id="515d2-121">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="515d2-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="515d2-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="515d2-122">Next steps</span></span>

<span data-ttu-id="515d2-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="515d2-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="515d2-124">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="515d2-124">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span></span>
