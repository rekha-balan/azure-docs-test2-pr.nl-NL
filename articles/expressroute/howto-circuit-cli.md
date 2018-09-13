---
title: 'Create and modify an Azure ExpressRoute circuit: CLI | Microsoft Docs'
description: This article describes how to create, provision, verify, update, delete, and deprovision an ExpressRoute circuit using CLI.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: cd4e31336fd0e90b13f1c3984de89f24e65b052b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856330"
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="d7bb7-103">Create and modify an ExpressRoute circuit using CLI</span><span class="sxs-lookup"><span data-stu-id="d7bb7-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="d7bb7-104">This article describes how to create an Azure ExpressRoute circuit by using the Command Line Interface (CLI).</span><span class="sxs-lookup"><span data-stu-id="d7bb7-104">This article describes how to create an Azure ExpressRoute circuit by using the Command Line Interface (CLI).</span></span> <span data-ttu-id="d7bb7-105">This article also shows you how to check the status, update, or delete and deprovision a circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-105">This article also shows you how to check the status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="d7bb7-106">If you want to use a different method to work with ExpressRoute circuits, you can select the article from the following list:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-106">If you want to use a different method to work with ExpressRoute circuits, you can select the article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [Video - Azure portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classic)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="d7bb7-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d7bb7-112">Before you begin</span></span>

* <span data-ttu-id="d7bb7-113">Before beginning, install the latest version of the CLI commands (2.0 or later).</span><span class="sxs-lookup"><span data-stu-id="d7bb7-113">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="d7bb7-114">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d7bb7-114">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="d7bb7-115">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-115">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create"></a><span data-ttu-id="d7bb7-116">Create and provision an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="d7bb7-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="d7bb7-117">1. Sign in to your Azure account and select your subscription</span><span class="sxs-lookup"><span data-stu-id="d7bb7-117">1. Sign in to your Azure account and select your subscription</span></span>

<span data-ttu-id="d7bb7-118">To begin your configuration, sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-118">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="d7bb7-119">Use the following examples to help you connect:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-119">Use the following examples to help you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="d7bb7-120">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-120">Check the subscriptions for the account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="d7bb7-121">Select the subscription for which you want to create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-121">Select the subscription for which you want to create an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="d7bb7-122">2. Get the list of supported providers, locations, and bandwidths</span><span class="sxs-lookup"><span data-stu-id="d7bb7-122">2. Get the list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="d7bb7-123">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-123">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="d7bb7-124">The CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-124">The CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="d7bb7-125">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-125">The response is similar to the following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="d7bb7-126">Check the response to see if your connectivity provider is listed.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-126">Check the response to see if your connectivity provider is listed.</span></span> <span data-ttu-id="d7bb7-127">Make a note of the following information, which you will need when you create a circuit:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-127">Make a note of the following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="d7bb7-128">Name</span><span class="sxs-lookup"><span data-stu-id="d7bb7-128">Name</span></span>
* <span data-ttu-id="d7bb7-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="d7bb7-129">PeeringLocations</span></span>
* <span data-ttu-id="d7bb7-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="d7bb7-130">BandwidthsOffered</span></span>

<span data-ttu-id="d7bb7-131">You're now ready to create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-131">You're now ready to create an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="d7bb7-132">3. Create an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="d7bb7-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> Your ExpressRoute circuit is billed from the moment a service key is issued. Perform this operation when the connectivity provider is ready to provision the circuit.
> 
> 

<span data-ttu-id="d7bb7-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="d7bb7-136">You can create a resource group by running the following command:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-136">You can create a resource group by running the following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="d7bb7-137">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-137">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="d7bb7-138">If you're using a different provider and different settings, substitute that information when you make your request.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="d7bb7-139">Make sure that you specify the correct SKU tier and SKU family:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-139">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="d7bb7-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="d7bb7-141">You can specify 'Standard' to get the standard SKU or 'Premium' for the premium add-on.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-141">You can specify 'Standard' to get the standard SKU or 'Premium' for the premium add-on.</span></span>
* <span data-ttu-id="d7bb7-142">SKU family determines the billing type.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-142">SKU family determines the billing type.</span></span> <span data-ttu-id="d7bb7-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="d7bb7-144">You can change the billing type from 'Metereddata' to 'Unlimiteddata', but you can't change the type from 'Unlimiteddata' to 'Metereddata'.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-144">You can change the billing type from 'Metereddata' to 'Unlimiteddata', but you can't change the type from 'Unlimiteddata' to 'Metereddata'.</span></span>


