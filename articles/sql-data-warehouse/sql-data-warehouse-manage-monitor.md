---
title: Monitor your workload using DMVs | Microsoft Docs
description: Learn how to monitor your workload using DMVs.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 3735d656429da1f1fe7569f640b272b099382032
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556440"
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="170e8-103">Monitor your workload using DMVs</span><span class="sxs-lookup"><span data-stu-id="170e8-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="170e8-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload and investigate query execution in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="170e8-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="170e8-105">Permissions</span><span class="sxs-lookup"><span data-stu-id="170e8-105">Permissions</span></span>
<span data-ttu-id="170e8-106">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span><span class="sxs-lookup"><span data-stu-id="170e8-106">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="170e8-107">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span><span class="sxs-lookup"><span data-stu-id="170e8-107">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE TO myuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="170e8-108">Monitor connections</span><span class="sxs-lookup"><span data-stu-id="170e8-108">Monitor connections</span></span>
<span data-ttu-id="170e8-109">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="170e8-109">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="170e8-110">This DMV contains the last 10,000 logins.</span><span class="sxs-lookup"><span data-stu-id="170e8-110">This DMV contains the last 10,000 logins.</span></span>  <span data-ttu-id="170e8-111">The session_id is the primary key and is assigned sequentially for each new logon.</span><span class="sxs-lookup"><span data-stu-id="170e8-111">The session_id is the primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="170e8-112">Monitor query execution</span><span class="sxs-lookup"><span data-stu-id="170e8-112">Monitor query execution</span></span>
<span data-ttu-id="170e8-113">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="170e8-113">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="170e8-114">This DMV contains the last 10,000 queries executed.</span><span class="sxs-lookup"><span data-stu-id="170e8-114">This DMV contains the last 10,000 queries executed.</span></span>  <span data-ttu-id="170e8-115">The request_id uniquely identifies each query and is the primary key for this DMV.</span><span class="sxs-lookup"><span data-stu-id="170e8-115">The request_id uniquely identifies each query and is the primary key for this DMV.</span></span>  <span data-ttu-id="170e8-116">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span><span class="sxs-lookup"><span data-stu-id="170e8-116">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="170e8-117">Querying this DMV for a given session_id shows all queries for a given logon.</span><span class="sxs-lookup"><span data-stu-id="170e8-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="170e8-118">Stored procedures use multiple Request IDs.</span><span class="sxs-lookup"><span data-stu-id="170e8-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="170e8-119">Request IDs are assigned in sequential order.</span><span class="sxs-lookup"><span data-stu-id="170e8-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="170e8-120">Here are steps to follow to investigate query execution plans and times for a particular query.</span><span class="sxs-lookup"><span data-stu-id="170e8-120">Here are steps to follow to investigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-the-query-you-wish-to-investigate"></a><span data-ttu-id="170e8-121">STEP 1: Identify the query you wish to investigate</span><span class="sxs-lookup"><span data-stu-id="170e8-121">STEP 1: Identify the query you wish to investigate</span></span>
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

<span data-ttu-id="170e8-122">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span><span class="sxs-lookup"><span data-stu-id="170e8-122">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span></span>

<span data-ttu-id="170e8-123">Queries in the **Suspended** state are being queued due to concurrency limits.</span><span class="sxs-lookup"><span data-stu-id="170e8-123">Queries in the **Suspended** state are being queued due to concurrency limits.</span></span> <span data-ttu-id="170e8-124">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="170e8-124">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="170e8-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span><span class="sxs-lookup"><span data-stu-id="170e8-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="170e8-126">Queries can also wait for other reasons such as for object locks.</span><span class="sxs-lookup"><span data-stu-id="170e8-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="170e8-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span><span class="sxs-lookup"><span data-stu-id="170e8-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="170e8-128">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span><span class="sxs-lookup"><span data-stu-id="170e8-128">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-the-query-plan"></a><span data-ttu-id="170e8-129">STEP 2: Investigate the query plan</span><span class="sxs-lookup"><span data-stu-id="170e8-129">STEP 2: Investigate the query plan</span></span>
<span data-ttu-id="170e8-130">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="170e8-130">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find the distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="170e8-131">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span><span class="sxs-lookup"><span data-stu-id="170e8-131">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="170e8-132">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span><span class="sxs-lookup"><span data-stu-id="170e8-132">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span></span> <span data-ttu-id="170e8-133">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span><span class="sxs-lookup"><span data-stu-id="170e8-133">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span></span>

<span data-ttu-id="170e8-134">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span><span class="sxs-lookup"><span data-stu-id="170e8-134">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span></span>

* <span data-ttu-id="170e8-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="170e8-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="170e8-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="170e8-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-the-distributed-databases"></a><span data-ttu-id="170e8-137">STEP 3a: Investigate SQL on the distributed databases</span><span class="sxs-lookup"><span data-stu-id="170e8-137">STEP 3a: Investigate SQL on the distributed databases</span></span>
<span data-ttu-id="170e8-138">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span><span class="sxs-lookup"><span data-stu-id="170e8-138">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span></span>

```sql
-- Find the distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="170e8-139">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span><span class="sxs-lookup"><span data-stu-id="170e8-139">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span></span>

```sql
-- Find the SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-the-distributed-databases"></a><span data-ttu-id="170e8-140">STEP 3b: Investigate data movement on the distributed databases</span><span class="sxs-lookup"><span data-stu-id="170e8-140">STEP 3b: Investigate data movement on the distributed databases</span></span>
<span data-ttu-id="170e8-141">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="170e8-141">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find the information about all the workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="170e8-142">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span><span class="sxs-lookup"><span data-stu-id="170e8-142">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="170e8-143">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span><span class="sxs-lookup"><span data-stu-id="170e8-143">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="170e8-144">If so, this may indicate skew of your underlying data.</span><span class="sxs-lookup"><span data-stu-id="170e8-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="170e8-145">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span><span class="sxs-lookup"><span data-stu-id="170e8-145">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find the SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="170e8-146">Monitor waiting queries</span><span class="sxs-lookup"><span data-stu-id="170e8-146">Monitor waiting queries</span></span>
<span data-ttu-id="170e8-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span><span class="sxs-lookup"><span data-stu-id="170e8-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span></span>

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

<span data-ttu-id="170e8-148">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="170e8-148">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span></span>  <span data-ttu-id="170e8-149">If the query has all the required resources, then the state will be **Granted**.</span><span class="sxs-lookup"><span data-stu-id="170e8-149">If the query has all the required resources, then the state will be **Granted**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="170e8-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="170e8-150">Next steps</span></span>
<span data-ttu-id="170e8-151">See [System views][System views] for more information on DMVs.</span><span class="sxs-lookup"><span data-stu-id="170e8-151">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="170e8-152">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span><span class="sxs-lookup"><span data-stu-id="170e8-152">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
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
