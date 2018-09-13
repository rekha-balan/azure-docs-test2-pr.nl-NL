
<span data-ttu-id="12e11-101">This section shows you how to install a SQL Server Express, enable TCP/IP, set a static port, and create a database that can be used with Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="12e11-101">This section shows you how to install a SQL Server Express, enable TCP/IP, set a static port, and create a database that can be used with Hybrid Connections.</span></span>  

### <a name="install-sql-server-express"></a><span data-ttu-id="12e11-102">Install SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="12e11-102">Install SQL Server Express</span></span>
<span data-ttu-id="12e11-103">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span><span class="sxs-lookup"><span data-stu-id="12e11-103">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="12e11-104">Default instances on SQL Server use static port 1433, whereas named instances do not.</span><span class="sxs-lookup"><span data-stu-id="12e11-104">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span> <span data-ttu-id="12e11-105">Because of this, we will install the default instance.</span><span class="sxs-lookup"><span data-stu-id="12e11-105">Because of this, we will install the default instance.</span></span> <span data-ttu-id="12e11-106">If you already have the default instance of SQL Server Express installed, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="12e11-106">If you already have the default instance of SQL Server Express installed, you can skip this section.</span></span>

1. <span data-ttu-id="12e11-107">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="12e11-107">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="12e11-108">The SQL Server Installation Center wizard appears.</span><span class="sxs-lookup"><span data-stu-id="12e11-108">The SQL Server Installation Center wizard appears.</span></span>
2. <span data-ttu-id="12e11-109">Choose **New SQL Server stand-alone installation or add features to an existing installation**, follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span><span class="sxs-lookup"><span data-stu-id="12e11-109">Choose **New SQL Server stand-alone installation or add features to an existing installation**, follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="12e11-110">On the **Instance Configuration** page, choose **Default instance**, then accept the default settings on the **Server Configuration** page.</span><span class="sxs-lookup"><span data-stu-id="12e11-110">On the **Instance Configuration** page, choose **Default instance**, then accept the default settings on the **Server Configuration** page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="12e11-111">If you already have a default instance of SQL Server installed, you can skip to the next section and use this instance with Hybrid Connections.</span><span class="sxs-lookup"><span data-stu-id="12e11-111">If you already have a default instance of SQL Server installed, you can skip to the next section and use this instance with Hybrid Connections.</span></span> 
   > 
   > 
4. <span data-ttu-id="12e11-112">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a secure password for the built-in **sa** administrator account.</span><span class="sxs-lookup"><span data-stu-id="12e11-112">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a secure password for the built-in **sa** administrator account.</span></span>
   
    <span data-ttu-id="12e11-113">In this tutorial, you will be using SQL Server authentication.</span><span class="sxs-lookup"><span data-stu-id="12e11-113">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="12e11-114">Be sure to remember the password that you provide, because you will need it later.</span><span class="sxs-lookup"><span data-stu-id="12e11-114">Be sure to remember the password that you provide, because you will need it later.</span></span>
5. <span data-ttu-id="12e11-115">Finish the wizard to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="12e11-115">Finish the wizard to complete the installation.</span></span>

### <a name="enable-tcpip-and-setting-a-static-port"></a><span data-ttu-id="12e11-116">Enable TCP/IP and setting a static port</span><span class="sxs-lookup"><span data-stu-id="12e11-116">Enable TCP/IP and setting a static port</span></span>
<span data-ttu-id="12e11-117">This section uses SQL Server Configuration Manager, which was installed when you installed SQL Server Express, to enable TCP/IP and set a static IP address.</span><span class="sxs-lookup"><span data-stu-id="12e11-117">This section uses SQL Server Configuration Manager, which was installed when you installed SQL Server Express, to enable TCP/IP and set a static IP address.</span></span> 

