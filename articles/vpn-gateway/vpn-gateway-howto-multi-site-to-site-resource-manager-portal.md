---
title: 'Add multiple VPN gateway Site-to-Site connections to a VNet: Azure Portal: Resource Manager| Microsoft Docs'
description: Add multi-site S2S connections to a VPN gateway that has an existing connection
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: jpconnock
editor: ''
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/14/2018
ms.author: cherylmc
ms.openlocfilehash: 4e7d2acecfe94401d7ce3b608ad20857c2ba4061
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819018"
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a>Add a Site-to-Site connection to a VNet with an existing VPN gateway connection

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (classic)](vpn-gateway-multi-site.md)
>
> 

This article helps you add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection by using the Azure portal. This type of connection is often referred to as a "multi-site" configuration. You can add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection. There are some limitations when adding connections. Check the [Before you begin](#before) section in this article to verify before you start your configuration. 

This article applies to Resource Manager VNets that have a RouteBased VPN gateway. These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations. See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.

### <a name="deployment-models-and-methods"></a>Deployment models and methods
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

We update this table as new articles and additional tools become available for this configuration. When an article is available, we link directly to it from this table.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Before you begin
Verify the following items:

* You are not creating an ExpressRoute/S2S coexisting connection.
* You have a virtual network that was created using the Resource Manager deployment model with an existing connection.
* The virtual network gateway for your VNet is RouteBased. If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RouteBased.
* None of the address ranges overlap for any of the VNets that this VNet is connecting to.
* You have compatible VPN device and someone who is able to configure it. See [About VPN Devices](vpn-gateway-about-vpn-devices.md). If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.
* You have an externally facing public IP address for your VPN device. This IP address cannot be located behind a NAT.

## <a name="part1"></a>Part 1 - Configure a connection
1. From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.
2. Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.
3. On the **Virtual network gateway** page, click **Connections**.
   
    ![Connections page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections page")<br>
4. On the **Connections** page, click **+Add**.
   
    ![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")<br>
5. On the **Add connection** page, fill out the following fields:
   
   * **Name:** The name you want to give to the site you are creating the connection to.
   * **Connection type:** Select **Site-to-site (IPsec)**.
     
     ![Add connection page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection page")<br>

## <a name="part2"></a>Part 2 - Add a local network gateway
1. Click **Local network gateway** ***Choose a local network gateway***. This will open the **Choose local network gateway** page.
   
    ![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")<br>
2. Click **Create new** to open the **Create local network gateway** page.
   
    ![Create local network gateway page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")<br>
3. On the **Create local network gateway** page, fill out the following fields:
   
   * **Name:** The name you want to give to the local network gateway resource.
   * **IP address:** The public IP address of the VPN device on the site that you want to connect to.
   * **Address space:** The address space that you want to be routed to the new local network site.
4. Click **OK** on the **Create local network gateway** page to save the changes.

## <a name="part3"></a>Part 3 - Add the shared key and create the connection
1. On the **Add connection** page, add the shared key that you want to use to create your connection. You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key. The important thing is that the keys are exactly the same.
   
    ![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")<br>
2. At the bottom of the page, click **OK** to create the connection.

## <a name="part4"></a>Part 4 - Verify the VPN connection


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Next steps

Once your connection is complete, you can add virtual machines to your virtual networks. See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.
