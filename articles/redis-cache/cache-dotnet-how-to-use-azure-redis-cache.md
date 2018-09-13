---
title: How to Use Azure Redis Cache | Microsoft Docs
description: Learn how to improve the performance of your Azure applications with Azure Redis Cache
services: redis-cache,app-service
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 2a828a9f091f3aed1fc80f2ba0f1ea9de8a5a3a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553965"
---
# <a name="how-to-use-azure-redis-cache"></a><span data-ttu-id="6607a-103">How to Use Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="6607a-103">How to Use Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

<span data-ttu-id="6607a-109">This guide shows you how to get started using **Azure Redis Cache**.</span><span class="sxs-lookup"><span data-stu-id="6607a-109">This guide shows you how to get started using **Azure Redis Cache**.</span></span> <span data-ttu-id="6607a-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span></span> <span data-ttu-id="6607a-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6607a-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="6607a-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6607a-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="6607a-113">Microsoft Azure Redis Cache is available in the following tiers:</span><span class="sxs-lookup"><span data-stu-id="6607a-113">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="6607a-114">**Basic** – Single node.</span><span class="sxs-lookup"><span data-stu-id="6607a-114">**Basic** – Single node.</span></span> <span data-ttu-id="6607a-115">Multiple sizes up to 53 GB.</span><span class="sxs-lookup"><span data-stu-id="6607a-115">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="6607a-116">**Standard** – Two-node Primary/Replica.</span><span class="sxs-lookup"><span data-stu-id="6607a-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="6607a-117">Multiple sizes up to 53 GB.</span><span class="sxs-lookup"><span data-stu-id="6607a-117">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="6607a-118">99.9% SLA.</span><span class="sxs-lookup"><span data-stu-id="6607a-118">99.9% SLA.</span></span>
* <span data-ttu-id="6607a-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span><span class="sxs-lookup"><span data-stu-id="6607a-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="6607a-120">Multiple sizes from 6 GB to 530 GB (contact us for more).</span><span class="sxs-lookup"><span data-stu-id="6607a-120">Multiple sizes from 6 GB to 530 GB (contact us for more).</span></span> <span data-ttu-id="6607a-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="6607a-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="6607a-122">99.9% SLA.</span><span class="sxs-lookup"><span data-stu-id="6607a-122">99.9% SLA.</span></span>

