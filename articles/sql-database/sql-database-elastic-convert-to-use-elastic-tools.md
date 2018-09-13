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
# <a name="migrate-existing-databases-to-scale-out"></a><span data-ttu-id="01fcc-103">Migrate existing databases to scale-out</span><span class="sxs-lookup"><span data-stu-id="01fcc-103">Migrate existing databases to scale-out</span></span>
<span data-ttu-id="01fcc-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="01fcc-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="01fcc-105">You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="01fcc-105">You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="01fcc-106">Overview</span><span class="sxs-lookup"><span data-stu-id="01fcc-106">Overview</span></span>
<span data-ttu-id="01fcc-107">To migrate an existing sharded database:</span><span class="sxs-lookup"><span data-stu-id="01fcc-107">To migrate an existing sharded database:</span></span> 

1. <span data-ttu-id="01fcc-108">Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="01fcc-108">Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="01fcc-109">Create the shard map.</span><span class="sxs-lookup"><span data-stu-id="01fcc-109">Create the shard map.</span></span>
3. <span data-ttu-id="01fcc-110">Prepare the individual shards.</span><span class="sxs-lookup"><span data-stu-id="01fcc-110">Prepare the individual shards.</span></span>  
4. <span data-ttu-id="01fcc-111">Add mappings to the shard map.</span><span class="sxs-lookup"><span data-stu-id="01fcc-111">Add mappings to the shard map.</span></span>

<span data-ttu-id="01fcc-112">These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="01fcc-112">These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="01fcc-113">The examples here use the PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="01fcc-113">The examples here use the PowerShell scripts.</span></span>

<span data-ttu-id="01fcc-114">For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="01fcc-114">For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="01fcc-115">For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="01fcc-115">For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-the-shard-map-manager-database"></a><span data-ttu-id="01fcc-116">Prepare the shard map manager database</span><span class="sxs-lookup"><span data-stu-id="01fcc-116">Prepare the shard map manager database</span></span>
<span data-ttu-id="01fcc-117">The shard map manager is a special database that contains the data to manage scaled-out databases.</span><span class="sxs-lookup"><span data-stu-id="01fcc-117">The shard map manager is a special database that contains the data to manage scaled-out databases.</span></span> <span data-ttu-id="01fcc-118">You can use an existing database, or create a new database.</span><span class="sxs-lookup"><span data-stu-id="01fcc-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="01fcc-119">Note that a database acting as shard map manager should not be the same database as a shard.</span><span class="sxs-lookup"><span data-stu-id="01fcc-119">Note that a database acting as shard map manager should not be the same database as a shard.</span></span> <span data-ttu-id="01fcc-120">Also note that the PowerShell script does not create the database for you.</span><span class="sxs-lookup"><span data-stu-id="01fcc-120">Also note that the PowerShell script does not create the database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="01fcc-121">Step 1: create a shard map manager</span><span class="sxs-lookup"><span data-stu-id="01fcc-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are the server name and database name 
    # for the new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="to-retrieve-the-shard-map-manager"></a><span data-ttu-id="01fcc-122">To retrieve the shard map manager</span><span class="sxs-lookup"><span data-stu-id="01fcc-122">To retrieve the shard map manager</span></span>
<span data-ttu-id="01fcc-123">After creation, you can retrieve the shard map manager with this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01fcc-123">After creation, you can retrieve the shard map manager with this cmdlet.</span></span> <span data-ttu-id="01fcc-124">This step is needed every time you need to use the ShardMapManager object.</span><span class="sxs-lookup"><span data-stu-id="01fcc-124">This step is needed every time you need to use the ShardMapManager object.</span></span>

    # Try to get a reference to the Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-the-shard-map"></a><span data-ttu-id="01fcc-125">Step 2: create the shard map</span><span class="sxs-lookup"><span data-stu-id="01fcc-125">Step 2: create the shard map</span></span>
<span data-ttu-id="01fcc-126">You must select the type of shard map to create.</span><span class="sxs-lookup"><span data-stu-id="01fcc-126">You must select the type of shard map to create.</span></span> <span data-ttu-id="01fcc-127">The choice depends on the database architecture:</span><span class="sxs-lookup"><span data-stu-id="01fcc-127">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="01fcc-128">Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="01fcc-128">Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="01fcc-129">Multiple tenants per database (two types):</span><span class="sxs-lookup"><span data-stu-id="01fcc-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="01fcc-130">List mapping</span><span class="sxs-lookup"><span data-stu-id="01fcc-130">List mapping</span></span>
   2. <span data-ttu-id="01fcc-131">Range mapping</span><span class="sxs-lookup"><span data-stu-id="01fcc-131">Range mapping</span></span>

<span data-ttu-id="01fcc-132">For a single-tenant model, create a **list mapping** shard map.</span><span class="sxs-lookup"><span data-stu-id="01fcc-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="01fcc-133">The single-tenant model assigns one database per tenant.</span><span class="sxs-lookup"><span data-stu-id="01fcc-133">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="01fcc-134">This is an effective model for SaaS developers as it simplifies management.</span><span class="sxs-lookup"><span data-stu-id="01fcc-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![List mapping][1]

<span data-ttu-id="01fcc-136">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span><span class="sxs-lookup"><span data-stu-id="01fcc-136">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="01fcc-137">Use this model when you expect each tenant to have small data needs.</span><span class="sxs-lookup"><span data-stu-id="01fcc-137">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="01fcc-138">In this model, we assign a range of tenants to a database using **range mapping**.</span><span class="sxs-lookup"><span data-stu-id="01fcc-138">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Range mapping][2]

<span data-ttu-id="01fcc-140">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span><span class="sxs-lookup"><span data-stu-id="01fcc-140">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="01fcc-141">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span><span class="sxs-lookup"><span data-stu-id="01fcc-141">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Muliple tenants on single DB][3] 

