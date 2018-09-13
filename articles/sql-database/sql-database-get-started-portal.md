---
title: 'Azure portal: Create a SQL database | Microsoft Docs'
description: Learn how to create a SQL Database logical server, server-level firewall rule, and databases in the Azure portal. You also learn to query an Azure SQL database using the Azure portal.
keywords: sql database tutorial, create a sql database
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: quick start create
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: a9eb7ef09309f0a40d54448f17b3f333a9c3379e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562859"
---
# <a name="create-an-azure-sql-database-in-the-azure-portal"></a><span data-ttu-id="ab69a-105">Create an Azure SQL database in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ab69a-105">Create an Azure SQL database in the Azure portal</span></span>

<span data-ttu-id="ab69a-106">This quick start tutorial walks through how to create a SQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="ab69a-106">This quick start tutorial walks through how to create a SQL database in Azure.</span></span> <span data-ttu-id="ab69a-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you to run and scale highly available SQL Server databases in the cloud.</span><span class="sxs-lookup"><span data-stu-id="ab69a-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you to run and scale highly available SQL Server databases in the cloud.</span></span> <span data-ttu-id="ab69a-108">This quick start shows you how to get started by creating a SQL database using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ab69a-108">This quick start shows you how to get started by creating a SQL database using the Azure portal.</span></span>

<span data-ttu-id="ab69a-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="ab69a-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="ab69a-110">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ab69a-110">Log in to the Azure portal</span></span>

<span data-ttu-id="ab69a-111">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ab69a-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="ab69a-112">Create a SQL database</span><span class="sxs-lookup"><span data-stu-id="ab69a-112">Create a SQL database</span></span>

