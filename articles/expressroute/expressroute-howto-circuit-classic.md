---
title: 'Create and modify an ExpressRoute circuit: PowerShell: Azure classic| Microsoft Docs'
description: This article walks you through the steps for creating and provisioning an ExpressRoute circuit. This article also shows you how to check the status, update, or delete and deprovision your circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: efdec32e565bf1d11b562d283e56bd8ed5d292b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555572"
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="1aea6-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span><span class="sxs-lookup"><span data-stu-id="1aea6-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-circuit-arm.md)
> * [Classic - PowerShell](expressroute-howto-circuit-classic.md)
> * [Video - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> 
>

<span data-ttu-id="1aea6-109">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="1aea6-109">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span></span> <span data-ttu-id="1aea6-110">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="1aea6-110">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="1aea6-111">**About Azure deployment models**</span><span class="sxs-lookup"><span data-stu-id="1aea6-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="1aea6-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1aea6-112">Before you begin</span></span>
### <a name="step-1-review-the-prerequisites-and-workflow-articles"></a><span data-ttu-id="1aea6-113">Step 1.</span><span class="sxs-lookup"><span data-stu-id="1aea6-113">Step 1.</span></span> <span data-ttu-id="1aea6-114">Review the prerequisites and workflow articles</span><span class="sxs-lookup"><span data-stu-id="1aea6-114">Review the prerequisites and workflow articles</span></span>
<span data-ttu-id="1aea6-115">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="1aea6-115">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-the-latest-versions-of-the-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="1aea6-116">Step 2.</span><span class="sxs-lookup"><span data-stu-id="1aea6-116">Step 2.</span></span> <span data-ttu-id="1aea6-117">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span><span class="sxs-lookup"><span data-stu-id="1aea6-117">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="1aea6-118">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span><span class="sxs-lookup"><span data-stu-id="1aea6-118">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azureps-cmdlets-docs) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="1aea6-119">Step 3.</span><span class="sxs-lookup"><span data-stu-id="1aea6-119">Step 3.</span></span> <span data-ttu-id="1aea6-120">Log in to your Azure account and select a subscription</span><span class="sxs-lookup"><span data-stu-id="1aea6-120">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="1aea6-121">Open your PowerShell console with elevated rights and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="1aea6-121">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="1aea6-122">Use the following example to help you connect:</span><span class="sxs-lookup"><span data-stu-id="1aea6-122">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="1aea6-123">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="1aea6-123">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="1aea6-124">If you have more than one subscription, select the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="1aea6-124">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="1aea6-125">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="1aea6-125">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="1aea6-126">Create and provision an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-126">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-the-powershell-modules-for-expressroute"></a><span data-ttu-id="1aea6-127">Step 1.</span><span class="sxs-lookup"><span data-stu-id="1aea6-127">Step 1.</span></span> <span data-ttu-id="1aea6-128">Import the PowerShell modules for ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="1aea6-128">Import the PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="1aea6-129">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span><span class="sxs-lookup"><span data-stu-id="1aea6-129">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="1aea6-130">You import the modules from the location that they were installed to on your local computer.</span><span class="sxs-lookup"><span data-stu-id="1aea6-130">You import the modules from the location that they were installed to on your local computer.</span></span> <span data-ttu-id="1aea6-131">Depending on the method you used to install the modules, the location may be different than the following example shows.</span><span class="sxs-lookup"><span data-stu-id="1aea6-131">Depending on the method you used to install the modules, the location may be different than the following example shows.</span></span> <span data-ttu-id="1aea6-132">Modify the example if necessary.</span><span class="sxs-lookup"><span data-stu-id="1aea6-132">Modify the example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="1aea6-133">Step 2.</span><span class="sxs-lookup"><span data-stu-id="1aea6-133">Step 2.</span></span> <span data-ttu-id="1aea6-134">Get the list of supported providers, locations, and bandwidths</span><span class="sxs-lookup"><span data-stu-id="1aea6-134">Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="1aea6-135">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span><span class="sxs-lookup"><span data-stu-id="1aea6-135">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="1aea6-136">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span><span class="sxs-lookup"><span data-stu-id="1aea6-136">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="1aea6-137">Check to see if your connectivity provider is listed there.</span><span class="sxs-lookup"><span data-stu-id="1aea6-137">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="1aea6-138">Make a note of the following information because you'll need it later when you create a circuit:</span><span class="sxs-lookup"><span data-stu-id="1aea6-138">Make a note of the following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="1aea6-139">Name</span><span class="sxs-lookup"><span data-stu-id="1aea6-139">Name</span></span>
* <span data-ttu-id="1aea6-140">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="1aea6-140">PeeringLocations</span></span>
* <span data-ttu-id="1aea6-141">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="1aea6-141">BandwidthsOffered</span></span>

