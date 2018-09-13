---
title: Using PowerShell to manage Traffic Manager in Azure | Microsoft Docs
description: Using PowerShell for Traffic Manager with Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 951e845e23a1ed0cbdc83fc24a97a545f00c52ad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824361"
---
# <a name="using-powershell-to-manage-traffic-manager"></a><span data-ttu-id="8a40c-103">Using PowerShell to manage Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8a40c-103">Using PowerShell to manage Traffic Manager</span></span>

<span data-ttu-id="8a40c-104">Azure Resource Manager is the preferred management interface for services in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a40c-104">Azure Resource Manager is the preferred management interface for services in Azure.</span></span> <span data-ttu-id="8a40c-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span><span class="sxs-lookup"><span data-stu-id="8a40c-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="8a40c-106">Resource model</span><span class="sxs-lookup"><span data-stu-id="8a40c-106">Resource model</span></span>

<span data-ttu-id="8a40c-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="8a40c-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints to which traffic is routed.</span><span class="sxs-lookup"><span data-stu-id="8a40c-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints to which traffic is routed.</span></span>

<span data-ttu-id="8a40c-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span><span class="sxs-lookup"><span data-stu-id="8a40c-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="8a40c-110">At the REST API level, the URI for each profile is as follows:</span><span class="sxs-lookup"><span data-stu-id="8a40c-110">At the REST API level, the URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="8a40c-111">Setting up Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a40c-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="8a40c-112">These instructions use Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a40c-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="8a40c-113">The following article explains how to install and configure Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a40c-113">The following article explains how to install and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="8a40c-114">How to install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a40c-114">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="8a40c-115">The examples in this article assume that you have an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="8a40c-115">The examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="8a40c-116">You can create a resource group using the following command:</span><span class="sxs-lookup"><span data-stu-id="8a40c-116">You can create a resource group using the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="8a40c-117">Azure Resource Manager requires that all resource groups have a location.</span><span class="sxs-lookup"><span data-stu-id="8a40c-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="8a40c-118">This location is used as the default for resources created in that resource group.</span><span class="sxs-lookup"><span data-stu-id="8a40c-118">This location is used as the default for resources created in that resource group.</span></span> <span data-ttu-id="8a40c-119">However, since Traffic Manager profile resources are global, not regional, the choice of resource group location has no impact on Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="8a40c-119">However, since Traffic Manager profile resources are global, not regional, the choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="8a40c-120">Create a Traffic Manager Profile</span><span class="sxs-lookup"><span data-stu-id="8a40c-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="8a40c-121">To create a Traffic Manager profile, use the `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8a40c-121">To create a Traffic Manager profile, use the `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="8a40c-122">The following table describes the parameters:</span><span class="sxs-lookup"><span data-stu-id="8a40c-122">The following table describes the parameters:</span></span>