1. <span data-ttu-id="12e11-118">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) to enable TCP/IP access to the instance.</span><span class="sxs-lookup"><span data-stu-id="12e11-118">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) to enable TCP/IP access to the instance.</span></span>
2. <span data-ttu-id="12e11-119">(Optional) If you are not able to use the default instance, you must follow the steps in [Configure a Server to Listen on a Specific TCP Port ](https://msdn.microsoft.com/library/ms177440.aspx) to set a static port for the instance.</span><span class="sxs-lookup"><span data-stu-id="12e11-119">(Optional) If you are not able to use the default instance, you must follow the steps in [Configure a Server to Listen on a Specific TCP Port ](https://msdn.microsoft.com/library/ms177440.aspx) to set a static port for the instance.</span></span> <span data-ttu-id="12e11-120">If you complete this step, you will connect using the new port that you define, instead of port 1433.</span><span class="sxs-lookup"><span data-stu-id="12e11-120">If you complete this step, you will connect using the new port that you define, instead of port 1433.</span></span>
3. <span data-ttu-id="12e11-121">(Optional) If needed, add exceptions in the firewall to allow remote access to the SQL Server process (sqlservr.exe).</span><span class="sxs-lookup"><span data-stu-id="12e11-121">(Optional) If needed, add exceptions in the firewall to allow remote access to the SQL Server process (sqlservr.exe).</span></span>

### <a name="create-a-new-database-in-the-on-premises-sql-server-instance"></a><span data-ttu-id="12e11-122">Create a new database in the on-premises SQL Server instance</span><span class="sxs-lookup"><span data-stu-id="12e11-122">Create a new database in the on-premises SQL Server instance</span></span>
1. <span data-ttu-id="12e11-123">In SQL Server Management Studio, connect to the SQL Server you just installed.</span><span class="sxs-lookup"><span data-stu-id="12e11-123">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="12e11-124">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.)</span><span class="sxs-lookup"><span data-stu-id="12e11-124">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.)</span></span>     
   
    ![Connect to Server](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/hybrid-connections-create-on-premises-database/A04SSMSConnectToServer.png)
   
    <span data-ttu-id="12e11-126">For **Server type**, choose **Database Engine**.</span><span class="sxs-lookup"><span data-stu-id="12e11-126">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="12e11-127">For **Server name**, you can use **localhost** or the name of the computer where you installed SQL Server.</span><span class="sxs-lookup"><span data-stu-id="12e11-127">For **Server name**, you can use **localhost** or the name of the computer where you installed SQL Server.</span></span> <span data-ttu-id="12e11-128">Choose **SQL Server authentication**, and supply the password for the sa login that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="12e11-128">Choose **SQL Server authentication**, and supply the password for the sa login that you created earlier.</span></span> 
2. <span data-ttu-id="12e11-129">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span><span class="sxs-lookup"><span data-stu-id="12e11-129">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
3. <span data-ttu-id="12e11-130">In the **New Database** dialog, type `OnPremisesDB`, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="12e11-130">In the **New Database** dialog, type `OnPremisesDB`, and then click **OK**.</span></span> 
4. <span data-ttu-id="12e11-131">In Object Explorer, if you expand **Databases**, you will see that the new database is created.</span><span class="sxs-lookup"><span data-stu-id="12e11-131">In Object Explorer, if you expand **Databases**, you will see that the new database is created.</span></span>

### <a name="create-a-new-sql-server-login-and-set-permissions"></a><span data-ttu-id="12e11-132">Create a new SQL Server login and set permissions</span><span class="sxs-lookup"><span data-stu-id="12e11-132">Create a new SQL Server login and set permissions</span></span>
<span data-ttu-id="12e11-133">Finally, you will create a new SQL Server login with restricted permissions.</span><span class="sxs-lookup"><span data-stu-id="12e11-133">Finally, you will create a new SQL Server login with restricted permissions.</span></span> <span data-ttu-id="12e11-134">Your Azure service will connect to the on-premise SQL Server using this login instead of the built-in sa login, which has full permissions on the server.</span><span class="sxs-lookup"><span data-stu-id="12e11-134">Your Azure service will connect to the on-premise SQL Server using this login instead of the built-in sa login, which has full permissions on the server.</span></span>

1. <span data-ttu-id="12e11-135">In SQL Server Management Studio Object Explorer, right-click the **OnPremisesDB** database and click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="12e11-135">In SQL Server Management Studio Object Explorer, right-click the **OnPremisesDB** database and click **New Query**.</span></span>
2. <span data-ttu-id="12e11-136">Paste the following TSQL query into the query window.</span><span class="sxs-lookup"><span data-stu-id="12e11-136">Paste the following TSQL query into the query window.</span></span>
   
       USE [master]
       GO
   
       /* Replace the PASSWORD in the following statement with a secure password. 
          If you save this script, make sure that you secure the file to 
          securely maintain the password. */ 
       CREATE LOGIN [HybridConnectionLogin] WITH PASSWORD=N'<**secure_password**>', 
           DEFAULT_DATABASE=[OnPremisesDB], DEFAULT_LANGUAGE=[us_english], 
           CHECK_EXPIRATION=OFF, CHECK_POLICY=ON
       GO
   
       USE [OnPremisesDB]
       GO
   
       CREATE USER [HybridConnectionLogin] FOR LOGIN [HybridConnectionLogin] 
       WITH DEFAULT_SCHEMA=[dbo]
       GO
   
       GRANT CONNECT TO [HybridConnectionLogin]
       GRANT CREATE TABLE TO [HybridConnectionLogin]
       GRANT CREATE SCHEMA TO [HybridConnectionLogin]
       GO  
3. <span data-ttu-id="12e11-137">In the above script, replace the string `<**secure_password**>` with a secure password for the new *HybridConnectionsLogin*.</span><span class="sxs-lookup"><span data-stu-id="12e11-137">In the above script, replace the string `<**secure_password**>` with a secure password for the new *HybridConnectionsLogin*.</span></span>
4. <span data-ttu-id="12e11-138">**Execute** the query to create the new login and grant the required permissions in the on-premises database.</span><span class="sxs-lookup"><span data-stu-id="12e11-138">**Execute** the query to create the new login and grant the required permissions in the on-premises database.</span></span>


