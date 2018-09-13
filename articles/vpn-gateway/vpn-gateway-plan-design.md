---
title: 'Planning and design for cross-premises connections: Azure VPN Gateway| Microsoft Docs'
description: Learn about VPN Gateway planning and design for cross-premises, hybrid, and VNet-to-VNet connections
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/05/2017
ms.author: cherylmc
ms.openlocfilehash: 83b850859cc51a72910c15788f0634bc99c94c6f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554250"
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="a176a-103">Planning and design for VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="a176a-103">Planning and design for VPN Gateway</span></span>
<span data-ttu-id="a176a-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span><span class="sxs-lookup"><span data-stu-id="a176a-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="a176a-105">This article walks you through basic planning and design considerations.</span><span class="sxs-lookup"><span data-stu-id="a176a-105">This article walks you through basic planning and design considerations.</span></span>

## <a name="planning"></a><span data-ttu-id="a176a-106">Planning</span><span class="sxs-lookup"><span data-stu-id="a176a-106">Planning</span></span>
### <a name="compare"></a><span data-ttu-id="a176a-107">Cross-premises connectivity options</span><span class="sxs-lookup"><span data-stu-id="a176a-107">Cross-premises connectivity options</span></span>
<span data-ttu-id="a176a-108">If you want to connect your on-premises sites securely to a virtual network, you have three different ways to do so: Site-to-Site, Point-to-Site, and ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a176a-108">If you want to connect your on-premises sites securely to a virtual network, you have three different ways to do so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="a176a-109">Compare the different cross-premises connections that are available.</span><span class="sxs-lookup"><span data-stu-id="a176a-109">Compare the different cross-premises connections that are available.</span></span> <span data-ttu-id="a176a-110">The option you choose can depend on various considerations, such as:</span><span class="sxs-lookup"><span data-stu-id="a176a-110">The option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="a176a-111">What kind of throughput does your solution require?</span><span class="sxs-lookup"><span data-stu-id="a176a-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="a176a-112">Do you want to communicate over the public Internet via secure VPN, or over a private connection?</span><span class="sxs-lookup"><span data-stu-id="a176a-112">Do you want to communicate over the public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="a176a-113">Do you have a public IP address available to use?</span><span class="sxs-lookup"><span data-stu-id="a176a-113">Do you have a public IP address available to use?</span></span>
* <span data-ttu-id="a176a-114">Are you planning to use a VPN device?</span><span class="sxs-lookup"><span data-stu-id="a176a-114">Are you planning to use a VPN device?</span></span> <span data-ttu-id="a176a-115">If so, is it compatible?</span><span class="sxs-lookup"><span data-stu-id="a176a-115">If so, is it compatible?</span></span>
* <span data-ttu-id="a176a-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span><span class="sxs-lookup"><span data-stu-id="a176a-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="a176a-117">What type of VPN gateway is required for the solution you want to create?</span><span class="sxs-lookup"><span data-stu-id="a176a-117">What type of VPN gateway is required for the solution you want to create?</span></span>
* <span data-ttu-id="a176a-118">Which gateway SKU should you use?</span><span class="sxs-lookup"><span data-stu-id="a176a-118">Which gateway SKU should you use?</span></span>

<span data-ttu-id="a176a-119">The following table can help you decide the best connectivity option for your solution.</span><span class="sxs-lookup"><span data-stu-id="a176a-119">The following table can help you decide the best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwrequire"></a><span data-ttu-id="a176a-120">Gateway requirements by VPN type and SKU</span><span class="sxs-lookup"><span data-stu-id="a176a-120">Gateway requirements by VPN type and SKU</span></span>
[!INCLUDE [vpn-gateway-gwsku](../../includes/vpn-gateway-gwsku-include.md)]

