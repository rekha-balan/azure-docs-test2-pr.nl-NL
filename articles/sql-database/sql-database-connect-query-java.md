---
title: Connect to Azure SQL Database by using Java | Microsoft Docs
description: Presents a Java code sample you can use to connect to and query Azure SQL Database.
services: sql-database
documentationcenter: ''
author: ajlam
manager: jhubbard
editor: ''
ms.assetid: ''
ms.service: sql-database
ms.custom: quick start connect
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 04/17/2017
ms.author: andrela;carlrab;sstein
ms.openlocfilehash: d1335348d5a7def4447473af16b6740f5bb7d85c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564395"
---
# <a name="azure-sql-database-use-java-to-connect-and-query-data"></a><span data-ttu-id="97c38-103">Azure SQL Database: Use Java to connect and query data</span><span class="sxs-lookup"><span data-stu-id="97c38-103">Azure SQL Database: Use Java to connect and query data</span></span>

<span data-ttu-id="97c38-104">This quick start demonstrates how to use [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span><span class="sxs-lookup"><span data-stu-id="97c38-104">This quick start demonstrates how to use [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span>

<span data-ttu-id="97c38-105">This quick start uses as its starting point the resources created in one of these quick starts:</span><span class="sxs-lookup"><span data-stu-id="97c38-105">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="97c38-106">Create DB - Portal</span><span class="sxs-lookup"><span data-stu-id="97c38-106">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="97c38-107">Create DB - CLI</span><span class="sxs-lookup"><span data-stu-id="97c38-107">Create DB - CLI</span></span>](sql-database-get-started-cli.md)

## <a name="install-java-software"></a><span data-ttu-id="97c38-108">Install Java software</span><span class="sxs-lookup"><span data-stu-id="97c38-108">Install Java software</span></span>

<span data-ttu-id="97c38-109">The steps in this section assume that you are familar with developing using Java and are new to working with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="97c38-109">The steps in this section assume that you are familar with developing using Java and are new to working with Azure SQL Database.</span></span> <span data-ttu-id="97c38-110">If you are new to developing with Java, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **Java** and then select your operating system.</span><span class="sxs-lookup"><span data-stu-id="97c38-110">If you are new to developing with Java, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **Java** and then select your operating system.</span></span>

### <a name="mac-os"></a><span data-ttu-id="97c38-111">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="97c38-111">**Mac OS**</span></span>
<span data-ttu-id="97c38-112">Open your terminal and navigate to a directory where you plan on creating your Java project.</span><span class="sxs-lookup"><span data-stu-id="97c38-112">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="97c38-113">Enter the following commands to install **brew** and **Maven**.</span><span class="sxs-lookup"><span data-stu-id="97c38-113">Enter the following commands to install **brew** and **Maven**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

### <a name="linux-ubuntu"></a><span data-ttu-id="97c38-114">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="97c38-114">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="97c38-115">Open your terminal and navigate to a directory where you plan on creating your Java project.</span><span class="sxs-lookup"><span data-stu-id="97c38-115">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="97c38-116">Enter the following commands to install **Maven**.</span><span class="sxs-lookup"><span data-stu-id="97c38-116">Enter the following commands to install **Maven**.</span></span> 

```bash
sudo apt-get install maven
```

### <a name="windows"></a><span data-ttu-id="97c38-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="97c38-117">**Windows**</span></span>
<span data-ttu-id="97c38-118">Install [Maven](https://maven.apache.org/download.cgi) using the official installer.</span><span class="sxs-lookup"><span data-stu-id="97c38-118">Install [Maven](https://maven.apache.org/download.cgi) using the official installer.</span></span> <span data-ttu-id="97c38-119">Maven can be used to help manage dependencies, build, test and run your Java project.</span><span class="sxs-lookup"><span data-stu-id="97c38-119">Maven can be used to help manage dependencies, build, test and run your Java project.</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="97c38-120">Get connection information</span><span class="sxs-lookup"><span data-stu-id="97c38-120">Get connection information</span></span>

<span data-ttu-id="97c38-121">Get the connection information needed to connect to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="97c38-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="97c38-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span><span class="sxs-lookup"><span data-stu-id="97c38-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="97c38-123">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="97c38-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="97c38-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="97c38-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="97c38-125">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="97c38-125">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span></span> <span data-ttu-id="97c38-126">You can hover over the server name to bring up the **Click to copy** option.</span><span class="sxs-lookup"><span data-stu-id="97c38-126">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="97c38-128">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span><span class="sxs-lookup"><span data-stu-id="97c38-128">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>
5. <span data-ttu-id="97c38-129">Click **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="97c38-129">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="97c38-130">Review the complete **JDBC** connection string.</span><span class="sxs-lookup"><span data-stu-id="97c38-130">Review the complete **JDBC** connection string.</span></span>

    ![JDBC connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-jdbc/jdbc-connection-string.png)  

### <a name="create-maven-project"></a><span data-ttu-id="97c38-132">**Create Maven project**</span><span class="sxs-lookup"><span data-stu-id="97c38-132">**Create Maven project**</span></span>
<span data-ttu-id="97c38-133">From the terminal, create a new Maven project.</span><span class="sxs-lookup"><span data-stu-id="97c38-133">From the terminal, create a new Maven project.</span></span> 
```bash
mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
```

<span data-ttu-id="97c38-134">Add the **Microsoft JDBC Driver for SQL Server** to the dependencies in ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="97c38-134">Add the **Microsoft JDBC Driver for SQL Server** to the dependencies in ***pom.xml***.</span></span> 

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
</dependency>
```

## <a name="select-data"></a><span data-ttu-id="97c38-135">Select data</span><span class="sxs-lookup"><span data-stu-id="97c38-135">Select data</span></span>

<span data-ttu-id="97c38-136">Use the following code to query for the top 20 products by category using the [connection](https://docs.microsoft.com/sql/connect/jdbc/working-with-a-connection) class with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="97c38-136">Use the following code to query for the top 20 products by category using the [connection](https://docs.microsoft.com/sql/connect/jdbc/working-with-a-connection) class with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="97c38-137">Replace the hostHame, dbName, user, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="97c38-137">Replace the hostHame, dbName, user, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span> 

```java
package com.sqldbsamples;

import java.sql.Connection;
import java.sql.Statement;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.DriverManager;

public class App {

    public static void main(String[] args) {
    
        // Connect to database
        String hostName = "your_server.database.windows.net";
        String dbName = "your_database";
        String user = "your_username";
        String password = "your_password";
        String url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
        Connection connection = null;

        try {
                connection = DriverManager.getConnection(url);
                String schema = connection.getSchema();
                System.out.println("Successful connection - Schema: " + schema);

                System.out.println("Query data example:");
                System.out.println("=========================================");

                // Create and execute a SELECT SQL statement.
                String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                    + "FROM [SalesLT].[ProductCategory] pc "  
                    + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                try (Statement statement = connection.createStatement();
                    ResultSet resultSet = statement.executeQuery(selectSql)) {

                        // Print results from select statement
                        System.out.println("Top 20 categories:");
                        while (resultSet.next())
                        {
                            System.out.println(resultSet.getString(1) + " "
                                + resultSet.getString(2));
                        }
                }
        }
        catch (Exception e) {
                e.printStackTrace();
        }
    }
}
```

## <a name="insert-data"></a><span data-ttu-id="97c38-138">Insert data</span><span class="sxs-lookup"><span data-stu-id="97c38-138">Insert data</span></span>

<span data-ttu-id="97c38-139">Use the following code to insert a new product into the SalesLT.Product table using the [Prepared Statements](https://docs.microsoft.com/sql/connect/jdbc/using-statements-with-sql) class with an [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="97c38-139">Use the following code to insert a new product into the SalesLT.Product table using the [Prepared Statements](https://docs.microsoft.com/sql/connect/jdbc/using-statements-with-sql) class with an [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="97c38-140">Replace the hostHame, dbName, user, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="97c38-140">Replace the hostHame, dbName, user, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span> 

```java
package com.sqldbsamples;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.DriverManager;

public class App {

    public static void main(String[] args) {
    
        // Connect to database
        String hostName = "your_server.database.windows.net";
        String dbName = "your_database";
        String user = "your_username";
        String password = "your_password";
        String url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
        Connection connection = null;

        try {
                connection = DriverManager.getConnection(url);
                String schema = connection.getSchema();
                System.out.println("Successful connection - Schema: " + schema);

                System.out.println("Insert data example:");
                System.out.println("=========================================");

                // Prepared statement to insert data
                String insertSql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, " 
                    + " StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

                java.util.Date date = new java.util.Date();
                java.sql.Timestamp sqlTimeStamp = new java.sql.Timestamp(date.getTime());

                try (PreparedStatement prep = connection.prepareStatement(insertSql)) {
                        prep.setString(1, "BrandNewProduct");
                        prep.setInt(2, 200989);
                        prep.setString(3, "Blue");
                        prep.setDouble(4, 75);
                        prep.setDouble(5, 80);
                        prep.setTimestamp(6, sqlTimeStamp);

                        int count = prep.executeUpdate();
                        System.out.println("Inserted: " + count + " row(s)");
                }
        }
        catch (Exception e) {
                e.printStackTrace();
        }
    }
}
```
## <a name="update-data"></a><span data-ttu-id="97c38-141">Update data</span><span class="sxs-lookup"><span data-stu-id="97c38-141">Update data</span></span>

<span data-ttu-id="97c38-142">Use the following code to update the new product that you previously added using the [Prepared Statements](https://docs.microsoft.com/sql/connect/jdbc/using-statements-with-sql) class with an [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement to update data in your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="97c38-142">Use the following code to update the new product that you previously added using the [Prepared Statements](https://docs.microsoft.com/sql/connect/jdbc/using-statements-with-sql) class with an [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement to update data in your Azure SQL database.</span></span> <span data-ttu-id="97c38-143">Replace the hostHame, dbName, user, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="97c38-143">Replace the hostHame, dbName, user, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span> 

```java
package com.sqldbsamples;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.DriverManager;

public class App {

    public static void main(String[] args) {
    
        // Connect to database
        String hostName = "your_server.database.windows.net";
        String dbName = "your_database";
        String user = "your_username";
        String password = "your_password";
        String url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
        Connection connection = null;

        try {
                connection = DriverManager.getConnection(url);
                String schema = connection.getSchema();
                System.out.println("Successful connection - Schema: " + schema);

                System.out.println("Update data example:");
                System.out.println("=========================================");

                // Prepared statement to update data
                String updateSql = "UPDATE SalesLT.Product SET ListPrice = ? WHERE Name = ?";

                try (PreparedStatement prep = connection.prepareStatement(updateSql)) {
                        prep.setString(1, "500");
                        prep.setString(2, "BrandNewProduct");

                        int count = prep.executeUpdate();
                        System.out.println("Updated: " + count + " row(s)")
                }
        }
        catch (Exception e) {
                e.printStackTrace();
        }
    }
}
```



## <a name="delete-data"></a><span data-ttu-id="97c38-144">Delete data</span><span class="sxs-lookup"><span data-stu-id="97c38-144">Delete data</span></span>

<span data-ttu-id="97c38-145">Use the following code to delete the new product that you previously added using the [Prepared Statements](https://docs.microsoft.com/sql/connect/jdbc/using-statements-with-sql) with a [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement .</span><span class="sxs-lookup"><span data-stu-id="97c38-145">Use the following code to delete the new product that you previously added using the [Prepared Statements](https://docs.microsoft.com/sql/connect/jdbc/using-statements-with-sql) with a [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement .</span></span> <span data-ttu-id="97c38-146">Replace the hostHame, dbName, user, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="97c38-146">Replace the hostHame, dbName, user, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span> 

```java
package com.sqldbsamples;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.DriverManager;

public class App {

    public static void main(String[] args) {
    
        // Connect to database
        String hostName = "your_server.database.windows.net";
        String dbName = "your_database";
        String user = "your_username";
        String password = "your_password";
        String url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
        Connection connection = null;

        try {
                connection = DriverManager.getConnection(url);
                String schema = connection.getSchema();
                System.out.println("Successful connection - Schema: " + schema);

                System.out.println("Delete data example:");
                System.out.println("=========================================");

                // Prepared statement to delete data
                String deleteSql = "DELETE SalesLT.Product WHERE Name = ?";

                try (PreparedStatement prep = connection.prepareStatement(deleteSql)) {
                        prep.setString(1, "BrandNewProduct");

                        int count = prep.executeUpdate();
                        System.out.println("Deleted: " + count + " row(s)");
                }
        }       
        catch (Exception e) {
                e.printStackTrace();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="97c38-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="97c38-147">Next steps</span></span>

- <span data-ttu-id="97c38-148">GitHub repository for [Microsoft JDBC Driver for SQL Server](https://github.com/microsoft/mssql-jdbc).</span><span class="sxs-lookup"><span data-stu-id="97c38-148">GitHub repository for [Microsoft JDBC Driver for SQL Server](https://github.com/microsoft/mssql-jdbc).</span></span>
- <span data-ttu-id="97c38-149">[File issues/ask questions](https://github.com/microsoft/mssql-jdbc/issues).</span><span class="sxs-lookup"><span data-stu-id="97c38-149">[File issues/ask questions](https://github.com/microsoft/mssql-jdbc/issues).</span></span>
- <span data-ttu-id="97c38-150">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="97c38-150">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="97c38-151">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="97c38-151">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="97c38-152">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="97c38-152">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="97c38-153">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="97c38-153">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="97c38-154">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="97c38-154">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="97c38-155">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="97c38-155">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="97c38-156">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="97c38-156">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>



