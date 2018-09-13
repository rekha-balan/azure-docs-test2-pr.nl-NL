---
title: Deploy Linux VMs into existing networks - Azure CLI | Microsoft Docs
description: Deploy a Linux VM into an existing Virtual Network using the CLI.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: vlivech
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 5c3cad9928a3f2db73fc0403c1ce39ba330ea24b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564341"
---
# <a name="deploy-a-linux-vm-into-an-existing-azure-virtual-network-using-the-cli"></a><span data-ttu-id="271c0-103">Deploy a Linux VM into an existing Azure Virtual Network using the CLI</span><span class="sxs-lookup"><span data-stu-id="271c0-103">Deploy a Linux VM into an existing Azure Virtual Network using the CLI</span></span>

<span data-ttu-id="271c0-104">This article shows you how to use CLI flags to deploy a VM into an existing Virtual Network (VNet).</span><span class="sxs-lookup"><span data-stu-id="271c0-104">This article shows you how to use CLI flags to deploy a VM into an existing Virtual Network (VNet).</span></span>  <span data-ttu-id="271c0-105">The requirements are:</span><span class="sxs-lookup"><span data-stu-id="271c0-105">The requirements are:</span></span>

- [<span data-ttu-id="271c0-106">an Azure account</span><span class="sxs-lookup"><span data-stu-id="271c0-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="271c0-107">SSH public and private key files</span><span class="sxs-lookup"><span data-stu-id="271c0-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="271c0-108">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="271c0-108">CLI versions to complete the task</span></span>
<span data-ttu-id="271c0-109">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="271c0-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="271c0-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="271c0-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="271c0-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="271c0-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="271c0-112">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="271c0-112">Quick Commands</span></span>

<span data-ttu-id="271c0-113">If you need to quickly accomplish the task, the following section details the  commands needed.</span><span class="sxs-lookup"><span data-stu-id="271c0-113">If you need to quickly accomplish the task, the following section details the  commands needed.</span></span> <span data-ttu-id="271c0-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="271c0-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#detailed-walkthrough).</span></span>

<span data-ttu-id="271c0-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span><span class="sxs-lookup"><span data-stu-id="271c0-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="271c0-116">Replace any examples with your own settings.</span><span class="sxs-lookup"><span data-stu-id="271c0-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="271c0-117">Deploy the VM into the virtual network infrastructure</span><span class="sxs-lookup"><span data-stu-id="271c0-117">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-n myVM \
-F myVNet \
-j mySubnet \
-N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="271c0-118">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="271c0-118">Detailed walkthrough</span></span>

<span data-ttu-id="271c0-119">It is recommended that Azure assets like the VNets and NSGs should be static and long lived resources that are rarely deployed.</span><span class="sxs-lookup"><span data-stu-id="271c0-119">It is recommended that Azure assets like the VNets and NSGs should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="271c0-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="271c0-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span>  <span data-ttu-id="271c0-121">Think about a VNet as being a traditional hardware network switch.</span><span class="sxs-lookup"><span data-stu-id="271c0-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="271c0-122">You would not need to configure a brand new hardware switch with each deployment.</span><span class="sxs-lookup"><span data-stu-id="271c0-122">You would not need to configure a brand new hardware switch with each deployment.</span></span>  <span data-ttu-id="271c0-123">With a correctly configured VNet, we can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span><span class="sxs-lookup"><span data-stu-id="271c0-123">With a correctly configured VNet, we can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="271c0-124">Create the Resource group</span><span class="sxs-lookup"><span data-stu-id="271c0-124">Create the Resource group</span></span>

<span data-ttu-id="271c0-125">First we create a Resource Group to organize everything we create in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="271c0-125">First we create a Resource Group to organize everything we create in this walkthrough.</span></span>  <span data-ttu-id="271c0-126">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="271c0-126">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-the-vnet"></a><span data-ttu-id="271c0-127">Create the VNet</span><span class="sxs-lookup"><span data-stu-id="271c0-127">Create the VNet</span></span>

<span data-ttu-id="271c0-128">The first step is to build a VNet to launch the VMs into.</span><span class="sxs-lookup"><span data-stu-id="271c0-128">The first step is to build a VNet to launch the VMs into.</span></span>  <span data-ttu-id="271c0-129">The VNet contains one subnet for this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="271c0-129">The VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="271c0-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="271c0-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-the-nsg"></a><span data-ttu-id="271c0-131">Create the NSG</span><span class="sxs-lookup"><span data-stu-id="271c0-131">Create the NSG</span></span>

<span data-ttu-id="271c0-132">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span><span class="sxs-lookup"><span data-stu-id="271c0-132">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span></span>  <span data-ttu-id="271c0-133">Azure NSGs are equivalent to a firewall at the network layer.</span><span class="sxs-lookup"><span data-stu-id="271c0-133">Azure NSGs are equivalent to a firewall at the network layer.</span></span>  <span data-ttu-id="271c0-134">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="271c0-134">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="271c0-135">Add an inbound SSH allow rule</span><span class="sxs-lookup"><span data-stu-id="271c0-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="271c0-136">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span><span class="sxs-lookup"><span data-stu-id="271c0-136">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix Internet \
--source-port-range 22 \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="271c0-137">Add a subnet to the VNet</span><span class="sxs-lookup"><span data-stu-id="271c0-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="271c0-138">VMs within the VNet must be located in a subnet.</span><span class="sxs-lookup"><span data-stu-id="271c0-138">VMs within the VNet must be located in a subnet.</span></span>  <span data-ttu-id="271c0-139">Each VNet can have multiple subnets.</span><span class="sxs-lookup"><span data-stu-id="271c0-139">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="271c0-140">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span><span class="sxs-lookup"><span data-stu-id="271c0-140">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="271c0-141">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span><span class="sxs-lookup"><span data-stu-id="271c0-141">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="271c0-142">Add a VNic to the subnet</span><span class="sxs-lookup"><span data-stu-id="271c0-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="271c0-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span><span class="sxs-lookup"><span data-stu-id="271c0-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span></span>  <span data-ttu-id="271c0-144">Create a VNic and associate it with the Subnet created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="271c0-144">Create a VNic and associate it with the Subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="271c0-145">Deploy the VM into the VNet and NSG</span><span class="sxs-lookup"><span data-stu-id="271c0-145">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="271c0-146">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span><span class="sxs-lookup"><span data-stu-id="271c0-146">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="271c0-147">The VM can now be deployed inside this existing network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="271c0-147">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="271c0-148">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span><span class="sxs-lookup"><span data-stu-id="271c0-148">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="271c0-149">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="271c0-149">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create myVM \
--resource-group myResourceGroup \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name myVNic
```

<span data-ttu-id="271c0-150">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span><span class="sxs-lookup"><span data-stu-id="271c0-150">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span>  <span data-ttu-id="271c0-151">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span><span class="sxs-lookup"><span data-stu-id="271c0-151">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="271c0-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="271c0-152">Next steps</span></span>

* [<span data-ttu-id="271c0-153">Use an Azure Resource Manager template to create a specific deployment</span><span class="sxs-lookup"><span data-stu-id="271c0-153">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="271c0-154">Create your own custom environment for a Linux VM using Azure CLI commands directly</span><span class="sxs-lookup"><span data-stu-id="271c0-154">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="271c0-155">Create a Linux VM on Azure using templates</span><span class="sxs-lookup"><span data-stu-id="271c0-155">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
