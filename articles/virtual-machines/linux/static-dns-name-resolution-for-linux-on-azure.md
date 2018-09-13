---
title: Use internal DNS for VM name resolution with the Azure CLI 2.0 | Microsoft Docs
description: How to create virtual network interface cards and use internal DNS for VM name resolution on Azure with the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: 9a6be924a9bcb403113f075b3142678f0a989ccd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554628"
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="da799-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span><span class="sxs-lookup"><span data-stu-id="da799-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="da799-104">This article shows you how to set static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="da799-104">This article shows you how to set static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with the Azure CLI 2.0.</span></span> <span data-ttu-id="da799-105">You can also perform these steps with the [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da799-105">You can also perform these steps with the [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="da799-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span><span class="sxs-lookup"><span data-stu-id="da799-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="da799-107">The requirements are:</span><span class="sxs-lookup"><span data-stu-id="da799-107">The requirements are:</span></span>

* [<span data-ttu-id="da799-108">an Azure account</span><span class="sxs-lookup"><span data-stu-id="da799-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="da799-109">SSH public and private key files</span><span class="sxs-lookup"><span data-stu-id="da799-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="da799-110">Quick commands</span><span class="sxs-lookup"><span data-stu-id="da799-110">Quick commands</span></span>
<span data-ttu-id="da799-111">If you need to quickly accomplish the task, the following section details the commands needed.</span><span class="sxs-lookup"><span data-stu-id="da799-111">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="da799-112">More detailed information and context for each step can be found in the rest of the document, [starting here](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="da799-112">More detailed information and context for each step can be found in the rest of the document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="da799-113">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="da799-113">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="da799-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span><span class="sxs-lookup"><span data-stu-id="da799-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="da799-115">Create a virtual network interface card with a static internal DNS name</span><span class="sxs-lookup"><span data-stu-id="da799-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="da799-116">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="da799-116">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="da799-117">The `--internal-dns-name` CLI flag is for setting the DNS label, which provides the static DNS name for the virtual network interface card (vNic).</span><span class="sxs-lookup"><span data-stu-id="da799-117">The `--internal-dns-name` CLI flag is for setting the DNS label, which provides the static DNS name for the virtual network interface card (vNic).</span></span> <span data-ttu-id="da799-118">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="da799-118">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-the-vnic"></a><span data-ttu-id="da799-119">Deploy a VM and connect the vNic</span><span class="sxs-lookup"><span data-stu-id="da799-119">Deploy a VM and connect the vNic</span></span>
<span data-ttu-id="da799-120">Create a VM with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="da799-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="da799-121">The `--nics` flag connects the vNic to the VM during the deployment to Azure.</span><span class="sxs-lookup"><span data-stu-id="da799-121">The `--nics` flag connects the vNic to the VM during the deployment to Azure.</span></span> <span data-ttu-id="da799-122">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span><span class="sxs-lookup"><span data-stu-id="da799-122">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="da799-123">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="da799-123">Detailed walkthrough</span></span>

<span data-ttu-id="da799-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span><span class="sxs-lookup"><span data-stu-id="da799-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span> <span data-ttu-id="da799-125">It is recommended that Azure assets like the virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span><span class="sxs-lookup"><span data-stu-id="da799-125">It is recommended that Azure assets like the virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="da799-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="da799-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="da799-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd to this virtual network for your development or test environments.</span><span class="sxs-lookup"><span data-stu-id="da799-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd to this virtual network for your development or test environments.</span></span>  

<span data-ttu-id="da799-128">Internal DNS names are only resolvable inside an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="da799-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="da799-129">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="da799-129">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="da799-130">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="da799-130">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="da799-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="da799-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="da799-132">Create the resource group</span><span class="sxs-lookup"><span data-stu-id="da799-132">Create the resource group</span></span>
<span data-ttu-id="da799-133">First, create the resource group with [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="da799-133">First, create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="da799-134">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span><span class="sxs-lookup"><span data-stu-id="da799-134">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="da799-135">Create the virtual network</span><span class="sxs-lookup"><span data-stu-id="da799-135">Create the virtual network</span></span>

<span data-ttu-id="da799-136">The next step is to build a virtual network to launch the VMs into.</span><span class="sxs-lookup"><span data-stu-id="da799-136">The next step is to build a virtual network to launch the VMs into.</span></span> <span data-ttu-id="da799-137">The virtual network contains one subnet for this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="da799-137">The virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="da799-138">For more information on Azure virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da799-138">For more information on Azure virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="da799-139">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="da799-139">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="da799-140">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="da799-140">The following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="da799-141">Create the Network Security Group</span><span class="sxs-lookup"><span data-stu-id="da799-141">Create the Network Security Group</span></span>
<span data-ttu-id="da799-142">Azure Network Security Groups are equivalent to a firewall at the network layer.</span><span class="sxs-lookup"><span data-stu-id="da799-142">Azure Network Security Groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="da799-143">For more information about Network Security Groups, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da799-143">For more information about Network Security Groups, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="da799-144">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="da799-144">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="da799-145">The following example creates a network security group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="da799-145">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-to-allow-ssh"></a><span data-ttu-id="da799-146">Add an inbound rule to allow SSH</span><span class="sxs-lookup"><span data-stu-id="da799-146">Add an inbound rule to allow SSH</span></span>
<span data-ttu-id="da799-147">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="da799-147">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="da799-148">The following example creates a rule named `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="da799-148">The following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-the-subnet-with-the-network-security-group"></a><span data-ttu-id="da799-149">Associate the subnet with the Network Security Group</span><span class="sxs-lookup"><span data-stu-id="da799-149">Associate the subnet with the Network Security Group</span></span>
<span data-ttu-id="da799-150">To associate the subnet with the Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="da799-150">To associate the subnet with the Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="da799-151">The following example associates the subnet name `mySubnet` with the Network Security Group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="da799-151">The following example associates the subnet name `mySubnet` with the Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-the-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="da799-152">Create the virtual network interface card and static DNS names</span><span class="sxs-lookup"><span data-stu-id="da799-152">Create the virtual network interface card and static DNS names</span></span>
<span data-ttu-id="da799-153">Azure is very flexible, but to use DNS names for VM name resolution, you need to create virtual network interface cards (vNics) that include a DNS label.</span><span class="sxs-lookup"><span data-stu-id="da799-153">Azure is very flexible, but to use DNS names for VM name resolution, you need to create virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="da799-154">vNics are important as you can reuse them by connecting them to different VMs over the infrastructure lifecycle.</span><span class="sxs-lookup"><span data-stu-id="da799-154">vNics are important as you can reuse them by connecting them to different VMs over the infrastructure lifecycle.</span></span> <span data-ttu-id="da799-155">This approach keeps the vNic as a static resource while the VMs can be temporary.</span><span class="sxs-lookup"><span data-stu-id="da799-155">This approach keeps the vNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="da799-156">By using DNS labeling on the vNic, we are able to enable simple name resolution from other VMs in the VNet.</span><span class="sxs-lookup"><span data-stu-id="da799-156">By using DNS labeling on the vNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span> <span data-ttu-id="da799-157">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="da799-157">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  

<span data-ttu-id="da799-158">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="da799-158">Create the vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="da799-159">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="da799-159">The following example creates a vNic named `myNic`, connects it to the `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="da799-160">Deploy the VM into the virtual network infrastructure</span><span class="sxs-lookup"><span data-stu-id="da799-160">Deploy the VM into the virtual network infrastructure</span></span>
<span data-ttu-id="da799-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span><span class="sxs-lookup"><span data-stu-id="da799-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="da799-162">You can now deploy a VM inside this existing network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="da799-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="da799-163">Create a VM with [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="da799-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="da799-164">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span><span class="sxs-lookup"><span data-stu-id="da799-164">The following example creates a VM named `myVM` with Azure Managed Disks and attaches the vNic named `myNic` from the preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="da799-165">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span><span class="sxs-lookup"><span data-stu-id="da799-165">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="da799-166">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span><span class="sxs-lookup"><span data-stu-id="da799-166">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="da799-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="da799-167">Next steps</span></span>

* [<span data-ttu-id="da799-168">Use an Azure Resource Manager template to create a specific deployment</span><span class="sxs-lookup"><span data-stu-id="da799-168">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="da799-169">Create your own custom environment for a Linux VM using Azure CLI commands directly</span><span class="sxs-lookup"><span data-stu-id="da799-169">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="da799-170">Create a Linux VM on Azure using templates</span><span class="sxs-lookup"><span data-stu-id="da799-170">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
