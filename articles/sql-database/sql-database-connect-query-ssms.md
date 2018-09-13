---
title: 'SSMS: Connect and query data in Azure SQL Database | Microsoft Docs'
description: Learn how to connect to SQL Database on Azure by using SQL Server Management Studio (SSMS). Then, run Transact-SQL (T-SQL) statements to query and edit data.
metacanonical: ''
keywords: connect to sql database,sql server management studio
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: 7cd2a114-c13c-4ace-9088-97bd9d68de12
ms.service: sql-database
ms.custom: quick start manage
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/15/2017
ms.author: carlrab
ms.openlocfilehash: 3a3e52c2b96117683f0c2095890ee64c5d5778e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553581"
---
# <a name="azure-sql-database-use-sql-server-management-studio-to-connect-and-query-data"></a><span data-ttu-id="fe7a5-105">Azure SQL Database: Use SQL Server Management Studio to connect and query data</span><span class="sxs-lookup"><span data-stu-id="fe7a5-105">Azure SQL Database: Use SQL Server Management Studio to connect and query data</span></span>

<span data-ttu-id="fe7a5-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is a management tool used to create and manage SQL Server resources from the user interface or in scripts.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-106">[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) is a management tool used to create and manage SQL Server resources from the user interface or in scripts.</span></span> <span data-ttu-id="fe7a5-107">This quick start demonstrates how to use SSMS to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-107">This quick start demonstrates how to use SSMS to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span> 

<span data-ttu-id="fe7a5-108">This quick start uses as its starting point the resources created in one of these quick starts:</span><span class="sxs-lookup"><span data-stu-id="fe7a5-108">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="fe7a5-109">Create DB - Portal</span><span class="sxs-lookup"><span data-stu-id="fe7a5-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="fe7a5-110">Create DB - CLI</span><span class="sxs-lookup"><span data-stu-id="fe7a5-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)

<span data-ttu-id="fe7a5-111">Before you start, make sure you have installed the newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-111">Before you start, make sure you have installed the newest version of [SSMS](https://msdn.microsoft.com/library/mt238290.aspx).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="fe7a5-112">Get connection information</span><span class="sxs-lookup"><span data-stu-id="fe7a5-112">Get connection information</span></span>

<span data-ttu-id="fe7a5-113">Get the connection information needed to connect to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-113">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="fe7a5-114">You will need the fully qualified server name, database name, and login information in the next procedures.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-114">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="fe7a5-115">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-115">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fe7a5-116">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-116">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="fe7a5-117">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-117">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span></span> <span data-ttu-id="fe7a5-118">You can hover over the server name to bring up the **Click to copy** option.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-118">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![connection information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connection-information.png) 

4. <span data-ttu-id="fe7a5-120">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-120">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="connect-to-your-database-in-the-sql-database-logical-server"></a><span data-ttu-id="fe7a5-121">Connect to your database in the SQL Database logical server</span><span class="sxs-lookup"><span data-stu-id="fe7a5-121">Connect to your database in the SQL Database logical server</span></span>

<span data-ttu-id="fe7a5-122">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-122">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fe7a5-123">An Azure SQL Database logical server listens on port 1433.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-123">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="fe7a5-124">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-124">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

1. <span data-ttu-id="fe7a5-125">Open SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-125">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="fe7a5-126">In the **Connect to Server** dialog box, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="fe7a5-126">In the **Connect to Server** dialog box, enter the following information:</span></span>
   - <span data-ttu-id="fe7a5-127">**Server type**: Specify Database engine</span><span class="sxs-lookup"><span data-stu-id="fe7a5-127">**Server type**: Specify Database engine</span></span>
   - <span data-ttu-id="fe7a5-128">**Server name**: Enter your fully qualified server name, such as **mynewserver20170313.database.windows.net**</span><span class="sxs-lookup"><span data-stu-id="fe7a5-128">**Server name**: Enter your fully qualified server name, such as **mynewserver20170313.database.windows.net**</span></span>
   - <span data-ttu-id="fe7a5-129">**Authentication**: Specify SQL Server Authentication</span><span class="sxs-lookup"><span data-stu-id="fe7a5-129">**Authentication**: Specify SQL Server Authentication</span></span>
   - <span data-ttu-id="fe7a5-130">**Login**: Enter your server admin account</span><span class="sxs-lookup"><span data-stu-id="fe7a5-130">**Login**: Enter your server admin account</span></span>
   - <span data-ttu-id="fe7a5-131">**Password**: Enter the password for your server admin account</span><span class="sxs-lookup"><span data-stu-id="fe7a5-131">**Password**: Enter the password for your server admin account</span></span>

   ![connect to server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connect.png)  

