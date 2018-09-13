---
title: In-Memory OLTP improves SQL txn perf | Microsoft Docs
description: Adopt In-Memory OLTP to improve transactional performance in an existing SQL database.
services: sql-database
documentationcenter: ''
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: development
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: db2d6dbdec80e8c443014c72c80172ad3effb82c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662771"
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a><span data-ttu-id="6296c-103">Use In-Memory OLTP to improve your application performance in SQL Database</span><span class="sxs-lookup"><span data-stu-id="6296c-103">Use In-Memory OLTP to improve your application performance in SQL Database</span></span>
<span data-ttu-id="6296c-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span><span class="sxs-lookup"><span data-stu-id="6296c-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="6296c-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="6296c-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="6296c-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span><span class="sxs-lookup"><span data-stu-id="6296c-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="6296c-107">Step 1: Ensure you are using a Premium database</span><span class="sxs-lookup"><span data-stu-id="6296c-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="6296c-108">In-Memory OLTP is supported only in Premium databases.</span><span class="sxs-lookup"><span data-stu-id="6296c-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="6296c-109">In-Memory is supported if the returned result is 1 (not 0):</span><span class="sxs-lookup"><span data-stu-id="6296c-109">In-Memory is supported if the returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="6296c-110">*XTP* stands for *Extreme Transaction Processing*</span><span class="sxs-lookup"><span data-stu-id="6296c-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a><span data-ttu-id="6296c-111">Step 2: Identify objects to migrate to In-Memory OLTP</span><span class="sxs-lookup"><span data-stu-id="6296c-111">Step 2: Identify objects to migrate to In-Memory OLTP</span></span>
<span data-ttu-id="6296c-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span><span class="sxs-lookup"><span data-stu-id="6296c-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="6296c-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span><span class="sxs-lookup"><span data-stu-id="6296c-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span></span>

<span data-ttu-id="6296c-114">In SSMS, to generate the report:</span><span class="sxs-lookup"><span data-stu-id="6296c-114">In SSMS, to generate the report:</span></span>

* <span data-ttu-id="6296c-115">In the **Object Explorer**, right-click your database node.</span><span class="sxs-lookup"><span data-stu-id="6296c-115">In the **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="6296c-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span><span class="sxs-lookup"><span data-stu-id="6296c-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="6296c-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="6296c-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="6296c-118">Step 3: Create a comparable test database</span><span class="sxs-lookup"><span data-stu-id="6296c-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="6296c-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span><span class="sxs-lookup"><span data-stu-id="6296c-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span></span> <span data-ttu-id="6296c-120">We recommend that you first test to confirm the indication by testing.</span><span class="sxs-lookup"><span data-stu-id="6296c-120">We recommend that you first test to confirm the indication by testing.</span></span>

<span data-ttu-id="6296c-121">You need a test copy of your production database.</span><span class="sxs-lookup"><span data-stu-id="6296c-121">You need a test copy of your production database.</span></span> <span data-ttu-id="6296c-122">The test database should be at the same service tier level as your production database.</span><span class="sxs-lookup"><span data-stu-id="6296c-122">The test database should be at the same service tier level as your production database.</span></span>

<span data-ttu-id="6296c-123">To ease testing, tweak your test database as follows:</span><span class="sxs-lookup"><span data-stu-id="6296c-123">To ease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="6296c-124">Connect to the test database by using SSMS.</span><span class="sxs-lookup"><span data-stu-id="6296c-124">Connect to the test database by using SSMS.</span></span>
2. <span data-ttu-id="6296c-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span><span class="sxs-lookup"><span data-stu-id="6296c-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="6296c-126">Step 4: Migrate tables</span><span class="sxs-lookup"><span data-stu-id="6296c-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="6296c-127">You must create and populate a memory-optimized copy of the table you want to test.</span><span class="sxs-lookup"><span data-stu-id="6296c-127">You must create and populate a memory-optimized copy of the table you want to test.</span></span> <span data-ttu-id="6296c-128">You can create it by using either:</span><span class="sxs-lookup"><span data-stu-id="6296c-128">You can create it by using either:</span></span>

