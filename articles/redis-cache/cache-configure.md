---
title: How to configure Azure Redis Cache | Microsoft Docs
description: Understand the default Redis configuration for Azure Redis Cache and learn how to configure your Azure Redis Cache instances
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 594edc9ca91f514c44ccf400841d760267c0bc04
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550285"
---
# <a name="how-to-configure-azure-redis-cache"></a><span data-ttu-id="391c2-103">How to configure Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="391c2-103">How to configure Azure Redis Cache</span></span>
<span data-ttu-id="391c2-104">This topic describes how to review and update the configuration for your Azure Redis Cache instances, and covers the default Redis server configuration for Azure Redis Cache instances.</span><span class="sxs-lookup"><span data-stu-id="391c2-104">This topic describes how to review and update the configuration for your Azure Redis Cache instances, and covers the default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="391c2-105">For more information on configuring and using premium cache features, see [How to configure persistence](cache-how-to-premium-persistence.md), [How to configure clustering](cache-how-to-premium-clustering.md), and [How to configure Virtual Network support](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-105">For more information on configuring and using premium cache features, see [How to configure persistence](cache-how-to-premium-persistence.md), [How to configure clustering](cache-how-to-premium-clustering.md), and [How to configure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="391c2-106">Configure Redis cache settings</span><span class="sxs-lookup"><span data-stu-id="391c2-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="391c2-107">Azure Redis Cache settings are viewed and configured on the **Redis Cache** blade using the **Resource Menu**.</span><span class="sxs-lookup"><span data-stu-id="391c2-107">Azure Redis Cache settings are viewed and configured on the **Redis Cache** blade using the **Resource Menu**.</span></span>

![Redis Cache Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="391c2-109">You can view and configure the following settings using the **Resource Menu**.</span><span class="sxs-lookup"><span data-stu-id="391c2-109">You can view and configure the following settings using the **Resource Menu**.</span></span>

* [<span data-ttu-id="391c2-110">Overview</span><span class="sxs-lookup"><span data-stu-id="391c2-110">Overview</span></span>](#overview)
* [<span data-ttu-id="391c2-111">Activity log</span><span class="sxs-lookup"><span data-stu-id="391c2-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="391c2-112">Access control (IAM)</span><span class="sxs-lookup"><span data-stu-id="391c2-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="391c2-113">Tags</span><span class="sxs-lookup"><span data-stu-id="391c2-113">Tags</span></span>](#tags)
* [<span data-ttu-id="391c2-114">Diagnose and solve problems</span><span class="sxs-lookup"><span data-stu-id="391c2-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="391c2-115">Settings</span><span class="sxs-lookup"><span data-stu-id="391c2-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="391c2-116">Access keys</span><span class="sxs-lookup"><span data-stu-id="391c2-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="391c2-117">Advanced settings</span><span class="sxs-lookup"><span data-stu-id="391c2-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="391c2-118">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="391c2-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="391c2-119">Scale</span><span class="sxs-lookup"><span data-stu-id="391c2-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="391c2-120">Redis cluster size</span><span class="sxs-lookup"><span data-stu-id="391c2-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="391c2-121">Redis data persistence</span><span class="sxs-lookup"><span data-stu-id="391c2-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="391c2-122">Schedule updates</span><span class="sxs-lookup"><span data-stu-id="391c2-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="391c2-123">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="391c2-123">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="391c2-124">Firewall</span><span class="sxs-lookup"><span data-stu-id="391c2-124">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="391c2-125">Properties</span><span class="sxs-lookup"><span data-stu-id="391c2-125">Properties</span></span>](#properties)
    * [<span data-ttu-id="391c2-126">Locks</span><span class="sxs-lookup"><span data-stu-id="391c2-126">Locks</span></span>](#locks)
    * [<span data-ttu-id="391c2-127">Automation script</span><span class="sxs-lookup"><span data-stu-id="391c2-127">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="391c2-128">Administration</span><span class="sxs-lookup"><span data-stu-id="391c2-128">Administration</span></span>](#administration)
    * [<span data-ttu-id="391c2-129">Import data</span><span class="sxs-lookup"><span data-stu-id="391c2-129">Import data</span></span>](#importexport)
    * [<span data-ttu-id="391c2-130">Export data</span><span class="sxs-lookup"><span data-stu-id="391c2-130">Export data</span></span>](#importexport)
    * [<span data-ttu-id="391c2-131">Reboot</span><span class="sxs-lookup"><span data-stu-id="391c2-131">Reboot</span></span>](#reboot)
* [<span data-ttu-id="391c2-132">Monitoring</span><span class="sxs-lookup"><span data-stu-id="391c2-132">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="391c2-133">Redis metrics</span><span class="sxs-lookup"><span data-stu-id="391c2-133">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="391c2-134">Alert rules</span><span class="sxs-lookup"><span data-stu-id="391c2-134">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="391c2-135">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="391c2-135">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="391c2-136">Support & troubleshooting settings</span><span class="sxs-lookup"><span data-stu-id="391c2-136">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="391c2-137">Resource health</span><span class="sxs-lookup"><span data-stu-id="391c2-137">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="391c2-138">New support request</span><span class="sxs-lookup"><span data-stu-id="391c2-138">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="391c2-139">Overview</span><span class="sxs-lookup"><span data-stu-id="391c2-139">Overview</span></span>

<span data-ttu-id="391c2-140">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span><span class="sxs-lookup"><span data-stu-id="391c2-140">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="391c2-141">Activity log</span><span class="sxs-lookup"><span data-stu-id="391c2-141">Activity log</span></span>

<span data-ttu-id="391c2-142">Click **Activity log** to view actions performed on your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-142">Click **Activity log** to view actions performed on your cache.</span></span> <span data-ttu-id="391c2-143">You can also use filtering to expand this view to include other resources.</span><span class="sxs-lookup"><span data-stu-id="391c2-143">You can also use filtering to expand this view to include other resources.</span></span> <span data-ttu-id="391c2-144">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-144">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="391c2-145">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="391c2-145">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="391c2-146">Access control (IAM)</span><span class="sxs-lookup"><span data-stu-id="391c2-146">Access control (IAM)</span></span>

<span data-ttu-id="391c2-147">The **Access control (IAM)** section provides support for role-based access control (RBAC) in the Azure portal to help organizations meet their access management requirements simply and precisely.</span><span class="sxs-lookup"><span data-stu-id="391c2-147">The **Access control (IAM)** section provides support for role-based access control (RBAC) in the Azure portal to help organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="391c2-148">For more information, see [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-148">For more information, see [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="391c2-149">Tags</span><span class="sxs-lookup"><span data-stu-id="391c2-149">Tags</span></span>

<span data-ttu-id="391c2-150">The **Tags** section helps you organize your resources.</span><span class="sxs-lookup"><span data-stu-id="391c2-150">The **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="391c2-151">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-151">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="391c2-152">Diagnose and solve problems</span><span class="sxs-lookup"><span data-stu-id="391c2-152">Diagnose and solve problems</span></span>

<span data-ttu-id="391c2-153">Click **Diagnose and solve problems** to be provided with common issues and strategies for resolving them.</span><span class="sxs-lookup"><span data-stu-id="391c2-153">Click **Diagnose and solve problems** to be provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="391c2-154">Settings</span><span class="sxs-lookup"><span data-stu-id="391c2-154">Settings</span></span>
<span data-ttu-id="391c2-155">The **Settings** section allows you to access and configure the following settings for your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-155">The **Settings** section allows you to access and configure the following settings for your cache.</span></span>

![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-general-settings.png)

* [<span data-ttu-id="391c2-157">Access keys</span><span class="sxs-lookup"><span data-stu-id="391c2-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="391c2-158">Advanced settings</span><span class="sxs-lookup"><span data-stu-id="391c2-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="391c2-159">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="391c2-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="391c2-160">Scale</span><span class="sxs-lookup"><span data-stu-id="391c2-160">Scale</span></span>](#scale)
* [<span data-ttu-id="391c2-161">Redis cluster size</span><span class="sxs-lookup"><span data-stu-id="391c2-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="391c2-162">Redis data persistence</span><span class="sxs-lookup"><span data-stu-id="391c2-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="391c2-163">Schedule updates</span><span class="sxs-lookup"><span data-stu-id="391c2-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="391c2-164">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="391c2-164">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="391c2-165">Firewall</span><span class="sxs-lookup"><span data-stu-id="391c2-165">Firewall</span></span>](#firewall)
* [<span data-ttu-id="391c2-166">Properties</span><span class="sxs-lookup"><span data-stu-id="391c2-166">Properties</span></span>](#properties)
* [<span data-ttu-id="391c2-167">Locks</span><span class="sxs-lookup"><span data-stu-id="391c2-167">Locks</span></span>](#locks)
* [<span data-ttu-id="391c2-168">Automation script</span><span class="sxs-lookup"><span data-stu-id="391c2-168">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="391c2-169">Access keys</span><span class="sxs-lookup"><span data-stu-id="391c2-169">Access keys</span></span>
<span data-ttu-id="391c2-170">Click **Access keys** to view or regenerate the access keys for your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-170">Click **Access keys** to view or regenerate the access keys for your cache.</span></span> <span data-ttu-id="391c2-171">These keys are used by the clients connecting to your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-171">These keys are used by the clients connecting to your cache.</span></span>

![Redis Cache Access Keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="391c2-173">Advanced settings</span><span class="sxs-lookup"><span data-stu-id="391c2-173">Advanced settings</span></span>
<span data-ttu-id="391c2-174">The following settings are configured on the **Advanced settings** blade.</span><span class="sxs-lookup"><span data-stu-id="391c2-174">The following settings are configured on the **Advanced settings** blade.</span></span>

* [<span data-ttu-id="391c2-175">Access Ports</span><span class="sxs-lookup"><span data-stu-id="391c2-175">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="391c2-176">Maxmemory-policy and maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="391c2-176">Maxmemory-policy and maxmemory-reserved</span></span>](#maxmemory-policy-and-maxmemory-reserved)
* [<span data-ttu-id="391c2-177">Keyspace notifications (advanced settings)</span><span class="sxs-lookup"><span data-stu-id="391c2-177">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="391c2-178">Access Ports</span><span class="sxs-lookup"><span data-stu-id="391c2-178">Access Ports</span></span>
<span data-ttu-id="391c2-179">By default, non-SSL access is disabled for new caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-179">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="391c2-180">To enable the non-SSL port, click **No** for **Allow access only via SSL** on the **Advanced settings** blade and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="391c2-180">To enable the non-SSL port, click **No** for **Allow access only via SSL** on the **Advanced settings** blade and then click **Save**.</span></span>

![Redis Cache Access Ports](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-access-ports.png)

#### <a name="maxmemory-policy-and-maxmemory-reserved"></a><span data-ttu-id="391c2-182">Maxmemory-policy and maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="391c2-182">Maxmemory-policy and maxmemory-reserved</span></span>
<span data-ttu-id="391c2-183">The **Maxmemory policy** and **maxmemory-reserved** settings on the **Advanced settings** blade configure the memory policies for the cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-183">The **Maxmemory policy** and **maxmemory-reserved** settings on the **Advanced settings** blade configure the memory policies for the cache.</span></span> <span data-ttu-id="391c2-184">The **maxmemory-policy** setting configures the eviction policy for the cache and **maxmemory-reserved** configures the memory reserved for non-cache processes.</span><span class="sxs-lookup"><span data-stu-id="391c2-184">The **maxmemory-policy** setting configures the eviction policy for the cache and **maxmemory-reserved** configures the memory reserved for non-cache processes.</span></span>

![Redis Cache Maxmemory Policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="391c2-186">**Maxmemory policy** allows you to choose from the following eviction policies:</span><span class="sxs-lookup"><span data-stu-id="391c2-186">**Maxmemory policy** allows you to choose from the following eviction policies:</span></span>

* <span data-ttu-id="391c2-187">`volatile-lru` - this is the default.</span><span class="sxs-lookup"><span data-stu-id="391c2-187">`volatile-lru` - this is the default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="391c2-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="391c2-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="391c2-189">The **maxmemory-reserved** setting configures the amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span><span class="sxs-lookup"><span data-stu-id="391c2-189">The **maxmemory-reserved** setting configures the amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="391c2-190">It can also be used when you have a high fragmentation ratio.</span><span class="sxs-lookup"><span data-stu-id="391c2-190">It can also be used when you have a high fragmentation ratio.</span></span> <span data-ttu-id="391c2-191">Setting this value allows you to have a more consistent Redis server experience when your load varies.</span><span class="sxs-lookup"><span data-stu-id="391c2-191">Setting this value allows you to have a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="391c2-192">This value should be set higher for workloads that are write heavy.</span><span class="sxs-lookup"><span data-stu-id="391c2-192">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="391c2-193">When memory is reserved for such operations, it is unavailable for storage of cached data.</span><span class="sxs-lookup"><span data-stu-id="391c2-193">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391c2-194">The **maxmemory-reserved** setting is only available for Standard and Premium caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-194">The **maxmemory-reserved** setting is only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="391c2-195">Keyspace notifications (advanced settings)</span><span class="sxs-lookup"><span data-stu-id="391c2-195">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="391c2-196">Redis keyspace notifications are configured on the **Advanced settings** blade.</span><span class="sxs-lookup"><span data-stu-id="391c2-196">Redis keyspace notifications are configured on the **Advanced settings** blade.</span></span> <span data-ttu-id="391c2-197">Keyspace notifications allow clients to receive notifications when certain events occur.</span><span class="sxs-lookup"><span data-stu-id="391c2-197">Keyspace notifications allow clients to receive notifications when certain events occur.</span></span>

![Redis Cache Advanced Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="391c2-199">Keyspace notifications and the **notify-keyspace-events** setting are only available for Standard and Premium caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-199">Keyspace notifications and the **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="391c2-200">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="391c2-200">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="391c2-201">For sample code, see the [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in the [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span><span class="sxs-lookup"><span data-stu-id="391c2-201">For sample code, see the [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in the [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="391c2-202">Redis Cache Advisor</span><span class="sxs-lookup"><span data-stu-id="391c2-202">Redis Cache Advisor</span></span>
<span data-ttu-id="391c2-203">The **Redis Cache Advisor** blade displays recommendations for your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-203">The **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="391c2-204">During normal operations, no recommendations are displayed.</span><span class="sxs-lookup"><span data-stu-id="391c2-204">During normal operations, no recommendations are displayed.</span></span> 

![Recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="391c2-206">If any conditions occur during the operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on the **Redis Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="391c2-206">If any conditions occur during the operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on the **Redis Cache** blade.</span></span>

![Recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="391c2-208">Further information can be found on the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="391c2-208">Further information can be found on the **Recommendations** blade.</span></span>

![Recommendations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="391c2-210">You can monitor these metrics on the [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of the **Redis Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="391c2-210">You can monitor these metrics on the [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of the **Redis Cache** blade.</span></span>

<span data-ttu-id="391c2-211">Each pricing tier has different limits for client connections, memory, and bandwidth.</span><span class="sxs-lookup"><span data-stu-id="391c2-211">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="391c2-212">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span><span class="sxs-lookup"><span data-stu-id="391c2-212">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="391c2-213">For more information about the metrics and limits reviewed by the **Recommendations** tool, see the following table:</span><span class="sxs-lookup"><span data-stu-id="391c2-213">For more information about the metrics and limits reviewed by the **Recommendations** tool, see the following table:</span></span>

| <span data-ttu-id="391c2-214">Redis Cache metric</span><span class="sxs-lookup"><span data-stu-id="391c2-214">Redis Cache metric</span></span> | <span data-ttu-id="391c2-215">More information</span><span class="sxs-lookup"><span data-stu-id="391c2-215">More information</span></span> |
| --- | --- |
| <span data-ttu-id="391c2-216">Network bandwidth usage</span><span class="sxs-lookup"><span data-stu-id="391c2-216">Network bandwidth usage</span></span> |[<span data-ttu-id="391c2-217">Cache performance - available bandwidth</span><span class="sxs-lookup"><span data-stu-id="391c2-217">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="391c2-218">Connected clients</span><span class="sxs-lookup"><span data-stu-id="391c2-218">Connected clients</span></span> |[<span data-ttu-id="391c2-219">Default Redis server configuration - maxclients</span><span class="sxs-lookup"><span data-stu-id="391c2-219">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="391c2-220">Server load</span><span class="sxs-lookup"><span data-stu-id="391c2-220">Server load</span></span> |[<span data-ttu-id="391c2-221">Usage charts - Redis Server Load</span><span class="sxs-lookup"><span data-stu-id="391c2-221">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="391c2-222">Memory usage</span><span class="sxs-lookup"><span data-stu-id="391c2-222">Memory usage</span></span> |[<span data-ttu-id="391c2-223">Cache performance - size</span><span class="sxs-lookup"><span data-stu-id="391c2-223">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="391c2-224">To upgrade your cache, click **Upgrade now** to change the pricing tier and [scale](#scale) your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-224">To upgrade your cache, click **Upgrade now** to change the pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="391c2-225">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="391c2-225">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="391c2-226">Scale</span><span class="sxs-lookup"><span data-stu-id="391c2-226">Scale</span></span>
<span data-ttu-id="391c2-227">Click **Scale** to view or change the pricing tier for your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-227">Click **Scale** to view or change the pricing tier for your cache.</span></span> <span data-ttu-id="391c2-228">For more information on scaling, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-228">For more information on scaling, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Redis Cache pricing tier](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="391c2-230">Redis Cluster Size</span><span class="sxs-lookup"><span data-stu-id="391c2-230">Redis Cluster Size</span></span>
<span data-ttu-id="391c2-231">Click **(PREVIEW) Redis Cluster Size** to change the cluster size for a running premium cache with clustering enabled.</span><span class="sxs-lookup"><span data-stu-id="391c2-231">Click **(PREVIEW) Redis Cluster Size** to change the cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="391c2-232">Note that while the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="391c2-232">Note that while the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Redis cluster size](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="391c2-234">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span><span class="sxs-lookup"><span data-stu-id="391c2-234">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391c2-235">Redis clustering is only available for Premium caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-235">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="391c2-236">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-236">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="391c2-237">Redis data persistence</span><span class="sxs-lookup"><span data-stu-id="391c2-237">Redis data persistence</span></span>
<span data-ttu-id="391c2-238">Click **Redis data persistence** to enable, disable, or configure data persistence for your premium cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-238">Click **Redis data persistence** to enable, disable, or configure data persistence for your premium cache.</span></span>

![Redis data persistence](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-persistence-settings.png)

<span data-ttu-id="391c2-240">To enable Redis persistence, click **Enabled** to enable RDB (Redis database) backup.</span><span class="sxs-lookup"><span data-stu-id="391c2-240">To enable Redis persistence, click **Enabled** to enable RDB (Redis database) backup.</span></span> <span data-ttu-id="391c2-241">To disable Redis persistence, click **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="391c2-241">To disable Redis persistence, click **Disabled**.</span></span>

<span data-ttu-id="391c2-242">To configure the backup interval, select one of the following **Backup Frequency** entries from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="391c2-242">To configure the backup interval, select one of the following **Backup Frequency** entries from the drop-down list.</span></span> 

- <span data-ttu-id="391c2-243">**15 Minutes**</span><span class="sxs-lookup"><span data-stu-id="391c2-243">**15 Minutes**</span></span>
- <span data-ttu-id="391c2-244">**30 minutes**</span><span class="sxs-lookup"><span data-stu-id="391c2-244">**30 minutes**</span></span>
- <span data-ttu-id="391c2-245">**60 minutes**</span><span class="sxs-lookup"><span data-stu-id="391c2-245">**60 minutes**</span></span>
- <span data-ttu-id="391c2-246">**6 hours**</span><span class="sxs-lookup"><span data-stu-id="391c2-246">**6 hours**</span></span>
- <span data-ttu-id="391c2-247">**12 hours**</span><span class="sxs-lookup"><span data-stu-id="391c2-247">**12 hours**</span></span>
- <span data-ttu-id="391c2-248">**24 hours**</span><span class="sxs-lookup"><span data-stu-id="391c2-248">**24 hours**</span></span>

<span data-ttu-id="391c2-249">The backup interval starts counting down after the previous backup operation successfully completes, and when it elapses a new backup is initiated.</span><span class="sxs-lookup"><span data-stu-id="391c2-249">The backup interval starts counting down after the previous backup operation successfully completes, and when it elapses a new backup is initiated.</span></span>

<span data-ttu-id="391c2-250">Click **Storage Account** to select the storage account to use, and choose either the **Primary key** or **Secondary key** to use from the **Storage Key** drop-down.</span><span class="sxs-lookup"><span data-stu-id="391c2-250">Click **Storage Account** to select the storage account to use, and choose either the **Primary key** or **Secondary key** to use from the **Storage Key** drop-down.</span></span> <span data-ttu-id="391c2-251">You must choose a storage account in the same region as the cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span><span class="sxs-lookup"><span data-stu-id="391c2-251">You must choose a storage account in the same region as the cache, and a **Premium Storage** account is recommended because premium storage has higher throughput.</span></span> <span data-ttu-id="391c2-252">Anytime the storage key for your persistence account is regenerated, you must rechoose the desired key from the **Storage Key** drop-down.</span><span class="sxs-lookup"><span data-stu-id="391c2-252">Anytime the storage key for your persistence account is regenerated, you must rechoose the desired key from the **Storage Key** drop-down.</span></span>

<span data-ttu-id="391c2-253">Click **OK** to save the persistence configuration.</span><span class="sxs-lookup"><span data-stu-id="391c2-253">Click **OK** to save the persistence configuration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391c2-254">Redis data persistence is only available for Premium caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-254">Redis data persistence is only available for Premium caches.</span></span> <span data-ttu-id="391c2-255">For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-255">For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="391c2-256">Schedule updates</span><span class="sxs-lookup"><span data-stu-id="391c2-256">Schedule updates</span></span>
<span data-ttu-id="391c2-257">The **Schedule updates** blade allows you to designate a maintenance window for Redis server updates for your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-257">The **Schedule updates** blade allows you to designate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="391c2-258">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-258">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![Schedule updates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="391c2-260">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="391c2-260">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="391c2-261">Note that the maintenance window time is in UTC.</span><span class="sxs-lookup"><span data-stu-id="391c2-261">Note that the maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="391c2-262">The **Schedule updates** functionality is only available for Premium tier caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-262">The **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="391c2-263">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="391c2-263">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 



### <a name="virtual-network"></a><span data-ttu-id="391c2-264">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="391c2-264">Virtual Network</span></span>
<span data-ttu-id="391c2-265">The **Virtual Network** section allows you to configure the virtual network settings for your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-265">The **Virtual Network** section allows you to configure the virtual network settings for your cache.</span></span> <span data-ttu-id="391c2-266">For information on creating a premium cache with VNET support and updating its settings, see [How to configure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-266">For information on creating a premium cache with VNET support and updating its settings, see [How to configure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391c2-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span><span class="sxs-lookup"><span data-stu-id="391c2-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="391c2-268">Firewall</span><span class="sxs-lookup"><span data-stu-id="391c2-268">Firewall</span></span>

<span data-ttu-id="391c2-269">Click **Firewall** to view and configure firewall rules for your Premium Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-269">Click **Firewall** to view and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Firewall](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="391c2-271">You can specify firewall rules with a start and end IP address range.</span><span class="sxs-lookup"><span data-stu-id="391c2-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="391c2-272">When firewall rules are configured, only client connections from the specified IP address ranges can connect to the cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-272">When firewall rules are configured, only client connections from the specified IP address ranges can connect to the cache.</span></span> <span data-ttu-id="391c2-273">When a firewall rule is saved there is a short delay before the rule is effective.</span><span class="sxs-lookup"><span data-stu-id="391c2-273">When a firewall rule is saved there is a short delay before the rule is effective.</span></span> <span data-ttu-id="391c2-274">This delay is typically less than one minute.</span><span class="sxs-lookup"><span data-stu-id="391c2-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391c2-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span><span class="sxs-lookup"><span data-stu-id="391c2-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="391c2-276">Firewall rules are only available for Premium tier caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="391c2-277">Properties</span><span class="sxs-lookup"><span data-stu-id="391c2-277">Properties</span></span>
<span data-ttu-id="391c2-278">Click **Properties** to view information about your cache, including the cache endpoint and ports.</span><span class="sxs-lookup"><span data-stu-id="391c2-278">Click **Properties** to view information about your cache, including the cache endpoint and ports.</span></span>

![Redis Cache Properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="391c2-280">Locks</span><span class="sxs-lookup"><span data-stu-id="391c2-280">Locks</span></span>
<span data-ttu-id="391c2-281">The **Locks** section allows you to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span><span class="sxs-lookup"><span data-stu-id="391c2-281">The **Locks** section allows you to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="391c2-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="391c2-283">Automation script</span><span class="sxs-lookup"><span data-stu-id="391c2-283">Automation script</span></span>

<span data-ttu-id="391c2-284">Click **Automation script** to build and export a template of your deployed resources for future deployments.</span><span class="sxs-lookup"><span data-stu-id="391c2-284">Click **Automation script** to build and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="391c2-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="391c2-286">Administration settings</span><span class="sxs-lookup"><span data-stu-id="391c2-286">Administration settings</span></span>
<span data-ttu-id="391c2-287">The settings in the **Administration** section allow you to perform the following administrative tasks for your premium cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-287">The settings in the **Administration** section allow you to perform the following administrative tasks for your premium cache.</span></span> 

![Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="391c2-289">Import data</span><span class="sxs-lookup"><span data-stu-id="391c2-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="391c2-290">Export data</span><span class="sxs-lookup"><span data-stu-id="391c2-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="391c2-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="391c2-291">Reboot</span></span>](#reboot)


> [!IMPORTANT]
> <span data-ttu-id="391c2-292">The settings in this section are only available for Premium tier caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-292">The settings in this section are only available for Premium tier caches.</span></span>
> 
> 

### <a name="importexport"></a><span data-ttu-id="391c2-293">Import/Export</span><span class="sxs-lookup"><span data-stu-id="391c2-293">Import/Export</span></span>
<span data-ttu-id="391c2-294">Import/Export is an Azure Redis Cache data management operation, which allows you to import and export data in the cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span><span class="sxs-lookup"><span data-stu-id="391c2-294">Import/Export is an Azure Redis Cache data management operation, which allows you to import and export data in the cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span></span> <span data-ttu-id="391c2-295">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span><span class="sxs-lookup"><span data-stu-id="391c2-295">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="391c2-296">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span><span class="sxs-lookup"><span data-stu-id="391c2-296">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="391c2-297">Importing data is an easy way to create a cache with pre-populated data.</span><span class="sxs-lookup"><span data-stu-id="391c2-297">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="391c2-298">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory, and then inserts the keys into the cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-298">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory, and then inserts the keys into the cache.</span></span>

<span data-ttu-id="391c2-299">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB files.</span><span class="sxs-lookup"><span data-stu-id="391c2-299">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB files.</span></span> <span data-ttu-id="391c2-300">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span><span class="sxs-lookup"><span data-stu-id="391c2-300">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="391c2-301">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span><span class="sxs-lookup"><span data-stu-id="391c2-301">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="391c2-302">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span><span class="sxs-lookup"><span data-stu-id="391c2-302">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391c2-303">Import/Export is only available for Premium tier caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-303">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="391c2-304">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-304">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="391c2-305">Reboot</span><span class="sxs-lookup"><span data-stu-id="391c2-305">Reboot</span></span>
<span data-ttu-id="391c2-306">The **Reboot** blade allows you to reboot the nodes of your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-306">The **Reboot** blade allows you to reboot the nodes of your cache.</span></span> <span data-ttu-id="391c2-307">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span><span class="sxs-lookup"><span data-stu-id="391c2-307">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="391c2-309">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span><span class="sxs-lookup"><span data-stu-id="391c2-309">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![Reboot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="391c2-311">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span><span class="sxs-lookup"><span data-stu-id="391c2-311">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="391c2-312">If you have a premium cache with clustering enabled, select the shard(s) to reboot and then click **Reboot**.</span><span class="sxs-lookup"><span data-stu-id="391c2-312">If you have a premium cache with clustering enabled, select the shard(s) to reboot and then click **Reboot**.</span></span> <span data-ttu-id="391c2-313">After a few minutes, the selected node(s) reboot, and are back online a few minutes later.</span><span class="sxs-lookup"><span data-stu-id="391c2-313">After a few minutes, the selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391c2-314">Reboot is only available for Premium tier caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-314">Reboot is only available for Premium tier caches.</span></span> <span data-ttu-id="391c2-315">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="391c2-315">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="391c2-316">Monitoring</span><span class="sxs-lookup"><span data-stu-id="391c2-316">Monitoring</span></span>

<span data-ttu-id="391c2-317">The **Monitoring** section allows you to configure diagnostics and monitoring for your Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-317">The **Monitoring** section allows you to configure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="391c2-318">For more information on Azure Redis Cache monitoring and diagnostics, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-318">For more information on Azure Redis Cache monitoring and diagnostics, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="391c2-320">Redis metrics</span><span class="sxs-lookup"><span data-stu-id="391c2-320">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="391c2-321">Alert rules</span><span class="sxs-lookup"><span data-stu-id="391c2-321">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="391c2-322">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="391c2-322">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="391c2-323">Redis metrics</span><span class="sxs-lookup"><span data-stu-id="391c2-323">Redis metrics</span></span>
<span data-ttu-id="391c2-324">Click **Redis metrics** to [view metrics](cache-how-to-monitor.md#how-to-view-metrics-and-customize-charts) for your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-324">Click **Redis metrics** to [view metrics](cache-how-to-monitor.md#how-to-view-metrics-and-customize-charts) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="391c2-325">Alert rules</span><span class="sxs-lookup"><span data-stu-id="391c2-325">Alert rules</span></span>

<span data-ttu-id="391c2-326">Click **Alert rules** to configure alerts based on Redis Cache metrics.</span><span class="sxs-lookup"><span data-stu-id="391c2-326">Click **Alert rules** to configure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="391c2-327">For more information, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="391c2-327">For more information, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="391c2-328">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="391c2-328">Diagnostics</span></span>

<span data-ttu-id="391c2-329">Click **Diagnostics** to [configure the storage account](cache-how-to-monitor.md#enable-cache-diagnostics) used to store cache diagnostics.</span><span class="sxs-lookup"><span data-stu-id="391c2-329">Click **Diagnostics** to [configure the storage account](cache-how-to-monitor.md#enable-cache-diagnostics) used to store cache diagnostics.</span></span>

![Redis Cache Diagnostics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-diagnostics-settings.png)

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="391c2-331">Support & troubleshooting settings</span><span class="sxs-lookup"><span data-stu-id="391c2-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="391c2-332">The settings in the **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-332">The settings in the **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Support + troubleshooting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="391c2-334">Resource health</span><span class="sxs-lookup"><span data-stu-id="391c2-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="391c2-335">New support request</span><span class="sxs-lookup"><span data-stu-id="391c2-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="391c2-336">Resource health</span><span class="sxs-lookup"><span data-stu-id="391c2-336">Resource health</span></span>
<span data-ttu-id="391c2-337">**Resource health** watches your resource and tells you if it's running as expected.</span><span class="sxs-lookup"><span data-stu-id="391c2-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="391c2-338">For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-338">For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="391c2-339">Resource health is currently unable to report on the health of Azure Redis Cache instances hosted in a virtual network.</span><span class="sxs-lookup"><span data-stu-id="391c2-339">Resource health is currently unable to report on the health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="391c2-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="391c2-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="391c2-341">New support request</span><span class="sxs-lookup"><span data-stu-id="391c2-341">New support request</span></span>
<span data-ttu-id="391c2-342">Click **New support request** to open a support request for your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-342">Click **New support request** to open a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="391c2-343">Default Redis server configuration</span><span class="sxs-lookup"><span data-stu-id="391c2-343">Default Redis server configuration</span></span>
<span data-ttu-id="391c2-344">New Azure Redis Cache instances are configured with the following default Redis configuration values.</span><span class="sxs-lookup"><span data-stu-id="391c2-344">New Azure Redis Cache instances are configured with the following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="391c2-345">The settings in this section cannot be changed using the `StackExchange.Redis.IServer.ConfigSet` method.</span><span class="sxs-lookup"><span data-stu-id="391c2-345">The settings in this section cannot be changed using the `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="391c2-346">If this method is called with one of the commands in this section, an exception similar to the following is thrown:</span><span class="sxs-lookup"><span data-stu-id="391c2-346">If this method is called with one of the commands in this section, an exception similar to the following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="391c2-347">Any values that are configurable, such as **max-memory-policy**, are configurable through the Azure portal or command-line management tools such as Azure CLI or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="391c2-347">Any values that are configurable, such as **max-memory-policy**, are configurable through the Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="391c2-348">Setting</span><span class="sxs-lookup"><span data-stu-id="391c2-348">Setting</span></span> | <span data-ttu-id="391c2-349">Default value</span><span class="sxs-lookup"><span data-stu-id="391c2-349">Default value</span></span> | <span data-ttu-id="391c2-350">Description</span><span class="sxs-lookup"><span data-stu-id="391c2-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="391c2-351">16</span><span class="sxs-lookup"><span data-stu-id="391c2-351">16</span></span> |<span data-ttu-id="391c2-352">The default number of databases is 16 but you can configure a different number based on the pricing tier.<sup>1</sup> The default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="391c2-352">The default number of databases is 16 but you can configure a different number based on the pricing tier.<sup>1</sup> The default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="391c2-353">Depends on the pricing tier<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="391c2-353">Depends on the pricing tier<sup>2</sup></span></span> |<span data-ttu-id="391c2-354">This is the maximum number of connected clients allowed at the same time.</span><span class="sxs-lookup"><span data-stu-id="391c2-354">This is the maximum number of connected clients allowed at the same time.</span></span> <span data-ttu-id="391c2-355">Once the limit is reached Redis closes all the new connections, returning a 'max number of clients reached' error.</span><span class="sxs-lookup"><span data-stu-id="391c2-355">Once the limit is reached Redis closes all the new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="391c2-356">Maxmemory policy is the setting for how Redis selects what to remove when `maxmemory` (the size of the cache offering you selected when you created the cache) is reached.</span><span class="sxs-lookup"><span data-stu-id="391c2-356">Maxmemory policy is the setting for how Redis selects what to remove when `maxmemory` (the size of the cache offering you selected when you created the cache) is reached.</span></span> <span data-ttu-id="391c2-357">With Azure Redis Cache the default setting is `volatile-lru`, which removes the keys with an expiration set using an LRU algorithm.</span><span class="sxs-lookup"><span data-stu-id="391c2-357">With Azure Redis Cache the default setting is `volatile-lru`, which removes the keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="391c2-358">This setting can be configured in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="391c2-358">This setting can be configured in the Azure portal.</span></span> <span data-ttu-id="391c2-359">For more information, see [Maxmemory-policy and maxmemory-reserved](#maxmemory-policy-and-maxmemory-reserved).</span><span class="sxs-lookup"><span data-stu-id="391c2-359">For more information, see [Maxmemory-policy and maxmemory-reserved](#maxmemory-policy-and-maxmemory-reserved).</span></span> |
| <span data-ttu-id="391c2-360">`maxmemory-sample`s</span><span class="sxs-lookup"><span data-stu-id="391c2-360">`maxmemory-sample`s</span></span> |<span data-ttu-id="391c2-361">3</span><span class="sxs-lookup"><span data-stu-id="391c2-361">3</span></span> |<span data-ttu-id="391c2-362">To save memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span><span class="sxs-lookup"><span data-stu-id="391c2-362">To save memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="391c2-363">By default Redis checks three keys and picks the one that was used less recently.</span><span class="sxs-lookup"><span data-stu-id="391c2-363">By default Redis checks three keys and picks the one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="391c2-364">5,000</span><span class="sxs-lookup"><span data-stu-id="391c2-364">5,000</span></span> |<span data-ttu-id="391c2-365">Max execution time of a Lua script in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="391c2-365">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="391c2-366">If the maximum execution time is reached, Redis logs that a script is still in execution after the maximum allowed time, and starts to reply to queries with an error.</span><span class="sxs-lookup"><span data-stu-id="391c2-366">If the maximum execution time is reached, Redis logs that a script is still in execution after the maximum allowed time, and starts to reply to queries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="391c2-367">500</span><span class="sxs-lookup"><span data-stu-id="391c2-367">500</span></span> |<span data-ttu-id="391c2-368">Max size of script event queue.</span><span class="sxs-lookup"><span data-stu-id="391c2-368">Max size of script event queue.</span></span> |
| <span data-ttu-id="391c2-369">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="391c2-369">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="391c2-370">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="391c2-370">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="391c2-371">The client output buffer limits can be used to force disconnection of clients that are not reading data from the server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as the publisher can produce them).</span><span class="sxs-lookup"><span data-stu-id="391c2-371">The client output buffer limits can be used to force disconnection of clients that are not reading data from the server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as the publisher can produce them).</span></span> <span data-ttu-id="391c2-372">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="391c2-372">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<a name="databases"></a>
<span data-ttu-id="391c2-373"><sup>1</sup>The limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span><span class="sxs-lookup"><span data-stu-id="391c2-373"><sup>1</sup>The limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="391c2-374">If no `databases` setting is specified during cache creation, the default is 16.</span><span class="sxs-lookup"><span data-stu-id="391c2-374">If no `databases` setting is specified during cache creation, the default is 16.</span></span>

* <span data-ttu-id="391c2-375">Basic and Standard caches</span><span class="sxs-lookup"><span data-stu-id="391c2-375">Basic and Standard caches</span></span>
  * <span data-ttu-id="391c2-376">C0 (250 MB) cache - up to 16 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-376">C0 (250 MB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="391c2-377">C1 (1 GB) cache - up to 16 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-377">C1 (1 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="391c2-378">C2 (2.5 GB) cache - up to 16 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-378">C2 (2.5 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="391c2-379">C3 (6 GB) cache - up to 16 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-379">C3 (6 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="391c2-380">C4 (13 GB) cache - up to 32 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-380">C4 (13 GB) cache - up to 32 databases</span></span>
  * <span data-ttu-id="391c2-381">C5 (26 GB) cache - up to 48 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-381">C5 (26 GB) cache - up to 48 databases</span></span>
  * <span data-ttu-id="391c2-382">C6 (53 GB) cache - up to 64 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-382">C6 (53 GB) cache - up to 64 databases</span></span>
* <span data-ttu-id="391c2-383">Premium caches</span><span class="sxs-lookup"><span data-stu-id="391c2-383">Premium caches</span></span>
  * <span data-ttu-id="391c2-384">P1 (6 GB - 60 GB) - up to 16 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-384">P1 (6 GB - 60 GB) - up to 16 databases</span></span>
  * <span data-ttu-id="391c2-385">P2 (13 GB - 130 GB) - up to 32 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-385">P2 (13 GB - 130 GB) - up to 32 databases</span></span>
  * <span data-ttu-id="391c2-386">P3 (26 GB - 260 GB) - up to 48 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-386">P3 (26 GB - 260 GB) - up to 48 databases</span></span>
  * <span data-ttu-id="391c2-387">P4 (53 GB - 530 GB) - up to 64 databases</span><span class="sxs-lookup"><span data-stu-id="391c2-387">P4 (53 GB - 530 GB) - up to 64 databases</span></span>
  * <span data-ttu-id="391c2-388">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so the `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and the [Select](http://redis.io/commands/select) command is not allowed.</span><span class="sxs-lookup"><span data-stu-id="391c2-388">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so the `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and the [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="391c2-389">For more information, see [Do I need to make any changes to my client application to use clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="391c2-389">For more information, see [Do I need to make any changes to my client application to use clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="391c2-390">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="391c2-390">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="391c2-391">The `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span><span class="sxs-lookup"><span data-stu-id="391c2-391">The `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="391c2-392">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="391c2-392">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<a name="maxclients"></a>
<span data-ttu-id="391c2-393"><sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span><span class="sxs-lookup"><span data-stu-id="391c2-393"><sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="391c2-394">Basic and Standard caches</span><span class="sxs-lookup"><span data-stu-id="391c2-394">Basic and Standard caches</span></span>
  * <span data-ttu-id="391c2-395">C0 (250 MB) cache - up to 256 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-395">C0 (250 MB) cache - up to 256 connections</span></span>
  * <span data-ttu-id="391c2-396">C1 (1 GB) cache - up to 1,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-396">C1 (1 GB) cache - up to 1,000 connections</span></span>
  * <span data-ttu-id="391c2-397">C2 (2.5 GB) cache - up to 2,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-397">C2 (2.5 GB) cache - up to 2,000 connections</span></span>
  * <span data-ttu-id="391c2-398">C3 (6 GB) cache - up to 5,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-398">C3 (6 GB) cache - up to 5,000 connections</span></span>
  * <span data-ttu-id="391c2-399">C4 (13 GB) cache - up to 10,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-399">C4 (13 GB) cache - up to 10,000 connections</span></span>
  * <span data-ttu-id="391c2-400">C5 (26 GB) cache - up to 15,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-400">C5 (26 GB) cache - up to 15,000 connections</span></span>
  * <span data-ttu-id="391c2-401">C6 (53 GB) cache - up to 20,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-401">C6 (53 GB) cache - up to 20,000 connections</span></span>
* <span data-ttu-id="391c2-402">Premium caches</span><span class="sxs-lookup"><span data-stu-id="391c2-402">Premium caches</span></span>
  * <span data-ttu-id="391c2-403">P1 (6 GB - 60 GB) - up to 7,500 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-403">P1 (6 GB - 60 GB) - up to 7,500 connections</span></span>
  * <span data-ttu-id="391c2-404">P2 (13 GB - 130 GB) - up to 15,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-404">P2 (13 GB - 130 GB) - up to 15,000 connections</span></span>
  * <span data-ttu-id="391c2-405">P3 (26 GB - 260 GB) - up to 30,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-405">P3 (26 GB - 260 GB) - up to 30,000 connections</span></span>
  * <span data-ttu-id="391c2-406">P4 (53 GB - 530 GB) - up to 40,000 connections</span><span class="sxs-lookup"><span data-stu-id="391c2-406">P4 (53 GB - 530 GB) - up to 40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="391c2-407">While each size of cache allows *up to* a certain number of connections, each connection to Redis has overhead associated with it.</span><span class="sxs-lookup"><span data-stu-id="391c2-407">While each size of cache allows *up to* a certain number of connections, each connection to Redis has overhead associated with it.</span></span> <span data-ttu-id="391c2-408">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span><span class="sxs-lookup"><span data-stu-id="391c2-408">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="391c2-409">The maximum connection limit for a given cache size assumes a lightly loaded cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-409">The maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="391c2-410">If load from connection overhead *plus* load from client operations exceeds capacity for the system, the cache can experience capacity issues even if you have not exceeded the connection limit for the current cache size.</span><span class="sxs-lookup"><span data-stu-id="391c2-410">If load from connection overhead *plus* load from client operations exceeds capacity for the system, the cache can experience capacity issues even if you have not exceeded the connection limit for the current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="391c2-411">Redis commands not supported in Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="391c2-411">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="391c2-412">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, the following commands are disabled.</span><span class="sxs-lookup"><span data-stu-id="391c2-412">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, the following commands are disabled.</span></span> <span data-ttu-id="391c2-413">If you try to invoke them, you receive an error message similar to `"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="391c2-413">If you try to invoke them, you receive an error message similar to `"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="391c2-414">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="391c2-414">BGREWRITEAOF</span></span>
> * <span data-ttu-id="391c2-415">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="391c2-415">BGSAVE</span></span>
> * <span data-ttu-id="391c2-416">CONFIG</span><span class="sxs-lookup"><span data-stu-id="391c2-416">CONFIG</span></span>
> * <span data-ttu-id="391c2-417">DEBUG</span><span class="sxs-lookup"><span data-stu-id="391c2-417">DEBUG</span></span>
> * <span data-ttu-id="391c2-418">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="391c2-418">MIGRATE</span></span>
> * <span data-ttu-id="391c2-419">SAVE</span><span class="sxs-lookup"><span data-stu-id="391c2-419">SAVE</span></span>
> * <span data-ttu-id="391c2-420">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="391c2-420">SHUTDOWN</span></span>
> * <span data-ttu-id="391c2-421">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="391c2-421">SLAVEOF</span></span>
> * <span data-ttu-id="391c2-422">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span><span class="sxs-lookup"><span data-stu-id="391c2-422">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="391c2-423">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="391c2-423">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="391c2-424">Redis console</span><span class="sxs-lookup"><span data-stu-id="391c2-424">Redis console</span></span>
<span data-ttu-id="391c2-425">You can securely issue commands to your Azure Redis Cache instances using the **Redis Console**, which is available for Standard and Premium caches.</span><span class="sxs-lookup"><span data-stu-id="391c2-425">You can securely issue commands to your Azure Redis Cache instances using the **Redis Console**, which is available for Standard and Premium caches.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="391c2-426">The Redis Console does not work with VNET, clustering, and databases other than 0.</span><span class="sxs-lookup"><span data-stu-id="391c2-426">The Redis Console does not work with VNET, clustering, and databases other than 0.</span></span> 
> 
> * <span data-ttu-id="391c2-427">[VNET](cache-how-to-premium-vnet.md) - When your cache is part of a VNET, only clients in the VNET can access the cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-427">[VNET](cache-how-to-premium-vnet.md) - When your cache is part of a VNET, only clients in the VNET can access the cache.</span></span> <span data-ttu-id="391c2-428">Because the Redis Console uses the redis-cli.exe client hosted on VMs that are not part of your VNET, it can't connect to your cache.</span><span class="sxs-lookup"><span data-stu-id="391c2-428">Because the Redis Console uses the redis-cli.exe client hosted on VMs that are not part of your VNET, it can't connect to your cache.</span></span>
> * <span data-ttu-id="391c2-429">[Clustering](cache-how-to-premium-clustering.md) - The Redis Console uses the redis-cli.exe client, which does not currently support clustering.</span><span class="sxs-lookup"><span data-stu-id="391c2-429">[Clustering](cache-how-to-premium-clustering.md) - The Redis Console uses the redis-cli.exe client, which does not currently support clustering.</span></span> <span data-ttu-id="391c2-430">The redis-cli utility in the [unstable](http://redis.io/download) branch of the Redis repository at GitHub implements basic support when started with the `-c` switch.</span><span class="sxs-lookup"><span data-stu-id="391c2-430">The redis-cli utility in the [unstable](http://redis.io/download) branch of the Redis repository at GitHub implements basic support when started with the `-c` switch.</span></span> <span data-ttu-id="391c2-431">For more information, see [Playing with the cluster](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) on [http://redis.io](http://redis.io) in the [Redis cluster tutorial](http://redis.io/topics/cluster-tutorial).</span><span class="sxs-lookup"><span data-stu-id="391c2-431">For more information, see [Playing with the cluster](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) on [http://redis.io](http://redis.io) in the [Redis cluster tutorial](http://redis.io/topics/cluster-tutorial).</span></span>
> * <span data-ttu-id="391c2-432">The Redis Console makes a new connection to database 0 each time you submit a command.</span><span class="sxs-lookup"><span data-stu-id="391c2-432">The Redis Console makes a new connection to database 0 each time you submit a command.</span></span> <span data-ttu-id="391c2-433">You can't use the `SELECT` command to select a different database, because the database is reset to 0 with each command.</span><span class="sxs-lookup"><span data-stu-id="391c2-433">You can't use the `SELECT` command to select a different database, because the database is reset to 0 with each command.</span></span> <span data-ttu-id="391c2-434">For information on running Redis commands, including changing to a different database, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="391c2-434">For information on running Redis commands, including changing to a different database, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>
> 
> 

<span data-ttu-id="391c2-435">To access the Redis Console, click **Console** from the **Redis Cache** blade.</span><span class="sxs-lookup"><span data-stu-id="391c2-435">To access the Redis Console, click **Console** from the **Redis Cache** blade.</span></span>

![Redis console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-console-menu.png)

<span data-ttu-id="391c2-437">To issue commands against your cache instance, simply type in the desired command into the console.</span><span class="sxs-lookup"><span data-stu-id="391c2-437">To issue commands against your cache instance, simply type in the desired command into the console.</span></span>

![Redis console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-console.png)

<span data-ttu-id="391c2-439">For list of Redis commands that are disabled for Azure Redis Cache, see the previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span><span class="sxs-lookup"><span data-stu-id="391c2-439">For list of Redis commands that are disabled for Azure Redis Cache, see the previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="391c2-440">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="391c2-440">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span> 

## <a name="move-your-cache-to-a-new-subscription"></a><span data-ttu-id="391c2-441">Move your cache to a new subscription</span><span class="sxs-lookup"><span data-stu-id="391c2-441">Move your cache to a new subscription</span></span>
<span data-ttu-id="391c2-442">You can move your cache to a new subscription by clicking **Move**.</span><span class="sxs-lookup"><span data-stu-id="391c2-442">You can move your cache to a new subscription by clicking **Move**.</span></span>

![Move Redis Cache](https://docstestmedia1.blob.core.windows.net/azure-media/articles/redis-cache/media/cache-configure/redis-cache-move.png)

<span data-ttu-id="391c2-444">For information on moving resources from one resource group to another, and from one subscription to another, see [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="391c2-444">For information on moving resources from one resource group to another, and from one subscription to another, see [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="391c2-445">Next steps</span><span class="sxs-lookup"><span data-stu-id="391c2-445">Next steps</span></span>
* <span data-ttu-id="391c2-446">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="391c2-446">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

























