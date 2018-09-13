---
title: include file
description: include file
services: virtual-wan
author: cherylmc
ms.service: virtual-wan
ms.topic: include
ms.date: 07/18/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: d059cab5668eef8d4dafc1442ca9749a7dcf8c9d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864986"
---
### <a name="what-is-the-difference-between-an-azure-virtual-network-gateway-vpn-gateway-and-an-azure-virtual-wan-vpngateway"></a><span data-ttu-id="51540-103">What is the difference between an Azure virtual network gateway (VPN Gateway) and an Azure Virtual WAN vpngateway?</span><span class="sxs-lookup"><span data-stu-id="51540-103">What is the difference between an Azure virtual network gateway (VPN Gateway) and an Azure Virtual WAN vpngateway?</span></span>

<span data-ttu-id="51540-104">Virtual WAN provides large-scale Site-to-Site connectivity and is built for throughput, scalability, and ease of use.</span><span class="sxs-lookup"><span data-stu-id="51540-104">Virtual WAN provides large-scale Site-to-Site connectivity and is built for throughput, scalability, and ease of use.</span></span> <span data-ttu-id="51540-105">CPE branch devices auto-provision and connect into Azure Virtual WAN.</span><span class="sxs-lookup"><span data-stu-id="51540-105">CPE branch devices auto-provision and connect into Azure Virtual WAN.</span></span> <span data-ttu-id="51540-106">These devices are available from a growing ecosystem of SD-WAN and VPN partners.</span><span class="sxs-lookup"><span data-stu-id="51540-106">These devices are available from a growing ecosystem of SD-WAN and VPN partners.</span></span>

### <a name="which-device-providers-virtual-wan-partners-are-supported-at-launch-time"></a><span data-ttu-id="51540-107">Which device providers (Virtual WAN partners) are supported at launch time?</span><span class="sxs-lookup"><span data-stu-id="51540-107">Which device providers (Virtual WAN partners) are supported at launch time?</span></span> 

