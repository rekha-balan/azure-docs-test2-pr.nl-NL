---
title: Configure Geo-Replication for Azure SQL Database with Transact-SQL | Microsoft Docs
description: Configure Geo-Replication for Azure SQL Database using Transact-SQL
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/13/2016
ms.author: carlrab
ms.openlocfilehash: 07593e7f1d92a9a5943714f662568fec10a8886a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563717"
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a><span data-ttu-id="8014d-103">Configure active geo-replication for Azure SQL Database with Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="8014d-103">Configure active geo-replication for Azure SQL Database with Transact-SQL</span></span>

<span data-ttu-id="8014d-104">This article shows you how to configure active geo-replication for an Azure SQL Database with Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="8014d-104">This article shows you how to configure active geo-replication for an Azure SQL Database with Transact-SQL.</span></span>

<span data-ttu-id="8014d-105">To initiate failover using Transact-SQL, see [Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8014d-105">To initiate failover using Transact-SQL, see [Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8014d-106">Active geo-replication (readable secondaries) is now available for all databases in all service tiers.</span><span class="sxs-lookup"><span data-stu-id="8014d-106">Active geo-replication (readable secondaries) is now available for all databases in all service tiers.</span></span> <span data-ttu-id="8014d-107">In April 2017 the non-readable secondary type will be retired and existing non-readable databases will automatically be upgraded to readable secondaries.</span><span class="sxs-lookup"><span data-stu-id="8014d-107">In April 2017 the non-readable secondary type will be retired and existing non-readable databases will automatically be upgraded to readable secondaries.</span></span>
> 
> 

<span data-ttu-id="8014d-108">To configure Active Geo-Replication using Transact-SQL, you need the following:</span><span class="sxs-lookup"><span data-stu-id="8014d-108">To configure Active Geo-Replication using Transact-SQL, you need the following:</span></span>

* <span data-ttu-id="8014d-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8014d-109">An Azure subscription.</span></span>
* <span data-ttu-id="8014d-110">A logical Azure SQL Database server <MyLocalServer> and a SQL database <MyDB> - The primary database that you want to replicate.</span><span class="sxs-lookup"><span data-stu-id="8014d-110">A logical Azure SQL Database server <MyLocalServer> and a SQL database <MyDB> - The primary database that you want to replicate.</span></span>
* <span data-ttu-id="8014d-111">One or more logical Azure SQL Database servers <MySecondaryServer(n)> - The logical servers that will be the partner servers in which you will create secondary databases.</span><span class="sxs-lookup"><span data-stu-id="8014d-111">One or more logical Azure SQL Database servers <MySecondaryServer(n)> - The logical servers that will be the partner servers in which you will create secondary databases.</span></span>
* <span data-ttu-id="8014d-112">A login that is DBManager on the primary, have db_ownership of the local database that you will geo-replicate, and be DBManager on the partner server(s) to which you will configure Geo-Replication.</span><span class="sxs-lookup"><span data-stu-id="8014d-112">A login that is DBManager on the primary, have db_ownership of the local database that you will geo-replicate, and be DBManager on the partner server(s) to which you will configure Geo-Replication.</span></span>
* <span data-ttu-id="8014d-113">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="8014d-113">SQL Server Management Studio (SSMS)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8014d-114">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8014d-114">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="8014d-115">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="8014d-115">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

## <a name="add-secondary-database"></a><span data-ttu-id="8014d-116">Add secondary database</span><span class="sxs-lookup"><span data-stu-id="8014d-116">Add secondary database</span></span>
<span data-ttu-id="8014d-117">You can use the **ALTER DATABASE** statement to create a geo-replicated secondary database on a partner server.</span><span class="sxs-lookup"><span data-stu-id="8014d-117">You can use the **ALTER DATABASE** statement to create a geo-replicated secondary database on a partner server.</span></span> <span data-ttu-id="8014d-118">You execute this statement on the master database of the server containing the database to be replicated.</span><span class="sxs-lookup"><span data-stu-id="8014d-118">You execute this statement on the master database of the server containing the database to be replicated.</span></span> <span data-ttu-id="8014d-119">The geo-replicated database (the "primary database") will have the same name as the database being replicated and will, by default, have the same service level as the primary database.</span><span class="sxs-lookup"><span data-stu-id="8014d-119">The geo-replicated database (the "primary database") will have the same name as the database being replicated and will, by default, have the same service level as the primary database.</span></span> <span data-ttu-id="8014d-120">The secondary database can be readable or non-readable, and can be a single database or in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="8014d-120">The secondary database can be readable or non-readable, and can be a single database or in an elastic pool.</span></span> <span data-ttu-id="8014d-121">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="8014d-121">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="8014d-122">After the secondary database is created and seeded, data will begin replicating asynchronously from the primary database.</span><span class="sxs-lookup"><span data-stu-id="8014d-122">After the secondary database is created and seeded, data will begin replicating asynchronously from the primary database.</span></span> <span data-ttu-id="8014d-123">The steps below describe how to configure Geo-Replication using Management Studio.</span><span class="sxs-lookup"><span data-stu-id="8014d-123">The steps below describe how to configure Geo-Replication using Management Studio.</span></span> <span data-ttu-id="8014d-124">Steps to create non-readable and readable secondaries, either as a single database or in an elastic pool, are provided.</span><span class="sxs-lookup"><span data-stu-id="8014d-124">Steps to create non-readable and readable secondaries, either as a single database or in an elastic pool, are provided.</span></span>

> [!NOTE]
> <span data-ttu-id="8014d-125">If a database exists on the specified partner server with the same name as the primary database the command will fail.</span><span class="sxs-lookup"><span data-stu-id="8014d-125">If a database exists on the specified partner server with the same name as the primary database the command will fail.</span></span>
> 
> 

### <a name="add-non-readable-secondary-single-database"></a><span data-ttu-id="8014d-126">Add non-readable secondary (single database)</span><span class="sxs-lookup"><span data-stu-id="8014d-126">Add non-readable secondary (single database)</span></span>
<span data-ttu-id="8014d-127">Use the following steps to create a non-readable secondary as a single database.</span><span class="sxs-lookup"><span data-stu-id="8014d-127">Use the following steps to create a non-readable secondary as a single database.</span></span>

1. <span data-ttu-id="8014d-128">Using version 13.0.600.65 or later of SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="8014d-128">Using version 13.0.600.65 or later of SQL Server Management Studio.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8014d-129">Download the [latest](https://msdn.microsoft.com/library/mt238290.aspx) version of SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="8014d-129">Download the [latest](https://msdn.microsoft.com/library/mt238290.aspx) version of SQL Server Management Studio.</span></span> <span data-ttu-id="8014d-130">It is recommended that you always use the latest version of Management Studio to remain in sync with updates to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8014d-130">It is recommended that you always use the latest version of Management Studio to remain in sync with updates to the Azure portal.</span></span>
   > 
   > 
2. <span data-ttu-id="8014d-131">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="8014d-131">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="8014d-132">Use the following **ALTER DATABASE** statement to make a local database into a Geo-Replication primary with a non-readable secondary database on MySecondaryServer1 where MySecondaryServer1 is your friendly server name.</span><span class="sxs-lookup"><span data-stu-id="8014d-132">Use the following **ALTER DATABASE** statement to make a local database into a Geo-Replication primary with a non-readable secondary database on MySecondaryServer1 where MySecondaryServer1 is your friendly server name.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer1> WITH (ALLOW_CONNECTIONS = NO);
4. <span data-ttu-id="8014d-133">Click **Execute** to run the query.</span><span class="sxs-lookup"><span data-stu-id="8014d-133">Click **Execute** to run the query.</span></span>

### <a name="add-readable-secondary-single-database"></a><span data-ttu-id="8014d-134">Add readable secondary (single database)</span><span class="sxs-lookup"><span data-stu-id="8014d-134">Add readable secondary (single database)</span></span>
<span data-ttu-id="8014d-135">Use the following steps to create a readable secondary as a single database.</span><span class="sxs-lookup"><span data-stu-id="8014d-135">Use the following steps to create a readable secondary as a single database.</span></span>

1. <span data-ttu-id="8014d-136">In Management Studio, connect to your Azure SQL Database logical server.</span><span class="sxs-lookup"><span data-stu-id="8014d-136">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="8014d-137">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="8014d-137">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="8014d-138">Use the following **ALTER DATABASE** statement to make a local database into a Geo-Replication primary with a readable secondary database on a secondary server.</span><span class="sxs-lookup"><span data-stu-id="8014d-138">Use the following **ALTER DATABASE** statement to make a local database into a Geo-Replication primary with a readable secondary database on a secondary server.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. <span data-ttu-id="8014d-139">Click **Execute** to run the query.</span><span class="sxs-lookup"><span data-stu-id="8014d-139">Click **Execute** to run the query.</span></span>

### <a name="add-non-readable-secondary-elastic-pool"></a><span data-ttu-id="8014d-140">Add non-readable secondary (elastic pool)</span><span class="sxs-lookup"><span data-stu-id="8014d-140">Add non-readable secondary (elastic pool)</span></span>
<span data-ttu-id="8014d-141">Use the following steps to create a non-readable secondary in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="8014d-141">Use the following steps to create a non-readable secondary in an elastic pool.</span></span>

1. <span data-ttu-id="8014d-142">In Management Studio, connect to your Azure SQL Database logical server.</span><span class="sxs-lookup"><span data-stu-id="8014d-142">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="8014d-143">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="8014d-143">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="8014d-144">Use the following **ALTER DATABASE** statement to make a local database into a Geo-Replication primary with a non-readable secondary database on a secondary server in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="8014d-144">Use the following **ALTER DATABASE** statement to make a local database into a Geo-Replication primary with a non-readable secondary database on a secondary server in an elastic pool.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer3> WITH (ALLOW_CONNECTIONS = NO
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool1));
4. <span data-ttu-id="8014d-145">Click **Execute** to run the query.</span><span class="sxs-lookup"><span data-stu-id="8014d-145">Click **Execute** to run the query.</span></span>