<span data-ttu-id="01fcc-143">**Based on your choice, choose one of these options:**</span><span class="sxs-lookup"><span data-stu-id="01fcc-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="01fcc-144">Option 1: create a shard map for a list mapping</span><span class="sxs-lookup"><span data-stu-id="01fcc-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="01fcc-145">Create a shard map using the ShardMapManager object.</span><span class="sxs-lookup"><span data-stu-id="01fcc-145">Create a shard map using the ShardMapManager object.</span></span> 

    # $ShardMapManager is the shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="01fcc-146">Option 2: create a shard map for a range mapping</span><span class="sxs-lookup"><span data-stu-id="01fcc-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="01fcc-147">Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.</span><span class="sxs-lookup"><span data-stu-id="01fcc-147">Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.</span></span>

    # $ShardMapManager is the shard map manager object 
    # 'RangeShardMap' is the unique identifier for the range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="01fcc-148">Option 3: List mappings on a single database</span><span class="sxs-lookup"><span data-stu-id="01fcc-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="01fcc-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span><span class="sxs-lookup"><span data-stu-id="01fcc-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="01fcc-150">Step 3: Prepare individual shards</span><span class="sxs-lookup"><span data-stu-id="01fcc-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="01fcc-151">Add each shard (database) to the shard map manager.</span><span class="sxs-lookup"><span data-stu-id="01fcc-151">Add each shard (database) to the shard map manager.</span></span> <span data-ttu-id="01fcc-152">This prepares the individual databases for storing mapping information.</span><span class="sxs-lookup"><span data-stu-id="01fcc-152">This prepares the individual databases for storing mapping information.</span></span> <span data-ttu-id="01fcc-153">Execute this method on each shard.</span><span class="sxs-lookup"><span data-stu-id="01fcc-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # The $ShardMap is the shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="01fcc-154">Step 4: Add mappings</span><span class="sxs-lookup"><span data-stu-id="01fcc-154">Step 4: Add mappings</span></span>
<span data-ttu-id="01fcc-155">The addition of mappings depends on the kind of shard map you created.</span><span class="sxs-lookup"><span data-stu-id="01fcc-155">The addition of mappings depends on the kind of shard map you created.</span></span> <span data-ttu-id="01fcc-156">If you created a list map, you add list mappings.</span><span class="sxs-lookup"><span data-stu-id="01fcc-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="01fcc-157">If you created a range map, you add range mappings.</span><span class="sxs-lookup"><span data-stu-id="01fcc-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-the-data-for-a-list-mapping"></a><span data-ttu-id="01fcc-158">Option 1: map the data for a list mapping</span><span class="sxs-lookup"><span data-stu-id="01fcc-158">Option 1: map the data for a list mapping</span></span>
<span data-ttu-id="01fcc-159">Map the data by adding a list mapping for each tenant.</span><span class="sxs-lookup"><span data-stu-id="01fcc-159">Map the data by adding a list mapping for each tenant.</span></span>  

    # Create the mappings and associate it with the new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-the-data-for-a-range-mapping"></a><span data-ttu-id="01fcc-160">Option 2: map the data for a range mapping</span><span class="sxs-lookup"><span data-stu-id="01fcc-160">Option 2: map the data for a range mapping</span></span>
<span data-ttu-id="01fcc-161">Add the range mappings for all the tenant id range - database associations:</span><span class="sxs-lookup"><span data-stu-id="01fcc-161">Add the range mappings for all the tenant id range - database associations:</span></span>

    # Create the mappings and associate it with the new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-the-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="01fcc-162">Step 4 option 3: map the data for multiple tenants on a single database</span><span class="sxs-lookup"><span data-stu-id="01fcc-162">Step 4 option 3: map the data for multiple tenants on a single database</span></span>
<span data-ttu-id="01fcc-163">For each tenant, run the Add-ListMapping (option 1, above).</span><span class="sxs-lookup"><span data-stu-id="01fcc-163">For each tenant, run the Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-the-mappings"></a><span data-ttu-id="01fcc-164">Checking the mappings</span><span class="sxs-lookup"><span data-stu-id="01fcc-164">Checking the mappings</span></span>
<span data-ttu-id="01fcc-165">Information about the existing shards and the mappings associated with them can be queried using following commands:</span><span class="sxs-lookup"><span data-stu-id="01fcc-165">Information about the existing shards and the mappings associated with them can be queried using following commands:</span></span>  

    # List the shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="01fcc-166">Summary</span><span class="sxs-lookup"><span data-stu-id="01fcc-166">Summary</span></span>
<span data-ttu-id="01fcc-167">Once you have completed the setup, you can begin to use the Elastic Database client library.</span><span class="sxs-lookup"><span data-stu-id="01fcc-167">Once you have completed the setup, you can begin to use the Elastic Database client library.</span></span> <span data-ttu-id="01fcc-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="01fcc-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01fcc-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="01fcc-169">Next steps</span></span>
<span data-ttu-id="01fcc-170">Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="01fcc-170">Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="01fcc-171">The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="01fcc-171">The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="01fcc-172">Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model.</span><span class="sxs-lookup"><span data-stu-id="01fcc-172">Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model.</span></span> <span data-ttu-id="01fcc-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="01fcc-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="01fcc-174">Additional resources</span><span class="sxs-lookup"><span data-stu-id="01fcc-174">Additional resources</span></span>
<span data-ttu-id="01fcc-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="01fcc-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="01fcc-176">Questions and Feature Requests</span><span class="sxs-lookup"><span data-stu-id="01fcc-176">Questions and Feature Requests</span></span>
<span data-ttu-id="01fcc-177">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="01fcc-177">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png




