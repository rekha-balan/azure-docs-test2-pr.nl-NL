---
title: 'How to configure routing (peering) for an ExpressRoute circuit: Resource Manager: PowerShell: Azure | Microsoft Docs'
description: This article walks you through the steps for creating and provisioning the private, public and Microsoft peering of an ExpressRoute circuit. This article also shows you how to check the status, update, or delete peerings for your circuit.
documentationcenter: na
services: expressroute
author: osamazia
manager: jonor
editor: ''
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 1/3/2018
ms.author: osamaz, jaredr80
ms.openlocfilehash: d4f8f0e6c8fab5dfb4efcc4f1659ba90336c8bf0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44785270"
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="59152-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span><span class="sxs-lookup"><span data-stu-id="59152-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="59152-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59152-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="59152-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="59152-107">If you want to use a different method to work with your circuit, select an article from the following list:</span><span class="sxs-lookup"><span data-stu-id="59152-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [Video - Private peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - Public peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (classic)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="59152-115">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="59152-115">Configuration prerequisites</span></span>

* <span data-ttu-id="59152-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="59152-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="59152-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="59152-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="59152-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="59152-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="59152-119">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="59152-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="59152-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="59152-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span><span class="sxs-lookup"><span data-stu-id="59152-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="59152-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span><span class="sxs-lookup"><span data-stu-id="59152-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="59152-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span><span class="sxs-lookup"><span data-stu-id="59152-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> We currently do not advertise peerings configured by service providers through the service management portal. We are working on enabling this capability soon. Check with your service provider before configuring BGP peerings.
> 
> 

<span data-ttu-id="59152-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="59152-128">You can configure peerings in any order you choose.</span><span class="sxs-lookup"><span data-stu-id="59152-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="59152-129">However, you must make sure that you complete the configuration of each peering one at a time.</span><span class="sxs-lookup"><span data-stu-id="59152-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> <span data-ttu-id="59152-130">For more information about routing domains and peerings, see [ExpressRoute routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="59152-130">For more information about routing domains and peerings, see [ExpressRoute routing domains](expressroute-circuit-peerings.md).</span></span>

## <a name="msft"></a><span data-ttu-id="59152-131">Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="59152-131">Microsoft peering</span></span>

<span data-ttu-id="59152-132">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-132">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined. Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit. For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="59152-136">To create Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="59152-136">To create Microsoft peering</span></span>

1. <span data-ttu-id="59152-137">Import the PowerShell module for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="59152-137">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="59152-138">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="59152-138">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="59152-139">You will need to run PowerShell as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="59152-139">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="59152-140">Import all of the AzureRM.\* modules within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="59152-140">Import all of the AzureRM.\* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="59152-141">You can also just import a select module within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="59152-141">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="59152-142">Sign in to your account.</span><span class="sxs-lookup"><span data-stu-id="59152-142">Sign in to your account.</span></span>

  ```powershell
  Connect-AzureRmAccount
  ```

  <span data-ttu-id="59152-143">Select the subscription you want to create ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-143">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="59152-144">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-144">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="59152-145">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="59152-145">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="59152-146">f your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Microsoft peering for you.</span><span class="sxs-lookup"><span data-stu-id="59152-146">f your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Microsoft peering for you.</span></span> <span data-ttu-id="59152-147">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="59152-147">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="59152-148">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span><span class="sxs-lookup"><span data-stu-id="59152-148">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span> 

3. <span data-ttu-id="59152-149">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span><span class="sxs-lookup"><span data-stu-id="59152-149">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="59152-150">Use the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-150">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="59152-151">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-151">The response is similar to the following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="59152-152">Configure Microsoft peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-152">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="59152-153">Make sure that you have the following information before you proceed.</span><span class="sxs-lookup"><span data-stu-id="59152-153">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="59152-154">A /30 or /126 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="59152-154">A /30 or /126 subnet for the primary link.</span></span> <span data-ttu-id="59152-155">This must be a valid public IPv4 or IPv6 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="59152-155">This must be a valid public IPv4 or IPv6 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="59152-156">A /30 or /126 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="59152-156">A /30 or /126 subnet for the secondary link.</span></span> <span data-ttu-id="59152-157">This must be a valid public IPv4 or IPv6 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="59152-157">This must be a valid public IPv4 or IPv6 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="59152-158">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="59152-158">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="59152-159">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="59152-159">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="59152-160">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="59152-160">AS number for peering.</span></span> <span data-ttu-id="59152-161">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="59152-161">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="59152-162">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span><span class="sxs-lookup"><span data-stu-id="59152-162">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="59152-163">Only public IP address prefixes are accepted.</span><span class="sxs-lookup"><span data-stu-id="59152-163">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="59152-164">If you plan to send a set of prefixes, you can send a comma-separated list.</span><span class="sxs-lookup"><span data-stu-id="59152-164">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="59152-165">These prefixes must be registered to you in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="59152-165">These prefixes must be registered to you in an RIR / IRR.</span></span> <span data-ttu-id="59152-166">IPv4 BGP sessions require IPv4 advertised prefixes and IPv6 BGP sessions require IPv6 advertised prefixes.</span><span class="sxs-lookup"><span data-stu-id="59152-166">IPv4 BGP sessions require IPv4 advertised prefixes and IPv6 BGP sessions require IPv6 advertised prefixes.</span></span> 
  * <span data-ttu-id="59152-167">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span><span class="sxs-lookup"><span data-stu-id="59152-167">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="59152-168">Optional:</span><span class="sxs-lookup"><span data-stu-id="59152-168">Optional:</span></span>
    * <span data-ttu-id="59152-169">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span><span class="sxs-lookup"><span data-stu-id="59152-169">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
    * <span data-ttu-id="59152-170">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="59152-170">An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="59152-171">Use the following example to configure Microsoft peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="59152-171">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PeerAddressType IPv4 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PeerAddressType IPv6 -PrimaryPeerAddressPrefix "3FFE:FFFF:0:CD30::/126" -SecondaryPeerAddressPrefix "3FFE:FFFF:0:CD30::4/126" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "3FFE:FFFF:0:CD31::/120" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="getmsft"></a><span data-ttu-id="59152-172">To get Microsoft peering details</span><span class="sxs-lookup"><span data-stu-id="59152-172">To get Microsoft peering details</span></span>

