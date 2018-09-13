---
title: Using labels to instrument queries in SQL Data Warehouse | Microsoft Docs
description: Tips for using labels to instrument queries in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: rortloff
ms.reviewer: igorstan
ms.openlocfilehash: 959fddfd24041a245f80b048eca4bef3cd612905
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44827294"
---
# <a name="using-labels-to-instrument-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="81654-103">Using labels to instrument queries in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="81654-103">Using labels to instrument queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="81654-104">Tips for using labels to instrument queries in Azure SQL Data Warehouse for developing solutions.</span><span class="sxs-lookup"><span data-stu-id="81654-104">Tips for using labels to instrument queries in Azure SQL Data Warehouse for developing solutions.</span></span>


## <a name="what-are-labels"></a><span data-ttu-id="81654-105">What are labels?</span><span class="sxs-lookup"><span data-stu-id="81654-105">What are labels?</span></span>
<span data-ttu-id="81654-106">SQL Data Warehouse supports a concept called query labels.</span><span class="sxs-lookup"><span data-stu-id="81654-106">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="81654-107">Before going into any depth, let's look at an example:</span><span class="sxs-lookup"><span data-stu-id="81654-107">Before going into any depth, let's look at an example:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="81654-108">The last line tags the string 'My Query Label' to the query.</span><span class="sxs-lookup"><span data-stu-id="81654-108">The last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="81654-109">This tag is particularly helpful since the label is query-able through the DMVs.</span><span class="sxs-lookup"><span data-stu-id="81654-109">This tag is particularly helpful since the label is query-able through the DMVs.</span></span> <span data-ttu-id="81654-110">Querying for labels provides a mechanism for locating problem queries and helping to identify progress through an ELT run.</span><span class="sxs-lookup"><span data-stu-id="81654-110">Querying for labels provides a mechanism for locating problem queries and helping to identify progress through an ELT run.</span></span>

<span data-ttu-id="81654-111">A good naming convention really helps.</span><span class="sxs-lookup"><span data-stu-id="81654-111">A good naming convention really helps.</span></span> <span data-ttu-id="81654-112">For example, starting the label with PROJECT, PROCEDURE, STATEMENT, or COMMENT helps to uniquely identify the query among all the code in source control.</span><span class="sxs-lookup"><span data-stu-id="81654-112">For example, starting the label with PROJECT, PROCEDURE, STATEMENT, or COMMENT helps to uniquely identify the query among all the code in source control.</span></span>

<span data-ttu-id="81654-113">The following query uses a dynamic management view to search by label.</span><span class="sxs-lookup"><span data-stu-id="81654-113">The following query uses a dynamic management view to search by label.</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="81654-114">It is essential to put square brackets or double quotes around the word label when querying.</span><span class="sxs-lookup"><span data-stu-id="81654-114">It is essential to put square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="81654-115">Label is a reserved word and causes an error when it is not delimited.</span><span class="sxs-lookup"><span data-stu-id="81654-115">Label is a reserved word and causes an error when it is not delimited.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="81654-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="81654-116">Next steps</span></span>
<span data-ttu-id="81654-117">For more development tips, see [development overview](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="81654-117">For more development tips, see [development overview](sql-data-warehouse-overview-develop.md).</span></span>


