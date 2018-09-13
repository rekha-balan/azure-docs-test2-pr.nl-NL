<span data-ttu-id="90637-101">This guide will show you how to use [ClearDB] to create a MySQL database from the Azure Store and  how to create a MySQL database as a linked resource when you create a [Azure Web Site][waws] .</span><span class="sxs-lookup"><span data-stu-id="90637-101">This guide will show you how to use [ClearDB] to create a MySQL database from the Azure Store and  how to create a MySQL database as a linked resource when you create a [Azure Web Site][waws] .</span></span> <span data-ttu-id="90637-102">[ClearDB] is a fault-tolerant database-as-a-service provider that allows you to run and manage MySQL databases in Azure datacenters and connect to them from any application.</span><span class="sxs-lookup"><span data-stu-id="90637-102">[ClearDB] is a fault-tolerant database-as-a-service provider that allows you to run and manage MySQL databases in Azure datacenters and connect to them from any application.</span></span>  

> [!NOTE]
> <span data-ttu-id="90637-103">When you create a MySQL database as part of the Website creation process, you can only create a free database.</span><span class="sxs-lookup"><span data-stu-id="90637-103">When you create a MySQL database as part of the Website creation process, you can only create a free database.</span></span> <span data-ttu-id="90637-104">Creating a MySQL database from the Azure Store allows you to create a free database or choose from paid options.</span><span class="sxs-lookup"><span data-stu-id="90637-104">Creating a MySQL database from the Azure Store allows you to create a free database or choose from paid options.</span></span>
> 
> 

## <a name="how-to-create-a-mysql-database-from-the-azure-store"></a><span data-ttu-id="90637-105">How to: Create a MySQL database from the Azure Store</span><span class="sxs-lookup"><span data-stu-id="90637-105">How to: Create a MySQL database from the Azure Store</span></span>
<span data-ttu-id="90637-106">To create a MySQL database from the Azure Store, do the following:</span><span class="sxs-lookup"><span data-stu-id="90637-106">To create a MySQL database from the Azure Store, do the following:</span></span>

