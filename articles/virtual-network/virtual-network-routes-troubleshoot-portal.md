---
title: Troubleshoot routes - Portal | Microsoft Docs
description: Learn how to troubleshoot routes in the Azure Resource Manager deployment model using the Azure Portal.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: ''
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: d129c02b15c22d0b1f246f0047149f45abd0c036
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552250"
---
# <a name="troubleshoot-routes-using-the-azure-portal"></a><span data-ttu-id="74e43-103">Troubleshoot routes using the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="74e43-103">Troubleshoot routes using the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
>
>

<span data-ttu-id="74e43-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span><span class="sxs-lookup"><span data-stu-id="74e43-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="74e43-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span><span class="sxs-lookup"><span data-stu-id="74e43-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="74e43-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span><span class="sxs-lookup"><span data-stu-id="74e43-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="74e43-109">The following types of routes can be applied to each network interface:</span><span class="sxs-lookup"><span data-stu-id="74e43-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="74e43-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="74e43-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="74e43-111">System routes also exist for peered VNets.</span><span class="sxs-lookup"><span data-stu-id="74e43-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="74e43-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span><span class="sxs-lookup"><span data-stu-id="74e43-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="74e43-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span><span class="sxs-lookup"><span data-stu-id="74e43-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="74e43-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span><span class="sxs-lookup"><span data-stu-id="74e43-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="74e43-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span><span class="sxs-lookup"><span data-stu-id="74e43-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="74e43-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span><span class="sxs-lookup"><span data-stu-id="74e43-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="74e43-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="74e43-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="74e43-118">Using Effective Routes to troubleshoot VM traffic flow</span><span class="sxs-lookup"><span data-stu-id="74e43-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="74e43-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span><span class="sxs-lookup"><span data-stu-id="74e43-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="74e43-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="74e43-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="74e43-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span><span class="sxs-lookup"><span data-stu-id="74e43-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="74e43-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span><span class="sxs-lookup"><span data-stu-id="74e43-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="74e43-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span><span class="sxs-lookup"><span data-stu-id="74e43-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="74e43-125">View effective routes for a virtual machine</span><span class="sxs-lookup"><span data-stu-id="74e43-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="74e43-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="74e43-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

1. <span data-ttu-id="74e43-127">Login to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="74e43-127">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="74e43-128">Click **More services**, then click **Virtual machines** in the list that appears.</span><span class="sxs-lookup"><span data-stu-id="74e43-128">Click **More services**, then click **Virtual machines** in the list that appears.</span></span>
3. <span data-ttu-id="74e43-129">Select a VM to troubleshoot from the list that appears and a VM blade with options appears.</span><span class="sxs-lookup"><span data-stu-id="74e43-129">Select a VM to troubleshoot from the list that appears and a VM blade with options appears.</span></span>
4. <span data-ttu-id="74e43-130">Click **Diagnose & solve problems** and then select a common problem.</span><span class="sxs-lookup"><span data-stu-id="74e43-130">Click **Diagnose & solve problems** and then select a common problem.</span></span> <span data-ttu-id="74e43-131">For this example, **I can’t connect to my Windows VM** is selected.</span><span class="sxs-lookup"><span data-stu-id="74e43-131">For this example, **I can’t connect to my Windows VM** is selected.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image1.png)
5. <span data-ttu-id="74e43-132">Steps appear under the problem, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="74e43-132">Steps appear under the problem, as shown in the following picture:</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image2.png)

    <span data-ttu-id="74e43-133">Click *effective routes* in the list of recommended steps.</span><span class="sxs-lookup"><span data-stu-id="74e43-133">Click *effective routes* in the list of recommended steps.</span></span>
