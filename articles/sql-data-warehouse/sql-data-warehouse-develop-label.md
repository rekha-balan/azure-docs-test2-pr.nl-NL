---
title: Use labels to instrument queries in SQL Data Warehouse | Microsoft Docs
description: Tips for using labels to instrument queries in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555322"
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="1725c-103">Use labels to instrument queries in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1725c-103">Use labels to instrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="1725c-104">SQL Data Warehouse supports a concept called query labels.</span><span class="sxs-lookup"><span data-stu-id="1725c-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="1725c-105">Before going into any depth let's look at an example of one:</span><span class="sxs-lookup"><span data-stu-id="1725c-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="1725c-106">This last line tags the string 'My Query Label' to the query.</span><span class="sxs-lookup"><span data-stu-id="1725c-106">This last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="1725c-107">This is particularly helpful as the label is query-able through the DMVs.</span><span class="sxs-lookup"><span data-stu-id="1725c-107">This is particularly helpful as the label is query-able through the DMVs.</span></span> <span data-ttu-id="1725c-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span><span class="sxs-lookup"><span data-stu-id="1725c-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span></span>

<span data-ttu-id="1725c-109">A good naming convention really helps here.</span><span class="sxs-lookup"><span data-stu-id="1725c-109">A good naming convention really helps here.</span></span> <span data-ttu-id="1725c-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span><span class="sxs-lookup"><span data-stu-id="1725c-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span></span>

<span data-ttu-id="1725c-111">To search by label you can use the following query that uses the dynamic management views:</span><span class="sxs-lookup"><span data-stu-id="1725c-111">To search by label you can use the following query that uses the dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="1725c-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span><span class="sxs-lookup"><span data-stu-id="1725c-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="1725c-113">Label is a reserved word and will caused an error if it has not been delimited.</span><span class="sxs-lookup"><span data-stu-id="1725c-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1725c-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="1725c-114">Next steps</span></span>
<span data-ttu-id="1725c-115">For more development tips, see [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="1725c-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
