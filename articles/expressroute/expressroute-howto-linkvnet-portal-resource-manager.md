---
title: 'Link a virtual network to an ExpressRoute circuit: Azure portal | Microsoft Docs'
description: Connect a VNet to an Azure ExpressRoute Circuit. How-to steps.
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
ms.date: 03/08/2018
ms.author: cherylmc
ms.openlocfilehash: c2bef1d79d3133ea6306928a8c917e1bc3000a58
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791146"
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-the-portal"></a><span data-ttu-id="3f6d4-104">Connect a virtual network to an ExpressRoute circuit using the portal</span><span class="sxs-lookup"><span data-stu-id="3f6d4-104">Connect a virtual network to an ExpressRoute circuit using the portal</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [Video - Azure portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classic)](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="3f6d4-110">This article helps you create a connection to link a virtual network to an Azure ExpressRoute circuit using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-110">This article helps you create a connection to link a virtual network to an Azure ExpressRoute circuit using the Azure portal.</span></span> <span data-ttu-id="3f6d4-111">The virtual networks that you connect to your Azure ExpressRoute circuit can either be in the same subscription, or they can be part of another subscription.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-111">The virtual networks that you connect to your Azure ExpressRoute circuit can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3f6d4-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="3f6d4-112">Before you begin</span></span>

* <span data-ttu-id="3f6d4-113">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-113">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

* <span data-ttu-id="3f6d4-114">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-114">You must have an active ExpressRoute circuit.</span></span>
  * <span data-ttu-id="3f6d4-115">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-115">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="3f6d4-116">Ensure that you have Azure private peering configured for your circuit.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-116">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="3f6d4-117">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-117">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="3f6d4-118">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-118">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="3f6d4-119">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-119">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="3f6d4-120">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3f6d4-120">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="3f6d4-121">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-121">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="3f6d4-122">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-122">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="3f6d4-123">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-123">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span>

* <span data-ttu-id="3f6d4-124">A single VNet can be linked to up to four ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-124">A single VNet can be linked to up to four ExpressRoute circuits.</span></span> <span data-ttu-id="3f6d4-125">Use the process below to create a new connection object for each ExpressRoute circuit you are connecting to.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-125">Use the process below to create a new connection object for each ExpressRoute circuit you are connecting to.</span></span> <span data-ttu-id="3f6d4-126">The ExpressRoute circuits can be in the same subscription, different subscriptions, or a mix of both.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-126">The ExpressRoute circuits can be in the same subscription, different subscriptions, or a mix of both.</span></span>

* <span data-ttu-id="3f6d4-127">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-127">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="3f6d4-128">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-128">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

* <span data-ttu-id="3f6d4-129">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-129">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-vnet-to-a-circuit---same-subscription"></a><span data-ttu-id="3f6d4-130">Connect a VNet to a circuit - same subscription</span><span class="sxs-lookup"><span data-stu-id="3f6d4-130">Connect a VNet to a circuit - same subscription</span></span>

> [!NOTE]
> BGP configuration information will not show up if the layer 3 provider configured your peerings. If your circuit is in a provisioned state, you should be able to create connections.
>

### <a name="to-create-a-connection"></a><span data-ttu-id="3f6d4-133">To create a connection</span><span class="sxs-lookup"><span data-stu-id="3f6d4-133">To create a connection</span></span>

