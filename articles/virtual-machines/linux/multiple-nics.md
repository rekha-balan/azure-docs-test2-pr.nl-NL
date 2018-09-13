---
title: Create a Linux VM with multiple NICs using the Azure CLI 2.0 | Microsoft Docs
description: Learn how to create a Linux VM with multiple NICs attached to it using the Azure CLI 2.0 or Resource Manager templates.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/10/2017
ms.author: iainfou
ms.openlocfilehash: 9ee9c3e427ce46a8a1bbdf6b3e5a05d26d262bfe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540669"
---
# <a name="create-a-linux-vm-with-multiple-nics"></a><span data-ttu-id="a678b-103">Create a Linux VM with multiple NICs</span><span class="sxs-lookup"><span data-stu-id="a678b-103">Create a Linux VM with multiple NICs</span></span>
<span data-ttu-id="a678b-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span><span class="sxs-lookup"><span data-stu-id="a678b-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="a678b-105">A common scenario would be to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span><span class="sxs-lookup"><span data-stu-id="a678b-105">A common scenario would be to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="a678b-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span><span class="sxs-lookup"><span data-stu-id="a678b-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="a678b-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a678b-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="a678b-108">Different [VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) support a varying number of NICs, so size your VM accordingly.</span><span class="sxs-lookup"><span data-stu-id="a678b-108">Different [VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="a678b-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a678b-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="a678b-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a678b-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="a678b-111">Create supporting resources</span><span class="sxs-lookup"><span data-stu-id="a678b-111">Create supporting resources</span></span>
<span data-ttu-id="a678b-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a678b-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a678b-113">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="a678b-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a678b-114">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="a678b-114">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="a678b-115">First, create a resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a678b-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a678b-116">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span><span class="sxs-lookup"><span data-stu-id="a678b-116">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="a678b-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="a678b-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="a678b-118">The following example creates a virtual network named `myVnet` and subnet named `mySubnetFrontEnd`:</span><span class="sxs-lookup"><span data-stu-id="a678b-118">The following example creates a virtual network named `myVnet` and subnet named `mySubnetFrontEnd`:</span></span>

```azurecli
az network vnet create --resource-group myResourceGroup --name myVnet \
  --address-prefix 192.168.0.0/16 --subnet-name mySubnetFrontEnd --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="a678b-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="a678b-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="a678b-120">The following example creates a subnet named `mySubnetBackEnd`:</span><span class="sxs-lookup"><span data-stu-id="a678b-120">The following example creates a subnet named `mySubnetBackEnd`:</span></span>

```azurecli
az network vnet subnet create --resource-group myResourceGroup --vnet-name myVnet \
    --name mySubnetBackEnd --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="a678b-121">Create and configure multiple NICs</span><span class="sxs-lookup"><span data-stu-id="a678b-121">Create and configure multiple NICs</span></span>
<span data-ttu-id="a678b-122">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span><span class="sxs-lookup"><span data-stu-id="a678b-122">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span></span>

<span data-ttu-id="a678b-123">Typically you create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span><span class="sxs-lookup"><span data-stu-id="a678b-123">Typically you create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="a678b-124">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="a678b-124">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="a678b-125">The following example creates a network security group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="a678b-125">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create --resource-group myResourceGroup \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="a678b-126">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="a678b-126">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="a678b-127">The following example creates two NICs, named `myNic1` and `myNic2`, connected the network security group, with one NIC connecting to each subnet:</span><span class="sxs-lookup"><span data-stu-id="a678b-127">The following example creates two NICs, named `myNic1` and `myNic2`, connected the network security group, with one NIC connecting to each subnet:</span></span>

```azurecli
az network nic create --resource-group myResourceGroup --name myNic1 \
  --vnet-name myVnet --subnet mySubnetFrontEnd \
  --network-security-group myNetworkSecurityGroup
az network nic create --resource-group myResourceGroup --name myNic2 \
  --vnet-name myVnet --subnet mySubnetBackEnd \
  --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="a678b-128">Create a VM and attach the NICs</span><span class="sxs-lookup"><span data-stu-id="a678b-128">Create a VM and attach the NICs</span></span>
<span data-ttu-id="a678b-129">When you create the VM, specify the NICs you created with `--nics`.</span><span class="sxs-lookup"><span data-stu-id="a678b-129">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="a678b-130">You also need to take care when you select the VM size.</span><span class="sxs-lookup"><span data-stu-id="a678b-130">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="a678b-131">There are limits for the total number of NICs that you can add to a VM.</span><span class="sxs-lookup"><span data-stu-id="a678b-131">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="a678b-132">Read more about [Linux VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a678b-132">Read more about [Linux VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="a678b-133">Create a VM with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a678b-133">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a678b-134">The following example creates a VM named `myVM` using [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json):</span><span class="sxs-lookup"><span data-stu-id="a678b-134">The following example creates a VM named `myVM` using [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json):</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic1 myNic2
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="a678b-135">Create multiple NICs using Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="a678b-135">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="a678b-136">Azure Resource Manager templates use declarative JSON files to define your environment.</span><span class="sxs-lookup"><span data-stu-id="a678b-136">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="a678b-137">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a678b-137">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="a678b-138">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="a678b-138">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="a678b-139">You use *copy* to specify the number of instances to create:</span><span class="sxs-lookup"><span data-stu-id="a678b-139">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="a678b-140">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a678b-140">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="a678b-141">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span><span class="sxs-lookup"><span data-stu-id="a678b-141">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="a678b-142">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="a678b-142">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a678b-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="a678b-143">Next steps</span></span>
<span data-ttu-id="a678b-144">Review [Linux VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) when trying to creating a VM with multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="a678b-144">Review [Linux VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="a678b-145">Pay attention to the maximum number of NICs each VM size supports.</span><span class="sxs-lookup"><span data-stu-id="a678b-145">Pay attention to the maximum number of NICs each VM size supports.</span></span> 