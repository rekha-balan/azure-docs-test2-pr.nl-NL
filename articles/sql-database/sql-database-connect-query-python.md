---
title: Connect to Azure SQL Database by using Python | Microsoft Docs
description: Presents a Python code sample you can use to connect to and query Azure SQL Database.
services: sql-database
documentationcenter: ''
author: meet-bhagdev
manager: jhubbard
editor: ''
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: quick start connect
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 04/17/2017
ms.author: meetb;carlrab;sstein
ms.openlocfilehash: 0bfffa50c173c4c2ab4e64650fee74b2a460d0d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554396"
---
# <a name="azure-sql-database-use-python-to-connect-and-query-data"></a><span data-ttu-id="aa6e5-103">Azure SQL Database: Use Python to connect and query data</span><span class="sxs-lookup"><span data-stu-id="aa6e5-103">Azure SQL Database: Use Python to connect and query data</span></span>

 <span data-ttu-id="aa6e5-104">This quick start demonstrates how to use [Python](https://python.org) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-104">This quick start demonstrates how to use [Python](https://python.org) to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span>

<span data-ttu-id="aa6e5-105">This quick start uses as its starting point the resources created in one of these quick starts:</span><span class="sxs-lookup"><span data-stu-id="aa6e5-105">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="aa6e5-106">Create DB - Portal</span><span class="sxs-lookup"><span data-stu-id="aa6e5-106">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="aa6e5-107">Create DB - CLI</span><span class="sxs-lookup"><span data-stu-id="aa6e5-107">Create DB - CLI</span></span>](sql-database-get-started-cli.md)

## <a name="install-the-python-and-database-communication-libraries"></a><span data-ttu-id="aa6e5-108">Install the Python and database communication libraries</span><span class="sxs-lookup"><span data-stu-id="aa6e5-108">Install the Python and database communication libraries</span></span>

