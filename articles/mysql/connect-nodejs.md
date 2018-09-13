---
title: Connect to Azure Database for MySQL from Node.js
description: This quickstart provides several Node.js code samples you can use to connect and query data from Azure Database for MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.devlang: nodejs
ms.topic: quickstart
ms.date: 02/28/2018
ms.openlocfilehash: e0edd31027480df3592b46a4c1246462611da26e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869306"
---
# <a name="azure-database-for-mysql-use-nodejs-to-connect-and-query-data"></a><span data-ttu-id="4efe1-103">Azure Database for MySQL: Use Node.js to connect and query data</span><span class="sxs-lookup"><span data-stu-id="4efe1-103">Azure Database for MySQL: Use Node.js to connect and query data</span></span>
<span data-ttu-id="4efe1-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span><span class="sxs-lookup"><span data-stu-id="4efe1-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using [Node.js](https://nodejs.org/) from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="4efe1-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="4efe1-106">This topic assumes that you are familiar with developing using Node.js and that you are new to working with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4efe1-106">This topic assumes that you are familiar with developing using Node.js and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4efe1-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4efe1-107">Prerequisites</span></span>
<span data-ttu-id="4efe1-108">This quickstart uses the resources created in either of these guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="4efe1-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="4efe1-109">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="4efe1-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="4efe1-110">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4efe1-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="4efe1-111">You also need to:</span><span class="sxs-lookup"><span data-stu-id="4efe1-111">You also need to:</span></span>
- <span data-ttu-id="4efe1-112">Install the [Node.js](https://nodejs.org) runtime.</span><span class="sxs-lookup"><span data-stu-id="4efe1-112">Install the [Node.js](https://nodejs.org) runtime.</span></span>
- <span data-ttu-id="4efe1-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package to connect to MySQL from the Node.js application.</span><span class="sxs-lookup"><span data-stu-id="4efe1-113">Install [mysql2](https://www.npmjs.com/package/mysql2) package to connect to MySQL from the Node.js application.</span></span> 

## <a name="install-nodejs-and-the-mysql-connector"></a><span data-ttu-id="4efe1-114">Install Node.js and the MySQL connector</span><span class="sxs-lookup"><span data-stu-id="4efe1-114">Install Node.js and the MySQL connector</span></span>
<span data-ttu-id="4efe1-115">Depending on your platform, follow the instructions in the appropriate section to install Node.js.</span><span class="sxs-lookup"><span data-stu-id="4efe1-115">Depending on your platform, follow the instructions in the appropriate section to install Node.js.</span></span> <span data-ttu-id="4efe1-116">Use npm to install the mysql2 package and its dependencies into your project folder.</span><span class="sxs-lookup"><span data-stu-id="4efe1-116">Use npm to install the mysql2 package and its dependencies into your project folder.</span></span>

### <a name="windows"></a><span data-ttu-id="4efe1-117">**Windows**</span><span class="sxs-lookup"><span data-stu-id="4efe1-117">**Windows**</span></span>
1. <span data-ttu-id="4efe1-118">Visit the [Node.js downloads page](https://nodejs.org/en/download/), and then select your desired Windows installer option.</span><span class="sxs-lookup"><span data-stu-id="4efe1-118">Visit the [Node.js downloads page](https://nodejs.org/en/download/), and then select your desired Windows installer option.</span></span>
2. <span data-ttu-id="4efe1-119">Make a local project folder such as `nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="4efe1-119">Make a local project folder such as `nodejsmysql`.</span></span> 
3. <span data-ttu-id="4efe1-120">Launch the command prompt, and then change directory into the project folder, such as `cd c:\nodejsmysql\`</span><span class="sxs-lookup"><span data-stu-id="4efe1-120">Launch the command prompt, and then change directory into the project folder, such as `cd c:\nodejsmysql\`</span></span>
4. <span data-ttu-id="4efe1-121">Run the NPM tool to install the mysql2 library into the project folder.</span><span class="sxs-lookup"><span data-stu-id="4efe1-121">Run the NPM tool to install the mysql2 library into the project folder.</span></span>

   ```cmd
   cd c:\nodejsmysql\
   "C:\Program Files\nodejs\npm" install mysql2
   "C:\Program Files\nodejs\npm" list
   ```

5. <span data-ttu-id="4efe1-122">Verify the installation by checking the `npm list` output text for `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="4efe1-122">Verify the installation by checking the `npm list` output text for `mysql2@1.3.5`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="4efe1-123">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="4efe1-123">**Linux (Ubuntu)**</span></span>
1. <span data-ttu-id="4efe1-124">Run the following commands to install **Node.js** and **npm** the package manager for Node.js.</span><span class="sxs-lookup"><span data-stu-id="4efe1-124">Run the following commands to install **Node.js** and **npm** the package manager for Node.js.</span></span>

   ```bash
   sudo apt-get install -y nodejs npm
   ```

2. <span data-ttu-id="4efe1-125">Run the following commands to create a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span><span class="sxs-lookup"><span data-stu-id="4efe1-125">Run the following commands to create a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```
3. <span data-ttu-id="4efe1-126">Verify the installation by checking npm list output text for `mysql2@1.3.5`.</span><span class="sxs-lookup"><span data-stu-id="4efe1-126">Verify the installation by checking npm list output text for `mysql2@1.3.5`.</span></span>

### <a name="mac-os"></a><span data-ttu-id="4efe1-127">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="4efe1-127">**Mac OS**</span></span>
1. <span data-ttu-id="4efe1-128">Enter the following commands to install **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="4efe1-128">Enter the following commands to install **brew**, an easy-to-use package manager for Mac OS X and **Node.js**.</span></span>

   ```bash
   ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   brew install node
   ```
2. <span data-ttu-id="4efe1-129">Run the following commands to create a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span><span class="sxs-lookup"><span data-stu-id="4efe1-129">Run the following commands to create a project folder `mysqlnodejs` and install the mysql2 package into that folder.</span></span>

   ```bash
   mkdir nodejsmysql
   cd nodejsmysql
   npm install --save mysql2
   npm list
   ```

3. <span data-ttu-id="4efe1-130">Verify the installation by checking the `npm list` output text for `mysql2@1.3.6`.</span><span class="sxs-lookup"><span data-stu-id="4efe1-130">Verify the installation by checking the `npm list` output text for `mysql2@1.3.6`.</span></span> <span data-ttu-id="4efe1-131">The version number may vary as new patches are released.</span><span class="sxs-lookup"><span data-stu-id="4efe1-131">The version number may vary as new patches are released.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4efe1-132">Get connection information</span><span class="sxs-lookup"><span data-stu-id="4efe1-132">Get connection information</span></span>
<span data-ttu-id="4efe1-133">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4efe1-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="4efe1-134">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="4efe1-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4efe1-135">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4efe1-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4efe1-136">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="4efe1-136">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>
3. <span data-ttu-id="4efe1-137">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="4efe1-137">Click the server name.</span></span>
4. <span data-ttu-id="4efe1-138">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="4efe1-138">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="4efe1-139">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="4efe1-139">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="4efe1-140">![Azure Database for MySQL server name](./media/connect-nodejs/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4efe1-140">![Azure Database for MySQL server name](./media/connect-nodejs/1_server-overview-name-login.png)</span></span>

## <a name="running-the-javascript-code-in-nodejs"></a><span data-ttu-id="4efe1-141">Running the JavaScript code in Node.js</span><span class="sxs-lookup"><span data-stu-id="4efe1-141">Running the JavaScript code in Node.js</span></span>
1. <span data-ttu-id="4efe1-142">Paste the JavaScript code into text files, and then save it into a project folder with file extension .js (such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js).</span><span class="sxs-lookup"><span data-stu-id="4efe1-142">Paste the JavaScript code into text files, and then save it into a project folder with file extension .js (such as C:\nodejsmysql\createtable.js or /home/username/nodejsmysql/createtable.js).</span></span>
2. <span data-ttu-id="4efe1-143">Launch the command prompt or bash shell, and then change directory into your project folder `cd nodejsmysql`.</span><span class="sxs-lookup"><span data-stu-id="4efe1-143">Launch the command prompt or bash shell, and then change directory into your project folder `cd nodejsmysql`.</span></span>
3. <span data-ttu-id="4efe1-144">To run the application, type the node command followed by the file name, such as `node createtable.js`.</span><span class="sxs-lookup"><span data-stu-id="4efe1-144">To run the application, type the node command followed by the file name, such as `node createtable.js`.</span></span>
4. <span data-ttu-id="4efe1-145">On Windows, if the node application is not in your environment variable path, you may need to use the full path to launch the node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span><span class="sxs-lookup"><span data-stu-id="4efe1-145">On Windows, if the node application is not in your environment variable path, you may need to use the full path to launch the node application, such as `"C:\Program Files\nodejs\node.exe" createtable.js`</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="4efe1-146">Connect, create table, and insert data</span><span class="sxs-lookup"><span data-stu-id="4efe1-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="4efe1-147">Use the following code to connect and load the data by using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span><span class="sxs-lookup"><span data-stu-id="4efe1-147">Use the following code to connect and load the data by using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span>

<span data-ttu-id="4efe1-148">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="4efe1-148">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="4efe1-149">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used to establish the connection to the server.</span><span class="sxs-lookup"><span data-stu-id="4efe1-149">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) function is used to establish the connection to the server.</span></span> <span data-ttu-id="4efe1-150">The [query()](https://github.com/mysqljs/mysql#performing-queries) function is used to execute the SQL query against MySQL database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-150">The [query()](https://github.com/mysqljs/mysql#performing-queries) function is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="4efe1-151">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-151">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'mydemoserver.mysql.database.azure.com',
    user: 'myadmin@mydemoserver',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
    if (err) { 
        console.log("!!! Cannot connect !!! Error:");
        throw err;
    }
    else
    {
       console.log("Connection established.");
           queryDatabase();
    }   
});

function queryDatabase(){
       conn.query('DROP TABLE IF EXISTS inventory;', function (err, results, fields) { 
            if (err) throw err; 
            console.log('Dropped inventory table if existed.');
        })
       conn.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);', 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Created inventory table.');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['banana', 150], 
            function (err, results, fields) {
                if (err) throw err;
            else console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['orange', 154], 
            function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.query('INSERT INTO inventory (name, quantity) VALUES (?, ?);', ['apple', 100], 
        function (err, results, fields) {
                if (err) throw err;
            console.log('Inserted ' + results.affectedRows + ' row(s).');
        })
       conn.end(function (err) { 
        if (err) throw err;
        else  console.log('Done.') 
        });
};
```

## <a name="read-data"></a><span data-ttu-id="4efe1-152">Read data</span><span class="sxs-lookup"><span data-stu-id="4efe1-152">Read data</span></span>
<span data-ttu-id="4efe1-153">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="4efe1-153">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="4efe1-154">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="4efe1-154">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="4efe1-155">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span><span class="sxs-lookup"><span data-stu-id="4efe1-155">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="4efe1-156">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-156">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> <span data-ttu-id="4efe1-157">The results array is used to hold the results of the query.</span><span class="sxs-lookup"><span data-stu-id="4efe1-157">The results array is used to hold the results of the query.</span></span>

<span data-ttu-id="4efe1-158">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-158">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'mydemoserver.mysql.database.azure.com',
    user: 'myadmin@mydemoserver',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            readData();
        }   
    });

