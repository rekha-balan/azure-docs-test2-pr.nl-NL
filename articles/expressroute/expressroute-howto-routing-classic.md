---
title: 'How to configure routing (peering) for an ExpressRoute circuit: Azure: classic | Microsoft Docs'
description: This article walks you through the steps for creating and provisioning the private, public and Microsoft peering of an ExpressRoute circuit. This article also shows you how to check the status, update, or delete peerings for your circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 6315e0fda231f2bfd3a92cf03cea7cd558bfda37
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549093"
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="c46b2-104">Create and modify peering for an ExpressRoute circuit (classic)</span><span class="sxs-lookup"><span data-stu-id="c46b2-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager- Azure Portal](expressroute-howto-routing-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-routing-arm.md)
> * [Classic- PowerShell](expressroute-howto-routing-classic.md)
> * [Video - Private peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - Public peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> 
> 

<span data-ttu-id="c46b2-111">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="c46b2-111">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span></span> <span data-ttu-id="c46b2-112">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c46b2-112">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="c46b2-113">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="c46b2-113">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="c46b2-114">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="c46b2-114">Configuration prerequisites</span></span>
* <span data-ttu-id="c46b2-115">You will need the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c46b2-115">You will need the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="c46b2-116">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="c46b2-116">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs).</span></span>  
* <span data-ttu-id="c46b2-117">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="c46b2-117">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="c46b2-118">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c46b2-118">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="c46b2-119">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="c46b2-119">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="c46b2-120">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span><span class="sxs-lookup"><span data-stu-id="c46b2-120">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

> [!IMPORTANT]
> These instructions only apply to circuits created with service providers offering Layer 2 connectivity services. If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.
> 
> 

<span data-ttu-id="c46b2-123">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c46b2-123">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="c46b2-124">You can configure peerings in any order you choose.</span><span class="sxs-lookup"><span data-stu-id="c46b2-124">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="c46b2-125">However, you must make sure that you complete the configuration of each peering one at a time.</span><span class="sxs-lookup"><span data-stu-id="c46b2-125">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>


### <a name="log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="c46b2-126">Log in to your Azure account and select a subscription</span><span class="sxs-lookup"><span data-stu-id="c46b2-126">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="c46b2-127">Open your PowerShell console with elevated rights and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="c46b2-127">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="c46b2-128">Use the following example to help you connect:</span><span class="sxs-lookup"><span data-stu-id="c46b2-128">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="c46b2-129">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="c46b2-129">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="c46b2-130">If you have more than one subscription, select the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="c46b2-130">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="c46b2-131">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="c46b2-131">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="c46b2-132">Azure private peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-132">Azure private peering</span></span>
<span data-ttu-id="c46b2-133">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c46b2-133">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="c46b2-134">To create Azure private peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-134">To create Azure private peering</span></span>
1. <span data-ttu-id="c46b2-135">**Import the PowerShell module for ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="c46b2-135">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="c46b2-136">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c46b2-136">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="c46b2-137">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="c46b2-137">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="c46b2-138">**Create an ExpressRoute circuit.**</span><span class="sxs-lookup"><span data-stu-id="c46b2-138">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="c46b2-139">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="c46b2-139">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="c46b2-140">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span><span class="sxs-lookup"><span data-stu-id="c46b2-140">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="c46b2-141">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="c46b2-141">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="c46b2-142">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="c46b2-142">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span> 
3. <span data-ttu-id="c46b2-143">**Check the ExpressRoute circuit to ensure it is provisioned.**</span><span class="sxs-lookup"><span data-stu-id="c46b2-143">**Check the ExpressRoute circuit to ensure it is provisioned.**</span></span>
   
    <span data-ttu-id="c46b2-144">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span><span class="sxs-lookup"><span data-stu-id="c46b2-144">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="c46b2-145">See the example below.</span><span class="sxs-lookup"><span data-stu-id="c46b2-145">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="c46b2-146">Make sure that the circuit shows as Provisioned and Enabled.</span><span class="sxs-lookup"><span data-stu-id="c46b2-146">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="c46b2-147">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span><span class="sxs-lookup"><span data-stu-id="c46b2-147">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="c46b2-148">**Configure Azure private peering for the circuit.**</span><span class="sxs-lookup"><span data-stu-id="c46b2-148">**Configure Azure private peering for the circuit.**</span></span>
   
    <span data-ttu-id="c46b2-149">Make sure that you have the following items before you proceed with the next steps:</span><span class="sxs-lookup"><span data-stu-id="c46b2-149">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="c46b2-150">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="c46b2-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c46b2-151">This must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="c46b2-151">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="c46b2-152">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="c46b2-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c46b2-153">This must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="c46b2-153">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="c46b2-154">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="c46b2-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c46b2-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="c46b2-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="c46b2-156">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="c46b2-156">AS number for peering.</span></span> <span data-ttu-id="c46b2-157">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="c46b2-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="c46b2-158">You can use a private AS number for this peering.</span><span class="sxs-lookup"><span data-stu-id="c46b2-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="c46b2-159">Ensure that you are not using 65515.</span><span class="sxs-lookup"><span data-stu-id="c46b2-159">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="c46b2-160">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="c46b2-160">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="c46b2-161">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="c46b2-161">**This is optional**.</span></span>
     
    <span data-ttu-id="c46b2-162">You can run the following cmdlet to configure Azure private peering for your circuit.</span><span class="sxs-lookup"><span data-stu-id="c46b2-162">You can run the following cmdlet to configure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="c46b2-163">New-AzureBGPPeering -AccessType Private -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="c46b2-163">New-AzureBGPPeering -AccessType Private -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="c46b2-164">You can use the cmdlet below if you choose to use an MD5 hash.</span><span class="sxs-lookup"><span data-stu-id="c46b2-164">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="c46b2-165">New-AzureBGPPeering -AccessType Private -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="c46b2-165">New-AzureBGPPeering -AccessType Private -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > Ensure that you specify your AS number as peering ASN, not customer ASN.
     > 
     > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="c46b2-167">To view Azure private peering details</span><span class="sxs-lookup"><span data-stu-id="c46b2-167">To view Azure private peering details</span></span>
<span data-ttu-id="c46b2-168">You can get configuration details using the following cmdlet</span><span class="sxs-lookup"><span data-stu-id="c46b2-168">You can get configuration details using the following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="c46b2-169">To update Azure private peering configuration</span><span class="sxs-lookup"><span data-stu-id="c46b2-169">To update Azure private peering configuration</span></span>
<span data-ttu-id="c46b2-170">You can update any part of the configuration using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c46b2-170">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="c46b2-171">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span><span class="sxs-lookup"><span data-stu-id="c46b2-171">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="c46b2-172">To delete Azure private peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-172">To delete Azure private peering</span></span>
<span data-ttu-id="c46b2-173">You can remove your peering configuration by running the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c46b2-173">You can remove your peering configuration by running the following cmdlet.</span></span>

> [!WARNING]
> You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="c46b2-175">Azure public peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-175">Azure public peering</span></span>
<span data-ttu-id="c46b2-176">This section provides instructions on how to create, get, update and delete the Azure public peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c46b2-176">This section provides instructions on how to create, get, update and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="c46b2-177">To create Azure public peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-177">To create Azure public peering</span></span>
1. <span data-ttu-id="c46b2-178">**Import the PowerShell module for ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="c46b2-178">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="c46b2-179">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c46b2-179">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="c46b2-180">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="c46b2-180">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="c46b2-181">**Create an ExpressRoute circuit**</span><span class="sxs-lookup"><span data-stu-id="c46b2-181">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="c46b2-182">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="c46b2-182">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="c46b2-183">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span><span class="sxs-lookup"><span data-stu-id="c46b2-183">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="c46b2-184">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="c46b2-184">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="c46b2-185">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="c46b2-185">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="c46b2-186">**Check ExpressRoute circuit to ensure it is provisioned**</span><span class="sxs-lookup"><span data-stu-id="c46b2-186">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="c46b2-187">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span><span class="sxs-lookup"><span data-stu-id="c46b2-187">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="c46b2-188">See the example below.</span><span class="sxs-lookup"><span data-stu-id="c46b2-188">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="c46b2-189">Make sure that the circuit shows as Provisioned and Enabled.</span><span class="sxs-lookup"><span data-stu-id="c46b2-189">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="c46b2-190">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span><span class="sxs-lookup"><span data-stu-id="c46b2-190">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="c46b2-191">**Configure Azure public peering for the circuit**</span><span class="sxs-lookup"><span data-stu-id="c46b2-191">**Configure Azure public peering for the circuit**</span></span>
   
    <span data-ttu-id="c46b2-192">Ensure that you have the following information before you proceed further.</span><span class="sxs-lookup"><span data-stu-id="c46b2-192">Ensure that you have the following information before you proceed further.</span></span>
   
   * <span data-ttu-id="c46b2-193">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="c46b2-193">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c46b2-194">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="c46b2-194">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="c46b2-195">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="c46b2-195">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c46b2-196">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="c46b2-196">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="c46b2-197">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="c46b2-197">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c46b2-198">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="c46b2-198">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="c46b2-199">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="c46b2-199">AS number for peering.</span></span> <span data-ttu-id="c46b2-200">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="c46b2-200">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="c46b2-201">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="c46b2-201">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="c46b2-202">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="c46b2-202">**This is optional**.</span></span>
     
    <span data-ttu-id="c46b2-203">You can run the following cmdlet to configure Azure public peering for your circuit</span><span class="sxs-lookup"><span data-stu-id="c46b2-203">You can run the following cmdlet to configure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="c46b2-204">New-AzureBGPPeering -AccessType Public -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="c46b2-204">New-AzureBGPPeering -AccessType Public -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="c46b2-205">You can use the cmdlet below if you choose to use an MD5 hash</span><span class="sxs-lookup"><span data-stu-id="c46b2-205">You can use the cmdlet below if you choose to use an MD5 hash</span></span>
     
        <span data-ttu-id="c46b2-206">New-AzureBGPPeering -AccessType Public -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="c46b2-206">New-AzureBGPPeering -AccessType Public -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > Ensure that you specify your AS number as peering ASN and not customer ASN.
     > 
     > 

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="c46b2-208">To view Azure public peering details</span><span class="sxs-lookup"><span data-stu-id="c46b2-208">To view Azure public peering details</span></span>
<span data-ttu-id="c46b2-209">You can get configuration details using the following cmdlet</span><span class="sxs-lookup"><span data-stu-id="c46b2-209">You can get configuration details using the following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="c46b2-210">To update Azure public peering configuration</span><span class="sxs-lookup"><span data-stu-id="c46b2-210">To update Azure public peering configuration</span></span>
<span data-ttu-id="c46b2-211">You can update any part of the configuration using the following cmdlet</span><span class="sxs-lookup"><span data-stu-id="c46b2-211">You can update any part of the configuration using the following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="c46b2-212">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span><span class="sxs-lookup"><span data-stu-id="c46b2-212">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span></span>

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="c46b2-213">To delete Azure public peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-213">To delete Azure public peering</span></span>
<span data-ttu-id="c46b2-214">You can remove your peering configuration by running the following cmdlet</span><span class="sxs-lookup"><span data-stu-id="c46b2-214">You can remove your peering configuration by running the following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="c46b2-215">Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-215">Microsoft peering</span></span>
<span data-ttu-id="c46b2-216">This section provides instructions on how to create, get, update and delete the Microsoft peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="c46b2-216">This section provides instructions on how to create, get, update and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="c46b2-217">To create Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-217">To create Microsoft peering</span></span>
1. <span data-ttu-id="c46b2-218">**Import the PowerShell module for ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="c46b2-218">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="c46b2-219">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c46b2-219">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="c46b2-220">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="c46b2-220">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="c46b2-221">**Create an ExpressRoute circuit**</span><span class="sxs-lookup"><span data-stu-id="c46b2-221">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="c46b2-222">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="c46b2-222">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="c46b2-223">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span><span class="sxs-lookup"><span data-stu-id="c46b2-223">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="c46b2-224">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="c46b2-224">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="c46b2-225">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="c46b2-225">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="c46b2-226">**Check ExpressRoute circuit to ensure it is provisioned**</span><span class="sxs-lookup"><span data-stu-id="c46b2-226">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="c46b2-227">You must first check to see if the ExpressRoute circuit is in Provisioned and Enabled state.</span><span class="sxs-lookup"><span data-stu-id="c46b2-227">You must first check to see if the ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="c46b2-228">Make sure that the circuit shows as Provisioned and Enabled.</span><span class="sxs-lookup"><span data-stu-id="c46b2-228">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="c46b2-229">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span><span class="sxs-lookup"><span data-stu-id="c46b2-229">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="c46b2-230">**Configure Microsoft peering for the circuit**</span><span class="sxs-lookup"><span data-stu-id="c46b2-230">**Configure Microsoft peering for the circuit**</span></span>
   
    <span data-ttu-id="c46b2-231">Make sure that you have the following information before you proceed.</span><span class="sxs-lookup"><span data-stu-id="c46b2-231">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="c46b2-232">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="c46b2-232">A /30 subnet for the primary link.</span></span> <span data-ttu-id="c46b2-233">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="c46b2-233">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="c46b2-234">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="c46b2-234">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="c46b2-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="c46b2-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="c46b2-236">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="c46b2-236">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="c46b2-237">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="c46b2-237">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="c46b2-238">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="c46b2-238">AS number for peering.</span></span> <span data-ttu-id="c46b2-239">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="c46b2-239">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="c46b2-240">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span><span class="sxs-lookup"><span data-stu-id="c46b2-240">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="c46b2-241">Only public IP address prefixes are accepted.</span><span class="sxs-lookup"><span data-stu-id="c46b2-241">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="c46b2-242">You can send a comma separated list if you plan to send a set of prefixes.</span><span class="sxs-lookup"><span data-stu-id="c46b2-242">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="c46b2-243">These prefixes must be registered to you in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="c46b2-243">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="c46b2-244">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span><span class="sxs-lookup"><span data-stu-id="c46b2-244">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="c46b2-245">**This is optional**.</span><span class="sxs-lookup"><span data-stu-id="c46b2-245">**This is optional**.</span></span>
   * <span data-ttu-id="c46b2-246">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span><span class="sxs-lookup"><span data-stu-id="c46b2-246">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="c46b2-247">An MD5 hash, if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="c46b2-247">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="c46b2-248">**This is optional.**</span><span class="sxs-lookup"><span data-stu-id="c46b2-248">**This is optional.**</span></span>
     
    <span data-ttu-id="c46b2-249">You can run the following cmdlet to configure Microsoft pering for your circuit</span><span class="sxs-lookup"><span data-stu-id="c46b2-249">You can run the following cmdlet to configure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="c46b2-250">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="c46b2-250">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="c46b2-251">To view Microsoft peering details</span><span class="sxs-lookup"><span data-stu-id="c46b2-251">To view Microsoft peering details</span></span>
<span data-ttu-id="c46b2-252">You can get configuration details using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c46b2-252">You can get configuration details using the following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="c46b2-253">To update Microsoft peering configuration</span><span class="sxs-lookup"><span data-stu-id="c46b2-253">To update Microsoft peering configuration</span></span>
<span data-ttu-id="c46b2-254">You can update any part of the configuration using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c46b2-254">You can update any part of the configuration using the following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="c46b2-255">To delete Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="c46b2-255">To delete Microsoft peering</span></span>
<span data-ttu-id="c46b2-256">You can remove your peering configuration by running the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c46b2-256">You can remove your peering configuration by running the following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="c46b2-257">Next steps</span><span class="sxs-lookup"><span data-stu-id="c46b2-257">Next steps</span></span>
<span data-ttu-id="c46b2-258">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c46b2-258">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="c46b2-259">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="c46b2-259">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="c46b2-260">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="c46b2-260">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

