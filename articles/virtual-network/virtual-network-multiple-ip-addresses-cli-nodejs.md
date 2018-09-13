---
title: VM with multiple IP addresses using the Azure CLI 1.0 | Microsoft Docs
description: Learn how to assign multiple IP addresses to a virtual machine using the Azure CLI 1.0 | Resource Manager.
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
ms.openlocfilehash: 9f085dfa1fe4db36d58cb976bb550a46bf241ac7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556028"
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-azure-cli-10"></a><span data-ttu-id="4a08a-103">Assign multiple IP addresses to virtual machines using Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4a08a-103">Assign multiple IP addresses to virtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="4a08a-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="4a08a-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 1.0.</span></span> <span data-ttu-id="4a08a-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="4a08a-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="4a08a-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="4a08a-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a><span data-ttu-id="4a08a-107">Create a VM with multiple IP addresses</span><span class="sxs-lookup"><span data-stu-id="4a08a-107">Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="4a08a-108">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4a08a-108">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="4a08a-109">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span><span class="sxs-lookup"><span data-stu-id="4a08a-109">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="4a08a-110">Change variable names and IP address types as required for your implementation.</span><span class="sxs-lookup"><span data-stu-id="4a08a-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="4a08a-111">Install and configure the Azure CLI 1.0 by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with the `azure-login` command.</span><span class="sxs-lookup"><span data-stu-id="4a08a-111">Install and configure the Azure CLI 1.0 by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with the `azure-login` command.</span></span>

2. <span data-ttu-id="4a08a-112">Create a resource group:</span><span class="sxs-lookup"><span data-stu-id="4a08a-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="4a08a-113">Create a virtual network:</span><span class="sxs-lookup"><span data-stu-id="4a08a-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="4a08a-114">Create a subnet in the virtual network:</span><span class="sxs-lookup"><span data-stu-id="4a08a-114">Create a subnet in the virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="4a08a-115">Create  a storage account for the VM.</span><span class="sxs-lookup"><span data-stu-id="4a08a-115">Create  a storage account for the VM.</span></span> <span data-ttu-id="4a08a-116">Before running the following command, replace *mystorageaccount* with a unique name.</span><span class="sxs-lookup"><span data-stu-id="4a08a-116">Before running the following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="4a08a-117">The name must be unique across Azure:</span><span class="sxs-lookup"><span data-stu-id="4a08a-117">The name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="4a08a-118">Create the IP configurations, a NIC, and assign the IP configurations to the NIC.</span><span class="sxs-lookup"><span data-stu-id="4a08a-118">Create the IP configurations, a NIC, and assign the IP configurations to the NIC.</span></span> <span data-ttu-id="4a08a-119">You can add, remove, or change the configurations as necessary.</span><span class="sxs-lookup"><span data-stu-id="4a08a-119">You can add, remove, or change the configurations as necessary.</span></span> <span data-ttu-id="4a08a-120">The following configurations are described in the scenario:</span><span class="sxs-lookup"><span data-stu-id="4a08a-120">The following configurations are described in the scenario:</span></span>

    <span data-ttu-id="4a08a-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="4a08a-121">**IPConfig-1**</span></span>

    <span data-ttu-id="4a08a-122">Enter the commands that follow to create:</span><span class="sxs-lookup"><span data-stu-id="4a08a-122">Enter the commands that follow to create:</span></span>

    - <span data-ttu-id="4a08a-123">A public IP address resource with a static public IP address</span><span class="sxs-lookup"><span data-stu-id="4a08a-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="4a08a-124">A NIC, assigning the public IP address and a static private IP address to it.</span><span class="sxs-lookup"><span data-stu-id="4a08a-124">A NIC, assigning the public IP address and a static private IP address to it.</span></span>
    
    <span data-ttu-id="4a08a-125">Replace *mypublicdns* with a name that is unique within the Azure location.</span><span class="sxs-lookup"><span data-stu-id="4a08a-125">Replace *mypublicdns* with a name that is unique within the Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="4a08a-126">Public IP addresses have a nominal fee.</span><span class="sxs-lookup"><span data-stu-id="4a08a-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="4a08a-127">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="4a08a-127">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="4a08a-128">There is a limit to the number of public IP addresses that can be used in a subscription.</span><span class="sxs-lookup"><span data-stu-id="4a08a-128">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="4a08a-129">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span><span class="sxs-lookup"><span data-stu-id="4a08a-129">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="4a08a-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="4a08a-130">**IPConfig-2**</span></span>

     <span data-ttu-id="4a08a-131">Enter the following commands to create a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span><span class="sxs-lookup"><span data-stu-id="4a08a-131">Enter the following commands to create a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="4a08a-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="4a08a-132">**IPConfig-3**</span></span>

    <span data-ttu-id="4a08a-133">Enter the following commands to create an IP configuration with a static private IP address and no public IP address:</span><span class="sxs-lookup"><span data-stu-id="4a08a-133">Enter the following commands to create an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="4a08a-134">Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations to any NIC in a VM.</span><span class="sxs-lookup"><span data-stu-id="4a08a-134">Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations to any NIC in a VM.</span></span> <span data-ttu-id="4a08a-135">To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs article.</span><span class="sxs-lookup"><span data-stu-id="4a08a-135">To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="4a08a-136">Create a Linux VM</span><span class="sxs-lookup"><span data-stu-id="4a08a-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="4a08a-137">To change the VM size to Standard DS2 v2, for example, simply add the following property `--vm-size Standard_DS3_v2` to the `azure vm create` command in step 6.</span><span class="sxs-lookup"><span data-stu-id="4a08a-137">To change the VM size to Standard DS2 v2, for example, simply add the following property `--vm-size Standard_DS3_v2` to the `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="4a08a-138">Enter the following command to view the NIC and the associated IP configurations:</span><span class="sxs-lookup"><span data-stu-id="4a08a-138">Enter the following command to view the NIC and the associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="4a08a-139">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span><span class="sxs-lookup"><span data-stu-id="4a08a-139">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <a name="add"></a><span data-ttu-id="4a08a-140">Add IP addresses to a VM</span><span class="sxs-lookup"><span data-stu-id="4a08a-140">Add IP addresses to a VM</span></span>