### <a name="add-readable-secondary-elastic-pool"></a><span data-ttu-id="8014d-146">Add readable secondary (elastic pool)</span><span class="sxs-lookup"><span data-stu-id="8014d-146">Add readable secondary (elastic pool)</span></span>
<span data-ttu-id="8014d-147">Use the following steps to create a readable secondary in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="8014d-147">Use the following steps to create a readable secondary in an elastic pool.</span></span>

1. <span data-ttu-id="8014d-148">In Management Studio, connect to your Azure SQL Database logical server.</span><span class="sxs-lookup"><span data-stu-id="8014d-148">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="8014d-149">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="8014d-149">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="8014d-150">Use the following **ALTER DATABASE** statement to make a local database into a Geo-Replication primary with a readable secondary database on a secondary server in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="8014d-150">Use the following **ALTER DATABASE** statement to make a local database into a Geo-Replication primary with a readable secondary database on a secondary server in an elastic pool.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. <span data-ttu-id="8014d-151">Click **Execute** to run the query.</span><span class="sxs-lookup"><span data-stu-id="8014d-151">Click **Execute** to run the query.</span></span>

## <a name="remove-secondary-database"></a><span data-ttu-id="8014d-152">Remove secondary database</span><span class="sxs-lookup"><span data-stu-id="8014d-152">Remove secondary database</span></span>
<span data-ttu-id="8014d-153">You can use the **ALTER DATABASE** statement to permanently terminate the replication partnership between a secondary database and its primary.</span><span class="sxs-lookup"><span data-stu-id="8014d-153">You can use the **ALTER DATABASE** statement to permanently terminate the replication partnership between a secondary database and its primary.</span></span> <span data-ttu-id="8014d-154">This statement is executed on the master database on which the primary database resides.</span><span class="sxs-lookup"><span data-stu-id="8014d-154">This statement is executed on the master database on which the primary database resides.</span></span> <span data-ttu-id="8014d-155">After the relationship termination, the secondary database becomes a regular read-write database.</span><span class="sxs-lookup"><span data-stu-id="8014d-155">After the relationship termination, the secondary database becomes a regular read-write database.</span></span> <span data-ttu-id="8014d-156">If the connectivity to secondary database is broken the command succeeds but the secondary will become read-write after connectivity is restored.</span><span class="sxs-lookup"><span data-stu-id="8014d-156">If the connectivity to secondary database is broken the command succeeds but the secondary will become read-write after connectivity is restored.</span></span> <span data-ttu-id="8014d-157">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="8014d-157">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>

