---
title: Compare Azure Government and global Azure | Microsoft Docs
description: This article compares Azure Government and global Azure.
services: azure-government
cloud: gov
documentationcenter: ''
author: Juliako
manager: femila
ms.service: azure-government
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 08/03/2018
ms.author: juliako
ms.openlocfilehash: d3839539c7dffe99ff02cf2fd2c7912d4685af90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870545"
---
# <a name="compare-azure-government-and-global-azure"></a><span data-ttu-id="622bb-103">Compare Azure Government and global Azure</span><span class="sxs-lookup"><span data-stu-id="622bb-103">Compare Azure Government and global Azure</span></span>

<span data-ttu-id="622bb-104">Microsoft Azure Government uses same underlying technologies as global Azure, which includes the core components of [Infrastructure-as-a-Service (IaaS)](https://azure.microsoft.com/overview/what-is-iaas/), [Platform-as-a-Service (PaaS)](https://azure.microsoft.com/overview/what-is-paas/), and [Software-as-a-Service (SaaS)](https://azure.microsoft.com/overview/what-is-saas/).</span><span class="sxs-lookup"><span data-stu-id="622bb-104">Microsoft Azure Government uses same underlying technologies as global Azure, which includes the core components of [Infrastructure-as-a-Service (IaaS)](https://azure.microsoft.com/overview/what-is-iaas/), [Platform-as-a-Service (PaaS)](https://azure.microsoft.com/overview/what-is-paas/), and [Software-as-a-Service (SaaS)](https://azure.microsoft.com/overview/what-is-saas/).</span></span> <span data-ttu-id="622bb-105">Azure Government includes Geo-Synchronous data replication, auto scaling, network, storage, data management, identity management, among other services.</span><span class="sxs-lookup"><span data-stu-id="622bb-105">Azure Government includes Geo-Synchronous data replication, auto scaling, network, storage, data management, identity management, among other services.</span></span> <span data-ttu-id="622bb-106">However, there are some key differences that developers working on applications hosted in Azure Government must be aware of.</span><span class="sxs-lookup"><span data-stu-id="622bb-106">However, there are some key differences that developers working on applications hosted in Azure Government must be aware of.</span></span> <span data-ttu-id="622bb-107">For detailed information, see [Guidance for developers](documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="622bb-107">For detailed information, see [Guidance for developers](documentation-government-developer-guide.md).</span></span>

<span data-ttu-id="622bb-108">As a developer, you must know how to connect to Azure Government and once you connect you will mostly have the same experience as global Azure.</span><span class="sxs-lookup"><span data-stu-id="622bb-108">As a developer, you must know how to connect to Azure Government and once you connect you will mostly have the same experience as global Azure.</span></span> <span data-ttu-id="622bb-109">This document provides links to variations in each service.</span><span class="sxs-lookup"><span data-stu-id="622bb-109">This document provides links to variations in each service.</span></span> <span data-ttu-id="622bb-110">Service specific articles include two key types of information:</span><span class="sxs-lookup"><span data-stu-id="622bb-110">Service specific articles include two key types of information:</span></span>

* <span data-ttu-id="622bb-111">**Variations**: Variations due to features that are not deployed yet or properties (for example, URLs) that are unique to the government environment.</span><span class="sxs-lookup"><span data-stu-id="622bb-111">**Variations**: Variations due to features that are not deployed yet or properties (for example, URLs) that are unique to the government environment.</span></span>  
* <span data-ttu-id="622bb-112">**Considerations**: Government-specific implementation detail to ensure that data stays within your compliance boundary.</span><span class="sxs-lookup"><span data-stu-id="622bb-112">**Considerations**: Government-specific implementation detail to ensure that data stays within your compliance boundary.</span></span>

<span data-ttu-id="622bb-113">For the most current list of services, see the [Products available by region](https://azure.microsoft.com/regions/services/) page (select Azure Government region).</span><span class="sxs-lookup"><span data-stu-id="622bb-113">For the most current list of services, see the [Products available by region](https://azure.microsoft.com/regions/services/) page (select Azure Government region).</span></span> <span data-ttu-id="622bb-114">The **services available in Azure Government** are listed by category, as well as whether they are Generally Available or available through preview.</span><span class="sxs-lookup"><span data-stu-id="622bb-114">The **services available in Azure Government** are listed by category, as well as whether they are Generally Available or available through preview.</span></span> 

> [!NOTE]
> <span data-ttu-id="622bb-115">The services listed below are Generally Available unless they have (Preview) next to them.</span><span class="sxs-lookup"><span data-stu-id="622bb-115">The services listed below are Generally Available unless they have (Preview) next to them.</span></span>

## <a name="compute"></a><span data-ttu-id="622bb-116">Compute</span><span class="sxs-lookup"><span data-stu-id="622bb-116">Compute</span></span>

* [<span data-ttu-id="622bb-117">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="622bb-117">Virtual Machines</span></span>](documentation-government-compute.md#virtual-machines) 
* [<span data-ttu-id="622bb-118">Batch</span><span class="sxs-lookup"><span data-stu-id="622bb-118">Batch</span></span>](documentation-government-compute.md#batch) 
* [<span data-ttu-id="622bb-119">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="622bb-119">Cloud Services</span></span>](documentation-government-compute.md#cloud-services)
* [<span data-ttu-id="622bb-120">Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="622bb-120">Virtual Machine Scale Sets</span></span>](documentation-government-compute.md#virtual-machine-scale-sets) 
* [<span data-ttu-id="622bb-121">Functions</span><span class="sxs-lookup"><span data-stu-id="622bb-121">Functions</span></span>](documentation-government-compute.md#azure-functions)
* [<span data-ttu-id="622bb-122">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="622bb-122">Service Fabric</span></span>](documentation-government-compute.md#service-fabric)

## <a name="networking"></a><span data-ttu-id="622bb-123">Networking</span><span class="sxs-lookup"><span data-stu-id="622bb-123">Networking</span></span>

* [<span data-ttu-id="622bb-124">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="622bb-124">ExpressRoute</span></span>](documentation-government-networking.md#expressroute-private-connectivity) 
* [<span data-ttu-id="622bb-125">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="622bb-125">Virtual Network</span></span>](documentation-government-networking.md#support-for-virtual-network) 
* [<span data-ttu-id="622bb-126">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="622bb-126">Load Balancer</span></span>](documentation-government-networking.md#support-for-load-balancer)
* [<span data-ttu-id="622bb-127">DNS</span><span class="sxs-lookup"><span data-stu-id="622bb-127">DNS</span></span>](documentation-government-networking.md#support-for-dns) 
* [<span data-ttu-id="622bb-128">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="622bb-128">Traffic Manager</span></span>](documentation-government-networking.md#support-for-traffic-manager)
* [<span data-ttu-id="622bb-129">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="622bb-129">VPN Gateway</span></span>](documentation-government-networking.md#support-for-vpn-gateway)
* [<span data-ttu-id="622bb-130">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="622bb-130">Application Gateway</span></span>](documentation-government-networking.md#support-for-application-gateway) 
* [<span data-ttu-id="622bb-131">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="622bb-131">Network Watcher</span></span>](documentation-government-networking.md#support-for-network-watcher) 

## <a name="storage"></a><span data-ttu-id="622bb-132">Storage</span><span class="sxs-lookup"><span data-stu-id="622bb-132">Storage</span></span>

* [<span data-ttu-id="622bb-133">Blob storage</span><span class="sxs-lookup"><span data-stu-id="622bb-133">Blob storage</span></span>](documentation-government-services-storage.md#azure-storage) 
* [<span data-ttu-id="622bb-134">Table storage</span><span class="sxs-lookup"><span data-stu-id="622bb-134">Table storage</span></span>](documentation-government-services-storage.md#azure-storage) 
* [<span data-ttu-id="622bb-135">Queue storage</span><span class="sxs-lookup"><span data-stu-id="622bb-135">Queue storage</span></span>](documentation-government-services-storage.md#azure-storage) 
* [<span data-ttu-id="622bb-136">File storage</span><span class="sxs-lookup"><span data-stu-id="622bb-136">File storage</span></span>](documentation-government-services-storage.md#azure-storage) 
* [<span data-ttu-id="622bb-137">Disk storage</span><span class="sxs-lookup"><span data-stu-id="622bb-137">Disk storage</span></span>](documentation-government-services-storage.md#azure-storage) 
* [<span data-ttu-id="622bb-138">StorSimple</span><span class="sxs-lookup"><span data-stu-id="622bb-138">StorSimple</span></span>](documentation-government-services-storage.md) 
* [<span data-ttu-id="622bb-139">Import/Export</span><span class="sxs-lookup"><span data-stu-id="622bb-139">Import/Export</span></span>](documentation-government-services-storage.md#azure-importexport) 

## <a name="web--mobile"></a><span data-ttu-id="622bb-140">Web + Mobile</span><span class="sxs-lookup"><span data-stu-id="622bb-140">Web + Mobile</span></span>
 
* [<span data-ttu-id="622bb-141">App Service: Web Apps</span><span class="sxs-lookup"><span data-stu-id="622bb-141">App Service: Web Apps</span></span>](documentation-government-services-webandmobile.md#app-services) 
* [<span data-ttu-id="622bb-142">App Service: Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="622bb-142">App Service: Mobile Apps</span></span>](documentation-government-services-webandmobile.md#app-services) 
* [<span data-ttu-id="622bb-143">API Management</span><span class="sxs-lookup"><span data-stu-id="622bb-143">API Management</span></span>](documentation-government-services-webandmobile.md#api-management) 
* [<span data-ttu-id="622bb-144">Media Services</span><span class="sxs-lookup"><span data-stu-id="622bb-144">Media Services</span></span>](documentation-government-services-media.md) 

## <a name="databases"></a><span data-ttu-id="622bb-145">Databases</span><span class="sxs-lookup"><span data-stu-id="622bb-145">Databases</span></span>

* [<span data-ttu-id="622bb-146">SQL Database</span><span class="sxs-lookup"><span data-stu-id="622bb-146">SQL Database</span></span>](documentation-government-services-database.md#sql-database) 
* [<span data-ttu-id="622bb-147">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="622bb-147">SQL Data Warehouse</span></span>](documentation-government-services-database.md#sql-data-warehouse)
* [<span data-ttu-id="622bb-148">SQL Server Stretch Database</span><span class="sxs-lookup"><span data-stu-id="622bb-148">SQL Server Stretch Database</span></span>](documentation-government-services-database.md#sql-server-stretch-database) 
* [<span data-ttu-id="622bb-149">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="622bb-149">Azure Cosmos DB</span></span>](documentation-government-services-database.md#azure-cosmos-db)
* [<span data-ttu-id="622bb-150">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="622bb-150">Azure Redis Cache</span></span>](documentation-government-services-database.md#azure-redis-cache) 

## <a name="data--analytics"></a><span data-ttu-id="622bb-151">Data + Analytics</span><span class="sxs-lookup"><span data-stu-id="622bb-151">Data + Analytics</span></span>
 
* [<span data-ttu-id="622bb-152">HDInsight</span><span class="sxs-lookup"><span data-stu-id="622bb-152">HDInsight</span></span>](documentation-government-services-dataandanalytics.md#hdinsight) 
* [<span data-ttu-id="622bb-153">Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="622bb-153">Azure Analysis Services</span></span>](documentation-government-services-dataandanalytics.md#azure-analysis-services) 
* <span data-ttu-id="622bb-154">[Power BI Pro](documentation-government-services-dataandanalytics.md#power-bi) (This service can be accessed through PowerShell and CLI, but not yet available through the [Azure Government portal](https://portal.azure.us).)</span><span class="sxs-lookup"><span data-stu-id="622bb-154">[Power BI Pro](documentation-government-services-dataandanalytics.md#power-bi) (This service can be accessed through PowerShell and CLI, but not yet available through the [Azure Government portal](https://portal.azure.us).)</span></span>

## <a name="ai--cognitive-services"></a><span data-ttu-id="622bb-155">AI + Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="622bb-155">AI + Cognitive Services</span></span> 
 
* <span data-ttu-id="622bb-156">[Cognitive Services](documentation-government-services-aiandcognitiveservices.md) (Preview) (This service can be accessed through PowerShell and CLI, but not yet available through the [Azure Government portal](https://portal.azure.us).)</span><span class="sxs-lookup"><span data-stu-id="622bb-156">[Cognitive Services](documentation-government-services-aiandcognitiveservices.md) (Preview) (This service can be accessed through PowerShell and CLI, but not yet available through the [Azure Government portal](https://portal.azure.us).)</span></span>

## <a name="internet-of-things"></a><span data-ttu-id="622bb-157">Internet of Things</span><span class="sxs-lookup"><span data-stu-id="622bb-157">Internet of Things</span></span>

* [<span data-ttu-id="622bb-158">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="622bb-158">IoT Hub</span></span>](documentation-government-services-iot-hub.md#azure-iot-hub) 
* [<span data-ttu-id="622bb-159">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="622bb-159">Azure Event Hubs</span></span>](documentation-government-services-iot-hub.md#azure-event-hubs) 
* <span data-ttu-id="622bb-160">[Azure Notification Hubs](documentation-government-services-iot-hub.md#azure-notification-hubs) (This service can be accessed through PowerShell and CLI, but not yet available through the [Azure Government portal](https://portal.azure.us)).</span><span class="sxs-lookup"><span data-stu-id="622bb-160">[Azure Notification Hubs](documentation-government-services-iot-hub.md#azure-notification-hubs) (This service can be accessed through PowerShell and CLI, but not yet available through the [Azure Government portal](https://portal.azure.us)).</span></span>

## <a name="enterprise-integration"></a><span data-ttu-id="622bb-161">Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="622bb-161">Enterprise Integration</span></span>

* [<span data-ttu-id="622bb-162">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="622bb-162">Logic Apps</span></span>](documentation-government-services-integration.md#logic-apps) 
* [<span data-ttu-id="622bb-163">Service Bus</span><span class="sxs-lookup"><span data-stu-id="622bb-163">Service Bus</span></span>](documentation-government-networking.md#support-for-service-bus) 
* [<span data-ttu-id="622bb-164">StorSimple</span><span class="sxs-lookup"><span data-stu-id="622bb-164">StorSimple</span></span>](documentation-government-services-storage.md) 
* [<span data-ttu-id="622bb-165">SQL Server Stretch Database</span><span class="sxs-lookup"><span data-stu-id="622bb-165">SQL Server Stretch Database</span></span>](documentation-government-services-database.md#sql-server-stretch-database) 

## <a name="security--identity"></a><span data-ttu-id="622bb-166">Security + Identity</span><span class="sxs-lookup"><span data-stu-id="622bb-166">Security + Identity</span></span>
 
* <span data-ttu-id="622bb-167">[Azure Security Center](documentation-government-services-securityandidentity.md#azure-security-center) (Preview)</span><span class="sxs-lookup"><span data-stu-id="622bb-167">[Azure Security Center](documentation-government-services-securityandidentity.md#azure-security-center) (Preview)</span></span>
* [<span data-ttu-id="622bb-168">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="622bb-168">Azure Active Directory</span></span>](documentation-government-services-securityandidentity.md#azure-active-directory) 
* [<span data-ttu-id="622bb-169">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="622bb-169">Azure Active Directory Premium</span></span>](documentation-government-services-securityandidentity.md#azure-active-directory-premium-p1-and-p2) 
* [<span data-ttu-id="622bb-170">Key Vault</span><span class="sxs-lookup"><span data-stu-id="622bb-170">Key Vault</span></span>](documentation-government-services-securityandidentity.md#key-vault) 
* [<span data-ttu-id="622bb-171">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="622bb-171">Azure Multi-Factor Authentication</span></span>](documentation-government-services-securityandidentity.md#azure-multi-factor-authentication) 

## <a name="monitoring--management"></a><span data-ttu-id="622bb-172">Monitoring + Management</span><span class="sxs-lookup"><span data-stu-id="622bb-172">Monitoring + Management</span></span>

* <span data-ttu-id="622bb-173">[Advisor](documentation-government-services-monitoringandmanagement.md#advisor) (Preview)</span><span class="sxs-lookup"><span data-stu-id="622bb-173">[Advisor](documentation-government-services-monitoringandmanagement.md#advisor) (Preview)</span></span>
* [<span data-ttu-id="622bb-174">Automation</span><span class="sxs-lookup"><span data-stu-id="622bb-174">Automation</span></span>](documentation-government-services-monitoringandmanagement.md#automation) 
* [<span data-ttu-id="622bb-175">Backup</span><span class="sxs-lookup"><span data-stu-id="622bb-175">Backup</span></span>](documentation-government-services-backup.md) 
* [<span data-ttu-id="622bb-176">Policy</span><span class="sxs-lookup"><span data-stu-id="622bb-176">Policy</span></span>](documentation-government-services-monitoringandmanagement.md#policy) 
* [<span data-ttu-id="622bb-177">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="622bb-177">Log Analytics</span></span>](documentation-government-services-monitoringandmanagement.md#log-analytics) 
* [<span data-ttu-id="622bb-178">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="622bb-178">Site Recovery</span></span>](documentation-government-services-monitoringandmanagement.md#site-recovery) 
* [<span data-ttu-id="622bb-179">Scheduler</span><span class="sxs-lookup"><span data-stu-id="622bb-179">Scheduler</span></span>](documentation-government-services-monitoringandmanagement.md#scheduler) 
* [<span data-ttu-id="622bb-180">Monitoring and Diagnostics</span><span class="sxs-lookup"><span data-stu-id="622bb-180">Monitoring and Diagnostics</span></span>](documentation-government-services-monitoringandmanagement.md#monitor) 
* [<span data-ttu-id="622bb-181">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="622bb-181">Azure Portal</span></span>](documentation-government-services-monitoringandmanagement.md#azure-portal) 
* [<span data-ttu-id="622bb-182">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="622bb-182">Azure Resource Manager</span></span>](documentation-government-services-monitoringandmanagement.md#azure-resource-manager) 

## <a name="developer-tools"></a><span data-ttu-id="622bb-183">Developer tools</span><span class="sxs-lookup"><span data-stu-id="622bb-183">Developer tools</span></span>

* [<span data-ttu-id="622bb-184">DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="622bb-184">DevTest Labs</span></span>](documentation-government-services-devtools.md#devtest-labs) 

## <a name="next-steps"></a><span data-ttu-id="622bb-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="622bb-185">Next steps</span></span>

<span data-ttu-id="622bb-186">Learn more about Azure Government:</span><span class="sxs-lookup"><span data-stu-id="622bb-186">Learn more about Azure Government:</span></span>

* [<span data-ttu-id="622bb-187">Acquiring and accessing Azure Government</span><span class="sxs-lookup"><span data-stu-id="622bb-187">Acquiring and accessing Azure Government</span></span>](https://azure.microsoft.com/offers/azure-government/)

<span data-ttu-id="622bb-188">Start using Azure Government:</span><span class="sxs-lookup"><span data-stu-id="622bb-188">Start using Azure Government:</span></span>

* [<span data-ttu-id="622bb-189">Guidance for developers</span><span class="sxs-lookup"><span data-stu-id="622bb-189">Guidance for developers</span></span>](documentation-government-developer-guide.md)
* [<span data-ttu-id="622bb-190">Connect with the Azure Government portal</span><span class="sxs-lookup"><span data-stu-id="622bb-190">Connect with the Azure Government portal</span></span>](documentation-government-get-started-connect-with-portal.md)
