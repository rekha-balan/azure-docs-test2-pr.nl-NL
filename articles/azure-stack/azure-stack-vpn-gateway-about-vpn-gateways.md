---
title: About VPN gateway for Azure Stack | Microsoft Docs
description: Learn about and configure VPN gateways you use with Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: 0e30522f-20d6-4da7-87d3-28ca3567a890
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/02/2018
ms.author: brenduns
ms.openlocfilehash: 0ff3402115ae9f4c736bf9058fc09de16eaefb1e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856238"
---
# <a name="about-vpn-gateway-for-azure-stack"></a><span data-ttu-id="2f14b-103">About VPN gateway for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2f14b-103">About VPN gateway for Azure Stack</span></span>

<span data-ttu-id="2f14b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="2f14b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="2f14b-105">Before you can send network traffic between your Azure virtual network and your on-premises site, you must create a virtual network gateway for your virtual network.</span><span class="sxs-lookup"><span data-stu-id="2f14b-105">Before you can send network traffic between your Azure virtual network and your on-premises site, you must create a virtual network gateway for your virtual network.</span></span>

<span data-ttu-id="2f14b-106">A VPN gateway is a type of virtual network gateway that sends encrypted traffic across a public connection.</span><span class="sxs-lookup"><span data-stu-id="2f14b-106">A VPN gateway is a type of virtual network gateway that sends encrypted traffic across a public connection.</span></span> <span data-ttu-id="2f14b-107">You can use VPN gateways to send traffic securely between a virtual network in Azure Stack and a virtual network in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f14b-107">You can use VPN gateways to send traffic securely between a virtual network in Azure Stack and a virtual network in Azure.</span></span> <span data-ttu-id="2f14b-108">You can also send traffic securely between a virtual network and another network that is connected to a VPN device.</span><span class="sxs-lookup"><span data-stu-id="2f14b-108">You can also send traffic securely between a virtual network and another network that is connected to a VPN device.</span></span>

<span data-ttu-id="2f14b-109">When you create a virtual network gateway, you specify the gateway type that you want to create.</span><span class="sxs-lookup"><span data-stu-id="2f14b-109">When you create a virtual network gateway, you specify the gateway type that you want to create.</span></span> <span data-ttu-id="2f14b-110">Azure Stack supports one type of virtual network gateway, the **Vpn** type.</span><span class="sxs-lookup"><span data-stu-id="2f14b-110">Azure Stack supports one type of virtual network gateway, the **Vpn** type.</span></span>

<span data-ttu-id="2f14b-111">Each virtual network can have two virtual network gateways, but only one of each type.</span><span class="sxs-lookup"><span data-stu-id="2f14b-111">Each virtual network can have two virtual network gateways, but only one of each type.</span></span> <span data-ttu-id="2f14b-112">Depending on the settings that you choose, you can create multiple connections to a single VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="2f14b-112">Depending on the settings that you choose, you can create multiple connections to a single VPN gateway.</span></span> <span data-ttu-id="2f14b-113">An example is a Multi-Site connection configuration.</span><span class="sxs-lookup"><span data-stu-id="2f14b-113">An example is a Multi-Site connection configuration.</span></span>

<span data-ttu-id="2f14b-114">Before you create and configure VPN Gateways for Azure Stack, review the [considerations for Azure Stack networking](/azure/azure-stack/user/azure-stack-network-differences) to learn how configurations for Azure Stack differ from Azure.</span><span class="sxs-lookup"><span data-stu-id="2f14b-114">Before you create and configure VPN Gateways for Azure Stack, review the [considerations for Azure Stack networking](/azure/azure-stack/user/azure-stack-network-differences) to learn how configurations for Azure Stack differ from Azure.</span></span>

