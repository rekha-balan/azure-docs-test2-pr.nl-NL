---
title: VPN gateway settings for cross-premises Azure connections | Microsoft Docs
description: Learn about VPN Gateway settings for Azure virtual network gateways.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: cherylmc
ms.openlocfilehash: 1ac5a78c8d9419e4c641bf66f8dac7aa8cbcd179
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551367"
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="b0fee-103">About VPN Gateway configuration settings</span><span class="sxs-lookup"><span data-stu-id="b0fee-103">About VPN Gateway configuration settings</span></span>
<span data-ttu-id="b0fee-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span><span class="sxs-lookup"><span data-stu-id="b0fee-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="b0fee-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span><span class="sxs-lookup"><span data-stu-id="b0fee-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span></span>

<span data-ttu-id="b0fee-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span><span class="sxs-lookup"><span data-stu-id="b0fee-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="b0fee-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="b0fee-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="b0fee-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span><span class="sxs-lookup"><span data-stu-id="b0fee-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>  

## <a name="gwtype"></a><span data-ttu-id="b0fee-109">Gateway types</span><span class="sxs-lookup"><span data-stu-id="b0fee-109">Gateway types</span></span>
<span data-ttu-id="b0fee-110">Each virtual network can only have one virtual network gateway of each type.</span><span class="sxs-lookup"><span data-stu-id="b0fee-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="b0fee-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span><span class="sxs-lookup"><span data-stu-id="b0fee-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span>

<span data-ttu-id="b0fee-112">The available values for -GatewayType are:</span><span class="sxs-lookup"><span data-stu-id="b0fee-112">The available values for -GatewayType are:</span></span> 

* <span data-ttu-id="b0fee-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="b0fee-113">Vpn</span></span>
* <span data-ttu-id="b0fee-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b0fee-114">ExpressRoute</span></span>

<span data-ttu-id="b0fee-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="b0fee-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span></span>  

<span data-ttu-id="b0fee-116">Example:</span><span class="sxs-lookup"><span data-stu-id="b0fee-116">Example:</span></span>

    New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
    -Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
    -VpnType RouteBased


