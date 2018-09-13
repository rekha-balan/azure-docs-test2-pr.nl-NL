---
title: Create a PHP-MySQL web app in Azure App Service and deploy using FTP
description: A tutorial that demonstrates how to create a PHP web app that stores data in MySQL and use FTP deployment to Azure.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: bfdcf44ef32c380bf1e60118e077bacdbaf82092
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551483"
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="660f3-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span><span class="sxs-lookup"><span data-stu-id="660f3-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="660f3-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span><span class="sxs-lookup"><span data-stu-id="660f3-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="660f3-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="660f3-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="660f3-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span><span class="sxs-lookup"><span data-stu-id="660f3-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="660f3-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span><span class="sxs-lookup"><span data-stu-id="660f3-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="660f3-108">You will learn:</span><span class="sxs-lookup"><span data-stu-id="660f3-108">You will learn:</span></span>

* <span data-ttu-id="660f3-109">How to create a web app and a MySQL database using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="660f3-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="660f3-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span><span class="sxs-lookup"><span data-stu-id="660f3-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="660f3-111">How to publish your application to Azure using FTP.</span><span class="sxs-lookup"><span data-stu-id="660f3-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="660f3-112">By following this tutorial, you will build a simple registration web app in PHP.</span><span class="sxs-lookup"><span data-stu-id="660f3-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="660f3-113">The application will be hosted in a Web App.</span><span class="sxs-lookup"><span data-stu-id="660f3-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="660f3-114">A screenshot of the completed application is below:</span><span class="sxs-lookup"><span data-stu-id="660f3-114">A screenshot of the completed application is below:</span></span>

![Azure PHP Web Site][running-app]

> [!NOTE]
> <span data-ttu-id="660f3-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="660f3-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="660f3-117">No credit cards required, no commitments.</span><span class="sxs-lookup"><span data-stu-id="660f3-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="660f3-118">Create a web app and set up FTP publishing</span><span class="sxs-lookup"><span data-stu-id="660f3-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="660f3-119">Follow these steps to create a web app and a MySQL database:</span><span class="sxs-lookup"><span data-stu-id="660f3-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="660f3-120">Login to the [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="660f3-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="660f3-121">Click the **+ New** icon on the top left of the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="660f3-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Create New Azure Web Site][new-website]
3. <span data-ttu-id="660f3-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="660f3-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Custom Create a new Web Site][custom-create]
4. <span data-ttu-id="660f3-125">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="660f3-125">Click **Create**.</span></span> <span data-ttu-id="660f3-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span><span class="sxs-lookup"><span data-stu-id="660f3-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Set resource group name][resource-group]
5. <span data-ttu-id="660f3-128">Enter values for your new database, including agreeing to the legal terms.</span><span class="sxs-lookup"><span data-stu-id="660f3-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Create new MySQL database][new-mysql-db]
6. <span data-ttu-id="660f3-130">When the web app has been created, you will see the new app service blade.</span><span class="sxs-lookup"><span data-stu-id="660f3-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="660f3-131">Click on **Settings** > **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="660f3-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Set deployment credentials][set-deployment-credentials]
8. <span data-ttu-id="660f3-133">To enable FTP publishing, you must provide a user name and password.</span><span class="sxs-lookup"><span data-stu-id="660f3-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="660f3-134">Save the credentials and make a note of the user name and password you create.</span><span class="sxs-lookup"><span data-stu-id="660f3-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Create publishing credentials][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="660f3-136">Build and test your app locally</span><span class="sxs-lookup"><span data-stu-id="660f3-136">Build and test your app locally</span></span>
<span data-ttu-id="660f3-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span><span class="sxs-lookup"><span data-stu-id="660f3-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="660f3-138">Information about previous registrants is displayed in a table.</span><span class="sxs-lookup"><span data-stu-id="660f3-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="660f3-139">Registration information is stored in a MySQL database.</span><span class="sxs-lookup"><span data-stu-id="660f3-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="660f3-140">The app consists of two files:</span><span class="sxs-lookup"><span data-stu-id="660f3-140">The app consists of two files:</span></span>

* <span data-ttu-id="660f3-141">**index.php**: Displays a form for registration and a table containing registrant information.</span><span class="sxs-lookup"><span data-stu-id="660f3-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="660f3-142">**createtable.php**: Creates the MySQL table for the application.</span><span class="sxs-lookup"><span data-stu-id="660f3-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="660f3-143">This file will only be used once.</span><span class="sxs-lookup"><span data-stu-id="660f3-143">This file will only be used once.</span></span>

<span data-ttu-id="660f3-144">To build and run the app locally, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="660f3-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="660f3-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="660f3-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="660f3-146">Create a MySQL database called `registration`.</span><span class="sxs-lookup"><span data-stu-id="660f3-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="660f3-147">You can do this from the MySQL command prompt with this command:</span><span class="sxs-lookup"><span data-stu-id="660f3-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="660f3-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span><span class="sxs-lookup"><span data-stu-id="660f3-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="660f3-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span><span class="sxs-lookup"><span data-stu-id="660f3-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="660f3-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span><span class="sxs-lookup"><span data-stu-id="660f3-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > <span data-ttu-id="660f3-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span><span class="sxs-lookup"><span data-stu-id="660f3-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="660f3-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="660f3-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="660f3-153">This will create the `registration_tbl` table in the database.</span><span class="sxs-lookup"><span data-stu-id="660f3-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="660f3-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span><span class="sxs-lookup"><span data-stu-id="660f3-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="660f3-155">Within the PHP tags, add PHP code for connecting to the database.</span><span class="sxs-lookup"><span data-stu-id="660f3-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="660f3-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span><span class="sxs-lookup"><span data-stu-id="660f3-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="660f3-157">Following the database connection code, add code for inserting registration information into the database.</span><span class="sxs-lookup"><span data-stu-id="660f3-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="660f3-158">Finally, following the code above, add code for retrieving data from the database.</span><span class="sxs-lookup"><span data-stu-id="660f3-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="660f3-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span><span class="sxs-lookup"><span data-stu-id="660f3-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="660f3-160">Get MySQL and FTP connection information</span><span class="sxs-lookup"><span data-stu-id="660f3-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="660f3-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span><span class="sxs-lookup"><span data-stu-id="660f3-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="660f3-162">To get MySQL connection information, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="660f3-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="660f3-163">From the app service web app blade click on the resource group link:</span><span class="sxs-lookup"><span data-stu-id="660f3-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Select Resource Group][select-resourcegroup]
2. <span data-ttu-id="660f3-165">From your resource group, click the database:</span><span class="sxs-lookup"><span data-stu-id="660f3-165">From your resource group, click the database:</span></span>
   
    ![Select database][select-database]
