---
title: 'Configure route filters for Azure ExpressRoute Microsoft peering: CLI | Microsoft Docs'
description: This article describes how to configure route filters for Microsoft Peering using Azure CLI
documentationcenter: na
services: expressroute
author: anzaman
manager: ganesr
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: anzaman
ms.openlocfilehash: a85a68393f3dc946db651791de9efff0694f9989
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870803"
---
# <a name="configure-route-filters-for-microsoft-peering-azure-cli"></a><span data-ttu-id="eea1d-103">Configure route filters for Microsoft peering: Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eea1d-103">Configure route filters for Microsoft peering: Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](how-to-routefilter-portal.md)
> * [Azure PowerShell](how-to-routefilter-powershell.md)
> * [Azure CLI](how-to-routefilter-cli.md)
> 

<span data-ttu-id="eea1d-107">Route filters are a way to consume a subset of supported services through Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="eea1d-107">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="eea1d-108">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="eea1d-108">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="eea1d-109">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="eea1d-109">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="eea1d-110">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span><span class="sxs-lookup"><span data-stu-id="eea1d-110">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="eea1d-111">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span><span class="sxs-lookup"><span data-stu-id="eea1d-111">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="eea1d-112">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="eea1d-112">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="eea1d-113">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span><span class="sxs-lookup"><span data-stu-id="eea1d-113">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="eea1d-114">This significantly increases the size of the route tables maintained by routers within your network.</span><span class="sxs-lookup"><span data-stu-id="eea1d-114">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="eea1d-115">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span><span class="sxs-lookup"><span data-stu-id="eea1d-115">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="eea1d-116">You can:</span><span class="sxs-lookup"><span data-stu-id="eea1d-116">You can:</span></span>

* <span data-ttu-id="eea1d-117">Filter out unwanted prefixes by applying route filters on BGP communities.</span><span class="sxs-lookup"><span data-stu-id="eea1d-117">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="eea1d-118">This is a standard networking practice and is used commonly within many networks.</span><span class="sxs-lookup"><span data-stu-id="eea1d-118">This is a standard networking practice and is used commonly within many networks.</span></span>

* <span data-ttu-id="eea1d-119">Define route filters and apply them to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="eea1d-119">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="eea1d-120">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="eea1d-120">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="eea1d-121">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span><span class="sxs-lookup"><span data-stu-id="eea1d-121">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <a name="about"></a><span data-ttu-id="eea1d-122">About route filters</span><span class="sxs-lookup"><span data-stu-id="eea1d-122">About route filters</span></span>

<span data-ttu-id="eea1d-123">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span><span class="sxs-lookup"><span data-stu-id="eea1d-123">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="eea1d-124">No routes are advertised to your network.</span><span class="sxs-lookup"><span data-stu-id="eea1d-124">No routes are advertised to your network.</span></span> <span data-ttu-id="eea1d-125">To enable route advertisements to your network, you must associate a route filter.</span><span class="sxs-lookup"><span data-stu-id="eea1d-125">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="eea1d-126">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="eea1d-126">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="eea1d-127">It is essentially a white list of all the BGP community values.</span><span class="sxs-lookup"><span data-stu-id="eea1d-127">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="eea1d-128">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span><span class="sxs-lookup"><span data-stu-id="eea1d-128">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="eea1d-129">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="eea1d-129">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="eea1d-130">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span><span class="sxs-lookup"><span data-stu-id="eea1d-130">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="eea1d-131">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="eea1d-131">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="eea1d-132">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span><span class="sxs-lookup"><span data-stu-id="eea1d-132">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined. Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.
> 
> 

### <a name="workflow"></a><span data-ttu-id="eea1d-135">Workflow</span><span class="sxs-lookup"><span data-stu-id="eea1d-135">Workflow</span></span>

<span data-ttu-id="eea1d-136">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span><span class="sxs-lookup"><span data-stu-id="eea1d-136">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

