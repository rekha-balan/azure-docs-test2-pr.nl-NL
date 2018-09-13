---
title: Create a Linux VM in Azure with multiple NICs | Microsoft Docs
description: Learn how to create a Linux VM with multiple NICs attached to it using the Azure CLI 2.0 or Resource Manager templates.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: jeconnoc
editor: ''
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/07/2018
ms.author: iainfou
ms.openlocfilehash: 0beb824310017a31de4d5a67434c9093e4051faa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776366"
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="a1c19-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span><span class="sxs-lookup"><span data-stu-id="a1c19-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="a1c19-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span><span class="sxs-lookup"><span data-stu-id="a1c19-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="a1c19-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span><span class="sxs-lookup"><span data-stu-id="a1c19-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="a1c19-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span><span class="sxs-lookup"><span data-stu-id="a1c19-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="a1c19-107">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span><span class="sxs-lookup"><span data-stu-id="a1c19-107">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="a1c19-108">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a1c19-108">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="a1c19-109">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a1c19-109">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="a1c19-110">Create supporting resources</span><span class="sxs-lookup"><span data-stu-id="a1c19-110">Create supporting resources</span></span>
<span data-ttu-id="a1c19-111">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="a1c19-111">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

<span data-ttu-id="a1c19-112">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="a1c19-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a1c19-113">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span><span class="sxs-lookup"><span data-stu-id="a1c19-113">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="a1c19-114">First, create a resource group with [az group create](/cli/azure/group#az_group_create).</span><span class="sxs-lookup"><span data-stu-id="a1c19-114">First, create a resource group with [az group create](/cli/azure/group#az_group_create).</span></span> <span data-ttu-id="a1c19-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span><span class="sxs-lookup"><span data-stu-id="a1c19-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a1c19-116">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#az_network_vnet_create).</span><span class="sxs-lookup"><span data-stu-id="a1c19-116">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#az_network_vnet_create).</span></span> <span data-ttu-id="a1c19-117">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="a1c19-117">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 10.0.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 10.0.1.0/24
```

<span data-ttu-id="a1c19-118">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_create).</span><span class="sxs-lookup"><span data-stu-id="a1c19-118">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_create).</span></span> <span data-ttu-id="a1c19-119">The following example creates a subnet named *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="a1c19-119">The following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 10.0.2.0/24
```

<span data-ttu-id="a1c19-120">Create a network security group with [az network nsg create](/cli/azure/network/nsg#az_network_nsg_create).</span><span class="sxs-lookup"><span data-stu-id="a1c19-120">Create a network security group with [az network nsg create](/cli/azure/network/nsg#az_network_nsg_create).</span></span> <span data-ttu-id="a1c19-121">The following example creates a network security group named *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="a1c19-121">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="a1c19-122">Create and configure multiple NICs</span><span class="sxs-lookup"><span data-stu-id="a1c19-122">Create and configure multiple NICs</span></span>
<span data-ttu-id="a1c19-123">Create two NICs with [az network nic create](/cli/azure/network/nic#az_network_nic_create).</span><span class="sxs-lookup"><span data-stu-id="a1c19-123">Create two NICs with [az network nic create](/cli/azure/network/nic#az_network_nic_create).</span></span> <span data-ttu-id="a1c19-124">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span><span class="sxs-lookup"><span data-stu-id="a1c19-124">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="a1c19-125">Create a VM and attach the NICs</span><span class="sxs-lookup"><span data-stu-id="a1c19-125">Create a VM and attach the NICs</span></span>
<span data-ttu-id="a1c19-126">When you create the VM, specify the NICs you created with `--nics`.</span><span class="sxs-lookup"><span data-stu-id="a1c19-126">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="a1c19-127">You also need to take care when you select the VM size.</span><span class="sxs-lookup"><span data-stu-id="a1c19-127">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="a1c19-128">There are limits for the total number of NICs that you can add to a VM.</span><span class="sxs-lookup"><span data-stu-id="a1c19-128">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="a1c19-129">Read more about [Linux VM sizes](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="a1c19-129">Read more about [Linux VM sizes](sizes.md).</span></span>

<span data-ttu-id="a1c19-130">Create a VM with [az vm create](/cli/azure/vm#az_vm_create).</span><span class="sxs-lookup"><span data-stu-id="a1c19-130">Create a VM with [az vm create](/cli/azure/vm#az_vm_create).</span></span> <span data-ttu-id="a1c19-131">The following example creates a VM named *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a1c19-131">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

<span data-ttu-id="a1c19-132">Add routing tables to the guest OS by completing the steps in [Configure the guest OS for multiple NICs](#configure-guest-os-for- multiple-nics).</span><span class="sxs-lookup"><span data-stu-id="a1c19-132">Add routing tables to the guest OS by completing the steps in [Configure the guest OS for multiple NICs](#configure-guest-os-for- multiple-nics).</span></span>

## <a name="add-a-nic-to-a-vm"></a><span data-ttu-id="a1c19-133">Add a NIC to a VM</span><span class="sxs-lookup"><span data-stu-id="a1c19-133">Add a NIC to a VM</span></span>
<span data-ttu-id="a1c19-134">The previous steps created a VM with multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="a1c19-134">The previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="a1c19-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a1c19-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="a1c19-136">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span><span class="sxs-lookup"><span data-stu-id="a1c19-136">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span> <span data-ttu-id="a1c19-137">If needed, you can [resize a VM](change-vm-size.md).</span><span class="sxs-lookup"><span data-stu-id="a1c19-137">If needed, you can [resize a VM](change-vm-size.md).</span></span>

<span data-ttu-id="a1c19-138">Create another NIC with [az network nic create](/cli/azure/network/nic#az_network_nic_create).</span><span class="sxs-lookup"><span data-stu-id="a1c19-138">Create another NIC with [az network nic create](/cli/azure/network/nic#az_network_nic_create).</span></span> <span data-ttu-id="a1c19-139">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span><span class="sxs-lookup"><span data-stu-id="a1c19-139">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="a1c19-140">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#az_vm_deallocate).</span><span class="sxs-lookup"><span data-stu-id="a1c19-140">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#az_vm_deallocate).</span></span> <span data-ttu-id="a1c19-141">The following example deallocates the VM named *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a1c19-141">The following example deallocates the VM named *myVM*:</span></span>


```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="a1c19-142">Add the NIC with [az vm nic add](/cli/azure/vm/nic#az_vm_nic_add).</span><span class="sxs-lookup"><span data-stu-id="a1c19-142">Add the NIC with [az vm nic add](/cli/azure/vm/nic#az_vm_nic_add).</span></span> <span data-ttu-id="a1c19-143">The following example adds *myNic3* to *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a1c19-143">The following example adds *myNic3* to *myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="a1c19-144">Start the VM with [az vm start](/cli/azure/vm#az_vm_start):</span><span class="sxs-lookup"><span data-stu-id="a1c19-144">Start the VM with [az vm start](/cli/azure/vm#az_vm_start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="a1c19-145">Add routing tables to the guest OS by completing the steps in [Configure the guest OS for multiple NICs](#configure-guest-os-for- multiple-nics).</span><span class="sxs-lookup"><span data-stu-id="a1c19-145">Add routing tables to the guest OS by completing the steps in [Configure the guest OS for multiple NICs](#configure-guest-os-for- multiple-nics).</span></span>

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="a1c19-146">Remove a NIC from a VM</span><span class="sxs-lookup"><span data-stu-id="a1c19-146">Remove a NIC from a VM</span></span>
<span data-ttu-id="a1c19-147">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#az_vm_deallocate).</span><span class="sxs-lookup"><span data-stu-id="a1c19-147">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#az_vm_deallocate).</span></span> <span data-ttu-id="a1c19-148">The following example deallocates the VM named *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a1c19-148">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="a1c19-149">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#az_vm_nic_remove).</span><span class="sxs-lookup"><span data-stu-id="a1c19-149">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#az_vm_nic_remove).</span></span> <span data-ttu-id="a1c19-150">The following example removes *myNic3* from *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a1c19-150">The following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="a1c19-151">Start the VM with [az vm start](/cli/azure/vm#az_vm_start):</span><span class="sxs-lookup"><span data-stu-id="a1c19-151">Start the VM with [az vm start](/cli/azure/vm#az_vm_start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="a1c19-152">Create multiple NICs using Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="a1c19-152">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="a1c19-153">Azure Resource Manager templates use declarative JSON files to define your environment.</span><span class="sxs-lookup"><span data-stu-id="a1c19-153">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="a1c19-154">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1c19-154">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="a1c19-155">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="a1c19-155">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="a1c19-156">You use *copy* to specify the number of instances to create:</span><span class="sxs-lookup"><span data-stu-id="a1c19-156">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="a1c19-157">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a1c19-157">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="a1c19-158">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span><span class="sxs-lookup"><span data-stu-id="a1c19-158">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="a1c19-159">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/template-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a1c19-159">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/template-samples.md).</span></span>

<span data-ttu-id="a1c19-160">Add routing tables to the guest OS by completing the steps in [Configure the guest OS for multiple NICs](#configure-guest-os-for- multiple-nics).</span><span class="sxs-lookup"><span data-stu-id="a1c19-160">Add routing tables to the guest OS by completing the steps in [Configure the guest OS for multiple NICs](#configure-guest-os-for- multiple-nics).</span></span>

## <a name="configure-guest-os-for-multiple-nics"></a><span data-ttu-id="a1c19-161">Configure guest OS for multiple NICs</span><span class="sxs-lookup"><span data-stu-id="a1c19-161">Configure guest OS for multiple NICs</span></span>

<span data-ttu-id="a1c19-162">The previous steps created a virtual network and subnet, attached NICs, then created a VM.</span><span class="sxs-lookup"><span data-stu-id="a1c19-162">The previous steps created a virtual network and subnet, attached NICs, then created a VM.</span></span> <span data-ttu-id="a1c19-163">A public IP address and network security group rules that allow SSH traffic were not created.</span><span class="sxs-lookup"><span data-stu-id="a1c19-163">A public IP address and network security group rules that allow SSH traffic were not created.</span></span> <span data-ttu-id="a1c19-164">To configure the guest OS for multiple NICs, you need to allow remote connections and run commands locally on the VM.</span><span class="sxs-lookup"><span data-stu-id="a1c19-164">To configure the guest OS for multiple NICs, you need to allow remote connections and run commands locally on the VM.</span></span>

<span data-ttu-id="a1c19-165">To allow SSH traffic, create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create) as follows:</span><span class="sxs-lookup"><span data-stu-id="a1c19-165">To allow SSH traffic, create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#az-network-nsg-rule-create) as follows:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name allow_ssh \
    --priority 101 \
    --destination-port-ranges 22
```

<span data-ttu-id="a1c19-166">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) and assign it to the first NIC with [az network nic ip-config update](/cli/azure/network/nic/ip-config#az-network-nic-ip-config-update):</span><span class="sxs-lookup"><span data-stu-id="a1c19-166">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#az-network-public-ip-create) and assign it to the first NIC with [az network nic ip-config update](/cli/azure/network/nic/ip-config#az-network-nic-ip-config-update):</span></span>

```azurecli
az network public-ip-address create --resource-group myResourceGroup --name myPublicIP

az network nic ip-config update \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --name ipconfig1 \
    --public-ip-addres myPublicIP
```

<span data-ttu-id="a1c19-167">To view the public IP address of the VM, use [az vm show](/cli/azure/vm#az-vm-show) as follows::</span><span class="sxs-lookup"><span data-stu-id="a1c19-167">To view the public IP address of the VM, use [az vm show](/cli/azure/vm#az-vm-show) as follows::</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM -d --query publicIps -o tsv
```

<span data-ttu-id="a1c19-168">Now SSH to the public IP address of your VM.</span><span class="sxs-lookup"><span data-stu-id="a1c19-168">Now SSH to the public IP address of your VM.</span></span> <span data-ttu-id="a1c19-169">The default username provided in a previous step was *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="a1c19-169">The default username provided in a previous step was *azureuser*.</span></span> <span data-ttu-id="a1c19-170">Provide your own username and public IP address:</span><span class="sxs-lookup"><span data-stu-id="a1c19-170">Provide your own username and public IP address:</span></span>

```bash
ssh azureuser@137.117.58.232
```

<span data-ttu-id="a1c19-171">To send to or from a secondary network interface, you have to manually add persistent routes to the operating system for each secondary network interface.</span><span class="sxs-lookup"><span data-stu-id="a1c19-171">To send to or from a secondary network interface, you have to manually add persistent routes to the operating system for each secondary network interface.</span></span> <span data-ttu-id="a1c19-172">In this article, *eth1* is the secondary interface.</span><span class="sxs-lookup"><span data-stu-id="a1c19-172">In this article, *eth1* is the secondary interface.</span></span> <span data-ttu-id="a1c19-173">Instructions for adding persistent routes to the operating system vary by distro.</span><span class="sxs-lookup"><span data-stu-id="a1c19-173">Instructions for adding persistent routes to the operating system vary by distro.</span></span> <span data-ttu-id="a1c19-174">See documentation for your distro for instructions.</span><span class="sxs-lookup"><span data-stu-id="a1c19-174">See documentation for your distro for instructions.</span></span>

<span data-ttu-id="a1c19-175">When adding the route to the operating system, the gateway address is *.1* for whichever subnet the network interface is in.</span><span class="sxs-lookup"><span data-stu-id="a1c19-175">When adding the route to the operating system, the gateway address is *.1* for whichever subnet the network interface is in.</span></span> <span data-ttu-id="a1c19-176">For example, if the network interface is assigned the address *10.0.2.4*, the gateway you specify for the route is *10.0.2.1*.</span><span class="sxs-lookup"><span data-stu-id="a1c19-176">For example, if the network interface is assigned the address *10.0.2.4*, the gateway you specify for the route is *10.0.2.1*.</span></span> <span data-ttu-id="a1c19-177">You can define a specific network for the route's destination, or specify a destination of *0.0.0.0*, if you want all traffic for the interface to go through the specified gateway.</span><span class="sxs-lookup"><span data-stu-id="a1c19-177">You can define a specific network for the route's destination, or specify a destination of *0.0.0.0*, if you want all traffic for the interface to go through the specified gateway.</span></span> <span data-ttu-id="a1c19-178">The gateway for each subnet is managed by the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a1c19-178">The gateway for each subnet is managed by the virtual network.</span></span>

<span data-ttu-id="a1c19-179">Once you've added the route for a secondary interface, verify that the route is in your route table with `route -n`.</span><span class="sxs-lookup"><span data-stu-id="a1c19-179">Once you've added the route for a secondary interface, verify that the route is in your route table with `route -n`.</span></span> <span data-ttu-id="a1c19-180">The following example output is for the route table that has the two network interfaces added to the VM in this article:</span><span class="sxs-lookup"><span data-stu-id="a1c19-180">The following example output is for the route table that has the two network interfaces added to the VM in this article:</span></span>

```bash
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         10.0.1.1        0.0.0.0         UG    0      0        0 eth0
0.0.0.0         10.0.2.1        0.0.0.0         UG    0      0        0 eth1
10.0.1.0        0.0.0.0         255.255.255.0   U     0      0        0 eth0
10.0.2.0        0.0.0.0         255.255.255.0   U     0      0        0 eth1
168.63.129.16   10.0.1.1        255.255.255.255 UGH   0      0        0 eth0
169.254.169.254 10.0.1.1        255.255.255.255 UGH   0      0        0 eth0
```

<span data-ttu-id="a1c19-181">Confirm that the route you added persists across reboots by checking your route table again after a reboot.</span><span class="sxs-lookup"><span data-stu-id="a1c19-181">Confirm that the route you added persists across reboots by checking your route table again after a reboot.</span></span> <span data-ttu-id="a1c19-182">To test connectivity, you can enter the following command, for example, where *eth1* is the name of a secondary network interface:</span><span class="sxs-lookup"><span data-stu-id="a1c19-182">To test connectivity, you can enter the following command, for example, where *eth1* is the name of a secondary network interface:</span></span>

```bash
ping bing.com -c 4 -I eth1
```

## <a name="next-steps"></a><span data-ttu-id="a1c19-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1c19-183">Next steps</span></span>
<span data-ttu-id="a1c19-184">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="a1c19-184">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="a1c19-185">Pay attention to the maximum number of NICs each VM size supports.</span><span class="sxs-lookup"><span data-stu-id="a1c19-185">Pay attention to the maximum number of NICs each VM size supports.</span></span>

<span data-ttu-id="a1c19-186">To further secure your VMs, use just in time VM access.</span><span class="sxs-lookup"><span data-stu-id="a1c19-186">To further secure your VMs, use just in time VM access.</span></span> <span data-ttu-id="a1c19-187">This feature opens network security group rules for SSH traffic when needed, and for a defined period of time.</span><span class="sxs-lookup"><span data-stu-id="a1c19-187">This feature opens network security group rules for SSH traffic when needed, and for a defined period of time.</span></span> <span data-ttu-id="a1c19-188">For more information, see [Manage virtual machine access using just in time](../../security-center/security-center-just-in-time.md).</span><span class="sxs-lookup"><span data-stu-id="a1c19-188">For more information, see [Manage virtual machine access using just in time](../../security-center/security-center-just-in-time.md).</span></span>
