---
title: Create a Linux VM in Azure with multiple NICs | Microsoft Docs
description: Learn how to create a Linux VM with multiple NICs attached to it using the Azure CLI or Resource Manager templates.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: a379eec482167ab56c8c412ab7177582efbe6cc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551140"
---
# <a name="create-a-linux-vm-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="763ff-103">Create a Linux VM with multiple NICs using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="763ff-103">Create a Linux VM with multiple NICs using the Azure CLI 1.0</span></span>
<span data-ttu-id="763ff-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span><span class="sxs-lookup"><span data-stu-id="763ff-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="763ff-105">A common scenario would be to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span><span class="sxs-lookup"><span data-stu-id="763ff-105">A common scenario would be to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="763ff-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span><span class="sxs-lookup"><span data-stu-id="763ff-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="763ff-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="763ff-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="763ff-108">Different [VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) support a varying number of NICs, so size your VM accordingly.</span><span class="sxs-lookup"><span data-stu-id="763ff-108">Different [VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="763ff-109">You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM.</span><span class="sxs-lookup"><span data-stu-id="763ff-109">You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM.</span></span> <span data-ttu-id="763ff-110">You can [create a VM based on the original virtual disk(s)](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and create multiple NICs as you deploy the VM.</span><span class="sxs-lookup"><span data-stu-id="763ff-110">You can [create a VM based on the original virtual disk(s)](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and create multiple NICs as you deploy the VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="763ff-111">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="763ff-111">CLI versions to complete the task</span></span>
<span data-ttu-id="763ff-112">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="763ff-112">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="763ff-113">[Azure CLI 1.0](#create-supporting-resources) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="763ff-113">[Azure CLI 1.0](#create-supporting-resources) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="763ff-114">[Azure CLI 2.0](../windows/multiple-nics.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="763ff-114">[Azure CLI 2.0](../windows/multiple-nics.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="763ff-115">Create supporting resources</span><span class="sxs-lookup"><span data-stu-id="763ff-115">Create supporting resources</span></span>
<span data-ttu-id="763ff-116">Make sure that you have the [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="763ff-116">Make sure that you have the [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="763ff-117">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="763ff-117">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="763ff-118">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="763ff-118">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="763ff-119">First, create a resource group.</span><span class="sxs-lookup"><span data-stu-id="763ff-119">First, create a resource group.</span></span> <span data-ttu-id="763ff-120">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span><span class="sxs-lookup"><span data-stu-id="763ff-120">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup -l WestUS
```

<span data-ttu-id="763ff-121">Create a storage account to hold your VMs.</span><span class="sxs-lookup"><span data-stu-id="763ff-121">Create a storage account to hold your VMs.</span></span> <span data-ttu-id="763ff-122">The following example creates a storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="763ff-122">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount -g myResourceGroup \
    -l WestUS --kind Storage --sku-name PLRS
```

<span data-ttu-id="763ff-123">Create a virtual network to connect your VMs to.</span><span class="sxs-lookup"><span data-stu-id="763ff-123">Create a virtual network to connect your VMs to.</span></span> <span data-ttu-id="763ff-124">The following example creates a virtual network named `myVnet` with an address prefix of `192.168.0.0/16`:</span><span class="sxs-lookup"><span data-stu-id="763ff-124">The following example creates a virtual network named `myVnet` with an address prefix of `192.168.0.0/16`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l WestUS \
    -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="763ff-125">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span><span class="sxs-lookup"><span data-stu-id="763ff-125">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="763ff-126">The following example creates two subnets, named `mySubnetFrontEnd` and `mySubnetBackEnd`:</span><span class="sxs-lookup"><span data-stu-id="763ff-126">The following example creates two subnets, named `mySubnetFrontEnd` and `mySubnetBackEnd`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup -e myVnet \
    -n mySubnetFrontEnd -a 192.168.1.0/24
azure network vnet subnet create -g myResourceGroup -e myVnet \
    -n mySubnetBackEnd -a 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="763ff-127">Create and configure multiple NICs</span><span class="sxs-lookup"><span data-stu-id="763ff-127">Create and configure multiple NICs</span></span>
<span data-ttu-id="763ff-128">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span><span class="sxs-lookup"><span data-stu-id="763ff-128">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span></span>

<span data-ttu-id="763ff-129">The following example creates two NICs, named `myNic1` and `myNic2`, with one NIC connecting to each subnet:</span><span class="sxs-lookup"><span data-stu-id="763ff-129">The following example creates two NICs, named `myNic1` and `myNic2`, with one NIC connecting to each subnet:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location WestUS \
    -n myNic1 --subnet-vnet-name myVnet --subnet-name mySubnetFrontEnd
azure network nic create --resource-group myResourceGroup --location WestUS \
    -n myNic2 --subnet-vnet-name myVnet --subnet-name mySubnetBackEnd
```

<span data-ttu-id="763ff-130">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span><span class="sxs-lookup"><span data-stu-id="763ff-130">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="763ff-131">The following example creates a Network Security Group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="763ff-131">The following example creates a Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location WestUS \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="763ff-132">Bind your NICs to the Network Security Group using `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="763ff-132">Bind your NICs to the Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="763ff-133">The following example binds `myNic1` and `myNic2` with `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="763ff-133">The following example binds `myNic1` and `myNic2` with `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set --resource-group myResourceGroup --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="763ff-134">Create a VM and attach the NICs</span><span class="sxs-lookup"><span data-stu-id="763ff-134">Create a VM and attach the NICs</span></span>
<span data-ttu-id="763ff-135">When creating the VM, you now specify multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="763ff-135">When creating the VM, you now specify multiple NICs.</span></span> <span data-ttu-id="763ff-136">Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span><span class="sxs-lookup"><span data-stu-id="763ff-136">Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="763ff-137">You also need to take care when you select the VM size.</span><span class="sxs-lookup"><span data-stu-id="763ff-137">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="763ff-138">There are limits for the total number of NICs that you can add to a VM.</span><span class="sxs-lookup"><span data-stu-id="763ff-138">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="763ff-139">Read more about [Linux VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="763ff-139">Read more about [Linux VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="763ff-140">The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (`Standard_DS2_v2`):</span><span class="sxs-lookup"><span data-stu-id="763ff-140">The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (`Standard_DS2_v2`):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location WestUS \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="763ff-141">Create multiple NICs using Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="763ff-141">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="763ff-142">Azure Resource Manager templates use declarative JSON files to define your environment.</span><span class="sxs-lookup"><span data-stu-id="763ff-142">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="763ff-143">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="763ff-143">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="763ff-144">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="763ff-144">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="763ff-145">You use *copy* to specify the number of instances to create:</span><span class="sxs-lookup"><span data-stu-id="763ff-145">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="763ff-146">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="763ff-146">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="763ff-147">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span><span class="sxs-lookup"><span data-stu-id="763ff-147">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="763ff-148">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="763ff-148">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="763ff-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="763ff-149">Next steps</span></span>
<span data-ttu-id="763ff-150">Make sure to review [Linux VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) when trying to creating a VM with multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="763ff-150">Make sure to review [Linux VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="763ff-151">Pay attention to the maximum number of NICs each VM size supports.</span><span class="sxs-lookup"><span data-stu-id="763ff-151">Pay attention to the maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="763ff-152">Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM.</span><span class="sxs-lookup"><span data-stu-id="763ff-152">Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM.</span></span> <span data-ttu-id="763ff-153">Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.</span><span class="sxs-lookup"><span data-stu-id="763ff-153">Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.</span></span>

