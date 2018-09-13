---
title: Stored procedures in SQL Data Warehouse | Microsoft Docs
description: Tips for implementing stored procedures in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: e42d80f0ca35f3fbb67389c66d072bc40d8a8d2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661542"
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="97ada-103">Stored procedures in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="97ada-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="97ada-104">SQL Data Warehouse supports many of the Transact-SQL features found in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="97ada-104">SQL Data Warehouse supports many of the Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="97ada-105">More importantly there are scale out specific features that we will want to leverage to maximize the performance of your solution.</span><span class="sxs-lookup"><span data-stu-id="97ada-105">More importantly there are scale out specific features that we will want to leverage to maximize the performance of your solution.</span></span>

<span data-ttu-id="97ada-106">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span><span class="sxs-lookup"><span data-stu-id="97ada-106">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="97ada-107">This article explains how to implement stored procedures within SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="97ada-107">This article explains how to implement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="97ada-108">Introducing stored procedures</span><span class="sxs-lookup"><span data-stu-id="97ada-108">Introducing stored procedures</span></span>
<span data-ttu-id="97ada-109">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span><span class="sxs-lookup"><span data-stu-id="97ada-109">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span></span> <span data-ttu-id="97ada-110">By encapsulating the code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span><span class="sxs-lookup"><span data-stu-id="97ada-110">By encapsulating the code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="97ada-111">Each stored procedure can also accept parameters to make them even more flexible.</span><span class="sxs-lookup"><span data-stu-id="97ada-111">Each stored procedure can also accept parameters to make them even more flexible.</span></span>

<span data-ttu-id="97ada-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span><span class="sxs-lookup"><span data-stu-id="97ada-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="97ada-113">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span><span class="sxs-lookup"><span data-stu-id="97ada-113">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="97ada-114">In data warehouses we are generally less concerned with the compilation time.</span><span class="sxs-lookup"><span data-stu-id="97ada-114">In data warehouses we are generally less concerned with the compilation time.</span></span> <span data-ttu-id="97ada-115">It is more important that the stored procedure code is correctly optimised when operating against large data volumes.</span><span class="sxs-lookup"><span data-stu-id="97ada-115">It is more important that the stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="97ada-116">The goal is to save hours, minutes and seconds not milliseconds.</span><span class="sxs-lookup"><span data-stu-id="97ada-116">The goal is to save hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="97ada-117">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span><span class="sxs-lookup"><span data-stu-id="97ada-117">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="97ada-118">When SQL Data Warehouse executes your stored procedure the SQL statements are parsed, translated and optimized at run time.</span><span class="sxs-lookup"><span data-stu-id="97ada-118">When SQL Data Warehouse executes your stored procedure the SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="97ada-119">During this process each statement is converted into distributed queries.</span><span class="sxs-lookup"><span data-stu-id="97ada-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="97ada-120">The SQL code that is actually executed against the data is different to the query submitted.</span><span class="sxs-lookup"><span data-stu-id="97ada-120">The SQL code that is actually executed against the data is different to the query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="97ada-121">Nesting stored procedures</span><span class="sxs-lookup"><span data-stu-id="97ada-121">Nesting stored procedures</span></span>
<span data-ttu-id="97ada-122">When stored procedures call other stored procedures or execute dynamic sql then the inner stored procedure or code invocation is said to be nested.</span><span class="sxs-lookup"><span data-stu-id="97ada-122">When stored procedures call other stored procedures or execute dynamic sql then the inner stored procedure or code invocation is said to be nested.</span></span>

<span data-ttu-id="97ada-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span><span class="sxs-lookup"><span data-stu-id="97ada-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="97ada-124">This is slightly different to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="97ada-124">This is slightly different to SQL Server.</span></span> <span data-ttu-id="97ada-125">The nest level in SQL Server is 32.</span><span class="sxs-lookup"><span data-stu-id="97ada-125">The nest level in SQL Server is 32.</span></span>

