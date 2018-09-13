---
title: 'How to configure routing (peering) for an ExpressRoute circuit: Resource Manager: Azure | Microsoft Docs'
description: This article walks you through the steps for creating and provisioning the private, public and Microsoft peering of an ExpressRoute circuit. This article also shows you how to check the status, update, or delete peerings for your circuit.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: cherylmc
ms.openlocfilehash: 04e688e6651f347e03de2fd103019cf34d2d0e33
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662118"
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a><span data-ttu-id="4b6d9-104">Create and modify peering for an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="4b6d9-104">Create and modify peering for an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager- Azure Portal](expressroute-howto-routing-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-routing-arm.md)
> * [Classic- PowerShell](expressroute-howto-routing-classic.md)
> * [Video - Private peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - Public peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> 
> 

<span data-ttu-id="4b6d9-111">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using the Azure portal and the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-111">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using the Azure portal and the Resource Manager deployment model.</span></span>

<span data-ttu-id="4b6d9-112">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="4b6d9-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="4b6d9-113">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="4b6d9-113">Configuration prerequisites</span></span>
* <span data-ttu-id="4b6d9-114">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-114">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="4b6d9-115">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-115">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="4b6d9-116">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-116">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="4b6d9-117">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-117">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>
* <span data-ttu-id="4b6d9-118">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-118">If you plan to use a shared key/MD5 hash, be sure to use this on both sides of the tunnel and limit the number of characters to a maximum of 25.</span></span>

<span data-ttu-id="4b6d9-119">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-119">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="4b6d9-120">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-120">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span> 

> [!IMPORTANT]
> We currently do not advertise peerings configured by service providers through the service management portal. We are working on enabling this capability soon. Please check with your service provider before configuring BGP peerings.
> 
> 

<span data-ttu-id="4b6d9-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="4b6d9-125">You can configure peerings in any order you choose.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="4b6d9-126">However, you must make sure that you complete the configuration of each peering one at a time.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="4b6d9-127">Azure private peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-127">Azure private peering</span></span>
<span data-ttu-id="4b6d9-128">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-128">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="4b6d9-129">To create Azure private peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-129">To create Azure private peering</span></span>
1. <span data-ttu-id="4b6d9-130">Configure the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-130">Configure the ExpressRoute circuit.</span></span> <span data-ttu-id="4b6d9-131">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-131">Ensure that the circuit is fully provisioned by the connectivity provider before continuing.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="4b6d9-132">Configure Azure private peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-132">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="4b6d9-133">Make sure that you have the following items before you proceed with the next steps:</span><span class="sxs-lookup"><span data-stu-id="4b6d9-133">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="4b6d9-134">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-134">A /30 subnet for the primary link.</span></span> <span data-ttu-id="4b6d9-135">This must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-135">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="4b6d9-136">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-136">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="4b6d9-137">This must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-137">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="4b6d9-138">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-138">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="4b6d9-139">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-139">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="4b6d9-140">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-140">AS number for peering.</span></span> <span data-ttu-id="4b6d9-141">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-141">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="4b6d9-142">You can use a private AS number for this peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-142">You can use a private AS number for this peering.</span></span> <span data-ttu-id="4b6d9-143">Ensure that you are not using 65515.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-143">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="4b6d9-144">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-144">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="4b6d9-145">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-145">**This is optional**.</span></span>
3. <span data-ttu-id="4b6d9-146">Select the Azure Private peering row, as shown below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-146">Select the Azure Private peering row, as shown below.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. <span data-ttu-id="4b6d9-147">Configure private peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-147">Configure private peering.</span></span> <span data-ttu-id="4b6d9-148">The image below shows a configuration example.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-148">The image below shows a configuration example.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. <span data-ttu-id="4b6d9-149">Save the configuration once you have specified all parameters.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-149">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="4b6d9-150">Once the configuration has been accepted successfully, you will see something similar to the example below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-150">Once the configuration has been accepted successfully, you will see something similar to the example below.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="4b6d9-151">To view Azure private peering details</span><span class="sxs-lookup"><span data-stu-id="4b6d9-151">To view Azure private peering details</span></span>
<span data-ttu-id="4b6d9-152">You can view the properties of Azure private peering by selecting the peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-152">You can view the properties of Azure private peering by selecting the peering.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="4b6d9-153">To update Azure private peering configuration</span><span class="sxs-lookup"><span data-stu-id="4b6d9-153">To update Azure private peering configuration</span></span>
<span data-ttu-id="4b6d9-154">You can select the row for peering and modify the peering properties.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-154">You can select the row for peering and modify the peering properties.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="4b6d9-155">To delete Azure private peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-155">To delete Azure private peering</span></span>
<span data-ttu-id="4b6d9-156">You can remove your peering configuration by selecting the delete icon as shown below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-156">You can remove your peering configuration by selecting the delete icon as shown below.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a><span data-ttu-id="4b6d9-157">Azure public peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-157">Azure public peering</span></span>
<span data-ttu-id="4b6d9-158">This section provides instructions on how to create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-158">This section provides instructions on how to create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="4b6d9-159">To create Azure public peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-159">To create Azure public peering</span></span>
1. <span data-ttu-id="4b6d9-160">Configure ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-160">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="4b6d9-161">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-161">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="4b6d9-162">Configure Azure public peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-162">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="4b6d9-163">Make sure that you have the following items before you proceed with the next steps:</span><span class="sxs-lookup"><span data-stu-id="4b6d9-163">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="4b6d9-164">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-164">A /30 subnet for the primary link.</span></span> 
   * <span data-ttu-id="4b6d9-165">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-165">A /30 subnet for the secondary link.</span></span> 
   * <span data-ttu-id="4b6d9-166">All IP addresses used to setup this peering must be valid public IPv4 addresses.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-166">All IP addresses used to setup this peering must be valid public IPv4 addresses.</span></span>
   * <span data-ttu-id="4b6d9-167">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-167">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="4b6d9-168">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-168">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="4b6d9-169">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-169">AS number for peering.</span></span> <span data-ttu-id="4b6d9-170">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-170">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="4b6d9-171">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-171">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="4b6d9-172">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-172">**This is optional**.</span></span>
3. <span data-ttu-id="4b6d9-173">Select the Azure public peering row, as shown below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-173">Select the Azure public peering row, as shown below.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. <span data-ttu-id="4b6d9-174">Configure public peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-174">Configure public peering.</span></span> <span data-ttu-id="4b6d9-175">The image below shows a configuration example.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-175">The image below shows a configuration example.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. <span data-ttu-id="4b6d9-176">Save the configuration once you have specified all parameters.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-176">Save the configuration once you have specified all parameters.</span></span> <span data-ttu-id="4b6d9-177">Once the configuration has been accepted successfully, you will see something similar to the example below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-177">Once the configuration has been accepted successfully, you will see something similar to the example below.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="4b6d9-178">To view Azure public peering details</span><span class="sxs-lookup"><span data-stu-id="4b6d9-178">To view Azure public peering details</span></span>
<span data-ttu-id="4b6d9-179">You can view the properties of Azure public peering by selecting the peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-179">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="4b6d9-180">To update Azure public peering configuration</span><span class="sxs-lookup"><span data-stu-id="4b6d9-180">To update Azure public peering configuration</span></span>
<span data-ttu-id="4b6d9-181">You can select the row for peering and modify the peering properties.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-181">You can select the row for peering and modify the peering properties.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="4b6d9-182">To delete Azure public peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-182">To delete Azure public peering</span></span>
<span data-ttu-id="4b6d9-183">You can remove your peering configuration by selecting the delete icon as shown below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-183">You can remove your peering configuration by selecting the delete icon as shown below.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a><span data-ttu-id="4b6d9-184">Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-184">Microsoft peering</span></span>
<span data-ttu-id="4b6d9-185">This section provides instructions on how to create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-185">This section provides instructions on how to create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="4b6d9-186">To create Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-186">To create Microsoft peering</span></span>
1. <span data-ttu-id="4b6d9-187">Configure ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-187">Configure ExpressRoute circuit.</span></span> <span data-ttu-id="4b6d9-188">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-188">Ensure that the circuit is fully provisioned by the connectivity provider before continuing further.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. <span data-ttu-id="4b6d9-189">Configure Microsoft peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-189">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="4b6d9-190">Make sure that you have the following information before you proceed.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-190">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="4b6d9-191">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-191">A /30 subnet for the primary link.</span></span> <span data-ttu-id="4b6d9-192">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-192">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="4b6d9-193">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-193">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="4b6d9-194">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-194">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="4b6d9-195">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-195">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="4b6d9-196">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-196">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="4b6d9-197">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-197">AS number for peering.</span></span> <span data-ttu-id="4b6d9-198">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-198">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="4b6d9-199">**Advertised prefixes:** You must provide a list of all prefixes you plan to advertise over the BGP session.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-199">**Advertised prefixes:** You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="4b6d9-200">Only public IP address prefixes are accepted.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-200">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="4b6d9-201">You can send a comma separated list if you plan to send a set of prefixes.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-201">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="4b6d9-202">These prefixes must be registered to you in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-202">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="4b6d9-203">**Customer ASN:** If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-203">**Customer ASN:** If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="4b6d9-204">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-204">**This is optional**.</span></span>
   * <span data-ttu-id="4b6d9-205">**Routing Registry Name:** You can specify the RIR / IRR against which the AS number and prefixes are registered.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-205">**Routing Registry Name:** You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span> <span data-ttu-id="4b6d9-206">**This is optional.**</span><span class="sxs-lookup"><span data-stu-id="4b6d9-206">**This is optional.**</span></span>
   * <span data-ttu-id="4b6d9-207">An MD5 hash, if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-207">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="4b6d9-208">**This is optional.**</span><span class="sxs-lookup"><span data-stu-id="4b6d9-208">**This is optional.**</span></span>
3. <span data-ttu-id="4b6d9-209">You can select the peering you wish to configure as shown below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-209">You can select the peering you wish to configure as shown below.</span></span> <span data-ttu-id="4b6d9-210">Select the Microsoft peering row.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-210">Select the Microsoft peering row.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. <span data-ttu-id="4b6d9-211">Configure Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-211">Configure Microsoft peering.</span></span> <span data-ttu-id="4b6d9-212">The image below shows a configuration example.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-212">The image below shows a configuration example.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. <span data-ttu-id="4b6d9-213">Save the configuration once you have specified all parameters.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-213">Save the configuration once you have specified all parameters.</span></span> 
   
    <span data-ttu-id="4b6d9-214">If your circuit gets to a validation needed state (as shown below), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-214">If your circuit gets to a validation needed state (as shown below), you must open a support ticket to show proof of ownership of the prefixes to our support team.</span></span>    
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

    <span data-ttu-id="4b6d9-215">You can open a support ticket directly from the portal as shown below</span><span class="sxs-lookup"><span data-stu-id="4b6d9-215">You can open a support ticket directly from the portal as shown below</span></span>     

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. <span data-ttu-id="4b6d9-216">Once the configuration has been accepted successfully, you will see something similar to the example below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-216">Once the configuration has been accepted successfully, you will see something similar to the example below.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="4b6d9-217">To view Microsoft peering details</span><span class="sxs-lookup"><span data-stu-id="4b6d9-217">To view Microsoft peering details</span></span>
<span data-ttu-id="4b6d9-218">You can view the properties of Azure public peering by selecting the peering.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-218">You can view the properties of Azure public peering by selecting the peering.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="4b6d9-219">To update Microsoft peering configuration</span><span class="sxs-lookup"><span data-stu-id="4b6d9-219">To update Microsoft peering configuration</span></span>
<span data-ttu-id="4b6d9-220">You can select the row for peering and modify the peering properties.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-220">You can select the row for peering and modify the peering properties.</span></span> 

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="4b6d9-221">To delete Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="4b6d9-221">To delete Microsoft peering</span></span>
<span data-ttu-id="4b6d9-222">You can remove your peering configuration by selecting the delete icon as shown below.</span><span class="sxs-lookup"><span data-stu-id="4b6d9-222">You can remove your peering configuration by selecting the delete icon as shown below.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a><span data-ttu-id="4b6d9-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b6d9-223">Next steps</span></span>
<span data-ttu-id="4b6d9-224">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="4b6d9-224">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md)</span></span>
* <span data-ttu-id="4b6d9-225">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="4b6d9-225">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="4b6d9-226">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="4b6d9-226">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="4b6d9-227">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b6d9-227">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
























