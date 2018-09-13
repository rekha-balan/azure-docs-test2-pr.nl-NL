---
title: Create a complete Linux environment with the Azure CLI 1.0 | Microsoft Docs
description: Create storage, a Linux VM, a virtual network and subnet, a load balancer, an NIC, a public IP, and a network security group, all from the ground up by using the Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: d87e4ff70e98c31d760d983bf7dfe9241b5e5a4a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556653"
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="8b870-103">Create a complete Linux environment with the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8b870-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="8b870-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span><span class="sxs-lookup"><span data-stu-id="8b870-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="8b870-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span><span class="sxs-lookup"><span data-stu-id="8b870-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="8b870-106">Then you can move on to more complex networks and environments.</span><span class="sxs-lookup"><span data-stu-id="8b870-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="8b870-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span><span class="sxs-lookup"><span data-stu-id="8b870-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="8b870-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b870-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8b870-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span><span class="sxs-lookup"><span data-stu-id="8b870-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="8b870-110">The environment contains:</span><span class="sxs-lookup"><span data-stu-id="8b870-110">The environment contains:</span></span>

* <span data-ttu-id="8b870-111">Two VMs inside an availability set.</span><span class="sxs-lookup"><span data-stu-id="8b870-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="8b870-112">A load balancer with a load-balancing rule on port 80.</span><span class="sxs-lookup"><span data-stu-id="8b870-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="8b870-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span><span class="sxs-lookup"><span data-stu-id="8b870-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

![Basic environment overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/create-cli-complete/environment_overview.png)

