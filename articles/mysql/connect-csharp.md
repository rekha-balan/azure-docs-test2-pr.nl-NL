---
title: Connect to Azure Database for MySQL from C#
description: This quickstart provides a C# (.NET) code sample you can use to connect and query data from Azure Database for MySQL.
services: MySQL
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 02/28/2018
ms.openlocfilehash: c92d28bd7515372c17af34d90a4ac73317a13630
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865878"
---
# <a name="azure-database-for-mysql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="76f5a-103">Azure Database for MySQL: Use .NET (C#) to connect and query data</span><span class="sxs-lookup"><span data-stu-id="76f5a-103">Azure Database for MySQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="76f5a-104">This quickstart demonstrates how to connect to an Azure Database for MySQL by using a C# application.</span><span class="sxs-lookup"><span data-stu-id="76f5a-104">This quickstart demonstrates how to connect to an Azure Database for MySQL by using a C# application.</span></span> <span data-ttu-id="76f5a-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="76f5a-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="76f5a-106">This topic assumes that you are familiar with developing using C# and that you are new to working with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="76f5a-106">This topic assumes that you are familiar with developing using C# and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76f5a-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="76f5a-107">Prerequisites</span></span>
<span data-ttu-id="76f5a-108">This quickstart uses the resources created in either of these guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="76f5a-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="76f5a-109">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="76f5a-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="76f5a-110">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="76f5a-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="76f5a-111">You also need to:</span><span class="sxs-lookup"><span data-stu-id="76f5a-111">You also need to:</span></span>
- <span data-ttu-id="76f5a-112">Install [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="76f5a-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="76f5a-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span><span class="sxs-lookup"><span data-stu-id="76f5a-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="76f5a-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="76f5a-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>

## <a name="create-a-c-project"></a><span data-ttu-id="76f5a-115">Create a C# project</span><span class="sxs-lookup"><span data-stu-id="76f5a-115">Create a C# project</span></span>
<span data-ttu-id="76f5a-116">At a command prompt, run:</span><span class="sxs-lookup"><span data-stu-id="76f5a-116">At a command prompt, run:</span></span>

```
mkdir AzureMySqlExample
cd AzureMySqlExample
dotnet new console
dotnet add package MySqlConnector
```

## <a name="get-connection-information"></a><span data-ttu-id="76f5a-117">Get connection information</span><span class="sxs-lookup"><span data-stu-id="76f5a-117">Get connection information</span></span>
<span data-ttu-id="76f5a-118">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="76f5a-118">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="76f5a-119">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="76f5a-119">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="76f5a-120">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="76f5a-120">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="76f5a-121">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="76f5a-121">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>
3. <span data-ttu-id="76f5a-122">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="76f5a-122">Click the server name.</span></span>
4. <span data-ttu-id="76f5a-123">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="76f5a-123">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="76f5a-124">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="76f5a-124">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="76f5a-125">![Azure Database for MySQL server name](./media/connect-csharp/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="76f5a-125">![Azure Database for MySQL server name](./media/connect-csharp/1_server-overview-name-login.png)</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="76f5a-126">Connect, create table, and insert data</span><span class="sxs-lookup"><span data-stu-id="76f5a-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="76f5a-127">Use the following code to connect and load the data by using `CREATE TABLE` and  `INSERT INTO` SQL statements.</span><span class="sxs-lookup"><span data-stu-id="76f5a-127">Use the following code to connect and load the data by using `CREATE TABLE` and  `INSERT INTO` SQL statements.</span></span> <span data-ttu-id="76f5a-128">The code uses the `MySqlConnection` class with method [OpenAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.openasync#System_Data_Common_DbConnection_OpenAsync) to establish a connection to MySQL.</span><span class="sxs-lookup"><span data-stu-id="76f5a-128">The code uses the `MySqlConnection` class with method [OpenAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.openasync#System_Data_Common_DbConnection_OpenAsync) to establish a connection to MySQL.</span></span> <span data-ttu-id="76f5a-129">Then the code uses method [CreateCommand()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.createcommand), sets the CommandText property, and calls method [ExecuteNonQueryAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbcommand.executenonqueryasync) to run the database commands.</span><span class="sxs-lookup"><span data-stu-id="76f5a-129">Then the code uses method [CreateCommand()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.createcommand), sets the CommandText property, and calls method [ExecuteNonQueryAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbcommand.executenonqueryasync) to run the database commands.</span></span> 

<span data-ttu-id="76f5a-130">Replace the `Server`, `Database`, `UserID`, and `Password` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="76f5a-130">Replace the `Server`, `Database`, `UserID`, and `Password` parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Threading.Tasks;
using MySql.Data.MySqlClient;

namespace AzureMySqlExample
{
    class MySqlCreate
    {
        static async Task Main(string[] args)
        {
            var builder = new MySqlConnectionStringBuilder
            {
                Server = "YOUR-SERVER.mysql.database.azure.com",
                Database = "YOUR-DATABASE",
                UserID = "USER@YOUR-SERVER",
                Password = "PASSWORD",
                SslMode = MySqlSslMode.Required,
            };

            using (var conn = new MySqlConnection(builder.ConnectionString))
            {
                Console.WriteLine("Opening connection");
                await conn.OpenAsync();

                using (var command = conn.CreateCommand())
                {
                    command.CommandText = "DROP TABLE IF EXISTS inventory;";
                    await command.ExecuteNonQueryAsync();
                    Console.WriteLine("Finished dropping table (if existed)");

                    command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
                    await command.ExecuteNonQueryAsync();
                    Console.WriteLine("Finished creating table");

                    command.CommandText = @"INSERT INTO inventory (name, quantity) VALUES (@name1, @quantity1),
                        (@name2, @quantity2), (@name3, @quantity3);";
                    command.Parameters.AddWithValue("@name1", "banana");
                    command.Parameters.AddWithValue("@quantity1", 150);
                    command.Parameters.AddWithValue("@name2", "orange");
                    command.Parameters.AddWithValue("@quantity2", 154);
                    command.Parameters.AddWithValue("@name3", "apple");
                    command.Parameters.AddWithValue("@quantity3", 100);

                    int rowCount = await command.ExecuteNonQueryAsync();
                    Console.WriteLine(String.Format("Number of rows inserted={0}", rowCount));
                }

                // connection will be closed by the 'using' block
                Console.WriteLine("Closing connection");
            }

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="76f5a-131">Read data</span><span class="sxs-lookup"><span data-stu-id="76f5a-131">Read data</span></span>

<span data-ttu-id="76f5a-132">Use the following code to connect and read the data by using a `SELECT` SQL statement.</span><span class="sxs-lookup"><span data-stu-id="76f5a-132">Use the following code to connect and read the data by using a `SELECT` SQL statement.</span></span> <span data-ttu-id="76f5a-133">The code uses the `MySqlConnection` class with method [OpenAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.openasync#System_Data_Common_DbConnection_OpenAsync) to establish a connection to MySQL.</span><span class="sxs-lookup"><span data-stu-id="76f5a-133">The code uses the `MySqlConnection` class with method [OpenAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.openasync#System_Data_Common_DbConnection_OpenAsync) to establish a connection to MySQL.</span></span> <span data-ttu-id="76f5a-134">Then the code uses method [CreateCommand()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.createcommand) and method [ExecuteReaderAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbcommand.executereaderasync) to run the database commands.</span><span class="sxs-lookup"><span data-stu-id="76f5a-134">Then the code uses method [CreateCommand()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.createcommand) and method [ExecuteReaderAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbcommand.executereaderasync) to run the database commands.</span></span> <span data-ttu-id="76f5a-135">Next the code uses [ReadAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbdatareader.readasync#System_Data_Common_DbDataReader_ReadAsync) to advance to the records in the results.</span><span class="sxs-lookup"><span data-stu-id="76f5a-135">Next the code uses [ReadAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbdatareader.readasync#System_Data_Common_DbDataReader_ReadAsync) to advance to the records in the results.</span></span> <span data-ttu-id="76f5a-136">Then the code uses GetInt32 and GetString to parse the values in the record.</span><span class="sxs-lookup"><span data-stu-id="76f5a-136">Then the code uses GetInt32 and GetString to parse the values in the record.</span></span>

<span data-ttu-id="76f5a-137">Replace the `Server`, `Database`, `UserID`, and `Password` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="76f5a-137">Replace the `Server`, `Database`, `UserID`, and `Password` parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Threading.Tasks;
using MySql.Data.MySqlClient;

namespace AzureMySqlExample
{
    class MySqlRead
    {
        static async Task Main(string[] args)
        {
            var builder = new MySqlConnectionStringBuilder
            {
                Server = "YOUR-SERVER.mysql.database.azure.com",
                Database = "YOUR-DATABASE",
                UserID = "USER@YOUR-SERVER",
                Password = "PASSWORD",
                SslMode = MySqlSslMode.Required,
            };

            using (var conn = new MySqlConnection(builder.ConnectionString))
            {
                Console.WriteLine("Opening connection");
                await conn.OpenAsync();

                using (var command = conn.CreateCommand())
                {
                    command.CommandText = "SELECT * FROM inventory;";

                    using (var reader = await command.ExecuteReaderAsync())
                    {
                        while (await reader.ReadAsync())
                        {
                            Console.WriteLine(string.Format(
                                "Reading from table=({0}, {1}, {2})",
                                reader.GetInt32(0),
                                reader.GetString(1),
                                reader.GetInt32(2)));
                        }
                    }
                }

                Console.WriteLine("Closing connection");
            }

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="update-data"></a><span data-ttu-id="76f5a-138">Update data</span><span class="sxs-lookup"><span data-stu-id="76f5a-138">Update data</span></span>
<span data-ttu-id="76f5a-139">Use the following code to connect and read the data by using an `UPDATE` SQL statement.</span><span class="sxs-lookup"><span data-stu-id="76f5a-139">Use the following code to connect and read the data by using an `UPDATE` SQL statement.</span></span> <span data-ttu-id="76f5a-140">The code uses the `MySqlConnection` class with method [OpenAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.openasync#System_Data_Common_DbConnection_OpenAsync) to establish a connection to MySQL.</span><span class="sxs-lookup"><span data-stu-id="76f5a-140">The code uses the `MySqlConnection` class with method [OpenAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.openasync#System_Data_Common_DbConnection_OpenAsync) to establish a connection to MySQL.</span></span> <span data-ttu-id="76f5a-141">Then the code uses method [CreateCommand()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.createcommand), sets the CommandText property, and calls method [ExecuteNonQueryAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbcommand.executenonqueryasync) to run the database commands.</span><span class="sxs-lookup"><span data-stu-id="76f5a-141">Then the code uses method [CreateCommand()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.createcommand), sets the CommandText property, and calls method [ExecuteNonQueryAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbcommand.executenonqueryasync) to run the database commands.</span></span> 

<span data-ttu-id="76f5a-142">Replace the `Server`, `Database`, `UserID`, and `Password` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="76f5a-142">Replace the `Server`, `Database`, `UserID`, and `Password` parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Threading.Tasks;
using MySql.Data.MySqlClient;

namespace AzureMySqlExample
{
    class MySqlUpdate
    {
        static async Task Main(string[] args)
        {
            var builder = new MySqlConnectionStringBuilder
            {
                Server = "YOUR-SERVER.mysql.database.azure.com",
                Database = "YOUR-DATABASE",
                UserID = "USER@YOUR-SERVER",
                Password = "PASSWORD",
                SslMode = MySqlSslMode.Required,
            };

            using (var conn = new MySqlConnection(builder.ConnectionString))
            {
                Console.WriteLine("Opening connection");
                await conn.OpenAsync();

                using (var command = conn.CreateCommand())
                {
                    command.CommandText = "UPDATE inventory SET quantity = @quantity WHERE name = @name;";
                    command.Parameters.AddWithValue("@quantity", 200);
                    command.Parameters.AddWithValue("@name", "banana");

                    int rowCount = await command.ExecuteNonQueryAsync();
                    Console.WriteLine(String.Format("Number of rows updated={0}", rowCount));
                }

                Console.WriteLine("Closing connection");
            }

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="delete-data"></a><span data-ttu-id="76f5a-143">Delete data</span><span class="sxs-lookup"><span data-stu-id="76f5a-143">Delete data</span></span>
<span data-ttu-id="76f5a-144">Use the following code to connect and delete the data by using a `DELETE` SQL statement.</span><span class="sxs-lookup"><span data-stu-id="76f5a-144">Use the following code to connect and delete the data by using a `DELETE` SQL statement.</span></span> 

<span data-ttu-id="76f5a-145">The code uses the `MySqlConnection` class with method [OpenAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.openasync#System_Data_Common_DbConnection_OpenAsync) to establish a connection to MySQL.</span><span class="sxs-lookup"><span data-stu-id="76f5a-145">The code uses the `MySqlConnection` class with method [OpenAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.openasync#System_Data_Common_DbConnection_OpenAsync) to establish a connection to MySQL.</span></span> <span data-ttu-id="76f5a-146">Then the code uses method [CreateCommand()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.createcommand), sets the CommandText property, and calls method [ExecuteNonQueryAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbcommand.executenonqueryasync) to run the database commands.</span><span class="sxs-lookup"><span data-stu-id="76f5a-146">Then the code uses method [CreateCommand()](https://docs.microsoft.com/dotnet/api/system.data.common.dbconnection.createcommand), sets the CommandText property, and calls method [ExecuteNonQueryAsync()](https://docs.microsoft.com/dotnet/api/system.data.common.dbcommand.executenonqueryasync) to run the database commands.</span></span> 

<span data-ttu-id="76f5a-147">Replace the `Server`, `Database`, `UserID`, and `Password` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="76f5a-147">Replace the `Server`, `Database`, `UserID`, and `Password` parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Threading.Tasks;
using MySql.Data.MySqlClient;

namespace AzureMySqlExample
{
    class MySqlDelete
    {
        static async Task Main(string[] args)
        {
            var builder = new MySqlConnectionStringBuilder
            {
                Server = "YOUR-SERVER.mysql.database.azure.com",
                Database = "YOUR-DATABASE",
                UserID = "USER@YOUR-SERVER",
                Password = "PASSWORD",
                SslMode = MySqlSslMode.Required,
            };

            using (var conn = new MySqlConnection(builder.ConnectionString))
            {
                Console.WriteLine("Opening connection");
                await conn.OpenAsync();

                using (var command = conn.CreateCommand())
                {
                    command.CommandText = "DELETE FROM inventory WHERE name = @name;";
                    command.Parameters.AddWithValue("@name", "orange");

                    int rowCount = await command.ExecuteNonQueryAsync();
                    Console.WriteLine(String.Format("Number of rows deleted={0}", rowCount));
                }

                Console.WriteLine("Closing connection");
            }

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="76f5a-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="76f5a-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="76f5a-149">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span><span class="sxs-lookup"><span data-stu-id="76f5a-149">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