<span data-ttu-id="4a08a-141">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span><span class="sxs-lookup"><span data-stu-id="4a08a-141">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="4a08a-142">The examples build upon the [scenario](#Scenario) described in this article.</span><span class="sxs-lookup"><span data-stu-id="4a08a-142">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="4a08a-143">Open Azure CLI and complete the remaining steps in this section within a single CLI session.</span><span class="sxs-lookup"><span data-stu-id="4a08a-143">Open Azure CLI and complete the remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="4a08a-144">If you don't already have Azure CLI installed and configured, complete the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span><span class="sxs-lookup"><span data-stu-id="4a08a-144">If you don't already have Azure CLI installed and configured, complete the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="4a08a-145">Complete the steps in one of the following sections, based on your requirements:</span><span class="sxs-lookup"><span data-stu-id="4a08a-145">Complete the steps in one of the following sections, based on your requirements:</span></span>

    - <span data-ttu-id="4a08a-146">**Add a private IP address**</span><span class="sxs-lookup"><span data-stu-id="4a08a-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="4a08a-147">To add a private IP address to a NIC, you must create an IP configuration using the command below.</span><span class="sxs-lookup"><span data-stu-id="4a08a-147">To add a private IP address to a NIC, you must create an IP configuration using the command below.</span></span> <span data-ttu-id="4a08a-148">The static address must be an unused address for the subnet.</span><span class="sxs-lookup"><span data-stu-id="4a08a-148">The static address must be an unused address for the subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="4a08a-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span><span class="sxs-lookup"><span data-stu-id="4a08a-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="4a08a-150">**Add a public IP address**</span><span class="sxs-lookup"><span data-stu-id="4a08a-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="4a08a-151">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span><span class="sxs-lookup"><span data-stu-id="4a08a-151">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="4a08a-152">Complete the steps in one of the sections that follow, as you require.</span><span class="sxs-lookup"><span data-stu-id="4a08a-152">Complete the steps in one of the sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4a08a-153">Public IP addresses have a nominal fee.</span><span class="sxs-lookup"><span data-stu-id="4a08a-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="4a08a-154">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="4a08a-154">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="4a08a-155">There is a limit to the number of public IP addresses that can be used in a subscription.</span><span class="sxs-lookup"><span data-stu-id="4a08a-155">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="4a08a-156">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span><span class="sxs-lookup"><span data-stu-id="4a08a-156">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="4a08a-157">**Associate the resource to a new IP configuration**</span><span class="sxs-lookup"><span data-stu-id="4a08a-157">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="4a08a-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span><span class="sxs-lookup"><span data-stu-id="4a08a-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="4a08a-159">You can either add an existing public IP address resource, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="4a08a-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="4a08a-160">To create a new one, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="4a08a-160">To create a new one, enter the following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="4a08a-161">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="4a08a-161">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="4a08a-162">**Associate the resource to an existing IP configuration**</span><span class="sxs-lookup"><span data-stu-id="4a08a-162">**Associate the resource to an existing IP configuration**</span></span>

        <span data-ttu-id="4a08a-163">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span><span class="sxs-lookup"><span data-stu-id="4a08a-163">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="4a08a-164">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="4a08a-164">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="4a08a-165">Look for a line similar to the one that follows for IPConfig-3 in the returned output:</span><span class="sxs-lookup"><span data-stu-id="4a08a-165">Look for a line similar to the one that follows for IPConfig-3 in the returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="4a08a-166">Since the **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span><span class="sxs-lookup"><span data-stu-id="4a08a-166">Since the **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="4a08a-167">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span><span class="sxs-lookup"><span data-stu-id="4a08a-167">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="4a08a-168">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="4a08a-168">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="4a08a-169">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="4a08a-169">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="4a08a-170">The returned output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="4a08a-170">The returned output is similar to the following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="4a08a-171">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span><span class="sxs-lookup"><span data-stu-id="4a08a-171">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="4a08a-172">Do not add the public IP addresses to the operating system.</span><span class="sxs-lookup"><span data-stu-id="4a08a-172">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
