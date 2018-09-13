---
title: Leverage T-SQL loops in Azure SQL Data Warehouse | Microsoft Docs
description: Tips for Transact-SQL loops and replacing cursors in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 40a872ff310f48bfd543ac184fe7301b85b50258
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555233"
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="dd196-103">Loops in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dd196-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="dd196-104">SQL Data Warehouse supports the [WHILE][WHILE] loop for repeatedly executing statement blocks.</span><span class="sxs-lookup"><span data-stu-id="dd196-104">SQL Data Warehouse supports the [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="dd196-105">This will continue for as long as the specified conditions are true or until the code specifically terminates the loop using the `BREAK` keyword.</span><span class="sxs-lookup"><span data-stu-id="dd196-105">This will continue for as long as the specified conditions are true or until the code specifically terminates the loop using the `BREAK` keyword.</span></span> <span data-ttu-id="dd196-106">Loops are particularly useful for replacing cursors defined in SQL code.</span><span class="sxs-lookup"><span data-stu-id="dd196-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="dd196-107">Fortunately, almost all cursors that are written in SQL code are of the fast forward, read only variety.</span><span class="sxs-lookup"><span data-stu-id="dd196-107">Fortunately, almost all cursors that are written in SQL code are of the fast forward, read only variety.</span></span> <span data-ttu-id="dd196-108">Therefore [WHILE] loops are a great alternative if you find yourself having to replace one.</span><span class="sxs-lookup"><span data-stu-id="dd196-108">Therefore [WHILE] loops are a great alternative if you find yourself having to replace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="dd196-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="dd196-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="dd196-110">However, before diving in head first you should ask yourself the following question: "Could this cursor be re-written to use set based operations?".</span><span class="sxs-lookup"><span data-stu-id="dd196-110">However, before diving in head first you should ask yourself the following question: "Could this cursor be re-written to use set based operations?".</span></span> <span data-ttu-id="dd196-111">In many cases the answer will be yes and is often the best approach.</span><span class="sxs-lookup"><span data-stu-id="dd196-111">In many cases the answer will be yes and is often the best approach.</span></span> <span data-ttu-id="dd196-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span><span class="sxs-lookup"><span data-stu-id="dd196-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="dd196-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span><span class="sxs-lookup"><span data-stu-id="dd196-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="dd196-114">Below is a simple example.</span><span class="sxs-lookup"><span data-stu-id="dd196-114">Below is a simple example.</span></span> <span data-ttu-id="dd196-115">This code example updates the statistics for every table in the database.</span><span class="sxs-lookup"><span data-stu-id="dd196-115">This code example updates the statistics for every table in the database.</span></span> <span data-ttu-id="dd196-116">By iterating over the tables in the loop we are able to execute each command in sequence.</span><span class="sxs-lookup"><span data-stu-id="dd196-116">By iterating over the tables in the loop we are able to execute each command in sequence.</span></span>

<span data-ttu-id="dd196-117">First, create a temporary table containing a unique row number used to identify the individual statements:</span><span class="sxs-lookup"><span data-stu-id="dd196-117">First, create a temporary table containing a unique row number used to identify the individual statements:</span></span>

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

<span data-ttu-id="dd196-118">Second, initialize the variables required to perform the loop:</span><span class="sxs-lookup"><span data-stu-id="dd196-118">Second, initialize the variables required to perform the loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="dd196-119">Now loop over statements executing them one at a time:</span><span class="sxs-lookup"><span data-stu-id="dd196-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="dd196-120">Finally drop the temporary table created in the first step</span><span class="sxs-lookup"><span data-stu-id="dd196-120">Finally drop the temporary table created in the first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="dd196-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd196-121">Next steps</span></span>
<span data-ttu-id="dd196-122">For more development tips, see [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="dd196-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
