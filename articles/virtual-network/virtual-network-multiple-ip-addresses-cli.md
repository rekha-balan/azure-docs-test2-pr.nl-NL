---
title: VM with multiple IP addresses using the Azure CLI 2.0 | Microsoft Docs
description: Learn how to assign multiple IP addresses to a virtual machine using the Azure CLI 2.0 | Resource Manager.
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 0e9b2ef89ca39a7988a7b2573496a605dfc604b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661770"
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-cli-20"></a><span data-ttu-id="4cf91-103">Assign multiple IP addresses to virtual machines using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4cf91-103">Assign multiple IP addresses to virtual machines using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="4cf91-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="4cf91-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 2.0.</span></span> <span data-ttu-id="4cf91-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="4cf91-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="4cf91-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="4cf91-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a><span data-ttu-id="4cf91-107">Create a VM with multiple IP addresses</span><span class="sxs-lookup"><span data-stu-id="4cf91-107">Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="4cf91-108">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4cf91-108">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="4cf91-109">Change the values, as appropriate, for your environment.</span><span class="sxs-lookup"><span data-stu-id="4cf91-109">Change the values, as appropriate, for your environment.</span></span> <span data-ttu-id="4cf91-110">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span><span class="sxs-lookup"><span data-stu-id="4cf91-110">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="4cf91-111">Change variable values in "" and IP address types as required for your implementation.</span><span class="sxs-lookup"><span data-stu-id="4cf91-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="4cf91-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span><span class="sxs-lookup"><span data-stu-id="4cf91-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="4cf91-113">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4cf91-113">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="4cf91-114">From a command shell, login with the command `az login` and select the subscription you're using.</span><span class="sxs-lookup"><span data-stu-id="4cf91-114">From a command shell, login with the command `az login` and select the subscription you're using.</span></span>
4. <span data-ttu-id="4cf91-115">Create the VM by executing the script that follows on a Linux or Mac computer.</span><span class="sxs-lookup"><span data-stu-id="4cf91-115">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="4cf91-116">The script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with the two NICs attached to it.</span><span class="sxs-lookup"><span data-stu-id="4cf91-116">The script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="4cf91-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span><span class="sxs-lookup"><span data-stu-id="4cf91-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="4cf91-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span><span class="sxs-lookup"><span data-stu-id="4cf91-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using the `--allocation-method Static` option. If you
# do not specify this option, the address is allocated dynamically. The address is assigned to the resource from a pool
# of IP adresses unique to each Azure region. Download and view the file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists the ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected to the subnet and associate the public IP address to it. Azure will create the
# first IP configuration with a static private IP address and will associate the public IP address resource to it.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it to the NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it to the NIC. This configuration has  static private IP address and   # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations
# to any NIC in a VM. To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach the NIC.

