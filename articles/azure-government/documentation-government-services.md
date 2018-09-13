---
title: Azure Government available services | Microsoft Docs
description: Provides an overview of the available services in Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: smichelotti
manager: liki
ms.assetid: a453a23c-bc0f-4203-9075-0f579dea7e23
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 02/13/2017
ms.author: stemi
ms.openlocfilehash: 21c2a0faad87b84058093f02c831b374a644b4b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553610"
---
# <a name="available-services-on-azure-government"></a><span data-ttu-id="40038-103">Available Services on Azure Government</span><span class="sxs-lookup"><span data-stu-id="40038-103">Available Services on Azure Government</span></span>
<span data-ttu-id="40038-104">Azure Government is continually expanding the services that are available.</span><span class="sxs-lookup"><span data-stu-id="40038-104">Azure Government is continually expanding the services that are available.</span></span>  <span data-ttu-id="40038-105">These services are deployed using the same code that is used in Azure Public.</span><span class="sxs-lookup"><span data-stu-id="40038-105">These services are deployed using the same code that is used in Azure Public.</span></span>  <span data-ttu-id="40038-106">This section documents the services that are currently available on Azure Government, including two key types of information:</span><span class="sxs-lookup"><span data-stu-id="40038-106">This section documents the services that are currently available on Azure Government, including two key types of information:</span></span>

* <span data-ttu-id="40038-107">**Variations:** Variations due to features that have not been deployed yet or properties (for example, URLs) that are unique to the government environment.</span><span class="sxs-lookup"><span data-stu-id="40038-107">**Variations:** Variations due to features that have not been deployed yet or properties (for example, URLs) that are unique to the government environment.</span></span>  
* <span data-ttu-id="40038-108">**Considerations:** Government-specific implementation detail to ensure data stays within your compliance boundary.</span><span class="sxs-lookup"><span data-stu-id="40038-108">**Considerations:** Government-specific implementation detail to ensure data stays within your compliance boundary.</span></span>

<span data-ttu-id="40038-109">Everything else you need to know about these services can be found in their general documentation.</span><span class="sxs-lookup"><span data-stu-id="40038-109">Everything else you need to know about these services can be found in their general documentation.</span></span>

