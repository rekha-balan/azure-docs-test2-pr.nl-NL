---
title: Diagnose a virtual machine network routing problem - Azure CLI | Microsoft Docs
description: In this article, you learn how to diagnose a virtual machine network routing problem using the next hop capability of Azure Network Watcher.
services: network-watcher
documentationcenter: network-watcher
author: jimdial
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: I need to diagnose virtual machine (VM) network routing problem that prevents communication to different destinations.
ms.assetid: ''
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: network-watcher
ms.workload: infrastructure
ms.date: 04/20/2018
ms.author: jdial
ms.custom: ''
ms.openlocfilehash: 15fb39a74047bdeffed0076501f0129eb00de4e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865757"
---
# <a name="diagnose-a-virtual-machine-network-routing-problem---azure-cli"></a><span data-ttu-id="6f203-103">Diagnose a virtual machine network routing problem - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6f203-103">Diagnose a virtual machine network routing problem - Azure CLI</span></span>

<span data-ttu-id="6f203-104">In this article, you deploy a virtual machine (VM), and then check communications to an IP address and URL.</span><span class="sxs-lookup"><span data-stu-id="6f203-104">In this article, you deploy a virtual machine (VM), and then check communications to an IP address and URL.</span></span> <span data-ttu-id="6f203-105">You determine the cause of a communication failure and how you can resolve it.</span><span class="sxs-lookup"><span data-stu-id="6f203-105">You determine the cause of a communication failure and how you can resolve it.</span></span>

<span data-ttu-id="6f203-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="6f203-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6f203-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.28 or later.</span><span class="sxs-lookup"><span data-stu-id="6f203-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.28 or later.</span></span> <span data-ttu-id="6f203-108">To find the installed version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="6f203-108">To find the installed version, run `az --version`.</span></span> <span data-ttu-id="6f203-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6f203-109">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="6f203-110">After you verify the CLI version, run `az login`  to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="6f203-110">After you verify the CLI version, run `az login`  to create a connection with Azure.</span></span> <span data-ttu-id="6f203-111">The CLI commands in this article are formatted to run in a Bash shell.</span><span class="sxs-lookup"><span data-stu-id="6f203-111">The CLI commands in this article are formatted to run in a Bash shell.</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="6f203-112">Create a VM</span><span class="sxs-lookup"><span data-stu-id="6f203-112">Create a VM</span></span>