1. <span data-ttu-id="3f6d4-134">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-134">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="3f6d4-135">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="3f6d4-135">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="3f6d4-136">Your ExpressRoute circuit should look like the following image:</span><span class="sxs-lookup"><span data-stu-id="3f6d4-136">Your ExpressRoute circuit should look like the following image:</span></span>

  ![ExpressRoute circuit screenshot](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
2. <span data-ttu-id="3f6d4-138">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-138">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="3f6d4-139">Click **Connection** > **Add** to open the **Add connection** page, and then configure the values.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-139">Click **Connection** > **Add** to open the **Add connection** page, and then configure the values.</span></span>

  ![Add connection screenshot](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)
3. <span data-ttu-id="3f6d4-141">After your connection has been successfully configured, your connection object will show the information for the connection.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-141">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

  ![Connection object screenshot](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

## <a name="connect-a-vnet-to-a-circuit---different-subscription"></a><span data-ttu-id="3f6d4-143">Connect a VNet to a circuit - different subscription</span><span class="sxs-lookup"><span data-stu-id="3f6d4-143">Connect a VNet to a circuit - different subscription</span></span>

<span data-ttu-id="3f6d4-144">You can share an ExpressRoute circuit across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-144">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="3f6d4-145">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-145">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Cross-subscription connectivity](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="3f6d4-147">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-147">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="3f6d4-148">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-148">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="3f6d4-149">A single department (in this example: IT) can own the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-149">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="3f6d4-150">Other subscriptions within the organization can use the ExpressRoute circuit and authorizations associated to the circuit, including subscriptions linked to other Azure Active Directory tenants and Enterprise Agreement enrollments.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-150">Other subscriptions within the organization can use the ExpressRoute circuit and authorizations associated to the circuit, including subscriptions linked to other Azure Active Directory tenants and Enterprise Agreement enrollments.</span></span>

  > [!NOTE]
  > Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner. All virtual networks share the same bandwidth.
  >
  >

### <a name="administration---about-circuit-owners-and-circuit-users"></a><span data-ttu-id="3f6d4-153">Administration - About circuit owners and circuit users</span><span class="sxs-lookup"><span data-stu-id="3f6d4-153">Administration - About circuit owners and circuit users</span></span>

<span data-ttu-id="3f6d4-154">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-154">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="3f6d4-155">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-155">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="3f6d4-156">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-156">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="3f6d4-157">Circuit users can redeem authorizations (one authorization per virtual network).</span><span class="sxs-lookup"><span data-stu-id="3f6d4-157">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="3f6d4-158">The circuit owner has the power to modify and revoke authorizations at any time.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-158">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="3f6d4-159">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-159">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="3f6d4-160">Circuit owner operations</span><span class="sxs-lookup"><span data-stu-id="3f6d4-160">Circuit owner operations</span></span>

<span data-ttu-id="3f6d4-161">**To create a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="3f6d4-161">**To create a connection authorization**</span></span>

<span data-ttu-id="3f6d4-162">The circuit owner creates an authorization.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-162">The circuit owner creates an authorization.</span></span> <span data-ttu-id="3f6d4-163">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-163">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="3f6d4-164">An authorization is valid for only one connection.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-164">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="3f6d4-165">In the ExpressRoute page, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-165">In the ExpressRoute page, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

  ![Authorizations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)
2. <span data-ttu-id="3f6d4-167">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-167">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

  ![Authorization key](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="3f6d4-169">**To delete a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="3f6d4-169">**To delete a connection authorization**</span></span>

<span data-ttu-id="3f6d4-170">You can delete a connection by selecting the **Delete** icon on the page for your connection.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-170">You can delete a connection by selecting the **Delete** icon on the page for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="3f6d4-171">Circuit user operations</span><span class="sxs-lookup"><span data-stu-id="3f6d4-171">Circuit user operations</span></span>

<span data-ttu-id="3f6d4-172">The circuit user needs the resource ID and an authorization key from the circuit owner.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-172">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span>

<span data-ttu-id="3f6d4-173">**To redeem a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="3f6d4-173">**To redeem a connection authorization**</span></span>

1. <span data-ttu-id="3f6d4-174">Click the **+New** button.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-174">Click the **+New** button.</span></span>

  ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)
2. <span data-ttu-id="3f6d4-176">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-176">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

  ![Search for connection](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)
3. <span data-ttu-id="3f6d4-178">Make sure the **Connection type** is set to "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="3f6d4-178">Make sure the **Connection type** is set to "ExpressRoute".</span></span>
4. <span data-ttu-id="3f6d4-179">Fill in the details, then click **OK** in the Basics page.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-179">Fill in the details, then click **OK** in the Basics page.</span></span>

  ![Basics page](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)
5. <span data-ttu-id="3f6d4-181">In the **Settings** page, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-181">In the **Settings** page, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>
6. <span data-ttu-id="3f6d4-182">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-182">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="3f6d4-183">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-183">Click **OK**.</span></span>

  ![Settings page](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)
7. <span data-ttu-id="3f6d4-185">Review the information in the **Summary** page and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-185">Review the information in the **Summary** page and click **OK**.</span></span>

<span data-ttu-id="3f6d4-186">**To release a connection authorization**</span><span class="sxs-lookup"><span data-stu-id="3f6d4-186">**To release a connection authorization**</span></span>

<span data-ttu-id="3f6d4-187">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-187">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="delete-a-connection-to-unlink-a-vnet"></a><span data-ttu-id="3f6d4-188">Delete a connection to unlink a VNet</span><span class="sxs-lookup"><span data-stu-id="3f6d4-188">Delete a connection to unlink a VNet</span></span>

<span data-ttu-id="3f6d4-189">You can delete a connection and unlink your VNet to an ExpressRoute circuit by selecting the **Delete** icon on the page for your connection.</span><span class="sxs-lookup"><span data-stu-id="3f6d4-189">You can delete a connection and unlink your VNet to an ExpressRoute circuit by selecting the **Delete** icon on the page for your connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f6d4-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f6d4-190">Next steps</span></span>
<span data-ttu-id="3f6d4-191">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="3f6d4-191">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>