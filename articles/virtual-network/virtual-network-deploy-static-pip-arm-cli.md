---
title: Create a VM with a static public IP address - Azure CLI 2.0 | Microsoft Docs
description: Learn how to create a VM with a static public IP address using the Azure command-line interface (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c32694949880037f01bb2b6b9779d2cbb9809c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551186"
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-cli-20"></a><span data-ttu-id="01094-103">Create a VM with a static public IP address using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="01094-103">Create a VM with a static public IP address using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Template](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Classic)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="01094-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01094-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="01094-111">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="01094-111">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a><span data-ttu-id="01094-112">Create the VM</span><span class="sxs-lookup"><span data-stu-id="01094-112">Create the VM</span></span>

<span data-ttu-id="01094-113">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="01094-113">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="01094-114">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span><span class="sxs-lookup"><span data-stu-id="01094-114">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="01094-115">Change the values, as appropriate, for your environment.</span><span class="sxs-lookup"><span data-stu-id="01094-115">Change the values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="01094-116">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span><span class="sxs-lookup"><span data-stu-id="01094-116">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="01094-117">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01094-117">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="01094-118">From a command shell, login with the command `az login`.</span><span class="sxs-lookup"><span data-stu-id="01094-118">From a command shell, login with the command `az login`.</span></span>
4. <span data-ttu-id="01094-119">Create the VM by executing the script that follows on a Linux or Mac computer.</span><span class="sxs-lookup"><span data-stu-id="01094-119">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="01094-120">The Azure public IP address, virtual network, network interface, and VM resources must all exist in the same location.</span><span class="sxs-lookup"><span data-stu-id="01094-120">The Azure public IP address, virtual network, network interface, and VM resources must all exist in the same location.</span></span> <span data-ttu-id="01094-121">Though the resources don't all have to exist in the same resource group, in the following script they do.</span><span class="sxs-lookup"><span data-stu-id="01094-121">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using the --allocation-method Static option.
# If you do not specify this option, the address is allocated dynamically. The address is assigned to the
# resource from a pool of IP adresses unique to each Azure region. The DnsName must be unique within the
# Azure location it's created in. Download and view the file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists the ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected to the VNet with a static private IP address and associate the public IP address
# resource to the NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with the NIC

VmName="WEB1"

# Replace the value for the VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace the value for the OsImage variable with a value for *urn* from the output returned by entering
# the `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace the following value with the path to your public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove the previous line and you'll be prompted for the password you want to configure for the VM.
```

<span data-ttu-id="01094-122">In addition to creating a VM, the script creates:</span><span class="sxs-lookup"><span data-stu-id="01094-122">In addition to creating a VM, the script creates:</span></span>
- <span data-ttu-id="01094-123">A single premium managed disk by default, but you have other options for the disk type you can create.</span><span class="sxs-lookup"><span data-stu-id="01094-123">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="01094-124">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span><span class="sxs-lookup"><span data-stu-id="01094-124">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="01094-125">Virtual network, subnet, NIC, and public IP address resources.</span><span class="sxs-lookup"><span data-stu-id="01094-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="01094-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span><span class="sxs-lookup"><span data-stu-id="01094-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="01094-127">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="01094-127">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <a name = "validate"></a><span data-ttu-id="01094-128">Validate VM creation and public IP address</span><span class="sxs-lookup"><span data-stu-id="01094-128">Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="01094-129">Enter the command `az resource list --resouce-group IaaSStory --output table` to see a list of the resources created by the script.</span><span class="sxs-lookup"><span data-stu-id="01094-129">Enter the command `az resource list --resouce-group IaaSStory --output table` to see a list of the resources created by the script.</span></span> <span data-ttu-id="01094-130">There should be five resources in the returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="01094-130">There should be five resources in the returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="01094-131">Enter the command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="01094-131">Enter the command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="01094-132">In the returned output, note the value of **IpAddress** and that the value of **PublicIpAllocationMethod** is *Static*.</span><span class="sxs-lookup"><span data-stu-id="01094-132">In the returned output, note the value of **IpAddress** and that the value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="01094-133">Before executing the following command, remove the <>, replace *Username* with the name you used for the **Username** variable in the script, and replace *ipAddress* with the **ipAddress** from the previous step.</span><span class="sxs-lookup"><span data-stu-id="01094-133">Before executing the following command, remove the <>, replace *Username* with the name you used for the **Username** variable in the script, and replace *ipAddress* with the **ipAddress** from the previous step.</span></span> <span data-ttu-id="01094-134">Run the following command to connect to the VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="01094-134">Run the following command to connect to the VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <a name= "clean-up"></a><span data-ttu-id="01094-135">Remove the VM and associated resources</span><span class="sxs-lookup"><span data-stu-id="01094-135">Remove the VM and associated resources</span></span>

<span data-ttu-id="01094-136">It's recommended that you delete the resources created in this exercise if you won't use them in production.</span><span class="sxs-lookup"><span data-stu-id="01094-136">It's recommended that you delete the resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="01094-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span><span class="sxs-lookup"><span data-stu-id="01094-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="01094-138">To remove the resources created during this exercise, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="01094-138">To remove the resources created during this exercise, complete the following steps:</span></span>

1. <span data-ttu-id="01094-139">To view the resources in the resource group, run the `az resource list --resource-group IaaSStory` command.</span><span class="sxs-lookup"><span data-stu-id="01094-139">To view the resources in the resource group, run the `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="01094-140">Confirm there are no resources in the resource group, other than the resources created by the script in this article.</span><span class="sxs-lookup"><span data-stu-id="01094-140">Confirm there are no resources in the resource group, other than the resources created by the script in this article.</span></span> 
3. <span data-ttu-id="01094-141">To delete all resources created in this exercise, run the `az group delete -n IaaSStory` command.</span><span class="sxs-lookup"><span data-stu-id="01094-141">To delete all resources created in this exercise, run the `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="01094-142">The command deletes the resource group and all the resources it contains.</span><span class="sxs-lookup"><span data-stu-id="01094-142">The command deletes the resource group and all the resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01094-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="01094-143">Next steps</span></span>

<span data-ttu-id="01094-144">Any network traffic can flow to and from the VM created in this article.</span><span class="sxs-lookup"><span data-stu-id="01094-144">Any network traffic can flow to and from the VM created in this article.</span></span> <span data-ttu-id="01094-145">You can define inbound and outbound rules within an NSG that limit the traffic that can flow to and from the network interface, the subnet, or both.</span><span class="sxs-lookup"><span data-stu-id="01094-145">You can define inbound and outbound rules within an NSG that limit the traffic that can flow to and from the network interface, the subnet, or both.</span></span> <span data-ttu-id="01094-146">To learn more about NSGs, read the [NSG overview](virtual-networks-nsg.md) article.</span><span class="sxs-lookup"><span data-stu-id="01094-146">To learn more about NSGs, read the [NSG overview](virtual-networks-nsg.md) article.</span></span>