| <span data-ttu-id="8a40c-123">Parameter</span><span class="sxs-lookup"><span data-stu-id="8a40c-123">Parameter</span></span> | <span data-ttu-id="8a40c-124">Description</span><span class="sxs-lookup"><span data-stu-id="8a40c-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a40c-125">Name</span><span class="sxs-lookup"><span data-stu-id="8a40c-125">Name</span></span> |<span data-ttu-id="8a40c-126">The resource name for the Traffic Manager profile resource.</span><span class="sxs-lookup"><span data-stu-id="8a40c-126">The resource name for the Traffic Manager profile resource.</span></span> <span data-ttu-id="8a40c-127">Profiles in the same resource group must have unique names.</span><span class="sxs-lookup"><span data-stu-id="8a40c-127">Profiles in the same resource group must have unique names.</span></span> <span data-ttu-id="8a40c-128">This name is separate from the DNS name used for DNS queries.</span><span class="sxs-lookup"><span data-stu-id="8a40c-128">This name is separate from the DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="8a40c-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8a40c-129">ResourceGroupName</span></span> |<span data-ttu-id="8a40c-130">The name of the resource group containing the profile resource.</span><span class="sxs-lookup"><span data-stu-id="8a40c-130">The name of the resource group containing the profile resource.</span></span> |
| <span data-ttu-id="8a40c-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="8a40c-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="8a40c-132">Specifies the traffic-routing method used to determine which endpoint is returned in response a DNS query.</span><span class="sxs-lookup"><span data-stu-id="8a40c-132">Specifies the traffic-routing method used to determine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="8a40c-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span><span class="sxs-lookup"><span data-stu-id="8a40c-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="8a40c-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="8a40c-134">RelativeDnsName</span></span> |<span data-ttu-id="8a40c-135">Specifies the hostname portion of the DNS name provided by this Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-135">Specifies the hostname portion of the DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="8a40c-136">This value is combined with the DNS domain name used by Azure Traffic Manager to form the fully qualified domain name (FQDN) of the profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-136">This value is combined with the DNS domain name used by Azure Traffic Manager to form the fully qualified domain name (FQDN) of the profile.</span></span> <span data-ttu-id="8a40c-137">For example, setting the value of 'contoso' becomes 'contoso.trafficmanager.net.'</span><span class="sxs-lookup"><span data-stu-id="8a40c-137">For example, setting the value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="8a40c-138">TTL</span><span class="sxs-lookup"><span data-stu-id="8a40c-138">TTL</span></span> |<span data-ttu-id="8a40c-139">Specifies the DNS Time-to-Live (TTL), in seconds.</span><span class="sxs-lookup"><span data-stu-id="8a40c-139">Specifies the DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="8a40c-140">This TTL informs the Local DNS resolvers and DNS clients how long to cache DNS responses for this Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-140">This TTL informs the Local DNS resolvers and DNS clients how long to cache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="8a40c-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="8a40c-141">MonitorProtocol</span></span> |<span data-ttu-id="8a40c-142">Specifies the protocol to use to monitor endpoint health.</span><span class="sxs-lookup"><span data-stu-id="8a40c-142">Specifies the protocol to use to monitor endpoint health.</span></span> <span data-ttu-id="8a40c-143">Possible values are 'HTTP' and 'HTTPS'.</span><span class="sxs-lookup"><span data-stu-id="8a40c-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="8a40c-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="8a40c-144">MonitorPort</span></span> |<span data-ttu-id="8a40c-145">Specifies the TCP port used to monitor endpoint health.</span><span class="sxs-lookup"><span data-stu-id="8a40c-145">Specifies the TCP port used to monitor endpoint health.</span></span> |
| <span data-ttu-id="8a40c-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="8a40c-146">MonitorPath</span></span> |<span data-ttu-id="8a40c-147">Specifies the path relative to the endpoint domain name used to probe for endpoint health.</span><span class="sxs-lookup"><span data-stu-id="8a40c-147">Specifies the path relative to the endpoint domain name used to probe for endpoint health.</span></span> |

<span data-ttu-id="8a40c-148">The cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object to PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a40c-148">The cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object to PowerShell.</span></span> <span data-ttu-id="8a40c-149">At this point, the profile does not contain any endpoints.</span><span class="sxs-lookup"><span data-stu-id="8a40c-149">At this point, the profile does not contain any endpoints.</span></span> <span data-ttu-id="8a40c-150">For more information about adding endpoints to a Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="8a40c-150">For more information about adding endpoints to a Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="8a40c-151">Get a Traffic Manager Profile</span><span class="sxs-lookup"><span data-stu-id="8a40c-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="8a40c-152">To retrieve an existing Traffic Manager profile object, use the `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8a40c-152">To retrieve an existing Traffic Manager profile object, use the `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="8a40c-153">This cmdlet returns a Traffic Manager profile object.</span><span class="sxs-lookup"><span data-stu-id="8a40c-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="8a40c-154">Update a Traffic Manager Profile</span><span class="sxs-lookup"><span data-stu-id="8a40c-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="8a40c-155">Modifying Traffic Manager profiles follows a 3-step process:</span><span class="sxs-lookup"><span data-stu-id="8a40c-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="8a40c-156">Retrieve the profile using `Get-AzureRmTrafficManagerProfile` or use the profile returned by `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="8a40c-156">Retrieve the profile using `Get-AzureRmTrafficManagerProfile` or use the profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="8a40c-157">Modify the profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-157">Modify the profile.</span></span> <span data-ttu-id="8a40c-158">You can add and remove endpoints or change endpoint or profile parameters.</span><span class="sxs-lookup"><span data-stu-id="8a40c-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="8a40c-159">These changes are off-line operations.</span><span class="sxs-lookup"><span data-stu-id="8a40c-159">These changes are off-line operations.</span></span> <span data-ttu-id="8a40c-160">You are only changing the local object in memory that represents the profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-160">You are only changing the local object in memory that represents the profile.</span></span>
3. <span data-ttu-id="8a40c-161">Commit your changes using the `Set-AzureRmTrafficManagerProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a40c-161">Commit your changes using the `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="8a40c-162">All profile properties can be changed except the profile's RelativeDnsName.</span><span class="sxs-lookup"><span data-stu-id="8a40c-162">All profile properties can be changed except the profile's RelativeDnsName.</span></span> <span data-ttu-id="8a40c-163">To change the RelativeDnsName, you must delete profile and a new profile with a new name.</span><span class="sxs-lookup"><span data-stu-id="8a40c-163">To change the RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="8a40c-164">The following example demonstrates how to change the profile's TTL:</span><span class="sxs-lookup"><span data-stu-id="8a40c-164">The following example demonstrates how to change the profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="8a40c-165">There are three types of Traffic Manager endpoints:</span><span class="sxs-lookup"><span data-stu-id="8a40c-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="8a40c-166">**Azure endpoints** are services hosted in Azure</span><span class="sxs-lookup"><span data-stu-id="8a40c-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="8a40c-167">**External endpoints** are services hosted outside of Azure</span><span class="sxs-lookup"><span data-stu-id="8a40c-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="8a40c-168">**Nested endpoints** are used to construct nested hierarchies of Traffic Manager profiles.</span><span class="sxs-lookup"><span data-stu-id="8a40c-168">**Nested endpoints** are used to construct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="8a40c-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span><span class="sxs-lookup"><span data-stu-id="8a40c-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="8a40c-170">In all three cases, endpoints can be added in two ways:</span><span class="sxs-lookup"><span data-stu-id="8a40c-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="8a40c-171">Using a 3-step process described previously.</span><span class="sxs-lookup"><span data-stu-id="8a40c-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="8a40c-172">The advantage of this method is that several endpoint changes can be made in a single update.</span><span class="sxs-lookup"><span data-stu-id="8a40c-172">The advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="8a40c-173">Using the New-AzureRmTrafficManagerEndpoint cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a40c-173">Using the New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="8a40c-174">This cmdlet adds an endpoint to an existing Traffic Manager profile in a single operation.</span><span class="sxs-lookup"><span data-stu-id="8a40c-174">This cmdlet adds an endpoint to an existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="8a40c-175">Adding Azure Endpoints</span><span class="sxs-lookup"><span data-stu-id="8a40c-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="8a40c-176">Azure endpoints reference services hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a40c-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="8a40c-177">Two types of Azure endpoints are supported:</span><span class="sxs-lookup"><span data-stu-id="8a40c-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="8a40c-178">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="8a40c-178">Azure Web Apps</span></span>
2. <span data-ttu-id="8a40c-179">Azure PublicIpAddress resources (which can be attached to a load-balancer or a virtual machine NIC).</span><span class="sxs-lookup"><span data-stu-id="8a40c-179">Azure PublicIpAddress resources (which can be attached to a load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="8a40c-180">The PublicIpAddress must have a DNS name assigned to be used in Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="8a40c-180">The PublicIpAddress must have a DNS name assigned to be used in Traffic Manager.</span></span>

<span data-ttu-id="8a40c-181">In each case:</span><span class="sxs-lookup"><span data-stu-id="8a40c-181">In each case:</span></span>

* <span data-ttu-id="8a40c-182">The service is specified using the 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="8a40c-182">The service is specified using the 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="8a40c-183">The 'Target' and 'EndpointLocation' are implied by the TargetResourceId.</span><span class="sxs-lookup"><span data-stu-id="8a40c-183">The 'Target' and 'EndpointLocation' are implied by the TargetResourceId.</span></span>
* <span data-ttu-id="8a40c-184">Specifying the 'Weight' is optional.</span><span class="sxs-lookup"><span data-stu-id="8a40c-184">Specifying the 'Weight' is optional.</span></span> <span data-ttu-id="8a40c-185">Weights are only used if the profile is configured to use the 'Weighted' traffic-routing method.</span><span class="sxs-lookup"><span data-stu-id="8a40c-185">Weights are only used if the profile is configured to use the 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="8a40c-186">Otherwise, they are ignored.</span><span class="sxs-lookup"><span data-stu-id="8a40c-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="8a40c-187">If specified, the value must be a number between 1 and 1000.</span><span class="sxs-lookup"><span data-stu-id="8a40c-187">If specified, the value must be a number between 1 and 1000.</span></span> <span data-ttu-id="8a40c-188">The default value is '1'.</span><span class="sxs-lookup"><span data-stu-id="8a40c-188">The default value is '1'.</span></span>
* <span data-ttu-id="8a40c-189">Specifying the 'Priority' is optional.</span><span class="sxs-lookup"><span data-stu-id="8a40c-189">Specifying the 'Priority' is optional.</span></span> <span data-ttu-id="8a40c-190">Priorities are only used if the profile is configured to use the 'Priority' traffic-routing method.</span><span class="sxs-lookup"><span data-stu-id="8a40c-190">Priorities are only used if the profile is configured to use the 'Priority' traffic-routing method.</span></span> <span data-ttu-id="8a40c-191">Otherwise, they are ignored.</span><span class="sxs-lookup"><span data-stu-id="8a40c-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="8a40c-192">Valid values are from 1 to 1000 with lower values indicating a higher priority.</span><span class="sxs-lookup"><span data-stu-id="8a40c-192">Valid values are from 1 to 1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="8a40c-193">If specified for one endpoint, they must be specified for all endpoints.</span><span class="sxs-lookup"><span data-stu-id="8a40c-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="8a40c-194">If omitted, default values starting from '1' are applied in the order that the endpoints are listed.</span><span class="sxs-lookup"><span data-stu-id="8a40c-194">If omitted, default values starting from '1' are applied in the order that the endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="8a40c-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="8a40c-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="8a40c-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using the `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a40c-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using the `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="8a40c-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="8a40c-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="8a40c-198">In this example, a public IP address resource is added to the Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-198">In this example, a public IP address resource is added to the Traffic Manager profile.</span></span> <span data-ttu-id="8a40c-199">The public IP address must have a DNS name configured, and can be bound either to the NIC of a VM or to a load balancer.</span><span class="sxs-lookup"><span data-stu-id="8a40c-199">The public IP address must have a DNS name configured, and can be bound either to the NIC of a VM or to a load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="8a40c-200">Adding External Endpoints</span><span class="sxs-lookup"><span data-stu-id="8a40c-200">Adding External Endpoints</span></span>

<span data-ttu-id="8a40c-201">Traffic Manager uses external endpoints to direct traffic to services hosted outside of Azure.</span><span class="sxs-lookup"><span data-stu-id="8a40c-201">Traffic Manager uses external endpoints to direct traffic to services hosted outside of Azure.</span></span> <span data-ttu-id="8a40c-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="8a40c-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="8a40c-203">When specifying external endpoints:</span><span class="sxs-lookup"><span data-stu-id="8a40c-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="8a40c-204">The endpoint domain name must be specified using the 'Target' parameter</span><span class="sxs-lookup"><span data-stu-id="8a40c-204">The endpoint domain name must be specified using the 'Target' parameter</span></span>
* <span data-ttu-id="8a40c-205">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span><span class="sxs-lookup"><span data-stu-id="8a40c-205">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span></span> <span data-ttu-id="8a40c-206">Otherwise it is optional.</span><span class="sxs-lookup"><span data-stu-id="8a40c-206">Otherwise it is optional.</span></span> <span data-ttu-id="8a40c-207">The value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="8a40c-207">The value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="8a40c-208">The 'Weight' and 'Priority' are optional.</span><span class="sxs-lookup"><span data-stu-id="8a40c-208">The 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="8a40c-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="8a40c-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="8a40c-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit the changes.</span><span class="sxs-lookup"><span data-stu-id="8a40c-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit the changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="8a40c-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="8a40c-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="8a40c-212">In this example, we add an external endpoint to an existing profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-212">In this example, we add an external endpoint to an existing profile.</span></span> <span data-ttu-id="8a40c-213">The profile is specified using the profile and resource group names.</span><span class="sxs-lookup"><span data-stu-id="8a40c-213">The profile is specified using the profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="8a40c-214">Adding 'Nested' endpoints</span><span class="sxs-lookup"><span data-stu-id="8a40c-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="8a40c-215">Each Traffic Manager profile specifies a single traffic-routing method.</span><span class="sxs-lookup"><span data-stu-id="8a40c-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="8a40c-216">However, there are scenarios that require more sophisticated traffic routing than the routing provided by a single Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-216">However, there are scenarios that require more sophisticated traffic routing than the routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="8a40c-217">You can nest Traffic Manager profiles to combine the benefits of more than one traffic-routing method.</span><span class="sxs-lookup"><span data-stu-id="8a40c-217">You can nest Traffic Manager profiles to combine the benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="8a40c-218">Nested profiles allow you to override the default Traffic Manager behavior to support larger and more complex application deployments.</span><span class="sxs-lookup"><span data-stu-id="8a40c-218">Nested profiles allow you to override the default Traffic Manager behavior to support larger and more complex application deployments.</span></span> <span data-ttu-id="8a40c-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="8a40c-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="8a40c-220">Nested endpoints are configured at the parent profile, using a specific endpoint type, 'NestedEndpoints'.</span><span class="sxs-lookup"><span data-stu-id="8a40c-220">Nested endpoints are configured at the parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="8a40c-221">When specifying nested endpoints:</span><span class="sxs-lookup"><span data-stu-id="8a40c-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="8a40c-222">The endpoint must be specified using the 'targetResourceId' parameter</span><span class="sxs-lookup"><span data-stu-id="8a40c-222">The endpoint must be specified using the 'targetResourceId' parameter</span></span>
* <span data-ttu-id="8a40c-223">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span><span class="sxs-lookup"><span data-stu-id="8a40c-223">If the 'Performance' traffic-routing method is used, the 'EndpointLocation' is required.</span></span> <span data-ttu-id="8a40c-224">Otherwise it is optional.</span><span class="sxs-lookup"><span data-stu-id="8a40c-224">Otherwise it is optional.</span></span> <span data-ttu-id="8a40c-225">The value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="8a40c-225">The value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="8a40c-226">The 'Weight' and 'Priority' are optional, as for Azure endpoints.</span><span class="sxs-lookup"><span data-stu-id="8a40c-226">The 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="8a40c-227">The 'MinChildEndpoints' parameter is optional.</span><span class="sxs-lookup"><span data-stu-id="8a40c-227">The 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="8a40c-228">The default value is '1'.</span><span class="sxs-lookup"><span data-stu-id="8a40c-228">The default value is '1'.</span></span> <span data-ttu-id="8a40c-229">If the number of available endpoints falls below this threshold, the parent profile considers the child profile 'degraded' and diverts traffic to the other endpoints in the parent profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-229">If the number of available endpoints falls below this threshold, the parent profile considers the child profile 'degraded' and diverts traffic to the other endpoints in the parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="8a40c-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="8a40c-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="8a40c-231">In this example, we create new Traffic Manager child and parent profiles, add the child as a nested endpoint to the parent, and commit the changes.</span><span class="sxs-lookup"><span data-stu-id="8a40c-231">In this example, we create new Traffic Manager child and parent profiles, add the child as a nested endpoint to the parent, and commit the changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="8a40c-232">For brevity in this example, we did not add any other endpoints to the child or parent profiles.</span><span class="sxs-lookup"><span data-stu-id="8a40c-232">For brevity in this example, we did not add any other endpoints to the child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="8a40c-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="8a40c-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="8a40c-234">In this example, we add an existing child profile as a nested endpoint to an existing parent profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-234">In this example, we add an existing child profile as a nested endpoint to an existing parent profile.</span></span> <span data-ttu-id="8a40c-235">The profile is specified using the profile and resource group names.</span><span class="sxs-lookup"><span data-stu-id="8a40c-235">The profile is specified using the profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="adding-endpoints-from-another-subscription"></a><span data-ttu-id="8a40c-236">Adding endpoints from another subscription</span><span class="sxs-lookup"><span data-stu-id="8a40c-236">Adding endpoints from another subscription</span></span>

<span data-ttu-id="8a40c-237">Traffic Manager can work with endpoints from different subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8a40c-237">Traffic Manager can work with endpoints from different subscriptions.</span></span> <span data-ttu-id="8a40c-238">You need to switch to the subscription with the endpoint you want to add to retrieve the needed input to Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="8a40c-238">You need to switch to the subscription with the endpoint you want to add to retrieve the needed input to Traffic Manager.</span></span> <span data-ttu-id="8a40c-239">Then you need to switch to the subscriptions with the Traffic Manager profile, and add the encpoint to it.</span><span class="sxs-lookup"><span data-stu-id="8a40c-239">Then you need to switch to the subscriptions with the Traffic Manager profile, and add the encpoint to it.</span></span> <span data-ttu-id="8a40c-240">The below example shows how to do this with a public IP address.</span><span class="sxs-lookup"><span data-stu-id="8a40c-240">The below example shows how to do this with a public IP address.</span></span>

```powershell
Set-AzureRmContext -SubscriptionId $EndpointSubscription
$ip = Get-AzureRmPublicIpAddress -Name $IpAddresName -ResourceGroupName $EndpointRG

Set-AzureRmContext -SubscriptionId $trafficmanagerSubscription
New-AzureRmTrafficManagerEndpoint -Name $EndpointName -ProfileName $ProfileName -ResourceGroupName $TrafficManagerRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="8a40c-241">Update a Traffic Manager Endpoint</span><span class="sxs-lookup"><span data-stu-id="8a40c-241">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="8a40c-242">There are two ways to update an existing Traffic Manager endpoint:</span><span class="sxs-lookup"><span data-stu-id="8a40c-242">There are two ways to update an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="8a40c-243">Get the Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update the endpoint properties within the profile, and commit the changes using `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="8a40c-243">Get the Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update the endpoint properties within the profile, and commit the changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="8a40c-244">This method has the advantage of being able to update more than one endpoint in a single operation.</span><span class="sxs-lookup"><span data-stu-id="8a40c-244">This method has the advantage of being able to update more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="8a40c-245">Get the Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update the endpoint properties, and commit the changes using `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="8a40c-245">Get the Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update the endpoint properties, and commit the changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="8a40c-246">This method is simpler, since it does not require indexing into the Endpoints array in the profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-246">This method is simpler, since it does not require indexing into the Endpoints array in the profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="8a40c-247">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="8a40c-247">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="8a40c-248">In this example, we modify the priority on two endpoints within an existing profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-248">In this example, we modify the priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="8a40c-249">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="8a40c-249">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="8a40c-250">In this example, we modify the weight of a single endpoint in an existing profile.</span><span class="sxs-lookup"><span data-stu-id="8a40c-250">In this example, we modify the weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="8a40c-251">Enabling and Disabling Endpoints and Profiles</span><span class="sxs-lookup"><span data-stu-id="8a40c-251">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="8a40c-252">Traffic Manager allows individual endpoints to be enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span><span class="sxs-lookup"><span data-stu-id="8a40c-252">Traffic Manager allows individual endpoints to be enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="8a40c-253">These changes can be made by getting/updating/setting the endpoint or profile resources.</span><span class="sxs-lookup"><span data-stu-id="8a40c-253">These changes can be made by getting/updating/setting the endpoint or profile resources.</span></span> <span data-ttu-id="8a40c-254">To streamline these common operations, they are also supported via dedicated cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8a40c-254">To streamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="8a40c-255">Example 1: Enabling and disabling a Traffic Manager profile</span><span class="sxs-lookup"><span data-stu-id="8a40c-255">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="8a40c-256">To enable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="8a40c-256">To enable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="8a40c-257">The profile can be specified using a profile object.</span><span class="sxs-lookup"><span data-stu-id="8a40c-257">The profile can be specified using a profile object.</span></span> <span data-ttu-id="8a40c-258">The profile object can be passed via the pipeline or by using the '-TrafficManagerProfile' parameter.</span><span class="sxs-lookup"><span data-stu-id="8a40c-258">The profile object can be passed via the pipeline or by using the '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="8a40c-259">In this example, we specify the profile by the profile and resource group name.</span><span class="sxs-lookup"><span data-stu-id="8a40c-259">In this example, we specify the profile by the profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="8a40c-260">To disable a Traffic Manager profile:</span><span class="sxs-lookup"><span data-stu-id="8a40c-260">To disable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="8a40c-261">The Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span><span class="sxs-lookup"><span data-stu-id="8a40c-261">The Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="8a40c-262">This prompt can be suppressed using the '-Force' parameter.</span><span class="sxs-lookup"><span data-stu-id="8a40c-262">This prompt can be suppressed using the '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="8a40c-263">Example 2: Enabling and disabling a Traffic Manager endpoint</span><span class="sxs-lookup"><span data-stu-id="8a40c-263">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="8a40c-264">To enable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="8a40c-264">To enable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="8a40c-265">There are two ways to specify the endpoint</span><span class="sxs-lookup"><span data-stu-id="8a40c-265">There are two ways to specify the endpoint</span></span>

1. <span data-ttu-id="8a40c-266">Using a TrafficManagerEndpoint object passed via the pipeline or using the '-TrafficManagerEndpoint' parameter</span><span class="sxs-lookup"><span data-stu-id="8a40c-266">Using a TrafficManagerEndpoint object passed via the pipeline or using the '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="8a40c-267">Using the endpoint name, endpoint type, profile name, and resource group name:</span><span class="sxs-lookup"><span data-stu-id="8a40c-267">Using the endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="8a40c-268">Similarly, to disable a Traffic Manager endpoint:</span><span class="sxs-lookup"><span data-stu-id="8a40c-268">Similarly, to disable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="8a40c-269">As with `Disable-AzureRmTrafficManagerProfile`, the `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span><span class="sxs-lookup"><span data-stu-id="8a40c-269">As with `Disable-AzureRmTrafficManagerProfile`, the `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="8a40c-270">This prompt can be suppressed using the '-Force' parameter.</span><span class="sxs-lookup"><span data-stu-id="8a40c-270">This prompt can be suppressed using the '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="8a40c-271">Delete a Traffic Manager Endpoint</span><span class="sxs-lookup"><span data-stu-id="8a40c-271">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="8a40c-272">To remove individual endpoints, use the `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8a40c-272">To remove individual endpoints, use the `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="8a40c-273">This cmdlet prompts for confirmation.</span><span class="sxs-lookup"><span data-stu-id="8a40c-273">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="8a40c-274">This prompt can be suppressed using the '-Force' parameter.</span><span class="sxs-lookup"><span data-stu-id="8a40c-274">This prompt can be suppressed using the '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="8a40c-275">Delete a Traffic Manager Profile</span><span class="sxs-lookup"><span data-stu-id="8a40c-275">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="8a40c-276">To delete a Traffic Manager profile, use the `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying the profile and resource group names:</span><span class="sxs-lookup"><span data-stu-id="8a40c-276">To delete a Traffic Manager profile, use the `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying the profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="8a40c-277">This cmdlet prompts for confirmation.</span><span class="sxs-lookup"><span data-stu-id="8a40c-277">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="8a40c-278">This prompt can be suppressed using the '-Force' parameter.</span><span class="sxs-lookup"><span data-stu-id="8a40c-278">This prompt can be suppressed using the '-Force' parameter.</span></span>

<span data-ttu-id="8a40c-279">The profile to be deleted can also be specified using a profile object:</span><span class="sxs-lookup"><span data-stu-id="8a40c-279">The profile to be deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="8a40c-280">This sequence can also be piped:</span><span class="sxs-lookup"><span data-stu-id="8a40c-280">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="8a40c-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a40c-281">Next steps</span></span>

[<span data-ttu-id="8a40c-282">Traffic Manager monitoring</span><span class="sxs-lookup"><span data-stu-id="8a40c-282">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="8a40c-283">Traffic Manager performance considerations</span><span class="sxs-lookup"><span data-stu-id="8a40c-283">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
