---
title: How to configure data persistence for a Premium Azure Redis Cache
description: Learn how to configure and manage data persistence your Premium tier Azure Redis Cache instances
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: sdanie
ms.openlocfilehash: 896cef11ecc84008c94a55a636c01bc51d7c03ed
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562957"
---
# <a name="how-to-configure-data-persistence-for-a-premium-azure-redis-cache"></a><span data-ttu-id="6cf05-103">How to configure data persistence for a Premium Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="6cf05-103">How to configure data persistence for a Premium Azure Redis Cache</span></span>
<span data-ttu-id="6cf05-104">Azure Redis Cache has different cache offerings which provide flexibility in the choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span><span class="sxs-lookup"><span data-stu-id="6cf05-104">Azure Redis Cache has different cache offerings which provide flexibility in the choice of cache size and features, including Premium tier features such as clustering, persistence, and virtual network support.</span></span> <span data-ttu-id="6cf05-105">This article describes how to configure persistence in a premium Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="6cf05-105">This article describes how to configure persistence in a premium Azure Redis Cache instance.</span></span>

<span data-ttu-id="6cf05-106">For information on other premium cache features, see [Introduction to the Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span><span class="sxs-lookup"><span data-stu-id="6cf05-106">For information on other premium cache features, see [Introduction to the Azure Redis Cache Premium tier](cache-premium-tier-intro.md).</span></span>

## <a name="what-is-data-persistence"></a><span data-ttu-id="6cf05-107">What is data persistence?</span><span class="sxs-lookup"><span data-stu-id="6cf05-107">What is data persistence?</span></span>
<span data-ttu-id="6cf05-108">Redis persistence allows you to persist data stored in Redis.</span><span class="sxs-lookup"><span data-stu-id="6cf05-108">Redis persistence allows you to persist data stored in Redis.</span></span> <span data-ttu-id="6cf05-109">You can also take snapshots and back up the data, which you can load in case of a hardware failure.</span><span class="sxs-lookup"><span data-stu-id="6cf05-109">You can also take snapshots and back up the data, which you can load in case of a hardware failure.</span></span> <span data-ttu-id="6cf05-110">This is a huge advantage over Basic or Standard tier where all the data is stored in memory and there can be potential data loss in case of a failure where Cache nodes are down.</span><span class="sxs-lookup"><span data-stu-id="6cf05-110">This is a huge advantage over Basic or Standard tier where all the data is stored in memory and there can be potential data loss in case of a failure where Cache nodes are down.</span></span> 

<span data-ttu-id="6cf05-111">Azure Redis Cache offers Redis persistence using the [RDB model](http://redis.io/topics/persistence), where the data is stored in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="6cf05-111">Azure Redis Cache offers Redis persistence using the [RDB model](http://redis.io/topics/persistence), where the data is stored in an Azure storage account.</span></span> <span data-ttu-id="6cf05-112">When persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span><span class="sxs-lookup"><span data-stu-id="6cf05-112">When persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span></span> <span data-ttu-id="6cf05-113">If a catastrophic event occurs that disables both the primary and replica cache, the cache is reconstructed using the most recent snapshot.</span><span class="sxs-lookup"><span data-stu-id="6cf05-113">If a catastrophic event occurs that disables both the primary and replica cache, the cache is reconstructed using the most recent snapshot.</span></span>

<span data-ttu-id="6cf05-114">Persistence can be configured from the **New Redis Cache** blade during cache creation and on the **Resource menu** for existing premium caches.</span><span class="sxs-lookup"><span data-stu-id="6cf05-114">Persistence can be configured from the **New Redis Cache** blade during cache creation and on the **Resource menu** for existing premium caches.</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

<span data-ttu-id="6cf05-115">Once a premium pricing tier is selected, click **Redis persistence**.</span><span class="sxs-lookup"><span data-stu-id="6cf05-115">Once a premium pricing tier is selected, click **Redis persistence**.</span></span>

![Redis persistence][redis-cache-persistence]

<span data-ttu-id="6cf05-117">The steps in the following section describe how to configure Redis persistence on your new premium cache.</span><span class="sxs-lookup"><span data-stu-id="6cf05-117">The steps in the following section describe how to configure Redis persistence on your new premium cache.</span></span> <span data-ttu-id="6cf05-118">Once Redis persistence is configured, click **Create** to create your new premium cache with Redis persistence.</span><span class="sxs-lookup"><span data-stu-id="6cf05-118">Once Redis persistence is configured, click **Create** to create your new premium cache with Redis persistence.</span></span>

## <a name="configure-redis-persistence"></a><span data-ttu-id="6cf05-119">Configure Redis persistence</span><span class="sxs-lookup"><span data-stu-id="6cf05-119">Configure Redis persistence</span></span>
<span data-ttu-id="6cf05-120">Redis persistence is configured on the **Redis data persistence** blade.</span><span class="sxs-lookup"><span data-stu-id="6cf05-120">Redis persistence is configured on the **Redis data persistence** blade.</span></span> <span data-ttu-id="6cf05-121">For new caches, this blade is accessed during the cache creation process, as described in the previous section.</span><span class="sxs-lookup"><span data-stu-id="6cf05-121">For new caches, this blade is accessed during the cache creation process, as described in the previous section.</span></span> <span data-ttu-id="6cf05-122">For existing caches, the **Redis data persistence** blade is accessed from the **Resource menu** for your cache.</span><span class="sxs-lookup"><span data-stu-id="6cf05-122">For existing caches, the **Redis data persistence** blade is accessed from the **Resource menu** for your cache.</span></span>

![Redis settings][redis-cache-settings]

<span data-ttu-id="6cf05-124">To enable Redis persistence, click **Enabled** to enable RDB (Redis database) backup.</span><span class="sxs-lookup"><span data-stu-id="6cf05-124">To enable Redis persistence, click **Enabled** to enable RDB (Redis database) backup.</span></span> <span data-ttu-id="6cf05-125">To disable Redis persistence on a previously enabled premium cache, click **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="6cf05-125">To disable Redis persistence on a previously enabled premium cache, click **Disabled**.</span></span>

<span data-ttu-id="6cf05-126">To configure the backup interval, select a **Backup Frequency** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="6cf05-126">To configure the backup interval, select a **Backup Frequency** from the drop-down list.</span></span> <span data-ttu-id="6cf05-127">Choices include **15 Minutes**, **30 minutes**, **60 minutes**, **6 hours**, **12 hours**, and **24 hours**.</span><span class="sxs-lookup"><span data-stu-id="6cf05-127">Choices include **15 Minutes**, **30 minutes**, **60 minutes**, **6 hours**, **12 hours**, and **24 hours**.</span></span> <span data-ttu-id="6cf05-128">This interval starts counting down after the previous backup operation successfully completes and when it elapses a new backup is initiated.</span><span class="sxs-lookup"><span data-stu-id="6cf05-128">This interval starts counting down after the previous backup operation successfully completes and when it elapses a new backup is initiated.</span></span>

<span data-ttu-id="6cf05-129">Click **Storage Account** to select the storage account to use, and choose either the **Primary key** or **Secondary key** to use from the **Storage Key** drop-down.</span><span class="sxs-lookup"><span data-stu-id="6cf05-129">Click **Storage Account** to select the storage account to use, and choose either the **Primary key** or **Secondary key** to use from the **Storage Key** drop-down.</span></span> <span data-ttu-id="6cf05-130">You must choose a storage account in the same region as the cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span><span class="sxs-lookup"><span data-stu-id="6cf05-130">You must choose a storage account in the same region as the cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6cf05-131">If the storage key for your persistence account is regenerated, you must reconfigure the desired key from the **Storage Key** drop-down.</span><span class="sxs-lookup"><span data-stu-id="6cf05-131">If the storage key for your persistence account is regenerated, you must reconfigure the desired key from the **Storage Key** drop-down.</span></span>
> 
> 

![Redis persistence][redis-cache-persistence-selected]

<span data-ttu-id="6cf05-133">Click **OK** to save the persistence configuration.</span><span class="sxs-lookup"><span data-stu-id="6cf05-133">Click **OK** to save the persistence configuration.</span></span>

<span data-ttu-id="6cf05-134">The next backup (or first backup for new caches) is initiated once the backup frequency interval elapses.</span><span class="sxs-lookup"><span data-stu-id="6cf05-134">The next backup (or first backup for new caches) is initiated once the backup frequency interval elapses.</span></span>

## <a name="persistence-faq"></a><span data-ttu-id="6cf05-135">Persistence FAQ</span><span class="sxs-lookup"><span data-stu-id="6cf05-135">Persistence FAQ</span></span>
<span data-ttu-id="6cf05-136">The following list contains answers to commonly asked questions about Azure Redis Cache persistence.</span><span class="sxs-lookup"><span data-stu-id="6cf05-136">The following list contains answers to commonly asked questions about Azure Redis Cache persistence.</span></span>

* [<span data-ttu-id="6cf05-137">Can I enable persistence on a previously created cache?</span><span class="sxs-lookup"><span data-stu-id="6cf05-137">Can I enable persistence on a previously created cache?</span></span>](#can-i-enable-persistence-on-a-previously-created-cache)
* [<span data-ttu-id="6cf05-138">Can I change the backup frequency after I create the cache?</span><span class="sxs-lookup"><span data-stu-id="6cf05-138">Can I change the backup frequency after I create the cache?</span></span>](#can-i-change-the-backup-frequency-after-i-create-the-cache)
* [<span data-ttu-id="6cf05-139">Why if I have a backup frequency of 60 minutes there is more than 60 minutes between backups?</span><span class="sxs-lookup"><span data-stu-id="6cf05-139">Why if I have a backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>](#why-if-i-have-a-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [<span data-ttu-id="6cf05-140">What happens to the old backups when a new backup is made?</span><span class="sxs-lookup"><span data-stu-id="6cf05-140">What happens to the old backups when a new backup is made?</span></span>](#what-happens-to-the-old-backups-when-a-new-backup-is-made)
* [<span data-ttu-id="6cf05-141">What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?</span><span class="sxs-lookup"><span data-stu-id="6cf05-141">What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?</span></span>](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a><span data-ttu-id="6cf05-142">Can I enable persistence on a previously created cache?</span><span class="sxs-lookup"><span data-stu-id="6cf05-142">Can I enable persistence on a previously created cache?</span></span>
<span data-ttu-id="6cf05-143">Yes, Redis persistence can be configured both at cache creation and on existing premium caches.</span><span class="sxs-lookup"><span data-stu-id="6cf05-143">Yes, Redis persistence can be configured both at cache creation and on existing premium caches.</span></span>

### <a name="can-i-change-the-backup-frequency-after-i-create-the-cache"></a><span data-ttu-id="6cf05-144">Can I change the backup frequency after I create the cache?</span><span class="sxs-lookup"><span data-stu-id="6cf05-144">Can I change the backup frequency after I create the cache?</span></span>
<span data-ttu-id="6cf05-145">Yes, you can change the backup frequency on the **Redis data persistence** blade.</span><span class="sxs-lookup"><span data-stu-id="6cf05-145">Yes, you can change the backup frequency on the **Redis data persistence** blade.</span></span> <span data-ttu-id="6cf05-146">For instructions, see [Configure Redis persistence](#configure-redis-persistence).</span><span class="sxs-lookup"><span data-stu-id="6cf05-146">For instructions, see [Configure Redis persistence](#configure-redis-persistence).</span></span>

### <a name="why-if-i-have-a-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a><span data-ttu-id="6cf05-147">Why if I have a backup frequency of 60 minutes there is more than 60 minutes between backups?</span><span class="sxs-lookup"><span data-stu-id="6cf05-147">Why if I have a backup frequency of 60 minutes there is more than 60 minutes between backups?</span></span>
<span data-ttu-id="6cf05-148">The backup frequency interval does not start until the previous backup process has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="6cf05-148">The backup frequency interval does not start until the previous backup process has completed successfully.</span></span> <span data-ttu-id="6cf05-149">If the backup frequency is 60 minutes and it takes a backup process 15 minutes to successfully complete, the next backup won't start until 75 minutes after the start time of the previous backup.</span><span class="sxs-lookup"><span data-stu-id="6cf05-149">If the backup frequency is 60 minutes and it takes a backup process 15 minutes to successfully complete, the next backup won't start until 75 minutes after the start time of the previous backup.</span></span>

### <a name="what-happens-to-the-old-backups-when-a-new-backup-is-made"></a><span data-ttu-id="6cf05-150">What happens to the old backups when a new backup is made?</span><span class="sxs-lookup"><span data-stu-id="6cf05-150">What happens to the old backups when a new backup is made?</span></span>
<span data-ttu-id="6cf05-151">All backups except for the most recent one are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="6cf05-151">All backups except for the most recent one are automatically deleted.</span></span> <span data-ttu-id="6cf05-152">This deletion may not happen immediately but older backups are not persisted indefinitely.</span><span class="sxs-lookup"><span data-stu-id="6cf05-152">This deletion may not happen immediately but older backups are not persisted indefinitely.</span></span>

### <a name="what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation"></a><span data-ttu-id="6cf05-153">What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?</span><span class="sxs-lookup"><span data-stu-id="6cf05-153">What happens if I have scaled to a different size and a backup is restored that was made before the scaling operation?</span></span>
* <span data-ttu-id="6cf05-154">If you have scaled to a larger size, there is no impact.</span><span class="sxs-lookup"><span data-stu-id="6cf05-154">If you have scaled to a larger size, there is no impact.</span></span>
* <span data-ttu-id="6cf05-155">If you have scaled to a smaller size, and you have a custom [databases](cache-configure.md#databases) setting that is greater than the [databases limit](cache-configure.md#databases) for your new size, data in those databases isn't be restored.</span><span class="sxs-lookup"><span data-stu-id="6cf05-155">If you have scaled to a smaller size, and you have a custom [databases](cache-configure.md#databases) setting that is greater than the [databases limit](cache-configure.md#databases) for your new size, data in those databases isn't be restored.</span></span> <span data-ttu-id="6cf05-156">For more information, see [Is my custom databases setting affected during scaling?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span><span class="sxs-lookup"><span data-stu-id="6cf05-156">For more information, see [Is my custom databases setting affected during scaling?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)</span></span>
* <span data-ttu-id="6cf05-157">If you have scaled to a smaller size, and there isn't enough room in the smaller size to hold all of the data from the last backup, keys will be evicted during the restore process, typically using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span><span class="sxs-lookup"><span data-stu-id="6cf05-157">If you have scaled to a smaller size, and there isn't enough room in the smaller size to hold all of the data from the last backup, keys will be evicted during the restore process, typically using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cf05-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="6cf05-158">Next steps</span></span>
<span data-ttu-id="6cf05-159">Learn how to use more premium cache features.</span><span class="sxs-lookup"><span data-stu-id="6cf05-159">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="6cf05-160">Introduction to the Azure Redis Cache Premium tier</span><span class="sxs-lookup"><span data-stu-id="6cf05-160">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-new-cache-menu]: ./media/cache-how-to-premium-persistence/redis-cache-new-cache-menu.png

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-persistence-selected]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-premium-persistence/redis-cache-persistence-selected.png

[redis-cache-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-premium-persistence/redis-cache-settings.png