* <span data-ttu-id="6296c-129">The handy Memory Optimization Wizard in SSMS.</span><span class="sxs-lookup"><span data-stu-id="6296c-129">The handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="6296c-130">Manual T-SQL.</span><span class="sxs-lookup"><span data-stu-id="6296c-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="6296c-131">Memory Optimization Wizard in SSMS</span><span class="sxs-lookup"><span data-stu-id="6296c-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="6296c-132">To use this migration option:</span><span class="sxs-lookup"><span data-stu-id="6296c-132">To use this migration option:</span></span>

1. <span data-ttu-id="6296c-133">Connect to the test database with SSMS.</span><span class="sxs-lookup"><span data-stu-id="6296c-133">Connect to the test database with SSMS.</span></span>
2. <span data-ttu-id="6296c-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span><span class="sxs-lookup"><span data-stu-id="6296c-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="6296c-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span><span class="sxs-lookup"><span data-stu-id="6296c-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="6296c-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span><span class="sxs-lookup"><span data-stu-id="6296c-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="6296c-137">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="6296c-137">For more information, see:</span></span>
   
   * <span data-ttu-id="6296c-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="6296c-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="6296c-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="6296c-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="6296c-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="6296c-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="6296c-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span><span class="sxs-lookup"><span data-stu-id="6296c-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="6296c-142">Manual T-SQL</span><span class="sxs-lookup"><span data-stu-id="6296c-142">Manual T-SQL</span></span>
<span data-ttu-id="6296c-143">To use this migration option:</span><span class="sxs-lookup"><span data-stu-id="6296c-143">To use this migration option:</span></span>

1. <span data-ttu-id="6296c-144">Connect to your test database by using SSMS (or a similar utility).</span><span class="sxs-lookup"><span data-stu-id="6296c-144">Connect to your test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="6296c-145">Obtain the complete T-SQL script for your table and its indexes.</span><span class="sxs-lookup"><span data-stu-id="6296c-145">Obtain the complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="6296c-146">In SSMS, right-click your table node.</span><span class="sxs-lookup"><span data-stu-id="6296c-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="6296c-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span><span class="sxs-lookup"><span data-stu-id="6296c-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="6296c-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span><span class="sxs-lookup"><span data-stu-id="6296c-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span></span>
4. <span data-ttu-id="6296c-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="6296c-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span></span>
5. <span data-ttu-id="6296c-150">Rename the existing table by using SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="6296c-150">Rename the existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="6296c-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span><span class="sxs-lookup"><span data-stu-id="6296c-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="6296c-152">Copy the data to your memory-optimized table by using INSERT...SELECT \* INTO:</span><span class="sxs-lookup"><span data-stu-id="6296c-152">Copy the data to your memory-optimized table by using INSERT...SELECT \* INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="6296c-153">Step 5 (optional): Migrate stored procedures</span><span class="sxs-lookup"><span data-stu-id="6296c-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="6296c-154">The In-Memory feature can also modify a stored procedure for improved performance.</span><span class="sxs-lookup"><span data-stu-id="6296c-154">The In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="6296c-155">Considerations with natively compiled stored procedures</span><span class="sxs-lookup"><span data-stu-id="6296c-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="6296c-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span><span class="sxs-lookup"><span data-stu-id="6296c-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="6296c-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="6296c-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="6296c-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6296c-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span></span>