>[!NOTE]
><span data-ttu-id="2f14b-115">In Azure, the bandwidth throughput for VPN gateway SKU you choose must be divided across all the Connections that are connected to the gateway.</span><span class="sxs-lookup"><span data-stu-id="2f14b-115">In Azure, the bandwidth throughput for VPN gateway SKU you choose must be divided across all the Connections that are connected to the gateway.</span></span> <span data-ttu-id="2f14b-116">But in Azure Stack, the bandwidth value for the VPN gateway SKU is applied to each Connection resource that is connected to the gateway.</span><span class="sxs-lookup"><span data-stu-id="2f14b-116">But in Azure Stack, the bandwidth value for the VPN gateway SKU is applied to each Connection resource that is connected to the gateway.</span></span>
>
> <span data-ttu-id="2f14b-117">For example:</span><span class="sxs-lookup"><span data-stu-id="2f14b-117">For example:</span></span>
> * <span data-ttu-id="2f14b-118">In Azure, the Basic VPN Gateway SKU can accommodate approximately 100 Mbps of aggregate throughput.</span><span class="sxs-lookup"><span data-stu-id="2f14b-118">In Azure, the Basic VPN Gateway SKU can accommodate approximately 100 Mbps of aggregate throughput.</span></span> <span data-ttu-id="2f14b-119">If you create two Connections to that VPN Gateway, and one connection is using 50 Mbps of bandwidth, then 50 Mbps is available to the other Connection.</span><span class="sxs-lookup"><span data-stu-id="2f14b-119">If you create two Connections to that VPN Gateway, and one connection is using 50 Mbps of bandwidth, then 50 Mbps is available to the other Connection.</span></span>
> * <span data-ttu-id="2f14b-120">In Azure Stack, *each* Connection to the Basic VPN Gateway SKU gets allocated 100 Mbps of throughput.</span><span class="sxs-lookup"><span data-stu-id="2f14b-120">In Azure Stack, *each* Connection to the Basic VPN Gateway SKU gets allocated 100 Mbps of throughput.</span></span>

## <a name="configuring-a-vpn-gateway"></a><span data-ttu-id="2f14b-121">Configuring a VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="2f14b-121">Configuring a VPN Gateway</span></span>

<span data-ttu-id="2f14b-122">A VPN gateway connection relies on several resources that are configured with specific settings.</span><span class="sxs-lookup"><span data-stu-id="2f14b-122">A VPN gateway connection relies on several resources that are configured with specific settings.</span></span> <span data-ttu-id="2f14b-123">Most of these resources can be configured separately, but in some cases they must be configured in a specific order.</span><span class="sxs-lookup"><span data-stu-id="2f14b-123">Most of these resources can be configured separately, but in some cases they must be configured in a specific order.</span></span>

### <a name="settings"></a><span data-ttu-id="2f14b-124">Settings</span><span class="sxs-lookup"><span data-stu-id="2f14b-124">Settings</span></span>

<span data-ttu-id="2f14b-125">The settings that you chose for each resource are critical for creating a successful connection.</span><span class="sxs-lookup"><span data-stu-id="2f14b-125">The settings that you chose for each resource are critical for creating a successful connection.</span></span>

