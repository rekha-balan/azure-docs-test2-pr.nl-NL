---
title: Create an ASP.NET web app with Azure Redis Cache | Microsoft Docs
description: In this quickstart, you learn how to create an ASP.NET web app with Azure Redis Cache
services: redis-cache
documentationcenter: ''
author: wesmc7777
manager: cfowler
editor: ''
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: quickstart
ms.date: 03/26/2018
ms.author: wesmc
ms.custom: mvc
ms.openlocfilehash: a92621d852ec60fb4773957d71dc6a55caaf991c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44824374"
---
# <a name="quickstart-create-an-aspnet-web-app"></a><span data-ttu-id="e701b-103">Quickstart: Create an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="e701b-103">Quickstart: Create an ASP.NET web app</span></span> 

## <a name="introduction"></a><span data-ttu-id="e701b-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="e701b-104">Introduction</span></span>

<span data-ttu-id="e701b-105">This quickstart shows how to create and deploy an ASP.NET web application to Azure App Service by using Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e701b-105">This quickstart shows how to create and deploy an ASP.NET web application to Azure App Service by using Visual Studio 2017.</span></span> <span data-ttu-id="e701b-106">The sample application connects to Azure Redis Cache to store and retrieve data from the cache.</span><span class="sxs-lookup"><span data-stu-id="e701b-106">The sample application connects to Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="e701b-107">After you finish the quickstart, you'll have a running web app, hosted in Azure, that reads and writes to Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="e701b-107">After you finish the quickstart, you'll have a running web app, hosted in Azure, that reads and writes to Azure Redis Cache.</span></span>

