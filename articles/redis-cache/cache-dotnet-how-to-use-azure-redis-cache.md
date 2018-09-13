---
title: Quickstart to learn how to Use Azure Redis Cache with .NET apps | Microsoft Docs
description: In this quickstart, learn how to access Azure Redis Cache from your .NET apps
services: redis-cache,app-service
documentationcenter: ''
author: wesmc7777
manager: cfowler
editor: ''
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 05/18/2018
ms.author: wesmc
ms.custom: mvc
ms.openlocfilehash: 31d93fc8b2034152e61d24a789bba62bfd3b7892
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818225"
---
# <a name="quickstart-use-azure-redis-cache-with-a-net-application"></a><span data-ttu-id="bcac9-103">Quickstart: Use Azure Redis Cache with a .NET application</span><span class="sxs-lookup"><span data-stu-id="bcac9-103">Quickstart: Use Azure Redis Cache with a .NET application</span></span>



<span data-ttu-id="bcac9-104">This quickstart shows you how to get started using Microsoft Azure Redis Cache with .NET.</span><span class="sxs-lookup"><span data-stu-id="bcac9-104">This quickstart shows you how to get started using Microsoft Azure Redis Cache with .NET.</span></span> <span data-ttu-id="bcac9-105">Microsoft Azure Redis Cache is based on the popular open-source Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="bcac9-105">Microsoft Azure Redis Cache is based on the popular open-source Redis Cache.</span></span> <span data-ttu-id="bcac9-106">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bcac9-106">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="bcac9-107">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bcac9-107">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="bcac9-108">In this quickstart, you will use the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) client with C\# code in a console app.</span><span class="sxs-lookup"><span data-stu-id="bcac9-108">In this quickstart, you will use the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) client with C\# code in a console app.</span></span> <span data-ttu-id="bcac9-109">You will create a cache and configure the .NET client app.</span><span class="sxs-lookup"><span data-stu-id="bcac9-109">You will create a cache and configure the .NET client app.</span></span> <span data-ttu-id="bcac9-110">Then, you will add, and update objects in the cache.</span><span class="sxs-lookup"><span data-stu-id="bcac9-110">Then, you will add, and update objects in the cache.</span></span> 

