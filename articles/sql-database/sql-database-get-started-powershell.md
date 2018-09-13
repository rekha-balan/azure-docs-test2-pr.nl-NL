---
title: 'Azure PowerShell: Create a SQL database | Microsoft Docs'
description: Learn how to create a SQL Database logical server, server-level firewall rule, and databases in the Azure portal.
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
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: bb8fcd907a03350dc21106944e72e6f06109b5f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562783"
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="298c6-104">Create a single Azure SQL database using PowerShell</span><span class="sxs-lookup"><span data-stu-id="298c6-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="298c6-105">PowerShell is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="298c6-105">PowerShell is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="298c6-106">This guide details using PowerShell to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="298c6-106">This guide details using PowerShell to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="298c6-107">To complete this tutorial, make sure you have installed the latest [Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="298c6-107">To complete this tutorial, make sure you have installed the latest [Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> 

<span data-ttu-id="298c6-108">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="298c6-108">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="298c6-109">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="298c6-109">Log in to Azure</span></span>

<span data-ttu-id="298c6-110">Log in to your Azure subscription using the [Add-AzureRmAccount](https://docs.microsoft.com/powershell/resourcemanager/azurerm.profile/v2.5.0/add-azurermaccount) command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="298c6-110">Log in to your Azure subscription using the [Add-AzureRmAccount](https://docs.microsoft.com/powershell/resourcemanager/azurerm.profile/v2.5.0/add-azurermaccount) command and follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="298c6-111">Create variables</span><span class="sxs-lookup"><span data-stu-id="298c6-111">Create variables</span></span>

<span data-ttu-id="298c6-112">Define variables for use in the scripts in this quick start.</span><span class="sxs-lookup"><span data-stu-id="298c6-112">Define variables for use in the scripts in this quick start.</span></span>

```powershell
# The data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# The logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# The login information for the server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The ip address range that you want to allow to access your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.1"
# The database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="298c6-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="298c6-113">Create a resource group</span></span>

<span data-ttu-id="298c6-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="298c6-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="298c6-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span><span class="sxs-lookup"><span data-stu-id="298c6-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="298c6-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span><span class="sxs-lookup"><span data-stu-id="298c6-116">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="298c6-117">Create a logical server</span><span class="sxs-lookup"><span data-stu-id="298c6-117">Create a logical server</span></span>

<span data-ttu-id="298c6-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [New-AzureRmSqlServer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) command.</span><span class="sxs-lookup"><span data-stu-id="298c6-118">Create an [Azure SQL Database logical server](sql-database-features.md) using the [New-AzureRmSqlServer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserver) command.</span></span> <span data-ttu-id="298c6-119">A logical server contains a group of databases managed as a group.</span><span class="sxs-lookup"><span data-stu-id="298c6-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="298c6-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="298c6-120">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="298c6-121">Replace these pre-defined values as desired.</span><span class="sxs-lookup"><span data-stu-id="298c6-121">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="298c6-122">Configure a server firewall rule</span><span class="sxs-lookup"><span data-stu-id="298c6-122">Configure a server firewall rule</span></span>

<span data-ttu-id="298c6-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [New-AzureRmSqlServerFirewallRule](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserverfirewallrule) command.</span><span class="sxs-lookup"><span data-stu-id="298c6-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [New-AzureRmSqlServerFirewallRule](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="298c6-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span><span class="sxs-lookup"><span data-stu-id="298c6-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="298c6-125">In the following example, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="298c6-125">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="298c6-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span><span class="sxs-lookup"><span data-stu-id="298c6-126">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="298c6-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span><span class="sxs-lookup"><span data-stu-id="298c6-127">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="298c6-128">SQL Database communicates over port 1433.</span><span class="sxs-lookup"><span data-stu-id="298c6-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="298c6-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span><span class="sxs-lookup"><span data-stu-id="298c6-129">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="298c6-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span><span class="sxs-lookup"><span data-stu-id="298c6-130">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-blank-database"></a><span data-ttu-id="298c6-131">Create a blank database</span><span class="sxs-lookup"><span data-stu-id="298c6-131">Create a blank database</span></span>

<span data-ttu-id="298c6-132">Create a blank SQL database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [New-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) command.</span><span class="sxs-lookup"><span data-stu-id="298c6-132">Create a blank SQL database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [New-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/resourcemanager/azurerm.sql/v2.5.0/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="298c6-133">The following example creates a database called `mySampleDatabase`.</span><span class="sxs-lookup"><span data-stu-id="298c6-133">The following example creates a database called `mySampleDatabase`.</span></span> <span data-ttu-id="298c6-134">Replace this predefined value as desired.</span><span class="sxs-lookup"><span data-stu-id="298c6-134">Replace this predefined value as desired.</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName databasename `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="298c6-135">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="298c6-135">Clean up resources</span></span>

<span data-ttu-id="298c6-136">Other quick starts in this collection build upon this quick start.</span><span class="sxs-lookup"><span data-stu-id="298c6-136">Other quick starts in this collection build upon this quick start.</span></span> <span data-ttu-id="298c6-137">If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this quick start.</span><span class="sxs-lookup"><span data-stu-id="298c6-137">If you plan to continue on to work with subsequent quick starts or with the tutorials, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="298c6-138">If you do not plan to continue, use the following command to delete all resources created by this quick start.</span><span class="sxs-lookup"><span data-stu-id="298c6-138">If you do not plan to continue, use the following command to delete all resources created by this quick start.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="298c6-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="298c6-139">Next steps</span></span>

- <span data-ttu-id="298c6-140">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span><span class="sxs-lookup"><span data-stu-id="298c6-140">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md)</span></span>
- <span data-ttu-id="298c6-141">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="298c6-141">To connect and query using Visual Studio Code, see [Connect and query with Visual Studio Code](sql-database-connect-query-vscode.md).</span></span>
- <span data-ttu-id="298c6-142">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="298c6-142">To connect and query using .NET, see [Connect and query with .NET](sql-database-connect-query-dotnet.md).</span></span>
- <span data-ttu-id="298c6-143">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span><span class="sxs-lookup"><span data-stu-id="298c6-143">To connect and query using PHP, see [Connect and query with PHP](sql-database-connect-query-php.md).</span></span>
- <span data-ttu-id="298c6-144">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="298c6-144">To connect and query using Node.js, see [Connect and query with Node.js](sql-database-connect-query-nodejs.md).</span></span>
- <span data-ttu-id="298c6-145">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span><span class="sxs-lookup"><span data-stu-id="298c6-145">To connect and query using Java, see [Connect and query with Java](sql-database-connect-query-java.md).</span></span>
- <span data-ttu-id="298c6-146">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span><span class="sxs-lookup"><span data-stu-id="298c6-146">To connect and query using Python, see [Connect and query with Python](sql-database-connect-query-python.md).</span></span>
- <span data-ttu-id="298c6-147">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span><span class="sxs-lookup"><span data-stu-id="298c6-147">To connect and query using Ruby, see [Connect and query with Ruby](sql-database-connect-query-ruby.md).</span></span>
