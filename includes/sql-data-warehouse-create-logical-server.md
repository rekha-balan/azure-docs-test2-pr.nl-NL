### <a name="create-a-new-logical-sql-server-in-the-azure-portal"></a><span data-ttu-id="e5a92-101">Create a new logical SQL server in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e5a92-101">Create a new logical SQL server in the Azure portal</span></span>

1. <span data-ttu-id="e5a92-102">Click **New**, search **logical server**, and then hit **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e5a92-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![search logical server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="e5a92-104">Select **SQL server (logical server)**</span><span class="sxs-lookup"><span data-stu-id="e5a92-104">Select **SQL server (logical server)**</span></span> 

    ![select logical server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="e5a92-106">Click **Create** to open the new SQL Server (logical server) blade.</span><span class="sxs-lookup"><span data-stu-id="e5a92-106">Click **Create** to open the new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="e5a92-107"><kbd> ![open logical server blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span><span class="sxs-lookup"><span data-stu-id="e5a92-107"><kbd> ![open logical server blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="e5a92-108">In the SQL Server (logical server) blade's server name text box, provide a valid name for the new logical server.</span><span class="sxs-lookup"><span data-stu-id="e5a92-108">In the SQL Server (logical server) blade's server name text box, provide a valid name for the new logical server.</span></span> <span data-ttu-id="e5a92-109">A green check mark indicates that you have provided a valid name.</span><span class="sxs-lookup"><span data-stu-id="e5a92-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![new server name](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="e5a92-111">The fully qualified name for your new server will be <your_server_name>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="e5a92-111">The fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="e5a92-112">In the Server admin login text box, provide a user name for the SQL authentication login for this server.</span><span class="sxs-lookup"><span data-stu-id="e5a92-112">In the Server admin login text box, provide a user name for the SQL authentication login for this server.</span></span> <span data-ttu-id="e5a92-113">This login is known as the server principal login.</span><span class="sxs-lookup"><span data-stu-id="e5a92-113">This login is known as the server principal login.</span></span> <span data-ttu-id="e5a92-114">A green check mark indicates that you have provided a valid name.</span><span class="sxs-lookup"><span data-stu-id="e5a92-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![SQL admin login](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="e5a92-116">In the **Password** and **Confirm password** text boxes, provide a password for the server principal login account.</span><span class="sxs-lookup"><span data-stu-id="e5a92-116">In the **Password** and **Confirm password** text boxes, provide a password for the server principal login account.</span></span> <span data-ttu-id="e5a92-117">A green check mark indicates that you have provided a valid password.</span><span class="sxs-lookup"><span data-stu-id="e5a92-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![SQL admin password](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="e5a92-119">Select a subscription in which you have permission to create objects.</span><span class="sxs-lookup"><span data-stu-id="e5a92-119">Select a subscription in which you have permission to create objects.</span></span>

    ![subscription](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="e5a92-121">In the Resource group text box, select **Create new** and then, in the resource group text box, provide a valid name for the new resource group (you can also use an existing resource group if you have already created one for yourself).</span><span class="sxs-lookup"><span data-stu-id="e5a92-121">In the Resource group text box, select **Create new** and then, in the resource group text box, provide a valid name for the new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="e5a92-122">A green check mark indicates that you have provided a valid name.</span><span class="sxs-lookup"><span data-stu-id="e5a92-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![new resource group](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="e5a92-124">In the **Location** text box, select a data center appropriate to your location - such as "Australia East".</span><span class="sxs-lookup"><span data-stu-id="e5a92-124">In the **Location** text box, select a data center appropriate to your location - such as "Australia East".</span></span>
    
    ![server location](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="e5a92-126">The checkbox for **Allow azure services to access server** cannot be changed on this blade.</span><span class="sxs-lookup"><span data-stu-id="e5a92-126">The checkbox for **Allow azure services to access server** cannot be changed on this blade.</span></span> <span data-ttu-id="e5a92-127">You can change this setting on the server firewall blade.</span><span class="sxs-lookup"><span data-stu-id="e5a92-127">You can change this setting on the server firewall blade.</span></span> <span data-ttu-id="e5a92-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5a92-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="e5a92-129">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e5a92-129">Click **Create**.</span></span>

    ![create button](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/sql-data-warehouse-create-logical-server/create.png)












