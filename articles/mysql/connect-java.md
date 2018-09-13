---
title: Connect to Azure Database for MySQL using Java
description: This quickstart provides a Java code sample you can use to connect and query data from a Azure Database for MySQL database.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc, devcenter
ms.topic: quickstart
ms.devlang: java
ms.date: 02/28/2018
ms.openlocfilehash: d22eb6c6b56e24c2699bed8ac0a71a8192f0804e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865615"
---
# <a name="azure-database-for-mysql-use-java-to-connect-and-query-data"></a><span data-ttu-id="32c85-103">Azure Database for MySQL: Use Java to connect and query data</span><span class="sxs-lookup"><span data-stu-id="32c85-103">Azure Database for MySQL: Use Java to connect and query data</span></span>
<span data-ttu-id="32c85-104">This quickstart demonstrates how to connect to an Azure Database for MySQL by using a Java application and the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/).</span><span class="sxs-lookup"><span data-stu-id="32c85-104">This quickstart demonstrates how to connect to an Azure Database for MySQL by using a Java application and the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/).</span></span> <span data-ttu-id="32c85-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="32c85-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="32c85-106">This article assumes that you are familiar with developing using Java and that you are new to working with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="32c85-106">This article assumes that you are familiar with developing using Java and that you are new to working with Azure Database for MySQL.</span></span>

