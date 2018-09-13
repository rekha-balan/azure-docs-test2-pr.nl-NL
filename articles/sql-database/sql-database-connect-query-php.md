---
title: Connect to Azure SQL Database by using PHP | Microsoft Docs
description: Presents a PHP code sample you can use to connect to and query Azure SQL Database.
services: sql-database
documentationcenter: ''
author: meet-bhagdev
manager: jhubbard
editor: ''
ms.assetid: 4e71db4a-a22f-4f1c-83e5-4a34a036ecf3
ms.service: sql-database
ms.custom: quick start connect
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 04/17/2017
ms.author: meetb;carlrab;sstein
ms.openlocfilehash: c01423081b6a35a160f5e6d1d1587c2f69fefc24
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564664"
---
# <a name="azure-sql-database-use-php-to-connect-and-query-data"></a><span data-ttu-id="f170f-103">Azure SQL Database: Use PHP to connect and query data</span><span class="sxs-lookup"><span data-stu-id="f170f-103">Azure SQL Database: Use PHP to connect and query data</span></span>

<span data-ttu-id="f170f-104">This quick start demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span><span class="sxs-lookup"><span data-stu-id="f170f-104">This quick start demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span>

<span data-ttu-id="f170f-105">This quick start uses as its starting point the resources created in one of these quick starts:</span><span class="sxs-lookup"><span data-stu-id="f170f-105">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="f170f-106">Create DB - Portal</span><span class="sxs-lookup"><span data-stu-id="f170f-106">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="f170f-107">Create DB - CLI</span><span class="sxs-lookup"><span data-stu-id="f170f-107">Create DB - CLI</span></span>](sql-database-get-started-cli.md)

## <a name="install-php-and-database-communications-software"></a><span data-ttu-id="f170f-108">Install PHP and database communications software</span><span class="sxs-lookup"><span data-stu-id="f170f-108">Install PHP and database communications software</span></span>

<span data-ttu-id="f170f-109">The steps in this section assume that you are familar with developing using PHP and are new to working with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f170f-109">The steps in this section assume that you are familar with developing using PHP and are new to working with Azure SQL Database.</span></span> <span data-ttu-id="f170f-110">If you are new to developing with PHP, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **PHP** and then select your operating system.</span><span class="sxs-lookup"><span data-stu-id="f170f-110">If you are new to developing with PHP, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **PHP** and then select your operating system.</span></span>

### <a name="mac-os"></a><span data-ttu-id="f170f-111">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="f170f-111">**Mac OS**</span></span>
<span data-ttu-id="f170f-112">Open your terminal and enter the following commands to install **brew**, **Microsoft ODBC Driver for Mac** and the **Microsoft PHP Drivers for SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f170f-112">Open your terminal and enter the following commands to install **brew**, **Microsoft ODBC Driver for Mac** and the **Microsoft PHP Drivers for SQL Server**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/msodbcsql https://github.com/Microsoft/homebrew-msodbcsql-preview
brew update
brew install msodbcsql 
#for silent install ACCEPT_EULA=y brew install msodbcsql 
pecl install sqlsrv-4.1.7preview
pecl install pdo_sqlsrv-4.1.7preview
```

### <a name="linux-ubuntu"></a><span data-ttu-id="f170f-113">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="f170f-113">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="f170f-114">Enter the following commands to install the **Microsoft ODBC Driver for Linux** and the **Microsoft PHP Drivers for SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f170f-114">Enter the following commands to install the **Microsoft ODBC Driver for Linux** and the **Microsoft PHP Drivers for SQL Server**.</span></span>

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql.list
exit
sudo apt-get update
sudo apt-get install msodbcsql mssql-tools unixodbc-dev gcc g++ php-dev
sudo pecl install sqlsrv pdo_sqlsrv
sudo echo "extension= pdo_sqlsrv.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
sudo echo "extension= sqlsrv.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
```

