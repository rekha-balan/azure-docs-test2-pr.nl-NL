---
title: 'How to configure routing for an Azure ExpressRoute circuit: CLI | Microsoft Docs'
description: This article helps you create and provision the private, public and Microsoft peering of an ExpressRoute circuit. This article also shows you how to check the status, update, or delete peerings for your circuit.
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
ms.date: 10/11/2017
ms.author: cherylmc
ms.openlocfilehash: f4ad959de1425e828ce11fb658f8b5304e9d8775
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857294"
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="7bd08-104">Create and modify routing for an ExpressRoute circuit using CLI</span><span class="sxs-lookup"><span data-stu-id="7bd08-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="7bd08-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span><span class="sxs-lookup"><span data-stu-id="7bd08-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="7bd08-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="7bd08-107">If you want to use a different method to work with your circuit, select an article from the following list:</span><span class="sxs-lookup"><span data-stu-id="7bd08-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [Video - Private peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - Public peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (classic)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="7bd08-115">Configuration prerequisites</span><span class="sxs-lookup"><span data-stu-id="7bd08-115">Configuration prerequisites</span></span>

* <span data-ttu-id="7bd08-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span><span class="sxs-lookup"><span data-stu-id="7bd08-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="7bd08-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7bd08-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="7bd08-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="7bd08-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="7bd08-119">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="7bd08-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="7bd08-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="7bd08-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span><span class="sxs-lookup"><span data-stu-id="7bd08-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span></span>

<span data-ttu-id="7bd08-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span><span class="sxs-lookup"><span data-stu-id="7bd08-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="7bd08-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span><span class="sxs-lookup"><span data-stu-id="7bd08-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="7bd08-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="7bd08-125">You can configure peerings in any order you choose.</span><span class="sxs-lookup"><span data-stu-id="7bd08-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="7bd08-126">However, you must make sure that you complete the configuration of each peering one at a time.</span><span class="sxs-lookup"><span data-stu-id="7bd08-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> <span data-ttu-id="7bd08-127">For more information about routing domains and peerings, see [ExpressRoute routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="7bd08-127">For more information about routing domains and peerings, see [ExpressRoute routing domains](expressroute-circuit-peerings.md).</span></span>

## <a name="msft"></a><span data-ttu-id="7bd08-128">Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-128">Microsoft peering</span></span>

<span data-ttu-id="7bd08-129">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-129">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined. Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit. For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="7bd08-133">To create Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-133">To create Microsoft peering</span></span>

1. <span data-ttu-id="7bd08-134">Install the latest version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7bd08-134">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="7bd08-135">Use the latest version of the Azure Command-line Interface (CLI).\* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="7bd08-135">Use the latest version of the Azure Command-line Interface (CLI).\* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="7bd08-136">Select the subscription for which you want to create ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-136">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="7bd08-137">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-137">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="7bd08-138">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="7bd08-138">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="7bd08-139">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Microsoft peering for you.</span><span class="sxs-lookup"><span data-stu-id="7bd08-139">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Microsoft peering for you.</span></span> <span data-ttu-id="7bd08-140">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="7bd08-140">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="7bd08-141">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span><span class="sxs-lookup"><span data-stu-id="7bd08-141">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span> 

3. <span data-ttu-id="7bd08-142">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span><span class="sxs-lookup"><span data-stu-id="7bd08-142">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="7bd08-143">Use the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-143">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="7bd08-144">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-144">The response is similar to the following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="7bd08-145">Configure Microsoft peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-145">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="7bd08-146">Make sure that you have the following information before you proceed.</span><span class="sxs-lookup"><span data-stu-id="7bd08-146">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="7bd08-147">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="7bd08-147">A /30 subnet for the primary link.</span></span> <span data-ttu-id="7bd08-148">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="7bd08-148">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="7bd08-149">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="7bd08-149">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="7bd08-150">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="7bd08-150">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="7bd08-151">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="7bd08-151">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="7bd08-152">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="7bd08-152">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="7bd08-153">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="7bd08-153">AS number for peering.</span></span> <span data-ttu-id="7bd08-154">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="7bd08-154">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="7bd08-155">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span><span class="sxs-lookup"><span data-stu-id="7bd08-155">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="7bd08-156">Only public IP address prefixes are accepted.</span><span class="sxs-lookup"><span data-stu-id="7bd08-156">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="7bd08-157">If you plan to send a set of prefixes, you can send a comma-separated list.</span><span class="sxs-lookup"><span data-stu-id="7bd08-157">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="7bd08-158">These prefixes must be registered to you in an RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="7bd08-158">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="7bd08-159">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span><span class="sxs-lookup"><span data-stu-id="7bd08-159">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="7bd08-160">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span><span class="sxs-lookup"><span data-stu-id="7bd08-160">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="7bd08-161">**Optional -** An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="7bd08-161">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="7bd08-162">Run the following example to configure Microsoft peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="7bd08-162">Run the following example to configure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="getmsft"></a><span data-ttu-id="7bd08-163">To view Microsoft peering details</span><span class="sxs-lookup"><span data-stu-id="7bd08-163">To view Microsoft peering details</span></span>

