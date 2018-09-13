---
title: 'Create and modify an ExpressRoute circuit: PowerShell: Azure Resource Manager | Microsoft Docs'
description: This article describes how to create, provision, verify, update, delete, and deprovision an ExpressRoute circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 15c08c950bc1dcd620f2943885e427991585d817
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550395"
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="996bd-103">Create and modify an ExpressRoute circuit using PowerShell</span><span class="sxs-lookup"><span data-stu-id="996bd-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-circuit-arm.md)
> * [Video - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> 
>

<span data-ttu-id="996bd-107">This article describes how to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="996bd-107">This article describes how to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="996bd-108">This article also shows you how to check the status of the circuit, update it, or delete and deprovision it.</span><span class="sxs-lookup"><span data-stu-id="996bd-108">This article also shows you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="996bd-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="996bd-109">Before you begin</span></span>
* <span data-ttu-id="996bd-110">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="996bd-110">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="996bd-111">For more information, see [Overview of Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="996bd-111">For more information, see [Overview of Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="996bd-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="996bd-112">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="996bd-113">Create and provision an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-113">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="996bd-114">1. Sign in to your Azure account and select your subscription</span><span class="sxs-lookup"><span data-stu-id="996bd-114">1. Sign in to your Azure account and select your subscription</span></span>
<span data-ttu-id="996bd-115">To begin your configuration, sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="996bd-115">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="996bd-116">Use the following examples to help you connect:</span><span class="sxs-lookup"><span data-stu-id="996bd-116">Use the following examples to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="996bd-117">Check the subscriptions for the account:</span><span class="sxs-lookup"><span data-stu-id="996bd-117">Check the subscriptions for the account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="996bd-118">Select the subscription that you want to create an ExpressRoute circuit for:</span><span class="sxs-lookup"><span data-stu-id="996bd-118">Select the subscription that you want to create an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="996bd-119">2. Get the list of supported providers, locations, and bandwidths</span><span class="sxs-lookup"><span data-stu-id="996bd-119">2. Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="996bd-120">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span><span class="sxs-lookup"><span data-stu-id="996bd-120">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="996bd-121">The PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span><span class="sxs-lookup"><span data-stu-id="996bd-121">The PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="996bd-122">Check to see if your connectivity provider is listed there.</span><span class="sxs-lookup"><span data-stu-id="996bd-122">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="996bd-123">Make a note of the following information.</span><span class="sxs-lookup"><span data-stu-id="996bd-123">Make a note of the following information.</span></span> <span data-ttu-id="996bd-124">You'll need it later when you create a circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-124">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="996bd-125">Name</span><span class="sxs-lookup"><span data-stu-id="996bd-125">Name</span></span>
* <span data-ttu-id="996bd-126">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="996bd-126">PeeringLocations</span></span>
* <span data-ttu-id="996bd-127">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="996bd-127">BandwidthsOffered</span></span>

<span data-ttu-id="996bd-128">You're now ready to create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-128">You're now ready to create an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="996bd-129">3. Create an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-129">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="996bd-130">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-130">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="996bd-131">You can do so by running the following command:</span><span class="sxs-lookup"><span data-stu-id="996bd-131">You can do so by running the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="996bd-132">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="996bd-132">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="996bd-133">If you're using a different provider and different settings, substitute that information when you make your request.</span><span class="sxs-lookup"><span data-stu-id="996bd-133">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="996bd-134">The following is an example request for a new service key:</span><span class="sxs-lookup"><span data-stu-id="996bd-134">The following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="996bd-135">Make sure that you specify the correct SKU tier and SKU family:</span><span class="sxs-lookup"><span data-stu-id="996bd-135">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="996bd-136">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span><span class="sxs-lookup"><span data-stu-id="996bd-136">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="996bd-137">You can specify *Standard* to get the standard SKU or *Premium* for the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="996bd-137">You can specify *Standard* to get the standard SKU or *Premium* for the premium add-on.</span></span>
* <span data-ttu-id="996bd-138">SKU family determines the billing type.</span><span class="sxs-lookup"><span data-stu-id="996bd-138">SKU family determines the billing type.</span></span> <span data-ttu-id="996bd-139">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span><span class="sxs-lookup"><span data-stu-id="996bd-139">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="996bd-140">You can change the billing type from *Metereddata* to *Unlimiteddata*, but you can't change the type from *Unlimiteddata* to *Metereddata*.</span><span class="sxs-lookup"><span data-stu-id="996bd-140">You can change the billing type from *Metereddata* to *Unlimiteddata*, but you can't change the type from *Unlimiteddata* to *Metereddata*.</span></span>

> [!IMPORTANT]
> Your ExpressRoute circuit will be billed from the moment a service key is issued. Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.
> 
> 

<span data-ttu-id="996bd-143">The response contains the service key.</span><span class="sxs-lookup"><span data-stu-id="996bd-143">The response contains the service key.</span></span> <span data-ttu-id="996bd-144">You can get detailed descriptions of all the parameters by running the following command:</span><span class="sxs-lookup"><span data-stu-id="996bd-144">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="996bd-145">4. List all ExpressRoute circuits</span><span class="sxs-lookup"><span data-stu-id="996bd-145">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="996bd-146">To get a list of all the ExpressRoute circuits that you created, run the **Get-AzureRmExpressRouteCircuit** command:</span><span class="sxs-lookup"><span data-stu-id="996bd-146">To get a list of all the ExpressRoute circuits that you created, run the **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="996bd-147">The response will look similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="996bd-147">The response will look similar to the following example:</span></span>

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="996bd-148">You can retrieve this information at any time by using the `Get-AzureRmExpressRouteCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="996bd-148">You can retrieve this information at any time by using the `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="996bd-149">Making the call with no parameters lists all the circuits.</span><span class="sxs-lookup"><span data-stu-id="996bd-149">Making the call with no parameters lists all the circuits.</span></span> <span data-ttu-id="996bd-150">Your service key will be listed in the *ServiceKey* field:</span><span class="sxs-lookup"><span data-stu-id="996bd-150">Your service key will be listed in the *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="996bd-151">The response will look similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="996bd-151">The response will look similar to the following example:</span></span>

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="996bd-152">You can get detailed descriptions of all the parameters by running the following command:</span><span class="sxs-lookup"><span data-stu-id="996bd-152">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="996bd-153">5. Send the service key to your connectivity provider for provisioning</span><span class="sxs-lookup"><span data-stu-id="996bd-153">5. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="996bd-154">*ServiceProviderProvisioningState* provides information about the current state of provisioning on the service-provider side.</span><span class="sxs-lookup"><span data-stu-id="996bd-154">*ServiceProviderProvisioningState* provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="996bd-155">Status provides the state on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="996bd-155">Status provides the state on the Microsoft side.</span></span> <span data-ttu-id="996bd-156">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span><span class="sxs-lookup"><span data-stu-id="996bd-156">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="996bd-157">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span><span class="sxs-lookup"><span data-stu-id="996bd-157">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="996bd-158">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span><span class="sxs-lookup"><span data-stu-id="996bd-158">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="996bd-159">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span><span class="sxs-lookup"><span data-stu-id="996bd-159">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="996bd-160">6. Periodically check the status and the state of the circuit key</span><span class="sxs-lookup"><span data-stu-id="996bd-160">6. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="996bd-161">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-161">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="996bd-162">After the circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="996bd-162">After the circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in the following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="996bd-163">The response will look similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="996bd-163">The response will look similar to the following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="996bd-164">7. Create your routing configuration</span><span class="sxs-lookup"><span data-stu-id="996bd-164">7. Create your routing configuration</span></span>
<span data-ttu-id="996bd-165">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article to create and modify circuit peerings.</span><span class="sxs-lookup"><span data-stu-id="996bd-165">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services. If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="996bd-168">8. Link a virtual network to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-168">8. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="996bd-169">Next, link a virtual network to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-169">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="996bd-170">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="996bd-170">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="996bd-171">Getting the status of an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-171">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="996bd-172">You can retrieve this information at any time by using the **Get-AzureRmExpressRouteCircuit** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="996bd-172">You can retrieve this information at any time by using the **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="996bd-173">Making the call with no parameters lists all the circuits.</span><span class="sxs-lookup"><span data-stu-id="996bd-173">Making the call with no parameters lists all the circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="996bd-174">The response will be similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="996bd-174">The response will be similar to the following example:</span></span>

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


<span data-ttu-id="996bd-175">You can get information on a specific ExpressRoute circuit by passing the resource group name and circuit name as a parameter to the call:</span><span class="sxs-lookup"><span data-stu-id="996bd-175">You can get information on a specific ExpressRoute circuit by passing the resource group name and circuit name as a parameter to the call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="996bd-176">The response will look similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="996bd-176">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="996bd-177">You can get detailed descriptions of all the parameters by running the following command:</span><span class="sxs-lookup"><span data-stu-id="996bd-177">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a><span data-ttu-id="996bd-178">Modifying an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-178">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="996bd-179">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span><span class="sxs-lookup"><span data-stu-id="996bd-179">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="996bd-180">You can do the following with no downtime:</span><span class="sxs-lookup"><span data-stu-id="996bd-180">You can do the following with no downtime:</span></span>

* <span data-ttu-id="996bd-181">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-181">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="996bd-182">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span><span class="sxs-lookup"><span data-stu-id="996bd-182">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="996bd-183">Downgrading the bandwidth of a circuit is not supported.</span><span class="sxs-lookup"><span data-stu-id="996bd-183">Downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="996bd-184">Change the metering plan from Metered Data to Unlimited Data.</span><span class="sxs-lookup"><span data-stu-id="996bd-184">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="996bd-185">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span><span class="sxs-lookup"><span data-stu-id="996bd-185">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="996bd-186">You can enable and disable *Allow Classic Operations*.</span><span class="sxs-lookup"><span data-stu-id="996bd-186">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="996bd-187">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="996bd-187">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="996bd-188">To enable the ExpressRoute premium add-on</span><span class="sxs-lookup"><span data-stu-id="996bd-188">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="996bd-189">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell snippet:</span><span class="sxs-lookup"><span data-stu-id="996bd-189">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="996bd-190">The circuit will now have the ExpressRoute premium add-on features enabled.</span><span class="sxs-lookup"><span data-stu-id="996bd-190">The circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="996bd-191">We will begin billing you for the premium add-on capability as soon as the command has successfully run.</span><span class="sxs-lookup"><span data-stu-id="996bd-191">We will begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="996bd-192">To disable the ExpressRoute premium add-on</span><span class="sxs-lookup"><span data-stu-id="996bd-192">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.
> 
> 

<span data-ttu-id="996bd-194">Note the following:</span><span class="sxs-lookup"><span data-stu-id="996bd-194">Note the following:</span></span>

* <span data-ttu-id="996bd-195">Before you downgrade from premium to standard, you must ensure that the number of virtual networks that are linked to the circuit is less than 10.</span><span class="sxs-lookup"><span data-stu-id="996bd-195">Before you downgrade from premium to standard, you must ensure that the number of virtual networks that are linked to the circuit is less than 10.</span></span> <span data-ttu-id="996bd-196">If you don't do this, your update request fails, and we will bill you at premium rates.</span><span class="sxs-lookup"><span data-stu-id="996bd-196">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="996bd-197">You must unlink all virtual networks in other geopolitical regions.</span><span class="sxs-lookup"><span data-stu-id="996bd-197">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="996bd-198">If you don't do this, your update request will fail, and we will bill you at premium rates.</span><span class="sxs-lookup"><span data-stu-id="996bd-198">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="996bd-199">Your route table must be less than 4,000 routes for private peering.</span><span class="sxs-lookup"><span data-stu-id="996bd-199">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="996bd-200">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span><span class="sxs-lookup"><span data-stu-id="996bd-200">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="996bd-201">You can disable the ExpressRoute premium add-on for the existing circuit by using the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="996bd-201">You can disable the ExpressRoute premium add-on for the existing circuit by using the following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="996bd-202">To update the ExpressRoute circuit bandwidth</span><span class="sxs-lookup"><span data-stu-id="996bd-202">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="996bd-203">For supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="996bd-203">For supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="996bd-204">You can pick any size greater than the size of your existing circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-204">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port. You cannot upgrade the circuit if there is no additional capacity available at that location.
>
> You cannot reduce the bandwidth of an ExpressRoute circuit without disruption. Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.
> 

<span data-ttu-id="996bd-209">After you decide what size you need, use the following command to resize your circuit:</span><span class="sxs-lookup"><span data-stu-id="996bd-209">After you decide what size you need, use the following command to resize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="996bd-210">Your circuit will be sized up on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="996bd-210">Your circuit will be sized up on the Microsoft side.</span></span> <span data-ttu-id="996bd-211">Then you must contact your connectivity provider to update configurations on their side to match this change.</span><span class="sxs-lookup"><span data-stu-id="996bd-211">Then you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="996bd-212">After you make this notification, we will begin billing you for the updated bandwidth option.</span><span class="sxs-lookup"><span data-stu-id="996bd-212">After you make this notification, we will begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="996bd-213">To move the SKU from metered to unlimited</span><span class="sxs-lookup"><span data-stu-id="996bd-213">To move the SKU from metered to unlimited</span></span>
<span data-ttu-id="996bd-214">You can change the SKU of an ExpressRoute circuit by using the following PowerShell snippet:</span><span class="sxs-lookup"><span data-stu-id="996bd-214">You can change the SKU of an ExpressRoute circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="996bd-215">To control access to the classic and Resource Manager environments</span><span class="sxs-lookup"><span data-stu-id="996bd-215">To control access to the classic and Resource Manager environments</span></span>
<span data-ttu-id="996bd-216">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="996bd-216">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="996bd-217">Deprovisioning and deleting an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-217">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="996bd-218">Note the following:</span><span class="sxs-lookup"><span data-stu-id="996bd-218">Note the following:</span></span>

* <span data-ttu-id="996bd-219">You must unlink all virtual networks from the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-219">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="996bd-220">If this operation fails, check to see if any virtual networks are linked to the circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-220">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="996bd-221">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span><span class="sxs-lookup"><span data-stu-id="996bd-221">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="996bd-222">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span><span class="sxs-lookup"><span data-stu-id="996bd-222">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="996bd-223">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span><span class="sxs-lookup"><span data-stu-id="996bd-223">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="996bd-224">This will stop billing for the circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-224">This will stop billing for the circuit</span></span>

<span data-ttu-id="996bd-225">You can delete your ExpressRoute circuit by running the following command:</span><span class="sxs-lookup"><span data-stu-id="996bd-225">You can delete your ExpressRoute circuit by running the following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="996bd-226">Next steps</span><span class="sxs-lookup"><span data-stu-id="996bd-226">Next steps</span></span>

<span data-ttu-id="996bd-227">After you create your circuit, make sure that you do the following:</span><span class="sxs-lookup"><span data-stu-id="996bd-227">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="996bd-228">Create and modify routing for your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-228">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="996bd-229">Link your virtual network to your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="996bd-229">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
