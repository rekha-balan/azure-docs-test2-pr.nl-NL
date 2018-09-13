---
title: 'How to configure routing (peering) for an ExpressRoute circuit: Resource Manager: PowerShell: Azure | Microsoft Docs'
description: This article walks you through the steps for creating and provisioning the private, public and Microsoft peering of an ExpressRoute circuit. This article also shows you how to check the status, update, or delete peerings for your circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 160560fcc3d586d2bbcba67d2f7c60cfed26f5c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551673"
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="c5e53-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5e53-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager- Azure Portal](expressroute-howto-routing-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-routing-arm.md)
> * [Classic- PowerShell](expressroute-howto-routing-classic.md)
> * [Video - Private peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - Public peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> 
> 

<span data-ttu-id="c5e53-111">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="c5e53-111">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the Azure Resource Manager deployment model.</span></span>  <span data-ttu-id="c5e53-112">The steps below also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-112">The steps below also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> 

<span data-ttu-id="c5e53-113">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="c5e53-113">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="c5e53-114">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="c5e53-114">Configuration prerequisites</span></span>
* <span data-ttu-id="c5e53-115">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c5e53-115">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c5e53-116">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="c5e53-116">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> 
* <span data-ttu-id="c5e53-117">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="c5e53-117">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="c5e53-118">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-118">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="c5e53-119">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="c5e53-119">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="c5e53-120">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span><span class="sxs-lookup"><span data-stu-id="c5e53-120">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

<span data-ttu-id="c5e53-121">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span><span class="sxs-lookup"><span data-stu-id="c5e53-121">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="c5e53-122">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span><span class="sxs-lookup"><span data-stu-id="c5e53-122">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> We currently do not advertise peerings configured by service providers through the service management portal. We are working on enabling this capability soon. Please check with your service provider before configuring BGP peerings.
> 
> 

<span data-ttu-id="c5e53-126">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-126">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="c5e53-127">You can configure peerings in any order you choose.</span><span class="sxs-lookup"><span data-stu-id="c5e53-127">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="c5e53-128">However, you must make sure that you complete the configuration of each peering one at a time.</span><span class="sxs-lookup"><span data-stu-id="c5e53-128">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="c5e53-129">Azure private peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-129">Azure private peering</span></span>
<span data-ttu-id="c5e53-130">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-130">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="c5e53-131">To create Azure private peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-131">To create Azure private peering</span></span>
1. <span data-ttu-id="c5e53-132">Import the PowerShell module for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c5e53-132">Import the PowerShell module for ExpressRoute.</span></span>
   
     <span data-ttu-id="c5e53-133">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c5e53-133">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="c5e53-134">You will need to run PowerShell as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="c5e53-134">You will need to run PowerShell as an Administrator.</span></span>
   
        Install-Module AzureRM
   
        Install-AzureRM
   
    <span data-ttu-id="c5e53-135">Import all of the AzureRM.\* modules within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="c5e53-135">Import all of the AzureRM.\* modules within the known semantic version range.</span></span>
   
        Import-AzureRM
   
    <span data-ttu-id="c5e53-136">You can also just import a select module within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="c5e53-136">You can also just import a select module within the known semantic version range.</span></span> 
   
        Import-Module AzureRM.Network 
   
    <span data-ttu-id="c5e53-137">Logon to your account.</span><span class="sxs-lookup"><span data-stu-id="c5e53-137">Logon to your account.</span></span>
   
        Login-AzureRmAccount
   
    <span data-ttu-id="c5e53-138">Select the subscription you want to create ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-138">Select the subscription you want to create ExpressRoute circuit.</span></span>
   
        Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
2. <span data-ttu-id="c5e53-139">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-139">Create an ExpressRoute circuit.</span></span>
   
    <span data-ttu-id="c5e53-140">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="c5e53-140">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span> 
   
    <span data-ttu-id="c5e53-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span><span class="sxs-lookup"><span data-stu-id="c5e53-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="c5e53-142">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="c5e53-142">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="c5e53-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="c5e53-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span> 
3. <span data-ttu-id="c5e53-144">Check the ExpressRoute circuit to ensure it is provisioned.</span><span class="sxs-lookup"><span data-stu-id="c5e53-144">Check the ExpressRoute circuit to ensure it is provisioned.</span></span>
   
    <span data-ttu-id="c5e53-145">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span><span class="sxs-lookup"><span data-stu-id="c5e53-145">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="c5e53-146">See the example below.</span><span class="sxs-lookup"><span data-stu-id="c5e53-146">See the example below.</span></span>
   
        Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
   
    <span data-ttu-id="c5e53-147">The response will be something similar to the example below:</span><span class="sxs-lookup"><span data-stu-id="c5e53-147">The response will be something similar to the example below:</span></span>
   
        Name                             : ExpressRouteARMCircuit
        ResourceGroupName                : ExpressRouteResourceGroup
        Location                         : westus
        Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
        Etag                             : W/"################################"
        ProvisioningState                : Succeeded
        Sku                              : {
                                             "Name": "Standard_MeteredData",
                                             "Tier": "Standard",
                                             "Family": "MeteredData"
                                           }
        CircuitProvisioningState         : Enabled
        ServiceProviderProvisioningState : Provisioned
        ServiceProviderNotes             : 
        ServiceProviderProperties        : {
                                             "ServiceProviderName": "Equinix",
                                             "PeeringLocation": "Silicon Valley",
                                             "BandwidthInMbps": 200
                                           }
        ServiceKey                       : **************************************
        Peerings                         : []
4. <span data-ttu-id="c5e53-148">Configure Azure private peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-148">Configure Azure private peering for the circuit.</span></span>
   
    <span data-ttu-id="c5e53-149">Make sure that you have the following items before you proceed with the next steps:</span><span class="sxs-lookup"><span data-stu-id="c5e53-149">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="c5e53-150">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="c5e53-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c5e53-151">This must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="c5e53-151">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="c5e53-152">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="c5e53-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c5e53-153">This must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="c5e53-153">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="c5e53-154">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="c5e53-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c5e53-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="c5e53-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="c5e53-156">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="c5e53-156">AS number for peering.</span></span> <span data-ttu-id="c5e53-157">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="c5e53-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="c5e53-158">You can use a private AS number for this peering.</span><span class="sxs-lookup"><span data-stu-id="c5e53-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="c5e53-159">Ensure that you are not using 65515.</span><span class="sxs-lookup"><span data-stu-id="c5e53-159">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="c5e53-160">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="c5e53-160">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="c5e53-161">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="c5e53-161">**This is optional**.</span></span>
     
    <span data-ttu-id="c5e53-162">You can run the following cmdlet to configure Azure private peering for your circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-162">You can run the following cmdlet to configure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="c5e53-163">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="c5e53-163">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200</span></span>
     
        <span data-ttu-id="c5e53-164">Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt</span><span class="sxs-lookup"><span data-stu-id="c5e53-164">Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt</span></span>
     
    <span data-ttu-id="c5e53-165">You can use the cmdlet below if you choose to use an MD5 hash.</span><span class="sxs-lookup"><span data-stu-id="c5e53-165">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="c5e53-166">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="c5e53-166">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"</span></span>

     
   > [!IMPORTANT]
   > Ensure that you specify your AS number as peering ASN, not customer ASN.
   > 
   >


### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="c5e53-168">To view Azure private peering details</span><span class="sxs-lookup"><span data-stu-id="c5e53-168">To view Azure private peering details</span></span>
<span data-ttu-id="c5e53-169">You can get configuration details using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c5e53-169">You can get configuration details using the following cmdlet.</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt    


### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="c5e53-170">To update Azure private peering configuration</span><span class="sxs-lookup"><span data-stu-id="c5e53-170">To update Azure private peering configuration</span></span>
<span data-ttu-id="c5e53-171">You can update any part of the configuration using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c5e53-171">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="c5e53-172">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span><span class="sxs-lookup"><span data-stu-id="c5e53-172">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

    Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

    Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt


### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="c5e53-173">To delete Azure private peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-173">To delete Azure private peering</span></span>
<span data-ttu-id="c5e53-174">You can remove your peering configuration by running the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c5e53-174">You can remove your peering configuration by running the following cmdlet.</span></span>

> [!WARNING]
> You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet. 
> 
> 

    Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt
    Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt



## <a name="azure-public-peering"></a><span data-ttu-id="c5e53-176">Azure public peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-176">Azure public peering</span></span>
<span data-ttu-id="c5e53-177">This section provides instructions on how to create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-177">This section provides instructions on how to create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="c5e53-178">To create Azure public peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-178">To create Azure public peering</span></span>
1. <span data-ttu-id="c5e53-179">Import the PowerShell module for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c5e53-179">Import the PowerShell module for ExpressRoute.</span></span>
   
     <span data-ttu-id="c5e53-180">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c5e53-180">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="c5e53-181">You will need to run PowerShell as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="c5e53-181">You will need to run PowerShell as an Administrator.</span></span>
   
        Install-Module AzureRM
   
        Install-AzureRM
   
    <span data-ttu-id="c5e53-182">Import all of the AzureRM.\* modules within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="c5e53-182">Import all of the AzureRM.\* modules within the known semantic version range.</span></span>
   
        Import-AzureRM
   
    <span data-ttu-id="c5e53-183">You can also just import a select module within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="c5e53-183">You can also just import a select module within the known semantic version range.</span></span> 
   
        Import-Module AzureRM.Network 
   
    <span data-ttu-id="c5e53-184">Logon to your account.</span><span class="sxs-lookup"><span data-stu-id="c5e53-184">Logon to your account.</span></span>
   
        Login-AzureRmAccount
   
    <span data-ttu-id="c5e53-185">Select the subscription you want to create ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-185">Select the subscription you want to create ExpressRoute circuit.</span></span>
   
        Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
2. <span data-ttu-id="c5e53-186">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-186">Create an ExpressRoute circuit.</span></span>
   
    <span data-ttu-id="c5e53-187">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="c5e53-187">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span> 
   
    <span data-ttu-id="c5e53-188">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span><span class="sxs-lookup"><span data-stu-id="c5e53-188">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="c5e53-189">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="c5e53-189">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="c5e53-190">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="c5e53-190">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="c5e53-191">Check ExpressRoute circuit to ensure it is provisioned.</span><span class="sxs-lookup"><span data-stu-id="c5e53-191">Check ExpressRoute circuit to ensure it is provisioned.</span></span>
   
    <span data-ttu-id="c5e53-192">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span><span class="sxs-lookup"><span data-stu-id="c5e53-192">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="c5e53-193">See the example below.</span><span class="sxs-lookup"><span data-stu-id="c5e53-193">See the example below.</span></span>
   
        Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
   
    <span data-ttu-id="c5e53-194">The response will be something similar to the example below:</span><span class="sxs-lookup"><span data-stu-id="c5e53-194">The response will be something similar to the example below:</span></span>
   
        Name                             : ExpressRouteARMCircuit
        ResourceGroupName                : ExpressRouteResourceGroup
        Location                         : westus
        Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
        Etag                             : W/"################################"
        ProvisioningState                : Succeeded
        Sku                              : {
                                             "Name": "Standard_MeteredData",
                                             "Tier": "Standard",
                                             "Family": "MeteredData"
                                           }
        CircuitProvisioningState         : Enabled
        ServiceProviderProvisioningState : Provisioned
        ServiceProviderNotes             : 
        ServiceProviderProperties        : {
                                             "ServiceProviderName": "Equinix",
                                             "PeeringLocation": "Silicon Valley",
                                             "BandwidthInMbps": 200
                                           }
        ServiceKey                       : **************************************
        Peerings                         : []    
4. <span data-ttu-id="c5e53-195">Configure Azure public peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-195">Configure Azure public peering for the circuit.</span></span>
   
    <span data-ttu-id="c5e53-196">Make sure that you have the following information before you proceed further.</span><span class="sxs-lookup"><span data-stu-id="c5e53-196">Make sure that you have the following information before you proceed further.</span></span>
   
   * <span data-ttu-id="c5e53-197">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="c5e53-197">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c5e53-198">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="c5e53-198">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="c5e53-199">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="c5e53-199">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c5e53-200">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="c5e53-200">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="c5e53-201">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="c5e53-201">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c5e53-202">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="c5e53-202">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="c5e53-203">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="c5e53-203">AS number for peering.</span></span> <span data-ttu-id="c5e53-204">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="c5e53-204">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="c5e53-205">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="c5e53-205">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="c5e53-206">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="c5e53-206">**This is optional**.</span></span>

    
    <span data-ttu-id="c5e53-207">You can run the following cmdlet to configure Azure public peering for your circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-207">You can run the following cmdlet to configure Azure public peering for your circuit.</span></span>
     
        <span data-ttu-id="c5e53-208">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="c5e53-208">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100</span></span>

        <span data-ttu-id="c5e53-209">Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt</span><span class="sxs-lookup"><span data-stu-id="c5e53-209">Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt</span></span>
     
    <span data-ttu-id="c5e53-210">You can use the cmdlet below if you choose to use an MD5 hash.</span><span class="sxs-lookup"><span data-stu-id="c5e53-210">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="c5e53-211">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="c5e53-211">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"</span></span>

        <span data-ttu-id="c5e53-212">Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt</span><span class="sxs-lookup"><span data-stu-id="c5e53-212">Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt</span></span>

     
> [!IMPORTANT]
> Ensure that you specify your AS number as peering ASN, not customer ASN.
> 
>


### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="c5e53-214">To view Azure public peering details</span><span class="sxs-lookup"><span data-stu-id="c5e53-214">To view Azure public peering details</span></span>
<span data-ttu-id="c5e53-215">You can get configuration details using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c5e53-215">You can get configuration details using the following cmdlet:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="c5e53-216">To update Azure public peering configuration</span><span class="sxs-lookup"><span data-stu-id="c5e53-216">To update Azure public peering configuration</span></span>
<span data-ttu-id="c5e53-217">You can update any part of the configuration using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c5e53-217">You can update any part of the configuration using the following cmdlet:</span></span>

    Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600 

    Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt

<span data-ttu-id="c5e53-218">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span><span class="sxs-lookup"><span data-stu-id="c5e53-218">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span></span>

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="c5e53-219">To delete Azure public peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-219">To delete Azure public peering</span></span>
<span data-ttu-id="c5e53-220">You can remove your peering configuration by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c5e53-220">You can remove your peering configuration by running the following cmdlet:</span></span>

    Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
    Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt

## <a name="microsoft-peering"></a><span data-ttu-id="c5e53-221">Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-221">Microsoft peering</span></span>
<span data-ttu-id="c5e53-222">This section provides instructions on how to create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-222">This section provides instructions on how to create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="c5e53-223">To create Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-223">To create Microsoft peering</span></span>
1. <span data-ttu-id="c5e53-224">Import the PowerShell module for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c5e53-224">Import the PowerShell module for ExpressRoute.</span></span>
   
     <span data-ttu-id="c5e53-225">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c5e53-225">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="c5e53-226">You will need to run PowerShell as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="c5e53-226">You will need to run PowerShell as an Administrator.</span></span>
   
        Install-Module AzureRM
   
        Install-AzureRM
   
    <span data-ttu-id="c5e53-227">Import all of the AzureRM.\* modules within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="c5e53-227">Import all of the AzureRM.\* modules within the known semantic version range.</span></span>
   
        Import-AzureRM
   
    <span data-ttu-id="c5e53-228">You can also just import a select module within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="c5e53-228">You can also just import a select module within the known semantic version range.</span></span> 
   
        Import-Module AzureRM.Network 
   
    <span data-ttu-id="c5e53-229">Logon to your account.</span><span class="sxs-lookup"><span data-stu-id="c5e53-229">Logon to your account.</span></span>
   
        Login-AzureRmAccount
   
    <span data-ttu-id="c5e53-230">Select the subscription you want to create ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-230">Select the subscription you want to create ExpressRoute circuit.</span></span>
   
        Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
2. <span data-ttu-id="c5e53-231">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-231">Create an ExpressRoute circuit.</span></span>
   
    <span data-ttu-id="c5e53-232">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="c5e53-232">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span> 
   
    <span data-ttu-id="c5e53-233">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span><span class="sxs-lookup"><span data-stu-id="c5e53-233">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="c5e53-234">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="c5e53-234">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="c5e53-235">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="c5e53-235">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="c5e53-236">Check ExpressRoute circuit to ensure it is provisioned.</span><span class="sxs-lookup"><span data-stu-id="c5e53-236">Check ExpressRoute circuit to ensure it is provisioned.</span></span>
   
    <span data-ttu-id="c5e53-237">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span><span class="sxs-lookup"><span data-stu-id="c5e53-237">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="c5e53-238">See the example below.</span><span class="sxs-lookup"><span data-stu-id="c5e53-238">See the example below.</span></span>
   
        Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
   
    <span data-ttu-id="c5e53-239">The response will be something similar to the example below:</span><span class="sxs-lookup"><span data-stu-id="c5e53-239">The response will be something similar to the example below:</span></span>
   
        Name                             : ExpressRouteARMCircuit
        ResourceGroupName                : ExpressRouteResourceGroup
        Location                         : westus
        Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
        Etag                             : W/"################################"
        ProvisioningState                : Succeeded
        Sku                              : {
                                             "Name": "Standard_MeteredData",
                                             "Tier": "Standard",
                                             "Family": "MeteredData"
                                           }
        CircuitProvisioningState         : Enabled
        ServiceProviderProvisioningState : Provisioned
        ServiceProviderNotes             : 
        ServiceProviderProperties        : {
                                             "ServiceProviderName": "Equinix",
                                             "PeeringLocation": "Silicon Valley",
                                             "BandwidthInMbps": 200
                                           }
        ServiceKey                       : **************************************
        Peerings                         : []    
4. <span data-ttu-id="c5e53-240">Configure Microsoft peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="c5e53-240">Configure Microsoft peering for the circuit.</span></span>
   
    <span data-ttu-id="c5e53-241">Make sure that you have the following information before you proceed.</span><span class="sxs-lookup"><span data-stu-id="c5e53-241">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="c5e53-242">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="c5e53-242">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c5e53-243">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="c5e53-243">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="c5e53-244">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="c5e53-244">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c5e53-245">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="c5e53-245">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="c5e53-246">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="c5e53-246">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c5e53-247">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="c5e53-247">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="c5e53-248">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="c5e53-248">AS number for peering.</span></span> <span data-ttu-id="c5e53-249">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="c5e53-249">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="c5e53-250">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span><span class="sxs-lookup"><span data-stu-id="c5e53-250">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="c5e53-251">Only public IP address prefixes are accepted.</span><span class="sxs-lookup"><span data-stu-id="c5e53-251">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="c5e53-252">You can send a comma separated list if you plan to send a set of prefixes.</span><span class="sxs-lookup"><span data-stu-id="c5e53-252">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="c5e53-253">These prefixes must be registered to you in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="c5e53-253">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="c5e53-254">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span><span class="sxs-lookup"><span data-stu-id="c5e53-254">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="c5e53-255">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="c5e53-255">**This is optional**.</span></span>
   * <span data-ttu-id="c5e53-256">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span><span class="sxs-lookup"><span data-stu-id="c5e53-256">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="c5e53-257">An MD5 hash, if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="c5e53-257">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="c5e53-258">**This is optional.**</span><span class="sxs-lookup"><span data-stu-id="c5e53-258">**This is optional.**</span></span>
     
    <span data-ttu-id="c5e53-259">You can run the following cmdlet to configure Microsoft peering for your circuit</span><span class="sxs-lookup"><span data-stu-id="c5e53-259">You can run the following cmdlet to configure Microsoft peering for your circuit</span></span>
     
        <span data-ttu-id="c5e53-260">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"</span><span class="sxs-lookup"><span data-stu-id="c5e53-260">Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"</span></span>
     
        <span data-ttu-id="c5e53-261">Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt</span><span class="sxs-lookup"><span data-stu-id="c5e53-261">Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt</span></span>

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="c5e53-262">To get Microsoft peering details</span><span class="sxs-lookup"><span data-stu-id="c5e53-262">To get Microsoft peering details</span></span>
<span data-ttu-id="c5e53-263">You can get configuration details using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c5e53-263">You can get configuration details using the following cmdlet:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt


### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="c5e53-264">To update Microsoft peering configuration</span><span class="sxs-lookup"><span data-stu-id="c5e53-264">To update Microsoft peering configuration</span></span>
<span data-ttu-id="c5e53-265">You can update any part of the configuration using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c5e53-265">You can update any part of the configuration using the following cmdlet:</span></span>

    Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

    Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt


### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="c5e53-266">To delete Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="c5e53-266">To delete Microsoft peering</span></span>
<span data-ttu-id="c5e53-267">You can remove your peering configuration by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c5e53-267">You can remove your peering configuration by running the following cmdlet:</span></span>

    Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

    Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt

## <a name="next-steps"></a><span data-ttu-id="c5e53-268">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5e53-268">Next steps</span></span>
<span data-ttu-id="c5e53-269">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c5e53-269">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="c5e53-270">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="c5e53-270">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="c5e53-271">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="c5e53-271">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="c5e53-272">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c5e53-272">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>

