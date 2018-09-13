---
title: Azure Redis Cache samples | Microsoft Docs
description: Learn how to use Azure Redis Cache
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 7841fcf0b5f4dcb409abf8bfb804c2e03dad6d3a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550730"
---
# <a name="azure-redis-cache-samples"></a><span data-ttu-id="83f87-103">Azure Redis Cache samples</span><span class="sxs-lookup"><span data-stu-id="83f87-103">Azure Redis Cache samples</span></span>
<span data-ttu-id="83f87-104">This topic provides a list of Azure Redis Cache samples, covering scenarios such as connecting to a cache, reading and writing data to and from a cache, and using the ASP.NET Redis Cache providers.</span><span class="sxs-lookup"><span data-stu-id="83f87-104">This topic provides a list of Azure Redis Cache samples, covering scenarios such as connecting to a cache, reading and writing data to and from a cache, and using the ASP.NET Redis Cache providers.</span></span> <span data-ttu-id="83f87-105">Some of the samples are downloadable projects, and some provide step-by-step guidance and include code snippets but do not link to a downloadable project.</span><span class="sxs-lookup"><span data-stu-id="83f87-105">Some of the samples are downloadable projects, and some provide step-by-step guidance and include code snippets but do not link to a downloadable project.</span></span>

## <a name="hello-world-samples"></a><span data-ttu-id="83f87-106">Hello world samples</span><span class="sxs-lookup"><span data-stu-id="83f87-106">Hello world samples</span></span>
<span data-ttu-id="83f87-107">The samples in this section show the basics of connecting to an Azure Redis Cache instance and reading and writing data to the cache using a variety of languages and Redis clients.</span><span class="sxs-lookup"><span data-stu-id="83f87-107">The samples in this section show the basics of connecting to an Azure Redis Cache instance and reading and writing data to the cache using a variety of languages and Redis clients.</span></span>

<span data-ttu-id="83f87-108">The [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample shows how to perform various cache operations using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET client.</span><span class="sxs-lookup"><span data-stu-id="83f87-108">The [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample shows how to perform various cache operations using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .NET client.</span></span>

<span data-ttu-id="83f87-109">This sample shows how to:</span><span class="sxs-lookup"><span data-stu-id="83f87-109">This sample shows how to:</span></span>

* <span data-ttu-id="83f87-110">Use various connection options</span><span class="sxs-lookup"><span data-stu-id="83f87-110">Use various connection options</span></span>
* <span data-ttu-id="83f87-111">Read and write objects to and from the cache using synchronous and asynchronous operations</span><span class="sxs-lookup"><span data-stu-id="83f87-111">Read and write objects to and from the cache using synchronous and asynchronous operations</span></span>
* <span data-ttu-id="83f87-112">Use Redis MGET/MSET commands to return values of specified keys</span><span class="sxs-lookup"><span data-stu-id="83f87-112">Use Redis MGET/MSET commands to return values of specified keys</span></span>
* <span data-ttu-id="83f87-113">Perform Redis transactional operations</span><span class="sxs-lookup"><span data-stu-id="83f87-113">Perform Redis transactional operations</span></span>
* <span data-ttu-id="83f87-114">Work with Redis lists and sorted sets</span><span class="sxs-lookup"><span data-stu-id="83f87-114">Work with Redis lists and sorted sets</span></span>
* <span data-ttu-id="83f87-115">Store .NET objects using JsonConvert serializers</span><span class="sxs-lookup"><span data-stu-id="83f87-115">Store .NET objects using JsonConvert serializers</span></span>
* <span data-ttu-id="83f87-116">Use Redis sets to implement tagging</span><span class="sxs-lookup"><span data-stu-id="83f87-116">Use Redis sets to implement tagging</span></span>
* <span data-ttu-id="83f87-117">Work with Redis Cluster</span><span class="sxs-lookup"><span data-stu-id="83f87-117">Work with Redis Cluster</span></span>

<span data-ttu-id="83f87-118">For more information, see the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) documentation on github, and for more usage scenarios see the [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) unit tests.</span><span class="sxs-lookup"><span data-stu-id="83f87-118">For more information, see the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) documentation on github, and for more usage scenarios see the [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) unit tests.</span></span>

