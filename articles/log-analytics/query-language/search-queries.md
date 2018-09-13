---
title: Search queries in Log Analytics | Microsoft Docs
description: This article provides a tutorial for getting started writing search queries in Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/06/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 6a375da3c97790bd6a7a6fa505de82b2fc298385
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966715"
---
# <a name="search-queries-in-log-analytics"></a><span data-ttu-id="220b7-103">Search queries in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="220b7-103">Search queries in Log Analytics</span></span>

> [!NOTE]
> <span data-ttu-id="220b7-104">You should complete [Get started with queries in Log Analytics](get-started-queries.md) before completing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="220b7-104">You should complete [Get started with queries in Log Analytics](get-started-queries.md) before completing this tutorial.</span></span>

<span data-ttu-id="220b7-105">Azure Log Analytics queries can start with either a table name or a search command.</span><span class="sxs-lookup"><span data-stu-id="220b7-105">Azure Log Analytics queries can start with either a table name or a search command.</span></span> <span data-ttu-id="220b7-106">This tutorial covers search-based queries.</span><span class="sxs-lookup"><span data-stu-id="220b7-106">This tutorial covers search-based queries.</span></span> <span data-ttu-id="220b7-107">There are advantages to each method.</span><span class="sxs-lookup"><span data-stu-id="220b7-107">There are advantages to each method.</span></span>

<span data-ttu-id="220b7-108">Table-based queries start by scoping the query and therefore tend to be more efficient than search queries.</span><span class="sxs-lookup"><span data-stu-id="220b7-108">Table-based queries start by scoping the query and therefore tend to be more efficient than search queries.</span></span> <span data-ttu-id="220b7-109">Search queries are less structured which makes them the better choice when searching for a specific value across columns or tables.</span><span class="sxs-lookup"><span data-stu-id="220b7-109">Search queries are less structured which makes them the better choice when searching for a specific value across columns or tables.</span></span> <span data-ttu-id="220b7-110">**search** can scan all columns in a given table, or in all tables, for the specified value.</span><span class="sxs-lookup"><span data-stu-id="220b7-110">**search** can scan all columns in a given table, or in all tables, for the specified value.</span></span> <span data-ttu-id="220b7-111">The amount of data being processed could be enormous, which is why these queries could take longer to complete and might return very large result sets.</span><span class="sxs-lookup"><span data-stu-id="220b7-111">The amount of data being processed could be enormous, which is why these queries could take longer to complete and might return very large result sets.</span></span>

## <a name="search-a-term"></a><span data-ttu-id="220b7-112">Search a term</span><span class="sxs-lookup"><span data-stu-id="220b7-112">Search a term</span></span>
<span data-ttu-id="220b7-113">The **search** command is typically used to search a specific term.</span><span class="sxs-lookup"><span data-stu-id="220b7-113">The **search** command is typically used to search a specific term.</span></span> <span data-ttu-id="220b7-114">In the following example, all columns in all tables are scanned for the term "error":</span><span class="sxs-lookup"><span data-stu-id="220b7-114">In the following example, all columns in all tables are scanned for the term "error":</span></span>

```OQL
search "error"
| take 100
```

<span data-ttu-id="220b7-115">While they're easy to use, unscoped queries like the one showed above are not efficient and are likely to return many irrelevant results.</span><span class="sxs-lookup"><span data-stu-id="220b7-115">While they're easy to use, unscoped queries like the one showed above are not efficient and are likely to return many irrelevant results.</span></span> <span data-ttu-id="220b7-116">A better practice would be to search in the relevant table, or even a specific column.</span><span class="sxs-lookup"><span data-stu-id="220b7-116">A better practice would be to search in the relevant table, or even a specific column.</span></span>

