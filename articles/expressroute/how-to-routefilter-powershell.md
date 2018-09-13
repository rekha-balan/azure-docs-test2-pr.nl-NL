---
title: 'Configure route filters for Azure ExpressRoute Microsoft peering: PowerShell | Microsoft Docs'
description: This article describes how to configure route filters for Microsoft Peering using PowerShell
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
ms.openlocfilehash: 6e767166ecf248aa0e7fc16dc21361394e03107d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868562"
---
# <a name="configure-route-filters-for-microsoft-peering-powershell"></a><span data-ttu-id="20339-103">Configure route filters for Microsoft peering: PowerShell</span><span class="sxs-lookup"><span data-stu-id="20339-103">Configure route filters for Microsoft peering: PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](how-to-routefilter-portal.md)
> * [Azure PowerShell](how-to-routefilter-powershell.md)
> * [Azure CLI](how-to-routefilter-cli.md)
> 

<span data-ttu-id="20339-107">Route filters are a way to consume a subset of supported services through Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="20339-107">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="20339-108">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span><span class="sxs-lookup"><span data-stu-id="20339-108">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="20339-109">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, and Azure public services, such as storage and SQL DB are accessible through Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="20339-109">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, and Azure public services, such as storage and SQL DB are accessible through Microsoft peering.</span></span> <span data-ttu-id="20339-110">Azure public services are selectable on a per region basis and cannot be defined per public service.</span><span class="sxs-lookup"><span data-stu-id="20339-110">Azure public services are selectable on a per region basis and cannot be defined per public service.</span></span> 

<span data-ttu-id="20339-111">When Microsoft peering is configured on an ExpressRoute circuit and a route filter is attached, all prefixes that are selected for these services are advertised through the BGP sessions that are established.</span><span class="sxs-lookup"><span data-stu-id="20339-111">When Microsoft peering is configured on an ExpressRoute circuit and a route filter is attached, all prefixes that are selected for these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="20339-112">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span><span class="sxs-lookup"><span data-stu-id="20339-112">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="20339-113">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="20339-113">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="20339-114">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span><span class="sxs-lookup"><span data-stu-id="20339-114">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="20339-115">This significantly increases the size of the route tables maintained by routers within your network.</span><span class="sxs-lookup"><span data-stu-id="20339-115">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="20339-116">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span><span class="sxs-lookup"><span data-stu-id="20339-116">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="20339-117">You can:</span><span class="sxs-lookup"><span data-stu-id="20339-117">You can:</span></span>

- <span data-ttu-id="20339-118">Filter out unwanted prefixes by applying route filters on BGP communities.</span><span class="sxs-lookup"><span data-stu-id="20339-118">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="20339-119">This is a standard networking practice and is used commonly within many networks.</span><span class="sxs-lookup"><span data-stu-id="20339-119">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="20339-120">Define route filters and apply them to your ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="20339-120">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="20339-121">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="20339-121">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="20339-122">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span><span class="sxs-lookup"><span data-stu-id="20339-122">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <a name="about"></a><span data-ttu-id="20339-123">About route filters</span><span class="sxs-lookup"><span data-stu-id="20339-123">About route filters</span></span>

<span data-ttu-id="20339-124">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span><span class="sxs-lookup"><span data-stu-id="20339-124">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="20339-125">No routes are advertised to your network.</span><span class="sxs-lookup"><span data-stu-id="20339-125">No routes are advertised to your network.</span></span> <span data-ttu-id="20339-126">To enable route advertisements to your network, you must associate a route filter.</span><span class="sxs-lookup"><span data-stu-id="20339-126">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="20339-127">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="20339-127">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="20339-128">It is essentially a white list of all the BGP community values.</span><span class="sxs-lookup"><span data-stu-id="20339-128">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="20339-129">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span><span class="sxs-lookup"><span data-stu-id="20339-129">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="20339-130">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="20339-130">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="20339-131">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span><span class="sxs-lookup"><span data-stu-id="20339-131">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="20339-132">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="20339-132">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="20339-133">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span><span class="sxs-lookup"><span data-stu-id="20339-133">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined. Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.
> 
> 

### <a name="workflow"></a><span data-ttu-id="20339-136">Workflow</span><span class="sxs-lookup"><span data-stu-id="20339-136">Workflow</span></span>