<span data-ttu-id="1aea6-142">You're now ready to create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="1aea6-142">You're now ready to create an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="1aea6-143">Step 3.</span><span class="sxs-lookup"><span data-stu-id="1aea6-143">Step 3.</span></span> <span data-ttu-id="1aea6-144">Create an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-144">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="1aea6-145">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="1aea6-145">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="1aea6-146">If you're using a different provider and different settings, substitute that information when you make your request.</span><span class="sxs-lookup"><span data-stu-id="1aea6-146">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> Your ExpressRoute circuit will be billed from the moment a service key is issued. Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.
> 
> 

<span data-ttu-id="1aea6-149">The following is an example request for a new service key:</span><span class="sxs-lookup"><span data-stu-id="1aea6-149">The following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="1aea6-150">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span><span class="sxs-lookup"><span data-stu-id="1aea6-150">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span></span> <span data-ttu-id="1aea6-151">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="1aea6-151">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="1aea6-152">The response will contain the service key.</span><span class="sxs-lookup"><span data-stu-id="1aea6-152">The response will contain the service key.</span></span> <span data-ttu-id="1aea6-153">You can get detailed descriptions of all the parameters by running the following:</span><span class="sxs-lookup"><span data-stu-id="1aea6-153">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-the-expressroute-circuits"></a><span data-ttu-id="1aea6-154">Step 4.</span><span class="sxs-lookup"><span data-stu-id="1aea6-154">Step 4.</span></span> <span data-ttu-id="1aea6-155">List all the ExpressRoute circuits</span><span class="sxs-lookup"><span data-stu-id="1aea6-155">List all the ExpressRoute circuits</span></span>
<span data-ttu-id="1aea6-156">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span><span class="sxs-lookup"><span data-stu-id="1aea6-156">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="1aea6-157">The response will be something similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="1aea6-157">The response will be something similar to the following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="1aea6-158">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1aea6-158">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="1aea6-159">Making the call without any parameters lists all the circuits.</span><span class="sxs-lookup"><span data-stu-id="1aea6-159">Making the call without any parameters lists all the circuits.</span></span> <span data-ttu-id="1aea6-160">Your service key will be listed in the *ServiceKey* field.</span><span class="sxs-lookup"><span data-stu-id="1aea6-160">Your service key will be listed in the *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="1aea6-161">You can get detailed descriptions of all the parameters by running the following:</span><span class="sxs-lookup"><span data-stu-id="1aea6-161">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="1aea6-162">Step 5.</span><span class="sxs-lookup"><span data-stu-id="1aea6-162">Step 5.</span></span> <span data-ttu-id="1aea6-163">Send the service key to your connectivity provider for provisioning</span><span class="sxs-lookup"><span data-stu-id="1aea6-163">Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="1aea6-164">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span><span class="sxs-lookup"><span data-stu-id="1aea6-164">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="1aea6-165">*Status* provides the state on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="1aea6-165">*Status* provides the state on the Microsoft side.</span></span> <span data-ttu-id="1aea6-166">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span><span class="sxs-lookup"><span data-stu-id="1aea6-166">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="1aea6-167">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span><span class="sxs-lookup"><span data-stu-id="1aea6-167">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="1aea6-168">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span><span class="sxs-lookup"><span data-stu-id="1aea6-168">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="1aea6-169">An ExpressRoute circuit must be in the following state for you to be able to use it:</span><span class="sxs-lookup"><span data-stu-id="1aea6-169">An ExpressRoute circuit must be in the following state for you to be able to use it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="1aea6-170">Step 6.</span><span class="sxs-lookup"><span data-stu-id="1aea6-170">Step 6.</span></span> <span data-ttu-id="1aea6-171">Periodically check the status and the state of the circuit key</span><span class="sxs-lookup"><span data-stu-id="1aea6-171">Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="1aea6-172">This lets you know when your provider has enabled your circuit.</span><span class="sxs-lookup"><span data-stu-id="1aea6-172">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="1aea6-173">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1aea6-173">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="1aea6-174">Step 7.</span><span class="sxs-lookup"><span data-stu-id="1aea6-174">Step 7.</span></span> <span data-ttu-id="1aea6-175">Create your routing configuration</span><span class="sxs-lookup"><span data-stu-id="1aea6-175">Create your routing configuration</span></span>
<span data-ttu-id="1aea6-176">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="1aea6-176">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services. If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.
> 
> 

