---
title: Troubleshoot routes - PowerShell | Microsoft Docs
description: Learn how to troubleshoot routes in the Azure Resource Manager deployment model using Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: ''
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 943417181c7379c7ed2eb8766e7c6a2d9e95330b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556380"
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="452aa-103">Troubleshoot routes using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="452aa-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="452aa-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span><span class="sxs-lookup"><span data-stu-id="452aa-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="452aa-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span><span class="sxs-lookup"><span data-stu-id="452aa-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="452aa-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span><span class="sxs-lookup"><span data-stu-id="452aa-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="452aa-109">The following types of routes can be applied to each network interface:</span><span class="sxs-lookup"><span data-stu-id="452aa-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="452aa-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="452aa-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="452aa-111">System routes also exist for peered VNets.</span><span class="sxs-lookup"><span data-stu-id="452aa-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="452aa-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span><span class="sxs-lookup"><span data-stu-id="452aa-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="452aa-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span><span class="sxs-lookup"><span data-stu-id="452aa-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="452aa-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span><span class="sxs-lookup"><span data-stu-id="452aa-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="452aa-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span><span class="sxs-lookup"><span data-stu-id="452aa-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="452aa-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span><span class="sxs-lookup"><span data-stu-id="452aa-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="452aa-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="452aa-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="452aa-118">Using Effective Routes to troubleshoot VM traffic flow</span><span class="sxs-lookup"><span data-stu-id="452aa-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="452aa-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span><span class="sxs-lookup"><span data-stu-id="452aa-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="452aa-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="452aa-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="452aa-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span><span class="sxs-lookup"><span data-stu-id="452aa-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="452aa-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span><span class="sxs-lookup"><span data-stu-id="452aa-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="452aa-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span><span class="sxs-lookup"><span data-stu-id="452aa-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="452aa-125">View effective routes for a virtual machine</span><span class="sxs-lookup"><span data-stu-id="452aa-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="452aa-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="452aa-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="452aa-127">View effective routes for a network interface</span><span class="sxs-lookup"><span data-stu-id="452aa-127">View effective routes for a network interface</span></span>
<span data-ttu-id="452aa-128">To see the aggregate routes that are applied to a network interface, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="452aa-128">To see the aggregate routes that are applied to a network interface, complete the following steps:</span></span>

1. <span data-ttu-id="452aa-129">Start an Azure PowerShell session and login to Azure.</span><span class="sxs-lookup"><span data-stu-id="452aa-129">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="452aa-130">If you’re not familiar with Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span><span class="sxs-lookup"><span data-stu-id="452aa-130">If you’re not familiar with Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article.</span></span>
2. <span data-ttu-id="452aa-131">The following command returns all routes applied to a network interface named *VM1-NIC1* in the resource group *RG1*.</span><span class="sxs-lookup"><span data-stu-id="452aa-131">The following command returns all routes applied to a network interface named *VM1-NIC1* in the resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > If you don’t know the name of a network interface, type the following command to retrieve the names of all network interfaces in a resource group.*
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="452aa-133">The following output looks similar to the output for each route applied to the subnet the NIC is connected to:</span><span class="sxs-lookup"><span data-stu-id="452aa-133">The following output looks similar to the output for each route applied to the subnet the NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="452aa-134">Notice the following in the output:</span><span class="sxs-lookup"><span data-stu-id="452aa-134">Notice the following in the output:</span></span>
   
   * <span data-ttu-id="452aa-135">**Name**: Name of the effective route may be empty, unless explicitly specified, for user-defined routes.</span><span class="sxs-lookup"><span data-stu-id="452aa-135">**Name**: Name of the effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="452aa-136">**State**: Indicates state of the effective route.</span><span class="sxs-lookup"><span data-stu-id="452aa-136">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="452aa-137">Possible values are "Active" or "Invalid"</span><span class="sxs-lookup"><span data-stu-id="452aa-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="452aa-138">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span><span class="sxs-lookup"><span data-stu-id="452aa-138">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="452aa-139">**nextHopType**: Indicates the next hop for the given route.</span><span class="sxs-lookup"><span data-stu-id="452aa-139">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="452aa-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span><span class="sxs-lookup"><span data-stu-id="452aa-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="452aa-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span><span class="sxs-lookup"><span data-stu-id="452aa-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="452aa-142">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span><span class="sxs-lookup"><span data-stu-id="452aa-142">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="452aa-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span><span class="sxs-lookup"><span data-stu-id="452aa-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
   * <span data-ttu-id="452aa-144">**NextHopIpAddress**: Specifies the IP address of the next hop of the effective route.</span><span class="sxs-lookup"><span data-stu-id="452aa-144">**NextHopIpAddress**: Specifies the IP address of the next hop of the effective route.</span></span>
   
   <span data-ttu-id="452aa-145">The following command returns the routes in an easier to view table:</span><span class="sxs-lookup"><span data-stu-id="452aa-145">The following command returns the routes in an easier to view table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="452aa-146">The following output is some of the output received for the scenario described previously:</span><span class="sxs-lookup"><span data-stu-id="452aa-146">The following output is some of the output received for the scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="452aa-147">There is no route listed to the *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)\*\* from *WestUS-VNet1* (Prefix 10.9.0.0/16) in the output from the previous step.</span><span class="sxs-lookup"><span data-stu-id="452aa-147">There is no route listed to the *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)\*\* from *WestUS-VNet1* (Prefix 10.9.0.0/16) in the output from the previous step.</span></span> <span data-ttu-id="452aa-148">As shown in the following picture, the VNet peering link with the *WestUS-VNet3* VNet is in the *Disconnected* state.</span><span class="sxs-lookup"><span data-stu-id="452aa-148">As shown in the following picture, the VNet peering link with the *WestUS-VNet3* VNet is in the *Disconnected* state.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="452aa-149">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span><span class="sxs-lookup"><span data-stu-id="452aa-149">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="452aa-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span><span class="sxs-lookup"><span data-stu-id="452aa-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="452aa-151">The output returned after the VNet peering link is correctly established follows:</span><span class="sxs-lookup"><span data-stu-id="452aa-151">The output returned after the VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="452aa-152">Once you determine the issue, you can add, remove, or change routes and route tables.</span><span class="sxs-lookup"><span data-stu-id="452aa-152">Once you determine the issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="452aa-153">Type the following command to see a list of the commands used to do so:</span><span class="sxs-lookup"><span data-stu-id="452aa-153">Type the following command to see a list of the commands used to do so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="452aa-154">Considerations</span><span class="sxs-lookup"><span data-stu-id="452aa-154">Considerations</span></span>
