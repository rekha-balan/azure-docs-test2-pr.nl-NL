---
title: Deploy Linux VM into existing network with the Azure CLI 2.0 | Microsoft Docs
description: Learn how to deploy a Linux virtual machine into an existing Virtual Network using the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 01/31/2017
ms.author: iainfou
ms.openlocfilehash: 8f40fbdca22b6fc7591c82f7543492bafaba1041
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562727"
---
# <a name="deploy-a-linux-vm-into-an-existing-virtual-network"></a><span data-ttu-id="b2119-103">Deploy a Linux VM into an existing virtual network</span><span class="sxs-lookup"><span data-stu-id="b2119-103">Deploy a Linux VM into an existing virtual network</span></span>

<span data-ttu-id="b2119-104">This article shows you how to use the Azure CLI 2.0 to deploy a virtual machine (VM) into an existing virtual network.</span><span class="sxs-lookup"><span data-stu-id="b2119-104">This article shows you how to use the Azure CLI 2.0 to deploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="b2119-105">The requirements are:</span><span class="sxs-lookup"><span data-stu-id="b2119-105">The requirements are:</span></span>

- [<span data-ttu-id="b2119-106">an Azure account</span><span class="sxs-lookup"><span data-stu-id="b2119-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="b2119-107">SSH public and private key files</span><span class="sxs-lookup"><span data-stu-id="b2119-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="b2119-108">You can also perform these steps with the [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2119-108">You can also perform these steps with the [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="b2119-109">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="b2119-109">Quick Commands</span></span>
<span data-ttu-id="b2119-110">If you need to quickly accomplish the task, the following section details the  commands needed.</span><span class="sxs-lookup"><span data-stu-id="b2119-110">If you need to quickly accomplish the task, the following section details the  commands needed.</span></span> <span data-ttu-id="b2119-111">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b2119-111">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="b2119-112">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b2119-112">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b2119-113">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="b2119-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b2119-114">Example parameter names include `myResourceGroup`, `myVnet`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="b2119-114">Example parameter names include `myResourceGroup`, `myVnet`, and `myVM`.</span></span>

<span data-ttu-id="b2119-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span><span class="sxs-lookup"><span data-stu-id="b2119-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="b2119-116">Deploy the VM into the virtual network infrastructure</span><span class="sxs-lookup"><span data-stu-id="b2119-116">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b2119-117">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="b2119-117">Detailed walkthrough</span></span>

<span data-ttu-id="b2119-118">It is recommended that Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span><span class="sxs-lookup"><span data-stu-id="b2119-118">It is recommended that Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="b2119-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b2119-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="b2119-120">Think about a virtual network as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span><span class="sxs-lookup"><span data-stu-id="b2119-120">Think about a virtual network as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="b2119-121">With a correctly configured virtual network, we can continue to deploy new VMs into that virtual network over and over with few, if any, changes required over the life of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="b2119-121">With a correctly configured virtual network, we can continue to deploy new VMs into that virtual network over and over with few, if any, changes required over the life of the virtual network.</span></span>

<span data-ttu-id="b2119-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b2119-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b2119-123">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="b2119-123">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b2119-124">Example parameter names include `myResourceGroup`, `myVnet`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="b2119-124">Example parameter names include `myResourceGroup`, `myVnet`, and `myVM`.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="b2119-125">Create the resource group</span><span class="sxs-lookup"><span data-stu-id="b2119-125">Create the resource group</span></span>

<span data-ttu-id="b2119-126">First we create an Azure resource group to organize everything we create in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="b2119-126">First we create an Azure resource group to organize everything we create in this walkthrough.</span></span> <span data-ttu-id="b2119-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2119-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b2119-128">Create the resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b2119-128">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b2119-129">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span><span class="sxs-lookup"><span data-stu-id="b2119-129">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location westus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="b2119-130">Create the virtual network</span><span class="sxs-lookup"><span data-stu-id="b2119-130">Create the virtual network</span></span>

<span data-ttu-id="b2119-131">Lets build an Azure virtual network to launch the VMs into.</span><span class="sxs-lookup"><span data-stu-id="b2119-131">Lets build an Azure virtual network to launch the VMs into.</span></span> <span data-ttu-id="b2119-132">For more information on virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2119-132">For more information on virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b2119-133">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="b2119-133">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="b2119-134">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="b2119-134">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location westus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="b2119-135">Create the network security group</span><span class="sxs-lookup"><span data-stu-id="b2119-135">Create the network security group</span></span>

<span data-ttu-id="b2119-136">Azure network security groups are equivalent to a firewall at the network layer.</span><span class="sxs-lookup"><span data-stu-id="b2119-136">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="b2119-137">For more information on network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2119-137">For more information on network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b2119-138">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="b2119-138">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="b2119-139">The following example creates a network security group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="b2119-139">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location westus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="b2119-140">Add an inbound SSH allow rule</span><span class="sxs-lookup"><span data-stu-id="b2119-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="b2119-141">The Linux VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span><span class="sxs-lookup"><span data-stu-id="b2119-141">The Linux VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span> <span data-ttu-id="b2119-142">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="b2119-142">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="b2119-143">The following example creates a rule named `myNetworkSecurityGroupRuleSSH`:</span><span class="sxs-lookup"><span data-stu-id="b2119-143">The following example creates a rule named `myNetworkSecurityGroupRuleSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="attach-the-subnet-to-the-network-security-group"></a><span data-ttu-id="b2119-144">Attach the subnet to the network security group</span><span class="sxs-lookup"><span data-stu-id="b2119-144">Attach the subnet to the network security group</span></span>

<span data-ttu-id="b2119-145">The network security group rules can be applied to a subnet or a specific virtual network interface.</span><span class="sxs-lookup"><span data-stu-id="b2119-145">The network security group rules can be applied to a subnet or a specific virtual network interface.</span></span> <span data-ttu-id="b2119-146">Lets attach the network security group to our subnet.</span><span class="sxs-lookup"><span data-stu-id="b2119-146">Lets attach the network security group to our subnet.</span></span> <span data-ttu-id="b2119-147">Attach your subnet to the network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="b2119-147">Attach your subnet to the network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-to-the-subnet"></a><span data-ttu-id="b2119-148">Add a virtual network interface card to the subnet</span><span class="sxs-lookup"><span data-stu-id="b2119-148">Add a virtual network interface card to the subnet</span></span>

<span data-ttu-id="b2119-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them to different VMs.</span><span class="sxs-lookup"><span data-stu-id="b2119-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="b2119-150">This reuse allows you to keep the VNic as a static resource while the VMs can be temporary.</span><span class="sxs-lookup"><span data-stu-id="b2119-150">This reuse allows you to keep the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="b2119-151">Create a VNic and associate it with the subnet with [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b2119-151">Create a VNic and associate it with the subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="b2119-152">The following example creates a VNic named `myNic`:</span><span class="sxs-lookup"><span data-stu-id="b2119-152">The following example creates a VNic named `myNic`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location westus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="b2119-153">Deploy the VM into the virtual network infrastructure</span><span class="sxs-lookup"><span data-stu-id="b2119-153">Deploy the VM into the virtual network infrastructure</span></span>

<span data-ttu-id="b2119-154">We now have a virtual network, a subnet, and a network security group acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span><span class="sxs-lookup"><span data-stu-id="b2119-154">We now have a virtual network, a subnet, and a network security group acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="b2119-155">The VM can now be deployed inside this existing network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b2119-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="b2119-156">Create your VM with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b2119-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b2119-157">For more information on the flags to use with the Azure CLI 2.0 to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2119-157">For more information on the flags to use with the Azure CLI 2.0 to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b2119-158">The following example creates a VM using Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="b2119-158">The following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="b2119-159">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span><span class="sxs-lookup"><span data-stu-id="b2119-159">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="b2119-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2119-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="b2119-161">If you wish to use unmanaged disks, see the additional note below.</span><span class="sxs-lookup"><span data-stu-id="b2119-161">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic
```

<span data-ttu-id="b2119-162">If you use managed disks, skip this step.</span><span class="sxs-lookup"><span data-stu-id="b2119-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="b2119-163">If you wish to use unmanaged disks, you need to add the following additional parameters to the proceeding command to create unmanaged disks in the storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="b2119-163">If you wish to use unmanaged disks, you need to add the following additional parameters to the proceeding command to create unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="b2119-164">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span><span class="sxs-lookup"><span data-stu-id="b2119-164">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="b2119-165">To reiterate, once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span><span class="sxs-lookup"><span data-stu-id="b2119-165">To reiterate, once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="b2119-166">In this example, we did not create and assign a public IP address to the VNic, so this VM is not publicly accessible over the Internet.</span><span class="sxs-lookup"><span data-stu-id="b2119-166">In this example, we did not create and assign a public IP address to the VNic, so this VM is not publicly accessible over the Internet.</span></span> <span data-ttu-id="b2119-167">For more information, see [Create a VM with a static public IP using the Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2119-167">For more information, see [Create a VM with a static public IP using the Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2119-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2119-168">Next steps</span></span>
<span data-ttu-id="b2119-169">For more information about ways to create virtual machines in Azure, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="b2119-169">For more information about ways to create virtual machines in Azure, see the following resources:</span></span>

* [<span data-ttu-id="b2119-170">Use an Azure Resource Manager template to create a specific deployment</span><span class="sxs-lookup"><span data-stu-id="b2119-170">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b2119-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span><span class="sxs-lookup"><span data-stu-id="b2119-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="b2119-172">Create a Linux VM on Azure using templates</span><span class="sxs-lookup"><span data-stu-id="b2119-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
