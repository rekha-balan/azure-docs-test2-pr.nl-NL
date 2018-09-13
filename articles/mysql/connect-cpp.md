---
title: Connect to Azure Database for MySQL from C++
description: This quickstart provides a C++ code sample you can use to connect and query data from Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.devlang: C++
ms.topic: quickstart
ms.date: 04/12/2018
ms.openlocfilehash: 0c017907378376c01e4a4a98190f73a9452b9a3d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866887"
---
# <a name="azure-database-for-mysql-use-connectorc-to-connect-and-query-data"></a><span data-ttu-id="8019c-103">Azure Database for MySQL: Use Connector/C++ to connect and query data</span><span class="sxs-lookup"><span data-stu-id="8019c-103">Azure Database for MySQL: Use Connector/C++ to connect and query data</span></span>
<span data-ttu-id="8019c-104">This quickstart demonstrates how to connect to an Azure Database for MySQL by using a C++ application.</span><span class="sxs-lookup"><span data-stu-id="8019c-104">This quickstart demonstrates how to connect to an Azure Database for MySQL by using a C++ application.</span></span> <span data-ttu-id="8019c-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="8019c-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="8019c-106">This topic assumes that you are familiar with developing using C++ and that you are new to working with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="8019c-106">This topic assumes that you are familiar with developing using C++ and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8019c-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8019c-107">Prerequisites</span></span>
<span data-ttu-id="8019c-108">This quickstart uses the resources created in either of the following guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="8019c-108">This quickstart uses the resources created in either of the following guides as a starting point:</span></span>
- [<span data-ttu-id="8019c-109">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="8019c-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="8019c-110">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8019c-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="8019c-111">You also need to:</span><span class="sxs-lookup"><span data-stu-id="8019c-111">You also need to:</span></span>
- <span data-ttu-id="8019c-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="8019c-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="8019c-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="8019c-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="8019c-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="8019c-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="8019c-115">Install [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="8019c-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="8019c-116">Install Visual Studio and .NET</span><span class="sxs-lookup"><span data-stu-id="8019c-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="8019c-117">The steps in this section assume that you are familiar with developing using .NET.</span><span class="sxs-lookup"><span data-stu-id="8019c-117">The steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="8019c-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="8019c-118">**Windows**</span></span>
- <span data-ttu-id="8019c-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web and database applications, and cloud services.</span><span class="sxs-lookup"><span data-stu-id="8019c-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web and database applications, and cloud services.</span></span> <span data-ttu-id="8019c-120">You can install either the full .NET Framework or just .NET Core: the code snippets in the Quickstart work with either.</span><span class="sxs-lookup"><span data-stu-id="8019c-120">You can install either the full .NET Framework or just .NET Core: the code snippets in the Quickstart work with either.</span></span> <span data-ttu-id="8019c-121">If you already have Visual Studio installed on your computer, skip the next two steps.</span><span class="sxs-lookup"><span data-stu-id="8019c-121">If you already have Visual Studio installed on your computer, skip the next two steps.</span></span>
   1. <span data-ttu-id="8019c-122">Download the [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="8019c-122">Download the [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   2. <span data-ttu-id="8019c-123">Run the installer and follow the installation prompts to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="8019c-123">Run the installer and follow the installation prompts to complete the installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="8019c-124">**Configure Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="8019c-124">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="8019c-125">From Visual Studio, Project -> Properties -> Linker -> General > Additional Library Directories, add the "\lib\opt" directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of the C++ connector.</span><span class="sxs-lookup"><span data-stu-id="8019c-125">From Visual Studio, Project -> Properties -> Linker -> General > Additional Library Directories, add the "\lib\opt" directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of the C++ connector.</span></span>
2. <span data-ttu-id="8019c-126">From Visual Studio, Project -> Properties -> C/C++ -> General -> Additional Include Directories:</span><span class="sxs-lookup"><span data-stu-id="8019c-126">From Visual Studio, Project -> Properties -> C/C++ -> General -> Additional Include Directories:</span></span>
   - <span data-ttu-id="8019c-127">Add the "\include" directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\).</span><span class="sxs-lookup"><span data-stu-id="8019c-127">Add the "\include" directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\).</span></span>
   - <span data-ttu-id="8019c-128">Add the Boost library's root directory (i.e.: C:\boost_1_64_0\).</span><span class="sxs-lookup"><span data-stu-id="8019c-128">Add the Boost library's root directory (i.e.: C:\boost_1_64_0\).</span></span>
3. <span data-ttu-id="8019c-129">From Visual Studio, Project -> Properties -> Linker -> Input > Additional Dependencies, add **mysqlcppconn.lib** into the text field.</span><span class="sxs-lookup"><span data-stu-id="8019c-129">From Visual Studio, Project -> Properties -> Linker -> Input > Additional Dependencies, add **mysqlcppconn.lib** into the text field.</span></span>
4. <span data-ttu-id="8019c-130">Either copy **mysqlcppconn.dll** from the C++ connector library folder in step 3 to the same directory as the application executable or add it to the environment variable so your application can find it.</span><span class="sxs-lookup"><span data-stu-id="8019c-130">Either copy **mysqlcppconn.dll** from the C++ connector library folder in step 3 to the same directory as the application executable or add it to the environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="8019c-131">Get connection information</span><span class="sxs-lookup"><span data-stu-id="8019c-131">Get connection information</span></span>
<span data-ttu-id="8019c-132">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="8019c-132">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="8019c-133">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="8019c-133">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="8019c-134">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8019c-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8019c-135">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="8019c-135">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>
3. <span data-ttu-id="8019c-136">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="8019c-136">Click the server name.</span></span>
4. <span data-ttu-id="8019c-137">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="8019c-137">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="8019c-138">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="8019c-138">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="8019c-139">![Azure Database for MySQL server name](./media/connect-cpp/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="8019c-139">![Azure Database for MySQL server name](./media/connect-cpp/1_server-overview-name-login.png)</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="8019c-140">Connect, create table, and insert data</span><span class="sxs-lookup"><span data-stu-id="8019c-140">Connect, create table, and insert data</span></span>
<span data-ttu-id="8019c-141">Use the following code to connect and load the data by using **CREATE TABLE** and **INSERT INTO** SQL statements.</span><span class="sxs-lookup"><span data-stu-id="8019c-141">Use the following code to connect and load the data by using **CREATE TABLE** and **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="8019c-142">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span><span class="sxs-lookup"><span data-stu-id="8019c-142">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="8019c-143">Then the code uses method createStatement() and execute() to run the database commands.</span><span class="sxs-lookup"><span data-stu-id="8019c-143">Then the code uses method createStatement() and execute() to run the database commands.</span></span> 

<span data-ttu-id="8019c-144">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="8019c-144">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

//for demonstration only. never save your password in the code!
const string server = "tcp://yourservername.mysql.database.azure.com:3306";
const string username = "username@servername";
const string password = "yourpassword";

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        con = driver->connect(server, username, password);
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to server. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    //please create database "quickstartdb" ahead of time
    con->setSchema("quickstartdb");

    stmt = con->createStatement();
    stmt->execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt->execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con->prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt->setString(1, "banana");
    pstmt->setInt(2, 150);
    pstmt->execute();
    cout << "One row inserted." << endl;

    pstmt->setString(1, "orange");
    pstmt->setInt(2, 154);
    pstmt->execute();
    cout << "One row inserted." << endl;

    pstmt->setString(1, "apple");
    pstmt->setInt(2, 100);
    pstmt->execute();
    cout << "One row inserted." << endl;

    delete pstmt;
    delete con;
    system("pause");
    return 0;
}
```

## <a name="read-data"></a><span data-ttu-id="8019c-145">Read data</span><span class="sxs-lookup"><span data-stu-id="8019c-145">Read data</span></span>

<span data-ttu-id="8019c-146">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="8019c-146">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span></span> <span data-ttu-id="8019c-147">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span><span class="sxs-lookup"><span data-stu-id="8019c-147">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="8019c-148">Then the code uses method prepareStatement() and executeQuery() to run the select commands.</span><span class="sxs-lookup"><span data-stu-id="8019c-148">Then the code uses method prepareStatement() and executeQuery() to run the select commands.</span></span> <span data-ttu-id="8019c-149">Next, the code uses next() to advance to the records in the results.</span><span class="sxs-lookup"><span data-stu-id="8019c-149">Next, the code uses next() to advance to the records in the results.</span></span> <span data-ttu-id="8019c-150">Finally, the code uses getInt() and getString() to parse the values in the record.</span><span class="sxs-lookup"><span data-stu-id="8019c-150">Finally, the code uses getInt() and getString() to parse the values in the record.</span></span>

<span data-ttu-id="8019c-151">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="8019c-151">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

//for demonstration only. never save your password in the code!
const string server = "tcp://yourservername.mysql.database.azure.com:3306";
const string username = "username@servername";
const string password = "yourpassword";

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver->connect(server, username, password);
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to server. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    con->setSchema("quickstartdb");

    //select  
    pstmt = con->prepareStatement("SELECT * FROM inventory;");
    result = pstmt->executeQuery();

    while (result->next())
        printf("Reading from table=(%d, %s, %d)\n", result->getInt(1), result->getString(2).c_str(), result->getInt(3));

    delete result;
    delete pstmt;
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="8019c-152">Update data</span><span class="sxs-lookup"><span data-stu-id="8019c-152">Update data</span></span>
<span data-ttu-id="8019c-153">Use the following code to connect and read the data by using an **UPDATE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="8019c-153">Use the following code to connect and read the data by using an **UPDATE** SQL statement.</span></span> <span data-ttu-id="8019c-154">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span><span class="sxs-lookup"><span data-stu-id="8019c-154">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="8019c-155">Then the code uses method prepareStatement() and executeQuery() to run the update commands.</span><span class="sxs-lookup"><span data-stu-id="8019c-155">Then the code uses method prepareStatement() and executeQuery() to run the update commands.</span></span> 

<span data-ttu-id="8019c-156">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="8019c-156">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

//for demonstration only. never save your password in the code!
const string server = "tcp://yourservername.mysql.database.azure.com:3306";
const string username = "username@servername";
const string password = "yourpassword";

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver->connect(server, username, password);
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to server. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
    
    con->setSchema("quickstartdb");

    //update
    pstmt = con->prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt->setInt(1, 200);
    pstmt->setString(2, "banana");
    pstmt->executeQuery();
    printf("Row updated\n");

    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="8019c-157">Delete data</span><span class="sxs-lookup"><span data-stu-id="8019c-157">Delete data</span></span>
<span data-ttu-id="8019c-158">Use the following code to connect and read the data by using a **DELETE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="8019c-158">Use the following code to connect and read the data by using a **DELETE** SQL statement.</span></span> <span data-ttu-id="8019c-159">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span><span class="sxs-lookup"><span data-stu-id="8019c-159">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="8019c-160">Then the code uses method prepareStatement() and executeQuery() to run the delete commands.</span><span class="sxs-lookup"><span data-stu-id="8019c-160">Then the code uses method prepareStatement() and executeQuery() to run the delete commands.</span></span>

<span data-ttu-id="8019c-161">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="8019c-161">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

//for demonstration only. never save your password in the code!
const string server = "tcp://yourservername.mysql.database.azure.com:3306";
const string username = "username@servername";
const string password = "yourpassword";

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver->connect(server, username, password);
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to server. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
    
    con->setSchema("quickstartdb");
        
    //delete
    pstmt = con->prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt->setString(1, "orange");
    result = pstmt->executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="8019c-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="8019c-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8019c-163">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span><span class="sxs-lookup"><span data-stu-id="8019c-163">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