<span data-ttu-id="8014d-158">Use the following steps to remove geo-replicated secondary from a Geo-Replication partnership.</span><span class="sxs-lookup"><span data-stu-id="8014d-158">Use the following steps to remove geo-replicated secondary from a Geo-Replication partnership.</span></span>

1. <span data-ttu-id="8014d-159">In Management Studio, connect to your Azure SQL Database logical server.</span><span class="sxs-lookup"><span data-stu-id="8014d-159">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="8014d-160">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="8014d-160">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="8014d-161">Use the following **ALTER DATABASE** statement to remove a geo-replicated secondary.</span><span class="sxs-lookup"><span data-stu-id="8014d-161">Use the following **ALTER DATABASE** statement to remove a geo-replicated secondary.</span></span>
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. <span data-ttu-id="8014d-162">Click **Execute** to run the query.</span><span class="sxs-lookup"><span data-stu-id="8014d-162">Click **Execute** to run the query.</span></span>

## <a name="monitor-active-geo-replication-configuration-and-health"></a><span data-ttu-id="8014d-163">Monitor active geo-replication configuration and health</span><span class="sxs-lookup"><span data-stu-id="8014d-163">Monitor active geo-replication configuration and health</span></span>

<span data-ttu-id="8014d-164">Monitoring tasks include monitoring of the Geo-Replication configuration and monitoring data replication health.</span><span class="sxs-lookup"><span data-stu-id="8014d-164">Monitoring tasks include monitoring of the Geo-Replication configuration and monitoring data replication health.</span></span>  <span data-ttu-id="8014d-165">You can use the **sys.dm_geo_replication_links** dynamic management view in the master database to return information about all exiting replication links for each database on the Azure SQL Database logical server.</span><span class="sxs-lookup"><span data-stu-id="8014d-165">You can use the **sys.dm_geo_replication_links** dynamic management view in the master database to return information about all exiting replication links for each database on the Azure SQL Database logical server.</span></span> <span data-ttu-id="8014d-166">This view contains a row for each of the replication link between primary and secondary databases.</span><span class="sxs-lookup"><span data-stu-id="8014d-166">This view contains a row for each of the replication link between primary and secondary databases.</span></span> <span data-ttu-id="8014d-167">You can use the **sys.dm_replication_link_status** dynamic management view to return a row for each Azure SQL Database that is currently engaged in a replication replication link.</span><span class="sxs-lookup"><span data-stu-id="8014d-167">You can use the **sys.dm_replication_link_status** dynamic management view to return a row for each Azure SQL Database that is currently engaged in a replication replication link.</span></span> <span data-ttu-id="8014d-168">This includes both primary and secondary databases.</span><span class="sxs-lookup"><span data-stu-id="8014d-168">This includes both primary and secondary databases.</span></span> <span data-ttu-id="8014d-169">If more than one continuous replication link exists for a given primary database, this table contains a row for each of the relationships.</span><span class="sxs-lookup"><span data-stu-id="8014d-169">If more than one continuous replication link exists for a given primary database, this table contains a row for each of the relationships.</span></span> <span data-ttu-id="8014d-170">The view is created in all databases, including the logical master.</span><span class="sxs-lookup"><span data-stu-id="8014d-170">The view is created in all databases, including the logical master.</span></span> <span data-ttu-id="8014d-171">However, querying this view in the logical master returns an empty set.</span><span class="sxs-lookup"><span data-stu-id="8014d-171">However, querying this view in the logical master returns an empty set.</span></span> <span data-ttu-id="8014d-172">You can use the **sys.dm_operation_status** dynamic management view to show the status for all database operations including the status of the replication links.</span><span class="sxs-lookup"><span data-stu-id="8014d-172">You can use the **sys.dm_operation_status** dynamic management view to show the status for all database operations including the status of the replication links.</span></span> <span data-ttu-id="8014d-173">For more information, see [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), and [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).</span><span class="sxs-lookup"><span data-stu-id="8014d-173">For more information, see [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), and [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).</span></span>

