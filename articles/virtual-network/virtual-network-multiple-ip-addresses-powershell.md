---
title: Multiple IP addresses for Azure virtual machines - PowerShell | Microsoft Docs
description: Learn how to assign multiple IP addresses to a virtual machine using PowerShell | Resource Manager.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: e37c2d1591fbb4a0fbc198697846e2bce73b085b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555501"
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-powershell"></a><span data-ttu-id="cb675-103">Assign multiple IP addresses to virtual machines using PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb675-103">Assign multiple IP addresses to virtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="cb675-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb675-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="cb675-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="cb675-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="cb675-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="cb675-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a><span data-ttu-id="cb675-107">Create a VM with multiple IP addresses</span><span class="sxs-lookup"><span data-stu-id="cb675-107">Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="cb675-108">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span><span class="sxs-lookup"><span data-stu-id="cb675-108">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="cb675-109">Change variable values as required for your implementation.</span><span class="sxs-lookup"><span data-stu-id="cb675-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="cb675-110">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="cb675-110">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="cb675-111">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span><span class="sxs-lookup"><span data-stu-id="cb675-111">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="cb675-112">Login to your account with the `login-azurermaccount` command.</span><span class="sxs-lookup"><span data-stu-id="cb675-112">Login to your account with the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="cb675-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span><span class="sxs-lookup"><span data-stu-id="cb675-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="cb675-114">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="cb675-114">Create a resource group.</span></span> <span data-ttu-id="cb675-115">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="cb675-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="cb675-116">Create a virtual network (VNet) and subnet in the same location as the resource group:</span><span class="sxs-lookup"><span data-stu-id="cb675-116">Create a virtual network (VNet) and subnet in the same location as the resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get the subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="cb675-117">Create a network security group (NSG) and a rule.</span><span class="sxs-lookup"><span data-stu-id="cb675-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="cb675-118">The NSG secures the VM using inbound and outbound rules.</span><span class="sxs-lookup"><span data-stu-id="cb675-118">The NSG secures the VM using inbound and outbound rules.</span></span> <span data-ttu-id="cb675-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span><span class="sxs-lookup"><span data-stu-id="cb675-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="cb675-120">Define the primary IP configuration for the NIC.</span><span class="sxs-lookup"><span data-stu-id="cb675-120">Define the primary IP configuration for the NIC.</span></span> <span data-ttu-id="cb675-121">Change 10.0.0.4 to a valid address in the subnet you created, if you didn't use the value defined previously.</span><span class="sxs-lookup"><span data-stu-id="cb675-121">Change 10.0.0.4 to a valid address in the subnet you created, if you didn't use the value defined previously.</span></span> <span data-ttu-id="cb675-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span><span class="sxs-lookup"><span data-stu-id="cb675-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="cb675-123">Enter the command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="cb675-123">Enter the command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="cb675-124">If the address is available, the output returns *True*.</span><span class="sxs-lookup"><span data-stu-id="cb675-124">If the address is available, the output returns *True*.</span></span> <span data-ttu-id="cb675-125">If it's not available, the output returns *False* and a list of addresses that are available.</span><span class="sxs-lookup"><span data-stu-id="cb675-125">If it's not available, the output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="cb675-126">In the following commands, **Replace <replace-with-your-unique-name> with the unique DNS name to use.**</span><span class="sxs-lookup"><span data-stu-id="cb675-126">In the following commands, **Replace <replace-with-your-unique-name> with the unique DNS name to use.**</span></span> <span data-ttu-id="cb675-127">The name must be unique across all public IP addresses within an Azure region.</span><span class="sxs-lookup"><span data-stu-id="cb675-127">The name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="cb675-128">This is an optional parameter.</span><span class="sxs-lookup"><span data-stu-id="cb675-128">This is an optional parameter.</span></span> <span data-ttu-id="cb675-129">It can be removed if you only want to connect to the VM using the public IP address.</span><span class="sxs-lookup"><span data-stu-id="cb675-129">It can be removed if you only want to connect to the VM using the public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="cb675-130">When you assign multiple IP configurations to a NIC, one configuration must be assigned as the *-Primary*.</span><span class="sxs-lookup"><span data-stu-id="cb675-130">When you assign multiple IP configurations to a NIC, one configuration must be assigned as the *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cb675-131">Public IP addresses have a nominal fee.</span><span class="sxs-lookup"><span data-stu-id="cb675-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="cb675-132">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="cb675-132">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="cb675-133">There is a limit to the number of public IP addresses that can be used in a subscription.</span><span class="sxs-lookup"><span data-stu-id="cb675-133">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="cb675-134">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span><span class="sxs-lookup"><span data-stu-id="cb675-134">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="cb675-135">Define the secondary IP configurations for the NIC.</span><span class="sxs-lookup"><span data-stu-id="cb675-135">Define the secondary IP configurations for the NIC.</span></span> <span data-ttu-id="cb675-136">You can add or remove configurations as necessary.</span><span class="sxs-lookup"><span data-stu-id="cb675-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="cb675-137">Each IP configuration must have a private IP address assigned.</span><span class="sxs-lookup"><span data-stu-id="cb675-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="cb675-138">Each configuration can optionally have one public IP address assigned.</span><span class="sxs-lookup"><span data-stu-id="cb675-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="cb675-139">Create the NIC and associate the three IP configurations to it:</span><span class="sxs-lookup"><span data-stu-id="cb675-139">Create the NIC and associate the three IP configurations to it:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="cb675-140">Though all configurations are assigned to one NIC in this article, you can assign multiple IP configurations to every NIC attached to the VM.</span><span class="sxs-lookup"><span data-stu-id="cb675-140">Though all configurations are assigned to one NIC in this article, you can assign multiple IP configurations to every NIC attached to the VM.</span></span> <span data-ttu-id="cb675-141">To learn how to create a VM with multiple NICs, read the [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span><span class="sxs-lookup"><span data-stu-id="cb675-141">To learn how to create a VM with multiple NICs, read the [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="cb675-142">Create the VM by entering the following commands:</span><span class="sxs-lookup"><span data-stu-id="cb675-142">Create the VM by entering the following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted to enter a sername and password for the VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create the VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="cb675-143">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span><span class="sxs-lookup"><span data-stu-id="cb675-143">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="cb675-144">Do not add the public IP addresses to the operating system.</span><span class="sxs-lookup"><span data-stu-id="cb675-144">Do not add the public IP addresses to the operating system.</span></span>

