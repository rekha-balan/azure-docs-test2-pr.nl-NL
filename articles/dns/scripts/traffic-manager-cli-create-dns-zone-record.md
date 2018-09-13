---
title: CLI Example - Create a DNS zone and record for a domain name - Azure | Microsoft Docs
description: This Azure CLI script example shows how to create a DNS zone and record for a domain name
services: load-balancer
documentationcenter: traffic-manager
author: vhorne
manager: jeconnoc
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 04/30/2018
ms.author: victorh
ms.openlocfilehash: b8a69b44714a24c78bf4077c27b5bf5633cc56d3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856317"
---
# <a name="azure-cli-script-example-create-a-dns-zone-and-record"></a><span data-ttu-id="13bbc-103">Azure CLI script example: Create a DNS zone and record</span><span class="sxs-lookup"><span data-stu-id="13bbc-103">Azure CLI script example: Create a DNS zone and record</span></span>

<span data-ttu-id="13bbc-104">This Azure CLI script example creates a DNS zone and record for a domain name.</span><span class="sxs-lookup"><span data-stu-id="13bbc-104">This Azure CLI script example creates a DNS zone and record for a domain name.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="13bbc-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="13bbc-105">Sample script</span></span>

```azurecli-interactive

# Create a resource group.
az group create \
  -n myResourceGroup \
  -l eastus

# Create a DNS zone. Substitute zone name "contoso.com" with the values for your own.

az network dns zone create \
  -g MyResourceGroup \
  -n contoso.com

# Create a DNS record. Substitute zone name "contoso.com" and IP address "1.2.3.4* with the values for your own.

az network dns record-set a add-record \
  -g MyResourceGroup \
  -z contoso.com \
  -n www \
  -a 1.2.3.4

# Get a list the DNS records in your zone
az network dns record-set list \
  -g MyResourceGroup \ 
  -z contoso.com
```

## <a name="clean-up-deployment"></a><span data-ttu-id="13bbc-106">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="13bbc-106">Clean up deployment</span></span> 

<span data-ttu-id="13bbc-107">Run the following command to remove the resource group, DNS zone, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="13bbc-107">Run the following command to remove the resource group, DNS zone, and all related resources.</span></span>

```azurecli
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="13bbc-108">Script explanation</span><span class="sxs-lookup"><span data-stu-id="13bbc-108">Script explanation</span></span>

<span data-ttu-id="13bbc-109">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="13bbc-109">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="13bbc-110">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="13bbc-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="13bbc-111">Command</span><span class="sxs-lookup"><span data-stu-id="13bbc-111">Command</span></span> | <span data-ttu-id="13bbc-112">Notes</span><span class="sxs-lookup"><span data-stu-id="13bbc-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="13bbc-113">az group create</span><span class="sxs-lookup"><span data-stu-id="13bbc-113">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="13bbc-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="13bbc-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="13bbc-115">az network dns zone create</span><span class="sxs-lookup"><span data-stu-id="13bbc-115">az network dns zone create</span></span>](/cli/azure/network/dns/zone#az-network-dns-zone-create) | <span data-ttu-id="13bbc-116">Creates an Azure DNS zone.</span><span class="sxs-lookup"><span data-stu-id="13bbc-116">Creates an Azure DNS zone.</span></span> |
| [<span data-ttu-id="13bbc-117">az network dns record-set a add-record</span><span class="sxs-lookup"><span data-stu-id="13bbc-117">az network dns record-set a add-record</span></span>](/cli/azure/network/dns/record-set#az-network-dns-record-set-a-add-record) | <span data-ttu-id="13bbc-118">Adds an *A* record to a DNS zone.</span><span class="sxs-lookup"><span data-stu-id="13bbc-118">Adds an *A* record to a DNS zone.</span></span> |
| [<span data-ttu-id="13bbc-119">az network dns record-set list</span><span class="sxs-lookup"><span data-stu-id="13bbc-119">az network dns record-set list</span></span>](/cli/azure/network/dns/record-set#az-network-dns-record-set-a-list) | <span data-ttu-id="13bbc-120">List all *A* record sets in a DNS zone.</span><span class="sxs-lookup"><span data-stu-id="13bbc-120">List all *A* record sets in a DNS zone.</span></span> |
| [<span data-ttu-id="13bbc-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="13bbc-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az-vm-extension-set) | <span data-ttu-id="13bbc-122">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="13bbc-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="13bbc-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="13bbc-123">Next steps</span></span>

<span data-ttu-id="13bbc-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="13bbc-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

