---
title: Defining data types - Azure SQL Data Warehouse | Microsoft Docs
description: Recommendations for defining table data types in Azure SQL Data Warehouse.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: rortloff
ms.reviewer: igorstan
ms.openlocfilehash: eb469e6a654414b0411f8c45b73658f99a383751
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819174"
---
# <a name="table-data-types-in-azure-sql-data-warehouse"></a><span data-ttu-id="c3276-103">Table data types in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c3276-103">Table data types in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="c3276-104">Recommendations for defining table data types in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3276-104">Recommendations for defining table data types in Azure SQL Data Warehouse.</span></span> 

## <a name="what-are-the-data-types"></a><span data-ttu-id="c3276-105">What are the data types?</span><span class="sxs-lookup"><span data-stu-id="c3276-105">What are the data types?</span></span>

<span data-ttu-id="c3276-106">SQL Data Warehouse supports the most commonly used data types.</span><span class="sxs-lookup"><span data-stu-id="c3276-106">SQL Data Warehouse supports the most commonly used data types.</span></span> <span data-ttu-id="c3276-107">For a list of the supported data types, see [data types](/sql/t-sql/statements/create-table-azure-sql-data-warehouse#DataTypes) in the CREATE TABLE statement.</span><span class="sxs-lookup"><span data-stu-id="c3276-107">For a list of the supported data types, see [data types](/sql/t-sql/statements/create-table-azure-sql-data-warehouse#DataTypes) in the CREATE TABLE statement.</span></span> 

## <a name="minimize-row-length"></a><span data-ttu-id="c3276-108">Minimize row length</span><span class="sxs-lookup"><span data-stu-id="c3276-108">Minimize row length</span></span>
<span data-ttu-id="c3276-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span><span class="sxs-lookup"><span data-stu-id="c3276-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span></span> <span data-ttu-id="c3276-110">Use the smallest data type that works for your data.</span><span class="sxs-lookup"><span data-stu-id="c3276-110">Use the smallest data type that works for your data.</span></span> 

- <span data-ttu-id="c3276-111">Avoid defining character columns with a large default length.</span><span class="sxs-lookup"><span data-stu-id="c3276-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="c3276-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="c3276-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="c3276-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="c3276-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="c3276-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="c3276-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="c3276-115">If you are using PolyBase external tables to load your tables, the defined length of the table row cannot exceed 1 MB.</span><span class="sxs-lookup"><span data-stu-id="c3276-115">If you are using PolyBase external tables to load your tables, the defined length of the table row cannot exceed 1 MB.</span></span> <span data-ttu-id="c3276-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span><span class="sxs-lookup"><span data-stu-id="c3276-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="c3276-117">Identify unsupported data types</span><span class="sxs-lookup"><span data-stu-id="c3276-117">Identify unsupported data types</span></span>
<span data-ttu-id="c3276-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c3276-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="c3276-119">Use this query to discover unsupported data types in your existing SQL schema.</span><span class="sxs-lookup"><span data-stu-id="c3276-119">Use this query to discover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','xml')
 AND  y.[is_user_defined] = 1;
```


## <a name="unsupported-data-types"></a><span data-ttu-id="c3276-120">Workarounds for unsupported data types</span><span class="sxs-lookup"><span data-stu-id="c3276-120">Workarounds for unsupported data types</span></span>

<span data-ttu-id="c3276-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span><span class="sxs-lookup"><span data-stu-id="c3276-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span></span>

| <span data-ttu-id="c3276-122">Unsupported data type</span><span class="sxs-lookup"><span data-stu-id="c3276-122">Unsupported data type</span></span> | <span data-ttu-id="c3276-123">Workaround</span><span class="sxs-lookup"><span data-stu-id="c3276-123">Workaround</span></span> |
| --- | --- |
| [<span data-ttu-id="c3276-124">geometry</span><span class="sxs-lookup"><span data-stu-id="c3276-124">geometry</span></span>](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql) |[<span data-ttu-id="c3276-125">varbinary</span><span class="sxs-lookup"><span data-stu-id="c3276-125">varbinary</span></span>](/sql/t-sql/data-types/binary-and-varbinary-transact-sql) |
| [<span data-ttu-id="c3276-126">geography</span><span class="sxs-lookup"><span data-stu-id="c3276-126">geography</span></span>](/sql/t-sql/spatial-geography/spatial-types-geography) |[<span data-ttu-id="c3276-127">varbinary</span><span class="sxs-lookup"><span data-stu-id="c3276-127">varbinary</span></span>](/sql/t-sql/data-types/binary-and-varbinary-transact-sql) |
| [<span data-ttu-id="c3276-128">hierarchyid</span><span class="sxs-lookup"><span data-stu-id="c3276-128">hierarchyid</span></span>](/sql/t-sql/data-types/hierarchyid-data-type-method-reference) |<span data-ttu-id="c3276-129">[nvarchar](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)(4000)</span><span class="sxs-lookup"><span data-stu-id="c3276-129">[nvarchar](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)(4000)</span></span> |
| [<span data-ttu-id="c3276-130">image</span><span class="sxs-lookup"><span data-stu-id="c3276-130">image</span></span>](/sql/t-sql/data-types/ntext-text-and-image-transact-sql) |[<span data-ttu-id="c3276-131">varbinary</span><span class="sxs-lookup"><span data-stu-id="c3276-131">varbinary</span></span>](/sql/t-sql/data-types/binary-and-varbinary-transact-sql) |
| [<span data-ttu-id="c3276-132">text</span><span class="sxs-lookup"><span data-stu-id="c3276-132">text</span></span>](/sql/t-sql/data-types/ntext-text-and-image-transact-sql) |[<span data-ttu-id="c3276-133">varchar</span><span class="sxs-lookup"><span data-stu-id="c3276-133">varchar</span></span>](/sql/t-sql/data-types/char-and-varchar-transact-sql) |
| [<span data-ttu-id="c3276-134">ntext</span><span class="sxs-lookup"><span data-stu-id="c3276-134">ntext</span></span>](/sql/t-sql/data-types/ntext-text-and-image-transact-sql) |[<span data-ttu-id="c3276-135">nvarchar</span><span class="sxs-lookup"><span data-stu-id="c3276-135">nvarchar</span></span>](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql) |
| [<span data-ttu-id="c3276-136">sql_variant</span><span class="sxs-lookup"><span data-stu-id="c3276-136">sql_variant</span></span>](/sql/t-sql/data-types/sql-variant-transact-sql) |<span data-ttu-id="c3276-137">Split column into several strongly typed columns.</span><span class="sxs-lookup"><span data-stu-id="c3276-137">Split column into several strongly typed columns.</span></span> |
| [<span data-ttu-id="c3276-138">table</span><span class="sxs-lookup"><span data-stu-id="c3276-138">table</span></span>](/sql/t-sql/data-types/table-transact-sql) |<span data-ttu-id="c3276-139">Convert to temporary tables.</span><span class="sxs-lookup"><span data-stu-id="c3276-139">Convert to temporary tables.</span></span> |
| [<span data-ttu-id="c3276-140">timestamp</span><span class="sxs-lookup"><span data-stu-id="c3276-140">timestamp</span></span>](/sql/t-sql/data-types/date-and-time-types) |<span data-ttu-id="c3276-141">Rework code to use [datetime2](/sql/t-sql/data-types/datetime2-transact-sql) and the [CURRENT_TIMESTAMP](/sql/t-sql/functions/current-timestamp-transact-sql) function.</span><span class="sxs-lookup"><span data-stu-id="c3276-141">Rework code to use [datetime2](/sql/t-sql/data-types/datetime2-transact-sql) and the [CURRENT_TIMESTAMP](/sql/t-sql/functions/current-timestamp-transact-sql) function.</span></span> <span data-ttu-id="c3276-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span><span class="sxs-lookup"><span data-stu-id="c3276-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="c3276-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)(8) or [VARBINARY](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)(8) for NOT NULL or NULL row version values.</span><span class="sxs-lookup"><span data-stu-id="c3276-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)(8) or [VARBINARY](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)(8) for NOT NULL or NULL row version values.</span></span> |
| [<span data-ttu-id="c3276-144">xml</span><span class="sxs-lookup"><span data-stu-id="c3276-144">xml</span></span>](/sql/t-sql/xml/xml-transact-sql) |[<span data-ttu-id="c3276-145">varchar</span><span class="sxs-lookup"><span data-stu-id="c3276-145">varchar</span></span>](/sql/t-sql/data-types/char-and-varchar-transact-sql) |
| [<span data-ttu-id="c3276-146">user-defined type</span><span class="sxs-lookup"><span data-stu-id="c3276-146">user-defined type</span></span>](/sql/relational-databases/native-client/features/using-user-defined-types) |<span data-ttu-id="c3276-147">Convert back to the native data type when possible.</span><span class="sxs-lookup"><span data-stu-id="c3276-147">Convert back to the native data type when possible.</span></span> |
| <span data-ttu-id="c3276-148">default values</span><span class="sxs-lookup"><span data-stu-id="c3276-148">default values</span></span> | <span data-ttu-id="c3276-149">Default values support literals and constants only.</span><span class="sxs-lookup"><span data-stu-id="c3276-149">Default values support literals and constants only.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c3276-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3276-150">Next steps</span></span>
<span data-ttu-id="c3276-151">For more information on developing tables, see [Table Overview](sql-data-warehouse-tables-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3276-151">For more information on developing tables, see [Table Overview](sql-data-warehouse-tables-overview.md).</span></span>