1. <span data-ttu-id="90637-107">Log in to the [Azure Management Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="90637-107">Log in to the [Azure Management Portal][portal].</span></span>
2. <span data-ttu-id="90637-108">Click **+NEW** at the bottom of the page, then select **MARKETPLACE**.</span><span class="sxs-lookup"><span data-stu-id="90637-108">Click **+NEW** at the bottom of the page, then select **MARKETPLACE**.</span></span>
   
    ![Select add-on from store](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/select-store.png)
3. <span data-ttu-id="90637-110">Select **ClearDB MySQL Database**, then click the arrow at the bottom of the frame.</span><span class="sxs-lookup"><span data-stu-id="90637-110">Select **ClearDB MySQL Database**, then click the arrow at the bottom of the frame.</span></span>
   
    ![Select ClearDB MySQL Database](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/select-cleardb-mysql.png)
4. <span data-ttu-id="90637-112">Select a plan, enter a database name, and select a region, then click the arrow at the bottom of the frame.</span><span class="sxs-lookup"><span data-stu-id="90637-112">Select a plan, enter a database name, and select a region, then click the arrow at the bottom of the frame.</span></span>
   
    ![Purchase MySQL database from store](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/purchase-mysql.png)
5. <span data-ttu-id="90637-114">Click the checkmark to complete your purchase.</span><span class="sxs-lookup"><span data-stu-id="90637-114">Click the checkmark to complete your purchase.</span></span>
   
    ![Review and complete your purchase](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/complete-mysql-purchase.png)
6. <span data-ttu-id="90637-116">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span><span class="sxs-lookup"><span data-stu-id="90637-116">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span>
   
    ![Manage MySQL database in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/manage-mysql-add-on.png)
7. <span data-ttu-id="90637-118">You can get the database connection information by clicking on **CONNECTION INFO** at the bottom of the page (shown above).</span><span class="sxs-lookup"><span data-stu-id="90637-118">You can get the database connection information by clicking on **CONNECTION INFO** at the bottom of the page (shown above).</span></span>
   
    ![MySql connection information](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/mysql-conn-info.png) 

## <a name="how-to-create-a-mysql-database-as-a-linked-resource-for-azure-website"></a><span data-ttu-id="90637-120">How to: Create a MySQL database as a linked resource for Azure Website</span><span class="sxs-lookup"><span data-stu-id="90637-120">How to: Create a MySQL database as a linked resource for Azure Website</span></span>
<span data-ttu-id="90637-121">To create a MySQL database as a linked resource when you create a [Azure Web Site][waws], do the following:</span><span class="sxs-lookup"><span data-stu-id="90637-121">To create a MySQL database as a linked resource when you create a [Azure Web Site][waws], do the following:</span></span>

1. <span data-ttu-id="90637-122">Log in to the [Azure Management Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="90637-122">Log in to the [Azure Management Portal][portal].</span></span>
2. <span data-ttu-id="90637-123">Click **+NEW** at the bottom of the page, then select **COMPUTE**, **WEBSITE**, and **CREATE WITH DATABASE**.</span><span class="sxs-lookup"><span data-stu-id="90637-123">Click **+NEW** at the bottom of the page, then select **COMPUTE**, **WEBSITE**, and **CREATE WITH DATABASE**.</span></span>
   
    ![Create website with database](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/custom_create.png)
3. <span data-ttu-id="90637-125">Provide a **URL** for your website, select the **REGION** for your site, and choose **Create a new MySQL database** from the **DATABASE** dropdown.</span><span class="sxs-lookup"><span data-stu-id="90637-125">Provide a **URL** for your website, select the **REGION** for your site, and choose **Create a new MySQL database** from the **DATABASE** dropdown.</span></span> <span data-ttu-id="90637-126">Optionally, you can replace the default name for the connection string.</span><span class="sxs-lookup"><span data-stu-id="90637-126">Optionally, you can replace the default name for the connection string.</span></span> <span data-ttu-id="90637-127">Click the arrow at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="90637-127">Click the arrow at the bottom of the page.</span></span>
   
    ![Provide website details](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/provide-website-details.png) 
4. <span data-ttu-id="90637-129">Provide a database **NAME**, select the **REGION** for your database (this should be same as the region for your website), agree to ClearDB's legal terms, and click the checkmark at the bottom of the frame.</span><span class="sxs-lookup"><span data-stu-id="90637-129">Provide a database **NAME**, select the **REGION** for your database (this should be same as the region for your website), agree to ClearDB's legal terms, and click the checkmark at the bottom of the frame.</span></span>
   
    ![Provide MySQL details](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/provide-mysql-details.png)
5. <span data-ttu-id="90637-131">After your website has been created, click on the name of your site to go to your site's dashboard.</span><span class="sxs-lookup"><span data-stu-id="90637-131">After your website has been created, click on the name of your site to go to your site's dashboard.</span></span>
   
    ![Go to web site dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/go-to-website-dashboard.png)
6. <span data-ttu-id="90637-133">Click on **CONFIGURE**.</span><span class="sxs-lookup"><span data-stu-id="90637-133">Click on **CONFIGURE**.</span></span>
   
    ![Go to configure tab](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/go-to-configure-tab.png)
7. <span data-ttu-id="90637-135">Scroll down to the **connection strings** section and click **Show Connection Strings**.</span><span class="sxs-lookup"><span data-stu-id="90637-135">Scroll down to the **connection strings** section and click **Show Connection Strings**.</span></span> 
   
    ![Show connection string](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/show-conn-string.png)
8. <span data-ttu-id="90637-137">Copy the connection string for use in your application.</span><span class="sxs-lookup"><span data-stu-id="90637-137">Copy the connection string for use in your application.</span></span>
   
    ![Shown connection string](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/create-mysql-db/shown-conn-string.png)

> [!NOTE]
> <span data-ttu-id="90637-139">Connection strings are accessible to your website application by connection string name.</span><span class="sxs-lookup"><span data-stu-id="90637-139">Connection strings are accessible to your website application by connection string name.</span></span> <span data-ttu-id="90637-140">In .NET applications, connection strings are availble in the **connectionStrings** object.</span><span class="sxs-lookup"><span data-stu-id="90637-140">In .NET applications, connection strings are availble in the **connectionStrings** object.</span></span> <span data-ttu-id="90637-141">In other programming languages, connection strings are accessible as environment variables.</span><span class="sxs-lookup"><span data-stu-id="90637-141">In other programming languages, connection strings are accessible as environment variables.</span></span> <span data-ttu-id="90637-142">For more information, see [How to Configure Web Sites][configure].</span><span class="sxs-lookup"><span data-stu-id="90637-142">For more information, see [How to Configure Web Sites][configure].</span></span>
> 
> 

[ClearDB]: http://www.cleardb.com/
[waws]: /documentation/services/web-sites/
[portal]: http://manage.windowsazure.com
[configure]: ../articles/app-service-web/web-sites-configure.md