<span data-ttu-id="8b870-115">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="8b870-115">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="8b870-116">You also need a JSON parsing tool.</span><span class="sxs-lookup"><span data-stu-id="8b870-116">You also need a JSON parsing tool.</span></span> <span data-ttu-id="8b870-117">This example uses [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="8b870-117">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8b870-118">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="8b870-118">CLI versions to complete the task</span></span>
<span data-ttu-id="8b870-119">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="8b870-119">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="8b870-120">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="8b870-120">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8b870-121">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="8b870-121">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="8b870-122">Quick commands</span><span class="sxs-lookup"><span data-stu-id="8b870-122">Quick commands</span></span>
<span data-ttu-id="8b870-123">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span><span class="sxs-lookup"><span data-stu-id="8b870-123">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="8b870-124">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="8b870-124">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="8b870-125">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="8b870-125">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="8b870-126">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="8b870-126">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8b870-127">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="8b870-127">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="8b870-128">Create the resource group.</span><span class="sxs-lookup"><span data-stu-id="8b870-128">Create the resource group.</span></span> <span data-ttu-id="8b870-129">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span><span class="sxs-lookup"><span data-stu-id="8b870-129">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="8b870-130">Verify the resource group by using the JSON parser:</span><span class="sxs-lookup"><span data-stu-id="8b870-130">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="8b870-131">Create the storage account.</span><span class="sxs-lookup"><span data-stu-id="8b870-131">Create the storage account.</span></span> <span data-ttu-id="8b870-132">The following example creates a storage account named `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="8b870-132">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="8b870-133">(The storage account name must be unique, so provide your own unique name.)</span><span class="sxs-lookup"><span data-stu-id="8b870-133">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="8b870-134">Verify the storage account by using the JSON parser:</span><span class="sxs-lookup"><span data-stu-id="8b870-134">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="8b870-135">Create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="8b870-135">Create the virtual network.</span></span> <span data-ttu-id="8b870-136">The following example creates a virtual network named `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="8b870-136">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="8b870-137">Create a subnet.</span><span class="sxs-lookup"><span data-stu-id="8b870-137">Create a subnet.</span></span> <span data-ttu-id="8b870-138">The following example creates a subnet named `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="8b870-138">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="8b870-139">Verify the virtual network and subnet by using the JSON parser:</span><span class="sxs-lookup"><span data-stu-id="8b870-139">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="8b870-140">Create a public IP.</span><span class="sxs-lookup"><span data-stu-id="8b870-140">Create a public IP.</span></span> <span data-ttu-id="8b870-141">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="8b870-141">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="8b870-142">(The DNS name must be unique, so provide your own unique name.)</span><span class="sxs-lookup"><span data-stu-id="8b870-142">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="8b870-143">Create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b870-143">Create the load balancer.</span></span> <span data-ttu-id="8b870-144">The following example creates a load balancer named `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="8b870-144">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="8b870-145">Create a front-end IP pool for the load balancer, and associate the public IP.</span><span class="sxs-lookup"><span data-stu-id="8b870-145">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="8b870-146">The following example creates a front-end IP pool named `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="8b870-146">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="8b870-147">Create the back-end IP pool for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b870-147">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="8b870-148">The following example creates a back-end IP pool named `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="8b870-148">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="8b870-149">Create SSH inbound network address translation (NAT) rules for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b870-149">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="8b870-150">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="8b870-150">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="8b870-151">Create the web inbound NAT rules for the load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b870-151">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="8b870-152">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="8b870-152">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="8b870-153">Create the load balancer health probe.</span><span class="sxs-lookup"><span data-stu-id="8b870-153">Create the load balancer health probe.</span></span> <span data-ttu-id="8b870-154">The following example creates a TCP probe named `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="8b870-154">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="8b870-155">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span><span class="sxs-lookup"><span data-stu-id="8b870-155">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="8b870-156">Create the first network interface card (NIC).</span><span class="sxs-lookup"><span data-stu-id="8b870-156">Create the first network interface card (NIC).</span></span> <span data-ttu-id="8b870-157">Replace the `#####-###-###` sections with your own Azure subscription ID.</span><span class="sxs-lookup"><span data-stu-id="8b870-157">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="8b870-158">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span><span class="sxs-lookup"><span data-stu-id="8b870-158">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="8b870-159">You can also view your subscription ID with `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="8b870-159">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="8b870-160">The following example creates a NIC named `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="8b870-160">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="8b870-161">Create the second NIC.</span><span class="sxs-lookup"><span data-stu-id="8b870-161">Create the second NIC.</span></span> <span data-ttu-id="8b870-162">The following example creates a NIC named `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="8b870-162">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="8b870-163">Verify the two NICs by using the JSON parser:</span><span class="sxs-lookup"><span data-stu-id="8b870-163">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="8b870-164">Create the network security group.</span><span class="sxs-lookup"><span data-stu-id="8b870-164">Create the network security group.</span></span> <span data-ttu-id="8b870-165">The following example creates a network security group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="8b870-165">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="8b870-166">Add two inbound rules for the network security group.</span><span class="sxs-lookup"><span data-stu-id="8b870-166">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="8b870-167">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="8b870-167">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="8b870-168">Verify the network security group and inbound rules by using the JSON parser:</span><span class="sxs-lookup"><span data-stu-id="8b870-168">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="8b870-169">Bind the network security group to the two NICs:</span><span class="sxs-lookup"><span data-stu-id="8b870-169">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="8b870-170">Create the availability set.</span><span class="sxs-lookup"><span data-stu-id="8b870-170">Create the availability set.</span></span> <span data-ttu-id="8b870-171">The following example creates an availability set named `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="8b870-171">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="8b870-172">Create the first Linux VM.</span><span class="sxs-lookup"><span data-stu-id="8b870-172">Create the first Linux VM.</span></span> <span data-ttu-id="8b870-173">The following example creates a VM named `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="8b870-173">The following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="8b870-174">Create the second Linux VM.</span><span class="sxs-lookup"><span data-stu-id="8b870-174">Create the second Linux VM.</span></span> <span data-ttu-id="8b870-175">The following example creates a VM named `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="8b870-175">The following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="8b870-176">Use the JSON parser to verify that everything that was built:</span><span class="sxs-lookup"><span data-stu-id="8b870-176">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="8b870-177">Export your new environment to a template to quickly re-create new instances:</span><span class="sxs-lookup"><span data-stu-id="8b870-177">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="8b870-178">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="8b870-178">Detailed walkthrough</span></span>
<span data-ttu-id="8b870-179">The detailed steps that follow explain what each command is doing as you build out your environment.</span><span class="sxs-lookup"><span data-stu-id="8b870-179">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="8b870-180">These concepts are helpful when you build your own custom environments for development or production.</span><span class="sxs-lookup"><span data-stu-id="8b870-180">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="8b870-181">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="8b870-181">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="8b870-182">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="8b870-182">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8b870-183">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="8b870-183">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="8b870-184">Create resource groups and choose deployment locations</span><span class="sxs-lookup"><span data-stu-id="8b870-184">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="8b870-185">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span><span class="sxs-lookup"><span data-stu-id="8b870-185">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="8b870-186">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span><span class="sxs-lookup"><span data-stu-id="8b870-186">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="8b870-187">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-187">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="8b870-188">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="8b870-188">Create a storage account</span></span>
<span data-ttu-id="8b870-189">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span><span class="sxs-lookup"><span data-stu-id="8b870-189">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="8b870-190">You create storage accounts almost immediately after you create resource groups.</span><span class="sxs-lookup"><span data-stu-id="8b870-190">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="8b870-191">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span><span class="sxs-lookup"><span data-stu-id="8b870-191">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="8b870-192">The following example creates a storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="8b870-192">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="8b870-193">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-193">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="8b870-194">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span><span class="sxs-lookup"><span data-stu-id="8b870-194">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="8b870-195">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span><span class="sxs-lookup"><span data-stu-id="8b870-195">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="8b870-196">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-196">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="8b870-197">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span><span class="sxs-lookup"><span data-stu-id="8b870-197">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="8b870-198">Replace the name of the storage account in the following example with a name that you choose:</span><span class="sxs-lookup"><span data-stu-id="8b870-198">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="8b870-199">Then you can view your storage information easily:</span><span class="sxs-lookup"><span data-stu-id="8b870-199">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="8b870-200">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-200">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="8b870-201">Create a virtual network and subnet</span><span class="sxs-lookup"><span data-stu-id="8b870-201">Create a virtual network and subnet</span></span>
<span data-ttu-id="8b870-202">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-202">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="8b870-203">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span><span class="sxs-lookup"><span data-stu-id="8b870-203">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="8b870-204">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-204">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="8b870-205">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span><span class="sxs-lookup"><span data-stu-id="8b870-205">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="8b870-206">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span><span class="sxs-lookup"><span data-stu-id="8b870-206">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="8b870-207">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-207">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="8b870-208">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span><span class="sxs-lookup"><span data-stu-id="8b870-208">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="8b870-209">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span><span class="sxs-lookup"><span data-stu-id="8b870-209">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="8b870-210">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="8b870-210">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="8b870-211">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-211">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="8b870-212">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span><span class="sxs-lookup"><span data-stu-id="8b870-212">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="8b870-213">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span><span class="sxs-lookup"><span data-stu-id="8b870-213">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="8b870-214">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-214">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="8b870-215">Create a public IP address</span><span class="sxs-lookup"><span data-stu-id="8b870-215">Create a public IP address</span></span>
<span data-ttu-id="8b870-216">Now let's create the public IP address (PIP) that we assign to your load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b870-216">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="8b870-217">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span><span class="sxs-lookup"><span data-stu-id="8b870-217">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="8b870-218">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span><span class="sxs-lookup"><span data-stu-id="8b870-218">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="8b870-219">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="8b870-219">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="8b870-220">Because the DNS name must be unique, you provide your own unique DNS name:</span><span class="sxs-lookup"><span data-stu-id="8b870-220">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="8b870-221">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-221">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="8b870-222">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="8b870-222">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="8b870-223">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-223">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="8b870-224">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span><span class="sxs-lookup"><span data-stu-id="8b870-224">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="8b870-225">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span><span class="sxs-lookup"><span data-stu-id="8b870-225">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="8b870-226">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span><span class="sxs-lookup"><span data-stu-id="8b870-226">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="8b870-227">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-227">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="8b870-228">Create a load balancer and IP pools</span><span class="sxs-lookup"><span data-stu-id="8b870-228">Create a load balancer and IP pools</span></span>
<span data-ttu-id="8b870-229">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-229">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="8b870-230">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span><span class="sxs-lookup"><span data-stu-id="8b870-230">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="8b870-231">The following example creates a load balancer named `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="8b870-231">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="8b870-232">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-232">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="8b870-233">Our load balancer is fairly empty, so let's create some IP pools.</span><span class="sxs-lookup"><span data-stu-id="8b870-233">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="8b870-234">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span><span class="sxs-lookup"><span data-stu-id="8b870-234">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="8b870-235">The front-end IP pool is publicly visible.</span><span class="sxs-lookup"><span data-stu-id="8b870-235">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="8b870-236">It's also the location to which we assign the PIP that we created earlier.</span><span class="sxs-lookup"><span data-stu-id="8b870-236">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="8b870-237">Then we use the back-end pool as a location for our VMs to connect to.</span><span class="sxs-lookup"><span data-stu-id="8b870-237">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="8b870-238">That way, the traffic can flow through the load balancer to the VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-238">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="8b870-239">First, let's create our front-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="8b870-239">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="8b870-240">The following example creates a front-end pool named `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="8b870-240">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="8b870-241">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-241">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="8b870-242">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span><span class="sxs-lookup"><span data-stu-id="8b870-242">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="8b870-243">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span><span class="sxs-lookup"><span data-stu-id="8b870-243">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="8b870-244">Next, let's create our second IP pool, this time for our back-end traffic.</span><span class="sxs-lookup"><span data-stu-id="8b870-244">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="8b870-245">The following example creates a back-end pool named `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="8b870-245">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="8b870-246">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-246">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="8b870-247">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span><span class="sxs-lookup"><span data-stu-id="8b870-247">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="8b870-248">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-248">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="8b870-249">Create load balancer NAT rules</span><span class="sxs-lookup"><span data-stu-id="8b870-249">Create load balancer NAT rules</span></span>
<span data-ttu-id="8b870-250">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span><span class="sxs-lookup"><span data-stu-id="8b870-250">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="8b870-251">You can specify the protocol to use, then map external ports to internal ports as desired.</span><span class="sxs-lookup"><span data-stu-id="8b870-251">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="8b870-252">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-252">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="8b870-253">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span><span class="sxs-lookup"><span data-stu-id="8b870-253">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="8b870-254">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span><span class="sxs-lookup"><span data-stu-id="8b870-254">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="8b870-255">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-255">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="8b870-256">Repeat the procedure for your second NAT rule for SSH.</span><span class="sxs-lookup"><span data-stu-id="8b870-256">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="8b870-257">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span><span class="sxs-lookup"><span data-stu-id="8b870-257">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="8b870-258">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span><span class="sxs-lookup"><span data-stu-id="8b870-258">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="8b870-259">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span><span class="sxs-lookup"><span data-stu-id="8b870-259">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="8b870-260">The load balancer automatically adjusts the flow of traffic.</span><span class="sxs-lookup"><span data-stu-id="8b870-260">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="8b870-261">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span><span class="sxs-lookup"><span data-stu-id="8b870-261">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="8b870-262">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-262">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="8b870-263">Create a load balancer health probe</span><span class="sxs-lookup"><span data-stu-id="8b870-263">Create a load balancer health probe</span></span>
<span data-ttu-id="8b870-264">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span><span class="sxs-lookup"><span data-stu-id="8b870-264">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="8b870-265">If not, they're removed from operation to ensure that users aren't being directed to them.</span><span class="sxs-lookup"><span data-stu-id="8b870-265">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="8b870-266">You can define custom checks for the health probe, along with intervals and timeout values.</span><span class="sxs-lookup"><span data-stu-id="8b870-266">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="8b870-267">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b870-267">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8b870-268">The following example creates a TCP health probed named `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="8b870-268">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="8b870-269">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-269">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="8b870-270">Here, we specified an interval of 15 seconds for our health checks.</span><span class="sxs-lookup"><span data-stu-id="8b870-270">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="8b870-271">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span><span class="sxs-lookup"><span data-stu-id="8b870-271">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="8b870-272">Verify the load balancer</span><span class="sxs-lookup"><span data-stu-id="8b870-272">Verify the load balancer</span></span>
<span data-ttu-id="8b870-273">Now the load balancer configuration is done.</span><span class="sxs-lookup"><span data-stu-id="8b870-273">Now the load balancer configuration is done.</span></span> <span data-ttu-id="8b870-274">Here are the steps you took:</span><span class="sxs-lookup"><span data-stu-id="8b870-274">Here are the steps you took:</span></span>

1. <span data-ttu-id="8b870-275">You created a load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b870-275">You created a load balancer.</span></span>
2. <span data-ttu-id="8b870-276">You created a front-end IP pool and assigned a public IP to it.</span><span class="sxs-lookup"><span data-stu-id="8b870-276">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="8b870-277">You created a back-end IP pool that VMs can connect to.</span><span class="sxs-lookup"><span data-stu-id="8b870-277">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="8b870-278">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span><span class="sxs-lookup"><span data-stu-id="8b870-278">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="8b870-279">You added a health probe to periodically check the VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-279">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="8b870-280">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span><span class="sxs-lookup"><span data-stu-id="8b870-280">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="8b870-281">Let's review what your load balancer looks like now:</span><span class="sxs-lookup"><span data-stu-id="8b870-281">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="8b870-282">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-282">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="8b870-283">Create an NIC to use with the Linux VM</span><span class="sxs-lookup"><span data-stu-id="8b870-283">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="8b870-284">NICs are programmatically available because you can apply rules to their use.</span><span class="sxs-lookup"><span data-stu-id="8b870-284">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="8b870-285">You can also have more than one.</span><span class="sxs-lookup"><span data-stu-id="8b870-285">You can also have more than one.</span></span> <span data-ttu-id="8b870-286">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="8b870-286">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="8b870-287">Replace the `#####-###-###` sections with your own Azure subscription ID.</span><span class="sxs-lookup"><span data-stu-id="8b870-287">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="8b870-288">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span><span class="sxs-lookup"><span data-stu-id="8b870-288">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="8b870-289">You can also view your subscription ID with `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="8b870-289">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="8b870-290">The following example creates a NIC named `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="8b870-290">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="8b870-291">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-291">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="8b870-292">You can see the details by examining the resource directly.</span><span class="sxs-lookup"><span data-stu-id="8b870-292">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="8b870-293">You examine the resource by using the `azure network nic show` command:</span><span class="sxs-lookup"><span data-stu-id="8b870-293">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="8b870-294">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-294">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="8b870-295">Now we create the second NIC, hooking in to our back-end IP pool again.</span><span class="sxs-lookup"><span data-stu-id="8b870-295">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="8b870-296">This time the second NAT rule permits SSH traffic.</span><span class="sxs-lookup"><span data-stu-id="8b870-296">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="8b870-297">The following example creates a NIC named `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="8b870-297">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="8b870-298">Create a network security group and rules</span><span class="sxs-lookup"><span data-stu-id="8b870-298">Create a network security group and rules</span></span>
<span data-ttu-id="8b870-299">Now we create a network security group and the inbound rules that govern access to the NIC.</span><span class="sxs-lookup"><span data-stu-id="8b870-299">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="8b870-300">A network security group can be applied to a NIC or subnet.</span><span class="sxs-lookup"><span data-stu-id="8b870-300">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="8b870-301">You define rules to control the flow of traffic in and out of your VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-301">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="8b870-302">The following example creates a network security group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="8b870-302">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="8b870-303">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span><span class="sxs-lookup"><span data-stu-id="8b870-303">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="8b870-304">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span><span class="sxs-lookup"><span data-stu-id="8b870-304">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="8b870-305">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span><span class="sxs-lookup"><span data-stu-id="8b870-305">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="8b870-306">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span><span class="sxs-lookup"><span data-stu-id="8b870-306">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="8b870-307">The inbound rule is a filter for inbound network connections.</span><span class="sxs-lookup"><span data-stu-id="8b870-307">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="8b870-308">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span><span class="sxs-lookup"><span data-stu-id="8b870-308">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="8b870-309">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span><span class="sxs-lookup"><span data-stu-id="8b870-309">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="8b870-310">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span><span class="sxs-lookup"><span data-stu-id="8b870-310">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="8b870-311">Ports are typically dynamic.</span><span class="sxs-lookup"><span data-stu-id="8b870-311">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="8b870-312">Bind to the NIC</span><span class="sxs-lookup"><span data-stu-id="8b870-312">Bind to the NIC</span></span>
<span data-ttu-id="8b870-313">Bind the NSG to the NICs.</span><span class="sxs-lookup"><span data-stu-id="8b870-313">Bind the NSG to the NICs.</span></span> <span data-ttu-id="8b870-314">We need to connect our NICs with our network security group.</span><span class="sxs-lookup"><span data-stu-id="8b870-314">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="8b870-315">Run both commands, to hook up both of our NICs:</span><span class="sxs-lookup"><span data-stu-id="8b870-315">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="8b870-316">Create an availability set</span><span class="sxs-lookup"><span data-stu-id="8b870-316">Create an availability set</span></span>
<span data-ttu-id="8b870-317">Availability sets help spread your VMs across fault domains and upgrade domains.</span><span class="sxs-lookup"><span data-stu-id="8b870-317">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="8b870-318">Let's create an availability set for your VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-318">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="8b870-319">The following example creates an availability set named `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="8b870-319">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="8b870-320">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span><span class="sxs-lookup"><span data-stu-id="8b870-320">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="8b870-321">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span><span class="sxs-lookup"><span data-stu-id="8b870-321">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="8b870-322">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span><span class="sxs-lookup"><span data-stu-id="8b870-322">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="8b870-323">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span><span class="sxs-lookup"><span data-stu-id="8b870-323">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="8b870-324">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span><span class="sxs-lookup"><span data-stu-id="8b870-324">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="8b870-325">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span><span class="sxs-lookup"><span data-stu-id="8b870-325">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="8b870-326">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span><span class="sxs-lookup"><span data-stu-id="8b870-326">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="8b870-327">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b870-327">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="8b870-328">Create the Linux VMs</span><span class="sxs-lookup"><span data-stu-id="8b870-328">Create the Linux VMs</span></span>
<span data-ttu-id="8b870-329">You've created the storage and network resources to support Internet-accessible VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-329">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="8b870-330">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span><span class="sxs-lookup"><span data-stu-id="8b870-330">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="8b870-331">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span><span class="sxs-lookup"><span data-stu-id="8b870-331">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="8b870-332">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b870-332">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8b870-333">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="8b870-333">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="8b870-334">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="8b870-334">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="8b870-335">For the last field, we pass `latest` so that in the future we always get the most recent build.</span><span class="sxs-lookup"><span data-stu-id="8b870-335">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="8b870-336">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="8b870-336">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="8b870-337">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="8b870-337">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="8b870-338">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span><span class="sxs-lookup"><span data-stu-id="8b870-338">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="8b870-339">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span><span class="sxs-lookup"><span data-stu-id="8b870-339">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="8b870-340">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b870-340">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8b870-341">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span><span class="sxs-lookup"><span data-stu-id="8b870-341">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="8b870-342">This method is typically less secure.</span><span class="sxs-lookup"><span data-stu-id="8b870-342">This method is typically less secure.</span></span>

<span data-ttu-id="8b870-343">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span><span class="sxs-lookup"><span data-stu-id="8b870-343">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="8b870-344">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-344">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="8b870-345">You can connect to your VM immediately by using your default SSH keys.</span><span class="sxs-lookup"><span data-stu-id="8b870-345">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="8b870-346">Make sure that you specify the appropriate port since we're passing through the load balancer.</span><span class="sxs-lookup"><span data-stu-id="8b870-346">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="8b870-347">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span><span class="sxs-lookup"><span data-stu-id="8b870-347">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="8b870-348">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-348">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="8b870-349">Go ahead and create your second VM in the same manner:</span><span class="sxs-lookup"><span data-stu-id="8b870-349">Go ahead and create your second VM in the same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="8b870-350">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span><span class="sxs-lookup"><span data-stu-id="8b870-350">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="8b870-351">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span><span class="sxs-lookup"><span data-stu-id="8b870-351">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="8b870-352">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-352">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="8b870-353">Output:</span><span class="sxs-lookup"><span data-stu-id="8b870-353">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="8b870-354">Export the environment as a template</span><span class="sxs-lookup"><span data-stu-id="8b870-354">Export the environment as a template</span></span>
<span data-ttu-id="8b870-355">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span><span class="sxs-lookup"><span data-stu-id="8b870-355">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="8b870-356">Resource Manager uses JSON templates that define all the parameters for your environment.</span><span class="sxs-lookup"><span data-stu-id="8b870-356">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="8b870-357">You build out entire environments by referencing this JSON template.</span><span class="sxs-lookup"><span data-stu-id="8b870-357">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="8b870-358">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span><span class="sxs-lookup"><span data-stu-id="8b870-358">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="8b870-359">This command creates the `myResourceGroup.json` file in your current working directory.</span><span class="sxs-lookup"><span data-stu-id="8b870-359">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="8b870-360">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-360">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="8b870-361">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span><span class="sxs-lookup"><span data-stu-id="8b870-361">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="8b870-362">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span><span class="sxs-lookup"><span data-stu-id="8b870-362">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="8b870-363">To create an environment from your template:</span><span class="sxs-lookup"><span data-stu-id="8b870-363">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="8b870-364">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8b870-364">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8b870-365">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span><span class="sxs-lookup"><span data-stu-id="8b870-365">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b870-366">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b870-366">Next steps</span></span>
<span data-ttu-id="8b870-367">Now you're ready to begin working with multiple networking components and VMs.</span><span class="sxs-lookup"><span data-stu-id="8b870-367">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="8b870-368">You can use this sample environment to build out your application by using the core components introduced here.</span><span class="sxs-lookup"><span data-stu-id="8b870-368">You can use this sample environment to build out your application by using the core components introduced here.</span></span>