<span data-ttu-id="8014d-174">Use the following steps to monitor an active geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="8014d-174">Use the following steps to monitor an active geo-replication partnership.</span></span>

1. <span data-ttu-id="8014d-175">In Management Studio, connect to your Azure SQL Database logical server.</span><span class="sxs-lookup"><span data-stu-id="8014d-175">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="8014d-176">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="8014d-176">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="8014d-177">Use the following statement to show all databases with Geo-Replication links.</span><span class="sxs-lookup"><span data-stu-id="8014d-177">Use the following statement to show all databases with Geo-Replication links.</span></span>
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM [sys].geo_replication_links;
4. <span data-ttu-id="8014d-178">Click **Execute** to run the query.</span><span class="sxs-lookup"><span data-stu-id="8014d-178">Click **Execute** to run the query.</span></span>
5. <span data-ttu-id="8014d-179">Open the Databases folder, expand the **System Databases** folder, right-click on **MyDB**, and then click **New Query**.</span><span class="sxs-lookup"><span data-stu-id="8014d-179">Open the Databases folder, expand the **System Databases** folder, right-click on **MyDB**, and then click **New Query**.</span></span>
6. <span data-ttu-id="8014d-180">Use the following statement to show the replication lags and last replication time of my secondary databases of MyDB.</span><span class="sxs-lookup"><span data-stu-id="8014d-180">Use the following statement to show the replication lags and last replication time of my secondary databases of MyDB.</span></span>
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. <span data-ttu-id="8014d-181">Click **Execute** to run the query.</span><span class="sxs-lookup"><span data-stu-id="8014d-181">Click **Execute** to run the query.</span></span>
8. <span data-ttu-id="8014d-182">Use the following statement to show the most recent geo-replication operations associated with database MyDB.</span><span class="sxs-lookup"><span data-stu-id="8014d-182">Use the following statement to show the most recent geo-replication operations associated with database MyDB.</span></span>
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. <span data-ttu-id="8014d-183">Click **Execute** to run the query.</span><span class="sxs-lookup"><span data-stu-id="8014d-183">Click **Execute** to run the query.</span></span>