<span data-ttu-id="7bd08-164">You can get configuration details by using the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-164">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="7bd08-165">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-165">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="updatemsft"></a><span data-ttu-id="7bd08-166">To update Microsoft peering configuration</span><span class="sxs-lookup"><span data-stu-id="7bd08-166">To update Microsoft peering configuration</span></span>

<span data-ttu-id="7bd08-167">You can update any part of the configuration.</span><span class="sxs-lookup"><span data-stu-id="7bd08-167">You can update any part of the configuration.</span></span> <span data-ttu-id="7bd08-168">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-168">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="addIPv6msft"></a><span data-ttu-id="7bd08-169">To add IPv6 Microsoft peering settings to an existing IPv4 configuration</span><span class="sxs-lookup"><span data-stu-id="7bd08-169">To add IPv6 Microsoft peering settings to an existing IPv4 configuration</span></span>

```azurecli
az network express-route peering update -g ExpressRouteResourceGroup --circuit-name MyCircuit --peering-type MicrosoftPeering --ip-version ipv6 --primary-peer-subnet 2002:db00::/126 --secondary-peer-subnet 2003:db00::/126 --advertised-public-prefixes 2002:db00::/126
```

### <a name="deletemsft"></a><span data-ttu-id="7bd08-170">To delete Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-170">To delete Microsoft peering</span></span>

<span data-ttu-id="7bd08-171">You can remove your peering configuration by running the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-171">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="private"></a><span data-ttu-id="7bd08-172">Azure private peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-172">Azure private peering</span></span>

<span data-ttu-id="7bd08-173">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-173">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="7bd08-174">To create Azure private peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-174">To create Azure private peering</span></span>

1. <span data-ttu-id="7bd08-175">Install the latest version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7bd08-175">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="7bd08-176">You must use the latest version of the Azure Command-line Interface (CLI).\* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="7bd08-176">You must use the latest version of the Azure Command-line Interface (CLI).\* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="7bd08-177">Select the subscription you want to create ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="7bd08-177">Select the subscription you want to create ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="7bd08-178">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-178">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="7bd08-179">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="7bd08-179">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="7bd08-180">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Azure private peering for you.</span><span class="sxs-lookup"><span data-stu-id="7bd08-180">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="7bd08-181">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="7bd08-181">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="7bd08-182">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span><span class="sxs-lookup"><span data-stu-id="7bd08-182">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="7bd08-183">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span><span class="sxs-lookup"><span data-stu-id="7bd08-183">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="7bd08-184">Use the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-184">Use the following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="7bd08-185">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-185">The response is similar to the following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="7bd08-186">Configure Azure private peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-186">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="7bd08-187">Make sure that you have the following items before you proceed with the next steps:</span><span class="sxs-lookup"><span data-stu-id="7bd08-187">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="7bd08-188">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="7bd08-188">A /30 subnet for the primary link.</span></span> <span data-ttu-id="7bd08-189">The subnet must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="7bd08-189">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="7bd08-190">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="7bd08-190">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="7bd08-191">The subnet must not be part of any address space reserved for virtual networks.</span><span class="sxs-lookup"><span data-stu-id="7bd08-191">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="7bd08-192">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="7bd08-192">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="7bd08-193">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="7bd08-193">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="7bd08-194">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="7bd08-194">AS number for peering.</span></span> <span data-ttu-id="7bd08-195">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="7bd08-195">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="7bd08-196">You can use a private AS number for this peering.</span><span class="sxs-lookup"><span data-stu-id="7bd08-196">You can use a private AS number for this peering.</span></span> <span data-ttu-id="7bd08-197">Ensure that you are not using 65515.</span><span class="sxs-lookup"><span data-stu-id="7bd08-197">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="7bd08-198">**Optional -** An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="7bd08-198">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="7bd08-199">Use the following example to configure Azure private peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="7bd08-199">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="7bd08-200">If you choose to use an MD5 hash, use the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-200">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Ensure that you specify your AS number as peering ASN, not customer ASN.
  > 
  > 

### <a name="getprivate"></a><span data-ttu-id="7bd08-202">To view Azure private peering details</span><span class="sxs-lookup"><span data-stu-id="7bd08-202">To view Azure private peering details</span></span>

<span data-ttu-id="7bd08-203">You can get configuration details by using the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-203">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="7bd08-204">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-204">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="updateprivate"></a><span data-ttu-id="7bd08-205">To update Azure private peering configuration</span><span class="sxs-lookup"><span data-stu-id="7bd08-205">To update Azure private peering configuration</span></span>

<span data-ttu-id="7bd08-206">You can update any part of the configuration using the following example.</span><span class="sxs-lookup"><span data-stu-id="7bd08-206">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="7bd08-207">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span><span class="sxs-lookup"><span data-stu-id="7bd08-207">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="deleteprivate"></a><span data-ttu-id="7bd08-208">To delete Azure private peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-208">To delete Azure private peering</span></span>

