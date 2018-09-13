---
title: 'Delete a virtual network gateway: Azure portal: Resource Manager | Microsoft Docs'
description: Delete a virtual network gateway using PowerShell in the Resource Manager deployment model.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: vpn-gateway
ms.devlang: na
ms.topic: ''
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: cherylmc
ms.openlocfilehash: 2944259927cd7806dbdebf8e2cf6a9708f11bcd5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553359"
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a>Delete a virtual network gateway using the portal
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-delete-vnet-gateway-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [Classic - PowerShell](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.

- If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group. When you delete a resource group, it deletes all the resources within the group. This is method is only recommended if you don't want to keep any of the resources in the resource group. You can't selectively delete only a few resources using this approach.

- If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated. Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway. The steps you follow depend on the type of connections that you created and the dependent resources for each connection.

##<a name="deletegw"></a>Delete a VPN gateway

To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway. Resources must be deleted in a certain order due to dependencies.

###<a name="step-1-navigate-to-the-virtual-network-gateway"></a>Step 1: Navigate to the virtual network gateway

In the [Azure portal](https://portal.azure.com), in **All resources**, click the virtual network gateway that you want to delete. The graphic for a gateway is:

![Locate virtual network gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-delete-vnet-gateway-portal/gw.png)

###<a name="step-2-delete-connections"></a>Step 2: Delete connections

1. On the blade for your virtual network gateway, click **Connections** to view all connections to the gateway.
2. Click the **...** on the row of the name of the connection, then select **Delete** from the dropdown.
3. Click **Yes** to confirm that you want to delete the connection. If you have multiple connections, delete each connection.

###<a name="step-3-delete-the-local-network-gateways"></a>Step 3: Delete the local network gateways
1. In **All resources**, locate the local network gateways that were associated with each connection. The graphic for a local network gateway is:

    ![Locate local network gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-delete-vnet-gateway-portal/lng.png)
2. On the **Overview** blade for the local network gateway, click **Delete**.

###<a name="step-4-delete-the-virtual-network-gateway"></a>Step 4: Delete the virtual network gateway
1. In **All resources**, locate the virtual network gateway that you want to delete.
2. On the **Overview** blade, click **Delete** to delete the gateway.

>[!NOTE]
> If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.
>
>

###<a name="step-5-delete-the-public-ip-address-for-the-gateway"></a>Step 5: Delete the Public IP address for the gateway

1. In **All resources**, locate the Public IP address that was assigned to the gateway. If the virtual network gateway was active-active, you will see two Public IP addresses. The graphic for a Public IP address is:

    ![Public IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-delete-vnet-gateway-portal/pip.png)

2. On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.

###<a name="step-6-delete-the-gateway-subnet"></a>Step 6: Delete the gateway subnet

1. In **All resources**, locate the virtual network. 
2. On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**. 
3. Click **Yes** to confirm that you want to delete the gateway subnet.

##<a name="deleterg"></a>Delete a VPN gateway by deleting the resource group

If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group. This is a quick way to remove everything. The following steps apply only to the Resource Manager deployment model.

1. In **All resources**, locate the resource group and click to open the blade.
2. Click **Delete**. On the Delete blade, view the affected resources. Make sure that you want to delete all of these resources. If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.
3. To proceed, type the name of the resource group that you want to delete, then click **Delete**.