![Simple test completed Azure](./media/cache-web-app-howto/cache-simple-test-complete-azure.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="e701b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e701b-109">Prerequisites</span></span>

<span data-ttu-id="e701b-110">To complete the quickstart, you need to install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following environments:</span><span class="sxs-lookup"><span data-stu-id="e701b-110">To complete the quickstart, you need to install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following environments:</span></span>
* <span data-ttu-id="e701b-111">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="e701b-111">ASP.NET and web development</span></span>
* <span data-ttu-id="e701b-112">Azure development</span><span class="sxs-lookup"><span data-stu-id="e701b-112">Azure development</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="e701b-113">Create the Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="e701b-113">Create the Visual Studio project</span></span>

1. <span data-ttu-id="e701b-114">Open Visual Studio, and then and select **File** >**New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="e701b-114">Open Visual Studio, and then and select **File** >**New** > **Project**.</span></span>

2. <span data-ttu-id="e701b-115">In the **New Project** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="e701b-115">In the **New Project** dialog box, take the following steps:</span></span>

    ![Create project](./media/cache-web-app-howto/cache-create-project.png)

    <span data-ttu-id="e701b-117">a.</span><span class="sxs-lookup"><span data-stu-id="e701b-117">a.</span></span> <span data-ttu-id="e701b-118">In the **Templates** list, expand the **Visual C#** node.</span><span class="sxs-lookup"><span data-stu-id="e701b-118">In the **Templates** list, expand the **Visual C#** node.</span></span>

    <span data-ttu-id="e701b-119">b.</span><span class="sxs-lookup"><span data-stu-id="e701b-119">b.</span></span> <span data-ttu-id="e701b-120">Select **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="e701b-120">Select **Cloud**.</span></span>

    <span data-ttu-id="e701b-121">c.</span><span class="sxs-lookup"><span data-stu-id="e701b-121">c.</span></span> <span data-ttu-id="e701b-122">Select **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="e701b-122">Select **ASP.NET Web Application**.</span></span>

    <span data-ttu-id="e701b-123">d.</span><span class="sxs-lookup"><span data-stu-id="e701b-123">d.</span></span> <span data-ttu-id="e701b-124">Verify that **.NET Framework 4.5.2** or higher is selected.</span><span class="sxs-lookup"><span data-stu-id="e701b-124">Verify that **.NET Framework 4.5.2** or higher is selected.</span></span>

    <span data-ttu-id="e701b-125">e.</span><span class="sxs-lookup"><span data-stu-id="e701b-125">e.</span></span> <span data-ttu-id="e701b-126">In the **Name** box, give the project a name.</span><span class="sxs-lookup"><span data-stu-id="e701b-126">In the **Name** box, give the project a name.</span></span> <span data-ttu-id="e701b-127">For this example, we used **ContosoTeamStats**.</span><span class="sxs-lookup"><span data-stu-id="e701b-127">For this example, we used **ContosoTeamStats**.</span></span>

    <span data-ttu-id="e701b-128">f.</span><span class="sxs-lookup"><span data-stu-id="e701b-128">f.</span></span> <span data-ttu-id="e701b-129">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="e701b-129">Select **OK**.</span></span>
   
3. <span data-ttu-id="e701b-130">Select **MVC** as the project type.</span><span class="sxs-lookup"><span data-stu-id="e701b-130">Select **MVC** as the project type.</span></span>

4. <span data-ttu-id="e701b-131">Make sure that **No Authentication** is specified for the **Authentication** settings.</span><span class="sxs-lookup"><span data-stu-id="e701b-131">Make sure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="e701b-132">Depending on your version of Visual Studio, the default **Authentication** setting might be something else.</span><span class="sxs-lookup"><span data-stu-id="e701b-132">Depending on your version of Visual Studio, the default **Authentication** setting might be something else.</span></span> <span data-ttu-id="e701b-133">To change it, select **Change Authentication** and then **No Authentication**.</span><span class="sxs-lookup"><span data-stu-id="e701b-133">To change it, select **Change Authentication** and then **No Authentication**.</span></span>

5. <span data-ttu-id="e701b-134">Select **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="e701b-134">Select **OK** to create the project.</span></span>

## <a name="create-a-cache"></a><span data-ttu-id="e701b-135">Create a cache</span><span class="sxs-lookup"><span data-stu-id="e701b-135">Create a cache</span></span>

<span data-ttu-id="e701b-136">Next, you create the cache for the app.</span><span class="sxs-lookup"><span data-stu-id="e701b-136">Next, you create the cache for the app.</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

[!INCLUDE [redis-cache-access-keys](../../includes/redis-cache-access-keys.md)]

#### <a name="to-edit-the-cachesecretsconfig-file"></a><span data-ttu-id="e701b-137">To edit the *CacheSecrets.config* file</span><span class="sxs-lookup"><span data-stu-id="e701b-137">To edit the *CacheSecrets.config* file</span></span>

3. <span data-ttu-id="e701b-138">Create a file on your computer named *CacheSecrets.config*. Put it in a location where it won't be checked in with the source code of your sample application.</span><span class="sxs-lookup"><span data-stu-id="e701b-138">Create a file on your computer named *CacheSecrets.config*. Put it in a location where it won't be checked in with the source code of your sample application.</span></span> <span data-ttu-id="e701b-139">For this quickstart, the *CacheSecrets.config* file is located at *C:\AppSecrets\CacheSecrets.config*.</span><span class="sxs-lookup"><span data-stu-id="e701b-139">For this quickstart, the *CacheSecrets.config* file is located at *C:\AppSecrets\CacheSecrets.config*.</span></span>

4. <span data-ttu-id="e701b-140">Edit the *CacheSecrets.config* file.</span><span class="sxs-lookup"><span data-stu-id="e701b-140">Edit the *CacheSecrets.config* file.</span></span> <span data-ttu-id="e701b-141">Then add the following content:</span><span class="sxs-lookup"><span data-stu-id="e701b-141">Then add the following content:</span></span>

    ```xml
    <appSettings>
        <add key="CacheConnection" value="<cache-name>.redis.cache.windows.net,abortConnect=false,ssl=true,password=<access-key>"/>
    </appSettings>
    ```

5. <span data-ttu-id="e701b-142">Replace `<cache-name>` with your cache host name.</span><span class="sxs-lookup"><span data-stu-id="e701b-142">Replace `<cache-name>` with your cache host name.</span></span>

6. <span data-ttu-id="e701b-143">Replace `<access-key>` with the primary key for your cache.</span><span class="sxs-lookup"><span data-stu-id="e701b-143">Replace `<access-key>` with the primary key for your cache.</span></span>

    > [!TIP]
    > <span data-ttu-id="e701b-144">You can use the secondary access key during key rotation as an alternate key while you regenerate the primary access key.</span><span class="sxs-lookup"><span data-stu-id="e701b-144">You can use the secondary access key during key rotation as an alternate key while you regenerate the primary access key.</span></span>
>
7. <span data-ttu-id="e701b-145">Save the file.</span><span class="sxs-lookup"><span data-stu-id="e701b-145">Save the file.</span></span>

## <a name="update-the-mvc-application"></a><span data-ttu-id="e701b-146">Update the MVC application</span><span class="sxs-lookup"><span data-stu-id="e701b-146">Update the MVC application</span></span>

<span data-ttu-id="e701b-147">In this section, you update the application to support a new view that displays a simple test against Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="e701b-147">In this section, you update the application to support a new view that displays a simple test against Azure Redis Cache.</span></span>

* [<span data-ttu-id="e701b-148">Update the web.config file with an app setting for the cache</span><span class="sxs-lookup"><span data-stu-id="e701b-148">Update the web.config file with an app setting for the cache</span></span>](#Update-the-webconfig-file-with-an-app-setting-for-the-cache)
* [<span data-ttu-id="e701b-149">Configure the application to use the StackExchange.Redis client</span><span class="sxs-lookup"><span data-stu-id="e701b-149">Configure the application to use the StackExchange.Redis client</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="e701b-150">Update the HomeController and Layout</span><span class="sxs-lookup"><span data-stu-id="e701b-150">Update the HomeController and Layout</span></span>](#update-the-homecontroller-and-layout)
* [<span data-ttu-id="e701b-151">Add a new RedisCache view</span><span class="sxs-lookup"><span data-stu-id="e701b-151">Add a new RedisCache view</span></span>](#add-a-new-rediscache-view)

### <a name="update-the-webconfig-file-with-an-app-setting-for-the-cache"></a><span data-ttu-id="e701b-152">Update the web.config file with an app setting for the cache</span><span class="sxs-lookup"><span data-stu-id="e701b-152">Update the web.config file with an app setting for the cache</span></span>

<span data-ttu-id="e701b-153">When you run the application locally, the information in *CacheSecrets.config* is used to connect to your Azure Redis Cache instance.</span><span class="sxs-lookup"><span data-stu-id="e701b-153">When you run the application locally, the information in *CacheSecrets.config* is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="e701b-154">Later you deploy this application to Azure.</span><span class="sxs-lookup"><span data-stu-id="e701b-154">Later you deploy this application to Azure.</span></span> <span data-ttu-id="e701b-155">At that time, you configure an app setting in Azure that the application uses to retrieve the cache connection information instead of this file.</span><span class="sxs-lookup"><span data-stu-id="e701b-155">At that time, you configure an app setting in Azure that the application uses to retrieve the cache connection information instead of this file.</span></span> 

<span data-ttu-id="e701b-156">Because the file *CacheSecrets.config* isn't deployed to Azure with your application, you only use it while testing the application locally.</span><span class="sxs-lookup"><span data-stu-id="e701b-156">Because the file *CacheSecrets.config* isn't deployed to Azure with your application, you only use it while testing the application locally.</span></span> <span data-ttu-id="e701b-157">Keep this information as secure as possible to prevent malicious access to your cache data.</span><span class="sxs-lookup"><span data-stu-id="e701b-157">Keep this information as secure as possible to prevent malicious access to your cache data.</span></span>

#### <a name="to-update-the-webconfig-file"></a><span data-ttu-id="e701b-158">To update the *web.config* file</span><span class="sxs-lookup"><span data-stu-id="e701b-158">To update the *web.config* file</span></span>
1. <span data-ttu-id="e701b-159">In **Solution Explorer**, double-click the *web.config* file to open it.</span><span class="sxs-lookup"><span data-stu-id="e701b-159">In **Solution Explorer**, double-click the *web.config* file to open it.</span></span>

    ![Web.config](./media/cache-web-app-howto/cache-web-config.png)

2. <span data-ttu-id="e701b-161">In the *web.config* file, find the `<appSetting>` element.</span><span class="sxs-lookup"><span data-stu-id="e701b-161">In the *web.config* file, find the `<appSetting>` element.</span></span> <span data-ttu-id="e701b-162">Then add the following `file` attribute.</span><span class="sxs-lookup"><span data-stu-id="e701b-162">Then add the following `file` attribute.</span></span> <span data-ttu-id="e701b-163">If you used a different file name or location, substitute those values for the ones that are shown in the example.</span><span class="sxs-lookup"><span data-stu-id="e701b-163">If you used a different file name or location, substitute those values for the ones that are shown in the example.</span></span>

* <span data-ttu-id="e701b-164">Before: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="e701b-164">Before: `<appSettings>`</span></span>
* <span data-ttu-id="e701b-165">After: ` <appSettings file="C:\AppSecrets\CacheSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="e701b-165">After: ` <appSettings file="C:\AppSecrets\CacheSecrets.config">`</span></span>

<span data-ttu-id="e701b-166">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span><span class="sxs-lookup"><span data-stu-id="e701b-166">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="e701b-167">The runtime ignores the file attribute if the specified file can't be found.</span><span class="sxs-lookup"><span data-stu-id="e701b-167">The runtime ignores the file attribute if the specified file can't be found.</span></span> <span data-ttu-id="e701b-168">Your secrets (the connection string to your cache) aren't included as part of the source code for the application.</span><span class="sxs-lookup"><span data-stu-id="e701b-168">Your secrets (the connection string to your cache) aren't included as part of the source code for the application.</span></span> <span data-ttu-id="e701b-169">When you deploy your web app to Azure, the *CacheSecrests.config* file isn't deployed.</span><span class="sxs-lookup"><span data-stu-id="e701b-169">When you deploy your web app to Azure, the *CacheSecrests.config* file isn't deployed.</span></span>

### <a name="to-configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="e701b-170">To configure the application to use StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="e701b-170">To configure the application to use StackExchange.Redis</span></span>

1. <span data-ttu-id="e701b-171">To configure the app to use the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) NuGet package for Visual Studio, select **Tools > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e701b-171">To configure the app to use the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) NuGet package for Visual Studio, select **Tools > NuGet Package Manager > Package Manager Console**.</span></span>

2. <span data-ttu-id="e701b-172">Run the following command from the `Package Manager Console` window:</span><span class="sxs-lookup"><span data-stu-id="e701b-172">Run the following command from the `Package Manager Console` window:</span></span>

    ```powershell
    Install-Package StackExchange.Redis
    ```

3. <span data-ttu-id="e701b-173">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span><span class="sxs-lookup"><span data-stu-id="e701b-173">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="e701b-174">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span><span class="sxs-lookup"><span data-stu-id="e701b-174">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>

### <a name="to-update-the-homecontroller-and-layout"></a><span data-ttu-id="e701b-175">To update the HomeController and Layout</span><span class="sxs-lookup"><span data-stu-id="e701b-175">To update the HomeController and Layout</span></span>

1. <span data-ttu-id="e701b-176">In **Solution Explorer**, expand the **Controllers** folder, and then open the *HomeController.cs* file.</span><span class="sxs-lookup"><span data-stu-id="e701b-176">In **Solution Explorer**, expand the **Controllers** folder, and then open the *HomeController.cs* file.</span></span>

2. <span data-ttu-id="e701b-177">Add the following two `using` statements at the top of the file to support the cache client and app settings.</span><span class="sxs-lookup"><span data-stu-id="e701b-177">Add the following two `using` statements at the top of the file to support the cache client and app settings.</span></span>

    ```csharp
    using System.Configuration;
    using StackExchange.Redis;
    ```

3. <span data-ttu-id="e701b-178">Add the following method to the `HomeController` class to support a new `RedisCache` action that runs some commands against the new cache.</span><span class="sxs-lookup"><span data-stu-id="e701b-178">Add the following method to the `HomeController` class to support a new `RedisCache` action that runs some commands against the new cache.</span></span>

    ```csharp
        public ActionResult RedisCache()
        {
            ViewBag.Message = "A simple example with Azure Redis Cache on ASP.NET.";

            var lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
            {
                string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
                return ConnectionMultiplexer.Connect(cacheConnection);
            });

            // Connection refers to a property that returns a ConnectionMultiplexer
            // as shown in the previous example.
            IDatabase cache = lazyConnection.Value.GetDatabase();

            // Perform cache operations using the cache object...

            // Simple PING command
            ViewBag.command1 = "PING";
            ViewBag.command1Result = cache.Execute(ViewBag.command1).ToString();

            // Simple get and put of integral data types into the cache
            ViewBag.command2 = "GET Message";
            ViewBag.command2Result = cache.StringGet("Message").ToString();

            ViewBag.command3 = "SET Message \"Hello! The cache is working from ASP.NET!\"";
            ViewBag.command3Result = cache.StringSet("Message", "Hello! The cache is working from ASP.NET!").ToString();

            // Demostrate "SET Message" executed as expected...
            ViewBag.command4 = "GET Message";
            ViewBag.command4Result = cache.StringGet("Message").ToString();

            // Get the client list, useful to see if connection list is growing...
            ViewBag.command5 = "CLIENT LIST";
            ViewBag.command5Result = cache.Execute("CLIENT", "LIST").ToString().Replace(" id=", "\rid=");

            lazyConnection.Value.Dispose();

            return View();
        }
    ```

4. In **Solution Explorer**, expand the **Views** > **Shared** folder. <span data-ttu-id="e701b-180">Then open the *_Layout.cshtml* file.</span><span class="sxs-lookup"><span data-stu-id="e701b-180">Then open the *_Layout.cshtml* file.</span></span>

    <span data-ttu-id="e701b-181">Replace:</span><span class="sxs-lookup"><span data-stu-id="e701b-181">Replace:</span></span>

        ```csharp
        @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })
        ```

    <span data-ttu-id="e701b-182">with:</span><span class="sxs-lookup"><span data-stu-id="e701b-182">with:</span></span>

        ```csharp
        @Html.ActionLink("Azure Redis Cache Test", "RedisCache", "Home", new { area = "" }, new { @class = "navbar-brand" })
        ```

### <a name="to-add-a-new-rediscache-view"></a><span data-ttu-id="e701b-183">To add a new RedisCache view</span><span class="sxs-lookup"><span data-stu-id="e701b-183">To add a new RedisCache view</span></span>

1. <span data-ttu-id="e701b-184">In **Solution Explorer**, expand the **Views** folder, and then right-click the **Home** folder.</span><span class="sxs-lookup"><span data-stu-id="e701b-184">In **Solution Explorer**, expand the **Views** folder, and then right-click the **Home** folder.</span></span> <span data-ttu-id="e701b-185">Choose **Add** > **View...**.</span><span class="sxs-lookup"><span data-stu-id="e701b-185">Choose **Add** > **View...**.</span></span>

2. <span data-ttu-id="e701b-186">In the **Add View** dialog box, enter **RedisCache** for the View Name.</span><span class="sxs-lookup"><span data-stu-id="e701b-186">In the **Add View** dialog box, enter **RedisCache** for the View Name.</span></span> <span data-ttu-id="e701b-187">Then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="e701b-187">Then select **Add**.</span></span>

3. <span data-ttu-id="e701b-188">Replace the code in the *RedisCache.cshtml* file with the following code:</span><span class="sxs-lookup"><span data-stu-id="e701b-188">Replace the code in the *RedisCache.cshtml* file with the following code:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Azure Redis Cache Test";
    }

    <h2>@ViewBag.Title.</h2>
    <h3>@ViewBag.Message</h3>
    <br /><br />
    <table border="1" cellpadding="10">
        <tr>
            <th>Command</th>
            <th>Result</th>
        </tr>
        <tr>
            <td>@ViewBag.command1</td>
            <td><pre>@ViewBag.command1Result</pre></td>
        </tr>
        <tr>
            <td>@ViewBag.command2</td>
            <td><pre>@ViewBag.command2Result</pre></td>
        </tr>
        <tr>
            <td>@ViewBag.command3</td>
            <td><pre>@ViewBag.command3Result</pre></td>
        </tr>
        <tr>
            <td>@ViewBag.command4</td>
            <td><pre>@ViewBag.command4Result</pre></td>
        </tr>
        <tr>
            <td>@ViewBag.command5</td>
            <td><pre>@ViewBag.command5Result</pre></td>
        </tr>
    </table>
    ```

## <a name="run-the-app-locally"></a><span data-ttu-id="e701b-189">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="e701b-189">Run the app locally</span></span>

<span data-ttu-id="e701b-190">By default, the project is configured to host the app locally in [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) for testing and debugging.</span><span class="sxs-lookup"><span data-stu-id="e701b-190">By default, the project is configured to host the app locally in [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) for testing and debugging.</span></span>

### <a name="to-run-the-app-locally"></a><span data-ttu-id="e701b-191">To run the app locally</span><span class="sxs-lookup"><span data-stu-id="e701b-191">To run the app locally</span></span>
1. <span data-ttu-id="e701b-192">In Visual Studio, select **Debug** > **Start Debugging** to build and start the app locally for testing and debugging.</span><span class="sxs-lookup"><span data-stu-id="e701b-192">In Visual Studio, select **Debug** > **Start Debugging** to build and start the app locally for testing and debugging.</span></span>

2. <span data-ttu-id="e701b-193">In the browser, select **Azure Redis Cache Test** on the navigation bar.</span><span class="sxs-lookup"><span data-stu-id="e701b-193">In the browser, select **Azure Redis Cache Test** on the navigation bar.</span></span>

3. <span data-ttu-id="e701b-194">In the following example, the `Message` key previously had a cached value, which was set by using the Azure Redis Cache console in the portal.</span><span class="sxs-lookup"><span data-stu-id="e701b-194">In the following example, the `Message` key previously had a cached value, which was set by using the Azure Redis Cache console in the portal.</span></span> <span data-ttu-id="e701b-195">The app updated that cached value.</span><span class="sxs-lookup"><span data-stu-id="e701b-195">The app updated that cached value.</span></span> <span data-ttu-id="e701b-196">The app also executed the `PING` and `CLIENT LIST` commands.</span><span class="sxs-lookup"><span data-stu-id="e701b-196">The app also executed the `PING` and `CLIENT LIST` commands.</span></span>

    ![Simple test completed local](./media/cache-web-app-howto/cache-simple-test-complete-local.png)

## <a name="publish-and-run-in-azure"></a><span data-ttu-id="e701b-198">Publish and run in Azure</span><span class="sxs-lookup"><span data-stu-id="e701b-198">Publish and run in Azure</span></span>

<span data-ttu-id="e701b-199">After you successfully test the app locally, you can deploy the app to Azure and run it in the cloud.</span><span class="sxs-lookup"><span data-stu-id="e701b-199">After you successfully test the app locally, you can deploy the app to Azure and run it in the cloud.</span></span>

### <a name="to-publish-the-app-to-azure"></a><span data-ttu-id="e701b-200">To publish the app to Azure</span><span class="sxs-lookup"><span data-stu-id="e701b-200">To publish the app to Azure</span></span>

1. <span data-ttu-id="e701b-201">In Visual Studio, right-click the project node in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="e701b-201">In Visual Studio, right-click the project node in Solution Explorer.</span></span> <span data-ttu-id="e701b-202">Then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="e701b-202">Then select **Publish**.</span></span>

    ![Publish](./media/cache-web-app-howto/cache-publish-app.png)

2. <span data-ttu-id="e701b-204">Select **Microsoft Azure App Service**, select **Create New**, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="e701b-204">Select **Microsoft Azure App Service**, select **Create New**, and then select **Publish**.</span></span>

    ![Publish to App Service](./media/cache-web-app-howto/cache-publish-to-app-service.png)

3. <span data-ttu-id="e701b-206">In the **Create App Service** dialog box, make the following changes:</span><span class="sxs-lookup"><span data-stu-id="e701b-206">In the **Create App Service** dialog box, make the following changes:</span></span>

    | <span data-ttu-id="e701b-207">Setting</span><span class="sxs-lookup"><span data-stu-id="e701b-207">Setting</span></span> | <span data-ttu-id="e701b-208">Recommended value</span><span class="sxs-lookup"><span data-stu-id="e701b-208">Recommended value</span></span> | <span data-ttu-id="e701b-209">Description</span><span class="sxs-lookup"><span data-stu-id="e701b-209">Description</span></span> |
    | ------- | :---------------: | ----------- |
    | <span data-ttu-id="e701b-210">**App name**</span><span class="sxs-lookup"><span data-stu-id="e701b-210">**App name**</span></span> | <span data-ttu-id="e701b-211">Use the default.</span><span class="sxs-lookup"><span data-stu-id="e701b-211">Use the default.</span></span> | <span data-ttu-id="e701b-212">The app name is the host name for the app when it's deployed to Azure.</span><span class="sxs-lookup"><span data-stu-id="e701b-212">The app name is the host name for the app when it's deployed to Azure.</span></span> <span data-ttu-id="e701b-213">The name might have a timestamp suffix added to it to make it unique if necessary.</span><span class="sxs-lookup"><span data-stu-id="e701b-213">The name might have a timestamp suffix added to it to make it unique if necessary.</span></span> |
    | <span data-ttu-id="e701b-214">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="e701b-214">**Subscription**</span></span> | <span data-ttu-id="e701b-215">Choose your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e701b-215">Choose your Azure subscription.</span></span> | <span data-ttu-id="e701b-216">This subscription is charged for any related hosting costs.</span><span class="sxs-lookup"><span data-stu-id="e701b-216">This subscription is charged for any related hosting costs.</span></span> <span data-ttu-id="e701b-217">If you have multiple Azure subscriptions, verify that the subscription that you want is selected.</span><span class="sxs-lookup"><span data-stu-id="e701b-217">If you have multiple Azure subscriptions, verify that the subscription that you want is selected.</span></span>|
    | <span data-ttu-id="e701b-218">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="e701b-218">**Resource group**</span></span> | <span data-ttu-id="e701b-219">Use the same resource group where you created the cache (for example, *TestResourceGroup*).</span><span class="sxs-lookup"><span data-stu-id="e701b-219">Use the same resource group where you created the cache (for example, *TestResourceGroup*).</span></span> | <span data-ttu-id="e701b-220">The resource group helps you manage all resources as a group.</span><span class="sxs-lookup"><span data-stu-id="e701b-220">The resource group helps you manage all resources as a group.</span></span> <span data-ttu-id="e701b-221">Later, when you want to delete the app, you can just delete the group.</span><span class="sxs-lookup"><span data-stu-id="e701b-221">Later, when you want to delete the app, you can just delete the group.</span></span> |
    | <span data-ttu-id="e701b-222">**App Service plan**</span><span class="sxs-lookup"><span data-stu-id="e701b-222">**App Service plan**</span></span> | <span data-ttu-id="e701b-223">Select **New**, and then create a new App Service plan named *TestingPlan*.</span><span class="sxs-lookup"><span data-stu-id="e701b-223">Select **New**, and then create a new App Service plan named *TestingPlan*.</span></span> <br /><span data-ttu-id="e701b-224">Use the same **Location** you used when creating your cache.</span><span class="sxs-lookup"><span data-stu-id="e701b-224">Use the same **Location** you used when creating your cache.</span></span> <br /><span data-ttu-id="e701b-225">Choose **Free** for the size.</span><span class="sxs-lookup"><span data-stu-id="e701b-225">Choose **Free** for the size.</span></span> | <span data-ttu-id="e701b-226">An App Service plan defines a set of compute resources for a web app to run with.</span><span class="sxs-lookup"><span data-stu-id="e701b-226">An App Service plan defines a set of compute resources for a web app to run with.</span></span> |

    ![App Service dialog box](./media/cache-web-app-howto/cache-create-app-service-dialog.png)

4. <span data-ttu-id="e701b-228">After you configure the App Service hosting settings, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e701b-228">After you configure the App Service hosting settings, select **Create**.</span></span>

5. <span data-ttu-id="e701b-229">Monitor the **Output** window in Visual Studio to see the publishing status.</span><span class="sxs-lookup"><span data-stu-id="e701b-229">Monitor the **Output** window in Visual Studio to see the publishing status.</span></span> <span data-ttu-id="e701b-230">After the app has been published, the URL for the app is logged:</span><span class="sxs-lookup"><span data-stu-id="e701b-230">After the app has been published, the URL for the app is logged:</span></span>

    ![Publishing output](./media/cache-web-app-howto/cache-publishing-output.png)

### <a name="add-the-app-setting-for-the-cache"></a><span data-ttu-id="e701b-232">Add the app setting for the cache</span><span class="sxs-lookup"><span data-stu-id="e701b-232">Add the app setting for the cache</span></span>

<span data-ttu-id="e701b-233">After the new app has been published, add a new app setting.</span><span class="sxs-lookup"><span data-stu-id="e701b-233">After the new app has been published, add a new app setting.</span></span> <span data-ttu-id="e701b-234">This setting is used to store the cache connection information.</span><span class="sxs-lookup"><span data-stu-id="e701b-234">This setting is used to store the cache connection information.</span></span> 

#### <a name="to-add-the-app-setting"></a><span data-ttu-id="e701b-235">To add the app setting</span><span class="sxs-lookup"><span data-stu-id="e701b-235">To add the app setting</span></span> 

1. <span data-ttu-id="e701b-236">Type the app name in the search bar at the top of the Azure portal to find the new app you created.</span><span class="sxs-lookup"><span data-stu-id="e701b-236">Type the app name in the search bar at the top of the Azure portal to find the new app you created.</span></span>

    ![Find app](./media/cache-web-app-howto/cache-find-app-service.png)

2. <span data-ttu-id="e701b-238">Add a new app setting named **CacheConnection** for the app to use to connect to the cache.</span><span class="sxs-lookup"><span data-stu-id="e701b-238">Add a new app setting named **CacheConnection** for the app to use to connect to the cache.</span></span> <span data-ttu-id="e701b-239">Use the same value you configured for `CacheConnection` in your *CacheSecrets.config* file.</span><span class="sxs-lookup"><span data-stu-id="e701b-239">Use the same value you configured for `CacheConnection` in your *CacheSecrets.config* file.</span></span> <span data-ttu-id="e701b-240">The value contains the cache host name and access key.</span><span class="sxs-lookup"><span data-stu-id="e701b-240">The value contains the cache host name and access key.</span></span>

    ![Add app setting](./media/cache-web-app-howto/cache-add-app-setting.png)

### <a name="run-the-app-in-azure"></a><span data-ttu-id="e701b-242">Run the app in Azure</span><span class="sxs-lookup"><span data-stu-id="e701b-242">Run the app in Azure</span></span>

<span data-ttu-id="e701b-243">In your browser, go to the URL for the app.</span><span class="sxs-lookup"><span data-stu-id="e701b-243">In your browser, go to the URL for the app.</span></span> <span data-ttu-id="e701b-244">The URL appears in the results of the publishing operation in the Visual Studio output window.</span><span class="sxs-lookup"><span data-stu-id="e701b-244">The URL appears in the results of the publishing operation in the Visual Studio output window.</span></span> <span data-ttu-id="e701b-245">It's also provided in the Azure portal on the overview page of the app you created.</span><span class="sxs-lookup"><span data-stu-id="e701b-245">It's also provided in the Azure portal on the overview page of the app you created.</span></span>

<span data-ttu-id="e701b-246">Select **Azure Redis Cache Test** on the navigation bar to test cache access.</span><span class="sxs-lookup"><span data-stu-id="e701b-246">Select **Azure Redis Cache Test** on the navigation bar to test cache access.</span></span>

![Simple test completed Azure](./media/cache-web-app-howto/cache-simple-test-complete-azure.png)

## <a name="clean-up-resources"></a><span data-ttu-id="e701b-248">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e701b-248">Clean up resources</span></span>

<span data-ttu-id="e701b-249">If you're continuing to the next tutorial, you can keep the resources that you created in this quickstart and reuse them.</span><span class="sxs-lookup"><span data-stu-id="e701b-249">If you're continuing to the next tutorial, you can keep the resources that you created in this quickstart and reuse them.</span></span>

<span data-ttu-id="e701b-250">Otherwise, if you're finished with the quickstart sample application, you can delete the Azure resources that you created in this quickstart to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="e701b-250">Otherwise, if you're finished with the quickstart sample application, you can delete the Azure resources that you created in this quickstart to avoid charges.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e701b-251">Deleting a resource group is irreversible.</span><span class="sxs-lookup"><span data-stu-id="e701b-251">Deleting a resource group is irreversible.</span></span> <span data-ttu-id="e701b-252">When you delete a resource group, all the resources in it are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="e701b-252">When you delete a resource group, all the resources in it are permanently deleted.</span></span> <span data-ttu-id="e701b-253">Make sure that you do not accidentally delete the wrong resource group or resources.</span><span class="sxs-lookup"><span data-stu-id="e701b-253">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="e701b-254">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="e701b-254">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span></span>

### <a name="to-delete-a-resource-group"></a><span data-ttu-id="e701b-255">To delete a resource group</span><span class="sxs-lookup"><span data-stu-id="e701b-255">To delete a resource group</span></span>

1. <span data-ttu-id="e701b-256">Sign in to the [Azure portal](https://portal.azure.com), and then select **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="e701b-256">Sign in to the [Azure portal](https://portal.azure.com), and then select **Resource groups**.</span></span>

2. <span data-ttu-id="e701b-257">In the **Filter by name...** box, type the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="e701b-257">In the **Filter by name...** box, type the name of your resource group.</span></span> <span data-ttu-id="e701b-258">The instructions for this article used a resource group named *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="e701b-258">The instructions for this article used a resource group named *TestResources*.</span></span> <span data-ttu-id="e701b-259">On your resource group, in the results list, select **...**, and then select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="e701b-259">On your resource group, in the results list, select **...**, and then select **Delete resource group**.</span></span>

    ![Delete](./media/cache-web-app-howto/cache-delete-resource-group.png)

<span data-ttu-id="e701b-261">You're asked to confirm the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="e701b-261">You're asked to confirm the deletion of the resource group.</span></span> <span data-ttu-id="e701b-262">Type the name of your resource group to confirm, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e701b-262">Type the name of your resource group to confirm, and then select **Delete**.</span></span>

<span data-ttu-id="e701b-263">After a few moments, the resource group and all of its resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="e701b-263">After a few moments, the resource group and all of its resources are deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e701b-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="e701b-264">Next steps</span></span>

<span data-ttu-id="e701b-265">In the next tutorial, you use Azure Redis Cache in a more realistic scenario to improve performance of an app.</span><span class="sxs-lookup"><span data-stu-id="e701b-265">In the next tutorial, you use Azure Redis Cache in a more realistic scenario to improve performance of an app.</span></span> <span data-ttu-id="e701b-266">You update this application to cache leaderboard results using the cache-aside pattern with ASP.NET and a database.</span><span class="sxs-lookup"><span data-stu-id="e701b-266">You update this application to cache leaderboard results using the cache-aside pattern with ASP.NET and a database.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e701b-267">Create a cache-aside leaderboard on ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e701b-267">Create a cache-aside leaderboard on ASP.NET</span></span>](cache-web-app-cache-aside-leaderboard.md)
