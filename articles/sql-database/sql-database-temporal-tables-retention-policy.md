---
title: Manage historical data in Temporal Tables with retention policy | Microsoft Docs
description: Learn how to use temporal retention policy to keep historical data under your control.
services: sql-database
documentationcenter: ''
author: bonova
manager: drasumic
editor: ''
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: development
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: 357d188c44fcfb688275f7377486df722ea50d5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553299"
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="437f6-103">Manage historical data in Temporal Tables with retention policy</span><span class="sxs-lookup"><span data-stu-id="437f6-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="437f6-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span><span class="sxs-lookup"><span data-stu-id="437f6-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="437f6-105">Hence, retention policy for historical data is an important aspect of planning and managing the lifecycle of every temporal table.</span><span class="sxs-lookup"><span data-stu-id="437f6-105">Hence, retention policy for historical data is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="437f6-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span><span class="sxs-lookup"><span data-stu-id="437f6-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="437f6-107">Temporal history retention can be configured at the individual table level, which allows users to create flexible aging polices.</span><span class="sxs-lookup"><span data-stu-id="437f6-107">Temporal history retention can be configured at the individual table level, which allows users to create flexible aging polices.</span></span> <span data-ttu-id="437f6-108">Applying temporal retention is simple: it requires only one parameter to be set during table creation or schema change.</span><span class="sxs-lookup"><span data-stu-id="437f6-108">Applying temporal retention is simple: it requires only one parameter to be set during table creation or schema change.</span></span>

<span data-ttu-id="437f6-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span><span class="sxs-lookup"><span data-stu-id="437f6-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="437f6-110">Identification of matching rows and their removal from the history table occur transparently, in the background task that is scheduled and run by the system.</span><span class="sxs-lookup"><span data-stu-id="437f6-110">Identification of matching rows and their removal from the history table occur transparently, in the background task that is scheduled and run by the system.</span></span> <span data-ttu-id="437f6-111">Age condition for the history table rows is checked based on the column representing end of SYSTEM_TIME period.</span><span class="sxs-lookup"><span data-stu-id="437f6-111">Age condition for the history table rows is checked based on the column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="437f6-112">If retention period, for example, is set to six months, table rows eligible for cleanup satisfy the following condition:</span><span class="sxs-lookup"><span data-stu-id="437f6-112">If retention period, for example, is set to six months, table rows eligible for cleanup satisfy the following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="437f6-113">In the preceding example, we assumed that **ValidTo** column corresponds to the end of SYSTEM_TIME period.</span><span class="sxs-lookup"><span data-stu-id="437f6-113">In the preceding example, we assumed that **ValidTo** column corresponds to the end of SYSTEM_TIME period.</span></span>

## <a name="how-to-configure-retention-policy"></a><span data-ttu-id="437f6-114">How to configure retention policy?</span><span class="sxs-lookup"><span data-stu-id="437f6-114">How to configure retention policy?</span></span>
<span data-ttu-id="437f6-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at the database level*.</span><span class="sxs-lookup"><span data-stu-id="437f6-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at the database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="437f6-116">Database flag **is_temporal_history_retention_enabled** is set to ON by default, but users can change it with ALTER DATABASE statement.</span><span class="sxs-lookup"><span data-stu-id="437f6-116">Database flag **is_temporal_history_retention_enabled** is set to ON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="437f6-117">It is also automatically set to OFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span><span class="sxs-lookup"><span data-stu-id="437f6-117">It is also automatically set to OFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="437f6-118">To enable temporal history retention cleanup for your database, execute the following statement:</span><span class="sxs-lookup"><span data-stu-id="437f6-118">To enable temporal history retention cleanup for your database, execute the following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="437f6-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span><span class="sxs-lookup"><span data-stu-id="437f6-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="437f6-120">Retention policy is configured during table creation by specifying value for the HISTORY_RETENTION_PERIOD parameter:</span><span class="sxs-lookup"><span data-stu-id="437f6-120">Retention policy is configured during table creation by specifying value for the HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="437f6-121">Azure SQL Database allows you to specify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span><span class="sxs-lookup"><span data-stu-id="437f6-121">Azure SQL Database allows you to specify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="437f6-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span><span class="sxs-lookup"><span data-stu-id="437f6-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="437f6-123">You can also use INFINITE keyword explicitly.</span><span class="sxs-lookup"><span data-stu-id="437f6-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="437f6-124">In some scenarios, you may want to configure retention after table creation, or to change previously configured value.</span><span class="sxs-lookup"><span data-stu-id="437f6-124">In some scenarios, you may want to configure retention after table creation, or to change previously configured value.</span></span> <span data-ttu-id="437f6-125">In that case use ALTER TABLE statement:</span><span class="sxs-lookup"><span data-stu-id="437f6-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="437f6-126">Setting SYSTEM_VERSIONING to OFF *does not preserve* retention period value.</span><span class="sxs-lookup"><span data-stu-id="437f6-126">Setting SYSTEM_VERSIONING to OFF *does not preserve* retention period value.</span></span> <span data-ttu-id="437f6-127">Setting SYSTEM_VERSIONING to ON without HISTORY_RETENTION_PERIOD specified explicitly results in the INFINITE retention period.</span><span class="sxs-lookup"><span data-stu-id="437f6-127">Setting SYSTEM_VERSIONING to ON without HISTORY_RETENTION_PERIOD specified explicitly results in the INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="437f6-128">To review current state of the retention policy, use the following query that joins temporal retention enablement flag at the database level with retention periods for individual tables:</span><span class="sxs-lookup"><span data-stu-id="437f6-128">To review current state of the retention policy, use the following query that joins temporal retention enablement flag at the database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="437f6-129">How SQL Database deletes aged rows?</span><span class="sxs-lookup"><span data-stu-id="437f6-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="437f6-130">The cleanup process depends on the index layout of the history table.</span><span class="sxs-lookup"><span data-stu-id="437f6-130">The cleanup process depends on the index layout of the history table.</span></span> <span data-ttu-id="437f6-131">It is important to notice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span><span class="sxs-lookup"><span data-stu-id="437f6-131">It is important to notice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="437f6-132">A background task is created to perform aged data cleanup for all temporal tables with finite retention period.</span><span class="sxs-lookup"><span data-stu-id="437f6-132">A background task is created to perform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="437f6-133">Cleanup logic for the rowstore (B-tree) clustered index deletes aged row in smaller chunks (up to 10K) minimizing pressure on database log and I/O subsystem.</span><span class="sxs-lookup"><span data-stu-id="437f6-133">Cleanup logic for the rowstore (B-tree) clustered index deletes aged row in smaller chunks (up to 10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="437f6-134">Although cleanup logic utilizes required B-tree index, order of deletions for the rows older than retention period cannot be firmly guaranteed.</span><span class="sxs-lookup"><span data-stu-id="437f6-134">Although cleanup logic utilizes required B-tree index, order of deletions for the rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="437f6-135">Hence, *do not take any dependency on the cleanup order in your applications*.</span><span class="sxs-lookup"><span data-stu-id="437f6-135">Hence, *do not take any dependency on the cleanup order in your applications*.</span></span>