<span data-ttu-id="83f87-119">[How to use Azure Redis Cache with Python](cache-python-get-started.md) shows how to get started with Azure Redis Cache using Python and the [redis-py](https://github.com/andymccurdy/redis-py) client.</span><span class="sxs-lookup"><span data-stu-id="83f87-119">[How to use Azure Redis Cache with Python](cache-python-get-started.md) shows how to get started with Azure Redis Cache using Python and the [redis-py](https://github.com/andymccurdy/redis-py) client.</span></span>

<span data-ttu-id="83f87-120">[Work with .NET objects in the cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) shows you one way to serialize .NET objects so you can write them to and read them from an Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="83f87-120">[Work with .NET objects in the cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) shows you one way to serialize .NET objects so you can write them to and read them from an Azure Redis Cache instance.</span></span> 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a><span data-ttu-id="83f87-121">Use Redis Cache as a Scale out Backplane for ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="83f87-121">Use Redis Cache as a Scale out Backplane for ASP.NET SignalR</span></span>
<span data-ttu-id="83f87-122">The [Use Redis Cache as a Scale out Backplane for ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) sample demonstrates how you can use Azure Redis Cache as a SignalR backplane.</span><span class="sxs-lookup"><span data-stu-id="83f87-122">The [Use Redis Cache as a Scale out Backplane for ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) sample demonstrates how you can use Azure Redis Cache as a SignalR backplane.</span></span> <span data-ttu-id="83f87-123">For more information about backplane, see [SignalR Scaleout with Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).</span><span class="sxs-lookup"><span data-stu-id="83f87-123">For more information about backplane, see [SignalR Scaleout with Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).</span></span>

## <a name="redis-cache-customer-query-sample"></a><span data-ttu-id="83f87-124">Redis Cache customer query sample</span><span class="sxs-lookup"><span data-stu-id="83f87-124">Redis Cache customer query sample</span></span>
<span data-ttu-id="83f87-125">This sample demonstrates compares performance between accessing data from a cache and accessing data from persistence storage.</span><span class="sxs-lookup"><span data-stu-id="83f87-125">This sample demonstrates compares performance between accessing data from a cache and accessing data from persistence storage.</span></span> <span data-ttu-id="83f87-126">This sample has two projects.</span><span class="sxs-lookup"><span data-stu-id="83f87-126">This sample has two projects.</span></span>

* [<span data-ttu-id="83f87-127">Demo how Redis Cache can improve performance by Caching data</span><span class="sxs-lookup"><span data-stu-id="83f87-127">Demo how Redis Cache can improve performance by Caching data</span></span>](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [<span data-ttu-id="83f87-128">Seed the Database and Cache for the demo</span><span class="sxs-lookup"><span data-stu-id="83f87-128">Seed the Database and Cache for the demo</span></span>](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a><span data-ttu-id="83f87-129">ASP.NET Session State and Output Caching</span><span class="sxs-lookup"><span data-stu-id="83f87-129">ASP.NET Session State and Output Caching</span></span>
<span data-ttu-id="83f87-130">The [Use Azure Redis Cache to store ASP.NET SessionState and OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) sample demonstrates how you to use Azure Redis Cache to store ASP.NET Session and Output Cache using the SessionState and OutputCache providers for Redis.</span><span class="sxs-lookup"><span data-stu-id="83f87-130">The [Use Azure Redis Cache to store ASP.NET SessionState and OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) sample demonstrates how you to use Azure Redis Cache to store ASP.NET Session and Output Cache using the SessionState and OutputCache providers for Redis.</span></span>

## <a name="manage-azure-redis-cache-with-maml"></a><span data-ttu-id="83f87-131">Manage Azure Redis Cache with MAML</span><span class="sxs-lookup"><span data-stu-id="83f87-131">Manage Azure Redis Cache with MAML</span></span>
<span data-ttu-id="83f87-132">The [Manage Azure Redis Cache using Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample demonstrates how can you use Azure Management Libraries to manage - (Create/ Update/ delete) your Cache.</span><span class="sxs-lookup"><span data-stu-id="83f87-132">The [Manage Azure Redis Cache using Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample demonstrates how can you use Azure Management Libraries to manage - (Create/ Update/ delete) your Cache.</span></span> 

## <a name="custom-monitoring-sample"></a><span data-ttu-id="83f87-133">Custom monitoring sample</span><span class="sxs-lookup"><span data-stu-id="83f87-133">Custom monitoring sample</span></span>
<span data-ttu-id="83f87-134">The [Access Redis Cache Monitoring data](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) sample demonstrates how you can access monitoring data for your Azure Redis Cache outside of the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="83f87-134">The [Access Redis Cache Monitoring data](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) sample demonstrates how you can access monitoring data for your Azure Redis Cache outside of the Azure Portal.</span></span>

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a><span data-ttu-id="83f87-135">A Twitter-style clone written using PHP and Redis</span><span class="sxs-lookup"><span data-stu-id="83f87-135">A Twitter-style clone written using PHP and Redis</span></span>
<span data-ttu-id="83f87-136">The [Retwis](https://github.com/SyntaxC4-MSFT/retwis) sample is the Redis Hello World.</span><span class="sxs-lookup"><span data-stu-id="83f87-136">The [Retwis](https://github.com/SyntaxC4-MSFT/retwis) sample is the Redis Hello World.</span></span> <span data-ttu-id="83f87-137">It is a minimal Twitter-style social network clone written using Redis and PHP using the [Predis](https://github.com/nrk/predis) client.</span><span class="sxs-lookup"><span data-stu-id="83f87-137">It is a minimal Twitter-style social network clone written using Redis and PHP using the [Predis](https://github.com/nrk/predis) client.</span></span> <span data-ttu-id="83f87-138">The source code is designed to be very simple and at the same time to show different Redis data structures.</span><span class="sxs-lookup"><span data-stu-id="83f87-138">The source code is designed to be very simple and at the same time to show different Redis data structures.</span></span>

## <a name="bandwidth-monitor"></a><span data-ttu-id="83f87-139">Bandwidth monitor</span><span class="sxs-lookup"><span data-stu-id="83f87-139">Bandwidth monitor</span></span>
<span data-ttu-id="83f87-140">The [Bandwidth monitor](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) sample allows you to monitor the bandwidth used on the client.</span><span class="sxs-lookup"><span data-stu-id="83f87-140">The [Bandwidth monitor](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) sample allows you to monitor the bandwidth used on the client.</span></span> <span data-ttu-id="83f87-141">To measure the bandwidth, run the sample on the cache client machine, make calls to the cache, and observe the bandwidth reported by the bandwidth monitor sample.</span><span class="sxs-lookup"><span data-stu-id="83f87-141">To measure the bandwidth, run the sample on the cache client machine, make calls to the cache, and observe the bandwidth reported by the bandwidth monitor sample.</span></span>