### <a name="step-8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="1aea6-179">Step 8.</span><span class="sxs-lookup"><span data-stu-id="1aea6-179">Step 8.</span></span> <span data-ttu-id="1aea6-180">Link a virtual network to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-180">Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="1aea6-181">Next, link a virtual network to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="1aea6-181">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="1aea6-182">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="1aea6-182">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="1aea6-183">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="1aea6-183">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="1aea6-184">Getting the status of an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-184">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="1aea6-185">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1aea6-185">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="1aea6-186">Making the call without any parameters lists all the circuits.</span><span class="sxs-lookup"><span data-stu-id="1aea6-186">Making the call without any parameters lists all the circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="1aea6-187">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span><span class="sxs-lookup"><span data-stu-id="1aea6-187">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="1aea6-188">You can get detailed descriptions of all the parameters by running the following example:</span><span class="sxs-lookup"><span data-stu-id="1aea6-188">You can get detailed descriptions of all the parameters by running the following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="1aea6-189">Modifying an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-189">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="1aea6-190">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span><span class="sxs-lookup"><span data-stu-id="1aea6-190">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="1aea6-191">You can do the following with no downtime:</span><span class="sxs-lookup"><span data-stu-id="1aea6-191">You can do the following with no downtime:</span></span>

* <span data-ttu-id="1aea6-192">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="1aea6-192">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="1aea6-193">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span><span class="sxs-lookup"><span data-stu-id="1aea6-193">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="1aea6-194">Note that downgrading the bandwidth of a circuit is not supported.</span><span class="sxs-lookup"><span data-stu-id="1aea6-194">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="1aea6-195">Change the metering plan from Metered Data to Unlimited Data.</span><span class="sxs-lookup"><span data-stu-id="1aea6-195">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="1aea6-196">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span><span class="sxs-lookup"><span data-stu-id="1aea6-196">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="1aea6-197">You can enable and disable *Allow Classic Operations*.</span><span class="sxs-lookup"><span data-stu-id="1aea6-197">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="1aea6-198">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span><span class="sxs-lookup"><span data-stu-id="1aea6-198">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="1aea6-199">To enable the ExpressRoute premium add-on</span><span class="sxs-lookup"><span data-stu-id="1aea6-199">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="1aea6-200">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1aea6-200">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="1aea6-201">Your circuit will now have the ExpressRoute premium add-on features enabled.</span><span class="sxs-lookup"><span data-stu-id="1aea6-201">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="1aea6-202">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span><span class="sxs-lookup"><span data-stu-id="1aea6-202">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="1aea6-203">To disable the ExpressRoute premium add-on</span><span class="sxs-lookup"><span data-stu-id="1aea6-203">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.
> 
> 

#### <a name="considerations"></a><span data-ttu-id="1aea6-205">Considerations</span><span class="sxs-lookup"><span data-stu-id="1aea6-205">Considerations</span></span>

