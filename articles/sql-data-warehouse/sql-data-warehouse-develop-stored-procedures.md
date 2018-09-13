---
title: Using stored procedures in Azure SQL Data Warehouse | Microsoft Docs
description: Tips for implementing stored procedures in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
author: ckarst
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: cakarst
ms.reviewer: igorstan
ms.openlocfilehash: 4cd8394104c72e8df53fa0c44e60037b4dc05976
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44816067"
---
# <a name="using-stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="bd75a-103">Using stored procedures in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="bd75a-103">Using stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="bd75a-104">Tips for implementing stored procedures in Azure SQL Data Warehouse for developing solutions.</span><span class="sxs-lookup"><span data-stu-id="bd75a-104">Tips for implementing stored procedures in Azure SQL Data Warehouse for developing solutions.</span></span>

## <a name="what-to-expect"></a><span data-ttu-id="bd75a-105">What to expect</span><span class="sxs-lookup"><span data-stu-id="bd75a-105">What to expect</span></span>

<span data-ttu-id="bd75a-106">SQL Data Warehouse supports many of the T-SQL features that are used in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bd75a-106">SQL Data Warehouse supports many of the T-SQL features that are used in SQL Server.</span></span> <span data-ttu-id="bd75a-107">More importantly, there are scale-out specific features that you can use to maximize the performance of your solution.</span><span class="sxs-lookup"><span data-stu-id="bd75a-107">More importantly, there are scale-out specific features that you can use to maximize the performance of your solution.</span></span>

<span data-ttu-id="bd75a-108">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span><span class="sxs-lookup"><span data-stu-id="bd75a-108">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>


## <a name="introducing-stored-procedures"></a><span data-ttu-id="bd75a-109">Introducing stored procedures</span><span class="sxs-lookup"><span data-stu-id="bd75a-109">Introducing stored procedures</span></span>
<span data-ttu-id="bd75a-110">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span><span class="sxs-lookup"><span data-stu-id="bd75a-110">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span></span> <span data-ttu-id="bd75a-111">Stored procedures help developers modularize their solutions by encapsulating the code into manageable units; facilitating greater reusability of code.</span><span class="sxs-lookup"><span data-stu-id="bd75a-111">Stored procedures help developers modularize their solutions by encapsulating the code into manageable units; facilitating greater reusability of code.</span></span> <span data-ttu-id="bd75a-112">Each stored procedure can also accept parameters to make them even more flexible.</span><span class="sxs-lookup"><span data-stu-id="bd75a-112">Each stored procedure can also accept parameters to make them even more flexible.</span></span>

<span data-ttu-id="bd75a-113">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span><span class="sxs-lookup"><span data-stu-id="bd75a-113">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="bd75a-114">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span><span class="sxs-lookup"><span data-stu-id="bd75a-114">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="bd75a-115">In data warehouses, the compilation time is small in comparison to the time it takes to run queries against large data volumes.</span><span class="sxs-lookup"><span data-stu-id="bd75a-115">In data warehouses, the compilation time is small in comparison to the time it takes to run queries against large data volumes.</span></span> <span data-ttu-id="bd75a-116">It is more important to ensure the stored procedure code is correctly optimized for large queries.</span><span class="sxs-lookup"><span data-stu-id="bd75a-116">It is more important to ensure the stored procedure code is correctly optimized for large queries.</span></span> <span data-ttu-id="bd75a-117">The goal is to save hours, minutes, and seconds, not milliseconds.</span><span class="sxs-lookup"><span data-stu-id="bd75a-117">The goal is to save hours, minutes, and seconds, not milliseconds.</span></span> <span data-ttu-id="bd75a-118">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span><span class="sxs-lookup"><span data-stu-id="bd75a-118">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="bd75a-119">When SQL Data Warehouse executes your stored procedure, the SQL statements are parsed, translated, and optimized at run time.</span><span class="sxs-lookup"><span data-stu-id="bd75a-119">When SQL Data Warehouse executes your stored procedure, the SQL statements are parsed, translated, and optimized at run time.</span></span> <span data-ttu-id="bd75a-120">During this process, each statement is converted into distributed queries.</span><span class="sxs-lookup"><span data-stu-id="bd75a-120">During this process, each statement is converted into distributed queries.</span></span> <span data-ttu-id="bd75a-121">The SQL code that is executed against the data is different than the query submitted.</span><span class="sxs-lookup"><span data-stu-id="bd75a-121">The SQL code that is executed against the data is different than the query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="bd75a-122">Nesting stored procedures</span><span class="sxs-lookup"><span data-stu-id="bd75a-122">Nesting stored procedures</span></span>
<span data-ttu-id="bd75a-123">When stored procedures call other stored procedures, or execute dynamic SQL, then the inner stored procedure or code invocation is said to be nested.</span><span class="sxs-lookup"><span data-stu-id="bd75a-123">When stored procedures call other stored procedures, or execute dynamic SQL, then the inner stored procedure or code invocation is said to be nested.</span></span>