6. <span data-ttu-id="74e43-134">The **Effective routes** blade appears, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="74e43-134">The **Effective routes** blade appears, as shown in the following picture:</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image3.png)

    <span data-ttu-id="74e43-135">If your VM has only one NIC, it is selected by default.</span><span class="sxs-lookup"><span data-stu-id="74e43-135">If your VM has only one NIC, it is selected by default.</span></span> <span data-ttu-id="74e43-136">If you have more than one NIC, select the NIC for which you want to view the effective routes.</span><span class="sxs-lookup"><span data-stu-id="74e43-136">If you have more than one NIC, select the NIC for which you want to view the effective routes.</span></span>

   > [!NOTE]
   > If the VM associated with the NIC is not in a running state, effective routes will not be shown. Only the first 200 effective routes are shown in the portal. For the full list, click **Download**. You can further filter on the results from the downloaded .csv file.
   >
   >

    <span data-ttu-id="74e43-141">Notice the following in the output:</span><span class="sxs-lookup"><span data-stu-id="74e43-141">Notice the following in the output:</span></span>

   * <span data-ttu-id="74e43-142">**Source**: Indicates the type of route.</span><span class="sxs-lookup"><span data-stu-id="74e43-142">**Source**: Indicates the type of route.</span></span> <span data-ttu-id="74e43-143">System routes are shown as *Default*, UDRs are shown as *User* and gateway routes (static or BGP) are shown as *VPNGateway*.</span><span class="sxs-lookup"><span data-stu-id="74e43-143">System routes are shown as *Default*, UDRs are shown as *User* and gateway routes (static or BGP) are shown as *VPNGateway*.</span></span>
   * <span data-ttu-id="74e43-144">**State**: Indicates state of the effective route.</span><span class="sxs-lookup"><span data-stu-id="74e43-144">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="74e43-145">Possible values are *Active* or *Invalid*.</span><span class="sxs-lookup"><span data-stu-id="74e43-145">Possible values are *Active* or *Invalid*.</span></span>
   * <span data-ttu-id="74e43-146">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span><span class="sxs-lookup"><span data-stu-id="74e43-146">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span>
   * <span data-ttu-id="74e43-147">**nextHopType**: Indicates the next hop for the given route.</span><span class="sxs-lookup"><span data-stu-id="74e43-147">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="74e43-148">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span><span class="sxs-lookup"><span data-stu-id="74e43-148">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="74e43-149">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span><span class="sxs-lookup"><span data-stu-id="74e43-149">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="74e43-150">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span><span class="sxs-lookup"><span data-stu-id="74e43-150">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="74e43-151">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span><span class="sxs-lookup"><span data-stu-id="74e43-151">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
7. <span data-ttu-id="74e43-152">There is no route listed to the *WestUS-VNET3* VNet (Prefix 10.10.0.0/16) from the *WestUS-VNet1* (Prefix 10.9.0.0/16) in the picture in the previous step.</span><span class="sxs-lookup"><span data-stu-id="74e43-152">There is no route listed to the *WestUS-VNET3* VNet (Prefix 10.10.0.0/16) from the *WestUS-VNet1* (Prefix 10.9.0.0/16) in the picture in the previous step.</span></span> <span data-ttu-id="74e43-153">In the following picture, the peering link is in the *Disconnected* state:</span><span class="sxs-lookup"><span data-stu-id="74e43-153">In the following picture, the peering link is in the *Disconnected* state:</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image4.png)

    <span data-ttu-id="74e43-154">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span><span class="sxs-lookup"><span data-stu-id="74e43-154">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span>
8. <span data-ttu-id="74e43-155">The following picture shows the routes after establishing the bi-directional peering link:</span><span class="sxs-lookup"><span data-stu-id="74e43-155">The following picture shows the routes after establishing the bi-directional peering link:</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image5.png)