<span data-ttu-id="59152-173">You can get configuration details using the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-173">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="updatemsft"></a><span data-ttu-id="59152-174">To update Microsoft peering configuration</span><span class="sxs-lookup"><span data-stu-id="59152-174">To update Microsoft peering configuration</span></span>

<span data-ttu-id="59152-175">You can update any part of the configuration using the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-175">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PeerAddressType IPv4 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PeerAddressType IPv6 -PrimaryPeerAddressPrefix "3FFE:FFFF:0:CD30::/126" -SecondaryPeerAddressPrefix "3FFE:FFFF:0:CD30::4/126" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "3FFE:FFFF:0:CD31::/120" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="deletemsft"></a><span data-ttu-id="59152-176">To delete Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="59152-176">To delete Microsoft peering</span></span>

<span data-ttu-id="59152-177">You can remove your peering configuration by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="59152-177">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="private"></a><span data-ttu-id="59152-178">Azure private peering</span><span class="sxs-lookup"><span data-stu-id="59152-178">Azure private peering</span></span>

<span data-ttu-id="59152-179">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-179">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="59152-180">To create Azure private peering</span><span class="sxs-lookup"><span data-stu-id="59152-180">To create Azure private peering</span></span>

1. <span data-ttu-id="59152-181">Import the PowerShell module for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="59152-181">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="59152-182">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="59152-182">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="59152-183">You will need to run PowerShell as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="59152-183">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="59152-184">Import all of the AzureRM.\* modules within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="59152-184">Import all of the AzureRM.\* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="59152-185">You can also just import a select module within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="59152-185">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="59152-186">Sign in to your account.</span><span class="sxs-lookup"><span data-stu-id="59152-186">Sign in to your account.</span></span>

  ```powershell
  Connect-AzureRmAccount
  ```

  <span data-ttu-id="59152-187">Select the subscription you want to create ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-187">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="59152-188">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-188">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="59152-189">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="59152-189">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="59152-190">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Azure private peering for you.</span><span class="sxs-lookup"><span data-stu-id="59152-190">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="59152-191">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="59152-191">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="59152-192">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span><span class="sxs-lookup"><span data-stu-id="59152-192">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="59152-193">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span><span class="sxs-lookup"><span data-stu-id="59152-193">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="59152-194">Use the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-194">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="59152-195">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-195">The response is similar to the following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="59152-196">Configure Azure private peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-196">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="59152-197">Make sure that you have the following items before you proceed with the next steps:</span><span class="sxs-lookup"><span data-stu-id="59152-197">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="59152-198">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="59152-198">A /30 subnet for the primary link.</span></span> <span data-ttu-id="59152-199">The subnet must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="59152-199">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="59152-200">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="59152-200">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="59152-201">The subnet must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="59152-201">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="59152-202">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="59152-202">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="59152-203">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="59152-203">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="59152-204">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="59152-204">AS number for peering.</span></span> <span data-ttu-id="59152-205">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="59152-205">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="59152-206">You can use a private AS number for this peering.</span><span class="sxs-lookup"><span data-stu-id="59152-206">You can use a private AS number for this peering.</span></span> <span data-ttu-id="59152-207">Ensure that you are not using 65515.</span><span class="sxs-lookup"><span data-stu-id="59152-207">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="59152-208">Optional:</span><span class="sxs-lookup"><span data-stu-id="59152-208">Optional:</span></span>
    * <span data-ttu-id="59152-209">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="59152-209">An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="59152-210">Use the following example to configure Azure private peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="59152-210">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="59152-211">If you choose to use an MD5 hash, use the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-211">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Ensure that you specify your AS number as peering ASN, not customer ASN.
  > 
  >