![Console app completed](./media/cache-dotnet-how-to-use-azure-redis-cache/cache-console-app-complete.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="bcac9-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bcac9-112">Prerequisites</span></span>

* [<span data-ttu-id="bcac9-113">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bcac9-113">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="bcac9-114">The StackExchange.Redis client requires [.NET Framework 4 or higher](https://www.microsoft.com/net/download/dotnet-framework-runtime).</span><span class="sxs-lookup"><span data-stu-id="bcac9-114">The StackExchange.Redis client requires [.NET Framework 4 or higher](https://www.microsoft.com/net/download/dotnet-framework-runtime).</span></span>

## <a name="create-a-cache"></a><span data-ttu-id="bcac9-115">Create a cache</span><span class="sxs-lookup"><span data-stu-id="bcac9-115">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

[!INCLUDE [redis-cache-access-keys](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="bcac9-116">Create a file on your computer named *CacheSecrets.config* and place it in a location where it won't be checked in with the source code of your sample application.</span><span class="sxs-lookup"><span data-stu-id="bcac9-116">Create a file on your computer named *CacheSecrets.config* and place it in a location where it won't be checked in with the source code of your sample application.</span></span> <span data-ttu-id="bcac9-117">For this quickstart, the *CacheSecrets.config* file is located here, *C:\AppSecrets\CacheSecrets.config*.</span><span class="sxs-lookup"><span data-stu-id="bcac9-117">For this quickstart, the *CacheSecrets.config* file is located here, *C:\AppSecrets\CacheSecrets.config*.</span></span>

<span data-ttu-id="bcac9-118">Edit the *CacheSecrets.config* file and add the following contents:</span><span class="sxs-lookup"><span data-stu-id="bcac9-118">Edit the *CacheSecrets.config* file and add the following contents:</span></span>

```xml
<appSettings>
    <add key="CacheConnection" value="<cache-name>.redis.cache.windows.net,abortConnect=false,ssl=true,password=<access-key>"/>
</appSettings>
```

<span data-ttu-id="bcac9-119">Replace `<cache-name>` with your cache host name.</span><span class="sxs-lookup"><span data-stu-id="bcac9-119">Replace `<cache-name>` with your cache host name.</span></span>

<span data-ttu-id="bcac9-120">Replace `<access-key>` with the primary key for your cache.</span><span class="sxs-lookup"><span data-stu-id="bcac9-120">Replace `<access-key>` with the primary key for your cache.</span></span>


## <a name="create-a-console-app"></a><span data-ttu-id="bcac9-121">Create a console app</span><span class="sxs-lookup"><span data-stu-id="bcac9-121">Create a console app</span></span>

<span data-ttu-id="bcac9-122">In Visual Studio, click **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="bcac9-122">In Visual Studio, click **File** > **New** > **Project**.</span></span>

<span data-ttu-id="bcac9-123">Under **Visual C#**, click **Windows Classic Desktop** and then click **Console App**, and **OK** to create a new console application.</span><span class="sxs-lookup"><span data-stu-id="bcac9-123">Under **Visual C#**, click **Windows Classic Desktop** and then click **Console App**, and **OK** to create a new console application.</span></span>


<a name="configure-the-cache-clients"></a>

## <a name="configure-the-cache-client"></a><span data-ttu-id="bcac9-124">Configure the cache client</span><span class="sxs-lookup"><span data-stu-id="bcac9-124">Configure the cache client</span></span>

<span data-ttu-id="bcac9-125">In this section, you will configure the console application to use the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) client for .NET.</span><span class="sxs-lookup"><span data-stu-id="bcac9-125">In this section, you will configure the console application to use the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) client for .NET.</span></span>

<span data-ttu-id="bcac9-126">In Visual Studio, click **Tools** > **NuGet Package Manager** > **Package Manager Console**, and run the following command from the Package Manager Console window.</span><span class="sxs-lookup"><span data-stu-id="bcac9-126">In Visual Studio, click **Tools** > **NuGet Package Manager** > **Package Manager Console**, and run the following command from the Package Manager Console window.</span></span>

```powershell
Install-Package StackExchange.Redis
```

<span data-ttu-id="bcac9-127">Once the installation is completed, the *StackExchange.Redis* cache client is available to use with your project.</span><span class="sxs-lookup"><span data-stu-id="bcac9-127">Once the installation is completed, the *StackExchange.Redis* cache client is available to use with your project.</span></span>


## <a name="connect-to-the-cache"></a><span data-ttu-id="bcac9-128">Connect to the cache</span><span class="sxs-lookup"><span data-stu-id="bcac9-128">Connect to the cache</span></span>

<span data-ttu-id="bcac9-129">In Visual Studio, open your *App.config* file and update it to include an `appSettings` `file` attribute that references the *CacheSecrets.config* file.</span><span class="sxs-lookup"><span data-stu-id="bcac9-129">In Visual Studio, open your *App.config* file and update it to include an `appSettings` `file` attribute that references the *CacheSecrets.config* file.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.1" />
    </startup>

    <appSettings file="C:\AppSecrets\CacheSecrets.config"></appSettings>  

</configuration>
```

<span data-ttu-id="bcac9-130">In Solution Explorer, right-click **References** and click **Add a reference**.</span><span class="sxs-lookup"><span data-stu-id="bcac9-130">In Solution Explorer, right-click **References** and click **Add a reference**.</span></span> <span data-ttu-id="bcac9-131">Add a reference to the **System.Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="bcac9-131">Add a reference to the **System.Configuration** assembly.</span></span>

<span data-ttu-id="bcac9-132">Add the following `using` statements to *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="bcac9-132">Add the following `using` statements to *Program.cs*:</span></span>

```csharp
using StackExchange.Redis;
using System.Configuration;
```

<span data-ttu-id="bcac9-133">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span><span class="sxs-lookup"><span data-stu-id="bcac9-133">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="bcac9-134">This class should be shared and reused throughout your client application.</span><span class="sxs-lookup"><span data-stu-id="bcac9-134">This class should be shared and reused throughout your client application.</span></span> <span data-ttu-id="bcac9-135">Do not create a new connection for each operation.</span><span class="sxs-lookup"><span data-stu-id="bcac9-135">Do not create a new connection for each operation.</span></span> 

<span data-ttu-id="bcac9-136">Never store credentials in source code.</span><span class="sxs-lookup"><span data-stu-id="bcac9-136">Never store credentials in source code.</span></span> <span data-ttu-id="bcac9-137">To keep this sample simple, I’m only using an external secrets config file.</span><span class="sxs-lookup"><span data-stu-id="bcac9-137">To keep this sample simple, I’m only using an external secrets config file.</span></span> <span data-ttu-id="bcac9-138">A better approach would be to use [Azure Key Vault with certificates](https://docs.microsoft.com/rest/api/keyvault/certificate-scenarios).</span><span class="sxs-lookup"><span data-stu-id="bcac9-138">A better approach would be to use [Azure Key Vault with certificates](https://docs.microsoft.com/rest/api/keyvault/certificate-scenarios).</span></span>

<span data-ttu-id="bcac9-139">In *Program.cs*, add the following members to the `Program` class of your console application:</span><span class="sxs-lookup"><span data-stu-id="bcac9-139">In *Program.cs*, add the following members to the `Program` class of your console application:</span></span>

```csharp
        private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
        {
            string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
            return ConnectionMultiplexer.Connect(cacheConnection);
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }
```


<span data-ttu-id="bcac9-140">This approach to sharing a `ConnectionMultiplexer` instance in your application uses a static property that returns a connected instance.</span><span class="sxs-lookup"><span data-stu-id="bcac9-140">This approach to sharing a `ConnectionMultiplexer` instance in your application uses a static property that returns a connected instance.</span></span> <span data-ttu-id="bcac9-141">The code provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span><span class="sxs-lookup"><span data-stu-id="bcac9-141">The code provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="bcac9-142">`abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span><span class="sxs-lookup"><span data-stu-id="bcac9-142">`abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="bcac9-143">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span><span class="sxs-lookup"><span data-stu-id="bcac9-143">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

<span data-ttu-id="bcac9-144">The value of the *CacheConnection* appSetting is used to reference the cache connection string from the Azure portal as the password parameter.</span><span class="sxs-lookup"><span data-stu-id="bcac9-144">The value of the *CacheConnection* appSetting is used to reference the cache connection string from the Azure portal as the password parameter.</span></span>

## <a name="executing-cache-commands"></a><span data-ttu-id="bcac9-145">Executing cache commands</span><span class="sxs-lookup"><span data-stu-id="bcac9-145">Executing cache commands</span></span>

<span data-ttu-id="bcac9-146">Add the following code for the `Main` procedure of the `Program` class for your console application:</span><span class="sxs-lookup"><span data-stu-id="bcac9-146">Add the following code for the `Main` procedure of the `Program` class for your console application:</span></span>

```csharp
        static void Main(string[] args)
        {
            // Connection refers to a property that returns a ConnectionMultiplexer
            // as shown in the previous example.
            IDatabase cache = lazyConnection.Value.GetDatabase();

            // Perform cache operations using the cache object...

            // Simple PING command
            string cacheCommand = "PING";
            Console.WriteLine("\nCache command  : " + cacheCommand);
            Console.WriteLine("Cache response : " + cache.Execute(cacheCommand).ToString());

            // Simple get and put of integral data types into the cache
            cacheCommand = "GET Message";
            Console.WriteLine("\nCache command  : " + cacheCommand + " or StringGet()");
            Console.WriteLine("Cache response : " + cache.StringGet("Message").ToString());

            cacheCommand = "SET Message \"Hello! The cache is working from a .NET console app!\"";
            Console.WriteLine("\nCache command  : " + cacheCommand + " or StringSet()");
            Console.WriteLine("Cache response : " + cache.StringSet("Message", "Hello! The cache is working from a .NET console app!").ToString());

            // Demostrate "SET Message" executed as expected...
            cacheCommand = "GET Message";
            Console.WriteLine("\nCache command  : " + cacheCommand + " or StringGet()");
            Console.WriteLine("Cache response : " + cache.StringGet("Message").ToString());

            // Get the client list, useful to see if connection list is growing...
            cacheCommand = "CLIENT LIST";
            Console.WriteLine("\nCache command  : " + cacheCommand);
            Console.WriteLine("Cache response : \n" + cache.Execute("CLIENT", "LIST").ToString().Replace("id=", "id="));

            lazyConnection.Value.Dispose();
        }
```

Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache. The code connects to the default database, DB 0. <span data-ttu-id="bcac9-149">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="bcac9-149">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="bcac9-150">Cache items can be stored and retrieved by using the `StringSet` and `StringGet` methods.</span><span class="sxs-lookup"><span data-stu-id="bcac9-150">Cache items can be stored and retrieved by using the `StringSet` and `StringGet` methods.</span></span>

<span data-ttu-id="bcac9-151">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span><span class="sxs-lookup"><span data-stu-id="bcac9-151">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="bcac9-152">Press **Ctrl+F5** to build and run the console app.</span><span class="sxs-lookup"><span data-stu-id="bcac9-152">Press **Ctrl+F5** to build and run the console app.</span></span>

<span data-ttu-id="bcac9-153">In the example below, you can see the `Message` key previously had a cached value, which was set using the Redis Console in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bcac9-153">In the example below, you can see the `Message` key previously had a cached value, which was set using the Redis Console in the Azure portal.</span></span> <span data-ttu-id="bcac9-154">The app updated that cached value.</span><span class="sxs-lookup"><span data-stu-id="bcac9-154">The app updated that cached value.</span></span> <span data-ttu-id="bcac9-155">The app also executed the `PING` and `CLIENT LIST` commands.</span><span class="sxs-lookup"><span data-stu-id="bcac9-155">The app also executed the `PING` and `CLIENT LIST` commands.</span></span>

![Console app partial](./media/cache-dotnet-how-to-use-azure-redis-cache/cache-console-app-partial.png)


## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="bcac9-157">Work with .NET objects in the cache</span><span class="sxs-lookup"><span data-stu-id="bcac9-157">Work with .NET objects in the cache</span></span>

<span data-ttu-id="bcac9-158">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span><span class="sxs-lookup"><span data-stu-id="bcac9-158">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="bcac9-159">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span><span class="sxs-lookup"><span data-stu-id="bcac9-159">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="bcac9-160">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) and serialize to and from JSON.</span><span class="sxs-lookup"><span data-stu-id="bcac9-160">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) and serialize to and from JSON.</span></span> <span data-ttu-id="bcac9-161">In this section, you will add a .NET object to the cache.</span><span class="sxs-lookup"><span data-stu-id="bcac9-161">In this section, you will add a .NET object to the cache.</span></span>

<span data-ttu-id="bcac9-162">In Visual Studio, click **Tools** > **NuGet Package Manager** > **Package Manager Console**, and run the following command from the Package Manager Console window.</span><span class="sxs-lookup"><span data-stu-id="bcac9-162">In Visual Studio, click **Tools** > **NuGet Package Manager** > **Package Manager Console**, and run the following command from the Package Manager Console window.</span></span>

```powershell
Install-Package Newtonsoft.Json
```

<span data-ttu-id="bcac9-163">Add the following `using` statement to the top of *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="bcac9-163">Add the following `using` statement to the top of *Program.cs*:</span></span>

```charp
using Newtonsoft.Json;
```

<span data-ttu-id="bcac9-164">Add the following `Employee` class definition to *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="bcac9-164">Add the following `Employee` class definition to *Program.cs*:</span></span>

```csharp
        class Employee
        {
            public string Id { get; set; }
            public string Name { get; set; }
            public int Age { get; set; }

            public Employee(string EmployeeId, string Name, int Age)
            {
                this.Id = EmployeeId;
                this.Name = Name;
                this.Age = Age;
            }
        }
```

<span data-ttu-id="bcac9-165">At the bottom of `Main()` procedure in *Program.cs*, and before the call to `Dispose()`, add the following lines of code to cache and retrieve a serialized .NET object:</span><span class="sxs-lookup"><span data-stu-id="bcac9-165">At the bottom of `Main()` procedure in *Program.cs*, and before the call to `Dispose()`, add the following lines of code to cache and retrieve a serialized .NET object:</span></span>

```csharp
            // Store .NET object to cache
            Employee e007 = new Employee("007", "Davide Columbo", 100);
            Console.WriteLine("Cache response from storing Employee .NET object : " + 
                cache.StringSet("e007", JsonConvert.SerializeObject(e007)));

            // Retrieve .NET object from cache
            Employee e007FromCache = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e007"));
            Console.WriteLine("Deserialized Employee .NET object :\n");
            Console.WriteLine("\tEmployee.Name : " + e007FromCache.Name);
            Console.WriteLine("\tEmployee.Id   : " + e007FromCache.Id);
            Console.WriteLine("\tEmployee.Age  : " + e007FromCache.Age + "\n");
```

<span data-ttu-id="bcac9-166">Press **Ctrl+F5** to build and run the console app to test serialization of .NET objects.</span><span class="sxs-lookup"><span data-stu-id="bcac9-166">Press **Ctrl+F5** to build and run the console app to test serialization of .NET objects.</span></span> 

![Console app completed](./media/cache-dotnet-how-to-use-azure-redis-cache/cache-console-app-complete.png)


## <a name="clean-up-resources"></a><span data-ttu-id="bcac9-168">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="bcac9-168">Clean up resources</span></span>

<span data-ttu-id="bcac9-169">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them.</span><span class="sxs-lookup"><span data-stu-id="bcac9-169">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them.</span></span>

<span data-ttu-id="bcac9-170">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="bcac9-170">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bcac9-171">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="bcac9-171">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="bcac9-172">Make sure that you do not accidentally delete the wrong resource group or resources.</span><span class="sxs-lookup"><span data-stu-id="bcac9-172">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="bcac9-173">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="bcac9-173">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span></span>
>

<span data-ttu-id="bcac9-174">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="bcac9-174">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>

<span data-ttu-id="bcac9-175">In the **Filter by name...** textbox, type the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="bcac9-175">In the **Filter by name...** textbox, type the name of your resource group.</span></span> <span data-ttu-id="bcac9-176">The instructions for this article used a resource group named *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="bcac9-176">The instructions for this article used a resource group named *TestResources*.</span></span> <span data-ttu-id="bcac9-177">On your resource group in the result list, click **...** then **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="bcac9-177">On your resource group in the result list, click **...** then **Delete resource group**.</span></span>

![Delete](./media/cache-dotnet-how-to-use-azure-redis-cache/cache-delete-resource-group.png)

<span data-ttu-id="bcac9-179">You will be asked to confirm the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="bcac9-179">You will be asked to confirm the deletion of the resource group.</span></span> <span data-ttu-id="bcac9-180">Type the name of your resource group to confirm, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="bcac9-180">Type the name of your resource group to confirm, and click **Delete**.</span></span>

<span data-ttu-id="bcac9-181">After a few moments, the resource group and all of its contained resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="bcac9-181">After a few moments, the resource group and all of its contained resources are deleted.</span></span>



<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="bcac9-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="bcac9-182">Next steps</span></span>

<span data-ttu-id="bcac9-183">In this quickstart, you learned how to use Azure Redis Cache from a .NET application.</span><span class="sxs-lookup"><span data-stu-id="bcac9-183">In this quickstart, you learned how to use Azure Redis Cache from a .NET application.</span></span> <span data-ttu-id="bcac9-184">Continue to the next quickstart to use Redis Cache with an ASP.NET web app.</span><span class="sxs-lookup"><span data-stu-id="bcac9-184">Continue to the next quickstart to use Redis Cache with an ASP.NET web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bcac9-185">Create an ASP.NET web app that uses an Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="bcac9-185">Create an ASP.NET web app that uses an Azure Redis Cache.</span></span>](./cache-web-app-howto.md)


