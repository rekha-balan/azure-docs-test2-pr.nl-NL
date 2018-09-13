---
title: Create SQL Data Warehouse by using PowerShell | Microsoft Docs
description: Create SQL Data Warehouse by using PowerShell
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: f10c22bc1148e34af176fe50e1823ee16ae3a8f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556495"
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="1ba08-103">Create SQL Data Warehouse using PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ba08-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="1ba08-107">This article shows you how to create a SQL Data Warehouse using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ba08-107">This article shows you how to create a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ba08-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1ba08-108">Prerequisites</span></span>
<span data-ttu-id="1ba08-109">To get started, you need:</span><span class="sxs-lookup"><span data-stu-id="1ba08-109">To get started, you need:</span></span>

* <span data-ttu-id="1ba08-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span><span class="sxs-lookup"><span data-stu-id="1ba08-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="1ba08-111">**Azure SQL server**:  See [Create an Azure SQL database in the Azure Portal][Create an Azure SQL database in the Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span><span class="sxs-lookup"><span data-stu-id="1ba08-111">**Azure SQL server**:  See [Create an Azure SQL database in the Azure Portal][Create an Azure SQL database in the Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="1ba08-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1ba08-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="1ba08-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="1ba08-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="1ba08-114">The latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="1ba08-114">The latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="1ba08-115">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="1ba08-115">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

> [!NOTE]
> Creating a SQL Data Warehouse may result in a new billable service.  See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="1ba08-118">Create a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1ba08-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="1ba08-119">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ba08-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="1ba08-120">Run this cmdlet to login to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1ba08-120">Run this cmdlet to login to Azure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="1ba08-121">Select the subscription you want to use for your current session.</span><span class="sxs-lookup"><span data-stu-id="1ba08-121">Select the subscription you want to use for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="1ba08-122">Create database.</span><span class="sxs-lookup"><span data-stu-id="1ba08-122">Create database.</span></span> <span data-ttu-id="1ba08-123">This example creates a database named "mynewsqldw", with service objective level "DW400", to the server named "sqldwserver1", which is in the resource group named "mywesteuroperesgp1".</span><span class="sxs-lookup"><span data-stu-id="1ba08-123">This example creates a database named "mynewsqldw", with service objective level "DW400", to the server named "sqldwserver1", which is in the resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="1ba08-124">Required Parameters are:</span><span class="sxs-lookup"><span data-stu-id="1ba08-124">Required Parameters are:</span></span>

* <span data-ttu-id="1ba08-125">**RequestedServiceObjectiveName**: The amount of [DWU][DWU] you are requesting.</span><span class="sxs-lookup"><span data-stu-id="1ba08-125">**RequestedServiceObjectiveName**: The amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="1ba08-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span><span class="sxs-lookup"><span data-stu-id="1ba08-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="1ba08-127">**DatabaseName**: The name of the SQL Data Warehouse that you are creating.</span><span class="sxs-lookup"><span data-stu-id="1ba08-127">**DatabaseName**: The name of the SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="1ba08-128">**ServerName**: The name of the server that you are using for creation (must be V12).</span><span class="sxs-lookup"><span data-stu-id="1ba08-128">**ServerName**: The name of the server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="1ba08-129">**ResourceGroupName**: Resource group you are using.</span><span class="sxs-lookup"><span data-stu-id="1ba08-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="1ba08-130">To find available resource groups in your subscription use Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="1ba08-130">To find available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="1ba08-131">**Edition**: Must be "DataWarehouse" to create a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1ba08-131">**Edition**: Must be "DataWarehouse" to create a SQL Data Warehouse.</span></span>

<span data-ttu-id="1ba08-132">Optional Parameters are:</span><span class="sxs-lookup"><span data-stu-id="1ba08-132">Optional Parameters are:</span></span>

* <span data-ttu-id="1ba08-133">**CollationName**: The default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="1ba08-133">**CollationName**: The default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="1ba08-134">Collation cannot be changed on a database.</span><span class="sxs-lookup"><span data-stu-id="1ba08-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="1ba08-135">**MaxSizeBytes**: The default max size of a database is 10 GB.</span><span class="sxs-lookup"><span data-stu-id="1ba08-135">**MaxSizeBytes**: The default max size of a database is 10 GB.</span></span>

<span data-ttu-id="1ba08-136">For more details on the parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="1ba08-136">For more details on the parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ba08-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ba08-137">Next steps</span></span>
<span data-ttu-id="1ba08-138">After your SQL Data Warehouse has finished provisioning you may want to try [loading sample data][loading sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span><span class="sxs-lookup"><span data-stu-id="1ba08-138">After your SQL Data Warehouse has finished provisioning you may want to try [loading sample data][loading sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="1ba08-139">If you're interested in more on how to manage SQL Data Warehouse programmatically, check out our article on how to use [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="1ba08-139">If you're interested in more on how to manage SQL Data Warehouse programmatically, check out our article on how to use [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how to create a SQL Data Warehouse from the Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