3. <span data-ttu-id="fe7a5-133">Click **Options** in the **Connect to server** dialog box.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-133">Click **Options** in the **Connect to server** dialog box.</span></span> <span data-ttu-id="fe7a5-134">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-134">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span></span>

   ![connect to db on server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="fe7a5-136">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-136">Click **Connect**.</span></span> <span data-ttu-id="fe7a5-137">The Object Explorer window opens in SSMS.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-137">The Object Explorer window opens in SSMS.</span></span> 

   ![connected to server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connected.png)  

5. <span data-ttu-id="fe7a5-139">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-139">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span></span>

## <a name="query-data"></a><span data-ttu-id="fe7a5-140">Query data</span><span class="sxs-lookup"><span data-stu-id="fe7a5-140">Query data</span></span>

<span data-ttu-id="fe7a5-141">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-141">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="fe7a5-142">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-142">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="fe7a5-143">A blank query window opens that is connected to your database.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-143">A blank query window opens that is connected to your database.</span></span>
2. <span data-ttu-id="fe7a5-144">In the query window, enter the following query:</span><span class="sxs-lookup"><span data-stu-id="fe7a5-144">In the query window, enter the following query:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

3. <span data-ttu-id="fe7a5-145">On the toolbar, click **Execute** to retrieve data from the Product and ProductCategory tables.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-145">On the toolbar, click **Execute** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/query.png)

## <a name="insert-data"></a><span data-ttu-id="fe7a5-147">Insert data</span><span class="sxs-lookup"><span data-stu-id="fe7a5-147">Insert data</span></span>

<span data-ttu-id="fe7a5-148">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-148">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="fe7a5-149">In the query window, replace the previous query with the following query:</span><span class="sxs-lookup"><span data-stu-id="fe7a5-149">In the query window, replace the previous query with the following query:</span></span>

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. <span data-ttu-id="fe7a5-150">On the toolbar, click **Execute**  to insert a new row in the Product table.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-150">On the toolbar, click **Execute**  to insert a new row in the Product table.</span></span>

    <img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/insert.png" alt="insert" style="width: 780px;" />

## <a name="update-data"></a><span data-ttu-id="fe7a5-151">Update data</span><span class="sxs-lookup"><span data-stu-id="fe7a5-151">Update data</span></span>

<span data-ttu-id="fe7a5-152">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-152">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="fe7a5-153">In the query window, replace the previous query with the following query:</span><span class="sxs-lookup"><span data-stu-id="fe7a5-153">In the query window, replace the previous query with the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="fe7a5-154">On the toolbar, click **Execute** to update the specified row in the Product table.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-154">On the toolbar, click **Execute** to update the specified row in the Product table.</span></span>

    <img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/update.png" alt="update" style="width: 780px;" />

## <a name="delete-data"></a><span data-ttu-id="fe7a5-155">Delete data</span><span class="sxs-lookup"><span data-stu-id="fe7a5-155">Delete data</span></span>

<span data-ttu-id="fe7a5-156">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-156">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="fe7a5-157">In the query window, replace the previous query with the following query:</span><span class="sxs-lookup"><span data-stu-id="fe7a5-157">In the query window, replace the previous query with the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="fe7a5-158">On the toolbar, click **Execute** to delete the specified row in the Product table.</span><span class="sxs-lookup"><span data-stu-id="fe7a5-158">On the toolbar, click **Execute** to delete the specified row in the Product table.</span></span>

    <img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/delete.png" alt="delete" style="width: 780px;" />

## <a name="next-steps"></a><span data-ttu-id="fe7a5-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="fe7a5-159">Next steps</span></span>

- <span data-ttu-id="fe7a5-160">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-160">For information about SSMS, see [Use SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).</span></span>
- <span data-ttu-id="fe7a5-161">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-161">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="fe7a5-162">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-162">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="fe7a5-163">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-163">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="fe7a5-164">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-164">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="fe7a5-165">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-165">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="fe7a5-166">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-166">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="fe7a5-167">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="fe7a5-167">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>








