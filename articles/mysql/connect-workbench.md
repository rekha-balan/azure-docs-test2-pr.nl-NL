---
title: Connect to Azure Database for MySQL from MySQL Workbench
description: This Quickstart provides the steps to use MySQL Workbench to connect and query data from Azure Database for MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: kfile
editor: seanli1988
ms.service: mysql
ms.custom: mvc
ms.topic: quickstart
ms.date: 02/28/2018
ms.openlocfilehash: def984a6a31cdfe9b9dfbba93ccfb5016b5e315d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855606"
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a><span data-ttu-id="425ba-103">Azure Database for MySQL: Use MySQL Workbench to connect and query data</span><span class="sxs-lookup"><span data-stu-id="425ba-103">Azure Database for MySQL: Use MySQL Workbench to connect and query data</span></span>
<span data-ttu-id="425ba-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using the MySQL Workbench application.</span><span class="sxs-lookup"><span data-stu-id="425ba-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using the MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="425ba-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="425ba-105">Prerequisites</span></span>
<span data-ttu-id="425ba-106">This quickstart uses the resources created in either of these guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="425ba-106">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="425ba-107">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="425ba-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="425ba-108">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="425ba-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="425ba-109">Install MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="425ba-109">Install MySQL Workbench</span></span>
<span data-ttu-id="425ba-110">Download and install MySQL Workbench on your computer from [the MySQL website](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="425ba-110">Download and install MySQL Workbench on your computer from [the MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="425ba-111">Get connection information</span><span class="sxs-lookup"><span data-stu-id="425ba-111">Get connection information</span></span>
<span data-ttu-id="425ba-112">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="425ba-112">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="425ba-113">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="425ba-113">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="425ba-114">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="425ba-114">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="425ba-115">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="425ba-115">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>

3. <span data-ttu-id="425ba-116">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="425ba-116">Click the server name.</span></span>

4. <span data-ttu-id="425ba-117">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="425ba-117">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="425ba-118">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="425ba-118">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="425ba-119">![Azure Database for MySQL server name](./media/connect-php/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="425ba-119">![Azure Database for MySQL server name](./media/connect-php/1_server-overview-name-login.png)</span></span>

## <a name="connect-to-the-server-by-using-mysql-workbench"></a><span data-ttu-id="425ba-120">Connect to the server by using MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="425ba-120">Connect to the server by using MySQL Workbench</span></span> 
<span data-ttu-id="425ba-121">To connect to Azure MySQL Server by using the GUI tool MySQL Workbench:</span><span class="sxs-lookup"><span data-stu-id="425ba-121">To connect to Azure MySQL Server by using the GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="425ba-122">Launch the MySQL Workbench application on your computer.</span><span class="sxs-lookup"><span data-stu-id="425ba-122">Launch the MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="425ba-123">In **Setup New Connection** dialog box, enter the following information on the **Parameters** tab:</span><span class="sxs-lookup"><span data-stu-id="425ba-123">In **Setup New Connection** dialog box, enter the following information on the **Parameters** tab:</span></span>

    ![setup new connection](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="425ba-125">**Setting**</span><span class="sxs-lookup"><span data-stu-id="425ba-125">**Setting**</span></span> | <span data-ttu-id="425ba-126">**Suggested value**</span><span class="sxs-lookup"><span data-stu-id="425ba-126">**Suggested value**</span></span> | <span data-ttu-id="425ba-127">**Field description**</span><span class="sxs-lookup"><span data-stu-id="425ba-127">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="425ba-128">Connection Name</span><span class="sxs-lookup"><span data-stu-id="425ba-128">Connection Name</span></span> | <span data-ttu-id="425ba-129">Demo Connection</span><span class="sxs-lookup"><span data-stu-id="425ba-129">Demo Connection</span></span> | <span data-ttu-id="425ba-130">Specify a label for this connection.</span><span class="sxs-lookup"><span data-stu-id="425ba-130">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="425ba-131">Connection Method</span><span class="sxs-lookup"><span data-stu-id="425ba-131">Connection Method</span></span> | <span data-ttu-id="425ba-132">Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="425ba-132">Standard (TCP/IP)</span></span> | <span data-ttu-id="425ba-133">Standard (TCP/IP) is sufficient.</span><span class="sxs-lookup"><span data-stu-id="425ba-133">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="425ba-134">Hostname</span><span class="sxs-lookup"><span data-stu-id="425ba-134">Hostname</span></span> | <span data-ttu-id="425ba-135">*server name*</span><span class="sxs-lookup"><span data-stu-id="425ba-135">*server name*</span></span> | <span data-ttu-id="425ba-136">Specify the server name value that was used when you created the Azure Database for MySQL earlier.</span><span class="sxs-lookup"><span data-stu-id="425ba-136">Specify the server name value that was used when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="425ba-137">Our example server shown is mydemoserver.mysql.database.azure.com.</span><span class="sxs-lookup"><span data-stu-id="425ba-137">Our example server shown is mydemoserver.mysql.database.azure.com.</span></span> <span data-ttu-id="425ba-138">Use the fully qualified domain name (\*.mysql.database.azure.com) as shown in the example.</span><span class="sxs-lookup"><span data-stu-id="425ba-138">Use the fully qualified domain name (\*.mysql.database.azure.com) as shown in the example.</span></span> <span data-ttu-id="425ba-139">Follow the steps in the previous section to get the connection information if you do not remember your server name.</span><span class="sxs-lookup"><span data-stu-id="425ba-139">Follow the steps in the previous section to get the connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="425ba-140">Port</span><span class="sxs-lookup"><span data-stu-id="425ba-140">Port</span></span> | <span data-ttu-id="425ba-141">3306</span><span class="sxs-lookup"><span data-stu-id="425ba-141">3306</span></span> | <span data-ttu-id="425ba-142">Always use port 3306 when connecting to Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="425ba-142">Always use port 3306 when connecting to Azure Database for MySQL.</span></span> |
    | <span data-ttu-id="425ba-143">Username</span><span class="sxs-lookup"><span data-stu-id="425ba-143">Username</span></span> |  <span data-ttu-id="425ba-144">*server admin login name*</span><span class="sxs-lookup"><span data-stu-id="425ba-144">*server admin login name*</span></span> | <span data-ttu-id="425ba-145">Type in the server admin login username supplied when you created the Azure Database for MySQL earlier.</span><span class="sxs-lookup"><span data-stu-id="425ba-145">Type in the server admin login username supplied when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="425ba-146">Our example username is myadmin@mydemoserver.</span><span class="sxs-lookup"><span data-stu-id="425ba-146">Our example username is myadmin@mydemoserver.</span></span> <span data-ttu-id="425ba-147">Follow the steps in the previous section to get the connection information if you do not remember the username.</span><span class="sxs-lookup"><span data-stu-id="425ba-147">Follow the steps in the previous section to get the connection information if you do not remember the username.</span></span> <span data-ttu-id="425ba-148">The format is *username@servername*.</span><span class="sxs-lookup"><span data-stu-id="425ba-148">The format is *username@servername*.</span></span>
    | <span data-ttu-id="425ba-149">Password</span><span class="sxs-lookup"><span data-stu-id="425ba-149">Password</span></span> | <span data-ttu-id="425ba-150">your password</span><span class="sxs-lookup"><span data-stu-id="425ba-150">your password</span></span> | <span data-ttu-id="425ba-151">Click **Store in Vault...** button to save the password.</span><span class="sxs-lookup"><span data-stu-id="425ba-151">Click **Store in Vault...** button to save the password.</span></span> |

3.   <span data-ttu-id="425ba-152">Click **Test Connection** to test if all parameters are correctly configured.</span><span class="sxs-lookup"><span data-stu-id="425ba-152">Click **Test Connection** to test if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="425ba-153">Click **OK** to save the connection.</span><span class="sxs-lookup"><span data-stu-id="425ba-153">Click **OK** to save the connection.</span></span> 

5.   <span data-ttu-id="425ba-154">In the listing of **MySQL Connections**, click the tile corresponding to your server, and then wait for the connection to be established.</span><span class="sxs-lookup"><span data-stu-id="425ba-154">In the listing of **MySQL Connections**, click the tile corresponding to your server, and then wait for the connection to be established.</span></span>

        <span data-ttu-id="425ba-155">A new SQL tab opens with a blank editor where you can type your queries.</span><span class="sxs-lookup"><span data-stu-id="425ba-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>
    
        > [!NOTE]
        > <span data-ttu-id="425ba-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="425ba-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="425ba-157">Although typically no additional configuration with SSL certificates is required for MySQL Workbench to connect to your server, we recommend binding the SSL CA certification with MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="425ba-157">Although typically no additional configuration with SSL certificates is required for MySQL Workbench to connect to your server, we recommend binding the SSL CA certification with MySQL Workbench.</span></span> <span data-ttu-id="425ba-158">For more information on how to download and bind the certification, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="425ba-158">For more information on how to download and bind the certification, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="425ba-159">If you need to disable SSL, visit the Azure portal and click the Connection security page to disable the Enforce SSL connection toggle button.</span><span class="sxs-lookup"><span data-stu-id="425ba-159">If you need to disable SSL, visit the Azure portal and click the Connection security page to disable the Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="425ba-160">Create a table, insert data, read data, update data, delete data</span><span class="sxs-lookup"><span data-stu-id="425ba-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="425ba-161">Copy and paste the sample SQL code into a blank SQL tab to illustrate some sample data.</span><span class="sxs-lookup"><span data-stu-id="425ba-161">Copy and paste the sample SQL code into a blank SQL tab to illustrate some sample data.</span></span>

    <span data-ttu-id="425ba-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span><span class="sxs-lookup"><span data-stu-id="425ba-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="425ba-163">It inserts some rows, then reads the rows.</span><span class="sxs-lookup"><span data-stu-id="425ba-163">It inserts some rows, then reads the rows.</span></span> <span data-ttu-id="425ba-164">It changes the data with an update statement, and reads the rows again.</span><span class="sxs-lookup"><span data-stu-id="425ba-164">It changes the data with an update statement, and reads the rows again.</span></span> <span data-ttu-id="425ba-165">Finally it deletes a row, and then reads the rows again.</span><span class="sxs-lookup"><span data-stu-id="425ba-165">Finally it deletes a row, and then reads the rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="425ba-166">The screenshot shows an example of the SQL code in SQL Workbench and the output after it has been run.</span><span class="sxs-lookup"><span data-stu-id="425ba-166">The screenshot shows an example of the SQL code in SQL Workbench and the output after it has been run.</span></span>
    
    ![MySQL Workbench SQL Tab to run sample SQL code](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="425ba-168">To run the sample SQL Code, click the lightening bolt icon in the toolbar of the **SQL File** tab.</span><span class="sxs-lookup"><span data-stu-id="425ba-168">To run the sample SQL Code, click the lightening bolt icon in the toolbar of the **SQL File** tab.</span></span>
3. <span data-ttu-id="425ba-169">Notice the three tabbed results in the **Result Grid** section in the middle of the page.</span><span class="sxs-lookup"><span data-stu-id="425ba-169">Notice the three tabbed results in the **Result Grid** section in the middle of the page.</span></span> 
4. <span data-ttu-id="425ba-170">Notice the **Output** list at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="425ba-170">Notice the **Output** list at the bottom of the page.</span></span> <span data-ttu-id="425ba-171">The status of each command is shown.</span><span class="sxs-lookup"><span data-stu-id="425ba-171">The status of each command is shown.</span></span> 

<span data-ttu-id="425ba-172">Now, you have connected to Azure Database for MySQL by using MySQL Workbench, and you have queried data using the SQL language.</span><span class="sxs-lookup"><span data-stu-id="425ba-172">Now, you have connected to Azure Database for MySQL by using MySQL Workbench, and you have queried data using the SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="425ba-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="425ba-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="425ba-174">Migrate your database using Export and Import</span><span class="sxs-lookup"><span data-stu-id="425ba-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
