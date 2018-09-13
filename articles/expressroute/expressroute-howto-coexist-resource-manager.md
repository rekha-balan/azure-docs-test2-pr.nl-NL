---
title: 'Configure ExpressRoute and Site-to-Site VPN connections that can coexist: Resource Manager: Azure | Microsoft Docs'
description: This article walks you through configuring ExpressRoute and a Site-to-Site VPN connection that can coexist for Resource Manager model.
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: 32d670d18ea5d6e6c10087802ffe19336b10ef27
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555829"
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="70556-103">Configure ExpressRoute and Site-to-Site coexisting connections</span><span class="sxs-lookup"><span data-stu-id="70556-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Classic](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="70556-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span><span class="sxs-lookup"><span data-stu-id="70556-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="70556-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="70556-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="70556-108">We cover the steps to configure both scenarios in this article.</span><span class="sxs-lookup"><span data-stu-id="70556-108">We cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="70556-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70556-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="70556-110">This configuration is not available in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="70556-110">This configuration is not available in the Azure portal.</span></span>

> [!IMPORTANT]
> ExpressRoute circuits must be pre-configured before you follow the instructions below. Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you follow proceed.
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="70556-113">Limits and limitations</span><span class="sxs-lookup"><span data-stu-id="70556-113">Limits and limitations</span></span>
* <span data-ttu-id="70556-114">**Transit routing is not supported.**</span><span class="sxs-lookup"><span data-stu-id="70556-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="70556-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="70556-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="70556-116">**Basic SKU gateway is not supported.**</span><span class="sxs-lookup"><span data-stu-id="70556-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="70556-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="70556-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="70556-118">**Only route-based VPN gateway is supported.**</span><span class="sxs-lookup"><span data-stu-id="70556-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="70556-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="70556-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="70556-120">**Static route should be configured for your VPN gateway.**</span><span class="sxs-lookup"><span data-stu-id="70556-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="70556-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span><span class="sxs-lookup"><span data-stu-id="70556-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="70556-122">**ExpressRoute gateway must be configured first.**</span><span class="sxs-lookup"><span data-stu-id="70556-122">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="70556-123">You must create the ExpressRoute gateway first, before you add the Site-to-Site VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-123">You must create the ExpressRoute gateway first, before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="70556-124">Configuration designs</span><span class="sxs-lookup"><span data-stu-id="70556-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="70556-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="70556-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="70556-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="70556-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="70556-127">This applies only to virtual networks linked to the Azure private peering path.</span><span class="sxs-lookup"><span data-stu-id="70556-127">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="70556-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span><span class="sxs-lookup"><span data-stu-id="70556-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="70556-129">The ExpressRoute circuit is always the primary link.</span><span class="sxs-lookup"><span data-stu-id="70556-129">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="70556-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span><span class="sxs-lookup"><span data-stu-id="70556-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span>

> [!NOTE]
> While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.
> 
> 

