---
title: Migrate your schema to SQL Data Warehouse | Microsoft Docs
description: Tips for migrating your schema to Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
author: jrowlandjones
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: jrj
ms.reviewer: igorstan
ms.openlocfilehash: 51ad7eed0bf37194b1e5ff2c605b39246e9a1191
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44778861"
---
# <a name="migrate-your-schemas-to-sql-data-warehouse"></a><span data-ttu-id="f3257-103">Migrate your schemas to SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f3257-103">Migrate your schemas to SQL Data Warehouse</span></span>
<span data-ttu-id="f3257-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f3257-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="f3257-105">Plan your schema migration</span><span class="sxs-lookup"><span data-stu-id="f3257-105">Plan your schema migration</span></span>

<span data-ttu-id="f3257-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span><span class="sxs-lookup"><span data-stu-id="f3257-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="f3257-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span><span class="sxs-lookup"><span data-stu-id="f3257-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-to-consolidate-databases"></a><span data-ttu-id="f3257-108">Use user-defined schemas to consolidate databases</span><span class="sxs-lookup"><span data-stu-id="f3257-108">Use user-defined schemas to consolidate databases</span></span>

<span data-ttu-id="f3257-109">Your existing workload probably has more than one database.</span><span class="sxs-lookup"><span data-stu-id="f3257-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="f3257-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span><span class="sxs-lookup"><span data-stu-id="f3257-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="f3257-111">In this topology, each database runs as a separate workload with separate security policies.</span><span class="sxs-lookup"><span data-stu-id="f3257-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="f3257-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span><span class="sxs-lookup"><span data-stu-id="f3257-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="f3257-113">Cross database joins are not permitted.</span><span class="sxs-lookup"><span data-stu-id="f3257-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="f3257-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span><span class="sxs-lookup"><span data-stu-id="f3257-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span></span>

<span data-ttu-id="f3257-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span><span class="sxs-lookup"><span data-stu-id="f3257-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span></span> <span data-ttu-id="f3257-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="f3257-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="f3257-117">Use compatible data types</span><span class="sxs-lookup"><span data-stu-id="f3257-117">Use compatible data types</span></span>
<span data-ttu-id="f3257-118">Modify your data types to be compatible with SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f3257-118">Modify your data types to be compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="f3257-119">For a list of supported and unsupported data types, see [data types][data types].</span><span class="sxs-lookup"><span data-stu-id="f3257-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="f3257-120">That topic gives workarounds for the unsupported types.</span><span class="sxs-lookup"><span data-stu-id="f3257-120">That topic gives workarounds for the unsupported types.</span></span> <span data-ttu-id="f3257-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f3257-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="f3257-122">Minimize row size</span><span class="sxs-lookup"><span data-stu-id="f3257-122">Minimize row size</span></span>
<span data-ttu-id="f3257-123">For best performance, minimize the row length of your tables.</span><span class="sxs-lookup"><span data-stu-id="f3257-123">For best performance, minimize the row length of your tables.</span></span> <span data-ttu-id="f3257-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span><span class="sxs-lookup"><span data-stu-id="f3257-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span></span> 

<span data-ttu-id="f3257-125">For table row width, PolyBase has a 1 MB limit.</span><span class="sxs-lookup"><span data-stu-id="f3257-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="f3257-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span><span class="sxs-lookup"><span data-stu-id="f3257-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but the largest possible size of the row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and the defined row width is less than one MB. When loading rows, PolyBase allocates the full length of the variable-length data. The full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-the-distribution-option"></a><span data-ttu-id="f3257-127">Specify the distribution option</span><span class="sxs-lookup"><span data-stu-id="f3257-127">Specify the distribution option</span></span>
<span data-ttu-id="f3257-128">SQL Data Warehouse is a distributed database system.</span><span class="sxs-lookup"><span data-stu-id="f3257-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="f3257-129">Each table is distributed or replicated across the Compute nodes.</span><span class="sxs-lookup"><span data-stu-id="f3257-129">Each table is distributed or replicated across the Compute nodes.</span></span> <span data-ttu-id="f3257-130">There's a table option that lets you specify how to distribute the data.</span><span class="sxs-lookup"><span data-stu-id="f3257-130">There's a table option that lets you specify how to distribute the data.</span></span> <span data-ttu-id="f3257-131">The choices are  round-robin, replicated, or hash distributed.</span><span class="sxs-lookup"><span data-stu-id="f3257-131">The choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="f3257-132">Each has pros and cons.</span><span class="sxs-lookup"><span data-stu-id="f3257-132">Each has pros and cons.</span></span> <span data-ttu-id="f3257-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span><span class="sxs-lookup"><span data-stu-id="f3257-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span></span>

- <span data-ttu-id="f3257-134">Round-robin is the default.</span><span class="sxs-lookup"><span data-stu-id="f3257-134">Round-robin is the default.</span></span> <span data-ttu-id="f3257-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span><span class="sxs-lookup"><span data-stu-id="f3257-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="f3257-136">Replicated stores a copy of the table on each Compute node.</span><span class="sxs-lookup"><span data-stu-id="f3257-136">Replicated stores a copy of the table on each Compute node.</span></span> <span data-ttu-id="f3257-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span><span class="sxs-lookup"><span data-stu-id="f3257-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="f3257-138">They do require extra storage, and therefore work best for smaller tables.</span><span class="sxs-lookup"><span data-stu-id="f3257-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="f3257-139">Hash distributed distributes the rows across all the nodes via a hash function.</span><span class="sxs-lookup"><span data-stu-id="f3257-139">Hash distributed distributes the rows across all the nodes via a hash function.</span></span> <span data-ttu-id="f3257-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span><span class="sxs-lookup"><span data-stu-id="f3257-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span></span> <span data-ttu-id="f3257-141">This option requires some planning to select the best column on which to distribute the data.</span><span class="sxs-lookup"><span data-stu-id="f3257-141">This option requires some planning to select the best column on which to distribute the data.</span></span> <span data-ttu-id="f3257-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span><span class="sxs-lookup"><span data-stu-id="f3257-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span></span> 

<span data-ttu-id="f3257-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="f3257-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="f3257-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3257-144">Next steps</span></span>
<span data-ttu-id="f3257-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span><span class="sxs-lookup"><span data-stu-id="f3257-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="f3257-146">[Migrate your data][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="f3257-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="f3257-147">[Migrate your code][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="f3257-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="f3257-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span><span class="sxs-lookup"><span data-stu-id="f3257-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
