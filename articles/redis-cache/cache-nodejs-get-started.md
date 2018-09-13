---
title: Quickstart to learn how to use Azure Redis Cache with Node.js | Microsoft Docs
description: In this quickstart you will learn how to use Azure Redis Cache with Node.js and node_redis.
services: redis-cache
documentationcenter: ''
author: wesmc7777
manager: cfowler
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: quickstart
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/21/2018
ms.author: wesmc
ms.custom: mvc
ms.openlocfilehash: 8f71feb610884af29bdfbf170cfc411f32c50233
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774663"
---
# <a name="quickstart-how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="985bf-103">Quickstart: How to use Azure Redis Cache with Node.js</span><span class="sxs-lookup"><span data-stu-id="985bf-103">Quickstart: How to use Azure Redis Cache with Node.js</span></span>



<span data-ttu-id="985bf-104">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="985bf-104">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="985bf-105">Your cache is accessible from any application within Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="985bf-105">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="985bf-106">This topic shows you how to get started with Azure Redis Cache using Node.js.</span><span class="sxs-lookup"><span data-stu-id="985bf-106">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> 

<span data-ttu-id="985bf-107">You can use any code editor to complete the steps in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="985bf-107">You can use any code editor to complete the steps in this quickstart.</span></span> <span data-ttu-id="985bf-108">However, [Visual Studio Code](https://code.visualstudio.com/) is an excellent option available on the Windows, macOS, and Linux platforms.</span><span class="sxs-lookup"><span data-stu-id="985bf-108">However, [Visual Studio Code](https://code.visualstudio.com/) is an excellent option available on the Windows, macOS, and Linux platforms.</span></span>

![Cache app completed](./media/cache-nodejs-get-started/cache-app-complete.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a><span data-ttu-id="985bf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="985bf-110">Prerequisites</span></span>
<span data-ttu-id="985bf-111">Install [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="985bf-111">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="985bf-112">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="985bf-112">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="985bf-113">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="985bf-113">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>


## <a name="create-a-cache"></a><span data-ttu-id="985bf-114">Create a cache</span><span class="sxs-lookup"><span data-stu-id="985bf-114">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

[!INCLUDE [redis-cache-access-keys](../../includes/redis-cache-access-keys.md)]


<span data-ttu-id="985bf-115">Add environment variables for your **HOST NAME** and **Primary** access key.</span><span class="sxs-lookup"><span data-stu-id="985bf-115">Add environment variables for your **HOST NAME** and **Primary** access key.</span></span> <span data-ttu-id="985bf-116">You will use these variables from your code instead of including the sensitive information directly in your code.</span><span class="sxs-lookup"><span data-stu-id="985bf-116">You will use these variables from your code instead of including the sensitive information directly in your code.</span></span>

```
set REDISCACHEHOSTNAME=contosoCache.redis.cache.windows.net
set REDISCACHEKEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```


## <a name="connect-to-the-cache"></a><span data-ttu-id="985bf-117">Connect to the cache</span><span class="sxs-lookup"><span data-stu-id="985bf-117">Connect to the cache</span></span>

<span data-ttu-id="985bf-118">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span><span class="sxs-lookup"><span data-stu-id="985bf-118">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="985bf-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span><span class="sxs-lookup"><span data-stu-id="985bf-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> 

```js
var redis = require("redis");

// Add your cache name and access key.
var client = redis.createClient(6380, process.env.REDISCACHEHOSTNAME,
    {auth_pass: process.env.REDISCACHEKEY, tls: {servername: process.env.REDISCACHEHOSTNAME}});
```

<span data-ttu-id="985bf-120">Don't create a new connections for each operation in your code.</span><span class="sxs-lookup"><span data-stu-id="985bf-120">Don't create a new connections for each operation in your code.</span></span> <span data-ttu-id="985bf-121">Instead, reuse connections as much as possible.</span><span class="sxs-lookup"><span data-stu-id="985bf-121">Instead, reuse connections as much as possible.</span></span> 

## <a name="create-a-new-nodejs-app"></a><span data-ttu-id="985bf-122">Create a new Node.js app</span><span class="sxs-lookup"><span data-stu-id="985bf-122">Create a new Node.js app</span></span>

<span data-ttu-id="985bf-123">Create a new script file named *redistest.js*.</span><span class="sxs-lookup"><span data-stu-id="985bf-123">Create a new script file named *redistest.js*.</span></span>

<span data-ttu-id="985bf-124">Add the following example JavaScript to the file.</span><span class="sxs-lookup"><span data-stu-id="985bf-124">Add the following example JavaScript to the file.</span></span> <span data-ttu-id="985bf-125">This code shows you how to connect to an Azure Redis Cache instance using the cache host name and key environment variables.</span><span class="sxs-lookup"><span data-stu-id="985bf-125">This code shows you how to connect to an Azure Redis Cache instance using the cache host name and key environment variables.</span></span> <span data-ttu-id="985bf-126">The code also stores and retrieves a string value in the cache.</span><span class="sxs-lookup"><span data-stu-id="985bf-126">The code also stores and retrieves a string value in the cache.</span></span> <span data-ttu-id="985bf-127">The `PING` and `CLIENT LIST` commands are also executed.</span><span class="sxs-lookup"><span data-stu-id="985bf-127">The `PING` and `CLIENT LIST` commands are also executed.</span></span> <span data-ttu-id="985bf-128">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="985bf-128">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

```js
var redis = require("redis");
var bluebird = require("bluebird");

bluebird.promisifyAll(redis.RedisClient.prototype);
bluebird.promisifyAll(redis.Multi.prototype);

async function testCache() {

    // Connect to the Redis cache over the SSL port using the key.
    var cacheConnection = redis.createClient(6380, process.env.REDISCACHEHOSTNAME, 
        {auth_pass: process.env.REDISCACHEKEY, tls: {servername: process.env.REDISCACHEHOSTNAME}});
        
    // Perform cache operations using the cache connection object...

    // Simple PING command
    console.log("\nCache command: PING");
    console.log("Cache response : " + await cacheConnection.pingAsync());

    // Simple get and put of integral data types into the cache
    console.log("\nCache command: GET Message");
    console.log("Cache response : " + await cacheConnection.getAsync("Message"));    

    console.log("\nCache command: SET Message");
    console.log("Cache response : " + await cacheConnection.setAsync("Message",
        "Hello! The cache is working from Node.js!"));    

    // Demostrate "SET Message" executed as expected...
    console.log("\nCache command: GET Message");
    console.log("Cache response : " + await cacheConnection.getAsync("Message"));    

    // Get the client list, useful to see if connection list is growing...
    console.log("\nCache command: CLIENT LIST");
    console.log("Cache response : " + await cacheConnection.clientAsync("LIST"));    
}

testCache();
```

<span data-ttu-id="985bf-129">Run the script with Node.js.</span><span class="sxs-lookup"><span data-stu-id="985bf-129">Run the script with Node.js.</span></span>

```
node redistest.js
```

<span data-ttu-id="985bf-130">In the example below, you can see the `Message` key previously had a cached value, which was set using the Redis Console in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="985bf-130">In the example below, you can see the `Message` key previously had a cached value, which was set using the Redis Console in the Azure portal.</span></span> <span data-ttu-id="985bf-131">The app updated that cached value.</span><span class="sxs-lookup"><span data-stu-id="985bf-131">The app updated that cached value.</span></span> <span data-ttu-id="985bf-132">The app also executed the `PING` and `CLIENT LIST` commands.</span><span class="sxs-lookup"><span data-stu-id="985bf-132">The app also executed the `PING` and `CLIENT LIST` commands.</span></span>

![Cache app completed](./media/cache-nodejs-get-started/cache-app-complete.png)


## <a name="clean-up-resources"></a><span data-ttu-id="985bf-134">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="985bf-134">Clean up resources</span></span>

<span data-ttu-id="985bf-135">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them.</span><span class="sxs-lookup"><span data-stu-id="985bf-135">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them.</span></span>

<span data-ttu-id="985bf-136">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="985bf-136">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="985bf-137">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="985bf-137">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="985bf-138">Make sure that you do not accidentally delete the wrong resource group or resources.</span><span class="sxs-lookup"><span data-stu-id="985bf-138">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="985bf-139">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="985bf-139">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span></span>
>

<span data-ttu-id="985bf-140">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="985bf-140">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>

<span data-ttu-id="985bf-141">In the **Filter by name...** textbox, type the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="985bf-141">In the **Filter by name...** textbox, type the name of your resource group.</span></span> <span data-ttu-id="985bf-142">The instructions for this article used a resource group named *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="985bf-142">The instructions for this article used a resource group named *TestResources*.</span></span> <span data-ttu-id="985bf-143">On your resource group in the result list, click **...** then **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="985bf-143">On your resource group in the result list, click **...** then **Delete resource group**.</span></span>

![Delete](./media/cache-nodejs-get-started/cache-delete-resource-group.png)

<span data-ttu-id="985bf-145">You will be asked to confirm the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="985bf-145">You will be asked to confirm the deletion of the resource group.</span></span> <span data-ttu-id="985bf-146">Type the name of your resource group to confirm, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="985bf-146">Type the name of your resource group to confirm, and click **Delete**.</span></span>

<span data-ttu-id="985bf-147">After a few moments, the resource group and all of its contained resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="985bf-147">After a few moments, the resource group and all of its contained resources are deleted.</span></span>



## <a name="next-steps"></a><span data-ttu-id="985bf-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="985bf-148">Next steps</span></span>

<span data-ttu-id="985bf-149">In this quickstart, you learned how to use Azure Redis Cache from a Node.js application.</span><span class="sxs-lookup"><span data-stu-id="985bf-149">In this quickstart, you learned how to use Azure Redis Cache from a Node.js application.</span></span> <span data-ttu-id="985bf-150">Continue to the next quickstart to use Redis Cache with an ASP.NET web app.</span><span class="sxs-lookup"><span data-stu-id="985bf-150">Continue to the next quickstart to use Redis Cache with an ASP.NET web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="985bf-151">Create an ASP.NET web app that uses an Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="985bf-151">Create an ASP.NET web app that uses an Azure Redis Cache.</span></span>](./cache-web-app-howto.md)



