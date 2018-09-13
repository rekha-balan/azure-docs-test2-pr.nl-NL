---
title: Scale out an Azure SQL database | Microsoft Docs
description: How to use the ShardMapManager, elastic database client library
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
editor: ''
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: e69b769d6b5b84e99b111246891c782dd08eb6db
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555339"
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a><span data-ttu-id="f0501-103">Scale out databases with the shard map manager</span><span class="sxs-lookup"><span data-stu-id="f0501-103">Scale out databases with the shard map manager</span></span>
<span data-ttu-id="f0501-104">To easily scale out databases on SQL Azure, use a shard map manager.</span><span class="sxs-lookup"><span data-stu-id="f0501-104">To easily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="f0501-105">The shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span><span class="sxs-lookup"><span data-stu-id="f0501-105">The shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="f0501-106">The metadata allows an application to connect to the correct database based upon the value of the **sharding key**.</span><span class="sxs-lookup"><span data-stu-id="f0501-106">The metadata allows an application to connect to the correct database based upon the value of the **sharding key**.</span></span> <span data-ttu-id="f0501-107">In addition, every shard in the set contains maps that track the local shard data (known as **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="f0501-107">In addition, every shard in the set contains maps that track the local shard data (known as **shardlets**).</span></span> 

![Shard map management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="f0501-109">Understanding how these maps are constructed is essential to shard map management.</span><span class="sxs-lookup"><span data-stu-id="f0501-109">Understanding how these maps are constructed is essential to shard map management.</span></span> <span data-ttu-id="f0501-110">This is done using the [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in the [Elastic Database client library](sql-database-elastic-database-client-library.md) to manage shard maps.</span><span class="sxs-lookup"><span data-stu-id="f0501-110">This is done using the [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in the [Elastic Database client library](sql-database-elastic-database-client-library.md) to manage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="f0501-111">Shard maps and shard mappings</span><span class="sxs-lookup"><span data-stu-id="f0501-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="f0501-112">For each shard, you must select the type of shard map to create.</span><span class="sxs-lookup"><span data-stu-id="f0501-112">For each shard, you must select the type of shard map to create.</span></span> <span data-ttu-id="f0501-113">The choice depends on the database architecture:</span><span class="sxs-lookup"><span data-stu-id="f0501-113">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="f0501-114">Single tenant per database</span><span class="sxs-lookup"><span data-stu-id="f0501-114">Single tenant per database</span></span>  
2. <span data-ttu-id="f0501-115">Multiple tenants per database (two types):</span><span class="sxs-lookup"><span data-stu-id="f0501-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="f0501-116">List mapping</span><span class="sxs-lookup"><span data-stu-id="f0501-116">List mapping</span></span>
   2. <span data-ttu-id="f0501-117">Range mapping</span><span class="sxs-lookup"><span data-stu-id="f0501-117">Range mapping</span></span>

<span data-ttu-id="f0501-118">For a single-tenant model, create a **list mapping** shard map.</span><span class="sxs-lookup"><span data-stu-id="f0501-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="f0501-119">The single-tenant model assigns one database per tenant.</span><span class="sxs-lookup"><span data-stu-id="f0501-119">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="f0501-120">This is an effective model for SaaS developers as it simplifies management.</span><span class="sxs-lookup"><span data-stu-id="f0501-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![List mapping][1]

<span data-ttu-id="f0501-122">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span><span class="sxs-lookup"><span data-stu-id="f0501-122">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="f0501-123">Use this model when you expect each tenant to have small data needs.</span><span class="sxs-lookup"><span data-stu-id="f0501-123">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="f0501-124">In this model, we assign a range of tenants to a database using **range mapping**.</span><span class="sxs-lookup"><span data-stu-id="f0501-124">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Range mapping][2]

<span data-ttu-id="f0501-126">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span><span class="sxs-lookup"><span data-stu-id="f0501-126">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="f0501-127">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span><span class="sxs-lookup"><span data-stu-id="f0501-127">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Muliple tenants on single DB][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="f0501-129">Supported .Net types for sharding keys</span><span class="sxs-lookup"><span data-stu-id="f0501-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="f0501-130">Elastic Scale support the following .Net Framework types as sharding keys:</span><span class="sxs-lookup"><span data-stu-id="f0501-130">Elastic Scale support the following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="f0501-131">integer</span><span class="sxs-lookup"><span data-stu-id="f0501-131">integer</span></span>
* <span data-ttu-id="f0501-132">long</span><span class="sxs-lookup"><span data-stu-id="f0501-132">long</span></span>
* <span data-ttu-id="f0501-133">guid</span><span class="sxs-lookup"><span data-stu-id="f0501-133">guid</span></span>
* <span data-ttu-id="f0501-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="f0501-134">byte[]</span></span>  
* <span data-ttu-id="f0501-135">datetime</span><span class="sxs-lookup"><span data-stu-id="f0501-135">datetime</span></span>
* <span data-ttu-id="f0501-136">timespan</span><span class="sxs-lookup"><span data-stu-id="f0501-136">timespan</span></span>
* <span data-ttu-id="f0501-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f0501-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="f0501-138">List and range shard maps</span><span class="sxs-lookup"><span data-stu-id="f0501-138">List and range shard maps</span></span>
<span data-ttu-id="f0501-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span><span class="sxs-lookup"><span data-stu-id="f0501-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="f0501-140">List shard maps</span><span class="sxs-lookup"><span data-stu-id="f0501-140">List shard maps</span></span>
<span data-ttu-id="f0501-141">**Shards** contain **shardlets** and the mapping of shardlets to shards is maintained by a shard map.</span><span class="sxs-lookup"><span data-stu-id="f0501-141">**Shards** contain **shardlets** and the mapping of shardlets to shards is maintained by a shard map.</span></span> <span data-ttu-id="f0501-142">A **list shard map** is an association between the individual key values that identify the shardlets and the databases that serve as shards.</span><span class="sxs-lookup"><span data-stu-id="f0501-142">A **list shard map** is an association between the individual key values that identify the shardlets and the databases that serve as shards.</span></span>  <span data-ttu-id="f0501-143">**List mappings** are explicit and different key values can be mapped to the same database.</span><span class="sxs-lookup"><span data-stu-id="f0501-143">**List mappings** are explicit and different key values can be mapped to the same database.</span></span> <span data-ttu-id="f0501-144">For example, key 1 maps to Database A, and key values 3 and 6 both reference Database B.</span><span class="sxs-lookup"><span data-stu-id="f0501-144">For example, key 1 maps to Database A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="f0501-145">Key</span><span class="sxs-lookup"><span data-stu-id="f0501-145">Key</span></span> | <span data-ttu-id="f0501-146">Shard Location</span><span class="sxs-lookup"><span data-stu-id="f0501-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="f0501-147">1</span><span class="sxs-lookup"><span data-stu-id="f0501-147">1</span></span> |<span data-ttu-id="f0501-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="f0501-148">Database_A</span></span> |
| <span data-ttu-id="f0501-149">3</span><span class="sxs-lookup"><span data-stu-id="f0501-149">3</span></span> |<span data-ttu-id="f0501-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="f0501-150">Database_B</span></span> |
| <span data-ttu-id="f0501-151">4</span><span class="sxs-lookup"><span data-stu-id="f0501-151">4</span></span> |<span data-ttu-id="f0501-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="f0501-152">Database_C</span></span> |
| <span data-ttu-id="f0501-153">6</span><span class="sxs-lookup"><span data-stu-id="f0501-153">6</span></span> |<span data-ttu-id="f0501-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="f0501-154">Database_B</span></span> |
| <span data-ttu-id="f0501-155">...</span><span class="sxs-lookup"><span data-stu-id="f0501-155">...</span></span> |<span data-ttu-id="f0501-156">...</span><span class="sxs-lookup"><span data-stu-id="f0501-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="f0501-157">Range shard maps</span><span class="sxs-lookup"><span data-stu-id="f0501-157">Range shard maps</span></span>
<span data-ttu-id="f0501-158">In a **range shard map**, the key range is described by a pair **[Low Value, High Value)** where the *Low Value* is the minimum key in the range, and the *High Value* is the first value higher than the range.</span><span class="sxs-lookup"><span data-stu-id="f0501-158">In a **range shard map**, the key range is described by a pair **[Low Value, High Value)** where the *Low Value* is the minimum key in the range, and the *High Value* is the first value higher than the range.</span></span> 

<span data-ttu-id="f0501-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span><span class="sxs-lookup"><span data-stu-id="f0501-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="f0501-160">Note that multiple ranges can point to the same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point to Database C in the example below.)</span><span class="sxs-lookup"><span data-stu-id="f0501-160">Note that multiple ranges can point to the same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point to Database C in the example below.)</span></span>

| <span data-ttu-id="f0501-161">Key</span><span class="sxs-lookup"><span data-stu-id="f0501-161">Key</span></span> | <span data-ttu-id="f0501-162">Shard Location</span><span class="sxs-lookup"><span data-stu-id="f0501-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="f0501-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="f0501-163">[1,50)</span></span> |<span data-ttu-id="f0501-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="f0501-164">Database_A</span></span> |
| <span data-ttu-id="f0501-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="f0501-165">[50,100)</span></span> |<span data-ttu-id="f0501-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="f0501-166">Database_B</span></span> |
| <span data-ttu-id="f0501-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="f0501-167">[100,200)</span></span> |<span data-ttu-id="f0501-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="f0501-168">Database_C</span></span> |
| <span data-ttu-id="f0501-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="f0501-169">[400,600)</span></span> |<span data-ttu-id="f0501-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="f0501-170">Database_C</span></span> |
| <span data-ttu-id="f0501-171">...</span><span class="sxs-lookup"><span data-stu-id="f0501-171">...</span></span> |<span data-ttu-id="f0501-172">...</span><span class="sxs-lookup"><span data-stu-id="f0501-172">...</span></span> |

<span data-ttu-id="f0501-173">Each of the tables shown above is a conceptual example of a **ShardMap** object.</span><span class="sxs-lookup"><span data-stu-id="f0501-173">Each of the tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="f0501-174">Each row is a simplified example of an individual **PointMapping** (for the list shard map) or **RangeMapping** (for the range shard map) object.</span><span class="sxs-lookup"><span data-stu-id="f0501-174">Each row is a simplified example of an individual **PointMapping** (for the list shard map) or **RangeMapping** (for the range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="f0501-175">Shard map manager</span><span class="sxs-lookup"><span data-stu-id="f0501-175">Shard map manager</span></span>
<span data-ttu-id="f0501-176">In the client library, the shard map  manager is a collection of shard maps.</span><span class="sxs-lookup"><span data-stu-id="f0501-176">In the client library, the shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="f0501-177">The data managed by a **ShardMapManager** instance is kept in three places:</span><span class="sxs-lookup"><span data-stu-id="f0501-177">The data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="f0501-178">**Global Shard Map (GSM)**: You specify a database to serve as the repository for all of its shard maps and mappings.</span><span class="sxs-lookup"><span data-stu-id="f0501-178">**Global Shard Map (GSM)**: You specify a database to serve as the repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="f0501-179">Special tables and stored procedures are automatically created to manage the information.</span><span class="sxs-lookup"><span data-stu-id="f0501-179">Special tables and stored procedures are automatically created to manage the information.</span></span> <span data-ttu-id="f0501-180">This is typically a small database and lightly accessed, and it should not be used for other needs of the application.</span><span class="sxs-lookup"><span data-stu-id="f0501-180">This is typically a small database and lightly accessed, and it should not be used for other needs of the application.</span></span> <span data-ttu-id="f0501-181">The tables are in a special schema named **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="f0501-181">The tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="f0501-182">**Local Shard Map (LSM)**: Every database that you specify to be a shard is modified to contain several small tables and special stored procedures that contain and manage shard map information specific to that shard.</span><span class="sxs-lookup"><span data-stu-id="f0501-182">**Local Shard Map (LSM)**: Every database that you specify to be a shard is modified to contain several small tables and special stored procedures that contain and manage shard map information specific to that shard.</span></span> <span data-ttu-id="f0501-183">This information is redundant with the information in the GSM, and it allows the application to validate cached shard map information without placing any load on the GSM; the application uses the LSM to determine if a cached mapping is still valid.</span><span class="sxs-lookup"><span data-stu-id="f0501-183">This information is redundant with the information in the GSM, and it allows the application to validate cached shard map information without placing any load on the GSM; the application uses the LSM to determine if a cached mapping is still valid.</span></span> <span data-ttu-id="f0501-184">The tables corresponding to the LSM on each shard are also in the schema **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="f0501-184">The tables corresponding to the LSM on each shard are also in the schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="f0501-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span><span class="sxs-lookup"><span data-stu-id="f0501-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="f0501-186">It stores routing information that has recently been retrieved.</span><span class="sxs-lookup"><span data-stu-id="f0501-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="f0501-187">Constructing a ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="f0501-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="f0501-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span><span class="sxs-lookup"><span data-stu-id="f0501-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="f0501-189">The **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including the server name and database name holding the GSM) in the form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="f0501-189">The **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including the server name and database name holding the GSM) in the form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="f0501-190">**Please Note:** The **ShardMapManager** should be instantiated only once per app domain, within the initialization code for an application.</span><span class="sxs-lookup"><span data-stu-id="f0501-190">**Please Note:** The **ShardMapManager** should be instantiated only once per app domain, within the initialization code for an application.</span></span> <span data-ttu-id="f0501-191">Creation of additional instances of ShardMapManager in the same appdomain, will result in increased memory and CPU utilization of the application.</span><span class="sxs-lookup"><span data-stu-id="f0501-191">Creation of additional instances of ShardMapManager in the same appdomain, will result in increased memory and CPU utilization of the application.</span></span> <span data-ttu-id="f0501-192">A **ShardMapManager** can contain any number of shard maps.</span><span class="sxs-lookup"><span data-stu-id="f0501-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="f0501-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span><span class="sxs-lookup"><span data-stu-id="f0501-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="f0501-194">In this code, an application tries to open an existing **ShardMapManager** with the [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0501-194">In this code, an application tries to open an existing **ShardMapManager** with the [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="f0501-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside the database, the client library creates them there using the [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0501-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside the database, the client library creates them there using the [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try to get a reference to the Shard Map Manager 
     // via the Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create the Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // The connectionString contains server name, database name, and admin credentials 
        // for privileges on both the GSM and the shards themselves.
    } 

