---
title: Cache ASP.NET Output Cache Provider
description: Learn how to cache ASP.NET Page Output using Azure Redis Cache
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: 845f25637a0e48460fc76c1ee36060274b3cec38
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548966"
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="74b14-103">ASP.NET Output Cache Provider for Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="74b14-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="74b14-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span><span class="sxs-lookup"><span data-stu-id="74b14-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="74b14-105">This data is specifically for full HTTP responses (page output caching).</span><span class="sxs-lookup"><span data-stu-id="74b14-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="74b14-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="74b14-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="74b14-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span><span class="sxs-lookup"><span data-stu-id="74b14-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="74b14-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span><span class="sxs-lookup"><span data-stu-id="74b14-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span></span> <span data-ttu-id="74b14-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="74b14-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-the-cache"></a><span data-ttu-id="74b14-110">Store ASP.NET page output in the cache</span><span class="sxs-lookup"><span data-stu-id="74b14-110">Store ASP.NET page output in the cache</span></span>
<span data-ttu-id="74b14-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span><span class="sxs-lookup"><span data-stu-id="74b14-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="74b14-112">Run the following command from the `Package Manager Console` window.</span><span class="sxs-lookup"><span data-stu-id="74b14-112">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="74b14-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span><span class="sxs-lookup"><span data-stu-id="74b14-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="74b14-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span><span class="sxs-lookup"><span data-stu-id="74b14-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="74b14-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span><span class="sxs-lookup"><span data-stu-id="74b14-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="74b14-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span><span class="sxs-lookup"><span data-stu-id="74b14-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="74b14-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span><span class="sxs-lookup"><span data-stu-id="74b14-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="74b14-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="74b14-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="74b14-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span><span class="sxs-lookup"><span data-stu-id="74b14-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="74b14-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span><span class="sxs-lookup"><span data-stu-id="74b14-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="74b14-121">The commented section provides an example of the attributes and sample settings for each attribute.</span><span class="sxs-lookup"><span data-stu-id="74b14-121">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="74b14-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span><span class="sxs-lookup"><span data-stu-id="74b14-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="74b14-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="74b14-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="74b14-124">**host** – specify your cache endpoint.</span><span class="sxs-lookup"><span data-stu-id="74b14-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="74b14-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span><span class="sxs-lookup"><span data-stu-id="74b14-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="74b14-126">**accessKey** – use either the primary or secondary key for your cache.</span><span class="sxs-lookup"><span data-stu-id="74b14-126">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="74b14-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span><span class="sxs-lookup"><span data-stu-id="74b14-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="74b14-128">Be sure to specify the correct port.</span><span class="sxs-lookup"><span data-stu-id="74b14-128">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="74b14-129">The non-SSL port is disabled by default for new caches.</span><span class="sxs-lookup"><span data-stu-id="74b14-129">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="74b14-130">Specify true for this setting to use the SSL port.</span><span class="sxs-lookup"><span data-stu-id="74b14-130">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="74b14-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span><span class="sxs-lookup"><span data-stu-id="74b14-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="74b14-132">**databaseId** – Specified which database to use for cache output data.</span><span class="sxs-lookup"><span data-stu-id="74b14-132">**databaseId** – Specified which database to use for cache output data.</span></span> <span data-ttu-id="74b14-133">If not specified, the default value of 0 is used.</span><span class="sxs-lookup"><span data-stu-id="74b14-133">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="74b14-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="74b14-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="74b14-135">This naming scheme enables multiple applications to share the same key.</span><span class="sxs-lookup"><span data-stu-id="74b14-135">This naming scheme enables multiple applications to share the same key.</span></span> <span data-ttu-id="74b14-136">This parameter is optional and if you do not provide it a default value is used.</span><span class="sxs-lookup"><span data-stu-id="74b14-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="74b14-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span><span class="sxs-lookup"><span data-stu-id="74b14-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="74b14-138">If not specified, the default connectTimeout setting of 5000 is used.</span><span class="sxs-lookup"><span data-stu-id="74b14-138">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="74b14-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="74b14-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="74b14-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span><span class="sxs-lookup"><span data-stu-id="74b14-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="74b14-141">If not specified, the default syncTimeout setting of 1000 is used.</span><span class="sxs-lookup"><span data-stu-id="74b14-141">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="74b14-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="74b14-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="74b14-143">Add an OutputCache directive to each page for which you wish to cache the output.</span><span class="sxs-lookup"><span data-stu-id="74b14-143">Add an OutputCache directive to each page for which you wish to cache the output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="74b14-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span><span class="sxs-lookup"><span data-stu-id="74b14-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span></span> <span data-ttu-id="74b14-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="74b14-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="74b14-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span><span class="sxs-lookup"><span data-stu-id="74b14-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74b14-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="74b14-147">Next steps</span></span>
<span data-ttu-id="74b14-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="74b14-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