### <a name="table-scoping"></a><span data-ttu-id="220b7-117">Table scoping</span><span class="sxs-lookup"><span data-stu-id="220b7-117">Table scoping</span></span>
<span data-ttu-id="220b7-118">To search a term in a specific table, add `in (table-name)` just after the **search** operator:</span><span class="sxs-lookup"><span data-stu-id="220b7-118">To search a term in a specific table, add `in (table-name)` just after the **search** operator:</span></span>

```OQL
search in (Event) "error"
| take 100
```

<span data-ttu-id="220b7-119">or in multiple tables:</span><span class="sxs-lookup"><span data-stu-id="220b7-119">or in multiple tables:</span></span>
```OQL
search in (Event, SecurityEvent) "error"
| take 100
```

### <a name="table-and-column-scoping"></a><span data-ttu-id="220b7-120">Table and column scoping</span><span class="sxs-lookup"><span data-stu-id="220b7-120">Table and column scoping</span></span>
<span data-ttu-id="220b7-121">By default, **search** will evaluate all columns in the data set.</span><span class="sxs-lookup"><span data-stu-id="220b7-121">By default, **search** will evaluate all columns in the data set.</span></span> <span data-ttu-id="220b7-122">To search only a specific column, use this syntax:</span><span class="sxs-lookup"><span data-stu-id="220b7-122">To search only a specific column, use this syntax:</span></span>

```OQL
search in (Event) Source:"error"
| take 100
```

> [!TIP]
> <span data-ttu-id="220b7-123">If you use `==` instead of `:`, the results would include records in which the *Source* column has the exact value "error", and in this exact case.</span><span class="sxs-lookup"><span data-stu-id="220b7-123">If you use `==` instead of `:`, the results would include records in which the *Source* column has the exact value "error", and in this exact case.</span></span> <span data-ttu-id="220b7-124">Using ':' will not include records where *Source* has values such as "error code 404" or "Error".</span><span class="sxs-lookup"><span data-stu-id="220b7-124">Using ':' will not include records where *Source* has values such as "error code 404" or "Error".</span></span>

## <a name="case-sensitivity"></a><span data-ttu-id="220b7-125">Case-sensitivity</span><span class="sxs-lookup"><span data-stu-id="220b7-125">Case-sensitivity</span></span>
<span data-ttu-id="220b7-126">By default, term search is case-insensitive, so searching "dns" could yield results such as "DNS", "dns", or "Dns".</span><span class="sxs-lookup"><span data-stu-id="220b7-126">By default, term search is case-insensitive, so searching "dns" could yield results such as "DNS", "dns", or "Dns".</span></span> <span data-ttu-id="220b7-127">To make the search case-sensitive, use the `kind` option:</span><span class="sxs-lookup"><span data-stu-id="220b7-127">To make the search case-sensitive, use the `kind` option:</span></span>

```OQL
search kind=case_sensitive in (Event) "DNS"
| take 100
```

## <a name="use-wild-cards"></a><span data-ttu-id="220b7-128">Use wild cards</span><span class="sxs-lookup"><span data-stu-id="220b7-128">Use wild cards</span></span>
<span data-ttu-id="220b7-129">The **search** command supports wild cards, at the beginning, end or middle of a term.</span><span class="sxs-lookup"><span data-stu-id="220b7-129">The **search** command supports wild cards, at the beginning, end or middle of a term.</span></span>

<span data-ttu-id="220b7-130">To search terms that start with "win":</span><span class="sxs-lookup"><span data-stu-id="220b7-130">To search terms that start with "win":</span></span>
```OQL
search in (Event) "win*"
| take 100
```

<span data-ttu-id="220b7-131">To search terms that end with ".com":</span><span class="sxs-lookup"><span data-stu-id="220b7-131">To search terms that end with ".com":</span></span>
```OQL
search in (Event) "*.com"
| take 100
```

<span data-ttu-id="220b7-132">To search terms that contain "www":</span><span class="sxs-lookup"><span data-stu-id="220b7-132">To search terms that contain "www":</span></span>
```OQL
search in (Event) "*www*"
| take 100
```