<span data-ttu-id="a176a-121">For more information about gateway SKUs, see [VPN Gateway settings](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="a176a-121">For more information about gateway SKUs, see [VPN Gateway settings](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

#### <a name="aggregate-throughput-by-sku-and-vpn-type"></a><span data-ttu-id="a176a-122">Aggregate throughput by SKU and VPN type</span><span class="sxs-lookup"><span data-stu-id="a176a-122">Aggregate throughput by SKU and VPN type</span></span>
[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

#### <a name="supported-configurations-by-sku-and-vpn-type"></a><span data-ttu-id="a176a-123">Supported configurations by SKU and VPN type</span><span class="sxs-lookup"><span data-stu-id="a176a-123">Supported configurations by SKU and VPN type</span></span>
[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

### <a name="wf"></a><span data-ttu-id="a176a-124">Workflow</span><span class="sxs-lookup"><span data-stu-id="a176a-124">Workflow</span></span>
<span data-ttu-id="a176a-125">The following list outlines the common workflow for cloud connectivity:</span><span class="sxs-lookup"><span data-stu-id="a176a-125">The following list outlines the common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="a176a-126">Design and plan your connectivity topology and list the address spaces for all networks you want to connect.</span><span class="sxs-lookup"><span data-stu-id="a176a-126">Design and plan your connectivity topology and list the address spaces for all networks you want to connect.</span></span>
2. <span data-ttu-id="a176a-127">Create an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="a176a-127">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="a176a-128">Create a VPN gateway for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a176a-128">Create a VPN gateway for the virtual network.</span></span>
4. <span data-ttu-id="a176a-129">Create and configure connections to on-premises networks or other virtual networks (as needed).</span><span class="sxs-lookup"><span data-stu-id="a176a-129">Create and configure connections to on-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="a176a-130">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span><span class="sxs-lookup"><span data-stu-id="a176a-130">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <a name="design"></a><span data-ttu-id="a176a-131">Design</span><span class="sxs-lookup"><span data-stu-id="a176a-131">Design</span></span>
### <a name="topologies"></a><span data-ttu-id="a176a-132">Connection topologies</span><span class="sxs-lookup"><span data-stu-id="a176a-132">Connection topologies</span></span>
<span data-ttu-id="a176a-133">Start by looking at the diagrams in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span><span class="sxs-lookup"><span data-stu-id="a176a-133">Start by looking at the diagrams in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="a176a-134">The article contains basic diagrams, the deployment models for each topology (Resource Manager or classic), and which deployment tools you can use to deploy your configuration.</span><span class="sxs-lookup"><span data-stu-id="a176a-134">The article contains basic diagrams, the deployment models for each topology (Resource Manager or classic), and which deployment tools you can use to deploy your configuration.</span></span>   

### <a name="designbasics"></a><span data-ttu-id="a176a-135">Design basics</span><span class="sxs-lookup"><span data-stu-id="a176a-135">Design basics</span></span>
<span data-ttu-id="a176a-136">The following sections discuss the VPN gateway basics.</span><span class="sxs-lookup"><span data-stu-id="a176a-136">The following sections discuss the VPN gateway basics.</span></span> <span data-ttu-id="a176a-137">Also, consider [networking services limitations](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="a176a-137">Also, consider [networking services limitations](../azure-subscription-service-limits.md#networking-limits).</span></span>

#### <a name="subnets"></a><span data-ttu-id="a176a-138">About subnets</span><span class="sxs-lookup"><span data-stu-id="a176a-138">About subnets</span></span>
<span data-ttu-id="a176a-139">When you are creating connections, you must consider your subnet ranges.</span><span class="sxs-lookup"><span data-stu-id="a176a-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="a176a-140">You cannot have overlapping subnet address ranges.</span><span class="sxs-lookup"><span data-stu-id="a176a-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="a176a-141">An overlapping subnet is when one virtual network or on-premises location contains the same address space that the other location contains.</span><span class="sxs-lookup"><span data-stu-id="a176a-141">An overlapping subnet is when one virtual network or on-premises location contains the same address space that the other location contains.</span></span> <span data-ttu-id="a176a-142">This means that you need your network engineers for your local on-premises networks to carve out a range for you to use for your Azure IP addressing space/subnets.</span><span class="sxs-lookup"><span data-stu-id="a176a-142">This means that you need your network engineers for your local on-premises networks to carve out a range for you to use for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="a176a-143">You need address space that is not being used on the local on-premises network.</span><span class="sxs-lookup"><span data-stu-id="a176a-143">You need address space that is not being used on the local on-premises network.</span></span> 

<span data-ttu-id="a176a-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span><span class="sxs-lookup"><span data-stu-id="a176a-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="a176a-145">If your subnets overlap and an IP address exists in both the sending and destination VNets, VNet-to-VNet connections fail.</span><span class="sxs-lookup"><span data-stu-id="a176a-145">If your subnets overlap and an IP address exists in both the sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="a176a-146">Azure can't route the data to the other VNet because the destination address is part of the sending VNet.</span><span class="sxs-lookup"><span data-stu-id="a176a-146">Azure can't route the data to the other VNet because the destination address is part of the sending VNet.</span></span> 

<span data-ttu-id="a176a-147">VPN Gateways require a specific subnet called a gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="a176a-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="a176a-148">All gateway subnets must be named GatewaySubnet to work properly.</span><span class="sxs-lookup"><span data-stu-id="a176a-148">All gateway subnets must be named GatewaySubnet to work properly.</span></span> <span data-ttu-id="a176a-149">Be sure not to name your gateway subnet a different name, and don't deploy VMs or anything else to the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="a176a-149">Be sure not to name your gateway subnet a different name, and don't deploy VMs or anything else to the gateway subnet.</span></span> <span data-ttu-id="a176a-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="a176a-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <a name="local"></a><span data-ttu-id="a176a-151">About local network gateways</span><span class="sxs-lookup"><span data-stu-id="a176a-151">About local network gateways</span></span>
<span data-ttu-id="a176a-152">The local network gateway typically refers to your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="a176a-152">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="a176a-153">In the classic deployment model, the local network gateway is referred to as a Local Network Site.</span><span class="sxs-lookup"><span data-stu-id="a176a-153">In the classic deployment model, the local network gateway is referred to as a Local Network Site.</span></span> <span data-ttu-id="a176a-154">When you configure a local network gateway, you give it a name, specify the public IP address of the on-premises VPN device, and specify the address prefixes that are in the on-premises location.</span><span class="sxs-lookup"><span data-stu-id="a176a-154">When you configure a local network gateway, you give it a name, specify the public IP address of the on-premises VPN device, and specify the address prefixes that are in the on-premises location.</span></span> <span data-ttu-id="a176a-155">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for the local network gateway, and routes packets accordingly.</span><span class="sxs-lookup"><span data-stu-id="a176a-155">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for the local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="a176a-156">You can modify these address prefixes as needed.</span><span class="sxs-lookup"><span data-stu-id="a176a-156">You can modify these address prefixes as needed.</span></span> <span data-ttu-id="a176a-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="a176a-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <a name="gwtype"></a><span data-ttu-id="a176a-158">About gateway types</span><span class="sxs-lookup"><span data-stu-id="a176a-158">About gateway types</span></span>
<span data-ttu-id="a176a-159">Selecting the correct gateway type for your topology is critical.</span><span class="sxs-lookup"><span data-stu-id="a176a-159">Selecting the correct gateway type for your topology is critical.</span></span> <span data-ttu-id="a176a-160">If you select the wrong type, your gateway won't work properly.</span><span class="sxs-lookup"><span data-stu-id="a176a-160">If you select the wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="a176a-161">The gateway type specifies how the gateway itself connects and is a required configuration setting for the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="a176a-161">The gateway type specifies how the gateway itself connects and is a required configuration setting for the Resource Manager deployment model.</span></span>

<span data-ttu-id="a176a-162">The gateway types are:</span><span class="sxs-lookup"><span data-stu-id="a176a-162">The gateway types are:</span></span>

* <span data-ttu-id="a176a-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="a176a-163">Vpn</span></span>
* <span data-ttu-id="a176a-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a176a-164">ExpressRoute</span></span>

#### <a name="connectiontype"></a><span data-ttu-id="a176a-165">About connection types</span><span class="sxs-lookup"><span data-stu-id="a176a-165">About connection types</span></span>
<span data-ttu-id="a176a-166">Each configuration requires a specific connection type.</span><span class="sxs-lookup"><span data-stu-id="a176a-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="a176a-167">The connection types are:</span><span class="sxs-lookup"><span data-stu-id="a176a-167">The connection types are:</span></span>

* <span data-ttu-id="a176a-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="a176a-168">IPsec</span></span>
* <span data-ttu-id="a176a-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="a176a-169">Vnet2Vnet</span></span>
* <span data-ttu-id="a176a-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a176a-170">ExpressRoute</span></span>
* <span data-ttu-id="a176a-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="a176a-171">VPNClient</span></span>

#### <a name="vpntype"></a><span data-ttu-id="a176a-172">About VPN types</span><span class="sxs-lookup"><span data-stu-id="a176a-172">About VPN types</span></span>
<span data-ttu-id="a176a-173">Each configuration requires a specific VPN type.</span><span class="sxs-lookup"><span data-stu-id="a176a-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="a176a-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection to the same VNet, you must use a VPN type that satisfies both connection requirements.</span><span class="sxs-lookup"><span data-stu-id="a176a-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection to the same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="a176a-175">The following tables show the VPN type as it maps to each connection configuration.</span><span class="sxs-lookup"><span data-stu-id="a176a-175">The following tables show the VPN type as it maps to each connection configuration.</span></span> <span data-ttu-id="a176a-176">Make sure the VPN type for your gateway matches the configuration that you want to create.</span><span class="sxs-lookup"><span data-stu-id="a176a-176">Make sure the VPN type for your gateway matches the configuration that you want to create.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a><span data-ttu-id="a176a-177">VPN devices for Site-to-Site connections</span><span class="sxs-lookup"><span data-stu-id="a176a-177">VPN devices for Site-to-Site connections</span></span>
<span data-ttu-id="a176a-178">To configure a Site-to-Site connection, regardless of deployment model, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a176a-178">To configure a Site-to-Site connection, regardless of deployment model, you need the following items:</span></span>

* <span data-ttu-id="a176a-179">A VPN device that is compatible with Azure VPN gateways</span><span class="sxs-lookup"><span data-stu-id="a176a-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="a176a-180">A public-facing IPv4 IP address that is not behind a NAT</span><span class="sxs-lookup"><span data-stu-id="a176a-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="a176a-181">You need to have experience configuring your VPN device, or have someone that can configure the device for you.</span><span class="sxs-lookup"><span data-stu-id="a176a-181">You need to have experience configuring your VPN device, or have someone that can configure the device for you.</span></span> <span data-ttu-id="a176a-182">For more information about VPN devices, see [About VPN devices](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="a176a-182">For more information about VPN devices, see [About VPN devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="a176a-183">The VPN devices article contains information about validated devices, requirements for devices that have not been validated, and links to device configuration documents if available.</span><span class="sxs-lookup"><span data-stu-id="a176a-183">The VPN devices article contains information about validated devices, requirements for devices that have not been validated, and links to device configuration documents if available.</span></span>

### <a name="forcedtunnel"></a><span data-ttu-id="a176a-184">Consider forced tunnel routing</span><span class="sxs-lookup"><span data-stu-id="a176a-184">Consider forced tunnel routing</span></span>
<span data-ttu-id="a176a-185">For most configurations, you can configure forced tunneling.</span><span class="sxs-lookup"><span data-stu-id="a176a-185">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="a176a-186">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span><span class="sxs-lookup"><span data-stu-id="a176a-186">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="a176a-187">This is a critical security requirement for most enterprise IT policies.</span><span class="sxs-lookup"><span data-stu-id="a176a-187">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="a176a-188">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span><span class="sxs-lookup"><span data-stu-id="a176a-188">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="a176a-189">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span><span class="sxs-lookup"><span data-stu-id="a176a-189">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

<span data-ttu-id="a176a-190">A forced tunneling connection can be configured in both deployment models and by using different tools.</span><span class="sxs-lookup"><span data-stu-id="a176a-190">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="a176a-191">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="a176a-191">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="a176a-192">**Forced tunneling diagram**</span><span class="sxs-lookup"><span data-stu-id="a176a-192">**Forced tunneling diagram**</span></span>

![Azure VPN Gateway forced tunneling diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="a176a-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="a176a-194">Next steps</span></span>
<span data-ttu-id="a176a-195">See the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information to help you with your design.</span><span class="sxs-lookup"><span data-stu-id="a176a-195">See the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information to help you with your design.</span></span>

<span data-ttu-id="a176a-196">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="a176a-196">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>