<span data-ttu-id="20339-137">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span><span class="sxs-lookup"><span data-stu-id="20339-137">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="20339-138">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span><span class="sxs-lookup"><span data-stu-id="20339-138">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="20339-139">You can use the following instructions to accomplish these tasks:</span><span class="sxs-lookup"><span data-stu-id="20339-139">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="20339-140">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="20339-140">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="20339-141">The ExpressRoute circuit must be in a provisioned and enabled state.</span><span class="sxs-lookup"><span data-stu-id="20339-141">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="20339-142">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage the BGP session directly.</span><span class="sxs-lookup"><span data-stu-id="20339-142">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="20339-143">Or, have your connectivity provider provision Microsoft peering for your circuit.</span><span class="sxs-lookup"><span data-stu-id="20339-143">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="20339-144">You must create and configure a route filter.</span><span class="sxs-lookup"><span data-stu-id="20339-144">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="20339-145">Identify the services you with to consume through Microsoft peering</span><span class="sxs-lookup"><span data-stu-id="20339-145">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="20339-146">Identify the list of BGP community values associated with the services</span><span class="sxs-lookup"><span data-stu-id="20339-146">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="20339-147">Create a rule to allow the prefix list matching the BGP community values</span><span class="sxs-lookup"><span data-stu-id="20339-147">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="20339-148">You must attach the route filter to the ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="20339-148">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="20339-149">Before you begin</span><span class="sxs-lookup"><span data-stu-id="20339-149">Before you begin</span></span>

<span data-ttu-id="20339-150">Before you begin configuration, make sure you meet the following criteria:</span><span class="sxs-lookup"><span data-stu-id="20339-150">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="20339-151">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="20339-151">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="20339-152">For more information, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="20339-152">For more information, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > Download the latest version from the PowerShell Gallery, rather than using the Installer. The Installer currently does not support the required cmdlets.
  > 

 - <span data-ttu-id="20339-155">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span><span class="sxs-lookup"><span data-stu-id="20339-155">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="20339-156">You must have an active ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="20339-156">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="20339-157">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span><span class="sxs-lookup"><span data-stu-id="20339-157">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="20339-158">The ExpressRoute circuit must be in a provisioned and enabled state.</span><span class="sxs-lookup"><span data-stu-id="20339-158">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="20339-159">You must have an active Microsoft peering.</span><span class="sxs-lookup"><span data-stu-id="20339-159">You must have an active Microsoft peering.</span></span> <span data-ttu-id="20339-160">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="20339-160">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-to-your-azure-account"></a><span data-ttu-id="20339-161">Log in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="20339-161">Log in to your Azure account</span></span>

<span data-ttu-id="20339-162">Before beginning this configuration, you must log in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="20339-162">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="20339-163">The cmdlet prompts you for the login credentials for your Azure account.</span><span class="sxs-lookup"><span data-stu-id="20339-163">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="20339-164">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20339-164">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="20339-165">Open your PowerShell console with elevated privileges, and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="20339-165">Open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="20339-166">Use the following example to help you connect:</span><span class="sxs-lookup"><span data-stu-id="20339-166">Use the following example to help you connect:</span></span>

```powershell
Connect-AzureRmAccount
```

<span data-ttu-id="20339-167">If you have multiple Azure subscriptions, check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="20339-167">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="20339-168">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="20339-168">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a><span data-ttu-id="20339-169">Step 1: Get a list of prefixes and BGP community values</span><span class="sxs-lookup"><span data-stu-id="20339-169">Step 1: Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="20339-170">1. Get a list of BGP community values</span><span class="sxs-lookup"><span data-stu-id="20339-170">1. Get a list of BGP community values</span></span>

<span data-ttu-id="20339-171">Use the following cmdlet to get the list of BGP community values associated with services accessible through Microsoft peering, and the list of prefixes associated with them:</span><span class="sxs-lookup"><span data-stu-id="20339-171">Use the following cmdlet to get the list of BGP community values associated with services accessible through Microsoft peering, and the list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="20339-172">2. Make a list of the values that you want to use</span><span class="sxs-lookup"><span data-stu-id="20339-172">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="20339-173">Make a list of BGP community values you want to use in the route filter.</span><span class="sxs-lookup"><span data-stu-id="20339-173">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="20339-174">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="20339-174">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <a name="filter"></a><span data-ttu-id="20339-175">Step 2: Create a route filter and a filter rule</span><span class="sxs-lookup"><span data-stu-id="20339-175">Step 2: Create a route filter and a filter rule</span></span>

<span data-ttu-id="20339-176">A route filter can have only one rule, and the rule must be of type 'Allow'.</span><span class="sxs-lookup"><span data-stu-id="20339-176">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="20339-177">This rule can have a list of BGP community values associated with it.</span><span class="sxs-lookup"><span data-stu-id="20339-177">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="20339-178">1. Create a route filter</span><span class="sxs-lookup"><span data-stu-id="20339-178">1. Create a route filter</span></span>

<span data-ttu-id="20339-179">First, create the route filter.</span><span class="sxs-lookup"><span data-stu-id="20339-179">First, create the route filter.</span></span> <span data-ttu-id="20339-180">The command 'New-AzureRmRouteFilter' only creates a route filter resource.</span><span class="sxs-lookup"><span data-stu-id="20339-180">The command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="20339-181">After you create the resource, you must then create a rule and attach it to the route filter object.</span><span class="sxs-lookup"><span data-stu-id="20339-181">After you create the resource, you must then create a rule and attach it to the route filter object.</span></span> <span data-ttu-id="20339-182">Run the following command to create a route filter resource:</span><span class="sxs-lookup"><span data-stu-id="20339-182">Run the following command to create a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="20339-183">2. Create a filter rule</span><span class="sxs-lookup"><span data-stu-id="20339-183">2. Create a filter rule</span></span>

