---
title: 'Tutorial: Design an Azure Database for MySQL using Azure CLI'
description: This tutorial explains how to create and manage Azure Database for MySQL server and database using Azure CLI 2.0 from the command line.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 04/01/2018
ms.custom: mvc
ms.openlocfilehash: 07dc1c2fa166be066df9bd8a663e08db830fe1af
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867162"
---
# <a name="tutorial-design-an-azure-database-for-mysql-using-azure-cli"></a><span data-ttu-id="6dc8b-103">Tutorial: Design an Azure Database for MySQL using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6dc8b-103">Tutorial: Design an Azure Database for MySQL using Azure CLI</span></span>

<span data-ttu-id="6dc8b-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="6dc8b-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span><span class="sxs-lookup"><span data-stu-id="6dc8b-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6dc8b-106">Create an Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="6dc8b-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="6dc8b-107">Configure the server firewall</span><span class="sxs-lookup"><span data-stu-id="6dc8b-107">Configure the server firewall</span></span>
> * <span data-ttu-id="6dc8b-108">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span><span class="sxs-lookup"><span data-stu-id="6dc8b-108">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="6dc8b-109">Load sample data</span><span class="sxs-lookup"><span data-stu-id="6dc8b-109">Load sample data</span></span>
> * <span data-ttu-id="6dc8b-110">Query data</span><span class="sxs-lookup"><span data-stu-id="6dc8b-110">Query data</span></span>
> * <span data-ttu-id="6dc8b-111">Update data</span><span class="sxs-lookup"><span data-stu-id="6dc8b-111">Update data</span></span>
> * <span data-ttu-id="6dc8b-112">Restore data</span><span class="sxs-lookup"><span data-stu-id="6dc8b-112">Restore data</span></span>

<span data-ttu-id="6dc8b-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6dc8b-114">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-114">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6dc8b-115">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="6dc8b-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6dc8b-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="6dc8b-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="6dc8b-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#az-account-set) command.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#az-account-set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="6dc8b-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="6dc8b-119">Create a resource group</span></span>
<span data-ttu-id="6dc8b-120">Create an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-120">Create an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="6dc8b-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="6dc8b-122">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-122">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="6dc8b-123">Create an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="6dc8b-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="6dc8b-124">Create an Azure Database for MySQL server with the az mysql server create command.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="6dc8b-125">A server can manage multiple databases.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-125">A server can manage multiple databases.</span></span> <span data-ttu-id="6dc8b-126">Typically, a separate database is used for each project or for each user.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="6dc8b-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `myresourcegroup` with name `mydemoserver`.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `myresourcegroup` with name `mydemoserver`.</span></span> <span data-ttu-id="6dc8b-128">The server has an administrator log in named `myadmin`.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-128">The server has an administrator log in named `myadmin`.</span></span> <span data-ttu-id="6dc8b-129">It is a General Purpose, Gen 4 server with 2 vCores.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-129">It is a General Purpose, Gen 4 server with 2 vCores.</span></span> <span data-ttu-id="6dc8b-130">Substitute the `<server_admin_password>` with your own value.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-130">Substitute the `<server_admin_password>` with your own value.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name mydemoserver --location westus --admin-user myadmin --admin-password <server_admin_password> --sku-name GP_Gen4_2 --version 5.7
```
<span data-ttu-id="6dc8b-131">The sku-name parameter value follows the convention {pricing tier}\_{compute generation}\_{vCores} as in the examples below:</span><span class="sxs-lookup"><span data-stu-id="6dc8b-131">The sku-name parameter value follows the convention {pricing tier}\_{compute generation}\_{vCores} as in the examples below:</span></span>
+ <span data-ttu-id="6dc8b-132">`--sku-name B_Gen4_4` maps to Basic, Gen 4, and 4 vCores.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-132">`--sku-name B_Gen4_4` maps to Basic, Gen 4, and 4 vCores.</span></span>
+ <span data-ttu-id="6dc8b-133">`--sku-name GP_Gen5_32` maps to General Purpose, Gen 5, and 32 vCores.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-133">`--sku-name GP_Gen5_32` maps to General Purpose, Gen 5, and 32 vCores.</span></span>
+ <span data-ttu-id="6dc8b-134">`--sku-name MO_Gen5_2` maps to Memory Optimized, Gen 5, and 2 vCores.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-134">`--sku-name MO_Gen5_2` maps to Memory Optimized, Gen 5, and 2 vCores.</span></span>

<span data-ttu-id="6dc8b-135">Please see the [pricing tiers](./concepts-pricing-tiers.md) documentation to understand the valid values per region and per tier.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-135">Please see the [pricing tiers](./concepts-pricing-tiers.md) documentation to understand the valid values per region and per tier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dc8b-136">The server admin login and password that you specify here are required to log in to the server and its databases later in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-136">The server admin login and password that you specify here are required to log in to the server and its databases later in this quickstart.</span></span> <span data-ttu-id="6dc8b-137">Remember or record this information for later use.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-137">Remember or record this information for later use.</span></span>


## <a name="configure-firewall-rule"></a><span data-ttu-id="6dc8b-138">Configure firewall rule</span><span class="sxs-lookup"><span data-stu-id="6dc8b-138">Configure firewall rule</span></span>
<span data-ttu-id="6dc8b-139">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-139">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="6dc8b-140">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-140">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="6dc8b-141">The following example creates a firewall rule called `AllowMyIP` that allows connections from a specific IP address, 192.168.0.1.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-141">The following example creates a firewall rule called `AllowMyIP` that allows connections from a specific IP address, 192.168.0.1.</span></span> <span data-ttu-id="6dc8b-142">Substitute in the IP address or range of IP addresses that correspond to where you'll be connecting from.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-142">Substitute in the IP address or range of IP addresses that correspond to where you'll be connecting from.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server mydemoserver --name AllowMyIP --start-ip-address 192.168.0.1 --end-ip-address 192.168.0.1
```

