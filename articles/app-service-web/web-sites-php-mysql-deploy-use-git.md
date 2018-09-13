---
title: Create a PHP-MySQL web app in Azure App Service and deploy using Git
description: A tutorial that demonstrates how to create a PHP web app that stores data in MySQL and use Git deployment to Azure.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: ''
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: bb0e08a4397fd659ee849f73939e10d895af23a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552941"
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="45671-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span><span class="sxs-lookup"><span data-stu-id="45671-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="45671-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span><span class="sxs-lookup"><span data-stu-id="45671-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="45671-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="45671-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="45671-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span><span class="sxs-lookup"><span data-stu-id="45671-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="45671-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span><span class="sxs-lookup"><span data-stu-id="45671-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="45671-108">You will learn:</span><span class="sxs-lookup"><span data-stu-id="45671-108">You will learn:</span></span>

* <span data-ttu-id="45671-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="45671-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span></span> <span data-ttu-id="45671-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span><span class="sxs-lookup"><span data-stu-id="45671-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="45671-111">How to publish and re-publish your application to Azure using Git.</span><span class="sxs-lookup"><span data-stu-id="45671-111">How to publish and re-publish your application to Azure using Git.</span></span>
* <span data-ttu-id="45671-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span><span class="sxs-lookup"><span data-stu-id="45671-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="45671-113">By following this tutorial, you will build a simple registration web app in PHP.</span><span class="sxs-lookup"><span data-stu-id="45671-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="45671-114">The application will be hosted in Web Apps.</span><span class="sxs-lookup"><span data-stu-id="45671-114">The application will be hosted in Web Apps.</span></span> <span data-ttu-id="45671-115">A screenshot of the completed application is below:</span><span class="sxs-lookup"><span data-stu-id="45671-115">A screenshot of the completed application is below:</span></span>

![Azure PHP web site][running-app]

## <a name="set-up-the-development-environment"></a><span data-ttu-id="45671-117">Set up the development environment</span><span class="sxs-lookup"><span data-stu-id="45671-117">Set up the development environment</span></span>
<span data-ttu-id="45671-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="45671-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="45671-119">Create a web app and set up Git publishing</span><span class="sxs-lookup"><span data-stu-id="45671-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="45671-120">Follow these steps to create a web app and a MySQL database:</span><span class="sxs-lookup"><span data-stu-id="45671-120">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="45671-121">Login to the [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="45671-121">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="45671-122">Click the **New** icon.</span><span class="sxs-lookup"><span data-stu-id="45671-122">Click the **New** icon.</span></span>
3. <span data-ttu-id="45671-123">Click **See All** next to **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="45671-123">Click **See All** next to **Marketplace**.</span></span> 
4. <span data-ttu-id="45671-124">Click **Web + Mobile**, then **Web app + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="45671-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="45671-125">Then, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="45671-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="45671-126">Enter a valid name for your resource group.</span><span class="sxs-lookup"><span data-stu-id="45671-126">Enter a valid name for your resource group.</span></span>
   
    ![Set resource group name][resource-group]
6. <span data-ttu-id="45671-128">Enter values for your new web app.</span><span class="sxs-lookup"><span data-stu-id="45671-128">Enter values for your new web app.</span></span>
   
    ![Create web app][new-web-app]
7. <span data-ttu-id="45671-130">Enter values for your new database, including agreeing to the legal terms.</span><span class="sxs-lookup"><span data-stu-id="45671-130">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Create new MySQL database][new-mysql-db]
8. <span data-ttu-id="45671-132">When the web app has been created, you will see the new web app blade.</span><span class="sxs-lookup"><span data-stu-id="45671-132">When the web app has been created, you will see the new web app blade.</span></span>
9. <span data-ttu-id="45671-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span><span class="sxs-lookup"><span data-stu-id="45671-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Set up Git publishing][setup-publishing]
10. <span data-ttu-id="45671-135">Select **Local Git Repository** for the source.</span><span class="sxs-lookup"><span data-stu-id="45671-135">Select **Local Git Repository** for the source.</span></span>
    
     ![Set up Git repository][setup-repository]
11. <span data-ttu-id="45671-137">To enable Git publishing, you must provide a user name and password.</span><span class="sxs-lookup"><span data-stu-id="45671-137">To enable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="45671-138">Make a note of the user name and password you create.</span><span class="sxs-lookup"><span data-stu-id="45671-138">Make a note of the user name and password you create.</span></span> <span data-ttu-id="45671-139">(If you have set up a Git repository before, this step will be skipped.)</span><span class="sxs-lookup"><span data-stu-id="45671-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Create publishing credentials][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="45671-141">Get remote MySQL connection information</span><span class="sxs-lookup"><span data-stu-id="45671-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="45671-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span><span class="sxs-lookup"><span data-stu-id="45671-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="45671-143">To get MySQL connection information, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="45671-143">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="45671-144">From your resource group, click the database:</span><span class="sxs-lookup"><span data-stu-id="45671-144">From your resource group, click the database:</span></span>
   
    ![Select database][select-database]
2. <span data-ttu-id="45671-146">From the database **Settings**, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="45671-146">From the database **Settings**, select **Properties**.</span></span>
   
    ![Select properties][select-properties]
