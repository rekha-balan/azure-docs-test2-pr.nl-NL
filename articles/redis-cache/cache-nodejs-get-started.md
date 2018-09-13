---
title: How to use Azure Redis Cache with Node.js | Microsoft Docs
description: Get started with Azure Redis Cache using Node.js and node_redis.
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554618"
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="3e62a-103">How to use Azure Redis Cache with Node.js</span><span class="sxs-lookup"><span data-stu-id="3e62a-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

<span data-ttu-id="3e62a-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3e62a-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="3e62a-110">Your cache is accessible from any application within Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3e62a-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="3e62a-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span><span class="sxs-lookup"><span data-stu-id="3e62a-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="3e62a-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="3e62a-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e62a-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3e62a-113">Prerequisites</span></span>
<span data-ttu-id="3e62a-114">Install [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="3e62a-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="3e62a-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="3e62a-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="3e62a-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="3e62a-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="3e62a-117">Create a Redis cache on Azure</span><span class="sxs-lookup"><span data-stu-id="3e62a-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="3e62a-118">Retrieve the host name and access keys</span><span class="sxs-lookup"><span data-stu-id="3e62a-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="3e62a-119">Connect to the cache securely using SSL</span><span class="sxs-lookup"><span data-stu-id="3e62a-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="3e62a-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span><span class="sxs-lookup"><span data-stu-id="3e62a-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="3e62a-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span><span class="sxs-lookup"><span data-stu-id="3e62a-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="3e62a-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span><span class="sxs-lookup"><span data-stu-id="3e62a-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> The non-SSL port is disabled for new Azure Redis Cache instances. If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="3e62a-125">Add something to the cache and retrieve it</span><span class="sxs-lookup"><span data-stu-id="3e62a-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="3e62a-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span><span class="sxs-lookup"><span data-stu-id="3e62a-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="3e62a-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="3e62a-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="3e62a-128">Output:</span><span class="sxs-lookup"><span data-stu-id="3e62a-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="3e62a-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="3e62a-129">Next steps</span></span>
* <span data-ttu-id="3e62a-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span><span class="sxs-lookup"><span data-stu-id="3e62a-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="3e62a-131">Read the official [Redis documentation](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="3e62a-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>

