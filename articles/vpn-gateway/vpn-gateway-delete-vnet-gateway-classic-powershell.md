---
title: 'Delete a virtual network gateway: PowerShell: Azure classic | Microsoft Docs'
description: Delete a virtual network gateway using PowerShell in the classic deployment model.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: ''
ms.service: vpn-gateway
ms.devlang: na
ms.topic: ''
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: cherylmc
ms.openlocfilehash: 4437c8cb9f428bea54505dc4949410d361f77c11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564007"
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a>Delete a virtual network gateway using PowerShell (classic)
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-delete-vnet-gateway-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [Classic - PowerShell](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

You can delete a VPN gateway in the classic deployment model by using PowerShell. After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.

##<a name="step-1-connect-to-azure"></a>Step 1: Connect to Azure

### <a name="1-install-the-latest-powershell-cmdlets"></a>1. Install the latest PowerShell cmdlets.

Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets. For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="2-connect-to-your-azure-account"></a>2. Connect to your Azure account. 

Open your PowerShell console with elevated rights and connect to your account. Use the following example to help you connect:

    Login-AzureRmAccount

Check the subscriptions for the account.

    Get-AzureRmSubscription

If you have more than one subscription, select the subscription that you want to use.

    Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.

    Add-AzureAccount

## <a name="step-2-export-and-view-the-network-configuration-file"></a>Step 2: Export and view the network configuration file

Create a directory on your computer and then export the network configuration file to the directory. You use this file to both view the current configuration information, and also to modify the network configuration.

In this example, the network configuration file is exported to C:\AzureNet.

     Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml

Open the file with a text editor and view the name for your classic VNet. When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal. For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file. The name might look something like: 'Group ClassicRG1 ClassicVNet1'. Virtual network names are listed as **VirtualNetworkSite name =**. Use the names in the network configuration file when running your PowerShell cmdlets.

## <a name="step-3-delete-the-virtual-network-gateway"></a>Step 3: Delete the virtual network gateway

When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected. If you have P2S clients connected to the VNet, they will be disconnected without warning.

This example deletes the virtual network gateway. Make sure to use the full name of the virtual network from the network configuration file.

    Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"

If successful, the return shows:

    Status : Successful

## <a name="step-4-modify-the-network-configuration-file"></a>Step 4: Modify the network configuration file

When you delete a virtual network gateway, the cmdlet does not modify the network configuration file. You need to modify the file to remove the elements that are no longer being used. The following sections help you modify the network configuration file that you downloaded.

###<a name="local-network-site-references"></a>Local Network Site References

To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**. Removing a local site reference triggers Azure to delete a tunnel. Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.

    <Gateway>
       <ConnectionsToLocalNetwork>
         <LocalNetworkSiteRef name="D1BFC9CB_Site2">
           <Connection type="IPsec" />
         </LocalNetworkSiteRef>
       </ConnectionsToLocalNetwork>
    </Gateway>

Example:

    <Gateway>
       <ConnectionsToLocalNetwork>
       </ConnectionsToLocalNetwork>
     </Gateway>

###<a name="local-network-sites"></a>Local Network Sites

Remove any local sites that you are no longer using. Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.

    <LocalNetworkSites>
      <LocalNetworkSite name="Site1">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
      </LocalNetworkSite>
      <LocalNetworkSite name="Site3">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

In this example, we removed only Site3.

    <LocalNetworkSites>
        <LocalNetworkSite name="Site1">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="client-addresspool"></a>Client AddressPool

If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**. Remove the client address pools that correspond to the virtual network gateway that you deleted.

    <Gateway>
       <VPNClientAddressPool>
         <AddressPrefix>10.1.0.0/24</AddressPrefix>
       </VPNClientAddressPool>
       <ConnectionsToLocalNetwork />
    </Gateway>

Example:

     <Gateway>
       <ConnectionsToLocalNetwork />
     </Gateway>

### <a name="gatewaysubnet"></a>GatewaySubnet

Delete the **GatewaySubnet** that corresponds to the VNet.

    <Subnets>
       <Subnet name="FrontEnd">
         <AddressPrefix>10.11.0.0/24</AddressPrefix>
       </Subnet>
       <Subnet name="GatewaySubnet">
         <AddressPrefix>10.11.1.0/29</AddressPrefix>
       </Subnet>
     </Subnets>

Example:

    <Subnets>
       <Subnet name="FrontEnd">
         <AddressPrefix>10.11.0.0/24</AddressPrefix>
       </Subnet>
     </Subnets>

## <a name="step-5-upload-the-network-configuration-file"></a>Step 5: Upload the network configuration file

Save your changes and upload the network configuration file to Azure. Make sure you change the file path as necessary for your environment.

     Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml

If successful, the return shows something similar to this example:

     OperationDescription        OperationId                      OperationStatus                                                
     --------------------        -----------                      ---------------                                                
     Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded