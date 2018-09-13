---
title: 'Configure route filters for Azure ExpressRoute Microsoft peering: Portal | Microsoft Docs'
description: This article describes how to configure route filters for Microsoft Peering using the Azure portal
documentationcenter: na
services: expressroute
author: ganesr
manager: rossort
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/26/2017
ms.author: ganesr
ms.openlocfilehash: 37e2ab0bea7edf9971173e136259da04224d2989
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858028"
---
# <a name="configure-route-filters-for-microsoft-peering-azure-portal"></a><span data-ttu-id="22a5f-103">Configure route filters for Microsoft peering: Azure portal</span><span class="sxs-lookup"><span data-stu-id="22a5f-103">Configure route filters for Microsoft peering: Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](how-to-routefilter-portal.md)
> * [Azure PowerShell](how-to-routefilter-powershell.md)
> * [Azure CLI](how-to-routefilter-cli.md)
> 

<span data-ttu-id="22a5f-107">Route filters are a way to consume a subset of supported services through Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="22a5f-107">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="22a5f-108">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="22a5f-108">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="22a5f-109">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, and Azure services such as storage and SQL DB are accessible through Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="22a5f-109">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, and Azure services such as storage and SQL DB are accessible through Microsoft peering.</span></span> <span data-ttu-id="22a5f-110">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span><span class="sxs-lookup"><span data-stu-id="22a5f-110">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="22a5f-111">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span><span class="sxs-lookup"><span data-stu-id="22a5f-111">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="22a5f-112">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="22a5f-112">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="22a5f-113">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span><span class="sxs-lookup"><span data-stu-id="22a5f-113">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="22a5f-114">This significantly increases the size of the route tables maintained by routers within your network.</span><span class="sxs-lookup"><span data-stu-id="22a5f-114">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="22a5f-115">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span><span class="sxs-lookup"><span data-stu-id="22a5f-115">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="22a5f-116">You can:</span><span class="sxs-lookup"><span data-stu-id="22a5f-116">You can:</span></span>

- <span data-ttu-id="22a5f-117">Filter out unwanted prefixes by applying route filters on BGP communities.</span><span class="sxs-lookup"><span data-stu-id="22a5f-117">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="22a5f-118">This is a standard networking practice and is used commonly within many networks.</span><span class="sxs-lookup"><span data-stu-id="22a5f-118">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="22a5f-119">Define route filters and apply them to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="22a5f-119">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="22a5f-120">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="22a5f-120">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="22a5f-121">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span><span class="sxs-lookup"><span data-stu-id="22a5f-121">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <a name="about"></a><span data-ttu-id="22a5f-122">About route filters</span><span class="sxs-lookup"><span data-stu-id="22a5f-122">About route filters</span></span>

<span data-ttu-id="22a5f-123">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span><span class="sxs-lookup"><span data-stu-id="22a5f-123">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="22a5f-124">No routes are advertised to your network.</span><span class="sxs-lookup"><span data-stu-id="22a5f-124">No routes are advertised to your network.</span></span> <span data-ttu-id="22a5f-125">To enable route advertisements to your network, you must associate a route filter.</span><span class="sxs-lookup"><span data-stu-id="22a5f-125">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="22a5f-126">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="22a5f-126">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="22a5f-127">It is essentially a white list of all the BGP community values.</span><span class="sxs-lookup"><span data-stu-id="22a5f-127">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="22a5f-128">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span><span class="sxs-lookup"><span data-stu-id="22a5f-128">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="22a5f-129">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="22a5f-129">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="22a5f-130">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span><span class="sxs-lookup"><span data-stu-id="22a5f-130">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="22a5f-131">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="22a5f-131">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="22a5f-132">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span><span class="sxs-lookup"><span data-stu-id="22a5f-132">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined. Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.
> 
> 

### <a name="workflow"></a><span data-ttu-id="22a5f-135">Workflow</span><span class="sxs-lookup"><span data-stu-id="22a5f-135">Workflow</span></span>

<span data-ttu-id="22a5f-136">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span><span class="sxs-lookup"><span data-stu-id="22a5f-136">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="22a5f-137">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span><span class="sxs-lookup"><span data-stu-id="22a5f-137">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="22a5f-138">You can use the following instructions to accomplish these tasks:</span><span class="sxs-lookup"><span data-stu-id="22a5f-138">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="22a5f-139">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="22a5f-139">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="22a5f-140">The ExpressRoute circuit must be in a provisioned and enabled state.</span><span class="sxs-lookup"><span data-stu-id="22a5f-140">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="22a5f-141">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage the BGP session directly.</span><span class="sxs-lookup"><span data-stu-id="22a5f-141">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="22a5f-142">Or, have your connectivity provider provision Microsoft peering for your circuit.</span><span class="sxs-lookup"><span data-stu-id="22a5f-142">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="22a5f-143">You must create and configure a route filter.</span><span class="sxs-lookup"><span data-stu-id="22a5f-143">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="22a5f-144">Identify the services you with to consume through Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="22a5f-144">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="22a5f-145">Identify the list of BGP community values associated with the services</span><span class="sxs-lookup"><span data-stu-id="22a5f-145">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="22a5f-146">Create a rule to allow the prefix list matching the BGP community values</span><span class="sxs-lookup"><span data-stu-id="22a5f-146">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="22a5f-147">You must attach the route filter to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="22a5f-147">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="22a5f-148">Before you begin</span><span class="sxs-lookup"><span data-stu-id="22a5f-148">Before you begin</span></span>

<span data-ttu-id="22a5f-149">Before you begin configuration, make sure you meet the following criteria:</span><span class="sxs-lookup"><span data-stu-id="22a5f-149">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="22a5f-150">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="22a5f-150">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="22a5f-151">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="22a5f-151">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="22a5f-152">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="22a5f-152">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="22a5f-153">The ExpressRoute circuit must be in a provisioned and enabled state.</span><span class="sxs-lookup"><span data-stu-id="22a5f-153">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="22a5f-154">You must have an active Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="22a5f-154">You must have an active Microsoft peering.</span></span> <span data-ttu-id="22a5f-155">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="22a5f-155">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <a name="prefixes"></a><span data-ttu-id="22a5f-156">Step 1: Get a list of prefixes and BGP community values</span><span class="sxs-lookup"><span data-stu-id="22a5f-156">Step 1: Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="22a5f-157">1. Get a list of BGP community values</span><span class="sxs-lookup"><span data-stu-id="22a5f-157">1. Get a list of BGP community values</span></span>

