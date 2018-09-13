---
title: Using T-SQL views in Azure SQL Data Warehouse | Microsoft Docs
description: Tips for using T-SQL views in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: rortloff
ms.reviewer: igorstan
ms.openlocfilehash: 796a549c3a01c235422667dc63b729244b1917bf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44781123"
---
# <a name="views-in-azure-sql-data-warehouse"></a><span data-ttu-id="44b45-103">Views in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="44b45-103">Views in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="44b45-104">Tips for using T-SQL views in Azure SQL Data Warehouse for developing solutions.</span><span class="sxs-lookup"><span data-stu-id="44b45-104">Tips for using T-SQL views in Azure SQL Data Warehouse for developing solutions.</span></span> 

## <a name="why-use-views"></a><span data-ttu-id="44b45-105">Why use views?</span><span class="sxs-lookup"><span data-stu-id="44b45-105">Why use views?</span></span>
<span data-ttu-id="44b45-106">Views can be used in a number of different ways to improve the quality of your solution.</span><span class="sxs-lookup"><span data-stu-id="44b45-106">Views can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="44b45-107">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span><span class="sxs-lookup"><span data-stu-id="44b45-107">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="44b45-108">Syntax for CREATE VIEW is not discussed in this article.</span><span class="sxs-lookup"><span data-stu-id="44b45-108">Syntax for CREATE VIEW is not discussed in this article.</span></span> <span data-ttu-id="44b45-109">For more information, see the [CREATE VIEW](/sql/t-sql/statements/create-view-transact-sql) documentation.</span><span class="sxs-lookup"><span data-stu-id="44b45-109">For more information, see the [CREATE VIEW](/sql/t-sql/statements/create-view-transact-sql) documentation.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="44b45-110">Architectural abstraction</span><span class="sxs-lookup"><span data-stu-id="44b45-110">Architectural abstraction</span></span>
<span data-ttu-id="44b45-111">A common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span><span class="sxs-lookup"><span data-stu-id="44b45-111">A common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="44b45-112">The following example adds new date records to a date dimension.</span><span class="sxs-lookup"><span data-stu-id="44b45-112">The following example adds new date records to a date dimension.</span></span> <span data-ttu-id="44b45-113">Note how a new table, DimDate_New, is first created and then renamed to replace the original version of the table.</span><span class="sxs-lookup"><span data-stu-id="44b45-113">Note how a new table, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="44b45-114">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span><span class="sxs-lookup"><span data-stu-id="44b45-114">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="44b45-115">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span><span class="sxs-lookup"><span data-stu-id="44b45-115">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="44b45-116">By providing access to data through views, users do not need visibility to the underlying tables.</span><span class="sxs-lookup"><span data-stu-id="44b45-116">By providing access to data through views, users do not need visibility to the underlying tables.</span></span> <span data-ttu-id="44b45-117">This layer provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model.</span><span class="sxs-lookup"><span data-stu-id="44b45-117">This layer provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model.</span></span> <span data-ttu-id="44b45-118">Being able to evolve the underlying tables means designers can use CTAS to maximize performance during the data loading process.</span><span class="sxs-lookup"><span data-stu-id="44b45-118">Being able to evolve the underlying tables means designers can use CTAS to maximize performance during the data loading process.</span></span>   

## <a name="performance-optimization"></a><span data-ttu-id="44b45-119">Performance optimization</span><span class="sxs-lookup"><span data-stu-id="44b45-119">Performance optimization</span></span>
<span data-ttu-id="44b45-120">Views can also be utilized to enforce performance optimized joins between tables.</span><span class="sxs-lookup"><span data-stu-id="44b45-120">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="44b45-121">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span><span class="sxs-lookup"><span data-stu-id="44b45-121">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span> <span data-ttu-id="44b45-122">Another benefit of a view could be to force a specific query or joining hint.</span><span class="sxs-lookup"><span data-stu-id="44b45-122">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="44b45-123">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span><span class="sxs-lookup"><span data-stu-id="44b45-123">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="44b45-124">Limitations</span><span class="sxs-lookup"><span data-stu-id="44b45-124">Limitations</span></span>
<span data-ttu-id="44b45-125">Views in SQL Data Warehouse are stored as metadata only.</span><span class="sxs-lookup"><span data-stu-id="44b45-125">Views in SQL Data Warehouse are stored as metadata only.</span></span> <span data-ttu-id="44b45-126">Consequently, the following options are not available:</span><span class="sxs-lookup"><span data-stu-id="44b45-126">Consequently, the following options are not available:</span></span>

* <span data-ttu-id="44b45-127">There is no schema binding option</span><span class="sxs-lookup"><span data-stu-id="44b45-127">There is no schema binding option</span></span>
* <span data-ttu-id="44b45-128">Base tables cannot be updated through the view</span><span class="sxs-lookup"><span data-stu-id="44b45-128">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="44b45-129">Views cannot be created over temporary tables</span><span class="sxs-lookup"><span data-stu-id="44b45-129">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="44b45-130">There is no support for the EXPAND / NOEXPAND hints</span><span class="sxs-lookup"><span data-stu-id="44b45-130">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="44b45-131">There are no indexed views in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="44b45-131">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="44b45-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="44b45-132">Next steps</span></span>
<span data-ttu-id="44b45-133">For more development tips, see [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="44b45-133">For more development tips, see [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>


