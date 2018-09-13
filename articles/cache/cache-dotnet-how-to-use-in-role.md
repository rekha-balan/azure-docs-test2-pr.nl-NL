---
title: How to use In-Role Cache (.NET) | Microsoft Docs
description: Learn how to use Azure In-Role Cache. The samples are written in C# code and use the .NET API.
services: cache
documentationcenter: .net
author: steved0x
manager: douge
editor: ''
ms.assetid: 4dad61ec-422a-4618-8054-84ae4ce652a2
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: sdanie
ROBOTS: NOINDEX
ms.openlocfilehash: ad6cee041d9c70805f6fc44242b1ba2d6ba77dc2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562993"
---
# <a name="how-to-use-in-role-cache-for-azure-cache"></a><span data-ttu-id="ee3f0-104">How to Use In-Role Cache for Azure Cache</span><span class="sxs-lookup"><span data-stu-id="ee3f0-104">How to Use In-Role Cache for Azure Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ee3f0-105">As per last year's [announcement](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/), Azure Managed Cache Service and Azure In-Role Cache **have been retired** as of November 30, 2016.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-105">As per last year's [announcement](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/), Azure Managed Cache Service and Azure In-Role Cache **have been retired** as of November 30, 2016.</span></span> <span data-ttu-id="ee3f0-106">Our recommendation is to use [Azure Redis Cache](https://azure.microsoft.com/services/cache/).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-106">Our recommendation is to use [Azure Redis Cache](https://azure.microsoft.com/services/cache/).</span></span> <span data-ttu-id="ee3f0-107">For information on migrating, please see [Migrate from Managed Cache Service to Azure Redis Cache](../redis-cache/cache-migrate-to-redis.md).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-107">For information on migrating, please see [Migrate from Managed Cache Service to Azure Redis Cache](../redis-cache/cache-migrate-to-redis.md).</span></span>
> 
> 

<span data-ttu-id="ee3f0-108">This guide shows you how to get started using **In-Role Cache for Azure Cache**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-108">This guide shows you how to get started using **In-Role Cache for Azure Cache**.</span></span> <span data-ttu-id="ee3f0-109">The samples are written in C\# code and use the .NET API.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-109">The samples are written in C\# code and use the .NET API.</span></span> <span data-ttu-id="ee3f0-110">The scenarios covered include **configuring a cache cluster**, **configuring cache clients**, **adding and removing objects from the cache, storing ASP.NET session state in the cache**, and **enabling ASP.NET page output caching using the cache**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-110">The scenarios covered include **configuring a cache cluster**, **configuring cache clients**, **adding and removing objects from the cache, storing ASP.NET session state in the cache**, and **enabling ASP.NET page output caching using the cache**.</span></span> <span data-ttu-id="ee3f0-111">For more information on using In-Role Cache, refer to the [Next Steps][Next Steps] section.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-111">For more information on using In-Role Cache, refer to the [Next Steps][Next Steps] section.</span></span>



<a name="what-is"></a>

## <a name="what-is-in-role-cache"></a><span data-ttu-id="ee3f0-112">What is In-Role Cache?</span><span class="sxs-lookup"><span data-stu-id="ee3f0-112">What is In-Role Cache?</span></span>
<span data-ttu-id="ee3f0-113">In-Role Cache provides a caching layer to your Azure applications.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-113">In-Role Cache provides a caching layer to your Azure applications.</span></span> <span data-ttu-id="ee3f0-114">Caching increases performance by temporarily storing information in-memory from other backend sources, and can reduce the costs associated with database transactions in the cloud.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-114">Caching increases performance by temporarily storing information in-memory from other backend sources, and can reduce the costs associated with database transactions in the cloud.</span></span> <span data-ttu-id="ee3f0-115">In-Role Cache includes the following features:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-115">In-Role Cache includes the following features:</span></span>

* <span data-ttu-id="ee3f0-116">Pre-built ASP.NET providers for session state and page output caching, enabling acceleration of web applications without having to modify application code.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-116">Pre-built ASP.NET providers for session state and page output caching, enabling acceleration of web applications without having to modify application code.</span></span>
* <span data-ttu-id="ee3f0-117">Caches any serializable managed object - for example: CLR objects, rows, XML, binary data.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-117">Caches any serializable managed object - for example: CLR objects, rows, XML, binary data.</span></span>
* <span data-ttu-id="ee3f0-118">Consistent development model across both Azure and Windows Server AppFabric.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-118">Consistent development model across both Azure and Windows Server AppFabric.</span></span>

