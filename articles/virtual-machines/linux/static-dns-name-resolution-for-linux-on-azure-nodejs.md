---
title: Using internal DNS for VM name resolution on Azure | Microsoft Docs
description: Using internal DNS for VM name resolution on Azure.
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
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: a4acec5cb7fc93e21670c7cb9a35d10c4ad5bb81
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550019"
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="d3c40-103">Using internal DNS for VM name resolution on Azure</span><span class="sxs-lookup"><span data-stu-id="d3c40-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="d3c40-104">This article shows how to set static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span><span class="sxs-lookup"><span data-stu-id="d3c40-104">This article shows how to set static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="d3c40-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span><span class="sxs-lookup"><span data-stu-id="d3c40-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="d3c40-106">The requirements are:</span><span class="sxs-lookup"><span data-stu-id="d3c40-106">The requirements are:</span></span>

* [<span data-ttu-id="d3c40-107">an Azure account</span><span class="sxs-lookup"><span data-stu-id="d3c40-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="d3c40-108">SSH public and private key files</span><span class="sxs-lookup"><span data-stu-id="d3c40-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="d3c40-109">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="d3c40-109">CLI versions to complete the task</span></span>
<span data-ttu-id="d3c40-110">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="d3c40-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="d3c40-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="d3c40-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="d3c40-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="d3c40-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="d3c40-113">Quick commands</span><span class="sxs-lookup"><span data-stu-id="d3c40-113">Quick commands</span></span>

<span data-ttu-id="d3c40-114">If you need to quickly accomplish the task, the following section details the commands needed.</span><span class="sxs-lookup"><span data-stu-id="d3c40-114">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="d3c40-115">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="d3c40-115">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="d3c40-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span><span class="sxs-lookup"><span data-stu-id="d3c40-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="d3c40-117">Create a VNic with a static internal DNS name</span><span class="sxs-lookup"><span data-stu-id="d3c40-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="d3c40-118">The `-r` cli flag is for setting the DNS label, which provides the static DNS name for the VNic.</span><span class="sxs-lookup"><span data-stu-id="d3c40-118">The `-r` cli flag is for setting the DNS label, which provides the static DNS name for the VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-the-vm-into-the-vnet-nsg-and-connect-the-vnic"></a><span data-ttu-id="d3c40-119">Deploy the VM into the VNet, NSG and, connect the VNic</span><span class="sxs-lookup"><span data-stu-id="d3c40-119">Deploy the VM into the VNet, NSG and, connect the VNic</span></span>

<span data-ttu-id="d3c40-120">The `-N` connects the VNic to the new VM during the deployment to Azure.</span><span class="sxs-lookup"><span data-stu-id="d3c40-120">The `-N` connects the VNic to the new VM during the deployment to Azure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="d3c40-121">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="d3c40-121">Detailed walkthrough</span></span>

<span data-ttu-id="d3c40-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span><span class="sxs-lookup"><span data-stu-id="d3c40-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span>  <span data-ttu-id="d3c40-123">It is recommended that Azure assets like the Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span><span class="sxs-lookup"><span data-stu-id="d3c40-123">It is recommended that Azure assets like the Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="d3c40-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="d3c40-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span>  <span data-ttu-id="d3c40-125">Adding to this static network a Git repository server and a Jenkins automation server delivers CiCd to your development or test environments.</span><span class="sxs-lookup"><span data-stu-id="d3c40-125">Adding to this static network a Git repository server and a Jenkins automation server delivers CiCd to your development or test environments.</span></span>  

<span data-ttu-id="d3c40-126">Internal DNS names are only resolvable inside an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="d3c40-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="d3c40-127">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span><span class="sxs-lookup"><span data-stu-id="d3c40-127">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="d3c40-128">_Replace any examples with your own naming._</span><span class="sxs-lookup"><span data-stu-id="d3c40-128">_Replace any examples with your own naming._</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="d3c40-129">Create the Resource group</span><span class="sxs-lookup"><span data-stu-id="d3c40-129">Create the Resource group</span></span>

<span data-ttu-id="d3c40-130">A Resource Group is needed to organize everything we create in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="d3c40-130">A Resource Group is needed to organize everything we create in this walkthrough.</span></span>  <span data-ttu-id="d3c40-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d3c40-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-the-vnet"></a><span data-ttu-id="d3c40-132">Create the VNet</span><span class="sxs-lookup"><span data-stu-id="d3c40-132">Create the VNet</span></span>

<span data-ttu-id="d3c40-133">The first step is to build a VNet to launch the VMs into.</span><span class="sxs-lookup"><span data-stu-id="d3c40-133">The first step is to build a VNet to launch the VMs into.</span></span>  <span data-ttu-id="d3c40-134">The VNet contains one subnet for this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="d3c40-134">The VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="d3c40-135">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d3c40-135">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-the-nsg"></a><span data-ttu-id="d3c40-136">Create the NSG</span><span class="sxs-lookup"><span data-stu-id="d3c40-136">Create the NSG</span></span>

<span data-ttu-id="d3c40-137">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span><span class="sxs-lookup"><span data-stu-id="d3c40-137">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span></span>  <span data-ttu-id="d3c40-138">Azure NSGs are equivalent to a firewall at the network layer.</span><span class="sxs-lookup"><span data-stu-id="d3c40-138">Azure NSGs are equivalent to a firewall at the network layer.</span></span>  <span data-ttu-id="d3c40-139">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d3c40-139">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="d3c40-140">Add an inbound SSH allow rule</span><span class="sxs-lookup"><span data-stu-id="d3c40-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="d3c40-141">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span><span class="sxs-lookup"><span data-stu-id="d3c40-141">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="d3c40-142">Add a subnet to the VNet</span><span class="sxs-lookup"><span data-stu-id="d3c40-142">Add a subnet to the VNet</span></span>

<span data-ttu-id="d3c40-143">VMs within the VNet must be located in a subnet.</span><span class="sxs-lookup"><span data-stu-id="d3c40-143">VMs within the VNet must be located in a subnet.</span></span>  <span data-ttu-id="d3c40-144">Each VNet can have multiple subnets.</span><span class="sxs-lookup"><span data-stu-id="d3c40-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="d3c40-145">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span><span class="sxs-lookup"><span data-stu-id="d3c40-145">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="d3c40-146">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span><span class="sxs-lookup"><span data-stu-id="d3c40-146">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="d3c40-147">Creating static DNS names</span><span class="sxs-lookup"><span data-stu-id="d3c40-147">Creating static DNS names</span></span>

<span data-ttu-id="d3c40-148">Azure is very flexible, but to use DNS names for VMs name resolution, you need to create them as Virtual network cards (VNics) using DNS labeling.</span><span class="sxs-lookup"><span data-stu-id="d3c40-148">Azure is very flexible, but to use DNS names for VMs name resolution, you need to create them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="d3c40-149">VNics are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span><span class="sxs-lookup"><span data-stu-id="d3c40-149">VNics are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span></span>  <span data-ttu-id="d3c40-150">By using DNS labeling on the VNic, we are able to enable simple name resolution from other VMs in the VNet.</span><span class="sxs-lookup"><span data-stu-id="d3c40-150">By using DNS labeling on the VNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span>  <span data-ttu-id="d3c40-151">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="d3c40-151">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  <span data-ttu-id="d3c40-152">Create a VNic and associate it with the Subnet created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="d3c40-152">Create a VNic and associate it with the Subnet created in the previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="d3c40-153">Deploy the VM into the VNet and NSG</span><span class="sxs-lookup"><span data-stu-id="d3c40-153">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="d3c40-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span><span class="sxs-lookup"><span data-stu-id="d3c40-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="d3c40-155">The VM can now be deployed inside this existing network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="d3c40-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="d3c40-156">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span><span class="sxs-lookup"><span data-stu-id="d3c40-156">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="d3c40-157">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d3c40-157">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="d3c40-158">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span><span class="sxs-lookup"><span data-stu-id="d3c40-158">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span>  <span data-ttu-id="d3c40-159">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span><span class="sxs-lookup"><span data-stu-id="d3c40-159">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d3c40-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3c40-160">Next steps</span></span>

* [<span data-ttu-id="d3c40-161">Use an Azure Resource Manager template to create a specific deployment</span><span class="sxs-lookup"><span data-stu-id="d3c40-161">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d3c40-162">Create your own custom environment for a Linux VM using Azure CLI commands directly</span><span class="sxs-lookup"><span data-stu-id="d3c40-162">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d3c40-163">Create a Linux VM on Azure using templates</span><span class="sxs-lookup"><span data-stu-id="d3c40-163">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
