---
title: Monitor your workload using DMVs | Microsoft Docs
description: Learn how to monitor your workload using DMVs.
services: sql-data-warehouse
author: kevinvngo
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: manage
ms.date: 04/17/2018
ms.author: kevin
ms.reviewer: igorstan
ms.openlocfilehash: fe989a1693d73dbbea7ed0e3e91ed7aaf6fc37c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44794981"
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="ba4d1-103">Monitor your workload using DMVs</span><span class="sxs-lookup"><span data-stu-id="ba4d1-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="ba4d1-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload.</span></span> <span data-ttu-id="ba4d1-105">This includes investigating query execution in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-105">This includes investigating query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="ba4d1-106">Permissions</span><span class="sxs-lookup"><span data-stu-id="ba4d1-106">Permissions</span></span>
<span data-ttu-id="ba4d1-107">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-107">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="ba4d1-108">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-108">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE TO myuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="ba4d1-109">Monitor connections</span><span class="sxs-lookup"><span data-stu-id="ba4d1-109">Monitor connections</span></span>
<span data-ttu-id="ba4d1-110">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="ba4d1-110">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="ba4d1-111">This DMV contains the last 10,000 logins.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-111">This DMV contains the last 10,000 logins.</span></span>  <span data-ttu-id="ba4d1-112">The session_id is the primary key and is assigned sequentially for each new logon.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-112">The session_id is the primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="ba4d1-113">Monitor query execution</span><span class="sxs-lookup"><span data-stu-id="ba4d1-113">Monitor query execution</span></span>
<span data-ttu-id="ba4d1-114">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="ba4d1-114">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="ba4d1-115">This DMV contains the last 10,000 queries executed.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-115">This DMV contains the last 10,000 queries executed.</span></span>  <span data-ttu-id="ba4d1-116">The request_id uniquely identifies each query and is the primary key for this DMV.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-116">The request_id uniquely identifies each query and is the primary key for this DMV.</span></span>  <span data-ttu-id="ba4d1-117">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-117">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="ba4d1-118">Querying this DMV for a given session_id shows all queries for a given logon.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-118">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="ba4d1-119">Stored procedures use multiple Request IDs.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-119">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="ba4d1-120">Request IDs are assigned in sequential order.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-120">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="ba4d1-121">Here are steps to follow to investigate query execution plans and times for a particular query.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-121">Here are steps to follow to investigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-the-query-you-wish-to-investigate"></a><span data-ttu-id="ba4d1-122">STEP 1: Identify the query you wish to investigate</span><span class="sxs-lookup"><span data-stu-id="ba4d1-122">STEP 1: Identify the query you wish to investigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with the Label 'My Query'
-- Use brackets when querying the label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="ba4d1-123">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-123">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span></span>

<span data-ttu-id="ba4d1-124">Queries in the **Suspended** state are being queued due to concurrency limits.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-124">Queries in the **Suspended** state are being queued due to concurrency limits.</span></span> <span data-ttu-id="ba4d1-125">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-125">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="ba4d1-126">For information on concurrency limits, see [Performance tiers](performance-tiers.md) or [Resource classes for workload management](resource-classes-for-workload-management.md).</span><span class="sxs-lookup"><span data-stu-id="ba4d1-126">For information on concurrency limits, see [Performance tiers](performance-tiers.md) or [Resource classes for workload management](resource-classes-for-workload-management.md).</span></span> <span data-ttu-id="ba4d1-127">Queries can also wait for other reasons such as for object locks.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-127">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="ba4d1-128">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-128">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="ba4d1-129">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-129">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-the-query-plan"></a><span data-ttu-id="ba4d1-130">STEP 2: Investigate the query plan</span><span class="sxs-lookup"><span data-stu-id="ba4d1-130">STEP 2: Investigate the query plan</span></span>
<span data-ttu-id="ba4d1-131">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="ba4d1-131">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find the distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="ba4d1-132">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-132">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="ba4d1-133">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-133">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span></span> <span data-ttu-id="ba4d1-134">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-134">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span></span>

<span data-ttu-id="ba4d1-135">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span><span class="sxs-lookup"><span data-stu-id="ba4d1-135">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span></span>

