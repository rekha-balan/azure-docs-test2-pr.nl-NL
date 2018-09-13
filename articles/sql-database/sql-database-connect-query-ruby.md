---
title: Connect Azure SQL Database by using Ruby | Microsoft Docs
description: Presents a Ruby code sample you can use to connect to and query Azure SQL Database.
services: sql-database
documentationcenter: ''
author: ajlam
manager: jhubbard
editor: ''
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: quick start connect
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 04/17/2017
ms.author: andrela;sstein;carlrab
ms.openlocfilehash: 2f905333da4dcfc9ce075ec8164520577802359e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553963"
---
# <a name="azure-sql-database-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="acb1b-103">Azure SQL Database: Use Ruby to connect and query data</span><span class="sxs-lookup"><span data-stu-id="acb1b-103">Azure SQL Database: Use Ruby to connect and query data</span></span>

<span data-ttu-id="acb1b-104">This quick start demonstrates how to use [Ruby](https://Ruby.org) to connect to an Azure SQL database, and then use Transact-SQL statements to  query, insert, update, and delete data in the database from Mac OS and Ubuntu Linux platforms.</span><span class="sxs-lookup"><span data-stu-id="acb1b-104">This quick start demonstrates how to use [Ruby](https://Ruby.org) to connect to an Azure SQL database, and then use Transact-SQL statements to  query, insert, update, and delete data in the database from Mac OS and Ubuntu Linux platforms.</span></span>

<span data-ttu-id="acb1b-105">This quick start uses as its starting point the resources created in one of these quick starts:</span><span class="sxs-lookup"><span data-stu-id="acb1b-105">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="acb1b-106">Create DB - Portal</span><span class="sxs-lookup"><span data-stu-id="acb1b-106">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="acb1b-107">Create DB - CLI</span><span class="sxs-lookup"><span data-stu-id="acb1b-107">Create DB - CLI</span></span>](sql-database-get-started-cli.md)

## <a name="install-ruby-and-database-communication-libraries"></a><span data-ttu-id="acb1b-108">Install Ruby and database communication libraries</span><span class="sxs-lookup"><span data-stu-id="acb1b-108">Install Ruby and database communication libraries</span></span>

<span data-ttu-id="acb1b-109">The steps in this section assume that you are familar with developing using Ruby and are new to working with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="acb1b-109">The steps in this section assume that you are familar with developing using Ruby and are new to working with Azure SQL Database.</span></span> <span data-ttu-id="acb1b-110">If you are new to developing with Ruby, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **Ruby** and then select your operating system.</span><span class="sxs-lookup"><span data-stu-id="acb1b-110">If you are new to developing with Ruby, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **Ruby** and then select your operating system.</span></span>

