---
title: Create a PHP-SQL web app and deploy to Azure App Service using Git
description: A tutorial that demonstrates how to create a PHP web app that stores data in Azure SQL Database and use Git deployment to Azure App Service.
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 155a7091ce4fb8df5590cefd94f78e19539191b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556120"
---
# <a name="create-a-php-sql-web-app-and-deploy-to-azure-app-service-using-git"></a><span data-ttu-id="7fb44-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span><span class="sxs-lookup"><span data-stu-id="7fb44-103">Create a PHP-SQL web app and deploy to Azure App Service using Git</span></span>
<span data-ttu-id="7fb44-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span><span class="sxs-lookup"><span data-stu-id="7fb44-104">This tutorial shows you how to create a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects to Azure SQL Database and how to deploy it using Git.</span></span> <span data-ttu-id="7fb44-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="7fb44-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], the [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="7fb44-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb44-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="7fb44-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="7fb44-107">You can install and configure PHP, SQL Server Express, and the Microsoft Drivers for SQL Server for PHP using the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="7fb44-108">You will learn:</span><span class="sxs-lookup"><span data-stu-id="7fb44-108">You will learn:</span></span>

* <span data-ttu-id="7fb44-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="7fb44-109">How to create an Azure web app and a SQL Database using the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="7fb44-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span><span class="sxs-lookup"><span data-stu-id="7fb44-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="7fb44-111">How to publish and re-publish your application to Azure using Git.</span><span class="sxs-lookup"><span data-stu-id="7fb44-111">How to publish and re-publish your application to Azure using Git.</span></span>

<span data-ttu-id="7fb44-112">By following this tutorial, you will build a simple registration web application in PHP.</span><span class="sxs-lookup"><span data-stu-id="7fb44-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="7fb44-113">The application will be hosted in an Azure Website.</span><span class="sxs-lookup"><span data-stu-id="7fb44-113">The application will be hosted in an Azure Website.</span></span> <span data-ttu-id="7fb44-114">A screenshot of the completed application is below:</span><span class="sxs-lookup"><span data-stu-id="7fb44-114">A screenshot of the completed application is below:</span></span>