## <a name="upgrade-a-non-readable-secondary-to-readable"></a><span data-ttu-id="8014d-184">Upgrade a non-readable secondary to readable</span><span class="sxs-lookup"><span data-stu-id="8014d-184">Upgrade a non-readable secondary to readable</span></span>
<span data-ttu-id="8014d-185">In April 2017, the non-readable secondary type will be retired and existing non-readable databases will automatically be upgraded to readable secondaries.</span><span class="sxs-lookup"><span data-stu-id="8014d-185">In April 2017, the non-readable secondary type will be retired and existing non-readable databases will automatically be upgraded to readable secondaries.</span></span> <span data-ttu-id="8014d-186">If you are using non-readable secondaries today and want to upgrade them to be readable, you can use the following simple steps for each secondary.</span><span class="sxs-lookup"><span data-stu-id="8014d-186">If you are using non-readable secondaries today and want to upgrade them to be readable, you can use the following simple steps for each secondary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8014d-187">There is no self-service method of in-place upgrading of a non-readable secondary to readable.</span><span class="sxs-lookup"><span data-stu-id="8014d-187">There is no self-service method of in-place upgrading of a non-readable secondary to readable.</span></span> <span data-ttu-id="8014d-188">If you drop your only secondary, then the primary database will remain unprotected until the new secondary is fully synchronized.</span><span class="sxs-lookup"><span data-stu-id="8014d-188">If you drop your only secondary, then the primary database will remain unprotected until the new secondary is fully synchronized.</span></span> <span data-ttu-id="8014d-189">If your application’s SLA requires that the primary is always protected, you should consider creating a parallel secondary in a different server before applying the upgrade steps above.</span><span class="sxs-lookup"><span data-stu-id="8014d-189">If your application’s SLA requires that the primary is always protected, you should consider creating a parallel secondary in a different server before applying the upgrade steps above.</span></span> <span data-ttu-id="8014d-190">Note each primary can have up to 4 secondary databases.</span><span class="sxs-lookup"><span data-stu-id="8014d-190">Note each primary can have up to 4 secondary databases.</span></span>
> 
> 

1. <span data-ttu-id="8014d-191">First, connect to the *secondary* server and drop the non-readable secondary database:</span><span class="sxs-lookup"><span data-stu-id="8014d-191">First, connect to the *secondary* server and drop the non-readable secondary database:</span></span>  
   
        DROP DATABASE <MyNonReadableSecondaryDB>;
2. <span data-ttu-id="8014d-192">Now connect to the *primary* server and add a new readable secondary</span><span class="sxs-lookup"><span data-stu-id="8014d-192">Now connect to the *primary* server and add a new readable secondary</span></span>
   
        ALTER DATABASE <MyDB>
            ADD SECONDARY ON SERVER <MySecondaryServer> WITH (ALLOW_CONNECTIONS = ALL);

## <a name="next-steps"></a><span data-ttu-id="8014d-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="8014d-193">Next steps</span></span>
* <span data-ttu-id="8014d-194">To learn more about active geo-replication, see - [Active geo-replication](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8014d-194">To learn more about active geo-replication, see - [Active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="8014d-195">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="8014d-195">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md)</span></span>