<span data-ttu-id="bd75a-124">SQL Data Warehouse supports a maximum of eight nesting levels.</span><span class="sxs-lookup"><span data-stu-id="bd75a-124">SQL Data Warehouse supports a maximum of eight nesting levels.</span></span> <span data-ttu-id="bd75a-125">This is slightly different to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bd75a-125">This is slightly different to SQL Server.</span></span> <span data-ttu-id="bd75a-126">The nest level in SQL Server is 32.</span><span class="sxs-lookup"><span data-stu-id="bd75a-126">The nest level in SQL Server is 32.</span></span>

<span data-ttu-id="bd75a-127">The top-level stored procedure call equates to nest level 1.</span><span class="sxs-lookup"><span data-stu-id="bd75a-127">The top-level stored procedure call equates to nest level 1.</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="bd75a-128">If the stored procedure also makes another EXEC call, the nest level increases to two.</span><span class="sxs-lookup"><span data-stu-id="bd75a-128">If the stored procedure also makes another EXEC call, the nest level increases to two.</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="bd75a-129">If the second procedure then executes some dynamic SQL, the nest level increases to three.</span><span class="sxs-lookup"><span data-stu-id="bd75a-129">If the second procedure then executes some dynamic SQL, the nest level increases to three.</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="bd75a-130">Note, SQL Data Warehouse does not currently support [@@NESTLEVEL](/sql/t-sql/functions/nestlevel-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="bd75a-130">Note, SQL Data Warehouse does not currently support [@@NESTLEVEL](/sql/t-sql/functions/nestlevel-transact-sql).</span></span> <span data-ttu-id="bd75a-131">You need to track the nest level.</span><span class="sxs-lookup"><span data-stu-id="bd75a-131">You need to track the nest level.</span></span> <span data-ttu-id="bd75a-132">It is unlikely for you to exceed the eight nest level limit, but if you do, you need to rework your code to fit the nesting levels within this limit.</span><span class="sxs-lookup"><span data-stu-id="bd75a-132">It is unlikely for you to exceed the eight nest level limit, but if you do, you need to rework your code to fit the nesting levels within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="bd75a-133">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="bd75a-133">INSERT..EXECUTE</span></span>
<span data-ttu-id="bd75a-134">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span><span class="sxs-lookup"><span data-stu-id="bd75a-134">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="bd75a-135">However, there is an alternative approach you can use.</span><span class="sxs-lookup"><span data-stu-id="bd75a-135">However, there is an alternative approach you can use.</span></span> <span data-ttu-id="bd75a-136">For an example, see the article on [temporary tables](sql-data-warehouse-tables-temporary.md).</span><span class="sxs-lookup"><span data-stu-id="bd75a-136">For an example, see the article on [temporary tables](sql-data-warehouse-tables-temporary.md).</span></span> 

## <a name="limitations"></a><span data-ttu-id="bd75a-137">Limitations</span><span class="sxs-lookup"><span data-stu-id="bd75a-137">Limitations</span></span>
<span data-ttu-id="bd75a-138">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="bd75a-138">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="bd75a-139">They are:</span><span class="sxs-lookup"><span data-stu-id="bd75a-139">They are:</span></span>

* <span data-ttu-id="bd75a-140">temporary stored procedures</span><span class="sxs-lookup"><span data-stu-id="bd75a-140">temporary stored procedures</span></span>
* <span data-ttu-id="bd75a-141">numbered stored procedures</span><span class="sxs-lookup"><span data-stu-id="bd75a-141">numbered stored procedures</span></span>
* <span data-ttu-id="bd75a-142">extended stored procedures</span><span class="sxs-lookup"><span data-stu-id="bd75a-142">extended stored procedures</span></span>
* <span data-ttu-id="bd75a-143">CLR stored procedures</span><span class="sxs-lookup"><span data-stu-id="bd75a-143">CLR stored procedures</span></span>
* <span data-ttu-id="bd75a-144">encryption option</span><span class="sxs-lookup"><span data-stu-id="bd75a-144">encryption option</span></span>
* <span data-ttu-id="bd75a-145">replication option</span><span class="sxs-lookup"><span data-stu-id="bd75a-145">replication option</span></span>
* <span data-ttu-id="bd75a-146">table-valued parameters</span><span class="sxs-lookup"><span data-stu-id="bd75a-146">table-valued parameters</span></span>
* <span data-ttu-id="bd75a-147">read-only parameters</span><span class="sxs-lookup"><span data-stu-id="bd75a-147">read-only parameters</span></span>
* <span data-ttu-id="bd75a-148">default parameters</span><span class="sxs-lookup"><span data-stu-id="bd75a-148">default parameters</span></span>
* <span data-ttu-id="bd75a-149">execution contexts</span><span class="sxs-lookup"><span data-stu-id="bd75a-149">execution contexts</span></span>
* <span data-ttu-id="bd75a-150">return statement</span><span class="sxs-lookup"><span data-stu-id="bd75a-150">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd75a-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="bd75a-151">Next steps</span></span>
<span data-ttu-id="bd75a-152">For more development tips, see [development overview](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="bd75a-152">For more development tips, see [development overview](sql-data-warehouse-overview-develop.md).</span></span>