## <a name="get-the-connection-information"></a><span data-ttu-id="6dc8b-143">Get the connection information</span><span class="sxs-lookup"><span data-stu-id="6dc8b-143">Get the connection information</span></span>

<span data-ttu-id="6dc8b-144">To connect to your server, you need to provide host information and access credentials.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-144">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name mydemoserver
```

<span data-ttu-id="6dc8b-145">The result is in JSON format.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-145">The result is in JSON format.</span></span> <span data-ttu-id="6dc8b-146">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-146">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mydemoserver.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/mydemoserver",
  "location": "westus",
  "name": "mydemoserver",
  "resourceGroup": "myresourcegroup",
 "sku": {
    "capacity": 2,
    "family": "Gen4",
    "name": "GP_Gen4_2",
    "size": null,
    "tier": "GeneralPurpose"
  },
  "sslEnforcement": "Enabled",
  "storageProfile": {
    "backupRetentionDays": 7,
    "geoRedundantBackup": "Disabled",
    "storageMb": 5120
  },
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": "5.7"
}
```

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="6dc8b-147">Connect to the server using mysql</span><span class="sxs-lookup"><span data-stu-id="6dc8b-147">Connect to the server using mysql</span></span>
<span data-ttu-id="6dc8b-148">Use the [mysql command-line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-148">Use the [mysql command-line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="6dc8b-149">In this example, the command is:</span><span class="sxs-lookup"><span data-stu-id="6dc8b-149">In this example, the command is:</span></span>
```cmd
mysql -h mydemoserver.database.windows.net -u myadmin@mydemoserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="6dc8b-150">Create a blank database</span><span class="sxs-lookup"><span data-stu-id="6dc8b-150">Create a blank database</span></span>
<span data-ttu-id="6dc8b-151">Once you’re connected to the server, create a blank database.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-151">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="6dc8b-152">At the prompt, run the following command to switch the connection to this newly created database:</span><span class="sxs-lookup"><span data-stu-id="6dc8b-152">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="6dc8b-153">Create tables in the database</span><span class="sxs-lookup"><span data-stu-id="6dc8b-153">Create tables in the database</span></span>
<span data-ttu-id="6dc8b-154">Now that you know how to connect to the Azure Database for MySQL database, complete some basic tasks.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-154">Now that you know how to connect to the Azure Database for MySQL database, complete some basic tasks.</span></span>

<span data-ttu-id="6dc8b-155">First, create a table and load it with some data.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-155">First, create a table and load it with some data.</span></span> <span data-ttu-id="6dc8b-156">Let's create a table that stores inventory information.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-156">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="6dc8b-157">Load data into the tables</span><span class="sxs-lookup"><span data-stu-id="6dc8b-157">Load data into the tables</span></span>
<span data-ttu-id="6dc8b-158">Now that you have a table, insert some data into it.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-158">Now that you have a table, insert some data into it.</span></span> <span data-ttu-id="6dc8b-159">At the open command prompt window, run the following query to insert some rows of data.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-159">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="6dc8b-160">Now you have two rows of sample data into the table you created earlier.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-160">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="6dc8b-161">Query and update the data in the tables</span><span class="sxs-lookup"><span data-stu-id="6dc8b-161">Query and update the data in the tables</span></span>
<span data-ttu-id="6dc8b-162">Execute the following query to retrieve information from the database table.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-162">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="6dc8b-163">You can also update the data in the tables.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-163">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="6dc8b-164">The row gets updated accordingly when you retrieve data.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-164">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="6dc8b-165">Restore a database to a previous point in time</span><span class="sxs-lookup"><span data-stu-id="6dc8b-165">Restore a database to a previous point in time</span></span>
<span data-ttu-id="6dc8b-166">Imagine you have accidentally deleted this table.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-166">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="6dc8b-167">This is something you cannot easily recover from.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-167">This is something you cannot easily recover from.</span></span> <span data-ttu-id="6dc8b-168">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-168">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="6dc8b-169">You can use this new server to recover your deleted data.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-169">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="6dc8b-170">The following steps restore the sample server to a point before the table was added.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-170">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="6dc8b-171">For the restore, you need the following information:</span><span class="sxs-lookup"><span data-stu-id="6dc8b-171">For the restore, you need the following information:</span></span>

- <span data-ttu-id="6dc8b-172">Restore point: Select a point-in-time that occurs before the server was changed.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-172">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="6dc8b-173">Must be greater than or equal to the source database's Oldest backup value.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-173">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="6dc8b-174">Target server: Provide a new server name you want to restore to</span><span class="sxs-lookup"><span data-stu-id="6dc8b-174">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="6dc8b-175">Source server: Provide the name of the server you want to restore from</span><span class="sxs-lookup"><span data-stu-id="6dc8b-175">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="6dc8b-176">Location: You cannot select the region, by default it is same as the source server</span><span class="sxs-lookup"><span data-stu-id="6dc8b-176">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group myresourcegroup --name mydemoserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mydemoserver
```

<span data-ttu-id="6dc8b-177">The `az mysql server restore` command needs the following parameters:</span><span class="sxs-lookup"><span data-stu-id="6dc8b-177">The `az mysql server restore` command needs the following parameters:</span></span>
| <span data-ttu-id="6dc8b-178">Setting</span><span class="sxs-lookup"><span data-stu-id="6dc8b-178">Setting</span></span> | <span data-ttu-id="6dc8b-179">Suggested value</span><span class="sxs-lookup"><span data-stu-id="6dc8b-179">Suggested value</span></span> | <span data-ttu-id="6dc8b-180">Description</span><span class="sxs-lookup"><span data-stu-id="6dc8b-180">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="6dc8b-181">resource-group</span><span class="sxs-lookup"><span data-stu-id="6dc8b-181">resource-group</span></span> |  <span data-ttu-id="6dc8b-182">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="6dc8b-182">myresourcegroup</span></span> |  <span data-ttu-id="6dc8b-183">The resource group in which the source server exists.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-183">The resource group in which the source server exists.</span></span>  |
| <span data-ttu-id="6dc8b-184">name</span><span class="sxs-lookup"><span data-stu-id="6dc8b-184">name</span></span> | <span data-ttu-id="6dc8b-185">mydemoserver-restored</span><span class="sxs-lookup"><span data-stu-id="6dc8b-185">mydemoserver-restored</span></span> | <span data-ttu-id="6dc8b-186">The name of the new server that is created by the restore command.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-186">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="6dc8b-187">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="6dc8b-187">restore-point-in-time</span></span> | <span data-ttu-id="6dc8b-188">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="6dc8b-188">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="6dc8b-189">Select a point-in-time to restore to.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-189">Select a point-in-time to restore to.</span></span> <span data-ttu-id="6dc8b-190">This date and time must be within the source server's backup retention period.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-190">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="6dc8b-191">Use ISO8601 date and time format.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-191">Use ISO8601 date and time format.</span></span> <span data-ttu-id="6dc8b-192">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-192">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="6dc8b-193">source-server</span><span class="sxs-lookup"><span data-stu-id="6dc8b-193">source-server</span></span> | <span data-ttu-id="6dc8b-194">mydemoserver</span><span class="sxs-lookup"><span data-stu-id="6dc8b-194">mydemoserver</span></span> | <span data-ttu-id="6dc8b-195">The name or ID of the source server to restore from.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-195">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="6dc8b-196">Restoring a server to a point-in-time creates a new server, copied as the original server as of the point in time you specify.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-196">Restoring a server to a point-in-time creates a new server, copied as the original server as of the point in time you specify.</span></span> <span data-ttu-id="6dc8b-197">The location and pricing tier values for the restored server are the same as the source server.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-197">The location and pricing tier values for the restored server are the same as the source server.</span></span>

<span data-ttu-id="6dc8b-198">The command is synchronous, and will return after the server is restored.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-198">The command is synchronous, and will return after the server is restored.</span></span> <span data-ttu-id="6dc8b-199">Once the restore finishes, locate the new server that was created.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-199">Once the restore finishes, locate the new server that was created.</span></span> <span data-ttu-id="6dc8b-200">Verify the data was restored as expected.</span><span class="sxs-lookup"><span data-stu-id="6dc8b-200">Verify the data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dc8b-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="6dc8b-201">Next steps</span></span>
<span data-ttu-id="6dc8b-202">In this tutorial you learned to:</span><span class="sxs-lookup"><span data-stu-id="6dc8b-202">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="6dc8b-203">Create an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="6dc8b-203">Create an Azure Database for MySQL server</span></span>
> * <span data-ttu-id="6dc8b-204">Configure the server firewall</span><span class="sxs-lookup"><span data-stu-id="6dc8b-204">Configure the server firewall</span></span>
> * <span data-ttu-id="6dc8b-205">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span><span class="sxs-lookup"><span data-stu-id="6dc8b-205">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="6dc8b-206">Load sample data</span><span class="sxs-lookup"><span data-stu-id="6dc8b-206">Load sample data</span></span>
> * <span data-ttu-id="6dc8b-207">Query data</span><span class="sxs-lookup"><span data-stu-id="6dc8b-207">Query data</span></span>
> * <span data-ttu-id="6dc8b-208">Update data</span><span class="sxs-lookup"><span data-stu-id="6dc8b-208">Update data</span></span>
> * <span data-ttu-id="6dc8b-209">Restore data</span><span class="sxs-lookup"><span data-stu-id="6dc8b-209">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6dc8b-210">Azure Database for MySQL - Azure CLI samples</span><span class="sxs-lookup"><span data-stu-id="6dc8b-210">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