<span data-ttu-id="220b7-133">To search terms that starts with "corp" and ends in ".com", such as "corp.mydomain.com""</span><span class="sxs-lookup"><span data-stu-id="220b7-133">To search terms that starts with "corp" and ends in ".com", such as "corp.mydomain.com""</span></span>

```OQL
search in (Event) "corp*.com"
| take 100
```

<span data-ttu-id="220b7-134">You can also get everything in a table by using just a wild card: `search in (Event) *`, but that would be the same as writing just `Event`.</span><span class="sxs-lookup"><span data-stu-id="220b7-134">You can also get everything in a table by using just a wild card: `search in (Event) *`, but that would be the same as writing just `Event`.</span></span>

> [!TIP]
> <span data-ttu-id="220b7-135">While you can use `search *` to get every column from every table, it's recommended that you always scope your queries to specific tables.</span><span class="sxs-lookup"><span data-stu-id="220b7-135">While you can use `search *` to get every column from every table, it's recommended that you always scope your queries to specific tables.</span></span> <span data-ttu-id="220b7-136">Unscoped queries may take a while to complete and might return too many results.</span><span class="sxs-lookup"><span data-stu-id="220b7-136">Unscoped queries may take a while to complete and might return too many results.</span></span>

## <a name="add-and--or-to-search-queries"></a><span data-ttu-id="220b7-137">Add *and* / *or* to search queries</span><span class="sxs-lookup"><span data-stu-id="220b7-137">Add *and* / *or* to search queries</span></span>
<span data-ttu-id="220b7-138">Use **and** to search for records that contain multiple terms:</span><span class="sxs-lookup"><span data-stu-id="220b7-138">Use **and** to search for records that contain multiple terms:</span></span>

```OQL
search in (Event) "error" and "register"
| take 100
```

<span data-ttu-id="220b7-139">Use **or** to get records that contain at least one of the terms:</span><span class="sxs-lookup"><span data-stu-id="220b7-139">Use **or** to get records that contain at least one of the terms:</span></span>

```OQL
search in (Event) "error" or "register"
| take 100
```

<span data-ttu-id="220b7-140">If you have multiple search conditions, you can combine them into the same query using parentheses:</span><span class="sxs-lookup"><span data-stu-id="220b7-140">If you have multiple search conditions, you can combine them into the same query using parentheses:</span></span>

```OQL
search in (Event) "error" and ("register" or "marshal*")
| take 100
```

<span data-ttu-id="220b7-141">The results of this example would be records that contain the term "error" and also contain either "register" or something that starts with "marshal".</span><span class="sxs-lookup"><span data-stu-id="220b7-141">The results of this example would be records that contain the term "error" and also contain either "register" or something that starts with "marshal".</span></span>

## <a name="pipe-search-queries"></a><span data-ttu-id="220b7-142">Pipe search queries</span><span class="sxs-lookup"><span data-stu-id="220b7-142">Pipe search queries</span></span>
<span data-ttu-id="220b7-143">Just like any other command, **search** can be piped so search results can be filtered, sorted, and aggregated.</span><span class="sxs-lookup"><span data-stu-id="220b7-143">Just like any other command, **search** can be piped so search results can be filtered, sorted, and aggregated.</span></span> <span data-ttu-id="220b7-144">For example, to get the number of *Event* records that contain "win":</span><span class="sxs-lookup"><span data-stu-id="220b7-144">For example, to get the number of *Event* records that contain "win":</span></span>

```OQL
search in (Event) "win"
| count
```




## <a name="next-steps"></a><span data-ttu-id="220b7-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="220b7-145">Next steps</span></span>

- <span data-ttu-id="220b7-146">See further tutorials on the [Log Analytics query language site](https://docs.loganalytics.io)</span><span class="sxs-lookup"><span data-stu-id="220b7-146">See further tutorials on the [Log Analytics query language site](https://docs.loganalytics.io)</span></span>