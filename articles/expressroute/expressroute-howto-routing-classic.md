---
title: 'How to configure routing (peering) for an ExpressRoute circuit: Azure: classic | Microsoft Docs'
description: This article walks you through the steps for creating and provisioning the private, public and Microsoft peering of an ExpressRoute circuit. This article also shows you how to check the status, update, or delete peerings for your circuit.
services: expressroute
author: cherylmc
ms.service: expressroute
ms.topic: conceptual
ms.date: 07/27/2018
ms.author: cherylmc;ganesr
ms.openlocfilehash: 14e96a36eed99d9967ac6f8188a161c922d6f334
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830739"
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="d953e-104">Create and modify peering for an ExpressRoute circuit (classic)</span><span class="sxs-lookup"><span data-stu-id="d953e-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [Video - Private peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - Public peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (classic)](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="d953e-112">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="d953e-112">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span></span> <span data-ttu-id="d953e-113">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d953e-113">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="d953e-114">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d953e-114">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="d953e-115">You can configure peerings in any order you choose.</span><span class="sxs-lookup"><span data-stu-id="d953e-115">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="d953e-116">However, you must make sure that you complete the configuration of each peering one at a time.</span><span class="sxs-lookup"><span data-stu-id="d953e-116">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

<span data-ttu-id="d953e-117">These instructions only apply to circuits created with service providers that offer Layer 2 connectivity services.</span><span class="sxs-lookup"><span data-stu-id="d953e-117">These instructions only apply to circuits created with service providers that offer Layer 2 connectivity services.</span></span> <span data-ttu-id="d953e-118">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span><span class="sxs-lookup"><span data-stu-id="d953e-118">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="d953e-119">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="d953e-119">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="d953e-120">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="d953e-120">Configuration prerequisites</span></span>

* <span data-ttu-id="d953e-121">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="d953e-121">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="d953e-122">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d953e-122">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="d953e-123">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="d953e-123">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="d953e-124">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span><span class="sxs-lookup"><span data-stu-id="d953e-124">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

### <a name="download-the-latest-powershell-cmdlets"></a><span data-ttu-id="d953e-125">Download the latest PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="d953e-125">Download the latest PowerShell cmdlets</span></span>

<span data-ttu-id="d953e-126">Install the latest versions of the Azure Service Management (SM) PowerShell modules and the ExpressRoute module.</span><span class="sxs-lookup"><span data-stu-id="d953e-126">Install the latest versions of the Azure Service Management (SM) PowerShell modules and the ExpressRoute module.</span></span> <span data-ttu-id="d953e-127">When using the following example, note that the version number (in this example, 5.1.1) will change as newer versions of the cmdlets are released.</span><span class="sxs-lookup"><span data-stu-id="d953e-127">When using the following example, note that the version number (in this example, 5.1.1) will change as newer versions of the cmdlets are released.</span></span>

```powershell
Import-Module 'C:\Program Files\WindowsPowerShell\Modules\Azure\5.1.1\Azure\Azure.psd1'
Import-Module 'C:\Program Files\WindowsPowerShell\Modules\Azure\5.1.1\ExpressRoute\ExpressRoute.psd1'
```

<span data-ttu-id="d953e-128">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="d953e-128">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="sign-in"></a><span data-ttu-id="d953e-129">Sign in</span><span class="sxs-lookup"><span data-stu-id="d953e-129">Sign in</span></span>

<span data-ttu-id="d953e-130">To sign in to your Azure account, use the following examples:</span><span class="sxs-lookup"><span data-stu-id="d953e-130">To sign in to your Azure account, use the following examples:</span></span>

1. <span data-ttu-id="d953e-131">Open your PowerShell console with elevated rights and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="d953e-131">Open your PowerShell console with elevated rights and connect to your account.</span></span>

  ```powershell
  Connect-AzureRmAccount
  ```
2. <span data-ttu-id="d953e-132">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="d953e-132">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="d953e-133">If you have more than one subscription, select the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="d953e-133">If you have more than one subscription, select the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

