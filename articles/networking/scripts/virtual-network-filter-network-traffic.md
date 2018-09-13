---
title: Azure CLI script sample - Filter VM network traffic | Microsoft Docs
description: Azure CLI script sample - Filter inbound and outbound VM network traffic.
services: virtual-network
documentationcenter: virtual-network
author: jimdial
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
ms.author: jdial
ms.openlocfilehash: 07211d7b6dccd377f94308da5c572255ba5727c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857516"
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="e9827-103">Filter inbound and outbound VM network traffic</span><span class="sxs-lookup"><span data-stu-id="e9827-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="e9827-104">This script sample creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="e9827-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="e9827-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span><span class="sxs-lookup"><span data-stu-id="e9827-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="e9827-106">After running the script, you will have one virtual machine with two NICs.</span><span class="sxs-lookup"><span data-stu-id="e9827-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="e9827-107">Each NIC is connected to a different subnet.</span><span class="sxs-lookup"><span data-stu-id="e9827-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e9827-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="e9827-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e9827-109">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="e9827-109">Clean up deployment</span></span> 

<span data-ttu-id="e9827-110">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e9827-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e9827-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="e9827-111">Script explanation</span></span>

<span data-ttu-id="e9827-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span><span class="sxs-lookup"><span data-stu-id="e9827-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="e9827-113">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="e9827-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="e9827-114">Command</span><span class="sxs-lookup"><span data-stu-id="e9827-114">Command</span></span> | <span data-ttu-id="e9827-115">Notes</span><span class="sxs-lookup"><span data-stu-id="e9827-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e9827-116">az group create</span><span class="sxs-lookup"><span data-stu-id="e9827-116">az group create</span></span>](/cli/azure/group#az_group_create) | <span data-ttu-id="e9827-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="e9827-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e9827-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="e9827-118">az network vnet create</span></span>](/cli/azure/network/vnet#az_network_vnet_create) | <span data-ttu-id="e9827-119">Creates an Azure virtual network and front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="e9827-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="e9827-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="e9827-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_create) | <span data-ttu-id="e9827-121">Creates a back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="e9827-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="e9827-122">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="e9827-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_update) | <span data-ttu-id="e9827-123">Associates NSGs to subnets.</span><span class="sxs-lookup"><span data-stu-id="e9827-123">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="e9827-124">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="e9827-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#az_network_public_ip_create) | <span data-ttu-id="e9827-125">Creates a public IP address to access the VM from the Internet.</span><span class="sxs-lookup"><span data-stu-id="e9827-125">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="e9827-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="e9827-126">az network nic create</span></span>](/cli/azure/network/nic#az_network_nic_create) | <span data-ttu-id="e9827-127">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="e9827-127">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="e9827-128">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="e9827-128">az network nsg create</span></span>](/cli/azure/network/nsg#az_network_nsg_create) | <span data-ttu-id="e9827-129">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="e9827-129">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="e9827-130">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="e9827-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#az_network_nsg_rule_create) |<span data-ttu-id="e9827-131">Creates NSG rules that allow or block specific ports to specific subnets.</span><span class="sxs-lookup"><span data-stu-id="e9827-131">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="e9827-132">az vm create</span><span class="sxs-lookup"><span data-stu-id="e9827-132">az vm create</span></span>](/cli/azure/vm#az_vm_create) | <span data-ttu-id="e9827-133">Creates virtual machines and attaches a NIC to each VM.</span><span class="sxs-lookup"><span data-stu-id="e9827-133">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="e9827-134">This command also specifies the virtual machine image to use and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="e9827-134">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="e9827-135">az group delete</span><span class="sxs-lookup"><span data-stu-id="e9827-135">az group delete</span></span>](/cli/azure/group#az_group_delete) | <span data-ttu-id="e9827-136">Deletes a resource group and all resources it contains.</span><span class="sxs-lookup"><span data-stu-id="e9827-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9827-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="e9827-137">Next steps</span></span>

<span data-ttu-id="e9827-138">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="e9827-138">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span></span>

<span data-ttu-id="e9827-139">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="e9827-139">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>