function readData(){
        conn.query('SELECT * FROM inventory', 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Selected ' + results.length + ' row(s).');
                for (i = 0; i < results.length; i++) {
                    console.log('Row: ' + JSON.stringify(results[i]));
                }
                console.log('Done.');
            })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Closing connection.') 
        });
};
```

## <a name="update-data"></a><span data-ttu-id="4efe1-159">Update data</span><span class="sxs-lookup"><span data-stu-id="4efe1-159">Update data</span></span>
<span data-ttu-id="4efe1-160">Use the following code to connect and read the data by using an **UPDATE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="4efe1-160">Use the following code to connect and read the data by using an **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="4efe1-161">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="4efe1-161">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="4efe1-162">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span><span class="sxs-lookup"><span data-stu-id="4efe1-162">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="4efe1-163">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-163">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="4efe1-164">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-164">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'mydemoserver.mysql.database.azure.com',
    user: 'myadmin@mydemoserver',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            updateData();
        }   
    });

function updateData(){
       conn.query('UPDATE inventory SET quantity = ? WHERE name = ?', [200, 'banana'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Updated ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="delete-data"></a><span data-ttu-id="4efe1-165">Delete data</span><span class="sxs-lookup"><span data-stu-id="4efe1-165">Delete data</span></span>
<span data-ttu-id="4efe1-166">Use the following code to connect and read the data by using a **DELETE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="4efe1-166">Use the following code to connect and read the data by using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="4efe1-167">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="4efe1-167">The [mysql.createConnection()](https://github.com/mysqljs/mysql#establishing-connections) method is used to interface with the MySQL server.</span></span> <span data-ttu-id="4efe1-168">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span><span class="sxs-lookup"><span data-stu-id="4efe1-168">The [connect()](https://github.com/mysqljs/mysql#establishing-connections) method is used to establish the connection to the server.</span></span> <span data-ttu-id="4efe1-169">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-169">The [query()](https://github.com/mysqljs/mysql#performing-queries) method is used to execute the SQL query against MySQL database.</span></span> 

<span data-ttu-id="4efe1-170">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span><span class="sxs-lookup"><span data-stu-id="4efe1-170">Replace the `host`, `user`, `password`, and `database` parameters with the values that you specified when you created the server and database.</span></span>

```javascript
const mysql = require('mysql2');

var config =
{
    host: 'mydemoserver.mysql.database.azure.com',
    user: 'myadmin@mydemoserver',
    password: 'your_password',
    database: 'quickstartdb',
    port: 3306,
    ssl: true
};

const conn = new mysql.createConnection(config);

conn.connect(
    function (err) { 
        if (err) { 
            console.log("!!! Cannot connect !!! Error:");
            throw err;
        }
        else {
            console.log("Connection established.");
            deleteData();
        }   
    });

function deleteData(){
       conn.query('DELETE FROM inventory WHERE name = ?', ['orange'], 
            function (err, results, fields) {
                if (err) throw err;
                else console.log('Deleted ' + results.affectedRows + ' row(s).');
        })
       conn.end(
           function (err) { 
                if (err) throw err;
                else  console.log('Done.') 
        });
};
```

## <a name="next-steps"></a><span data-ttu-id="4efe1-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="4efe1-171">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4efe1-172">Migrate your database using Export and Import</span><span class="sxs-lookup"><span data-stu-id="4efe1-172">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