<span data-ttu-id="74e43-156">For more troubleshooting scenarios for forced-tunneling and route evaluation, read the [Considerations](virtual-network-routes-troubleshoot-portal.md#considerations) section of this article.</span><span class="sxs-lookup"><span data-stu-id="74e43-156">For more troubleshooting scenarios for forced-tunneling and route evaluation, read the [Considerations](virtual-network-routes-troubleshoot-portal.md#considerations) section of this article.</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="74e43-157">View effective routes for a network interface</span><span class="sxs-lookup"><span data-stu-id="74e43-157">View effective routes for a network interface</span></span>
<span data-ttu-id="74e43-158">If network traffic flow is impacted for a particular network interface (NIC), you can view a full list of effective routes on a NIC directly.</span><span class="sxs-lookup"><span data-stu-id="74e43-158">If network traffic flow is impacted for a particular network interface (NIC), you can view a full list of effective routes on a NIC directly.</span></span> <span data-ttu-id="74e43-159">To see the aggregate routes that are applied to a NIC, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="74e43-159">To see the aggregate routes that are applied to a NIC, complete the following steps:</span></span>

1. <span data-ttu-id="74e43-160">Login to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="74e43-160">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="74e43-161">Click **More services**, then click **Network interfaces**</span><span class="sxs-lookup"><span data-stu-id="74e43-161">Click **More services**, then click **Network interfaces**</span></span>
3. <span data-ttu-id="74e43-162">Search the list for the name of a NIC, or select it from the list that appears.</span><span class="sxs-lookup"><span data-stu-id="74e43-162">Search the list for the name of a NIC, or select it from the list that appears.</span></span> <span data-ttu-id="74e43-163">In this example, **VM1-NIC1** is selected.</span><span class="sxs-lookup"><span data-stu-id="74e43-163">In this example, **VM1-NIC1** is selected.</span></span>
4. <span data-ttu-id="74e43-164">Select **Effective routes** in the **Network interface** blade, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="74e43-164">Select **Effective routes** in the **Network interface** blade, as shown in the following picture:</span></span>

       ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image6.png)

    <span data-ttu-id="74e43-165">The **Scope** defaults to the network interface selected.</span><span class="sxs-lookup"><span data-stu-id="74e43-165">The **Scope** defaults to the network interface selected.</span></span>

      ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a><span data-ttu-id="74e43-166">View effective routes for a route table</span><span class="sxs-lookup"><span data-stu-id="74e43-166">View effective routes for a route table</span></span>
<span data-ttu-id="74e43-167">When modifying user-defined routes (UDRs) in a route table, you may want to review the impact of the routes being added on a particular VM.</span><span class="sxs-lookup"><span data-stu-id="74e43-167">When modifying user-defined routes (UDRs) in a route table, you may want to review the impact of the routes being added on a particular VM.</span></span> <span data-ttu-id="74e43-168">A route table can be associated with any number of subnets.</span><span class="sxs-lookup"><span data-stu-id="74e43-168">A route table can be associated with any number of subnets.</span></span> <span data-ttu-id="74e43-169">You can now view all the effective routes for all the NICs that a given route table is applied to, without having to switch context from the given route table blade.</span><span class="sxs-lookup"><span data-stu-id="74e43-169">You can now view all the effective routes for all the NICs that a given route table is applied to, without having to switch context from the given route table blade.</span></span>

<span data-ttu-id="74e43-170">For this example, a UDR (*UDRoute*) is specified in a route table (*UDRouteTable*).</span><span class="sxs-lookup"><span data-stu-id="74e43-170">For this example, a UDR (*UDRoute*) is specified in a route table (*UDRouteTable*).</span></span> <span data-ttu-id="74e43-171">This route sends all Internet traffic from *Subnet1* in the *WestUS-VNet1* VNet, through a network virtual appliance (NVA), in *Subnet2* of the same VNet.</span><span class="sxs-lookup"><span data-stu-id="74e43-171">This route sends all Internet traffic from *Subnet1* in the *WestUS-VNet1* VNet, through a network virtual appliance (NVA), in *Subnet2* of the same VNet.</span></span> <span data-ttu-id="74e43-172">The route is shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="74e43-172">The route is shown in the following picture:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image8.png)

<span data-ttu-id="74e43-173">To see the aggregate routes for a route table, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="74e43-173">To see the aggregate routes for a route table, complete the following steps:</span></span>