<span data-ttu-id="2f14b-126">For information about individual resources and settings for a VPN gateway, see [About VPN gateway settings for Azure Stack](azure-stack-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="2f14b-126">For information about individual resources and settings for a VPN gateway, see [About VPN gateway settings for Azure Stack](azure-stack-vpn-gateway-settings.md).</span></span> <span data-ttu-id="2f14b-127">This article will help you understand:</span><span class="sxs-lookup"><span data-stu-id="2f14b-127">This article will help you understand:</span></span>

* <span data-ttu-id="2f14b-128">Gateway types, VPN types, and connection types.</span><span class="sxs-lookup"><span data-stu-id="2f14b-128">Gateway types, VPN types, and connection types.</span></span>
* <span data-ttu-id="2f14b-129">Gateway subnets, local network gateways, and other resource settings that you might want to consider.</span><span class="sxs-lookup"><span data-stu-id="2f14b-129">Gateway subnets, local network gateways, and other resource settings that you might want to consider.</span></span>

### <a name="deployment-tools"></a><span data-ttu-id="2f14b-130">Deployment tools</span><span class="sxs-lookup"><span data-stu-id="2f14b-130">Deployment tools</span></span>

<span data-ttu-id="2f14b-131">You can create and configure resources using one configuration tool, such as the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f14b-131">You can create and configure resources using one configuration tool, such as the Azure portal.</span></span> <span data-ttu-id="2f14b-132">Later you might switch to another tool like PowerShell to configure additional resources or modify existing resources when applicable.</span><span class="sxs-lookup"><span data-stu-id="2f14b-132">Later you might switch to another tool like PowerShell to configure additional resources or modify existing resources when applicable.</span></span> <span data-ttu-id="2f14b-133">Currently, you can't configure every resource and resource setting in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f14b-133">Currently, you can't configure every resource and resource setting in the Azure portal.</span></span> <span data-ttu-id="2f14b-134">The instructions in the articles for each connection topology specify when a specific configuration tool is needed.</span><span class="sxs-lookup"><span data-stu-id="2f14b-134">The instructions in the articles for each connection topology specify when a specific configuration tool is needed.</span></span>

## <a name="connection-topology-diagrams"></a><span data-ttu-id="2f14b-135">Connection topology diagrams</span><span class="sxs-lookup"><span data-stu-id="2f14b-135">Connection topology diagrams</span></span>

<span data-ttu-id="2f14b-136">It's important to know that there are different configurations available for VPN gateway connections.</span><span class="sxs-lookup"><span data-stu-id="2f14b-136">It's important to know that there are different configurations available for VPN gateway connections.</span></span> <span data-ttu-id="2f14b-137">Determine which configuration best fits your needs.</span><span class="sxs-lookup"><span data-stu-id="2f14b-137">Determine which configuration best fits your needs.</span></span> <span data-ttu-id="2f14b-138">In the following sections, you can view information and topology diagrams about the following VPN gateway connections:</span><span class="sxs-lookup"><span data-stu-id="2f14b-138">In the following sections, you can view information and topology diagrams about the following VPN gateway connections:</span></span>

* <span data-ttu-id="2f14b-139">Available deployment model</span><span class="sxs-lookup"><span data-stu-id="2f14b-139">Available deployment model</span></span>
* <span data-ttu-id="2f14b-140">Available configuration tools</span><span class="sxs-lookup"><span data-stu-id="2f14b-140">Available configuration tools</span></span>
* <span data-ttu-id="2f14b-141">Links that take you directly to an article, if available</span><span class="sxs-lookup"><span data-stu-id="2f14b-141">Links that take you directly to an article, if available</span></span>

<span data-ttu-id="2f14b-142">The diagrams and descriptions in the following sections can help you select a connection topology to match your requirements.</span><span class="sxs-lookup"><span data-stu-id="2f14b-142">The diagrams and descriptions in the following sections can help you select a connection topology to match your requirements.</span></span> <span data-ttu-id="2f14b-143">The diagrams show the main baseline topologies, but it's possible to build more complex configurations using the diagrams as a guide.</span><span class="sxs-lookup"><span data-stu-id="2f14b-143">The diagrams show the main baseline topologies, but it's possible to build more complex configurations using the diagrams as a guide.</span></span>

## <a name="site-to-site-and-multi-site-ipsecike-vpn-tunnel"></a><span data-ttu-id="2f14b-144">Site-to-Site and Multi-Site (IPsec/IKE VPN tunnel)</span><span class="sxs-lookup"><span data-stu-id="2f14b-144">Site-to-Site and Multi-Site (IPsec/IKE VPN tunnel)</span></span>

### <a name="site-to-site"></a><span data-ttu-id="2f14b-145">Site-to-Site</span><span class="sxs-lookup"><span data-stu-id="2f14b-145">Site-to-Site</span></span>

<span data-ttu-id="2f14b-146">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="2f14b-146">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="2f14b-147">This type of connection requires a VPN device that's located on-premises and is assigned a public IP address.</span><span class="sxs-lookup"><span data-stu-id="2f14b-147">This type of connection requires a VPN device that's located on-premises and is assigned a public IP address.</span></span> <span data-ttu-id="2f14b-148">This device can't be located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="2f14b-148">This device can't be located behind a NAT.</span></span> <span data-ttu-id="2f14b-149">S2S connections can be used for cross-premises and hybrid configurations.</span><span class="sxs-lookup"><span data-stu-id="2f14b-149">S2S connections can be used for cross-premises and hybrid configurations.</span></span>

![Site-to-site VPN connection configuration example](media/azure-stack-vpn-gateway-about-vpn-gateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="multi-site"></a><span data-ttu-id="2f14b-151">Multi-Site</span><span class="sxs-lookup"><span data-stu-id="2f14b-151">Multi-Site</span></span>

<span data-ttu-id="2f14b-152">This type of connection is a variation of the Site-to-Site connection.</span><span class="sxs-lookup"><span data-stu-id="2f14b-152">This type of connection is a variation of the Site-to-Site connection.</span></span> <span data-ttu-id="2f14b-153">You create more than one VPN connection from your virtual network gateway, typically connecting to multiple on-premises sites.</span><span class="sxs-lookup"><span data-stu-id="2f14b-153">You create more than one VPN connection from your virtual network gateway, typically connecting to multiple on-premises sites.</span></span> <span data-ttu-id="2f14b-154">When working with multiple connections, you must use a RouteBased VPN type (known as a dynamic gateway when working with classic VNets.) Because each virtual network can only have one VPN gateway, all connections through the gateway share the available bandwidth.</span><span class="sxs-lookup"><span data-stu-id="2f14b-154">When working with multiple connections, you must use a RouteBased VPN type (known as a dynamic gateway when working with classic VNets.) Because each virtual network can only have one VPN gateway, all connections through the gateway share the available bandwidth.</span></span> <span data-ttu-id="2f14b-155">This is often called a "multi-site" connection.</span><span class="sxs-lookup"><span data-stu-id="2f14b-155">This is often called a "multi-site" connection.</span></span>

![Azure VPN Gateway Multi-Site connection example](media/azure-stack-vpn-gateway-about-vpn-gateways/vpngateway-multisite-connection-diagram.png)

## <a name="gateway-skus"></a><span data-ttu-id="2f14b-157">Gateway SKUs</span><span class="sxs-lookup"><span data-stu-id="2f14b-157">Gateway SKUs</span></span>

<span data-ttu-id="2f14b-158">When you create a virtual network gateway for Azure Stack, you specify the gateway SKU that you want to use.</span><span class="sxs-lookup"><span data-stu-id="2f14b-158">When you create a virtual network gateway for Azure Stack, you specify the gateway SKU that you want to use.</span></span> <span data-ttu-id="2f14b-159">The following VPN gateway SKUs are supported:</span><span class="sxs-lookup"><span data-stu-id="2f14b-159">The following VPN gateway SKUs are supported:</span></span>

* <span data-ttu-id="2f14b-160">Basic</span><span class="sxs-lookup"><span data-stu-id="2f14b-160">Basic</span></span>
* <span data-ttu-id="2f14b-161">Standard</span><span class="sxs-lookup"><span data-stu-id="2f14b-161">Standard</span></span>
* <span data-ttu-id="2f14b-162">HighPerformance</span><span class="sxs-lookup"><span data-stu-id="2f14b-162">HighPerformance</span></span>

<span data-ttu-id="2f14b-163">When you select a higher gateway SKU, like Standard over Basic, or HighPerformance over Standard or Basic, more CPUs and network bandwidth are allocated to the gateway.</span><span class="sxs-lookup"><span data-stu-id="2f14b-163">When you select a higher gateway SKU, like Standard over Basic, or HighPerformance over Standard or Basic, more CPUs and network bandwidth are allocated to the gateway.</span></span> <span data-ttu-id="2f14b-164">As a result, the gateway can support higher network throughput to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="2f14b-164">As a result, the gateway can support higher network throughput to the virtual network.</span></span>

<span data-ttu-id="2f14b-165">Azure Stack does not support the UltraPerformance gateway SKU, which is used exclusively with Express Route.</span><span class="sxs-lookup"><span data-stu-id="2f14b-165">Azure Stack does not support the UltraPerformance gateway SKU, which is used exclusively with Express Route.</span></span>

<span data-ttu-id="2f14b-166">Consider the following when you select SKU:</span><span class="sxs-lookup"><span data-stu-id="2f14b-166">Consider the following when you select SKU:</span></span>

* <span data-ttu-id="2f14b-167">Azure Stack does not support Policy-based gateways.</span><span class="sxs-lookup"><span data-stu-id="2f14b-167">Azure Stack does not support Policy-based gateways.</span></span>
* <span data-ttu-id="2f14b-168">Border Gateway Protocol (BGP) is not supported on the Basic SKU.</span><span class="sxs-lookup"><span data-stu-id="2f14b-168">Border Gateway Protocol (BGP) is not supported on the Basic SKU.</span></span>
* <span data-ttu-id="2f14b-169">ExpressRoute-VPN Gateway coexist configurations are not supported in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2f14b-169">ExpressRoute-VPN Gateway coexist configurations are not supported in Azure Stack.</span></span>
* <span data-ttu-id="2f14b-170">Active-active S2S VPN Gateway connections can be configured on the HighPerformance SKU only.</span><span class="sxs-lookup"><span data-stu-id="2f14b-170">Active-active S2S VPN Gateway connections can be configured on the HighPerformance SKU only.</span></span>

## <a name="estimated-aggregate-throughput-by-sku"></a><span data-ttu-id="2f14b-171">Estimated aggregate throughput by SKU</span><span class="sxs-lookup"><span data-stu-id="2f14b-171">Estimated aggregate throughput by SKU</span></span>

<span data-ttu-id="2f14b-172">The following table shows the gateway types and the estimated aggregate throughput by gateway SKU.</span><span class="sxs-lookup"><span data-stu-id="2f14b-172">The following table shows the gateway types and the estimated aggregate throughput by gateway SKU.</span></span>

|   | <span data-ttu-id="2f14b-173">VPN Gateway throughput *(1)*</span><span class="sxs-lookup"><span data-stu-id="2f14b-173">VPN Gateway throughput *(1)*</span></span> | <span data-ttu-id="2f14b-174">VPN Gateway max IPsec tunnels *(2)*</span><span class="sxs-lookup"><span data-stu-id="2f14b-174">VPN Gateway max IPsec tunnels *(2)*</span></span> |
|-------|-------|-------|
|<span data-ttu-id="2f14b-175">**Basic SKU** ***(3)***</span><span class="sxs-lookup"><span data-stu-id="2f14b-175">**Basic SKU** ***(3)***</span></span>    | <span data-ttu-id="2f14b-176">100 Mbps</span><span class="sxs-lookup"><span data-stu-id="2f14b-176">100 Mbps</span></span>  | <span data-ttu-id="2f14b-177">10</span><span class="sxs-lookup"><span data-stu-id="2f14b-177">10</span></span>    |
|<span data-ttu-id="2f14b-178">**Standard SKU**</span><span class="sxs-lookup"><span data-stu-id="2f14b-178">**Standard SKU**</span></span>       | <span data-ttu-id="2f14b-179">100 Mbps</span><span class="sxs-lookup"><span data-stu-id="2f14b-179">100 Mbps</span></span>  | <span data-ttu-id="2f14b-180">10</span><span class="sxs-lookup"><span data-stu-id="2f14b-180">10</span></span>    |
|<span data-ttu-id="2f14b-181">**High-Performance SKU**</span><span class="sxs-lookup"><span data-stu-id="2f14b-181">**High-Performance SKU**</span></span> | <span data-ttu-id="2f14b-182">200 Mbps</span><span class="sxs-lookup"><span data-stu-id="2f14b-182">200 Mbps</span></span>    | <span data-ttu-id="2f14b-183">5</span><span class="sxs-lookup"><span data-stu-id="2f14b-183">5</span></span> |

<span data-ttu-id="2f14b-184">**Table notes:**</span><span class="sxs-lookup"><span data-stu-id="2f14b-184">**Table notes:**</span></span>

<span data-ttu-id="2f14b-185">*Note (1)* - VPN throughput isn't a guaranteed throughput for cross-premises connections across the Internet.</span><span class="sxs-lookup"><span data-stu-id="2f14b-185">*Note (1)* - VPN throughput isn't a guaranteed throughput for cross-premises connections across the Internet.</span></span> <span data-ttu-id="2f14b-186">It's the maximum possible throughput measurement.</span><span class="sxs-lookup"><span data-stu-id="2f14b-186">It's the maximum possible throughput measurement.</span></span>  
<span data-ttu-id="2f14b-187">*Note (2)* - Max tunnels is the total per Azure Stack deployment for ALL subscriptions.</span><span class="sxs-lookup"><span data-stu-id="2f14b-187">*Note (2)* - Max tunnels is the total per Azure Stack deployment for ALL subscriptions.</span></span>  
<span data-ttu-id="2f14b-188">*Note (3)* - BGP routing isn't supported for the Basic SKU.</span><span class="sxs-lookup"><span data-stu-id="2f14b-188">*Note (3)* - BGP routing isn't supported for the Basic SKU.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f14b-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f14b-189">Next steps</span></span>

[<span data-ttu-id="2f14b-190">VPN gateway configuration settings for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2f14b-190">VPN gateway configuration settings for Azure Stack</span></span>](azure-stack-vpn-gateway-settings.md)
