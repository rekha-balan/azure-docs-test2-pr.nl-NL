---
title: How to Scale Azure Redis Cache | Microsoft Docs
description: Learn how to scale your Azure Redis Cache instances
services: redis-cache
documentationcenter: ''
author: wesmc7777
manager: cfowler
editor: ''
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: wesmc
ms.openlocfilehash: 885258379e71ea945e41c4b43c34b35b16dd4a7a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44831077"
---
# <a name="how-to-scale-azure-redis-cache"></a><span data-ttu-id="a7332-103">How to Scale Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="a7332-103">How to Scale Azure Redis Cache</span></span>
<span data-ttu-id="a7332-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span><span class="sxs-lookup"><span data-stu-id="a7332-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span></span> <span data-ttu-id="a7332-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span><span class="sxs-lookup"><span data-stu-id="a7332-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span></span> <span data-ttu-id="a7332-106">This article shows you how to scale your cache using the Azure portal, and tools such as Azure PowerShell, and Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a7332-106">This article shows you how to scale your cache using the Azure portal, and tools such as Azure PowerShell, and Azure CLI.</span></span>

## <a name="when-to-scale"></a><span data-ttu-id="a7332-107">When to scale</span><span class="sxs-lookup"><span data-stu-id="a7332-107">When to scale</span></span>
<span data-ttu-id="a7332-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span></span> 

<span data-ttu-id="a7332-109">You can monitor the following metrics to help determine if you need to scale.</span><span class="sxs-lookup"><span data-stu-id="a7332-109">You can monitor the following metrics to help determine if you need to scale.</span></span>

* <span data-ttu-id="a7332-110">Redis Server Load</span><span class="sxs-lookup"><span data-stu-id="a7332-110">Redis Server Load</span></span>
* <span data-ttu-id="a7332-111">Memory Usage</span><span class="sxs-lookup"><span data-stu-id="a7332-111">Memory Usage</span></span>
* <span data-ttu-id="a7332-112">Network Bandwidth</span><span class="sxs-lookup"><span data-stu-id="a7332-112">Network Bandwidth</span></span>
* <span data-ttu-id="a7332-113">CPU Usage</span><span class="sxs-lookup"><span data-stu-id="a7332-113">CPU Usage</span></span>

<span data-ttu-id="a7332-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span><span class="sxs-lookup"><span data-stu-id="a7332-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="a7332-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="a7332-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="a7332-116">Scale a cache</span><span class="sxs-lookup"><span data-stu-id="a7332-116">Scale a cache</span></span>
<span data-ttu-id="a7332-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="a7332-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span></span>

