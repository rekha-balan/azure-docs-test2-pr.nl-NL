---
title: 'Connect your on-premises network to an Azure virtual network: Site-to-Site VPN: Portal | Microsoft Docs'
description: Steps to create an IPsec connection from your on-premises network to an Azure virtual network over the public Internet. These steps will help you create a cross-premises Site-to-Site VPN Gateway connection using the portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 67a886ec215ea372e8f5ce67ed9abf060c1c6b92
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661559"
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a>Create a Site-to-Site connection in the Azure portal

A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel. This type of connection requires a VPN device located on-premises that has a public IP address assigned to it and is not located behind a NAT. Site-to-Site connections can be used for cross-premises and hybrid configurations.

![Site-to-Site VPN Gateway cross-premises connection diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

This article walks you through creating a virtual network and a Site-to-Site VPN gateway connection to your on-premises network using the Azure Resource Manager deployment model and the Azure portal. You can also create this configuration by using different deployment tools, or for the classic deployment model, by selecting a different option from the following list:

> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [Classic - Azure portal](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Classic - classic portal](vpn-gateway-site-to-site-create.md)
>
>


#### <a name="additional-configurations"></a>Additional configurations
If you want to connect VNets together, but are not creating a connection to an on-premises location, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md). If you want to add a Site-to-Site connection to a VNet that already has a connection, see [Add a S2S connection to a VNet with an existing VPN gateway connection](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).

## <a name="before-you-begin"></a>Before you begin

[!INCLUDE [deployment models](../../includes/vpn-gateway-deployment-models-include.md)]

Verify that you have the following items before beginning your configuration:

* A compatible VPN device and someone who is able to configure it. See [About VPN Devices](vpn-gateway-about-vpn-devices.md).
* If you aren't familiar with the IP address spaces located in your on-premises network, you need to coordinate with someone who can provide those details for you. Site-to-Site connections cannot have overlapping address spaces.
* An externally facing public IP address for your VPN device. This IP address cannot be located behind a NAT.
* An Azure subscription. If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](http://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](http://azure.microsoft.com/pricing/free-trial).

### <a name="values"></a>Example values
When using these steps as an exercise, you can use the following example values:

* **VNet Name:** TestVNet1
* **Address Space:** 
    * 10.11.0.0/16
    * 10.12.0.0/16 (optional for this exercise)
* **Subnets:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (optional for this exercise)
  * GatewaySubnet: 10.11.255.0/27
* **Resource Group:** TestRG1
* **Location:** East US
* **DNS Server:** The IP address of your DNS server
* **Virtual Network Gateway Name:** VNet1GW
* **Public IP:** VNet1GWIP
* **VPN Type:** Route-based
* **Connection Type:** Site-to-site (IPsec)
* **Gateway Type:** VPN
* **Local Network Gateway Name:** Site2
* **Connection Name:** VNet1toSite2

## <a name="CreatVNet"></a>1. Create a virtual network

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. Specify a DNS server
DNS is not required for Site-to-Site connections. However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server. This setting lets you specify the DNS server that you want to use for name resolution for this virtual network. It does not create a DNS server.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Create a gateway subnet
You must create a gateway subnet for your VPN gateway. The gateway subnet contains the IP addresses that the VPN gateway services use. If possible, create a gateway subnet using a CIDR block of /28 or /27. This will ensure that you have enough IP addresses to accommodate possible future gateway features.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Create a virtual network gateway

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Create a local network gateway
The local network gateway refers to your on-premises location. The settings that you specify for the local network gateway determine the address spaces that are routed to your on-premises VPN device.

[!INCLUDE [vpn-gateway-add-lng-s2s-rm-portal](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. Configure your VPN device
[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Create a Site-to-Site VPN connection

In this step, you create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device. Before beginning this section, verify that your virtual network gateway and local network gateways have finished creating.

[!INCLUDE [vpn-gateway-add-site-to-site-connection-rm-portal](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Verify the VPN connection

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="next-steps"></a>Next steps
*  Once your connection is complete, you can add virtual machines to your virtual networks. For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
*  For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).


