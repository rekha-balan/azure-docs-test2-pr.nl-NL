---
title: 'Connect a virtual network to multiple sites using VPN Gateway and PowerShell : Classic | Microsoft Docs'
description: Connect multiple local on-premises sites to a classic virtual network using a VPN Gateway.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: ''
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/14/2018
ms.author: yushwang
ms.openlocfilehash: 3c733e125b860fd7fb3d593ba79395d0ba467990
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819005"
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Add a Site-to-Site connection to a VNet with an existing VPN gateway connection (classic)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (classic)](vpn-gateway-multi-site.md)
>
>

This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection. This type of connection is often referred to as a "multi-site" configuration. The steps in this article apply to virtual networks created using the classic deployment model (also known as Service Management). These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.

### <a name="deployment-models-and-methods"></a>Deployment models and methods

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

We update this table as new articles and additional tools become available for this configuration. When an article is available, we link directly to it from this table.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>About connecting

You can connect multiple on-premises sites to a single virtual network. This is especially attractive for building hybrid cloud solutions. Creating a multi-site connection to your Azure virtual network gateway is similar to creating other Site-to-Site connections. In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).

If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site. Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.

![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")

## <a name="points-to-consider"></a>Points to consider

**You won't be able to use the portal to make changes to this virtual network.** You need to make changes to the network configuration file instead of using the portal. If you make changes in the portal, they'll overwrite your multi-site reference settings for this virtual network.

You should feel comfortable using the network configuration file by the time you've completed the multi-site procedure. However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation. This doesn't mean that you can't use the portal at all. You can use it for everything else, except making configuration changes to this particular virtual network.

## <a name="before-you-begin"></a>Before you begin

Before you begin configuration, verify that you have the following:

* Compatible VPN hardware for each on-premises location. Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.
* An externally facing public IPv4 IP address for each VPN device. The IP address cannot be located behind a NAT. This is requirement.
* You'll need to install the latest version of the Azure PowerShell cmdlets. Make sure you install the Service Management (SM) version in addition to the Resource Manager version. See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.
* Someone who is proficient at configuring your VPN hardware. You'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.
* The IP address ranges that you want to use for your virtual network (if you haven't already created one).
* The IP address ranges for each of the local network sites that you'll be connecting to. You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap. Otherwise, the portal or the REST API will reject the configuration being uploaded.<br>For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping. To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.

## <a name="1-create-a-site-to-site-vpn"></a>1. Create a Site-to-Site VPN
If you already have a Site-to-Site VPN with a dynamic routing gateway, great! You can proceed to [Export the virtual network configuration settings](#export). If not, do the following:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:
1. Change your gateway type to dynamic routing. A multi-site VPN requires a dynamic (also known as route-based) routing gateway. To change your gateway type, you'll need to first delete the existing gateway, then create a new one.
2. Configure your new gateway and create your VPN tunnel. For instructions, For instructions, see [Specify the SKU and VPN type](vpn-gateway-howto-site-to-site-classic-portal.md#sku). Make sure you specify the Routing Type as 'Dynamic'.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>If you don't have a Site-to-Site virtual network:
1. Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection](vpn-gateway-site-to-site-create.md).  
2. Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md). Be sure to select **dynamic routing** for your gateway type.

## <a name="export"></a>2. Export the network configuration file
Export your Azure network configuration file by running the following command. You can change the location of the file to export to a different location if necessary.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-the-network-configuration-file"></a>3. Open the network configuration file
Open the network configuration file that you downloaded in the last step. Use any xml editor that you like. The file should look similar to the following:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Add multiple site references
When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef. Adding a new local site reference triggers Azure to create a new tunnel. In the example below, the network configuration is for a single-site connection. Save the file once you have finished making your changes.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

To add additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in the example below:

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-the-network-configuration-file"></a>5. Import the network configuration file
Import the network configuration file. When you import this file with the changes, the new tunnels will be added. The tunnels will use the dynamic gateway that you created earlier. You can use PowerShell to import the file.

## <a name="6-download-keys"></a>6. Download keys
Once your new tunnels have been added, use the PowerShell cmdlet 'Get-AzureVNetGatewayKey' to get the IPsec/IKE pre-shared keys for each tunnel.

For example:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.

## <a name="7-verify-your-connections"></a>7. Verify your connections
Check the multi-site tunnel status. After downloading the keys for each tunnel, you'll want to verify connections. Use 'Get-AzureVnetConnection' to get a list of virtual network tunnels, as shown in the example below. VNet1 is the name of the VNet.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Example return:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site1' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site2' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Next steps

To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).