* <span data-ttu-id="ba4d1-136">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-136">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="ba4d1-137">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-137">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-the-distributed-databases"></a><span data-ttu-id="ba4d1-138">STEP 3a: Investigate SQL on the distributed databases</span><span class="sxs-lookup"><span data-stu-id="ba4d1-138">STEP 3a: Investigate SQL on the distributed databases</span></span>
<span data-ttu-id="ba4d1-139">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-139">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span></span>

```sql
-- Find the distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="ba4d1-140">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-140">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span></span>

```sql
-- Find the SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-the-distributed-databases"></a><span data-ttu-id="ba4d1-141">STEP 3b: Investigate data movement on the distributed databases</span><span class="sxs-lookup"><span data-stu-id="ba4d1-141">STEP 3b: Investigate data movement on the distributed databases</span></span>
<span data-ttu-id="ba4d1-142">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="ba4d1-142">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find the information about all the workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="ba4d1-143">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-143">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="ba4d1-144">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-144">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="ba4d1-145">If so, this finding might indicate skew of your underlying data.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-145">If so, this finding might indicate skew of your underlying data.</span></span>

<span data-ttu-id="ba4d1-146">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-146">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find the SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="ba4d1-147">Monitor waiting queries</span><span class="sxs-lookup"><span data-stu-id="ba4d1-147">Monitor waiting queries</span></span>
<span data-ttu-id="ba4d1-148">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-148">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="ba4d1-149">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-149">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span></span>  <span data-ttu-id="ba4d1-150">If the query has all the required resources, then the state will be **Granted**.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-150">If the query has all the required resources, then the state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="ba4d1-151">Monitor tempdb</span><span class="sxs-lookup"><span data-stu-id="ba4d1-151">Monitor tempdb</span></span>
<span data-ttu-id="ba4d1-152">High tempdb utilization can be the root cause for slow performance and out of memory issues.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-152">High tempdb utilization can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="ba4d1-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="ba4d1-154">The following information describes how to identify tempdb usage per query on each node.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-154">The following information describes how to identify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="ba4d1-155">Create the following view to associate the appropriate node ID for sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-155">Create the following view to associate the appropriate node ID for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="ba4d1-156">Having the node ID will enable you to use other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-156">Having the node ID will enable you to use other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with the correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="ba4d1-157">To monitor tempdb, run the following query:</span><span class="sxs-lookup"><span data-stu-id="ba4d1-157">To monitor tempdb, run the following query:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="ba4d1-158">Monitor memory</span><span class="sxs-lookup"><span data-stu-id="ba4d1-158">Monitor memory</span></span>

<span data-ttu-id="ba4d1-159">Memory can be the root cause for slow performance and out of memory issues.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-159">Memory can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="ba4d1-160">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-160">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="ba4d1-161">The following query returns SQL Server memory usage and memory pressure per node:</span><span class="sxs-lookup"><span data-stu-id="ba4d1-161">The following query returns SQL Server memory usage and memory pressure per node:</span></span>   
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="ba4d1-162">Monitor transaction log size</span><span class="sxs-lookup"><span data-stu-id="ba4d1-162">Monitor transaction log size</span></span>
<span data-ttu-id="ba4d1-163">The following query returns the transaction log size on each distribution.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-163">The following query returns the transaction log size on each distribution.</span></span> <span data-ttu-id="ba4d1-164">If one of the log files is reaching 160 GB, you should consider scaling up your instance or limiting your transaction size.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-164">If one of the log files is reaching 160 GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="ba4d1-165">Monitor transaction log rollback</span><span class="sxs-lookup"><span data-stu-id="ba4d1-165">Monitor transaction log rollback</span></span>
<span data-ttu-id="ba4d1-166">If your queries are failing or taking a long time to proceed, you can check and monitor if you have any transactions rolling back.</span><span class="sxs-lookup"><span data-stu-id="ba4d1-166">If your queries are failing or taking a long time to proceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="ba4d1-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="ba4d1-167">Next steps</span></span>
<span data-ttu-id="ba4d1-168">For more information about DMVs, see [System views][System views].</span><span class="sxs-lookup"><span data-stu-id="ba4d1-168">For more information about DMVs, see [System views][System views].</span></span>


<!--Image references-->

<!--Article references-->
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
