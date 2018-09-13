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
### <a name="what-is-the-difference-between-an-azure-virtual-network-gateway-vpn-gateway-and-an-azure-virtual-wan-vpngateway"></a>What is the difference between an Azure virtual network gateway (VPN Gateway) and an Azure Virtual WAN vpngateway?

Virtual WAN provides large-scale Site-to-Site connectivity and is built for throughput, scalability, and ease of use. CPE branch devices auto-provision and connect into Azure Virtual WAN. These devices are available from a growing ecosystem of SD-WAN and VPN partners.

### <a name="which-device-providers-virtual-wan-partners-are-supported-at-launch-time"></a>Which device providers (Virtual WAN partners) are supported at launch time? 

At this time, Citrix and Riverbed support the fully automated Virtual WAN experience. For more information, see [Virtual WAN partners](https://aka.ms/virtualwan).

### <a name="am-i-required-to-use-a-preferred-partner-device"></a>Am I required to use a preferred partner device?

No. You can use any VPN-capable device that adheres to the Preview requirements for IKEv2 IPsec support.

### <a name="how-do-virtual-wan-partners-automate-connectivity-with-azure-virtual-wan"></a>How do Virtual WAN partners automate connectivity with Azure Virtual WAN?

Software-defined connectivity solutions typically manage their branch devices using a controller, or a device provisioning center. The controller can use Azure APIs to automate connectivity to the Azure Virtual WAN. For more information, see [Virtual WAN partner automation](../articles/virtual-wan/virtual-wan-configure-automation-providers.md).

### <a name="does-virtual-wan-change-any-existing-connectivity-features"></a>Does Virtual WAN change any existing connectivity features?   

There are no changes to existing Azure connectivity features.

### <a name="are-there-new-resource-manager-resources-available-for-virtual-wan"></a>Are there new Resource Manager resources available for Virtual WAN?
  
Yes, Virtual WAN introduces new Resource Manager resources. For more information, please see the [Overview](https://go.microsoft.com/fwlink/p/?LinkId=2004389).

### <a name="are-there-any-special-requirements-to-join-the-preview"></a>Are there any special requirements to join the Preview? 

Before you can configure an Azure Virtual WAN, you must first enroll your subscription in the Preview. To enroll, send an email to <azurevirtualwan@microsoft.com> with your subscription ID. You will receive an email back once your subscription has been enrolled. Until you receive confirmation that your subscription has been enrolled, you will not be able to work with Virtual WAN in the portal.

Considerations:

* The Preview is limited to Azure public regions only.
* Up to 100 connections are supported per virtual hub. Each connection consists of two tunnels that are in an active-active configuration. The tunnels terminate in an Azure Virtual Hub vpngateway.
* Consider using this Preview if:
  * You want to deploy aggregated bandwidth less than 1 Gbps per virtual hub.
  * You have a VPN device that supports route-based configuration and IKEv2 IPsec connectivity.
  * You want to explore using SD-WAN and operating branch devices from the launch partners (Riverbed and Citrix).<br>or<br>You want to set up branch-to-branch and branch to Azure connectivity that includes configuration management of your on-premises device. (Self-configure)

### <a name="is-global-vnet-peering-supported-with-azure-virtual-wan"></a>Is Global VNet peering supported with Azure Virtual WAN? 

 No.

### <a name="can-spoke-vnets-connected-to-a-virtual-hub-communicate-with-each-other"></a>Can spoke VNets connected to a virtual hub communicate with each other?

Yes. You can directly do VNet peering between spokes that are connected to a virtual hub. For more information, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md).

### <a name="can-i-deploy-and-use-my-favorite-network-virtual-appliance-in-an-nva-vnet-with-azure-virtual-wan"></a>Can I deploy and use my favorite network virtual appliance (in an NVA VNet) with Azure Virtual WAN?

Yes, you can connect your favorite network virtual appliance (NVA) VNet to the Azure Virtual WAN, but will require routing capabilities in the hub, which is on our roadmap. All spokes connected to the NVA VNet must additionally be connected to the virtual hub. 

### <a name="can-an-nva-vnet-have-a-virtual-network-gateway"></a>Can an NVA VNet have a virtual network gateway?

No. The NVA VNet cannot have a virtual network gateway if it is connected to the virtual hub. 

### <a name="is-there-support-for-bgp"></a>Is there support for BGP?

Yes, BGP is supported. To ensure that routes from an NVA VNet are advertised appropriately, spokes must disable BGP if they are connected to an NVA VNet which, in turn, is connected to a virtual hub. Additionally, connect the spoke VNets to the virtual hub.

### <a name="can-i-direct-traffic-using-udr-in-the-virtual-hub"></a>Can I direct traffic using UDR in the virtual hub?

This is on our roadmap. Stay tuned!

### <a name="is-there-any-licensing-or-pricing-information-for-virtual-wan"></a>Is there any licensing or pricing information for Virtual WAN?
 
There is no additional charge during Preview. Current [Azure VPN and egress pricing](https://azure.microsoft.com/pricing/details/vpn-gateway/) remains in effect during Preview.

### <a name="how-do-new-partners-that-are-not-listed-in-your-launch-partner-list-get-onboarded"></a>How do new partners that are not listed in your launch partner list get onboarded?

Send an email to azurevirtualwan@microsoft.com. An ideal partner is one that has a device that can be provisioned for IKEv2 IPSec connectivity.

### <a name="is-it-possible-to-construct-azure-virtual-wan-with-a-resource-manager-template"></a>Is it possible to construct Azure Virtual WAN with a Resource Manager template?

We are working on it. At the moment, the service is REST and Portal driven.

### <a name="is-branch-to-branch-connectivity-allowed-in-virtual-wan"></a>Is branch-to-branch connectivity allowed in Virtual WAN?

Yes, branch-to-branch connectivity is available in Virtual WAN.

### <a name="does-branch-to-branch-traffic-traverse-through-the-azure-virtual-wan"></a>Does Branch to Branch traffic traverse through the Azure Virtual WAN?

Yes.

### <a name="how-is-virtual-wan-different-from-the-existing-azure-virtual-network-gateway"></a>How is Virtual WAN different from the existing Azure Virtual Network Gateway?

Virtual Network Gateway VPN is limited to 30 tunnels. For connections, you should use Virtual WAN for large-scale VPN. In public preview, this is limited to 100 branch connections with 1 Gbps in the hub.

### <a name="does-this-virtual-wan-require-expressroute-from-each-site"></a>Does this Virtual WAN require ExpressRoute from each site?

No, the Virtual WAN does not require ExpressRoute from each site. It uses standard IPsec site-to-site connectivity via Internet links from the device to an Azure Virtual WAN hub.

### <a name="is-there-a-network-throughput-limit-when-using-azure-virtual-wan"></a>Is there a network throughput limit when using Azure Virtual WAN?

In public preview, number of branches is limited to 100 connections per hub/region and a total of 1 G in the hub.

### <a name="does-virtual-wan-allow-the-on-premises-device-to-utilize-multiple-isps-in-parallel-or-is-it-always-a-single-vpn-tunnel"></a>Does Virtual WAN allow the on-premises device to utilize multiple ISPs in parallel or is it always a single VPN tunnel?

Yes, you can have active-active tunnels (2 tunnels = 1 Azure Virtual WAN connection) from a single branch depending on the branch device.

### <a name="how-is-traffic-is-routed-on-the-azure-backbone"></a>How is traffic is routed on the Azure backbone?

The traffic follows the pattern: branch device ->ISP->Microsoft Edge->Microsoft DC->Microsoft edge->ISP->branch device.

### <a name="in-this-model-what-do-you-need-at-each-site-just-an-internet-connection"></a>In this model, what do you need at each site? Just an internet connection?

Yes. An Internet connection and physical device, preferably from our integrated partners. Unless you want to manually manage the configuration and connectivity to Azure from your preferred device.