<span data-ttu-id="ee3f0-119">In-Role Cache provides a way to perform caching by using a portion of the memory of the virtual machines that host the role instances in your Azure cloud services (also known as hosted services).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-119">In-Role Cache provides a way to perform caching by using a portion of the memory of the virtual machines that host the role instances in your Azure cloud services (also known as hosted services).</span></span> <span data-ttu-id="ee3f0-120">You have greater flexibility in terms of deployment options, the caches can be very large in size and have no cache-specific quota restrictions.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-120">You have greater flexibility in terms of deployment options, the caches can be very large in size and have no cache-specific quota restrictions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee3f0-121">Starting with Azure SDK 2.6, In-Role Cache is using Microsoft Azure Storage SDK version 4.3.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-121">Starting with Azure SDK 2.6, In-Role Cache is using Microsoft Azure Storage SDK version 4.3.</span></span> <span data-ttu-id="ee3f0-122">In previous versions of the Azure SDK, In-Role Cache used Azure Storage SDK 1.7.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-122">In previous versions of the Azure SDK, In-Role Cache used Azure Storage SDK 1.7.</span></span> <span data-ttu-id="ee3f0-123">Applications using In-Role Cache with versions of the Azure SDK before 2.6 should migrate to Azure SDK 2.6 before Azure Storage version 2011-08-18 is decommissioned on August 1, 2016.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-123">Applications using In-Role Cache with versions of the Azure SDK before 2.6 should migrate to Azure SDK 2.6 before Azure Storage version 2011-08-18 is decommissioned on August 1, 2016.</span></span> <span data-ttu-id="ee3f0-124">For more information, see [Azure SDK 2.6 Release Notes - In-Role Cache](../app-service-web/azure-sdk-dotnet-release-notes-2-6.md#in-role-cache-updates) and [Microsoft Azure Storage Service Version Removal Update: Extension to 2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-124">For more information, see [Azure SDK 2.6 Release Notes - In-Role Cache](../app-service-web/azure-sdk-dotnet-release-notes-2-6.md#in-role-cache-updates) and [Microsoft Azure Storage Service Version Removal Update: Extension to 2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).</span></span>
> 
> 

<span data-ttu-id="ee3f0-125">Caching on role instances has the following advantages:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-125">Caching on role instances has the following advantages:</span></span>

* <span data-ttu-id="ee3f0-126">Pay no premium for caching.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-126">Pay no premium for caching.</span></span> <span data-ttu-id="ee3f0-127">You pay only for the compute resources that host the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-127">You pay only for the compute resources that host the cache.</span></span>
* <span data-ttu-id="ee3f0-128">Eliminates cache quotas and throttling.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-128">Eliminates cache quotas and throttling.</span></span>
* <span data-ttu-id="ee3f0-129">Offers greater control and isolation.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-129">Offers greater control and isolation.</span></span> 
* <span data-ttu-id="ee3f0-130">Improved performance.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-130">Improved performance.</span></span>
* <span data-ttu-id="ee3f0-131">Automatically sizes caches when roles are scaled in or out. Effectively scales the memory that is available for caching up or down when role instances are added or removed.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-131">Automatically sizes caches when roles are scaled in or out. Effectively scales the memory that is available for caching up or down when role instances are added or removed.</span></span>
* <span data-ttu-id="ee3f0-132">Provides full-fidelity development time debugging.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-132">Provides full-fidelity development time debugging.</span></span> 
* <span data-ttu-id="ee3f0-133">Supports the memcache protocol.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-133">Supports the memcache protocol.</span></span>

<span data-ttu-id="ee3f0-134">In addition, caching on role instances offers these configurable options:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-134">In addition, caching on role instances offers these configurable options:</span></span>

* <span data-ttu-id="ee3f0-135">Configure a dedicated role for caching, or co-locate caching on existing roles.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-135">Configure a dedicated role for caching, or co-locate caching on existing roles.</span></span> 
* <span data-ttu-id="ee3f0-136">Make your cache available to multiple clients in the same cloud service deployment.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-136">Make your cache available to multiple clients in the same cloud service deployment.</span></span>
* <span data-ttu-id="ee3f0-137">Create multiple named caches with different properties.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-137">Create multiple named caches with different properties.</span></span>
* <span data-ttu-id="ee3f0-138">Optionally configure high availability on individual caches.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-138">Optionally configure high availability on individual caches.</span></span>
* <span data-ttu-id="ee3f0-139">Use expanded caching capabilities such as regions, tagging, and notifications.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-139">Use expanded caching capabilities such as regions, tagging, and notifications.</span></span>

<span data-ttu-id="ee3f0-140">This guide provides an overview of getting started with In-Role Cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-140">This guide provides an overview of getting started with In-Role Cache.</span></span> <span data-ttu-id="ee3f0-141">For more detailed information on these features that are beyond the scope of this getting started guide, see [Overview of In-Role Cache][Overview of In-Role Cache].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-141">For more detailed information on these features that are beyond the scope of this getting started guide, see [Overview of In-Role Cache][Overview of In-Role Cache].</span></span>

<a name="getting-started-cache-role-instance"></a>

## <a name="getting-started-with-in-role-cache"></a><span data-ttu-id="ee3f0-142">Getting Started with In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="ee3f0-142">Getting Started with In-Role Cache</span></span>
<span data-ttu-id="ee3f0-143">In-Role Cache provides a way to enable caching using the memory that is on the virtual machines that host your role instances.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-143">In-Role Cache provides a way to enable caching using the memory that is on the virtual machines that host your role instances.</span></span> <span data-ttu-id="ee3f0-144">The role instances that host your caches are known as a **cache cluster**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-144">The role instances that host your caches are known as a **cache cluster**.</span></span> <span data-ttu-id="ee3f0-145">There are two deployment topologies for caching on role instances:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-145">There are two deployment topologies for caching on role instances:</span></span>

* <span data-ttu-id="ee3f0-146">**Dedicated Role** caching - The role instances are used exclusively for caching.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-146">**Dedicated Role** caching - The role instances are used exclusively for caching.</span></span>
* <span data-ttu-id="ee3f0-147">**Co-located Role** caching - The cache shares the VM resources (bandwidth, CPU, and memory) with the application.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-147">**Co-located Role** caching - The cache shares the VM resources (bandwidth, CPU, and memory) with the application.</span></span>

<span data-ttu-id="ee3f0-148">To use caching on role instances, you need to configure a cache cluster, and then configure the cache clients so they can access the cache cluster.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-148">To use caching on role instances, you need to configure a cache cluster, and then configure the cache clients so they can access the cache cluster.</span></span>

* <span data-ttu-id="ee3f0-149">[Configure the cache cluster][Configure the cache cluster]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-149">[Configure the cache cluster][Configure the cache cluster]</span></span>
* <span data-ttu-id="ee3f0-150">[Configure the cache clients][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-150">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="enable-caching"></a>

## <a name="configure-the-cache-cluster"></a><span data-ttu-id="ee3f0-151">Configure the cache cluster</span><span class="sxs-lookup"><span data-stu-id="ee3f0-151">Configure the cache cluster</span></span>
<span data-ttu-id="ee3f0-152">To configure a **Co-located Role** cache cluster, select the role in which you wish to host the cache cluster.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-152">To configure a **Co-located Role** cache cluster, select the role in which you wish to host the cache cluster.</span></span> <span data-ttu-id="ee3f0-153">Right-click the role properties in **Solution Explorer** and choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-153">Right-click the role properties in **Solution Explorer** and choose **Properties**.</span></span>

![RoleCache1][RoleCache1]

<span data-ttu-id="ee3f0-155">Switch to the **Caching** tab, check the **Enable Caching** checkbox, and specify the desired caching options.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-155">Switch to the **Caching** tab, check the **Enable Caching** checkbox, and specify the desired caching options.</span></span> <span data-ttu-id="ee3f0-156">When caching is enabled in a **Worker Role** or **ASP.NET Web Role**, the default configuration is **Co-located Role** caching with 30% of the memory of the role instances allocated for caching.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-156">When caching is enabled in a **Worker Role** or **ASP.NET Web Role**, the default configuration is **Co-located Role** caching with 30% of the memory of the role instances allocated for caching.</span></span> <span data-ttu-id="ee3f0-157">A default cache is automatically configured, and additional named caches can be created if desired, and these caches will share the allocated memory.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-157">A default cache is automatically configured, and additional named caches can be created if desired, and these caches will share the allocated memory.</span></span>

![RoleCache2][RoleCache2]

<span data-ttu-id="ee3f0-159">To configure a **Dedicated Role** cache cluster, add a **Cache Worker Role** to your project.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-159">To configure a **Dedicated Role** cache cluster, add a **Cache Worker Role** to your project.</span></span>

![RoleCache7][RoleCache7]

<span data-ttu-id="ee3f0-161">When a **Cache Worker Role** is added to a project, the default configuration is **Dedicated Role** caching.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-161">When a **Cache Worker Role** is added to a project, the default configuration is **Dedicated Role** caching.</span></span>

![RoleCache8][RoleCache8]

<span data-ttu-id="ee3f0-163">Once caching is enabled, the cache cluster storage account can be configured.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-163">Once caching is enabled, the cache cluster storage account can be configured.</span></span> <span data-ttu-id="ee3f0-164">In-Role Cache requires an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-164">In-Role Cache requires an Azure storage account.</span></span> <span data-ttu-id="ee3f0-165">This storage account is used to hold configuration data about the cache cluster that is accessed from all virtual machines that make up the cache cluster.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-165">This storage account is used to hold configuration data about the cache cluster that is accessed from all virtual machines that make up the cache cluster.</span></span> <span data-ttu-id="ee3f0-166">This storage account is specified on the **Caching** tab of the cache cluster role property page, just above the **Named Cache Settings**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-166">This storage account is specified on the **Caching** tab of the cache cluster role property page, just above the **Named Cache Settings**.</span></span>

![RoleCache10][RoleCache10]

> <span data-ttu-id="ee3f0-168">If this storage account is not configured the roles will fail to start.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-168">If this storage account is not configured the roles will fail to start.</span></span> 
> 
> 

<span data-ttu-id="ee3f0-169">The size of the cache is determined by a combination of the VM size of the role, the instance count of the role, and whether the cache cluster is configured as a dedicated role or co-located role cache cluster.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-169">The size of the cache is determined by a combination of the VM size of the role, the instance count of the role, and whether the cache cluster is configured as a dedicated role or co-located role cache cluster.</span></span>

> <span data-ttu-id="ee3f0-170">This section provides a simplified overview on configuring the cache size.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-170">This section provides a simplified overview on configuring the cache size.</span></span> <span data-ttu-id="ee3f0-171">For more information on cache size and other capacity planning considerations, see [In-Role Cache Capacity Planning Considerations][In-Role Cache Capacity Planning Considerations].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-171">For more information on cache size and other capacity planning considerations, see [In-Role Cache Capacity Planning Considerations][In-Role Cache Capacity Planning Considerations].</span></span>
> 
> 

<span data-ttu-id="ee3f0-172">To configure the virtual machine size and the number of role instances, right-click the role properties in **Solution Explorer** and choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-172">To configure the virtual machine size and the number of role instances, right-click the role properties in **Solution Explorer** and choose **Properties**.</span></span>

![RoleCache1][RoleCache1]

<span data-ttu-id="ee3f0-174">Switch to the **Configuration** tab. The default **Instance count** is 1, and the default **VM size** is **Small**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-174">Switch to the **Configuration** tab. The default **Instance count** is 1, and the default **VM size** is **Small**.</span></span>

![RoleCache3][RoleCache3]

<span data-ttu-id="ee3f0-176">The total memory for the VM sizes is as follows:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-176">The total memory for the VM sizes is as follows:</span></span> 

* <span data-ttu-id="ee3f0-177">**Small**: 1.75 GB</span><span class="sxs-lookup"><span data-stu-id="ee3f0-177">**Small**: 1.75 GB</span></span>
* <span data-ttu-id="ee3f0-178">**Medium**: 3.5 GB</span><span class="sxs-lookup"><span data-stu-id="ee3f0-178">**Medium**: 3.5 GB</span></span>
* <span data-ttu-id="ee3f0-179">**Large**: 7 GB</span><span class="sxs-lookup"><span data-stu-id="ee3f0-179">**Large**: 7 GB</span></span>
* <span data-ttu-id="ee3f0-180">**ExtraLarge**: 14 GB</span><span class="sxs-lookup"><span data-stu-id="ee3f0-180">**ExtraLarge**: 14 GB</span></span>

> <span data-ttu-id="ee3f0-181">These memory sizes represent the total amount of memory available to the VM which is shared across the OS, cache process, cache data, and application.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-181">These memory sizes represent the total amount of memory available to the VM which is shared across the OS, cache process, cache data, and application.</span></span> <span data-ttu-id="ee3f0-182">For more information on configuring Virtual Machine Sizes, see [How to Configure Virtual Machine Sizes][How to Configure Virtual Machine Sizes].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-182">For more information on configuring Virtual Machine Sizes, see [How to Configure Virtual Machine Sizes][How to Configure Virtual Machine Sizes].</span></span> <span data-ttu-id="ee3f0-183">Note that cache is unsupported on **ExtraSmall** VM sizes.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-183">Note that cache is unsupported on **ExtraSmall** VM sizes.</span></span>
> 
> 

<span data-ttu-id="ee3f0-184">When **Co-located Role** caching is specified, the cache size is determined by taking the specified percentage of the virtual machine memory.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-184">When **Co-located Role** caching is specified, the cache size is determined by taking the specified percentage of the virtual machine memory.</span></span> <span data-ttu-id="ee3f0-185">When **Dedicated Role** caching is specified, all of the available memory of the virtual machine is used for caching.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-185">When **Dedicated Role** caching is specified, all of the available memory of the virtual machine is used for caching.</span></span> <span data-ttu-id="ee3f0-186">If two role instances are configured, the combined memory of the virtual machines is used.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-186">If two role instances are configured, the combined memory of the virtual machines is used.</span></span> <span data-ttu-id="ee3f0-187">This forms a cache cluster where the available caching memory is distributed across multiple role instances but presented to the clients of the cache as a single resource.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-187">This forms a cache cluster where the available caching memory is distributed across multiple role instances but presented to the clients of the cache as a single resource.</span></span> <span data-ttu-id="ee3f0-188">Configuring additional role instances increases the cache size in the same manner.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-188">Configuring additional role instances increases the cache size in the same manner.</span></span> <span data-ttu-id="ee3f0-189">To determine the settings needed to provision a cache of the desired size, you can use the Capacity Planning Spreadsheet which is covered in [In-Role Cache Capacity Planning Considerations][In-Role Cache Capacity Planning Considerations].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-189">To determine the settings needed to provision a cache of the desired size, you can use the Capacity Planning Spreadsheet which is covered in [In-Role Cache Capacity Planning Considerations][In-Role Cache Capacity Planning Considerations].</span></span>

<span data-ttu-id="ee3f0-190">Once the cache cluster is configured, you can configure the cache clients to allow access to the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-190">Once the cache cluster is configured, you can configure the cache clients to allow access to the cache.</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="ee3f0-191">Configure the cache clients</span><span class="sxs-lookup"><span data-stu-id="ee3f0-191">Configure the cache clients</span></span>
<span data-ttu-id="ee3f0-192">To access an In-Role Cache cache, the clients must be within the same deployment.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-192">To access an In-Role Cache cache, the clients must be within the same deployment.</span></span> <span data-ttu-id="ee3f0-193">If the cache cluster is a dedicated role cache cluster, then the clients are other roles in the deployment.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-193">If the cache cluster is a dedicated role cache cluster, then the clients are other roles in the deployment.</span></span> <span data-ttu-id="ee3f0-194">If the cache cluster is a co-located role cache cluster, then the clients could be either the other roles in the deployment, or the roles themselves that host the cache cluster.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-194">If the cache cluster is a co-located role cache cluster, then the clients could be either the other roles in the deployment, or the roles themselves that host the cache cluster.</span></span> <span data-ttu-id="ee3f0-195">A NuGet package is provided that can be used to configure each client role that accesses the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-195">A NuGet package is provided that can be used to configure each client role that accesses the cache.</span></span> <span data-ttu-id="ee3f0-196">To configure a role to access a cache cluster using the Caching NuGet package, right-click the role project in **Solution Explorer** and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-196">To configure a role to access a cache cluster using the Caching NuGet package, right-click the role project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![RoleCache4][RoleCache4]

<span data-ttu-id="ee3f0-198">Select **In-Role Cache**, click **Install**, and then click **I Accept**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-198">Select **In-Role Cache**, click **Install**, and then click **I Accept**.</span></span>

> <span data-ttu-id="ee3f0-199">If **In-Role Cache** does not appear in the list type **WindowsAzure.Caching** into the **Search Online** text box and select it from the results.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-199">If **In-Role Cache** does not appear in the list type **WindowsAzure.Caching** into the **Search Online** text box and select it from the results.</span></span>
> 
> 

![RoleCache5][RoleCache5]

<span data-ttu-id="ee3f0-201">The NuGet package does several things: it adds the required configuration to the config file of the role, it adds a cache client diagnostic level setting to the ServiceConfiguration.cscfg file of the Azure application, and it adds the required assembly references.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-201">The NuGet package does several things: it adds the required configuration to the config file of the role, it adds a cache client diagnostic level setting to the ServiceConfiguration.cscfg file of the Azure application, and it adds the required assembly references.</span></span>

> <span data-ttu-id="ee3f0-202">For ASP.NET web roles, the Caching NuGet package also adds two commented out sections to web.config. The first section enables session state to be stored in the cache, and the second section enables ASP.NET page output caching.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-202">For ASP.NET web roles, the Caching NuGet package also adds two commented out sections to web.config. The first section enables session state to be stored in the cache, and the second section enables ASP.NET page output caching.</span></span> <span data-ttu-id="ee3f0-203">For more information, see [How To: Store ASP.NET Session State in the Cache] and [How To: Store ASP.NET Page Output Caching in the Cache][How To: Store ASP.NET Page Output Caching in the Cache].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-203">For more information, see [How To: Store ASP.NET Session State in the Cache] and [How To: Store ASP.NET Page Output Caching in the Cache][How To: Store ASP.NET Page Output Caching in the Cache].</span></span>
> 
> 

<span data-ttu-id="ee3f0-204">The NuGet package adds the following configuration elements into your role's web.config or app.config. A **dataCacheClients** section and a **cacheDiagnostics** section are added under the **configSections** element.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-204">The NuGet package adds the following configuration elements into your role's web.config or app.config. A **dataCacheClients** section and a **cacheDiagnostics** section are added under the **configSections** element.</span></span> <span data-ttu-id="ee3f0-205">If there is no **configSections** element present, one is created as a child of the **configuration** element.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-205">If there is no **configSections** element present, one is created as a child of the **configuration** element.</span></span>

    <configSections>
      <!-- Existing sections omitted for clarity. -->

      <section name="dataCacheClients" 
               type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" 
               allowLocation="true" 
               allowDefinition="Everywhere" />

      <section name="cacheDiagnostics" 
               type="Microsoft.ApplicationServer.Caching.AzureCommon.DiagnosticsConfigurationSection, Microsoft.ApplicationServer.Caching.AzureCommon" 
               allowLocation="true" 
               allowDefinition="Everywhere" />
    </configSections>

<span data-ttu-id="ee3f0-206">These new sections include references to a **dataCacheClients** element and a **cacheDiagnostics** element.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-206">These new sections include references to a **dataCacheClients** element and a **cacheDiagnostics** element.</span></span> <span data-ttu-id="ee3f0-207">These elements are also added to the **configuration** element.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-207">These elements are also added to the **configuration** element.</span></span>

    <dataCacheClients>
      <dataCacheClient name="default">
        <autoDiscover isEnabled="true" identifier="[cache cluster role name]" />
        <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
      </dataCacheClient>
    </dataCacheClients>
    <cacheDiagnostics>
      <crashDump dumpLevel="Off" dumpStorageQuotaInMB="100" />
    </cacheDiagnostics>

<span data-ttu-id="ee3f0-208">After the configuration is added, replace **[cache cluster role name]** with the name of the role that hosts the cache cluster.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-208">After the configuration is added, replace **[cache cluster role name]** with the name of the role that hosts the cache cluster.</span></span>

> <span data-ttu-id="ee3f0-209">If **[cache cluster role name]** is not replaced with the name of the role that hosts the cache cluster, then a **TargetInvocationException** will be thrown when the cache is accessed with an inner **DatacacheException** with the message "No such role exists".</span><span class="sxs-lookup"><span data-stu-id="ee3f0-209">If **[cache cluster role name]** is not replaced with the name of the role that hosts the cache cluster, then a **TargetInvocationException** will be thrown when the cache is accessed with an inner **DatacacheException** with the message "No such role exists".</span></span>
> 
> 

<span data-ttu-id="ee3f0-210">The NuGet package also adds a **ClientDiagnosticLevel** setting to the **ConfigurationSettings** of the cache client role in ServiceConfiguration.cscfg.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-210">The NuGet package also adds a **ClientDiagnosticLevel** setting to the **ConfigurationSettings** of the cache client role in ServiceConfiguration.cscfg.</span></span> <span data-ttu-id="ee3f0-211">The following example is the **WebRole1** section from a ServiceConfiguration.cscfg file with a **ClientDiagnosticLevel** of 1, which is the default **ClientDiagnosticLevel**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-211">The following example is the **WebRole1** section from a ServiceConfiguration.cscfg file with a **ClientDiagnosticLevel** of 1, which is the default **ClientDiagnosticLevel**.</span></span>

    <Role name="WebRole1">
      <Instances count="1" />
      <ConfigurationSettings>
        <!-- Existing settings omitted for clarity. -->
        <Setting name="Microsoft.WindowsAzure.Plugins.Caching.ClientDiagnosticLevel" 
                 value="1" />
      </ConfigurationSettings>
    </Role>

> <span data-ttu-id="ee3f0-212">In-Role Cache provides both a cache server and a cache client diagnostic level.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-212">In-Role Cache provides both a cache server and a cache client diagnostic level.</span></span> <span data-ttu-id="ee3f0-213">The diagnostic level is a single setting that configures the level of diagnostic information collected for caching.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-213">The diagnostic level is a single setting that configures the level of diagnostic information collected for caching.</span></span> <span data-ttu-id="ee3f0-214">For more information, see [Troubleshooting and Diagnostics for In-Role Cache][Troubleshooting and Diagnostics for In-Role Cache]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-214">For more information, see [Troubleshooting and Diagnostics for In-Role Cache][Troubleshooting and Diagnostics for In-Role Cache]</span></span>
> 
> 

<span data-ttu-id="ee3f0-215">The NuGet package also adds references to the following assemblies:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-215">The NuGet package also adds references to the following assemblies:</span></span>

* <span data-ttu-id="ee3f0-216">Microsoft.ApplicationServer.Caching.Client.dll</span><span class="sxs-lookup"><span data-stu-id="ee3f0-216">Microsoft.ApplicationServer.Caching.Client.dll</span></span>
* <span data-ttu-id="ee3f0-217">Microsoft.ApplicationServer.Caching.Core.dll</span><span class="sxs-lookup"><span data-stu-id="ee3f0-217">Microsoft.ApplicationServer.Caching.Core.dll</span></span>
* <span data-ttu-id="ee3f0-218">Microsoft.WindowsFabric.Common.dll</span><span class="sxs-lookup"><span data-stu-id="ee3f0-218">Microsoft.WindowsFabric.Common.dll</span></span>
* <span data-ttu-id="ee3f0-219">Microsoft.WindowsFabric.Data.Common.dll</span><span class="sxs-lookup"><span data-stu-id="ee3f0-219">Microsoft.WindowsFabric.Data.Common.dll</span></span>
* <span data-ttu-id="ee3f0-220">Microsoft.ApplicationServer.Caching.AzureCommon.dll</span><span class="sxs-lookup"><span data-stu-id="ee3f0-220">Microsoft.ApplicationServer.Caching.AzureCommon.dll</span></span>
* <span data-ttu-id="ee3f0-221">Microsoft.ApplicationServer.Caching.AzureClientHelper.dll</span><span class="sxs-lookup"><span data-stu-id="ee3f0-221">Microsoft.ApplicationServer.Caching.AzureClientHelper.dll</span></span>

<span data-ttu-id="ee3f0-222">If your role is an ASP.NET Web Role, the following assembly reference is also added:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-222">If your role is an ASP.NET Web Role, the following assembly reference is also added:</span></span>

* <span data-ttu-id="ee3f0-223">Microsoft.Web.DistributedCache.dll.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-223">Microsoft.Web.DistributedCache.dll.</span></span>

<span data-ttu-id="ee3f0-224">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-224">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="ee3f0-225">Working with Caches</span><span class="sxs-lookup"><span data-stu-id="ee3f0-225">Working with Caches</span></span>
<span data-ttu-id="ee3f0-226">The steps in this section describe how to perform common tasks with caching.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-226">The steps in this section describe how to perform common tasks with caching.</span></span>

* <span data-ttu-id="ee3f0-227">[How To: Create a DataCache Object][How To: Create a DataCache Object]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-227">[How To: Create a DataCache Object][How To: Create a DataCache Object]</span></span>
* <span data-ttu-id="ee3f0-228">[How To: Add and Retrieve an Object from the Cache][How To: Add and Retrieve an Object from the Cache]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-228">[How To: Add and Retrieve an Object from the Cache][How To: Add and Retrieve an Object from the Cache]</span></span>
* <span data-ttu-id="ee3f0-229">[How To: Specify the Expiration of an Object in the Cache][How To: Specify the Expiration of an Object in the Cache]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-229">[How To: Specify the Expiration of an Object in the Cache][How To: Specify the Expiration of an Object in the Cache]</span></span>
* <span data-ttu-id="ee3f0-230">[How To: Store ASP.NET Session State in the Cache][How To: Store ASP.NET Session State in the Cache]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-230">[How To: Store ASP.NET Session State in the Cache][How To: Store ASP.NET Session State in the Cache]</span></span>
* <span data-ttu-id="ee3f0-231">[How To: Store ASP.NET Page Output Caching in the Cache][How To: Store ASP.NET Page Output Caching in the Cache]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-231">[How To: Store ASP.NET Page Output Caching in the Cache][How To: Store ASP.NET Page Output Caching in the Cache]</span></span>

<a name="create-cache-object"></a>

## <a name="how-to-create-a-datacache-object"></a><span data-ttu-id="ee3f0-232">How To: Create a DataCache Object</span><span class="sxs-lookup"><span data-stu-id="ee3f0-232">How To: Create a DataCache Object</span></span>
<span data-ttu-id="ee3f0-233">In order to programmatically work with a cache, you need a reference to the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-233">In order to programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="ee3f0-234">Add the following to the top of any file from which you want to use In-Role Cache:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-234">Add the following to the top of any file from which you want to use In-Role Cache:</span></span>

    using Microsoft.ApplicationServer.Caching;

> <span data-ttu-id="ee3f0-235">If Visual Studio doesn't recognize the types in the using statement even after installing the Caching NuGet package, which adds the necessary references, ensure that the target profile for the project is .NET Framework 4.0 or higher, and be sure to select one of the profiles that does not specify **Client Profile**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-235">If Visual Studio doesn't recognize the types in the using statement even after installing the Caching NuGet package, which adds the necessary references, ensure that the target profile for the project is .NET Framework 4.0 or higher, and be sure to select one of the profiles that does not specify **Client Profile**.</span></span> <span data-ttu-id="ee3f0-236">For instructions on configuring cache clients, see [Configure the cache clients][Configure the cache clients].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-236">For instructions on configuring cache clients, see [Configure the cache clients][Configure the cache clients].</span></span>
> 
> 

<span data-ttu-id="ee3f0-237">There are two ways to create a **DataCache** object.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-237">There are two ways to create a **DataCache** object.</span></span> <span data-ttu-id="ee3f0-238">The first way is to simply create a **DataCache**, passing in the name of the desired cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-238">The first way is to simply create a **DataCache**, passing in the name of the desired cache.</span></span>

    DataCache cache = new DataCache("default");

<span data-ttu-id="ee3f0-239">Once the **DataCache** is instantiated, you can use it to interact with the cache, as described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-239">Once the **DataCache** is instantiated, you can use it to interact with the cache, as described in the following sections.</span></span>

<span data-ttu-id="ee3f0-240">To use the second way, create a new **DataCacheFactory** object in your application using the default constructor.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-240">To use the second way, create a new **DataCacheFactory** object in your application using the default constructor.</span></span> <span data-ttu-id="ee3f0-241">This causes the cache client to use the settings in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-241">This causes the cache client to use the settings in the configuration file.</span></span> <span data-ttu-id="ee3f0-242">Call either the **GetDefaultCache** method of the new **DataCacheFactory** instance which returns a **DataCache** object, or the **GetCache** method and pass in the name of your cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-242">Call either the **GetDefaultCache** method of the new **DataCacheFactory** instance which returns a **DataCache** object, or the **GetCache** method and pass in the name of your cache.</span></span> <span data-ttu-id="ee3f0-243">These methods return a **DataCache** object that can then be used to programmatically access the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-243">These methods return a **DataCache** object that can then be used to programmatically access the cache.</span></span>

    // Cache client configured by settings in application configuration file.
    DataCacheFactory cacheFactory = new DataCacheFactory();
    DataCache cache = cacheFactory.GetDefaultCache();
    // Or DataCache cache = cacheFactory.GetCache("MyCache");
    // cache can now be used to add and retrieve items.    

<a name="add-object"></a>

## <a name="how-to-add-and-retrieve-an-object-from-the-cache"></a><span data-ttu-id="ee3f0-244">How To: Add and Retrieve an Object from the Cache</span><span class="sxs-lookup"><span data-stu-id="ee3f0-244">How To: Add and Retrieve an Object from the Cache</span></span>
<span data-ttu-id="ee3f0-245">To add an item to the cache, the **Add** method or the **Put** method can be used.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-245">To add an item to the cache, the **Add** method or the **Put** method can be used.</span></span> <span data-ttu-id="ee3f0-246">The **Add** method adds the specified object to the cache, keyed by the value of the key parameter.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-246">The **Add** method adds the specified object to the cache, keyed by the value of the key parameter.</span></span>

    // Add the string "value" to the cache, keyed by "item"
    cache.Add("item", "value");

<span data-ttu-id="ee3f0-247">If an object with the same key is already in the cache, a **DataCacheException** will be thrown with the following message:</span><span class="sxs-lookup"><span data-stu-id="ee3f0-247">If an object with the same key is already in the cache, a **DataCacheException** will be thrown with the following message:</span></span>

> <span data-ttu-id="ee3f0-248">ErrorCode:SubStatus: An attempt is being made to create an object with a Key that already exists in the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-248">ErrorCode:SubStatus: An attempt is being made to create an object with a Key that already exists in the cache.</span></span> <span data-ttu-id="ee3f0-249">Caching will only accept unique Key values for objects.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-249">Caching will only accept unique Key values for objects.</span></span>
> 
> 

<span data-ttu-id="ee3f0-250">To retrieve an object with a specific key, the **Get** method can be used.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-250">To retrieve an object with a specific key, the **Get** method can be used.</span></span> <span data-ttu-id="ee3f0-251">If the object exists, it is returned, and if it does not, null is returned.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-251">If the object exists, it is returned, and if it does not, null is returned.</span></span>

    // Add the string "value" to the cache, keyed by "key"
    object result = cache.Get("Item");
    if (result == null)
    {
        // "Item" not in cache. Obtain it from specified data source
        // and add it.
        string value = GetItemValue(...);
        cache.Add("item", value);
    }
    else
    {
        // "Item" is in cache, cast result to correct type.
    }

<span data-ttu-id="ee3f0-252">The **Put** method adds the object with the specified key to the cache if it does not exist, or replaces the object if it does exist.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-252">The **Put** method adds the object with the specified key to the cache if it does not exist, or replaces the object if it does exist.</span></span>

    // Add the string "value" to the cache, keyed by "item". If it exists,
    // replace it.
    cache.Put("item", "value");

<a name="specify-expiration"></a>

## <a name="how-to-specify-the-expiration-of-an-object-in-the-cache"></a><span data-ttu-id="ee3f0-253">How To: Specify the Expiration of an Object in the Cache</span><span class="sxs-lookup"><span data-stu-id="ee3f0-253">How To: Specify the Expiration of an Object in the Cache</span></span>
<span data-ttu-id="ee3f0-254">By default items in the cache expire 10 minutes after they are placed in the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-254">By default items in the cache expire 10 minutes after they are placed in the cache.</span></span> <span data-ttu-id="ee3f0-255">This can be configured in the **Time to Live (min)** setting in the role properties of the role that hosts the cache cluster.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-255">This can be configured in the **Time to Live (min)** setting in the role properties of the role that hosts the cache cluster.</span></span>

![RoleCache6][RoleCache6]

<span data-ttu-id="ee3f0-257">There are three types of **Expiration Type**: **None**, **Absolute**, and **Sliding Window**.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-257">There are three types of **Expiration Type**: **None**, **Absolute**, and **Sliding Window**.</span></span> <span data-ttu-id="ee3f0-258">These configure how **Time to Live (min)** is used to determine expiration.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-258">These configure how **Time to Live (min)** is used to determine expiration.</span></span> <span data-ttu-id="ee3f0-259">The default **Expiration Type** is **Absolute**, which means that the countdown timer for an item's expiration begins when the item is placed into the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-259">The default **Expiration Type** is **Absolute**, which means that the countdown timer for an item's expiration begins when the item is placed into the cache.</span></span> <span data-ttu-id="ee3f0-260">Once the specified amount of time has elapsed for an item, the item expires.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-260">Once the specified amount of time has elapsed for an item, the item expires.</span></span> <span data-ttu-id="ee3f0-261">If **Sliding Window** is specified, then the expiration countdown for an item is reset each time the item is accessed in the cache, and the item will not expire until the specified amount of time has elapsed since its last access.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-261">If **Sliding Window** is specified, then the expiration countdown for an item is reset each time the item is accessed in the cache, and the item will not expire until the specified amount of time has elapsed since its last access.</span></span> <span data-ttu-id="ee3f0-262">If **None** is specified, then **Time to Live (min)** must be set to **0**, and items will not expire, and will remain valid as long as they are in the cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-262">If **None** is specified, then **Time to Live (min)** must be set to **0**, and items will not expire, and will remain valid as long as they are in the cache.</span></span>

<span data-ttu-id="ee3f0-263">If a longer or shorter timeout interval than what is configured in the role properties is desired, a specific duration can be specified when an item is added or updated in the cache by using the overload of **Add** and **Put** that take a **TimeSpan** parameter.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-263">If a longer or shorter timeout interval than what is configured in the role properties is desired, a specific duration can be specified when an item is added or updated in the cache by using the overload of **Add** and **Put** that take a **TimeSpan** parameter.</span></span> <span data-ttu-id="ee3f0-264">In the following example, the string **value** is added to cache, keyed by **item**, with a timeout of 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-264">In the following example, the string **value** is added to cache, keyed by **item**, with a timeout of 30 minutes.</span></span>

    // Add the string "value" to the cache, keyed by "item"
    cache.Add("item", "value", TimeSpan.FromMinutes(30));

<span data-ttu-id="ee3f0-265">To view the remaining timeout interval of an item in the cache, the **GetCacheItem** method can be used to retrieve a **DataCacheItem** object that contains information about the item in the cache, including the remaining timeout interval.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-265">To view the remaining timeout interval of an item in the cache, the **GetCacheItem** method can be used to retrieve a **DataCacheItem** object that contains information about the item in the cache, including the remaining timeout interval.</span></span>

    // Get a DataCacheItem object that contains information about
    // "item" in the cache. If there is no object keyed by "item" null
    // is returned. 
    DataCacheItem item = cache.GetCacheItem("item");
    TimeSpan timeRemaining = item.Timeout;

<a name="store-session"></a>

## <a name="how-to-store-aspnet-session-state-in-the-cache"></a><span data-ttu-id="ee3f0-266">How To: Store ASP.NET Session State in the Cache</span><span class="sxs-lookup"><span data-stu-id="ee3f0-266">How To: Store ASP.NET Session State in the Cache</span></span>
<span data-ttu-id="ee3f0-267">The Session State Provider for In-Role Cache is an out-of-process storage mechanism for ASP.NET applications.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-267">The Session State Provider for In-Role Cache is an out-of-process storage mechanism for ASP.NET applications.</span></span> <span data-ttu-id="ee3f0-268">This provider enables you to store your session state in an Azure cache rather than in-memory or in a SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-268">This provider enables you to store your session state in an Azure cache rather than in-memory or in a SQL Server database.</span></span> <span data-ttu-id="ee3f0-269">To use the caching session state provider, first configure your cache cluster, and then configure your ASP.NET application for caching using the Caching NuGet package as described in [Getting Started with In-Role Cache][Getting Started with In-Role Cache].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-269">To use the caching session state provider, first configure your cache cluster, and then configure your ASP.NET application for caching using the Caching NuGet package as described in [Getting Started with In-Role Cache][Getting Started with In-Role Cache].</span></span> <span data-ttu-id="ee3f0-270">When the Caching NuGet package is installed, it adds a commented out section in web.config that contains the required configuration for your ASP.NET application to use the Session State Provider for In-Role Cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-270">When the Caching NuGet package is installed, it adds a commented out section in web.config that contains the required configuration for your ASP.NET application to use the Session State Provider for In-Role Cache.</span></span>

    <!--Uncomment this section to use In-Role Cache for session state caching
    <system.web>
      <sessionState mode="Custom" customProvider="AFCacheSessionStateProvider">
        <providers>
          <add name="AFCacheSessionStateProvider" 
            type="Microsoft.Web.DistributedCache.DistributedCacheSessionStateStoreProvider,
                  Microsoft.Web.DistributedCache" 
            cacheName="default" 
            dataCacheClientName="default"/>
        </providers>
      </sessionState>
    </system.web>-->

> <span data-ttu-id="ee3f0-271">If your web.config does not contain this commented out section after installing the Caching NuGet package, ensure that the latest NuGet Package Manager is installed from [NuGet Package Manager Installation][NuGet Package Manager Installation], and then uninstall and reinstall the package.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-271">If your web.config does not contain this commented out section after installing the Caching NuGet package, ensure that the latest NuGet Package Manager is installed from [NuGet Package Manager Installation][NuGet Package Manager Installation], and then uninstall and reinstall the package.</span></span>
> 
> 

<span data-ttu-id="ee3f0-272">To enable the Session State Provider for In-Role Cache, uncomment the specified section.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-272">To enable the Session State Provider for In-Role Cache, uncomment the specified section.</span></span> <span data-ttu-id="ee3f0-273">The default cache is specified in the provided snippet.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-273">The default cache is specified in the provided snippet.</span></span> <span data-ttu-id="ee3f0-274">To use a different cache, specify the desired cache in the **cacheName** attribute.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-274">To use a different cache, specify the desired cache in the **cacheName** attribute.</span></span>

<span data-ttu-id="ee3f0-275">For more information about using the Caching service session state provider, see [Session State Provider for In-Role Cache][Session State Provider for In-Role Cache].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-275">For more information about using the Caching service session state provider, see [Session State Provider for In-Role Cache][Session State Provider for In-Role Cache].</span></span>

<a name="store-page"></a>

## <a name="how-to-store-aspnet-page-output-caching-in-the-cache"></a><span data-ttu-id="ee3f0-276">How To: Store ASP.NET Page Output Caching in the Cache</span><span class="sxs-lookup"><span data-stu-id="ee3f0-276">How To: Store ASP.NET Page Output Caching in the Cache</span></span>
<span data-ttu-id="ee3f0-277">The Output Cache Provider for In-Role Cache is an out-of-process storage mechanism for output cache data.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-277">The Output Cache Provider for In-Role Cache is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="ee3f0-278">This data is specifically for full HTTP responses (page output caching).</span><span class="sxs-lookup"><span data-stu-id="ee3f0-278">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="ee3f0-279">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-279">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span> <span data-ttu-id="ee3f0-280">To use the output cache provider, first configure your cache cluster, and then configure your ASP.NET application for caching using the Caching NuGet package, as described in [Getting Started with In-Role Cache][Getting Started with In-Role Cache].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-280">To use the output cache provider, first configure your cache cluster, and then configure your ASP.NET application for caching using the Caching NuGet package, as described in [Getting Started with In-Role Cache][Getting Started with In-Role Cache].</span></span> <span data-ttu-id="ee3f0-281">When the Caching NuGet package is installed, it adds the following commented out section in web.config that contains the required configuration for your ASP.NET application to use the Output Cache Provider for In-Role Cache.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-281">When the Caching NuGet package is installed, it adds the following commented out section in web.config that contains the required configuration for your ASP.NET application to use the Output Cache Provider for In-Role Cache.</span></span>

    <!--Uncomment this section to use In-Role Cache for output caching
    <caching>
      <outputCache defaultProvider="AFCacheOutputCacheProvider">
        <providers>
          <add name="AFCacheOutputCacheProvider" 
            type="Microsoft.Web.DistributedCache.DistributedCacheOutputCacheProvider,
                  Microsoft.Web.DistributedCache" 
            cacheName="default" 
            dataCacheClientName="default" />
        </providers>
      </outputCache>
    </caching>-->

> <span data-ttu-id="ee3f0-282">If your web.config does not contain this commented out section after installing the Caching NuGet package, ensure that the latest NuGet Package Manager is installed from [NuGet Package Manager Installation][NuGet Package Manager Installation], and then uninstall and reinstall the package.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-282">If your web.config does not contain this commented out section after installing the Caching NuGet package, ensure that the latest NuGet Package Manager is installed from [NuGet Package Manager Installation][NuGet Package Manager Installation], and then uninstall and reinstall the package.</span></span>
> 
> 

<span data-ttu-id="ee3f0-283">To enable the Output Cache Provider for In-Role Cache, uncomment the specified section.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-283">To enable the Output Cache Provider for In-Role Cache, uncomment the specified section.</span></span> <span data-ttu-id="ee3f0-284">The default cache is specified in the provided snippet.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-284">The default cache is specified in the provided snippet.</span></span> <span data-ttu-id="ee3f0-285">To use a different cache, specify the desired cache in the **cacheName** attribute.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-285">To use a different cache, specify the desired cache in the **cacheName** attribute.</span></span>

<span data-ttu-id="ee3f0-286">Add an **OutputCache** directive to each page for which you wish to cache the output.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-286">Add an **OutputCache** directive to each page for which you wish to cache the output.</span></span>

    <%@ OutputCache Duration="60" VaryByParam="*" %>

<span data-ttu-id="ee3f0-287">In this example the cached page data will remain in the cache for 60 seconds, and a different version of the page will be cached for each parameter combination.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-287">In this example the cached page data will remain in the cache for 60 seconds, and a different version of the page will be cached for each parameter combination.</span></span> <span data-ttu-id="ee3f0-288">For more information on the available options, see [OutputCache Directive][OutputCache Directive].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-288">For more information on the available options, see [OutputCache Directive][OutputCache Directive].</span></span>

<span data-ttu-id="ee3f0-289">For more information about using the Output Cache Provider for In-Role Cache, see [Output Cache Provider for In-Role Cache][Output Cache Provider for In-Role Cache].</span><span class="sxs-lookup"><span data-stu-id="ee3f0-289">For more information about using the Output Cache Provider for In-Role Cache, see [Output Cache Provider for In-Role Cache][Output Cache Provider for In-Role Cache].</span></span>

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="ee3f0-290">Next Steps</span><span class="sxs-lookup"><span data-stu-id="ee3f0-290">Next Steps</span></span>
<span data-ttu-id="ee3f0-291">Now that you've learned the basics of In-Role Cache, follow these links to learn how to do more complex caching tasks.</span><span class="sxs-lookup"><span data-stu-id="ee3f0-291">Now that you've learned the basics of In-Role Cache, follow these links to learn how to do more complex caching tasks.</span></span>

* <span data-ttu-id="ee3f0-292">See the MSDN Reference: [In-Role Cache][In-Role Cache]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-292">See the MSDN Reference: [In-Role Cache][In-Role Cache]</span></span>
* <span data-ttu-id="ee3f0-293">Learn how to migrate to In-Role Cache: [Migrate to In-Role Cache][Migrate to In-Role Cache]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-293">Learn how to migrate to In-Role Cache: [Migrate to In-Role Cache][Migrate to In-Role Cache]</span></span>
* <span data-ttu-id="ee3f0-294">Check out the samples: [In-Role Cache Samples][In-Role Cache Samples]</span><span class="sxs-lookup"><span data-stu-id="ee3f0-294">Check out the samples: [In-Role Cache Samples][In-Role Cache Samples]</span></span>
* <span data-ttu-id="ee3f0-295">Watch the [Maximum Performance: Accelerate Your Cloud Services Applications with Azure Caching][Maximum Performance: Accelerate Your Cloud Services Applications with Azure Caching] session from TechEd 2013 on In-Role Cache</span><span class="sxs-lookup"><span data-stu-id="ee3f0-295">Watch the [Maximum Performance: Accelerate Your Cloud Services Applications with Azure Caching][Maximum Performance: Accelerate Your Cloud Services Applications with Azure Caching] session from TechEd 2013 on In-Role Cache</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[What is In-Role Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Getting Started with the In-Role Cache Service]: #getting-started-cache-service
[Prepare Your Visual Studio Project to Use In-Role Cache]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Getting Started with In-Role Cache]: #getting-started-cache-role-instance
[Configure the cache cluster]: #enable-caching
[Configure the desired cache size]: #cache-size
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[How To: Create a DataCache Object]: #create-cache-object
[How To: Add and Retrieve an Object from the Cache]: #add-object
[How To: Specify the Expiration of an Object in the Cache]: #specify-expiration
[How To: Store ASP.NET Session State in the Cache]: #store-session
[How To: Store ASP.NET Page Output Caching in the Cache]: #store-page
[Target a Supported .NET Framework Profile]: #prepare-vs-target-net

<!-- IMAGES --> 
[RoleCache1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache8.png
[RoleCache2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache9.png
[RoleCache3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache10.png
[RoleCache4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache11.png
[RoleCache5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache12.png
[RoleCache6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache13.png
[RoleCache7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache14.png
[RoleCache8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache15.png
[RoleCache10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cache/media/cache-dotnet-how-to-use-in-role/cache17.png

<!-- LINKS -->
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[In-Role Cache Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=252651
[In-Role Cache Samples]: http://msdn.microsoft.com/library/jj189876.aspx
[In-Role Cache]: http://go.microsoft.com/fwlink/?LinkId=252658
[In-Role Cache]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[Maximum Performance: Accelerate Your Cloud Services Applications with Azure Caching]: http://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/WAD-B326#fbid=kmrzkRxQ6gU
[Migrate to In-Role Cache]: http://msdn.microsoft.com/library/hh914163.aspx
[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Output Cache Provider for In-Role Cache]: http://msdn.microsoft.com/library/windowsazure/gg185662.aspx
[OutputCache Directive]: http://go.microsoft.com/fwlink/?LinkId=251979
[Overview of In-Role Cache]: http://go.microsoft.com/fwlink/?LinkId=254172
[Session State Provider for In-Role Cache]: http://msdn.microsoft.com/library/windowsazure/gg185668.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Troubleshooting and Diagnostics for In-Role Cache]: http://msdn.microsoft.com/library/windowsazure/hh914135.aspx
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx

[Which Azure Cache offering is right for me?]: cache-faq.md#which-azure-cache-offering-is-right-for-me