* <span data-ttu-id="eea1d-137">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span><span class="sxs-lookup"><span data-stu-id="eea1d-137">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="eea1d-138">You can use the following instructions to accomplish these tasks:</span><span class="sxs-lookup"><span data-stu-id="eea1d-138">You can use the following instructions to accomplish these tasks:</span></span>
  * <span data-ttu-id="eea1d-139">[Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="eea1d-139">[Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="eea1d-140">The ExpressRoute circuit must be in a provisioned and enabled state.</span><span class="sxs-lookup"><span data-stu-id="eea1d-140">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  * <span data-ttu-id="eea1d-141">[Create Microsoft peering](howto-routing-cli.md) if you manage the BGP session directly.</span><span class="sxs-lookup"><span data-stu-id="eea1d-141">[Create Microsoft peering](howto-routing-cli.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="eea1d-142">Or, have your connectivity provider provision Microsoft peering for your circuit.</span><span class="sxs-lookup"><span data-stu-id="eea1d-142">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

* <span data-ttu-id="eea1d-143">You must create and configure a route filter.</span><span class="sxs-lookup"><span data-stu-id="eea1d-143">You must create and configure a route filter.</span></span>
  * <span data-ttu-id="eea1d-144">Identify the services you with to consume through Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="eea1d-144">Identify the services you with to consume through Microsoft peering</span></span>
  * <span data-ttu-id="eea1d-145">Identify the list of BGP community values associated with the services</span><span class="sxs-lookup"><span data-stu-id="eea1d-145">Identify the list of BGP community values associated with the services</span></span>
  * <span data-ttu-id="eea1d-146">Create a rule to allow the prefix list matching the BGP community values</span><span class="sxs-lookup"><span data-stu-id="eea1d-146">Create a rule to allow the prefix list matching the BGP community values</span></span>

* <span data-ttu-id="eea1d-147">You must attach the route filter to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="eea1d-147">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="eea1d-148">Before you begin</span><span class="sxs-lookup"><span data-stu-id="eea1d-148">Before you begin</span></span>

<span data-ttu-id="eea1d-149">Before beginning, install the latest version of the CLI commands (2.0 or later).</span><span class="sxs-lookup"><span data-stu-id="eea1d-149">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="eea1d-150">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eea1d-150">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

* <span data-ttu-id="eea1d-151">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="eea1d-151">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

* <span data-ttu-id="eea1d-152">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="eea1d-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="eea1d-153">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="eea1d-153">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="eea1d-154">The ExpressRoute circuit must be in a provisioned and enabled state.</span><span class="sxs-lookup"><span data-stu-id="eea1d-154">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

* <span data-ttu-id="eea1d-155">You must have an active Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="eea1d-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="eea1d-156">Follow instructions at [Create and modifying peering configuration](howto-routing-cli.md)</span><span class="sxs-lookup"><span data-stu-id="eea1d-156">Follow instructions at [Create and modifying peering configuration](howto-routing-cli.md)</span></span>

### <a name="sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="eea1d-157">Sign in to your Azure account and select your subscription</span><span class="sxs-lookup"><span data-stu-id="eea1d-157">Sign in to your Azure account and select your subscription</span></span>

<span data-ttu-id="eea1d-158">To begin your configuration, sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="eea1d-158">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="eea1d-159">Use the following examples to help you connect:</span><span class="sxs-lookup"><span data-stu-id="eea1d-159">Use the following examples to help you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="eea1d-160">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="eea1d-160">Check the subscriptions for the account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="eea1d-161">Select the subscription for which you want to create an ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="eea1d-161">Select the subscription for which you want to create an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

## <a name="prefixes"></a><span data-ttu-id="eea1d-162">Step 1: Get a list of prefixes and BGP community values</span><span class="sxs-lookup"><span data-stu-id="eea1d-162">Step 1: Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="eea1d-163">1. Get a list of BGP community values</span><span class="sxs-lookup"><span data-stu-id="eea1d-163">1. Get a list of BGP community values</span></span>

<span data-ttu-id="eea1d-164">Use the following cmdlet to get the list of BGP community values associated with services accessible through Microsoft peering, and the list of prefixes associated with them:</span><span class="sxs-lookup"><span data-stu-id="eea1d-164">Use the following cmdlet to get the list of BGP community values associated with services accessible through Microsoft peering, and the list of prefixes associated with them:</span></span>

```azurecli
az network route-filter rule list-service-communities
```
### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="eea1d-165">2. Make a list of the values that you want to use</span><span class="sxs-lookup"><span data-stu-id="eea1d-165">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="eea1d-166">Make a list of BGP community values you want to use in the route filter.</span><span class="sxs-lookup"><span data-stu-id="eea1d-166">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="eea1d-167">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="eea1d-167">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <a name="filter"></a><span data-ttu-id="eea1d-168">Step 2: Create a route filter and a filter rule</span><span class="sxs-lookup"><span data-stu-id="eea1d-168">Step 2: Create a route filter and a filter rule</span></span>

<span data-ttu-id="eea1d-169">A route filter can have only one rule, and the rule must be of type 'Allow'.</span><span class="sxs-lookup"><span data-stu-id="eea1d-169">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="eea1d-170">This rule can have a list of BGP community values associated with it.</span><span class="sxs-lookup"><span data-stu-id="eea1d-170">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="eea1d-171">1. Create a route filter</span><span class="sxs-lookup"><span data-stu-id="eea1d-171">1. Create a route filter</span></span>

<span data-ttu-id="eea1d-172">First, create the route filter.</span><span class="sxs-lookup"><span data-stu-id="eea1d-172">First, create the route filter.</span></span> <span data-ttu-id="eea1d-173">The command 'az network route-filter create' only creates a route filter resource.</span><span class="sxs-lookup"><span data-stu-id="eea1d-173">The command 'az network route-filter create' only creates a route filter resource.</span></span> <span data-ttu-id="eea1d-174">After you create the resource, you must then create a rule and attach it to the route filter object.</span><span class="sxs-lookup"><span data-stu-id="eea1d-174">After you create the resource, you must then create a rule and attach it to the route filter object.</span></span> <span data-ttu-id="eea1d-175">Run the following command to create a route filter resource:</span><span class="sxs-lookup"><span data-stu-id="eea1d-175">Run the following command to create a route filter resource:</span></span>

```azurecli
az network route-filter create -n MyRouteFilter -g MyResourceGroup
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="eea1d-176">2. Create a filter rule</span><span class="sxs-lookup"><span data-stu-id="eea1d-176">2. Create a filter rule</span></span>

<span data-ttu-id="eea1d-177">Run the following command to create a new rule:</span><span class="sxs-lookup"><span data-stu-id="eea1d-177">Run the following command to create a new rule:</span></span>
 
```azurecli
az network route-filter rule create --filter-name MyRouteFilter -n CRM --communities 12076:5040 --access Allow -g MyResourceGroup
```

## <a name="attach"></a><span data-ttu-id="eea1d-178">Step 3: Attach the route filter to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="eea1d-178">Step 3: Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="eea1d-179">Run the following command to attach the route filter to the ExpressRoute circuit:</span><span class="sxs-lookup"><span data-stu-id="eea1d-179">Run the following command to attach the route filter to the ExpressRoute circuit:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroupName --name MicrosoftPeering --route-filter MyRouteFilter
```

## <a name="tasks"></a><span data-ttu-id="eea1d-180">Common tasks</span><span class="sxs-lookup"><span data-stu-id="eea1d-180">Common tasks</span></span>

### <a name="getproperties"></a><span data-ttu-id="eea1d-181">To get the properties of a route filter</span><span class="sxs-lookup"><span data-stu-id="eea1d-181">To get the properties of a route filter</span></span>

<span data-ttu-id="eea1d-182">To get the properties of a route filter, use the following command:</span><span class="sxs-lookup"><span data-stu-id="eea1d-182">To get the properties of a route filter, use the following command:</span></span>

```azurecli
az network route-filter show -g ExpressRouteResourceGroupName --name MyRouteFilter 
```

### <a name="updateproperties"></a><span data-ttu-id="eea1d-183">To update the properties of a route filter</span><span class="sxs-lookup"><span data-stu-id="eea1d-183">To update the properties of a route filter</span></span>

<span data-ttu-id="eea1d-184">If the route filter is already attached to a circuit, updates to the BGP community list automatically propagate appropriate prefix advertisement changes through the established BGP sessions.</span><span class="sxs-lookup"><span data-stu-id="eea1d-184">If the route filter is already attached to a circuit, updates to the BGP community list automatically propagate appropriate prefix advertisement changes through the established BGP sessions.</span></span> <span data-ttu-id="eea1d-185">You can update the BGP community list of your route filter using the following command:</span><span class="sxs-lookup"><span data-stu-id="eea1d-185">You can update the BGP community list of your route filter using the following command:</span></span>

```azurecli
az network route-filter rule update --filter-name MyRouteFilter -n CRM -g ExpressRouteResourceGroupName --add communities '12076:5040' --add communities '12076:5010'
```

### <a name="detach"></a><span data-ttu-id="eea1d-186">To detach a route filter from an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="eea1d-186">To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="eea1d-187">Once a route filter is detached from the ExpressRoute circuit, no prefixes are advertised through the BGP session.</span><span class="sxs-lookup"><span data-stu-id="eea1d-187">Once a route filter is detached from the ExpressRoute circuit, no prefixes are advertised through the BGP session.</span></span> <span data-ttu-id="eea1d-188">You can detach a route filter from an ExpressRoute circuit using the following command:</span><span class="sxs-lookup"><span data-stu-id="eea1d-188">You can detach a route filter from an ExpressRoute circuit using the following command:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroupName --name MicrosoftPeering --remove routeFilter
```

### <a name="delete"></a><span data-ttu-id="eea1d-189">To delete a route filter</span><span class="sxs-lookup"><span data-stu-id="eea1d-189">To delete a route filter</span></span>

<span data-ttu-id="eea1d-190">You can only delete a route filter if it is not attached to any circuit.</span><span class="sxs-lookup"><span data-stu-id="eea1d-190">You can only delete a route filter if it is not attached to any circuit.</span></span> <span data-ttu-id="eea1d-191">Ensure that the route filter is not attached to any circuit before attempting to delete it.</span><span class="sxs-lookup"><span data-stu-id="eea1d-191">Ensure that the route filter is not attached to any circuit before attempting to delete it.</span></span> <span data-ttu-id="eea1d-192">You can delete a route filter using the following command:</span><span class="sxs-lookup"><span data-stu-id="eea1d-192">You can delete a route filter using the following command:</span></span>

```azurecli
az network route-filter delete -n MyRouteFilter -g MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="eea1d-193">Next Steps</span><span class="sxs-lookup"><span data-stu-id="eea1d-193">Next Steps</span></span>

<span data-ttu-id="eea1d-194">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="eea1d-194">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
