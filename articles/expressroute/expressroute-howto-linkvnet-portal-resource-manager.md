---
title: 'Link a virtual network to an ExpressRoute circuit: Azure portal | Microsoft Docs'
description: This document provides an overview of how to link virtual networks (VNets) to ExpressRoute circuits.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: c90bced4fc89ee26a49c8b112534499027c815de
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555057"
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="31f94-103">Connect a virtual network to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="31f94-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Classic - PowerShell](expressroute-howto-linkvnet-classic.md)
> * [Video - Azure portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> 
>  

<span data-ttu-id="31f94-108">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="31f94-108">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="31f94-109">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span><span class="sxs-lookup"><span data-stu-id="31f94-109">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="31f94-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="31f94-110">Before you begin</span></span>
* <span data-ttu-id="31f94-111">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="31f94-111">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="31f94-112">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-112">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="31f94-113">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="31f94-113">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="31f94-114">Ensure that you have Azure private peering configured for your circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-114">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="31f94-115">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span><span class="sxs-lookup"><span data-stu-id="31f94-115">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="31f94-116">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span><span class="sxs-lookup"><span data-stu-id="31f94-116">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="31f94-117">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="31f94-117">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="31f94-118">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="31f94-118">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="31f94-119">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span><span class="sxs-lookup"><span data-stu-id="31f94-119">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="31f94-120">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-120">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="31f94-121">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-121">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="31f94-122">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span><span class="sxs-lookup"><span data-stu-id="31f94-122">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="31f94-123">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="31f94-123">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>
* <span data-ttu-id="31f94-124">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span><span class="sxs-lookup"><span data-stu-id="31f94-124">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="31f94-125">Connect a virtual network in the same subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="31f94-125">Connect a virtual network in the same subscription to a circuit</span></span>

### <a name="to-create-a-connection"></a><span data-ttu-id="31f94-126">To create a connection</span><span class="sxs-lookup"><span data-stu-id="31f94-126">To create a connection</span></span>

> [!NOTE]
> BGP configuration information will not show up if the layer 3 provider configured your peerings. If your circuit is in a provisioned state, you should be able to create connections.
>

1. <span data-ttu-id="31f94-129">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span><span class="sxs-lookup"><span data-stu-id="31f94-129">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="31f94-130">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="31f94-130">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="31f94-131">Your ExpressRoute circuit should look like the following image:</span><span class="sxs-lookup"><span data-stu-id="31f94-131">Your ExpressRoute circuit should look like the following image:</span></span>

    ![ExpressRoute circuit screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="31f94-133">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-133">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="31f94-134">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span><span class="sxs-lookup"><span data-stu-id="31f94-134">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span></span>

    ![Add connection screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="31f94-136">After your connection has been successfully configured, your connection object will show the information for the connection.</span><span class="sxs-lookup"><span data-stu-id="31f94-136">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

     ![Connection object screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a><span data-ttu-id="31f94-138">To delete a connection</span><span class="sxs-lookup"><span data-stu-id="31f94-138">To delete a connection</span></span>
<span data-ttu-id="31f94-139">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span><span class="sxs-lookup"><span data-stu-id="31f94-139">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="31f94-140">Connect a virtual network in a different subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="31f94-140">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="31f94-141">You can share an ExpressRoute circuit across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="31f94-141">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="31f94-142">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="31f94-142">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Cross-subscription connectivity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="31f94-144">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span><span class="sxs-lookup"><span data-stu-id="31f94-144">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="31f94-145">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="31f94-145">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="31f94-146">A single department (in this example: IT) can own the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-146">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="31f94-147">Other subscriptions within the organization can use the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-147">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

    > [!NOTE]
    > Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner. All virtual networks share the same bandwidth.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="31f94-150">Administration - circuit owners and circuit users</span><span class="sxs-lookup"><span data-stu-id="31f94-150">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="31f94-151">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span><span class="sxs-lookup"><span data-stu-id="31f94-151">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="31f94-152">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span><span class="sxs-lookup"><span data-stu-id="31f94-152">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="31f94-153">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-153">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="31f94-154">Circuit users can redeem authorizations (one authorization per virtual network).</span><span class="sxs-lookup"><span data-stu-id="31f94-154">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="31f94-155">The circuit owner has the power to modify and revoke authorizations at any time.</span><span class="sxs-lookup"><span data-stu-id="31f94-155">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="31f94-156">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span><span class="sxs-lookup"><span data-stu-id="31f94-156">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="31f94-157">Circuit owner operations</span><span class="sxs-lookup"><span data-stu-id="31f94-157">Circuit owner operations</span></span>

<span data-ttu-id="31f94-158">**To create a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="31f94-158">**To create a connection authorization**</span></span>

<span data-ttu-id="31f94-159">The circuit owner creates an authorization.</span><span class="sxs-lookup"><span data-stu-id="31f94-159">The circuit owner creates an authorization.</span></span> <span data-ttu-id="31f94-160">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="31f94-160">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="31f94-161">An authorization is valid for only one connection.</span><span class="sxs-lookup"><span data-stu-id="31f94-161">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="31f94-162">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="31f94-162">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

    ![Authorizations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="31f94-164">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span><span class="sxs-lookup"><span data-stu-id="31f94-164">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

    ![Authorization key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/AuthKey.png)

<span data-ttu-id="31f94-166">**To delete a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="31f94-166">**To delete a connection authorization**</span></span>

<span data-ttu-id="31f94-167">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span><span class="sxs-lookup"><span data-stu-id="31f94-167">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="31f94-168">Circuit user operations</span><span class="sxs-lookup"><span data-stu-id="31f94-168">Circuit user operations</span></span>

<span data-ttu-id="31f94-169">The circuit user needs the resource ID and an authorization key from the circuit owner.</span><span class="sxs-lookup"><span data-stu-id="31f94-169">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span> 

<span data-ttu-id="31f94-170">**To redeem a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="31f94-170">**To redeem a connection authorization**</span></span>

1.  <span data-ttu-id="31f94-171">Click the **+New** button.</span><span class="sxs-lookup"><span data-stu-id="31f94-171">Click the **+New** button.</span></span>

    ![Click New](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="31f94-173">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="31f94-173">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

    ![Search for connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="31f94-175">Make sure the **Connection type** is set to "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="31f94-175">Make sure the **Connection type** is set to "ExpressRoute".</span></span>


4.  <span data-ttu-id="31f94-176">Fill in the details, then click **OK** in the Basics blade.</span><span class="sxs-lookup"><span data-stu-id="31f94-176">Fill in the details, then click **OK** in the Basics blade.</span></span>

    ![Basics blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="31f94-178">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span><span class="sxs-lookup"><span data-stu-id="31f94-178">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="31f94-179">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span><span class="sxs-lookup"><span data-stu-id="31f94-179">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="31f94-180">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="31f94-180">Click **OK**.</span></span>

    ![Settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="31f94-182">Review the information in the **Summary** blade and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="31f94-182">Review the information in the **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="31f94-183">**To release a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="31f94-183">**To release a connection authorization**</span></span>

<span data-ttu-id="31f94-184">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="31f94-184">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31f94-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="31f94-185">Next steps</span></span>
<span data-ttu-id="31f94-186">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="31f94-186">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>










