---
title: Working with strings in Azure Log Analytics queries | Microsoft Docs
description: This article provides a tutorial for using the Analytics portal to write queries in Log Analytics.
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
ms.date: 08/16/2018
ms.author: bwren
ms.component: na
ms.openlocfilehash: f027754f26a9063aa5faa548fd01576624811005
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865671"
---
# <a name="working-with-json-and-data-structures-in-log-analytics-queries"></a><span data-ttu-id="ddbc4-103">Working with JSON and data Structures in Log Analytics queries</span><span class="sxs-lookup"><span data-stu-id="ddbc4-103">Working with JSON and data Structures in Log Analytics queries</span></span>

> [!NOTE]
> <span data-ttu-id="ddbc4-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-104">You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.</span></span>


<span data-ttu-id="ddbc4-105">Nested objects are objects that contain other objects in an array or a map of key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-105">Nested objects are objects that contain other objects in an array or a map of key-value pairs.</span></span> <span data-ttu-id="ddbc4-106">These objects are represented as JSON strings.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-106">These objects are represented as JSON strings.</span></span> <span data-ttu-id="ddbc4-107">This article describes how JSON is used to retrieve data and analyze nested objects.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-107">This article describes how JSON is used to retrieve data and analyze nested objects.</span></span>

## <a name="working-with-json-strings"></a><span data-ttu-id="ddbc4-108">Working with JSON strings</span><span class="sxs-lookup"><span data-stu-id="ddbc4-108">Working with JSON strings</span></span>
<span data-ttu-id="ddbc4-109">Use `extractjson` to access a specific JSON element in a known path.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-109">Use `extractjson` to access a specific JSON element in a known path.</span></span> <span data-ttu-id="ddbc4-110">This function requires a path expression that uses the following conventions.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-110">This function requires a path expression that uses the following conventions.</span></span>

- <span data-ttu-id="ddbc4-111">_$_ to refer to the root folder</span><span class="sxs-lookup"><span data-stu-id="ddbc4-111">_$_ to refer to the root folder</span></span>
- <span data-ttu-id="ddbc4-112">Use the bracket or dot notation to refer to indexes and elements as illustrated in the following examples.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-112">Use the bracket or dot notation to refer to indexes and elements as illustrated in the following examples.</span></span>


<span data-ttu-id="ddbc4-113">Use brackets for indexes and dots to separate elements:</span><span class="sxs-lookup"><span data-stu-id="ddbc4-113">Use brackets for indexes and dots to separate elements:</span></span>

```OQL
let hosts_report='{"hosts": [{"location":"North_DC", "status":"running", "rate":5},{"location":"South_DC", "status":"stopped", "rate":3}]}';
print hosts_report
| extend status = extractjson("$.hosts[0].status", hosts_report)
```

<span data-ttu-id="ddbc4-114">This is the same result using only the brackets notation:</span><span class="sxs-lookup"><span data-stu-id="ddbc4-114">This is the same result using only the brackets notation:</span></span>

```OQL
let hosts_report='{"hosts": [{"location":"North_DC", "status":"running", "rate":5},{"location":"South_DC", "status":"stopped", "rate":3}]}';
print hosts_report 
| extend status = extractjson("$['hosts'][0]['status']", hosts_report)
```

<span data-ttu-id="ddbc4-115">If there is only one element, you can use only the dot notation:</span><span class="sxs-lookup"><span data-stu-id="ddbc4-115">If there is only one element, you can use only the dot notation:</span></span>

```OQL
let hosts_report='{"location":"North_DC", "status":"running", "rate":5}';
print hosts_report 
| extend status = hosts_report.status
```


## <a name="working-with-objects"></a><span data-ttu-id="ddbc4-116">Working with objects</span><span class="sxs-lookup"><span data-stu-id="ddbc4-116">Working with objects</span></span>

### <a name="parsejson"></a><span data-ttu-id="ddbc4-117">parsejson</span><span class="sxs-lookup"><span data-stu-id="ddbc4-117">parsejson</span></span>
<span data-ttu-id="ddbc4-118">To access mulitple elements in your json structure, it's easier to access it as a dynamic object.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-118">To access mulitple elements in your json structure, it's easier to access it as a dynamic object.</span></span> <span data-ttu-id="ddbc4-119">Use `parsejson` to cast text data to a dynamic object.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-119">Use `parsejson` to cast text data to a dynamic object.</span></span> <span data-ttu-id="ddbc4-120">Once converted to a dynamic type, additional functions can be used to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-120">Once converted to a dynamic type, additional functions can be used to analyze the data.</span></span>

```OQL
let hosts_object = parsejson('{"hosts": [{"location":"North_DC", "status":"running", "rate":5},{"location":"South_DC", "status":"stopped", "rate":3}]}');
print hosts_object 
| extend status0=hosts_object.hosts[0].status, rate1=hosts_object.hosts[1].rate
```



