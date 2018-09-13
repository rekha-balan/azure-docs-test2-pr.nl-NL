---
title: Report across scaled-out cloud databases (horizontal partitioning) | Microsoft Docs
description: how to use cross database database queries
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: e21c338c03d89d34d7508d6f92f8450d9744c735
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661379"
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="0e1c0-103">Report across scaled-out cloud databases (preview)</span><span class="sxs-lookup"><span data-stu-id="0e1c0-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="0e1c0-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="0e1c0-105">The databases must be horizontally partitioned (also known as "sharded").</span><span class="sxs-lookup"><span data-stu-id="0e1c0-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="0e1c0-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="0e1c0-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e1c0-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0e1c0-108">Prerequisites</span></span>
<span data-ttu-id="0e1c0-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="0e1c0-110">Create a shard map manager using the sample app</span><span class="sxs-lookup"><span data-stu-id="0e1c0-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="0e1c0-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="0e1c0-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="0e1c0-113">Build and run the **Getting started with Elastic Database tools** sample application.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="0e1c0-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="0e1c0-115">At the end of Step 7, you will see the following command prompt:</span><span class="sxs-lookup"><span data-stu-id="0e1c0-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![command prompt][1]
2. <span data-ttu-id="0e1c0-117">In the command window, type "1" and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="0e1c0-118">This creates the shard map manager, and adds two shards to the server.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="0e1c0-119">Then type "3" and press **Enter**; repeat the action four times.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="0e1c0-120">This inserts sample data rows in your shards.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="0e1c0-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span><span class="sxs-lookup"><span data-stu-id="0e1c0-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio confirmation][2]

   <span data-ttu-id="0e1c0-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="0e1c0-124">For example, use option 4 in the command window.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="0e1c0-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="0e1c0-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="0e1c0-127">Create an elastic query database</span><span class="sxs-lookup"><span data-stu-id="0e1c0-127">Create an elastic query database</span></span>
1. <span data-ttu-id="0e1c0-128">Open the [Azure portal](https://portal.azure.com) and log in.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="0e1c0-129">Create a new Azure SQL database in the same server as your shard setup.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="0e1c0-130">Name the database "ElasticDBQuery."</span><span class="sxs-lookup"><span data-stu-id="0e1c0-130">Name the database "ElasticDBQuery."</span></span>

    ![Azure portal and pricing tier][3]

    > [!NOTE]
    > <span data-ttu-id="0e1c0-132">you can use an existing database.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-132">you can use an existing database.</span></span> <span data-ttu-id="0e1c0-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="0e1c0-134">This database will be used for creating the metadata objects for an elastic database query.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="0e1c0-135">Create database objects</span><span class="sxs-lookup"><span data-stu-id="0e1c0-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="0e1c0-136">Database-scoped master key and credentials</span><span class="sxs-lookup"><span data-stu-id="0e1c0-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="0e1c0-137">These are used to connect to the shard map manager and the shards:</span><span class="sxs-lookup"><span data-stu-id="0e1c0-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="0e1c0-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="0e1c0-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span><span class="sxs-lookup"><span data-stu-id="0e1c0-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="0e1c0-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="0e1c0-141">External data sources</span><span class="sxs-lookup"><span data-stu-id="0e1c0-141">External data sources</span></span>
<span data-ttu-id="0e1c0-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span><span class="sxs-lookup"><span data-stu-id="0e1c0-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="0e1c0-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="0e1c0-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="0e1c0-145">External tables</span><span class="sxs-lookup"><span data-stu-id="0e1c0-145">External tables</span></span>
<span data-ttu-id="0e1c0-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span><span class="sxs-lookup"><span data-stu-id="0e1c0-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="0e1c0-147">Execute a sample elastic database T-SQL query</span><span class="sxs-lookup"><span data-stu-id="0e1c0-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="0e1c0-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="0e1c0-149">Execute this query on the ElasticDBQuery database:</span><span class="sxs-lookup"><span data-stu-id="0e1c0-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="0e1c0-150">You will notice that the query aggregates results from all the shards and gives the following output:</span><span class="sxs-lookup"><span data-stu-id="0e1c0-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![Output details][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="0e1c0-152">Import elastic database query results to Excel</span><span class="sxs-lookup"><span data-stu-id="0e1c0-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="0e1c0-153">You can import the results from of a query to an Excel file.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="0e1c0-154">Launch Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="0e1c0-155">Navigate to the **Data** ribbon.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="0e1c0-156">Click **From Other Sources** and click **From SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel import from other sources][5]
4. <span data-ttu-id="0e1c0-158">In the **Data Connection Wizard** type the server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="0e1c0-159">Then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-159">Then click **Next**.</span></span>
5. <span data-ttu-id="0e1c0-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="0e1c0-161">Select the **Customers** table in the list view and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="0e1c0-162">Then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="0e1c0-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="0e1c0-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="0e1c0-165">You can now use Excel’s powerful data visualization functions.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="0e1c0-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="0e1c0-167">Make sure that SQL Server is supported as a data source for your tool.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="0e1c0-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="0e1c0-169">Cost</span><span class="sxs-lookup"><span data-stu-id="0e1c0-169">Cost</span></span>
<span data-ttu-id="0e1c0-170">There is no additional charge for using the Elastic Database Query feature.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="0e1c0-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e1c0-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="0e1c0-172">Next steps</span></span>

* <span data-ttu-id="0e1c0-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="0e1c0-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="0e1c0-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="0e1c0-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="0e1c0-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="0e1c0-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="0e1c0-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="0e1c0-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span><span class="sxs-lookup"><span data-stu-id="0e1c0-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/portal.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/tiers.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/details.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->