<span data-ttu-id="aa6e5-109">The steps in this section assume that you are familar with developing using Python and are new to working with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-109">The steps in this section assume that you are familar with developing using Python and are new to working with Azure SQL Database.</span></span> <span data-ttu-id="aa6e5-110">If you are new to developing with Python, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **Python** and then select your operating system.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-110">If you are new to developing with Python, go the [Build an app using SQL Server](https://www.microsoft.com/en-us/sql-server/developer-get-started/) and select **Python** and then select your operating system.</span></span>

### <a name="mac-os"></a><span data-ttu-id="aa6e5-111">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="aa6e5-111">**Mac OS**</span></span>
<span data-ttu-id="aa6e5-112">Open your terminal and navigate to a directory where you plan on creating your python script.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-112">Open your terminal and navigate to a directory where you plan on creating your python script.</span></span> <span data-ttu-id="aa6e5-113">Enter the following commands to install **brew**, **Microsoft ODBC Driver for Mac** and **pyodbc**.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-113">Enter the following commands to install **brew**, **Microsoft ODBC Driver for Mac** and **pyodbc**.</span></span> <span data-ttu-id="aa6e5-114">pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-114">pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span></span>

``` bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/msodbcsql https://github.com/Microsoft/homebrew-msodbcsql-preview
brew update
brew install msodbcsql 
#for silent install ACCEPT_EULA=y brew install msodbcsql
sudo pip install pyodbc==3.1.1
```

### <a name="linux-ubuntu"></a><span data-ttu-id="aa6e5-115">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="aa6e5-115">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="aa6e5-116">Open your terminal and navigate to a directory where you plan on creating your python script.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-116">Open your terminal and navigate to a directory where you plan on creating your python script.</span></span> <span data-ttu-id="aa6e5-117">Enter the following commands to install the **Microsoft ODBC Driver for Linux** and **pyodbc**.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-117">Enter the following commands to install the **Microsoft ODBC Driver for Linux** and **pyodbc**.</span></span> <span data-ttu-id="aa6e5-118">pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-118">pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span></span>

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql.list
exit
sudo apt-get update
sudo apt-get install msodbcsql mssql-tools unixodbc-dev
sudo pip install pyodbc==3.1.1
```

### <a name="windows"></a><span data-ttu-id="aa6e5-119">**Windows**</span><span class="sxs-lookup"><span data-stu-id="aa6e5-119">**Windows**</span></span>
<span data-ttu-id="aa6e5-120">Install the [Microsoft ODBC Driver 13.1](https://www.microsoft.com/download/details.aspx?id=53339) (upgrade the driver if prompted).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-120">Install the [Microsoft ODBC Driver 13.1](https://www.microsoft.com/download/details.aspx?id=53339) (upgrade the driver if prompted).</span></span> <span data-ttu-id="aa6e5-121">Pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-121">Pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span></span> 

<span data-ttu-id="aa6e5-122">Then install **pyodbc** using pip.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-122">Then install **pyodbc** using pip.</span></span>

```cmd
pip install pyodbc==3.1.1
```

<span data-ttu-id="aa6e5-123">Instructions to enable the use pip can be found [here](http://stackoverflow.com/questions/4750806/how-to-install-pip-on-windows)</span><span class="sxs-lookup"><span data-stu-id="aa6e5-123">Instructions to enable the use pip can be found [here](http://stackoverflow.com/questions/4750806/how-to-install-pip-on-windows)</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="aa6e5-124">Get connection information</span><span class="sxs-lookup"><span data-stu-id="aa6e5-124">Get connection information</span></span>

<span data-ttu-id="aa6e5-125">Get the connection information needed to connect to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-125">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="aa6e5-126">You will need the fully qualified server name, database name, and login information in the next procedures.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-126">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="aa6e5-127">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-127">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="aa6e5-128">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-128">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="aa6e5-129">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-129">On the **Overview** page for your database, review the fully qualified server name as shown in the image below.</span></span> <span data-ttu-id="aa6e5-130">You can hover over the server name to bring up the **Click to copy** option.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-130">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="aa6e5-132">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-132">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span>     
   
## <a name="select-data"></a><span data-ttu-id="aa6e5-133">Select Data</span><span class="sxs-lookup"><span data-stu-id="aa6e5-133">Select Data</span></span>

<span data-ttu-id="aa6e5-134">Use the following code to query for the top 20 products by category using the [pyodbc.connect]((https://github.com/mkleehammer/pyodbc/wiki)) function with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-134">Use the following code to query for the top 20 products by category using the [pyodbc.connect]((https://github.com/mkleehammer/pyodbc/wiki)) function with a [SELECT](https://docs.microsoft.com/sql/t-sql/queries/select-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="aa6e5-135">The [cursor.execute](https://mkleehammer.github.io/pyodbc/api-cursor.html) function is used to retrieve a result set from a query against SQL Database.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-135">The [cursor.execute](https://mkleehammer.github.io/pyodbc/api-cursor.html) function is used to retrieve a result set from a query against SQL Database.</span></span> <span data-ttu-id="aa6e5-136">This function accepts a query and returns a result set that can be iterated over with the use of [cursor.fetchone()](https://mkleehammer.github.io/pyodbc/api-cursor.html).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-136">This function accepts a query and returns a result set that can be iterated over with the use of [cursor.fetchone()](https://mkleehammer.github.io/pyodbc/api-cursor.html).</span></span> <span data-ttu-id="aa6e5-137">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-137">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print str(row[0]) + " " + str(row[1])
    row = cursor.fetchone()
```

## <a name="insert-data"></a><span data-ttu-id="aa6e5-138">Insert data</span><span class="sxs-lookup"><span data-stu-id="aa6e5-138">Insert data</span></span>
<span data-ttu-id="aa6e5-139">Use the following code to insert a new product into the SalesLT.Product table using the [cursor.execute](https://mkleehammer.github.io/pyodbc/api-cursor.html) function and the [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-139">Use the following code to insert a new product into the SalesLT.Product table using the [cursor.execute](https://mkleehammer.github.io/pyodbc/api-cursor.html) function and the [INSERT](https://docs.microsoft.com/sql/t-sql/statements/insert-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="aa6e5-140">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-140">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
with cursor.execute("INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('BrandNewProduct', '200989', 'Blue', 75, 80, '7/1/2016')"): 
    print ('Successfuly Inserted!')
cnxn.commit()
```

## <a name="update-data"></a><span data-ttu-id="aa6e5-141">Update data</span><span class="sxs-lookup"><span data-stu-id="aa6e5-141">Update data</span></span>
<span data-ttu-id="aa6e5-142">Use the following code to update the new product that you previously added using the [cursor.execute](https://mkleehammer.github.io/pyodbc/api-cursor.html) function and the [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-142">Use the following code to update the new product that you previously added using the [cursor.execute](https://mkleehammer.github.io/pyodbc/api-cursor.html) function and the [UPDATE](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="aa6e5-143">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-143">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
tsql = "UPDATE SalesLT.Product SET ListPrice = ? WHERE Name = ?"
with cursor.execute(tsql,50,'BrandNewProduct'):
    print ('Successfuly Updated!')
cnxn.commit()

```

## <a name="delete-data"></a><span data-ttu-id="aa6e5-144">Delete data</span><span class="sxs-lookup"><span data-stu-id="aa6e5-144">Delete data</span></span>
<span data-ttu-id="aa6e5-145">Use the following code to delete the new product that you previously added using the [cursor.execute](https://mkleehammer.github.io/pyodbc/api-cursor.html) function and the [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-145">Use the following code to delete the new product that you previously added using the [cursor.execute](https://mkleehammer.github.io/pyodbc/api-cursor.html) function and the [DELETE](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) Transact-SQL statement.</span></span> <span data-ttu-id="aa6e5-146">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span><span class="sxs-lookup"><span data-stu-id="aa6e5-146">Replace the server, database, username, and password parameters with the values that you specified when you created the database with the AdventureWorksLT sample data.</span></span>

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
tsql = "DELETE FROM SalesLT.Product WHERE Name = ?"
with cursor.execute(tsql,'BrandNewProduct'):
    print ('Successfuly Deleted!')
cnxn.commit()
```

## <a name="next-steps"></a><span data-ttu-id="aa6e5-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa6e5-147">Next steps</span></span>

- <span data-ttu-id="aa6e5-148">More information on the [Microsoft Python Driver for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-148">More information on the [Microsoft Python Driver for SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/).</span></span>
- <span data-ttu-id="aa6e5-149">Visit the [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-149">Visit the [Python Developer Center](/develop/python/).</span></span>
- <span data-ttu-id="aa6e5-150">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="aa6e5-150">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="aa6e5-151">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-151">To connect and query using Visual Studio, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="aa6e5-152">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-152">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="aa6e5-153">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-153">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="aa6e5-154">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-154">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="aa6e5-155">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-155">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="aa6e5-156">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="aa6e5-156">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>