### <a name="arraylength"></a><span data-ttu-id="ddbc4-121">arraylength</span><span class="sxs-lookup"><span data-stu-id="ddbc4-121">arraylength</span></span>
<span data-ttu-id="ddbc4-122">Use `arraylength` to count the number of elements in an array:</span><span class="sxs-lookup"><span data-stu-id="ddbc4-122">Use `arraylength` to count the number of elements in an array:</span></span>

```OQL
let hosts_object = parsejson('{"hosts": [{"location":"North_DC", "status":"running", "rate":5},{"location":"South_DC", "status":"stopped", "rate":3}]}');
print hosts_object 
| extend hosts_num=arraylength(hosts_object.hosts)
```

### <a name="mvexpand"></a><span data-ttu-id="ddbc4-123">mvexpand</span><span class="sxs-lookup"><span data-stu-id="ddbc4-123">mvexpand</span></span>
<span data-ttu-id="ddbc4-124">Use `mvexpand` to break the properties of an object into separate rows.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-124">Use `mvexpand` to break the properties of an object into separate rows.</span></span>

```OQL
let hosts_object = parsejson('{"hosts": [{"location":"North_DC", "status":"running", "rate":5},{"location":"South_DC", "status":"stopped", "rate":3}]}');
print hosts_object 
| mvexpand hosts_object.hosts[0]
```

![mvexpand](media/json-data-structures/mvexpand.png)

### <a name="buildschema"></a><span data-ttu-id="ddbc4-126">buildschema</span><span class="sxs-lookup"><span data-stu-id="ddbc4-126">buildschema</span></span>
<span data-ttu-id="ddbc4-127">Use `buildschema` to get the schema that admits all values of an object:</span><span class="sxs-lookup"><span data-stu-id="ddbc4-127">Use `buildschema` to get the schema that admits all values of an object:</span></span>

```OQL
let hosts_object = parsejson('{"hosts": [{"location":"North_DC", "status":"running", "rate":5},{"location":"South_DC", "status":"stopped", "rate":3}]}');
print hosts_object 
| summarize buildschema(hosts_object)
```

<span data-ttu-id="ddbc4-128">The output is a schema in JSON format:</span><span class="sxs-lookup"><span data-stu-id="ddbc4-128">The output is a schema in JSON format:</span></span>
```json
{
    "hosts":
    {
        "indexer":
        {
            "location": "string",
            "rate": "int",
            "status": "string"
        }
    }
}
```
<span data-ttu-id="ddbc4-129">This output describes the names of the object fields and their matching data types.</span><span class="sxs-lookup"><span data-stu-id="ddbc4-129">This output describes the names of the object fields and their matching data types.</span></span> 

<span data-ttu-id="ddbc4-130">Nested objects may have different schemas such as in the following example:</span><span class="sxs-lookup"><span data-stu-id="ddbc4-130">Nested objects may have different schemas such as in the following example:</span></span>

```OQL
let hosts_object = parsejson('{"hosts": [{"location":"North_DC", "status":"running", "rate":5},{"status":"stopped", "rate":"3", "range":100}]}');
print hosts_object 
| summarize buildschema(hosts_object)
```


![Build schema](media/json-data-structures/buildschema.png)

## <a name="next-steps"></a><span data-ttu-id="ddbc4-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="ddbc4-132">Next steps</span></span>
<span data-ttu-id="ddbc4-133">See other lessons for using the Log Analytics query language:</span><span class="sxs-lookup"><span data-stu-id="ddbc4-133">See other lessons for using the Log Analytics query language:</span></span>

- [<span data-ttu-id="ddbc4-134">String operations</span><span class="sxs-lookup"><span data-stu-id="ddbc4-134">String operations</span></span>](string-operations.md)
- [<span data-ttu-id="ddbc4-135">Date and time operations</span><span class="sxs-lookup"><span data-stu-id="ddbc4-135">Date and time operations</span></span>](datetime-operations.md)
- [<span data-ttu-id="ddbc4-136">Aggregation functions</span><span class="sxs-lookup"><span data-stu-id="ddbc4-136">Aggregation functions</span></span>](aggregations.md)
- [<span data-ttu-id="ddbc4-137">Advanced aggregations</span><span class="sxs-lookup"><span data-stu-id="ddbc4-137">Advanced aggregations</span></span>](advanced-aggregations.md)
- [<span data-ttu-id="ddbc4-138">Advanced query writing</span><span class="sxs-lookup"><span data-stu-id="ddbc4-138">Advanced query writing</span></span>](advanced-query-writing.md)
- [<span data-ttu-id="ddbc4-139">Joins</span><span class="sxs-lookup"><span data-stu-id="ddbc4-139">Joins</span></span>](joins.md)
- [<span data-ttu-id="ddbc4-140">Charts</span><span class="sxs-lookup"><span data-stu-id="ddbc4-140">Charts</span></span>](charts.md)