![Scale](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="a7332-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="a7332-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span></span>

![Pricing tier][redis-cache-pricing-tier-blade]


<span data-ttu-id="a7332-121">You can scale to a different pricing tier with the following restrictions:</span><span class="sxs-lookup"><span data-stu-id="a7332-121">You can scale to a different pricing tier with the following restrictions:</span></span>

* <span data-ttu-id="a7332-122">You can't scale from a higher pricing tier to a lower pricing tier.</span><span class="sxs-lookup"><span data-stu-id="a7332-122">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="a7332-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="a7332-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="a7332-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span><span class="sxs-lookup"><span data-stu-id="a7332-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="a7332-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span><span class="sxs-lookup"><span data-stu-id="a7332-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="a7332-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="a7332-128">First, scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span><span class="sxs-lookup"><span data-stu-id="a7332-128">First, scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="a7332-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span><span class="sxs-lookup"><span data-stu-id="a7332-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="a7332-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="a7332-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span></span>

![Scaling][redis-cache-scaling]

<span data-ttu-id="a7332-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="a7332-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span></span>

## <a name="how-to-automate-a-scaling-operation"></a><span data-ttu-id="a7332-133">How to automate a scaling operation</span><span class="sxs-lookup"><span data-stu-id="a7332-133">How to automate a scaling operation</span></span>
<span data-ttu-id="a7332-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span><span class="sxs-lookup"><span data-stu-id="a7332-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="a7332-135">Scale using PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7332-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="a7332-136">Scale using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a7332-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="a7332-137">Scale using MAML</span><span class="sxs-lookup"><span data-stu-id="a7332-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="a7332-138">Scale using PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7332-138">Scale using PowerShell</span></span>
<span data-ttu-id="a7332-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://docs.microsoft.com/powershell/module/azurerm.rediscache/set-azurermrediscache?view=azurermps-6.6.0) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span><span class="sxs-lookup"><span data-stu-id="a7332-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://docs.microsoft.com/powershell/module/azurerm.rediscache/set-azurermrediscache?view=azurermps-6.6.0) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="a7332-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="a7332-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="a7332-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="a7332-142">Scale using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a7332-142">Scale using Azure CLI</span></span>
<span data-ttu-id="a7332-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span><span class="sxs-lookup"><span data-stu-id="a7332-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span></span>

<span data-ttu-id="a7332-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="a7332-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="a7332-145">Scale using MAML</span><span class="sxs-lookup"><span data-stu-id="a7332-145">Scale using MAML</span></span>
<span data-ttu-id="a7332-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="a7332-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting the access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // To scale, set a new size for the redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="a7332-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span><span class="sxs-lookup"><span data-stu-id="a7332-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="a7332-148">Scaling FAQ</span><span class="sxs-lookup"><span data-stu-id="a7332-148">Scaling FAQ</span></span>
<span data-ttu-id="a7332-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span><span class="sxs-lookup"><span data-stu-id="a7332-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="a7332-150">Can I scale to, from, or within a Premium cache?</span><span class="sxs-lookup"><span data-stu-id="a7332-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="a7332-151">After scaling, do I have to change my cache name or access keys?</span><span class="sxs-lookup"><span data-stu-id="a7332-151">After scaling, do I have to change my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="a7332-152">How does scaling work?</span><span class="sxs-lookup"><span data-stu-id="a7332-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="a7332-153">Will I lose data from my cache during scaling?</span><span class="sxs-lookup"><span data-stu-id="a7332-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="a7332-154">Is my custom databases setting affected during scaling?</span><span class="sxs-lookup"><span data-stu-id="a7332-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="a7332-155">Will my cache be available during scaling?</span><span class="sxs-lookup"><span data-stu-id="a7332-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="a7332-156">With Geo-replication configured, why am I not able to scale my cache or change the shards in a cluster?</span><span class="sxs-lookup"><span data-stu-id="a7332-156">With Geo-replication configured, why am I not able to scale my cache or change the shards in a cluster?</span></span>](#scaling-limitations-with-geo-relication)
* [<span data-ttu-id="a7332-157">Operations that are not supported</span><span class="sxs-lookup"><span data-stu-id="a7332-157">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="a7332-158">How long does scaling take?</span><span class="sxs-lookup"><span data-stu-id="a7332-158">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="a7332-159">How can I tell when scaling is complete?</span><span class="sxs-lookup"><span data-stu-id="a7332-159">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="a7332-160">Can I scale to, from, or within a Premium cache?</span><span class="sxs-lookup"><span data-stu-id="a7332-160">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="a7332-161">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span><span class="sxs-lookup"><span data-stu-id="a7332-161">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="a7332-162">You can scale from one **Premium** cache pricing tier to another.</span><span class="sxs-lookup"><span data-stu-id="a7332-162">You can scale from one **Premium** cache pricing tier to another.</span></span>
* <span data-ttu-id="a7332-163">You can't scale from a **Basic** cache directly to a **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-163">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="a7332-164">First, scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span><span class="sxs-lookup"><span data-stu-id="a7332-164">First, scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="a7332-165">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="a7332-165">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="a7332-166">If your cache was created without clustering enabled, you can configure clustering at a later time.</span><span class="sxs-lookup"><span data-stu-id="a7332-166">If your cache was created without clustering enabled, you can configure clustering at a later time.</span></span>
  
  <span data-ttu-id="a7332-167">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="a7332-167">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-to-change-my-cache-name-or-access-keys"></a><span data-ttu-id="a7332-168">After scaling, do I have to change my cache name or access keys?</span><span class="sxs-lookup"><span data-stu-id="a7332-168">After scaling, do I have to change my cache name or access keys?</span></span>
<span data-ttu-id="a7332-169">No, your cache name and keys are unchanged during a scaling operation.</span><span class="sxs-lookup"><span data-stu-id="a7332-169">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="a7332-170">How does scaling work?</span><span class="sxs-lookup"><span data-stu-id="a7332-170">How does scaling work?</span></span>
* <span data-ttu-id="a7332-171">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span><span class="sxs-lookup"><span data-stu-id="a7332-171">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span></span> <span data-ttu-id="a7332-172">During this time, the cache is unavailable and all data in the cache is lost.</span><span class="sxs-lookup"><span data-stu-id="a7332-172">During this time, the cache is unavailable and all data in the cache is lost.</span></span>
* <span data-ttu-id="a7332-173">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-173">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span></span> <span data-ttu-id="a7332-174">The cache remains available during the scaling process.</span><span class="sxs-lookup"><span data-stu-id="a7332-174">The cache remains available during the scaling process.</span></span>
* <span data-ttu-id="a7332-175">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and reprovisioned to the new size and the data transferred over, and then the other replica performs a failover before it is reprovisioned, similar to the process that occurs during a failure of one of the cache nodes.</span><span class="sxs-lookup"><span data-stu-id="a7332-175">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and reprovisioned to the new size and the data transferred over, and then the other replica performs a failover before it is reprovisioned, similar to the process that occurs during a failure of one of the cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="a7332-176">Will I lose data from my cache during scaling?</span><span class="sxs-lookup"><span data-stu-id="a7332-176">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="a7332-177">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="a7332-177">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span></span>
* <span data-ttu-id="a7332-178">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span><span class="sxs-lookup"><span data-stu-id="a7332-178">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span></span>
* <span data-ttu-id="a7332-179">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span><span class="sxs-lookup"><span data-stu-id="a7332-179">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span></span> <span data-ttu-id="a7332-180">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span><span class="sxs-lookup"><span data-stu-id="a7332-180">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span></span> <span data-ttu-id="a7332-181">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span><span class="sxs-lookup"><span data-stu-id="a7332-181">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="a7332-182">Is my custom databases setting affected during scaling?</span><span class="sxs-lookup"><span data-stu-id="a7332-182">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="a7332-183">If you configured a custom value for the `databases` setting during cache creation, keep in mind that some pricing tiers have different [databases limits](cache-configure.md#databases).</span><span class="sxs-lookup"><span data-stu-id="a7332-183">If you configured a custom value for the `databases` setting during cache creation, keep in mind that some pricing tiers have different [databases limits](cache-configure.md#databases).</span></span> <span data-ttu-id="a7332-184">Here are some considerations when scaling in this scenario:</span><span class="sxs-lookup"><span data-stu-id="a7332-184">Here are some considerations when scaling in this scenario:</span></span>

* <span data-ttu-id="a7332-185">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span><span class="sxs-lookup"><span data-stu-id="a7332-185">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span></span>
  * <span data-ttu-id="a7332-186">If you are using the default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span><span class="sxs-lookup"><span data-stu-id="a7332-186">If you are using the default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="a7332-187">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span><span class="sxs-lookup"><span data-stu-id="a7332-187">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="a7332-188">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span><span class="sxs-lookup"><span data-stu-id="a7332-188">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span></span>
* <span data-ttu-id="a7332-189">When scaling to a pricing tier with the same or higher `databases` limit than the current tier, your `databases` setting is retained and no data is lost.</span><span class="sxs-lookup"><span data-stu-id="a7332-189">When scaling to a pricing tier with the same or higher `databases` limit than the current tier, your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="a7332-190">While Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span><span class="sxs-lookup"><span data-stu-id="a7332-190">While Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="a7332-191">Will my cache be available during scaling?</span><span class="sxs-lookup"><span data-stu-id="a7332-191">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="a7332-192">**Standard** and **Premium** caches remain available during the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="a7332-192">**Standard** and **Premium** caches remain available during the scaling operation.</span></span> <span data-ttu-id="a7332-193">However, connection blips can occur while scaling Standard and Premium caches, and also while scaling from Basic to Standard caches.</span><span class="sxs-lookup"><span data-stu-id="a7332-193">However, connection blips can occur while scaling Standard and Premium caches, and also while scaling from Basic to Standard caches.</span></span> <span data-ttu-id="a7332-194">These connection blips are expected to be small and redis clients should be able to re-establish their connection instantly.</span><span class="sxs-lookup"><span data-stu-id="a7332-194">These connection blips are expected to be small and redis clients should be able to re-establish their connection instantly.</span></span>
* <span data-ttu-id="a7332-195">**Basic** caches are offline during scaling operations to a different size.</span><span class="sxs-lookup"><span data-stu-id="a7332-195">**Basic** caches are offline during scaling operations to a different size.</span></span> <span data-ttu-id="a7332-196">Basic caches remain available when scaling from **Basic** to **Standard** but, may experience a small connection blip.</span><span class="sxs-lookup"><span data-stu-id="a7332-196">Basic caches remain available when scaling from **Basic** to **Standard** but, may experience a small connection blip.</span></span> <span data-ttu-id="a7332-197">If a connection blip occurs, redis clients should be able to re-establish their connection instantly.</span><span class="sxs-lookup"><span data-stu-id="a7332-197">If a connection blip occurs, redis clients should be able to re-establish their connection instantly.</span></span>


### <a name="scaling-limitations-with-geo-replication"></a><span data-ttu-id="a7332-198">Scaling limitations with Geo-replication</span><span class="sxs-lookup"><span data-stu-id="a7332-198">Scaling limitations with Geo-replication</span></span>

<span data-ttu-id="a7332-199">Once you have added a Geo-replication link between two caches, you will no longer be able to initiate a scaling operation or change the number of shards in a cluster.</span><span class="sxs-lookup"><span data-stu-id="a7332-199">Once you have added a Geo-replication link between two caches, you will no longer be able to initiate a scaling operation or change the number of shards in a cluster.</span></span> <span data-ttu-id="a7332-200">You must unlink the cache to issue these commands.</span><span class="sxs-lookup"><span data-stu-id="a7332-200">You must unlink the cache to issue these commands.</span></span> <span data-ttu-id="a7332-201">For more information, see [Configure Geo-replication](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="a7332-201">For more information, see [Configure Geo-replication](cache-how-to-geo-replication.md).</span></span>


### <a name="operations-that-are-not-supported"></a><span data-ttu-id="a7332-202">Operations that are not supported</span><span class="sxs-lookup"><span data-stu-id="a7332-202">Operations that are not supported</span></span>
* <span data-ttu-id="a7332-203">You can't scale from a higher pricing tier to a lower pricing tier.</span><span class="sxs-lookup"><span data-stu-id="a7332-203">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="a7332-204">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-204">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="a7332-205">You can't scale from a **Standard** cache down to a **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-205">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="a7332-206">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span><span class="sxs-lookup"><span data-stu-id="a7332-206">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="a7332-207">If you need a different size, you can do a subsequent scaling operation to the desired size.</span><span class="sxs-lookup"><span data-stu-id="a7332-207">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="a7332-208">You can't scale from a **Basic** cache directly to a **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-208">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="a7332-209">First scale from **Basic** to **Standard** in one scaling operation, and then scale from **Standard** to **Premium** in a subsequent operation.</span><span class="sxs-lookup"><span data-stu-id="a7332-209">First scale from **Basic** to **Standard** in one scaling operation, and then scale from **Standard** to **Premium** in a subsequent operation.</span></span>
* <span data-ttu-id="a7332-210">You can't scale from a larger size down to the **C0 (250 MB)** size.</span><span class="sxs-lookup"><span data-stu-id="a7332-210">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>

<span data-ttu-id="a7332-211">If a scaling operation fails, the service tries to revert the operation, and the cache will revert to the original size.</span><span class="sxs-lookup"><span data-stu-id="a7332-211">If a scaling operation fails, the service tries to revert the operation, and the cache will revert to the original size.</span></span>


### <a name="how-long-does-scaling-take"></a><span data-ttu-id="a7332-212">How long does scaling take?</span><span class="sxs-lookup"><span data-stu-id="a7332-212">How long does scaling take?</span></span>
<span data-ttu-id="a7332-213">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span><span class="sxs-lookup"><span data-stu-id="a7332-213">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="a7332-214">How can I tell when scaling is complete?</span><span class="sxs-lookup"><span data-stu-id="a7332-214">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="a7332-215">In the Azure portal, you can see the scaling operation in progress.</span><span class="sxs-lookup"><span data-stu-id="a7332-215">In the Azure portal, you can see the scaling operation in progress.</span></span> <span data-ttu-id="a7332-216">When scaling is complete, the status of the cache changes to **Running**.</span><span class="sxs-lookup"><span data-stu-id="a7332-216">When scaling is complete, the status of the cache changes to **Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



