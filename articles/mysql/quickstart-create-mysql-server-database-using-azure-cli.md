---
title: 'Quickstart: Create an Azure Database for MySQL server - Azure CLI'
description: This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 04/01/2018
ms.custom: mvc
ms.openlocfilehash: 43c9ee65b43bed7ac686edbf48ec670a85cf12cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865787"
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="34095-103">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="34095-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="34095-104">This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group in about five minutes.</span><span class="sxs-lookup"><span data-stu-id="34095-104">This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="34095-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="34095-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span>

<span data-ttu-id="34095-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="34095-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="34095-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="34095-107">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="34095-108">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="34095-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="34095-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="34095-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="34095-110">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span><span class="sxs-lookup"><span data-stu-id="34095-110">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="34095-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#az-account-set) command.</span><span class="sxs-lookup"><span data-stu-id="34095-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#az-account-set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="34095-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="34095-112">Create a resource group</span></span>
<span data-ttu-id="34095-113">Create an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="34095-113">Create an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="34095-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span><span class="sxs-lookup"><span data-stu-id="34095-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="34095-115">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span><span class="sxs-lookup"><span data-stu-id="34095-115">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="34095-116">Create an Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="34095-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="34095-117">Create an Azure Database for MySQL server with the **[az mysql server create](/cli/azure/mysql/server#az-mysql-server-create)** command.</span><span class="sxs-lookup"><span data-stu-id="34095-117">Create an Azure Database for MySQL server with the **[az mysql server create](/cli/azure/mysql/server#az-mysql-server-create)** command.</span></span> <span data-ttu-id="34095-118">A server can manage multiple databases.</span><span class="sxs-lookup"><span data-stu-id="34095-118">A server can manage multiple databases.</span></span> <span data-ttu-id="34095-119">Typically, a separate database is used for each project or for each user.</span><span class="sxs-lookup"><span data-stu-id="34095-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="34095-120">The following example creates a server in West US named `mydemoserver` in your resource group `myresourcegroup` with server admin login `myadmin`.</span><span class="sxs-lookup"><span data-stu-id="34095-120">The following example creates a server in West US named `mydemoserver` in your resource group `myresourcegroup` with server admin login `myadmin`.</span></span> <span data-ttu-id="34095-121">This is a **Gen 4** **General Purpose** server with 2 **vCores**.</span><span class="sxs-lookup"><span data-stu-id="34095-121">This is a **Gen 4** **General Purpose** server with 2 **vCores**.</span></span> <span data-ttu-id="34095-122">The name of a server maps to DNS name and is thus required to be globally unique in Azure.</span><span class="sxs-lookup"><span data-stu-id="34095-122">The name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="34095-123">Substitute the `<server_admin_password>` with your own value.</span><span class="sxs-lookup"><span data-stu-id="34095-123">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name mydemoserver  --location westus --admin-user myadmin --admin-password <server_admin_password> --sku-name GP_Gen4_2 --version 5.7
```
<span data-ttu-id="34095-124">The sku-name parameter value follows the convention {pricing tier}\_{compute generation}\_{vCores} as in the examples below:</span><span class="sxs-lookup"><span data-stu-id="34095-124">The sku-name parameter value follows the convention {pricing tier}\_{compute generation}\_{vCores} as in the examples below:</span></span>
+ <span data-ttu-id="34095-125">`--sku-name B_Gen4_4` maps to Basic, Gen 4, and 4 vCores.</span><span class="sxs-lookup"><span data-stu-id="34095-125">`--sku-name B_Gen4_4` maps to Basic, Gen 4, and 4 vCores.</span></span>
+ <span data-ttu-id="34095-126">`--sku-name GP_Gen5_32` maps to General Purpose, Gen 5, and 32 vCores.</span><span class="sxs-lookup"><span data-stu-id="34095-126">`--sku-name GP_Gen5_32` maps to General Purpose, Gen 5, and 32 vCores.</span></span>
+ <span data-ttu-id="34095-127">`--sku-name MO_Gen5_2` maps to Memory Optimized, Gen 5, and 2 vCores.</span><span class="sxs-lookup"><span data-stu-id="34095-127">`--sku-name MO_Gen5_2` maps to Memory Optimized, Gen 5, and 2 vCores.</span></span>

<span data-ttu-id="34095-128">Please see the [pricing tiers](./concepts-pricing-tiers.md) documentation to understand the valid values per region and per tier.</span><span class="sxs-lookup"><span data-stu-id="34095-128">Please see the [pricing tiers](./concepts-pricing-tiers.md) documentation to understand the valid values per region and per tier.</span></span>

## <a name="configure-firewall-rule"></a><span data-ttu-id="34095-129">Configure firewall rule</span><span class="sxs-lookup"><span data-stu-id="34095-129">Configure firewall rule</span></span>
<span data-ttu-id="34095-130">Create an Azure Database for MySQL server-level firewall rule using the **[az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-create)** command.</span><span class="sxs-lookup"><span data-stu-id="34095-130">Create an Azure Database for MySQL server-level firewall rule using the **[az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#az-mysql-server-firewall-rule-create)** command.</span></span> <span data-ttu-id="34095-131">A server-level firewall rule allows an external application, such as the **mysql.exe** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span><span class="sxs-lookup"><span data-stu-id="34095-131">A server-level firewall rule allows an external application, such as the **mysql.exe** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="34095-132">The following example creates a firewall rule called `AllowMyIP` that allows connections from a specific IP address, 192.168.0.1.</span><span class="sxs-lookup"><span data-stu-id="34095-132">The following example creates a firewall rule called `AllowMyIP` that allows connections from a specific IP address, 192.168.0.1.</span></span> <span data-ttu-id="34095-133">Substitute in the IP address or range of IP addresses that correspond to where you'll be connecting from.</span><span class="sxs-lookup"><span data-stu-id="34095-133">Substitute in the IP address or range of IP addresses that correspond to where you'll be connecting from.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server mydemoserver --name AllowMyIP --start-ip-address 192.168.0.1 --end-ip-address 192.168.0.1
```

