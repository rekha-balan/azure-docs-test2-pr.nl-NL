---
title: Azure CLI Script Sample - Create a Windows Server 2016 VM with NLB | Microsoft Docs
description: Azure CLI Script Sample - Create a Windows Server 2016 VM with NLB
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: ''
ms.assetid: ''
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: b58b594b082ad0e0957f799fbe770b83a2bcf70a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564347"
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="e8d25-103">Load balance traffic between highly available virtual machines</span><span class="sxs-lookup"><span data-stu-id="e8d25-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="e8d25-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span><span class="sxs-lookup"><span data-stu-id="e8d25-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="e8d25-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e8d25-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e8d25-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="e8d25-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e8d25-107">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="e8d25-107">Clean up deployment</span></span> 

<span data-ttu-id="e8d25-108">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e8d25-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e8d25-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="e8d25-109">Script explanation</span></span>

<span data-ttu-id="e8d25-110">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="e8d25-110">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="e8d25-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="e8d25-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e8d25-112">Command</span><span class="sxs-lookup"><span data-stu-id="e8d25-112">Command</span></span> | <span data-ttu-id="e8d25-113">Notes</span><span class="sxs-lookup"><span data-stu-id="e8d25-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8d25-114">az group create</span><span class="sxs-lookup"><span data-stu-id="e8d25-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e8d25-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="e8d25-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e8d25-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="e8d25-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="e8d25-117">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="e8d25-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="e8d25-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="e8d25-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="e8d25-119">Creates a public IP address with a static IP address and an associated DNS name.</span><span class="sxs-lookup"><span data-stu-id="e8d25-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="e8d25-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="e8d25-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="e8d25-121">Creates an Azure Network Load Balancer (NLB).</span><span class="sxs-lookup"><span data-stu-id="e8d25-121">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="e8d25-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="e8d25-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="e8d25-123">Creates an NLB probe.</span><span class="sxs-lookup"><span data-stu-id="e8d25-123">Creates an NLB probe.</span></span> <span data-ttu-id="e8d25-124">An NLB probe is used to monitor each VM in the NLB set.</span><span class="sxs-lookup"><span data-stu-id="e8d25-124">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="e8d25-125">If any VM becomes inaccessible, traffic is not routed to the VM.</span><span class="sxs-lookup"><span data-stu-id="e8d25-125">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="e8d25-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="e8d25-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="e8d25-127">Creates an NLB rule.</span><span class="sxs-lookup"><span data-stu-id="e8d25-127">Creates an NLB rule.</span></span> <span data-ttu-id="e8d25-128">In this sample, a rule is created for port 80.</span><span class="sxs-lookup"><span data-stu-id="e8d25-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="e8d25-129">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span><span class="sxs-lookup"><span data-stu-id="e8d25-129">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="e8d25-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="e8d25-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="e8d25-131">Creates an NLB Network Address Translation (NAT) rule.</span><span class="sxs-lookup"><span data-stu-id="e8d25-131">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="e8d25-132">NAT rules map a port of the NLB to a port on a VM.</span><span class="sxs-lookup"><span data-stu-id="e8d25-132">NAT rules map a port of the NLB to a port on a VM.</span></span> <span data-ttu-id="e8d25-133">In this sample, a NAT rule is created for SSH traffic to each VM in the NLB set.</span><span class="sxs-lookup"><span data-stu-id="e8d25-133">In this sample, a NAT rule is created for SSH traffic to each VM in the NLB set.</span></span>  |
| [<span data-ttu-id="e8d25-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="e8d25-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="e8d25-135">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e8d25-135">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="e8d25-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="e8d25-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="e8d25-137">Creates an NSG rule to allow inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="e8d25-137">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="e8d25-138">In this sample, port 22 is opened for SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="e8d25-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="e8d25-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="e8d25-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="e8d25-140">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="e8d25-140">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="e8d25-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="e8d25-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="e8d25-142">Creates an availability set.</span><span class="sxs-lookup"><span data-stu-id="e8d25-142">Creates an availability set.</span></span> <span data-ttu-id="e8d25-143">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span><span class="sxs-lookup"><span data-stu-id="e8d25-143">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="e8d25-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="e8d25-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="e8d25-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="e8d25-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="e8d25-146">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="e8d25-146">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="e8d25-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="e8d25-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e8d25-148">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="e8d25-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8d25-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8d25-149">Next steps</span></span>

<span data-ttu-id="e8d25-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8d25-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e8d25-151">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8d25-151">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
