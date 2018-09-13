---
title: Resources for developing a data warehouse in Azure | Microsoft Docs
description: Development concepts, design decisions, recommendations and coding techniques for SQL Data Warehouse.
services: sql-data-warehouse
author: kevinvngo
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 08/29/2018
ms.author: kevinvngo
ms.reviewer: igorstan
ms.openlocfilehash: 5cb3b3b261bcb762187b165e297225080b0fee81
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779368"
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="3c4ef-103">Design decisions and coding techniques for SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3c4ef-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="3c4ef-104">Take a look through these development articles to better understand key design decisions, recommendations, and coding techniques for SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3c4ef-104">Take a look through these development articles to better understand key design decisions, recommendations, and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="3c4ef-105">Key design decisions</span><span class="sxs-lookup"><span data-stu-id="3c4ef-105">Key design decisions</span></span>
<span data-ttu-id="3c4ef-106">The following articles highlight concepts and design decisions for developing a distributed data warehouse using SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="3c4ef-106">The following articles highlight concepts and design decisions for developing a distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="3c4ef-107">[connections][connections]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-107">[connections][connections]</span></span>
* <span data-ttu-id="3c4ef-108">[concurrency][concurrency]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="3c4ef-109">[transactions][transactions]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-109">[transactions][transactions]</span></span>
* <span data-ttu-id="3c4ef-110">[user-defined schemas][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="3c4ef-111">[table distribution][table distribution]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="3c4ef-112">[table indexes][table indexes]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="3c4ef-113">[table partitions][table partitions]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="3c4ef-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="3c4ef-115">[statistics][statistics]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="3c4ef-116">Development recommendations and coding techniques</span><span class="sxs-lookup"><span data-stu-id="3c4ef-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="3c4ef-117">These articles highlight specific coding techniques, tips, and recommendations for developing your SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="3c4ef-117">These articles highlight specific coding techniques, tips, and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="3c4ef-118">[stored procedures][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="3c4ef-119">[labels][labels]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-119">[labels][labels]</span></span>
* <span data-ttu-id="3c4ef-120">[views][views]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-120">[views][views]</span></span>
* <span data-ttu-id="3c4ef-121">[temporary tables][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="3c4ef-122">[dynamic SQL][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="3c4ef-123">[looping][looping]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-123">[looping][looping]</span></span>
* <span data-ttu-id="3c4ef-124">[group by options][group by options]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-124">[group by options][group by options]</span></span>
* <span data-ttu-id="3c4ef-125">[variable assignment][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="3c4ef-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c4ef-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c4ef-126">Next steps</span></span>
<span data-ttu-id="3c4ef-127">For more reference information, see [SQL Data Warehouse T-SQL statements](sql-data-warehouse-reference-tsql-statements.md).</span><span class="sxs-lookup"><span data-stu-id="3c4ef-127">For more reference information, see [SQL Data Warehouse T-SQL statements](sql-data-warehouse-reference-tsql-statements.md).</span></span>

<!--Image references-->

<!--Article references-->
[concurrency]: ./resource-classes-for-workload-management.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md


<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
