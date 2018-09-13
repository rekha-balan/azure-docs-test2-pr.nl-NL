---
title: Use Java to query Azure SQL Database | Microsoft Docs
description: This topic shows you how to use Java to create a program that connects to an Azure SQL Database and query it using Transact-SQL statements.
services: sql-database
author: ajlam
manager: craigg
ms.service: sql-database
ms.custom: mvc,develop apps
ms.devlang: java
ms.topic: quickstart
ms.date: 04/01/2018
ms.author: andrela
ms.openlocfilehash: 8bd2ad5c4b0ab17bd6a37d9fefbd36d5e2a3cf4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44789547"
---
# <a name="use-java-to-query-an-azure-sql-database"></a><span data-ttu-id="325cc-103">Use Java to query an Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="325cc-103">Use Java to query an Azure SQL database</span></span>

<span data-ttu-id="325cc-104">This quickstart demonstrates how to use [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) to connect to an Azure SQL database and then use Transact-SQL statements to query data.</span><span class="sxs-lookup"><span data-stu-id="325cc-104">This quickstart demonstrates how to use [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) to connect to an Azure SQL database and then use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="325cc-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="325cc-105">Prerequisites</span></span>

<span data-ttu-id="325cc-106">To complete this quickstart, make sure you have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="325cc-106">To complete this quickstart, make sure you have the following prerequisites:</span></span>

[!INCLUDE [prerequisites-create-db](../../includes/sql-database-connect-query-prerequisites-create-db-includes.md)]

- <span data-ttu-id="325cc-107">A [server-level firewall rule](sql-database-get-started-portal-firewall.md) for the public IP address of the computer you use for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="325cc-107">A [server-level firewall rule](sql-database-get-started-portal-firewall.md) for the public IP address of the computer you use for this quickstart.</span></span>

- <span data-ttu-id="325cc-108">You have installed Java and related software for your operating system:</span><span class="sxs-lookup"><span data-stu-id="325cc-108">You have installed Java and related software for your operating system:</span></span>

    - <span data-ttu-id="325cc-109">**MacOS**: Install Homebrew and Java, and then install Maven.</span><span class="sxs-lookup"><span data-stu-id="325cc-109">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="325cc-110">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="325cc-110">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="325cc-111">**Ubuntu**:  Install the Java Development Kit, and install Maven.</span><span class="sxs-lookup"><span data-stu-id="325cc-111">**Ubuntu**:  Install the Java Development Kit, and install Maven.</span></span> <span data-ttu-id="325cc-112">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="325cc-112">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="325cc-113">**Windows**: Install the Java Development Kit, and Maven.</span><span class="sxs-lookup"><span data-stu-id="325cc-113">**Windows**: Install the Java Development Kit, and Maven.</span></span> <span data-ttu-id="325cc-114">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="325cc-114">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="325cc-115">SQL server connection information</span><span class="sxs-lookup"><span data-stu-id="325cc-115">SQL server connection information</span></span>

[!INCLUDE [prerequisites-server-connection-info](../../includes/sql-database-connect-query-prerequisites-server-connection-info-includes.md)]

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="325cc-116">**Create Maven project and dependencies**</span><span class="sxs-lookup"><span data-stu-id="325cc-116">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="325cc-117">From the terminal, create a new Maven project called **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="325cc-117">From the terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="325cc-118">Enter **Y** when prompted.</span><span class="sxs-lookup"><span data-stu-id="325cc-118">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="325cc-119">Change directory to **sqltest** and open ***pom.xml*** with your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="325cc-119">Change directory to **sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="325cc-120">Add the **Microsoft JDBC Driver for SQL Server** to your project's dependencies using the following code:</span><span class="sxs-lookup"><span data-stu-id="325cc-120">Add the **Microsoft JDBC Driver for SQL Server** to your project's dependencies using the following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.4.0.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="325cc-121">Also in ***pom.xml***, add the following properties to your project.</span><span class="sxs-lookup"><span data-stu-id="325cc-121">Also in ***pom.xml***, add the following properties to your project.</span></span>  <span data-ttu-id="325cc-122">If you don't have a properties section, you can add it after the dependencies.</span><span class="sxs-lookup"><span data-stu-id="325cc-122">If you don't have a properties section, you can add it after the dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="325cc-123">Save and close ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="325cc-123">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="325cc-124">Insert code to query SQL database</span><span class="sxs-lookup"><span data-stu-id="325cc-124">Insert code to query SQL database</span></span>

1. <span data-ttu-id="325cc-125">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span><span class="sxs-lookup"><span data-stu-id="325cc-125">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="325cc-126">Open the file and replace its contents with the following code and add the appropriate values for your server, database, user, and password.</span><span class="sxs-lookup"><span data-stu-id="325cc-126">Open the file and replace its contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
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
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-the-code"></a><span data-ttu-id="325cc-127">Run the code</span><span class="sxs-lookup"><span data-stu-id="325cc-127">Run the code</span></span>

1. <span data-ttu-id="325cc-128">At the command prompt, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="325cc-128">At the command prompt, run the following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="325cc-129">Verify that the top 20 rows are returned and then close the application window.</span><span class="sxs-lookup"><span data-stu-id="325cc-129">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="325cc-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="325cc-130">Next steps</span></span>
- [<span data-ttu-id="325cc-131">Design your first Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="325cc-131">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="325cc-132">Microsoft JDBC Driver for SQL Server</span><span class="sxs-lookup"><span data-stu-id="325cc-132">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="325cc-133">Report issues/ask questions</span><span class="sxs-lookup"><span data-stu-id="325cc-133">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