> [!NOTE]
> <span data-ttu-id="34095-134">Connections to Azure Database for MySQL communicate over port 3306.</span><span class="sxs-lookup"><span data-stu-id="34095-134">Connections to Azure Database for MySQL communicate over port 3306.</span></span> <span data-ttu-id="34095-135">If you try to connect from within a corporate network, outbound traffic over port 3306 might not be allowed.</span><span class="sxs-lookup"><span data-stu-id="34095-135">If you try to connect from within a corporate network, outbound traffic over port 3306 might not be allowed.</span></span> <span data-ttu-id="34095-136">If this is the case, you can't connect to your server unless your IT department opens port 3306.</span><span class="sxs-lookup"><span data-stu-id="34095-136">If this is the case, you can't connect to your server unless your IT department opens port 3306.</span></span>
> 


## <a name="configure-ssl-settings"></a><span data-ttu-id="34095-137">Configure SSL settings</span><span class="sxs-lookup"><span data-stu-id="34095-137">Configure SSL settings</span></span>
<span data-ttu-id="34095-138">By default, SSL connections between your server and client applications are enforced.</span><span class="sxs-lookup"><span data-stu-id="34095-138">By default, SSL connections between your server and client applications are enforced.</span></span> <span data-ttu-id="34095-139">This default ensures security of "in-motion" data by encrypting the data stream over the internet.</span><span class="sxs-lookup"><span data-stu-id="34095-139">This default ensures security of "in-motion" data by encrypting the data stream over the internet.</span></span> <span data-ttu-id="34095-140">To make this quick start easier, disable SSL connections for your server.</span><span class="sxs-lookup"><span data-stu-id="34095-140">To make this quick start easier, disable SSL connections for your server.</span></span> <span data-ttu-id="34095-141">Disabling SSL is not recommended for production servers.</span><span class="sxs-lookup"><span data-stu-id="34095-141">Disabling SSL is not recommended for production servers.</span></span> <span data-ttu-id="34095-142">For more information, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="34095-142">For more information, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="34095-143">The following example disables enforcing SSL on your MySQL server.</span><span class="sxs-lookup"><span data-stu-id="34095-143">The following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name mydemoserver --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a><span data-ttu-id="34095-144">Get the connection information</span><span class="sxs-lookup"><span data-stu-id="34095-144">Get the connection information</span></span>

