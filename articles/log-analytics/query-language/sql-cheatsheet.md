---
title: SQL to Azure Log Analytics query language cheat sheet | Microsoft Docs
description: Common functions to use for different scenarios in Log Analytics queries.
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
ms.date: 08/21/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: 8cc05f02d97eac6bb24c4a0565df8c7335c5b33d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870677"
---
# <a name="sql-to-log-analytics-query-language-cheat-sheet"></a><span data-ttu-id="a081e-103">SQL to Log Analytics query language cheat sheet</span><span class="sxs-lookup"><span data-stu-id="a081e-103">SQL to Log Analytics query language cheat sheet</span></span> 

<span data-ttu-id="a081e-104">The table below helps users who are familiar with SQL to learn the Log Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="a081e-104">The table below helps users who are familiar with SQL to learn the Log Analytics query language.</span></span> <span data-ttu-id="a081e-105">Have a look at the T-SQL command for solving a common scenarios and the equivalent using Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a081e-105">Have a look at the T-SQL command for solving a common scenarios and the equivalent using Log Analytics.</span></span>

## <a name="sql-to-log-analytics"></a><span data-ttu-id="a081e-106">SQL to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="a081e-106">SQL to Log Analytics</span></span>

<span data-ttu-id="a081e-107">Description</span><span class="sxs-lookup"><span data-stu-id="a081e-107">Description</span></span>                             |<span data-ttu-id="a081e-108">SQL Query</span><span class="sxs-lookup"><span data-stu-id="a081e-108">SQL Query</span></span>                                                                                          |<span data-ttu-id="a081e-109">Azure Log Analytics Query</span><span class="sxs-lookup"><span data-stu-id="a081e-109">Azure Log Analytics Query</span></span>
----------------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------
<span data-ttu-id="a081e-110">Select all data from a table</span><span class="sxs-lookup"><span data-stu-id="a081e-110">Select all data from a table</span></span>            |`SELECT * FROM dependencies`                                                                       |<code>dependencies</code>
<span data-ttu-id="a081e-111">Select specific columns from a table</span><span class="sxs-lookup"><span data-stu-id="a081e-111">Select specific columns from a table</span></span>    |`SELECT name, resultCode FROM dependencies`                                                        |<code>dependencies <br>&#124; project name, resultCode</code>
<span data-ttu-id="a081e-112">Select 100 records from a table</span><span class="sxs-lookup"><span data-stu-id="a081e-112">Select 100 records from a table</span></span>         |`SELECT TOP 100 * FROM dependencies`                                                               |<code>dependencies <br>&#124; take 100</code>
<span data-ttu-id="a081e-113">Null evaluation</span><span class="sxs-lookup"><span data-stu-id="a081e-113">Null evaluation</span></span>                         |`SELECT * FROM dependencies WHERE resultCode IS NOT NULL`                                          |<code>dependencies <br>&#124; where isnotnull(resultCode)</code>
<span data-ttu-id="a081e-114">String comparison: equality</span><span class="sxs-lookup"><span data-stu-id="a081e-114">String comparison: equality</span></span>             |`SELECT * FROM dependencies WHERE name = "abcde"`                                                  |<code>dependencies <br>&#124; where name == "abcde"</code>
<span data-ttu-id="a081e-115">String comparison: substring</span><span class="sxs-lookup"><span data-stu-id="a081e-115">String comparison: substring</span></span>            |`SELECT * FROM dependencies WHERE like "%bcd%"`                                                    |<code>dependencies <br>&#124; where name contains "bcd"</code>
<span data-ttu-id="a081e-116">String comparison: wildcard</span><span class="sxs-lookup"><span data-stu-id="a081e-116">String comparison: wildcard</span></span>             |`SELECT * FROM dependencies WHERE name like "abc%"`                                                |<code>dependencies <br>&#124; where name startswith "abc"</code>
<span data-ttu-id="a081e-117">Date comparison: last 1 day</span><span class="sxs-lookup"><span data-stu-id="a081e-117">Date comparison: last 1 day</span></span>             |`SELECT * FROM dependencies WHERE timestamp > getdate()-1`                                         |<code>dependencies <br>&#124; where timestamp > ago(1d)</code>
<span data-ttu-id="a081e-118">Date comparison: date range</span><span class="sxs-lookup"><span data-stu-id="a081e-118">Date comparison: date range</span></span>             |`SELECT * FROM dependencies WHERE timestamp BETWEEN '2016-10-01' AND '2016-11-01'`                 |<code>dependencies <br>&#124; where timestamp between (datetime(2016-10-01) .. datetime(2016-10-01))</code>
<span data-ttu-id="a081e-119">Boolean comparison</span><span class="sxs-lookup"><span data-stu-id="a081e-119">Boolean comparison</span></span>                      |`SELECT * FROM dependencies WHERE !(success)`                                                      |<code>dependencies <br><span data-ttu-id="a081e-120">&#124; where success == "False" </code></span><span class="sxs-lookup"><span data-stu-id="a081e-120">&#124; where success == "False" </code></span></span>
<span data-ttu-id="a081e-121">Sort</span><span class="sxs-lookup"><span data-stu-id="a081e-121">Sort</span></span>                                    |`SELECT name, timestamp FROM dependencies ORDER BY timestamp asc`                                  |<code>dependencies <br><span data-ttu-id="a081e-122">&#124; order by timestamp asc </code></span><span class="sxs-lookup"><span data-stu-id="a081e-122">&#124; order by timestamp asc </code></span></span>
<span data-ttu-id="a081e-123">Distinct</span><span class="sxs-lookup"><span data-stu-id="a081e-123">Distinct</span></span>                                |`SELECT DISTINCT name, type  FROM dependencies`                                                    |<code>dependencies <br><span data-ttu-id="a081e-124">&#124; summarize by name, type </code></span><span class="sxs-lookup"><span data-stu-id="a081e-124">&#124; summarize by name, type </code></span></span>
<span data-ttu-id="a081e-125">Grouping, Aggregation</span><span class="sxs-lookup"><span data-stu-id="a081e-125">Grouping, Aggregation</span></span>                   |`SELECT name, AVG(duration) FROM dependencies GROUP BY name`                                       |<code>dependencies <br><span data-ttu-id="a081e-126">&#124; summarize avg(duration) by name </code></span><span class="sxs-lookup"><span data-stu-id="a081e-126">&#124; summarize avg(duration) by name </code></span></span>
<span data-ttu-id="a081e-127">Column aliases, Extend</span><span class="sxs-lookup"><span data-stu-id="a081e-127">Column aliases, Extend</span></span>                  |`SELECT operation_Name as Name, AVG(duration) as AvgD FROM dependencies GROUP BY name`             |<code>dependencies <br>&#124; summarize AvgD=avg(duration) by operation_Name <br>&#124; project Name=operation_Name, AvgD</code>
<span data-ttu-id="a081e-128">Top n recrods by measure</span><span class="sxs-lookup"><span data-stu-id="a081e-128">Top n recrods by measure</span></span>                |`SELECT TOP 100 name, COUNT(*) as Count FROM dependencies GROUP BY name ORDER BY Count asc`        |<code>dependencies <br>&#124; summarize Count=count() by name <br>&#124; top 100 by Count asc</code>
<span data-ttu-id="a081e-129">Union</span><span class="sxs-lookup"><span data-stu-id="a081e-129">Union</span></span>                                   |`SELECT * FROM dependencies UNION SELECT * FROM exceptions`                                        |<code>union dependencies, exceptions</code>
<span data-ttu-id="a081e-130">Union: with conditions</span><span class="sxs-lookup"><span data-stu-id="a081e-130">Union: with conditions</span></span>                  |`SELECT * FROM dependencies WHERE value > 4 UNION SELECT * FROM exceptions value < 5`              |<code>dependencies <br>&#124; where value > 4 <br>&#124; union (exceptions <br>&#124; where value < 5)</code>
<span data-ttu-id="a081e-131">Join</span><span class="sxs-lookup"><span data-stu-id="a081e-131">Join</span></span>                                    |`SELECT * FROM dependencies JOIN exceptions ON dependencies.operation_Id = exceptions.operation_Id`|<code>dependencies <br>&#124; join (exceptions) on operation_Id == operation_Id</code>


## <a name="next-steps"></a><span data-ttu-id="a081e-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="a081e-132">Next steps</span></span>

- <span data-ttu-id="a081e-133">Go through a lesson on the [writing queries in Log Analytics](get-started-queries.md).</span><span class="sxs-lookup"><span data-stu-id="a081e-133">Go through a lesson on the [writing queries in Log Analytics](get-started-queries.md).</span></span>