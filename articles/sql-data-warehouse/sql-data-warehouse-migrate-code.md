---
title: Migrate your SQL code to SQL Data Warehouse | Microsoft Docs
description: Tips for migrating your SQL code to Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 01/30/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 3fd5224983c723faefb8001888ae20e78acdb8ce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552260"
---
# <a name="migrate-your-sql-code-to-sql-data-warehouse"></a><span data-ttu-id="69168-103">Migrate your SQL code to SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="69168-103">Migrate your SQL code to SQL Data Warehouse</span></span>
<span data-ttu-id="69168-104">When migrating your code from another database to SQL Data Warehouse, you will most likely need to make changes to your code base.</span><span class="sxs-lookup"><span data-stu-id="69168-104">When migrating your code from another database to SQL Data Warehouse, you will most likely need to make changes to your code base.</span></span> <span data-ttu-id="69168-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span><span class="sxs-lookup"><span data-stu-id="69168-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span></span> <span data-ttu-id="69168-106">However, to maintain performance and scale, some features are also not available.</span><span class="sxs-lookup"><span data-stu-id="69168-106">However, to maintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="69168-107">Common T-SQL Limitations</span><span class="sxs-lookup"><span data-stu-id="69168-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="69168-108">The following list summarizes the most common feature which are not supported in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="69168-108">The following list summarizes the most common feature which are not supported in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="69168-109">The links take you to workarounds for the unsupported feature:</span><span class="sxs-lookup"><span data-stu-id="69168-109">The links take you to workarounds for the unsupported feature:</span></span>

