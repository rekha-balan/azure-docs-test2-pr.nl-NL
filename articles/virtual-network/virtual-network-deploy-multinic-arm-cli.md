---
title: Create a VM with multiple NICs - Azure CLI 2.0 | Microsoft Docs
description: Learn how to create a VM with multiple NICs using the Azure CLI 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 19b1757dd694e756cfd2d0d6cd67e64f43ccab7f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563414"
---
# <a name="create-a-vm-with-multiple-nics-using-the-azure-cli-20"></a><span data-ttu-id="f1a17-103">Create a VM with multiple NICs using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f1a17-103">Create a VM with multiple NICs using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f1a17-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f1a17-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="f1a17-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f1a17-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <a name="create"></a><span data-ttu-id="f1a17-106">Create the VM</span><span class="sxs-lookup"><span data-stu-id="f1a17-106">Create the VM</span></span>

<span data-ttu-id="f1a17-107">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f1a17-107">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="f1a17-108">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span><span class="sxs-lookup"><span data-stu-id="f1a17-108">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="f1a17-109">Change the values, as appropriate, for your environment.</span><span class="sxs-lookup"><span data-stu-id="f1a17-109">Change the values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="f1a17-110">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span><span class="sxs-lookup"><span data-stu-id="f1a17-110">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="f1a17-111">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f1a17-111">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="f1a17-112">From a command shell, login with the command `az login`.</span><span class="sxs-lookup"><span data-stu-id="f1a17-112">From a command shell, login with the command `az login`.</span></span>
4. <span data-ttu-id="f1a17-113">Create the VM by executing the script that follows on a Linux or Mac computer.</span><span class="sxs-lookup"><span data-stu-id="f1a17-113">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="f1a17-114">The script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with the two NICs attached to it.</span><span class="sxs-lookup"><span data-stu-id="f1a17-114">The script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="f1a17-115">One of the NICs is connected to one subnet and is assigned a static public and private IP address.</span><span class="sxs-lookup"><span data-stu-id="f1a17-115">One of the NICs is connected to one subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="f1a17-116">The other NIC is connected to the other subnet and is assigned a static private IP address and no public IP address.</span><span class="sxs-lookup"><span data-stu-id="f1a17-116">The other NIC is connected to the other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="f1a17-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span><span class="sxs-lookup"><span data-stu-id="f1a17-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="f1a17-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span><span class="sxs-lookup"><span data-stu-id="f1a17-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# The address is assigned to the resource from a pool of IP adresses unique to each Azure region. 
# Download and view the file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# the ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within the VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected to one of the subnets. The NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses to each NIC. To learn more about IP addressing
# options for NICs, enter the az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it to the other subnet. Though multiple NICs attached to the same
# VM can be connected to different subnets, the subnets must all be within the same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach the two NICs.

VmName="WEB"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure to select a VM size that supports the number of NICs you want to attach to the VM.
# You must create the VM with at least two NICs if you want to add more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs to the VM after VM creation, regardless of how many NICs the VM supports.
# The VM size specified in the following variable supports two NICs.

VmSize="Standard_DS2"

# Replace the value for the OsImage variable value with a value for *urn* from the output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing the following command, add variable names of additional NICs you may have added to the script that
# you want to attach to the VM. If creating a Windows VM, remove the **ssh-key-value** line and you'll be prompted for
# the password you want to configure for the VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

<span data-ttu-id="f1a17-119">In addition to creating a VM with two NICs, the script creates:</span><span class="sxs-lookup"><span data-stu-id="f1a17-119">In addition to creating a VM with two NICs, the script creates:</span></span>
- <span data-ttu-id="f1a17-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span><span class="sxs-lookup"><span data-stu-id="f1a17-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="f1a17-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span><span class="sxs-lookup"><span data-stu-id="f1a17-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="f1a17-122">A virtual network with two subnets and a single public IP address.</span><span class="sxs-lookup"><span data-stu-id="f1a17-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="f1a17-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span><span class="sxs-lookup"><span data-stu-id="f1a17-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="f1a17-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="f1a17-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <a name = "validate"></a><span data-ttu-id="f1a17-125">Validate VM creation and NICs</span><span class="sxs-lookup"><span data-stu-id="f1a17-125">Validate VM creation and NICs</span></span>