<span data-ttu-id="f0501-196">As an alternative, you can use Powershell to create a new Shard Map Manager.</span><span class="sxs-lookup"><span data-stu-id="f0501-196">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="f0501-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="f0501-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="f0501-198">Get a RangeShardMap or ListShardMap</span><span class="sxs-lookup"><span data-stu-id="f0501-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="f0501-199">After creating a shard map manager, you can get the [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="f0501-199">After creating a shard map manager, you can get the [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try to get a reference to the Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // The Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="f0501-200">Shard map administration credentials</span><span class="sxs-lookup"><span data-stu-id="f0501-200">Shard map administration credentials</span></span>
<span data-ttu-id="f0501-201">Applications that administer and manipulate shard maps are different from those that use the shard maps to route connections.</span><span class="sxs-lookup"><span data-stu-id="f0501-201">Applications that administer and manipulate shard maps are different from those that use the shard maps to route connections.</span></span> 

<span data-ttu-id="f0501-202">To administer shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate the **ShardMapManager** using **credentials that have read/write privileges on both the GSM database and on each database that serves as a shard**.</span><span class="sxs-lookup"><span data-stu-id="f0501-202">To administer shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate the **ShardMapManager** using **credentials that have read/write privileges on both the GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="f0501-203">The credentials must allow for writes against the tables in both the GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span><span class="sxs-lookup"><span data-stu-id="f0501-203">The credentials must allow for writes against the tables in both the GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="f0501-204">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="f0501-204">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="f0501-205">Only metadata affected</span><span class="sxs-lookup"><span data-stu-id="f0501-205">Only metadata affected</span></span>
<span data-ttu-id="f0501-206">Methods used for populating or changing the **ShardMapManager** data do not alter the user data stored in the shards themselves.</span><span class="sxs-lookup"><span data-stu-id="f0501-206">Methods used for populating or changing the **ShardMapManager** data do not alter the user data stored in the shards themselves.</span></span> <span data-ttu-id="f0501-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect the shard map metadata only.</span><span class="sxs-lookup"><span data-stu-id="f0501-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect the shard map metadata only.</span></span> <span data-ttu-id="f0501-208">They do not remove, add, or alter user data contained in the shards.</span><span class="sxs-lookup"><span data-stu-id="f0501-208">They do not remove, add, or alter user data contained in the shards.</span></span> <span data-ttu-id="f0501-209">Instead, these methods are designed to be used in conjunction with separate operations you perform to create or remove actual databases, or that move rows from one shard to another to rebalance a sharded environment.</span><span class="sxs-lookup"><span data-stu-id="f0501-209">Instead, these methods are designed to be used in conjunction with separate operations you perform to create or remove actual databases, or that move rows from one shard to another to rebalance a sharded environment.</span></span>  <span data-ttu-id="f0501-210">(The **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="f0501-210">(The **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="f0501-211">Populating a shard map example</span><span class="sxs-lookup"><span data-stu-id="f0501-211">Populating a shard map example</span></span>
<span data-ttu-id="f0501-212">An example sequence of operations to populate a specific shard map is shown below.</span><span class="sxs-lookup"><span data-stu-id="f0501-212">An example sequence of operations to populate a specific shard map is shown below.</span></span> <span data-ttu-id="f0501-213">The code performs these steps:</span><span class="sxs-lookup"><span data-stu-id="f0501-213">The code performs these steps:</span></span> 

1. <span data-ttu-id="f0501-214">A new shard map is created within a shard map manager.</span><span class="sxs-lookup"><span data-stu-id="f0501-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="f0501-215">The metadata for two different shards is added to the shard map.</span><span class="sxs-lookup"><span data-stu-id="f0501-215">The metadata for two different shards is added to the shard map.</span></span> 
3. <span data-ttu-id="f0501-216">A variety of key range mappings are added, and the overall contents of the shard map are displayed.</span><span class="sxs-lookup"><span data-stu-id="f0501-216">A variety of key range mappings are added, and the overall contents of the shard map are displayed.</span></span> 

<span data-ttu-id="f0501-217">The code is written so that the method can be rerun if an error occurs.</span><span class="sxs-lookup"><span data-stu-id="f0501-217">The code is written so that the method can be rerun if an error occurs.</span></span> <span data-ttu-id="f0501-218">Each request tests whether a shard or mapping already exists, before attempting to create it.</span><span class="sxs-lookup"><span data-stu-id="f0501-218">Each request tests whether a shard or mapping already exists, before attempting to create it.</span></span> <span data-ttu-id="f0501-219">The code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in the server referenced by string **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="f0501-219">The code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in the server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List the shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="f0501-220">As an alternative you can use PowerShell scripts to achieve the same result.</span><span class="sxs-lookup"><span data-stu-id="f0501-220">As an alternative you can use PowerShell scripts to achieve the same result.</span></span> <span data-ttu-id="f0501-221">Some of the sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="f0501-221">Some of the sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="f0501-222">Once shard maps have been populated, data access applications can be created or adapted to work with the maps.</span><span class="sxs-lookup"><span data-stu-id="f0501-222">Once shard maps have been populated, data access applications can be created or adapted to work with the maps.</span></span> <span data-ttu-id="f0501-223">Populating or manipulating the maps need not occur again until **map layout** needs to change.</span><span class="sxs-lookup"><span data-stu-id="f0501-223">Populating or manipulating the maps need not occur again until **map layout** needs to change.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="f0501-224">Data dependent routing</span><span class="sxs-lookup"><span data-stu-id="f0501-224">Data dependent routing</span></span>
<span data-ttu-id="f0501-225">The shard map manager will be most used in applications that require database connections to perform the app-specific data operations.</span><span class="sxs-lookup"><span data-stu-id="f0501-225">The shard map manager will be most used in applications that require database connections to perform the app-specific data operations.</span></span> <span data-ttu-id="f0501-226">Those connections must be associated with the correct database.</span><span class="sxs-lookup"><span data-stu-id="f0501-226">Those connections must be associated with the correct database.</span></span> <span data-ttu-id="f0501-227">This is known as **Data Dependent Routing**.</span><span class="sxs-lookup"><span data-stu-id="f0501-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="f0501-228">For these applications, instantiate a shard map manager object from the factory using credentials that have read-only access on the GSM database.</span><span class="sxs-lookup"><span data-stu-id="f0501-228">For these applications, instantiate a shard map manager object from the factory using credentials that have read-only access on the GSM database.</span></span> <span data-ttu-id="f0501-229">Individual requests for later connections supply credentials necessary for connecting to the appropriate shard database.</span><span class="sxs-lookup"><span data-stu-id="f0501-229">Individual requests for later connections supply credentials necessary for connecting to the appropriate shard database.</span></span>

<span data-ttu-id="f0501-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes to the maps or mappings.</span><span class="sxs-lookup"><span data-stu-id="f0501-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes to the maps or mappings.</span></span> <span data-ttu-id="f0501-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span><span class="sxs-lookup"><span data-stu-id="f0501-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="f0501-232">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="f0501-232">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="f0501-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="f0501-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="f0501-234">Modifying a shard map</span><span class="sxs-lookup"><span data-stu-id="f0501-234">Modifying a shard map</span></span>
<span data-ttu-id="f0501-235">A shard map can be changed in different ways.</span><span class="sxs-lookup"><span data-stu-id="f0501-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="f0501-236">All of the following methods modify the metadata describing the shards and their mappings, but they do not physically modify data within the shards, nor do they create or delete the actual databases.</span><span class="sxs-lookup"><span data-stu-id="f0501-236">All of the following methods modify the metadata describing the shards and their mappings, but they do not physically modify data within the shards, nor do they create or delete the actual databases.</span></span>  <span data-ttu-id="f0501-237">Some of the operations on the shard map described below may need to be coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span><span class="sxs-lookup"><span data-stu-id="f0501-237">Some of the operations on the shard map described below may need to be coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="f0501-238">These methods work together as the building blocks available for modifying the overall distribution of data in your sharded database environment.</span><span class="sxs-lookup"><span data-stu-id="f0501-238">These methods work together as the building blocks available for modifying the overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="f0501-239">To add or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of the [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0501-239">To add or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of the [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="f0501-240">The server and database representing the target shard must already exist for these operations to execute.</span><span class="sxs-lookup"><span data-stu-id="f0501-240">The server and database representing the target shard must already exist for these operations to execute.</span></span> <span data-ttu-id="f0501-241">These methods do not have any impact on the databases themselves, only on metadata in the shard map.</span><span class="sxs-lookup"><span data-stu-id="f0501-241">These methods do not have any impact on the databases themselves, only on metadata in the shard map.</span></span>
* <span data-ttu-id="f0501-242">To create or remove points or ranges that are mapped to the shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of the [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of the [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="f0501-242">To create or remove points or ranges that are mapped to the shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of the [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of the [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="f0501-243">Many different points or ranges can be mapped to the same shard.</span><span class="sxs-lookup"><span data-stu-id="f0501-243">Many different points or ranges can be mapped to the same shard.</span></span> <span data-ttu-id="f0501-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span><span class="sxs-lookup"><span data-stu-id="f0501-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="f0501-245">If data needs to be removed from the database in order to be consistent with **DeleteMapping** operations, you will need to perform those operations separately but in conjunction with using these methods.</span><span class="sxs-lookup"><span data-stu-id="f0501-245">If data needs to be removed from the database in order to be consistent with **DeleteMapping** operations, you will need to perform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="f0501-246">To split existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="f0501-246">To split existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="f0501-247">Note that split and merge operations **do not change the shard to which key values are mapped**.</span><span class="sxs-lookup"><span data-stu-id="f0501-247">Note that split and merge operations **do not change the shard to which key values are mapped**.</span></span> <span data-ttu-id="f0501-248">A split breaks an existing range into two parts, but leaves both as mapped to the same shard.</span><span class="sxs-lookup"><span data-stu-id="f0501-248">A split breaks an existing range into two parts, but leaves both as mapped to the same shard.</span></span> <span data-ttu-id="f0501-249">A merge operates on two adjacent ranges that are already mapped to the same shard, coalescing them into a single range.</span><span class="sxs-lookup"><span data-stu-id="f0501-249">A merge operates on two adjacent ranges that are already mapped to the same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="f0501-250">The movement of points or ranges themselves between shards needs to be coordinated by using **UpdateMapping** in conjunction with actual data movement.</span><span class="sxs-lookup"><span data-stu-id="f0501-250">The movement of points or ranges themselves between shards needs to be coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="f0501-251">You can use the **Split/Merge** service that is part of elastic database tools to coordinate shard map changes with data movement, when movement is needed.</span><span class="sxs-lookup"><span data-stu-id="f0501-251">You can use the **Split/Merge** service that is part of elastic database tools to coordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="f0501-252">To re-map (or move) individual points or ranges to different shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="f0501-252">To re-map (or move) individual points or ranges to different shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="f0501-253">Since data may need to be moved from one shard to another in order to be consistent with **UpdateMapping** operations, you will need to perform that movement separately but in conjunction with using these methods.</span><span class="sxs-lookup"><span data-stu-id="f0501-253">Since data may need to be moved from one shard to another in order to be consistent with **UpdateMapping** operations, you will need to perform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="f0501-254">To take mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** to control the online state of a mapping.</span><span class="sxs-lookup"><span data-stu-id="f0501-254">To take mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** to control the online state of a mapping.</span></span> 
  
    <span data-ttu-id="f0501-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="f0501-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="f0501-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span><span class="sxs-lookup"><span data-stu-id="f0501-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="f0501-257">In addition, when a range is first taken offline, all connections to the affected shard are automatically killed in order to prevent inconsistent or incomplete results for queries directed against ranges being changed.</span><span class="sxs-lookup"><span data-stu-id="f0501-257">In addition, when a range is first taken offline, all connections to the affected shard are automatically killed in order to prevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="f0501-258">Mappings are immutable objects in .Net.</span><span class="sxs-lookup"><span data-stu-id="f0501-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="f0501-259">All of the methods above that change mappings also invalidate any references to them in your code.</span><span class="sxs-lookup"><span data-stu-id="f0501-259">All of the methods above that change mappings also invalidate any references to them in your code.</span></span> <span data-ttu-id="f0501-260">To make it easier to perform sequences of operations that change a mapping’s state, all of the methods that change a mapping return a new mapping reference, so operations can be chained.</span><span class="sxs-lookup"><span data-stu-id="f0501-260">To make it easier to perform sequences of operations that change a mapping’s state, all of the methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="f0501-261">For example, to delete an existing mapping in shardmap sm that contains the key 25, you can execute the following:</span><span class="sxs-lookup"><span data-stu-id="f0501-261">For example, to delete an existing mapping in shardmap sm that contains the key 25, you can execute the following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="f0501-262">Adding a shard</span><span class="sxs-lookup"><span data-stu-id="f0501-262">Adding a shard</span></span>
<span data-ttu-id="f0501-263">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span><span class="sxs-lookup"><span data-stu-id="f0501-263">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="f0501-264">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span><span class="sxs-lookup"><span data-stu-id="f0501-264">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="f0501-265">If the new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple to add the new shard and associate the new key or range to that shard.</span><span class="sxs-lookup"><span data-stu-id="f0501-265">If the new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> <span data-ttu-id="f0501-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="f0501-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="f0501-267">For scenarios that require data movement, however, the split-merge tool is needed to orchestrate the data movement between shards in combination with the necessary shard map updates.</span><span class="sxs-lookup"><span data-stu-id="f0501-267">For scenarios that require data movement, however, the split-merge tool is needed to orchestrate the data movement between shards in combination with the necessary shard map updates.</span></span> <span data-ttu-id="f0501-268">For details on using the split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="f0501-268">For details on using the split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png




