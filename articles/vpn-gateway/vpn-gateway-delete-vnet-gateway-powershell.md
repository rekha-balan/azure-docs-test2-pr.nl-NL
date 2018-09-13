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
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="a2d7a-103">Delete a virtual network gateway using PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2d7a-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-delete-vnet-gateway-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [Classic - PowerShell](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="a2d7a-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="a2d7a-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="a2d7a-109">When you delete a resource group, it deletes all the resources within the group.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="a2d7a-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="a2d7a-111">You can't selectively delete only a few resources using this approach.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="a2d7a-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="a2d7a-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="a2d7a-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="a2d7a-115">Before beginning</span><span class="sxs-lookup"><span data-stu-id="a2d7a-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="a2d7a-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>
<span data-ttu-id="a2d7a-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="a2d7a-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a2d7a-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="a2d7a-119">2. Connect to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-119">2. Connect to your Azure account.</span></span> 
<span data-ttu-id="a2d7a-120">Open your PowerShell console and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="a2d7a-121">Use the following example to help you connect:</span><span class="sxs-lookup"><span data-stu-id="a2d7a-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a2d7a-122">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a2d7a-123">If you have more than one subscription, specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="S2S"></a><span data-ttu-id="a2d7a-124">Delete a Site-to-Site VPN gateway</span><span class="sxs-lookup"><span data-stu-id="a2d7a-124">Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="a2d7a-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="a2d7a-126">Resources must be deleted in a certain order due to dependencies.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="a2d7a-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="a2d7a-128">We use the following specific values in the examples for demonstration purposes:</span><span class="sxs-lookup"><span data-stu-id="a2d7a-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="a2d7a-129">VNet name: VNet1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="a2d7a-130">Resource Group name: RG1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="a2d7a-131">Virtual network gateway name: GW1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="a2d7a-132">The following steps apply to the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="a2d7a-133">1. Get the virtual network gateway that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="a2d7a-134">2. Check to see if the virtual network gateway has any connections.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="a2d7a-135">3. Delete all connections.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-135">3. Delete all connections.</span></span>
<span data-ttu-id="a2d7a-136">You may be prompted to confirm the deletion of each of the connections.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-get-the-list-of-the-corresponding-local-network-gateways"></a><span data-ttu-id="a2d7a-137">4. Get the list of the corresponding local network gateways.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-137">4. Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```
    
### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="a2d7a-138">5. Delete the local network gateways.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-138">5. Delete the local network gateways.</span></span>
<span data-ttu-id="a2d7a-139">You may be prompted to confirm the deletion of each of the local network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-139">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-virtual-network-gateway"></a><span data-ttu-id="a2d7a-140">6. Delete the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-140">6. Delete the virtual network gateway.</span></span>
<span data-ttu-id="a2d7a-141">You may be prompted to confirm the deletion of the gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-141">You may be prompted to confirm the deletion of the gateway.</span></span>

>[!NOTE]
> If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.
>
>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="7-get-the-ip-configurations-of-the-virtual-network-gateway"></a><span data-ttu-id="a2d7a-143">7. Get the IP configurations of the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-143">7. Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

### <a name="8-get-the-list-of-public-ip-addresses-used-for-this-virtual-network-gateway"></a><span data-ttu-id="a2d7a-144">8. Get the list of Public IP addresses used for this virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="a2d7a-144">8. Get the list of Public IP addresses used for this virtual network gateway</span></span> 
<span data-ttu-id="a2d7a-145">If the virtual network gateway was active-active, you will see two Public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-145">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

### <a name="9-delete-the-public-ips"></a><span data-ttu-id="a2d7a-146">9. Delete the Public IPs.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-146">9. Delete the Public IPs.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="10-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="a2d7a-147">10. Delete the gateway subnet and set the configuration.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-147">10. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <a name="v2v"></a><span data-ttu-id="a2d7a-148">Delete a VNet-to-VNet VPN gateway</span><span class="sxs-lookup"><span data-stu-id="a2d7a-148">Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="a2d7a-149">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-149">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="a2d7a-150">Resources must be deleted in a certain order due to dependencies.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-150">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="a2d7a-151">When working with the examples below, some of the values must be specified, while other values are an output result.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-151">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="a2d7a-152">We use the following specific values in the examples for demonstration purposes:</span><span class="sxs-lookup"><span data-stu-id="a2d7a-152">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="a2d7a-153">VNet name: VNet1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-153">VNet name: VNet1</span></span><br>
<span data-ttu-id="a2d7a-154">Resource Group name: RG1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-154">Resource Group name: RG1</span></span><br>
<span data-ttu-id="a2d7a-155">Virtual network gateway name: GW1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-155">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="a2d7a-156">The following steps apply to the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-156">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="a2d7a-157">1. Get the virtual network gateway that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-157">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="a2d7a-158">2. Check to see if the virtual network gateway has any connections.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-158">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="a2d7a-159">There may be other connections to the virtual network gateway that are part of a different resource group.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-159">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="a2d7a-160">Check for additional connections in each additional resource group.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-160">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="a2d7a-161">In this example, we are checking for connections from RG2.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-161">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="a2d7a-162">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-162">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="a2d7a-163">3. Get the list of connections in both directions.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-163">3. Get the list of connections in both directions.</span></span>
<span data-ttu-id="a2d7a-164">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-164">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="a2d7a-165">In this example, we are checking for connections from RG2.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="a2d7a-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="a2d7a-167">4. Delete all connections.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-167">4. Delete all connections.</span></span>
<span data-ttu-id="a2d7a-168">You may be prompted to confirm the deletion of each of the connections.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-168">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="a2d7a-169">5. Delete the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-169">5. Delete the virtual network gateway.</span></span>
<span data-ttu-id="a2d7a-170">You may be prompted to confirm the deletion of the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-170">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

>[!NOTE]
> If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.
>
>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="6-get-the-ip-configurations-of-the-virtual-network-gateway"></a><span data-ttu-id="a2d7a-172">6. Get the IP configurations of the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-172">6. Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

### <a name="7-get-the-list-of-public-ip-addresses-used-for-this-virtual-network-gateway"></a><span data-ttu-id="a2d7a-173">7. Get the list of Public IP addresses used for this virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-173">7. Get the list of Public IP addresses used for this virtual network gateway.</span></span> 
<span data-ttu-id="a2d7a-174">If the virtual network gateway was active-active, you will see two Public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-174">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

### <a name="8-delete-the-public-ips"></a><span data-ttu-id="a2d7a-175">8. Delete the Public IPs.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-175">8. Delete the Public IPs.</span></span>
<span data-ttu-id="a2d7a-176">You may be prompted to confirm the deletion of the Public IP.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-176">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="9-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="a2d7a-177">9. Delete the gateway subnet and set the configuration.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-177">9. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <a name="deletep2s"></a><span data-ttu-id="a2d7a-178">Delete a Point-to-Site VPN gateway</span><span class="sxs-lookup"><span data-stu-id="a2d7a-178">Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="a2d7a-179">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-179">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="a2d7a-180">Resources must be deleted in a certain order due to dependencies.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-180">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="a2d7a-181">When working with the examples below, some of the values must be specified, while other values are an output result.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-181">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="a2d7a-182">We use the following specific values in the examples for demonstration purposes:</span><span class="sxs-lookup"><span data-stu-id="a2d7a-182">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="a2d7a-183">VNet name: VNet1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-183">VNet name: VNet1</span></span><br>
<span data-ttu-id="a2d7a-184">Resource Group name: RG1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-184">Resource Group name: RG1</span></span><br>
<span data-ttu-id="a2d7a-185">Virtual network gateway name: GW1</span><span class="sxs-lookup"><span data-stu-id="a2d7a-185">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="a2d7a-186">The following steps apply to the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-186">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="a2d7a-188">1. Get the virtual network gateway that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-188">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="a2d7a-189">2. Delete the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-189">2. Delete the virtual network gateway.</span></span>
<span data-ttu-id="a2d7a-190">You may be prompted to confirm the deletion of the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-190">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="3-get-the-ip-configurations-of-the-virtual-network-gateway"></a><span data-ttu-id="a2d7a-191">3. Get the IP configurations of the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-191">3. Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

### <a name="4-get-the-list-of-public-ip-addresses-used-for-this-virtual-network-gateway"></a><span data-ttu-id="a2d7a-192">4. Get the list of Public IP addresses used for this virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-192">4. Get the list of Public IP addresses used for this virtual network gateway.</span></span> 
<span data-ttu-id="a2d7a-193">If the virtual network gateway was active-active, you will see two Public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-193">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

### <a name="5-delete-the-public-ips"></a><span data-ttu-id="a2d7a-194">5. Delete the Public IPs.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-194">5. Delete the Public IPs.</span></span>
<span data-ttu-id="a2d7a-195">You may be prompted to confirm the deletion of the Public IP.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-195">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="6-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="a2d7a-196">6. Delete the gateway subnet and set the configuration.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-196">6. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <a name="delete"></a><span data-ttu-id="a2d7a-197">Delete a VPN gateway by deleting the resource group</span><span class="sxs-lookup"><span data-stu-id="a2d7a-197">Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="a2d7a-198">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-198">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="a2d7a-199">This is a quick way to remove everything.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-199">This is a quick way to remove everything.</span></span> <span data-ttu-id="a2d7a-200">The following steps apply only to the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-200">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="a2d7a-201">1. Get a list of all the resource groups in your subscription.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-201">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="a2d7a-202">2. Locate the resource group that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-202">2. Locate the resource group that you want to delete.</span></span>
<span data-ttu-id="a2d7a-203">Locate the resource group that you want to delete and view the list of resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-203">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="a2d7a-204">In the example, the name of the resource group is RG1.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-204">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="a2d7a-205">Modify the example to retrieve a list of all the resources.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-205">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="a2d7a-206">3. Verify the resources in the list.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-206">3. Verify the resources in the list.</span></span>
<span data-ttu-id="a2d7a-207">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-207">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="a2d7a-208">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-208">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="a2d7a-209">4. Delete the resource group and resources.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-209">4. Delete the resource group and resources.</span></span>
<span data-ttu-id="a2d7a-210">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-210">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="a2d7a-211">5. Check the status.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-211">5. Check the status.</span></span>
<span data-ttu-id="a2d7a-212">It takes some time for Azure to delete all the resources.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-212">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="a2d7a-213">You can check the status of your resource group by using this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-213">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="a2d7a-214">The result that is returned shows 'Succeeded'.</span><span class="sxs-lookup"><span data-stu-id="a2d7a-214">The result that is returned shows 'Succeeded'.</span></span>

    ResourceGroupName : RG1
    Location          : eastus
    ProvisioningState : Succeeded