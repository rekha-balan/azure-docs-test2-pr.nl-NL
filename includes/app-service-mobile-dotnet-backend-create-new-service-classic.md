1. <span data-ttu-id="ca816-101">Log in at the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="ca816-101">Log in at the [Azure Portal].</span></span>
2. <span data-ttu-id="ca816-102">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="ca816-102">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="ca816-103">For the **Resource Group**, select an existing resource group, or create a new one (using the same name as your app.)</span><span class="sxs-lookup"><span data-stu-id="ca816-103">For the **Resource Group**, select an existing resource group, or create a new one (using the same name as your app.)</span></span> 
   
    <span data-ttu-id="ca816-104">You can either select another App Service plan or create a new one.</span><span class="sxs-lookup"><span data-stu-id="ca816-104">You can either select another App Service plan or create a new one.</span></span> <span data-ttu-id="ca816-105">For more about App Services plans and how to create a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca816-105">For more about App Services plans and how to create a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
4. <span data-ttu-id="ca816-106">For the **App Service plan**, the default plan (in the [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span><span class="sxs-lookup"><span data-stu-id="ca816-106">For the **App Service plan**, the default plan (in the [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span></span> <span data-ttu-id="ca816-107">You can also  select a different plan, or [create a new one](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="ca816-107">You can also  select a different plan, or [create a new one](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span></span> <span data-ttu-id="ca816-108">The App Service plan's settings determine the [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span><span class="sxs-lookup"><span data-stu-id="ca816-108">The App Service plan's settings determine the [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span></span> 
   
    <span data-ttu-id="ca816-109">After you decide on the plan, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ca816-109">After you decide on the plan, click **Create**.</span></span> <span data-ttu-id="ca816-110">This creates the Mobile App backend.</span><span class="sxs-lookup"><span data-stu-id="ca816-110">This creates the Mobile App backend.</span></span> 
5. <span data-ttu-id="ca816-111">In the **Settings** blade for the new Mobile App backend, click **Quick start** > your client app platform > **Connect a database**.</span><span class="sxs-lookup"><span data-stu-id="ca816-111">In the **Settings** blade for the new Mobile App backend, click **Quick start** > your client app platform > **Connect a database**.</span></span> 
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. <span data-ttu-id="ca816-112">In the **Add data connection** blade, click **SQL Database** > **Create a new database**, type the database **Name**, choose a pricing tier, then click **Server**.</span><span class="sxs-lookup"><span data-stu-id="ca816-112">In the **Add data connection** blade, click **SQL Database** > **Create a new database**, type the database **Name**, choose a pricing tier, then click **Server**.</span></span>  <span data-ttu-id="ca816-113">You can reuse this new database.</span><span class="sxs-lookup"><span data-stu-id="ca816-113">You can reuse this new database.</span></span> <span data-ttu-id="ca816-114">If you already have a database in the same location, you can instead choose **Use an existing database**.</span><span class="sxs-lookup"><span data-stu-id="ca816-114">If you already have a database in the same location, you can instead choose **Use an existing database**.</span></span> <span data-ttu-id="ca816-115">The use of a database in a different location isn't recommended due to bandwidth costs and higher latency.</span><span class="sxs-lookup"><span data-stu-id="ca816-115">The use of a database in a different location isn't recommended due to bandwidth costs and higher latency.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. <span data-ttu-id="ca816-116">In the **New server** blade, type a unique server name in the **Server name** field, provide a login and password, check **Allow azure services to access server**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca816-116">In the **New server** blade, type a unique server name in the **Server name** field, provide a login and password, check **Allow azure services to access server**, and click **OK**.</span></span> <span data-ttu-id="ca816-117">This creates the new database.</span><span class="sxs-lookup"><span data-stu-id="ca816-117">This creates the new database.</span></span>
8. <span data-ttu-id="ca816-118">Back in the **Add data connection** blade, click **Connection string**, type the login and password values for your database, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca816-118">Back in the **Add data connection** blade, click **Connection string**, type the login and password values for your database, and click **OK**.</span></span> <span data-ttu-id="ca816-119">Wait a few minutes for the database to be deployed successfully before proceeding.</span><span class="sxs-lookup"><span data-stu-id="ca816-119">Wait a few minutes for the database to be deployed successfully before proceeding.</span></span>

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

