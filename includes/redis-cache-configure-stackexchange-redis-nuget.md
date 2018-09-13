<span data-ttu-id="e919a-101">.NET applications can use the **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies the configuration of cache client applications.</span><span class="sxs-lookup"><span data-stu-id="e919a-101">.NET applications can use the **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies the configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="e919a-102">For more information, see the [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  the [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="e919a-102">For more information, see the [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  the [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="e919a-103">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, right-click the project in **Solution Explorer** and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="e919a-103">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, right-click the project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet packages](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="e919a-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into the search text box, select the desired version from the results, and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="e919a-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into the search text box, select the desired version from the results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="e919a-106">If you prefer to use a strong-named version of the **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="e919a-106">If you prefer to use a strong-named version of the **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet package](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="e919a-108">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span><span class="sxs-lookup"><span data-stu-id="e919a-108">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="e919a-109">If you have previously configured your project to use StackExchange.Redis, you can check for updates to the package from the **NuGet Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="e919a-109">If you have previously configured your project to use StackExchange.Redis, you can check for updates to the package from the **NuGet Package Manager**.</span></span> <span data-ttu-id="e919a-110">To check for and install updated versions of the StackExchange.Redis NuGet package, click **Updates** in the the **NuGet Package Manager** window.</span><span class="sxs-lookup"><span data-stu-id="e919a-110">To check for and install updated versions of the StackExchange.Redis NuGet package, click **Updates** in the the **NuGet Package Manager** window.</span></span> <span data-ttu-id="e919a-111">If an update to the StackExchange.Redis NuGet package is available, you can update your project to use the updated version.</span><span class="sxs-lookup"><span data-stu-id="e919a-111">If an update to the StackExchange.Redis NuGet package is available, you can update your project to use the updated version.</span></span>
> 
> 

<span data-ttu-id="e919a-112">You can also install the StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu, and running the following command from the **Package Manager Console** window.</span><span class="sxs-lookup"><span data-stu-id="e919a-112">You can also install the StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu, and running the following command from the **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```


