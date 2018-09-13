---
title: Build a PHP and MySQL web app in Azure App Service on Linux | Microsoft Docs
description: Learn how to get a PHP app working in Azure, with connection to a MySQL database in Azure.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
ms.service: app-service-web
ms.workload: web
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 11/28/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5b02f8f71299f2ff4f88cf63481d761afc2c5f49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865418"
---
# <a name="build-a-php-and-mysql-web-app-in-azure-app-service-on-linux"></a><span data-ttu-id="6e23d-103">Build a PHP and MySQL web app in Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="6e23d-103">Build a PHP and MySQL web app in Azure App Service on Linux</span></span>

> [!NOTE]
> <span data-ttu-id="6e23d-104">This article deploys an app to App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="6e23d-104">This article deploys an app to App Service on Linux.</span></span> <span data-ttu-id="6e23d-105">To deploy to App Service on _Windows_, see [Build a PHP and MySQL web app in Azure](../app-service-web-tutorial-php-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="6e23d-105">To deploy to App Service on _Windows_, see [Build a PHP and MySQL web app in Azure](../app-service-web-tutorial-php-mysql.md).</span></span>
>

<span data-ttu-id="6e23d-106">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="6e23d-106">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="6e23d-107">This tutorial shows how to create a PHP web app and connect it to a MySQL database.</span><span class="sxs-lookup"><span data-stu-id="6e23d-107">This tutorial shows how to create a PHP web app and connect it to a MySQL database.</span></span> <span data-ttu-id="6e23d-108">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="6e23d-108">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on App Service on Linux.</span></span>

![PHP app running in Azure App Service](./media/tutorial-php-mysql-app/complete-checkbox-published.png)

<span data-ttu-id="6e23d-110">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="6e23d-110">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e23d-111">Create a MySQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-111">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="6e23d-112">Connect a PHP app to MySQL</span><span class="sxs-lookup"><span data-stu-id="6e23d-112">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="6e23d-113">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-113">Deploy the app to Azure</span></span>
> * <span data-ttu-id="6e23d-114">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="6e23d-114">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="6e23d-115">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-115">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="6e23d-116">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e23d-116">Manage the app in the Azure portal</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="6e23d-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6e23d-117">Prerequisites</span></span>

<span data-ttu-id="6e23d-118">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="6e23d-118">To complete this tutorial:</span></span>

* [<span data-ttu-id="6e23d-119">Install Git</span><span class="sxs-lookup"><span data-stu-id="6e23d-119">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="6e23d-120">Install PHP 5.6.4 or above</span><span class="sxs-lookup"><span data-stu-id="6e23d-120">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="6e23d-121">Install Composer</span><span class="sxs-lookup"><span data-stu-id="6e23d-121">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="6e23d-122">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="6e23d-122">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="6e23d-123">Install and start MySQL</span><span class="sxs-lookup"><span data-stu-id="6e23d-123">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

## <a name="prepare-local-mysql"></a><span data-ttu-id="6e23d-124">Prepare local MySQL</span><span class="sxs-lookup"><span data-stu-id="6e23d-124">Prepare local MySQL</span></span>

<span data-ttu-id="6e23d-125">In this step, you create a database in your local MySQL server for your use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e23d-125">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-to-local-mysql-server"></a><span data-ttu-id="6e23d-126">Connect to local MySQL server</span><span class="sxs-lookup"><span data-stu-id="6e23d-126">Connect to local MySQL server</span></span>

<span data-ttu-id="6e23d-127">In a terminal window, connect to your local MySQL server.</span><span class="sxs-lookup"><span data-stu-id="6e23d-127">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="6e23d-128">You can use this terminal window to run all the commands in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e23d-128">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="6e23d-129">If you're prompted for a password, enter the password for the `root` account.</span><span class="sxs-lookup"><span data-stu-id="6e23d-129">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="6e23d-130">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="6e23d-130">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="6e23d-131">If your command runs successfully, then your MySQL server is running.</span><span class="sxs-lookup"><span data-stu-id="6e23d-131">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="6e23d-132">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="6e23d-132">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="6e23d-133">Create a database locally</span><span class="sxs-lookup"><span data-stu-id="6e23d-133">Create a database locally</span></span>

<span data-ttu-id="6e23d-134">At the `mysql` prompt, create a database.</span><span class="sxs-lookup"><span data-stu-id="6e23d-134">At the `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="6e23d-135">Exit your server connection by typing `quit`.</span><span class="sxs-lookup"><span data-stu-id="6e23d-135">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="6e23d-136">Create a PHP app locally</span><span class="sxs-lookup"><span data-stu-id="6e23d-136">Create a PHP app locally</span></span>
<span data-ttu-id="6e23d-137">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span><span class="sxs-lookup"><span data-stu-id="6e23d-137">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="6e23d-138">Clone the sample</span><span class="sxs-lookup"><span data-stu-id="6e23d-138">Clone the sample</span></span>

<span data-ttu-id="6e23d-139">In the terminal window, `cd` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="6e23d-139">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="6e23d-140">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="6e23d-140">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="6e23d-141">`cd` to your cloned directory.</span><span class="sxs-lookup"><span data-stu-id="6e23d-141">`cd` to your cloned directory.</span></span>
<span data-ttu-id="6e23d-142">Install the required packages.</span><span class="sxs-lookup"><span data-stu-id="6e23d-142">Install the required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="6e23d-143">Configure MySQL connection</span><span class="sxs-lookup"><span data-stu-id="6e23d-143">Configure MySQL connection</span></span>

<span data-ttu-id="6e23d-144">In the repository root, create a file named *.env*.</span><span class="sxs-lookup"><span data-stu-id="6e23d-144">In the repository root, create a file named *.env*.</span></span> <span data-ttu-id="6e23d-145">Copy the following variables into the *.env* file.</span><span class="sxs-lookup"><span data-stu-id="6e23d-145">Copy the following variables into the *.env* file.</span></span> <span data-ttu-id="6e23d-146">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span><span class="sxs-lookup"><span data-stu-id="6e23d-146">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span></span>

```txt
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="6e23d-147">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="6e23d-147">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-the-sample-locally"></a><span data-ttu-id="6e23d-148">Run the sample locally</span><span class="sxs-lookup"><span data-stu-id="6e23d-148">Run the sample locally</span></span>

<span data-ttu-id="6e23d-149">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span><span class="sxs-lookup"><span data-stu-id="6e23d-149">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span></span> <span data-ttu-id="6e23d-150">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span><span class="sxs-lookup"><span data-stu-id="6e23d-150">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="6e23d-151">Generate a new Laravel application key.</span><span class="sxs-lookup"><span data-stu-id="6e23d-151">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="6e23d-152">Run the application.</span><span class="sxs-lookup"><span data-stu-id="6e23d-152">Run the application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="6e23d-153">Navigate to `http://localhost:8000` in a browser.</span><span class="sxs-lookup"><span data-stu-id="6e23d-153">Navigate to `http://localhost:8000` in a browser.</span></span> <span data-ttu-id="6e23d-154">Add a few tasks in the page.</span><span class="sxs-lookup"><span data-stu-id="6e23d-154">Add a few tasks in the page.</span></span>

![PHP connects successfully to MySQL](./media/tutorial-php-mysql-app/mysql-connect-success.png)

<span data-ttu-id="6e23d-156">To stop PHP, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="6e23d-156">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="6e23d-157">Create MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-157">Create MySQL in Azure</span></span>

<span data-ttu-id="6e23d-158">In this step, you create a MySQL database in [Azure Database for MySQL](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="6e23d-158">In this step, you create a MySQL database in [Azure Database for MySQL](/azure/mysql).</span></span> <span data-ttu-id="6e23d-159">Later, you configure the PHP application to connect to this database.</span><span class="sxs-lookup"><span data-stu-id="6e23d-159">Later, you configure the PHP application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="6e23d-160">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="6e23d-160">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="6e23d-161">Create a MySQL server</span><span class="sxs-lookup"><span data-stu-id="6e23d-161">Create a MySQL server</span></span>

<span data-ttu-id="6e23d-162">Create a server in Azure Database for MySQL with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span><span class="sxs-lookup"><span data-stu-id="6e23d-162">Create a server in Azure Database for MySQL with the [`az mysql server create`](/cli/azure/mysql/server?view=azure-cli-latest#az-mysql-server-create) command.</span></span>

<span data-ttu-id="6e23d-163">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span><span class="sxs-lookup"><span data-stu-id="6e23d-163">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="6e23d-164">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span><span class="sxs-lookup"><span data-stu-id="6e23d-164">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> --resource-group myResourceGroup --location "North Europe" --admin-user adminuser --admin-password My5up3r$tr0ngPa$w0rd!
```

<span data-ttu-id="6e23d-165">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="6e23d-165">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="6e23d-166">Configure server firewall</span><span class="sxs-lookup"><span data-stu-id="6e23d-166">Configure server firewall</span></span>

<span data-ttu-id="6e23d-167">Create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az-mysql-server-firewall-rule-create) command.</span><span class="sxs-lookup"><span data-stu-id="6e23d-167">Create a firewall rule for your MySQL server to allow client connections by using the [`az mysql server firewall-rule create`](/cli/azure/mysql/server/firewall-rule?view=azure-cli-latest#az-mysql-server-firewall-rule-create) command.</span></span> <span data-ttu-id="6e23d-168">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="6e23d-168">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create --name allAzureIPs --server <mysql_server_name> --resource-group myResourceGroup --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP] 
> <span data-ttu-id="6e23d-169">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="6e23d-169">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span></span>
>

### <a name="connect-to-production-mysql-server-locally"></a><span data-ttu-id="6e23d-170">Connect to production MySQL server locally</span><span class="sxs-lookup"><span data-stu-id="6e23d-170">Connect to production MySQL server locally</span></span>

<span data-ttu-id="6e23d-171">In the terminal window, connect to the MySQL server in Azure.</span><span class="sxs-lookup"><span data-stu-id="6e23d-171">In the terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="6e23d-172">Use the value you specified previously for _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="6e23d-172">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="6e23d-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created the database server.</span><span class="sxs-lookup"><span data-stu-id="6e23d-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created the database server.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="6e23d-174">Create a production database</span><span class="sxs-lookup"><span data-stu-id="6e23d-174">Create a production database</span></span>

<span data-ttu-id="6e23d-175">At the `mysql` prompt, create a database.</span><span class="sxs-lookup"><span data-stu-id="6e23d-175">At the `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="6e23d-176">Create a user with permissions</span><span class="sxs-lookup"><span data-stu-id="6e23d-176">Create a user with permissions</span></span>

<span data-ttu-id="6e23d-177">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span><span class="sxs-lookup"><span data-stu-id="6e23d-177">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'phpappuser';
```

<span data-ttu-id="6e23d-178">Exit the server connection by typing `quit`.</span><span class="sxs-lookup"><span data-stu-id="6e23d-178">Exit the server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a><span data-ttu-id="6e23d-179">Connect app to Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="6e23d-179">Connect app to Azure MySQL</span></span>

<span data-ttu-id="6e23d-180">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="6e23d-180">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL.</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="6e23d-181">Configure the database connection</span><span class="sxs-lookup"><span data-stu-id="6e23d-181">Configure the database connection</span></span>

<span data-ttu-id="6e23d-182">In the repository root, create an _.env.production_ file and copy the following variables into it.</span><span class="sxs-lookup"><span data-stu-id="6e23d-182">In the repository root, create an _.env.production_ file and copy the following variables into it.</span></span> <span data-ttu-id="6e23d-183">Replace the placeholder _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="6e23d-183">Replace the placeholder _&lt;mysql_server_name>_.</span></span>

```txt
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.mysql.database.azure.com
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="6e23d-184">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="6e23d-184">Save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="6e23d-185">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span><span class="sxs-lookup"><span data-stu-id="6e23d-185">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span></span> <span data-ttu-id="6e23d-186">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="6e23d-186">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL.</span></span> <span data-ttu-id="6e23d-187">With environment variables, you don't need the *.env* file in App Service.</span><span class="sxs-lookup"><span data-stu-id="6e23d-187">With environment variables, you don't need the *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="6e23d-188">Configure SSL certificate</span><span class="sxs-lookup"><span data-stu-id="6e23d-188">Configure SSL certificate</span></span>

<span data-ttu-id="6e23d-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span><span class="sxs-lookup"><span data-stu-id="6e23d-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="6e23d-190">To connect to your MySQL database in Azure, you must use the [_.pem_ certificate supplied by Azure Database for MySQL](../../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="6e23d-190">To connect to your MySQL database in Azure, you must use the [_.pem_ certificate supplied by Azure Database for MySQL](../../mysql/howto-configure-ssl.md).</span></span>

<span data-ttu-id="6e23d-191">Open _config/database.php_ and add the _sslmode_ and _options_ parameters to `connections.mysql`, as shown in the following code.</span><span class="sxs-lookup"><span data-stu-id="6e23d-191">Open _config/database.php_ and add the _sslmode_ and _options_ parameters to `connections.mysql`, as shown in the following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/BaltimoreCyberTrustRoot.crt.pem', 
    ] : []
],
```

<span data-ttu-id="6e23d-192">The certificate `BaltimoreCyberTrustRoot.crt.pem` is provided in the repository for convenience in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e23d-192">The certificate `BaltimoreCyberTrustRoot.crt.pem` is provided in the repository for convenience in this tutorial.</span></span> 

### <a name="test-the-application-locally"></a><span data-ttu-id="6e23d-193">Test the application locally</span><span class="sxs-lookup"><span data-stu-id="6e23d-193">Test the application locally</span></span>

<span data-ttu-id="6e23d-194">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="6e23d-194">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL.</span></span> <span data-ttu-id="6e23d-195">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="6e23d-195">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="6e23d-196">_.env.production_ doesn't have a valid application key yet.</span><span class="sxs-lookup"><span data-stu-id="6e23d-196">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="6e23d-197">Generate a new one for it in the terminal.</span><span class="sxs-lookup"><span data-stu-id="6e23d-197">Generate a new one for it in the terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="6e23d-198">Run the sample application with _.env.production_ as the environment file.</span><span class="sxs-lookup"><span data-stu-id="6e23d-198">Run the sample application with _.env.production_ as the environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="6e23d-199">Navigate to `http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="6e23d-199">Navigate to `http://localhost:8000`.</span></span> <span data-ttu-id="6e23d-200">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="6e23d-200">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span></span>

<span data-ttu-id="6e23d-201">Add a few tasks in the page.</span><span class="sxs-lookup"><span data-stu-id="6e23d-201">Add a few tasks in the page.</span></span>

![PHP connects successfully to Azure Database for MySQL](./media/tutorial-php-mysql-app/mysql-connect-success.png)

<span data-ttu-id="6e23d-203">To stop PHP, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="6e23d-203">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="6e23d-204">Commit your changes</span><span class="sxs-lookup"><span data-stu-id="6e23d-204">Commit your changes</span></span>

<span data-ttu-id="6e23d-205">Run the following Git commands to commit your changes:</span><span class="sxs-lookup"><span data-stu-id="6e23d-205">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="6e23d-206">Your app is ready to be deployed.</span><span class="sxs-lookup"><span data-stu-id="6e23d-206">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="6e23d-207">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-207">Deploy to Azure</span></span>

<span data-ttu-id="6e23d-208">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6e23d-208">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span></span>

<span data-ttu-id="6e23d-209">The Laravel application starts in the _/public_ directory.</span><span class="sxs-lookup"><span data-stu-id="6e23d-209">The Laravel application starts in the _/public_ directory.</span></span> <span data-ttu-id="6e23d-210">The default PHP Docker image for App Service uses Apache, and it doesn't let you customize the `DocumentRoot` for Laravel.</span><span class="sxs-lookup"><span data-stu-id="6e23d-210">The default PHP Docker image for App Service uses Apache, and it doesn't let you customize the `DocumentRoot` for Laravel.</span></span> <span data-ttu-id="6e23d-211">However, you can use `.htaccess` to rewrite all requests to point to _/public_ instead of the root directory.</span><span class="sxs-lookup"><span data-stu-id="6e23d-211">However, you can use `.htaccess` to rewrite all requests to point to _/public_ instead of the root directory.</span></span> <span data-ttu-id="6e23d-212">In the repository root, an `.htaccess` is added already for this purpose.</span><span class="sxs-lookup"><span data-stu-id="6e23d-212">In the repository root, an `.htaccess` is added already for this purpose.</span></span> <span data-ttu-id="6e23d-213">With it, your Laravel application is ready to be deployed.</span><span class="sxs-lookup"><span data-stu-id="6e23d-213">With it, your Laravel application is ready to be deployed.</span></span>

> [!NOTE] 
> <span data-ttu-id="6e23d-214">If you would rather not use _.htaccess_ rewrite, you can deploy your Laravel application with a [custom Docker image](quickstart-docker-go.md) instead.</span><span class="sxs-lookup"><span data-stu-id="6e23d-214">If you would rather not use _.htaccess_ rewrite, you can deploy your Laravel application with a [custom Docker image](quickstart-docker-go.md) instead.</span></span>
>
>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="6e23d-215">Configure a deployment user</span><span class="sxs-lookup"><span data-stu-id="6e23d-215">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user-no-h.md)]

### <a name="create-an-app-service-plan"></a><span data-ttu-id="6e23d-216">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="6e23d-216">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../../includes/app-service-web-create-app-service-plan-linux-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="6e23d-217">Create a web app</span><span class="sxs-lookup"><span data-stu-id="6e23d-217">Create a web app</span></span>

[!INCLUDE [Create web app](../../../includes/app-service-web-create-web-app-php-linux-no-h.md)] 

### <a name="configure-database-settings"></a><span data-ttu-id="6e23d-218">Configure database settings</span><span class="sxs-lookup"><span data-stu-id="6e23d-218">Configure database settings</span></span>

<span data-ttu-id="6e23d-219">In App Service, you set environment variables as _app settings_ by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span><span class="sxs-lookup"><span data-stu-id="6e23d-219">In App Service, you set environment variables as _app settings_ by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span></span>

<span data-ttu-id="6e23d-220">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="6e23d-220">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="6e23d-221">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="6e23d-221">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="6e23d-222">You can use the PHP [getenv](http://php.net/manual/en/function.getenv.php) method to access the settings.</span><span class="sxs-lookup"><span data-stu-id="6e23d-222">You can use the PHP [getenv](http://php.net/manual/en/function.getenv.php) method to access the settings.</span></span> <span data-ttu-id="6e23d-223">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="6e23d-223">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span></span> <span data-ttu-id="6e23d-224">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span><span class="sxs-lookup"><span data-stu-id="6e23d-224">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="6e23d-225">Configure Laravel environment variables</span><span class="sxs-lookup"><span data-stu-id="6e23d-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="6e23d-226">Laravel needs an application key in App Service.</span><span class="sxs-lookup"><span data-stu-id="6e23d-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="6e23d-227">You can configure it with app settings.</span><span class="sxs-lookup"><span data-stu-id="6e23d-227">You can configure it with app settings.</span></span>

<span data-ttu-id="6e23d-228">Use `php artisan` to generate a new application key without saving it to _.env_.</span><span class="sxs-lookup"><span data-stu-id="6e23d-228">Use `php artisan` to generate a new application key without saving it to _.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="6e23d-229">Set the application key in the App Service web app by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span><span class="sxs-lookup"><span data-stu-id="6e23d-229">Set the application key in the App Service web app by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span></span> <span data-ttu-id="6e23d-230">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span><span class="sxs-lookup"><span data-stu-id="6e23d-230">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="6e23d-231">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span><span class="sxs-lookup"><span data-stu-id="6e23d-231">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span></span> <span data-ttu-id="6e23d-232">When running a production application, set it to `false`, which is more secure.</span><span class="sxs-lookup"><span data-stu-id="6e23d-232">When running a production application, set it to `false`, which is more secure.</span></span>

### <a name="push-to-azure-from-git"></a><span data-ttu-id="6e23d-233">Push to Azure from Git</span><span class="sxs-lookup"><span data-stu-id="6e23d-233">Push to Azure from Git</span></span>

<span data-ttu-id="6e23d-234">Add an Azure remote to your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="6e23d-234">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="6e23d-235">Push to the Azure remote to deploy the PHP application.</span><span class="sxs-lookup"><span data-stu-id="6e23d-235">Push to the Azure remote to deploy the PHP application.</span></span> <span data-ttu-id="6e23d-236">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span><span class="sxs-lookup"><span data-stu-id="6e23d-236">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="6e23d-237">During deployment, Azure App Service communicates its progress with Git.</span><span class="sxs-lookup"><span data-stu-id="6e23d-237">During deployment, Azure App Service communicates its progress with Git.</span></span>

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
> <span data-ttu-id="6e23d-238">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span><span class="sxs-lookup"><span data-stu-id="6e23d-238">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span></span> <span data-ttu-id="6e23d-239">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span><span class="sxs-lookup"><span data-stu-id="6e23d-239">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span></span>
>
> - <span data-ttu-id="6e23d-240">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="6e23d-240">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="6e23d-241">`deploy.sh` - The custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="6e23d-241">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="6e23d-242">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span><span class="sxs-lookup"><span data-stu-id="6e23d-242">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="6e23d-243">`composer.phar` - The Composer package manager.</span><span class="sxs-lookup"><span data-stu-id="6e23d-243">`composer.phar` - The Composer package manager.</span></span>
>
> <span data-ttu-id="6e23d-244">You can use this approach to add any step to your Git-based deployment to App Service.</span><span class="sxs-lookup"><span data-stu-id="6e23d-244">You can use this approach to add any step to your Git-based deployment to App Service.</span></span> <span data-ttu-id="6e23d-245">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="6e23d-245">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="6e23d-246">Browse to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="6e23d-246">Browse to the Azure web app</span></span>

<span data-ttu-id="6e23d-247">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span><span class="sxs-lookup"><span data-stu-id="6e23d-247">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![PHP app running in Azure App Service](./media/tutorial-php-mysql-app/php-mysql-in-azure.png)

<span data-ttu-id="6e23d-249">Congratulations, you're running a data-driven PHP app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6e23d-249">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="6e23d-250">Update model locally and redeploy</span><span class="sxs-lookup"><span data-stu-id="6e23d-250">Update model locally and redeploy</span></span>

<span data-ttu-id="6e23d-251">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span><span class="sxs-lookup"><span data-stu-id="6e23d-251">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="6e23d-252">For the tasks scenario, you modify the application so that you can mark a task as complete.</span><span class="sxs-lookup"><span data-stu-id="6e23d-252">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="6e23d-253">Add a column</span><span class="sxs-lookup"><span data-stu-id="6e23d-253">Add a column</span></span>

<span data-ttu-id="6e23d-254">In the terminal, navigate to the root of the Git repository.</span><span class="sxs-lookup"><span data-stu-id="6e23d-254">In the terminal, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="6e23d-255">Generate a new database migration for the `tasks` table:</span><span class="sxs-lookup"><span data-stu-id="6e23d-255">Generate a new database migration for the `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="6e23d-256">This command shows you the name of the migration file that's generated.</span><span class="sxs-lookup"><span data-stu-id="6e23d-256">This command shows you the name of the migration file that's generated.</span></span> <span data-ttu-id="6e23d-257">Find this file in _database/migrations_ and open it.</span><span class="sxs-lookup"><span data-stu-id="6e23d-257">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="6e23d-258">Replace the `up` method with the following code:</span><span class="sxs-lookup"><span data-stu-id="6e23d-258">Replace the `up` method with the following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="6e23d-259">The preceding code adds a boolean column in the `tasks` table called `complete`.</span><span class="sxs-lookup"><span data-stu-id="6e23d-259">The preceding code adds a boolean column in the `tasks` table called `complete`.</span></span>

<span data-ttu-id="6e23d-260">Replace the `down` method with the following code for the rollback action:</span><span class="sxs-lookup"><span data-stu-id="6e23d-260">Replace the `down` method with the following code for the rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="6e23d-261">In the terminal, run Laravel database migrations to make the change in the local database.</span><span class="sxs-lookup"><span data-stu-id="6e23d-261">In the terminal, run Laravel database migrations to make the change in the local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="6e23d-262">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span><span class="sxs-lookup"><span data-stu-id="6e23d-262">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="6e23d-263">Update application logic</span><span class="sxs-lookup"><span data-stu-id="6e23d-263">Update application logic</span></span>

<span data-ttu-id="6e23d-264">Open the *routes/web.php* file.</span><span class="sxs-lookup"><span data-stu-id="6e23d-264">Open the *routes/web.php* file.</span></span> <span data-ttu-id="6e23d-265">The application defines its routes and business logic here.</span><span class="sxs-lookup"><span data-stu-id="6e23d-265">The application defines its routes and business logic here.</span></span>

<span data-ttu-id="6e23d-266">At the end of the file, add a route with the following code:</span><span class="sxs-lookup"><span data-stu-id="6e23d-266">At the end of the file, add a route with the following code:</span></span>

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

<span data-ttu-id="6e23d-267">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span><span class="sxs-lookup"><span data-stu-id="6e23d-267">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span></span>

### <a name="update-the-view"></a><span data-ttu-id="6e23d-268">Update the view</span><span class="sxs-lookup"><span data-stu-id="6e23d-268">Update the view</span></span>

<span data-ttu-id="6e23d-269">Open the *resources/views/tasks.blade.php* file.</span><span class="sxs-lookup"><span data-stu-id="6e23d-269">Open the *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="6e23d-270">Find the `<tr>` opening tag and replace it with:</span><span class="sxs-lookup"><span data-stu-id="6e23d-270">Find the `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="6e23d-271">The preceding code changes the row color depending on whether the task is complete.</span><span class="sxs-lookup"><span data-stu-id="6e23d-271">The preceding code changes the row color depending on whether the task is complete.</span></span>

<span data-ttu-id="6e23d-272">In the next line, you have the following code:</span><span class="sxs-lookup"><span data-stu-id="6e23d-272">In the next line, you have the following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="6e23d-273">Replace the entire line with the following code:</span><span class="sxs-lookup"><span data-stu-id="6e23d-273">Replace the entire line with the following code:</span></span>

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

<span data-ttu-id="6e23d-274">The preceding code adds the submit button that references the route that you defined earlier.</span><span class="sxs-lookup"><span data-stu-id="6e23d-274">The preceding code adds the submit button that references the route that you defined earlier.</span></span>

### <a name="test-the-changes-locally"></a><span data-ttu-id="6e23d-275">Test the changes locally</span><span class="sxs-lookup"><span data-stu-id="6e23d-275">Test the changes locally</span></span>

<span data-ttu-id="6e23d-276">From the root directory of the Git repository, run the development server.</span><span class="sxs-lookup"><span data-stu-id="6e23d-276">From the root directory of the Git repository, run the development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="6e23d-277">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span><span class="sxs-lookup"><span data-stu-id="6e23d-277">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span></span>

![Added check box to task](./media/tutorial-php-mysql-app/complete-checkbox.png)

<span data-ttu-id="6e23d-279">To stop PHP, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="6e23d-279">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="6e23d-280">Publish changes to Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-280">Publish changes to Azure</span></span>

<span data-ttu-id="6e23d-281">In the terminal, run Laravel database migrations with the production connection string to make the change in the Azure database.</span><span class="sxs-lookup"><span data-stu-id="6e23d-281">In the terminal, run Laravel database migrations with the production connection string to make the change in the Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="6e23d-282">Commit all the changes in Git, and then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="6e23d-282">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="6e23d-283">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span><span class="sxs-lookup"><span data-stu-id="6e23d-283">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![Model and database changes published to Azure](media/tutorial-php-mysql-app/complete-checkbox-published.png)

<span data-ttu-id="6e23d-285">If you added any tasks, they are retained in the database.</span><span class="sxs-lookup"><span data-stu-id="6e23d-285">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="6e23d-286">Updates to the data schema leave existing data intact.</span><span class="sxs-lookup"><span data-stu-id="6e23d-286">Updates to the data schema leave existing data intact.</span></span>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="6e23d-287">Manage the Azure web app</span><span class="sxs-lookup"><span data-stu-id="6e23d-287">Manage the Azure web app</span></span>

<span data-ttu-id="6e23d-288">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="6e23d-288">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="6e23d-289">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="6e23d-289">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/tutorial-php-mysql-app/access-portal.png)

<span data-ttu-id="6e23d-291">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="6e23d-291">You see your web app's Overview page.</span></span> <span data-ttu-id="6e23d-292">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span><span class="sxs-lookup"><span data-stu-id="6e23d-292">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="6e23d-293">The left menu provides pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="6e23d-293">The left menu provides pages for configuring your app.</span></span>

![App Service page in Azure portal](./media/tutorial-php-mysql-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="6e23d-295">Next steps</span><span class="sxs-lookup"><span data-stu-id="6e23d-295">Next steps</span></span>

<span data-ttu-id="6e23d-296">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="6e23d-296">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6e23d-297">Create a MySQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-297">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="6e23d-298">Connect a PHP app to MySQL</span><span class="sxs-lookup"><span data-stu-id="6e23d-298">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="6e23d-299">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-299">Deploy the app to Azure</span></span>
> * <span data-ttu-id="6e23d-300">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="6e23d-300">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="6e23d-301">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="6e23d-301">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="6e23d-302">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e23d-302">Manage the app in the Azure portal</span></span>

<span data-ttu-id="6e23d-303">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span><span class="sxs-lookup"><span data-stu-id="6e23d-303">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e23d-304">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="6e23d-304">Map an existing custom DNS name to Azure Web Apps</span></span>](../app-service-web-tutorial-custom-domain.md)