<span data-ttu-id="d7bb7-145">Your ExpressRoute circuit is billed from the moment a service key is issued.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-145">Your ExpressRoute circuit is billed from the moment a service key is issued.</span></span> <span data-ttu-id="d7bb7-146">The following example is a request for a new service key:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-146">The following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="d7bb7-147">The response contains the service key.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-147">The response contains the service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="d7bb7-148">4. List all ExpressRoute circuits</span><span class="sxs-lookup"><span data-stu-id="d7bb7-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="d7bb7-149">To get a list of all the ExpressRoute circuits that you created, run the 'az network express-route list' command.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-149">To get a list of all the ExpressRoute circuits that you created, run the 'az network express-route list' command.</span></span> <span data-ttu-id="d7bb7-150">You can retrieve this information at any time by using this command.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="d7bb7-151">To list all circuits, make the call with no parameters.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-151">To list all circuits, make the call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="d7bb7-152">Your service key is listed in the *ServiceKey* field of the response.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-152">Your service key is listed in the *ServiceKey* field of the response.</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="d7bb7-153">You can get detailed descriptions of all the parameters by running the command using the '-h' parameter.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-153">You can get detailed descriptions of all the parameters by running the command using the '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="d7bb7-154">5. Send the service key to your connectivity provider for provisioning</span><span class="sxs-lookup"><span data-stu-id="d7bb7-154">5. Send the service key to your connectivity provider for provisioning</span></span>

