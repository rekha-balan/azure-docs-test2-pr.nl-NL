---
title: How to use Azure Redis Cache with Java | Microsoft Docs
description: Get started with Azure Redis Cache using Java
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: ''
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 3cfad3a7279b5f9bbff1e6cd9794c492e3544752
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661378"
---
# <a name="how-to-use-azure-redis-cache-with-java"></a><span data-ttu-id="98e95-103">How to use Azure Redis Cache with Java</span><span class="sxs-lookup"><span data-stu-id="98e95-103">How to use Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

<span data-ttu-id="98e95-109">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98e95-109">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="98e95-110">Your cache is accessible from any application within Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="98e95-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="98e95-111">This topic shows you how to get started with Azure Redis Cache using Java.</span><span class="sxs-lookup"><span data-stu-id="98e95-111">This topic shows you how to get started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98e95-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="98e95-112">Prerequisites</span></span>
<span data-ttu-id="98e95-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span><span class="sxs-lookup"><span data-stu-id="98e95-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="98e95-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="98e95-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="98e95-115">Create a Redis cache on Azure</span><span class="sxs-lookup"><span data-stu-id="98e95-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="98e95-116">Retrieve the host name and access keys</span><span class="sxs-lookup"><span data-stu-id="98e95-116">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="98e95-117">Connect to the cache securely using SSL</span><span class="sxs-lookup"><span data-stu-id="98e95-117">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="98e95-118">The latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting to Azure Redis Cache using SSL.</span><span class="sxs-lookup"><span data-stu-id="98e95-118">The latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="98e95-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span><span class="sxs-lookup"><span data-stu-id="98e95-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="98e95-120">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span><span class="sxs-lookup"><span data-stu-id="98e95-120">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> The non-SSL port is disabled for new Azure Redis Cache instances. If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="98e95-123">Add something to the cache and retrieve it</span><span class="sxs-lookup"><span data-stu-id="98e95-123">Add something to the cache and retrieve it</span></span>
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a><span data-ttu-id="98e95-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="98e95-124">Next steps</span></span>
* <span data-ttu-id="98e95-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) the health of your cache.</span><span class="sxs-lookup"><span data-stu-id="98e95-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) the health of your cache.</span></span>
* <span data-ttu-id="98e95-126">Read the official [Redis documentation](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="98e95-126">Read the official [Redis documentation](http://redis.io/documentation).</span></span>
