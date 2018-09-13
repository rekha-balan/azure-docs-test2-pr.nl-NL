---
title: CLI Example - Load balance traffic to VMs for high availability - Azure | Microsoft Docs
description: This Azure CLI script example shows how to load balance traffic to VMs for high availability
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: jeconnoc
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 04/20/2018
ms.author: kumud
ms.openlocfilehash: 039667eae1dc605706100b7eabf0cd144709fd7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870355"
---
# <a name="azure-cli-script-example-load-balance-traffic-to-vms-for-high-availability"></a><span data-ttu-id="be6e0-103">Azure CLI script example: Load balance traffic to VMs for high availability</span><span class="sxs-lookup"><span data-stu-id="be6e0-103">Azure CLI script example: Load balance traffic to VMs for high availability</span></span>

<span data-ttu-id="be6e0-104">This Azure CLI script example creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span><span class="sxs-lookup"><span data-stu-id="be6e0-104">This Azure CLI script example creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="be6e0-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="be6e0-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="be6e0-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="be6e0-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="be6e0-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="be6e0-107">Clean up deployment</span></span> 

<span data-ttu-id="be6e0-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="be6e0-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="be6e0-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="be6e0-109">Script explanation</span></span>

<span data-ttu-id="be6e0-110">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="be6e0-110">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="be6e0-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="be6e0-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="be6e0-112">Command</span><span class="sxs-lookup"><span data-stu-id="be6e0-112">Command</span></span> | <span data-ttu-id="be6e0-113">Notes</span><span class="sxs-lookup"><span data-stu-id="be6e0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="be6e0-114">az group create</span><span class="sxs-lookup"><span data-stu-id="be6e0-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="be6e0-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="be6e0-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="be6e0-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="be6e0-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#az-network-vnet-create) | <span data-ttu-id="be6e0-117">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="be6e0-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="be6e0-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="be6e0-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#az-network-public-ip-create) | <span data-ttu-id="be6e0-119">Creates a public IP address with a static IP address and an associated DNS name.</span><span class="sxs-lookup"><span data-stu-id="be6e0-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="be6e0-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="be6e0-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#az-network-lb-create) | <span data-ttu-id="be6e0-121">Creates an Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="be6e0-121">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="be6e0-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="be6e0-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#az-network-lb-probe-create) | <span data-ttu-id="be6e0-123">Creates a load balancer probe.</span><span class="sxs-lookup"><span data-stu-id="be6e0-123">Creates a load balancer probe.</span></span> <span data-ttu-id="be6e0-124">A load balancer probe is used to monitor each VM in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="be6e0-124">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="be6e0-125">If any VM becomes inaccessible, traffic is not routed to the VM.</span><span class="sxs-lookup"><span data-stu-id="be6e0-125">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="be6e0-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="be6e0-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az-network-lb-rule-create) | <span data-ttu-id="be6e0-127">Creates a load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="be6e0-127">Creates a load balancer rule.</span></span> <span data-ttu-id="be6e0-128">In this sample, a rule is created for port 80.</span><span class="sxs-lookup"><span data-stu-id="be6e0-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="be6e0-129">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the LB set.</span><span class="sxs-lookup"><span data-stu-id="be6e0-129">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the LB set.</span></span> |
| [<span data-ttu-id="be6e0-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="be6e0-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#az-network-lb-inbound-nat-rule-create) | <span data-ttu-id="be6e0-131">Creates load balancer Network Address Translation (NAT) rule.</span><span class="sxs-lookup"><span data-stu-id="be6e0-131">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="be6e0-132">NAT rules map a port of the load balancer to a port on a VM.</span><span class="sxs-lookup"><span data-stu-id="be6e0-132">NAT rules map a port of the load balancer to a port on a VM.</span></span> <span data-ttu-id="be6e0-133">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="be6e0-133">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span></span>  |
| [<span data-ttu-id="be6e0-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="be6e0-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#az-network-nsg-create) | <span data-ttu-id="be6e0-135">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="be6e0-135">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="be6e0-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="be6e0-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#az-network-nsg-rule-create) | <span data-ttu-id="be6e0-137">Creates an NSG rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="be6e0-137">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="be6e0-138">In this sample, port 22 is opened for SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="be6e0-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="be6e0-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="be6e0-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#az-network-nic-create) | <span data-ttu-id="be6e0-140">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="be6e0-140">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="be6e0-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="be6e0-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az-network-lb-rule-create) | <span data-ttu-id="be6e0-142">Creates an availability set.</span><span class="sxs-lookup"><span data-stu-id="be6e0-142">Creates an availability set.</span></span> <span data-ttu-id="be6e0-143">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span><span class="sxs-lookup"><span data-stu-id="be6e0-143">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="be6e0-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="be6e0-144">az vm create</span></span>](/cli/azure/vm#az-vm-create) | <span data-ttu-id="be6e0-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="be6e0-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="be6e0-146">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="be6e0-146">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="be6e0-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="be6e0-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az-vm-extension-set) | <span data-ttu-id="be6e0-148">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="be6e0-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="be6e0-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="be6e0-149">Next steps</span></span>

<span data-ttu-id="be6e0-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="be6e0-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="be6e0-151">Additional Azure Networking CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="be6e0-151">Additional Azure Networking CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>