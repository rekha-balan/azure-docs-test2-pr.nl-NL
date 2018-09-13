---
title: Connect Azure Stack to Azure using ExpressRoute
description: Learn how to connect virtual networks in Azure Stack to virtual networks in Azure using ExpressRoute.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: 878b7952938c7ec534bc09e27ee8b859c1aaeefb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865086"
---
# <a name="connect-azure-stack-to-azure-using-azure-expressroute"></a><span data-ttu-id="50e8b-103">Connect Azure Stack to Azure using Azure ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="50e8b-103">Connect Azure Stack to Azure using Azure ExpressRoute</span></span>

<span data-ttu-id="50e8b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="50e8b-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="50e8b-105">This article shows you how to connect an Azure Stack  virtual network to an Azure virtual network by using a Microsoft Azure ExpressRoute direct connection.</span><span class="sxs-lookup"><span data-stu-id="50e8b-105">This article shows you how to connect an Azure Stack  virtual network to an Azure virtual network by using a Microsoft Azure ExpressRoute direct connection.</span></span>

<span data-ttu-id="50e8b-106">You can use this article as a tutorial and use the examples to set up the same test environment.</span><span class="sxs-lookup"><span data-stu-id="50e8b-106">You can use this article as a tutorial and use the examples to set up the same test environment.</span></span> <span data-ttu-id="50e8b-107">Or, you can use the article as a walkthrough that guides you through setting up your own ExpressRoute environment.</span><span class="sxs-lookup"><span data-stu-id="50e8b-107">Or, you can use the article as a walkthrough that guides you through setting up your own ExpressRoute environment.</span></span>

## <a name="overview-assumptions-and-prerequisites"></a><span data-ttu-id="50e8b-108">Overview, assumptions, and prerequisites</span><span class="sxs-lookup"><span data-stu-id="50e8b-108">Overview, assumptions, and prerequisites</span></span>

<span data-ttu-id="50e8b-109">Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a private connection supplied by a connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="50e8b-109">Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a private connection supplied by a connectivity provider.</span></span> <span data-ttu-id="50e8b-110">ExpressRoute is not a VPN connection over the public Internet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-110">ExpressRoute is not a VPN connection over the public Internet.</span></span>

