---
title: 'Configure ExpressRoute and Site-to-Site VPN connections that can coexist: classic: Azure | Microsoft Docs'
description: This article walks you through configuring ExpressRoute and a Site-to-Site VPN connection that can coexist for the classic deployment model.
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: ''
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 380eb2b21db3a64175bb01ed7bdcd8819f4cc359
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669743"
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="8cf95-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span><span class="sxs-lookup"><span data-stu-id="8cf95-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Classic](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="8cf95-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span><span class="sxs-lookup"><span data-stu-id="8cf95-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="8cf95-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8cf95-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="8cf95-108">We will cover the steps to configure both scenarios in this article.</span><span class="sxs-lookup"><span data-stu-id="8cf95-108">We will cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="8cf95-109">This article applies to the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="8cf95-109">This article applies to the classic deployment model.</span></span> <span data-ttu-id="8cf95-110">This configuration is not available in the portal.</span><span class="sxs-lookup"><span data-stu-id="8cf95-110">This configuration is not available in the portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="8cf95-111">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="8cf95-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> ExpressRoute circuits must be pre-configured before you follow the instructions below. Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow the steps below.
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="8cf95-114">Limits and limitations</span><span class="sxs-lookup"><span data-stu-id="8cf95-114">Limits and limitations</span></span>
* <span data-ttu-id="8cf95-115">**Transit routing is not supported.**</span><span class="sxs-lookup"><span data-stu-id="8cf95-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="8cf95-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8cf95-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="8cf95-117">**Point-to-site is not supported.**</span><span class="sxs-lookup"><span data-stu-id="8cf95-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="8cf95-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8cf95-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span></span> <span data-ttu-id="8cf95-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span><span class="sxs-lookup"><span data-stu-id="8cf95-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span></span>
* <span data-ttu-id="8cf95-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span><span class="sxs-lookup"><span data-stu-id="8cf95-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="8cf95-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8cf95-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="8cf95-122">**Basic SKU gateway is not supported.**</span><span class="sxs-lookup"><span data-stu-id="8cf95-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="8cf95-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="8cf95-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8cf95-124">**Only route-based VPN gateway is supported.**</span><span class="sxs-lookup"><span data-stu-id="8cf95-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="8cf95-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="8cf95-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8cf95-126">**Static route should be configured for your VPN gateway.**</span><span class="sxs-lookup"><span data-stu-id="8cf95-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="8cf95-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span><span class="sxs-lookup"><span data-stu-id="8cf95-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="8cf95-128">**ExpressRoute gateway must be configured first.**</span><span class="sxs-lookup"><span data-stu-id="8cf95-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="8cf95-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="8cf95-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="8cf95-130">Configuration designs</span><span class="sxs-lookup"><span data-stu-id="8cf95-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="8cf95-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8cf95-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="8cf95-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8cf95-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="8cf95-133">This applies only to virtual networks linked to the Azure private peering path.</span><span class="sxs-lookup"><span data-stu-id="8cf95-133">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="8cf95-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span><span class="sxs-lookup"><span data-stu-id="8cf95-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="8cf95-135">The ExpressRoute circuit is always the primary link.</span><span class="sxs-lookup"><span data-stu-id="8cf95-135">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="8cf95-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span><span class="sxs-lookup"><span data-stu-id="8cf95-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span> 

![Coexist](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="8cf95-138">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8cf95-138">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="8cf95-139">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8cf95-139">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexist](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> You cannot a configure a virtual network as a transit router.
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="8cf95-142">Selecting the steps to use</span><span class="sxs-lookup"><span data-stu-id="8cf95-142">Selecting the steps to use</span></span>
<span data-ttu-id="8cf95-143">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span><span class="sxs-lookup"><span data-stu-id="8cf95-143">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span></span> <span data-ttu-id="8cf95-144">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span><span class="sxs-lookup"><span data-stu-id="8cf95-144">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="8cf95-145">I don't have a VNet and need to create one.</span><span class="sxs-lookup"><span data-stu-id="8cf95-145">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="8cf95-146">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span><span class="sxs-lookup"><span data-stu-id="8cf95-146">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="8cf95-147">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span><span class="sxs-lookup"><span data-stu-id="8cf95-147">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="8cf95-148">I already have a classic deployment model VNet.</span><span class="sxs-lookup"><span data-stu-id="8cf95-148">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="8cf95-149">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span><span class="sxs-lookup"><span data-stu-id="8cf95-149">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="8cf95-150">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span><span class="sxs-lookup"><span data-stu-id="8cf95-150">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="8cf95-151">Note that when creating the new connections, the steps must be completed in a very specific order.</span><span class="sxs-lookup"><span data-stu-id="8cf95-151">Note that when creating the new connections, the steps must be completed in a very specific order.</span></span> <span data-ttu-id="8cf95-152">Don't use the instructions in other articles to create your gateways and connections.</span><span class="sxs-lookup"><span data-stu-id="8cf95-152">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="8cf95-153">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span><span class="sxs-lookup"><span data-stu-id="8cf95-153">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="8cf95-154">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span><span class="sxs-lookup"><span data-stu-id="8cf95-154">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="8cf95-155">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span><span class="sxs-lookup"><span data-stu-id="8cf95-155">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <a name="new"></a><span data-ttu-id="8cf95-156">To create a new virtual network and coexisting connections</span><span class="sxs-lookup"><span data-stu-id="8cf95-156">To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="8cf95-157">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span><span class="sxs-lookup"><span data-stu-id="8cf95-157">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="8cf95-158">You'll need to install the latest version of the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8cf95-158">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8cf95-159">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8cf95-159">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="8cf95-160">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span><span class="sxs-lookup"><span data-stu-id="8cf95-160">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="8cf95-161">Be sure to use the cmdlets specified in these instructions.</span><span class="sxs-lookup"><span data-stu-id="8cf95-161">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="8cf95-162">Create a schema for your virtual network.</span><span class="sxs-lookup"><span data-stu-id="8cf95-162">Create a schema for your virtual network.</span></span> <span data-ttu-id="8cf95-163">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="8cf95-163">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="8cf95-164">When you create your schema, make sure you use the following values:</span><span class="sxs-lookup"><span data-stu-id="8cf95-164">When you create your schema, make sure you use the following values:</span></span>
   
   * <span data-ttu-id="8cf95-165">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span><span class="sxs-lookup"><span data-stu-id="8cf95-165">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="8cf95-166">The gateway connection type is "Dedicated".</span><span class="sxs-lookup"><span data-stu-id="8cf95-166">The gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="8cf95-167">After creating and configuring your xml schema file, upload the file.</span><span class="sxs-lookup"><span data-stu-id="8cf95-167">After creating and configuring your xml schema file, upload the file.</span></span> <span data-ttu-id="8cf95-168">This will create your virtual network.</span><span class="sxs-lookup"><span data-stu-id="8cf95-168">This will create your virtual network.</span></span>
   
    <span data-ttu-id="8cf95-169">Use the following cmdlet to upload your file, replacing the value with your own.</span><span class="sxs-lookup"><span data-stu-id="8cf95-169">Use the following cmdlet to upload your file, replacing the value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a><span data-ttu-id="8cf95-170">Create an ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="8cf95-170">Create an ExpressRoute gateway.</span></span> <span data-ttu-id="8cf95-171">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="8cf95-171">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="8cf95-172">Use the following sample, substituting the values for your own.</span><span class="sxs-lookup"><span data-stu-id="8cf95-172">Use the following sample, substituting the values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="8cf95-173">Link the ExpressRoute gateway to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="8cf95-173">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="8cf95-174">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span><span class="sxs-lookup"><span data-stu-id="8cf95-174">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a><span data-ttu-id="8cf95-175">Next, create your Site-to-Site VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="8cf95-175">Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="8cf95-176">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="8cf95-176">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="8cf95-177">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8cf95-177">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for the following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="8cf95-178">Create a local site VPN gateway entity.</span><span class="sxs-lookup"><span data-stu-id="8cf95-178">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="8cf95-179">This command doesn’t configure your on-premises VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="8cf95-179">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="8cf95-180">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span><span class="sxs-lookup"><span data-stu-id="8cf95-180">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
   > [!IMPORTANT]
   > The local site for the Site-to-Site VPN is not defined in the netcfg. Instead, you must use this cmdlet to specify the local site parameters. You cannot define it using either portal, or the netcfg file.
   > 
   > 
   
    <span data-ttu-id="8cf95-184">Use the following sample, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="8cf95-184">Use the following sample, replacing the values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > If your local network has multiple routes, you can pass them all in as an array.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    <span data-ttu-id="8cf95-187">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8cf95-187">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="8cf95-188">See the following example.</span><span class="sxs-lookup"><span data-stu-id="8cf95-188">See the following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="8cf95-189">Configure your local VPN device to connect to the new gateway.</span><span class="sxs-lookup"><span data-stu-id="8cf95-189">Configure your local VPN device to connect to the new gateway.</span></span> <span data-ttu-id="8cf95-190">Use the information that you retrieved in step 6 when configuring your VPN device.</span><span class="sxs-lookup"><span data-stu-id="8cf95-190">Use the information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="8cf95-191">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="8cf95-191">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="8cf95-192">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span><span class="sxs-lookup"><span data-stu-id="8cf95-192">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>
   
    <span data-ttu-id="8cf95-193">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="8cf95-193">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="8cf95-194">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8cf95-194">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="8cf95-195">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span><span class="sxs-lookup"><span data-stu-id="8cf95-195">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a><span data-ttu-id="8cf95-196">To configure coexsiting connections for an already existing VNet</span><span class="sxs-lookup"><span data-stu-id="8cf95-196">To configure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="8cf95-197">If you have an existing virtual network, check the gateway subnet size.</span><span class="sxs-lookup"><span data-stu-id="8cf95-197">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="8cf95-198">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span><span class="sxs-lookup"><span data-stu-id="8cf95-198">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="8cf95-199">The steps in this section will show you how to do that.</span><span class="sxs-lookup"><span data-stu-id="8cf95-199">The steps in this section will show you how to do that.</span></span>

<span data-ttu-id="8cf95-200">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span><span class="sxs-lookup"><span data-stu-id="8cf95-200">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span>

> [!NOTE]
> When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.
> 
> 

1. <span data-ttu-id="8cf95-202">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8cf95-202">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="8cf95-203">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8cf95-203">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="8cf95-204">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span><span class="sxs-lookup"><span data-stu-id="8cf95-204">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="8cf95-205">Be sure to use the cmdlets specified in these instructions.</span><span class="sxs-lookup"><span data-stu-id="8cf95-205">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="8cf95-206">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="8cf95-206">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="8cf95-207">Use the following cmdlet, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="8cf95-207">Use the following cmdlet, replacing the values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="8cf95-208">Export the virtual network schema.</span><span class="sxs-lookup"><span data-stu-id="8cf95-208">Export the virtual network schema.</span></span> <span data-ttu-id="8cf95-209">Use the following PowerShell cmdlet, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="8cf95-209">Use the following PowerShell cmdlet, replacing the values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="8cf95-210">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span><span class="sxs-lookup"><span data-stu-id="8cf95-210">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="8cf95-211">See the following example.</span><span class="sxs-lookup"><span data-stu-id="8cf95-211">See the following example.</span></span> 
   
   > [!NOTE]
   > If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space. For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="8cf95-214">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span><span class="sxs-lookup"><span data-stu-id="8cf95-214">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="8cf95-215">At this point, you'll have a VNet with no gateways.</span><span class="sxs-lookup"><span data-stu-id="8cf95-215">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="8cf95-216">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span><span class="sxs-lookup"><span data-stu-id="8cf95-216">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cf95-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="8cf95-217">Next steps</span></span>
<span data-ttu-id="8cf95-218">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="8cf95-218">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span></span>



