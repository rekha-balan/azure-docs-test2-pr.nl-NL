---
title: Connect to Azure Database for MySQL from PHP
description: This quickstart provides several PHP code samples you can use to connect and query data from Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.topic: quickstart
ms.date: 02/28/2018
ms.openlocfilehash: 1e919ddb063bcd96b0c6766a28762d1b474cb8a1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865554"
---
# <a name="azure-database-for-mysql-use-php-to-connect-and-query-data"></a><span data-ttu-id="b749d-103">Azure Database for MySQL: Use PHP to connect and query data</span><span class="sxs-lookup"><span data-stu-id="b749d-103">Azure Database for MySQL: Use PHP to connect and query data</span></span>
<span data-ttu-id="b749d-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span><span class="sxs-lookup"><span data-stu-id="b749d-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="b749d-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="b749d-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="b749d-106">This topic assumes that you are familiar with development using PHP and that you are new to working with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="b749d-106">This topic assumes that you are familiar with development using PHP and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b749d-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b749d-107">Prerequisites</span></span>
<span data-ttu-id="b749d-108">This quickstart uses the resources created in either of these guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="b749d-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b749d-109">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="b749d-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="b749d-110">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b749d-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="b749d-111">Install PHP</span><span class="sxs-lookup"><span data-stu-id="b749d-111">Install PHP</span></span>
<span data-ttu-id="b749d-112">Install PHP on your own server, or create an Azure [web app](../app-service/app-service-web-overview.md) that includes PHP.</span><span class="sxs-lookup"><span data-stu-id="b749d-112">Install PHP on your own server, or create an Azure [web app](../app-service/app-service-web-overview.md) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="b749d-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="b749d-113">MacOS</span></span>
- <span data-ttu-id="b749d-114">Download [PHP 7.1.4 version](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="b749d-114">Download [PHP 7.1.4 version](http://php.net/downloads.php).</span></span>
- <span data-ttu-id="b749d-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration.</span><span class="sxs-lookup"><span data-stu-id="b749d-115">Install PHP and refer to the [PHP manual](http://php.net/manual/install.macosx.php) for further configuration.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="b749d-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b749d-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="b749d-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php).</span><span class="sxs-lookup"><span data-stu-id="b749d-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php).</span></span>
- <span data-ttu-id="b749d-118">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration.</span><span class="sxs-lookup"><span data-stu-id="b749d-118">Install PHP and refer to the [PHP manual](http://php.net/manual/install.unix.php) for further configuration.</span></span>

### <a name="windows"></a><span data-ttu-id="b749d-119">Windows</span><span class="sxs-lookup"><span data-stu-id="b749d-119">Windows</span></span>
- <span data-ttu-id="b749d-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1).</span><span class="sxs-lookup"><span data-stu-id="b749d-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1).</span></span>
- <span data-ttu-id="b749d-121">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration.</span><span class="sxs-lookup"><span data-stu-id="b749d-121">Install PHP and refer to the [PHP manual](http://php.net/manual/install.windows.php) for further configuration.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b749d-122">Get connection information</span><span class="sxs-lookup"><span data-stu-id="b749d-122">Get connection information</span></span>
<span data-ttu-id="b749d-123">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="b749d-123">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="b749d-124">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="b749d-124">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b749d-125">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b749d-125">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b749d-126">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="b749d-126">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>
3. <span data-ttu-id="b749d-127">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="b749d-127">Click the server name.</span></span>
4. <span data-ttu-id="b749d-128">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="b749d-128">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="b749d-129">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="b749d-129">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="b749d-130">![Azure Database for MySQL server name](./media/connect-php/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b749d-130">![Azure Database for MySQL server name](./media/connect-php/1_server-overview-name-login.png)</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="b749d-131">Connect and create a table</span><span class="sxs-lookup"><span data-stu-id="b749d-131">Connect and create a table</span></span>
<span data-ttu-id="b749d-132">Use the following code to connect and create a table by using **CREATE TABLE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="b749d-132">Use the following code to connect and create a table by using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="b749d-133">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span><span class="sxs-lookup"><span data-stu-id="b749d-133">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b749d-134">The code calls methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) to connect to MySQL.</span><span class="sxs-lookup"><span data-stu-id="b749d-134">The code calls methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) to connect to MySQL.</span></span> <span data-ttu-id="b749d-135">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) to run the query.</span><span class="sxs-lookup"><span data-stu-id="b749d-135">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) to run the query.</span></span> <span data-ttu-id="b749d-136">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) to close the connection.</span><span class="sxs-lookup"><span data-stu-id="b749d-136">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) to close the connection.</span></span>

<span data-ttu-id="b749d-137">Replace the host, username, password, and db_name parameters with your own values.</span><span class="sxs-lookup"><span data-stu-id="b749d-137">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

// Run the create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a><span data-ttu-id="b749d-138">Insert data</span><span class="sxs-lookup"><span data-stu-id="b749d-138">Insert data</span></span>
<span data-ttu-id="b749d-139">Use the following code to connect and insert data by using an **INSERT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="b749d-139">Use the following code to connect and insert data by using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="b749d-140">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span><span class="sxs-lookup"><span data-stu-id="b749d-140">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b749d-141">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared insert statement, then binds the parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="b749d-141">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared insert statement, then binds the parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="b749d-142">The code runs the statement by using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement by using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="b749d-142">The code runs the statement by using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement by using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="b749d-143">Replace the host, username, password, and db_name parameters with your own values.</span><span class="sxs-lookup"><span data-stu-id="b749d-143">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close the connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a><span data-ttu-id="b749d-144">Read data</span><span class="sxs-lookup"><span data-stu-id="b749d-144">Read data</span></span>
<span data-ttu-id="b749d-145">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="b749d-145">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="b749d-146">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span><span class="sxs-lookup"><span data-stu-id="b749d-146">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b749d-147">The code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform the sql query and method [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) to fetch the resulting rows.</span><span class="sxs-lookup"><span data-stu-id="b749d-147">The code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform the sql query and method [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) to fetch the resulting rows.</span></span>

<span data-ttu-id="b749d-148">Replace the host, username, password, and db_name parameters with your own values.</span><span class="sxs-lookup"><span data-stu-id="b749d-148">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a><span data-ttu-id="b749d-149">Update data</span><span class="sxs-lookup"><span data-stu-id="b749d-149">Update data</span></span>
<span data-ttu-id="b749d-150">Use the following code to connect and update the data by using an **UPDATE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="b749d-150">Use the following code to connect and update the data by using an **UPDATE** SQL statement.</span></span>

<span data-ttu-id="b749d-151">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span><span class="sxs-lookup"><span data-stu-id="b749d-151">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b749d-152">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared update statement, then binds the parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="b749d-152">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared update statement, then binds the parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="b749d-153">The code runs the statement by using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement by using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="b749d-153">The code runs the statement by using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement by using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="b749d-154">Replace the host, username, password, and db_name parameters with your own values.</span><span class="sxs-lookup"><span data-stu-id="b749d-154">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close the connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a><span data-ttu-id="b749d-155">Delete data</span><span class="sxs-lookup"><span data-stu-id="b749d-155">Delete data</span></span>
<span data-ttu-id="b749d-156">Use the following code to connect and read the data by using a **DELETE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="b749d-156">Use the following code to connect and read the data by using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="b749d-157">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span><span class="sxs-lookup"><span data-stu-id="b749d-157">The code uses the **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="b749d-158">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared delete statement, then binds the parameters for the where clause in the statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="b749d-158">The code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) to create a prepared delete statement, then binds the parameters for the where clause in the statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="b749d-159">The code runs the statement by using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement by using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="b749d-159">The code runs the statement by using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes the statement by using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="b749d-160">Replace the host, username, password, and db_name parameters with your own values.</span><span class="sxs-lookup"><span data-stu-id="b749d-160">Replace the host, username, password, and db_name parameters with your own values.</span></span> 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a><span data-ttu-id="b749d-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="b749d-161">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b749d-162">Connect to Azure Database for MySQL via SSL</span><span class="sxs-lookup"><span data-stu-id="b749d-162">Connect to Azure Database for MySQL via SSL</span></span>](howto-configure-ssl.md)