<span data-ttu-id="50e8b-111">For more information about Azure ExpressRoute, see the [ExpressRoute overview](../expressroute/expressroute-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="50e8b-111">For more information about Azure ExpressRoute, see the [ExpressRoute overview](../expressroute/expressroute-introduction.md).</span></span>

### <a name="assumptions"></a><span data-ttu-id="50e8b-112">Assumptions</span><span class="sxs-lookup"><span data-stu-id="50e8b-112">Assumptions</span></span>

<span data-ttu-id="50e8b-113">This article assumes that:</span><span class="sxs-lookup"><span data-stu-id="50e8b-113">This article assumes that:</span></span>

* <span data-ttu-id="50e8b-114">You have a working knowledge of Azure.</span><span class="sxs-lookup"><span data-stu-id="50e8b-114">You have a working knowledge of Azure.</span></span>
* <span data-ttu-id="50e8b-115">You have a basic understanding of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="50e8b-115">You have a basic understanding of Azure Stack.</span></span>
* <span data-ttu-id="50e8b-116">You have a basic understanding of networking.</span><span class="sxs-lookup"><span data-stu-id="50e8b-116">You have a basic understanding of networking.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="50e8b-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="50e8b-117">Prerequisites</span></span>

<span data-ttu-id="50e8b-118">To connect Azure Stack and Azure using ExpressRoute, you must meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="50e8b-118">To connect Azure Stack and Azure using ExpressRoute, you must meet the following requirements:</span></span>

* <span data-ttu-id="50e8b-119">A provisioned [ExpressRoute circuit](../expressroute/expressroute-circuit-peerings.md) through a [connectivity provider](../expressroute/expressroute-locations.md).</span><span class="sxs-lookup"><span data-stu-id="50e8b-119">A provisioned [ExpressRoute circuit](../expressroute/expressroute-circuit-peerings.md) through a [connectivity provider](../expressroute/expressroute-locations.md).</span></span>
* <span data-ttu-id="50e8b-120">An Azure subscription to create an ExpressRoute circuit and VNets in Azure.</span><span class="sxs-lookup"><span data-stu-id="50e8b-120">An Azure subscription to create an ExpressRoute circuit and VNets in Azure.</span></span>
* <span data-ttu-id="50e8b-121">A router that must:</span><span class="sxs-lookup"><span data-stu-id="50e8b-121">A router that must:</span></span>
  * <span data-ttu-id="50e8b-122">Support Site-to-Site VPN connections between its LAN interface and Azure Stack Multitenant Gateway.</span><span class="sxs-lookup"><span data-stu-id="50e8b-122">Support Site-to-Site VPN connections between its LAN interface and Azure Stack Multitenant Gateway.</span></span>
  * <span data-ttu-id="50e8b-123">Support creating multiple VRFs (Virtual Routing and Forwarding) if there's more than one tenant in your Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="50e8b-123">Support creating multiple VRFs (Virtual Routing and Forwarding) if there's more than one tenant in your Azure Stack deployment.</span></span>
* <span data-ttu-id="50e8b-124">A router that has:</span><span class="sxs-lookup"><span data-stu-id="50e8b-124">A router that has:</span></span>
  * <span data-ttu-id="50e8b-125">A WAN port connected to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="50e8b-125">A WAN port connected to the ExpressRoute circuit.</span></span>
  * <span data-ttu-id="50e8b-126">A LAN port connected to the Azure Stack Multitenant Gateway.</span><span class="sxs-lookup"><span data-stu-id="50e8b-126">A LAN port connected to the Azure Stack Multitenant Gateway.</span></span>

### <a name="expressroute-network-architecture"></a><span data-ttu-id="50e8b-127">ExpressRoute network architecture</span><span class="sxs-lookup"><span data-stu-id="50e8b-127">ExpressRoute network architecture</span></span>

<span data-ttu-id="50e8b-128">The next diagram shows the Azure Stack and Azure environments after you finish setting up ExpressRoute using the examples in this article.</span><span class="sxs-lookup"><span data-stu-id="50e8b-128">The next diagram shows the Azure Stack and Azure environments after you finish setting up ExpressRoute using the examples in this article.</span></span>

<span data-ttu-id="50e8b-129">*Figure 1. ExpressRoute network*</span><span class="sxs-lookup"><span data-stu-id="50e8b-129">*Figure 1. ExpressRoute network*</span></span>

![ExpressRoute network](media/azure-stack-connect-expressroute/Conceptual.png)

<span data-ttu-id="50e8b-131">The next architecture diagram shows how multiple tenants connect from the Azure Stack infrastructure through the ExpressRoute router to Azure at the Microsoft edge.</span><span class="sxs-lookup"><span data-stu-id="50e8b-131">The next architecture diagram shows how multiple tenants connect from the Azure Stack infrastructure through the ExpressRoute router to Azure at the Microsoft edge.</span></span>

<span data-ttu-id="50e8b-132">*Figure 2. Multi-tenant connections*</span><span class="sxs-lookup"><span data-stu-id="50e8b-132">*Figure 2. Multi-tenant connections*</span></span>

![Multi-tenant connections with ExpressRoute](media/azure-stack-connect-expressroute/Architecture.png)

<span data-ttu-id="50e8b-134">The example in this article uses the same multi-tenant architecture shown in *Figure 2* to connect Azure Stack to Azure using ExpressRoute private peering.</span><span class="sxs-lookup"><span data-stu-id="50e8b-134">The example in this article uses the same multi-tenant architecture shown in *Figure 2* to connect Azure Stack to Azure using ExpressRoute private peering.</span></span> <span data-ttu-id="50e8b-135">It's done using a Site-to-Site VPN connection from the virtual network gateway in Azure Stack to an ExpressRoute router.</span><span class="sxs-lookup"><span data-stu-id="50e8b-135">It's done using a Site-to-Site VPN connection from the virtual network gateway in Azure Stack to an ExpressRoute router.</span></span>

<span data-ttu-id="50e8b-136">The steps in this article show you how to create an end-to-end connection between two VNets from two different tenants in Azure Stack to corresponding VNets in Azure.</span><span class="sxs-lookup"><span data-stu-id="50e8b-136">The steps in this article show you how to create an end-to-end connection between two VNets from two different tenants in Azure Stack to corresponding VNets in Azure.</span></span> <span data-ttu-id="50e8b-137">Setting up two tenants is optional, you can also use these steps for a single tenant.</span><span class="sxs-lookup"><span data-stu-id="50e8b-137">Setting up two tenants is optional, you can also use these steps for a single tenant.</span></span>

## <a name="configure-azure-stack"></a><span data-ttu-id="50e8b-138">Configure Azure Stack</span><span class="sxs-lookup"><span data-stu-id="50e8b-138">Configure Azure Stack</span></span>

<span data-ttu-id="50e8b-139">To set up the Azure Stack environment for the first tenant, use the steps in following diagram as a guide.</span><span class="sxs-lookup"><span data-stu-id="50e8b-139">To set up the Azure Stack environment for the first tenant, use the steps in following diagram as a guide.</span></span> <span data-ttu-id="50e8b-140">If you're setting up more than one tenant, repeat these steps.</span><span class="sxs-lookup"><span data-stu-id="50e8b-140">If you're setting up more than one tenant, repeat these steps.</span></span>

>[!NOTE]
><span data-ttu-id="50e8b-141">These steps show how to create resources using the Azure Stack portal, but you can also use PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50e8b-141">These steps show how to create resources using the Azure Stack portal, but you can also use PowerShell.</span></span>

![Azure Stack network setup](media/azure-stack-connect-expressroute/image2.png)

### <a name="before-you-begin"></a><span data-ttu-id="50e8b-143">Before you begin</span><span class="sxs-lookup"><span data-stu-id="50e8b-143">Before you begin</span></span>

<span data-ttu-id="50e8b-144">Before you start configuring Azure Stack, you need:</span><span class="sxs-lookup"><span data-stu-id="50e8b-144">Before you start configuring Azure Stack, you need:</span></span>

* <span data-ttu-id="50e8b-145">An Azure Stack integrated system deployment or an Azure Stack Development Kit (ASDK) deployment.</span><span class="sxs-lookup"><span data-stu-id="50e8b-145">An Azure Stack integrated system deployment or an Azure Stack Development Kit (ASDK) deployment.</span></span> <span data-ttu-id="50e8b-146">For information about deploying the ASDK, see the [Azure Stack Development Kit deployment quickstart](azure-stack-deploy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50e8b-146">For information about deploying the ASDK, see the [Azure Stack Development Kit deployment quickstart](azure-stack-deploy-overview.md).</span></span>
* <span data-ttu-id="50e8b-147">An offer in Azure Stack that your users can subscribe to.</span><span class="sxs-lookup"><span data-stu-id="50e8b-147">An offer in Azure Stack that your users can subscribe to.</span></span> <span data-ttu-id="50e8b-148">For more information, see [plans, offers, and subscriptions](azure-stack-plan-offer-quota-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50e8b-148">For more information, see [plans, offers, and subscriptions](azure-stack-plan-offer-quota-overview.md).</span></span>

### <a name="create-network-resources-in-azure-stack"></a><span data-ttu-id="50e8b-149">Create network resources in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="50e8b-149">Create network resources in Azure Stack</span></span>

<span data-ttu-id="50e8b-150">Use the following procedures to create the required network resources in Azure Stack for a tenant.</span><span class="sxs-lookup"><span data-stu-id="50e8b-150">Use the following procedures to create the required network resources in Azure Stack for a tenant.</span></span>

#### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="50e8b-151">Create the virtual network and VM subnet</span><span class="sxs-lookup"><span data-stu-id="50e8b-151">Create the virtual network and VM subnet</span></span>

1. <span data-ttu-id="50e8b-152">Sign in to the user portal with a user (tenant) account.</span><span class="sxs-lookup"><span data-stu-id="50e8b-152">Sign in to the user portal with a user (tenant) account.</span></span>
1. <span data-ttu-id="50e8b-153">In the portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-153">In the portal, select **New**.</span></span>

1. <span data-ttu-id="50e8b-154">Under **Azure Marketplace**, select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-154">Under **Azure Marketplace**, select **Networking**.</span></span>

1. <span data-ttu-id="50e8b-155">Under **Featured**, select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-155">Under **Featured**, select **Virtual network**.</span></span>

1. <span data-ttu-id="50e8b-156">Under **Create virtual network**, enter the values shown in the following table in the appropriate fields.</span><span class="sxs-lookup"><span data-stu-id="50e8b-156">Under **Create virtual network**, enter the values shown in the following table in the appropriate fields.</span></span>

   |<span data-ttu-id="50e8b-157">Field</span><span class="sxs-lookup"><span data-stu-id="50e8b-157">Field</span></span>  |<span data-ttu-id="50e8b-158">Value</span><span class="sxs-lookup"><span data-stu-id="50e8b-158">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="50e8b-159">Name</span><span class="sxs-lookup"><span data-stu-id="50e8b-159">Name</span></span>     |<span data-ttu-id="50e8b-160">Tenant1VNet1</span><span class="sxs-lookup"><span data-stu-id="50e8b-160">Tenant1VNet1</span></span>         |
   |<span data-ttu-id="50e8b-161">Address space</span><span class="sxs-lookup"><span data-stu-id="50e8b-161">Address space</span></span>     |<span data-ttu-id="50e8b-162">10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="50e8b-162">10.1.0.0/16</span></span>|
   |<span data-ttu-id="50e8b-163">Subnet name</span><span class="sxs-lookup"><span data-stu-id="50e8b-163">Subnet name</span></span>     |<span data-ttu-id="50e8b-164">Tenant1-Sub1</span><span class="sxs-lookup"><span data-stu-id="50e8b-164">Tenant1-Sub1</span></span>|
   |<span data-ttu-id="50e8b-165">Subnet address range</span><span class="sxs-lookup"><span data-stu-id="50e8b-165">Subnet address range</span></span>     |<span data-ttu-id="50e8b-166">10.1.1.0/24</span><span class="sxs-lookup"><span data-stu-id="50e8b-166">10.1.1.0/24</span></span>|

1. <span data-ttu-id="50e8b-167">You should see the Subscription you created earlier populated in the **Subscription** field.</span><span class="sxs-lookup"><span data-stu-id="50e8b-167">You should see the Subscription you created earlier populated in the **Subscription** field.</span></span> <span data-ttu-id="50e8b-168">For the remaining fields:</span><span class="sxs-lookup"><span data-stu-id="50e8b-168">For the remaining fields:</span></span>

    * <span data-ttu-id="50e8b-169">Under **Resource group**, select **Create new** to create a new resource Group or if you already have one, select **Use existing**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-169">Under **Resource group**, select **Create new** to create a new resource Group or if you already have one, select **Use existing**.</span></span>
    * <span data-ttu-id="50e8b-170">Verify the default **Location**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-170">Verify the default **Location**.</span></span>
    * <span data-ttu-id="50e8b-171">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-171">Select **Create**.</span></span>
    * <span data-ttu-id="50e8b-172">(Optional) Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-172">(Optional) Select **Pin to dashboard**.</span></span>

#### <a name="create-the-gateway-subnet"></a><span data-ttu-id="50e8b-173">Create the gateway subnet</span><span class="sxs-lookup"><span data-stu-id="50e8b-173">Create the gateway subnet</span></span>

1. <span data-ttu-id="50e8b-174">Under **Virtual network**, select Tenant1VNet1.</span><span class="sxs-lookup"><span data-stu-id="50e8b-174">Under **Virtual network**, select Tenant1VNet1.</span></span>
1. <span data-ttu-id="50e8b-175">Under **SETTINGS**, select **Subnets**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-175">Under **SETTINGS**, select **Subnets**.</span></span>
1. <span data-ttu-id="50e8b-176">Select **+ Gateway subnet** to add a gateway subnet to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="50e8b-176">Select **+ Gateway subnet** to add a gateway subnet to the virtual network.</span></span>
1. <span data-ttu-id="50e8b-177">The name of the subnet is set to **GatewaySubnet** by default.</span><span class="sxs-lookup"><span data-stu-id="50e8b-177">The name of the subnet is set to **GatewaySubnet** by default.</span></span> <span data-ttu-id="50e8b-178">Gateway subnets are a special case and must use this name to function properly.</span><span class="sxs-lookup"><span data-stu-id="50e8b-178">Gateway subnets are a special case and must use this name to function properly.</span></span>
1. <span data-ttu-id="50e8b-179">Verify that the **Address range** is **10.1.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-179">Verify that the **Address range** is **10.1.0.0/24**.</span></span>
1. <span data-ttu-id="50e8b-180">Select **OK** to create the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-180">Select **OK** to create the gateway subnet.</span></span>

#### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="50e8b-181">Create the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="50e8b-181">Create the virtual network gateway</span></span>

1. <span data-ttu-id="50e8b-182">In the Azure Stack user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-182">In the Azure Stack user portal, select **New**.</span></span>
1. <span data-ttu-id="50e8b-183">Under **Azure Marketplace**, select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-183">Under **Azure Marketplace**, select **Networking**.</span></span>
1. <span data-ttu-id="50e8b-184">Select **Virtual network gateway** from the list of network resources.</span><span class="sxs-lookup"><span data-stu-id="50e8b-184">Select **Virtual network gateway** from the list of network resources.</span></span>
1. <span data-ttu-id="50e8b-185">In the **Name** field, enter **GW1**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-185">In the **Name** field, enter **GW1**.</span></span>
1. <span data-ttu-id="50e8b-186">Select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-186">Select **Virtual network**.</span></span>
1. <span data-ttu-id="50e8b-187">Select **Tenant1VNet1** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="50e8b-187">Select **Tenant1VNet1** from the drop-down list.</span></span>
1. <span data-ttu-id="50e8b-188">Select **Public IP address**>**Choose public IP address**, and then select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-188">Select **Public IP address**>**Choose public IP address**, and then select **Create new**.</span></span>
1. <span data-ttu-id="50e8b-189">In the **Name** field, enter **GW1-PiP** and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-189">In the **Name** field, enter **GW1-PiP** and select **OK**.</span></span>
1. <span data-ttu-id="50e8b-190">The **VPN type** should have **Route-based** selected by default.</span><span class="sxs-lookup"><span data-stu-id="50e8b-190">The **VPN type** should have **Route-based** selected by default.</span></span> <span data-ttu-id="50e8b-191">Keep this setting.</span><span class="sxs-lookup"><span data-stu-id="50e8b-191">Keep this setting.</span></span>
1. <span data-ttu-id="50e8b-192">Verify that **Subscription** and **Location** are correct.</span><span class="sxs-lookup"><span data-stu-id="50e8b-192">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="50e8b-193">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-193">Select **Create**.</span></span>

#### <a name="create-the-local-network-gateway"></a><span data-ttu-id="50e8b-194">Create the local network gateway</span><span class="sxs-lookup"><span data-stu-id="50e8b-194">Create the local network gateway</span></span>

<span data-ttu-id="50e8b-195">The Local network gateway resource identifies the remote gateway at the other end of the VPN connection.</span><span class="sxs-lookup"><span data-stu-id="50e8b-195">The Local network gateway resource identifies the remote gateway at the other end of the VPN connection.</span></span> <span data-ttu-id="50e8b-196">For this example, the remote end of the connection is the LAN subinterface of the ExpressRoute router.</span><span class="sxs-lookup"><span data-stu-id="50e8b-196">For this example, the remote end of the connection is the LAN subinterface of the ExpressRoute router.</span></span> <span data-ttu-id="50e8b-197">For Tenant 1, shown in *Figure 2*, the remote address is 10.60.3.255.</span><span class="sxs-lookup"><span data-stu-id="50e8b-197">For Tenant 1, shown in *Figure 2*, the remote address is 10.60.3.255.</span></span>

1. <span data-ttu-id="50e8b-198">Sign in to the Azure Stack user portal with your user account and select **New**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-198">Sign in to the Azure Stack user portal with your user account and select **New**.</span></span>
1. <span data-ttu-id="50e8b-199">Under **Azure Marketplace**, select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-199">Under **Azure Marketplace**, select **Networking**.</span></span>
1. <span data-ttu-id="50e8b-200">Select **local network gateway** from the list of resources.</span><span class="sxs-lookup"><span data-stu-id="50e8b-200">Select **local network gateway** from the list of resources.</span></span>
1. <span data-ttu-id="50e8b-201">In the **Name** field, enter **ER-Router-GW**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-201">In the **Name** field, enter **ER-Router-GW**.</span></span>
1. <span data-ttu-id="50e8b-202">For the **IP address** field, refer to *Figure 2*.</span><span class="sxs-lookup"><span data-stu-id="50e8b-202">For the **IP address** field, refer to *Figure 2*.</span></span> <span data-ttu-id="50e8b-203">The IP address of the ExpressRoute router's LAN subinterface for Tenant 1 is 10.60.3.255.</span><span class="sxs-lookup"><span data-stu-id="50e8b-203">The IP address of the ExpressRoute router's LAN subinterface for Tenant 1 is 10.60.3.255.</span></span> <span data-ttu-id="50e8b-204">For your own environment, enter the IP address of your router's corresponding interface.</span><span class="sxs-lookup"><span data-stu-id="50e8b-204">For your own environment, enter the IP address of your router's corresponding interface.</span></span>
1. <span data-ttu-id="50e8b-205">In the **Address Space** field, enter the address space of the VNets that you want to connect to in Azure.</span><span class="sxs-lookup"><span data-stu-id="50e8b-205">In the **Address Space** field, enter the address space of the VNets that you want to connect to in Azure.</span></span> <span data-ttu-id="50e8b-206">The subnets for Tenant 1 in *Figure 2* are:</span><span class="sxs-lookup"><span data-stu-id="50e8b-206">The subnets for Tenant 1 in *Figure 2* are:</span></span>

   * <span data-ttu-id="50e8b-207">192.168.2.0/24 is the hub VNet in Azure.</span><span class="sxs-lookup"><span data-stu-id="50e8b-207">192.168.2.0/24 is the hub VNet in Azure.</span></span>
   * <span data-ttu-id="50e8b-208">10.100.0.0/16 is the spoke VNet in Azure.</span><span class="sxs-lookup"><span data-stu-id="50e8b-208">10.100.0.0/16 is the spoke VNet in Azure.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="50e8b-209">This example assumes that you're using static routes for the Site-to-Site VPN connection between the Azure Stack gateway and the ExpressRoute router.</span><span class="sxs-lookup"><span data-stu-id="50e8b-209">This example assumes that you're using static routes for the Site-to-Site VPN connection between the Azure Stack gateway and the ExpressRoute router.</span></span>

1. <span data-ttu-id="50e8b-210">Verify that your **Subscription**, **Resource Group**, and **Location** are correct.</span><span class="sxs-lookup"><span data-stu-id="50e8b-210">Verify that your **Subscription**, **Resource Group**, and **Location** are correct.</span></span> <span data-ttu-id="50e8b-211">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-211">Select **Create**.</span></span>

#### <a name="create-the-connection"></a><span data-ttu-id="50e8b-212">Create the connection</span><span class="sxs-lookup"><span data-stu-id="50e8b-212">Create the connection</span></span>

1. <span data-ttu-id="50e8b-213">In the Azure Stack user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-213">In the Azure Stack user portal, select **New**.</span></span>
1. <span data-ttu-id="50e8b-214">Under **Azure Marketplace**, select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-214">Under **Azure Marketplace**, select **Networking**.</span></span>
1. <span data-ttu-id="50e8b-215">Select **Connection** from the list of resources.</span><span class="sxs-lookup"><span data-stu-id="50e8b-215">Select **Connection** from the list of resources.</span></span>
1. <span data-ttu-id="50e8b-216">Under **Basics**, choose **Site-to-site (IPSec)** as the **Connection type**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-216">Under **Basics**, choose **Site-to-site (IPSec)** as the **Connection type**.</span></span>
1. <span data-ttu-id="50e8b-217">Select the **Subscription**, **Resource group**, and **Location**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-217">Select the **Subscription**, **Resource group**, and **Location**.</span></span> <span data-ttu-id="50e8b-218">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-218">Select **OK**.</span></span>
1. <span data-ttu-id="50e8b-219">Under **Settings**, select **Virtual network gateway**, and then select **GW1**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-219">Under **Settings**, select **Virtual network gateway**, and then select **GW1**.</span></span>
1. <span data-ttu-id="50e8b-220">Select **Local network gateway**, and then select **ER Router GW**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-220">Select **Local network gateway**, and then select **ER Router GW**.</span></span>
1. <span data-ttu-id="50e8b-221">In the **Connection name** field, enter **ConnectToAzure**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-221">In the **Connection name** field, enter **ConnectToAzure**.</span></span>
1. <span data-ttu-id="50e8b-222">In the **Shared key (PSK)** field, enter **abc123** and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-222">In the **Shared key (PSK)** field, enter **abc123** and then select **OK**.</span></span>
1. <span data-ttu-id="50e8b-223">Under **Summary**, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-223">Under **Summary**, select **OK**.</span></span>

<span data-ttu-id="50e8b-224">**Get the Virtual network gateway public IP address**</span><span class="sxs-lookup"><span data-stu-id="50e8b-224">**Get the Virtual network gateway public IP address**</span></span>

<span data-ttu-id="50e8b-225">After you create the Virtual network gateway you can get the gateway's public IP address.</span><span class="sxs-lookup"><span data-stu-id="50e8b-225">After you create the Virtual network gateway you can get the gateway's public IP address.</span></span> <span data-ttu-id="50e8b-226">Make note of this address in case you need it later for your deployment.</span><span class="sxs-lookup"><span data-stu-id="50e8b-226">Make note of this address in case you need it later for your deployment.</span></span> <span data-ttu-id="50e8b-227">Depending on your deployment, this address is used as the ***Internal IP address***.</span><span class="sxs-lookup"><span data-stu-id="50e8b-227">Depending on your deployment, this address is used as the ***Internal IP address***.</span></span>

1. <span data-ttu-id="50e8b-228">In the Azure Stack user portal, select **All resources**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-228">In the Azure Stack user portal, select **All resources**.</span></span>
1. <span data-ttu-id="50e8b-229">Under **All resources**, select the virtual network gateway, which is **GW1** in the example.</span><span class="sxs-lookup"><span data-stu-id="50e8b-229">Under **All resources**, select the virtual network gateway, which is **GW1** in the example.</span></span>
1. <span data-ttu-id="50e8b-230">Under **Virtual network gateway**, select **Overview** from the list of resources.</span><span class="sxs-lookup"><span data-stu-id="50e8b-230">Under **Virtual network gateway**, select **Overview** from the list of resources.</span></span> <span data-ttu-id="50e8b-231">Alternatively, you can select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-231">Alternatively, you can select **Properties**.</span></span>
1. <span data-ttu-id="50e8b-232">The IP address that you want to note is listed under **Public IP address**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-232">The IP address that you want to note is listed under **Public IP address**.</span></span> <span data-ttu-id="50e8b-233">For the example configuration, this address is 192.68.102.1.</span><span class="sxs-lookup"><span data-stu-id="50e8b-233">For the example configuration, this address is 192.68.102.1.</span></span>

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="50e8b-234">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="50e8b-234">Create a virtual machine</span></span>

<span data-ttu-id="50e8b-235">To test data traffic over the VPN Connection, you need virtual machines to send and receive data in the Azure Stack VNet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-235">To test data traffic over the VPN Connection, you need virtual machines to send and receive data in the Azure Stack VNet.</span></span> <span data-ttu-id="50e8b-236">Create a virtual machine and deploy it to the VM subnet for your virtual network.</span><span class="sxs-lookup"><span data-stu-id="50e8b-236">Create a virtual machine and deploy it to the VM subnet for your virtual network.</span></span>

1. <span data-ttu-id="50e8b-237">In the Azure Stack user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-237">In the Azure Stack user portal, select **New**.</span></span>
1. <span data-ttu-id="50e8b-238">Under **Azure Marketplace**, select **Compute**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-238">Under **Azure Marketplace**, select **Compute**.</span></span>
1. <span data-ttu-id="50e8b-239">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span><span class="sxs-lookup"><span data-stu-id="50e8b-239">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>

   >[!NOTE]
   ><span data-ttu-id="50e8b-240">If the image used for this article isn't available, ask your Azure Stack operator to provide a different Windows Server image.</span><span class="sxs-lookup"><span data-stu-id="50e8b-240">If the image used for this article isn't available, ask your Azure Stack operator to provide a different Windows Server image.</span></span>

1. <span data-ttu-id="50e8b-241">In **Create virtual machine**>**Basics**, enter **VM01** as the **Name**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-241">In **Create virtual machine**>**Basics**, enter **VM01** as the **Name**.</span></span>
1. <span data-ttu-id="50e8b-242">Enter a valid user name and password.</span><span class="sxs-lookup"><span data-stu-id="50e8b-242">Enter a valid user name and password.</span></span> <span data-ttu-id="50e8b-243">You’ll use this account to sign in to the VM after it's been created.</span><span class="sxs-lookup"><span data-stu-id="50e8b-243">You’ll use this account to sign in to the VM after it's been created.</span></span>
1. <span data-ttu-id="50e8b-244">Provide a **Subscription**, **Resource group**, and a **Location**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-244">Provide a **Subscription**, **Resource group**, and a **Location**.</span></span> <span data-ttu-id="50e8b-245">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-245">Select **OK**.</span></span>
1. <span data-ttu-id="50e8b-246">Under **Choose a size**, select a virtual machine size for this instance, and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-246">Under **Choose a size**, select a virtual machine size for this instance, and then select **Select**.</span></span>
1. <span data-ttu-id="50e8b-247">Under **Settings**, confirm that:</span><span class="sxs-lookup"><span data-stu-id="50e8b-247">Under **Settings**, confirm that:</span></span>

   * <span data-ttu-id="50e8b-248">The virtual network is **Tenant1VNet1**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-248">The virtual network is **Tenant1VNet1**.</span></span>
   * <span data-ttu-id="50e8b-249">The subnet is set to **10.1.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-249">The subnet is set to **10.1.1.0/24**.</span></span>

   <span data-ttu-id="50e8b-250">Use the default settings and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-250">Use the default settings and select **OK**.</span></span>

1. <span data-ttu-id="50e8b-251">Under **Summary**, review the VM configuration and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-251">Under **Summary**, review the VM configuration and then select **OK**.</span></span>

>[!NOTE]
>
><span data-ttu-id="50e8b-252">To add more tenants, repeat the steps you followed in these sections:</span><span class="sxs-lookup"><span data-stu-id="50e8b-252">To add more tenants, repeat the steps you followed in these sections:</span></span>
>
>* <span data-ttu-id="50e8b-253">Create the virtual network and VM subnet</span><span class="sxs-lookup"><span data-stu-id="50e8b-253">Create the virtual network and VM subnet</span></span>
>* <span data-ttu-id="50e8b-254">Create the gateway subnet</span><span class="sxs-lookup"><span data-stu-id="50e8b-254">Create the gateway subnet</span></span>
>* <span data-ttu-id="50e8b-255">Create the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="50e8b-255">Create the virtual network gateway</span></span>
>* <span data-ttu-id="50e8b-256">Create the local network gateway</span><span class="sxs-lookup"><span data-stu-id="50e8b-256">Create the local network gateway</span></span>
>* <span data-ttu-id="50e8b-257">Create the connection</span><span class="sxs-lookup"><span data-stu-id="50e8b-257">Create the connection</span></span>
>* <span data-ttu-id="50e8b-258">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="50e8b-258">Create a virtual machine</span></span>
>
><span data-ttu-id="50e8b-259">If you're going to use Tenant 2 as an example, remember to change the IP addresses to avoid overlaps.</span><span class="sxs-lookup"><span data-stu-id="50e8b-259">If you're going to use Tenant 2 as an example, remember to change the IP addresses to avoid overlaps.</span></span>

### <a name="configure-the-nat-virtual-machine-for-gateway-traversal"></a><span data-ttu-id="50e8b-260">Configure the NAT virtual machine for gateway traversal</span><span class="sxs-lookup"><span data-stu-id="50e8b-260">Configure the NAT virtual machine for gateway traversal</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50e8b-261">This section is for Azure Stack Development Kit deployments only.</span><span class="sxs-lookup"><span data-stu-id="50e8b-261">This section is for Azure Stack Development Kit deployments only.</span></span> <span data-ttu-id="50e8b-262">The NAT isn't needed for multi-node deployments.</span><span class="sxs-lookup"><span data-stu-id="50e8b-262">The NAT isn't needed for multi-node deployments.</span></span>

<span data-ttu-id="50e8b-263">The Azure Stack Development Kit is self-contained and isolated from the network where the physical host is deployed.</span><span class="sxs-lookup"><span data-stu-id="50e8b-263">The Azure Stack Development Kit is self-contained and isolated from the network where the physical host is deployed.</span></span> <span data-ttu-id="50e8b-264">The VIP network that the gateways are connected to isn't external, it's hidden behind a router doing Network Address Translation (NAT).</span><span class="sxs-lookup"><span data-stu-id="50e8b-264">The VIP network that the gateways are connected to isn't external, it's hidden behind a router doing Network Address Translation (NAT).</span></span>

<span data-ttu-id="50e8b-265">The router is a Windows Server virtual machine (AzS-BGPNAT01) running the Routing and Remote Access Services (RRAS) role.</span><span class="sxs-lookup"><span data-stu-id="50e8b-265">The router is a Windows Server virtual machine (AzS-BGPNAT01) running the Routing and Remote Access Services (RRAS) role.</span></span> <span data-ttu-id="50e8b-266">You must configure NAT on the AzS-BGPNAT01 virtual machine to enable the Site-to-Site VPN Connection to connect on both ends.</span><span class="sxs-lookup"><span data-stu-id="50e8b-266">You must configure NAT on the AzS-BGPNAT01 virtual machine to enable the Site-to-Site VPN Connection to connect on both ends.</span></span>

#### <a name="configure-the-nat"></a><span data-ttu-id="50e8b-267">Configure the NAT</span><span class="sxs-lookup"><span data-stu-id="50e8b-267">Configure the NAT</span></span>

1. <span data-ttu-id="50e8b-268">Sign in to the Azure Stack host computer with your administrator account.</span><span class="sxs-lookup"><span data-stu-id="50e8b-268">Sign in to the Azure Stack host computer with your administrator account.</span></span>
1. <span data-ttu-id="50e8b-269">Copy and edit the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="50e8b-269">Copy and edit the following PowerShell script.</span></span>  <span data-ttu-id="50e8b-270">Replace `"<your administrator password>"` with your administrator password, and then run the script in an elevated PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="50e8b-270">Replace `"<your administrator password>"` with your administrator password, and then run the script in an elevated PowerShell ISE.</span></span> <span data-ttu-id="50e8b-271">This script returns your  *External BGPNAT address*.</span><span class="sxs-lookup"><span data-stu-id="50e8b-271">This script returns your  *External BGPNAT address*.</span></span>

   ```PowerShell
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "azs-bgpnat01" `
    -Password $Password

   ```

1. <span data-ttu-id="50e8b-272">To configure the NAT, copy and edit the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="50e8b-272">To configure the NAT, copy and edit the following PowerShell script.</span></span> <span data-ttu-id="50e8b-273">Edit the script to replace the `'<External BGPNAT address>'` and `'<Internal IP address>'` with the following example values:</span><span class="sxs-lookup"><span data-stu-id="50e8b-273">Edit the script to replace the `'<External BGPNAT address>'` and `'<Internal IP address>'` with the following example values:</span></span>

   * <span data-ttu-id="50e8b-274">For *External BGPNAT address* use 10.10.0.62</span><span class="sxs-lookup"><span data-stu-id="50e8b-274">For *External BGPNAT address* use 10.10.0.62</span></span>
   * <span data-ttu-id="50e8b-275">For *Internal IP address* use 192.168.102.1</span><span class="sxs-lookup"><span data-stu-id="50e8b-275">For *Internal IP address* use 192.168.102.1</span></span>

   <span data-ttu-id="50e8b-276">Run the following script from an elevated PowerShell ISE:</span><span class="sxs-lookup"><span data-stu-id="50e8b-276">Run the following script from an elevated PowerShell ISE:</span></span>

   ```PowerShell
   $ExtBgpNat = '<External BGPNAT address>'
   $IntBgpNat = '<Internal IP address>'

   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress $Using:ExtBgpNat `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress $Using:ExtBgpNat `
      -PortStart 4499 `
      -PortEnd 4501}
   # Create a static NAT mapping to map the external address to the Gateway public IP address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel.
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress $Using:ExtBgpNat `
      -InternalIPAddress $Using:IntBgpNat `
      -ExternalPort 500 `
      -InternalPort 500}
   # Configure NAT traversal which uses port 4500 to  establish the complete IPSEC tunnel over NAT devices.
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress $Using:ExtBgpNat `
      -InternalIPAddress $Using:IntBgpNat `
      -ExternalPort 4500 `
      -InternalPort 4500}

   ```

## <a name="configure-azure"></a><span data-ttu-id="50e8b-277">Configure Azure</span><span class="sxs-lookup"><span data-stu-id="50e8b-277">Configure Azure</span></span>

<span data-ttu-id="50e8b-278">After you finish configuring Azure Stack, you can deploy the Azure resources.</span><span class="sxs-lookup"><span data-stu-id="50e8b-278">After you finish configuring Azure Stack, you can deploy the Azure resources.</span></span> <span data-ttu-id="50e8b-279">The following diagram shows an example of a tenant virtual network in Azure.</span><span class="sxs-lookup"><span data-stu-id="50e8b-279">The following diagram shows an example of a tenant virtual network in Azure.</span></span> <span data-ttu-id="50e8b-280">You can use any name and addressing scheme for your VNet in Azure.</span><span class="sxs-lookup"><span data-stu-id="50e8b-280">You can use any name and addressing scheme for your VNet in Azure.</span></span> <span data-ttu-id="50e8b-281">However, the address range of the VNets in Azure and Azure Stack must be unique and not overlap.</span><span class="sxs-lookup"><span data-stu-id="50e8b-281">However, the address range of the VNets in Azure and Azure Stack must be unique and not overlap.</span></span>

<span data-ttu-id="50e8b-282">*Figure 3. Azure VNets*</span><span class="sxs-lookup"><span data-stu-id="50e8b-282">*Figure 3. Azure VNets*</span></span>

![Azure VNets](media/azure-stack-connect-expressroute/AzureArchitecture.png)

<span data-ttu-id="50e8b-284">The resources you deploy in Azure are similar to the resources you deployed in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="50e8b-284">The resources you deploy in Azure are similar to the resources you deployed in Azure Stack.</span></span> <span data-ttu-id="50e8b-285">You'll deploy the following components:</span><span class="sxs-lookup"><span data-stu-id="50e8b-285">You'll deploy the following components:</span></span>

* <span data-ttu-id="50e8b-286">Virtual networks and subnets</span><span class="sxs-lookup"><span data-stu-id="50e8b-286">Virtual networks and subnets</span></span>
* <span data-ttu-id="50e8b-287">A gateway subnet</span><span class="sxs-lookup"><span data-stu-id="50e8b-287">A gateway subnet</span></span>
* <span data-ttu-id="50e8b-288">A virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="50e8b-288">A virtual network gateway</span></span>
* <span data-ttu-id="50e8b-289">A connection</span><span class="sxs-lookup"><span data-stu-id="50e8b-289">A connection</span></span>
* <span data-ttu-id="50e8b-290">An ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="50e8b-290">An ExpressRoute circuit</span></span>

<span data-ttu-id="50e8b-291">The example Azure network infrastructure is configured as follows:</span><span class="sxs-lookup"><span data-stu-id="50e8b-291">The example Azure network infrastructure is configured as follows:</span></span>

* <span data-ttu-id="50e8b-292">A standard hub (192.168.2.0/24) and spoke (10.100.0.0./16) VNet model.</span><span class="sxs-lookup"><span data-stu-id="50e8b-292">A standard hub (192.168.2.0/24) and spoke (10.100.0.0./16) VNet model.</span></span> <span data-ttu-id="50e8b-293">For more information about a hub-spoke network topology, see [Implement a hub-spoke network topology in Azure](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/hub-spoke).</span><span class="sxs-lookup"><span data-stu-id="50e8b-293">For more information about a hub-spoke network topology, see [Implement a hub-spoke network topology in Azure](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/hub-spoke).</span></span>
* <span data-ttu-id="50e8b-294">The workloads are deployed in the spoke VNet and the ExpressRoute circuit is connected to the hub VNet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-294">The workloads are deployed in the spoke VNet and the ExpressRoute circuit is connected to the hub VNet.</span></span>
* <span data-ttu-id="50e8b-295">The two VNets are connected using VNet peering.</span><span class="sxs-lookup"><span data-stu-id="50e8b-295">The two VNets are connected using VNet peering.</span></span>

### <a name="configure-the-azure-vnets"></a><span data-ttu-id="50e8b-296">Configure the Azure VNets</span><span class="sxs-lookup"><span data-stu-id="50e8b-296">Configure the Azure VNets</span></span>

1. <span data-ttu-id="50e8b-297">Sign in to the Azure portal with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="50e8b-297">Sign in to the Azure portal with your Azure credentials.</span></span>
1. <span data-ttu-id="50e8b-298">Create the hub VNet using the 192.168.2.0/24 address range.</span><span class="sxs-lookup"><span data-stu-id="50e8b-298">Create the hub VNet using the 192.168.2.0/24 address range.</span></span>
1. <span data-ttu-id="50e8b-299">Create a subnet using the 192.168.2.0/25 address range, and add a gateway subnet using the 192.168.2.128/27 address range.</span><span class="sxs-lookup"><span data-stu-id="50e8b-299">Create a subnet using the 192.168.2.0/25 address range, and add a gateway subnet using the 192.168.2.128/27 address range.</span></span>
1. <span data-ttu-id="50e8b-300">Create the spoke VNet and subnet using the 10.100.0.0/16 address range.</span><span class="sxs-lookup"><span data-stu-id="50e8b-300">Create the spoke VNet and subnet using the 10.100.0.0/16 address range.</span></span>

<span data-ttu-id="50e8b-301">For more information about creating virtual networks in Azure, see [Create a virtual network](../virtual-network/manage-virtual-network.md#create-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="50e8b-301">For more information about creating virtual networks in Azure, see [Create a virtual network](../virtual-network/manage-virtual-network.md#create-a-virtual-network).</span></span>

### <a name="configure-an-expressroute-circuit"></a><span data-ttu-id="50e8b-302">Configure an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="50e8b-302">Configure an ExpressRoute circuit</span></span>

1. <span data-ttu-id="50e8b-303">Review the ExpressRoute prerequisites in [ExpressRoute prerequisites & checklist](../expressroute/expressroute-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="50e8b-303">Review the ExpressRoute prerequisites in [ExpressRoute prerequisites & checklist](../expressroute/expressroute-prerequisites.md).</span></span>

1. <span data-ttu-id="50e8b-304">Follow the steps in [Create and modify an ExpressRoute circuit](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) to create an ExpressRoute circuit using your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="50e8b-304">Follow the steps in [Create and modify an ExpressRoute circuit](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) to create an ExpressRoute circuit using your Azure subscription.</span></span>

   >[!NOTE]
   ><span data-ttu-id="50e8b-305">Give the service key for your circuit to your service  so they can setup your ExpressRoute circuit at their end.</span><span class="sxs-lookup"><span data-stu-id="50e8b-305">Give the service key for your circuit to your service  so they can setup your ExpressRoute circuit at their end.</span></span>

1. <span data-ttu-id="50e8b-306">Follow the steps in [Create and modify peering for an ExpressRoute circuit](../expressroute/expressroute-howto-routing-portal-resource-manager.md) to configure private peering on the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="50e8b-306">Follow the steps in [Create and modify peering for an ExpressRoute circuit](../expressroute/expressroute-howto-routing-portal-resource-manager.md) to configure private peering on the ExpressRoute circuit.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="50e8b-307">Create the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="50e8b-307">Create the virtual network gateway</span></span>

<span data-ttu-id="50e8b-308">Follow the steps in [Configure a virtual network gateway for ExpressRoute using PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) to create a virtual network gateway for ExpressRoute in the hub VNet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-308">Follow the steps in [Configure a virtual network gateway for ExpressRoute using PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) to create a virtual network gateway for ExpressRoute in the hub VNet.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="50e8b-309">Create the connection</span><span class="sxs-lookup"><span data-stu-id="50e8b-309">Create the connection</span></span>

<span data-ttu-id="50e8b-310">To link the ExpressRoute circuit to the hub VNet, follow the steps in [Connect a virtual network to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="50e8b-310">To link the ExpressRoute circuit to the hub VNet, follow the steps in [Connect a virtual network to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>

### <a name="peer-the-vnets"></a><span data-ttu-id="50e8b-311">Peer the VNets</span><span class="sxs-lookup"><span data-stu-id="50e8b-311">Peer the VNets</span></span>

<span data-ttu-id="50e8b-312">Peer the hub and spoke VNets using the steps in [Create a virtual network peering using the Azure portal](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50e8b-312">Peer the hub and spoke VNets using the steps in [Create a virtual network peering using the Azure portal](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span></span> <span data-ttu-id="50e8b-313">When configuring VNet peering, make sure you use the following options:</span><span class="sxs-lookup"><span data-stu-id="50e8b-313">When configuring VNet peering, make sure you use the following options:</span></span>

* <span data-ttu-id="50e8b-314">From the hub to the spoke, **Allow gateway transit**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-314">From the hub to the spoke, **Allow gateway transit**.</span></span>
* <span data-ttu-id="50e8b-315">From the spoke to the hub, **Use remote gateway**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-315">From the spoke to the hub, **Use remote gateway**.</span></span>

### <a name="create-a-virtual-machine"></a><span data-ttu-id="50e8b-316">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="50e8b-316">Create a virtual machine</span></span>

<span data-ttu-id="50e8b-317">Deploy your workload virtual machines into the spoke VNet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-317">Deploy your workload virtual machines into the spoke VNet.</span></span>

<span data-ttu-id="50e8b-318">Repeat these steps for any additional tenant VNets you want to connect in Azure through their respective ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="50e8b-318">Repeat these steps for any additional tenant VNets you want to connect in Azure through their respective ExpressRoute circuits.</span></span>

## <a name="configure-the-router"></a><span data-ttu-id="50e8b-319">Configure the router</span><span class="sxs-lookup"><span data-stu-id="50e8b-319">Configure the router</span></span>

<span data-ttu-id="50e8b-320">You can use the following *ExpressRoute router configuration* diagram as a guide for configuring your ExpressRoute Router.</span><span class="sxs-lookup"><span data-stu-id="50e8b-320">You can use the following *ExpressRoute router configuration* diagram as a guide for configuring your ExpressRoute Router.</span></span> <span data-ttu-id="50e8b-321">This diagram shows two tenants (Tenant 1 and Tenant 2) with their respective ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="50e8b-321">This diagram shows two tenants (Tenant 1 and Tenant 2) with their respective ExpressRoute circuits.</span></span> <span data-ttu-id="50e8b-322">Each tenant is linked to their own VRF (Virtual Routing and Forwarding) in the LAN and WAN side of the ExpressRoute router.</span><span class="sxs-lookup"><span data-stu-id="50e8b-322">Each tenant is linked to their own VRF (Virtual Routing and Forwarding) in the LAN and WAN side of the ExpressRoute router.</span></span> <span data-ttu-id="50e8b-323">This configuration ensures end-to-end isolation between the two tenants.</span><span class="sxs-lookup"><span data-stu-id="50e8b-323">This configuration ensures end-to-end isolation between the two tenants.</span></span> <span data-ttu-id="50e8b-324">Take note of the IP addresses used in the router interfaces as you follow the configuration example.</span><span class="sxs-lookup"><span data-stu-id="50e8b-324">Take note of the IP addresses used in the router interfaces as you follow the configuration example.</span></span>

<span data-ttu-id="50e8b-325">*Figure 4. ExpressRoute router configuration*</span><span class="sxs-lookup"><span data-stu-id="50e8b-325">*Figure 4. ExpressRoute router configuration*</span></span>

![ExpressRoute router configuration](media/azure-stack-connect-expressroute/EndToEnd.png)

<span data-ttu-id="50e8b-327">You can use any router that supports IKEv2 VPN and BGP to terminate the Site-to-Site VPN connection from Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="50e8b-327">You can use any router that supports IKEv2 VPN and BGP to terminate the Site-to-Site VPN connection from Azure Stack.</span></span> <span data-ttu-id="50e8b-328">The same router is used to connect to Azure using an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="50e8b-328">The same router is used to connect to Azure using an ExpressRoute circuit.</span></span>

<span data-ttu-id="50e8b-329">The following Cisco ASR 1000 Series Aggregation Services Router configuration example supports the network infrastructure shown in the *ExpressRoute router configuration* diagram.</span><span class="sxs-lookup"><span data-stu-id="50e8b-329">The following Cisco ASR 1000 Series Aggregation Services Router configuration example supports the network infrastructure shown in the *ExpressRoute router configuration* diagram.</span></span>

<span data-ttu-id="50e8b-330">**Cisco ASR 1000 configuration example**</span><span class="sxs-lookup"><span data-stu-id="50e8b-330">**Cisco ASR 1000 configuration example**</span></span>

```
ip vrf Tenant 1
 description Routing Domain for PRIVATE peering to Azure for Tenant 1
 rd 1:1
!
ip vrf Tenant 2
 description Routing Domain for PRIVATE peering to Azure for Tenant 2
 rd 1:5
!
crypto ikev2 proposal V2-PROPOSAL2
description IKEv2 proposal for Tenant 1
encryption aes-cbc-256
 integrity sha256
 group 2
crypto ikev2 proposal V4-PROPOSAL2
description IKEv2 proposal for Tenant 2
encryption aes-cbc-256
 integrity sha256
 group 2
!
crypto ikev2 policy V2-POLICY2
description IKEv2 Policy for Tenant 1
match fvrf Tenant 1
 match address local 10.60.3.255
 proposal V2-PROPOSAL2
description IKEv2 Policy for Tenant 2
crypto ikev2 policy V4-POLICY2
 match fvrf Tenant 2
 match address local 10.60.3.251
 proposal V4-PROPOSAL2
!
crypto ikev2 profile V2-PROFILE
description IKEv2 profile for Tenant 1
match fvrf Tenant 1
 match address local 10.60.3.255
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 1
!
crypto ikev2 profile V4-PROFILE
description IKEv2 profile for Tenant 2
 match fvrf Tenant 2
 match address local 10.60.3.251
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 2
!
crypto ipsec transform-set V2-TRANSFORM2 esp-gcm 256
 mode tunnel
crypto ipsec transform-set V4-TRANSFORM2 esp-gcm 256
 mode tunnel
!
crypto ipsec profile V2-PROFILE
 set transform-set V2-TRANSFORM2
 set ikev2-profile V2-PROFILE
!
crypto ipsec profile V4-PROFILE
 set transform-set V4-TRANSFORM2
 set ikev2-profile V4-PROFILE
!
interface Tunnel10
description S2S VPN Tunnel for Tenant 1
 ip vrf forwarding Tenant 1
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.211
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf Tenant 1
 tunnel protection ipsec profile V2-PROFILE
!
interface Tunnel20
description S2S VPN Tunnel for Tenant 2
 ip vrf forwarding Tenant 2
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.213
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf VNET3
 tunnel protection ipsec profile V4-PROFILE
!
interface GigabitEthernet0/0/1
 description PRIMARY ExpressRoute Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/1.100
description Primary WAN interface of Tenant 1
 description PRIMARY ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.1 255.255.255.252
!
interface GigabitEthernet0/0/1.102
description Primary WAN interface of Tenant 2
 description PRIMARY ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.17 255.255.255.252
!
interface GigabitEthernet0/0/2
 description BACKUP ExpressRoute Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/2.100
description Secondary WAN interface of Tenant 1
 description BACKUP ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.5 255.255.255.252
!
interface GigabitEthernet0/0/2.102
description Secondary WAN interface of Tenant 2
description BACKUP ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.21 255.255.255.252
!
interface TenGigabitEthernet0/1/0
 description Downlink to ---Port 1/47
 no ip address
!
interface TenGigabitEthernet0/1/0.211
 description LAN interface of Tenant 1
description Downlink to --- Port 1/47.211
 encapsulation dot1Q 211
 ip vrf forwarding Tenant 1
 ip address 10.60.3.255 255.255.255.254
!
interface TenGigabitEthernet0/1/0.213
description LAN interface of Tenant 2
 description Downlink to --- Port 1/47.213
 encapsulation dot1Q 213
 ip vrf forwarding Tenant 2
 ip address 10.60.3.251 255.255.255.254
!
router bgp 65530
 bgp router-id <removed>
 bgp log-neighbor-changes
 description BGP neighbor config and route advertisement for Tenant 1 VRF
 address-family ipv4 vrf Tenant 1
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.254 mask 255.255.255.254
  network 192.168.1.0 mask 255.255.255.252
  network 192.168.1.4 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65100
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 1
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.254 remote-as 4232570301
  neighbor 10.60.3.254 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.254 activate
  neighbor 10.60.3.254 route-map BLOCK-ALL out
  neighbor 192.168.1.2 remote-as 12076
  neighbor 192.168.1.2 description PRIMARY ER peer for Tenant 1 to Azure
  neighbor 192.168.1.2 ebgp-multihop 5
  neighbor 192.168.1.2 activate
  neighbor 192.168.1.2 soft-reconfiguration inbound
  neighbor 192.168.1.2 route-map Tenant 1-ONLY out
  neighbor 192.168.1.6 remote-as 12076
  neighbor 192.168.1.6 description BACKUP ER peer for Tenant 1 to Azure
  neighbor 192.168.1.6 ebgp-multihop 5
  neighbor 192.168.1.6 activate
  neighbor 192.168.1.6 soft-reconfiguration inbound
  neighbor 192.168.1.6 route-map Tenant 1-ONLY out
  maximum-paths 8
 exit-address-family
 !
description BGP neighbor config and route advertisement for Tenant 2 VRF
address-family ipv4 vrf Tenant 2
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.250 mask 255.255.255.254
  network 192.168.1.16 mask 255.255.255.252
  network 192.168.1.20 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65300
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 2
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.250 remote-as 4232570301
  neighbor 10.60.3.250 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.250 activate
  neighbor 10.60.3.250 route-map BLOCK-ALL out
  neighbor 192.168.1.18 remote-as 12076
  neighbor 192.168.1.18 description PRIMARY ER peer for Tenant 2 to Azure
  neighbor 192.168.1.18 ebgp-multihop 5
  neighbor 192.168.1.18 activate
  neighbor 192.168.1.18 soft-reconfiguration inbound
  neighbor 192.168.1.18 route-map VNET-ONLY out
  neighbor 192.168.1.22 remote-as 12076
  neighbor 192.168.1.22 description BACKUP ER peer for Tenant 2 to Azure
  neighbor 192.168.1.22 ebgp-multihop 5
  neighbor 192.168.1.22 activate
  neighbor 192.168.1.22 soft-reconfiguration inbound
  neighbor 192.168.1.22 route-map VNET-ONLY out
  maximum-paths 8
 exit-address-family
!
ip forward-protocol nd
!
ip as-path access-list 1 permit ^$
ip route vrf Tenant 1 10.1.0.0 255.255.0.0 Tunnel10
ip route vrf Tenant 2 10.1.0.0 255.255.0.0 Tunnel20
!
ip prefix-list BLOCK-ALL seq 5 deny 0.0.0.0/0 le 32
!
route-map BLOCK-ALL permit 10
 match ip address prefix-list BLOCK-ALL
!
route-map VNET-ONLY permit 10
 match as-path 1
!
```

## <a name="test-the-connection"></a><span data-ttu-id="50e8b-331">Test the connection</span><span class="sxs-lookup"><span data-stu-id="50e8b-331">Test the connection</span></span>

<span data-ttu-id="50e8b-332">Test your connection after you establish the Site-to-Site connection and the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="50e8b-332">Test your connection after you establish the Site-to-Site connection and the ExpressRoute circuit.</span></span>

<span data-ttu-id="50e8b-333">Do the following ping tests:</span><span class="sxs-lookup"><span data-stu-id="50e8b-333">Do the following ping tests:</span></span>

* <span data-ttu-id="50e8b-334">Sign in to one of the virtual machines in your Azure VNet and ping the virtual machine you created in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="50e8b-334">Sign in to one of the virtual machines in your Azure VNet and ping the virtual machine you created in Azure Stack.</span></span>
* <span data-ttu-id="50e8b-335">Sign in to one of the virtual machines you created in Azure Stack and ping the virtual machine you created in the Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-335">Sign in to one of the virtual machines you created in Azure Stack and ping the virtual machine you created in the Azure VNet.</span></span>

>[!NOTE]
><span data-ttu-id="50e8b-336">To make sure you're sending traffic over the Site-to-Site and ExpressRoute connections, you must ping the dedicated IP (DIP) address of the virtual machine at both ends and not the VIP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="50e8b-336">To make sure you're sending traffic over the Site-to-Site and ExpressRoute connections, you must ping the dedicated IP (DIP) address of the virtual machine at both ends and not the VIP address of the virtual machine.</span></span>

### <a name="allow-icmp-in-through-the-firewall"></a><span data-ttu-id="50e8b-337">Allow ICMP in through the firewall</span><span class="sxs-lookup"><span data-stu-id="50e8b-337">Allow ICMP in through the firewall</span></span>

<span data-ttu-id="50e8b-338">By default, Windows Server 2016 doesn't allow incoming ICMP packets through the firewall.</span><span class="sxs-lookup"><span data-stu-id="50e8b-338">By default, Windows Server 2016 doesn't allow incoming ICMP packets through the firewall.</span></span> <span data-ttu-id="50e8b-339">For every virtual machine that you're using for ping tests you need to allow incoming ICMP packets.</span><span class="sxs-lookup"><span data-stu-id="50e8b-339">For every virtual machine that you're using for ping tests you need to allow incoming ICMP packets.</span></span> <span data-ttu-id="50e8b-340">To create a firewall rule for ICMP, run the following cmdlet in an elevated PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="50e8b-340">To create a firewall rule for ICMP, run the following cmdlet in an elevated PowerShell window:</span></span>

```PowerShell
# Create ICMP firewall rule.
New-NetFirewallRule `
  –DisplayName “Allow ICMPv4-In” `
  –Protocol ICMPv4

```

### <a name="ping-the-azure-stack-virtual-machine"></a><span data-ttu-id="50e8b-341">Ping the Azure Stack virtual machine</span><span class="sxs-lookup"><span data-stu-id="50e8b-341">Ping the Azure Stack virtual machine</span></span>

1. <span data-ttu-id="50e8b-342">Sign in to the Azure Stack user portal using a tenant account.</span><span class="sxs-lookup"><span data-stu-id="50e8b-342">Sign in to the Azure Stack user portal using a tenant account.</span></span>

1. <span data-ttu-id="50e8b-343">Find the virtual machine that you created and select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="50e8b-343">Find the virtual machine that you created and select the virtual machine.</span></span>

1. <span data-ttu-id="50e8b-344">Select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-344">Select **Connect**.</span></span>

1. <span data-ttu-id="50e8b-345">From an elevated Windows or PowerShell command prompt, enter **ipconfig /all**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-345">From an elevated Windows or PowerShell command prompt, enter **ipconfig /all**.</span></span> <span data-ttu-id="50e8b-346">Note the IPv4 address returned in the output.</span><span class="sxs-lookup"><span data-stu-id="50e8b-346">Note the IPv4 address returned in the output.</span></span>

1. <span data-ttu-id="50e8b-347">Ping the IPv4 address from the virtual machine in the Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-347">Ping the IPv4 address from the virtual machine in the Azure VNet.</span></span>

   <span data-ttu-id="50e8b-348">In the example environment, the IPv4 address is from the 10.1.1.x/24 subnet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-348">In the example environment, the IPv4 address is from the 10.1.1.x/24 subnet.</span></span> <span data-ttu-id="50e8b-349">In your environment, the address might be different.</span><span class="sxs-lookup"><span data-stu-id="50e8b-349">In your environment, the address might be different.</span></span> <span data-ttu-id="50e8b-350">But it should be in the subnet you created for the tenant VNet subnet.</span><span class="sxs-lookup"><span data-stu-id="50e8b-350">But it should be in the subnet you created for the tenant VNet subnet.</span></span>

### <a name="view-data-transfer-statistics"></a><span data-ttu-id="50e8b-351">View data transfer statistics</span><span class="sxs-lookup"><span data-stu-id="50e8b-351">View data transfer statistics</span></span>

<span data-ttu-id="50e8b-352">If you want to know how much traffic is passing through your connection, you can find this information on the Azure Stack user portal.</span><span class="sxs-lookup"><span data-stu-id="50e8b-352">If you want to know how much traffic is passing through your connection, you can find this information on the Azure Stack user portal.</span></span> <span data-ttu-id="50e8b-353">This is also a good way to find out whether or not your ping test data went through the VPN and ExpressRoute connections.</span><span class="sxs-lookup"><span data-stu-id="50e8b-353">This is also a good way to find out whether or not your ping test data went through the VPN and ExpressRoute connections.</span></span>

1. <span data-ttu-id="50e8b-354">Sign in to the Azure Stack user portal using your tenant account and select **All resources**.</span><span class="sxs-lookup"><span data-stu-id="50e8b-354">Sign in to the Azure Stack user portal using your tenant account and select **All resources**.</span></span>
1. <span data-ttu-id="50e8b-355">Navigate to the resource group for your VPN Gateway and select the **Connection** object type.</span><span class="sxs-lookup"><span data-stu-id="50e8b-355">Navigate to the resource group for your VPN Gateway and select the **Connection** object type.</span></span>
1. <span data-ttu-id="50e8b-356">Select the **ConnectToAzure** connection from the list.</span><span class="sxs-lookup"><span data-stu-id="50e8b-356">Select the **ConnectToAzure** connection from the list.</span></span>
1. <span data-ttu-id="50e8b-357">Under **Connections**>**Overview**, you can see statistics for **Data in** and **Data out**. You should see some non-zero values.</span><span class="sxs-lookup"><span data-stu-id="50e8b-357">Under **Connections**>**Overview**, you can see statistics for **Data in** and **Data out**. You should see some non-zero values.</span></span>

   ![Data In and Data Out](media/azure-stack-connect-expressroute/DataInDataOut.png)

## <a name="next-steps"></a><span data-ttu-id="50e8b-359">Next steps</span><span class="sxs-lookup"><span data-stu-id="50e8b-359">Next steps</span></span>

[<span data-ttu-id="50e8b-360">Deploy apps to Azure and Azure Stack</span><span class="sxs-lookup"><span data-stu-id="50e8b-360">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
