---
title: How to Scale Azure Redis Cache | Microsoft Docs
description: Learn how to scale your Azure Redis Cache instances
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: cb5cfab6b87225273c54701449829d4424205742
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661930"
---
# <a name="how-to-scale-azure-redis-cache"></a><span data-ttu-id="7b1b2-103">How to Scale Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="7b1b2-103">How to Scale Azure Redis Cache</span></span>
<span data-ttu-id="7b1b2-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span></span> <span data-ttu-id="7b1b2-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span></span> <span data-ttu-id="7b1b2-106">This article shows you how to scale your cache in both the Azure portal and using tools such as Azure PowerShell and Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-106">This article shows you how to scale your cache in both the Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-to-scale"></a><span data-ttu-id="7b1b2-107">When to scale</span><span class="sxs-lookup"><span data-stu-id="7b1b2-107">When to scale</span></span>
<span data-ttu-id="7b1b2-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span></span> 

<span data-ttu-id="7b1b2-109">You can monitor the following metrics to help determine if you need to scale.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-109">You can monitor the following metrics to help determine if you need to scale.</span></span>

* <span data-ttu-id="7b1b2-110">Redis Server Load</span><span class="sxs-lookup"><span data-stu-id="7b1b2-110">Redis Server Load</span></span>
* <span data-ttu-id="7b1b2-111">Memory Usage</span><span class="sxs-lookup"><span data-stu-id="7b1b2-111">Memory Usage</span></span>
* <span data-ttu-id="7b1b2-112">Network Bandwidth</span><span class="sxs-lookup"><span data-stu-id="7b1b2-112">Network Bandwidth</span></span>
* <span data-ttu-id="7b1b2-113">CPU Usage</span><span class="sxs-lookup"><span data-stu-id="7b1b2-113">CPU Usage</span></span>

<span data-ttu-id="7b1b2-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="7b1b2-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="7b1b2-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="7b1b2-116">Scale a cache</span><span class="sxs-lookup"><span data-stu-id="7b1b2-116">Scale a cache</span></span>
<span data-ttu-id="7b1b2-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span></span>

![Scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="7b1b2-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span></span>

![Pricing tier][redis-cache-pricing-tier-blade]


<span data-ttu-id="7b1b2-121">You can scale to a different pricing tier with the following restrictions:</span><span class="sxs-lookup"><span data-stu-id="7b1b2-121">You can scale to a different pricing tier with the following restrictions:</span></span>

* <span data-ttu-id="7b1b2-122">You can't scale from a higher pricing tier to a lower pricing tier.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-122">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="7b1b2-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="7b1b2-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="7b1b2-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="7b1b2-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="7b1b2-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="7b1b2-128">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-128">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="7b1b2-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="7b1b2-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span></span>

![Scaling][redis-cache-scaling]

<span data-ttu-id="7b1b2-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span></span>

## <a name="how-to-automate-a-scaling-operation"></a><span data-ttu-id="7b1b2-133">How to automate a scaling operation</span><span class="sxs-lookup"><span data-stu-id="7b1b2-133">How to automate a scaling operation</span></span>
<span data-ttu-id="7b1b2-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span><span class="sxs-lookup"><span data-stu-id="7b1b2-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="7b1b2-135">Scale using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b1b2-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="7b1b2-136">Scale using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b1b2-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="7b1b2-137">Scale using MAML</span><span class="sxs-lookup"><span data-stu-id="7b1b2-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="7b1b2-138">Scale using PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b1b2-138">Scale using PowerShell</span></span>
<span data-ttu-id="7b1b2-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="7b1b2-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="7b1b2-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="7b1b2-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="7b1b2-142">Scale using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b1b2-142">Scale using Azure CLI</span></span>
<span data-ttu-id="7b1b2-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span></span>

<span data-ttu-id="7b1b2-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="7b1b2-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="7b1b2-145">Scale using MAML</span><span class="sxs-lookup"><span data-stu-id="7b1b2-145">Scale using MAML</span></span>
<span data-ttu-id="7b1b2-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span></span>

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

<span data-ttu-id="7b1b2-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="7b1b2-148">Scaling FAQ</span><span class="sxs-lookup"><span data-stu-id="7b1b2-148">Scaling FAQ</span></span>
<span data-ttu-id="7b1b2-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="7b1b2-150">Can I scale to, from, or within a Premium cache?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="7b1b2-151">After scaling, do I have to change my cache name or access keys?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-151">After scaling, do I have to change my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="7b1b2-152">How does scaling work?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="7b1b2-153">Will I lose data from my cache during scaling?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="7b1b2-154">Is my custom databases setting affected during scaling?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="7b1b2-155">Will my cache be available during scaling?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="7b1b2-156">Operations that are not supported</span><span class="sxs-lookup"><span data-stu-id="7b1b2-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="7b1b2-157">How long does scaling take?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="7b1b2-158">How can I tell when scaling is complete?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="7b1b2-159">Can I scale to, from, or within a Premium cache?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="7b1b2-160">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-160">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="7b1b2-161">You can scale from one **Premium** cache pricing tier to another.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-161">You can scale from one **Premium** cache pricing tier to another.</span></span>
* <span data-ttu-id="7b1b2-162">You can't scale from a **Basic** cache directly to a **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-162">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="7b1b2-163">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-163">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="7b1b2-164">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="7b1b2-164">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="7b1b2-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="7b1b2-166">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="7b1b2-166">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-to-change-my-cache-name-or-access-keys"></a><span data-ttu-id="7b1b2-167">After scaling, do I have to change my cache name or access keys?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-167">After scaling, do I have to change my cache name or access keys?</span></span>
<span data-ttu-id="7b1b2-168">No, your cache name and keys are unchanged during a scaling operation.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="7b1b2-169">How does scaling work?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-169">How does scaling work?</span></span>
* <span data-ttu-id="7b1b2-170">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-170">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span></span> <span data-ttu-id="7b1b2-171">During this time, the cache is unavailable and all data in the cache is lost.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-171">During this time, the cache is unavailable and all data in the cache is lost.</span></span>
* <span data-ttu-id="7b1b2-172">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-172">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span></span> <span data-ttu-id="7b1b2-173">The cache remains available during the scaling process.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-173">The cache remains available during the scaling process.</span></span>
* <span data-ttu-id="7b1b2-174">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and re-provisioned to the new size and the data transferred over, and then the other replica performs a failover before it is re-provisioned, similar to the process that occurs during a failure of one of the cache nodes.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-174">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and re-provisioned to the new size and the data transferred over, and then the other replica performs a failover before it is re-provisioned, similar to the process that occurs during a failure of one of the cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="7b1b2-175">Will I lose data from my cache during scaling?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="7b1b2-176">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-176">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span></span>
* <span data-ttu-id="7b1b2-177">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-177">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span></span>
* <span data-ttu-id="7b1b2-178">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-178">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span></span> <span data-ttu-id="7b1b2-179">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-179">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span></span> <span data-ttu-id="7b1b2-180">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-180">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="7b1b2-181">Is my custom databases setting affected during scaling?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="7b1b2-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for the `databases` setting during cache creation.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="7b1b2-183">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span><span class="sxs-lookup"><span data-stu-id="7b1b2-183">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span></span>
  * <span data-ttu-id="7b1b2-184">If you are using the default number of `databases` which is 16 for all pricing tiers, no data is lost.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-184">If you are using the default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="7b1b2-185">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-185">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="7b1b2-186">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-186">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span></span>
* <span data-ttu-id="7b1b2-187">When scaling to a pricing tier with the same or higher `databases` limit than the current tier your `databases` setting is retained and no data is lost.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-187">When scaling to a pricing tier with the same or higher `databases` limit than the current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="7b1b2-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="7b1b2-189">Will my cache be available during scaling?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="7b1b2-190">**Standard** and **Premium** caches remain available during the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-190">**Standard** and **Premium** caches remain available during the scaling operation.</span></span>
* <span data-ttu-id="7b1b2-191">**Basic** caches are offline during scaling operations to a different size, but remain available when scaling from **Basic** to **Standard**.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-191">**Basic** caches are offline during scaling operations to a different size, but remain available when scaling from **Basic** to **Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="7b1b2-192">Operations that are not supported</span><span class="sxs-lookup"><span data-stu-id="7b1b2-192">Operations that are not supported</span></span>
* <span data-ttu-id="7b1b2-193">You can't scale from a higher pricing tier to a lower pricing tier.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-193">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="7b1b2-194">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-194">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="7b1b2-195">You can't scale from a **Standard** cache down to a **Basic** cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-195">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="7b1b2-196">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-196">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="7b1b2-197">If you need a different size, you can do a subsequent scaling operation to the desired size.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-197">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="7b1b2-198">You can't scale from a **Basic** cache directly to a **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-198">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="7b1b2-199">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-199">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="7b1b2-200">You can't scale from a larger size down to the **C0 (250 MB)** size.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-200">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>

<span data-ttu-id="7b1b2-201">If a scaling operation fails, the service will try to revert the operation and the cache will revert to the original size.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-201">If a scaling operation fails, the service will try to revert the operation and the cache will revert to the original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="7b1b2-202">How long does scaling take?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-202">How long does scaling take?</span></span>
<span data-ttu-id="7b1b2-203">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-203">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="7b1b2-204">How can I tell when scaling is complete?</span><span class="sxs-lookup"><span data-stu-id="7b1b2-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="7b1b2-205">In the Azure portal you can see the scaling operation in progress.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-205">In the Azure portal you can see the scaling operation in progress.</span></span> <span data-ttu-id="7b1b2-206">When scaling is complete, the status of the cache changes to **Running**.</span><span class="sxs-lookup"><span data-stu-id="7b1b2-206">When scaling is complete, the status of the cache changes to **Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-how-to-scale/redis-cache-scaling.png