<span data-ttu-id="6f203-113">Before you can create a VM, you must create a resource group to contain the VM.</span><span class="sxs-lookup"><span data-stu-id="6f203-113">Before you can create a VM, you must create a resource group to contain the VM.</span></span> <span data-ttu-id="6f203-114">Create a resource group with [az group create](/cli/azure/group#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="6f203-114">Create a resource group with [az group create](/cli/azure/group#az-group-create).</span></span> <span data-ttu-id="6f203-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="6f203-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="6f203-116">Create a VM with [az vm create](/cli/azure/vm#az-vm-create).</span><span class="sxs-lookup"><span data-stu-id="6f203-116">Create a VM with [az vm create](/cli/azure/vm#az-vm-create).</span></span> <span data-ttu-id="6f203-117">If SSH keys do not already exist in a default key location, the command creates them.</span><span class="sxs-lookup"><span data-stu-id="6f203-117">If SSH keys do not already exist in a default key location, the command creates them.</span></span> <span data-ttu-id="6f203-118">To use a specific set of keys, use the `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="6f203-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span> <span data-ttu-id="6f203-119">The following example creates a VM named *myVm*:</span><span class="sxs-lookup"><span data-stu-id="6f203-119">The following example creates a VM named *myVm*:</span></span>

```azurecli-interactive
az vm create \
  --resource-group myResourceGroup \
  --name myVm \
  --image UbuntuLTS \
  --generate-ssh-keys
```

<span data-ttu-id="6f203-120">The VM takes a few minutes to create.</span><span class="sxs-lookup"><span data-stu-id="6f203-120">The VM takes a few minutes to create.</span></span> <span data-ttu-id="6f203-121">Don't continue with remaining steps until the VM is created and the CLI returns output.</span><span class="sxs-lookup"><span data-stu-id="6f203-121">Don't continue with remaining steps until the VM is created and the CLI returns output.</span></span>

## <a name="test-network-communication"></a><span data-ttu-id="6f203-122">Test network communication</span><span class="sxs-lookup"><span data-stu-id="6f203-122">Test network communication</span></span>

<span data-ttu-id="6f203-123">To test network communication with Network Watcher, you must first enable a network watcher in the region the VM that you want to test is in, and then use Network Watcher's next hop capability to test communication.</span><span class="sxs-lookup"><span data-stu-id="6f203-123">To test network communication with Network Watcher, you must first enable a network watcher in the region the VM that you want to test is in, and then use Network Watcher's next hop capability to test communication.</span></span>

### <a name="enable-network-watcher"></a><span data-ttu-id="6f203-124">Enable network watcher</span><span class="sxs-lookup"><span data-stu-id="6f203-124">Enable network watcher</span></span>

<span data-ttu-id="6f203-125">If you already have a network watcher enabled in the East US region, skip to [Use next hop](#use-next-hop).</span><span class="sxs-lookup"><span data-stu-id="6f203-125">If you already have a network watcher enabled in the East US region, skip to [Use next hop](#use-next-hop).</span></span> <span data-ttu-id="6f203-126">Use the [az network watcher configure](/cli/azure/network/watcher#az-network-watcher-configure) command to create a network watcher in the East US region:</span><span class="sxs-lookup"><span data-stu-id="6f203-126">Use the [az network watcher configure](/cli/azure/network/watcher#az-network-watcher-configure) command to create a network watcher in the East US region:</span></span>

```azurecli-interactive
az network watcher configure \
  --resource-group NetworkWatcherRG \
  --locations eastus \
  --enabled
```

### <a name="use-next-hop"></a><span data-ttu-id="6f203-127">Use next hop</span><span class="sxs-lookup"><span data-stu-id="6f203-127">Use next hop</span></span>

<span data-ttu-id="6f203-128">Azure automatically creates routes to default destinations.</span><span class="sxs-lookup"><span data-stu-id="6f203-128">Azure automatically creates routes to default destinations.</span></span> <span data-ttu-id="6f203-129">You may create custom routes that override the default routes.</span><span class="sxs-lookup"><span data-stu-id="6f203-129">You may create custom routes that override the default routes.</span></span> <span data-ttu-id="6f203-130">Sometimes, custom routes can cause communication to fail.</span><span class="sxs-lookup"><span data-stu-id="6f203-130">Sometimes, custom routes can cause communication to fail.</span></span> <span data-ttu-id="6f203-131">To test routing from a VM, use [az network watcher show-next-hop](/cli/azure/network/watcher?view=azure-cli-latest#az-network-watcher-show-next-hop) to determine the next routing hop when traffic is destined for a specific address.</span><span class="sxs-lookup"><span data-stu-id="6f203-131">To test routing from a VM, use [az network watcher show-next-hop](/cli/azure/network/watcher?view=azure-cli-latest#az-network-watcher-show-next-hop) to determine the next routing hop when traffic is destined for a specific address.</span></span>

<span data-ttu-id="6f203-132">Test outbound communication from the VM to one of the IP addresses for www.bing.com:</span><span class="sxs-lookup"><span data-stu-id="6f203-132">Test outbound communication from the VM to one of the IP addresses for www.bing.com:</span></span>

```azurecli-interactive
az network watcher show-next-hop \
  --dest-ip 13.107.21.200 \
  --resource-group myResourceGroup \
  --source-ip 10.0.0.4 \
  --vm myVm \
  --nic myVmVMNic \
  --out table
```

<span data-ttu-id="6f203-133">After a few seconds, the output informs you that the **nextHopType** is **Internet**, and that the **routeTableId** is **System Route**.</span><span class="sxs-lookup"><span data-stu-id="6f203-133">After a few seconds, the output informs you that the **nextHopType** is **Internet**, and that the **routeTableId** is **System Route**.</span></span> <span data-ttu-id="6f203-134">This result lets you know that there is a valid route to the destination.</span><span class="sxs-lookup"><span data-stu-id="6f203-134">This result lets you know that there is a valid route to the destination.</span></span>

<span data-ttu-id="6f203-135">Test outbound communication from the VM to 172.31.0.100:</span><span class="sxs-lookup"><span data-stu-id="6f203-135">Test outbound communication from the VM to 172.31.0.100:</span></span>

```azurecli-interactive
az network watcher show-next-hop \
  --dest-ip 172.31.0.100 \
  --resource-group myResourceGroup \
  --source-ip 10.0.0.4 \
  --vm myVm \
  --nic myVmVMNic \
  --out table
```

<span data-ttu-id="6f203-136">The output returned informs you that **None** is the **nextHopType**, and that the **routeTableId** is also **System Route**.</span><span class="sxs-lookup"><span data-stu-id="6f203-136">The output returned informs you that **None** is the **nextHopType**, and that the **routeTableId** is also **System Route**.</span></span> <span data-ttu-id="6f203-137">This result lets you know that, while there is a valid system route to the destination, there is no next hop to route the traffic to the destination.</span><span class="sxs-lookup"><span data-stu-id="6f203-137">This result lets you know that, while there is a valid system route to the destination, there is no next hop to route the traffic to the destination.</span></span>

## <a name="view-details-of-a-route"></a><span data-ttu-id="6f203-138">View details of a route</span><span class="sxs-lookup"><span data-stu-id="6f203-138">View details of a route</span></span>

<span data-ttu-id="6f203-139">To analyze routing further, review the effective routes for the network interface with the [az network nic show-effective-route-table](/cli/azure/network/nic#az-network-nic-show-effective-route-table) command:</span><span class="sxs-lookup"><span data-stu-id="6f203-139">To analyze routing further, review the effective routes for the network interface with the [az network nic show-effective-route-table](/cli/azure/network/nic#az-network-nic-show-effective-route-table) command:</span></span>

```azurecli-interactive
az network nic show-effective-route-table \
  --resource-group myResourceGroup \
  --name myVmVMNic
```

<span data-ttu-id="6f203-140">The following text is included in the returned output:</span><span class="sxs-lookup"><span data-stu-id="6f203-140">The following text is included in the returned output:</span></span>

```azurecli
{
  "additionalProperties": {
    "disableBgpRoutePropagation": false
  },
  "addressPrefix": [
    "0.0.0.0/0"
  ],
  "name": null,
  "nextHopIpAddress": [],
  "nextHopType": "Internet",
  "source": "Default",
  "state": "Active"
},
```

<span data-ttu-id="6f203-141">When you used the `az network watcher show-next-hop` command to test outbound communication to 13.107.21.200 in [Use next hop](#use-next-hop), the route with the **addressPrefix** 0.0.0.0/0\*\* was used to route traffic to the address, since no other route in the output includes the address.</span><span class="sxs-lookup"><span data-stu-id="6f203-141">When you used the `az network watcher show-next-hop` command to test outbound communication to 13.107.21.200 in [Use next hop](#use-next-hop), the route with the **addressPrefix** 0.0.0.0/0\*\* was used to route traffic to the address, since no other route in the output includes the address.</span></span> <span data-ttu-id="6f203-142">By default, all addresses not specified within the address prefix of another route are routed to the internet.</span><span class="sxs-lookup"><span data-stu-id="6f203-142">By default, all addresses not specified within the address prefix of another route are routed to the internet.</span></span>

<span data-ttu-id="6f203-143">When you used the `az network watcher show-next-hop` command to test outbound communication to 172.31.0.100 however, the result informed you that there was no next hop type.</span><span class="sxs-lookup"><span data-stu-id="6f203-143">When you used the `az network watcher show-next-hop` command to test outbound communication to 172.31.0.100 however, the result informed you that there was no next hop type.</span></span> <span data-ttu-id="6f203-144">In the returned output you also see the following text:</span><span class="sxs-lookup"><span data-stu-id="6f203-144">In the returned output you also see the following text:</span></span>

```azurecli
{
  "additionalProperties": {
    "disableBgpRoutePropagation": false
      },
  "addressPrefix": [
    "172.16.0.0/12"
  ],
  "name": null,
  "nextHopIpAddress": [],
  "nextHopType": "None",
  "source": "Default",
  "state": "Active"
},
```

<span data-ttu-id="6f203-145">As you can see in the output from the `az network watcher nic show-effective-route-table` command, though there is a default route to the 172.16.0.0/12 prefix, which includes the 172.31.0.100 address, the **nextHopType** is **None**.</span><span class="sxs-lookup"><span data-stu-id="6f203-145">As you can see in the output from the `az network watcher nic show-effective-route-table` command, though there is a default route to the 172.16.0.0/12 prefix, which includes the 172.31.0.100 address, the **nextHopType** is **None**.</span></span> <span data-ttu-id="6f203-146">Azure creates a default route to 172.16.0.0/12, but doesn't specify a next hop type until there is a reason to.</span><span class="sxs-lookup"><span data-stu-id="6f203-146">Azure creates a default route to 172.16.0.0/12, but doesn't specify a next hop type until there is a reason to.</span></span> <span data-ttu-id="6f203-147">If, for example, you added the 172.16.0.0/12 address range to the address space of the virtual network, Azure changes the **nextHopType** to **Virtual network** for the route.</span><span class="sxs-lookup"><span data-stu-id="6f203-147">If, for example, you added the 172.16.0.0/12 address range to the address space of the virtual network, Azure changes the **nextHopType** to **Virtual network** for the route.</span></span> <span data-ttu-id="6f203-148">A check would then show **Virtual network** as the **nextHopType**.</span><span class="sxs-lookup"><span data-stu-id="6f203-148">A check would then show **Virtual network** as the **nextHopType**.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="6f203-149">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="6f203-149">Clean up resources</span></span>

<span data-ttu-id="6f203-150">When no longer needed, you can use [az group delete](/cli/azure/group#az-group-delete) to remove the resource group and all of the resources it contains:</span><span class="sxs-lookup"><span data-stu-id="6f203-150">When no longer needed, you can use [az group delete](/cli/azure/group#az-group-delete) to remove the resource group and all of the resources it contains:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="6f203-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f203-151">Next steps</span></span>

<span data-ttu-id="6f203-152">In this article, you created a VM and diagnosed network routing from the VM.</span><span class="sxs-lookup"><span data-stu-id="6f203-152">In this article, you created a VM and diagnosed network routing from the VM.</span></span> <span data-ttu-id="6f203-153">You learned that Azure creates several default routes and tested routing to two different destinations.</span><span class="sxs-lookup"><span data-stu-id="6f203-153">You learned that Azure creates several default routes and tested routing to two different destinations.</span></span> <span data-ttu-id="6f203-154">Learn more about [routing in Azure](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and how to [create custom routes](../virtual-network/manage-route-table.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#create-a-route).</span><span class="sxs-lookup"><span data-stu-id="6f203-154">Learn more about [routing in Azure](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and how to [create custom routes](../virtual-network/manage-route-table.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#create-a-route).</span></span>

<span data-ttu-id="6f203-155">For outbound VM connections, you can also determine the latency and allowed and denied network traffic between the VM and an endpoint using Network Watcher's [connection troubleshoot](network-watcher-connectivity-cli.md) capability.</span><span class="sxs-lookup"><span data-stu-id="6f203-155">For outbound VM connections, you can also determine the latency and allowed and denied network traffic between the VM and an endpoint using Network Watcher's [connection troubleshoot](network-watcher-connectivity-cli.md) capability.</span></span> <span data-ttu-id="6f203-156">You can monitor communication between a VM and an endpoint, such as an IP address or URL, over time using the Network Watcher connection monitor capability.</span><span class="sxs-lookup"><span data-stu-id="6f203-156">You can monitor communication between a VM and an endpoint, such as an IP address or URL, over time using the Network Watcher connection monitor capability.</span></span> <span data-ttu-id="6f203-157">To learn how, see [Monitor a network connection](connection-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="6f203-157">To learn how, see [Monitor a network connection](connection-monitor.md).</span></span>