<span data-ttu-id="d7bb7-155">'ServiceProviderProvisioningState' provides information about the current state of provisioning on the service-provider side.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-155">'ServiceProviderProvisioningState' provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="d7bb7-156">The status provides the state on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-156">The status provides the state on the Microsoft side.</span></span> <span data-ttu-id="d7bb7-157">For more information, see the [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="d7bb7-157">For more information, see the [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="d7bb7-158">When you create a new ExpressRoute circuit, the circuit is in the following state:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-158">When you create a new ExpressRoute circuit, the circuit is in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="d7bb7-159">The circuit changes to the following state when the connectivity provider is in the process of enabling it for you:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-159">The circuit changes to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="d7bb7-160">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-160">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="d7bb7-161">6. Periodically check the status and the state of the circuit key</span><span class="sxs-lookup"><span data-stu-id="d7bb7-161">6. Periodically check the status and the state of the circuit key</span></span>

<span data-ttu-id="d7bb7-162">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-162">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="d7bb7-163">After the circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-163">After the circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in the following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="d7bb7-164">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-164">The response is similar to the following example:</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="d7bb7-165">7. Create your routing configuration</span><span class="sxs-lookup"><span data-stu-id="d7bb7-165">7. Create your routing configuration</span></span>

<span data-ttu-id="d7bb7-166">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](howto-routing-cli.md) article to create and modify circuit peerings.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-166">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](howto-routing-cli.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services. If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="d7bb7-169">8. Link a virtual network to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="d7bb7-169">8. Link a virtual network to an ExpressRoute circuit</span></span>

<span data-ttu-id="d7bb7-170">Next, link a virtual network to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-170">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="d7bb7-171">Use the [Linking virtual networks to ExpressRoute circuits](howto-linkvnet-cli.md) article.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-171">Use the [Linking virtual networks to ExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <a name="modify"></a><span data-ttu-id="d7bb7-172">Modifying an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="d7bb7-172">Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="d7bb7-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="d7bb7-174">You can make the following changes with no downtime:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-174">You can make the following changes with no downtime:</span></span>

* <span data-ttu-id="d7bb7-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="d7bb7-176">You can increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-176">You can increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="d7bb7-177">However, downgrading the bandwidth of a circuit is not supported.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-177">However, downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="d7bb7-178">You can change the metering plan from Metered Data to Unlimited Data.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-178">You can change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="d7bb7-179">However, changing the metering plan from Unlimited Data to Metered Data is not supported.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-179">However, changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="d7bb7-180">You can enable and disable *Allow Classic Operations*.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="d7bb7-181">For more information on limits and limitations, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="d7bb7-181">For more information on limits and limitations, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="d7bb7-182">To enable the ExpressRoute premium add-on</span><span class="sxs-lookup"><span data-stu-id="d7bb7-182">To enable the ExpressRoute premium add-on</span></span>

<span data-ttu-id="d7bb7-183">You can enable the ExpressRoute premium add-on for your existing circuit by using the following command:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-183">You can enable the ExpressRoute premium add-on for your existing circuit by using the following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="d7bb7-184">The circuit now has the ExpressRoute premium add-on features enabled.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-184">The circuit now has the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="d7bb7-185">We begin billing you for the premium add-on capability as soon as the command has successfully run.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-185">We begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="d7bb7-186">To disable the ExpressRoute premium add-on</span><span class="sxs-lookup"><span data-stu-id="d7bb7-186">To disable the ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.
> 
> 

<span data-ttu-id="d7bb7-188">Before disabling the ExpressRoute premium add-on, understand the following criteria:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-188">Before disabling the ExpressRoute premium add-on, understand the following criteria:</span></span>

* <span data-ttu-id="d7bb7-189">Before you downgrade from premium to standard, you must make sure that you have fewer than 10 virtual networks linked to the circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-189">Before you downgrade from premium to standard, you must make sure that you have fewer than 10 virtual networks linked to the circuit.</span></span> <span data-ttu-id="d7bb7-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="d7bb7-191">You must unlink all virtual networks in other geopolitical regions.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="d7bb7-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="d7bb7-193">Your route table must be less than 4,000 routes for private peering.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="d7bb7-194">If your route table size is greater than 4,000 routes, the BGP session drops.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-194">If your route table size is greater than 4,000 routes, the BGP session drops.</span></span> <span data-ttu-id="d7bb7-195">The session won't be reenabled until the number of advertised prefixes is below 4,000.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-195">The session won't be reenabled until the number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="d7bb7-196">You can disable the ExpressRoute premium add-on for the existing circuit by using the following example:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-196">You can disable the ExpressRoute premium add-on for the existing circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="d7bb7-197">To update the ExpressRoute circuit bandwidth</span><span class="sxs-lookup"><span data-stu-id="d7bb7-197">To update the ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="d7bb7-198">For the supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="d7bb7-198">For the supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="d7bb7-199">You can pick any size greater than the size of your existing circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-199">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> If there is inadequate capacity on the existing port, you may have to recreate the ExpressRoute circuit. You cannot upgrade the circuit if there is no additional capacity available at that location.
>
> You cannot reduce the bandwidth of an ExpressRoute circuit without disruption. Downgrading bandwidth requires you to deprovision the ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.
>

<span data-ttu-id="d7bb7-204">After you decide the size you need, use the following command to resize your circuit:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-204">After you decide the size you need, use the following command to resize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="d7bb7-205">Your circuit is sized up on the Microsoft side.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-205">Your circuit is sized up on the Microsoft side.</span></span> <span data-ttu-id="d7bb7-206">Next, you must contact your connectivity provider to update configurations on their side to match this change.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-206">Next, you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="d7bb7-207">After you make this notification, we begin billing you for the updated bandwidth option.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-207">After you make this notification, we begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="d7bb7-208">To move the SKU from metered to unlimited</span><span class="sxs-lookup"><span data-stu-id="d7bb7-208">To move the SKU from metered to unlimited</span></span>

<span data-ttu-id="d7bb7-209">You can change the SKU of an ExpressRoute circuit by using the following example:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-209">You can change the SKU of an ExpressRoute circuit by using the following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="d7bb7-210">To control access to the classic and Resource Manager environments</span><span class="sxs-lookup"><span data-stu-id="d7bb7-210">To control access to the classic and Resource Manager environments</span></span>

<span data-ttu-id="d7bb7-211">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d7bb7-211">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="delete"></a><span data-ttu-id="d7bb7-212">Deprovisioning and deleting an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="d7bb7-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="d7bb7-213">To deprovision and delete an ExpressRoute circuit, make sure you understand the following criteria:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-213">To deprovision and delete an ExpressRoute circuit, make sure you understand the following criteria:</span></span>

* <span data-ttu-id="d7bb7-214">You must unlink all virtual networks from the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-214">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="d7bb7-215">If this operation fails, check to see if any virtual networks are linked to the circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-215">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="d7bb7-216">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider to deprovision the circuit on their side.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-216">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="d7bb7-217">We continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-217">We continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="d7bb7-218">You can delete the circuit if the service provider has deprovisioned the circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-218">You can delete the circuit if the service provider has deprovisioned the circuit.</span></span> <span data-ttu-id="d7bb7-219">When a circuit is deprovisioned, the service provider provisioning state is set to **Not provisioned**.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-219">When a circuit is deprovisioned, the service provider provisioning state is set to **Not provisioned**.</span></span> <span data-ttu-id="d7bb7-220">This stops billing for the circuit.</span><span class="sxs-lookup"><span data-stu-id="d7bb7-220">This stops billing for the circuit.</span></span>

<span data-ttu-id="d7bb7-221">You can delete your ExpressRoute circuit by running the following command:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-221">You can delete your ExpressRoute circuit by running the following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d7bb7-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7bb7-222">Next steps</span></span>

<span data-ttu-id="d7bb7-223">After you create your circuit, make sure that you do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="d7bb7-223">After you create your circuit, make sure that you do the following tasks:</span></span>

* [<span data-ttu-id="d7bb7-224">Create and modify routing for your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="d7bb7-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="d7bb7-225">Link your virtual network to your ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="d7bb7-225">Link your virtual network to your ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)