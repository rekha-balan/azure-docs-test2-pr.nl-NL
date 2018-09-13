---
title: Azure CLI Script Sample - Load balance multiple websites with the Azure CLI | Microsoft Docs
description: Azure CLI Script Sample - Load balance multiple websites to the same virtual machine
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
ms.openlocfilehash: 72a780f1870d05a714aaeec879004b6f06d8bb7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867538"
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="3a8b7-103">Load balance multiple websites</span><span class="sxs-lookup"><span data-stu-id="3a8b7-103">Load balance multiple websites</span></span>

<span data-ttu-id="3a8b7-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="3a8b7-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="3a8b7-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3a8b7-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="3a8b7-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3a8b7-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="3a8b7-108">Clean up deployment</span></span> 

<span data-ttu-id="3a8b7-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3a8b7-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3a8b7-110">Script explanation</span></span>

<span data-ttu-id="3a8b7-111">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-111">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="3a8b7-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3a8b7-113">Command</span><span class="sxs-lookup"><span data-stu-id="3a8b7-113">Command</span></span> | <span data-ttu-id="3a8b7-114">Notes</span><span class="sxs-lookup"><span data-stu-id="3a8b7-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3a8b7-115">az group create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az_group_create) | <span data-ttu-id="3a8b7-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3a8b7-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_create) | <span data-ttu-id="3a8b7-118">Creates an Azure virtual network and subnet.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="3a8b7-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#az_network_public_ip_create) | <span data-ttu-id="3a8b7-120">Creates a public IP address with a static IP address and an associated DNS name.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="3a8b7-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#az_network_lb_create) | <span data-ttu-id="3a8b7-122">Creates an Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="3a8b7-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#az_network_lb_probe_create) | <span data-ttu-id="3a8b7-124">Creates a load balancer probe.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-124">Creates a load balancer probe.</span></span> <span data-ttu-id="3a8b7-125">A load balancer probe is used to monitor each VM in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-125">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="3a8b7-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="3a8b7-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | <span data-ttu-id="3a8b7-128">Creates a load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-128">Creates a load balancer rule.</span></span> <span data-ttu-id="3a8b7-129">In this sample, a rule is created for port 80.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="3a8b7-130">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-130">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="3a8b7-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#az_network_lb_frontend_ip_create) | <span data-ttu-id="3a8b7-132">Create a frontend IP address for the Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-132">Create a frontend IP address for the Load Balancer.</span></span> |
| [<span data-ttu-id="3a8b7-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#az_network_lb_address_pool_create) | <span data-ttu-id="3a8b7-134">Creates a backend address pool.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="3a8b7-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#az_network_nic_create) | <span data-ttu-id="3a8b7-136">Creates a virtual network card and attaches it to the virtual network, and subnet.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-136">Creates a virtual network card and attaches it to the virtual network, and subnet.</span></span> |
| [<span data-ttu-id="3a8b7-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#az_network_lb_rule_create) | <span data-ttu-id="3a8b7-138">Creates an availability set.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-138">Creates an availability set.</span></span> <span data-ttu-id="3a8b7-139">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-139">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="3a8b7-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#az_network_nic_ip_config_create) | <span data-ttu-id="3a8b7-141">Creates an IP confiuration.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-141">Creates an IP confiuration.</span></span> <span data-ttu-id="3a8b7-142">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-142">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="3a8b7-143">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-143">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span></span> |
| [<span data-ttu-id="3a8b7-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="3a8b7-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#az_vm_availability_set_create) | <span data-ttu-id="3a8b7-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-145">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="3a8b7-146">This command also specifies the virtual machine image to be used and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-146">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="3a8b7-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="3a8b7-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | <span data-ttu-id="3a8b7-148">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="3a8b7-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a8b7-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="3a8b7-149">Next steps</span></span>

<span data-ttu-id="3a8b7-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="3a8b7-150">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="3a8b7-151">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a8b7-151">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
