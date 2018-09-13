---
title: Azure CLI Script Sample - Load balance traffic to VMs for high availability | Microsoft Docs
description: Azure CLI Script Sample - Load balance traffic to VMs for high availability
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 810899c671ea141f45f7ce140c3f862f568a2f87
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869971"
---
# <a name="load-balance-traffic-to-vms-for-high-availability"></a><span data-ttu-id="440ff-103">Load balance traffic to VMs for high availability</span><span class="sxs-lookup"><span data-stu-id="440ff-103">Load balance traffic to VMs for high availability</span></span>

<span data-ttu-id="440ff-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span><span class="sxs-lookup"><span data-stu-id="440ff-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="440ff-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="440ff-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="440ff-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="440ff-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="440ff-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="440ff-107">Clean up deployment</span></span> 

<span data-ttu-id="440ff-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="440ff-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="440ff-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="440ff-109">Script explanation</span></span>

<span data-ttu-id="440ff-110">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="440ff-110">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="440ff-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="440ff-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="440ff-112">Command</span><span class="sxs-lookup"><span data-stu-id="440ff-112">Command</span></span> | <span data-ttu-id="440ff-113">Notes</span><span class="sxs-lookup"><span data-stu-id="440ff-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="440ff-114">az group create</span><span class="sxs-lookup"><span data-stu-id="440ff-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az_group_create) | <span data-ttu-id="440ff-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="440ff-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="440ff-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="440ff-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_create) | <span data-ttu-id="440ff-117">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="440ff-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="440ff-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="440ff-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#az_network_public_ip_create) | <span data-ttu-id="440ff-119">Creates a public IP address with a static IP address and an associated DNS name.</span><span class="sxs-lookup"><span data-stu-id="440ff-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="440ff-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="440ff-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#az_network_lb_create) | <span data-ttu-id="440ff-121">Creates an Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="440ff-121">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="440ff-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="440ff-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#az_network_lb_probe_create) | <span data-ttu-id="440ff-123">Creates a load balancer probe.</span><span class="sxs-lookup"><span data-stu-id="440ff-123">Creates a load balancer probe.</span></span> <span data-ttu-id="440ff-124">A load balancer probe is used to monitor each VM in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="440ff-124">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="440ff-125">If any VM becomes inaccessible, traffic is not routed to the VM.</span><span class="sxs-lookup"><span data-stu-id="440ff-125">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="440ff-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="440ff-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | <span data-ttu-id="440ff-127">Creates a load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="440ff-127">Creates a load balancer rule.</span></span> <span data-ttu-id="440ff-128">In this sample, a rule is created for port 80.</span><span class="sxs-lookup"><span data-stu-id="440ff-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="440ff-129">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the LB set.</span><span class="sxs-lookup"><span data-stu-id="440ff-129">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the LB set.</span></span> |
| [<span data-ttu-id="440ff-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="440ff-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#az_network_lb_inbound_nat_rule_create) | <span data-ttu-id="440ff-131">Creates load balancer Network Address Translation (NAT) rule.</span><span class="sxs-lookup"><span data-stu-id="440ff-131">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="440ff-132">NAT rules map a port of the load balancer to a port on a VM.</span><span class="sxs-lookup"><span data-stu-id="440ff-132">NAT rules map a port of the load balancer to a port on a VM.</span></span> <span data-ttu-id="440ff-133">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="440ff-133">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span></span>  |
| [<span data-ttu-id="440ff-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="440ff-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#az_network_nsg_create) | <span data-ttu-id="440ff-135">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="440ff-135">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="440ff-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="440ff-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#az_network_nsg_rule_create) | <span data-ttu-id="440ff-137">Creates an NSG rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="440ff-137">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="440ff-138">In this sample, port 22 is opened for SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="440ff-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="440ff-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="440ff-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#az_network_nic_create) | <span data-ttu-id="440ff-140">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="440ff-140">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="440ff-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="440ff-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | <span data-ttu-id="440ff-142">Creates an availability set.</span><span class="sxs-lookup"><span data-stu-id="440ff-142">Creates an availability set.</span></span> <span data-ttu-id="440ff-143">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span><span class="sxs-lookup"><span data-stu-id="440ff-143">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="440ff-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="440ff-144">az vm create</span></span>](/cli/azure/vm#az_vm_create) | <span data-ttu-id="440ff-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="440ff-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="440ff-146">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="440ff-146">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="440ff-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="440ff-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | <span data-ttu-id="440ff-148">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="440ff-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="440ff-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="440ff-149">Next steps</span></span>

<span data-ttu-id="440ff-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="440ff-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="440ff-151">Additional Azure Networking CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="440ff-151">Additional Azure Networking CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>