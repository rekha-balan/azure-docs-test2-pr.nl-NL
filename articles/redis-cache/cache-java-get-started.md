---
title: Quickstart to learn how to use Azure Redis Cache with Java | Microsoft Docs
description: In this quickstart, you will create a new Java app that uses Azure Redis Cache
services: redis-cache
documentationcenter: ''
author: wesmc7777
manager: cfowler
editor: ''
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: quickstart
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/23/2018
ms.author: wesmc
ms.custom: mvc
ms.openlocfilehash: cc1dd773d14aedb9a4e64a18a7b8f7963aca986b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828412"
---
# <a name="quickstart-how-to-use-azure-redis-cache-with-java"></a><span data-ttu-id="a9dfb-103">Quickstart: How to use Azure Redis Cache with Java</span><span class="sxs-lookup"><span data-stu-id="a9dfb-103">Quickstart: How to use Azure Redis Cache with Java</span></span>


<span data-ttu-id="a9dfb-104">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-104">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="a9dfb-105">Your cache is accessible from any application within Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-105">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="a9dfb-106">This article shows you how to get started with Azure Redis Cache using the [Jedis](https://github.com/xetorthio/jedis) Redis Cache client for Java.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-106">This article shows you how to get started with Azure Redis Cache using the [Jedis](https://github.com/xetorthio/jedis) Redis Cache client for Java.</span></span>

![Cache app completed](./media/cache-java-get-started/cache-app-complete.png)

<span data-ttu-id="a9dfb-108">You can use any code editor to complete the steps in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-108">You can use any code editor to complete the steps in this quickstart.</span></span> <span data-ttu-id="a9dfb-109">However, [Visual Studio Code](https://code.visualstudio.com/) is an excellent option available on the Windows, macOS, and Linux platforms.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-109">However, [Visual Studio Code](https://code.visualstudio.com/) is an excellent option available on the Windows, macOS, and Linux platforms.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a><span data-ttu-id="a9dfb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a9dfb-110">Prerequisites</span></span>

[<span data-ttu-id="a9dfb-111">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="a9dfb-111">Apache Maven</span></span>](http://maven.apache.org/)



## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="a9dfb-112">Create an Azure Redis cache</span><span class="sxs-lookup"><span data-stu-id="a9dfb-112">Create an Azure Redis cache</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

[!INCLUDE [redis-cache-access-keys](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="a9dfb-113">Add environment variables for your **HOST NAME** and **Primary** access key.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-113">Add environment variables for your **HOST NAME** and **Primary** access key.</span></span> <span data-ttu-id="a9dfb-114">You will use these variables from your code instead of including the sensitive information directly in your code.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-114">You will use these variables from your code instead of including the sensitive information directly in your code.</span></span>

```
set REDISCACHEHOSTNAME=contosoCache.redis.cache.windows.net
set REDISCACHEKEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

## <a name="create-a-new-java-app"></a><span data-ttu-id="a9dfb-115">Create a new Java app</span><span class="sxs-lookup"><span data-stu-id="a9dfb-115">Create a new Java app</span></span>

<span data-ttu-id="a9dfb-116">Using Maven, generate a new quickstart app:</span><span class="sxs-lookup"><span data-stu-id="a9dfb-116">Using Maven, generate a new quickstart app:</span></span>

```
mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.3 -DgroupId=example.demo -DartifactId=redistest -Dversion=1.0
```

<span data-ttu-id="a9dfb-117">Change to the new *redistest* project directory.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-117">Change to the new *redistest* project directory.</span></span>

<span data-ttu-id="a9dfb-118">Open the *pom.xml* file and add a dependency for [Jedis](https://github.com/xetorthio/jedis):</span><span class="sxs-lookup"><span data-stu-id="a9dfb-118">Open the *pom.xml* file and add a dependency for [Jedis](https://github.com/xetorthio/jedis):</span></span>

```xml
    <dependency>
        <groupId>redis.clients</groupId>
        <artifactId>jedis</artifactId>
        <version>2.9.0</version>
        <type>jar</type>
        <scope>compile</scope>
    </dependency>
```

<span data-ttu-id="a9dfb-119">Save the *pom.xml* file.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-119">Save the *pom.xml* file.</span></span>

<span data-ttu-id="a9dfb-120">Open *App.java* and replace the code with the following code:</span><span class="sxs-lookup"><span data-stu-id="a9dfb-120">Open *App.java* and replace the code with the following code:</span></span>

```java
package example.demo;

import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisShardInfo;

/**
 * Redis test
 *
 */
public class App 
{
    public static void main( String[] args )
    {

        boolean useSsl = true;
        String cacheHostname = System.getenv("REDISCACHEHOSTNAME");
        String cachekey = System.getenv("REDISCACHEKEY");

        // Connect to the Redis cache over the SSL port using the key.
        JedisShardInfo shardInfo = new JedisShardInfo(cacheHostname, 6380, useSsl);
        shardInfo.setPassword(cachekey); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);      

        // Perform cache operations using the cache connection object...

        // Simple PING command        
        System.out.println( "\nCache Command  : Ping" );
        System.out.println( "Cache Response : " + jedis.ping());

        // Simple get and put of integral data types into the cache
        System.out.println( "\nCache Command  : GET Message" );
        System.out.println( "Cache Response : " + jedis.get("Message"));

        System.out.println( "\nCache Command  : SET Message" );
        System.out.println( "Cache Response : " + jedis.set("Message", "Hello! The cache is working from Java!"));

        // Demostrate "SET Message" executed as expected...
        System.out.println( "\nCache Command  : GET Message" );
        System.out.println( "Cache Response : " + jedis.get("Message"));

        // Get the client list, useful to see if connection list is growing...
        System.out.println( "\nCache Command  : CLIENT LIST" );
        System.out.println( "Cache Response : " + jedis.clientList());

        jedis.close();
    }
}
```

<span data-ttu-id="a9dfb-121">This code shows you how to connect to an Azure Redis Cache instance using the cache host name and key environment variables.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-121">This code shows you how to connect to an Azure Redis Cache instance using the cache host name and key environment variables.</span></span> <span data-ttu-id="a9dfb-122">The code also stores and retrieves a string value in the cache.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-122">The code also stores and retrieves a string value in the cache.</span></span> <span data-ttu-id="a9dfb-123">The `PING` and `CLIENT LIST` commands are also executed.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-123">The `PING` and `CLIENT LIST` commands are also executed.</span></span> 

<span data-ttu-id="a9dfb-124">Save *App.java*.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-124">Save *App.java*.</span></span>

## <a name="build-and-run-the-app"></a><span data-ttu-id="a9dfb-125">Build and run the app</span><span class="sxs-lookup"><span data-stu-id="a9dfb-125">Build and run the app</span></span>

<span data-ttu-id="a9dfb-126">Execute the following Maven command to build and run the app:</span><span class="sxs-lookup"><span data-stu-id="a9dfb-126">Execute the following Maven command to build and run the app:</span></span>

```
mvn compile
mvn exec:java -D exec.mainClass=example.demo.App
```

<span data-ttu-id="a9dfb-127">In the example below, you can see the `Message` key previously had a cached value, which was set using the Redis Console in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-127">In the example below, you can see the `Message` key previously had a cached value, which was set using the Redis Console in the Azure portal.</span></span> <span data-ttu-id="a9dfb-128">The app updated that cached value.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-128">The app updated that cached value.</span></span> <span data-ttu-id="a9dfb-129">The app also executed the `PING` and `CLIENT LIST` commands.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-129">The app also executed the `PING` and `CLIENT LIST` commands.</span></span>

![Cache app completed](./media/cache-java-get-started/cache-app-complete.png)


## <a name="clean-up-resources"></a><span data-ttu-id="a9dfb-131">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a9dfb-131">Clean up resources</span></span>

<span data-ttu-id="a9dfb-132">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-132">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them.</span></span>

<span data-ttu-id="a9dfb-133">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-133">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a9dfb-134">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-134">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="a9dfb-135">Make sure that you do not accidentally delete the wrong resource group or resources.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-135">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="a9dfb-136">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-136">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span></span>
>

<span data-ttu-id="a9dfb-137">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-137">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>

<span data-ttu-id="a9dfb-138">In the **Filter by name...** textbox, type the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-138">In the **Filter by name...** textbox, type the name of your resource group.</span></span> <span data-ttu-id="a9dfb-139">The instructions for this article used a resource group named *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-139">The instructions for this article used a resource group named *TestResources*.</span></span> <span data-ttu-id="a9dfb-140">On your resource group in the result list, click **...** then **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-140">On your resource group in the result list, click **...** then **Delete resource group**.</span></span>

![Delete](./media/cache-java-get-started/cache-delete-resource-group.png)

<span data-ttu-id="a9dfb-142">You will be asked to confirm the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-142">You will be asked to confirm the deletion of the resource group.</span></span> <span data-ttu-id="a9dfb-143">Type the name of your resource group to confirm, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-143">Type the name of your resource group to confirm, and click **Delete**.</span></span>

<span data-ttu-id="a9dfb-144">After a few moments, the resource group and all of its contained resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-144">After a few moments, the resource group and all of its contained resources are deleted.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a9dfb-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="a9dfb-145">Next steps</span></span>

<span data-ttu-id="a9dfb-146">In this quickstart, you learned how to use Azure Redis Cache from a Java application.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-146">In this quickstart, you learned how to use Azure Redis Cache from a Java application.</span></span> <span data-ttu-id="a9dfb-147">Continue to the next quickstart to use Redis Cache with an ASP.NET web app.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-147">Continue to the next quickstart to use Redis Cache with an ASP.NET web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a9dfb-148">Create an ASP.NET web app that uses an Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="a9dfb-148">Create an ASP.NET web app that uses an Azure Redis Cache.</span></span>](./cache-web-app-howto.md)



