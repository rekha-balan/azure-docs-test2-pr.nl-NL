---
title: 'Configure forced tunneling for Azure Site-to-Site connections: Resource Manager | Microsoft Docs'
description: How to redirect or 'force' all Internet-bound traffic back to your on-premises location.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: cherylmc
ms.openlocfilehash: 58c5d8fadbb7c8dada36a836a2ee52cdbe53acdb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551593"
---
# <a name="configure-forced-tunneling-using-the-azure-resource-manager-deployment-model"></a><span data-ttu-id="c1c3a-103">Configure forced tunneling using the Azure Resource Manager deployment model</span><span class="sxs-lookup"><span data-stu-id="c1c3a-103">Configure forced tunneling using the Azure Resource Manager deployment model</span></span>

<span data-ttu-id="c1c3a-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="c1c3a-105">This is a critical security requirement for most enterprise IT policies.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="c1c3a-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="c1c3a-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches</span><span class="sxs-lookup"><span data-stu-id="c1c3a-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="c1c3a-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-108">This article walks you through configuring forced tunneling for virtual networks created using the Resource Manager deployment model.</span></span> <span data-ttu-id="c1c3a-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="c1c3a-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span><span class="sxs-lookup"><span data-stu-id="c1c3a-110">If you want to configure forced tunneling for the classic deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [PowerShell - Classic](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 


## <a name="about-forced-tunneling"></a><span data-ttu-id="c1c3a-113">About forced tunneling</span><span class="sxs-lookup"><span data-stu-id="c1c3a-113">About forced tunneling</span></span>
<span data-ttu-id="c1c3a-114">The following diagram illustrates how forced tunneling works.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-114">The following diagram illustrates how forced tunneling works.</span></span> 

![Forced Tunneling](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="c1c3a-116">In the example above, the Frontend subnet is not forced tunneled.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-116">In the example above, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="c1c3a-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-117">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="c1c3a-118">The Mid-tier and Backend subnets are forced tunneled.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-118">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="c1c3a-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-119">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="c1c3a-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-120">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="c1c3a-121">You also can apply forced tunneling to the entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-121">You also can apply forced tunneling to the entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="c1c3a-122">Requirements and considerations</span><span class="sxs-lookup"><span data-stu-id="c1c3a-122">Requirements and considerations</span></span>
<span data-ttu-id="c1c3a-123">Forced tunneling in Azure is configured via virtual network user defined routes.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-123">Forced tunneling in Azure is configured via virtual network user defined routes.</span></span> <span data-ttu-id="c1c3a-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-124">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="c1c3a-125">For more information about user defined routing and virtual networks, see [User defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1c3a-125">For more information about user defined routing and virtual networks, see [User defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="c1c3a-126">Each virtual network subnet has a built-in, system routing table.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="c1c3a-127">The system routing table has the following three groups of routes:</span><span class="sxs-lookup"><span data-stu-id="c1c3a-127">The system routing table has the following three groups of routes:</span></span>
  
  * <span data-ttu-id="c1c3a-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network</span><span class="sxs-lookup"><span data-stu-id="c1c3a-128">**Local VNet routes:** Directly to the destination VMs in the same virtual network</span></span>
  * <span data-ttu-id="c1c3a-129">**On-premises routes:** To the Azure VPN gateway</span><span class="sxs-lookup"><span data-stu-id="c1c3a-129">**On-premises routes:** To the Azure VPN gateway</span></span>
  * <span data-ttu-id="c1c3a-130">**Default route:** Directly to the Internet.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-130">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="c1c3a-131">Packets destined to the private IP addresses not covered by the previous two routes will be dropped.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-131">Packets destined to the private IP addresses not covered by the previous two routes will be dropped.</span></span>
* <span data-ttu-id="c1c3a-132">This procedure uses user defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-132">This procedure uses user defined routes (UDR) to create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="c1c3a-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="c1c3a-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-134">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span>
* <span data-ttu-id="c1c3a-135">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-135">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="c1c3a-136">Please see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-136">Please see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="c1c3a-137">Configuration overview</span><span class="sxs-lookup"><span data-stu-id="c1c3a-137">Configuration overview</span></span>
<span data-ttu-id="c1c3a-138">The following procedure helps you create a resource group and a VNet.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-138">The following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="c1c3a-139">You'll then create a VPN gateway and configure forced tunneling.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-139">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="c1c3a-140">In this procedure, the virtual network "MultiTier-VNet" has 3 subnets: *Frontend*, *Midtier*, and *Backend*, with 4 cross-premises connections: *DefaultSiteHQ*, and 3 *Branches*.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-140">In this procedure, the virtual network "MultiTier-VNet" has 3 subnets: *Frontend*, *Midtier*, and *Backend*, with 4 cross-premises connections: *DefaultSiteHQ*, and 3 *Branches*.</span></span>

<span data-ttu-id="c1c3a-141">The procedure steps set the *DefaultSiteHQ* as the default site connection for forced tunneling, and configure the Midtier and Backend subnets to use forced tunneling.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-141">The procedure steps set the *DefaultSiteHQ* as the default site connection for forced tunneling, and configure the Midtier and Backend subnets to use forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c1c3a-142">Before you begin</span><span class="sxs-lookup"><span data-stu-id="c1c3a-142">Before you begin</span></span>
<span data-ttu-id="c1c3a-143">Verify that you have the following items before beginning your configuration.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-143">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="c1c3a-144">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-144">An Azure subscription.</span></span> <span data-ttu-id="c1c3a-145">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1c3a-145">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c1c3a-146">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets (1.0 or later).</span><span class="sxs-lookup"><span data-stu-id="c1c3a-146">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets (1.0 or later).</span></span> <span data-ttu-id="c1c3a-147">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-147">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="c1c3a-148">Configure forced tunneling</span><span class="sxs-lookup"><span data-stu-id="c1c3a-148">Configure forced tunneling</span></span>
1. <span data-ttu-id="c1c3a-149">In the PowerShell console, log in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-149">In the PowerShell console, log in to your Azure account.</span></span> <span data-ttu-id="c1c3a-150">This cmdlet prompts you for the login credentials for your Azure Account.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-150">This cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="c1c3a-151">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-151">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="c1c3a-152">Get a list of your Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-152">Get a list of your Azure subscriptions.</span></span>

 ```powershell
 Get-AzureRmSubscription
 ```
3. <span data-ttu-id="c1c3a-153">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-153">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```
4. <span data-ttu-id="c1c3a-154">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-154">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "ForcedTunneling" -Location "North Europe"
  ```
5. <span data-ttu-id="c1c3a-155">Create a virtual network and specify subnets.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-155">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
6. <span data-ttu-id="c1c3a-156">Create the local network gateways.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-156">Create the local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
7. <span data-ttu-id="c1c3a-157">Create the route table and route rule.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-157">Create the route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
8. <span data-ttu-id="c1c3a-158">Associate the route table to the Midtier and Backend subnets.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-158">Associate the route table to the Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
9. <span data-ttu-id="c1c3a-159">Create the Gateway with a default site.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-159">Create the Gateway with a default site.</span></span> <span data-ttu-id="c1c3a-160">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-160">This step takes some time to complete, sometimes 45 minutes or more, because you are creating and configuring the gateway.</span></span><br> <span data-ttu-id="c1c3a-161">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-161">The **-GatewayDefaultSite** is the cmdlet parameter that allows the forced routing configuration to work, so take care to configure this setting properly.</span></span> <span data-ttu-id="c1c3a-162">This parameter is available in PowerShell 1.0 or later.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-162">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
10. <span data-ttu-id="c1c3a-163">Establish the Site-to-Site VPN connections.</span><span class="sxs-lookup"><span data-stu-id="c1c3a-163">Establish the Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```

