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
# <a name="azure-sql-database-use-php-to-connect-and-query-data"></a>Azure SQL Database: Use PHP to connect and query data

This quick start demonstrates how to use [PHP](http://php.net/manual/en/intro-whatis.php) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.

This quick start uses as its starting point the resources created in one of these quick starts:

- [Create DB - Portal](sql-database-get-started-portal.md)
- [Create DB - CLI](sql-database-get-started-cli.md)

## <a name="install-php-and-database-communications-software"></a>Install PHP and database communications software

The steps in this section assume that you are familar with developing using PHP and are new to working with Azure SQL Database. If you are new to developing with PHP, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **PHP** and then select your operating system.

### <a name="mac-os"></a>**Mac OS**
Open your terminal and enter the following commands to install **brew**, **Microsoft ODBC Driver for Mac** and the **Microsoft PHP Drivers for SQL Server**. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/msodbcsql https://github.com/Microsoft/homebrew-msodbcsql-preview
brew update
brew install msodbcsql 
#for silent install ACCEPT_EULA=y brew install msodbcsql 
pecl install sqlsrv-4.1.7preview
pecl install pdo_sqlsrv-4.1.7preview
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Enter the following commands to install the **Microsoft ODBC Driver for Linux** and the **Microsoft PHP Drivers for SQL Server**.

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

### <a name="windows"></a>**Windows**
- Install PHP 7.1.1 (x64) [from WebPlatform Installer](https://www.microsoft.com/web/downloads/platform.aspx?lang=) 
- Install the [Microsoft ODBC Driver 13.1](https://www.microsoft.com/download/details.aspx?id=53339). 
- Download the non-thread safe dll's for the [Microsoft PHP Driver for SQL Server](https://pecl.php.net/package/sqlsrv/4.1.6.1/windows) and place the binaries in the PHP\v7.x\ext folder.
- Next edit your php.ini (C:\Program Files\PHP\v7.1\php.ini) file by adding the reference to the dll. For example:
      
      extension=php_sqlsrv.dll
      extension=php_pdo_sqlsrv.dll

At this point you should have the dll's registered with PHP.

## <a name="get-connection-information"></a>Get connection information

Get the connection information needed to connect to the Azure SQL database. You will need the fully qualified server name, database name, and login information in the next procedures.

1. Log in to the [Azure portal](https://portal.azure.com/).
2. Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page. 
3. On the **Overview** page for your database, review the fully qualified server name as shown in the image below. You can hover over the server name to bring up the **Click to copy** option.  

   ![server-name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-dotnet/server-name.png) 

4. If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.     
    
## <a name="select-data"></a>Select data
Use the following code to query for the top 20 products by category using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement. The sqlsrv_query function is used to retrieve a result set from a query against a SQL database. This function accepts a query and returns a result set that can be iterated over with the use of [sqlsrv_fetch_array()](http://php.net/manual/en/function.sqlsrv-fetch-array.php). Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data. 

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


## <a name="insert-data"></a>Insert data
Use the following code to insert a new product into the SalesLT.Product table using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement. Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data. 

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

## <a name="update-data"></a>Update data
Use the following code to update data in your Azure SQL database using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement. Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.

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

## <a name="delete-data"></a>Delete data
Use the following code to delete the new product that you previously added using the [sqlsrv_query()](https://docs.microsoft.com/sql/connect/php/sqlsrv-query) function and the [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement. Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.

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

## <a name="next-steps"></a>Next steps

- More information on the [Microsoft PHP Driver for SQL Server](https://github.com/Microsoft/msphpsql/).
- [File issues/ask questions](https://github.com/Microsoft/msphpsql/issues).
- To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)
- To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).
- To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).
- To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).
- To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).
- To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).
- To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).