### <a name="getprivate"></a><span data-ttu-id="59152-213">To get Azure private peering details</span><span class="sxs-lookup"><span data-stu-id="59152-213">To get Azure private peering details</span></span>

<span data-ttu-id="59152-214">You can get configuration details by using the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-214">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt
```

### <a name="updateprivate"></a><span data-ttu-id="59152-215">To update Azure private peering configuration</span><span class="sxs-lookup"><span data-stu-id="59152-215">To update Azure private peering configuration</span></span>

<span data-ttu-id="59152-216">You can update any part of the configuration using the following example.</span><span class="sxs-lookup"><span data-stu-id="59152-216">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="59152-217">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span><span class="sxs-lookup"><span data-stu-id="59152-217">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="deleteprivate"></a><span data-ttu-id="59152-218">To delete Azure private peering</span><span class="sxs-lookup"><span data-stu-id="59152-218">To delete Azure private peering</span></span>

<span data-ttu-id="59152-219">You can remove your peering configuration by running the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-219">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="public"></a><span data-ttu-id="59152-221">Azure public peering</span><span class="sxs-lookup"><span data-stu-id="59152-221">Azure public peering</span></span>

<span data-ttu-id="59152-222">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-222">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="59152-223">To create Azure public peering</span><span class="sxs-lookup"><span data-stu-id="59152-223">To create Azure public peering</span></span>

1. <span data-ttu-id="59152-224">Import the PowerShell module for ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="59152-224">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="59152-225">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="59152-225">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="59152-226">You will need to run PowerShell as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="59152-226">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="59152-227">Import all of the AzureRM.\* modules within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="59152-227">Import all of the AzureRM.\* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="59152-228">You can also just import a select module within the known semantic version range.</span><span class="sxs-lookup"><span data-stu-id="59152-228">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="59152-229">Sign in to your account.</span><span class="sxs-lookup"><span data-stu-id="59152-229">Sign in to your account.</span></span>

  ```powershell
  Connect-AzureRmAccount
  ```

  <span data-ttu-id="59152-230">Select the subscription you want to create ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-230">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="59152-231">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-231">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="59152-232">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="59152-232">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="59152-233">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Azure public peering for you.</span><span class="sxs-lookup"><span data-stu-id="59152-233">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="59152-234">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="59152-234">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="59152-235">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span><span class="sxs-lookup"><span data-stu-id="59152-235">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="59152-236">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span><span class="sxs-lookup"><span data-stu-id="59152-236">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="59152-237">Use the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-237">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="59152-238">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-238">The response is similar to the following example:</span></span>

  ```
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
  ```
4. <span data-ttu-id="59152-239">Configure Azure public peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="59152-239">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="59152-240">Make sure that you have the following information before you proceed further.</span><span class="sxs-lookup"><span data-stu-id="59152-240">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="59152-241">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="59152-241">A /30 subnet for the primary link.</span></span> <span data-ttu-id="59152-242">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="59152-242">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="59152-243">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="59152-243">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="59152-244">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="59152-244">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="59152-245">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="59152-245">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="59152-246">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="59152-246">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="59152-247">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="59152-247">AS number for peering.</span></span> <span data-ttu-id="59152-248">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="59152-248">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="59152-249">Optional:</span><span class="sxs-lookup"><span data-stu-id="59152-249">Optional:</span></span>
    * <span data-ttu-id="59152-250">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="59152-250">An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="59152-251">Run the following example to configure Azure public peering for your circuit</span><span class="sxs-lookup"><span data-stu-id="59152-251">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="59152-252">If you choose to use an MD5 hash, use the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-252">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > Ensure that you specify your AS number as peering ASN, not customer ASN.
  > 
  >

### <a name="getpublic"></a><span data-ttu-id="59152-254">To get Azure public peering details</span><span class="sxs-lookup"><span data-stu-id="59152-254">To get Azure public peering details</span></span>

<span data-ttu-id="59152-255">You can get configuration details using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="59152-255">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="updatepublic"></a><span data-ttu-id="59152-256">To update Azure public peering configuration</span><span class="sxs-lookup"><span data-stu-id="59152-256">To update Azure public peering configuration</span></span>

<span data-ttu-id="59152-257">You can update any part of the configuration using the following example.</span><span class="sxs-lookup"><span data-stu-id="59152-257">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="59152-258">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span><span class="sxs-lookup"><span data-stu-id="59152-258">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="deletepublic"></a><span data-ttu-id="59152-259">To delete Azure public peering</span><span class="sxs-lookup"><span data-stu-id="59152-259">To delete Azure public peering</span></span>

<span data-ttu-id="59152-260">You can remove your peering configuration by running the following example:</span><span class="sxs-lookup"><span data-stu-id="59152-260">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="59152-261">Next steps</span><span class="sxs-lookup"><span data-stu-id="59152-261">Next steps</span></span>

<span data-ttu-id="59152-262">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="59152-262">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="59152-263">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="59152-263">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="59152-264">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="59152-264">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="59152-265">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59152-265">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