<span data-ttu-id="51540-108">At this time, Citrix and Riverbed support the fully automated Virtual WAN experience.</span><span class="sxs-lookup"><span data-stu-id="51540-108">At this time, Citrix and Riverbed support the fully automated Virtual WAN experience.</span></span> <span data-ttu-id="51540-109">For more information, see [Virtual WAN partners](https://aka.ms/virtualwan).</span><span class="sxs-lookup"><span data-stu-id="51540-109">For more information, see [Virtual WAN partners](https://aka.ms/virtualwan).</span></span>

### <a name="am-i-required-to-use-a-preferred-partner-device"></a><span data-ttu-id="51540-110">Am I required to use a preferred partner device?</span><span class="sxs-lookup"><span data-stu-id="51540-110">Am I required to use a preferred partner device?</span></span>

<span data-ttu-id="51540-111">No.</span><span class="sxs-lookup"><span data-stu-id="51540-111">No.</span></span> <span data-ttu-id="51540-112">You can use any VPN-capable device that adheres to the Preview requirements for IKEv2 IPsec support.</span><span class="sxs-lookup"><span data-stu-id="51540-112">You can use any VPN-capable device that adheres to the Preview requirements for IKEv2 IPsec support.</span></span>

### <a name="how-do-virtual-wan-partners-automate-connectivity-with-azure-virtual-wan"></a><span data-ttu-id="51540-113">How do Virtual WAN partners automate connectivity with Azure Virtual WAN?</span><span class="sxs-lookup"><span data-stu-id="51540-113">How do Virtual WAN partners automate connectivity with Azure Virtual WAN?</span></span>

<span data-ttu-id="51540-114">Software-defined connectivity solutions typically manage their branch devices using a controller, or a device provisioning center.</span><span class="sxs-lookup"><span data-stu-id="51540-114">Software-defined connectivity solutions typically manage their branch devices using a controller, or a device provisioning center.</span></span> <span data-ttu-id="51540-115">The controller can use Azure APIs to automate connectivity to the Azure Virtual WAN.</span><span class="sxs-lookup"><span data-stu-id="51540-115">The controller can use Azure APIs to automate connectivity to the Azure Virtual WAN.</span></span> <span data-ttu-id="51540-116">For more information, see [Virtual WAN partner automation](../articles/virtual-wan/virtual-wan-configure-automation-providers.md).</span><span class="sxs-lookup"><span data-stu-id="51540-116">For more information, see [Virtual WAN partner automation](../articles/virtual-wan/virtual-wan-configure-automation-providers.md).</span></span>

### <a name="does-virtual-wan-change-any-existing-connectivity-features"></a><span data-ttu-id="51540-117">Does Virtual WAN change any existing connectivity features?</span><span class="sxs-lookup"><span data-stu-id="51540-117">Does Virtual WAN change any existing connectivity features?</span></span>   

<span data-ttu-id="51540-118">There are no changes to existing Azure connectivity features.</span><span class="sxs-lookup"><span data-stu-id="51540-118">There are no changes to existing Azure connectivity features.</span></span>

### <a name="are-there-new-resource-manager-resources-available-for-virtual-wan"></a><span data-ttu-id="51540-119">Are there new Resource Manager resources available for Virtual WAN?</span><span class="sxs-lookup"><span data-stu-id="51540-119">Are there new Resource Manager resources available for Virtual WAN?</span></span>
  
<span data-ttu-id="51540-120">Yes, Virtual WAN introduces new Resource Manager resources.</span><span class="sxs-lookup"><span data-stu-id="51540-120">Yes, Virtual WAN introduces new Resource Manager resources.</span></span> <span data-ttu-id="51540-121">For more information, please see the [Overview](https://go.microsoft.com/fwlink/p/?LinkId=2004389).</span><span class="sxs-lookup"><span data-stu-id="51540-121">For more information, please see the [Overview](https://go.microsoft.com/fwlink/p/?LinkId=2004389).</span></span>

### <a name="are-there-any-special-requirements-to-join-the-preview"></a><span data-ttu-id="51540-122">Are there any special requirements to join the Preview?</span><span class="sxs-lookup"><span data-stu-id="51540-122">Are there any special requirements to join the Preview?</span></span> 

<span data-ttu-id="51540-123">Before you can configure an Azure Virtual WAN, you must first enroll your subscription in the Preview.</span><span class="sxs-lookup"><span data-stu-id="51540-123">Before you can configure an Azure Virtual WAN, you must first enroll your subscription in the Preview.</span></span> <span data-ttu-id="51540-124">To enroll, send an email to <azurevirtualwan@microsoft.com> with your subscription ID.</span><span class="sxs-lookup"><span data-stu-id="51540-124">To enroll, send an email to <azurevirtualwan@microsoft.com> with your subscription ID.</span></span> <span data-ttu-id="51540-125">You will receive an email back once your subscription has been enrolled.</span><span class="sxs-lookup"><span data-stu-id="51540-125">You will receive an email back once your subscription has been enrolled.</span></span> <span data-ttu-id="51540-126">Until you receive confirmation that your subscription has been enrolled, you will not be able to work with Virtual WAN in the portal.</span><span class="sxs-lookup"><span data-stu-id="51540-126">Until you receive confirmation that your subscription has been enrolled, you will not be able to work with Virtual WAN in the portal.</span></span>

<span data-ttu-id="51540-127">Considerations:</span><span class="sxs-lookup"><span data-stu-id="51540-127">Considerations:</span></span>

* <span data-ttu-id="51540-128">The Preview is limited to Azure public regions only.</span><span class="sxs-lookup"><span data-stu-id="51540-128">The Preview is limited to Azure public regions only.</span></span>
* <span data-ttu-id="51540-129">Up to 100 connections are supported per virtual hub.</span><span class="sxs-lookup"><span data-stu-id="51540-129">Up to 100 connections are supported per virtual hub.</span></span> <span data-ttu-id="51540-130">Each connection consists of two tunnels that are in an active-active configuration.</span><span class="sxs-lookup"><span data-stu-id="51540-130">Each connection consists of two tunnels that are in an active-active configuration.</span></span> <span data-ttu-id="51540-131">The tunnels terminate in an Azure Virtual Hub vpngateway.</span><span class="sxs-lookup"><span data-stu-id="51540-131">The tunnels terminate in an Azure Virtual Hub vpngateway.</span></span>
* <span data-ttu-id="51540-132">Consider using this Preview if:</span><span class="sxs-lookup"><span data-stu-id="51540-132">Consider using this Preview if:</span></span>
  * <span data-ttu-id="51540-133">You want to deploy aggregated bandwidth less than 1 Gbps per virtual hub.</span><span class="sxs-lookup"><span data-stu-id="51540-133">You want to deploy aggregated bandwidth less than 1 Gbps per virtual hub.</span></span>
  * <span data-ttu-id="51540-134">You have a VPN device that supports route-based configuration and IKEv2 IPsec connectivity.</span><span class="sxs-lookup"><span data-stu-id="51540-134">You have a VPN device that supports route-based configuration and IKEv2 IPsec connectivity.</span></span>
  * <span data-ttu-id="51540-135">You want to explore using SD-WAN and operating branch devices from the launch partners (Riverbed and Citrix).</span><span class="sxs-lookup"><span data-stu-id="51540-135">You want to explore using SD-WAN and operating branch devices from the launch partners (Riverbed and Citrix).</span></span><br><span data-ttu-id="51540-136">or</span><span class="sxs-lookup"><span data-stu-id="51540-136">or</span></span><br><span data-ttu-id="51540-137">You want to set up branch-to-branch and branch to Azure connectivity that includes configuration management of your on-premises device.</span><span class="sxs-lookup"><span data-stu-id="51540-137">You want to set up branch-to-branch and branch to Azure connectivity that includes configuration management of your on-premises device.</span></span> <span data-ttu-id="51540-138">(Self-configure)</span><span class="sxs-lookup"><span data-stu-id="51540-138">(Self-configure)</span></span>

### <a name="is-global-vnet-peering-supported-with-azure-virtual-wan"></a><span data-ttu-id="51540-139">Is Global VNet peering supported with Azure Virtual WAN?</span><span class="sxs-lookup"><span data-stu-id="51540-139">Is Global VNet peering supported with Azure Virtual WAN?</span></span> 

 <span data-ttu-id="51540-140">No.</span><span class="sxs-lookup"><span data-stu-id="51540-140">No.</span></span>

### <a name="can-spoke-vnets-connected-to-a-virtual-hub-communicate-with-each-other"></a><span data-ttu-id="51540-141">Can spoke VNets connected to a virtual hub communicate with each other?</span><span class="sxs-lookup"><span data-stu-id="51540-141">Can spoke VNets connected to a virtual hub communicate with each other?</span></span>

<span data-ttu-id="51540-142">Yes.</span><span class="sxs-lookup"><span data-stu-id="51540-142">Yes.</span></span> <span data-ttu-id="51540-143">You can directly do VNet peering between spokes that are connected to a virtual hub.</span><span class="sxs-lookup"><span data-stu-id="51540-143">You can directly do VNet peering between spokes that are connected to a virtual hub.</span></span> <span data-ttu-id="51540-144">For more information, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51540-144">For more information, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md).</span></span>

### <a name="can-i-deploy-and-use-my-favorite-network-virtual-appliance-in-an-nva-vnet-with-azure-virtual-wan"></a><span data-ttu-id="51540-145">Can I deploy and use my favorite network virtual appliance (in an NVA VNet) with Azure Virtual WAN?</span><span class="sxs-lookup"><span data-stu-id="51540-145">Can I deploy and use my favorite network virtual appliance (in an NVA VNet) with Azure Virtual WAN?</span></span>

<span data-ttu-id="51540-146">Yes, you can connect your favorite network virtual appliance (NVA) VNet to the Azure Virtual WAN, but will require routing capabilities in the hub, which is on our roadmap.</span><span class="sxs-lookup"><span data-stu-id="51540-146">Yes, you can connect your favorite network virtual appliance (NVA) VNet to the Azure Virtual WAN, but will require routing capabilities in the hub, which is on our roadmap.</span></span> <span data-ttu-id="51540-147">All spokes connected to the NVA VNet must additionally be connected to the virtual hub.</span><span class="sxs-lookup"><span data-stu-id="51540-147">All spokes connected to the NVA VNet must additionally be connected to the virtual hub.</span></span> 

### <a name="can-an-nva-vnet-have-a-virtual-network-gateway"></a><span data-ttu-id="51540-148">Can an NVA VNet have a virtual network gateway?</span><span class="sxs-lookup"><span data-stu-id="51540-148">Can an NVA VNet have a virtual network gateway?</span></span>

<span data-ttu-id="51540-149">No.</span><span class="sxs-lookup"><span data-stu-id="51540-149">No.</span></span> <span data-ttu-id="51540-150">The NVA VNet cannot have a virtual network gateway if it is connected to the virtual hub.</span><span class="sxs-lookup"><span data-stu-id="51540-150">The NVA VNet cannot have a virtual network gateway if it is connected to the virtual hub.</span></span> 

### <a name="is-there-support-for-bgp"></a><span data-ttu-id="51540-151">Is there support for BGP?</span><span class="sxs-lookup"><span data-stu-id="51540-151">Is there support for BGP?</span></span>

<span data-ttu-id="51540-152">Yes, BGP is supported.</span><span class="sxs-lookup"><span data-stu-id="51540-152">Yes, BGP is supported.</span></span> <span data-ttu-id="51540-153">To ensure that routes from an NVA VNet are advertised appropriately, spokes must disable BGP if they are connected to an NVA VNet which, in turn, is connected to a virtual hub.</span><span class="sxs-lookup"><span data-stu-id="51540-153">To ensure that routes from an NVA VNet are advertised appropriately, spokes must disable BGP if they are connected to an NVA VNet which, in turn, is connected to a virtual hub.</span></span> <span data-ttu-id="51540-154">Additionally, connect the spoke VNets to the virtual hub.</span><span class="sxs-lookup"><span data-stu-id="51540-154">Additionally, connect the spoke VNets to the virtual hub.</span></span>

### <a name="can-i-direct-traffic-using-udr-in-the-virtual-hub"></a><span data-ttu-id="51540-155">Can I direct traffic using UDR in the virtual hub?</span><span class="sxs-lookup"><span data-stu-id="51540-155">Can I direct traffic using UDR in the virtual hub?</span></span>

<span data-ttu-id="51540-156">This is on our roadmap.</span><span class="sxs-lookup"><span data-stu-id="51540-156">This is on our roadmap.</span></span> <span data-ttu-id="51540-157">Stay tuned!</span><span class="sxs-lookup"><span data-stu-id="51540-157">Stay tuned!</span></span>

### <a name="is-there-any-licensing-or-pricing-information-for-virtual-wan"></a><span data-ttu-id="51540-158">Is there any licensing or pricing information for Virtual WAN?</span><span class="sxs-lookup"><span data-stu-id="51540-158">Is there any licensing or pricing information for Virtual WAN?</span></span>
 
<span data-ttu-id="51540-159">There is no additional charge during Preview.</span><span class="sxs-lookup"><span data-stu-id="51540-159">There is no additional charge during Preview.</span></span> <span data-ttu-id="51540-160">Current [Azure VPN and egress pricing](https://azure.microsoft.com/pricing/details/vpn-gateway/) remains in effect during Preview.</span><span class="sxs-lookup"><span data-stu-id="51540-160">Current [Azure VPN and egress pricing](https://azure.microsoft.com/pricing/details/vpn-gateway/) remains in effect during Preview.</span></span>

### <a name="how-do-new-partners-that-are-not-listed-in-your-launch-partner-list-get-onboarded"></a><span data-ttu-id="51540-161">How do new partners that are not listed in your launch partner list get onboarded?</span><span class="sxs-lookup"><span data-stu-id="51540-161">How do new partners that are not listed in your launch partner list get onboarded?</span></span>

<span data-ttu-id="51540-162">Send an email to azurevirtualwan@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="51540-162">Send an email to azurevirtualwan@microsoft.com.</span></span> <span data-ttu-id="51540-163">An ideal partner is one that has a device that can be provisioned for IKEv2 IPSec connectivity.</span><span class="sxs-lookup"><span data-stu-id="51540-163">An ideal partner is one that has a device that can be provisioned for IKEv2 IPSec connectivity.</span></span>

### <a name="is-it-possible-to-construct-azure-virtual-wan-with-a-resource-manager-template"></a><span data-ttu-id="51540-164">Is it possible to construct Azure Virtual WAN with a Resource Manager template?</span><span class="sxs-lookup"><span data-stu-id="51540-164">Is it possible to construct Azure Virtual WAN with a Resource Manager template?</span></span>

<span data-ttu-id="51540-165">We are working on it.</span><span class="sxs-lookup"><span data-stu-id="51540-165">We are working on it.</span></span> <span data-ttu-id="51540-166">At the moment, the service is REST and Portal driven.</span><span class="sxs-lookup"><span data-stu-id="51540-166">At the moment, the service is REST and Portal driven.</span></span>

### <a name="is-branch-to-branch-connectivity-allowed-in-virtual-wan"></a><span data-ttu-id="51540-167">Is branch-to-branch connectivity allowed in Virtual WAN?</span><span class="sxs-lookup"><span data-stu-id="51540-167">Is branch-to-branch connectivity allowed in Virtual WAN?</span></span>

<span data-ttu-id="51540-168">Yes, branch-to-branch connectivity is available in Virtual WAN.</span><span class="sxs-lookup"><span data-stu-id="51540-168">Yes, branch-to-branch connectivity is available in Virtual WAN.</span></span>

### <a name="does-branch-to-branch-traffic-traverse-through-the-azure-virtual-wan"></a><span data-ttu-id="51540-169">Does Branch to Branch traffic traverse through the Azure Virtual WAN?</span><span class="sxs-lookup"><span data-stu-id="51540-169">Does Branch to Branch traffic traverse through the Azure Virtual WAN?</span></span>

<span data-ttu-id="51540-170">Yes.</span><span class="sxs-lookup"><span data-stu-id="51540-170">Yes.</span></span>

### <a name="how-is-virtual-wan-different-from-the-existing-azure-virtual-network-gateway"></a><span data-ttu-id="51540-171">How is Virtual WAN different from the existing Azure Virtual Network Gateway?</span><span class="sxs-lookup"><span data-stu-id="51540-171">How is Virtual WAN different from the existing Azure Virtual Network Gateway?</span></span>

<span data-ttu-id="51540-172">Virtual Network Gateway VPN is limited to 30 tunnels.</span><span class="sxs-lookup"><span data-stu-id="51540-172">Virtual Network Gateway VPN is limited to 30 tunnels.</span></span> <span data-ttu-id="51540-173">For connections, you should use Virtual WAN for large-scale VPN.</span><span class="sxs-lookup"><span data-stu-id="51540-173">For connections, you should use Virtual WAN for large-scale VPN.</span></span> <span data-ttu-id="51540-174">In public preview, this is limited to 100 branch connections with 1 Gbps in the hub.</span><span class="sxs-lookup"><span data-stu-id="51540-174">In public preview, this is limited to 100 branch connections with 1 Gbps in the hub.</span></span>

### <a name="does-this-virtual-wan-require-expressroute-from-each-site"></a><span data-ttu-id="51540-175">Does this Virtual WAN require ExpressRoute from each site?</span><span class="sxs-lookup"><span data-stu-id="51540-175">Does this Virtual WAN require ExpressRoute from each site?</span></span>

<span data-ttu-id="51540-176">No, the Virtual WAN does not require ExpressRoute from each site.</span><span class="sxs-lookup"><span data-stu-id="51540-176">No, the Virtual WAN does not require ExpressRoute from each site.</span></span> <span data-ttu-id="51540-177">It uses standard IPsec site-to-site connectivity via Internet links from the device to an Azure Virtual WAN hub.</span><span class="sxs-lookup"><span data-stu-id="51540-177">It uses standard IPsec site-to-site connectivity via Internet links from the device to an Azure Virtual WAN hub.</span></span>

### <a name="is-there-a-network-throughput-limit-when-using-azure-virtual-wan"></a><span data-ttu-id="51540-178">Is there a network throughput limit when using Azure Virtual WAN?</span><span class="sxs-lookup"><span data-stu-id="51540-178">Is there a network throughput limit when using Azure Virtual WAN?</span></span>

<span data-ttu-id="51540-179">In public preview, number of branches is limited to 100 connections per hub/region and a total of 1 G in the hub.</span><span class="sxs-lookup"><span data-stu-id="51540-179">In public preview, number of branches is limited to 100 connections per hub/region and a total of 1 G in the hub.</span></span>

### <a name="does-virtual-wan-allow-the-on-premises-device-to-utilize-multiple-isps-in-parallel-or-is-it-always-a-single-vpn-tunnel"></a><span data-ttu-id="51540-180">Does Virtual WAN allow the on-premises device to utilize multiple ISPs in parallel or is it always a single VPN tunnel?</span><span class="sxs-lookup"><span data-stu-id="51540-180">Does Virtual WAN allow the on-premises device to utilize multiple ISPs in parallel or is it always a single VPN tunnel?</span></span>

<span data-ttu-id="51540-181">Yes, you can have active-active tunnels (2 tunnels = 1 Azure Virtual WAN connection) from a single branch depending on the branch device.</span><span class="sxs-lookup"><span data-stu-id="51540-181">Yes, you can have active-active tunnels (2 tunnels = 1 Azure Virtual WAN connection) from a single branch depending on the branch device.</span></span>

### <a name="how-is-traffic-is-routed-on-the-azure-backbone"></a><span data-ttu-id="51540-182">How is traffic is routed on the Azure backbone?</span><span class="sxs-lookup"><span data-stu-id="51540-182">How is traffic is routed on the Azure backbone?</span></span>

<span data-ttu-id="51540-183">The traffic follows the pattern: branch device ->ISP->Microsoft Edge->Microsoft DC->Microsoft edge->ISP->branch device.</span><span class="sxs-lookup"><span data-stu-id="51540-183">The traffic follows the pattern: branch device ->ISP->Microsoft Edge->Microsoft DC->Microsoft edge->ISP->branch device.</span></span>

### <a name="in-this-model-what-do-you-need-at-each-site-just-an-internet-connection"></a><span data-ttu-id="51540-184">In this model, what do you need at each site?</span><span class="sxs-lookup"><span data-stu-id="51540-184">In this model, what do you need at each site?</span></span> <span data-ttu-id="51540-185">Just an internet connection?</span><span class="sxs-lookup"><span data-stu-id="51540-185">Just an internet connection?</span></span>

<span data-ttu-id="51540-186">Yes.</span><span class="sxs-lookup"><span data-stu-id="51540-186">Yes.</span></span> <span data-ttu-id="51540-187">An Internet connection and physical device, preferably from our integrated partners.</span><span class="sxs-lookup"><span data-stu-id="51540-187">An Internet connection and physical device, preferably from our integrated partners.</span></span> <span data-ttu-id="51540-188">Unless you want to manually manage the configuration and connectivity to Azure from your preferred device.</span><span class="sxs-lookup"><span data-stu-id="51540-188">Unless you want to manually manage the configuration and connectivity to Azure from your preferred device.</span></span>