![Azure PHP Web Site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="7fb44-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="7fb44-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7fb44-117">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="7fb44-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="7fb44-118">Create an Azure web app and set up Git publishing</span><span class="sxs-lookup"><span data-stu-id="7fb44-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="7fb44-119">Follow these steps to create an Azure web app and a SQL Database:</span><span class="sxs-lookup"><span data-stu-id="7fb44-119">Follow these steps to create an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="7fb44-120">Log in to the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7fb44-120">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7fb44-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span><span class="sxs-lookup"><span data-stu-id="7fb44-121">Open the Azure Marketplace by clicking the **New** icon on the top left of the dashboard, click on **Select All** next to Marketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="7fb44-122">In the Marketplace, select **Web + Mobile**.</span><span class="sxs-lookup"><span data-stu-id="7fb44-122">In the Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="7fb44-123">Click the **Web app + SQL** icon.</span><span class="sxs-lookup"><span data-stu-id="7fb44-123">Click the **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="7fb44-124">After reading the description of the Web app + SQL app, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="7fb44-124">After reading the description of the Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="7fb44-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span><span class="sxs-lookup"><span data-stu-id="7fb44-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for the required fields:</span></span>
   
   * <span data-ttu-id="7fb44-126">Enter a URL name of your choice</span><span class="sxs-lookup"><span data-stu-id="7fb44-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="7fb44-127">Configure database server credentials</span><span class="sxs-lookup"><span data-stu-id="7fb44-127">Configure database server credentials</span></span>
   * <span data-ttu-id="7fb44-128">Select the region closest to you</span><span class="sxs-lookup"><span data-stu-id="7fb44-128">Select the region closest to you</span></span>
     
     ![configure your app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="7fb44-130">When finished defining the web app, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7fb44-130">When finished defining the web app, click **Create**.</span></span>
   
    <span data-ttu-id="7fb44-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span><span class="sxs-lookup"><span data-stu-id="7fb44-131">When the web app has been created, the **Notifications** button will flash a green **SUCCESS** and the resource group blade open to show both the web app and the SQL database in the group.</span></span>
8. <span data-ttu-id="7fb44-132">Click the web app's icon in the resource group blade to open the web app's blade.</span><span class="sxs-lookup"><span data-stu-id="7fb44-132">Click the web app's icon in the resource group blade to open the web app's blade.</span></span>
   
    ![web app's resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="7fb44-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span><span class="sxs-lookup"><span data-stu-id="7fb44-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="7fb44-135">Select **Local Git Repository** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fb44-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![where is your source code](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="7fb44-137">If you have not set up a Git repository before, you must provide a user name and password.</span><span class="sxs-lookup"><span data-stu-id="7fb44-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="7fb44-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span><span class="sxs-lookup"><span data-stu-id="7fb44-138">To do this, click **Settings** > **Deployment credentials** in the web app's blade.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="7fb44-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span><span class="sxs-lookup"><span data-stu-id="7fb44-139">In **Settings** click on **Properties** to see the Git remote URL you need to use to deploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="7fb44-140">Get SQL Database connection information</span><span class="sxs-lookup"><span data-stu-id="7fb44-140">Get SQL Database connection information</span></span>
<span data-ttu-id="7fb44-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span><span class="sxs-lookup"><span data-stu-id="7fb44-141">To connect to the SQL Database instance that is linked to your web app, your will need the connection information, which you specified when you created the database.</span></span> <span data-ttu-id="7fb44-142">To get the SQL Database connection information, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7fb44-142">To get the SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="7fb44-143">Back in the resource group's blade, click the SQL database's icon.</span><span class="sxs-lookup"><span data-stu-id="7fb44-143">Back in the resource group's blade, click the SQL database's icon.</span></span>
2. <span data-ttu-id="7fb44-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span><span class="sxs-lookup"><span data-stu-id="7fb44-144">In the SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![View database properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="7fb44-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span><span class="sxs-lookup"><span data-stu-id="7fb44-146">From the **PHP** section of the resulting dialog, make note of the values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="7fb44-147">You will use these values later when publishing your PHP web app to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7fb44-147">You will use these values later when publishing your PHP web app to Azure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="7fb44-148">Build and test your application locally</span><span class="sxs-lookup"><span data-stu-id="7fb44-148">Build and test your application locally</span></span>
<span data-ttu-id="7fb44-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span><span class="sxs-lookup"><span data-stu-id="7fb44-149">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="7fb44-150">Information about previous registrants is displayed in a table.</span><span class="sxs-lookup"><span data-stu-id="7fb44-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="7fb44-151">Registration information is stored in a SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="7fb44-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="7fb44-152">The application consists of two files (copy/paste code available below):</span><span class="sxs-lookup"><span data-stu-id="7fb44-152">The application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="7fb44-153">**index.php**: Displays a form for registration and a table containing registrant information.</span><span class="sxs-lookup"><span data-stu-id="7fb44-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="7fb44-154">**createtable.php**: Creates the SQL Database table for the application.</span><span class="sxs-lookup"><span data-stu-id="7fb44-154">**createtable.php**: Creates the SQL Database table for the application.</span></span> <span data-ttu-id="7fb44-155">This file will only be used once.</span><span class="sxs-lookup"><span data-stu-id="7fb44-155">This file will only be used once.</span></span>

<span data-ttu-id="7fb44-156">To run the application locally, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="7fb44-156">To run the application locally, follow the steps below.</span></span> <span data-ttu-id="7fb44-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="7fb44-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled the [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="7fb44-158">Create a SQL Server database called `registration`.</span><span class="sxs-lookup"><span data-stu-id="7fb44-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="7fb44-159">You can do this from the `sqlcmd` command prompt with these commands:</span><span class="sxs-lookup"><span data-stu-id="7fb44-159">You can do this from the `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="7fb44-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span><span class="sxs-lookup"><span data-stu-id="7fb44-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="7fb44-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span><span class="sxs-lookup"><span data-stu-id="7fb44-161">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="7fb44-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span><span class="sxs-lookup"><span data-stu-id="7fb44-162">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="7fb44-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span><span class="sxs-lookup"><span data-stu-id="7fb44-163">Note that you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="7fb44-164">In a terminal at the root directory of the application type the following command:</span><span class="sxs-lookup"><span data-stu-id="7fb44-164">In a terminal at the root directory of the application type the following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="7fb44-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="7fb44-165">Open a web browser and browse to **http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="7fb44-166">This will create the `registration_tbl` table in the database.</span><span class="sxs-lookup"><span data-stu-id="7fb44-166">This will create the `registration_tbl` table in the database.</span></span>
6. <span data-ttu-id="7fb44-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span><span class="sxs-lookup"><span data-stu-id="7fb44-167">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="7fb44-168">Within the PHP tags, add PHP code for connecting to the database.</span><span class="sxs-lookup"><span data-stu-id="7fb44-168">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="7fb44-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span><span class="sxs-lookup"><span data-stu-id="7fb44-169">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="7fb44-170">Following the database connection code, add code for inserting registration information into the database.</span><span class="sxs-lookup"><span data-stu-id="7fb44-170">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="7fb44-171">Finally, following the code above, add code for retrieving data from the database.</span><span class="sxs-lookup"><span data-stu-id="7fb44-171">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="7fb44-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span><span class="sxs-lookup"><span data-stu-id="7fb44-172">You can now browse to **http://localhost:8000/index.php** to test the application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="7fb44-173">Publish your application</span><span class="sxs-lookup"><span data-stu-id="7fb44-173">Publish your application</span></span>
<span data-ttu-id="7fb44-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span><span class="sxs-lookup"><span data-stu-id="7fb44-174">After you have tested your application locally, you can publish it to App Service Web Apps using Git.</span></span> <span data-ttu-id="7fb44-175">However, you first need to update the database connection information in the application.</span><span class="sxs-lookup"><span data-stu-id="7fb44-175">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="7fb44-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span><span class="sxs-lookup"><span data-stu-id="7fb44-176">Using the database connection information you obtained earlier (in the **Get SQL Database connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="7fb44-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="7fb44-177">In the <code>$host</code>, the value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="7fb44-178">Now, you are ready to set up Git publishing and publish the application.</span><span class="sxs-lookup"><span data-stu-id="7fb44-178">Now, you are ready to set up Git publishing and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="7fb44-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span><span class="sxs-lookup"><span data-stu-id="7fb44-179">These are the same steps noted at the end of the **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="7fb44-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="7fb44-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application (the **registration** directory), and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="7fb44-181">You will be prompted for the password you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7fb44-181">You will be prompted for the password you created earlier.</span></span>
2. <span data-ttu-id="7fb44-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span><span class="sxs-lookup"><span data-stu-id="7fb44-182">Browse to **http://[web app name].azurewebsites.net/createtable.php** to create the SQL database table for the application.</span></span>
3. <span data-ttu-id="7fb44-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span><span class="sxs-lookup"><span data-stu-id="7fb44-183">Browse to **http://[web app name].azurewebsites.net/index.php** to begin using the application.</span></span>

<span data-ttu-id="7fb44-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span><span class="sxs-lookup"><span data-stu-id="7fb44-184">After you have published your application, you can begin making changes to it and use Git to publish them.</span></span> 

## <a name="publish-changes-to-your-application"></a><span data-ttu-id="7fb44-185">Publish changes to your application</span><span class="sxs-lookup"><span data-stu-id="7fb44-185">Publish changes to your application</span></span>
<span data-ttu-id="7fb44-186">To publish changes to application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7fb44-186">To publish changes to application, follow these steps:</span></span>

1. <span data-ttu-id="7fb44-187">Make changes to your application locally.</span><span class="sxs-lookup"><span data-stu-id="7fb44-187">Make changes to your application locally.</span></span>
2. <span data-ttu-id="7fb44-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="7fb44-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="7fb44-189">You will be prompted for the password you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7fb44-189">You will be prompted for the password you created earlier.</span></span>
3. <span data-ttu-id="7fb44-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span><span class="sxs-lookup"><span data-stu-id="7fb44-190">Browse to **http://[web app name].azurewebsites.net/index.php** to see your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="7fb44-191">What's changed</span><span class="sxs-lookup"><span data-stu-id="7fb44-191">What's changed</span></span>
* <span data-ttu-id="7fb44-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7fb44-192">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv







