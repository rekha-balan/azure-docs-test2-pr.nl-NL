---
title: 'Azure CLI: Create a SQL database | Microsoft Docs'
description: Learn how to create a SQL Database logical server, server-level firewall rule, and databases using the Azure CLI.
keywords: sql database tutorial, create a sql database
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: ''
ms.service: sql-database
ms.custom: quick start create
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 06b6830b28745b0f6574d7bca5cca7907db8ecb1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562687"
---
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a>Create a single Azure SQL database using the Azure CLI

The Azure CLI is used to create and manage Azure resources from the command line or in scripts. This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).

To complete this quick start, make sure you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). 

If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.

## <a name="log-in-to-azure"></a>Log in to Azure

Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.

```azurecli
az login
```

## <a name="define-variables"></a>Define variables

Define variables for use in the scripts in this quick start.

```azurecli
# The data center and resource name for your resources
resourcegroupname = myResourceGroup
location = westeurope
# The logical server name: Use a random value or replace with your own value (do not capitalize)
servername = server-$RANDOM
# Set an admin login and password for your database
adminlogin = ServerAdmin
password = ChangeYourAdminPassword1
# The ip address range that you want to allow to access your DB
startip = "0.0.0.0"
endip = "0.0.0.1"
# The database name
databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>Create a resource group

Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command. A resource group is a logical container into which Azure resources are deployed and managed as a group. The following example creates a resource group named `myResourceGroup` in the `westeurope` location.

```azurecli
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>Create a logical server

Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command. A logical server contains a group of databases managed as a group. The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`. Replace these pre-defined values as desired.

```azurecli
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Configure a server firewall rule

Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command. A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall. In the following example, the firewall is only opened for other Azure resources. To enable external connectivity, change the IP address to an appropriate address for your environment. To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.  

```azurecli
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> SQL Database communicates over port 1433. If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall. If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.
>

## <a name="create-a-database-in-the-server-with-sample-data"></a>Create a database in the server with sample data

Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command. The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database. Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).

```azurecli
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Clean up resources

Other quick starts in this collection build upon this quick start. If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this quick start. If you do not plan to continue, use the following command to delete all resources created by this quick start.

```azurecli
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>Next steps

- To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)
- To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).
- To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).
- To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).
- To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).
- To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).
- To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).
- To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).
