---
title: Connect to Azure SQL Data Warehouse - VSTS | Microsoft Docs
description: Query SQL Data Warehouse with Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 830a6c70e8e30af100f710d458bc51054250ab60
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552150"
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="25b98-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span><span class="sxs-lookup"><span data-stu-id="25b98-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="25b98-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="25b98-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="25b98-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25b98-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="25b98-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="25b98-111">Prerequisites</span></span>
<span data-ttu-id="25b98-112">To use this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="25b98-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="25b98-113">An existing SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="25b98-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="25b98-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="25b98-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="25b98-115">SSDT for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25b98-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="25b98-116">If you have Visual Studio, you probably already have this.</span><span class="sxs-lookup"><span data-stu-id="25b98-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="25b98-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="25b98-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="25b98-118">The fully qualified SQL server name.</span><span class="sxs-lookup"><span data-stu-id="25b98-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="25b98-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="25b98-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="25b98-120">1. Connect to your SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="25b98-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="25b98-121">Open Visual Studio 2013 or 2015.</span><span class="sxs-lookup"><span data-stu-id="25b98-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="25b98-122">Open SQL Server Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="25b98-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="25b98-123">To do this, select **View** > **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="25b98-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server Object Explorer][1]
3. <span data-ttu-id="25b98-125">Click the **Add SQL Server** icon.</span><span class="sxs-lookup"><span data-stu-id="25b98-125">Click the **Add SQL Server** icon.</span></span>
   
    ![Add SQL Server][2]
4. <span data-ttu-id="25b98-127">Fill in the fields in the Connect to Server window.</span><span class="sxs-lookup"><span data-stu-id="25b98-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Connect to Server][3]
   
   * <span data-ttu-id="25b98-129">**Server name**.</span><span class="sxs-lookup"><span data-stu-id="25b98-129">**Server name**.</span></span> <span data-ttu-id="25b98-130">Enter the **server name** previously identified.</span><span class="sxs-lookup"><span data-stu-id="25b98-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="25b98-131">**Authentication**.</span><span class="sxs-lookup"><span data-stu-id="25b98-131">**Authentication**.</span></span> <span data-ttu-id="25b98-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span><span class="sxs-lookup"><span data-stu-id="25b98-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="25b98-133">**User Name** and **Password**.</span><span class="sxs-lookup"><span data-stu-id="25b98-133">**User Name** and **Password**.</span></span> <span data-ttu-id="25b98-134">Enter user name and password if SQL Server Authentication was selected above.</span><span class="sxs-lookup"><span data-stu-id="25b98-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="25b98-135">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="25b98-135">Click **Connect**.</span></span>
5. <span data-ttu-id="25b98-136">To explore, expand your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="25b98-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="25b98-137">You can view the databases associated with the server.</span><span class="sxs-lookup"><span data-stu-id="25b98-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="25b98-138">Expand AdventureWorksDW to see the tables in your sample database.</span><span class="sxs-lookup"><span data-stu-id="25b98-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Explore AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="25b98-140">2. Run a sample query</span><span class="sxs-lookup"><span data-stu-id="25b98-140">2. Run a sample query</span></span>
<span data-ttu-id="25b98-141">Now that a connection has been established to your database, let's write a query.</span><span class="sxs-lookup"><span data-stu-id="25b98-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="25b98-142">Right-click your database in SQL Server Object Explorer.</span><span class="sxs-lookup"><span data-stu-id="25b98-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="25b98-143">Select **New Query**.</span><span class="sxs-lookup"><span data-stu-id="25b98-143">Select **New Query**.</span></span> <span data-ttu-id="25b98-144">A new query window opens.</span><span class="sxs-lookup"><span data-stu-id="25b98-144">A new query window opens.</span></span>
   
    ![New query][5]
3. <span data-ttu-id="25b98-146">Copy this TSQL query into the query window:</span><span class="sxs-lookup"><span data-stu-id="25b98-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="25b98-147">Run the query.</span><span class="sxs-lookup"><span data-stu-id="25b98-147">Run the query.</span></span> <span data-ttu-id="25b98-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span><span class="sxs-lookup"><span data-stu-id="25b98-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Run query][6]
5. <span data-ttu-id="25b98-150">Look at the query results.</span><span class="sxs-lookup"><span data-stu-id="25b98-150">Look at the query results.</span></span> <span data-ttu-id="25b98-151">In this example, the FactInternetSales table has 60398 rows.</span><span class="sxs-lookup"><span data-stu-id="25b98-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Query results][7]

## <a name="next-steps"></a><span data-ttu-id="25b98-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="25b98-153">Next steps</span></span>
<span data-ttu-id="25b98-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="25b98-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="25b98-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="25b98-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-query-visual-studio/query-results.png







