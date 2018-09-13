---
title: Connect to Azure SQL Database by using .NET (C#) | Microsoft Docs
description: Presents a .NET code sample you can use to connect to and query Azure SQL Database
services: sql-database
documentationcenter: ''
author: ajlam
manager: jhubbard
editor: ''
ms.assetid: 7faca033-24b4-4f64-9301-b4de41e73dfd
ms.service: sql-database
ms.custom: quick start connect
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: andrela;sstein;carlrab
ms.openlocfilehash: 072994906fe31e54cb6eca4f467aeee5fc73e9e2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661371"
---
# <a name="azure-sql-database-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="b3560-103">Azure SQL Database: Use .NET (C#) to connect and query data</span><span class="sxs-lookup"><span data-stu-id="b3560-103">Azure SQL Database: Use .NET (C#) to connect and query data</span></span>

<span data-ttu-id="b3560-104">This quick start demonstrates how to use [C# and ADO.NET](https://msdn.microsoft.com/library/kb9s9ks0.aspx) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from the Windows, Mac OS, and Ubuntu Linux platforms.</span><span class="sxs-lookup"><span data-stu-id="b3560-104">This quick start demonstrates how to use [C# and ADO.NET](https://msdn.microsoft.com/library/kb9s9ks0.aspx) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from the Windows, Mac OS, and Ubuntu Linux platforms.</span></span>

<span data-ttu-id="b3560-105">This quick start uses as its starting point the resources created in one of these quick starts:</span><span class="sxs-lookup"><span data-stu-id="b3560-105">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="b3560-106">Create DB - Portal</span><span class="sxs-lookup"><span data-stu-id="b3560-106">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="b3560-107">Create DB - CLI</span><span class="sxs-lookup"><span data-stu-id="b3560-107">Create DB - CLI</span></span>](sql-database-get-started-cli.md)

## <a name="install-net"></a><span data-ttu-id="b3560-108">Install .NET</span><span class="sxs-lookup"><span data-stu-id="b3560-108">Install .NET</span></span>

<span data-ttu-id="b3560-109">The steps in this section assume that you are familar with developing using .NET and are new to working with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b3560-109">The steps in this section assume that you are familar with developing using .NET and are new to working with Azure SQL Database.</span></span> <span data-ttu-id="b3560-110">If you are new to developing with .NET, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **C#** and then select your operating system.</span><span class="sxs-lookup"><span data-stu-id="b3560-110">If you are new to developing with .NET, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **C#** and then select your operating system.</span></span>

### <a name="windows-net-framework-and-net-core"></a><span data-ttu-id="b3560-111">**Windows .NET framework and .NET core**</span><span class="sxs-lookup"><span data-stu-id="b3560-111">**Windows .NET framework and .NET core**</span></span>

<span data-ttu-id="b3560-112">Visual Studio 2017 Community is a fully-featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span><span class="sxs-lookup"><span data-stu-id="b3560-112">Visual Studio 2017 Community is a fully-featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="b3560-113">You can install either the full .NET framework or just .NET core.</span><span class="sxs-lookup"><span data-stu-id="b3560-113">You can install either the full .NET framework or just .NET core.</span></span> <span data-ttu-id="b3560-114">The code snippets in the quick start work with either.</span><span class="sxs-lookup"><span data-stu-id="b3560-114">The code snippets in the quick start work with either.</span></span> <span data-ttu-id="b3560-115">If you already have Visual Studio installed on your machine, skip the next few steps.</span><span class="sxs-lookup"><span data-stu-id="b3560-115">If you already have Visual Studio installed on your machine, skip the next few steps.</span></span>

1. <span data-ttu-id="b3560-116">Download the [installer](https://go.microsoft.com/fwlink/?LinkId=691978).</span><span class="sxs-lookup"><span data-stu-id="b3560-116">Download the [installer](https://go.microsoft.com/fwlink/?LinkId=691978).</span></span> 
2. <span data-ttu-id="b3560-117">Run the installer and follow the installation prompts to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="b3560-117">Run the installer and follow the installation prompts to complete the installation.</span></span>

### <a name="mac-os"></a><span data-ttu-id="b3560-118">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="b3560-118">**Mac OS**</span></span>
<span data-ttu-id="b3560-119">Open your terminal and navigate to a directory where you plan on creating your .NET Core project.</span><span class="sxs-lookup"><span data-stu-id="b3560-119">Open your terminal and navigate to a directory where you plan on creating your .NET Core project.</span></span> <span data-ttu-id="b3560-120">Enter the following commands to install **brew**, **OpenSSL**, and **.NET Core**.</span><span class="sxs-lookup"><span data-stu-id="b3560-120">Enter the following commands to install **brew**, **OpenSSL**, and **.NET Core**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

<span data-ttu-id="b3560-121">Install .NET Core on macOS.</span><span class="sxs-lookup"><span data-stu-id="b3560-121">Install .NET Core on macOS.</span></span> <span data-ttu-id="b3560-122">Download the [official installer](https://go.microsoft.com/fwlink/?linkid=843444).</span><span class="sxs-lookup"><span data-stu-id="b3560-122">Download the [official installer](https://go.microsoft.com/fwlink/?linkid=843444).</span></span> <span data-ttu-id="b3560-123">This installer will install the tools and put them on your PATH so you can run dotnet from the Console</span><span class="sxs-lookup"><span data-stu-id="b3560-123">This installer will install the tools and put them on your PATH so you can run dotnet from the Console</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="b3560-124">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="b3560-124">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="b3560-125">Open your terminal and navigate to a directory where you plan on creating your .NET Core project.</span><span class="sxs-lookup"><span data-stu-id="b3560-125">Open your terminal and navigate to a directory where you plan on creating your .NET Core project.</span></span> <span data-ttu-id="b3560-126">Enter the following commands to install **.NET Core**.</span><span class="sxs-lookup"><span data-stu-id="b3560-126">Enter the following commands to install **.NET Core**.</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.1
```

## <a name="get-connection-information"></a><span data-ttu-id="b3560-127">Get connection information</span><span class="sxs-lookup"><span data-stu-id="b3560-127">Get connection information</span></span>

<span data-ttu-id="b3560-128">Get the connection information needed to connect to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="b3560-128">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="b3560-129">You will need the fully qualified server name, database name, and login information in the next procedures.</span><span class="sxs-lookup"><span data-stu-id="b3560-129">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="b3560-130">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b3560-130">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b3560-131">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="b3560-131">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="b3560-132">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="b3560-132">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span></span> <span data-ttu-id="b3560-133">You can hover over the server name to bring up the **Click to copy** option.</span><span class="sxs-lookup"><span data-stu-id="b3560-133">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="b3560-135">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span><span class="sxs-lookup"><span data-stu-id="b3560-135">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>

5. <span data-ttu-id="b3560-136">Click **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="b3560-136">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="b3560-137">Review the complete**ADO.NET** connection string.</span><span class="sxs-lookup"><span data-stu-id="b3560-137">Review the complete**ADO.NET** connection string.</span></span>

    ![ADO.NET connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-dotnet/adonet-connection-string.png)
  
## <a name="add-systemdatasqlclient"></a><span data-ttu-id="b3560-139">Add System.Data.SqlClient</span><span class="sxs-lookup"><span data-stu-id="b3560-139">Add System.Data.SqlClient</span></span>
<span data-ttu-id="b3560-140">When using .NET core, add System.Data.SqlClient to your project's ***csproj*** file as a dependency.</span><span class="sxs-lookup"><span data-stu-id="b3560-140">When using .NET core, add System.Data.SqlClient to your project's ***csproj*** file as a dependency.</span></span>

```xml
<ItemGroup>
    <PackageReference Include="System.Data.SqlClient" Version="4.3.0" />
</ItemGroup>
```

## <a name="select-data"></a><span data-ttu-id="b3560-141">Select data</span><span class="sxs-lookup"><span data-stu-id="b3560-141">Select data</span></span>

1. <span data-ttu-id="b3560-142">In your development environment, open a blank code file.</span><span class="sxs-lookup"><span data-stu-id="b3560-142">In your development environment, open a blank code file.</span></span>
2. <span data-ttu-id="b3560-143">Add ```using System.Data.SqlClient``` to your code file ([System.Data.SqlClient namespace](https://msdn.microsoft.com/library/system.data.sqlclient.aspx)).</span><span class="sxs-lookup"><span data-stu-id="b3560-143">Add ```using System.Data.SqlClient``` to your code file ([System.Data.SqlClient namespace](https://msdn.microsoft.com/library/system.data.sqlclient.aspx)).</span></span> 

3. <span data-ttu-id="b3560-144">Use the following code to query for the top 20 products by category with the [SqlCommand.ExecuteReader](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executereader.aspx) command with a [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="b3560-144">Use the following code to query for the top 20 products by category with the [SqlCommand.ExecuteReader](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executereader.aspx) command with a [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span> <span data-ttu-id="b3560-145">Add the appropriate values for your server, database, user and password.</span><span class="sxs-lookup"><span data-stu-id="b3560-145">Add the appropriate values for your server, database, user and password.</span></span>

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
        }
    }
}
```

## <a name="insert-data"></a><span data-ttu-id="b3560-146">Insert data</span><span class="sxs-lookup"><span data-stu-id="b3560-146">Insert data</span></span>

<span data-ttu-id="b3560-147">Use the following code to insert a new product into the SalesLT.Product table using the [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) with an [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="b3560-147">Use the following code to insert a new product into the SalesLT.Product table using the [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) with an [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span> <span data-ttu-id="b3560-148">Add the appropriate values for your server, database, user and password.</span><span class="sxs-lookup"><span data-stu-id="b3560-148">Add the appropriate values for your server, database, user and password.</span></span>

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nInsert data example:");
                    Console.WriteLine("=========================================\n");

                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("INSERT INTO [SalesLT].[Product] ([Name], [ProductNumber], [Color], [StandardCost], [ListPrice], [SellStartDate]) ");
                    sb.Append("VALUES (@Name, @ProductNumber, @Color, @StandardCost, @ListPrice, @SellStartDate);");
                    String sql = sb.ToString();
                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        command.Parameters.AddWithValue("@Name", "BrandNewProduct");
                        command.Parameters.AddWithValue("@ProductNumber", "200989");
                        command.Parameters.AddWithValue("@Color", "Blue");
                        command.Parameters.AddWithValue("@StandardCost", 75);
                        command.Parameters.AddWithValue("@ListPrice", 80);
                        command.Parameters.AddWithValue("@SellStartDate", "7/1/2016");
                        int rowsAffected = command.ExecuteNonQuery();
                        Console.WriteLine(rowsAffected + " row(s) inserted");
                    }         
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
        }
    }
}
```

## <a name="update-data"></a><span data-ttu-id="b3560-149">Update data</span><span class="sxs-lookup"><span data-stu-id="b3560-149">Update data</span></span>

<span data-ttu-id="b3560-150">Use the following code to update the new product that you previously added using the [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) with an [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="b3560-150">Use the following code to update the new product that you previously added using the [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) with an [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span> <span data-ttu-id="b3560-151">Add the appropriate values for your server, database, user and password.</span><span class="sxs-lookup"><span data-stu-id="b3560-151">Add the appropriate values for your server, database, user and password.</span></span>

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nUpdate data example");
                    Console.WriteLine("=========================================\n");

                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("UPDATE [SalesLT].[Product] SET ListPrice = @ListPrice WHERE Name = @Name;");
                    String sql = sb.ToString();
                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        command.Parameters.AddWithValue("@Name", "BrandNewProduct");
                        command.Parameters.AddWithValue("@ListPrice", 500);
                        int rowsAffected = command.ExecuteNonQuery();
                        Console.WriteLine(rowsAffected + " row(s) updated");
                    }         
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
        }
    }
}
```

## <a name="delete-data"></a><span data-ttu-id="b3560-152">Delete data</span><span class="sxs-lookup"><span data-stu-id="b3560-152">Delete data</span></span>

<span data-ttu-id="b3560-153">Use the following code to delete the new product that you previously added using the [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) with a [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement .</span><span class="sxs-lookup"><span data-stu-id="b3560-153">Use the following code to delete the new product that you previously added using the [SqlCommand.ExecuteNonQuery](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.executenonquery.aspx) with a [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement .</span></span> <span data-ttu-id="b3560-154">Add the appropriate values for your server, database, user and password.</span><span class="sxs-lookup"><span data-stu-id="b3560-154">Add the appropriate values for your server, database, user and password.</span></span>

```csharp
using System;
using System.Data;
using System.Data.SqlClient;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nDelete data example");
                    Console.WriteLine("=========================================\n");

                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("DELETE FROM SalesLT.Product WHERE Name = @Name;");
                    String sql = sb.ToString();
                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        command.Parameters.AddWithValue("@Name", "BrandNewProduct");
                        int rowsAffected = command.ExecuteNonQuery();
                        Console.WriteLine(rowsAffected + " row(s) deleted");
                    }         
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="b3560-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="b3560-155">Next steps</span></span>

- <span data-ttu-id="b3560-156">For .NET documentation, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="b3560-156">For .NET documentation, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
- <span data-ttu-id="b3560-157">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="b3560-157">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="b3560-158">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="b3560-158">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="b3560-159">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="b3560-159">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="b3560-160">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b3560-160">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="b3560-161">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="b3560-161">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="b3560-162">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="b3560-162">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="b3560-163">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="b3560-163">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>


