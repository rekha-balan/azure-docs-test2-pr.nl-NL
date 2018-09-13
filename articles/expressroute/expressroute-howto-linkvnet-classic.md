---
title: 'Link a virtual network to an ExpressRoute circuit: PowerShell: classic: Azure | Microsoft Docs'
description: This document provides an overview of how to link virtual networks (VNets) to ExpressRoute circuits by using the classic deployment model and PowerShell.
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: ''
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/13/2016
ms.author: ganesr
ms.openlocfilehash: f261551ed106e541da1d89da00c65ed97e18e953
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661070"
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="9ca2f-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span><span class="sxs-lookup"><span data-stu-id="9ca2f-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Classic - PowerShell](expressroute-howto-linkvnet-classic.md)
> * [Video - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> 
> 

<span data-ttu-id="9ca2f-108">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-108">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span></span> <span data-ttu-id="9ca2f-109">Virtual networks can either be in the same subscription or can be part of another subscription.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-109">Virtual networks can either be in the same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="9ca2f-110">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="9ca2f-110">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="9ca2f-111">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="9ca2f-111">Configuration prerequisites</span></span>
1. <span data-ttu-id="9ca2f-112">You need the latest version of the Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-112">You need the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="9ca2f-113">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9ca2f-113">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="9ca2f-114">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-114">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>
2. <span data-ttu-id="9ca2f-115">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-115">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="9ca2f-116">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-116">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="9ca2f-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="9ca2f-118">Ensure that you have Azure private peering configured for your circuit.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="9ca2f-119">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-119">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="9ca2f-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="9ca2f-121">You must have a virtual network and a virtual network gateway created and fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-121">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="9ca2f-122">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="9ca2f-122">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="9ca2f-123">You can link up to 10 virtual networks to an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-123">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="9ca2f-124">All virtual networks must be in the same geopolitical region.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-124">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="9ca2f-125">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-125">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="9ca2f-126">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-126">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="9ca2f-127">Connect a virtual network in the same subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="9ca2f-127">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="9ca2f-128">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-128">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="9ca2f-129">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-129">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="9ca2f-130">Connect a virtual network in a different subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="9ca2f-130">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="9ca2f-131">You can share an ExpressRoute circuit across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-131">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="9ca2f-132">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-132">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="9ca2f-133">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-133">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="9ca2f-134">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-134">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="9ca2f-135">A single department (in this example: IT) can own the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-135">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="9ca2f-136">Other subscriptions within the organization can use the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-136">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner. All virtual networks share the same bandwidth.
> 
> 

![Cross-subscription connectivity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/expressroute/media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="9ca2f-140">Administration</span><span class="sxs-lookup"><span data-stu-id="9ca2f-140">Administration</span></span>
<span data-ttu-id="9ca2f-141">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-141">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="9ca2f-142">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-142">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="9ca2f-143">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-143">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="9ca2f-144">The circuit owner has the power to modify and revoke authorizations at any time.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-144">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="9ca2f-145">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-145">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="9ca2f-146">Circuit owner operations</span><span class="sxs-lookup"><span data-stu-id="9ca2f-146">Circuit owner operations</span></span>

<span data-ttu-id="9ca2f-147">**Creating an authorization**</span><span class="sxs-lookup"><span data-stu-id="9ca2f-147">**Creating an authorization**</span></span>

<span data-ttu-id="9ca2f-148">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-148">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="9ca2f-149">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-149">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="9ca2f-150">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-150">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="9ca2f-151">The cmdlet doesn't send email to the specified Microsoft ID.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-151">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="9ca2f-152">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span><span class="sxs-lookup"><span data-stu-id="9ca2f-152">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="9ca2f-153">**Reviewing authorizations**</span><span class="sxs-lookup"><span data-stu-id="9ca2f-153">**Reviewing authorizations**</span></span>

<span data-ttu-id="9ca2f-154">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9ca2f-154">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="9ca2f-155">**Updating authorizations**</span><span class="sxs-lookup"><span data-stu-id="9ca2f-155">**Updating authorizations**</span></span>

<span data-ttu-id="9ca2f-156">The circuit owner can modify authorizations by using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9ca2f-156">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="9ca2f-157">**Deleting authorizations**</span><span class="sxs-lookup"><span data-stu-id="9ca2f-157">**Deleting authorizations**</span></span>

<span data-ttu-id="9ca2f-158">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9ca2f-158">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="9ca2f-159">Circuit user operations</span><span class="sxs-lookup"><span data-stu-id="9ca2f-159">Circuit user operations</span></span>

<span data-ttu-id="9ca2f-160">**Reviewing authorizations**</span><span class="sxs-lookup"><span data-stu-id="9ca2f-160">**Reviewing authorizations**</span></span>

<span data-ttu-id="9ca2f-161">The circuit user can review authorizations by using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9ca2f-161">The circuit user can review authorizations by using the following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="9ca2f-162">**Redeeming link authorizations**</span><span class="sxs-lookup"><span data-stu-id="9ca2f-162">**Redeeming link authorizations**</span></span>

<span data-ttu-id="9ca2f-163">The circuit user can run the following cmdlet to redeem a link authorization:</span><span class="sxs-lookup"><span data-stu-id="9ca2f-163">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

## <a name="next-steps"></a><span data-ttu-id="9ca2f-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ca2f-164">Next steps</span></span>
<span data-ttu-id="9ca2f-165">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="9ca2f-165">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>