4. <span data-ttu-id="d953e-134">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="d953e-134">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

  ```powershell
  Add-AzureAccount
  ```

## <a name="azure-private-peering"></a><span data-ttu-id="d953e-135">Azure private peering</span><span class="sxs-lookup"><span data-stu-id="d953e-135">Azure private peering</span></span>

<span data-ttu-id="d953e-136">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d953e-136">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="d953e-137">To create Azure private peering</span><span class="sxs-lookup"><span data-stu-id="d953e-137">To create Azure private peering</span></span>

1. <span data-ttu-id="d953e-138">**Create an ExpressRoute circuit.**</span><span class="sxs-lookup"><span data-stu-id="d953e-138">**Create an ExpressRoute circuit.**</span></span>

  <span data-ttu-id="d953e-139">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="d953e-139">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="d953e-140">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span><span class="sxs-lookup"><span data-stu-id="d953e-140">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="d953e-141">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="d953e-141">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="d953e-142">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="d953e-142">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
2. <span data-ttu-id="d953e-143">**Check the ExpressRoute circuit to make sure it is provisioned.**</span><span class="sxs-lookup"><span data-stu-id="d953e-143">**Check the ExpressRoute circuit to make sure it is provisioned.**</span></span>
   
  <span data-ttu-id="d953e-144">Check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span><span class="sxs-lookup"><span data-stu-id="d953e-144">Check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit -ServiceKey "*********************************"
  ```

  <span data-ttu-id="d953e-145">Return:</span><span class="sxs-lookup"><span data-stu-id="d953e-145">Return:</span></span>

  ```powershell
  Bandwidth                        : 200
  CircuitName                      : MyTestCircuit
  Location                         : Silicon Valley
  ServiceKey                       : *********************************
  ServiceProviderName              : equinix
  ServiceProviderProvisioningState : Provisioned
  Sku                              : Standard
  Status                           : Enabled
  ```
   
  <span data-ttu-id="d953e-146">Make sure that the circuit shows as Provisioned and Enabled.</span><span class="sxs-lookup"><span data-stu-id="d953e-146">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="d953e-147">If it isn't, work with your connectivity provider to get your circuit to the required state and status.</span><span class="sxs-lookup"><span data-stu-id="d953e-147">If it isn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>

  ```powershell
  ServiceProviderProvisioningState : Provisioned
  Status                           : Enabled
  ```
3. <span data-ttu-id="d953e-148">**Configure Azure private peering for the circuit.**</span><span class="sxs-lookup"><span data-stu-id="d953e-148">**Configure Azure private peering for the circuit.**</span></span>

  <span data-ttu-id="d953e-149">Make sure that you have the following items before you proceed with the next steps:</span><span class="sxs-lookup"><span data-stu-id="d953e-149">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
  * <span data-ttu-id="d953e-150">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="d953e-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d953e-151">This must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="d953e-151">This must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d953e-152">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="d953e-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d953e-153">This must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="d953e-153">This must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="d953e-154">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="d953e-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d953e-155">Verify that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="d953e-155">Verify that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="d953e-156">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="d953e-156">AS number for peering.</span></span> <span data-ttu-id="d953e-157">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="d953e-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="d953e-158">You can use a private AS number for this peering.</span><span class="sxs-lookup"><span data-stu-id="d953e-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="d953e-159">Verify that you are not using 65515.</span><span class="sxs-lookup"><span data-stu-id="d953e-159">Verify that you are not using 65515.</span></span>
  * <span data-ttu-id="d953e-160">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="d953e-160">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="d953e-161">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="d953e-161">**Optional**.</span></span>
     
  <span data-ttu-id="d953e-162">You can use the following example to configure Azure private peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="d953e-162">You can use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100
  ```    

  <span data-ttu-id="d953e-163">If you want to use an MD5 hash, use the following example to configure private peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="d953e-163">If you want to use an MD5 hash, use the following example to configure private peering for your circuit:</span></span>

  ```powershell
  New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"
  ```
     
  > [!IMPORTANT]
  > Verify that you specify your AS number as peering ASN, not customer ASN.
  > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="d953e-165">To view Azure private peering details</span><span class="sxs-lookup"><span data-stu-id="d953e-165">To view Azure private peering details</span></span>

<span data-ttu-id="d953e-166">You can view configuration details using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d953e-166">You can view configuration details using the following cmdlet:</span></span>

```powershell
Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"
```

<span data-ttu-id="d953e-167">Return:</span><span class="sxs-lookup"><span data-stu-id="d953e-167">Return:</span></span>

```
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
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="d953e-168">To update Azure private peering configuration</span><span class="sxs-lookup"><span data-stu-id="d953e-168">To update Azure private peering configuration</span></span>

<span data-ttu-id="d953e-169">You can update any part of the configuration using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d953e-169">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="d953e-170">In the following example, the VLAN ID of the circuit is being updated from 100 to 500.</span><span class="sxs-lookup"><span data-stu-id="d953e-170">In the following example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="d953e-171">To delete Azure private peering</span><span class="sxs-lookup"><span data-stu-id="d953e-171">To delete Azure private peering</span></span>

<span data-ttu-id="d953e-172">You can remove your peering configuration by running the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d953e-172">You can remove your peering configuration by running the following cmdlet.</span></span> <span data-ttu-id="d953e-173">You must make sure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d953e-173">You must make sure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet.</span></span>

```powershell
Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"
```

## <a name="azure-public-peering"></a><span data-ttu-id="d953e-174">Azure public peering</span><span class="sxs-lookup"><span data-stu-id="d953e-174">Azure public peering</span></span>

<span data-ttu-id="d953e-175">This section provides instructions on how to create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d953e-175">This section provides instructions on how to create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="d953e-176">To create Azure public peering</span><span class="sxs-lookup"><span data-stu-id="d953e-176">To create Azure public peering</span></span>

1. <span data-ttu-id="d953e-177">**Create an ExpressRoute circuit**</span><span class="sxs-lookup"><span data-stu-id="d953e-177">**Create an ExpressRoute circuit**</span></span>

  <span data-ttu-id="d953e-178">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="d953e-178">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="d953e-179">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span><span class="sxs-lookup"><span data-stu-id="d953e-179">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="d953e-180">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="d953e-180">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="d953e-181">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="d953e-181">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
2. <span data-ttu-id="d953e-182">**Check ExpressRoute circuit to verify that it is provisioned**</span><span class="sxs-lookup"><span data-stu-id="d953e-182">**Check ExpressRoute circuit to verify that it is provisioned**</span></span>

  <span data-ttu-id="d953e-183">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span><span class="sxs-lookup"><span data-stu-id="d953e-183">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit -ServiceKey "*********************************"
  ```

  <span data-ttu-id="d953e-184">Return:</span><span class="sxs-lookup"><span data-stu-id="d953e-184">Return:</span></span>

  ```powershell
  Bandwidth                        : 200
  CircuitName                      : MyTestCircuit
  Location                         : Silicon Valley
  ServiceKey                       : *********************************
  ServiceProviderName              : equinix
  ServiceProviderProvisioningState : Provisioned
  Sku                              : Standard
  Status                           : Enabled
  ```
   
  <span data-ttu-id="d953e-185">Verify that the circuit shows as Provisioned and Enabled.</span><span class="sxs-lookup"><span data-stu-id="d953e-185">Verify that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="d953e-186">If it isn't, work with your connectivity provider to get your circuit to the required state and status.</span><span class="sxs-lookup"><span data-stu-id="d953e-186">If it isn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>

  ```powershell
  ServiceProviderProvisioningState : Provisioned
  Status                           : Enabled
  ```
