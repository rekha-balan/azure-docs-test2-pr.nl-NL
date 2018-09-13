---
title: How to administer Azure Redis Cache | Microsoft Docs
description: Learn how to perform administration tasks such as reboot and schedule updates for Azure Redis Cache
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: c716f157cdf3de1a0907256117c0986f067225a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551556"
---
# <a name="how-to-administer-azure-redis-cache"></a><span data-ttu-id="724f1-103">How to administer Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="724f1-103">How to administer Azure Redis Cache</span></span>
<span data-ttu-id="724f1-104">This topic describes how to perform administration tasks such as [rebooting](#reboot) and [scheduling updates](#schedule-updates) for your Azure Redis Cache instances.</span><span class="sxs-lookup"><span data-stu-id="724f1-104">This topic describes how to perform administration tasks such as [rebooting](#reboot) and [scheduling updates](#schedule-updates) for your Azure Redis Cache instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="724f1-105">The settings and features described in this article are only available for Premium tier caches.</span><span class="sxs-lookup"><span data-stu-id="724f1-105">The settings and features described in this article are only available for Premium tier caches.</span></span>
> 
> 

## <a name="reboot"></a><span data-ttu-id="724f1-106">Reboot</span><span class="sxs-lookup"><span data-stu-id="724f1-106">Reboot</span></span>
<span data-ttu-id="724f1-107">The **Reboot** blade allows you to reboot one or more nodes of your cache.</span><span class="sxs-lookup"><span data-stu-id="724f1-107">The **Reboot** blade allows you to reboot one or more nodes of your cache.</span></span> <span data-ttu-id="724f1-108">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span><span class="sxs-lookup"><span data-stu-id="724f1-108">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-administration/redis-cache-administration-reboot.png)

<span data-ttu-id="724f1-110">Select the nodes to reboot and click **Reboot**.</span><span class="sxs-lookup"><span data-stu-id="724f1-110">Select the nodes to reboot and click **Reboot**.</span></span>

![Reboot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-administration/redis-cache-reboot.png)

<span data-ttu-id="724f1-112">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span><span class="sxs-lookup"><span data-stu-id="724f1-112">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![Reboot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-administration/redis-cache-reboot-cluster.png)

<span data-ttu-id="724f1-114">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span><span class="sxs-lookup"><span data-stu-id="724f1-114">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="724f1-115">If you have a premium cache with clustering enabled, select the desired shards to reboot and then click **Reboot**.</span><span class="sxs-lookup"><span data-stu-id="724f1-115">If you have a premium cache with clustering enabled, select the desired shards to reboot and then click **Reboot**.</span></span> <span data-ttu-id="724f1-116">After a few minutes, the selected nodes reboot, and are back online a few minutes later.</span><span class="sxs-lookup"><span data-stu-id="724f1-116">After a few minutes, the selected nodes reboot, and are back online a few minutes later.</span></span>

<span data-ttu-id="724f1-117">The impact on client applications varies depending on which nodes that you reboot.</span><span class="sxs-lookup"><span data-stu-id="724f1-117">The impact on client applications varies depending on which nodes that you reboot.</span></span>