<span data-ttu-id="ab69a-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="ab69a-114">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-114">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="ab69a-115">Follow these steps to create a SQL database containing the Adventure Works LT sample data.</span><span class="sxs-lookup"><span data-stu-id="ab69a-115">Follow these steps to create a SQL database containing the Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="ab69a-116">Click the **New** button found on the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ab69a-116">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="ab69a-117">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span><span class="sxs-lookup"><span data-stu-id="ab69a-117">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span>

    ![create database-1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="ab69a-119">Fill out the SQL Database form with the following information, as shown on the preceding image:</span><span class="sxs-lookup"><span data-stu-id="ab69a-119">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>     
   - <span data-ttu-id="ab69a-120">Database name: **mySampleDatabase**</span><span class="sxs-lookup"><span data-stu-id="ab69a-120">Database name: **mySampleDatabase**</span></span>
   - <span data-ttu-id="ab69a-121">Resource group: **myResourceGroup**</span><span class="sxs-lookup"><span data-stu-id="ab69a-121">Resource group: **myResourceGroup**</span></span>
   - <span data-ttu-id="ab69a-122">Source source: **Sample (AdventureWorksLT)**</span><span class="sxs-lookup"><span data-stu-id="ab69a-122">Source source: **Sample (AdventureWorksLT)**</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ab69a-123">You must select the sample database on this form because it is used in the remainder of this quick start.</span><span class="sxs-lookup"><span data-stu-id="ab69a-123">You must select the sample database on this form because it is used in the remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="ab69a-124">Click **Server** and then fill out the **New server form** specifying a globally unique server name, provide a name for the server admin login, and then specify the password of your choice.</span><span class="sxs-lookup"><span data-stu-id="ab69a-124">Click **Server** and then fill out the **New server form** specifying a globally unique server name, provide a name for the server admin login, and then specify the password of your choice.</span></span> 

   > [!IMPORTANT]
   > <span data-ttu-id="ab69a-125">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span><span class="sxs-lookup"><span data-stu-id="ab69a-125">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="ab69a-126">Remember or record this information for later use.</span><span class="sxs-lookup"><span data-stu-id="ab69a-126">Remember or record this information for later use.</span></span> 
   >  

    ![create database-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/create-database-server.png)
5. <span data-ttu-id="ab69a-128">When you have completed the form, click **Select**.</span><span class="sxs-lookup"><span data-stu-id="ab69a-128">When you have completed the form, click **Select**.</span></span>

6. <span data-ttu-id="ab69a-129">Click **Pricing tier** to specify the service tier and performance level for your new database.</span><span class="sxs-lookup"><span data-stu-id="ab69a-129">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="ab69a-130">Use the slider to select **20 DTUs** and **250** GB of storage.</span><span class="sxs-lookup"><span data-stu-id="ab69a-130">Use the slider to select **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="ab69a-131">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-131">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

    ![create database-s1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="ab69a-133">After selected the amount of DTUs, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="ab69a-133">After selected the amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="ab69a-134">Now that you have completed the SQL Database form, click **Create** to provision the database.</span><span class="sxs-lookup"><span data-stu-id="ab69a-134">Now that you have completed the SQL Database form, click **Create** to provision the database.</span></span> <span data-ttu-id="ab69a-135">Provisioning takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="ab69a-135">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="ab69a-136">On the toolbar, click **Notifications** to monitor the deployment process.</span><span class="sxs-lookup"><span data-stu-id="ab69a-136">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

    ![notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/notification.png)


## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="ab69a-138">Create a server-level firewall rule</span><span class="sxs-lookup"><span data-stu-id="ab69a-138">Create a server-level firewall rule</span></span>

<span data-ttu-id="ab69a-139">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span><span class="sxs-lookup"><span data-stu-id="ab69a-139">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="ab69a-140">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span><span class="sxs-lookup"><span data-stu-id="ab69a-140">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="ab69a-141">SQL Database communicates over port 1433.</span><span class="sxs-lookup"><span data-stu-id="ab69a-141">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="ab69a-142">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span><span class="sxs-lookup"><span data-stu-id="ab69a-142">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="ab69a-143">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span><span class="sxs-lookup"><span data-stu-id="ab69a-143">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="ab69a-144">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the SQL databases page.</span><span class="sxs-lookup"><span data-stu-id="ab69a-144">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the SQL databases page.</span></span> <span data-ttu-id="ab69a-145">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170411.database.windows.net**) and provides options for further configuration.</span><span class="sxs-lookup"><span data-stu-id="ab69a-145">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170411.database.windows.net**) and provides options for further configuration.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ab69a-146">You will need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span><span class="sxs-lookup"><span data-stu-id="ab69a-146">You will need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

      ![server name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. <span data-ttu-id="ab69a-148">Click **Set server firewall** on the toolbar as shown in the previous image.</span><span class="sxs-lookup"><span data-stu-id="ab69a-148">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="ab69a-149">The **Firewall settings** page for the SQL Database server opens.</span><span class="sxs-lookup"><span data-stu-id="ab69a-149">The **Firewall settings** page for the SQL Database server opens.</span></span> 

      ![server firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="ab69a-151">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span><span class="sxs-lookup"><span data-stu-id="ab69a-151">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="ab69a-152">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="ab69a-152">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="ab69a-153">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ab69a-153">Click **Save**.</span></span> <span data-ttu-id="ab69a-154">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span><span class="sxs-lookup"><span data-stu-id="ab69a-154">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

      ![set server firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="ab69a-156">Click **OK** and then close the **Firewall settings** page.</span><span class="sxs-lookup"><span data-stu-id="ab69a-156">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="ab69a-157">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span><span class="sxs-lookup"><span data-stu-id="ab69a-157">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab69a-158">By default, access through the SQL Database firewall is enabled for all Azure services.</span><span class="sxs-lookup"><span data-stu-id="ab69a-158">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="ab69a-159">Click **OFF** on this page to disable for all Azure services.</span><span class="sxs-lookup"><span data-stu-id="ab69a-159">Click **OFF** on this page to disable for all Azure services.</span></span>

## <a name="query-the-sql-database"></a><span data-ttu-id="ab69a-160">Query the SQL database</span><span class="sxs-lookup"><span data-stu-id="ab69a-160">Query the SQL database</span></span>

<span data-ttu-id="ab69a-161">Now that you have created a sample database in Azure, let’s use the built-in query tool within the Azure portal to confirm that you can connect to the database and query the data.</span><span class="sxs-lookup"><span data-stu-id="ab69a-161">Now that you have created a sample database in Azure, let’s use the built-in query tool within the Azure portal to confirm that you can connect to the database and query the data.</span></span> 

1. <span data-ttu-id="ab69a-162">On the SQL Database page for your database, click **Tools** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="ab69a-162">On the SQL Database page for your database, click **Tools** on the toolbar.</span></span> <span data-ttu-id="ab69a-163">The **Tools** page opens.</span><span class="sxs-lookup"><span data-stu-id="ab69a-163">The **Tools** page opens.</span></span>

     ![tools menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="ab69a-165">Click **Query editor (preview)**, click the **Preview terms** checkbox, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab69a-165">Click **Query editor (preview)**, click the **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="ab69a-166">The Query editor page opens.</span><span class="sxs-lookup"><span data-stu-id="ab69a-166">The Query editor page opens.</span></span>

3. <span data-ttu-id="ab69a-167">Click **Login** and then, when prompted, select **SQL server authentication** and then provide the server admin login and password that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ab69a-167">Click **Login** and then, when prompted, select **SQL server authentication** and then provide the server admin login and password that you created earlier.</span></span>

    ![login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="ab69a-169">Click **OK** to log in.</span><span class="sxs-lookup"><span data-stu-id="ab69a-169">Click **OK** to log in.</span></span>

5. <span data-ttu-id="ab69a-170">After you are authenticated, type the following query in the query editor pane.</span><span class="sxs-lookup"><span data-stu-id="ab69a-170">After you are authenticated, type the following query in the query editor pane.</span></span>

   ```
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="ab69a-171">Click **Run** and then review the query results in the **Results** pane.</span><span class="sxs-lookup"><span data-stu-id="ab69a-171">Click **Run** and then review the query results in the **Results** pane.</span></span>

    ![query editor results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="ab69a-173">Close the **Query editor** page and the **Tools** page.</span><span class="sxs-lookup"><span data-stu-id="ab69a-173">Close the **Query editor** page and the **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ab69a-174">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ab69a-174">Clean up resources</span></span>

<span data-ttu-id="ab69a-175">Other quick starts in this collection build upon this quick start.</span><span class="sxs-lookup"><span data-stu-id="ab69a-175">Other quick starts in this collection build upon this quick start.</span></span> <span data-ttu-id="ab69a-176">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span><span class="sxs-lookup"><span data-stu-id="ab69a-176">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="ab69a-177">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ab69a-177">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>

1. <span data-ttu-id="ab69a-178">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="ab69a-178">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="ab69a-179">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ab69a-179">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab69a-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab69a-180">Next steps</span></span>

- <span data-ttu-id="ab69a-181">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="ab69a-181">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="ab69a-182">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-182">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="ab69a-183">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-183">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="ab69a-184">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-184">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="ab69a-185">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-185">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="ab69a-186">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-186">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="ab69a-187">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-187">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="ab69a-188">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="ab69a-188">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>










