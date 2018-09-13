
<!--
includes/sql-database-create-new-database-portal.md

Latest Freshness check:  2016-04-11 , carlrab.

As of circa 2016-04-11, the following topics might include this include:
articles/sql-database/sql-database-get-started-tutorial.md

-->
## <a name="create-a-new-azure-sql-database"></a><span data-ttu-id="76a12-101">Create a new Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="76a12-101">Create a new Azure SQL database</span></span>
<span data-ttu-id="76a12-102">Use the following steps in the Azure portal to create a new Azure SQL database on a new or existing Azure SQL Database logical server.</span><span class="sxs-lookup"><span data-stu-id="76a12-102">Use the following steps in the Azure portal to create a new Azure SQL database on a new or existing Azure SQL Database logical server.</span></span>

1. <span data-ttu-id="76a12-103">If you're not currently connected, connect to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="76a12-103">If you're not currently connected, connect to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="76a12-104">Click **New**, type **SQL Database**, and then click **SQL Database (new database)**.</span><span class="sxs-lookup"><span data-stu-id="76a12-104">Click **New**, type **SQL Database**, and then click **SQL Database (new database)**.</span></span>
   
     ![New database](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-portal/sql-database-create-new-database-portal-1.png)
3. <span data-ttu-id="76a12-106">Click **SQL Database (new database)**.</span><span class="sxs-lookup"><span data-stu-id="76a12-106">Click **SQL Database (new database)**.</span></span>
   
     ![New database](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-portal/sql-database-create-new-database-portal-2.png)
4. <span data-ttu-id="76a12-108">Click **Create** to create a new database in the SQL Database service.</span><span class="sxs-lookup"><span data-stu-id="76a12-108">Click **Create** to create a new database in the SQL Database service.</span></span>
   
     ![New database](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-portal/sql-database-create-new-database-portal-3.png)
5. <span data-ttu-id="76a12-110">Provide the values for the following server properties:</span><span class="sxs-lookup"><span data-stu-id="76a12-110">Provide the values for the following server properties:</span></span>
   
   * <span data-ttu-id="76a12-111">Database name</span><span class="sxs-lookup"><span data-stu-id="76a12-111">Database name</span></span>
   * <span data-ttu-id="76a12-112">Subscription: This applies only if you have multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="76a12-112">Subscription: This applies only if you have multiple subscriptions.</span></span>
   * <span data-ttu-id="76a12-113">Resource group: If you're just getting started, use the resource group of the logical server.</span><span class="sxs-lookup"><span data-stu-id="76a12-113">Resource group: If you're just getting started, use the resource group of the logical server.</span></span>
   * <span data-ttu-id="76a12-114">Select source: You can choose a blank database, sample data, or an Azure database backup.</span><span class="sxs-lookup"><span data-stu-id="76a12-114">Select source: You can choose a blank database, sample data, or an Azure database backup.</span></span> <span data-ttu-id="76a12-115">To migrate an on-premises SQL Server database or load data by using the BCP command-line tool, see the links at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="76a12-115">To migrate an on-premises SQL Server database or load data by using the BCP command-line tool, see the links at the end of this article.</span></span>
   * <span data-ttu-id="76a12-116">Server: A new or existing logical server.</span><span class="sxs-lookup"><span data-stu-id="76a12-116">Server: A new or existing logical server.</span></span>
   * <span data-ttu-id="76a12-117">Server admin login</span><span class="sxs-lookup"><span data-stu-id="76a12-117">Server admin login</span></span>
   * <span data-ttu-id="76a12-118">Password</span><span class="sxs-lookup"><span data-stu-id="76a12-118">Password</span></span>
   * <span data-ttu-id="76a12-119">Pricing tier: If you're just getting started, use the default value S0.</span><span class="sxs-lookup"><span data-stu-id="76a12-119">Pricing tier: If you're just getting started, use the default value S0.</span></span>
   * <span data-ttu-id="76a12-120">Collation: This applies only if a blank database was chosen.</span><span class="sxs-lookup"><span data-stu-id="76a12-120">Collation: This applies only if a blank database was chosen.</span></span>
     
        ![New database](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-portal/sql-database-create-new-database-portal-4.png)
6. <span data-ttu-id="76a12-122">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="76a12-122">Click **Create**.</span></span> <span data-ttu-id="76a12-123">In the notification area, you can see that deployment has started.</span><span class="sxs-lookup"><span data-stu-id="76a12-123">In the notification area, you can see that deployment has started.</span></span>
   
    ![New database](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-portal/sql-database-create-new-database-portal-5.png)
7. <span data-ttu-id="76a12-125">Wait for deployment to finish before continuing to the next step.</span><span class="sxs-lookup"><span data-stu-id="76a12-125">Wait for deployment to finish before continuing to the next step.</span></span>
   
     ![New database](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-database-create-new-database-portal/sql-database-create-new-database-portal-6.png)