3. <span data-ttu-id="45671-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span><span class="sxs-lookup"><span data-stu-id="45671-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Note properties][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="45671-150">Build and test your app locally</span><span class="sxs-lookup"><span data-stu-id="45671-150">Build and test your app locally</span></span>
<span data-ttu-id="45671-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span><span class="sxs-lookup"><span data-stu-id="45671-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="45671-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span><span class="sxs-lookup"><span data-stu-id="45671-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="45671-153">Information about previous registrants is displayed in a table.</span><span class="sxs-lookup"><span data-stu-id="45671-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="45671-154">Registration information is stored in a MySQL database.</span><span class="sxs-lookup"><span data-stu-id="45671-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="45671-155">The application consists of one file (copy/paste code available below):</span><span class="sxs-lookup"><span data-stu-id="45671-155">The application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="45671-156">**index.php**: Displays a form for registration and a table containing registrant information.</span><span class="sxs-lookup"><span data-stu-id="45671-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="45671-157">To build and run the application locally, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="45671-157">To build and run the application locally, follow the steps below.</span></span> <span data-ttu-id="45671-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="45671-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="45671-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span><span class="sxs-lookup"><span data-stu-id="45671-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="45671-160">The MySQL command prompt will appear:</span><span class="sxs-lookup"><span data-stu-id="45671-160">The MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="45671-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span><span class="sxs-lookup"><span data-stu-id="45671-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="45671-162">In the root of your local application folder create **index.php** file.</span><span class="sxs-lookup"><span data-stu-id="45671-162">In the root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="45671-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span><span class="sxs-lookup"><span data-stu-id="45671-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="45671-164">In a terminal go to your application folder and type the following command:</span><span class="sxs-lookup"><span data-stu-id="45671-164">In a terminal go to your application folder and type the following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="45671-165">You can now browse to **http://localhost:8000/** to test the application.</span><span class="sxs-lookup"><span data-stu-id="45671-165">You can now browse to **http://localhost:8000/** to test the application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="45671-166">Publish your app</span><span class="sxs-lookup"><span data-stu-id="45671-166">Publish your app</span></span>
<span data-ttu-id="45671-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span><span class="sxs-lookup"><span data-stu-id="45671-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span></span> <span data-ttu-id="45671-168">You will initialize your local Git repository and publish the application.</span><span class="sxs-lookup"><span data-stu-id="45671-168">You will initialize your local Git repository and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="45671-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span><span class="sxs-lookup"><span data-stu-id="45671-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="45671-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="45671-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span></span>
2. <span data-ttu-id="45671-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="45671-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="45671-172">You will be prompted for the password you created earlier.</span><span class="sxs-lookup"><span data-stu-id="45671-172">You will be prompted for the password you created earlier.</span></span>
   
    ![Initial Push to Azure via Git][git-initial-push]
3. <span data-ttu-id="45671-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span><span class="sxs-lookup"><span data-stu-id="45671-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span></span>
   
    ![Azure PHP web site][running-app]

<span data-ttu-id="45671-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span><span class="sxs-lookup"><span data-stu-id="45671-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span></span>

## <a name="publish-changes-to-your-app"></a><span data-ttu-id="45671-177">Publish changes to your app</span><span class="sxs-lookup"><span data-stu-id="45671-177">Publish changes to your app</span></span>
<span data-ttu-id="45671-178">To publish changes to your app, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="45671-178">To publish changes to your app, follow these steps:</span></span>

1. <span data-ttu-id="45671-179">Make changes to your app locally.</span><span class="sxs-lookup"><span data-stu-id="45671-179">Make changes to your app locally.</span></span>
2. <span data-ttu-id="45671-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="45671-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="45671-181">You will be prompted for the password you created earlier.</span><span class="sxs-lookup"><span data-stu-id="45671-181">You will be prompted for the password you created earlier.</span></span>
   
    ![Pushing site changes to Azure via Git][git-change-push]
3. <span data-ttu-id="45671-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span><span class="sxs-lookup"><span data-stu-id="45671-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span></span>
   
    ![Azure PHP web site][running-app]

> [!NOTE]
> <span data-ttu-id="45671-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="45671-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="45671-186">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="45671-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a><span data-ttu-id="45671-187">Enable Composer automation with the Composer extension</span><span class="sxs-lookup"><span data-stu-id="45671-187">Enable Composer automation with the Composer extension</span></span>
<span data-ttu-id="45671-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span><span class="sxs-lookup"><span data-stu-id="45671-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="45671-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span><span class="sxs-lookup"><span data-stu-id="45671-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

1. <span data-ttu-id="45671-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="45671-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Composer Extension Settings][composer-extension-settings]
2. <span data-ttu-id="45671-192">Click **Add**, then click **Composer**.</span><span class="sxs-lookup"><span data-stu-id="45671-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Composer Extension Add][composer-extension-add]
3. <span data-ttu-id="45671-194">Click **OK** to accept legal terms.</span><span class="sxs-lookup"><span data-stu-id="45671-194">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="45671-195">Click **OK** again to add the extension.</span><span class="sxs-lookup"><span data-stu-id="45671-195">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="45671-196">The **Installed extensions** blade will now show the Composer extension.</span><span class="sxs-lookup"><span data-stu-id="45671-196">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="45671-197">![Composer Extension View][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="45671-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="45671-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span><span class="sxs-lookup"><span data-stu-id="45671-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="45671-199">You'll now see that Composer is installing dependencies defined in composer.json.</span><span class="sxs-lookup"><span data-stu-id="45671-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Composer Extension Success][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="45671-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="45671-201">Next steps</span></span>
<span data-ttu-id="45671-202">For more information, see the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="45671-202">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png





