<span data-ttu-id="40038-110">For the most current list of services, see the [Products by Region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="40038-110">For the most current list of services, see the [Products by Region](https://azure.microsoft.com/regions/services/).</span></span> 

<span data-ttu-id="40038-111">In the following tables, services specified as Resource Manager enabled have resource providers and can be managed using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="40038-111">In the following tables, services specified as Resource Manager enabled have resource providers and can be managed using PowerShell.</span></span> <span data-ttu-id="40038-112">For detailed information on Resource Manager providers, API versions, and schemas, refer [here](../azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="40038-112">For detailed information on Resource Manager providers, API versions, and schemas, refer [here](../azure-resource-manager/resource-manager-supported-services.md).</span></span> <span data-ttu-id="40038-113">Services specified as available in the Portal, can be managed in the [Azure Government Portal](https://portal.azure.us/).</span><span class="sxs-lookup"><span data-stu-id="40038-113">Services specified as available in the Portal, can be managed in the [Azure Government Portal](https://portal.azure.us/).</span></span> 


## <a name="computedocumentation-government-computemd"></a>[<span data-ttu-id="40038-114">Compute</span><span class="sxs-lookup"><span data-stu-id="40038-114">Compute</span></span>](documentation-government-compute.md)

| <span data-ttu-id="40038-115">Service</span><span class="sxs-lookup"><span data-stu-id="40038-115">Service</span></span> | <span data-ttu-id="40038-116">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-116">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-117">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-117">Portal</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="40038-118">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="40038-118">Virtual Machines</span></span>](documentation-government-compute.md#virtual-machines) | <span data-ttu-id="40038-119">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-119">Yes</span></span> | <span data-ttu-id="40038-120">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-120">Yes</span></span> |
| <span data-ttu-id="40038-121">Batch</span><span class="sxs-lookup"><span data-stu-id="40038-121">Batch</span></span> | <span data-ttu-id="40038-122">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-122">Yes</span></span> | <span data-ttu-id="40038-123">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-123">Yes</span></span> |
| <span data-ttu-id="40038-124">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="40038-124">Cloud Services</span></span> | <span data-ttu-id="40038-125">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-125">Yes</span></span> | <span data-ttu-id="40038-126">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-126">Yes</span></span> |
| <span data-ttu-id="40038-127">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="40038-127">Service Fabric</span></span> | <span data-ttu-id="40038-128">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-128">Yes</span></span> | <span data-ttu-id="40038-129">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-129">Yes</span></span> |
| <span data-ttu-id="40038-130">VM Scale Sets</span><span class="sxs-lookup"><span data-stu-id="40038-130">VM Scale Sets</span></span> | <span data-ttu-id="40038-131">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-131">Yes</span></span> | <span data-ttu-id="40038-132">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-132">Yes</span></span> |


## <a name="networkingdocumentation-government-networkingmd"></a>[<span data-ttu-id="40038-133">Networking</span><span class="sxs-lookup"><span data-stu-id="40038-133">Networking</span></span>](documentation-government-networking.md)

| <span data-ttu-id="40038-134">Service</span><span class="sxs-lookup"><span data-stu-id="40038-134">Service</span></span> | <span data-ttu-id="40038-135">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-135">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-136">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-136">Portal</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="40038-137">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="40038-137">ExpressRoute</span></span>](documentation-government-networking.md#expressroute-private-connectivity) | <span data-ttu-id="40038-138">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-138">Yes</span></span> | <span data-ttu-id="40038-139">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-139">Yes</span></span> |
| <span data-ttu-id="40038-140">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="40038-140">Virtual Network</span></span> | <span data-ttu-id="40038-141">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-141">Yes</span></span> | <span data-ttu-id="40038-142">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-142">Yes</span></span> |
| [<span data-ttu-id="40038-143">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="40038-143">Load Balancer</span></span>](documentation-government-networking.md#support-for-load-balancer) | <span data-ttu-id="40038-144">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-144">Yes</span></span> | <span data-ttu-id="40038-145">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-145">Yes</span></span> |
| [<span data-ttu-id="40038-146">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="40038-146">Traffic Manager</span></span>](documentation-government-networking.md#support-for-traffic-manger) | <span data-ttu-id="40038-147">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-147">Yes</span></span> | <span data-ttu-id="40038-148">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-148">Yes</span></span> |
| [<span data-ttu-id="40038-149">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="40038-149">VPN Gateway</span></span>](documentation-government-networking.md#support-for-vpn-gateway) | <span data-ttu-id="40038-150">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-150">Yes</span></span> | <span data-ttu-id="40038-151">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-151">Yes</span></span> |
| <span data-ttu-id="40038-152">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="40038-152">Application Gateway</span></span> | <span data-ttu-id="40038-153">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-153">Yes</span></span> | <span data-ttu-id="40038-154">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-154">Yes</span></span> |
| <span data-ttu-id="40038-155">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="40038-155">ExpressRoute</span></span> | <span data-ttu-id="40038-156">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-156">Yes</span></span> | <span data-ttu-id="40038-157">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-157">Yes</span></span> |



## <a name="storagedocumentation-government-services-storagemd"></a>[<span data-ttu-id="40038-158">Storage</span><span class="sxs-lookup"><span data-stu-id="40038-158">Storage</span></span>](documentation-government-services-storage.md)

| <span data-ttu-id="40038-159">Service</span><span class="sxs-lookup"><span data-stu-id="40038-159">Service</span></span> | <span data-ttu-id="40038-160">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-160">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-161">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-161">Portal</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="40038-162">Storage - Blobs</span><span class="sxs-lookup"><span data-stu-id="40038-162">Storage - Blobs</span></span>](documentation-government-services-storage.md#azure-storage) | <span data-ttu-id="40038-163">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-163">Yes</span></span> | <span data-ttu-id="40038-164">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-164">Yes</span></span> |
| [<span data-ttu-id="40038-165">Storage - Tables</span><span class="sxs-lookup"><span data-stu-id="40038-165">Storage - Tables</span></span>](documentation-government-services-storage.md#azure-storage) | <span data-ttu-id="40038-166">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-166">Yes</span></span> | <span data-ttu-id="40038-167">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-167">Yes</span></span> |
| [<span data-ttu-id="40038-168">Storage - Queues</span><span class="sxs-lookup"><span data-stu-id="40038-168">Storage - Queues</span></span>](documentation-government-services-storage.md#azure-storage) | <span data-ttu-id="40038-169">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-169">Yes</span></span> | <span data-ttu-id="40038-170">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-170">Yes</span></span> |
| [<span data-ttu-id="40038-171">Storage - Files</span><span class="sxs-lookup"><span data-stu-id="40038-171">Storage - Files</span></span>](documentation-government-services-storage.md#azure-storage) | <span data-ttu-id="40038-172">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-172">Yes</span></span> | <span data-ttu-id="40038-173">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-173">Yes</span></span> |
| [<span data-ttu-id="40038-174">Storage - Disks</span><span class="sxs-lookup"><span data-stu-id="40038-174">Storage - Disks</span></span>](documentation-government-services-storage.md#azure-storage) | <span data-ttu-id="40038-175">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-175">Yes</span></span> | <span data-ttu-id="40038-176">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-176">Yes</span></span> |
| [<span data-ttu-id="40038-177">StorSimple</span><span class="sxs-lookup"><span data-stu-id="40038-177">StorSimple</span></span>](documentation-government-services-storage.md) | <span data-ttu-id="40038-178">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-178">Yes</span></span> | <span data-ttu-id="40038-179">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-179">Yes</span></span> |
| [<span data-ttu-id="40038-180">Backup</span><span class="sxs-lookup"><span data-stu-id="40038-180">Backup</span></span>](documentation-government-services-storage.md#azure-storage) | <span data-ttu-id="40038-181">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-181">Yes</span></span> | <span data-ttu-id="40038-182">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-182">Yes</span></span> |
| [<span data-ttu-id="40038-183">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="40038-183">Site Recovery</span></span>](documentation-government-services-storage.md#azure-storage) | <span data-ttu-id="40038-184">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-184">Yes</span></span> | <span data-ttu-id="40038-185">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-185">Yes</span></span> |
| [<span data-ttu-id="40038-186">Import/Export</span><span class="sxs-lookup"><span data-stu-id="40038-186">Import/Export</span></span>](documentation-government-services-storage.md#azure-storage) | <span data-ttu-id="40038-187">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-187">Yes</span></span> | <span data-ttu-id="40038-188">No</span><span class="sxs-lookup"><span data-stu-id="40038-188">No</span></span> |



## <a name="web--mobiledocumentation-government-services-webandmobilemd"></a>[<span data-ttu-id="40038-189">Web + Mobile</span><span class="sxs-lookup"><span data-stu-id="40038-189">Web + Mobile</span></span>](documentation-government-services-webandmobile.md)

| <span data-ttu-id="40038-190">Service</span><span class="sxs-lookup"><span data-stu-id="40038-190">Service</span></span> | <span data-ttu-id="40038-191">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-191">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-192">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-192">Portal</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="40038-193">App Service - Web Apps</span><span class="sxs-lookup"><span data-stu-id="40038-193">App Service - Web Apps</span></span>](documentation-government-services-webandmobile.md#app-services) | <span data-ttu-id="40038-194">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-194">Yes</span></span> | <span data-ttu-id="40038-195">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-195">Yes</span></span> |
| [<span data-ttu-id="40038-196">App Service - API Apps</span><span class="sxs-lookup"><span data-stu-id="40038-196">App Service - API Apps</span></span>](documentation-government-services-webandmobile.md#app-services) | <span data-ttu-id="40038-197">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-197">Yes</span></span> | <span data-ttu-id="40038-198">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-198">Yes</span></span> |
| [<span data-ttu-id="40038-199">App Service - Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="40038-199">App Service - Mobile Apps</span></span>](documentation-government-services-webandmobile.md#app-services) | <span data-ttu-id="40038-200">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-200">Yes</span></span> | <span data-ttu-id="40038-201">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-201">Yes</span></span> |
| <span data-ttu-id="40038-202">Media Services</span><span class="sxs-lookup"><span data-stu-id="40038-202">Media Services</span></span> | <span data-ttu-id="40038-203">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-203">Yes</span></span> | <span data-ttu-id="40038-204">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-204">Yes</span></span> |


## <a name="databasesdocumentation-government-services-databasemd"></a>[<span data-ttu-id="40038-205">Databases</span><span class="sxs-lookup"><span data-stu-id="40038-205">Databases</span></span>](documentation-government-services-database.md)

| <span data-ttu-id="40038-206">Service</span><span class="sxs-lookup"><span data-stu-id="40038-206">Service</span></span> | <span data-ttu-id="40038-207">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-207">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-208">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-208">Portal</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="40038-209">SQL Database</span><span class="sxs-lookup"><span data-stu-id="40038-209">SQL Database</span></span>](documentation-government-services-database.md#sql-database) | <span data-ttu-id="40038-210">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-210">Yes</span></span> | <span data-ttu-id="40038-211">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-211">Yes</span></span> |
| <span data-ttu-id="40038-212">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="40038-212">SQL Data Warehouse</span></span> | <span data-ttu-id="40038-213">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-213">Yes</span></span> | <span data-ttu-id="40038-214">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-214">Yes</span></span> |
| <span data-ttu-id="40038-215">SQL Server Stretch Database</span><span class="sxs-lookup"><span data-stu-id="40038-215">SQL Server Stretch Database</span></span> | <span data-ttu-id="40038-216">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-216">Yes</span></span> | <span data-ttu-id="40038-217">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-217">Yes</span></span> |
| [<span data-ttu-id="40038-218">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="40038-218">Redis Cache</span></span>](documentation-government-services-database.md#azure-redis-cache) | <span data-ttu-id="40038-219">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-219">Yes</span></span> | <span data-ttu-id="40038-220">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-220">Yes</span></span> |


## <a name="intelligence--analyticsdocumentation-government-services-intelligenceandanalyticsmd"></a>[<span data-ttu-id="40038-221">Intelligence + Analytics</span><span class="sxs-lookup"><span data-stu-id="40038-221">Intelligence + Analytics</span></span>](documentation-government-services-intelligenceandanalytics.md)

| <span data-ttu-id="40038-222">Service</span><span class="sxs-lookup"><span data-stu-id="40038-222">Service</span></span> | <span data-ttu-id="40038-223">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-223">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-224">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-224">Portal</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="40038-225">HDInsights</span><span class="sxs-lookup"><span data-stu-id="40038-225">HDInsights</span></span>](documentation-government-services-intelligenceandanalytics.md#hdinsight) | <span data-ttu-id="40038-226">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-226">Yes</span></span> | <span data-ttu-id="40038-227">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-227">Yes</span></span> |
| [<span data-ttu-id="40038-228">Power BI Pro</span><span class="sxs-lookup"><span data-stu-id="40038-228">Power BI Pro</span></span>](documentation-government-services-intelligenceandanalytics.md#power-bi) | <span data-ttu-id="40038-229">No</span><span class="sxs-lookup"><span data-stu-id="40038-229">No</span></span> | <span data-ttu-id="40038-230">No (Office 365 Admin Portal)</span><span class="sxs-lookup"><span data-stu-id="40038-230">No (Office 365 Admin Portal)</span></span> |


## <a name="internet-of-things-iot"></a><span data-ttu-id="40038-231">Internet of Things (IoT)</span><span class="sxs-lookup"><span data-stu-id="40038-231">Internet of Things (IoT)</span></span>

| <span data-ttu-id="40038-232">Service</span><span class="sxs-lookup"><span data-stu-id="40038-232">Service</span></span> | <span data-ttu-id="40038-233">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-233">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-234">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-234">Portal</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40038-235">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="40038-235">Event Hubs</span></span> | <span data-ttu-id="40038-236">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-236">Yes</span></span> | <span data-ttu-id="40038-237">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-237">Yes</span></span> |
| <span data-ttu-id="40038-238">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="40038-238">Notification Hubs</span></span> | <span data-ttu-id="40038-239">No</span><span class="sxs-lookup"><span data-stu-id="40038-239">No</span></span> | <span data-ttu-id="40038-240">No (Go to [Legacy portal](https://manage.windowsazure.us/))</span><span class="sxs-lookup"><span data-stu-id="40038-240">No (Go to [Legacy portal](https://manage.windowsazure.us/))</span></span> |


## <a name="enterprise-integration"></a><span data-ttu-id="40038-241">Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="40038-241">Enterprise Integration</span></span>

| <span data-ttu-id="40038-242">Service</span><span class="sxs-lookup"><span data-stu-id="40038-242">Service</span></span> | <span data-ttu-id="40038-243">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-243">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-244">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-244">Portal</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40038-245">Service Bus</span><span class="sxs-lookup"><span data-stu-id="40038-245">Service Bus</span></span> | <span data-ttu-id="40038-246">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-246">Yes</span></span> | <span data-ttu-id="40038-247">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-247">Yes</span></span> |
| [<span data-ttu-id="40038-248">StorSimple</span><span class="sxs-lookup"><span data-stu-id="40038-248">StorSimple</span></span>](documentation-government-services-storage.md) | <span data-ttu-id="40038-249">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-249">Yes</span></span> | <span data-ttu-id="40038-250">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-250">Yes</span></span> |
| <span data-ttu-id="40038-251">SQL Server Stretch Database</span><span class="sxs-lookup"><span data-stu-id="40038-251">SQL Server Stretch Database</span></span> | <span data-ttu-id="40038-252">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-252">Yes</span></span> | <span data-ttu-id="40038-253">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-253">Yes</span></span> |



## <a name="security--identitydocumentation-government-services-securityandidentitymd"></a>[<span data-ttu-id="40038-254">Security + Identity</span><span class="sxs-lookup"><span data-stu-id="40038-254">Security + Identity</span></span>](documentation-government-services-securityandidentity.md)

| <span data-ttu-id="40038-255">Service</span><span class="sxs-lookup"><span data-stu-id="40038-255">Service</span></span> | <span data-ttu-id="40038-256">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-256">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-257">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-257">Portal</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40038-258">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="40038-258">Azure Active Directory</span></span> | <span data-ttu-id="40038-259">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-259">Yes</span></span> | <span data-ttu-id="40038-260">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-260">Yes</span></span> |
| [<span data-ttu-id="40038-261">Key Vault</span><span class="sxs-lookup"><span data-stu-id="40038-261">Key Vault</span></span>](documentation-government-services-securityandidentity.md#key-vault) | <span data-ttu-id="40038-262">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-262">Yes</span></span> | <span data-ttu-id="40038-263">No (Coming soon)</span><span class="sxs-lookup"><span data-stu-id="40038-263">No (Coming soon)</span></span> |
| <span data-ttu-id="40038-264">Multi-Factory Authentication</span><span class="sxs-lookup"><span data-stu-id="40038-264">Multi-Factory Authentication</span></span> | <span data-ttu-id="40038-265">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-265">Yes</span></span> | <span data-ttu-id="40038-266">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-266">Yes</span></span> |


## <a name="intelligence--analytics"></a><span data-ttu-id="40038-267">Intelligence + Analytics</span><span class="sxs-lookup"><span data-stu-id="40038-267">Intelligence + Analytics</span></span>

| <span data-ttu-id="40038-268">Service</span><span class="sxs-lookup"><span data-stu-id="40038-268">Service</span></span> | <span data-ttu-id="40038-269">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-269">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-270">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-270">Portal</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40038-271">Power BI</span><span class="sxs-lookup"><span data-stu-id="40038-271">Power BI</span></span> | <span data-ttu-id="40038-272">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-272">Yes</span></span> | <span data-ttu-id="40038-273">No</span><span class="sxs-lookup"><span data-stu-id="40038-273">No</span></span> |
| <span data-ttu-id="40038-274">HDInsight</span><span class="sxs-lookup"><span data-stu-id="40038-274">HDInsight</span></span> | <span data-ttu-id="40038-275">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-275">Yes</span></span> | <span data-ttu-id="40038-276">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-276">Yes</span></span> |



## <a name="monitoring--managementdocumentation-government-services-monitoringandmanagementmd"></a>[<span data-ttu-id="40038-277">Monitoring + Management</span><span class="sxs-lookup"><span data-stu-id="40038-277">Monitoring + Management</span></span>](documentation-government-services-monitoringandmanagement.md)

| <span data-ttu-id="40038-278">Service</span><span class="sxs-lookup"><span data-stu-id="40038-278">Service</span></span> | <span data-ttu-id="40038-279">Resource Manager Enabled</span><span class="sxs-lookup"><span data-stu-id="40038-279">Resource Manager Enabled</span></span> | <span data-ttu-id="40038-280">Portal</span><span class="sxs-lookup"><span data-stu-id="40038-280">Portal</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="40038-281">Automation</span><span class="sxs-lookup"><span data-stu-id="40038-281">Automation</span></span>](documentation-government-services-monitoringandmanagement.md#automation) | <span data-ttu-id="40038-282">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-282">Yes</span></span> | <span data-ttu-id="40038-283">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-283">Yes</span></span> |
| [<span data-ttu-id="40038-284">Backup</span><span class="sxs-lookup"><span data-stu-id="40038-284">Backup</span></span>](documentation-government-services-backup.md) | <span data-ttu-id="40038-285">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-285">Yes</span></span> | <span data-ttu-id="40038-286">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-286">Yes</span></span> |
| [<span data-ttu-id="40038-287">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="40038-287">Log Analytics</span></span>](documentation-government-services-monitoringandmanagement.md#log-analytics) | <span data-ttu-id="40038-288">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-288">Yes</span></span> | <span data-ttu-id="40038-289">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-289">Yes</span></span> |
| [<span data-ttu-id="40038-290">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="40038-290">Site Recovery</span></span>](documentation-government-services-monitoringandmanagement.md#site-recovery) | <span data-ttu-id="40038-291">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-291">Yes</span></span> | <span data-ttu-id="40038-292">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-292">Yes</span></span> |
| <span data-ttu-id="40038-293">Scheduler</span><span class="sxs-lookup"><span data-stu-id="40038-293">Scheduler</span></span> | <span data-ttu-id="40038-294">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-294">Yes</span></span> | <span data-ttu-id="40038-295">No</span><span class="sxs-lookup"><span data-stu-id="40038-295">No</span></span> |
| <span data-ttu-id="40038-296">Monitoring and Diagnostics</span><span class="sxs-lookup"><span data-stu-id="40038-296">Monitoring and Diagnostics</span></span> | <span data-ttu-id="40038-297">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-297">Yes</span></span> | <span data-ttu-id="40038-298">Yes</span><span class="sxs-lookup"><span data-stu-id="40038-298">Yes</span></span> |




## <a name="next-steps"></a><span data-ttu-id="40038-299">Next Steps</span><span class="sxs-lookup"><span data-stu-id="40038-299">Next Steps</span></span>
<span data-ttu-id="40038-300">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span><span class="sxs-lookup"><span data-stu-id="40038-300">For supplemental information and updates, subscribe to the [Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span></span>