### <a name="windows"></a><span data-ttu-id="f170f-115">**Windows**</span><span class="sxs-lookup"><span data-stu-id="f170f-115">**Windows**</span></span>
- <span data-ttu-id="f170f-116">Install PHP 7.1.1 (x64) [from WebPlatform Installer](https://www.microsoft.com/web/downloads/platform.aspx?lang=)</span><span class="sxs-lookup"><span data-stu-id="f170f-116">Install PHP 7.1.1 (x64) [from WebPlatform Installer](https://www.microsoft.com/web/downloads/platform.aspx?lang=)</span></span> 
- <span data-ttu-id="f170f-117">Install the [Microsoft ODBC Driver 13.1](https://www.microsoft.com/download/details.aspx?id=53339).</span><span class="sxs-lookup"><span data-stu-id="f170f-117">Install the [Microsoft ODBC Driver 13.1](https://www.microsoft.com/download/details.aspx?id=53339).</span></span> 
- <span data-ttu-id="f170f-118">Download the non-thread safe dll's for the [Microsoft PHP Driver for SQL Server](https://pecl.php.net/package/sqlsrv/4.1.6.1/windows) and place the binaries in the PHP\v7.x\ext folder.</span><span class="sxs-lookup"><span data-stu-id="f170f-118">Download the non-thread safe dll's for the [Microsoft PHP Driver for SQL Server](https://pecl.php.net/package/sqlsrv/4.1.6.1/windows) and place the binaries in the PHP\v7.x\ext folder.</span></span>
- <span data-ttu-id="f170f-119">Next edit your php.ini (C:\Program Files\PHP\v7.1\php.ini) file by adding the reference to the dll.</span><span class="sxs-lookup"><span data-stu-id="f170f-119">Next edit your php.ini (C:\Program Files\PHP\v7.1\php.ini) file by adding the reference to the dll.</span></span> <span data-ttu-id="f170f-120">For example:</span><span class="sxs-lookup"><span data-stu-id="f170f-120">For example:</span></span>
      
      extension=php_sqlsrv.dll
      extension=php_pdo_sqlsrv.dll

<span data-ttu-id="f170f-121">At this point you should have the dll's registered with PHP.</span><span class="sxs-lookup"><span data-stu-id="f170f-121">At this point you should have the dll's registered with PHP.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="f170f-122">Get connection information</span><span class="sxs-lookup"><span data-stu-id="f170f-122">Get connection information</span></span>

<span data-ttu-id="f170f-123">Get the connection information needed to connect to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f170f-123">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="f170f-124">You will need the fully qualified server name, database name, and login information in the next procedures.</span><span class="sxs-lookup"><span data-stu-id="f170f-124">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="f170f-125">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f170f-125">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f170f-126">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="f170f-126">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="f170f-127">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="f170f-127">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span></span> <span data-ttu-id="f170f-128">You can hover over the server name to bring up the **Click to copy** option.</span><span class="sxs-lookup"><span data-stu-id="f170f-128">You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="f170f-130">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span><span class="sxs-lookup"><span data-stu-id="f170f-130">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
    
## <a name="select-data"></a><span data-ttu-id="f170f-131">Select data</span><span class="sxs-lookup"><span data-stu-id="f170f-131">Select data</span></span>
<span data-ttu-id="f170f-132">Use the following code to query for the top 20 products by category using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="f170f-132">Use the following code to query for the top 20 products by category using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="f170f-133">The sqlsrv_query function is used to retrieve a result set from a query against a SQL database.</span><span class="sxs-lookup"><span data-stu-id="f170f-133">The sqlsrv_query function is used to retrieve a result set from a query against a SQL database.</span></span> <span data-ttu-id="f170f-134">This function accepts a query and returns a result set that can be iterated over with the use of [sqlsrv_fetch_array()](http://php.net/manual/en/function.sqlsrv-fetch-array.php).</span><span class="sxs-lookup"><span data-stu-id="f170f-134">This function accepts a query and returns a result set that can be iterated over with the use of [sqlsrv_fetch_array()](http://php.net/manual/en/function.sqlsrv-fetch-array.php).</span></span> <span data-ttu-id="f170f-135">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="f170f-135">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span> 

```PHP
<?php
$serverName = "your_server.database.windows.net";
$connectionOptions = array(
    "Database" => "your_database",
    "Uid" => "your_username",
    "PWD" => "your_password"
);
//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
$tsql= "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
     FROM [SalesLT].[ProductCategory] pc
     JOIN [SalesLT].[Product] p
     ON pc.productcategoryid = p.productcategoryid";
$getResults= sqlsrv_query($conn, $tsql);
echo ("Reading data from table" . PHP_EOL);
if ($getResults == FALSE)
    echo (sqlsrv_errors());
while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['CategoryName'] . " " . $row['ProductName'] . PHP_EOL);
}
sqlsrv_free_stmt($getResults);
?>
```


## <a name="insert-data"></a><span data-ttu-id="f170f-136">Insert data</span><span class="sxs-lookup"><span data-stu-id="f170f-136">Insert data</span></span>
<span data-ttu-id="f170f-137">Use the following code to insert a new product into the SalesLT.Product table using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="f170f-137">Use the following code to insert a new product into the SalesLT.Product table using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="f170f-138">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="f170f-138">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span> 

```PHP
<?php
$serverName = "your_server.database.windows.net";
$connectionOptions = array(
    "Database" => "your_database",
    "Uid" => "your_username",
    "PWD" => "your_password"
);
//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
$tsql= "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";
$params = array("BrandNewProduct", "200989", "Blue", 75, 80, "7/1/2016");
$getResults= sqlsrv_query($conn, $tsql, $params);
if ($getResults == FALSE)
    echo print_r(sqlsrv_errors(), true);
else{
    $rowsAffected = sqlsrv_rows_affected($getResults);
    echo ($rowsAffected. " row(s) inserted" . PHP_EOL);
    sqlsrv_free_stmt($getResults);
}
?>
```

## <a name="update-data"></a><span data-ttu-id="f170f-139">Update data</span><span class="sxs-lookup"><span data-stu-id="f170f-139">Update data</span></span>
<span data-ttu-id="f170f-140">Use the following code to update data in your Azure SQL database using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="f170f-140">Use the following code to update data in your Azure SQL database using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="f170f-141">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="f170f-141">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```PHP
<?php
$serverName = "your_server.database.windows.net";
$connectionOptions = array(
    "Database" => "your_database",
    "Uid" => "your_username",
    "PWD" => "your_password"
);
//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
$tsql= "UPDATE SalesLT.Product SET ListPrice =? WHERE Name = ?";
$params = array(50,"BrandNewProduct");
$getResults= sqlsrv_query($conn, $tsql, $params);
if ($getResults == FALSE)
    echo print_r(sqlsrv_errors(), true);
else{
    $rowsAffected = sqlsrv_rows_affected($getResults);
    echo ($rowsAffected. " row(s) updated" . PHP_EOL);
    sqlsrv_free_stmt($getResults);
}
?>
```

## <a name="delete-data"></a><span data-ttu-id="f170f-142">Delete data</span><span class="sxs-lookup"><span data-stu-id="f170f-142">Delete data</span></span>
<span data-ttu-id="f170f-143">Use the following code to delete the new product that you previously added using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="f170f-143">Use the following code to delete the new product that you previously added using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="f170f-144">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="f170f-144">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```PHP
<?php
$serverName = "your_server.database.windows.net";
$connectionOptions = array(
    "Database" => "your_database",
    "Uid" => "your_username",
    "PWD" => "your_password"
);
//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
$tsql= "DELETE FROM SalesLT.Product WHERE Name = ?";
$params = array("BrandNewProduct");
$getResults= sqlsrv_query($conn, $tsql, $params);
if ($getResults == FALSE)
    echo print_r(sqlsrv_errors(), true);
else{
    $rowsAffected = sqlsrv_rows_affected($getResults);
    echo ($rowsAffected. " row(s) deleted" . PHP_EOL);
    sqlsrv_free_stmt($getResults);
}
```

## <a name="next-steps"></a><span data-ttu-id="f170f-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="f170f-145">Next steps</span></span>

- <span data-ttu-id="f170f-146">More information on the [Microsoft PHP Driver for SQL Server](https://github.com/Microsoft/msphpsql/).</span><span class="sxs-lookup"><span data-stu-id="f170f-146">More information on the [Microsoft PHP Driver for SQL Server](https://github.com/Microsoft/msphpsql/).</span></span>
- <span data-ttu-id="f170f-147">[File issues/ask questions](https://github.com/Microsoft/msphpsql/issues).</span><span class="sxs-lookup"><span data-stu-id="f170f-147">[File issues/ask questions](https://github.com/Microsoft/msphpsql/issues).</span></span>
- <span data-ttu-id="f170f-148">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="f170f-148">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="f170f-149">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="f170f-149">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="f170f-150">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f170f-150">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="f170f-151">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f170f-151">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="f170f-152">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="f170f-152">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="f170f-153">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="f170f-153">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="f170f-154">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="f170f-154">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>