![Coexist](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="70556-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="70556-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="70556-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="70556-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexist](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> You cannot configure a virtual network as a transit router.
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="70556-137">Selecting the steps to use</span><span class="sxs-lookup"><span data-stu-id="70556-137">Selecting the steps to use</span></span>
<span data-ttu-id="70556-138">There are two different sets of procedures to choose from.</span><span class="sxs-lookup"><span data-stu-id="70556-138">There are two different sets of procedures to choose from.</span></span> <span data-ttu-id="70556-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span><span class="sxs-lookup"><span data-stu-id="70556-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="70556-140">I don't have a VNet and need to create one.</span><span class="sxs-lookup"><span data-stu-id="70556-140">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="70556-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span><span class="sxs-lookup"><span data-stu-id="70556-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="70556-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span><span class="sxs-lookup"><span data-stu-id="70556-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="70556-143">I already have a Resource Manager deployment model VNet.</span><span class="sxs-lookup"><span data-stu-id="70556-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="70556-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span><span class="sxs-lookup"><span data-stu-id="70556-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="70556-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span><span class="sxs-lookup"><span data-stu-id="70556-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="70556-146">When creating the new connections, the steps must be completed in a specific order.</span><span class="sxs-lookup"><span data-stu-id="70556-146">When creating the new connections, the steps must be completed in a specific order.</span></span> <span data-ttu-id="70556-147">Don't use the instructions in other articles to create your gateways and connections.</span><span class="sxs-lookup"><span data-stu-id="70556-147">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="70556-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span><span class="sxs-lookup"><span data-stu-id="70556-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="70556-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span><span class="sxs-lookup"><span data-stu-id="70556-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="70556-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span><span class="sxs-lookup"><span data-stu-id="70556-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <a name="new"></a><span data-ttu-id="70556-151">To create a new virtual network and coexisting connections</span><span class="sxs-lookup"><span data-stu-id="70556-151">To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="70556-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span><span class="sxs-lookup"><span data-stu-id="70556-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="70556-153">Install the latest version of the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="70556-153">Install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="70556-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="70556-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="70556-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span><span class="sxs-lookup"><span data-stu-id="70556-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="70556-156">Be sure to use the cmdlets specified in these instructions.</span><span class="sxs-lookup"><span data-stu-id="70556-156">Be sure to use the cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="70556-157">Log in to your account and set up the environment.</span><span class="sxs-lookup"><span data-stu-id="70556-157">Log in to your account and set up the environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  ```
3. <span data-ttu-id="70556-158">Create a virtual network including Gateway Subnet.</span><span class="sxs-lookup"><span data-stu-id="70556-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="70556-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="70556-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > The Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).
   > 
   > 
   
    <span data-ttu-id="70556-161">Create a new VNet.</span><span class="sxs-lookup"><span data-stu-id="70556-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="70556-162">Add subnets.</span><span class="sxs-lookup"><span data-stu-id="70556-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="70556-163">Save the VNet configuration.</span><span class="sxs-lookup"><span data-stu-id="70556-163">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a><span data-ttu-id="70556-164">Create an ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-164">Create an ExpressRoute gateway.</span></span> <span data-ttu-id="70556-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="70556-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="70556-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="70556-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="70556-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="70556-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="70556-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span><span class="sxs-lookup"><span data-stu-id="70556-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="70556-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="70556-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a><span data-ttu-id="70556-170">Next, create your Site-to-Site VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-170">Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="70556-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="70556-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="70556-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="70556-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="70556-173">The VpnType must *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="70556-173">The VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="70556-174">Azure VPN gateway supports the BGP.</span><span class="sxs-lookup"><span data-stu-id="70556-174">Azure VPN gateway supports the BGP.</span></span> <span data-ttu-id="70556-175">You can specify -EnableBgp in the following command.</span><span class="sxs-lookup"><span data-stu-id="70556-175">You can specify -EnableBgp in the following command.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -EnableBgp $true
  ```
   
    <span data-ttu-id="70556-176">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="70556-176">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="70556-177">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-177">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="70556-178">Create a local site VPN gateway entity.</span><span class="sxs-lookup"><span data-stu-id="70556-178">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="70556-179">This command doesn’t configure your on-premises VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-179">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="70556-180">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span><span class="sxs-lookup"><span data-stu-id="70556-180">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
    <span data-ttu-id="70556-181">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span><span class="sxs-lookup"><span data-stu-id="70556-181">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="70556-182">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span><span class="sxs-lookup"><span data-stu-id="70556-182">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="70556-183">Configure your local VPN device to connect to the new Azure VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-183">Configure your local VPN device to connect to the new Azure VPN gateway.</span></span> <span data-ttu-id="70556-184">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="70556-184">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="70556-185">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-185">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a><span data-ttu-id="70556-186">To configure coexisting connections for an already existing VNet</span><span class="sxs-lookup"><span data-stu-id="70556-186">To configure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="70556-187">If you have an existing virtual network, check the gateway subnet size.</span><span class="sxs-lookup"><span data-stu-id="70556-187">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="70556-188">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span><span class="sxs-lookup"><span data-stu-id="70556-188">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="70556-189">The steps in this section show you how to do that.</span><span class="sxs-lookup"><span data-stu-id="70556-189">The steps in this section show you how to do that.</span></span>

<span data-ttu-id="70556-190">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span><span class="sxs-lookup"><span data-stu-id="70556-190">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span> 

> [!NOTE]
> When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration. 
> 
> 

1. <span data-ttu-id="70556-192">You'll need to install the latest version of the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="70556-192">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="70556-193">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="70556-193">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="70556-194">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span><span class="sxs-lookup"><span data-stu-id="70556-194">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="70556-195">Be sure to use the cmdlets specified in these instructions.</span><span class="sxs-lookup"><span data-stu-id="70556-195">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="70556-196">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-196">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="70556-197">Delete Gateway Subnet.</span><span class="sxs-lookup"><span data-stu-id="70556-197">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="70556-198">Add a Gateway Subnet that is /27 or larger.</span><span class="sxs-lookup"><span data-stu-id="70556-198">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="70556-200">Save the VNet configuration.</span><span class="sxs-lookup"><span data-stu-id="70556-200">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="70556-201">At this point, you have a VNet with no gateways.</span><span class="sxs-lookup"><span data-stu-id="70556-201">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="70556-202">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span><span class="sxs-lookup"><span data-stu-id="70556-202">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a><span data-ttu-id="70556-203">To add point-to-site configuration to the VPN gateway</span><span class="sxs-lookup"><span data-stu-id="70556-203">To add point-to-site configuration to the VPN gateway</span></span>
<span data-ttu-id="70556-204">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span><span class="sxs-lookup"><span data-stu-id="70556-204">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="70556-205">Add VPN Client address pool.</span><span class="sxs-lookup"><span data-stu-id="70556-205">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="70556-206">Upload the VPN root certificate to Azure for your VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="70556-206">Upload the VPN root certificate to Azure for your VPN gateway.</span></span> <span data-ttu-id="70556-207">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span><span class="sxs-lookup"><span data-stu-id="70556-207">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="70556-208">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="70556-208">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70556-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="70556-209">Next steps</span></span>
<span data-ttu-id="70556-210">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="70556-210">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