* <span data-ttu-id="724f1-118">**Master** - When the master node is rebooted, Azure Redis Cache fails over to the replica node and promotes it to master.</span><span class="sxs-lookup"><span data-stu-id="724f1-118">**Master** - When the master node is rebooted, Azure Redis Cache fails over to the replica node and promotes it to master.</span></span> <span data-ttu-id="724f1-119">During this failover, there may be a short interval in which connections may fail to the cache.</span><span class="sxs-lookup"><span data-stu-id="724f1-119">During this failover, there may be a short interval in which connections may fail to the cache.</span></span>
* <span data-ttu-id="724f1-120">**Slave** - When the slave node is rebooted, there is typically no impact to cache clients.</span><span class="sxs-lookup"><span data-stu-id="724f1-120">**Slave** - When the slave node is rebooted, there is typically no impact to cache clients.</span></span>
* <span data-ttu-id="724f1-121">**Both master and slave** - When both cache nodes are rebooted, all data is lost in the cache and connections to the cache fail until the primary node comes back online.</span><span class="sxs-lookup"><span data-stu-id="724f1-121">**Both master and slave** - When both cache nodes are rebooted, all data is lost in the cache and connections to the cache fail until the primary node comes back online.</span></span> <span data-ttu-id="724f1-122">If you have configured [data persistence](cache-how-to-premium-persistence.md), the most recent backup is restored when the cache comes back online, but any cache writes that occurred after the most recent backup are lost.</span><span class="sxs-lookup"><span data-stu-id="724f1-122">If you have configured [data persistence](cache-how-to-premium-persistence.md), the most recent backup is restored when the cache comes back online, but any cache writes that occurred after the most recent backup are lost.</span></span>
* <span data-ttu-id="724f1-123">**Nodes of a premium cache with clustering enabled** - When you reboot one or more nodes of a premium cache with clustering enabled, the behavior for the selected nodes is the same as when you reboot the corresponding node or nodes of a non-clustered cache.</span><span class="sxs-lookup"><span data-stu-id="724f1-123">**Nodes of a premium cache with clustering enabled** - When you reboot one or more nodes of a premium cache with clustering enabled, the behavior for the selected nodes is the same as when you reboot the corresponding node or nodes of a non-clustered cache.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="724f1-124">Reboot is only available for Premium tier caches.</span><span class="sxs-lookup"><span data-stu-id="724f1-124">Reboot is only available for Premium tier caches.</span></span>
> 
> 