* <span data-ttu-id="1aea6-206">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span><span class="sxs-lookup"><span data-stu-id="1aea6-206">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="1aea6-207">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span><span class="sxs-lookup"><span data-stu-id="1aea6-207">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="1aea6-208">You must unlink all virtual networks in other geopolitical regions.</span><span class="sxs-lookup"><span data-stu-id="1aea6-208">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="1aea6-209">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span><span class="sxs-lookup"><span data-stu-id="1aea6-209">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="1aea6-210">Your route table must be less than 4,000 routes for private peering.</span><span class="sxs-lookup"><span data-stu-id="1aea6-210">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="1aea6-211">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span><span class="sxs-lookup"><span data-stu-id="1aea6-211">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-the-premium-add-on"></a><span data-ttu-id="1aea6-212">Disable the premium add-on</span><span class="sxs-lookup"><span data-stu-id="1aea6-212">Disable the premium add-on</span></span>
<span data-ttu-id="1aea6-213">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="1aea6-213">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="1aea6-214">To update the ExpressRoute circuit bandwidth</span><span class="sxs-lookup"><span data-stu-id="1aea6-214">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="1aea6-215">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span><span class="sxs-lookup"><span data-stu-id="1aea6-215">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="1aea6-216">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span><span class="sxs-lookup"><span data-stu-id="1aea6-216">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port. You cannot upgrade the circuit if there is no additional capacity available at that location.
>
> You cannot reduce the bandwidth of an ExpressRoute circuit without disruption. Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="1aea6-221">Resize a circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-221">Resize a circuit</span></span>

<span data-ttu-id="1aea6-222">After you decide what size you need, you can use the following command to resize your circuit:</span><span class="sxs-lookup"><span data-stu-id="1aea6-222">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="1aea6-223">Your circuit will have been sized up on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="1aea6-223">Your circuit will have been sized up on the Microsoft side.</span></span> <span data-ttu-id="1aea6-224">You must contact your connectivity provider to update configurations on their side to match this change.</span><span class="sxs-lookup"><span data-stu-id="1aea6-224">You must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="1aea6-225">Note that we will start billing you for the updated bandwidth option from this point on.</span><span class="sxs-lookup"><span data-stu-id="1aea6-225">Note that we will start billing you for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="1aea6-226">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span><span class="sxs-lookup"><span data-stu-id="1aea6-226">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="1aea6-227">You have to delete this circuit and create a new circuit of the size you need.</span><span class="sxs-lookup"><span data-stu-id="1aea6-227">You have to delete this circuit and create a new circuit of the size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="1aea6-228">Deprovisioning and deleting an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-228">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="1aea6-229">Considerations</span><span class="sxs-lookup"><span data-stu-id="1aea6-229">Considerations</span></span>

* <span data-ttu-id="1aea6-230">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span><span class="sxs-lookup"><span data-stu-id="1aea6-230">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="1aea6-231">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span><span class="sxs-lookup"><span data-stu-id="1aea6-231">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="1aea6-232">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span><span class="sxs-lookup"><span data-stu-id="1aea6-232">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="1aea6-233">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span><span class="sxs-lookup"><span data-stu-id="1aea6-233">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="1aea6-234">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span><span class="sxs-lookup"><span data-stu-id="1aea6-234">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="1aea6-235">This will stop billing for the circuit.</span><span class="sxs-lookup"><span data-stu-id="1aea6-235">This will stop billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="1aea6-236">Delete a circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-236">Delete a circuit</span></span>

<span data-ttu-id="1aea6-237">You can delete your ExpressRoute circuit by running the following command:</span><span class="sxs-lookup"><span data-stu-id="1aea6-237">You can delete your ExpressRoute circuit by running the following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="1aea6-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="1aea6-238">Next steps</span></span>
<span data-ttu-id="1aea6-239">After you create your circuit, make sure that you do the following:</span><span class="sxs-lookup"><span data-stu-id="1aea6-239">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="1aea6-240">Create and modify routing for your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-240">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="1aea6-241">Link your virtual network to your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="1aea6-241">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

