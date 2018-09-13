---
title: Migrate existing databases to scale-out | Microsoft Docs
description: Convert sharded databases to use elastic database tools by creating a shard map manager
services: sql-database
documentationcenter: ''
author: ddove
manager: jhubbard
editor: ''
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: multiple databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: abc673e3b3b786abbfcb21197b2428fc7fc53b6d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661923"
---
# <a name="migrate-existing-databases-to-scale-out"></a>Migrate existing databases to scale-out
Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)). You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Overview
To migrate an existing sharded database: 

1. Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).
2. Create the shard map.
3. Prepare the individual shards.  
4. Add mappings to the shard map.

These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). The examples here use the PowerShell scripts.

For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md). For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).

## <a name="prepare-the-shard-map-manager-database"></a>Prepare the shard map manager database
The shard map manager is a special database that contains the data to manage scaled-out databases. You can use an existing database, or create a new database. Note that a database acting as shard map manager should not be the same database as a shard. Also note that the PowerShell script does not create the database for you. 

## <a name="step-1-create-a-shard-map-manager"></a>Step 1: create a shard map manager
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are the server name and database name 
    # for the new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="to-retrieve-the-shard-map-manager"></a>To retrieve the shard map manager
After creation, you can retrieve the shard map manager with this cmdlet. This step is needed every time you need to use the ShardMapManager object.

    # Try to get a reference to the Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-the-shard-map"></a>Step 2: create the shard map
You must select the type of shard map to create. The choice depends on the database architecture: 

1. Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).) 
2. Multiple tenants per database (two types):
   1. List mapping
   2. Range mapping

For a single-tenant model, create a **list mapping** shard map. The single-tenant model assigns one database per tenant. This is an effective model for SaaS developers as it simplifies management.

![List mapping][1]

The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases). Use this model when you expect each tenant to have small data needs. In this model, we assign a range of tenants to a database using **range mapping**. 

![Range mapping][2]

Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database. For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10. 

![Muliple tenants on single DB][3] 

**Based on your choice, choose one of these options:**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Option 1: create a shard map for a list mapping
Create a shard map using the ShardMapManager object. 

    # $ShardMapManager is the shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Option 2: create a shard map for a range mapping
Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.

    # $ShardMapManager is the shard map manager object 
    # 'RangeShardMap' is the unique identifier for the range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Option 3: List mappings on a single database
Setting up this pattern also requires creation of a list map as shown in step 2, option 1.

## <a name="step-3-prepare-individual-shards"></a>Step 3: Prepare individual shards
Add each shard (database) to the shard map manager. This prepares the individual databases for storing mapping information. Execute this method on each shard.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # The $ShardMap is the shard map created in step 2.


## <a name="step-4-add-mappings"></a>Step 4: Add mappings
The addition of mappings depends on the kind of shard map you created. If you created a list map, you add list mappings. If you created a range map, you add range mappings.

### <a name="option-1-map-the-data-for-a-list-mapping"></a>Option 1: map the data for a list mapping
Map the data by adding a list mapping for each tenant.  

    # Create the mappings and associate it with the new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-the-data-for-a-range-mapping"></a>Option 2: map the data for a range mapping
Add the range mappings for all the tenant id range - database associations:

    # Create the mappings and associate it with the new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-the-data-for-multiple-tenants-on-a-single-database"></a>Step 4 option 3: map the data for multiple tenants on a single database
For each tenant, run the Add-ListMapping (option 1, above). 

## <a name="checking-the-mappings"></a>Checking the mappings
Information about the existing shards and the mappings associated with them can be queried using following commands:  

    # List the shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Summary
Once you have completed the setup, you can begin to use the Elastic Database client library. You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Next steps
Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).

Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model. See [Split merge tool](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Additional resources
For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).

## <a name="questions-and-feature-requests"></a>Questions and Feature Requests
For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png