1. <span data-ttu-id="f1a17-126">Enter the command `az resource list --resouce-group Multi-NIC-VM --output table` to see a list of the resources created by the script.</span><span class="sxs-lookup"><span data-stu-id="f1a17-126">Enter the command `az resource list --resouce-group Multi-NIC-VM --output table` to see a list of the resources created by the script.</span></span> <span data-ttu-id="f1a17-127">There should be six resources in the returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f1a17-127">There should be six resources in the returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="f1a17-128">Enter the command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="f1a17-128">Enter the command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="f1a17-129">In the returned output, note the value of **IpAddress** and that the value of **PublicIpAllocationMethod** is *Static*.</span><span class="sxs-lookup"><span data-stu-id="f1a17-129">In the returned output, note the value of **IpAddress** and that the value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="f1a17-130">Before running the following command, remove the <>, replace *Username* with the name you used for the **Username** variable in the script, and replace *ipAddress* with the **ipAddress** from the previous step.</span><span class="sxs-lookup"><span data-stu-id="f1a17-130">Before running the following command, remove the <>, replace *Username* with the name you used for the **Username** variable in the script, and replace *ipAddress* with the **ipAddress** from the previous step.</span></span> <span data-ttu-id="f1a17-131">Run the following command to connect to the VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="f1a17-131">Run the following command to connect to the VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="f1a17-132">Once connected to the VM, run the `sudo ifconfig` command to see *eth0* and *eth1* interfaces.</span><span class="sxs-lookup"><span data-stu-id="f1a17-132">Once connected to the VM, run the `sudo ifconfig` command to see *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="f1a17-133">Each NIC has been assigned the static private IP addresses specified in the script by the Azure DHCP servers.</span><span class="sxs-lookup"><span data-stu-id="f1a17-133">Each NIC has been assigned the static private IP addresses specified in the script by the Azure DHCP servers.</span></span> <span data-ttu-id="f1a17-134">The IP and MAC addresses assigned to the NICs do not change until the VM is deleted.</span><span class="sxs-lookup"><span data-stu-id="f1a17-134">The IP and MAC addresses assigned to the NICs do not change until the VM is deleted.</span></span> <span data-ttu-id="f1a17-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity to the computer.</span><span class="sxs-lookup"><span data-stu-id="f1a17-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity to the computer.</span></span> <span data-ttu-id="f1a17-136">Public IP addresses do not appear within the operating system, as they are network address translated to and from the private IP address by the Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f1a17-136">Public IP addresses do not appear within the operating system, as they are network address translated to and from the private IP address by the Azure infrastructure.</span></span>

## <a name= "clean-up"></a><span data-ttu-id="f1a17-137">Remove the VM and associated resources</span><span class="sxs-lookup"><span data-stu-id="f1a17-137">Remove the VM and associated resources</span></span>

<span data-ttu-id="f1a17-138">It's recommended that you delete the resources created in this exercise if you won't use them in production.</span><span class="sxs-lookup"><span data-stu-id="f1a17-138">It's recommended that you delete the resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="f1a17-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span><span class="sxs-lookup"><span data-stu-id="f1a17-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="f1a17-140">To remove the resources created during this exercise, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="f1a17-140">To remove the resources created during this exercise, complete the following steps:</span></span>
1. <span data-ttu-id="f1a17-141">To view the resources in the resource group, run the `az resource list --resource-group Multi-NIC-VM` command.</span><span class="sxs-lookup"><span data-stu-id="f1a17-141">To view the resources in the resource group, run the `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="f1a17-142">Confirm there are no resources in the resource group, other than the resources created by the script in this article.</span><span class="sxs-lookup"><span data-stu-id="f1a17-142">Confirm there are no resources in the resource group, other than the resources created by the script in this article.</span></span> 
3. <span data-ttu-id="f1a17-143">To delete all resources created in this exercise, run the `az group delete --name Multi-NIC-VM` command.</span><span class="sxs-lookup"><span data-stu-id="f1a17-143">To delete all resources created in this exercise, run the `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="f1a17-144">The command deletes the resource group and all the resources it contains.</span><span class="sxs-lookup"><span data-stu-id="f1a17-144">The command deletes the resource group and all the resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1a17-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1a17-145">Next steps</span></span>

<span data-ttu-id="f1a17-146">Any network traffic can flow to and from the VM created in this article.</span><span class="sxs-lookup"><span data-stu-id="f1a17-146">Any network traffic can flow to and from the VM created in this article.</span></span> <span data-ttu-id="f1a17-147">You can define inbound and outbound rules within an NSG that limit the traffic that can flow to and from each network interface, each subnet, or both.</span><span class="sxs-lookup"><span data-stu-id="f1a17-147">You can define inbound and outbound rules within an NSG that limit the traffic that can flow to and from each network interface, each subnet, or both.</span></span> <span data-ttu-id="f1a17-148">To learn more about NSGs, read the [NSG overview](virtual-networks-nsg.md) article.</span><span class="sxs-lookup"><span data-stu-id="f1a17-148">To learn more about NSGs, read the [NSG overview](virtual-networks-nsg.md) article.</span></span>