3. <span data-ttu-id="660f3-167">From the database summary, select **Settings** > **Properties**.</span><span class="sxs-lookup"><span data-stu-id="660f3-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Select properties][select-properties]
4. <span data-ttu-id="660f3-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span><span class="sxs-lookup"><span data-stu-id="660f3-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Note properties][note-properties]
5. <span data-ttu-id="660f3-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span><span class="sxs-lookup"><span data-stu-id="660f3-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Download publish profile][download-publish-profile]
6. <span data-ttu-id="660f3-173">Open the `.publishsettings` file in an XML editor.</span><span class="sxs-lookup"><span data-stu-id="660f3-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="660f3-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="660f3-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="660f3-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span><span class="sxs-lookup"><span data-stu-id="660f3-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="660f3-176">Publish your app</span><span class="sxs-lookup"><span data-stu-id="660f3-176">Publish your app</span></span>
<span data-ttu-id="660f3-177">After you have tested your app locally, you can publish it to your web app using FTP.</span><span class="sxs-lookup"><span data-stu-id="660f3-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="660f3-178">However, you first need to update the database connection information in the application.</span><span class="sxs-lookup"><span data-stu-id="660f3-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="660f3-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span><span class="sxs-lookup"><span data-stu-id="660f3-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="660f3-180">Now you are ready to publish your app using FTP.</span><span class="sxs-lookup"><span data-stu-id="660f3-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="660f3-181">Open your FTP client of choice.</span><span class="sxs-lookup"><span data-stu-id="660f3-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="660f3-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span><span class="sxs-lookup"><span data-stu-id="660f3-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="660f3-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span><span class="sxs-lookup"><span data-stu-id="660f3-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="660f3-184">Establish a connection.</span><span class="sxs-lookup"><span data-stu-id="660f3-184">Establish a connection.</span></span>

<span data-ttu-id="660f3-185">After you have connected you will be able to upload and download files as needed.</span><span class="sxs-lookup"><span data-stu-id="660f3-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="660f3-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="660f3-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="660f3-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span><span class="sxs-lookup"><span data-stu-id="660f3-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="660f3-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="660f3-188">Next steps</span></span>
<span data-ttu-id="660f3-189">For more information, see the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="660f3-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png















