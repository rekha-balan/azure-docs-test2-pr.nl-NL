---
title: 'Link a virtual network to an ExpressRoute circuit: PowerShell: classic: Azure | Microsoft Docs'
description: This document provides an overview of how to link virtual networks (VNets) to ExpressRoute circuits by using the classic deployment model and PowerShell.
services: expressroute
documentationcenter: na
author: cherylmc
ms.service: expressroute
ms.topic: conceptual
ms.date: 07/27/2018
ms.author: cherylmc
ms.openlocfilehash: 10b623947b6e776c4f8f41e8424262d7f2a3e933
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819915"
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="b7b7f-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span><span class="sxs-lookup"><span data-stu-id="b7b7f-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [Video - Azure portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classic)](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="b7b7f-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits using PowerShell.</span></span> <span data-ttu-id="b7b7f-110">A single VNet can be linked to up to four ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-110">A single VNet can be linked to up to four ExpressRoute circuits.</span></span> <span data-ttu-id="b7b7f-111">Use the steps in this article to create a new link to each ExpressRoute circuit you are connecting to.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-111">Use the steps in this article to create a new link to each ExpressRoute circuit you are connecting to.</span></span> <span data-ttu-id="b7b7f-112">The ExpressRoute circuits can be in the same subscription, different subscriptions, or a mix of both.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-112">The ExpressRoute circuits can be in the same subscription, different subscriptions, or a mix of both.</span></span> <span data-ttu-id="b7b7f-113">This article applies to virtual networks created using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-113">This article applies to virtual networks created using the classic deployment model.</span></span>

<span data-ttu-id="b7b7f-114">You can link up to 10 virtual networks to an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-114">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="b7b7f-115">All virtual networks must be in the same geopolitical region.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-115">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="b7b7f-116">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enable the ExpressRoute premium add-on.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-116">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enable the ExpressRoute premium add-on.</span></span> <span data-ttu-id="b7b7f-117">Check the [FAQ](expressroute-faqs.md) for more details about the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-117">Check the [FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="b7b7f-118">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="b7b7f-118">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="b7b7f-119">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7b7f-119">Configuration prerequisites</span></span>

* <span data-ttu-id="b7b7f-120">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-120">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="b7b7f-121">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-121">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="b7b7f-122">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-122">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="b7b7f-123">Ensure that you have Azure private peering configured for your circuit.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-123">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="b7b7f-124">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-124">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="b7b7f-125">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-125">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="b7b7f-126">You must have a virtual network and a virtual network gateway created and fully provisioned.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-126">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="b7b7f-127">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="b7b7f-127">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

### <a name="download-the-latest-powershell-cmdlets"></a><span data-ttu-id="b7b7f-128">Download the latest PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b7b7f-128">Download the latest PowerShell cmdlets</span></span>

<span data-ttu-id="b7b7f-129">Install the latest versions of the Azure Service Management (SM) PowerShell modules and the ExpressRoute module.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-129">Install the latest versions of the Azure Service Management (SM) PowerShell modules and the ExpressRoute module.</span></span> <span data-ttu-id="b7b7f-130">When using the following example, note that the version number (in this example, 5.1.1) will change as newer versions of the cmdlets are released.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-130">When using the following example, note that the version number (in this example, 5.1.1) will change as newer versions of the cmdlets are released.</span></span>

```powershell
Import-Module 'C:\Program Files\WindowsPowerShell\Modules\Azure\5.1.1\Azure\Azure.psd1'
Import-Module 'C:\Program Files\WindowsPowerShell\Modules\Azure\5.1.1\ExpressRoute\ExpressRoute.psd1'
```

<span data-ttu-id="b7b7f-131">If you need more information about Azure PowerShell, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-131">If you need more information about Azure PowerShell, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="sign-in"></a><span data-ttu-id="b7b7f-132">Sign in</span><span class="sxs-lookup"><span data-stu-id="b7b7f-132">Sign in</span></span>

<span data-ttu-id="b7b7f-133">To sign in to your Azure account, use the following examples:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-133">To sign in to your Azure account, use the following examples:</span></span>

1. <span data-ttu-id="b7b7f-134">Open your PowerShell console with elevated rights and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-134">Open your PowerShell console with elevated rights and connect to your account.</span></span>

  ```powershell
  Connect-AzureRmAccount
  ```
2. <span data-ttu-id="b7b7f-135">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-135">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="b7b7f-136">If you have more than one subscription, select the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-136">If you have more than one subscription, select the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

4. <span data-ttu-id="b7b7f-137">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-137">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

  ```powershell
  Add-AzureAccount
  ```

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="b7b7f-138">Connect a virtual network in the same subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="b7b7f-138">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="b7b7f-139">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-139">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="b7b7f-140">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-140">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

```powershell
New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
Provisioned
```
    
## <a name="remove-a-virtual-network-link-to-a-circuit"></a><span data-ttu-id="b7b7f-141">Remove a virtual network link to a circuit</span><span class="sxs-lookup"><span data-stu-id="b7b7f-141">Remove a virtual network link to a circuit</span></span>
<span data-ttu-id="b7b7f-142">You can remove a virtual network link to an ExpressRoute circuit by using the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-142">You can remove a virtual network link to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="b7b7f-143">Make sure that the current subscription is selected for the given virtual network.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-143">Make sure that the current subscription is selected for the given virtual network.</span></span> 

```powershell
Remove-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
```
 

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="b7b7f-144">Connect a virtual network in a different subscription to a circuit</span><span class="sxs-lookup"><span data-stu-id="b7b7f-144">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="b7b7f-145">You can share an ExpressRoute circuit across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-145">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="b7b7f-146">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-146">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="b7b7f-147">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-147">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="b7b7f-148">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-148">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="b7b7f-149">A single department (in this example: IT) can own the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-149">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="b7b7f-150">Other subscriptions within the organization can use the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-150">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner. All virtual networks share the same bandwidth.
> 
> 

![Cross-subscription connectivity](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="b7b7f-154">Administration</span><span class="sxs-lookup"><span data-stu-id="b7b7f-154">Administration</span></span>
<span data-ttu-id="b7b7f-155">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-155">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="b7b7f-156">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-156">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="b7b7f-157">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-157">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="b7b7f-158">The circuit owner has the power to modify and revoke authorizations at any time.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-158">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="b7b7f-159">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-159">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="b7b7f-160">Circuit owner operations</span><span class="sxs-lookup"><span data-stu-id="b7b7f-160">Circuit owner operations</span></span>

<span data-ttu-id="b7b7f-161">**Creating an authorization**</span><span class="sxs-lookup"><span data-stu-id="b7b7f-161">**Creating an authorization**</span></span>

<span data-ttu-id="b7b7f-162">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-162">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="b7b7f-163">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-163">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="b7b7f-164">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-164">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="b7b7f-165">The cmdlet doesn't send email to the specified Microsoft ID.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-165">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="b7b7f-166">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span><span class="sxs-lookup"><span data-stu-id="b7b7f-166">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

```powershell
New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'
```

  <span data-ttu-id="b7b7f-167">Return:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-167">Return:</span></span>

  ```powershell
  Description         : Dev-Test Links
  Limit               : 2
  LinkAuthorizationId : **********************************
  MicrosoftIds        : devtest@contoso.com
  Used                : 0
  ```

<span data-ttu-id="b7b7f-168">**Reviewing authorizations**</span><span class="sxs-lookup"><span data-stu-id="b7b7f-168">**Reviewing authorizations**</span></span>

<span data-ttu-id="b7b7f-169">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-169">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"
```
  <span data-ttu-id="b7b7f-170">Return:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-170">Return:</span></span>

  ```powershell
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
  ```

<span data-ttu-id="b7b7f-171">**Updating authorizations**</span><span class="sxs-lookup"><span data-stu-id="b7b7f-171">**Updating authorizations**</span></span>

<span data-ttu-id="b7b7f-172">The circuit owner can modify authorizations by using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-172">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

```powershell
Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5
```

  <span data-ttu-id="b7b7f-173">Return:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-173">Return:</span></span>

  ```powershell
  Description         : Dev-Test Links
  Limit               : 5
  LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
  MicrosoftIds        : devtest@contoso.com
  Used                : 0
  ```

<span data-ttu-id="b7b7f-174">**Deleting authorizations**</span><span class="sxs-lookup"><span data-stu-id="b7b7f-174">**Deleting authorizations**</span></span>

<span data-ttu-id="b7b7f-175">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-175">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"
```

### <a name="circuit-user-operations"></a><span data-ttu-id="b7b7f-176">Circuit user operations</span><span class="sxs-lookup"><span data-stu-id="b7b7f-176">Circuit user operations</span></span>

<span data-ttu-id="b7b7f-177">**Reviewing authorizations**</span><span class="sxs-lookup"><span data-stu-id="b7b7f-177">**Reviewing authorizations**</span></span>

<span data-ttu-id="b7b7f-178">The circuit user can review authorizations by using the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-178">The circuit user can review authorizations by using the following cmdlet:</span></span>

```powershell
Get-AzureAuthorizedDedicatedCircuit
```

  <span data-ttu-id="b7b7f-179">Return:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-179">Return:</span></span>

  ```powershell
  Bandwidth                        : 200
  CircuitName                      : ContosoIT
  Location                         : Washington DC
  MaximumAllowedLinks              : 2
  ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
  ServiceProviderName              : equinix
  ServiceProviderProvisioningState : Provisioned
  Status                           : Enabled
  UsedLinks                        : 0
  ```

<span data-ttu-id="b7b7f-180">**Redeeming link authorizations**</span><span class="sxs-lookup"><span data-stu-id="b7b7f-180">**Redeeming link authorizations**</span></span>

<span data-ttu-id="b7b7f-181">The circuit user can run the following cmdlet to redeem a link authorization:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-181">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'
```

  <span data-ttu-id="b7b7f-182">Return:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-182">Return:</span></span>

  ```powershell
  State VnetName
  ----- --------
  Provisioned SalesVNET1
  ```

<span data-ttu-id="b7b7f-183">Run this command in the newly linked subscription for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="b7b7f-183">Run this command in the newly linked subscription for the virtual network:</span></span>

```powershell
New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
```

## <a name="next-steps"></a><span data-ttu-id="b7b7f-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7b7f-184">Next steps</span></span>

<span data-ttu-id="b7b7f-185">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="b7b7f-185">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>