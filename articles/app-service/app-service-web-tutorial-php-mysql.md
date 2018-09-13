---
title: Build a PHP and MySQL web app in Azure | Microsoft Docs
description: Learn how to get a PHP app working in Azure, with connection to a MySQL database in Azure.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: ''
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 10/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: b14163bfb9a5e6265158db39e98cb9b31ccef021
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870145"
---
# <a name="tutorial-build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="4da73-103">Tutorial: Build a PHP and MySQL web app in Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-103">Tutorial: Build a PHP and MySQL web app in Azure</span></span>

> [!NOTE]
> <span data-ttu-id="4da73-104">This article deploys an app to App Service on Windows.</span><span class="sxs-lookup"><span data-stu-id="4da73-104">This article deploys an app to App Service on Windows.</span></span> <span data-ttu-id="4da73-105">To deploy to App Service on _Linux_, see [Build a PHP and MySQL web app in Azure App Service on Linux](./containers/tutorial-php-mysql-app.md).</span><span class="sxs-lookup"><span data-stu-id="4da73-105">To deploy to App Service on _Linux_, see [Build a PHP and MySQL web app in Azure App Service on Linux](./containers/tutorial-php-mysql-app.md).</span></span>
>

<span data-ttu-id="4da73-106">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="4da73-106">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="4da73-107">This tutorial shows how to create a PHP web app in Azure and connect it to a MySQL database.</span><span class="sxs-lookup"><span data-stu-id="4da73-107">This tutorial shows how to create a PHP web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="4da73-108">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="4da73-108">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![PHP app running in Azure App Service](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="4da73-110">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="4da73-110">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4da73-111">Create a MySQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-111">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="4da73-112">Connect a PHP app to MySQL</span><span class="sxs-lookup"><span data-stu-id="4da73-112">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="4da73-113">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-113">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4da73-114">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="4da73-114">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="4da73-115">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-115">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="4da73-116">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4da73-116">Manage the app in the Azure portal</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="4da73-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4da73-117">Prerequisites</span></span>

<span data-ttu-id="4da73-118">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="4da73-118">To complete this tutorial:</span></span>

* [<span data-ttu-id="4da73-119">Install Git</span><span class="sxs-lookup"><span data-stu-id="4da73-119">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="4da73-120">Install PHP 5.6.4 or above</span><span class="sxs-lookup"><span data-stu-id="4da73-120">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="4da73-121">Install Composer</span><span class="sxs-lookup"><span data-stu-id="4da73-121">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="4da73-122">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="4da73-122">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="4da73-123">Install and start MySQL</span><span class="sxs-lookup"><span data-stu-id="4da73-123">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

## <a name="prepare-local-mysql"></a><span data-ttu-id="4da73-124">Prepare local MySQL</span><span class="sxs-lookup"><span data-stu-id="4da73-124">Prepare local MySQL</span></span>

<span data-ttu-id="4da73-125">In this step, you create a database in your local MySQL server for your use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4da73-125">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-to-local-mysql-server"></a><span data-ttu-id="4da73-126">Connect to local MySQL server</span><span class="sxs-lookup"><span data-stu-id="4da73-126">Connect to local MySQL server</span></span>

<span data-ttu-id="4da73-127">In a terminal window, connect to your local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="4da73-127">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="4da73-128">You can use this terminal window to run all the commands in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4da73-128">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="4da73-129">If you're prompted for a password, enter the password for the `root` account.</span><span class="sxs-lookup"><span data-stu-id="4da73-129">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="4da73-130">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="4da73-130">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="4da73-131">If your command runs successfully, then your MySQL server is running.</span><span class="sxs-lookup"><span data-stu-id="4da73-131">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="4da73-132">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="4da73-132">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="4da73-133">Create a database locally</span><span class="sxs-lookup"><span data-stu-id="4da73-133">Create a database locally</span></span>

<span data-ttu-id="4da73-134">At the `mysql` prompt, create a database.</span><span class="sxs-lookup"><span data-stu-id="4da73-134">At the `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="4da73-135">Exit your server connection by typing `quit`.</span><span class="sxs-lookup"><span data-stu-id="4da73-135">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="4da73-136">Create a PHP app locally</span><span class="sxs-lookup"><span data-stu-id="4da73-136">Create a PHP app locally</span></span>
<span data-ttu-id="4da73-137">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span><span class="sxs-lookup"><span data-stu-id="4da73-137">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="4da73-138">Clone the sample</span><span class="sxs-lookup"><span data-stu-id="4da73-138">Clone the sample</span></span>

<span data-ttu-id="4da73-139">In the terminal window, `cd` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="4da73-139">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="4da73-140">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="4da73-140">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="4da73-141">`cd` to your cloned directory.</span><span class="sxs-lookup"><span data-stu-id="4da73-141">`cd` to your cloned directory.</span></span>
<span data-ttu-id="4da73-142">Install the required packages.</span><span class="sxs-lookup"><span data-stu-id="4da73-142">Install the required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="4da73-143">Configure MySQL connection</span><span class="sxs-lookup"><span data-stu-id="4da73-143">Configure MySQL connection</span></span>

<span data-ttu-id="4da73-144">In the repository root, create a text file named *.env*.</span><span class="sxs-lookup"><span data-stu-id="4da73-144">In the repository root, create a text file named *.env*.</span></span> <span data-ttu-id="4da73-145">Copy the following variables into the *.env* file.</span><span class="sxs-lookup"><span data-stu-id="4da73-145">Copy the following variables into the *.env* file.</span></span> <span data-ttu-id="4da73-146">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span><span class="sxs-lookup"><span data-stu-id="4da73-146">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="4da73-147">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="4da73-147">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-the-sample-locally"></a><span data-ttu-id="4da73-148">Run the sample locally</span><span class="sxs-lookup"><span data-stu-id="4da73-148">Run the sample locally</span></span>

<span data-ttu-id="4da73-149">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span><span class="sxs-lookup"><span data-stu-id="4da73-149">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span></span> <span data-ttu-id="4da73-150">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span><span class="sxs-lookup"><span data-stu-id="4da73-150">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="4da73-151">Generate a new Laravel application key.</span><span class="sxs-lookup"><span data-stu-id="4da73-151">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="4da73-152">Run the application.</span><span class="sxs-lookup"><span data-stu-id="4da73-152">Run the application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="4da73-153">Navigate to `http://localhost:8000` in a browser.</span><span class="sxs-lookup"><span data-stu-id="4da73-153">Navigate to `http://localhost:8000` in a browser.</span></span> <span data-ttu-id="4da73-154">Add a few tasks in the page.</span><span class="sxs-lookup"><span data-stu-id="4da73-154">Add a few tasks in the page.</span></span>

![PHP connects successfully to MySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="4da73-156">To stop the PHP server, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="4da73-156">To stop the PHP server, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="4da73-157">Create MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-157">Create MySQL in Azure</span></span>

<span data-ttu-id="4da73-158">In this step, you create a MySQL database in [Azure Database for MySQL](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="4da73-158">In this step, you create a MySQL database in [Azure Database for MySQL](/azure/mysql).</span></span> <span data-ttu-id="4da73-159">Later, you configure the PHP application to connect to this database.</span><span class="sxs-lookup"><span data-stu-id="4da73-159">Later, you configure the PHP application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="4da73-160">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="4da73-160">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="4da73-161">Create a MySQL server</span><span class="sxs-lookup"><span data-stu-id="4da73-161">Create a MySQL server</span></span>

<span data-ttu-id="4da73-162">In the Cloud Shell, create a server in Azure Database for MySQL with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span><span class="sxs-lookup"><span data-stu-id="4da73-162">In the Cloud Shell, create a server in Azure Database for MySQL with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span></span>

<span data-ttu-id="4da73-163">In the following command, substitute a unique server name for the *\<mysql_server_name>* placeholder, a user name for the *\<admin_user>*, and a password for the *\<admin_password>*  placeholder.</span><span class="sxs-lookup"><span data-stu-id="4da73-163">In the following command, substitute a unique server name for the *\<mysql_server_name>* placeholder, a user name for the *\<admin_user>*, and a password for the *\<admin_password>*  placeholder.</span></span> <span data-ttu-id="4da73-164">The server name is used as part of your MySQL endpoint (`https://<mysql_server_name>.mysql.database.azure.com`), so the name needs to be unique across all servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="4da73-164">The server name is used as part of your MySQL endpoint (`https://<mysql_server_name>.mysql.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span>

```azurecli-interactive
az mysql server create --resource-group myResourceGroup --name <mysql_server_name> --location "West Europe" --admin-user <admin_user> --admin-password <server_admin_password> --sku-name GP_Gen4_2
```

> [!NOTE]
> <span data-ttu-id="4da73-165">Since there are several credentials to think about in this tutorial, to avoid confusion, `--admin-user` and `--admin-password` are set to dummy values.</span><span class="sxs-lookup"><span data-stu-id="4da73-165">Since there are several credentials to think about in this tutorial, to avoid confusion, `--admin-user` and `--admin-password` are set to dummy values.</span></span> <span data-ttu-id="4da73-166">In a production environment, follow security best practices when choosing a good username and password for your MySQL server in Azure.</span><span class="sxs-lookup"><span data-stu-id="4da73-166">In a production environment, follow security best practices when choosing a good username and password for your MySQL server in Azure.</span></span>
>
>

<span data-ttu-id="4da73-167">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="4da73-167">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "location": "westeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "additionalProperties": {},
    "capacity": 2,
    "family": "Gen4",
    "name": "GP_Gen4_2",
    "size": null,
    "tier": "GeneralPurpose"
  },
  "sslEnforcement": "Enabled",
  ...   +  
  -  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="4da73-168">Configure server firewall</span><span class="sxs-lookup"><span data-stu-id="4da73-168">Configure server firewall</span></span>

<span data-ttu-id="4da73-169">In the Cloud Shell, create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az-mysql-server-firewall-rule-create) command.</span><span class="sxs-lookup"><span data-stu-id="4da73-169">In the Cloud Shell, create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az-mysql-server-firewall-rule-create) command.</span></span> <span data-ttu-id="4da73-170">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="4da73-170">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create --name allAzureIPs --server <mysql_server_name> --resource-group myResourceGroup --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP] 
> <span data-ttu-id="4da73-171">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](app-service-ip-addresses.md#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="4da73-171">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](app-service-ip-addresses.md#find-outbound-ips).</span></span>
>

### <a name="connect-to-production-mysql-server-locally"></a><span data-ttu-id="4da73-172">Connect to production MySQL server locally</span><span class="sxs-lookup"><span data-stu-id="4da73-172">Connect to production MySQL server locally</span></span>

<span data-ttu-id="4da73-173">In the local terminal window, connect to the MySQL server in Azure.</span><span class="sxs-lookup"><span data-stu-id="4da73-173">In the local terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="4da73-174">Use the value you specified previously for _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="4da73-174">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span> <span data-ttu-id="4da73-175">When prompted for a password, use the password you specified when you created the database in Azure.</span><span class="sxs-lookup"><span data-stu-id="4da73-175">When prompted for a password, use the password you specified when you created the database in Azure.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com-P 3306 -p
```

### <a name="create-a-production-database"></a><span data-ttu-id="4da73-176">Create a production database</span><span class="sxs-lookup"><span data-stu-id="4da73-176">Create a production database</span></span>

<span data-ttu-id="4da73-177">At the `mysql` prompt, create a database.</span><span class="sxs-lookup"><span data-stu-id="4da73-177">At the `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="4da73-178">Create a user with permissions</span><span class="sxs-lookup"><span data-stu-id="4da73-178">Create a user with permissions</span></span>

<span data-ttu-id="4da73-179">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span><span class="sxs-lookup"><span data-stu-id="4da73-179">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span></span> <span data-ttu-id="4da73-180">Again, for simplicity of the tutorial, use _MySQLAzure2017_ as the password.</span><span class="sxs-lookup"><span data-stu-id="4da73-180">Again, for simplicity of the tutorial, use _MySQLAzure2017_ as the password.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'phpappuser';
```

<span data-ttu-id="4da73-181">Exit the server connection by typing `quit`.</span><span class="sxs-lookup"><span data-stu-id="4da73-181">Exit the server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a><span data-ttu-id="4da73-182">Connect app to Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="4da73-182">Connect app to Azure MySQL</span></span>

<span data-ttu-id="4da73-183">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4da73-183">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL.</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="4da73-184">Configure the database connection</span><span class="sxs-lookup"><span data-stu-id="4da73-184">Configure the database connection</span></span>

<span data-ttu-id="4da73-185">In the repository root, create an _.env.production_ file and copy the following variables into it.</span><span class="sxs-lookup"><span data-stu-id="4da73-185">In the repository root, create an _.env.production_ file and copy the following variables into it.</span></span> <span data-ttu-id="4da73-186">Replace the placeholder _&lt;mysql_server_name>_ in both *DB_HOST* and *DB_USERNAME*.</span><span class="sxs-lookup"><span data-stu-id="4da73-186">Replace the placeholder _&lt;mysql_server_name>_ in both *DB_HOST* and *DB_USERNAME*.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.mysql.database.azure.com
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="4da73-187">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="4da73-187">Save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="4da73-188">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span><span class="sxs-lookup"><span data-stu-id="4da73-188">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span></span> <span data-ttu-id="4da73-189">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4da73-189">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL.</span></span> <span data-ttu-id="4da73-190">With environment variables, you don't need the *.env* file in App Service.</span><span class="sxs-lookup"><span data-stu-id="4da73-190">With environment variables, you don't need the *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="4da73-191">Configure SSL certificate</span><span class="sxs-lookup"><span data-stu-id="4da73-191">Configure SSL certificate</span></span>

<span data-ttu-id="4da73-192">By default, Azure Database for MySQL enforces SSL connections from clients.</span><span class="sxs-lookup"><span data-stu-id="4da73-192">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="4da73-193">To connect to your MySQL database in Azure, you must use the [_.pem_ certificate supplied by Azure Database for MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="4da73-193">To connect to your MySQL database in Azure, you must use the [_.pem_ certificate supplied by Azure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

<span data-ttu-id="4da73-194">Open _config/database.php_ and add the `sslmode` and `options` parameters to `connections.mysql`, as shown in the following code.</span><span class="sxs-lookup"><span data-stu-id="4da73-194">Open _config/database.php_ and add the `sslmode` and `options` parameters to `connections.mysql`, as shown in the following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/BaltimoreCyberTrustRoot.crt.pem', 
    ] : []
],
```

<span data-ttu-id="4da73-195">The certificate `BaltimoreCyberTrustRoot.crt.pem` is provided in the repository for convenience in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4da73-195">The certificate `BaltimoreCyberTrustRoot.crt.pem` is provided in the repository for convenience in this tutorial.</span></span> 

### <a name="test-the-application-locally"></a><span data-ttu-id="4da73-196">Test the application locally</span><span class="sxs-lookup"><span data-stu-id="4da73-196">Test the application locally</span></span>

<span data-ttu-id="4da73-197">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="4da73-197">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL.</span></span> <span data-ttu-id="4da73-198">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="4da73-198">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="4da73-199">_.env.production_ doesn't have a valid application key yet.</span><span class="sxs-lookup"><span data-stu-id="4da73-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="4da73-200">Generate a new one for it in the terminal.</span><span class="sxs-lookup"><span data-stu-id="4da73-200">Generate a new one for it in the terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="4da73-201">Run the sample application with _.env.production_ as the environment file.</span><span class="sxs-lookup"><span data-stu-id="4da73-201">Run the sample application with _.env.production_ as the environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="4da73-202">Navigate to `http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="4da73-202">Navigate to `http://localhost:8000`.</span></span> <span data-ttu-id="4da73-203">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="4da73-203">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span></span>

<span data-ttu-id="4da73-204">Add a few tasks in the page.</span><span class="sxs-lookup"><span data-stu-id="4da73-204">Add a few tasks in the page.</span></span>

![PHP connects successfully to Azure Database for MySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="4da73-206">To stop PHP, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="4da73-206">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="4da73-207">Commit your changes</span><span class="sxs-lookup"><span data-stu-id="4da73-207">Commit your changes</span></span>

<span data-ttu-id="4da73-208">Run the following Git commands to commit your changes:</span><span class="sxs-lookup"><span data-stu-id="4da73-208">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="4da73-209">Your app is ready to be deployed.</span><span class="sxs-lookup"><span data-stu-id="4da73-209">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="4da73-210">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-210">Deploy to Azure</span></span>

<span data-ttu-id="4da73-211">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4da73-211">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="4da73-212">Configure a deployment user</span><span class="sxs-lookup"><span data-stu-id="4da73-212">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="create-an-app-service-plan"></a><span data-ttu-id="4da73-213">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="4da73-213">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

<a name="create"></a>
### <a name="create-a-web-app"></a><span data-ttu-id="4da73-214">Create a web app</span><span class="sxs-lookup"><span data-stu-id="4da73-214">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-php-no-h.md)] 

### <a name="configure-database-settings"></a><span data-ttu-id="4da73-215">Configure database settings</span><span class="sxs-lookup"><span data-stu-id="4da73-215">Configure database settings</span></span>

<span data-ttu-id="4da73-216">As pointed out previously, you can connect to your Azure MySQL database using environment variables in App Service.</span><span class="sxs-lookup"><span data-stu-id="4da73-216">As pointed out previously, you can connect to your Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="4da73-217">In the Cloud Shell, you set environment variables as _app settings_ by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span><span class="sxs-lookup"><span data-stu-id="4da73-217">In the Cloud Shell, you set environment variables as _app settings_ by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span></span>

<span data-ttu-id="4da73-218">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="4da73-218">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="4da73-219">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="4da73-219">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DB_HOST="<mysql_server_name>.mysql.database.azure.com" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="4da73-220">You can use the PHP [getenv](http://www.php.net/manual/function.getenv.php) method to access the settings.</span><span class="sxs-lookup"><span data-stu-id="4da73-220">You can use the PHP [getenv](http://www.php.net/manual/function.getenv.php) method to access the settings.</span></span> <span data-ttu-id="4da73-221">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="4da73-221">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span></span> <span data-ttu-id="4da73-222">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span><span class="sxs-lookup"><span data-stu-id="4da73-222">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="4da73-223">Configure Laravel environment variables</span><span class="sxs-lookup"><span data-stu-id="4da73-223">Configure Laravel environment variables</span></span>

<span data-ttu-id="4da73-224">Laravel needs an application key in App Service.</span><span class="sxs-lookup"><span data-stu-id="4da73-224">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="4da73-225">You can configure it with app settings.</span><span class="sxs-lookup"><span data-stu-id="4da73-225">You can configure it with app settings.</span></span>

<span data-ttu-id="4da73-226">In the local terminal window, use `php artisan` to generate a new application key without saving it to _.env_.</span><span class="sxs-lookup"><span data-stu-id="4da73-226">In the local terminal window, use `php artisan` to generate a new application key without saving it to _.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="4da73-227">In the Cloud Shell, set the application key in the App Service web app by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span><span class="sxs-lookup"><span data-stu-id="4da73-227">In the Cloud Shell, set the application key in the App Service web app by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span></span> <span data-ttu-id="4da73-228">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span><span class="sxs-lookup"><span data-stu-id="4da73-228">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="4da73-229">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span><span class="sxs-lookup"><span data-stu-id="4da73-229">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span></span> <span data-ttu-id="4da73-230">When running a production application, set it to `false`, which is more secure.</span><span class="sxs-lookup"><span data-stu-id="4da73-230">When running a production application, set it to `false`, which is more secure.</span></span>

### <a name="set-the-virtual-application-path"></a><span data-ttu-id="4da73-231">Set the virtual application path</span><span class="sxs-lookup"><span data-stu-id="4da73-231">Set the virtual application path</span></span>

<span data-ttu-id="4da73-232">Set the virtual application path for the web app.</span><span class="sxs-lookup"><span data-stu-id="4da73-232">Set the virtual application path for the web app.</span></span> <span data-ttu-id="4da73-233">This step is required because the [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in the _public_ directory instead of the application's root directory.</span><span class="sxs-lookup"><span data-stu-id="4da73-233">This step is required because the [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in the _public_ directory instead of the application's root directory.</span></span> <span data-ttu-id="4da73-234">Other PHP frameworks whose lifecycle start in the root directory can work without manual configuration of the virtual application path.</span><span class="sxs-lookup"><span data-stu-id="4da73-234">Other PHP frameworks whose lifecycle start in the root directory can work without manual configuration of the virtual application path.</span></span>

<span data-ttu-id="4da73-235">In the Cloud Shell, set the virtual application path by using the [`az resource update`](/cli/azure/resource#az-resource-update) command.</span><span class="sxs-lookup"><span data-stu-id="4da73-235">In the Cloud Shell, set the virtual application path by using the [`az resource update`](/cli/azure/resource#az-resource-update) command.</span></span> <span data-ttu-id="4da73-236">Replace the _&lt;appname>_ placeholder.</span><span class="sxs-lookup"><span data-stu-id="4da73-236">Replace the _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update --name web --resource-group myResourceGroup --namespace Microsoft.Web --resource-type config --parent sites/<app_name> --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" --api-version 2015-06-01
```

<span data-ttu-id="4da73-237">By default, Azure App Service points the root virtual application path (_/_) to the root directory of the deployed application files (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="4da73-237">By default, Azure App Service points the root virtual application path (_/_) to the root directory of the deployed application files (_sites\wwwroot_).</span></span>

### <a name="push-to-azure-from-git"></a><span data-ttu-id="4da73-238">Push to Azure from Git</span><span class="sxs-lookup"><span data-stu-id="4da73-238">Push to Azure from Git</span></span>

[!INCLUDE [app-service-plan-no-h](../../includes/app-service-web-git-push-to-azure-no-h.md)]

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="4da73-239">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span><span class="sxs-lookup"><span data-stu-id="4da73-239">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span></span> <span data-ttu-id="4da73-240">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span><span class="sxs-lookup"><span data-stu-id="4da73-240">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span></span>
>
> - <span data-ttu-id="4da73-241">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="4da73-241">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="4da73-242">`deploy.sh` - The custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="4da73-242">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="4da73-243">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span><span class="sxs-lookup"><span data-stu-id="4da73-243">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="4da73-244">`composer.phar` - The Composer package manager.</span><span class="sxs-lookup"><span data-stu-id="4da73-244">`composer.phar` - The Composer package manager.</span></span>
>
> <span data-ttu-id="4da73-245">You can use this approach to add any step to your Git-based deployment to App Service.</span><span class="sxs-lookup"><span data-stu-id="4da73-245">You can use this approach to add any step to your Git-based deployment to App Service.</span></span> <span data-ttu-id="4da73-246">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="4da73-246">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="4da73-247">Browse to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="4da73-247">Browse to the Azure web app</span></span>

<span data-ttu-id="4da73-248">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span><span class="sxs-lookup"><span data-stu-id="4da73-248">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![PHP app running in Azure App Service](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="4da73-250">Congratulations, you're running a data-driven PHP app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4da73-250">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="4da73-251">Update model locally and redeploy</span><span class="sxs-lookup"><span data-stu-id="4da73-251">Update model locally and redeploy</span></span>

<span data-ttu-id="4da73-252">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span><span class="sxs-lookup"><span data-stu-id="4da73-252">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="4da73-253">For the tasks scenario, you modify the application so that you can mark a task as complete.</span><span class="sxs-lookup"><span data-stu-id="4da73-253">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="4da73-254">Add a column</span><span class="sxs-lookup"><span data-stu-id="4da73-254">Add a column</span></span>

<span data-ttu-id="4da73-255">In the local terminal window, navigate to the root of the Git repository.</span><span class="sxs-lookup"><span data-stu-id="4da73-255">In the local terminal window, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="4da73-256">Generate a new database migration for the `tasks` table:</span><span class="sxs-lookup"><span data-stu-id="4da73-256">Generate a new database migration for the `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="4da73-257">This command shows you the name of the migration file that's generated.</span><span class="sxs-lookup"><span data-stu-id="4da73-257">This command shows you the name of the migration file that's generated.</span></span> <span data-ttu-id="4da73-258">Find this file in _database/migrations_ and open it.</span><span class="sxs-lookup"><span data-stu-id="4da73-258">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="4da73-259">Replace the `up` method with the following code:</span><span class="sxs-lookup"><span data-stu-id="4da73-259">Replace the `up` method with the following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="4da73-260">The preceding code adds a boolean column in the `tasks` table called `complete`.</span><span class="sxs-lookup"><span data-stu-id="4da73-260">The preceding code adds a boolean column in the `tasks` table called `complete`.</span></span>

<span data-ttu-id="4da73-261">Replace the `down` method with the following code for the rollback action:</span><span class="sxs-lookup"><span data-stu-id="4da73-261">Replace the `down` method with the following code for the rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="4da73-262">In the local terminal window, run Laravel database migrations to make the change in the local database.</span><span class="sxs-lookup"><span data-stu-id="4da73-262">In the local terminal window, run Laravel database migrations to make the change in the local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="4da73-263">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span><span class="sxs-lookup"><span data-stu-id="4da73-263">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="4da73-264">Update application logic</span><span class="sxs-lookup"><span data-stu-id="4da73-264">Update application logic</span></span>

<span data-ttu-id="4da73-265">Open the *routes/web.php* file.</span><span class="sxs-lookup"><span data-stu-id="4da73-265">Open the *routes/web.php* file.</span></span> <span data-ttu-id="4da73-266">The application defines its routes and business logic here.</span><span class="sxs-lookup"><span data-stu-id="4da73-266">The application defines its routes and business logic here.</span></span>

<span data-ttu-id="4da73-267">At the end of the file, add a route with the following code:</span><span class="sxs-lookup"><span data-stu-id="4da73-267">At the end of the file, add a route with the following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="4da73-268">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span><span class="sxs-lookup"><span data-stu-id="4da73-268">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span></span>

### <a name="update-the-view"></a><span data-ttu-id="4da73-269">Update the view</span><span class="sxs-lookup"><span data-stu-id="4da73-269">Update the view</span></span>

<span data-ttu-id="4da73-270">Open the *resources/views/tasks.blade.php* file.</span><span class="sxs-lookup"><span data-stu-id="4da73-270">Open the *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="4da73-271">Search for the `<tr>` opening tag and replace it with:</span><span class="sxs-lookup"><span data-stu-id="4da73-271">Search for the `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="4da73-272">The preceding code changes the row color depending on whether the task is complete.</span><span class="sxs-lookup"><span data-stu-id="4da73-272">The preceding code changes the row color depending on whether the task is complete.</span></span>

<span data-ttu-id="4da73-273">In the next line, you have the following code:</span><span class="sxs-lookup"><span data-stu-id="4da73-273">In the next line, you have the following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="4da73-274">Replace the entire line with the following code:</span><span class="sxs-lookup"><span data-stu-id="4da73-274">Replace the entire line with the following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="4da73-275">The preceding code adds the submit button that references the route that you defined earlier.</span><span class="sxs-lookup"><span data-stu-id="4da73-275">The preceding code adds the submit button that references the route that you defined earlier.</span></span>

### <a name="test-the-changes-locally"></a><span data-ttu-id="4da73-276">Test the changes locally</span><span class="sxs-lookup"><span data-stu-id="4da73-276">Test the changes locally</span></span>

<span data-ttu-id="4da73-277">In the local terminal window, run the development server from the root directory of the Git repository.</span><span class="sxs-lookup"><span data-stu-id="4da73-277">In the local terminal window, run the development server from the root directory of the Git repository.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="4da73-278">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span><span class="sxs-lookup"><span data-stu-id="4da73-278">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span></span>

![Added check box to task](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="4da73-280">To stop PHP, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="4da73-280">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="4da73-281">Publish changes to Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-281">Publish changes to Azure</span></span>

<span data-ttu-id="4da73-282">In the local terminal window, run Laravel database migrations with the production connection string to make the change in the Azure database.</span><span class="sxs-lookup"><span data-stu-id="4da73-282">In the local terminal window, run Laravel database migrations with the production connection string to make the change in the Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="4da73-283">Commit all the changes in Git, and then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="4da73-283">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="4da73-284">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span><span class="sxs-lookup"><span data-stu-id="4da73-284">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![Model and database changes published to Azure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="4da73-286">If you added any tasks, they are retained in the database.</span><span class="sxs-lookup"><span data-stu-id="4da73-286">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="4da73-287">Updates to the data schema leave existing data intact.</span><span class="sxs-lookup"><span data-stu-id="4da73-287">Updates to the data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="4da73-288">Stream diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="4da73-288">Stream diagnostic logs</span></span>

<span data-ttu-id="4da73-289">While the PHP application runs in Azure App Service, you can get the console logs piped to your terminal.</span><span class="sxs-lookup"><span data-stu-id="4da73-289">While the PHP application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="4da73-290">That way, you can get the same diagnostic messages to help you debug application errors.</span><span class="sxs-lookup"><span data-stu-id="4da73-290">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="4da73-291">To start log streaming, use the [`az webapp log tail`](/cli/azure/webapp/log?view=azure-cli-latest#az-webapp-log-tail) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="4da73-291">To start log streaming, use the [`az webapp log tail`](/cli/azure/webapp/log?view=azure-cli-latest#az-webapp-log-tail) command in the Cloud Shell.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="4da73-292">Once log streaming has started, refresh the Azure web app in the browser to get some web traffic.</span><span class="sxs-lookup"><span data-stu-id="4da73-292">Once log streaming has started, refresh the Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="4da73-293">You can now see console logs piped to the terminal.</span><span class="sxs-lookup"><span data-stu-id="4da73-293">You can now see console logs piped to the terminal.</span></span> <span data-ttu-id="4da73-294">If you don't see console logs immediately, check again in 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="4da73-294">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="4da73-295">To stop log streaming at anytime, type `Ctrl`+`C`.</span><span class="sxs-lookup"><span data-stu-id="4da73-295">To stop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="4da73-296">A PHP application can use the standard [error_log()](http://php.net/manual/function.error-log.php) to output to the console.</span><span class="sxs-lookup"><span data-stu-id="4da73-296">A PHP application can use the standard [error_log()](http://php.net/manual/function.error-log.php) to output to the console.</span></span> <span data-ttu-id="4da73-297">The sample application uses this approach in _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="4da73-297">The sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="4da73-298">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as the logging provider.</span><span class="sxs-lookup"><span data-stu-id="4da73-298">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as the logging provider.</span></span> <span data-ttu-id="4da73-299">To see how to get Monolog to output messages to the console, see [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="4da73-299">To see how to get Monolog to output messages to the console, see [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="4da73-300">Manage the Azure web app</span><span class="sxs-lookup"><span data-stu-id="4da73-300">Manage the Azure web app</span></span>

<span data-ttu-id="4da73-301">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="4da73-301">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="4da73-302">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="4da73-302">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="4da73-304">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="4da73-304">You see your web app's Overview page.</span></span> <span data-ttu-id="4da73-305">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span><span class="sxs-lookup"><span data-stu-id="4da73-305">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="4da73-306">The left menu provides pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="4da73-306">The left menu provides pages for configuring your app.</span></span>

![App Service page in Azure portal](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="4da73-308">Next steps</span><span class="sxs-lookup"><span data-stu-id="4da73-308">Next steps</span></span>

<span data-ttu-id="4da73-309">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="4da73-309">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4da73-310">Create a MySQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-310">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="4da73-311">Connect a PHP app to MySQL</span><span class="sxs-lookup"><span data-stu-id="4da73-311">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="4da73-312">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-312">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4da73-313">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="4da73-313">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="4da73-314">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="4da73-314">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="4da73-315">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4da73-315">Manage the app in the Azure portal</span></span>

<span data-ttu-id="4da73-316">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span><span class="sxs-lookup"><span data-stu-id="4da73-316">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4da73-317">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="4da73-317">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