## <a name="add"></a><span data-ttu-id="cb675-145">Add IP addresses to a VM</span><span class="sxs-lookup"><span data-stu-id="cb675-145">Add IP addresses to a VM</span></span>

<span data-ttu-id="cb675-146">You can add private and public IP addresses to a NIC by completing the steps that follow.</span><span class="sxs-lookup"><span data-stu-id="cb675-146">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="cb675-147">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span><span class="sxs-lookup"><span data-stu-id="cb675-147">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="cb675-148">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="cb675-148">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="cb675-149">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span><span class="sxs-lookup"><span data-stu-id="cb675-149">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="cb675-150">Change the "values" of the following $Variables to the name of the NIC you want to add IP address to and the resource group and location the NIC exists in:</span><span class="sxs-lookup"><span data-stu-id="cb675-150">Change the "values" of the following $Variables to the name of the NIC you want to add IP address to and the resource group and location the NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="cb675-151">If you don't know the name of the NIC you want to change, enter the following commands, then change the values of the previous variables:</span><span class="sxs-lookup"><span data-stu-id="cb675-151">If you don't know the name of the NIC you want to change, enter the following commands, then change the values of the previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="cb675-152">Create a variable and set it to the existing NIC by typing the following command:</span><span class="sxs-lookup"><span data-stu-id="cb675-152">Create a variable and set it to the existing NIC by typing the following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="cb675-153">In the following commands, change *MyVNet* and *MySubnet* to the names of the VNet and subnet the NIC is connected to.</span><span class="sxs-lookup"><span data-stu-id="cb675-153">In the following commands, change *MyVNet* and *MySubnet* to the names of the VNet and subnet the NIC is connected to.</span></span> <span data-ttu-id="cb675-154">Enter the commands to retrieve the VNet and subnet objects the NIC is connected to:</span><span class="sxs-lookup"><span data-stu-id="cb675-154">Enter the commands to retrieve the VNet and subnet objects the NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="cb675-155">If you don't know the VNet or subnet name the NIC is connected to, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="cb675-155">If you don't know the VNet or subnet name the NIC is connected to, enter the following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="cb675-156">In the output, look for text similar to the following example output:</span><span class="sxs-lookup"><span data-stu-id="cb675-156">In the output, look for text similar to the following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="cb675-157">In this output, *MyVnet* is the VNet and *MySubnet* is the subnet the NIC is connected to.</span><span class="sxs-lookup"><span data-stu-id="cb675-157">In this output, *MyVnet* is the VNet and *MySubnet* is the subnet the NIC is connected to.</span></span>

