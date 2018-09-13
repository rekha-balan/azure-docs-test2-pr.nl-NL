---
title: Connect to Azure SQL Data Warehouse - SSMS | Microsoft Docs
description: Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.
services: sql-data-warehouse
author: kavithaj
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: consume
ms.date: 04/17/2018
ms.author: kavithaj
ms.reviewer: igorstan
ms.openlocfilehash: 6079c3064699da38fad20468517eb97d6ab107f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773519"
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="40557-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="40557-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="40557-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="40557-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="40557-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="40557-110">Prerequisites</span></span>
<span data-ttu-id="40557-111">To use this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="40557-111">To use this tutorial, you need:</span></span>

* <span data-ttu-id="40557-112">An existing SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="40557-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="40557-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="40557-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="40557-114">SQL Server Management Studio (SSMS) installed.</span><span class="sxs-lookup"><span data-stu-id="40557-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="40557-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span><span class="sxs-lookup"><span data-stu-id="40557-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="40557-116">The fully qualified SQL server name.</span><span class="sxs-lookup"><span data-stu-id="40557-116">The fully qualified SQL server name.</span></span> <span data-ttu-id="40557-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="40557-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="40557-118">1. Connect to your SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="40557-118">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="40557-119">Open SSMS.</span><span class="sxs-lookup"><span data-stu-id="40557-119">Open SSMS.</span></span>
2. <span data-ttu-id="40557-120">Open Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="40557-120">Open Object Explorer.</span></span> <span data-ttu-id="40557-121">To do this, select **File** > **Connect Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="40557-121">To do this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![SQL Server Object Explorer][1]
3. <span data-ttu-id="40557-123">Fill in the fields in the Connect to Server window.</span><span class="sxs-lookup"><span data-stu-id="40557-123">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Connect to Server][2]
   
   * <span data-ttu-id="40557-125">**Server name**.</span><span class="sxs-lookup"><span data-stu-id="40557-125">**Server name**.</span></span> <span data-ttu-id="40557-126">Enter the **server name** previously identified.</span><span class="sxs-lookup"><span data-stu-id="40557-126">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="40557-127">**Authentication**.</span><span class="sxs-lookup"><span data-stu-id="40557-127">**Authentication**.</span></span> <span data-ttu-id="40557-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span><span class="sxs-lookup"><span data-stu-id="40557-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="40557-129">**User Name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="40557-129">**User Name** and **Password**.</span></span> <span data-ttu-id="40557-130">Enter user name and password if SQL Server Authentication was selected above.</span><span class="sxs-lookup"><span data-stu-id="40557-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="40557-131">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="40557-131">Click **Connect**.</span></span>
4. <span data-ttu-id="40557-132">To explore, expand your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="40557-132">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="40557-133">You can view the databases associated with the server.</span><span class="sxs-lookup"><span data-stu-id="40557-133">You can view the databases associated with the server.</span></span> <span data-ttu-id="40557-134">Expand AdventureWorksDW to see the tables in your sample database.</span><span class="sxs-lookup"><span data-stu-id="40557-134">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Explore AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="40557-136">2. Run a sample query</span><span class="sxs-lookup"><span data-stu-id="40557-136">2. Run a sample query</span></span>
<span data-ttu-id="40557-137">Now that a connection has been established to your database, let's write a query.</span><span class="sxs-lookup"><span data-stu-id="40557-137">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="40557-138">Right-click your database in SQL Server Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="40557-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="40557-139">Select **New Query**.</span><span class="sxs-lookup"><span data-stu-id="40557-139">Select **New Query**.</span></span> <span data-ttu-id="40557-140">A new query window opens.</span><span class="sxs-lookup"><span data-stu-id="40557-140">A new query window opens.</span></span>
   
    ![New query][4]
3. <span data-ttu-id="40557-142">Copy this TSQL query into the query window:</span><span class="sxs-lookup"><span data-stu-id="40557-142">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="40557-143">Run the query.</span><span class="sxs-lookup"><span data-stu-id="40557-143">Run the query.</span></span> <span data-ttu-id="40557-144">To do this, click `Execute` or use the following shortcut: `F5`.</span><span class="sxs-lookup"><span data-stu-id="40557-144">To do this, click `Execute` or use the following shortcut: `F5`.</span></span>
   
    ![Run query][5]
5. <span data-ttu-id="40557-146">Look at the query results.</span><span class="sxs-lookup"><span data-stu-id="40557-146">Look at the query results.</span></span> <span data-ttu-id="40557-147">In this example, the FactInternetSales table has 60398 rows.</span><span class="sxs-lookup"><span data-stu-id="40557-147">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Query results][6]

## <a name="next-steps"></a><span data-ttu-id="40557-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="40557-149">Next steps</span></span>
<span data-ttu-id="40557-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="40557-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="40557-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="40557-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
