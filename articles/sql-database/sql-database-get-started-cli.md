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
# <a name="create-a-single-azure-sql-database-using-the-azure-cli"></a><span data-ttu-id="15fd2-104">Create a single Azure SQL database using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15fd2-104">Create a single Azure SQL database using the Azure CLI</span></span>

<span data-ttu-id="15fd2-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="15fd2-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="15fd2-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="15fd2-106">This guide details using the Azure CLI to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="15fd2-107">To complete this quick start, make sure you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="15fd2-107">To complete this quick start, make sure you have installed the latest [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="15fd2-108">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="15fd2-108">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="15fd2-109">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="15fd2-109">Log in to Azure</span></span>

<span data-ttu-id="15fd2-110">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="15fd2-110">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="define-variables"></a><span data-ttu-id="15fd2-111">Define variables</span><span class="sxs-lookup"><span data-stu-id="15fd2-111">Define variables</span></span>

<span data-ttu-id="15fd2-112">Define variables for use in the scripts in this quick start.</span><span class="sxs-lookup"><span data-stu-id="15fd2-112">Define variables for use in the scripts in this quick start.</span></span>

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

## <a name="create-a-resource-group"></a><span data-ttu-id="15fd2-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="15fd2-113">Create a resource group</span></span>

<span data-ttu-id="15fd2-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span><span class="sxs-lookup"><span data-stu-id="15fd2-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="15fd2-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span><span class="sxs-lookup"><span data-stu-id="15fd2-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="15fd2-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span><span class="sxs-lookup"><span data-stu-id="15fd2-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```azurecli
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="15fd2-117">Create a logical server</span><span class="sxs-lookup"><span data-stu-id="15fd2-117">Create a logical server</span></span>

<span data-ttu-id="15fd2-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span><span class="sxs-lookup"><span data-stu-id="15fd2-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="15fd2-119">A logical server contains a group of databases managed as a group.</span><span class="sxs-lookup"><span data-stu-id="15fd2-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="15fd2-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="15fd2-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="15fd2-121">Replace these pre-defined values as desired.</span><span class="sxs-lookup"><span data-stu-id="15fd2-121">Replace these pre-defined values as desired.</span></span>

```azurecli
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="15fd2-122">Configure a server firewall rule</span><span class="sxs-lookup"><span data-stu-id="15fd2-122">Configure a server firewall rule</span></span>

<span data-ttu-id="15fd2-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span><span class="sxs-lookup"><span data-stu-id="15fd2-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="15fd2-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span><span class="sxs-lookup"><span data-stu-id="15fd2-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="15fd2-125">In the following example, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="15fd2-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="15fd2-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span><span class="sxs-lookup"><span data-stu-id="15fd2-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="15fd2-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span><span class="sxs-lookup"><span data-stu-id="15fd2-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>  

```azurecli
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="15fd2-128">SQL Database communicates over port 1433.</span><span class="sxs-lookup"><span data-stu-id="15fd2-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="15fd2-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span><span class="sxs-lookup"><span data-stu-id="15fd2-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="15fd2-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span><span class="sxs-lookup"><span data-stu-id="15fd2-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="15fd2-131">Create a database in the server with sample data</span><span class="sxs-lookup"><span data-stu-id="15fd2-131">Create a database in the server with sample data</span></span>

<span data-ttu-id="15fd2-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span><span class="sxs-lookup"><span data-stu-id="15fd2-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="15fd2-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span><span class="sxs-lookup"><span data-stu-id="15fd2-133">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="15fd2-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span><span class="sxs-lookup"><span data-stu-id="15fd2-134">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```azurecli
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="15fd2-135">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="15fd2-135">Clean up resources</span></span>

<span data-ttu-id="15fd2-136">Other quick starts in this collection build upon this quick start.</span><span class="sxs-lookup"><span data-stu-id="15fd2-136">Other quick starts in this collection build upon this quick start.</span></span> <span data-ttu-id="15fd2-137">If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this quick start.</span><span class="sxs-lookup"><span data-stu-id="15fd2-137">If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="15fd2-138">If you do not plan to continue, use the following command to delete all resources created by this quick start.</span><span class="sxs-lookup"><span data-stu-id="15fd2-138">If you do not plan to continue, use the following command to delete all resources created by this quick start.</span></span>

```azurecli
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="15fd2-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="15fd2-139">Next steps</span></span>

- <span data-ttu-id="15fd2-140">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="15fd2-140">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="15fd2-141">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="15fd2-141">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="15fd2-142">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="15fd2-142">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="15fd2-143">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="15fd2-143">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="15fd2-144">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="15fd2-144">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="15fd2-145">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="15fd2-145">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="15fd2-146">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="15fd2-146">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="15fd2-147">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="15fd2-147">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
