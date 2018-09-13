---
title: Query across cloud databases with different schema | Microsoft Docs
description: how to set up cross-database queries over vertical partitions
services: sql-database
manager: craigg
author: MladjoA
ms.service: sql-database
ms.custom: scale out apps
ms.topic: conceptual
ms.date: 04/01/2018
ms.author: mlandzic
ms.openlocfilehash: 29f477a5f6c8583f6224cb216356606129fedb81
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44770490"
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="b0338-103">Query across cloud databases with different schemas (preview)</span><span class="sxs-lookup"><span data-stu-id="b0338-103">Query across cloud databases with different schemas (preview)</span></span>
![Query across tables in different databases][1]

<span data-ttu-id="b0338-105">Vertically-partitioned databases use different sets of tables on different databases.</span><span class="sxs-lookup"><span data-stu-id="b0338-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="b0338-106">That means that the schema is different on different databases.</span><span class="sxs-lookup"><span data-stu-id="b0338-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="b0338-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span><span class="sxs-lookup"><span data-stu-id="b0338-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b0338-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b0338-108">Prerequisites</span></span>
* <span data-ttu-id="b0338-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span><span class="sxs-lookup"><span data-stu-id="b0338-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="b0338-110">This permission is included with the ALTER DATABASE permission.</span><span class="sxs-lookup"><span data-stu-id="b0338-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="b0338-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span><span class="sxs-lookup"><span data-stu-id="b0338-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="b0338-112">Overview</span><span class="sxs-lookup"><span data-stu-id="b0338-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="b0338-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span><span class="sxs-lookup"><span data-stu-id="b0338-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="b0338-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="b0338-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="b0338-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="b0338-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="b0338-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="b0338-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="b0338-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="b0338-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="b0338-118">Create database scoped master key and credentials</span><span class="sxs-lookup"><span data-stu-id="b0338-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="b0338-119">The credential is used by the elastic query to connect to your remote databases.</span><span class="sxs-lookup"><span data-stu-id="b0338-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'master_key_password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="b0338-120">Ensure that the `<username>` does not include any **"\@servername"** suffix.</span><span class="sxs-lookup"><span data-stu-id="b0338-120">Ensure that the `<username>` does not include any **"\@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="b0338-121">Create external data sources</span><span class="sxs-lookup"><span data-stu-id="b0338-121">Create external data sources</span></span>
<span data-ttu-id="b0338-122">Syntax:</span><span class="sxs-lookup"><span data-stu-id="b0338-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="b0338-123">The TYPE parameter must be set to **RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="b0338-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="b0338-124">Example</span><span class="sxs-lookup"><span data-stu-id="b0338-124">Example</span></span>
<span data-ttu-id="b0338-125">The following example illustrates the use of the CREATE statement for external data sources.</span><span class="sxs-lookup"><span data-stu-id="b0338-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="b0338-126">To retrieve the list of current external data sources:</span><span class="sxs-lookup"><span data-stu-id="b0338-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="b0338-127">External Tables</span><span class="sxs-lookup"><span data-stu-id="b0338-127">External Tables</span></span>
<span data-ttu-id="b0338-128">Syntax:</span><span class="sxs-lookup"><span data-stu-id="b0338-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="b0338-129">Example</span><span class="sxs-lookup"><span data-stu-id="b0338-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="b0338-130">The following example shows how to retrieve the list of external tables from the current database:</span><span class="sxs-lookup"><span data-stu-id="b0338-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="b0338-131">Remarks</span><span class="sxs-lookup"><span data-stu-id="b0338-131">Remarks</span></span>
<span data-ttu-id="b0338-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span><span class="sxs-lookup"><span data-stu-id="b0338-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="b0338-133">An external table definition for vertical partitioning covers the following aspects:</span><span class="sxs-lookup"><span data-stu-id="b0338-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="b0338-134">**Schema**: The external table DDL defines a schema that your queries can use.</span><span class="sxs-lookup"><span data-stu-id="b0338-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="b0338-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span><span class="sxs-lookup"><span data-stu-id="b0338-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="b0338-136">**Remote database reference**: The external table DDL refers to an external data source.</span><span class="sxs-lookup"><span data-stu-id="b0338-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="b0338-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span><span class="sxs-lookup"><span data-stu-id="b0338-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="b0338-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span><span class="sxs-lookup"><span data-stu-id="b0338-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="b0338-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span><span class="sxs-lookup"><span data-stu-id="b0338-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="b0338-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span><span class="sxs-lookup"><span data-stu-id="b0338-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="b0338-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span><span class="sxs-lookup"><span data-stu-id="b0338-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="b0338-142">The following DDL statement drops an existing external table definition from the local catalog.</span><span class="sxs-lookup"><span data-stu-id="b0338-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="b0338-143">It does not impact the remote database.</span><span class="sxs-lookup"><span data-stu-id="b0338-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="b0338-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span><span class="sxs-lookup"><span data-stu-id="b0338-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="b0338-145">Security considerations</span><span class="sxs-lookup"><span data-stu-id="b0338-145">Security considerations</span></span>
<span data-ttu-id="b0338-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span><span class="sxs-lookup"><span data-stu-id="b0338-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="b0338-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span><span class="sxs-lookup"><span data-stu-id="b0338-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="b0338-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span><span class="sxs-lookup"><span data-stu-id="b0338-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="b0338-149">Example: querying vertically partitioned databases</span><span class="sxs-lookup"><span data-stu-id="b0338-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="b0338-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span><span class="sxs-lookup"><span data-stu-id="b0338-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="b0338-151">This is an example of the reference data use case for elastic query:</span><span class="sxs-lookup"><span data-stu-id="b0338-151">This is an example of the reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="b0338-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="b0338-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="b0338-153">Elastic query also introduces a stored procedure that provides direct access to the remote database.</span><span class="sxs-lookup"><span data-stu-id="b0338-153">Elastic query also introduces a stored procedure that provides direct access to the remote database.</span></span> <span data-ttu-id="b0338-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote database.</span><span class="sxs-lookup"><span data-stu-id="b0338-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote database.</span></span> <span data-ttu-id="b0338-155">It takes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="b0338-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="b0338-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span><span class="sxs-lookup"><span data-stu-id="b0338-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="b0338-157">Query (nvarchar): The T-SQL query to be executed on the remote database.</span><span class="sxs-lookup"><span data-stu-id="b0338-157">Query (nvarchar): The T-SQL query to be executed on the remote database.</span></span> 
* <span data-ttu-id="b0338-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="b0338-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="b0338-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="b0338-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="b0338-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote database.</span><span class="sxs-lookup"><span data-stu-id="b0338-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote database.</span></span> <span data-ttu-id="b0338-161">It uses the credential of the external data source to connect to the remote database.</span><span class="sxs-lookup"><span data-stu-id="b0338-161">It uses the credential of the external data source to connect to the remote database.</span></span>  

