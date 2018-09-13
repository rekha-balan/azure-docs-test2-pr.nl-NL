---
title: 'Delete a virtual network gateway: PowerShell: Azure Resource Manager | Microsoft Docs'
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
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: b9bb77ae6d5a6b8bcf87521ed68ca28235583672
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564013"
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a>Delete a virtual network gateway using PowerShell
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-delete-vnet-gateway-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [Classic - PowerShell](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.

- If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group. When you delete a resource group, it deletes all the resources within the group. This is method is only recommended if you don't want to keep any of the resources in the resource group. You can't selectively delete only a few resources using this approach.

- If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated. Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway. The steps you follow depend on the type of connections that you created and the dependent resources for each connection.

## <a name="before-beginning"></a>Before beginning

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a>1. Download the latest Azure Resource Manager PowerShell cmdlets.
Download and install the latest version of the Azure Resource Manager PowerShell cmdlets. For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="2-connect-to-your-azure-account"></a>2. Connect to your Azure account. 
Open your PowerShell console and connect to your account. Use the following example to help you connect:

```powershell
Login-AzureRmAccount
```

Check the subscriptions for the account.

```powershell
Get-AzureRmSubscription
```

If you have more than one subscription, specify the subscription that you want to use.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="S2S"></a>Delete a Site-to-Site VPN gateway

To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway. Resources must be deleted in a certain order due to dependencies. When working with the examples below, some of the values must be specified, while other values are an output result. We use the following specific values in the examples for demonstration purposes:

VNet name: VNet1<br>
Resource Group name: RG1<br>
Virtual network gateway name: GW1<br>

The following steps apply to the Resource Manager deployment model.

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a>1. Get the virtual network gateway that you want to delete.

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a>2. Check to see if the virtual network gateway has any connections.

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a>3. Delete all connections.
You may be prompted to confirm the deletion of each of the connections.

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-get-the-list-of-the-corresponding-local-network-gateways"></a>4. Get the list of the corresponding local network gateways.

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```
    
### <a name="5-delete-the-local-network-gateways"></a>5. Delete the local network gateways.
You may be prompted to confirm the deletion of each of the local network gateway.

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-virtual-network-gateway"></a>6. Delete the virtual network gateway.
You may be prompted to confirm the deletion of the gateway.

>[!NOTE]
> If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.
>
>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="7-get-the-ip-configurations-of-the-virtual-network-gateway"></a>7. Get the IP configurations of the virtual network gateway.

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

### <a name="8-get-the-list-of-public-ip-addresses-used-for-this-virtual-network-gateway"></a>8. Get the list of Public IP addresses used for this virtual network gateway 
If the virtual network gateway was active-active, you will see two Public IP addresses.

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

### <a name="9-delete-the-public-ips"></a>9. Delete the Public IPs.

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="10-delete-the-gateway-subnet-and-set-the-configuration"></a>10. Delete the gateway subnet and set the configuration.

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <a name="v2v"></a>Delete a VNet-to-VNet VPN gateway

To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway. Resources must be deleted in a certain order due to dependencies. When working with the examples below, some of the values must be specified, while other values are an output result. We use the following specific values in the examples for demonstration purposes:

VNet name: VNet1<br>
Resource Group name: RG1<br>
Virtual network gateway name: GW1<br>

The following steps apply to the Resource Manager deployment model.

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a>1. Get the virtual network gateway that you want to delete.

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a>2. Check to see if the virtual network gateway has any connections.

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
There may be other connections to the virtual network gateway that are part of a different resource group. Check for additional connections in each additional resource group. In this example, we are checking for connections from RG2. Run this for each resource group that you have which may have a connection to the virtual network gateway.

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a>3. Get the list of connections in both directions.
Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
In this example, we are checking for connections from RG2. Run this for each resource group that you have which may have a connection to the virtual network gateway.

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a>4. Delete all connections.
You may be prompted to confirm the deletion of each of the connections.

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a>5. Delete the virtual network gateway.
You may be prompted to confirm the deletion of the virtual network gateway.

>[!NOTE]
> If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.
>
>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="6-get-the-ip-configurations-of-the-virtual-network-gateway"></a>6. Get the IP configurations of the virtual network gateway.

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

### <a name="7-get-the-list-of-public-ip-addresses-used-for-this-virtual-network-gateway"></a>7. Get the list of Public IP addresses used for this virtual network gateway. 
If the virtual network gateway was active-active, you will see two Public IP addresses.

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

### <a name="8-delete-the-public-ips"></a>8. Delete the Public IPs.
You may be prompted to confirm the deletion of the Public IP.

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="9-delete-the-gateway-subnet-and-set-the-configuration"></a>9. Delete the gateway subnet and set the configuration.

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <a name="deletep2s"></a>Delete a Point-to-Site VPN gateway

To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway. Resources must be deleted in a certain order due to dependencies. When working with the examples below, some of the values must be specified, while other values are an output result. We use the following specific values in the examples for demonstration purposes:

VNet name: VNet1<br>
Resource Group name: RG1<br>
Virtual network gateway name: GW1<br>

The following steps apply to the Resource Manager deployment model.


>[!NOTE]
> When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a>1. Get the virtual network gateway that you want to delete.

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a>2. Delete the virtual network gateway.
You may be prompted to confirm the deletion of the virtual network gateway.

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="3-get-the-ip-configurations-of-the-virtual-network-gateway"></a>3. Get the IP configurations of the virtual network gateway.

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

### <a name="4-get-the-list-of-public-ip-addresses-used-for-this-virtual-network-gateway"></a>4. Get the list of Public IP addresses used for this virtual network gateway. 
If the virtual network gateway was active-active, you will see two Public IP addresses.

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

### <a name="5-delete-the-public-ips"></a>5. Delete the Public IPs.
You may be prompted to confirm the deletion of the Public IP.

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="6-delete-the-gateway-subnet-and-set-the-configuration"></a>6. Delete the gateway subnet and set the configuration.

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <a name="delete"></a>Delete a VPN gateway by deleting the resource group

If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group. This is a quick way to remove everything. The following steps apply only to the Resource Manager deployment model.

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a>1. Get a list of all the resource groups in your subscription.

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a>2. Locate the resource group that you want to delete.
Locate the resource group that you want to delete and view the list of resources in that resource group. In the example, the name of the resource group is RG1. Modify the example to retrieve a list of all the resources.

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a>3. Verify the resources in the list.
When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself. If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.

### <a name="4-delete-the-resource-group-and-resources"></a>4. Delete the resource group and resources.
To delete the resource group and all the resource contained in the resource group, modify the example and run.

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a>5. Check the status.
It takes some time for Azure to delete all the resources. You can check the status of your resource group by using this cmdlet.

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

The result that is returned shows 'Succeeded'.

    ResourceGroupName : RG1
    Location          : eastus
    ProvisioningState : Succeeded