<span data-ttu-id="7bd08-209">You can remove your peering configuration by running the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-209">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="public"></a><span data-ttu-id="7bd08-211">Azure public peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-211">Azure public peering</span></span>

<span data-ttu-id="7bd08-212">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-212">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="7bd08-213">To create Azure public peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-213">To create Azure public peering</span></span>

1. <span data-ttu-id="7bd08-214">Install the latest version of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7bd08-214">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="7bd08-215">You must use the latest version of the Azure Command-line Interface (CLI).\* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="7bd08-215">You must use the latest version of the Azure Command-line Interface (CLI).\* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="7bd08-216">Select the subscription for which you want to create ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-216">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="7bd08-217">Create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-217">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="7bd08-218">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="7bd08-218">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="7bd08-219">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Azure public peering for you.</span><span class="sxs-lookup"><span data-stu-id="7bd08-219">If your connectivity provider offers managed Layer 3 services, you can ask your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="7bd08-220">In that case, you won't need to follow instructions listed in the next sections.</span><span class="sxs-lookup"><span data-stu-id="7bd08-220">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="7bd08-221">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span><span class="sxs-lookup"><span data-stu-id="7bd08-221">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="7bd08-222">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span><span class="sxs-lookup"><span data-stu-id="7bd08-222">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="7bd08-223">Use the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-223">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="7bd08-224">The response is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-224">The response is similar to the following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="7bd08-225">Configure Azure public peering for the circuit.</span><span class="sxs-lookup"><span data-stu-id="7bd08-225">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="7bd08-226">Make sure that you have the following information before you proceed further.</span><span class="sxs-lookup"><span data-stu-id="7bd08-226">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="7bd08-227">A /30 subnet for the primary link.</span><span class="sxs-lookup"><span data-stu-id="7bd08-227">A /30 subnet for the primary link.</span></span> <span data-ttu-id="7bd08-228">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="7bd08-228">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="7bd08-229">A /30 subnet for the secondary link.</span><span class="sxs-lookup"><span data-stu-id="7bd08-229">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="7bd08-230">This must be a valid public IPv4 prefix.</span><span class="sxs-lookup"><span data-stu-id="7bd08-230">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="7bd08-231">A valid VLAN ID to establish this peering on.</span><span class="sxs-lookup"><span data-stu-id="7bd08-231">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="7bd08-232">Ensure that no other peering in the circuit uses the same VLAN ID.</span><span class="sxs-lookup"><span data-stu-id="7bd08-232">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="7bd08-233">AS number for peering.</span><span class="sxs-lookup"><span data-stu-id="7bd08-233">AS number for peering.</span></span> <span data-ttu-id="7bd08-234">You can use both 2-byte and 4-byte AS numbers.</span><span class="sxs-lookup"><span data-stu-id="7bd08-234">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="7bd08-235">**Optional -** An MD5 hash if you choose to use one.</span><span class="sxs-lookup"><span data-stu-id="7bd08-235">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="7bd08-236">Run the following example to configure Azure public peering for your circuit:</span><span class="sxs-lookup"><span data-stu-id="7bd08-236">Run the following example to configure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="7bd08-237">If you choose to use an MD5 hash, use the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-237">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Ensure that you specify your AS number as peering ASN, not customer ASN.

### <a name="getpublic"></a><span data-ttu-id="7bd08-239">To view Azure public peering details</span><span class="sxs-lookup"><span data-stu-id="7bd08-239">To view Azure public peering details</span></span>

<span data-ttu-id="7bd08-240">You can get configuration details using the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-240">You can get configuration details using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="7bd08-241">The output is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-241">The output is similar to the following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="updatepublic"></a><span data-ttu-id="7bd08-242">To update Azure public peering configuration</span><span class="sxs-lookup"><span data-stu-id="7bd08-242">To update Azure public peering configuration</span></span>

<span data-ttu-id="7bd08-243">You can update any part of the configuration using the following example.</span><span class="sxs-lookup"><span data-stu-id="7bd08-243">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="7bd08-244">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span><span class="sxs-lookup"><span data-stu-id="7bd08-244">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="deletepublic"></a><span data-ttu-id="7bd08-245">To delete Azure public peering</span><span class="sxs-lookup"><span data-stu-id="7bd08-245">To delete Azure public peering</span></span>

<span data-ttu-id="7bd08-246">You can remove your peering configuration by running the following example:</span><span class="sxs-lookup"><span data-stu-id="7bd08-246">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="next-steps"></a><span data-ttu-id="7bd08-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="7bd08-247">Next steps</span></span>

<span data-ttu-id="7bd08-248">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7bd08-248">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="7bd08-249">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="7bd08-249">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="7bd08-250">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="7bd08-250">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="7bd08-251">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7bd08-251">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>