VmName="myVm"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. The script fails if the VM size
# is not supported in the location you select. Run the `azure vm sizes --location estcentralus` command to get a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace the value for the OsImage variable value with a value for *urn* from the utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file. If you're creating a Windows VM, remove the following
# line and you'll be prompted for the password you want to configure for the VM.

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
```

<span data-ttu-id="4cf91-119">In addition to creating a VM with a NIC with 3 IP configurations, the script creates:</span><span class="sxs-lookup"><span data-stu-id="4cf91-119">In addition to creating a VM with a NIC with 3 IP configurations, the script creates:</span></span>

- <span data-ttu-id="4cf91-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span><span class="sxs-lookup"><span data-stu-id="4cf91-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="4cf91-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span><span class="sxs-lookup"><span data-stu-id="4cf91-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="4cf91-122">A virtual network with one subnet and two public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="4cf91-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="4cf91-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span><span class="sxs-lookup"><span data-stu-id="4cf91-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="4cf91-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="4cf91-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="4cf91-125">Public IP addresses have a nominal fee.</span><span class="sxs-lookup"><span data-stu-id="4cf91-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="4cf91-126">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="4cf91-126">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="4cf91-127">There is a limit to the number of public IP addresses that can be used in a subscription.</span><span class="sxs-lookup"><span data-stu-id="4cf91-127">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="4cf91-128">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span><span class="sxs-lookup"><span data-stu-id="4cf91-128">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="4cf91-129">After the VM is created, enter the `az network nic show --name MyNic1 --resource-group myResourceGroup` command to view the NIC configuration.</span><span class="sxs-lookup"><span data-stu-id="4cf91-129">After the VM is created, enter the `az network nic show --name MyNic1 --resource-group myResourceGroup` command to view the NIC configuration.</span></span> <span data-ttu-id="4cf91-130">Enter the `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` to view a list of the IP configurations associated to the NIC.</span><span class="sxs-lookup"><span data-stu-id="4cf91-130">Enter the `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` to view a list of the IP configurations associated to the NIC.</span></span>

<span data-ttu-id="4cf91-131">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span><span class="sxs-lookup"><span data-stu-id="4cf91-131">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <a name="add"></a><span data-ttu-id="4cf91-132">Add IP addresses to a VM</span><span class="sxs-lookup"><span data-stu-id="4cf91-132">Add IP addresses to a VM</span></span>

<span data-ttu-id="4cf91-133">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span><span class="sxs-lookup"><span data-stu-id="4cf91-133">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="4cf91-134">The examples build upon the [scenario](#Scenario) described in this article.</span><span class="sxs-lookup"><span data-stu-id="4cf91-134">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="4cf91-135">Open a command shell and complete the remaining steps in this section within a single session.</span><span class="sxs-lookup"><span data-stu-id="4cf91-135">Open a command shell and complete the remaining steps in this section within a single session.</span></span> <span data-ttu-id="4cf91-136">If you don't already have Azure CLI installed and configured, complete the steps in the [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login to your Azure account with the `az-login` command.</span><span class="sxs-lookup"><span data-stu-id="4cf91-136">If you don't already have Azure CLI installed and configured, complete the steps in the [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login to your Azure account with the `az-login` command.</span></span>

2. <span data-ttu-id="4cf91-137">Complete the steps in one of the following sections, based on your requirements:</span><span class="sxs-lookup"><span data-stu-id="4cf91-137">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="4cf91-138">**Add a private IP address**</span><span class="sxs-lookup"><span data-stu-id="4cf91-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="4cf91-139">To add a private IP address to a NIC, you must create an IP configuration using the command that follows.</span><span class="sxs-lookup"><span data-stu-id="4cf91-139">To add a private IP address to a NIC, you must create an IP configuration using the command that follows.</span></span> <span data-ttu-id="4cf91-140">The static IP address must be an unused address for the subnet.</span><span class="sxs-lookup"><span data-stu-id="4cf91-140">The static IP address must be an unused address for the subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="4cf91-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span><span class="sxs-lookup"><span data-stu-id="4cf91-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="4cf91-142">**Add a public IP address**</span><span class="sxs-lookup"><span data-stu-id="4cf91-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="4cf91-143">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span><span class="sxs-lookup"><span data-stu-id="4cf91-143">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="4cf91-144">Complete the steps in one of the sections that follow, as you require.</span><span class="sxs-lookup"><span data-stu-id="4cf91-144">Complete the steps in one of the sections that follow, as you require.</span></span>

    <span data-ttu-id="4cf91-145">Public IP addresses have a nominal fee.</span><span class="sxs-lookup"><span data-stu-id="4cf91-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="4cf91-146">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="4cf91-146">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="4cf91-147">There is a limit to the number of public IP addresses that can be used in a subscription.</span><span class="sxs-lookup"><span data-stu-id="4cf91-147">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="4cf91-148">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span><span class="sxs-lookup"><span data-stu-id="4cf91-148">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="4cf91-149">**Associate the resource to a new IP configuration**</span><span class="sxs-lookup"><span data-stu-id="4cf91-149">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="4cf91-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span><span class="sxs-lookup"><span data-stu-id="4cf91-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="4cf91-151">You can either add an existing public IP address resource, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="4cf91-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="4cf91-152">To create a new one, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="4cf91-152">To create a new one, enter the following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="4cf91-153">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="4cf91-153">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="4cf91-154">**Associate the resource to an existing IP configuration** A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span><span class="sxs-lookup"><span data-stu-id="4cf91-154">**Associate the resource to an existing IP configuration** A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="4cf91-155">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="4cf91-155">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="4cf91-156">Returned output:</span><span class="sxs-lookup"><span data-stu-id="4cf91-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="4cf91-157">Since the **PublicIpAddressId** column for *IpConfig-3* is blank in the output, no public IP address resource is currently associated to it.</span><span class="sxs-lookup"><span data-stu-id="4cf91-157">Since the **PublicIpAddressId** column for *IpConfig-3* is blank in the output, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="4cf91-158">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span><span class="sxs-lookup"><span data-stu-id="4cf91-158">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="4cf91-159">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="4cf91-159">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="4cf91-160">View the private IP addresses and the public IP address resource Ids assigned to the NIC by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="4cf91-160">View the private IP addresses and the public IP address resource Ids assigned to the NIC by entering the following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="4cf91-161">Returned output:</span><span class="sxs-lookup"><span data-stu-id="4cf91-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="4cf91-162">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span><span class="sxs-lookup"><span data-stu-id="4cf91-162">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="4cf91-163">Do not add the public IP addresses to the operating system.</span><span class="sxs-lookup"><span data-stu-id="4cf91-163">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