* <span data-ttu-id="69168-110">[ANSI joins on updates][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="69168-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="69168-111">[ANSI joins on deletes][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="69168-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="69168-112">[merge statement][merge statement]</span><span class="sxs-lookup"><span data-stu-id="69168-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="69168-113">cross-database joins</span><span class="sxs-lookup"><span data-stu-id="69168-113">cross-database joins</span></span>
* <span data-ttu-id="69168-114">[cursors][cursors]</span><span class="sxs-lookup"><span data-stu-id="69168-114">[cursors][cursors]</span></span>
* <span data-ttu-id="69168-115">[INSERT..EXEC][INSERT..EXEC]</span><span class="sxs-lookup"><span data-stu-id="69168-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="69168-116">output clause</span><span class="sxs-lookup"><span data-stu-id="69168-116">output clause</span></span>
* <span data-ttu-id="69168-117">inline user-defined functions</span><span class="sxs-lookup"><span data-stu-id="69168-117">inline user-defined functions</span></span>
* <span data-ttu-id="69168-118">multi-statement functions</span><span class="sxs-lookup"><span data-stu-id="69168-118">multi-statement functions</span></span>
* [<span data-ttu-id="69168-119">common table expressions</span><span class="sxs-lookup"><span data-stu-id="69168-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="69168-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="69168-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="69168-121">CLR functions and procedures</span><span class="sxs-lookup"><span data-stu-id="69168-121">CLR functions and procedures</span></span>
* <span data-ttu-id="69168-122">$partition function</span><span class="sxs-lookup"><span data-stu-id="69168-122">$partition function</span></span>
* <span data-ttu-id="69168-123">table variables</span><span class="sxs-lookup"><span data-stu-id="69168-123">table variables</span></span>
* <span data-ttu-id="69168-124">table value parameters</span><span class="sxs-lookup"><span data-stu-id="69168-124">table value parameters</span></span>
* <span data-ttu-id="69168-125">distributed transactions</span><span class="sxs-lookup"><span data-stu-id="69168-125">distributed transactions</span></span>
* <span data-ttu-id="69168-126">commit / rollback work</span><span class="sxs-lookup"><span data-stu-id="69168-126">commit / rollback work</span></span>
* <span data-ttu-id="69168-127">save transaction</span><span class="sxs-lookup"><span data-stu-id="69168-127">save transaction</span></span>
* <span data-ttu-id="69168-128">execution contexts (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="69168-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="69168-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="69168-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="69168-130">[nesting levels beyond 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="69168-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="69168-131">[updating through views][updating through views]</span><span class="sxs-lookup"><span data-stu-id="69168-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="69168-132">[use of select for variable assignment][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="69168-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="69168-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="69168-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="69168-134">Fortunately most of these limitations can be worked around.</span><span class="sxs-lookup"><span data-stu-id="69168-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="69168-135">Explanations are provided in the relevant development articles referenced above.</span><span class="sxs-lookup"><span data-stu-id="69168-135">Explanations are provided in the relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="69168-136">Supported CTE features</span><span class="sxs-lookup"><span data-stu-id="69168-136">Supported CTE features</span></span>
<span data-ttu-id="69168-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="69168-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="69168-138">The following CTE features are currently supported:</span><span class="sxs-lookup"><span data-stu-id="69168-138">The following CTE features are currently supported:</span></span>

* <span data-ttu-id="69168-139">A CTE can be specified in a SELECT statement.</span><span class="sxs-lookup"><span data-stu-id="69168-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="69168-140">A CTE can be specified in a CREATE VIEW statement.</span><span class="sxs-lookup"><span data-stu-id="69168-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="69168-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span><span class="sxs-lookup"><span data-stu-id="69168-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="69168-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span><span class="sxs-lookup"><span data-stu-id="69168-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="69168-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span><span class="sxs-lookup"><span data-stu-id="69168-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="69168-144">A remote table can be referenced from a CTE.</span><span class="sxs-lookup"><span data-stu-id="69168-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="69168-145">An external table can be referenced from a CTE.</span><span class="sxs-lookup"><span data-stu-id="69168-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="69168-146">Multiple CTE query definitions can be defined in a CTE.</span><span class="sxs-lookup"><span data-stu-id="69168-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="69168-147">CTE Limitations</span><span class="sxs-lookup"><span data-stu-id="69168-147">CTE Limitations</span></span>
<span data-ttu-id="69168-148">Common table expressions have some limitations in SQL Data Warehouse including:</span><span class="sxs-lookup"><span data-stu-id="69168-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="69168-149">A CTE must be followed by a single SELECT statement.</span><span class="sxs-lookup"><span data-stu-id="69168-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="69168-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span><span class="sxs-lookup"><span data-stu-id="69168-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="69168-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span><span class="sxs-lookup"><span data-stu-id="69168-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="69168-152">Specifying more than one WITH clause in a CTE is not allowed.</span><span class="sxs-lookup"><span data-stu-id="69168-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="69168-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span><span class="sxs-lookup"><span data-stu-id="69168-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="69168-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span><span class="sxs-lookup"><span data-stu-id="69168-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="69168-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span><span class="sxs-lookup"><span data-stu-id="69168-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="69168-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span><span class="sxs-lookup"><span data-stu-id="69168-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="69168-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span><span class="sxs-lookup"><span data-stu-id="69168-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="69168-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span><span class="sxs-lookup"><span data-stu-id="69168-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="69168-159">Recursive CTEs</span><span class="sxs-lookup"><span data-stu-id="69168-159">Recursive CTEs</span></span>
<span data-ttu-id="69168-160">Recursive CTEs are not supported in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="69168-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="69168-161">The migraion of recursive CTE can be somewhat complete and the best process is to break down the into multiple steps.</span><span class="sxs-lookup"><span data-stu-id="69168-161">The migraion of recursive CTE can be somewhat complete and the best process is to break down the into multiple steps.</span></span> <span data-ttu-id="69168-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span><span class="sxs-lookup"><span data-stu-id="69168-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span></span> <span data-ttu-id="69168-163">Once the temporary table is populated you can then return the data as a single result set.</span><span class="sxs-lookup"><span data-stu-id="69168-163">Once the temporary table is populated you can then return the data as a single result set.</span></span> <span data-ttu-id="69168-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span><span class="sxs-lookup"><span data-stu-id="69168-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="69168-165">Unsupported system functions</span><span class="sxs-lookup"><span data-stu-id="69168-165">Unsupported system functions</span></span>
<span data-ttu-id="69168-166">There are also some system functions that are not supported.</span><span class="sxs-lookup"><span data-stu-id="69168-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="69168-167">Some of the main ones you might typically find used in data warehousing are:</span><span class="sxs-lookup"><span data-stu-id="69168-167">Some of the main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="69168-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="69168-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="69168-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="69168-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="69168-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="69168-170">@@IDENTITY()</span></span>
* <span data-ttu-id="69168-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="69168-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="69168-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="69168-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="69168-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="69168-173">ERROR_LINE()</span></span>

<span data-ttu-id="69168-174">Some of these issues can be worked around.</span><span class="sxs-lookup"><span data-stu-id="69168-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="69168-175">@@ROWCOUNT workaround</span><span class="sxs-lookup"><span data-stu-id="69168-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="69168-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span><span class="sxs-lookup"><span data-stu-id="69168-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a><span data-ttu-id="69168-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="69168-177">Next steps</span></span>
<span data-ttu-id="69168-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="69168-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
