---
title: 'Link a virtual network to an ExpressRoute circuit: CLI: Azure| Microsoft Docs'
description: This document provides an overview of how to link virtual networks (VNets) to ExpressRoute circuits by using the Resource Manager deployment model and CLI.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/08/2018
ms.author: anzaman,cherylmc
ms.openlocfilehash: 5e8d1739aa3d7f5be6c6450edcad43bc83db71fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866255"
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-cli"></a><span data-ttu-id="68041-103">Connect a virtual network to an ExpressRoute circuit using CLI</span><span class="sxs-lookup"><span data-stu-id="68041-103">Connect a virtual network to an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="68041-104">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits using CLI.</span><span class="sxs-lookup"><span data-stu-id="68041-104">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="68041-105">To link using Azure CLI, the virtual networks must be created using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="68041-105">To link using Azure CLI, the virtual networks must be created using the Resource Manager deployment model.</span></span> <span data-ttu-id="68041-106">They can either be in the same subscription, or part of another subscription.</span><span class="sxs-lookup"><span data-stu-id="68041-106">They can either be in the same subscription, or part of another subscription.</span></span> <span data-ttu-id="68041-107">If you want to use a different method to connect your VNet to an ExpressRoute circuit, you can select an article from the following list:</span><span class="sxs-lookup"><span data-stu-id="68041-107">If you want to use a different method to connect your VNet to an ExpressRoute circuit, you can select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [Video - Azure portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classic)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="68041-113">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="68041-113">Configuration prerequisites</span></span>

* <span data-ttu-id="68041-114">You need the latest version of the command-line interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="68041-114">You need the latest version of the command-line interface (CLI).</span></span> <span data-ttu-id="68041-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="68041-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

* <span data-ttu-id="68041-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="68041-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