5. <span data-ttu-id="cb675-158">Complete the steps in one of the following sections, based on your requirements:</span><span class="sxs-lookup"><span data-stu-id="cb675-158">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="cb675-159">**Add a private IP address**</span><span class="sxs-lookup"><span data-stu-id="cb675-159">**Add a private IP address**</span></span>

    <span data-ttu-id="cb675-160">To add a private IP address to a NIC, you must create an IP configuration.</span><span class="sxs-lookup"><span data-stu-id="cb675-160">To add a private IP address to a NIC, you must create an IP configuration.</span></span> <span data-ttu-id="cb675-161">The following command creates a configuration with a static IP address of 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="cb675-161">The following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="cb675-162">When specifying a static IP address, it must be an unused address for the subnet.</span><span class="sxs-lookup"><span data-stu-id="cb675-162">When specifying a static IP address, it must be an unused address for the subnet.</span></span> <span data-ttu-id="cb675-163">It's recommended that you first test the address to ensure it's available by entering the `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span><span class="sxs-lookup"><span data-stu-id="cb675-163">It's recommended that you first test the address to ensure it's available by entering the `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="cb675-164">If the IP address is available, the output returns *True*.</span><span class="sxs-lookup"><span data-stu-id="cb675-164">If the IP address is available, the output returns *True*.</span></span> <span data-ttu-id="cb675-165">If it's not available, the output returns *False*, and a list of addresses that are available.</span><span class="sxs-lookup"><span data-stu-id="cb675-165">If it's not available, the output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="cb675-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span><span class="sxs-lookup"><span data-stu-id="cb675-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="cb675-167">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span><span class="sxs-lookup"><span data-stu-id="cb675-167">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="cb675-168">**Add a public IP address**</span><span class="sxs-lookup"><span data-stu-id="cb675-168">**Add a public IP address**</span></span>

    <span data-ttu-id="cb675-169">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span><span class="sxs-lookup"><span data-stu-id="cb675-169">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="cb675-170">Complete the steps in one of the sections that follow, as you require.</span><span class="sxs-lookup"><span data-stu-id="cb675-170">Complete the steps in one of the sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cb675-171">Public IP addresses have a nominal fee.</span><span class="sxs-lookup"><span data-stu-id="cb675-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="cb675-172">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="cb675-172">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="cb675-173">There is a limit to the number of public IP addresses that can be used in a subscription.</span><span class="sxs-lookup"><span data-stu-id="cb675-173">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="cb675-174">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span><span class="sxs-lookup"><span data-stu-id="cb675-174">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="cb675-175">**Associate the public IP address resource to a new IP configuration**</span><span class="sxs-lookup"><span data-stu-id="cb675-175">**Associate the public IP address resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="cb675-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span><span class="sxs-lookup"><span data-stu-id="cb675-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="cb675-177">You can either add an existing public IP address resource, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="cb675-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="cb675-178">To create a new one, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="cb675-178">To create a new one, enter the following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="cb675-179">To create a new IP configuration with a static private IP address and the associated *myPublicIp3* public IP address resource, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="cb675-179">To create a new IP configuration with a static private IP address and the associated *myPublicIp3* public IP address resource, enter the following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="cb675-180">**Associate the public IP address resource to an existing IP configuration**</span><span class="sxs-lookup"><span data-stu-id="cb675-180">**Associate the public IP address resource to an existing IP configuration**</span></span>

        <span data-ttu-id="cb675-181">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span><span class="sxs-lookup"><span data-stu-id="cb675-181">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="cb675-182">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="cb675-182">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="cb675-183">You see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="cb675-183">You see output similar to the following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="cb675-184">Since the **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span><span class="sxs-lookup"><span data-stu-id="cb675-184">Since the **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="cb675-185">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span><span class="sxs-lookup"><span data-stu-id="cb675-185">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="cb675-186">Enter the following command to associate the public IP address resource to the existing IP configuration named *IpConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="cb675-186">Enter the following command to associate the public IP address resource to the existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="cb675-187">Set the NIC with the new IP configuration by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="cb675-187">Set the NIC with the new IP configuration by entering the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="cb675-188">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="cb675-188">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="cb675-189">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span><span class="sxs-lookup"><span data-stu-id="cb675-189">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="cb675-190">Do not add the public IP address to the operating system.</span><span class="sxs-lookup"><span data-stu-id="cb675-190">Do not add the public IP address to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
