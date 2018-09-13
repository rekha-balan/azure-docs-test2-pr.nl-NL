---
title: Create a VM (Classic) with multiple NICs using PowerShell | Microsoft Docs
description: Learn how to create and configure VMs with multiple NICs using PowerShell.
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 738d2087bd5f7b20372232be1e386c90d3ea6e4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550622"
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="6a872-103">Create a VM (Classic) with multiple NICs</span><span class="sxs-lookup"><span data-stu-id="6a872-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="6a872-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span><span class="sxs-lookup"><span data-stu-id="6a872-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="6a872-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span><span class="sxs-lookup"><span data-stu-id="6a872-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="6a872-106">Multiple NICs also provide isolation of traffic between NICs.</span><span class="sxs-lookup"><span data-stu-id="6a872-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Multi NIC for VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="6a872-108">The figure shows a VM with three NICs, each connected to a different subnet.</span><span class="sxs-lookup"><span data-stu-id="6a872-108">The figure shows a VM with three NICs, each connected to a different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a872-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6a872-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6a872-110">This article covers using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="6a872-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="6a872-111">Microsoft recommends that most new deployments use Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6a872-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="6a872-112">Internet-facing VIP (classic deployments) is only supported on the "default" NIC.</span><span class="sxs-lookup"><span data-stu-id="6a872-112">Internet-facing VIP (classic deployments) is only supported on the "default" NIC.</span></span> <span data-ttu-id="6a872-113">There is only one VIP to the IP of the default NIC.</span><span class="sxs-lookup"><span data-stu-id="6a872-113">There is only one VIP to the IP of the default NIC.</span></span>
* <span data-ttu-id="6a872-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span><span class="sxs-lookup"><span data-stu-id="6a872-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="6a872-115">The order of the NICs from inside the VM will be random, and could also change across Azure infrastructure updates.</span><span class="sxs-lookup"><span data-stu-id="6a872-115">The order of the NICs from inside the VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="6a872-116">However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same.</span><span class="sxs-lookup"><span data-stu-id="6a872-116">However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same.</span></span> <span data-ttu-id="6a872-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed to **Eth2**, but the IP and MAC pairing will remain the same.</span><span class="sxs-lookup"><span data-stu-id="6a872-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed to **Eth2**, but the IP and MAC pairing will remain the same.</span></span> <span data-ttu-id="6a872-118">When a restart is customer-initiated, the NIC order will remain the same.</span><span class="sxs-lookup"><span data-stu-id="6a872-118">When a restart is customer-initiated, the NIC order will remain the same.</span></span>
* <span data-ttu-id="6a872-119">The address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in the same subnet.</span><span class="sxs-lookup"><span data-stu-id="6a872-119">The address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in the same subnet.</span></span>
* <span data-ttu-id="6a872-120">The VM size determines the number of NICS that you can create for a VM.</span><span class="sxs-lookup"><span data-stu-id="6a872-120">The VM size determines the number of NICS that you can create for a VM.</span></span> <span data-ttu-id="6a872-121">Reference the [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles to determine how many NICS each VM size supports.</span><span class="sxs-lookup"><span data-stu-id="6a872-121">Reference the [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles to determine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="6a872-122">Network Security Groups (NSGs)</span><span class="sxs-lookup"><span data-stu-id="6a872-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="6a872-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span><span class="sxs-lookup"><span data-stu-id="6a872-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="6a872-124">If a NIC is assigned an address within a subnet where the subnet is associated with an NSG, then the rules in the subnet’s NSG also apply to that NIC.</span><span class="sxs-lookup"><span data-stu-id="6a872-124">If a NIC is assigned an address within a subnet where the subnet is associated with an NSG, then the rules in the subnet’s NSG also apply to that NIC.</span></span> <span data-ttu-id="6a872-125">In addition to associating subnets with NSGs, you can also associate a NIC with an NSG.</span><span class="sxs-lookup"><span data-stu-id="6a872-125">In addition to associating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="6a872-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, the associated NSG rules are applied in **flow order** according to the direction of the traffic being passed into or out of the NIC:</span><span class="sxs-lookup"><span data-stu-id="6a872-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, the associated NSG rules are applied in **flow order** according to the direction of the traffic being passed into or out of the NIC:</span></span>

* <span data-ttu-id="6a872-127">**Incoming traffic** whose destination is the NIC in question flows first through the subnet, triggering the subnet’s NSG rules, before passing into the NIC, then triggering the NIC’s NSG rules.</span><span class="sxs-lookup"><span data-stu-id="6a872-127">**Incoming traffic** whose destination is the NIC in question flows first through the subnet, triggering the subnet’s NSG rules, before passing into the NIC, then triggering the NIC’s NSG rules.</span></span>
* <span data-ttu-id="6a872-128">**Outgoing traffic** whose source is the NIC in question flows first out from the NIC, triggering the NIC’s NSG rules, before passing through the subnet, then triggering the subnet’s NSG rules.</span><span class="sxs-lookup"><span data-stu-id="6a872-128">**Outgoing traffic** whose source is the NIC in question flows first out from the NIC, triggering the NIC’s NSG rules, before passing through the subnet, then triggering the subnet’s NSG rules.</span></span>

<span data-ttu-id="6a872-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations to subnets, VMs, and NICs..</span><span class="sxs-lookup"><span data-stu-id="6a872-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations to subnets, VMs, and NICs..</span></span>

## <a name="how-to-configure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="6a872-130">How to Configure a multi NIC VM in a classic deployment</span><span class="sxs-lookup"><span data-stu-id="6a872-130">How to Configure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="6a872-131">The instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span><span class="sxs-lookup"><span data-stu-id="6a872-131">The instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="6a872-132">The configuration steps will create a VM that will be configured according to the service configuration file fragment below:</span><span class="sxs-lookup"><span data-stu-id="6a872-132">The configuration steps will create a VM that will be configured according to the service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over the remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="6a872-133">You need the following prerequisites before trying to run the PowerShell commands in the example.</span><span class="sxs-lookup"><span data-stu-id="6a872-133">You need the following prerequisites before trying to run the PowerShell commands in the example.</span></span>

* <span data-ttu-id="6a872-134">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="6a872-134">An Azure subscription.</span></span>
* <span data-ttu-id="6a872-135">A configured virtual network.</span><span class="sxs-lookup"><span data-stu-id="6a872-135">A configured virtual network.</span></span> <span data-ttu-id="6a872-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span><span class="sxs-lookup"><span data-stu-id="6a872-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="6a872-137">The latest version of Azure PowerShell downloaded and installed.</span><span class="sxs-lookup"><span data-stu-id="6a872-137">The latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="6a872-138">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="6a872-138">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="6a872-139">To create a VM with multiple NICs, complete the following steps by entering each command within a single PowerShell session:</span><span class="sxs-lookup"><span data-stu-id="6a872-139">To create a VM with multiple NICs, complete the following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="6a872-140">Select a VM image from Azure VM image gallery.</span><span class="sxs-lookup"><span data-stu-id="6a872-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="6a872-141">Note that images change frequently and are available by region.</span><span class="sxs-lookup"><span data-stu-id="6a872-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="6a872-142">The image specified in the example below may change or might not be in your region, so be sure to specify the image you need.</span><span class="sxs-lookup"><span data-stu-id="6a872-142">The image specified in the example below may change or might not be in your region, so be sure to specify the image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="6a872-143">Create a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="6a872-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="6a872-144">Create the default administrator login.</span><span class="sxs-lookup"><span data-stu-id="6a872-144">Create the default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="6a872-145">Add additional NICs to the VM configuration.</span><span class="sxs-lookup"><span data-stu-id="6a872-145">Add additional NICs to the VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="6a872-146">Specify the subnet and IP address for the default NIC.</span><span class="sxs-lookup"><span data-stu-id="6a872-146">Specify the subnet and IP address for the default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="6a872-147">Create the VM in your virtual network.</span><span class="sxs-lookup"><span data-stu-id="6a872-147">Create the VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="6a872-148">The VNet that you specify here must already exist (as mentioned in the prerequisites).</span><span class="sxs-lookup"><span data-stu-id="6a872-148">The VNet that you specify here must already exist (as mentioned in the prerequisites).</span></span> <span data-ttu-id="6a872-149">The example below specifies a virtual network named **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="6a872-149">The example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="6a872-150">Limitations</span><span class="sxs-lookup"><span data-stu-id="6a872-150">Limitations</span></span>
<span data-ttu-id="6a872-151">The following limitations are applicable when using multiple NICs:</span><span class="sxs-lookup"><span data-stu-id="6a872-151">The following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="6a872-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span><span class="sxs-lookup"><span data-stu-id="6a872-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="6a872-153">Non-VNet VMs cannot be configured with multiple NICs.</span><span class="sxs-lookup"><span data-stu-id="6a872-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="6a872-154">All VMs in an availability set need to use either multiple NICs or a single NIC.</span><span class="sxs-lookup"><span data-stu-id="6a872-154">All VMs in an availability set need to use either multiple NICs or a single NIC.</span></span> <span data-ttu-id="6a872-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span><span class="sxs-lookup"><span data-stu-id="6a872-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="6a872-156">Same rules apply for VMs in a cloud service.</span><span class="sxs-lookup"><span data-stu-id="6a872-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="6a872-157">For multiple NIC VMs, they aren't required to have the same number of NICs, as long as they each have at least two.</span><span class="sxs-lookup"><span data-stu-id="6a872-157">For multiple NIC VMs, they aren't required to have the same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="6a872-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span><span class="sxs-lookup"><span data-stu-id="6a872-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-to-other-subnets"></a><span data-ttu-id="6a872-159">Secondary NICs access to other subnets</span><span class="sxs-lookup"><span data-stu-id="6a872-159">Secondary NICs access to other subnets</span></span>
<span data-ttu-id="6a872-160">By default secondary NICs will not be configured with a default gateway, due to which the traffic flow on the secondary NICs will be limited to be within the same subnet.</span><span class="sxs-lookup"><span data-stu-id="6a872-160">By default secondary NICs will not be configured with a default gateway, due to which the traffic flow on the secondary NICs will be limited to be within the same subnet.</span></span> <span data-ttu-id="6a872-161">If the users want to enable secondary NICs to talk outside their own subnet, they will need to add an entry in the routing table to configure the gateway as described below.</span><span class="sxs-lookup"><span data-stu-id="6a872-161">If the users want to enable secondary NICs to talk outside their own subnet, they will need to add an entry in the routing table to configure the gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="6a872-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span><span class="sxs-lookup"><span data-stu-id="6a872-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="6a872-163">The default gateway for secondary NICs will not be removed until these VMs are rebooted.</span><span class="sxs-lookup"><span data-stu-id="6a872-163">The default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="6a872-164">In Operating systems that use the weak host routing model, such as Linux, Internet connectivity can break if the ingress and egress traffic use different NICs.</span><span class="sxs-lookup"><span data-stu-id="6a872-164">In Operating systems that use the weak host routing model, such as Linux, Internet connectivity can break if the ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="6a872-165">Configure Windows VMs</span><span class="sxs-lookup"><span data-stu-id="6a872-165">Configure Windows VMs</span></span>
<span data-ttu-id="6a872-166">Suppose that you have a Windows VM with two NICs as follows:</span><span class="sxs-lookup"><span data-stu-id="6a872-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="6a872-167">Primary NIC IP address: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="6a872-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="6a872-168">Secondary NIC IP address: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="6a872-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="6a872-169">The IPv4 route table for this VM would look like this:</span><span class="sxs-lookup"><span data-stu-id="6a872-169">The IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="6a872-170">Notice that the default route (0.0.0.0) is only available to the primary NIC.</span><span class="sxs-lookup"><span data-stu-id="6a872-170">Notice that the default route (0.0.0.0) is only available to the primary NIC.</span></span> <span data-ttu-id="6a872-171">You will not be able to access resources outside the subnet for the secondary NIC, as seen below:</span><span class="sxs-lookup"><span data-stu-id="6a872-171">You will not be able to access resources outside the subnet for the secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="6a872-172">To add a default route on the secondary NIC, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="6a872-172">To add a default route on the secondary NIC, follow the steps below:</span></span>

1. <span data-ttu-id="6a872-173">From a command prompt, run the command below to identify the index number for the secondary NIC:</span><span class="sxs-lookup"><span data-stu-id="6a872-173">From a command prompt, run the command below to identify the index number for the secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="6a872-174">Notice the second entry in the table, with an index of 27 (in this example).</span><span class="sxs-lookup"><span data-stu-id="6a872-174">Notice the second entry in the table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="6a872-175">From the command prompt, run the **route add** command as shown below.</span><span class="sxs-lookup"><span data-stu-id="6a872-175">From the command prompt, run the **route add** command as shown below.</span></span> <span data-ttu-id="6a872-176">In this example, you are specifying 192.168.2.1 as the default gateway for the secondary NIC:</span><span class="sxs-lookup"><span data-stu-id="6a872-176">In this example, you are specifying 192.168.2.1 as the default gateway for the secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="6a872-177">To test connectivity, go back to the command prompt and try to ping a different subnet from the secondary NIC as shown int eh example below:</span><span class="sxs-lookup"><span data-stu-id="6a872-177">To test connectivity, go back to the command prompt and try to ping a different subnet from the secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="6a872-178">You can also check your route table to check the newly added route, as shown below:</span><span class="sxs-lookup"><span data-stu-id="6a872-178">You can also check your route table to check the newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="6a872-179">Configure Linux VMs</span><span class="sxs-lookup"><span data-stu-id="6a872-179">Configure Linux VMs</span></span>
<span data-ttu-id="6a872-180">For Linux VMs, since the default behavior uses weak host routing, we recommend that the secondary NICs are restricted to traffic flows only within the same subnet.</span><span class="sxs-lookup"><span data-stu-id="6a872-180">For Linux VMs, since the default behavior uses weak host routing, we recommend that the secondary NICs are restricted to traffic flows only within the same subnet.</span></span> <span data-ttu-id="6a872-181">However if certain scenarios demand connectivity outside the subnet, users should enable policy based routing to ensure that the ingress and egress traffic uses the same NIC.</span><span class="sxs-lookup"><span data-stu-id="6a872-181">However if certain scenarios demand connectivity outside the subnet, users should enable policy based routing to ensure that the ingress and egress traffic uses the same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a872-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a872-182">Next steps</span></span>
* <span data-ttu-id="6a872-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="6a872-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="6a872-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6a872-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>