<span data-ttu-id="437f6-136">The cleanup task for the clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span><span class="sxs-lookup"><span data-stu-id="437f6-136">The cleanup task for the clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Clustered columnstore retention](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="437f6-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span><span class="sxs-lookup"><span data-stu-id="437f6-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="437f6-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span><span class="sxs-lookup"><span data-stu-id="437f6-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="437f6-140">Index considerations</span><span class="sxs-lookup"><span data-stu-id="437f6-140">Index considerations</span></span>
<span data-ttu-id="437f6-141">The cleanup task for tables with rowstore clustered index requires index to start with the column corresponding the end of SYSTEM_TIME period.</span><span class="sxs-lookup"><span data-stu-id="437f6-141">The cleanup task for tables with rowstore clustered index requires index to start with the column corresponding the end of SYSTEM_TIME period.</span></span> <span data-ttu-id="437f6-142">If such index doesn't exist, you cannot configure a finite retention period:</span><span class="sxs-lookup"><span data-stu-id="437f6-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="437f6-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because the history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with the column that matches end of SYSTEM_TIME period, on the history table.*</span><span class="sxs-lookup"><span data-stu-id="437f6-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because the history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with the column that matches end of SYSTEM_TIME period, on the history table.*</span></span>

<span data-ttu-id="437f6-144">It is important to notice that the default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span><span class="sxs-lookup"><span data-stu-id="437f6-144">It is important to notice that the default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="437f6-145">If you try to remove that index on a table with finite retention period, operation fails with the following error:</span><span class="sxs-lookup"><span data-stu-id="437f6-145">If you try to remove that index on a table with finite retention period, operation fails with the following error:</span></span>

<span data-ttu-id="437f6-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop the clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD to INFINITE on the corresponding system-versioned temporal table if you need to drop this index.*</span><span class="sxs-lookup"><span data-stu-id="437f6-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop the clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD to INFINITE on the corresponding system-versioned temporal table if you need to drop this index.*</span></span>

<span data-ttu-id="437f6-147">Cleanup on the clustered columnstore index works optimally if historical rows are inserted in the ascending order (ordered by the end of period column), which is always the case when the history table is populated exclusively by the SYSTEM_VERSIONIOING mechanism.</span><span class="sxs-lookup"><span data-stu-id="437f6-147">Cleanup on the clustered columnstore index works optimally if historical rows are inserted in the ascending order (ordered by the end of period column), which is always the case when the history table is populated exclusively by the SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="437f6-148">If rows in the history table are not ordered by end of period column (which may be the case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, to achieve optimal performance.</span><span class="sxs-lookup"><span data-stu-id="437f6-148">If rows in the history table are not ordered by end of period column (which may be the case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, to achieve optimal performance.</span></span>

<span data-ttu-id="437f6-149">Avoid rebuilding clustered columnstore index on the history table with the finite retention period, because it may change ordering in the row groups naturally imposed by the system-versioning operation.</span><span class="sxs-lookup"><span data-stu-id="437f6-149">Avoid rebuilding clustered columnstore index on the history table with the finite retention period, because it may change ordering in the row groups naturally imposed by the system-versioning operation.</span></span> <span data-ttu-id="437f6-150">If you need to rebuild clustered columnstore index on the history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in the rowgroups necessary for regular data cleanup.</span><span class="sxs-lookup"><span data-stu-id="437f6-150">If you need to rebuild clustered columnstore index on the history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in the rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="437f6-151">The same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span><span class="sxs-lookup"><span data-stu-id="437f6-151">The same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by the end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="437f6-152">When finite retention period is configured for the history table with the clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span><span class="sxs-lookup"><span data-stu-id="437f6-152">When finite retention period is configured for the history table with the clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="437f6-153">An attempt to execute above statement fails with the following error:</span><span class="sxs-lookup"><span data-stu-id="437f6-153">An attempt to execute above statement fails with the following error:</span></span>

<span data-ttu-id="437f6-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span><span class="sxs-lookup"><span data-stu-id="437f6-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="437f6-155">Querying tables with retention policy</span><span class="sxs-lookup"><span data-stu-id="437f6-155">Querying tables with retention policy</span></span>
<span data-ttu-id="437f6-156">All queries on the temporal table automatically filter out historical rows matching finite retention policy, to avoid unpredictable and inconsistent results, since aged rows can be deleted by the cleanup task, *at any point in time and in arbitrary order*.</span><span class="sxs-lookup"><span data-stu-id="437f6-156">All queries on the temporal table automatically filter out historical rows matching finite retention policy, to avoid unpredictable and inconsistent results, since aged rows can be deleted by the cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="437f6-157">The following picture shows the query plan for a simple query:</span><span class="sxs-lookup"><span data-stu-id="437f6-157">The following picture shows the query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FROM SYSTEM_TIME ALL;
````

<span data-ttu-id="437f6-158">The query plan includes additional filter applied to end of period column (ValidTo) in the Clustered Index Scan operator on the history table (highlighted).</span><span class="sxs-lookup"><span data-stu-id="437f6-158">The query plan includes additional filter applied to end of period column (ValidTo) in the Clustered Index Scan operator on the history table (highlighted).</span></span> <span data-ttu-id="437f6-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span><span class="sxs-lookup"><span data-stu-id="437f6-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Retention query filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="437f6-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span><span class="sxs-lookup"><span data-stu-id="437f6-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="437f6-162">The following picture shows query execution plan for the query on the history table without additional filters applied:</span><span class="sxs-lookup"><span data-stu-id="437f6-162">The following picture shows query execution plan for the query on the history table without additional filters applied:</span></span>

![Querying history without retention filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="437f6-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span><span class="sxs-lookup"><span data-stu-id="437f6-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="437f6-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span><span class="sxs-lookup"><span data-stu-id="437f6-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="437f6-166">Point in time restore considerations</span><span class="sxs-lookup"><span data-stu-id="437f6-166">Point in time restore considerations</span></span>
<span data-ttu-id="437f6-167">When you create new database by [restoring existing database to a specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at the database level.</span><span class="sxs-lookup"><span data-stu-id="437f6-167">When you create new database by [restoring existing database to a specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at the database level.</span></span> <span data-ttu-id="437f6-168">(**is_temporal_history_retention_enabled** flag set to OFF).</span><span class="sxs-lookup"><span data-stu-id="437f6-168">(**is_temporal_history_retention_enabled** flag set to OFF).</span></span> <span data-ttu-id="437f6-169">This functionality allows you to examine all historical rows upon restore, without worrying that aged rows are removed before you get to query them.</span><span class="sxs-lookup"><span data-stu-id="437f6-169">This functionality allows you to examine all historical rows upon restore, without worrying that aged rows are removed before you get to query them.</span></span> <span data-ttu-id="437f6-170">You can use it to *inspect historical data beyond configured retention period*.</span><span class="sxs-lookup"><span data-stu-id="437f6-170">You can use it to *inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="437f6-171">Say that a temporal table has one MONTH retention period specified.</span><span class="sxs-lookup"><span data-stu-id="437f6-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="437f6-172">If your database was created in Premium Service tier, you would be able to create database copy with the database state up to 35 days back in the past.</span><span class="sxs-lookup"><span data-stu-id="437f6-172">If your database was created in Premium Service tier, you would be able to create database copy with the database state up to 35 days back in the past.</span></span> <span data-ttu-id="437f6-173">That effectively would allow you to analyze historical rows that are up to 65 days old by querying the history table directly.</span><span class="sxs-lookup"><span data-stu-id="437f6-173">That effectively would allow you to analyze historical rows that are up to 65 days old by querying the history table directly.</span></span>

<span data-ttu-id="437f6-174">If you want to activate temporal retention cleanup, run the following Transact-SQL statement after point in time restore:</span><span class="sxs-lookup"><span data-stu-id="437f6-174">If you want to activate temporal retention cleanup, run the following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="437f6-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="437f6-175">Next steps</span></span>
<span data-ttu-id="437f6-176">To learn how to use Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="437f6-176">To learn how to use Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="437f6-177">Visit Channel 9 to hear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="437f6-177">Visit Channel 9 to hear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="437f6-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="437f6-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>