<span data-ttu-id="6607a-123">Each tier differs in terms of features and pricing.</span><span class="sxs-lookup"><span data-stu-id="6607a-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="6607a-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="6607a-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="6607a-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span><span class="sxs-lookup"><span data-stu-id="6607a-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="6607a-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span><span class="sxs-lookup"><span data-stu-id="6607a-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span></span> <span data-ttu-id="6607a-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="6607a-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="6607a-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="6607a-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="6607a-129">Get Started with Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="6607a-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="6607a-130">Getting started with Azure Redis Cache is easy.</span><span class="sxs-lookup"><span data-stu-id="6607a-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="6607a-131">To get started, you provision and configure a cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-131">To get started, you provision and configure a cache.</span></span> <span data-ttu-id="6607a-132">Next, you configure the cache clients so they can access the cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-132">Next, you configure the cache clients so they can access the cache.</span></span> <span data-ttu-id="6607a-133">Once the cache clients are configured, you can begin working with them.</span><span class="sxs-lookup"><span data-stu-id="6607a-133">Once the cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="6607a-134">[Create the cache][Create the cache]</span><span class="sxs-lookup"><span data-stu-id="6607a-134">[Create the cache][Create the cache]</span></span>
* <span data-ttu-id="6607a-135">[Configure the cache clients][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="6607a-135">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="6607a-136">Create a cache</span><span class="sxs-lookup"><span data-stu-id="6607a-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="to-access-your-cache-after-its-created"></a><span data-ttu-id="6607a-137">To access your cache after it's created</span><span class="sxs-lookup"><span data-stu-id="6607a-137">To access your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="6607a-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6607a-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="6607a-139">Configure the cache clients</span><span class="sxs-lookup"><span data-stu-id="6607a-139">Configure the cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="6607a-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="6607a-141">Working with Caches</span><span class="sxs-lookup"><span data-stu-id="6607a-141">Working with Caches</span></span>
<span data-ttu-id="6607a-142">The steps in this section describe how to perform common tasks with Cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-142">The steps in this section describe how to perform common tasks with Cache.</span></span>

* <span data-ttu-id="6607a-143">[Connect to the cache][Connect to the cache]</span><span class="sxs-lookup"><span data-stu-id="6607a-143">[Connect to the cache][Connect to the cache]</span></span>
* <span data-ttu-id="6607a-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span><span class="sxs-lookup"><span data-stu-id="6607a-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span></span>
* [<span data-ttu-id="6607a-145">Work with .NET objects in the cache</span><span class="sxs-lookup"><span data-stu-id="6607a-145">Work with .NET objects in the cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-to-the-cache"></a><span data-ttu-id="6607a-146">Connect to the cache</span><span class="sxs-lookup"><span data-stu-id="6607a-146">Connect to the cache</span></span>
<span data-ttu-id="6607a-147">To programmatically work with a cache, you need a reference to the cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-147">To programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="6607a-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> The StackExchange.Redis client requires .NET Framework 4 or higher.
> 
> 

<span data-ttu-id="6607a-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span><span class="sxs-lookup"><span data-stu-id="6607a-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="6607a-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span><span class="sxs-lookup"><span data-stu-id="6607a-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span></span> 

<span data-ttu-id="6607a-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span><span class="sxs-lookup"><span data-stu-id="6607a-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span></span> <span data-ttu-id="6607a-153">Use the key generated from the Azure portal as the password parameter.</span><span class="sxs-lookup"><span data-stu-id="6607a-153">Use the key generated from the Azure portal as the password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Warning: Never store credentials in source code. To keep this sample simple, I’m showing them in the source code. See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how to store credentials.
> 
> 

<span data-ttu-id="6607a-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span><span class="sxs-lookup"><span data-stu-id="6607a-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span></span>

> [!NOTE]
> The non-SSL port is disabled by default for new caches. For instructions on enabling the non-SSL port, see [Access Ports](cache-configure.md#access-ports).
> 
> 

<span data-ttu-id="6607a-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="6607a-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="6607a-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span><span class="sxs-lookup"><span data-stu-id="6607a-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="6607a-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span><span class="sxs-lookup"><span data-stu-id="6607a-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="6607a-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span><span class="sxs-lookup"><span data-stu-id="6607a-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="6607a-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="6607a-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="6607a-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span><span class="sxs-lookup"><span data-stu-id="6607a-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="6607a-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span><span class="sxs-lookup"><span data-stu-id="6607a-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

    // Connection refers to a property that returns a ConnectionMultiplexer
    // as shown in the previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using the cache object...
    // Simple put of integral data types into the cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from the cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="6607a-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span></span> <span data-ttu-id="6607a-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="6607a-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="6607a-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-the-cache"></a><span data-ttu-id="6607a-170">Add and retrieve objects from the cache</span><span class="sxs-lookup"><span data-stu-id="6607a-170">Add and retrieve objects from the cache</span></span>
<span data-ttu-id="6607a-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span><span class="sxs-lookup"><span data-stu-id="6607a-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="6607a-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="6607a-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span><span class="sxs-lookup"><span data-stu-id="6607a-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="6607a-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span><span class="sxs-lookup"><span data-stu-id="6607a-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="6607a-175">This usage pattern is known as the cache-aside pattern.</span><span class="sxs-lookup"><span data-stu-id="6607a-175">This usage pattern is known as the cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // The item keyed by "key1" is not in the cache. Obtain
        // it from the desired data source and add it to the cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="6607a-176">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="6607a-176">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="6607a-177">Work with .NET objects in the cache</span><span class="sxs-lookup"><span data-stu-id="6607a-177">Work with .NET objects in the cache</span></span>
<span data-ttu-id="6607a-178">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span><span class="sxs-lookup"><span data-stu-id="6607a-178">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="6607a-179">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span><span class="sxs-lookup"><span data-stu-id="6607a-179">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="6607a-180">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span><span class="sxs-lookup"><span data-stu-id="6607a-180">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span></span> <span data-ttu-id="6607a-181">The following example shows a get and set using an `Employee` object instance.</span><span class="sxs-lookup"><span data-stu-id="6607a-181">The following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store to cache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="6607a-182">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6607a-182">Next Steps</span></span>
<span data-ttu-id="6607a-183">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-183">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="6607a-184">Check out the ASP.NET providers for Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-184">Check out the ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="6607a-185">Azure Redis Session State Provider</span><span class="sxs-lookup"><span data-stu-id="6607a-185">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="6607a-186">Azure Redis Cache ASP.NET Output Cache Provider</span><span class="sxs-lookup"><span data-stu-id="6607a-186">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="6607a-187">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span><span class="sxs-lookup"><span data-stu-id="6607a-187">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span> <span data-ttu-id="6607a-188">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span><span class="sxs-lookup"><span data-stu-id="6607a-188">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span></span>
* <span data-ttu-id="6607a-189">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="6607a-189">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="6607a-190">Azure Redis Cache can be accessed from many Redis clients and development languages.</span><span class="sxs-lookup"><span data-stu-id="6607a-190">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="6607a-191">For more information, see [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="6607a-191">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="6607a-192">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="6607a-192">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="6607a-193">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="6607a-193">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="6607a-194">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="6607a-194">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="6607a-195">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span><span class="sxs-lookup"><span data-stu-id="6607a-195">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction to Azure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project to Use Azure Caching]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create the cache]: #create-cache
[Configure the cache]: #enable-caching
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect to the cache]: #connect-to-cache
[Add and retrieve objects from the cache]: #add-object
[Specify the expiration of an object in the cache]: #specify-expiration
[Store ASP.NET session state in the cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How to retrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in the cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate to Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups to manage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction to Redis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


