---
title: Azure CLI script sample - Route traffic through a network virtual appliance | Microsoft Docs
description: Azure CLI script sample - Route traffic through a firewall network virtual appliance.
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
ms.openlocfilehash: 62077f45d96e96a7fef35cf025740849d2b99445
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869394"
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="1ea24-103">Route traffic through a network virtual appliance</span><span class="sxs-lookup"><span data-stu-id="1ea24-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="1ea24-104">This script sample creates a virtual network with front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="1ea24-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="1ea24-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span><span class="sxs-lookup"><span data-stu-id="1ea24-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="1ea24-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span><span class="sxs-lookup"><span data-stu-id="1ea24-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="1ea24-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="1ea24-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1ea24-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="1ea24-108">Clean up deployment</span></span> 

<span data-ttu-id="1ea24-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="1ea24-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="1ea24-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="1ea24-110">Script explanation</span></span>

<span data-ttu-id="1ea24-111">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span><span class="sxs-lookup"><span data-stu-id="1ea24-111">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="1ea24-112">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="1ea24-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="1ea24-113">Command</span><span class="sxs-lookup"><span data-stu-id="1ea24-113">Command</span></span> | <span data-ttu-id="1ea24-114">Notes</span><span class="sxs-lookup"><span data-stu-id="1ea24-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1ea24-115">az group create</span><span class="sxs-lookup"><span data-stu-id="1ea24-115">az group create</span></span>](/cli/azure/group#az_group_create) | <span data-ttu-id="1ea24-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="1ea24-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1ea24-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="1ea24-117">az network vnet create</span></span>](/cli/azure/network/vnet#az_network_vnet_create) | <span data-ttu-id="1ea24-118">Creates an Azure virtual network and front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="1ea24-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="1ea24-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="1ea24-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_create) | <span data-ttu-id="1ea24-120">Creates back-end and DMZ subnets.</span><span class="sxs-lookup"><span data-stu-id="1ea24-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="1ea24-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="1ea24-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#az_network_public_ip_create) | <span data-ttu-id="1ea24-122">Creates a public IP address to access the VM from the Internet.</span><span class="sxs-lookup"><span data-stu-id="1ea24-122">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="1ea24-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="1ea24-123">az network nic create</span></span>](/cli/azure/network/nic#az_network_nic_create) | <span data-ttu-id="1ea24-124">Creates a virtual network interface and enable IP forwarding for it.</span><span class="sxs-lookup"><span data-stu-id="1ea24-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="1ea24-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="1ea24-125">az network nsg create</span></span>](/cli/azure/network/nsg#az_network_nsg_create) | <span data-ttu-id="1ea24-126">Creates a network security group (NSG).</span><span class="sxs-lookup"><span data-stu-id="1ea24-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="1ea24-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="1ea24-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#az_network_nsg_rule_create) | <span data-ttu-id="1ea24-128">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span><span class="sxs-lookup"><span data-stu-id="1ea24-128">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="1ea24-129">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="1ea24-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_update)| <span data-ttu-id="1ea24-130">Associates the NSGs and route tables to subnets.</span><span class="sxs-lookup"><span data-stu-id="1ea24-130">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="1ea24-131">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="1ea24-131">az network route-table create</span></span>](/cli/azure/network/route-table#az-network-route-table-create)| <span data-ttu-id="1ea24-132">Creates a route table for all routes.</span><span class="sxs-lookup"><span data-stu-id="1ea24-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="1ea24-133">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="1ea24-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#az-network-route-table-route-create)| <span data-ttu-id="1ea24-134">Creates routes to route traffic between subnets and the Internet through the VM.</span><span class="sxs-lookup"><span data-stu-id="1ea24-134">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="1ea24-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="1ea24-135">az vm create</span></span>](/cli/azure/vm#az_vm_create) | <span data-ttu-id="1ea24-136">Creates a virtual machine and attaches the NIC to it.</span><span class="sxs-lookup"><span data-stu-id="1ea24-136">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="1ea24-137">This command also specifies the virtual machine image to use and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="1ea24-137">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="1ea24-138">az group delete</span><span class="sxs-lookup"><span data-stu-id="1ea24-138">az group delete</span></span>](/cli/azure/group#az_group_delete) | <span data-ttu-id="1ea24-139">Deletes a resource group and all resources it contains.</span><span class="sxs-lookup"><span data-stu-id="1ea24-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1ea24-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ea24-140">Next steps</span></span>

<span data-ttu-id="1ea24-141">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="1ea24-141">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure).</span></span>

<span data-ttu-id="1ea24-142">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="1ea24-142">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>