<span data-ttu-id="34095-145">To connect to your server, you need to provide host information and access credentials.</span><span class="sxs-lookup"><span data-stu-id="34095-145">To connect to your server, you need to provide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name mydemoserver
```

<span data-ttu-id="34095-146">The result is in JSON format.</span><span class="sxs-lookup"><span data-stu-id="34095-146">The result is in JSON format.</span></span> <span data-ttu-id="34095-147">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="34095-147">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "earliestRestoreDate": null,
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

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a><span data-ttu-id="34095-148">Connect to the server using the mysql.exe command-line tool</span><span class="sxs-lookup"><span data-stu-id="34095-148">Connect to the server using the mysql.exe command-line tool</span></span>
<span data-ttu-id="34095-149">Connect to your server using the **mysql.exe** command-line tool.</span><span class="sxs-lookup"><span data-stu-id="34095-149">Connect to your server using the **mysql.exe** command-line tool.</span></span> <span data-ttu-id="34095-150">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span><span class="sxs-lookup"><span data-stu-id="34095-150">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="34095-151">Instead you may also click the **Try It** button on code samples, or the  `>_` button from the upper right toolbar in the Azure portal, and launch the **Azure Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="34095-151">Instead you may also click the **Try It** button on code samples, or the  `>_` button from the upper right toolbar in the Azure portal, and launch the **Azure Cloud Shell**.</span></span>

<span data-ttu-id="34095-152">Type the next commands:</span><span class="sxs-lookup"><span data-stu-id="34095-152">Type the next commands:</span></span> 

1. <span data-ttu-id="34095-153">Connect to the server using **mysql** command-line tool:</span><span class="sxs-lookup"><span data-stu-id="34095-153">Connect to the server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h mydemoserver.mysql.database.azure.com -u myadmin@mydemoserver -p
```

2. <span data-ttu-id="34095-154">View server status:</span><span class="sxs-lookup"><span data-stu-id="34095-154">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="34095-155">If everything goes well, the command-line tool should output the following text:</span><span class="sxs-lookup"><span data-stu-id="34095-155">If everything goes well, the command-line tool should output the following text:</span></span>