<span data-ttu-id="22a5f-158">BGP community values associated with services accessible through Microsoft peering is available in the [ExpressRoute routing requirements](expressroute-routing.md) page.</span><span class="sxs-lookup"><span data-stu-id="22a5f-158">BGP community values associated with services accessible through Microsoft peering is available in the [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="22a5f-159">2. Make a list of the values that you want to use</span><span class="sxs-lookup"><span data-stu-id="22a5f-159">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="22a5f-160">Make a list of BGP community values you want to use in the route filter.</span><span class="sxs-lookup"><span data-stu-id="22a5f-160">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="22a5f-161">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="22a5f-161">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <a name="filter"></a><span data-ttu-id="22a5f-162">Step 2: Create a route filter and a filter rule</span><span class="sxs-lookup"><span data-stu-id="22a5f-162">Step 2: Create a route filter and a filter rule</span></span>

<span data-ttu-id="22a5f-163">A route filter can have only one rule, and the rule must be of type 'Allow'.</span><span class="sxs-lookup"><span data-stu-id="22a5f-163">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="22a5f-164">This rule can have a list of BGP community values associated with it.</span><span class="sxs-lookup"><span data-stu-id="22a5f-164">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="22a5f-165">1. Create a route filter</span><span class="sxs-lookup"><span data-stu-id="22a5f-165">1. Create a route filter</span></span>
<span data-ttu-id="22a5f-166">You can create a route filter by selecting the option to create a new resource.</span><span class="sxs-lookup"><span data-stu-id="22a5f-166">You can create a route filter by selecting the option to create a new resource.</span></span> <span data-ttu-id="22a5f-167">Click **Create a resource** > **Networking** > **RouteFilter**, as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="22a5f-167">Click **Create a resource** > **Networking** > **RouteFilter**, as shown in the following image:</span></span>

![Create a route filter](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="22a5f-169">You must place the route filter in a resource group.</span><span class="sxs-lookup"><span data-stu-id="22a5f-169">You must place the route filter in a resource group.</span></span> 

![Create a route filter](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="22a5f-171">2. Create a filter rule</span><span class="sxs-lookup"><span data-stu-id="22a5f-171">2. Create a filter rule</span></span>

<span data-ttu-id="22a5f-172">You can add and update rules by selecting the manage rule tab for your route filter.</span><span class="sxs-lookup"><span data-stu-id="22a5f-172">You can add and update rules by selecting the manage rule tab for your route filter.</span></span>

![Create a route filter](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="22a5f-174">You can select the services you want to connect to from the drop down list and save the rule when done.</span><span class="sxs-lookup"><span data-stu-id="22a5f-174">You can select the services you want to connect to from the drop down list and save the rule when done.</span></span>

![Create a route filter](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a><span data-ttu-id="22a5f-176">Step 3: Attach the route filter to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="22a5f-176">Step 3: Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="22a5f-177">You can attach the route filter to a circuit by selecting the "add Circuit" button and selecting the ExpressRoute circuit from the drop down list.</span><span class="sxs-lookup"><span data-stu-id="22a5f-177">You can attach the route filter to a circuit by selecting the "add Circuit" button and selecting the ExpressRoute circuit from the drop down list.</span></span>

![Create a route filter](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

<span data-ttu-id="22a5f-179">If the connectivity provider configures peering for your ExpressRoute circuit refresh the circuit from the ExpressRoute circuit blade before you select the "add Circuit" button.</span><span class="sxs-lookup"><span data-stu-id="22a5f-179">If the connectivity provider configures peering for your ExpressRoute circuit refresh the circuit from the ExpressRoute circuit blade before you select the "add Circuit" button.</span></span>

![Create a route filter](.\media\how-to-routefilter-portal\RefreshExpressRouteCircuit.png)

## <a name="tasks"></a><span data-ttu-id="22a5f-181">Common tasks</span><span class="sxs-lookup"><span data-stu-id="22a5f-181">Common tasks</span></span>

### <a name="getproperties"></a><span data-ttu-id="22a5f-182">To get the properties of a route filter</span><span class="sxs-lookup"><span data-stu-id="22a5f-182">To get the properties of a route filter</span></span>

<span data-ttu-id="22a5f-183">You can view properties of a route filter when you open the resource in the portal.</span><span class="sxs-lookup"><span data-stu-id="22a5f-183">You can view properties of a route filter when you open the resource in the portal.</span></span>

![Create a route filter](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


### <a name="updateproperties"></a><span data-ttu-id="22a5f-185">To update the properties of a route filter</span><span class="sxs-lookup"><span data-stu-id="22a5f-185">To update the properties of a route filter</span></span>

<span data-ttu-id="22a5f-186">You can update the list of BGP community values attached to a circuit by selecting the "Manage rule" button.</span><span class="sxs-lookup"><span data-stu-id="22a5f-186">You can update the list of BGP community values attached to a circuit by selecting the "Manage rule" button.</span></span>


![Create a route filter](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Create a route filter](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


### <a name="detach"></a><span data-ttu-id="22a5f-189">To detach a route filter from an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="22a5f-189">To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="22a5f-190">To detach a circuit from the route filter, right click on the circuit and click on "disassociate".</span><span class="sxs-lookup"><span data-stu-id="22a5f-190">To detach a circuit from the route filter, right click on the circuit and click on "disassociate".</span></span>

![Create a route filter](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


### <a name="delete"></a><span data-ttu-id="22a5f-192">To delete a route filter</span><span class="sxs-lookup"><span data-stu-id="22a5f-192">To delete a route filter</span></span>

<span data-ttu-id="22a5f-193">You can delete a route filter by selecting the delete button.</span><span class="sxs-lookup"><span data-stu-id="22a5f-193">You can delete a route filter by selecting the delete button.</span></span> 

![Create a route filter](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="22a5f-195">Next Steps</span><span class="sxs-lookup"><span data-stu-id="22a5f-195">Next Steps</span></span>

<span data-ttu-id="22a5f-196">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="22a5f-196">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>