1. <span data-ttu-id="74e43-174">Login to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="74e43-174">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="74e43-175">Click **More services**, then click **Route tables**</span><span class="sxs-lookup"><span data-stu-id="74e43-175">Click **More services**, then click **Route tables**</span></span>
3. <span data-ttu-id="74e43-176">Search the list for the route table you want to see aggregate routes for and select it.</span><span class="sxs-lookup"><span data-stu-id="74e43-176">Search the list for the route table you want to see aggregate routes for and select it.</span></span> <span data-ttu-id="74e43-177">In this example, **UDRouteTable** is selected.</span><span class="sxs-lookup"><span data-stu-id="74e43-177">In this example, **UDRouteTable** is selected.</span></span> <span data-ttu-id="74e43-178">A blade for the selected route table appears, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="74e43-178">A blade for the selected route table appears, as shown in the following picture:</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image9.png)
4. <span data-ttu-id="74e43-179">Select **Effective Routes** in the **Route table** blade.</span><span class="sxs-lookup"><span data-stu-id="74e43-179">Select **Effective Routes** in the **Route table** blade.</span></span> <span data-ttu-id="74e43-180">The **Scope** is set to the route table you selected.</span><span class="sxs-lookup"><span data-stu-id="74e43-180">The **Scope** is set to the route table you selected.</span></span>
5. <span data-ttu-id="74e43-181">A route table can be applied to multiple subnets.</span><span class="sxs-lookup"><span data-stu-id="74e43-181">A route table can be applied to multiple subnets.</span></span> <span data-ttu-id="74e43-182">Select the **Subnet** you want to review from the list.</span><span class="sxs-lookup"><span data-stu-id="74e43-182">Select the **Subnet** you want to review from the list.</span></span> <span data-ttu-id="74e43-183">In this example, **Subnet1** is selected.</span><span class="sxs-lookup"><span data-stu-id="74e43-183">In this example, **Subnet1** is selected.</span></span>
6. <span data-ttu-id="74e43-184">Select a **Network Interface**.</span><span class="sxs-lookup"><span data-stu-id="74e43-184">Select a **Network Interface**.</span></span> <span data-ttu-id="74e43-185">All NICs connected to the selected subnet are listed.</span><span class="sxs-lookup"><span data-stu-id="74e43-185">All NICs connected to the selected subnet are listed.</span></span> <span data-ttu-id="74e43-186">In this example, **VM1-NIC1** is selected.</span><span class="sxs-lookup"><span data-stu-id="74e43-186">In this example, **VM1-NIC1** is selected.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-network/media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > If the NIC is not associated with a running VM, no effective routes are shown.
   >
   >

## <a name="considerations"></a><span data-ttu-id="74e43-188">Considerations</span><span class="sxs-lookup"><span data-stu-id="74e43-188">Considerations</span></span>
<span data-ttu-id="74e43-189">A few things to keep in mind when reviewing the list of routes returned:</span><span class="sxs-lookup"><span data-stu-id="74e43-189">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="74e43-190">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span><span class="sxs-lookup"><span data-stu-id="74e43-190">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="74e43-191">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span><span class="sxs-lookup"><span data-stu-id="74e43-191">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>

  * <span data-ttu-id="74e43-192">User-defined route</span><span class="sxs-lookup"><span data-stu-id="74e43-192">User-defined route</span></span>
  * <span data-ttu-id="74e43-193">BGP route</span><span class="sxs-lookup"><span data-stu-id="74e43-193">BGP route</span></span>
  * <span data-ttu-id="74e43-194">System (Default) route</span><span class="sxs-lookup"><span data-stu-id="74e43-194">System (Default) route</span></span>

    <span data-ttu-id="74e43-195">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span><span class="sxs-lookup"><span data-stu-id="74e43-195">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="74e43-196">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span><span class="sxs-lookup"><span data-stu-id="74e43-196">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="74e43-197">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span><span class="sxs-lookup"><span data-stu-id="74e43-197">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span>
* <span data-ttu-id="74e43-198">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span><span class="sxs-lookup"><span data-stu-id="74e43-198">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="74e43-199">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span><span class="sxs-lookup"><span data-stu-id="74e43-199">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span>
  <span data-ttu-id="74e43-200">Forced-tunneling can be enabled:</span><span class="sxs-lookup"><span data-stu-id="74e43-200">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="74e43-201">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="74e43-201">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="74e43-202">If a default route is advertised over BGP</span><span class="sxs-lookup"><span data-stu-id="74e43-202">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="74e43-203">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span><span class="sxs-lookup"><span data-stu-id="74e43-203">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="74e43-204">If such a route doesn’t exist and the VNet peering link looks OK:</span><span class="sxs-lookup"><span data-stu-id="74e43-204">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="74e43-205">Wait a few seconds and retry if it's a newly established peering link.</span><span class="sxs-lookup"><span data-stu-id="74e43-205">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="74e43-206">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span><span class="sxs-lookup"><span data-stu-id="74e43-206">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="74e43-207">Network Security Group (NSG) rules may be impacting the traffic flows.</span><span class="sxs-lookup"><span data-stu-id="74e43-207">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="74e43-208">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-portal.md) article.</span><span class="sxs-lookup"><span data-stu-id="74e43-208">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-portal.md) article.</span></span>










