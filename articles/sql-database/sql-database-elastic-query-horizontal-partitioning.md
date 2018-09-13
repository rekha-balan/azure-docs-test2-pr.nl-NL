---
title: Reporting across scaled-out cloud databases | Microsoft Docs
description: how to set up elastic queries over horizontal partitions
services: sql-database
documentationcenter: ''
manager: craigg
author: MladjoA
ms.service: sql-database
ms.custom: scale out apps
ms.topic: conceptual
ms.date: 04/01/2018
ms.author: mlandzic
ms.openlocfilehash: 6efc9da60017914eeeb06bdf3309cae79fac36d6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819057"
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="8393d-103">Reporting across scaled-out cloud databases (preview)</span><span class="sxs-lookup"><span data-stu-id="8393d-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Query across shards][1]

<span data-ttu-id="8393d-105">Sharded databases distribute rows across a scaled out data tier.</span><span class="sxs-lookup"><span data-stu-id="8393d-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="8393d-106">The schema is identical on all participating databases, also known as horizontal partitioning.</span><span class="sxs-lookup"><span data-stu-id="8393d-106">The schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="8393d-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span><span class="sxs-lookup"><span data-stu-id="8393d-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="8393d-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8393d-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="8393d-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="8393d-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8393d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8393d-110">Prerequisites</span></span>
* <span data-ttu-id="8393d-111">Create a shard map using the elastic database client library.</span><span class="sxs-lookup"><span data-stu-id="8393d-111">Create a shard map using the elastic database client library.</span></span> <span data-ttu-id="8393d-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="8393d-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="8393d-113">Or use the sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8393d-113">Or use the sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="8393d-114">Alternatively, see [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="8393d-114">Alternatively, see [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="8393d-115">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span><span class="sxs-lookup"><span data-stu-id="8393d-115">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="8393d-116">This permission is included with the ALTER DATABASE permission.</span><span class="sxs-lookup"><span data-stu-id="8393d-116">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="8393d-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span><span class="sxs-lookup"><span data-stu-id="8393d-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="8393d-118">Overview</span><span class="sxs-lookup"><span data-stu-id="8393d-118">Overview</span></span>
<span data-ttu-id="8393d-119">These statements create the metadata representation of your sharded data tier in the elastic query database.</span><span class="sxs-lookup"><span data-stu-id="8393d-119">These statements create the metadata representation of your sharded data tier in the elastic query database.</span></span> 