<span data-ttu-id="6296c-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span><span class="sxs-lookup"><span data-stu-id="6296c-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="6296c-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span><span class="sxs-lookup"><span data-stu-id="6296c-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="6296c-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span><span class="sxs-lookup"><span data-stu-id="6296c-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="6296c-162">Typical CREATE PROCEDURE for natively compiled</span><span class="sxs-lookup"><span data-stu-id="6296c-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="6296c-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span><span class="sxs-lookup"><span data-stu-id="6296c-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="6296c-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6296c-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span></span> <span data-ttu-id="6296c-165">However,  a subset of the other values are also supported:</span><span class="sxs-lookup"><span data-stu-id="6296c-165">However,  a subset of the other values are also supported:</span></span>
  
  * <span data-ttu-id="6296c-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="6296c-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="6296c-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="6296c-167">SERIALIZABLE</span></span>
* <span data-ttu-id="6296c-168">The LANGUAGE value must be present in the sys.languages view.</span><span class="sxs-lookup"><span data-stu-id="6296c-168">The LANGUAGE value must be present in the sys.languages view.</span></span>

### <a name="how-to-migrate-a-stored-procedure"></a><span data-ttu-id="6296c-169">How to migrate a stored procedure</span><span class="sxs-lookup"><span data-stu-id="6296c-169">How to migrate a stored procedure</span></span>
<span data-ttu-id="6296c-170">The migration steps are:</span><span class="sxs-lookup"><span data-stu-id="6296c-170">The migration steps are:</span></span>

1. <span data-ttu-id="6296c-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6296c-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="6296c-172">Rewrite its header to match the previous template.</span><span class="sxs-lookup"><span data-stu-id="6296c-172">Rewrite its header to match the previous template.</span></span>
3. <span data-ttu-id="6296c-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span><span class="sxs-lookup"><span data-stu-id="6296c-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="6296c-174">Implement workarounds if necessary.</span><span class="sxs-lookup"><span data-stu-id="6296c-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="6296c-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="6296c-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="6296c-176">Rename the old stored procedure by using SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="6296c-176">Rename the old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="6296c-177">Or simply DROP it.</span><span class="sxs-lookup"><span data-stu-id="6296c-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="6296c-178">Run your edited CREATE PROCEDURE T-SQL script.</span><span class="sxs-lookup"><span data-stu-id="6296c-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="6296c-179">Step 6: Run your workload in test</span><span class="sxs-lookup"><span data-stu-id="6296c-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="6296c-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span><span class="sxs-lookup"><span data-stu-id="6296c-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span></span> <span data-ttu-id="6296c-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span><span class="sxs-lookup"><span data-stu-id="6296c-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="6296c-182">Major attributes of the workload are:</span><span class="sxs-lookup"><span data-stu-id="6296c-182">Major attributes of the workload are:</span></span>

* <span data-ttu-id="6296c-183">Number of concurrent connections.</span><span class="sxs-lookup"><span data-stu-id="6296c-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="6296c-184">Read/write ratio.</span><span class="sxs-lookup"><span data-stu-id="6296c-184">Read/write ratio.</span></span>

<span data-ttu-id="6296c-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="6296c-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="6296c-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span><span class="sxs-lookup"><span data-stu-id="6296c-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="6296c-187">Step 7: Post-implementation monitoring</span><span class="sxs-lookup"><span data-stu-id="6296c-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="6296c-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span><span class="sxs-lookup"><span data-stu-id="6296c-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="6296c-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="6296c-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="6296c-190">Monitoring Azure SQL Database using dynamic management views</span><span class="sxs-lookup"><span data-stu-id="6296c-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="6296c-191">Related links</span><span class="sxs-lookup"><span data-stu-id="6296c-191">Related links</span></span>
* [<span data-ttu-id="6296c-192">In-Memory OLTP (In-Memory Optimization)</span><span class="sxs-lookup"><span data-stu-id="6296c-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="6296c-193">Introduction to Natively Compiled Stored Procedures</span><span class="sxs-lookup"><span data-stu-id="6296c-193">Introduction to Natively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="6296c-194">Memory Optimization Advisor</span><span class="sxs-lookup"><span data-stu-id="6296c-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