### <a name="mac-os"></a><span data-ttu-id="acb1b-111">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="acb1b-111">**Mac OS**</span></span>
<span data-ttu-id="acb1b-112">Open your terminal and navigate to a directory where you plan on creating your Ruby script.</span><span class="sxs-lookup"><span data-stu-id="acb1b-112">Open your terminal and navigate to a directory where you plan on creating your Ruby script.</span></span> <span data-ttu-id="acb1b-113">Enter the following commands to install **brew**, **FreeTDS**, and **TinyTDS**.</span><span class="sxs-lookup"><span data-stu-id="acb1b-113">Enter the following commands to install **brew**, **FreeTDS**, and **TinyTDS**.</span></span>

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/msodbcsql https://github.com/Microsoft/homebrew-msodbcsql-preview
brew update
brew install FreeTDS
gem install tiny_tds
```

### <a name="linux-ubuntu"></a><span data-ttu-id="acb1b-114">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="acb1b-114">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="acb1b-115">Open your terminal and navigate to a directory where you plan on creating your Ruby script.</span><span class="sxs-lookup"><span data-stu-id="acb1b-115">Open your terminal and navigate to a directory where you plan on creating your Ruby script.</span></span> <span data-ttu-id="acb1b-116">Enter the following commands to install the **FreeTDS** and **TinyTDS**.</span><span class="sxs-lookup"><span data-stu-id="acb1b-116">Enter the following commands to install the **FreeTDS** and **TinyTDS**.</span></span>

```bash
wget ftp://ftp.freetds.org/pub/freetds/stable/freetds-1.00.27.tar.gz
tar -xzf freetds-1.00.27.tar.gz
cd freetds-1.00.27
./configure --prefix=/usr/local --with-tdsver=7.3
make
make install
gem install tiny_tds
```

## <a name="get-connection-information"></a><span data-ttu-id="acb1b-117">Get connection information</span><span class="sxs-lookup"><span data-stu-id="acb1b-117">Get connection information</span></span>

<span data-ttu-id="acb1b-118">Get the connection information needed to connect to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="acb1b-118">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="acb1b-119">You will need the fully qualified server name, database name, and login information in the next procedures.</span><span class="sxs-lookup"><span data-stu-id="acb1b-119">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="acb1b-120">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="acb1b-120">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="acb1b-121">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="acb1b-121">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="acb1b-122">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="acb1b-122">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span></span> <span data-ttu-id="acb1b-123">You can hover over the server name to bring up the **Click to copy** option.</span><span class="sxs-lookup"><span data-stu-id="acb1b-123">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="acb1b-125">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span><span class="sxs-lookup"><span data-stu-id="acb1b-125">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>
    

## <a name="select-data"></a><span data-ttu-id="acb1b-126">Select data</span><span class="sxs-lookup"><span data-stu-id="acb1b-126">Select data</span></span>
<span data-ttu-id="acb1b-127">Use the following code to query for the top 20 products by category using the [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) function with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="acb1b-127">Use the following code to query for the top 20 products by category using the [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) function with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="acb1b-128">The TinyTDS::Client function accepts a query and returns a result set.</span><span class="sxs-lookup"><span data-stu-id="acb1b-128">The TinyTDS::Client function accepts a query and returns a result set.</span></span> <span data-ttu-id="acb1b-129">The results set is iterated over by using [result.each do |row|](https://github.com/rails-sqlserver/tiny_tds).</span><span class="sxs-lookup"><span data-stu-id="acb1b-129">The results set is iterated over by using [result.each do |row|](https://github.com/rails-sqlserver/tiny_tds).</span></span> <span data-ttu-id="acb1b-130">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="acb1b-130">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="insert-data"></a><span data-ttu-id="acb1b-131">Insert data</span><span class="sxs-lookup"><span data-stu-id="acb1b-131">Insert data</span></span>
<span data-ttu-id="acb1b-132">Use the following code to insert a new product into the SalesLT.Product table using the [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) function with an [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="acb1b-132">Use the following code to insert a new product into the SalesLT.Product table using the [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) function with an [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="acb1b-133">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="acb1b-133">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

<span data-ttu-id="acb1b-134">Tis example demonstrates how to execute an INSERT statement safely, pass parameters which protect your application from [SQL injection](https://technet.microsoft.com/library/ms161953(v=sql.105).aspx) vulnerability, and retrieve the auto-generated [Primary Key](https://docs.microsoft.com/sql/relational-databases/tables/primary-and-foreign-key-constraints) value.</span><span class="sxs-lookup"><span data-stu-id="acb1b-134">Tis example demonstrates how to execute an INSERT statement safely, pass parameters which protect your application from [SQL injection](https://technet.microsoft.com/library/ms161953(v=sql.105).aspx) vulnerability, and retrieve the auto-generated [Primary Key](https://docs.microsoft.com/sql/relational-databases/tables/primary-and-foreign-key-constraints) value.</span></span>    
  
<span data-ttu-id="acb1b-135">To use TinyTDS with Azure, it is recommended that you execute several `SET` statements to change how the current session handles specific information.</span><span class="sxs-lookup"><span data-stu-id="acb1b-135">To use TinyTDS with Azure, it is recommended that you execute several `SET` statements to change how the current session handles specific information.</span></span> <span data-ttu-id="acb1b-136">Recommended `SET` statements are provided in the code sample.</span><span class="sxs-lookup"><span data-stu-id="acb1b-136">Recommended `SET` statements are provided in the code sample.</span></span> <span data-ttu-id="acb1b-137">For example, `SET ANSI_NULL_DFLT_ON` will allow new columns created to allow null values even if the nullability status of the column is not explicitly stated.</span><span class="sxs-lookup"><span data-stu-id="acb1b-137">For example, `SET ANSI_NULL_DFLT_ON` will allow new columns created to allow null values even if the nullability status of the column is not explicitly stated.</span></span>  
  
<span data-ttu-id="acb1b-138">To align with the Microsoft SQL Server [datetime](https://docs.microsoft.com/sql/t-sql/data-types/datetime-transact-sql) format, use the [strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) function to cast to the corresponding datetime format.</span><span class="sxs-lookup"><span data-stu-id="acb1b-138">To align with the Microsoft SQL Server [datetime](https://docs.microsoft.com/sql/t-sql/data-types/datetime-transact-sql) format, use the [strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) function to cast to the corresponding datetime format.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

# settings for Azure
result = client.execute("SET ANSI_NULLS ON")
result = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")
result = client.execute("SET ANSI_NULL_DFLT_ON ON")
result = client.execute("SET IMPLICIT_TRANSACTIONS OFF")
result = client.execute("SET ANSI_PADDING ON")
result = client.execute("SET QUOTED_IDENTIFIER ON")
result = client.execute("SET ANSI_WARNINGS ON")
result = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")

def insert(name, productnumber, color, standardcost, listprice, sellstartdate)
    tsql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) 
        VALUES (N'#{name}', N'#{productnumber}',N'#{color}',N'#{standardcost}',N'#{listprice}',N'#{sellstartdate}')"
    result = client.execute(tsql)
    result.each
    puts "#{result.affected_rows} row(s) affected"
end
insert('BrandNewProduct', '200989', 'Blue', 75, 80, '7/1/2016')
```