## <a name="gwsku"></a><span data-ttu-id="b0fee-117">Gateway SKUs</span><span class="sxs-lookup"><span data-stu-id="b0fee-117">Gateway SKUs</span></span>
[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configuring-the-gateway-sku"></a><span data-ttu-id="b0fee-118">Configuring the gateway SKU</span><span class="sxs-lookup"><span data-stu-id="b0fee-118">Configuring the gateway SKU</span></span>
####<a name="specifying-the-gateway-sku-in-the-azure-portal"></a><span data-ttu-id="b0fee-119">Specifying the gateway SKU in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b0fee-119">Specifying the gateway SKU in the Azure portal</span></span>

<span data-ttu-id="b0fee-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span><span class="sxs-lookup"><span data-stu-id="b0fee-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span></span> <span data-ttu-id="b0fee-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span><span class="sxs-lookup"><span data-stu-id="b0fee-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span></span>

<span data-ttu-id="b0fee-122">For example, if you select the gateway type 'VPN' and the VPN type 'Policy-based', you see only the 'Basic' SKU because that is the only SKU available for PolicyBased VPNs.</span><span class="sxs-lookup"><span data-stu-id="b0fee-122">For example, if you select the gateway type 'VPN' and the VPN type 'Policy-based', you see only the 'Basic' SKU because that is the only SKU available for PolicyBased VPNs.</span></span> <span data-ttu-id="b0fee-123">If you select 'Route-based', you can select from Basic, Standard, and HighPerformance SKUs.</span><span class="sxs-lookup"><span data-stu-id="b0fee-123">If you select 'Route-based', you can select from Basic, Standard, and HighPerformance SKUs.</span></span> 

####<a name="specifying-the-gateway-sku-using-powershell"></a><span data-ttu-id="b0fee-124">Specifying the gateway SKU using PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0fee-124">Specifying the gateway SKU using PowerShell</span></span>

<span data-ttu-id="b0fee-125">The following PowerShell example specifies the `-GatewaySku` as *Standard*.</span><span class="sxs-lookup"><span data-stu-id="b0fee-125">The following PowerShell example specifies the `-GatewaySku` as *Standard*.</span></span>

    New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
    -Location 'West US' -IpConfigurations $gwipconfig -GatewaySku Standard `
    -GatewayType Vpn -VpnType RouteBased

####<a name="changing-a-gateway-sku"></a><span data-ttu-id="b0fee-126">Changing a gateway SKU</span><span class="sxs-lookup"><span data-stu-id="b0fee-126">Changing a gateway SKU</span></span>

<span data-ttu-id="b0fee-127">If you want to upgrade your gateway SKU to a more powerful SKU (from Basic/Standard to HighPerformance), you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0fee-127">If you want to upgrade your gateway SKU to a more powerful SKU (from Basic/Standard to HighPerformance), you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="b0fee-128">You can also downgrade the gateway SKU size using this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0fee-128">You can also downgrade the gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="b0fee-129">The following PowerShell example shows a gateway SKU being resized to HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="b0fee-129">The following PowerShell example shows a gateway SKU being resized to HighPerformance.</span></span>

    $gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
    Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance

### <a name="estimated-aggregate-throughput-by-gateway-sku-and-type"></a><span data-ttu-id="b0fee-130">Estimated aggregate throughput by gateway SKU and type</span><span class="sxs-lookup"><span data-stu-id="b0fee-130">Estimated aggregate throughput by gateway SKU and type</span></span>
[!INCLUDE [vpn-gateway-table-gwtype-aggthroughput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

## <a name="connectiontype"></a><span data-ttu-id="b0fee-131">Connection types</span><span class="sxs-lookup"><span data-stu-id="b0fee-131">Connection types</span></span>
<span data-ttu-id="b0fee-132">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span><span class="sxs-lookup"><span data-stu-id="b0fee-132">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="b0fee-133">The available Resource Manager PowerShell values for `-ConnectionType` are:</span><span class="sxs-lookup"><span data-stu-id="b0fee-133">The available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="b0fee-134">IPsec</span><span class="sxs-lookup"><span data-stu-id="b0fee-134">IPsec</span></span>
* <span data-ttu-id="b0fee-135">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="b0fee-135">Vnet2Vnet</span></span>
* <span data-ttu-id="b0fee-136">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b0fee-136">ExpressRoute</span></span>
* <span data-ttu-id="b0fee-137">VPNClient</span><span class="sxs-lookup"><span data-stu-id="b0fee-137">VPNClient</span></span>

<span data-ttu-id="b0fee-138">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="b0fee-138">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span></span>

    New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
    -Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
    -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'


## <a name="vpntype"></a><span data-ttu-id="b0fee-139">VPN types</span><span class="sxs-lookup"><span data-stu-id="b0fee-139">VPN types</span></span>
<span data-ttu-id="b0fee-140">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span><span class="sxs-lookup"><span data-stu-id="b0fee-140">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="b0fee-141">The VPN type that you choose depends on the connection topology that you want to create.</span><span class="sxs-lookup"><span data-stu-id="b0fee-141">The VPN type that you choose depends on the connection topology that you want to create.</span></span> <span data-ttu-id="b0fee-142">For example, a P2S connection requires a RouteBased VPN type.</span><span class="sxs-lookup"><span data-stu-id="b0fee-142">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="b0fee-143">A VPN type can also depend on the hardware that you will be using.</span><span class="sxs-lookup"><span data-stu-id="b0fee-143">A VPN type can also depend on the hardware that you will be using.</span></span> <span data-ttu-id="b0fee-144">S2S configurations require a VPN device.</span><span class="sxs-lookup"><span data-stu-id="b0fee-144">S2S configurations require a VPN device.</span></span> <span data-ttu-id="b0fee-145">Some VPN devices only support a certain VPN type.</span><span class="sxs-lookup"><span data-stu-id="b0fee-145">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="b0fee-146">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span><span class="sxs-lookup"><span data-stu-id="b0fee-146">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span></span> <span data-ttu-id="b0fee-147">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span><span class="sxs-lookup"><span data-stu-id="b0fee-147">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="b0fee-148">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span><span class="sxs-lookup"><span data-stu-id="b0fee-148">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="b0fee-149">Once a virtual network gateway has been created, you can't change the VPN type.</span><span class="sxs-lookup"><span data-stu-id="b0fee-149">Once a virtual network gateway has been created, you can't change the VPN type.</span></span> <span data-ttu-id="b0fee-150">You have to delete the virtual network gateway and create a new one.</span><span class="sxs-lookup"><span data-stu-id="b0fee-150">You have to delete the virtual network gateway and create a new one.</span></span> <span data-ttu-id="b0fee-151">There are two VPN types:</span><span class="sxs-lookup"><span data-stu-id="b0fee-151">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="b0fee-152">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="b0fee-152">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="b0fee-153">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span><span class="sxs-lookup"><span data-stu-id="b0fee-153">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span></span> 

    New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
    -Location 'West US' -IpConfigurations $gwipconfig `
    -GatewayType Vpn -VpnType RouteBased

## <a name="requirements"></a><span data-ttu-id="b0fee-154">Gateway requirements</span><span class="sxs-lookup"><span data-stu-id="b0fee-154">Gateway requirements</span></span>
[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a><span data-ttu-id="b0fee-155">Gateway subnet</span><span class="sxs-lookup"><span data-stu-id="b0fee-155">Gateway subnet</span></span>
<span data-ttu-id="b0fee-156">In order to configure a virtual network gateway for your VNet, you'll need to create a gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="b0fee-156">In order to configure a virtual network gateway for your VNet, you'll need to create a gateway subnet.</span></span> <span data-ttu-id="b0fee-157">The gateway subnet contains the IP addresses that the virtual network gateway services use.</span><span class="sxs-lookup"><span data-stu-id="b0fee-157">The gateway subnet contains the IP addresses that the virtual network gateway services use.</span></span> <span data-ttu-id="b0fee-158">The gateway subnet must be named *GatewaySubnet* to work properly.</span><span class="sxs-lookup"><span data-stu-id="b0fee-158">The gateway subnet must be named *GatewaySubnet* to work properly.</span></span> <span data-ttu-id="b0fee-159">This name lets Azure know that this subnet should be used for the gateway.</span><span class="sxs-lookup"><span data-stu-id="b0fee-159">This name lets Azure know that this subnet should be used for the gateway.</span></span>

<span data-ttu-id="b0fee-160">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span><span class="sxs-lookup"><span data-stu-id="b0fee-160">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="b0fee-161">The IP addresses in the gateway subnet are allocated to the gateway service.</span><span class="sxs-lookup"><span data-stu-id="b0fee-161">The IP addresses in the gateway subnet are allocated to the gateway service.</span></span> <span data-ttu-id="b0fee-162">Some configurations require more IP addresses to be allocated to the gateway service than do others.</span><span class="sxs-lookup"><span data-stu-id="b0fee-162">Some configurations require more IP addresses to be allocated to the gateway service than do others.</span></span> <span data-ttu-id="b0fee-163">You want to make sure your gateway subnet contains enough IP addresses to accommodate future growth and possible additional new connection configurations.</span><span class="sxs-lookup"><span data-stu-id="b0fee-163">You want to make sure your gateway subnet contains enough IP addresses to accommodate future growth and possible additional new connection configurations.</span></span> <span data-ttu-id="b0fee-164">So, while you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span><span class="sxs-lookup"><span data-stu-id="b0fee-164">So, while you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="b0fee-165">Look at the requirements for the configuration that you want to create and verify that the gateway subnet that you have will meet those requirements.</span><span class="sxs-lookup"><span data-stu-id="b0fee-165">Look at the requirements for the configuration that you want to create and verify that the gateway subnet that you have will meet those requirements.</span></span>

<span data-ttu-id="b0fee-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="b0fee-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="b0fee-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span><span class="sxs-lookup"><span data-stu-id="b0fee-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

    Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a><span data-ttu-id="b0fee-168">Local network gateways</span><span class="sxs-lookup"><span data-stu-id="b0fee-168">Local network gateways</span></span>
<span data-ttu-id="b0fee-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="b0fee-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="b0fee-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span><span class="sxs-lookup"><span data-stu-id="b0fee-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span></span> 

<span data-ttu-id="b0fee-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span><span class="sxs-lookup"><span data-stu-id="b0fee-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span></span> <span data-ttu-id="b0fee-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span><span class="sxs-lookup"><span data-stu-id="b0fee-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="b0fee-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span><span class="sxs-lookup"><span data-stu-id="b0fee-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="b0fee-174">The following PowerShell example creates a new local network gateway:</span><span class="sxs-lookup"><span data-stu-id="b0fee-174">The following PowerShell example creates a new local network gateway:</span></span>

    New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
    -Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'

<span data-ttu-id="b0fee-175">Sometimes you need to modify the local network gateway settings.</span><span class="sxs-lookup"><span data-stu-id="b0fee-175">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="b0fee-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span><span class="sxs-lookup"><span data-stu-id="b0fee-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="b0fee-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span><span class="sxs-lookup"><span data-stu-id="b0fee-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span></span> <span data-ttu-id="b0fee-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b0fee-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <a name="resources"></a><span data-ttu-id="b0fee-179">REST APIs and PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b0fee-179">REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="b0fee-180">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for VPN Gateway configurations, see the following pages:</span><span class="sxs-lookup"><span data-stu-id="b0fee-180">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for VPN Gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="b0fee-181">**Classic**</span><span class="sxs-lookup"><span data-stu-id="b0fee-181">**Classic**</span></span> | <span data-ttu-id="b0fee-182">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="b0fee-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="b0fee-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0fee-183">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="b0fee-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0fee-184">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="b0fee-185">REST API</span><span class="sxs-lookup"><span data-stu-id="b0fee-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="b0fee-186">REST API</span><span class="sxs-lookup"><span data-stu-id="b0fee-186">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="b0fee-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0fee-187">Next steps</span></span>
<span data-ttu-id="b0fee-188">See [About VPN Gateway](vpn-gateway-about-vpngateways.md) for more information about available connection configurations.</span><span class="sxs-lookup"><span data-stu-id="b0fee-188">See [About VPN Gateway](vpn-gateway-about-vpngateways.md) for more information about available connection configurations.</span></span> 

