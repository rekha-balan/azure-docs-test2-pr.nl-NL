---
title: Session state with Azure Redis cache in Azure App Service
description: Learn how to use the Azure Cache Service to support ASP.NET session state caching.
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549837"
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="700ed-103">Session state with Azure Redis cache in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="700ed-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="700ed-104">This topic explains how to use the Azure Redis Cache Service for session state.</span><span class="sxs-lookup"><span data-stu-id="700ed-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="700ed-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span><span class="sxs-lookup"><span data-stu-id="700ed-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="700ed-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span><span class="sxs-lookup"><span data-stu-id="700ed-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="700ed-107">The Redis Cache Service is the fastest and simplest to enable.</span><span class="sxs-lookup"><span data-stu-id="700ed-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a><span data-ttu-id="700ed-108">Create the Cache</span><span class="sxs-lookup"><span data-stu-id="700ed-108">Create the Cache</span></span>
<span data-ttu-id="700ed-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span><span class="sxs-lookup"><span data-stu-id="700ed-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <a id="configureproject"></a><span data-ttu-id="700ed-110">Add the RedisSessionStateProvider NuGet package to your web app</span><span class="sxs-lookup"><span data-stu-id="700ed-110">Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="700ed-111">Install the NuGet `RedisSessionStateProvider` package.</span><span class="sxs-lookup"><span data-stu-id="700ed-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="700ed-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span><span class="sxs-lookup"><span data-stu-id="700ed-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="700ed-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="700ed-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="700ed-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="700ed-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <a id="configurewebconfig"></a><span data-ttu-id="700ed-115">Modify the Web.Config File</span><span class="sxs-lookup"><span data-stu-id="700ed-115">Modify the Web.Config File</span></span>
<span data-ttu-id="700ed-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span><span class="sxs-lookup"><span data-stu-id="700ed-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="700ed-117">Open the *web.config* and find the the **sessionState** element.</span><span class="sxs-lookup"><span data-stu-id="700ed-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="700ed-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span><span class="sxs-lookup"><span data-stu-id="700ed-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="700ed-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span><span class="sxs-lookup"><span data-stu-id="700ed-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="700ed-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="700ed-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="700ed-121">Note that the non-SSL port is disabled by default for new caches.</span><span class="sxs-lookup"><span data-stu-id="700ed-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="700ed-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="700ed-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="700ed-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey\*, and *ssl*.</span><span class="sxs-lookup"><span data-stu-id="700ed-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey\*, and *ssl*.</span></span>
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <a id="usesessionobject"></a> <span data-ttu-id="700ed-124">Use the Session Object in Code</span><span class="sxs-lookup"><span data-stu-id="700ed-124">Use the Session Object in Code</span></span>
<span data-ttu-id="700ed-125">The final step is to begin using the Session object in your ASP.NET code.</span><span class="sxs-lookup"><span data-stu-id="700ed-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="700ed-126">You add objects to session state by using the **Session.Add** method.</span><span class="sxs-lookup"><span data-stu-id="700ed-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="700ed-127">This method uses key-value pairs to store items in the session state cache.</span><span class="sxs-lookup"><span data-stu-id="700ed-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="700ed-128">The following code retrieves this value from session state.</span><span class="sxs-lookup"><span data-stu-id="700ed-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="700ed-129">You can also use the Redis Cache to cache objects in your web app.</span><span class="sxs-lookup"><span data-stu-id="700ed-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="700ed-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="700ed-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="700ed-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="700ed-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="700ed-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="700ed-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="700ed-133">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="700ed-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="700ed-134">What's changed</span><span class="sxs-lookup"><span data-stu-id="700ed-134">What's changed</span></span>
* <span data-ttu-id="700ed-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="700ed-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="700ed-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="700ed-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

