---
title: Assign variables in SQL Data Warehouse | Microsoft Docs
description: Tips for assigning Transact-SQL variables in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 045d5148cd3f12dac63c961ccf7c953d355ed725
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550384"
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="c7d89-103">Assign variables in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c7d89-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="c7d89-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span><span class="sxs-lookup"><span data-stu-id="c7d89-104">Variables in SQL Data Warehouse are set using the `DECLARE` statement or the `SET` statement.</span></span>

<span data-ttu-id="c7d89-105">All of the following are perfectly valid ways to set a variable value:</span><span class="sxs-lookup"><span data-stu-id="c7d89-105">All of the following are perfectly valid ways to set a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="c7d89-106">Setting variables with DECLARE</span><span class="sxs-lookup"><span data-stu-id="c7d89-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="c7d89-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c7d89-107">Initializing variables with DECLARE is one of the most flexible ways to set a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="c7d89-108">You can also use DECLARE to set more than one variable at a time.</span><span class="sxs-lookup"><span data-stu-id="c7d89-108">You can also use DECLARE to set more than one variable at a time.</span></span> <span data-ttu-id="c7d89-109">You cannot use `SELECT` or `UPDATE` to do this:</span><span class="sxs-lookup"><span data-stu-id="c7d89-109">You cannot use `SELECT` or `UPDATE` to do this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="c7d89-110">You cannot initialise and use a variable in the same DECLARE statement.</span><span class="sxs-lookup"><span data-stu-id="c7d89-110">You cannot initialise and use a variable in the same DECLARE statement.</span></span> <span data-ttu-id="c7d89-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span><span class="sxs-lookup"><span data-stu-id="c7d89-111">To illustrate the point the example below is **not** allowed as @p1 is both initialized and used in the same DECLARE statement.</span></span> <span data-ttu-id="c7d89-112">This will result in an error.</span><span class="sxs-lookup"><span data-stu-id="c7d89-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="c7d89-113">Setting values with SET</span><span class="sxs-lookup"><span data-stu-id="c7d89-113">Setting values with SET</span></span>
<span data-ttu-id="c7d89-114">Set is a very common method for setting a single variable.</span><span class="sxs-lookup"><span data-stu-id="c7d89-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="c7d89-115">All of the examples below are valid ways of setting a variable with SET:</span><span class="sxs-lookup"><span data-stu-id="c7d89-115">All of the examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="c7d89-116">You can only set one variable at a time with SET.</span><span class="sxs-lookup"><span data-stu-id="c7d89-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="c7d89-117">However, as can be seen above compound operators are permissable.</span><span class="sxs-lookup"><span data-stu-id="c7d89-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="c7d89-118">Limitations</span><span class="sxs-lookup"><span data-stu-id="c7d89-118">Limitations</span></span>
<span data-ttu-id="c7d89-119">You cannot use SELECT or UPDATE for variable assignment.</span><span class="sxs-lookup"><span data-stu-id="c7d89-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7d89-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7d89-120">Next steps</span></span>
<span data-ttu-id="c7d89-121">For more development tips, see [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="c7d89-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
