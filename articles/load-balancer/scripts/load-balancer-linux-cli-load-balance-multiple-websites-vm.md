---
title: CLI Example - Load balance multiple websites with the Azure CLI | Microsoft Docs
description: This Azure CLI script example shows how to load balance multiple websites to the same virtual machine
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
ms.openlocfilehash: a8a7514624387d0fc00d32e4d47042e4a3b130f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865920"
---
# <a name="azure-cli-script-example-load-balance-multiple-websites"></a><span data-ttu-id="58934-103">Azure CLI script example: Load balance multiple websites</span><span class="sxs-lookup"><span data-stu-id="58934-103">Azure CLI script example: Load balance multiple websites</span></span>

<span data-ttu-id="58934-104">This Azure CLI script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span><span class="sxs-lookup"><span data-stu-id="58934-104">This Azure CLI script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="58934-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span><span class="sxs-lookup"><span data-stu-id="58934-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="58934-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span><span class="sxs-lookup"><span data-stu-id="58934-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="58934-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="58934-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="58934-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="58934-108">Clean up deployment</span></span> 

<span data-ttu-id="58934-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="58934-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="58934-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="58934-110">Script explanation</span></span>

<span data-ttu-id="58934-111">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="58934-111">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="58934-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="58934-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="58934-113">Command</span><span class="sxs-lookup"><span data-stu-id="58934-113">Command</span></span> | <span data-ttu-id="58934-114">Notes</span><span class="sxs-lookup"><span data-stu-id="58934-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="58934-115">az group create</span><span class="sxs-lookup"><span data-stu-id="58934-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="58934-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="58934-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="58934-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="58934-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#az-network-vnet-create) | <span data-ttu-id="58934-118">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="58934-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="58934-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="58934-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#az-network-public-ip-create) | <span data-ttu-id="58934-120">Creates a public IP address with a static IP address and an associated DNS name.</span><span class="sxs-lookup"><span data-stu-id="58934-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="58934-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="58934-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#az-network-lb-create) | <span data-ttu-id="58934-122">Creates an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="58934-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="58934-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="58934-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#az-network-lb-probe-create) | <span data-ttu-id="58934-124">Creates a load balancer probe.</span><span class="sxs-lookup"><span data-stu-id="58934-124">Creates a load balancer probe.</span></span> <span data-ttu-id="58934-125">A load balancer probe is used to monitor each VM in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="58934-125">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="58934-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span><span class="sxs-lookup"><span data-stu-id="58934-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="58934-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="58934-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az-network-lb-rule-create) | <span data-ttu-id="58934-128">Creates a load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="58934-128">Creates a load balancer rule.</span></span> <span data-ttu-id="58934-129">In this sample, a rule is created for port 80.</span><span class="sxs-lookup"><span data-stu-id="58934-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="58934-130">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="58934-130">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="58934-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="58934-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#az-network-lb-frontend-ip-create) | <span data-ttu-id="58934-132">Create a frontend IP address for the Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="58934-132">Create a frontend IP address for the Load Balancer.</span></span> |
| [<span data-ttu-id="58934-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="58934-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#az-network-lb-address-pool-create) | <span data-ttu-id="58934-134">Creates a backend address pool.</span><span class="sxs-lookup"><span data-stu-id="58934-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="58934-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="58934-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#az-network-nic-create) | <span data-ttu-id="58934-136">Creates a virtual network card and attaches it to the virtual network, and subnet.</span><span class="sxs-lookup"><span data-stu-id="58934-136">Creates a virtual network card and attaches it to the virtual network, and subnet.</span></span> |
| [<span data-ttu-id="58934-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="58934-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az-network-lb-rule-create) | <span data-ttu-id="58934-138">Creates an availability set.</span><span class="sxs-lookup"><span data-stu-id="58934-138">Creates an availability set.</span></span> <span data-ttu-id="58934-139">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span><span class="sxs-lookup"><span data-stu-id="58934-139">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="58934-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="58934-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#az-network-nic-ip-config-create) | <span data-ttu-id="58934-141">Creates an IP confiuration.</span><span class="sxs-lookup"><span data-stu-id="58934-141">Creates an IP confiuration.</span></span> <span data-ttu-id="58934-142">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="58934-142">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="58934-143">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span><span class="sxs-lookup"><span data-stu-id="58934-143">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span></span> |
| [<span data-ttu-id="58934-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="58934-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#az-vm-availability-set-create) | <span data-ttu-id="58934-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="58934-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="58934-146">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="58934-146">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="58934-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="58934-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az-vm-extension-set) | <span data-ttu-id="58934-148">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="58934-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="58934-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="58934-149">Next steps</span></span>

<span data-ttu-id="58934-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="58934-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="58934-151">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58934-151">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