<span data-ttu-id="20339-184">You can specify a set of BGP communities as a comma-separated list, as shown in the example.</span><span class="sxs-lookup"><span data-stu-id="20339-184">You can specify a set of BGP communities as a comma-separated list, as shown in the example.</span></span> <span data-ttu-id="20339-185">Run the following command to create a new rule:</span><span class="sxs-lookup"><span data-stu-id="20339-185">Run the following command to create a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-the-rule-to-the-route-filter"></a><span data-ttu-id="20339-186">3. Add the rule to the route filter</span><span class="sxs-lookup"><span data-stu-id="20339-186">3. Add the rule to the route filter</span></span>

<span data-ttu-id="20339-187">Run the following command to add the filter rule to the route filter:</span><span class="sxs-lookup"><span data-stu-id="20339-187">Run the following command to add the filter rule to the route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a><span data-ttu-id="20339-188">Step 3: Attach the route filter to an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="20339-188">Step 3: Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="20339-189">Run the following command to attach the route filter to the ExpressRoute circuit, assuming you have only Microsoft peering:</span><span class="sxs-lookup"><span data-stu-id="20339-189">Run the following command to attach the route filter to the ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="tasks"></a><span data-ttu-id="20339-190">Common tasks</span><span class="sxs-lookup"><span data-stu-id="20339-190">Common tasks</span></span>

### <a name="getproperties"></a><span data-ttu-id="20339-191">To get the properties of a route filter</span><span class="sxs-lookup"><span data-stu-id="20339-191">To get the properties of a route filter</span></span>

<span data-ttu-id="20339-192">To get the properties of a route filter, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="20339-192">To get the properties of a route filter, use the following steps:</span></span>

1. <span data-ttu-id="20339-193">Run the following command to get the route filter resource:</span><span class="sxs-lookup"><span data-stu-id="20339-193">Run the following command to get the route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="20339-194">Get the route filter rules for the route-filter resource by running the following command:</span><span class="sxs-lookup"><span data-stu-id="20339-194">Get the route filter rules for the route-filter resource by running the following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

### <a name="updateproperties"></a><span data-ttu-id="20339-195">To update the properties of a route filter</span><span class="sxs-lookup"><span data-stu-id="20339-195">To update the properties of a route filter</span></span>

<span data-ttu-id="20339-196">If the route filter is already attached to a circuit, updates to the BGP community list automatically propagate appropriate prefix advertisement changes through the established BGP sessions.</span><span class="sxs-lookup"><span data-stu-id="20339-196">If the route filter is already attached to a circuit, updates to the BGP community list automatically propagate appropriate prefix advertisement changes through the established BGP sessions.</span></span> <span data-ttu-id="20339-197">You can update the BGP community list of your route filter using the following command:</span><span class="sxs-lookup"><span data-stu-id="20339-197">You can update the BGP community list of your route filter using the following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

### <a name="detach"></a><span data-ttu-id="20339-198">To detach a route filter from an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="20339-198">To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="20339-199">Once a route filter is detached from the ExpressRoute circuit, no prefixes are advertised through the BGP session.</span><span class="sxs-lookup"><span data-stu-id="20339-199">Once a route filter is detached from the ExpressRoute circuit, no prefixes are advertised through the BGP session.</span></span> <span data-ttu-id="20339-200">You can detach a route filter from an ExpressRoute circuit using the following command:</span><span class="sxs-lookup"><span data-stu-id="20339-200">You can detach a route filter from an ExpressRoute circuit using the following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="delete"></a><span data-ttu-id="20339-201">To delete a route filter</span><span class="sxs-lookup"><span data-stu-id="20339-201">To delete a route filter</span></span>

<span data-ttu-id="20339-202">You can only delete a route filter if it is not attached to any circuit.</span><span class="sxs-lookup"><span data-stu-id="20339-202">You can only delete a route filter if it is not attached to any circuit.</span></span> <span data-ttu-id="20339-203">Ensure that the route filter is not attached to any circuit before attempting to delete it.</span><span class="sxs-lookup"><span data-stu-id="20339-203">Ensure that the route filter is not attached to any circuit before attempting to delete it.</span></span> <span data-ttu-id="20339-204">You can delete a route filter using the following command:</span><span class="sxs-lookup"><span data-stu-id="20339-204">You can delete a route filter using the following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="20339-205">Next Steps</span><span class="sxs-lookup"><span data-stu-id="20339-205">Next Steps</span></span>

<span data-ttu-id="20339-206">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="20339-206">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