<span data-ttu-id="b0338-162">Example:</span><span class="sxs-lookup"><span data-stu-id="b0338-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="b0338-163">Connectivity for tools</span><span class="sxs-lookup"><span data-stu-id="b0338-163">Connectivity for tools</span></span>
<span data-ttu-id="b0338-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span><span class="sxs-lookup"><span data-stu-id="b0338-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="b0338-165">Make sure that SQL Server is supported as a data source for your tool.</span><span class="sxs-lookup"><span data-stu-id="b0338-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="b0338-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span><span class="sxs-lookup"><span data-stu-id="b0338-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="b0338-167">Best practices</span><span class="sxs-lookup"><span data-stu-id="b0338-167">Best practices</span></span>
* <span data-ttu-id="b0338-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span><span class="sxs-lookup"><span data-stu-id="b0338-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="b0338-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span><span class="sxs-lookup"><span data-stu-id="b0338-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="b0338-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span><span class="sxs-lookup"><span data-stu-id="b0338-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="b0338-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span><span class="sxs-lookup"><span data-stu-id="b0338-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="b0338-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span><span class="sxs-lookup"><span data-stu-id="b0338-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b0338-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0338-173">Next steps</span></span>

* <span data-ttu-id="b0338-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0338-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="b0338-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="b0338-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="b0338-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b0338-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="b0338-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="b0338-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="b0338-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span><span class="sxs-lookup"><span data-stu-id="b0338-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
