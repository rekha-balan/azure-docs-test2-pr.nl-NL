---
title: Connect to Azure Database for MySQL from Python
description: This quickstart provides several Python code samples you can use to connect and query data from Azure Database for MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 02/28/2018
ms.openlocfilehash: 7eef3d71a35b5016e48e519b95c2573fbe3390e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867579"
---
# <a name="azure-database-for-mysql-use-python-to-connect-and-query-data"></a><span data-ttu-id="2d348-103">Azure Database for MySQL: Use Python to connect and query data</span><span class="sxs-lookup"><span data-stu-id="2d348-103">Azure Database for MySQL: Use Python to connect and query data</span></span>
<span data-ttu-id="2d348-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="2d348-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for MySQL.</span></span> <span data-ttu-id="2d348-105">It uses SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span><span class="sxs-lookup"><span data-stu-id="2d348-105">It uses SQL statements to query, insert, update, and delete data in the database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="2d348-106">This topic assumes that you are familiar with developing using Python and that you are new to working with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="2d348-106">This topic assumes that you are familiar with developing using Python and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d348-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d348-107">Prerequisites</span></span>
<span data-ttu-id="2d348-108">This quickstart uses the resources created in either of these guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="2d348-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2d348-109">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="2d348-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="2d348-110">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2d348-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-the-mysql-connector"></a><span data-ttu-id="2d348-111">Install Python and the MySQL connector</span><span class="sxs-lookup"><span data-stu-id="2d348-111">Install Python and the MySQL connector</span></span>
<span data-ttu-id="2d348-112">Install [Python](https://www.python.org/downloads/) and the [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span><span class="sxs-lookup"><span data-stu-id="2d348-112">Install [Python](https://www.python.org/downloads/) and the [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="2d348-113">Depending on your platform, follow the steps in the appropriate section:</span><span class="sxs-lookup"><span data-stu-id="2d348-113">Depending on your platform, follow the steps in the appropriate section:</span></span>

### <a name="windows"></a><span data-ttu-id="2d348-114">Windows</span><span class="sxs-lookup"><span data-stu-id="2d348-114">Windows</span></span>
1. <span data-ttu-id="2d348-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="2d348-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="2d348-116">Check the Python installation by launching the command prompt.</span><span class="sxs-lookup"><span data-stu-id="2d348-116">Check the Python installation by launching the command prompt.</span></span> <span data-ttu-id="2d348-117">Run the command `C:\python27\python.exe -V` using the uppercase V switch to see the version number.</span><span class="sxs-lookup"><span data-stu-id="2d348-117">Run the command `C:\python27\python.exe -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="2d348-118">Install the Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding to your version of Python.</span><span class="sxs-lookup"><span data-stu-id="2d348-118">Install the Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding to your version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="2d348-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="2d348-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="2d348-120">In Linux (Ubuntu), Python is typically installed as part of the default installation.</span><span class="sxs-lookup"><span data-stu-id="2d348-120">In Linux (Ubuntu), Python is typically installed as part of the default installation.</span></span>
2. <span data-ttu-id="2d348-121">Check the Python installation by launching the bash shell.</span><span class="sxs-lookup"><span data-stu-id="2d348-121">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="2d348-122">Run the command `python -V` using the uppercase V switch to see the version number.</span><span class="sxs-lookup"><span data-stu-id="2d348-122">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="2d348-123">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span><span class="sxs-lookup"><span data-stu-id="2d348-123">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span> 
4. <span data-ttu-id="2d348-124">PIP may be included in some versions of Python.</span><span class="sxs-lookup"><span data-stu-id="2d348-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="2d348-125">If PIP is not installed, you may install the [PIP](https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="2d348-125">If PIP is not installed, you may install the [PIP](https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="2d348-126">Update PIP to the latest version, by running the `pip install -U pip` command.</span><span class="sxs-lookup"><span data-stu-id="2d348-126">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="2d348-127">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span><span class="sxs-lookup"><span data-stu-id="2d348-127">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="2d348-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="2d348-128">MacOS</span></span>
1. <span data-ttu-id="2d348-129">In Mac OS, Python is typically installed as part of the default OS installation.</span><span class="sxs-lookup"><span data-stu-id="2d348-129">In Mac OS, Python is typically installed as part of the default OS installation.</span></span>
2. <span data-ttu-id="2d348-130">Check the Python installation by launching the bash shell.</span><span class="sxs-lookup"><span data-stu-id="2d348-130">Check the Python installation by launching the bash shell.</span></span> <span data-ttu-id="2d348-131">Run the command `python -V` using the uppercase V switch to see the version number.</span><span class="sxs-lookup"><span data-stu-id="2d348-131">Run the command `python -V` using the uppercase V switch to see the version number.</span></span>
3. <span data-ttu-id="2d348-132">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span><span class="sxs-lookup"><span data-stu-id="2d348-132">Check the PIP installation by running the `pip show pip -V` command to see the version number.</span></span>
4. <span data-ttu-id="2d348-133">PIP may be included in some versions of Python.</span><span class="sxs-lookup"><span data-stu-id="2d348-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="2d348-134">If PIP is not installed, you may install the [PIP](https://pip.pypa.io/en/stable/installing/) package.</span><span class="sxs-lookup"><span data-stu-id="2d348-134">If PIP is not installed, you may install the [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="2d348-135">Update PIP to the latest version, by running the `pip install -U pip` command.</span><span class="sxs-lookup"><span data-stu-id="2d348-135">Update PIP to the latest version, by running the `pip install -U pip` command.</span></span>
6. <span data-ttu-id="2d348-136">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span><span class="sxs-lookup"><span data-stu-id="2d348-136">Install the MySQL connector for Python, and its dependencies by using the PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="2d348-137">Get connection information</span><span class="sxs-lookup"><span data-stu-id="2d348-137">Get connection information</span></span>
<span data-ttu-id="2d348-138">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="2d348-138">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="2d348-139">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="2d348-139">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2d348-140">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2d348-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2d348-141">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="2d348-141">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>
3. <span data-ttu-id="2d348-142">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="2d348-142">Click the server name.</span></span>
4. <span data-ttu-id="2d348-143">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="2d348-143">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="2d348-144">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="2d348-144">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="2d348-145">![Azure Database for MySQL server name](./media/connect-python/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="2d348-145">![Azure Database for MySQL server name](./media/connect-python/1_server-overview-name-login.png)</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="2d348-146">Run Python code</span><span class="sxs-lookup"><span data-stu-id="2d348-146">Run Python code</span></span>
- <span data-ttu-id="2d348-147">Paste the code into a text file, and then save the file into a project folder with file extension .py (such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py).</span><span class="sxs-lookup"><span data-stu-id="2d348-147">Paste the code into a text file, and then save the file into a project folder with file extension .py (such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py).</span></span>
- <span data-ttu-id="2d348-148">To run the code, launch the command prompt or Bash shell.</span><span class="sxs-lookup"><span data-stu-id="2d348-148">To run the code, launch the command prompt or Bash shell.</span></span> <span data-ttu-id="2d348-149">Change directory into your project folder `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="2d348-149">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="2d348-150">Then type the python command followed by the file name `python createtable.py` to run the application.</span><span class="sxs-lookup"><span data-stu-id="2d348-150">Then type the python command followed by the file name `python createtable.py` to run the application.</span></span> <span data-ttu-id="2d348-151">On the Windows OS, if python.exe is not found, you may need to provide the full path to the executable or add the Python path into the path environment variable.</span><span class="sxs-lookup"><span data-stu-id="2d348-151">On the Windows OS, if python.exe is not found, you may need to provide the full path to the executable or add the Python path into the path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="2d348-152">Connect, create table, and insert data</span><span class="sxs-lookup"><span data-stu-id="2d348-152">Connect, create table, and insert data</span></span>
<span data-ttu-id="2d348-153">Use the following code to connect to the server, create a table, and load the data by using an **INSERT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="2d348-153">Use the following code to connect to the server, create a table, and load the data by using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="2d348-154">In the code, the mysql.connector library is imported.</span><span class="sxs-lookup"><span data-stu-id="2d348-154">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="2d348-155">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span><span class="sxs-lookup"><span data-stu-id="2d348-155">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="2d348-156">The code uses a cursor on the connection, and method [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) executes the SQL query against MySQL database.</span><span class="sxs-lookup"><span data-stu-id="2d348-156">The code uses a cursor on the connection, and method [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="2d348-157">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="2d348-157">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'mydemoserver.mysql.database.azure.com',
  'user':'myadmin@mydemoserver',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a><span data-ttu-id="2d348-158">Read data</span><span class="sxs-lookup"><span data-stu-id="2d348-158">Read data</span></span>
<span data-ttu-id="2d348-159">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="2d348-159">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="2d348-160">In the code, the mysql.connector library is imported.</span><span class="sxs-lookup"><span data-stu-id="2d348-160">In the code, the mysql.connector library is imported.</span></span> <span data-ttu-id="2d348-161">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span><span class="sxs-lookup"><span data-stu-id="2d348-161">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="2d348-162">The code uses a cursor on the connection, and method [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) executes the SQL statement against MySQL database.</span><span class="sxs-lookup"><span data-stu-id="2d348-162">The code uses a cursor on the connection, and method [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) executes the SQL statement against MySQL database.</span></span> <span data-ttu-id="2d348-163">The data rows are read using method [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html).</span><span class="sxs-lookup"><span data-stu-id="2d348-163">The data rows are read using method [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html).</span></span> <span data-ttu-id="2d348-164">The result set is kept in a collection row and a for iterator is used to loop over the rows.</span><span class="sxs-lookup"><span data-stu-id="2d348-164">The result set is kept in a collection row and a for iterator is used to loop over the rows.</span></span>

<span data-ttu-id="2d348-165">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="2d348-165">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'mydemoserver.mysql.database.azure.com',
  'user':'myadmin@mydemoserver',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a><span data-ttu-id="2d348-166">Update data</span><span class="sxs-lookup"><span data-stu-id="2d348-166">Update data</span></span>
<span data-ttu-id="2d348-167">Use the following code to connect and update the data by using an **UPDATE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="2d348-167">Use the following code to connect and update the data by using an **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="2d348-168">In the code, the mysql.connector library is imported.</span><span class="sxs-lookup"><span data-stu-id="2d348-168">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="2d348-169">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span><span class="sxs-lookup"><span data-stu-id="2d348-169">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="2d348-170">The code uses a cursor on the connection, and method [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) executes the SQL statement against MySQL database.</span><span class="sxs-lookup"><span data-stu-id="2d348-170">The code uses a cursor on the connection, and method [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) executes the SQL statement against MySQL database.</span></span> 

<span data-ttu-id="2d348-171">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="2d348-171">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'mydemoserver.mysql.database.azure.com',
  'user':'myadmin@mydemoserver',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in the table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="2d348-172">Delete data</span><span class="sxs-lookup"><span data-stu-id="2d348-172">Delete data</span></span>
<span data-ttu-id="2d348-173">Use the following code to connect and remove data by using a **DELETE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="2d348-173">Use the following code to connect and remove data by using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="2d348-174">In the code, the mysql.connector library is imported.</span><span class="sxs-lookup"><span data-stu-id="2d348-174">In the code, the mysql.connector library is imported.</span></span>  <span data-ttu-id="2d348-175">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span><span class="sxs-lookup"><span data-stu-id="2d348-175">The [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used to connect to Azure Database for MySQL using the [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in the config collection.</span></span> <span data-ttu-id="2d348-176">The code uses a cursor on the connection, and method [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) executes the SQL query against MySQL database.</span><span class="sxs-lookup"><span data-stu-id="2d348-176">The code uses a cursor on the connection, and method [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) executes the SQL query against MySQL database.</span></span> 

<span data-ttu-id="2d348-177">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="2d348-177">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from the portal
config = {
  'host':'mydemoserver.mysql.database.azure.com',
  'user':'myadmin@mydemoserver',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with the user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in the table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="2d348-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="2d348-178">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2d348-179">Migrate your database using Export and Import</span><span class="sxs-lookup"><span data-stu-id="2d348-179">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