1. [<span data-ttu-id="8393d-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="8393d-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="8393d-121">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="8393d-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="8393d-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="8393d-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="8393d-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="8393d-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="8393d-124">1.1 Create database scoped master key and credentials</span><span class="sxs-lookup"><span data-stu-id="8393d-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="8393d-125">The credential is used by the elastic query to connect to your remote databases.</span><span class="sxs-lookup"><span data-stu-id="8393d-125">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="8393d-126">Make sure that the *"\<username\>"* does not include any *"\@servername"* suffix.</span><span class="sxs-lookup"><span data-stu-id="8393d-126">Make sure that the *"\<username\>"* does not include any *"\@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="8393d-127">1.2 Create external data sources</span><span class="sxs-lookup"><span data-stu-id="8393d-127">1.2 Create external data sources</span></span>
<span data-ttu-id="8393d-128">Syntax:</span><span class="sxs-lookup"><span data-stu-id="8393d-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="8393d-129">Example</span><span class="sxs-lookup"><span data-stu-id="8393d-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="8393d-130">Retrieve the list of current external data sources:</span><span class="sxs-lookup"><span data-stu-id="8393d-130">Retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="8393d-131">The external data source references your shard map.</span><span class="sxs-lookup"><span data-stu-id="8393d-131">The external data source references your shard map.</span></span> <span data-ttu-id="8393d-132">An elastic query then uses the external data source and the underlying shard map to enumerate the databases that participate in the data tier.</span><span class="sxs-lookup"><span data-stu-id="8393d-132">An elastic query then uses the external data source and the underlying shard map to enumerate the databases that participate in the data tier.</span></span> <span data-ttu-id="8393d-133">The same credentials are used to read the shard map and to access the data on the shards during the processing of an elastic query.</span><span class="sxs-lookup"><span data-stu-id="8393d-133">The same credentials are used to read the shard map and to access the data on the shards during the processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="8393d-134">1.3 Create external tables</span><span class="sxs-lookup"><span data-stu-id="8393d-134">1.3 Create external tables</span></span>
<span data-ttu-id="8393d-135">Syntax:</span><span class="sxs-lookup"><span data-stu-id="8393d-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="8393d-136">**Example**</span><span class="sxs-lookup"><span data-stu-id="8393d-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="8393d-137">Retrieve the list of external tables from the current database:</span><span class="sxs-lookup"><span data-stu-id="8393d-137">Retrieve the list of external tables from the current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="8393d-138">To drop external tables:</span><span class="sxs-lookup"><span data-stu-id="8393d-138">To drop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="8393d-139">Remarks</span><span class="sxs-lookup"><span data-stu-id="8393d-139">Remarks</span></span>
<span data-ttu-id="8393d-140">The DATA\_SOURCE clause defines the external data source (a shard map) that is used for the external table.</span><span class="sxs-lookup"><span data-stu-id="8393d-140">The DATA\_SOURCE clause defines the external data source (a shard map) that is used for the external table.</span></span>  

<span data-ttu-id="8393d-141">The SCHEMA\_NAME and OBJECT\_NAME clauses map the external table definition to a table in a different schema.</span><span class="sxs-lookup"><span data-stu-id="8393d-141">The SCHEMA\_NAME and OBJECT\_NAME clauses map the external table definition to a table in a different schema.</span></span> <span data-ttu-id="8393d-142">If omitted, the schema of the remote object is assumed to be “dbo” and its name is assumed to be identical to the external table name being defined.</span><span class="sxs-lookup"><span data-stu-id="8393d-142">If omitted, the schema of the remote object is assumed to be “dbo” and its name is assumed to be identical to the external table name being defined.</span></span> <span data-ttu-id="8393d-143">This is useful if the name of your remote table is already taken in the database where you want to create the external table.</span><span class="sxs-lookup"><span data-stu-id="8393d-143">This is useful if the name of your remote table is already taken in the database where you want to create the external table.</span></span> <span data-ttu-id="8393d-144">For  example, you want to define an external table to get an aggregate view of catalog views or DMVs on your scaled out data tier.</span><span class="sxs-lookup"><span data-stu-id="8393d-144">For  example, you want to define an external table to get an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="8393d-145">Since catalog views and DMVs already exist locally, you cannot use their names for the external table definition.</span><span class="sxs-lookup"><span data-stu-id="8393d-145">Since catalog views and DMVs already exist locally, you cannot use their names for the external table definition.</span></span> <span data-ttu-id="8393d-146">Instead, use a different name and use the catalog view’s or the DMV’s name in the SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span><span class="sxs-lookup"><span data-stu-id="8393d-146">Instead, use a different name and use the catalog view’s or the DMV’s name in the SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="8393d-147">(See the example below.)</span><span class="sxs-lookup"><span data-stu-id="8393d-147">(See the example below.)</span></span> 

<span data-ttu-id="8393d-148">The DISTRIBUTION clause specifies the data distribution used for this table.</span><span class="sxs-lookup"><span data-stu-id="8393d-148">The DISTRIBUTION clause specifies the data distribution used for this table.</span></span> <span data-ttu-id="8393d-149">The query processor utilizes the information provided in the DISTRIBUTION clause to build the most efficient query plans.</span><span class="sxs-lookup"><span data-stu-id="8393d-149">The query processor utilizes the information provided in the DISTRIBUTION clause to build the most efficient query plans.</span></span>  

1. <span data-ttu-id="8393d-150">**SHARDED** means data is horizontally partitioned across the databases.</span><span class="sxs-lookup"><span data-stu-id="8393d-150">**SHARDED** means data is horizontally partitioned across the databases.</span></span> <span data-ttu-id="8393d-151">The partitioning key for the data distribution is the **<sharding_column_name>** parameter.</span><span class="sxs-lookup"><span data-stu-id="8393d-151">The partitioning key for the data distribution is the **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="8393d-152">**REPLICATED** means that identical copies of the table are present on each database.</span><span class="sxs-lookup"><span data-stu-id="8393d-152">**REPLICATED** means that identical copies of the table are present on each database.</span></span> <span data-ttu-id="8393d-153">It is your responsibility to ensure that the replicas are identical across the databases.</span><span class="sxs-lookup"><span data-stu-id="8393d-153">It is your responsibility to ensure that the replicas are identical across the databases.</span></span>
3. <span data-ttu-id="8393d-154">**ROUND\_ROBIN** means that the table is horizontally partitioned using an application-dependent distribution method.</span><span class="sxs-lookup"><span data-stu-id="8393d-154">**ROUND\_ROBIN** means that the table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="8393d-155">**Data tier reference**: The external table DDL refers to an external data source.</span><span class="sxs-lookup"><span data-stu-id="8393d-155">**Data tier reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="8393d-156">The external data source specifies a shard map which provides the external table with the information necessary to locate all the databases in your data tier.</span><span class="sxs-lookup"><span data-stu-id="8393d-156">The external data source specifies a shard map which provides the external table with the information necessary to locate all the databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="8393d-157">Security considerations</span><span class="sxs-lookup"><span data-stu-id="8393d-157">Security considerations</span></span>
<span data-ttu-id="8393d-158">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span><span class="sxs-lookup"><span data-stu-id="8393d-158">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="8393d-159">Avoid undesired elevation of privileges through the credential of the external data source.</span><span class="sxs-lookup"><span data-stu-id="8393d-159">Avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="8393d-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span><span class="sxs-lookup"><span data-stu-id="8393d-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="8393d-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span><span class="sxs-lookup"><span data-stu-id="8393d-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="8393d-162">Example: querying horizontal partitioned databases</span><span class="sxs-lookup"><span data-stu-id="8393d-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="8393d-163">The following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span><span class="sxs-lookup"><span data-stu-id="8393d-163">The following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="8393d-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by the warehouse id column, and that the elastic query can co-locate the joins on the shards and process the expensive part of the query on the shards in parallel.</span><span class="sxs-lookup"><span data-stu-id="8393d-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by the warehouse id column, and that the elastic query can co-locate the joins on the shards and process the expensive part of the query on the shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="8393d-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="8393d-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="8393d-166">Elastic query also introduces a stored procedure that provides direct access to the shards.</span><span class="sxs-lookup"><span data-stu-id="8393d-166">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="8393d-167">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span><span class="sxs-lookup"><span data-stu-id="8393d-167">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="8393d-168">It takes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="8393d-168">It takes the following parameters:</span></span> 

* <span data-ttu-id="8393d-169">Data source name (nvarchar): The name of the external data source of type RDBMS.</span><span class="sxs-lookup"><span data-stu-id="8393d-169">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="8393d-170">Query (nvarchar): The T-SQL query to be executed on each shard.</span><span class="sxs-lookup"><span data-stu-id="8393d-170">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="8393d-171">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="8393d-171">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="8393d-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="8393d-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="8393d-173">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span><span class="sxs-lookup"><span data-stu-id="8393d-173">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="8393d-174">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span><span class="sxs-lookup"><span data-stu-id="8393d-174">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="8393d-175">Example:</span><span class="sxs-lookup"><span data-stu-id="8393d-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="8393d-176">Connectivity for tools</span><span class="sxs-lookup"><span data-stu-id="8393d-176">Connectivity for tools</span></span>
<span data-ttu-id="8393d-177">Use regular SQL Server connection strings to connect your application, your BI and data integration tools to the database with your external table definitions.</span><span class="sxs-lookup"><span data-stu-id="8393d-177">Use regular SQL Server connection strings to connect your application, your BI and data integration tools to the database with your external table definitions.</span></span> <span data-ttu-id="8393d-178">Make sure that SQL Server is supported as a data source for your tool.</span><span class="sxs-lookup"><span data-stu-id="8393d-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="8393d-179">Then reference the elastic query database like any other SQL Server database connected to the tool, and use external tables from your tool or application as if they were local tables.</span><span class="sxs-lookup"><span data-stu-id="8393d-179">Then reference the elastic query database like any other SQL Server database connected to the tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="8393d-180">Best practices</span><span class="sxs-lookup"><span data-stu-id="8393d-180">Best practices</span></span>
* <span data-ttu-id="8393d-181">Ensure that the elastic query endpoint database has been given access to the shardmap database and all shards through the SQL DB firewalls.</span><span class="sxs-lookup"><span data-stu-id="8393d-181">Ensure that the elastic query endpoint database has been given access to the shardmap database and all shards through the SQL DB firewalls.</span></span>  
* <span data-ttu-id="8393d-182">Validate or enforce the data distribution defined by the external table.</span><span class="sxs-lookup"><span data-stu-id="8393d-182">Validate or enforce the data distribution defined by the external table.</span></span> <span data-ttu-id="8393d-183">If your actual data distribution is different from the distribution specified in your table definition, your queries may yield unexpected results.</span><span class="sxs-lookup"><span data-stu-id="8393d-183">If your actual data distribution is different from the distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="8393d-184">Elastic query currently does not perform shard elimination when predicates over the sharding key would allow it to safely exclude certain shards from processing.</span><span class="sxs-lookup"><span data-stu-id="8393d-184">Elastic query currently does not perform shard elimination when predicates over the sharding key would allow it to safely exclude certain shards from processing.</span></span>
* <span data-ttu-id="8393d-185">Elastic query works best for queries where most of the computation can be done on the shards.</span><span class="sxs-lookup"><span data-stu-id="8393d-185">Elastic query works best for queries where most of the computation can be done on the shards.</span></span> <span data-ttu-id="8393d-186">You typically get the best query performance with selective filter predicates that can be evaluated on the shards or joins over the partitioning keys that can be performed in a partition-aligned way on all shards.</span><span class="sxs-lookup"><span data-stu-id="8393d-186">You typically get the best query performance with selective filter predicates that can be evaluated on the shards or joins over the partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="8393d-187">Other query patterns may need to load large amounts of data from the shards to the head node and may perform poorly</span><span class="sxs-lookup"><span data-stu-id="8393d-187">Other query patterns may need to load large amounts of data from the shards to the head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="8393d-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="8393d-188">Next steps</span></span>

* <span data-ttu-id="8393d-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8393d-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="8393d-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="8393d-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="8393d-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="8393d-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="8393d-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8393d-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="8393d-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span><span class="sxs-lookup"><span data-stu-id="8393d-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
