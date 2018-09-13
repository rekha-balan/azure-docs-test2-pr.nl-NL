---
title: Azure subscription limits and quotas | Microsoft Docs
description: Provides a list of common Azure subscription and service limits, quotas, and constraints. This includes information on how to increase limits along with maximum values.
services: ''
documentationcenter: ''
author: rothja
manager: jeffreyg
editor: ''
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: byvinyal
ms.openlocfilehash: e1d2d8931848d5fb56a817731c6415ef2d253d3d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554037"
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="a48a2-104">Azure subscription and service limits, quotas, and constraints</span><span class="sxs-lookup"><span data-stu-id="a48a2-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="a48a2-105">This document lists some of the most common Microsoft Azure limits, which are also sometimes called quotas.</span><span class="sxs-lookup"><span data-stu-id="a48a2-105">This document lists some of the most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="a48a2-106">This document doesn't currently cover all Azure services.</span><span class="sxs-lookup"><span data-stu-id="a48a2-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="a48a2-107">Over time, the list will be expanded and updated to cover more of the platform.</span><span class="sxs-lookup"><span data-stu-id="a48a2-107">Over time, the list will be expanded and updated to cover more of the platform.</span></span>

<span data-ttu-id="a48a2-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) to learn more about Azure pricing.</span><span class="sxs-lookup"><span data-stu-id="a48a2-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) to learn more about Azure pricing.</span></span> <span data-ttu-id="a48a2-109">There, you can estimate your costs using the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting the pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="a48a2-109">There, you can estimate your costs using the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting the pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="a48a2-110">For tips to help manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a48a2-110">For tips to help manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a48a2-111">If you want to raise the limit or quota above the **Default Limit**, [open an online customer support request at no charge](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/).</span><span class="sxs-lookup"><span data-stu-id="a48a2-111">If you want to raise the limit or quota above the **Default Limit**, [open an online customer support request at no charge](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/).</span></span> <span data-ttu-id="a48a2-112">The limits can't be raised above the **Maximum Limit** value shown in the following tables.</span><span class="sxs-lookup"><span data-stu-id="a48a2-112">The limits can't be raised above the **Maximum Limit** value shown in the following tables.</span></span> <span data-ttu-id="a48a2-113">If there is no **Maximum Limit** column, then the resource doesn't have adjustable limits.</span><span class="sxs-lookup"><span data-stu-id="a48a2-113">If there is no **Maximum Limit** column, then the resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="a48a2-114">Free Trial subscriptions are not eligible for limit or quota increases.</span><span class="sxs-lookup"><span data-stu-id="a48a2-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="a48a2-115">If you have a Free Trial, you can upgrade to a [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span><span class="sxs-lookup"><span data-stu-id="a48a2-115">If you have a Free Trial, you can upgrade to a [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="a48a2-116">For more information, see [Upgrade Azure Free Trial to Pay-As-You-Go](billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="a48a2-116">For more information, see [Upgrade Azure Free Trial to Pay-As-You-Go](billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-the-azure-resource-manager"></a><span data-ttu-id="a48a2-117">Limits and the Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a48a2-117">Limits and the Azure Resource Manager</span></span>
<span data-ttu-id="a48a2-118">It is now possible to combine multiple Azure resources in to a single Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="a48a2-118">It is now possible to combine multiple Azure resources in to a single Azure Resource Group.</span></span> <span data-ttu-id="a48a2-119">When using Resource Groups, limits that once were global become managed at a regional level with the Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a48a2-119">When using Resource Groups, limits that once were global become managed at a regional level with the Azure Resource Manager.</span></span> <span data-ttu-id="a48a2-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a48a2-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="a48a2-121">In the limits below, a new table has been added to reflect any differences in limits when using the Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a48a2-121">In the limits below, a new table has been added to reflect any differences in limits when using the Azure Resource Manager.</span></span> <span data-ttu-id="a48a2-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span><span class="sxs-lookup"><span data-stu-id="a48a2-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="a48a2-123">When a limit applies to both scenarios, it is only shown in the first table.</span><span class="sxs-lookup"><span data-stu-id="a48a2-123">When a limit applies to both scenarios, it is only shown in the first table.</span></span> <span data-ttu-id="a48a2-124">Unless otherwise indicated, limits are global across all regions.</span><span class="sxs-lookup"><span data-stu-id="a48a2-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="a48a2-125">It is important to emphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as the service management quotas are.</span><span class="sxs-lookup"><span data-stu-id="a48a2-125">It is important to emphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as the service management quotas are.</span></span> <span data-ttu-id="a48a2-126">Let's use core quotas as an example.</span><span class="sxs-lookup"><span data-stu-id="a48a2-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="a48a2-127">If you need to request a quota increase with support for cores, you need to decide how many cores you want to use in which regions, and then make a specific request for Azure Resource Group core quotas for the amounts and regions that you want.</span><span class="sxs-lookup"><span data-stu-id="a48a2-127">If you need to request a quota increase with support for cores, you need to decide how many cores you want to use in which regions, and then make a specific request for Azure Resource Group core quotas for the amounts and regions that you want.</span></span> <span data-ttu-id="a48a2-128">Therefore, if you need to use 30 cores in West Europe to run your application there; you should specifically request 30 cores in West Europe.</span><span class="sxs-lookup"><span data-stu-id="a48a2-128">Therefore, if you need to use 30 cores in West Europe to run your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="a48a2-129">But you will not have a core quota increase in any other region -- only West Europe will have the 30-core quota.</span><span class="sxs-lookup"><span data-stu-id="a48a2-129">But you will not have a core quota increase in any other region -- only West Europe will have the 30-core quota.</span></span>
> <span data-ttu-id="a48a2-130"><!-- --> As a result, you may find it useful to consider deciding what your Azure Resource Group quotas need to be for your workload in any one region, and request that amount in each region into which you are considering deployment.</span><span class="sxs-lookup"><span data-stu-id="a48a2-130"><!-- --> As a result, you may find it useful to consider deciding what your Azure Resource Group quotas need to be for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="a48a2-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span><span class="sxs-lookup"><span data-stu-id="a48a2-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="a48a2-132">Service-specific limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-132">Service-specific limits</span></span>
* [<span data-ttu-id="a48a2-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="a48a2-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="a48a2-134">API Management</span><span class="sxs-lookup"><span data-stu-id="a48a2-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="a48a2-135">App Service</span><span class="sxs-lookup"><span data-stu-id="a48a2-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="a48a2-136">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="a48a2-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="a48a2-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="a48a2-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="a48a2-138">Automation</span><span class="sxs-lookup"><span data-stu-id="a48a2-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="a48a2-139">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="a48a2-139">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="a48a2-140">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a48a2-140">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="a48a2-141">Backup</span><span class="sxs-lookup"><span data-stu-id="a48a2-141">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="a48a2-142">Batch</span><span class="sxs-lookup"><span data-stu-id="a48a2-142">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="a48a2-143">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a48a2-143">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="a48a2-144">CDN</span><span class="sxs-lookup"><span data-stu-id="a48a2-144">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="a48a2-145">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a48a2-145">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="a48a2-146">Data Factory</span><span class="sxs-lookup"><span data-stu-id="a48a2-146">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="a48a2-147">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a48a2-147">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="a48a2-148">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a48a2-148">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="a48a2-149">DNS</span><span class="sxs-lookup"><span data-stu-id="a48a2-149">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="a48a2-150">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a48a2-150">DocumentDB</span></span>](#documentdb-limits)
* [<span data-ttu-id="a48a2-151">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a48a2-151">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="a48a2-152">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a48a2-152">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="a48a2-153">Key Vault</span><span class="sxs-lookup"><span data-stu-id="a48a2-153">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="a48a2-154">Log Analytics / Operational Insights</span><span class="sxs-lookup"><span data-stu-id="a48a2-154">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="a48a2-155">Media Services</span><span class="sxs-lookup"><span data-stu-id="a48a2-155">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="a48a2-156">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a48a2-156">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="a48a2-157">Mobile Services</span><span class="sxs-lookup"><span data-stu-id="a48a2-157">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="a48a2-158">Monitor</span><span class="sxs-lookup"><span data-stu-id="a48a2-158">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="a48a2-159">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="a48a2-159">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="a48a2-160">Networking</span><span class="sxs-lookup"><span data-stu-id="a48a2-160">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="a48a2-161">Notification Hub Service</span><span class="sxs-lookup"><span data-stu-id="a48a2-161">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="a48a2-162">Resource Group</span><span class="sxs-lookup"><span data-stu-id="a48a2-162">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="a48a2-163">Scheduler</span><span class="sxs-lookup"><span data-stu-id="a48a2-163">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="a48a2-164">Search</span><span class="sxs-lookup"><span data-stu-id="a48a2-164">Search</span></span>](#search-limits)
* [<span data-ttu-id="a48a2-165">Service Bus</span><span class="sxs-lookup"><span data-stu-id="a48a2-165">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="a48a2-166">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a48a2-166">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="a48a2-167">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a48a2-167">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="a48a2-168">Storage</span><span class="sxs-lookup"><span data-stu-id="a48a2-168">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="a48a2-169">StorSimple System</span><span class="sxs-lookup"><span data-stu-id="a48a2-169">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="a48a2-170">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a48a2-170">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="a48a2-171">Subscription</span><span class="sxs-lookup"><span data-stu-id="a48a2-171">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="a48a2-172">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a48a2-172">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="a48a2-173">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="a48a2-173">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="a48a2-174">Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="a48a2-174">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="a48a2-175">Subscription limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-175">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="a48a2-176">Subscription limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-176">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="a48a2-177">Subscription limits - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a48a2-177">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="a48a2-178">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span><span class="sxs-lookup"><span data-stu-id="a48a2-178">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="a48a2-179">Limits that have not changed with the Azure Resource Manager are not listed below.</span><span class="sxs-lookup"><span data-stu-id="a48a2-179">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="a48a2-180">Please refer to the previous table for those limits.</span><span class="sxs-lookup"><span data-stu-id="a48a2-180">Please refer to the previous table for those limits.</span></span>

<span data-ttu-id="a48a2-181">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a48a2-181">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="a48a2-182">Resource Group limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-182">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="a48a2-183">Virtual Machines limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-183">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="a48a2-184">Virtual Machine limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-184">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="a48a2-185">Virtual Machines limits - Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a48a2-185">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="a48a2-186">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span><span class="sxs-lookup"><span data-stu-id="a48a2-186">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="a48a2-187">Limits that have not changed with the Azure Resource Manager are not listed below.</span><span class="sxs-lookup"><span data-stu-id="a48a2-187">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="a48a2-188">Please refer to the previous table for those limits.</span><span class="sxs-lookup"><span data-stu-id="a48a2-188">Please refer to the previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="a48a2-189">Virtual Machine Scale Sets limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-189">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="a48a2-190">Networking limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-190">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="a48a2-191">Networking limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-191">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="a48a2-192">Application Gateway limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-192">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="a48a2-193">Traffic Manager limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-193">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="a48a2-194">DNS limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-194">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="a48a2-195">Storage limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-195">Storage limits</span></span>
<span data-ttu-id="a48a2-196">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="a48a2-196">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="a48a2-197">Storage Service limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-197">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="a48a2-198">Virtual machine disk limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-198">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="a48a2-199">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span><span class="sxs-lookup"><span data-stu-id="a48a2-199">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="a48a2-200">Managed virtual machine disks</span><span class="sxs-lookup"><span data-stu-id="a48a2-200">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="a48a2-201">Unmanaged virtual machine disks</span><span class="sxs-lookup"><span data-stu-id="a48a2-201">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="a48a2-202">Storage Resource Provider limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-202">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="a48a2-203">Cloud Services limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-203">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="a48a2-204">App Service limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-204">App Service limits</span></span>
<span data-ttu-id="a48a2-205">The following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="a48a2-205">The following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="a48a2-206">Scheduler limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-206">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="a48a2-207">Batch limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-207">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="a48a2-208">BizTalk Services limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-208">BizTalk Services limits</span></span>
<span data-ttu-id="a48a2-209">The following table shows the limits for Azure Biztalk Services.</span><span class="sxs-lookup"><span data-stu-id="a48a2-209">The following table shows the limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="documentdb-limits"></a><span data-ttu-id="a48a2-210">DocumentDB limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-210">DocumentDB limits</span></span>
<span data-ttu-id="a48a2-211">DocumentDB is a global scale database in which throughput and storage can be scaled to handle whatever your application requires.</span><span class="sxs-lookup"><span data-stu-id="a48a2-211">DocumentDB is a global scale database in which throughput and storage can be scaled to handle whatever your application requires.</span></span> <span data-ttu-id="a48a2-212">If you have any questions about the scale DocumentDB provides, please send email to askdocdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="a48a2-212">If you have any questions about the scale DocumentDB provides, please send email to askdocdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="a48a2-213">Mobile Engagement limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-213">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="a48a2-214">Search limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-214">Search limits</span></span>
<span data-ttu-id="a48a2-215">Pricing tiers determine the capacity and limits of your search service.</span><span class="sxs-lookup"><span data-stu-id="a48a2-215">Pricing tiers determine the capacity and limits of your search service.</span></span> <span data-ttu-id="a48a2-216">Tiers include:</span><span class="sxs-lookup"><span data-stu-id="a48a2-216">Tiers include:</span></span>

* <span data-ttu-id="a48a2-217">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span><span class="sxs-lookup"><span data-stu-id="a48a2-217">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="a48a2-218">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up to three replicas for highly available query workloads.</span><span class="sxs-lookup"><span data-stu-id="a48a2-218">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up to three replicas for highly available query workloads.</span></span>
* <span data-ttu-id="a48a2-219">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span><span class="sxs-lookup"><span data-stu-id="a48a2-219">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="a48a2-220">Multiple levels exist within the standard tier so that you can choose a resource configuration that best matches your workload profile.</span><span class="sxs-lookup"><span data-stu-id="a48a2-220">Multiple levels exist within the standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="a48a2-221">**Limits per subscription**</span><span class="sxs-lookup"><span data-stu-id="a48a2-221">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="a48a2-222">**Limits per search service**</span><span class="sxs-lookup"><span data-stu-id="a48a2-222">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="a48a2-223">To learn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="a48a2-223">To learn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="a48a2-224">Media Services limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-224">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="a48a2-225">CDN limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-225">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="a48a2-226">Mobile Services limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-226">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="a48a2-227">Monitor limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-227">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="a48a2-228">Notification Hub Service limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-228">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="a48a2-229">Event Hubs limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-229">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="a48a2-230">Service Bus limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-230">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="a48a2-231">IoT Hub limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-231">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="a48a2-232">Data Factory limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-232">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="a48a2-233">Data Lake Analytics limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-233">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="a48a2-234">Data Lake Store limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-234">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="a48a2-235">Stream Analytics limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-235">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="a48a2-236">Active Directory limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-236">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="a48a2-237">Azure RemoteApp limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-237">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="a48a2-238">StorSimple System limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-238">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="a48a2-239">Log Analytics limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-239">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="a48a2-240">Backup limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-240">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="a48a2-241">Site Recovery limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-241">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="a48a2-242">Application Insights limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-242">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="a48a2-243">API Management limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-243">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="a48a2-244">Azure Redis Cache limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-244">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="a48a2-245">Key Vault limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-245">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="a48a2-246">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="a48a2-246">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="a48a2-247">Automation limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-247">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="a48a2-248">SQL Database limits</span><span class="sxs-lookup"><span data-stu-id="a48a2-248">SQL Database limits</span></span>
<span data-ttu-id="a48a2-249">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a48a2-249">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a48a2-250">See also</span><span class="sxs-lookup"><span data-stu-id="a48a2-250">See also</span></span>
[<span data-ttu-id="a48a2-251">Understanding Azure Limits and Increases</span><span class="sxs-lookup"><span data-stu-id="a48a2-251">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="a48a2-252">Virtual Machine and Cloud Service Sizes for Azure</span><span class="sxs-lookup"><span data-stu-id="a48a2-252">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="a48a2-253">Sizes for Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a48a2-253">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