4. <span data-ttu-id="d953e-187">**Configure Azure public peering for the circuit**</span><span class="sxs-lookup"><span data-stu-id="d953e-187">**Configure Azure public peering for the circuit**</span></span>
   
  <span data-ttu-id="d953e-188">Make sure that you have the following information before you proceed:</span><span class="sxs-lookup"><span data-stu-id="d953e-188">Make sure that you have the following information before you proceed:</span></span>
   
  * <span data-ttu-id="d953e-189">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="d953e-189">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d953e-190">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="d953e-190">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d953e-191">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="d953e-191">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d953e-192">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="d953e-192">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="d953e-193">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="d953e-193">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d953e-194">Verify that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="d953e-194">Verify that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="d953e-195">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="d953e-195">AS number for peering.</span></span> <span data-ttu-id="d953e-196">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="d953e-196">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="d953e-197">An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="d953e-197">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="d953e-198">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="d953e-198">**Optional**.</span></span>

  > [!IMPORTANT]
  > Make sure that you specify your AS number as peering ASN and not customer ASN.
  >  
     
  <span data-ttu-id="d953e-200">You can use the following example to configure Azure public peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="d953e-200">You can use the following example to configure Azure public peering for your circuit:</span></span>

  ```powershell
  New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200
  ```
     
  <span data-ttu-id="d953e-201">If you want to use an MD5 hash, use the following example to configure your circuit:</span><span class="sxs-lookup"><span data-stu-id="d953e-201">If you want to use an MD5 hash, use the following example to configure your circuit:</span></span>
     
  ```powershell
  New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"
  ```
     
### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="d953e-202">To view Azure public peering details</span><span class="sxs-lookup"><span data-stu-id="d953e-202">To view Azure public peering details</span></span>

<span data-ttu-id="d953e-203">To view configuration details, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d953e-203">To view configuration details, use the following cmdlet:</span></span>

```powershell
Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"
```

<span data-ttu-id="d953e-204">Return:</span><span class="sxs-lookup"><span data-stu-id="d953e-204">Return:</span></span>

```powershell
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
```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="d953e-205">To update Azure public peering configuration</span><span class="sxs-lookup"><span data-stu-id="d953e-205">To update Azure public peering configuration</span></span>

<span data-ttu-id="d953e-206">You can update any part of the configuration using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d953e-206">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="d953e-207">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span><span class="sxs-lookup"><span data-stu-id="d953e-207">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"
```

<span data-ttu-id="d953e-208">Verify that the circuit shows as Provisioned and Enabled.</span><span class="sxs-lookup"><span data-stu-id="d953e-208">Verify that the circuit shows as Provisioned and Enabled.</span></span> 
### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="d953e-209">To delete Azure public peering</span><span class="sxs-lookup"><span data-stu-id="d953e-209">To delete Azure public peering</span></span>

<span data-ttu-id="d953e-210">You can remove your peering configuration by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d953e-210">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"
```

## <a name="microsoft-peering"></a><span data-ttu-id="d953e-211">Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="d953e-211">Microsoft peering</span></span>

<span data-ttu-id="d953e-212">This section provides instructions on how to create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d953e-212">This section provides instructions on how to create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="d953e-213">To create Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="d953e-213">To create Microsoft peering</span></span>

1. <span data-ttu-id="d953e-214">**Create an ExpressRoute circuit**</span><span class="sxs-lookup"><span data-stu-id="d953e-214">**Create an ExpressRoute circuit**</span></span>
  
  <span data-ttu-id="d953e-215">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="d953e-215">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="d953e-216">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span><span class="sxs-lookup"><span data-stu-id="d953e-216">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="d953e-217">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="d953e-217">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="d953e-218">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="d953e-218">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
2. <span data-ttu-id="d953e-219">**Check ExpressRoute circuit to verify that it is provisioned**</span><span class="sxs-lookup"><span data-stu-id="d953e-219">**Check ExpressRoute circuit to verify that it is provisioned**</span></span>

  <span data-ttu-id="d953e-220">Verify that the circuit shows as Provisioned and Enabled.</span><span class="sxs-lookup"><span data-stu-id="d953e-220">Verify that the circuit shows as Provisioned and Enabled.</span></span> 
   
  ```powershell
  Get-AzureDedicatedCircuit -ServiceKey "*********************************"
  ```

  <span data-ttu-id="d953e-221">Return:</span><span class="sxs-lookup"><span data-stu-id="d953e-221">Return:</span></span>
   
  ```powershell
  Bandwidth                        : 200
  CircuitName                      : MyTestCircuit
  Location                         : Silicon Valley
  ServiceKey                       : *********************************
  ServiceProviderName              : equinix
  ServiceProviderProvisioningState : Provisioned
  Sku                              : Standard
  Status                           : Enabled
  ```
   
  <span data-ttu-id="d953e-222">Verify that the circuit shows as Provisioned and Enabled.</span><span class="sxs-lookup"><span data-stu-id="d953e-222">Verify that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="d953e-223">If it isn't, work with your connectivity provider to get your circuit to the required state and status.</span><span class="sxs-lookup"><span data-stu-id="d953e-223">If it isn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>

  ```powershell
  ServiceProviderProvisioningState : Provisioned
  Status                           : Enabled
  ```