```dos
C:\Users\>mysql -h mydemoserver.mysql.database.azure.com -u myadmin@mydemoserver -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             mydemoserver.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="34095-156">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="34095-156">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a><span data-ttu-id="34095-157">Connect to the server using the MySQL Workbench GUI tool</span><span class="sxs-lookup"><span data-stu-id="34095-157">Connect to the server using the MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="34095-158">Launch the MySQL Workbench application on your client computer.</span><span class="sxs-lookup"><span data-stu-id="34095-158">Launch the MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="34095-159">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="34095-159">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="34095-160">In the **Setup New Connection** dialog box, enter the following information on **Parameters** tab:</span><span class="sxs-lookup"><span data-stu-id="34095-160">In the **Setup New Connection** dialog box, enter the following information on **Parameters** tab:</span></span>

   ![setup new connection](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="34095-162">**Setting**</span><span class="sxs-lookup"><span data-stu-id="34095-162">**Setting**</span></span> | <span data-ttu-id="34095-163">**Suggested Value**</span><span class="sxs-lookup"><span data-stu-id="34095-163">**Suggested Value**</span></span> | <span data-ttu-id="34095-164">**Description**</span><span class="sxs-lookup"><span data-stu-id="34095-164">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="34095-165">Connection Name</span><span class="sxs-lookup"><span data-stu-id="34095-165">Connection Name</span></span> | <span data-ttu-id="34095-166">My Connection</span><span class="sxs-lookup"><span data-stu-id="34095-166">My Connection</span></span> | <span data-ttu-id="34095-167">Specify a label for this connection (this can be anything)</span><span class="sxs-lookup"><span data-stu-id="34095-167">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="34095-168">Connection Method</span><span class="sxs-lookup"><span data-stu-id="34095-168">Connection Method</span></span> | <span data-ttu-id="34095-169">choose Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="34095-169">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="34095-170">Use TCP/IP protocol to connect to Azure Database for MySQL></span><span class="sxs-lookup"><span data-stu-id="34095-170">Use TCP/IP protocol to connect to Azure Database for MySQL></span></span> |
| <span data-ttu-id="34095-171">Hostname</span><span class="sxs-lookup"><span data-stu-id="34095-171">Hostname</span></span> | <span data-ttu-id="34095-172">mydemoserver.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="34095-172">mydemoserver.mysql.database.azure.com</span></span> | <span data-ttu-id="34095-173">Server name you previously noted.</span><span class="sxs-lookup"><span data-stu-id="34095-173">Server name you previously noted.</span></span> |
| <span data-ttu-id="34095-174">Port</span><span class="sxs-lookup"><span data-stu-id="34095-174">Port</span></span> | <span data-ttu-id="34095-175">3306</span><span class="sxs-lookup"><span data-stu-id="34095-175">3306</span></span> | <span data-ttu-id="34095-176">The default port for MySQL is used.</span><span class="sxs-lookup"><span data-stu-id="34095-176">The default port for MySQL is used.</span></span> |
| <span data-ttu-id="34095-177">Username</span><span class="sxs-lookup"><span data-stu-id="34095-177">Username</span></span> | myadmin@mydemoserver | <span data-ttu-id="34095-178">The server admin login you previously noted.</span><span class="sxs-lookup"><span data-stu-id="34095-178">The server admin login you previously noted.</span></span> |
| <span data-ttu-id="34095-179">Password</span><span class="sxs-lookup"><span data-stu-id="34095-179">Password</span></span> | **** | <span data-ttu-id="34095-180">Use the admin account password you configured earlier.</span><span class="sxs-lookup"><span data-stu-id="34095-180">Use the admin account password you configured earlier.</span></span> |

<span data-ttu-id="34095-181">Click **Test Connection** to test if all parameters are correctly configured.</span><span class="sxs-lookup"><span data-stu-id="34095-181">Click **Test Connection** to test if all parameters are correctly configured.</span></span>
<span data-ttu-id="34095-182">Now, you can click the connection to successfully connect to the server.</span><span class="sxs-lookup"><span data-stu-id="34095-182">Now, you can click the connection to successfully connect to the server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="34095-183">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="34095-183">Clean up resources</span></span>
<span data-ttu-id="34095-184">If you don't need these resources for another quickstart/tutorial, you can delete them by doing the following command:</span><span class="sxs-lookup"><span data-stu-id="34095-184">If you don't need these resources for another quickstart/tutorial, you can delete them by doing the following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="34095-185">If you would just like to delete the one newly created server, you can run **[az mysql server delete](/cli/azure/mysql/server#az-mysql-server-delete)** command.</span><span class="sxs-lookup"><span data-stu-id="34095-185">If you would just like to delete the one newly created server, you can run **[az mysql server delete](/cli/azure/mysql/server#az-mysql-server-delete)** command.</span></span>
```azurecli-interactive
az mysql server delete --resource-group myresourcegroup --name mydemoserver
```

## <a name="next-steps"></a><span data-ttu-id="34095-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="34095-186">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="34095-187">Design a MySQL Database with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="34095-187">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