<span data-ttu-id="32c85-107">There are numerous other examples and sample code at the [MySQL Connector examples page](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-examples.html).</span><span class="sxs-lookup"><span data-stu-id="32c85-107">There are numerous other examples and sample code at the [MySQL Connector examples page](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-examples.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32c85-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="32c85-108">Prerequisites</span></span>
1. <span data-ttu-id="32c85-109">This quickstart uses the resources created in either of these guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="32c85-109">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
   - [<span data-ttu-id="32c85-110">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="32c85-110">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
   - [<span data-ttu-id="32c85-111">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="32c85-111">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

2. <span data-ttu-id="32c85-112">Ensure your Azure Database for MySQL connection security is configured with the firewall opened and SSL settings adjusted for your application to connect successfully.</span><span class="sxs-lookup"><span data-stu-id="32c85-112">Ensure your Azure Database for MySQL connection security is configured with the firewall opened and SSL settings adjusted for your application to connect successfully.</span></span>

3. <span data-ttu-id="32c85-113">Obtain the MySQL Connector/J connector using one of the following approaches:</span><span class="sxs-lookup"><span data-stu-id="32c85-113">Obtain the MySQL Connector/J connector using one of the following approaches:</span></span>
   - <span data-ttu-id="32c85-114">Use the Maven package [mysql-connector-java](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22mysql%22%20AND%20a%3A%22mysql-connector-java%22) to include the [mysql dependency](https://mvnrepository.com/artifact/mysql/mysql-connector-java/5.1.6) in the POM file for your project.</span><span class="sxs-lookup"><span data-stu-id="32c85-114">Use the Maven package [mysql-connector-java](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22mysql%22%20AND%20a%3A%22mysql-connector-java%22) to include the [mysql dependency](https://mvnrepository.com/artifact/mysql/mysql-connector-java/5.1.6) in the POM file for your project.</span></span>
   - <span data-ttu-id="32c85-115">Download the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/) and include the JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span><span class="sxs-lookup"><span data-stu-id="32c85-115">Download the JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/) and include the JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="32c85-116">If you have trouble with classpaths, consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="32c85-116">If you have trouble with classpaths, consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="32c85-117">Get connection information</span><span class="sxs-lookup"><span data-stu-id="32c85-117">Get connection information</span></span>
<span data-ttu-id="32c85-118">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="32c85-118">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="32c85-119">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="32c85-119">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="32c85-120">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="32c85-120">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="32c85-121">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="32c85-121">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>
3. <span data-ttu-id="32c85-122">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="32c85-122">Click the server name.</span></span>
4. <span data-ttu-id="32c85-123">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="32c85-123">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="32c85-124">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="32c85-124">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="32c85-125">![Azure Database for MySQL server name](./media/connect-java/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="32c85-125">![Azure Database for MySQL server name](./media/connect-java/1_server-overview-name-login.png)</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="32c85-126">Connect, create table, and insert data</span><span class="sxs-lookup"><span data-stu-id="32c85-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="32c85-127">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="32c85-127">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="32c85-128">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span><span class="sxs-lookup"><span data-stu-id="32c85-128">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="32c85-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used to drop and create the table.</span><span class="sxs-lookup"><span data-stu-id="32c85-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used to drop and create the table.</span></span> <span data-ttu-id="32c85-130">The prepareStatement object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span><span class="sxs-lookup"><span data-stu-id="32c85-130">The prepareStatement object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="32c85-131">Method executeUpdate() runs the command for each set of parameters to insert the values.</span><span class="sxs-lookup"><span data-stu-id="32c85-131">Method executeUpdate() runs the command for each set of parameters to insert the values.</span></span> 

<span data-ttu-id="32c85-132">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span><span class="sxs-lookup"><span data-stu-id="32c85-132">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "mydemoserver.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@mydemoserver";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
                
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="read-data"></a><span data-ttu-id="32c85-133">Read data</span><span class="sxs-lookup"><span data-stu-id="32c85-133">Read data</span></span>
<span data-ttu-id="32c85-134">Use the following code to read the data with a **SELECT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="32c85-134">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="32c85-135">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span><span class="sxs-lookup"><span data-stu-id="32c85-135">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="32c85-136">The methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used to connect and run the select statement.</span><span class="sxs-lookup"><span data-stu-id="32c85-136">The methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used to connect and run the select statement.</span></span> <span data-ttu-id="32c85-137">The results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span><span class="sxs-lookup"><span data-stu-id="32c85-137">The results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="32c85-138">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span><span class="sxs-lookup"><span data-stu-id="32c85-138">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "mydemoserver.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@mydemoserver";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="32c85-139">Update data</span><span class="sxs-lookup"><span data-stu-id="32c85-139">Update data</span></span>
<span data-ttu-id="32c85-140">Use the following code to change the data with an **UPDATE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="32c85-140">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="32c85-141">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span><span class="sxs-lookup"><span data-stu-id="32c85-141">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span> <span data-ttu-id="32c85-142">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span><span class="sxs-lookup"><span data-stu-id="32c85-142">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="32c85-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span><span class="sxs-lookup"><span data-stu-id="32c85-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "mydemoserver.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@mydemoserver";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="delete-data"></a><span data-ttu-id="32c85-144">Delete data</span><span class="sxs-lookup"><span data-stu-id="32c85-144">Delete data</span></span>
<span data-ttu-id="32c85-145">Use the following code to remove data with a **DELETE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="32c85-145">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="32c85-146">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span><span class="sxs-lookup"><span data-stu-id="32c85-146">The [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used to connect to MySQL.</span></span>  <span data-ttu-id="32c85-147">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span><span class="sxs-lookup"><span data-stu-id="32c85-147">The methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used to prepare and run the update statement.</span></span> 

<span data-ttu-id="32c85-148">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span><span class="sxs-lookup"><span data-stu-id="32c85-148">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "mydemoserver.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@mydemoserver";
        String password = "<server_admin_password>";
        
        // check that the driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="32c85-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="32c85-149">Next steps</span></span>
<span data-ttu-id="32c85-150">There are numerous other examples and sample code at the [MySQL Connector/J examples page](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-examples.html).</span><span class="sxs-lookup"><span data-stu-id="32c85-150">There are numerous other examples and sample code at the [MySQL Connector/J examples page](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-examples.html).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="32c85-151">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span><span class="sxs-lookup"><span data-stu-id="32c85-151">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