3. <span data-ttu-id="d953e-224">**Configure Microsoft peering for the circuit**</span><span class="sxs-lookup"><span data-stu-id="d953e-224">**Configure Microsoft peering for the circuit**</span></span>
   
    <span data-ttu-id="d953e-225">Make sure that you have the following information before you proceed.</span><span class="sxs-lookup"><span data-stu-id="d953e-225">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="d953e-226">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="d953e-226">A /30 subnet for the primary link.</span></span> <span data-ttu-id="d953e-227">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="d953e-227">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="d953e-228">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="d953e-228">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="d953e-229">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="d953e-229">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="d953e-230">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="d953e-230">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="d953e-231">Verify that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="d953e-231">Verify that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="d953e-232">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="d953e-232">AS number for peering.</span></span> <span data-ttu-id="d953e-233">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="d953e-233">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="d953e-234">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span><span class="sxs-lookup"><span data-stu-id="d953e-234">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="d953e-235">Only public IP address prefixes are accepted.</span><span class="sxs-lookup"><span data-stu-id="d953e-235">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="d953e-236">You can send a comma-separated list if you plan to send a set of prefixes.</span><span class="sxs-lookup"><span data-stu-id="d953e-236">You can send a comma-separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="d953e-237">These prefixes must be registered to you in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="d953e-237">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="d953e-238">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span><span class="sxs-lookup"><span data-stu-id="d953e-238">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="d953e-239">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="d953e-239">**Optional**.</span></span>
   * <span data-ttu-id="d953e-240">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span><span class="sxs-lookup"><span data-stu-id="d953e-240">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="d953e-241">An MD5 hash, if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="d953e-241">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="d953e-242">**Optional.**</span><span class="sxs-lookup"><span data-stu-id="d953e-242">**Optional.**</span></span>
     
  <span data-ttu-id="d953e-243">Run the following cmdlet to configure Microsoft peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="d953e-243">Run the following cmdlet to configure Microsoft peering for your circuit:</span></span>
 
  ```powershell
  New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"
  ```

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="d953e-244">To view Microsoft peering details</span><span class="sxs-lookup"><span data-stu-id="d953e-244">To view Microsoft peering details</span></span>

<span data-ttu-id="d953e-245">You can view configuration details using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d953e-245">You can view configuration details using the following cmdlet:</span></span>

```powershell
Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"
```
<span data-ttu-id="d953e-246">Return:</span><span class="sxs-lookup"><span data-stu-id="d953e-246">Return:</span></span>

```powershell
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
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="d953e-247">To update Microsoft peering configuration</span><span class="sxs-lookup"><span data-stu-id="d953e-247">To update Microsoft peering configuration</span></span>

<span data-ttu-id="d953e-248">You can update any part of the configuration using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d953e-248">You can update any part of the configuration using the following cmdlet:</span></span>

```powershell
Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="d953e-249">To delete Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="d953e-249">To delete Microsoft peering</span></span>

<span data-ttu-id="d953e-250">You can remove your peering configuration by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d953e-250">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"
```

## <a name="next-steps"></a><span data-ttu-id="d953e-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="d953e-251">Next steps</span></span>

<span data-ttu-id="d953e-252">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="d953e-252">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="d953e-253">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="d953e-253">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="d953e-254">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="d953e-254">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>