* <span data-ttu-id="68041-117">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="68041-118">Follow the instructions to [create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="68041-118">Follow the instructions to [create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="68041-119">Ensure that you have Azure private peering configured for your circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="68041-120">See the [configure routing](howto-routing-cli.md) article for routing instructions.</span><span class="sxs-lookup"><span data-stu-id="68041-120">See the [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="68041-121">Ensure that Azure private peering is configured.</span><span class="sxs-lookup"><span data-stu-id="68041-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="68041-122">The BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span><span class="sxs-lookup"><span data-stu-id="68041-122">The BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="68041-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="68041-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="68041-124">Follow the instructions to [Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="68041-124">Follow the instructions to [Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="68041-125">Be sure to use `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="68041-125">Be sure to use `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="68041-126">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-126">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="68041-127">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-127">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="68041-128">A single VNet can be linked to up to four ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="68041-128">A single VNet can be linked to up to four ExpressRoute circuits.</span></span> <span data-ttu-id="68041-129">Use the process below to create a new connection object for each ExpressRoute circuit you are connecting to.</span><span class="sxs-lookup"><span data-stu-id="68041-129">Use the process below to create a new connection object for each ExpressRoute circuit you are connecting to.</span></span> <span data-ttu-id="68041-130">The ExpressRoute circuits can be in the same subscription, different subscriptions, or a mix of both.</span><span class="sxs-lookup"><span data-stu-id="68041-130">The ExpressRoute circuits can be in the same subscription, different subscriptions, or a mix of both.</span></span>

* <span data-ttu-id="68041-131">If you enable the ExpressRoute premium add-on, you can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-131">If you enable the ExpressRoute premium add-on, you can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="68041-132">For more information about the premium add-on, see the [FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="68041-132">For more information about the premium add-on, see the [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="68041-133">Connect a virtual network in the same subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="68041-133">Connect a virtual network in the same subscription to a circuit</span></span>

<span data-ttu-id="68041-134">You can connect a virtual network gateway to an ExpressRoute circuit by using the example.</span><span class="sxs-lookup"><span data-stu-id="68041-134">You can connect a virtual network gateway to an ExpressRoute circuit by using the example.</span></span> <span data-ttu-id="68041-135">Make sure that the virtual network gateway is created and is ready for linking before you run the command.</span><span class="sxs-lookup"><span data-stu-id="68041-135">Make sure that the virtual network gateway is created and is ready for linking before you run the command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="68041-136">Connect a virtual network in a different subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="68041-136">Connect a virtual network in a different subscription to a circuit</span></span>

<span data-ttu-id="68041-137">You can share an ExpressRoute circuit across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="68041-137">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="68041-138">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="68041-138">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="68041-139">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span><span class="sxs-lookup"><span data-stu-id="68041-139">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="68041-140">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="68041-140">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="68041-141">A single department (in this example: IT) can own the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-141">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="68041-142">Other subscriptions within the organization can use the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-142">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute Circuit Owner. All virtual networks share the same bandwidth.
> 
> 

![Cross-subscription connectivity](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="68041-146">Administration - Circuit Owners and Circuit Users</span><span class="sxs-lookup"><span data-stu-id="68041-146">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="68041-147">The 'Circuit Owner' is an authorized Power User of the ExpressRoute circuit resource.</span><span class="sxs-lookup"><span data-stu-id="68041-147">The 'Circuit Owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="68041-148">The Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span><span class="sxs-lookup"><span data-stu-id="68041-148">The Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="68041-149">Circuit Users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-149">Circuit Users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="68041-150">Circuit Users can redeem authorizations (one authorization per virtual network).</span><span class="sxs-lookup"><span data-stu-id="68041-150">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="68041-151">The Circuit Owner has the power to modify and revoke authorizations at any time.</span><span class="sxs-lookup"><span data-stu-id="68041-151">The Circuit Owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="68041-152">When an authorization is revoked, all link connections are deleted from the subscription whose access was revoked.</span><span class="sxs-lookup"><span data-stu-id="68041-152">When an authorization is revoked, all link connections are deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="68041-153">Circuit Owner operations</span><span class="sxs-lookup"><span data-stu-id="68041-153">Circuit Owner operations</span></span>

<span data-ttu-id="68041-154">**To create an authorization**</span><span class="sxs-lookup"><span data-stu-id="68041-154">**To create an authorization**</span></span>

<span data-ttu-id="68041-155">The Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User to connect their virtual network gateways to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="68041-155">The Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="68041-156">An authorization is valid for only one connection.</span><span class="sxs-lookup"><span data-stu-id="68041-156">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="68041-157">The following example shows how to create an authorization:</span><span class="sxs-lookup"><span data-stu-id="68041-157">The following example shows how to create an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="68041-158">The response contains the authorization key and status:</span><span class="sxs-lookup"><span data-stu-id="68041-158">The response contains the authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="68041-159">**To review authorizations**</span><span class="sxs-lookup"><span data-stu-id="68041-159">**To review authorizations**</span></span>

<span data-ttu-id="68041-160">The Circuit Owner can review all authorizations that are issued on a particular circuit by running the following example:</span><span class="sxs-lookup"><span data-stu-id="68041-160">The Circuit Owner can review all authorizations that are issued on a particular circuit by running the following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="68041-161">**To add authorizations**</span><span class="sxs-lookup"><span data-stu-id="68041-161">**To add authorizations**</span></span>

<span data-ttu-id="68041-162">The Circuit Owner can add authorizations by using the following example:</span><span class="sxs-lookup"><span data-stu-id="68041-162">The Circuit Owner can add authorizations by using the following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="68041-163">**To delete authorizations**</span><span class="sxs-lookup"><span data-stu-id="68041-163">**To delete authorizations**</span></span>

<span data-ttu-id="68041-164">The Circuit Owner can revoke/delete authorizations to the user by running the following example:</span><span class="sxs-lookup"><span data-stu-id="68041-164">The Circuit Owner can revoke/delete authorizations to the user by running the following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="68041-165">Circuit User operations</span><span class="sxs-lookup"><span data-stu-id="68041-165">Circuit User operations</span></span>

<span data-ttu-id="68041-166">The Circuit User needs the peer ID and an authorization key from the Circuit Owner.</span><span class="sxs-lookup"><span data-stu-id="68041-166">The Circuit User needs the peer ID and an authorization key from the Circuit Owner.</span></span> <span data-ttu-id="68041-167">The authorization key is a GUID.</span><span class="sxs-lookup"><span data-stu-id="68041-167">The authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="68041-168">**To redeem a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="68041-168">**To redeem a connection authorization**</span></span>

<span data-ttu-id="68041-169">The Circuit User can run the following example to redeem a link authorization:</span><span class="sxs-lookup"><span data-stu-id="68041-169">The Circuit User can run the following example to redeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="68041-170">**To release a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="68041-170">**To release a connection authorization**</span></span>

<span data-ttu-id="68041-171">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="68041-171">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68041-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="68041-172">Next steps</span></span>

<span data-ttu-id="68041-173">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="68041-173">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>