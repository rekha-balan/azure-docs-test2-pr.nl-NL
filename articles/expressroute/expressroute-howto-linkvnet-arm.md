---
title: 'Link a virtual network to an ExpressRoute circuit: PowerShell: Azure | Microsoft Docs'
description: This document provides an overview of how to link virtual networks (VNets) to ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr
ms.openlocfilehash: bcd8ca49d6da3ffbe475bbebf43fdfe97e1bf11b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553468"
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="5d2f9-103">Connect a virtual network to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="5d2f9-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Classic - PowerShell](expressroute-howto-linkvnet-classic.md)
> * [Video - Azure portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> 
> 

<span data-ttu-id="5d2f9-108">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-108">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="5d2f9-109">Virtual networks can either be in the same subscription or part of another subscription.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-109">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="5d2f9-110">This article also shows you how to update a virtual network link.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-110">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="5d2f9-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="5d2f9-111">Before you begin</span></span>
* <span data-ttu-id="5d2f9-112">Install the latest version of the Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-112">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="5d2f9-113">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="5d2f9-113">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="5d2f9-114">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-114">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="5d2f9-115">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-115">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="5d2f9-116">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-116">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="5d2f9-117">Ensure that you have Azure private peering configured for your circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-117">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="5d2f9-118">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-118">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="5d2f9-119">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-119">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="5d2f9-120">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-120">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="5d2f9-121">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5d2f9-121">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="5d2f9-122">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-122">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="5d2f9-123">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-123">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="5d2f9-124">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-124">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="5d2f9-125">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-125">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="5d2f9-126">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-126">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="5d2f9-127">Connect a virtual network in the same subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="5d2f9-127">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="5d2f9-128">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-128">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="5d2f9-129">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5d2f9-129">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="5d2f9-130">Connect a virtual network in a different subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="5d2f9-130">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="5d2f9-131">You can share an ExpressRoute circuit across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-131">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="5d2f9-132">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-132">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="5d2f9-133">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-133">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="5d2f9-134">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-134">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="5d2f9-135">A single department (in this example: IT) can own the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-135">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="5d2f9-136">Other subscriptions within the organization can use the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-136">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner. All virtual networks share the same bandwidth.
> 
> 

![Cross-subscription connectivity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="5d2f9-140">Administration - circuit owners and circuit users</span><span class="sxs-lookup"><span data-stu-id="5d2f9-140">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="5d2f9-141">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-141">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="5d2f9-142">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-142">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="5d2f9-143">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-143">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="5d2f9-144">Circuit users can redeem authorizations (one authorization per virtual network).</span><span class="sxs-lookup"><span data-stu-id="5d2f9-144">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="5d2f9-145">The circuit owner has the power to modify and revoke authorizations at any time.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-145">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="5d2f9-146">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-146">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="5d2f9-147">Circuit owner operations</span><span class="sxs-lookup"><span data-stu-id="5d2f9-147">Circuit owner operations</span></span>

<span data-ttu-id="5d2f9-148">**To create an authorization**</span><span class="sxs-lookup"><span data-stu-id="5d2f9-148">**To create an authorization**</span></span>

<span data-ttu-id="5d2f9-149">The circuit owner creates an authorization.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-149">The circuit owner creates an authorization.</span></span> <span data-ttu-id="5d2f9-150">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-150">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="5d2f9-151">An authorization is valid for only one connection.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-151">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="5d2f9-152">The following cmdlet snippet shows how to create an authorization:</span><span class="sxs-lookup"><span data-stu-id="5d2f9-152">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="5d2f9-153">The response to this will contain the authorization key and status:</span><span class="sxs-lookup"><span data-stu-id="5d2f9-153">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="5d2f9-154">**To review authorizations**</span><span class="sxs-lookup"><span data-stu-id="5d2f9-154">**To review authorizations**</span></span>

<span data-ttu-id="5d2f9-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5d2f9-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="5d2f9-156">**To add authorizations**</span><span class="sxs-lookup"><span data-stu-id="5d2f9-156">**To add authorizations**</span></span>

<span data-ttu-id="5d2f9-157">The circuit owner can add authorizations by using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5d2f9-157">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="5d2f9-158">**To delete authorizations**</span><span class="sxs-lookup"><span data-stu-id="5d2f9-158">**To delete authorizations**</span></span>

<span data-ttu-id="5d2f9-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5d2f9-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="5d2f9-160">Circuit user operations</span><span class="sxs-lookup"><span data-stu-id="5d2f9-160">Circuit user operations</span></span>

<span data-ttu-id="5d2f9-161">The circuit user needs the peer ID and an authorization key from the circuit owner.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-161">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="5d2f9-162">The authorization key is a GUID.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-162">The authorization key is a GUID.</span></span>

<span data-ttu-id="5d2f9-163">Peer ID can be checked from the following command:</span><span class="sxs-lookup"><span data-stu-id="5d2f9-163">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="5d2f9-164">**To redeem a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="5d2f9-164">**To redeem a connection authorization**</span></span>

<span data-ttu-id="5d2f9-165">The circuit user can run the following cmdlet to redeem a link authorization:</span><span class="sxs-lookup"><span data-stu-id="5d2f9-165">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="5d2f9-166">**To release a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="5d2f9-166">**To release a connection authorization**</span></span>

<span data-ttu-id="5d2f9-167">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-167">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="5d2f9-168">Modify a virtual network connection</span><span class="sxs-lookup"><span data-stu-id="5d2f9-168">Modify a virtual network connection</span></span>
<span data-ttu-id="5d2f9-169">You can update certain properties of a virtual network connection.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-169">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="5d2f9-170">**To update the connection weight**</span><span class="sxs-lookup"><span data-stu-id="5d2f9-170">**To update the connection weight**</span></span>

<span data-ttu-id="5d2f9-171">Your virtual network can be connected to multiple ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-171">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="5d2f9-172">You may receive the same prefix from more than one ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-172">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="5d2f9-173">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-173">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="5d2f9-174">Traffic will be sent on the connection with the highest *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-174">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="5d2f9-175">The range of *RoutingWeight* is 0 to 32000.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-175">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="5d2f9-176">The default value is 0.</span><span class="sxs-lookup"><span data-stu-id="5d2f9-176">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d2f9-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d2f9-177">Next steps</span></span>
<span data-ttu-id="5d2f9-178">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="5d2f9-178">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