<span data-ttu-id="97ada-126">The top level stored procedure call equates to nest level 1</span><span class="sxs-lookup"><span data-stu-id="97ada-126">The top level stored procedure call equates to nest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="97ada-127">If the stored procedure also makes another EXEC call then this will increase the nest level to 2</span><span class="sxs-lookup"><span data-stu-id="97ada-127">If the stored procedure also makes another EXEC call then this will increase the nest level to 2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="97ada-128">If the second procedure then executes some dynamic sql then this will increase the nest level to 3</span><span class="sxs-lookup"><span data-stu-id="97ada-128">If the second procedure then executes some dynamic sql then this will increase the nest level to 3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="97ada-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="97ada-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="97ada-130">You will need to keep a track of your nest level yourself.</span><span class="sxs-lookup"><span data-stu-id="97ada-130">You will need to keep a track of your nest level yourself.</span></span> <span data-ttu-id="97ada-131">It is unlikely you will hit the 8 nest level limit but if you do you will need to re-work your code and "flatten" it so that it fits within this limit.</span><span class="sxs-lookup"><span data-stu-id="97ada-131">It is unlikely you will hit the 8 nest level limit but if you do you will need to re-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="97ada-132">INSERT..EXECUTE</span><span class="sxs-lookup"><span data-stu-id="97ada-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="97ada-133">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span><span class="sxs-lookup"><span data-stu-id="97ada-133">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="97ada-134">However, there is an alternative approach you can use.</span><span class="sxs-lookup"><span data-stu-id="97ada-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="97ada-135">Please refer to the following article on [temporary tables] for an example on how to do this.</span><span class="sxs-lookup"><span data-stu-id="97ada-135">Please refer to the following article on [temporary tables] for an example on how to do this.</span></span>

## <a name="limitations"></a><span data-ttu-id="97ada-136">Limitations</span><span class="sxs-lookup"><span data-stu-id="97ada-136">Limitations</span></span>
<span data-ttu-id="97ada-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="97ada-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="97ada-138">They are:</span><span class="sxs-lookup"><span data-stu-id="97ada-138">They are:</span></span>

* <span data-ttu-id="97ada-139">temporary stored procedures</span><span class="sxs-lookup"><span data-stu-id="97ada-139">temporary stored procedures</span></span>
* <span data-ttu-id="97ada-140">numbered stored procedures</span><span class="sxs-lookup"><span data-stu-id="97ada-140">numbered stored procedures</span></span>
* <span data-ttu-id="97ada-141">extended stored procedures</span><span class="sxs-lookup"><span data-stu-id="97ada-141">extended stored procedures</span></span>
* <span data-ttu-id="97ada-142">CLR stored procedures</span><span class="sxs-lookup"><span data-stu-id="97ada-142">CLR stored procedures</span></span>
* <span data-ttu-id="97ada-143">encryption option</span><span class="sxs-lookup"><span data-stu-id="97ada-143">encryption option</span></span>
* <span data-ttu-id="97ada-144">replication option</span><span class="sxs-lookup"><span data-stu-id="97ada-144">replication option</span></span>
* <span data-ttu-id="97ada-145">table-valued parameters</span><span class="sxs-lookup"><span data-stu-id="97ada-145">table-valued parameters</span></span>
* <span data-ttu-id="97ada-146">read-only parameters</span><span class="sxs-lookup"><span data-stu-id="97ada-146">read-only parameters</span></span>
* <span data-ttu-id="97ada-147">default parameters</span><span class="sxs-lookup"><span data-stu-id="97ada-147">default parameters</span></span>
* <span data-ttu-id="97ada-148">execution contexts</span><span class="sxs-lookup"><span data-stu-id="97ada-148">execution contexts</span></span>
* <span data-ttu-id="97ada-149">return statement</span><span class="sxs-lookup"><span data-stu-id="97ada-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="97ada-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="97ada-150">Next steps</span></span>
<span data-ttu-id="97ada-151">For more development tips, see [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="97ada-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[temporary tables]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