<span data-ttu-id="452aa-155">A few things to keep in mind when reviewing the list of routes returned:</span><span class="sxs-lookup"><span data-stu-id="452aa-155">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="452aa-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span><span class="sxs-lookup"><span data-stu-id="452aa-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="452aa-157">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span><span class="sxs-lookup"><span data-stu-id="452aa-157">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>
  
  * <span data-ttu-id="452aa-158">User-defined route</span><span class="sxs-lookup"><span data-stu-id="452aa-158">User-defined route</span></span>
  * <span data-ttu-id="452aa-159">BGP route</span><span class="sxs-lookup"><span data-stu-id="452aa-159">BGP route</span></span>
  * <span data-ttu-id="452aa-160">System (Default) route</span><span class="sxs-lookup"><span data-stu-id="452aa-160">System (Default) route</span></span>
    
    <span data-ttu-id="452aa-161">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span><span class="sxs-lookup"><span data-stu-id="452aa-161">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="452aa-162">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span><span class="sxs-lookup"><span data-stu-id="452aa-162">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="452aa-163">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span><span class="sxs-lookup"><span data-stu-id="452aa-163">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span> 
* <span data-ttu-id="452aa-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span><span class="sxs-lookup"><span data-stu-id="452aa-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="452aa-165">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span><span class="sxs-lookup"><span data-stu-id="452aa-165">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span> 
  <span data-ttu-id="452aa-166">Forced-tunneling can be enabled:</span><span class="sxs-lookup"><span data-stu-id="452aa-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="452aa-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="452aa-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="452aa-168">If a default route is advertised over BGP</span><span class="sxs-lookup"><span data-stu-id="452aa-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="452aa-169">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span><span class="sxs-lookup"><span data-stu-id="452aa-169">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="452aa-170">If such a route doesn’t exist and the VNet peering link looks OK:</span><span class="sxs-lookup"><span data-stu-id="452aa-170">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="452aa-171">Wait a few seconds and retry if it's a newly established peering link.</span><span class="sxs-lookup"><span data-stu-id="452aa-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="452aa-172">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span><span class="sxs-lookup"><span data-stu-id="452aa-172">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="452aa-173">Network Security Group (NSG) rules may be impacting the traffic flows.</span><span class="sxs-lookup"><span data-stu-id="452aa-173">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="452aa-174">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span><span class="sxs-lookup"><span data-stu-id="452aa-174">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>


