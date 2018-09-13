---
title: 'VS Code: Connect and query data in Azure SQL Database | Microsoft Docs'
description: Learn how to connect to SQL Database on Azure by using Visual Studio Code. Then, run Transact-SQL (T-SQL) statements to query and edit data.
metacanonical: ''
keywords: connect to sql database
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: quick start manage
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 7b9c7f49caf6650fc65143887469a9cc3deffa81
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552142"
---
# <a name="azure-sql-database-use-visual-studio-code-to-connect-and-query-data"></a><span data-ttu-id="5627a-105">Azure SQL Database: Use Visual Studio Code to connect and query data</span><span class="sxs-lookup"><span data-stu-id="5627a-105">Azure SQL Database: Use Visual Studio Code to connect and query data</span></span>

<span data-ttu-id="5627a-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5627a-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="5627a-107">This quick start demonstrates how to use Visual Studio Code to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="5627a-107">This quick start demonstrates how to use Visual Studio Code to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span>

<span data-ttu-id="5627a-108">This quick start uses as its starting point the resources created in one of these quick starts:</span><span class="sxs-lookup"><span data-stu-id="5627a-108">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="5627a-109">Create DB - Portal</span><span class="sxs-lookup"><span data-stu-id="5627a-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="5627a-110">Create DB - CLI</span><span class="sxs-lookup"><span data-stu-id="5627a-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)