## <a name="update-data"></a><span data-ttu-id="acb1b-139">Update data</span><span class="sxs-lookup"><span data-stu-id="acb1b-139">Update data</span></span>
<span data-ttu-id="acb1b-140">Use the following code to update the new product that you previously added using the [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) function with a [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="acb1b-140">Use the following code to update the new product that you previously added using the [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) function with a [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="acb1b-141">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="acb1b-141">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true
    
def update(name, listPrice, client)
    tsql = "UPDATE SalesLT.Product SET ListPrice = N'#{listPrice}' WHERE Name =N'#{name}'";
    result = client.execute(tsql)
    result.each
    puts "#{result.affected_rows} row(s) affected"
end
update('BrandNewProduct', 500, client)
```

## <a name="delete-data"></a><span data-ttu-id="acb1b-142">Delete data</span><span class="sxs-lookup"><span data-stu-id="acb1b-142">Delete data</span></span>
<span data-ttu-id="acb1b-143">Use the following code to delete the new product that you previously added using the [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) function with a [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="acb1b-143">Use the following code to delete the new product that you previously added using the [TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) function with a [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="acb1b-144">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="acb1b-144">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

# settings for Azure
result = client.execute("SET ANSI_NULLS ON")
result = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")
result = client.execute("SET ANSI_NULL_DFLT_ON ON")
result = client.execute("SET IMPLICIT_TRANSACTIONS OFF")
result = client.execute("SET ANSI_PADDING ON")
result = client.execute("SET QUOTED_IDENTIFIER ON")
result = client.execute("SET ANSI_WARNINGS ON")
result = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")

def delete(name, client)
    tsql = "DELETE FROM SalesLT.Product WHERE Name = N'#{name}'"
    result = client.execute(tsql)
    result.each
    puts "#{result.affected_rows} row(s) affected"
end
delete('BrandNewProduct', client)
```

## <a name="next-steps"></a><span data-ttu-id="acb1b-145">Next Steps</span><span class="sxs-lookup"><span data-stu-id="acb1b-145">Next Steps</span></span>

- <span data-ttu-id="acb1b-146">Github repository for [TinyTDS](https://github.com/rails-sqlserver/tiny_tds).</span><span class="sxs-lookup"><span data-stu-id="acb1b-146">Github repository for [TinyTDS](https://github.com/rails-sqlserver/tiny_tds).</span></span>
- <span data-ttu-id="acb1b-147">[File issues/ask questions](https://github.com/rails-sqlserver/tiny_tds/issues).</span><span class="sxs-lookup"><span data-stu-id="acb1b-147">[File issues/ask questions](https://github.com/rails-sqlserver/tiny_tds/issues).</span></span>      
- <span data-ttu-id="acb1b-148">More information on the [Ruby Driver for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/).</span><span class="sxs-lookup"><span data-stu-id="acb1b-148">More information on the [Ruby Driver for SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/).</span></span>
- <span data-ttu-id="acb1b-149">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="acb1b-149">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="acb1b-150">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="acb1b-150">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="acb1b-151">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="acb1b-151">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="acb1b-152">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="acb1b-152">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="acb1b-153">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="acb1b-153">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="acb1b-154">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="acb1b-154">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="acb1b-155">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="acb1b-155">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>