## <a name="reboot-faq"></a><span data-ttu-id="724f1-125">Reboot FAQ</span><span class="sxs-lookup"><span data-stu-id="724f1-125">Reboot FAQ</span></span>
* [<span data-ttu-id="724f1-126">Which node should I reboot to test my application?</span><span class="sxs-lookup"><span data-stu-id="724f1-126">Which node should I reboot to test my application?</span></span>](#which-node-should-i-reboot-to-test-my-application)
* [<span data-ttu-id="724f1-127">Can I reboot the cache to clear client connections?</span><span class="sxs-lookup"><span data-stu-id="724f1-127">Can I reboot the cache to clear client connections?</span></span>](#can-i-reboot-the-cache-to-clear-client-connections)
* [<span data-ttu-id="724f1-128">Will I lose data from my cache if I do a reboot?</span><span class="sxs-lookup"><span data-stu-id="724f1-128">Will I lose data from my cache if I do a reboot?</span></span>](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [<span data-ttu-id="724f1-129">Can I reboot my cache using PowerShell, CLI, or other management tools?</span><span class="sxs-lookup"><span data-stu-id="724f1-129">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="724f1-130">What pricing tiers can use the reboot functionality?</span><span class="sxs-lookup"><span data-stu-id="724f1-130">What pricing tiers can use the reboot functionality?</span></span>](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-to-test-my-application"></a><span data-ttu-id="724f1-131">Which node should I reboot to test my application?</span><span class="sxs-lookup"><span data-stu-id="724f1-131">Which node should I reboot to test my application?</span></span>
<span data-ttu-id="724f1-132">To test the resiliency of your application against failure of the primary node of your cache, reboot the **Master** node.</span><span class="sxs-lookup"><span data-stu-id="724f1-132">To test the resiliency of your application against failure of the primary node of your cache, reboot the **Master** node.</span></span> <span data-ttu-id="724f1-133">To test the resiliency of your application against failure of the secondary node, reboot the **Slave** node.</span><span class="sxs-lookup"><span data-stu-id="724f1-133">To test the resiliency of your application against failure of the secondary node, reboot the **Slave** node.</span></span> <span data-ttu-id="724f1-134">To test the resiliency of your application against total failure of the cache, reboot **Both** nodes.</span><span class="sxs-lookup"><span data-stu-id="724f1-134">To test the resiliency of your application against total failure of the cache, reboot **Both** nodes.</span></span>

### <a name="can-i-reboot-the-cache-to-clear-client-connections"></a><span data-ttu-id="724f1-135">Can I reboot the cache to clear client connections?</span><span class="sxs-lookup"><span data-stu-id="724f1-135">Can I reboot the cache to clear client connections?</span></span>
<span data-ttu-id="724f1-136">Yes, if you reboot the cache all client connections are cleared.</span><span class="sxs-lookup"><span data-stu-id="724f1-136">Yes, if you reboot the cache all client connections are cleared.</span></span> <span data-ttu-id="724f1-137">Rebooting can be useful in the case where all client connections are used up due to a logic error or a bug in the client application.</span><span class="sxs-lookup"><span data-stu-id="724f1-137">Rebooting can be useful in the case where all client connections are used up due to a logic error or a bug in the client application.</span></span> <span data-ttu-id="724f1-138">Each pricing tier has different [client connection limits](cache-configure.md#default-redis-server-configuration) for the various sizes, and once these limits are reached, no more client connections are accepted.</span><span class="sxs-lookup"><span data-stu-id="724f1-138">Each pricing tier has different [client connection limits](cache-configure.md#default-redis-server-configuration) for the various sizes, and once these limits are reached, no more client connections are accepted.</span></span> <span data-ttu-id="724f1-139">Rebooting the cache provides a way to clear all client connections.</span><span class="sxs-lookup"><span data-stu-id="724f1-139">Rebooting the cache provides a way to clear all client connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="724f1-140">If you reboot your cache to clear client connections, StackExchange.Redis automatically reconnects once the Redis node is back online.</span><span class="sxs-lookup"><span data-stu-id="724f1-140">If you reboot your cache to clear client connections, StackExchange.Redis automatically reconnects once the Redis node is back online.</span></span> <span data-ttu-id="724f1-141">If the underlying issue is not resolved, the client connections may continue to be used up.</span><span class="sxs-lookup"><span data-stu-id="724f1-141">If the underlying issue is not resolved, the client connections may continue to be used up.</span></span>
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a><span data-ttu-id="724f1-142">Will I lose data from my cache if I do a reboot?</span><span class="sxs-lookup"><span data-stu-id="724f1-142">Will I lose data from my cache if I do a reboot?</span></span>
<span data-ttu-id="724f1-143">If you reboot both the **Master** and **Slave** nodes, all data in the cache (or in that shard if you are using a premium cache with clustering enabled) is lost.</span><span class="sxs-lookup"><span data-stu-id="724f1-143">If you reboot both the **Master** and **Slave** nodes, all data in the cache (or in that shard if you are using a premium cache with clustering enabled) is lost.</span></span> <span data-ttu-id="724f1-144">If you have configured [data persistence](cache-how-to-premium-persistence.md), the most recent backup will be restored when the cache comes back online, but any cache writes that have occurred after the backup was made are lost.</span><span class="sxs-lookup"><span data-stu-id="724f1-144">If you have configured [data persistence](cache-how-to-premium-persistence.md), the most recent backup will be restored when the cache comes back online, but any cache writes that have occurred after the backup was made are lost.</span></span>

<span data-ttu-id="724f1-145">If you reboot just one of the nodes, data is not typically lost, but it still may be.</span><span class="sxs-lookup"><span data-stu-id="724f1-145">If you reboot just one of the nodes, data is not typically lost, but it still may be.</span></span> <span data-ttu-id="724f1-146">For example if the master node is rebooted and a cache write is in progress, the data from the cache write is lost.</span><span class="sxs-lookup"><span data-stu-id="724f1-146">For example if the master node is rebooted and a cache write is in progress, the data from the cache write is lost.</span></span> <span data-ttu-id="724f1-147">Another scenario for data loss would be if you reboot one node and the other node happens to go down due to a failure at the same time.</span><span class="sxs-lookup"><span data-stu-id="724f1-147">Another scenario for data loss would be if you reboot one node and the other node happens to go down due to a failure at the same time.</span></span> <span data-ttu-id="724f1-148">For more information about possible causes for data loss, see [What happened to my data in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span><span class="sxs-lookup"><span data-stu-id="724f1-148">For more information about possible causes for data loss, see [What happened to my data in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)</span></span>

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="724f1-149">Can I reboot my cache using PowerShell, CLI, or other management tools?</span><span class="sxs-lookup"><span data-stu-id="724f1-149">Can I reboot my cache using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="724f1-150">Yes, for PowerShell instructions see [To reboot a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="724f1-150">Yes, for PowerShell instructions see [To reboot a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).</span></span>

### <a name="what-pricing-tiers-can-use-the-reboot-functionality"></a><span data-ttu-id="724f1-151">What pricing tiers can use the reboot functionality?</span><span class="sxs-lookup"><span data-stu-id="724f1-151">What pricing tiers can use the reboot functionality?</span></span>
<span data-ttu-id="724f1-152">Reboot is available only in the premium pricing tier.</span><span class="sxs-lookup"><span data-stu-id="724f1-152">Reboot is available only in the premium pricing tier.</span></span>

## <a name="schedule-updates"></a><span data-ttu-id="724f1-153">Schedule updates</span><span class="sxs-lookup"><span data-stu-id="724f1-153">Schedule updates</span></span>
<span data-ttu-id="724f1-154">The **Schedule updates** blade allows you to designate a maintenance window for your cache.</span><span class="sxs-lookup"><span data-stu-id="724f1-154">The **Schedule updates** blade allows you to designate a maintenance window for your cache.</span></span> <span data-ttu-id="724f1-155">When the maintenance window is specified, any Redis server updates are made during this window.</span><span class="sxs-lookup"><span data-stu-id="724f1-155">When the maintenance window is specified, any Redis server updates are made during this window.</span></span> 

> [!NOTE] 
> <span data-ttu-id="724f1-156">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span><span class="sxs-lookup"><span data-stu-id="724f1-156">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![Schedule updates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-administration/redis-schedule-updates.png)

<span data-ttu-id="724f1-158">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="724f1-158">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="724f1-159">Note that the maintenance window time is in UTC.</span><span class="sxs-lookup"><span data-stu-id="724f1-159">Note that the maintenance window time is in UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="724f1-160">The default maintenance window for updates is five hours.</span><span class="sxs-lookup"><span data-stu-id="724f1-160">The default maintenance window for updates is five hours.</span></span> <span data-ttu-id="724f1-161">This value is not configurable from the Azure portal, but you can configure it in PowerShell using the `MaintenanceWindow` parameter of the [New-AzureRmRedisCacheScheduleEntry](https://docs.microsoft.com/powershell/resourcemanager/azurerm.rediscache/v2.5.0/new-azurermrediscachescheduleentry) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="724f1-161">This value is not configurable from the Azure portal, but you can configure it in PowerShell using the `MaintenanceWindow` parameter of the [New-AzureRmRedisCacheScheduleEntry](https://docs.microsoft.com/powershell/resourcemanager/azurerm.rediscache/v2.5.0/new-azurermrediscachescheduleentry) cmdlet.</span></span> <span data-ttu-id="724f1-162">For more information, see [Can I manage scheduled updates using PowerShell, CLI, or other management tools?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)</span><span class="sxs-lookup"><span data-stu-id="724f1-162">For more information, see [Can I manage scheduled updates using PowerShell, CLI, or other management tools?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)</span></span>
> 
> 

## <a name="schedule-updates-faq"></a><span data-ttu-id="724f1-163">Schedule updates FAQ</span><span class="sxs-lookup"><span data-stu-id="724f1-163">Schedule updates FAQ</span></span>
* [<span data-ttu-id="724f1-164">When do updates occur if I don't use the schedule updates feature?</span><span class="sxs-lookup"><span data-stu-id="724f1-164">When do updates occur if I don't use the schedule updates feature?</span></span>](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [<span data-ttu-id="724f1-165">What type of updates are made during the scheduled maintenance window?</span><span class="sxs-lookup"><span data-stu-id="724f1-165">What type of updates are made during the scheduled maintenance window?</span></span>](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [<span data-ttu-id="724f1-166">Can I manage scheduled updates using PowerShell, CLI, or other management tools?</span><span class="sxs-lookup"><span data-stu-id="724f1-166">Can I manage scheduled updates using PowerShell, CLI, or other management tools?</span></span>](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [<span data-ttu-id="724f1-167">What pricing tiers can use the schedule updates functionality?</span><span class="sxs-lookup"><span data-stu-id="724f1-167">What pricing tiers can use the schedule updates functionality?</span></span>](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature"></a><span data-ttu-id="724f1-168">When do updates occur if I don't use the schedule updates feature?</span><span class="sxs-lookup"><span data-stu-id="724f1-168">When do updates occur if I don't use the schedule updates feature?</span></span>
<span data-ttu-id="724f1-169">If you don't specify a maintenance window, updates can be made at any time.</span><span class="sxs-lookup"><span data-stu-id="724f1-169">If you don't specify a maintenance window, updates can be made at any time.</span></span>

### <a name="what-type-of-updates-are-made-during-the-scheduled-maintenance-window"></a><span data-ttu-id="724f1-170">What type of updates are made during the scheduled maintenance window?</span><span class="sxs-lookup"><span data-stu-id="724f1-170">What type of updates are made during the scheduled maintenance window?</span></span>
<span data-ttu-id="724f1-171">Only Redis server updates are made during the scheduled maintenance window.</span><span class="sxs-lookup"><span data-stu-id="724f1-171">Only Redis server updates are made during the scheduled maintenance window.</span></span> <span data-ttu-id="724f1-172">The maintenance window does not apply to Azure updates or updates to the VM operating system.</span><span class="sxs-lookup"><span data-stu-id="724f1-172">The maintenance window does not apply to Azure updates or updates to the VM operating system.</span></span>

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a><span data-ttu-id="724f1-173">Can I managed scheduled updates using PowerShell, CLI, or other management tools?</span><span class="sxs-lookup"><span data-stu-id="724f1-173">Can I managed scheduled updates using PowerShell, CLI, or other management tools?</span></span>
<span data-ttu-id="724f1-174">Yes, you can manage your scheduled updates using the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="724f1-174">Yes, you can manage your scheduled updates using the following PowerShell cmdlets:</span></span>

* [<span data-ttu-id="724f1-175">Get-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="724f1-175">Get-AzureRmRedisCachePatchSchedule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.rediscache/v2.5.0/get-azurermrediscachepatchschedule)
* [<span data-ttu-id="724f1-176">New-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="724f1-176">New-AzureRmRedisCachePatchSchedule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.rediscache/v2.5.0/new-azurermrediscachepatchschedule)
* [<span data-ttu-id="724f1-177">New-AzureRmRedisCacheScheduleEntry</span><span class="sxs-lookup"><span data-stu-id="724f1-177">New-AzureRmRedisCacheScheduleEntry</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.rediscache/v2.5.0/new-azurermrediscachescheduleentry)
* [<span data-ttu-id="724f1-178">Remove-AzureRmRedisCachePatchSchedule</span><span class="sxs-lookup"><span data-stu-id="724f1-178">Remove-AzureRmRedisCachePatchSchedule</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.rediscache/v2.5.0/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-the-schedule-updates-functionality"></a><span data-ttu-id="724f1-179">What pricing tiers can use the schedule updates functionality?</span><span class="sxs-lookup"><span data-stu-id="724f1-179">What pricing tiers can use the schedule updates functionality?</span></span>
<span data-ttu-id="724f1-180">The **Schedule updates** feature is only available in the premium pricing tier.</span><span class="sxs-lookup"><span data-stu-id="724f1-180">The **Schedule updates** feature is only available in the premium pricing tier.</span></span>

## <a name="next-steps"></a><span data-ttu-id="724f1-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="724f1-181">Next steps</span></span>
* <span data-ttu-id="724f1-182">Explore more [Azure Redis Cache premium tier](cache-premium-tier-intro.md) features.</span><span class="sxs-lookup"><span data-stu-id="724f1-182">Explore more [Azure Redis Cache premium tier](cache-premium-tier-intro.md) features.</span></span>