<span data-ttu-id="5627a-111">Before you start, make sure you have installed the newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded the [mssql extension](https://aka.ms/mssql-marketplace).</span><span class="sxs-lookup"><span data-stu-id="5627a-111">Before you start, make sure you have installed the newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded the [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="5627a-112">For installation guidance for the mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span><span class="sxs-lookup"><span data-stu-id="5627a-112">For installation guidance for the mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="5627a-113">Configure VS Code</span><span class="sxs-lookup"><span data-stu-id="5627a-113">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="5627a-114">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="5627a-114">**Mac OS**</span></span>
<span data-ttu-id="5627a-115">For macOS, you need to install OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span><span class="sxs-lookup"><span data-stu-id="5627a-115">For macOS, you need to install OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="5627a-116">Open your terminal and enter the following commands to install **brew** and **OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="5627a-116">Open your terminal and enter the following commands to install **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="5627a-117">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="5627a-117">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="5627a-118">No special configuration needed.</span><span class="sxs-lookup"><span data-stu-id="5627a-118">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="5627a-119">**Windows**</span><span class="sxs-lookup"><span data-stu-id="5627a-119">**Windows**</span></span>

<span data-ttu-id="5627a-120">No special configuration needed.</span><span class="sxs-lookup"><span data-stu-id="5627a-120">No special configuration needed.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="5627a-121">Get connection information</span><span class="sxs-lookup"><span data-stu-id="5627a-121">Get connection information</span></span>

<span data-ttu-id="5627a-122">Get the connection information needed to connect to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="5627a-122">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="5627a-123">You will need the fully qualified server name, database name, and login information in the next procedures.</span><span class="sxs-lookup"><span data-stu-id="5627a-123">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="5627a-124">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5627a-124">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5627a-125">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="5627a-125">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="5627a-126">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="5627a-126">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="5627a-127">You can hover over the server name to bring up the **Click to copy** option.</span><span class="sxs-lookup"><span data-stu-id="5627a-127">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![connection information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connection-information.png) 

4. <span data-ttu-id="5627a-129">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span><span class="sxs-lookup"><span data-stu-id="5627a-129">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="set-language-mode-to-sql"></a><span data-ttu-id="5627a-130">Set language mode to SQL</span><span class="sxs-lookup"><span data-stu-id="5627a-130">Set language mode to SQL</span></span>

<span data-ttu-id="5627a-131">Set the language mode is set to **SQL** in Visual Studio Code to enable mssql commands and T-SQL IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="5627a-131">Set the language mode is set to **SQL** in Visual Studio Code to enable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="5627a-132">Open a new Visual Studio Code window.</span><span class="sxs-lookup"><span data-stu-id="5627a-132">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="5627a-133">Click **Plain Text** in the lower right-hand corner of the status bar.</span><span class="sxs-lookup"><span data-stu-id="5627a-133">Click **Plain Text** in the lower right-hand corner of the status bar.</span></span>
3. <span data-ttu-id="5627a-134">In the **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** to set the language mode to SQL.</span><span class="sxs-lookup"><span data-stu-id="5627a-134">In the **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** to set the language mode to SQL.</span></span> 

   ![SQL language mode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-to-your-database-in-the-sql-database-logical-server"></a><span data-ttu-id="5627a-136">Connect to your database in the SQL Database logical server</span><span class="sxs-lookup"><span data-stu-id="5627a-136">Connect to your database in the SQL Database logical server</span></span>

<span data-ttu-id="5627a-137">Use Visual Studio Code to establish a connection to your Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="5627a-137">Use Visual Studio Code to establish a connection to your Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5627a-138">Before continuing, make sure that you have your server, database, and login information ready.</span><span class="sxs-lookup"><span data-stu-id="5627a-138">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="5627a-139">Once you begin entering the connection profile information, if you change your focus from Visual Studio Code, you have to restart creating the connection profile.</span><span class="sxs-lookup"><span data-stu-id="5627a-139">Once you begin entering the connection profile information, if you change your focus from Visual Studio Code, you have to restart creating the connection profile.</span></span>
>

1. <span data-ttu-id="5627a-140">In VS Code, press **CTRL+SHIFT+P** (or **F1**) to open the Command Palette.</span><span class="sxs-lookup"><span data-stu-id="5627a-140">In VS Code, press **CTRL+SHIFT+P** (or **F1**) to open the Command Palette.</span></span>

2. <span data-ttu-id="5627a-141">Type **sqlcon** and press **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="5627a-141">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="5627a-142">Press **ENTER** to select **Create Connection Profile**.</span><span class="sxs-lookup"><span data-stu-id="5627a-142">Press **ENTER** to select **Create Connection Profile**.</span></span> <span data-ttu-id="5627a-143">This creates a connection profile for your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="5627a-143">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="5627a-144">Follow the prompts to specify the connection properties for the new connection profile.</span><span class="sxs-lookup"><span data-stu-id="5627a-144">Follow the prompts to specify the connection properties for the new connection profile.</span></span> <span data-ttu-id="5627a-145">After specifying each value, press **ENTER** to continue.</span><span class="sxs-lookup"><span data-stu-id="5627a-145">After specifying each value, press **ENTER** to continue.</span></span> 

   <span data-ttu-id="5627a-146">The following table describes the Connection Profile properties.</span><span class="sxs-lookup"><span data-stu-id="5627a-146">The following table describes the Connection Profile properties.</span></span>

   | <span data-ttu-id="5627a-147">Setting</span><span class="sxs-lookup"><span data-stu-id="5627a-147">Setting</span></span> | <span data-ttu-id="5627a-148">Description</span><span class="sxs-lookup"><span data-stu-id="5627a-148">Description</span></span> |
   |-----|-----|
   | <span data-ttu-id="5627a-149">**Server name**</span><span class="sxs-lookup"><span data-stu-id="5627a-149">**Server name**</span></span> | <span data-ttu-id="5627a-150">Enter your fully qualified server name, such as **mynewserver20170313.database.windows.net**</span><span class="sxs-lookup"><span data-stu-id="5627a-150">Enter your fully qualified server name, such as **mynewserver20170313.database.windows.net**</span></span> |
   | <span data-ttu-id="5627a-151">**Database name**</span><span class="sxs-lookup"><span data-stu-id="5627a-151">**Database name**</span></span> | <span data-ttu-id="5627a-152">Enter your database name, such as **mySampleDatabase**</span><span class="sxs-lookup"><span data-stu-id="5627a-152">Enter your database name, such as **mySampleDatabase**</span></span> |
   | <span data-ttu-id="5627a-153">**Authentication**</span><span class="sxs-lookup"><span data-stu-id="5627a-153">**Authentication**</span></span> | <span data-ttu-id="5627a-154">Select SQL Login</span><span class="sxs-lookup"><span data-stu-id="5627a-154">Select SQL Login</span></span> |
   | <span data-ttu-id="5627a-155">**User name**</span><span class="sxs-lookup"><span data-stu-id="5627a-155">**User name**</span></span> | <span data-ttu-id="5627a-156">Enter your server admin account</span><span class="sxs-lookup"><span data-stu-id="5627a-156">Enter your server admin account</span></span> |
   | <span data-ttu-id="5627a-157">**Password (SQL Login)**</span><span class="sxs-lookup"><span data-stu-id="5627a-157">**Password (SQL Login)**</span></span> | <span data-ttu-id="5627a-158">Enter the password for your server admin account</span><span class="sxs-lookup"><span data-stu-id="5627a-158">Enter the password for your server admin account</span></span> | 
   | <span data-ttu-id="5627a-159">**Save Password?**</span><span class="sxs-lookup"><span data-stu-id="5627a-159">**Save Password?**</span></span> | <span data-ttu-id="5627a-160">Select **Yes** or **No**</span><span class="sxs-lookup"><span data-stu-id="5627a-160">Select **Yes** or **No**</span></span> |
   | <span data-ttu-id="5627a-161">**[Optional] Enter a name for this profile**</span><span class="sxs-lookup"><span data-stu-id="5627a-161">**[Optional] Enter a name for this profile**</span></span> | <span data-ttu-id="5627a-162">Enter a connection profile name, such as **mySampleDatabase**.</span><span class="sxs-lookup"><span data-stu-id="5627a-162">Enter a connection profile name, such as **mySampleDatabase**.</span></span> 

5. <span data-ttu-id="5627a-163">Press the **ESC** key to close the info message that informs you that the profile is created and connected.</span><span class="sxs-lookup"><span data-stu-id="5627a-163">Press the **ESC** key to close the info message that informs you that the profile is created and connected.</span></span>

6. <span data-ttu-id="5627a-164">Verify your connection in the status bar.</span><span class="sxs-lookup"><span data-stu-id="5627a-164">Verify your connection in the status bar.</span></span>

   ![Connection status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="5627a-166">Query data</span><span class="sxs-lookup"><span data-stu-id="5627a-166">Query data</span></span>

<span data-ttu-id="5627a-167">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="5627a-167">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="5627a-168">In the **Editor** window, enter the following query in the empty query window:</span><span class="sxs-lookup"><span data-stu-id="5627a-168">In the **Editor** window, enter the following query in the empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="5627a-169">Press **CTRL+SHIFT+E** to retrieve data from the Product and ProductCategory tables.</span><span class="sxs-lookup"><span data-stu-id="5627a-169">Press **CTRL+SHIFT+E** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![Query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="5627a-171">Insert data</span><span class="sxs-lookup"><span data-stu-id="5627a-171">Insert data</span></span>

<span data-ttu-id="5627a-172">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="5627a-172">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="5627a-173">In the **Editor** window, delete the previous query and enter the following query:</span><span class="sxs-lookup"><span data-stu-id="5627a-173">In the **Editor** window, delete the previous query and enter the following query:</span></span>

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

2. <span data-ttu-id="5627a-174">Press **CTRL+SHIFT+E** to insert a new row in the Product table.</span><span class="sxs-lookup"><span data-stu-id="5627a-174">Press **CTRL+SHIFT+E** to insert a new row in the Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="5627a-175">Update data</span><span class="sxs-lookup"><span data-stu-id="5627a-175">Update data</span></span>

<span data-ttu-id="5627a-176">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="5627a-176">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="5627a-177">In the **Editor** window, delete the previous query and enter the following query:</span><span class="sxs-lookup"><span data-stu-id="5627a-177">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="5627a-178">Press **CTRL+SHIFT+E** to update the specified row in the Product table.</span><span class="sxs-lookup"><span data-stu-id="5627a-178">Press **CTRL+SHIFT+E** to update the specified row in the Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="5627a-179">Delete data</span><span class="sxs-lookup"><span data-stu-id="5627a-179">Delete data</span></span>

<span data-ttu-id="5627a-180">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="5627a-180">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="5627a-181">In the **Editor** window, delete the previous query and enter the following query:</span><span class="sxs-lookup"><span data-stu-id="5627a-181">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="5627a-182">Press **CTRL+SHIFT+E** to delete the specified row in the Product table.</span><span class="sxs-lookup"><span data-stu-id="5627a-182">Press **CTRL+SHIFT+E** to delete the specified row in the Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5627a-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="5627a-183">Next steps</span></span>

- <span data-ttu-id="5627a-184">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="5627a-184">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="5627a-185">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5627a-185">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="5627a-186">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="5627a-186">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="5627a-187">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5627a-187">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="5627a-188">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="5627a-188">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="5627a-189">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="5627a-189">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="5627a-190">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="5627a-190">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>




