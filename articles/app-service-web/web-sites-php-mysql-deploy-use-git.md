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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Create a PHP-MySQL web app in Azure App Service and deploy using Git
This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git. You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer. The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux. Upon completing this guide, you will have a PHP/MySQL web app running in Azure.

You will learn:

* How to create a web app and a MySQL database using the [Azure Portal][management-portal]. Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.
* How to publish and re-publish your application to Azure using Git.
* How to enable the Composer extension to automate Composer tasks at every `git push`.

By following this tutorial, you will build a simple registration web app in PHP. The application will be hosted in Web Apps. A screenshot of the completed application is below:

![Azure PHP web site][running-app]

## <a name="set-up-the-development-environment"></a>Set up the development environment
This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Create a web app and set up Git publishing
Follow these steps to create a web app and a MySQL database:

1. Login to the [Azure Portal][management-portal].
2. Click the **New** icon.
3. Click **See All** next to **Marketplace**. 
4. Click **Web + Mobile**, then **Web app + MySQL**. Then, click **Create**.
5. Enter a valid name for your resource group.
   
    ![Set resource group name][resource-group]
6. Enter values for your new web app.
   
    ![Create web app][new-web-app]
7. Enter values for your new database, including agreeing to the legal terms.
   
    ![Create new MySQL database][new-mysql-db]
8. When the web app has been created, you will see the new web app blade.
9. In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.
   
    ![Set up Git publishing][setup-publishing]
10. Select **Local Git Repository** for the source.
    
     ![Set up Git repository][setup-repository]
11. To enable Git publishing, you must provide a user name and password. Make a note of the user name and password you create. (If you have set up a Git repository before, this step will be skipped.)
    
     ![Create publishing credentials][credentials]

## <a name="get-remote-mysql-connection-information"></a>Get remote MySQL connection information
To connect to the MySQL database that is running in Web Apps, your will need the connection information. To get MySQL connection information, follow these steps:

1. From your resource group, click the database:
   
    ![Select database][select-database]
2. From the database **Settings**, select **Properties**.
   
    ![Select properties][select-properties]
3. Make note of the values for `Database`, `Host`, `User Id`, and `Password`.
   
    ![Note properties][note-properties]

## <a name="build-and-test-your-app-locally"></a>Build and test your app locally
Now that you have created a web app, you can develop your application locally, then deploy it after testing.

The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address. Information about previous registrants is displayed in a table. Registration information is stored in a MySQL database. The application consists of one file (copy/paste code available below):

* **index.php**: Displays a form for registration and a table containing registrant information.

To build and run the application locally, follow the steps below. Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].

1. Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. The MySQL command prompt will appear:
   
        mysql>
3. Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. In the root of your local application folder create **index.php** file.
5. Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.

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

1. In a terminal go to your application folder and type the following command:
   
       php -S localhost:8000

You can now browse to **http://localhost:8000/** to test the application.

## <a name="publish-your-app"></a>Publish your app
After you have tested your app locally, you can publish it to Web Apps using Git. You will initialize your local Git repository and publish the application.

> [!NOTE]
> These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.
> 
> 

1. (Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.
2. Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    You will be prompted for the password you created earlier.
   
    ![Initial Push to Azure via Git][git-initial-push]
3. Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):
   
    ![Azure PHP web site][running-app]

After you have published your app, you can begin making changes to it and use Git to publish them.

## <a name="publish-changes-to-your-app"></a>Publish changes to your app
To publish changes to your app, follow these steps:

1. Make changes to your app locally.
2. Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    You will be prompted for the password you created earlier.
   
    ![Pushing site changes to Azure via Git][git-change-push]
3. Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:
   
    ![Azure PHP web site][running-app]

> [!NOTE]
> If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service. No credit cards required; no commitments.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a>Enable Composer automation with the Composer extension
By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project. You can enable composer.json processing during `git push` by enabling the Composer extension.

1. In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.
   
    ![Composer Extension Settings][composer-extension-settings]
2. Click **Add**, then click **Composer**.
   
    ![Composer Extension Add][composer-extension-add]
3. Click **OK** to accept legal terms. Click **OK** again to add the extension.
   
    The **Installed extensions** blade will now show the Composer extension.  
    ![Composer Extension View][composer-extension-view]
4. Now, perform `git add`, `git commit`, and `git push` like in the previous section. You'll now see that Composer is installing dependencies defined in composer.json.
   
    ![Composer Extension Success][composer-extension-success]

## <a name="next-steps"></a>Next steps
For more information, see the [PHP Developer Center](/develop/php/).

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





















