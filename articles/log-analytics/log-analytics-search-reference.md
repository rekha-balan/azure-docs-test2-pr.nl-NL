---
title: Azure Log Analytics search reference | Microsoft Docs
description: The Log Analytics search reference describes the search language and provides the general query syntax options you can use when searching for data and filtering expressions to help narrow your search.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f819992125f77897545ce3194870b1eadf400852
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552357"
---
# <a name="log-analytics-search-reference"></a><span data-ttu-id="04541-103">Log Analytics search reference</span><span class="sxs-lookup"><span data-stu-id="04541-103">Log Analytics search reference</span></span>
<span data-ttu-id="04541-104">The following reference section about search language describes the general query syntax options you can use when searching for data and filtering expressions to help narrow your search.</span><span class="sxs-lookup"><span data-stu-id="04541-104">The following reference section about search language describes the general query syntax options you can use when searching for data and filtering expressions to help narrow your search.</span></span> <span data-ttu-id="04541-105">It also describes commands that you can use to take action on the data retrieved.</span><span class="sxs-lookup"><span data-stu-id="04541-105">It also describes commands that you can use to take action on the data retrieved.</span></span>

<span data-ttu-id="04541-106">You can read about the fields returned in searches, and the facets that help you discover more about similar categories of data, in the [Search field and facet reference section](#search-field-and-facet-reference).</span><span class="sxs-lookup"><span data-stu-id="04541-106">You can read about the fields returned in searches, and the facets that help you discover more about similar categories of data, in the [Search field and facet reference section](#search-field-and-facet-reference).</span></span>

## <a name="general-query-syntax"></a><span data-ttu-id="04541-107">General query syntax</span><span class="sxs-lookup"><span data-stu-id="04541-107">General query syntax</span></span>
<span data-ttu-id="04541-108">The syntax for general querying is as follows:</span><span class="sxs-lookup"><span data-stu-id="04541-108">The syntax for general querying is as follows:</span></span>

```
filterExpression | command1 | command2 …
```

<span data-ttu-id="04541-109">The filter expression (`filterExpression`) defines the "where" condition for the query.</span><span class="sxs-lookup"><span data-stu-id="04541-109">The filter expression (`filterExpression`) defines the "where" condition for the query.</span></span> <span data-ttu-id="04541-110">The commands apply to the results returned by the query.</span><span class="sxs-lookup"><span data-stu-id="04541-110">The commands apply to the results returned by the query.</span></span> <span data-ttu-id="04541-111">Multiple commands must be separated by the pipe character ( | ).</span><span class="sxs-lookup"><span data-stu-id="04541-111">Multiple commands must be separated by the pipe character ( | ).</span></span>

### <a name="general-syntax-examples"></a><span data-ttu-id="04541-112">General syntax examples</span><span class="sxs-lookup"><span data-stu-id="04541-112">General syntax examples</span></span>
<span data-ttu-id="04541-113">Examples:</span><span class="sxs-lookup"><span data-stu-id="04541-113">Examples:</span></span>

```
system
```

<span data-ttu-id="04541-114">This query returns results that contain the word *system* in any field that has been indexed for full text or terms searching.</span><span class="sxs-lookup"><span data-stu-id="04541-114">This query returns results that contain the word *system* in any field that has been indexed for full text or terms searching.</span></span>

> [!NOTE]
> <span data-ttu-id="04541-115">Not all fields are indexed this way, but the most common textual fields (such as descriptions and names) usually are.</span><span class="sxs-lookup"><span data-stu-id="04541-115">Not all fields are indexed this way, but the most common textual fields (such as descriptions and names) usually are.</span></span>
>
>

```
system error
```

<span data-ttu-id="04541-116">This query returns results that contain the words *system* and *error*.</span><span class="sxs-lookup"><span data-stu-id="04541-116">This query returns results that contain the words *system* and *error*.</span></span>

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

<span data-ttu-id="04541-117">This query returns results that contain the words *system* and *error*.</span><span class="sxs-lookup"><span data-stu-id="04541-117">This query returns results that contain the words *system* and *error*.</span></span> <span data-ttu-id="04541-118">It then sorts the results by the *ManagementGroupName* field (in ascending order), and then by the *TimeGenerated* field (in descending order).</span><span class="sxs-lookup"><span data-stu-id="04541-118">It then sorts the results by the *ManagementGroupName* field (in ascending order), and then by the *TimeGenerated* field (in descending order).</span></span> <span data-ttu-id="04541-119">It takes only the first 10 results.</span><span class="sxs-lookup"><span data-stu-id="04541-119">It takes only the first 10 results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04541-120">All the field names and the values for the string and text fields are case sensitive.</span><span class="sxs-lookup"><span data-stu-id="04541-120">All the field names and the values for the string and text fields are case sensitive.</span></span>
>
>

## <a name="filter-expressions"></a><span data-ttu-id="04541-121">Filter expressions</span><span class="sxs-lookup"><span data-stu-id="04541-121">Filter expressions</span></span>
<span data-ttu-id="04541-122">The following subsections explain the filter expressions.</span><span class="sxs-lookup"><span data-stu-id="04541-122">The following subsections explain the filter expressions.</span></span>

### <a name="string-literals"></a><span data-ttu-id="04541-123">String literals</span><span class="sxs-lookup"><span data-stu-id="04541-123">String literals</span></span>
<span data-ttu-id="04541-124">A string literal is any string that is not recognized by the parser as a keyword or a predefined data type (for example, a number or date).</span><span class="sxs-lookup"><span data-stu-id="04541-124">A string literal is any string that is not recognized by the parser as a keyword or a predefined data type (for example, a number or date).</span></span>

<span data-ttu-id="04541-125">Examples:</span><span class="sxs-lookup"><span data-stu-id="04541-125">Examples:</span></span>

```
These all are string literals
```

<span data-ttu-id="04541-126">This query searches for results that contain occurrences of all five words.</span><span class="sxs-lookup"><span data-stu-id="04541-126">This query searches for results that contain occurrences of all five words.</span></span> <span data-ttu-id="04541-127">To perform a complex string search, enclose the string literal in quotation marks.</span><span class="sxs-lookup"><span data-stu-id="04541-127">To perform a complex string search, enclose the string literal in quotation marks.</span></span> <span data-ttu-id="04541-128">For example:</span><span class="sxs-lookup"><span data-stu-id="04541-128">For example:</span></span>

```
"Windows Server"
```

<span data-ttu-id="04541-129">This only returns results with exact matches for *Windows Server*.</span><span class="sxs-lookup"><span data-stu-id="04541-129">This only returns results with exact matches for *Windows Server*.</span></span>

### <a name="numbers"></a><span data-ttu-id="04541-130">Numbers</span><span class="sxs-lookup"><span data-stu-id="04541-130">Numbers</span></span>
<span data-ttu-id="04541-131">The parser supports the decimal integer and floating-point number syntax for numerical fields.</span><span class="sxs-lookup"><span data-stu-id="04541-131">The parser supports the decimal integer and floating-point number syntax for numerical fields.</span></span>

<span data-ttu-id="04541-132">Examples:</span><span class="sxs-lookup"><span data-stu-id="04541-132">Examples:</span></span>

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a><span data-ttu-id="04541-133">Dates and times</span><span class="sxs-lookup"><span data-stu-id="04541-133">Dates and times</span></span>
<span data-ttu-id="04541-134">Every piece of data in the system has a *TimeGenerated* property, which represents the original date and time of the record.</span><span class="sxs-lookup"><span data-stu-id="04541-134">Every piece of data in the system has a *TimeGenerated* property, which represents the original date and time of the record.</span></span> <span data-ttu-id="04541-135">Some types of data can have additional date and time fields (for example, *LastModified*).</span><span class="sxs-lookup"><span data-stu-id="04541-135">Some types of data can have additional date and time fields (for example, *LastModified*).</span></span>

<span data-ttu-id="04541-136">The timeline **Chart/Time** selector in Azure Log Analytics shows a distribution of results over time (according to the current query being run).</span><span class="sxs-lookup"><span data-stu-id="04541-136">The timeline **Chart/Time** selector in Azure Log Analytics shows a distribution of results over time (according to the current query being run).</span></span> <span data-ttu-id="04541-137">This is based on the *TimeGenerated* field.</span><span class="sxs-lookup"><span data-stu-id="04541-137">This is based on the *TimeGenerated* field.</span></span> <span data-ttu-id="04541-138">Date and time fields have a specific string format that can be used in queries to restrict the query to a particular timeframe.</span><span class="sxs-lookup"><span data-stu-id="04541-138">Date and time fields have a specific string format that can be used in queries to restrict the query to a particular timeframe.</span></span> <span data-ttu-id="04541-139">You can also use syntax to refer to relative time intervals (for example, "between 3 days ago and 2 hours ago").</span><span class="sxs-lookup"><span data-stu-id="04541-139">You can also use syntax to refer to relative time intervals (for example, "between 3 days ago and 2 hours ago").</span></span>

<span data-ttu-id="04541-140">The following are valid forms of syntax for dates and times:</span><span class="sxs-lookup"><span data-stu-id="04541-140">The following are valid forms of syntax for dates and times:</span></span>

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


<span data-ttu-id="04541-141">For example:</span><span class="sxs-lookup"><span data-stu-id="04541-141">For example:</span></span>

```
TimeGenerated:2013-10-01T12:20
```

<span data-ttu-id="04541-142">The previous command returns only records with a *TimeGenerated* value of exactly 12:20 on October 1, 2013.</span><span class="sxs-lookup"><span data-stu-id="04541-142">The previous command returns only records with a *TimeGenerated* value of exactly 12:20 on October 1, 2013.</span></span>

<span data-ttu-id="04541-143">The parser also supports the mnemonic Date/Time value, NOW.</span><span class="sxs-lookup"><span data-stu-id="04541-143">The parser also supports the mnemonic Date/Time value, NOW.</span></span> <span data-ttu-id="04541-144">(It is unlikely that this will yield any results, because data doesn’t make it through the system that fast.)</span><span class="sxs-lookup"><span data-stu-id="04541-144">(It is unlikely that this will yield any results, because data doesn’t make it through the system that fast.)</span></span>

<span data-ttu-id="04541-145">These examples are building blocks to use for relative and absolute dates.</span><span class="sxs-lookup"><span data-stu-id="04541-145">These examples are building blocks to use for relative and absolute dates.</span></span> <span data-ttu-id="04541-146">In the next three subsections, you'll see how to use them in more advanced filters, with examples that use relative date ranges.</span><span class="sxs-lookup"><span data-stu-id="04541-146">In the next three subsections, you'll see how to use them in more advanced filters, with examples that use relative date ranges.</span></span>

### <a name="datetime-math"></a><span data-ttu-id="04541-147">Date/Time math</span><span class="sxs-lookup"><span data-stu-id="04541-147">Date/Time math</span></span>
<span data-ttu-id="04541-148">Use the Date/Time math operators to offset or round the Date/Time value, by using simple Date/Time calculations.</span><span class="sxs-lookup"><span data-stu-id="04541-148">Use the Date/Time math operators to offset or round the Date/Time value, by using simple Date/Time calculations.</span></span>

<span data-ttu-id="04541-149">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-149">Syntax:</span></span>

```
datetime/unit
```

```
datetime[+|-]count unit
```

| <span data-ttu-id="04541-150">Operator</span><span class="sxs-lookup"><span data-stu-id="04541-150">Operator</span></span> | <span data-ttu-id="04541-151">Description</span><span class="sxs-lookup"><span data-stu-id="04541-151">Description</span></span> |
| --- | --- |
| / |<span data-ttu-id="04541-152">Rounds Date/Time to the specified unit.</span><span class="sxs-lookup"><span data-stu-id="04541-152">Rounds Date/Time to the specified unit.</span></span> <span data-ttu-id="04541-153">For example, NOW/DAY rounds the current Date/Time to midnight of the current day.</span><span class="sxs-lookup"><span data-stu-id="04541-153">For example, NOW/DAY rounds the current Date/Time to midnight of the current day.</span></span> |
| <span data-ttu-id="04541-154">+ or -</span><span class="sxs-lookup"><span data-stu-id="04541-154">+ or -</span></span> |<span data-ttu-id="04541-155">Offsets Date/Time by the specified number of units.</span><span class="sxs-lookup"><span data-stu-id="04541-155">Offsets Date/Time by the specified number of units.</span></span> <span data-ttu-id="04541-156">For example, NOW+1HOUR offsets the current Date/Time by one hour ahead.</span><span class="sxs-lookup"><span data-stu-id="04541-156">For example, NOW+1HOUR offsets the current Date/Time by one hour ahead.</span></span> <span data-ttu-id="04541-157">2013-10-01T12:00-10DAYS offsets the Date value back by 10 days.</span><span class="sxs-lookup"><span data-stu-id="04541-157">2013-10-01T12:00-10DAYS offsets the Date value back by 10 days.</span></span> |

<span data-ttu-id="04541-158">You can chain the Date/Time math operators together.</span><span class="sxs-lookup"><span data-stu-id="04541-158">You can chain the Date/Time math operators together.</span></span> <span data-ttu-id="04541-159">For example:</span><span class="sxs-lookup"><span data-stu-id="04541-159">For example:</span></span>

```
NOW+1HOUR-10MONTHS/MINUTE
```

<span data-ttu-id="04541-160">The following table lists the supported Date/Time units.</span><span class="sxs-lookup"><span data-stu-id="04541-160">The following table lists the supported Date/Time units.</span></span>

| <span data-ttu-id="04541-161">Date/Time unit</span><span class="sxs-lookup"><span data-stu-id="04541-161">Date/Time unit</span></span> | <span data-ttu-id="04541-162">Description</span><span class="sxs-lookup"><span data-stu-id="04541-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04541-163">YEAR, YEARS</span><span class="sxs-lookup"><span data-stu-id="04541-163">YEAR, YEARS</span></span> |<span data-ttu-id="04541-164">Rounds to current year, or offsets by the specified number of years.</span><span class="sxs-lookup"><span data-stu-id="04541-164">Rounds to current year, or offsets by the specified number of years.</span></span> |
| <span data-ttu-id="04541-165">MONTH, MONTHS</span><span class="sxs-lookup"><span data-stu-id="04541-165">MONTH, MONTHS</span></span> |<span data-ttu-id="04541-166">Rounds to current month, or offsets by the specified number of months.</span><span class="sxs-lookup"><span data-stu-id="04541-166">Rounds to current month, or offsets by the specified number of months.</span></span> |
| <span data-ttu-id="04541-167">DAY, DAYS, DATE</span><span class="sxs-lookup"><span data-stu-id="04541-167">DAY, DAYS, DATE</span></span> |<span data-ttu-id="04541-168">Rounds to current day of the month, or offsets by the specified number of days.</span><span class="sxs-lookup"><span data-stu-id="04541-168">Rounds to current day of the month, or offsets by the specified number of days.</span></span> |
| <span data-ttu-id="04541-169">HOUR, HOURS</span><span class="sxs-lookup"><span data-stu-id="04541-169">HOUR, HOURS</span></span> |<span data-ttu-id="04541-170">Rounds to current hour, or offsets by the specified number of hours.</span><span class="sxs-lookup"><span data-stu-id="04541-170">Rounds to current hour, or offsets by the specified number of hours.</span></span> |
| <span data-ttu-id="04541-171">MINUTE, MINUTES</span><span class="sxs-lookup"><span data-stu-id="04541-171">MINUTE, MINUTES</span></span> |<span data-ttu-id="04541-172">Rounds to current minute, or offsets by the specified number of minutes.</span><span class="sxs-lookup"><span data-stu-id="04541-172">Rounds to current minute, or offsets by the specified number of minutes.</span></span> |
| <span data-ttu-id="04541-173">SECOND, SECONDS</span><span class="sxs-lookup"><span data-stu-id="04541-173">SECOND, SECONDS</span></span> |<span data-ttu-id="04541-174">Rounds to current second, or offsets by the specified number of seconds.</span><span class="sxs-lookup"><span data-stu-id="04541-174">Rounds to current second, or offsets by the specified number of seconds.</span></span> |
| <span data-ttu-id="04541-175">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span><span class="sxs-lookup"><span data-stu-id="04541-175">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span></span> |<span data-ttu-id="04541-176">Rounds to current millisecond, or offsets by the specified number of milliseconds.</span><span class="sxs-lookup"><span data-stu-id="04541-176">Rounds to current millisecond, or offsets by the specified number of milliseconds.</span></span> |

### <a name="field-facets"></a><span data-ttu-id="04541-177">Field facets</span><span class="sxs-lookup"><span data-stu-id="04541-177">Field facets</span></span>
<span data-ttu-id="04541-178">By using field facets, you can specify the search condition for specific fields and their exact values.</span><span class="sxs-lookup"><span data-stu-id="04541-178">By using field facets, you can specify the search condition for specific fields and their exact values.</span></span> <span data-ttu-id="04541-179">This differs from writing "free text" queries for various terms throughout the index.</span><span class="sxs-lookup"><span data-stu-id="04541-179">This differs from writing "free text" queries for various terms throughout the index.</span></span> <span data-ttu-id="04541-180">You have already seen this technique in several previous examples.</span><span class="sxs-lookup"><span data-stu-id="04541-180">You have already seen this technique in several previous examples.</span></span> <span data-ttu-id="04541-181">The following are more complex examples.</span><span class="sxs-lookup"><span data-stu-id="04541-181">The following are more complex examples.</span></span>

<span data-ttu-id="04541-182">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="04541-182">**Syntax**</span></span>

```
field:value
```

```
field=value
```

<span data-ttu-id="04541-183">**Description**</span><span class="sxs-lookup"><span data-stu-id="04541-183">**Description**</span></span>

<span data-ttu-id="04541-184">Searches the field for the specific value.</span><span class="sxs-lookup"><span data-stu-id="04541-184">Searches the field for the specific value.</span></span> <span data-ttu-id="04541-185">The value can be a string literal, number, or date and time.</span><span class="sxs-lookup"><span data-stu-id="04541-185">The value can be a string literal, number, or date and time.</span></span>

<span data-ttu-id="04541-186">For example:</span><span class="sxs-lookup"><span data-stu-id="04541-186">For example:</span></span>

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

<span data-ttu-id="04541-187">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="04541-187">**Syntax**</span></span>

<span data-ttu-id="04541-188">*field>value*</span><span class="sxs-lookup"><span data-stu-id="04541-188">*field>value*</span></span>

<span data-ttu-id="04541-189">*field<value*</span><span class="sxs-lookup"><span data-stu-id="04541-189">*field<value*</span></span>

<span data-ttu-id="04541-190">*field>=value*</span><span class="sxs-lookup"><span data-stu-id="04541-190">*field>=value*</span></span>

<span data-ttu-id="04541-191">*field<=value*</span><span class="sxs-lookup"><span data-stu-id="04541-191">*field<=value*</span></span>

<span data-ttu-id="04541-192">*field!=value*</span><span class="sxs-lookup"><span data-stu-id="04541-192">*field!=value*</span></span>

<span data-ttu-id="04541-193">**Description**</span><span class="sxs-lookup"><span data-stu-id="04541-193">**Description**</span></span>

<span data-ttu-id="04541-194">Provides comparisons.</span><span class="sxs-lookup"><span data-stu-id="04541-194">Provides comparisons.</span></span>

<span data-ttu-id="04541-195">For example:</span><span class="sxs-lookup"><span data-stu-id="04541-195">For example:</span></span>

```
TimeGenerated>NOW+2HOURS
```

<span data-ttu-id="04541-196">**Syntax**</span><span class="sxs-lookup"><span data-stu-id="04541-196">**Syntax**</span></span>

```
field:[from..to]
```

<span data-ttu-id="04541-197">**Description**</span><span class="sxs-lookup"><span data-stu-id="04541-197">**Description**</span></span>

<span data-ttu-id="04541-198">Provides range faceting.</span><span class="sxs-lookup"><span data-stu-id="04541-198">Provides range faceting.</span></span>

<span data-ttu-id="04541-199">For example:</span><span class="sxs-lookup"><span data-stu-id="04541-199">For example:</span></span>

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a><span data-ttu-id="04541-200">IN</span><span class="sxs-lookup"><span data-stu-id="04541-200">IN</span></span>
<span data-ttu-id="04541-201">The **IN** keyword allows you to select from a list of values.</span><span class="sxs-lookup"><span data-stu-id="04541-201">The **IN** keyword allows you to select from a list of values.</span></span> <span data-ttu-id="04541-202">Depending on the syntax you use, this can be a simple list of values you provide, or a list of values from an aggregation.</span><span class="sxs-lookup"><span data-stu-id="04541-202">Depending on the syntax you use, this can be a simple list of values you provide, or a list of values from an aggregation.</span></span>

<span data-ttu-id="04541-203">Syntax 1:</span><span class="sxs-lookup"><span data-stu-id="04541-203">Syntax 1:</span></span>

```
field IN {value1,value2,value3,...}
```

<span data-ttu-id="04541-204">This syntax allows you to include all values in a simple list.</span><span class="sxs-lookup"><span data-stu-id="04541-204">This syntax allows you to include all values in a simple list.</span></span>



<span data-ttu-id="04541-205">Examples:</span><span class="sxs-lookup"><span data-stu-id="04541-205">Examples:</span></span>

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

<span data-ttu-id="04541-206">Syntax 2:</span><span class="sxs-lookup"><span data-stu-id="04541-206">Syntax 2:</span></span>

```
(Outer query) (Field to use with inner query results) IN {Inner query | measure count() by (Field to send to outer query)} (rest  of outer query)  
```

<span data-ttu-id="04541-207">This syntax allows you to create an aggregation.</span><span class="sxs-lookup"><span data-stu-id="04541-207">This syntax allows you to create an aggregation.</span></span> <span data-ttu-id="04541-208">You can then feed the list of values from that aggregation into another outer (primary) search that looks for events with those value.</span><span class="sxs-lookup"><span data-stu-id="04541-208">You can then feed the list of values from that aggregation into another outer (primary) search that looks for events with those value.</span></span> <span data-ttu-id="04541-209">You do this by enclosing the inner search in braces, and feeding its results as possible values for a field in the outer search by using the IN operator.</span><span class="sxs-lookup"><span data-stu-id="04541-209">You do this by enclosing the inner search in braces, and feeding its results as possible values for a field in the outer search by using the IN operator.</span></span>

<span data-ttu-id="04541-210">Inner query example: *computers currently missing security updates* with the following aggregation query:</span><span class="sxs-lookup"><span data-stu-id="04541-210">Inner query example: *computers currently missing security updates* with the following aggregation query:</span></span>

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

<span data-ttu-id="04541-211">The final query that finds *all Windows events for computers currently missing security updates* resembles the following:</span><span class="sxs-lookup"><span data-stu-id="04541-211">The final query that finds *all Windows events for computers currently missing security updates* resembles the following:</span></span>

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a><span data-ttu-id="04541-212">Contains</span><span class="sxs-lookup"><span data-stu-id="04541-212">Contains</span></span>
<span data-ttu-id="04541-213">The **Contains** keyword allows you to filter for records with a field that contains a specified string.</span><span class="sxs-lookup"><span data-stu-id="04541-213">The **Contains** keyword allows you to filter for records with a field that contains a specified string.</span></span> <span data-ttu-id="04541-214">This is case sensitive, works only with string fields, and may not include any escape characters.</span><span class="sxs-lookup"><span data-stu-id="04541-214">This is case sensitive, works only with string fields, and may not include any escape characters.</span></span>

<span data-ttu-id="04541-215">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-215">Syntax:</span></span>

```
field:contains("string")
```

<span data-ttu-id="04541-216">Example:</span><span class="sxs-lookup"><span data-stu-id="04541-216">Example:</span></span>

```
Type:contains("Event")
```

<span data-ttu-id="04541-217">This returns records with a type that contains the string "Event".</span><span class="sxs-lookup"><span data-stu-id="04541-217">This returns records with a type that contains the string "Event".</span></span> <span data-ttu-id="04541-218">Examples include **Event**, **SecurityEvent**, and **ServiceFabricOperationEvent**.</span><span class="sxs-lookup"><span data-stu-id="04541-218">Examples include **Event**, **SecurityEvent**, and **ServiceFabricOperationEvent**.</span></span>



### <a name="regular-expressions"></a><span data-ttu-id="04541-219">Regular expressions</span><span class="sxs-lookup"><span data-stu-id="04541-219">Regular expressions</span></span>
<span data-ttu-id="04541-220">You can specify a search condition for a field with a regular expression, by using the **Regex** keyword.</span><span class="sxs-lookup"><span data-stu-id="04541-220">You can specify a search condition for a field with a regular expression, by using the **Regex** keyword.</span></span> <span data-ttu-id="04541-221">For a complete description of the syntax you can use in regular expressions, see [Using regular expressions to filter log searches in Log Analytics](log-analytics-log-searches-regex.md).</span><span class="sxs-lookup"><span data-stu-id="04541-221">For a complete description of the syntax you can use in regular expressions, see [Using regular expressions to filter log searches in Log Analytics](log-analytics-log-searches-regex.md).</span></span>

<span data-ttu-id="04541-222">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-222">Syntax:</span></span>

```
field:Regex("Regular Expression")
```

<span data-ttu-id="04541-223">Example:</span><span class="sxs-lookup"><span data-stu-id="04541-223">Example:</span></span>

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a><span data-ttu-id="04541-224">Logical operators</span><span class="sxs-lookup"><span data-stu-id="04541-224">Logical operators</span></span>
<span data-ttu-id="04541-225">The query languages support the logical operators (*AND*, *OR*, and *NOT*) and their C-style aliases (*&&*, *||*, and *!*, respectively).</span><span class="sxs-lookup"><span data-stu-id="04541-225">The query languages support the logical operators (*AND*, *OR*, and *NOT*) and their C-style aliases (*&&*, *||*, and *!*, respectively).</span></span> <span data-ttu-id="04541-226">You can use parentheses to group these operators.</span><span class="sxs-lookup"><span data-stu-id="04541-226">You can use parentheses to group these operators.</span></span>

<span data-ttu-id="04541-227">Examples:</span><span class="sxs-lookup"><span data-stu-id="04541-227">Examples:</span></span>

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

<span data-ttu-id="04541-228">You can omit the logical operator for the top-level filter arguments.</span><span class="sxs-lookup"><span data-stu-id="04541-228">You can omit the logical operator for the top-level filter arguments.</span></span> <span data-ttu-id="04541-229">In this case, the AND operator is assumed.</span><span class="sxs-lookup"><span data-stu-id="04541-229">In this case, the AND operator is assumed.</span></span>

| <span data-ttu-id="04541-230">Filter expression</span><span class="sxs-lookup"><span data-stu-id="04541-230">Filter expression</span></span> | <span data-ttu-id="04541-231">Equivalent to</span><span class="sxs-lookup"><span data-stu-id="04541-231">Equivalent to</span></span> |
| --- | --- |
| <span data-ttu-id="04541-232">system error</span><span class="sxs-lookup"><span data-stu-id="04541-232">system error</span></span> |<span data-ttu-id="04541-233">system AND error</span><span class="sxs-lookup"><span data-stu-id="04541-233">system AND error</span></span> |
| <span data-ttu-id="04541-234">system "Windows Server" OR Severity:1</span><span class="sxs-lookup"><span data-stu-id="04541-234">system "Windows Server" OR Severity:1</span></span> |<span data-ttu-id="04541-235">system AND ("Windows Server" OR Severity:1)</span><span class="sxs-lookup"><span data-stu-id="04541-235">system AND ("Windows Server" OR Severity:1)</span></span> |

### <a name="wildcarding"></a><span data-ttu-id="04541-236">Wildcarding</span><span class="sxs-lookup"><span data-stu-id="04541-236">Wildcarding</span></span>
<span data-ttu-id="04541-237">The query language supports using the ( \* ) character to  represent one or more characters for a value in a query.</span><span class="sxs-lookup"><span data-stu-id="04541-237">The query language supports using the ( \* ) character to  represent one or more characters for a value in a query.</span></span>

<span data-ttu-id="04541-238">Example:</span><span class="sxs-lookup"><span data-stu-id="04541-238">Example:</span></span>

 <span data-ttu-id="04541-239">Find all computers with "SQL" in the name, such as "Redmond-SQL".</span><span class="sxs-lookup"><span data-stu-id="04541-239">Find all computers with "SQL" in the name, such as "Redmond-SQL".</span></span>

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> <span data-ttu-id="04541-240">At this time, wildcards cannot be used within quotations.</span><span class="sxs-lookup"><span data-stu-id="04541-240">At this time, wildcards cannot be used within quotations.</span></span> <span data-ttu-id="04541-241">For example, the message `"*This text*"` considers the (\*) used as a literal (\*) character.</span><span class="sxs-lookup"><span data-stu-id="04541-241">For example, the message `"*This text*"` considers the (\*) used as a literal (\*) character.</span></span>


## <a name="commands"></a><span data-ttu-id="04541-242">Commands</span><span class="sxs-lookup"><span data-stu-id="04541-242">Commands</span></span>


<span data-ttu-id="04541-243">The commands apply to the results that are returned by the query.</span><span class="sxs-lookup"><span data-stu-id="04541-243">The commands apply to the results that are returned by the query.</span></span> <span data-ttu-id="04541-244">Use the pipe character ( | ) to apply a command to the retrieved results.</span><span class="sxs-lookup"><span data-stu-id="04541-244">Use the pipe character ( | ) to apply a command to the retrieved results.</span></span> <span data-ttu-id="04541-245">Multiple commands must be separated by the pipe character.</span><span class="sxs-lookup"><span data-stu-id="04541-245">Multiple commands must be separated by the pipe character.</span></span>

> [!NOTE]
> <span data-ttu-id="04541-246">Command names can be written in upper case or lower case, unlike the field names and the data.</span><span class="sxs-lookup"><span data-stu-id="04541-246">Command names can be written in upper case or lower case, unlike the field names and the data.</span></span>
>
>

### <a name="sort"></a><span data-ttu-id="04541-247">Sort</span><span class="sxs-lookup"><span data-stu-id="04541-247">Sort</span></span>
<span data-ttu-id="04541-248">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-248">Syntax:</span></span>

    sort field1 asc|desc, field2 asc|desc, …

<span data-ttu-id="04541-249">Sorts the results by particular fields.</span><span class="sxs-lookup"><span data-stu-id="04541-249">Sorts the results by particular fields.</span></span> <span data-ttu-id="04541-250">The asc/desc suffix to sort the results in ascending or descending order is optional.</span><span class="sxs-lookup"><span data-stu-id="04541-250">The asc/desc suffix to sort the results in ascending or descending order is optional.</span></span> <span data-ttu-id="04541-251">If it is omitted, the *asc* sort order is assumed.</span><span class="sxs-lookup"><span data-stu-id="04541-251">If it is omitted, the *asc* sort order is assumed.</span></span> <span data-ttu-id="04541-252">For the **TimeGenerated** field, *desc* sort order is assumed, so it returns the most recent results first by default.</span><span class="sxs-lookup"><span data-stu-id="04541-252">For the **TimeGenerated** field, *desc* sort order is assumed, so it returns the most recent results first by default.</span></span>

### <a name="toplimit"></a><span data-ttu-id="04541-253">Top/Limit</span><span class="sxs-lookup"><span data-stu-id="04541-253">Top/Limit</span></span>
<span data-ttu-id="04541-254">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-254">Syntax:</span></span>

    top number


    limit number
<span data-ttu-id="04541-255">Limits the response to the top N results.</span><span class="sxs-lookup"><span data-stu-id="04541-255">Limits the response to the top N results.</span></span>

<span data-ttu-id="04541-256">Example:</span><span class="sxs-lookup"><span data-stu-id="04541-256">Example:</span></span>

    Type:Alert errors detected | top 10

<span data-ttu-id="04541-257">Returns the top 10 matching results.</span><span class="sxs-lookup"><span data-stu-id="04541-257">Returns the top 10 matching results.</span></span>

### <a name="skip"></a><span data-ttu-id="04541-258">Skip</span><span class="sxs-lookup"><span data-stu-id="04541-258">Skip</span></span>
<span data-ttu-id="04541-259">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-259">Syntax:</span></span>

    skip number

<span data-ttu-id="04541-260">Skips the number of results listed.</span><span class="sxs-lookup"><span data-stu-id="04541-260">Skips the number of results listed.</span></span>

<span data-ttu-id="04541-261">Example:</span><span class="sxs-lookup"><span data-stu-id="04541-261">Example:</span></span>

    Type:Alert errors detected | top 10 | skip 200

<span data-ttu-id="04541-262">Returns top 10 matching results starting at result 200.</span><span class="sxs-lookup"><span data-stu-id="04541-262">Returns top 10 matching results starting at result 200.</span></span>

### <a name="select"></a><span data-ttu-id="04541-263">Select</span><span class="sxs-lookup"><span data-stu-id="04541-263">Select</span></span>
<span data-ttu-id="04541-264">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-264">Syntax:</span></span>

    select field1, field2, ...

<span data-ttu-id="04541-265">Limits results to the fields you choose.</span><span class="sxs-lookup"><span data-stu-id="04541-265">Limits results to the fields you choose.</span></span>

<span data-ttu-id="04541-266">Example:</span><span class="sxs-lookup"><span data-stu-id="04541-266">Example:</span></span>

    Type:Alert errors detected | select Name, Severity

<span data-ttu-id="04541-267">Limits the returned results fields to *Name* and *Severity*.</span><span class="sxs-lookup"><span data-stu-id="04541-267">Limits the returned results fields to *Name* and *Severity*.</span></span>

### <a name="measure"></a><span data-ttu-id="04541-268">Measure</span><span class="sxs-lookup"><span data-stu-id="04541-268">Measure</span></span>
<span data-ttu-id="04541-269">The *measure* command is used to apply statistical functions to the raw search results.</span><span class="sxs-lookup"><span data-stu-id="04541-269">The *measure* command is used to apply statistical functions to the raw search results.</span></span> <span data-ttu-id="04541-270">This is very useful to get *group-by* views over the data.</span><span class="sxs-lookup"><span data-stu-id="04541-270">This is very useful to get *group-by* views over the data.</span></span> <span data-ttu-id="04541-271">When you use the measure command, Log Analytics search displays a table with aggregated results.</span><span class="sxs-lookup"><span data-stu-id="04541-271">When you use the measure command, Log Analytics search displays a table with aggregated results.</span></span>

<span data-ttu-id="04541-272">**Syntax:**</span><span class="sxs-lookup"><span data-stu-id="04541-272">**Syntax:**</span></span>

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



<span data-ttu-id="04541-273">Aggregates the results by *groupField*, and calculates the aggregated measure values by using *aggregatedField*.</span><span class="sxs-lookup"><span data-stu-id="04541-273">Aggregates the results by *groupField*, and calculates the aggregated measure values by using *aggregatedField*.</span></span>

| <span data-ttu-id="04541-274">Measure statistical function</span><span class="sxs-lookup"><span data-stu-id="04541-274">Measure statistical function</span></span> | <span data-ttu-id="04541-275">Description</span><span class="sxs-lookup"><span data-stu-id="04541-275">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04541-276">*aggregateFunction*</span><span class="sxs-lookup"><span data-stu-id="04541-276">*aggregateFunction*</span></span> |<span data-ttu-id="04541-277">The name of the aggregate function (case insensitive).</span><span class="sxs-lookup"><span data-stu-id="04541-277">The name of the aggregate function (case insensitive).</span></span> <span data-ttu-id="04541-278">The following aggregate functions are supported: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span><span class="sxs-lookup"><span data-stu-id="04541-278">The following aggregate functions are supported: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> |
| <span data-ttu-id="04541-279">*aggregatedField*</span><span class="sxs-lookup"><span data-stu-id="04541-279">*aggregatedField*</span></span> |<span data-ttu-id="04541-280">The field that is being aggregated.</span><span class="sxs-lookup"><span data-stu-id="04541-280">The field that is being aggregated.</span></span> <span data-ttu-id="04541-281">This field is optional for the COUNT aggregate function, but has to be an existing numeric field for SUM, MAX, MIN, AVG, STDDEV, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span><span class="sxs-lookup"><span data-stu-id="04541-281">This field is optional for the COUNT aggregate function, but has to be an existing numeric field for SUM, MAX, MIN, AVG, STDDEV, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> <span data-ttu-id="04541-282">The aggregatedField can also be any of the **Extend** supported functions.</span><span class="sxs-lookup"><span data-stu-id="04541-282">The aggregatedField can also be any of the **Extend** supported functions.</span></span> |
| <span data-ttu-id="04541-283">*fieldAlias*</span><span class="sxs-lookup"><span data-stu-id="04541-283">*fieldAlias*</span></span> |<span data-ttu-id="04541-284">The (optional) alias for the calculated aggregated value.</span><span class="sxs-lookup"><span data-stu-id="04541-284">The (optional) alias for the calculated aggregated value.</span></span> <span data-ttu-id="04541-285">If not specified, the field name is **AggregatedValue**.</span><span class="sxs-lookup"><span data-stu-id="04541-285">If not specified, the field name is **AggregatedValue**.</span></span> |
| <span data-ttu-id="04541-286">*groupField*</span><span class="sxs-lookup"><span data-stu-id="04541-286">*groupField*</span></span> |<span data-ttu-id="04541-287">The name of the field that the result set is grouped by.</span><span class="sxs-lookup"><span data-stu-id="04541-287">The name of the field that the result set is grouped by.</span></span> |
| <span data-ttu-id="04541-288">*Interval*</span><span class="sxs-lookup"><span data-stu-id="04541-288">*Interval*</span></span> |<span data-ttu-id="04541-289">The time interval, in the format:**nnnNAME**.</span><span class="sxs-lookup"><span data-stu-id="04541-289">The time interval, in the format:**nnnNAME**.</span></span> <span data-ttu-id="04541-290">**nnn** is the positive integer number.</span><span class="sxs-lookup"><span data-stu-id="04541-290">**nnn** is the positive integer number.</span></span> <span data-ttu-id="04541-291">**NAME** is the interval name.</span><span class="sxs-lookup"><span data-stu-id="04541-291">**NAME** is the interval name.</span></span> <span data-ttu-id="04541-292">Supported interval names are case sensitive, and include:MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S], and YEAR[S].</span><span class="sxs-lookup"><span data-stu-id="04541-292">Supported interval names are case sensitive, and include:MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S], and YEAR[S].</span></span> |

<span data-ttu-id="04541-293">The interval option can only be used in Date/Time group fields (such as *TimeGenerated* and *TimeCreated*).</span><span class="sxs-lookup"><span data-stu-id="04541-293">The interval option can only be used in Date/Time group fields (such as *TimeGenerated* and *TimeCreated*).</span></span> <span data-ttu-id="04541-294">Currently, this is not enforced by the service, but a field without Date/Time that is passed to the back end causes a runtime error.</span><span class="sxs-lookup"><span data-stu-id="04541-294">Currently, this is not enforced by the service, but a field without Date/Time that is passed to the back end causes a runtime error.</span></span> <span data-ttu-id="04541-295">When the schema validation is implemented, the service API rejects queries that use fields without Date/Time for interval aggregation.</span><span class="sxs-lookup"><span data-stu-id="04541-295">When the schema validation is implemented, the service API rejects queries that use fields without Date/Time for interval aggregation.</span></span> <span data-ttu-id="04541-296">The current *Measure* implementation supports interval grouping for any aggregate function.</span><span class="sxs-lookup"><span data-stu-id="04541-296">The current *Measure* implementation supports interval grouping for any aggregate function.</span></span>

<span data-ttu-id="04541-297">If the BY clause is omitted, but an interval is specified (as a second syntax), the *TimeGenerated* field is assumed by default.</span><span class="sxs-lookup"><span data-stu-id="04541-297">If the BY clause is omitted, but an interval is specified (as a second syntax), the *TimeGenerated* field is assumed by default.</span></span>

<span data-ttu-id="04541-298">Examples:</span><span class="sxs-lookup"><span data-stu-id="04541-298">Examples:</span></span>

<span data-ttu-id="04541-299">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="04541-299">**Example 1**</span></span>

    Type:Alert | measure count() as Count by ObjectId

<span data-ttu-id="04541-300">Groups the alerts by *ObjectID*, and calculates the number of alerts for each group.</span><span class="sxs-lookup"><span data-stu-id="04541-300">Groups the alerts by *ObjectID*, and calculates the number of alerts for each group.</span></span> <span data-ttu-id="04541-301">The aggregated value is returned as the *Count* field (alias).</span><span class="sxs-lookup"><span data-stu-id="04541-301">The aggregated value is returned as the *Count* field (alias).</span></span>

<span data-ttu-id="04541-302">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="04541-302">**Example 2**</span></span>

    Type:Alert | measure count() interval 1HOUR

<span data-ttu-id="04541-303">Groups the alerts by 1-hour intervals by using the *TimeGenerated* field, and returns the number of alerts in each interval.</span><span class="sxs-lookup"><span data-stu-id="04541-303">Groups the alerts by 1-hour intervals by using the *TimeGenerated* field, and returns the number of alerts in each interval.</span></span>

<span data-ttu-id="04541-304">**Example 3**</span><span class="sxs-lookup"><span data-stu-id="04541-304">**Example 3**</span></span>

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

<span data-ttu-id="04541-305">Same as the previous example, but with an aggregated field alias (*AlertsPerHour*).</span><span class="sxs-lookup"><span data-stu-id="04541-305">Same as the previous example, but with an aggregated field alias (*AlertsPerHour*).</span></span>

<span data-ttu-id="04541-306">**Example 4**</span><span class="sxs-lookup"><span data-stu-id="04541-306">**Example 4**</span></span>

    * <span data-ttu-id="04541-307">| measure count() by TimeCreated interval 5DAYS</span><span class="sxs-lookup"><span data-stu-id="04541-307">| measure count() by TimeCreated interval 5DAYS</span></span>

<span data-ttu-id="04541-308">Groups the results by 5-day intervals by using the *TimeCreated* field, and returns the number of results in each interval.</span><span class="sxs-lookup"><span data-stu-id="04541-308">Groups the results by 5-day intervals by using the *TimeCreated* field, and returns the number of results in each interval.</span></span>

<span data-ttu-id="04541-309">**Example 5**</span><span class="sxs-lookup"><span data-stu-id="04541-309">**Example 5**</span></span>

    Type:Alert | measure max(Severity) by WorkflowName

<span data-ttu-id="04541-310">Groups the alerts by workload name, and returns the maximum alert severity value for each workflow.</span><span class="sxs-lookup"><span data-stu-id="04541-310">Groups the alerts by workload name, and returns the maximum alert severity value for each workflow.</span></span>

<span data-ttu-id="04541-311">**Example 6**</span><span class="sxs-lookup"><span data-stu-id="04541-311">**Example 6**</span></span>

    Type:Alert | measure min(Severity) by WorkflowName

<span data-ttu-id="04541-312">Same as the previous example, but with the *min* aggregated function.</span><span class="sxs-lookup"><span data-stu-id="04541-312">Same as the previous example, but with the *min* aggregated function.</span></span>

<span data-ttu-id="04541-313">**Example 7**</span><span class="sxs-lookup"><span data-stu-id="04541-313">**Example 7**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer

<span data-ttu-id="04541-314">Groups Perf by computer, and calculates the average (avg).</span><span class="sxs-lookup"><span data-stu-id="04541-314">Groups Perf by computer, and calculates the average (avg).</span></span>

<span data-ttu-id="04541-315">**Example 8**</span><span class="sxs-lookup"><span data-stu-id="04541-315">**Example 8**</span></span>

    Type:Perf | measure sum(CounterValue) by Computer

<span data-ttu-id="04541-316">Same as the previous example, but uses *sum*.</span><span class="sxs-lookup"><span data-stu-id="04541-316">Same as the previous example, but uses *sum*.</span></span>

<span data-ttu-id="04541-317">**Example 9**</span><span class="sxs-lookup"><span data-stu-id="04541-317">**Example 9**</span></span>

    Type:Perf | measure stddev(CounterValue) by Computer

<span data-ttu-id="04541-318">Same as the previous example, but uses *stddev*.</span><span class="sxs-lookup"><span data-stu-id="04541-318">Same as the previous example, but uses *stddev*.</span></span>

<span data-ttu-id="04541-319">**Example 10**</span><span class="sxs-lookup"><span data-stu-id="04541-319">**Example 10**</span></span>

    Type:Perf | measure percentile70(CounterValue) by Computer

<span data-ttu-id="04541-320">Same as the previous example, but uses *percentile70*.</span><span class="sxs-lookup"><span data-stu-id="04541-320">Same as the previous example, but uses *percentile70*.</span></span>

<span data-ttu-id="04541-321">**Example 11**</span><span class="sxs-lookup"><span data-stu-id="04541-321">**Example 11**</span></span>

    Type:Perf | measure pct70(CounterValue) by Computer

<span data-ttu-id="04541-322">Same as the previous example, but uses *pct70*.</span><span class="sxs-lookup"><span data-stu-id="04541-322">Same as the previous example, but uses *pct70*.</span></span> <span data-ttu-id="04541-323">Note that *PCT##* is only an alias for *PERCENTILE##* function.</span><span class="sxs-lookup"><span data-stu-id="04541-323">Note that *PCT##* is only an alias for *PERCENTILE##* function.</span></span>

<span data-ttu-id="04541-324">**Example 12**</span><span class="sxs-lookup"><span data-stu-id="04541-324">**Example 12**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

<span data-ttu-id="04541-325">Groups Perf first by Computer and then CounterName, and calculates the average (avg).</span><span class="sxs-lookup"><span data-stu-id="04541-325">Groups Perf first by Computer and then CounterName, and calculates the average (avg).</span></span>

<span data-ttu-id="04541-326">**Example 13**</span><span class="sxs-lookup"><span data-stu-id="04541-326">**Example 13**</span></span>

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

<span data-ttu-id="04541-327">Gets the top five workflows with the maximum number of alerts.</span><span class="sxs-lookup"><span data-stu-id="04541-327">Gets the top five workflows with the maximum number of alerts.</span></span>

<span data-ttu-id="04541-328">**Example 14**</span><span class="sxs-lookup"><span data-stu-id="04541-328">**Example 14**</span></span>

    * <span data-ttu-id="04541-329">| measure countdistinct(Computer) by Type</span><span class="sxs-lookup"><span data-stu-id="04541-329">| measure countdistinct(Computer) by Type</span></span>

<span data-ttu-id="04541-330">Counts the number of unique computers reporting for each Type.</span><span class="sxs-lookup"><span data-stu-id="04541-330">Counts the number of unique computers reporting for each Type.</span></span>

<span data-ttu-id="04541-331">**Example 15**</span><span class="sxs-lookup"><span data-stu-id="04541-331">**Example 15**</span></span>

    * <span data-ttu-id="04541-332">| measure countdistinct(Computer) Interval 1HOUR</span><span class="sxs-lookup"><span data-stu-id="04541-332">| measure countdistinct(Computer) Interval 1HOUR</span></span>

<span data-ttu-id="04541-333">Counts the number of unique computers reporting for every hour.</span><span class="sxs-lookup"><span data-stu-id="04541-333">Counts the number of unique computers reporting for every hour.</span></span>

<span data-ttu-id="04541-334">**Example 16**</span><span class="sxs-lookup"><span data-stu-id="04541-334">**Example 16**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

<span data-ttu-id="04541-335">Groups % Processor Time by Computer, and returns the average for every hour.</span><span class="sxs-lookup"><span data-stu-id="04541-335">Groups % Processor Time by Computer, and returns the average for every hour.</span></span>

<span data-ttu-id="04541-336">**Example 17**</span><span class="sxs-lookup"><span data-stu-id="04541-336">**Example 17**</span></span>

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

<span data-ttu-id="04541-337">Groups W3CIISLog by method, and returns the maximum for every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="04541-337">Groups W3CIISLog by method, and returns the maximum for every 5 minutes.</span></span>

<span data-ttu-id="04541-338">**Example 18**</span><span class="sxs-lookup"><span data-stu-id="04541-338">**Example 18**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

<span data-ttu-id="04541-339">Groups % Processor Time by computer, and returns the minimum, average, 75th percentile, and maximum for every hour.</span><span class="sxs-lookup"><span data-stu-id="04541-339">Groups % Processor Time by computer, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="04541-340">**Example 19**</span><span class="sxs-lookup"><span data-stu-id="04541-340">**Example 19**</span></span>

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

<span data-ttu-id="04541-341">Groups % Processor Time first by computer and then by Instance name, and returns the minimum, average, 75th percentile, and maximum for every hour.</span><span class="sxs-lookup"><span data-stu-id="04541-341">Groups % Processor Time first by computer and then by Instance name, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="04541-342">**Example 20**</span><span class="sxs-lookup"><span data-stu-id="04541-342">**Example 20**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

<span data-ttu-id="04541-343">Calculates the maximum of disk writes per minute for every disk on your computer.</span><span class="sxs-lookup"><span data-stu-id="04541-343">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

### <a name="where"></a><span data-ttu-id="04541-344">Where</span><span class="sxs-lookup"><span data-stu-id="04541-344">Where</span></span>
<span data-ttu-id="04541-345">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-345">Syntax:</span></span>

```
**where** AggregatedValue>20
```

<span data-ttu-id="04541-346">Can only be used after a *Measure* command to further filter the aggregated results that the *Measure* aggregation function has produced.</span><span class="sxs-lookup"><span data-stu-id="04541-346">Can only be used after a *Measure* command to further filter the aggregated results that the *Measure* aggregation function has produced.</span></span>

<span data-ttu-id="04541-347">Examples:</span><span class="sxs-lookup"><span data-stu-id="04541-347">Examples:</span></span>

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a><span data-ttu-id="04541-348">Dedup</span><span class="sxs-lookup"><span data-stu-id="04541-348">Dedup</span></span>
<span data-ttu-id="04541-349">Syntax:</span><span class="sxs-lookup"><span data-stu-id="04541-349">Syntax:</span></span>

    Dedup FieldName

<span data-ttu-id="04541-350">Returns the first document found for every unique value of the given field.</span><span class="sxs-lookup"><span data-stu-id="04541-350">Returns the first document found for every unique value of the given field.</span></span>

<span data-ttu-id="04541-351">Example:</span><span class="sxs-lookup"><span data-stu-id="04541-351">Example:</span></span>

    Type=Event | Dedup EventID | sort TimeGenerated DESC

<span data-ttu-id="04541-352">This example returns one event (the latest event) per EventID.</span><span class="sxs-lookup"><span data-stu-id="04541-352">This example returns one event (the latest event) per EventID.</span></span>


### <a name="extend"></a><span data-ttu-id="04541-353">Extend</span><span class="sxs-lookup"><span data-stu-id="04541-353">Extend</span></span>
<span data-ttu-id="04541-354">Allows you to create run-time fields in queries.</span><span class="sxs-lookup"><span data-stu-id="04541-354">Allows you to create run-time fields in queries.</span></span> <span data-ttu-id="04541-355">You can also use the measure command after the extend command if you want to perform aggregation.</span><span class="sxs-lookup"><span data-stu-id="04541-355">You can also use the measure command after the extend command if you want to perform aggregation.</span></span>

<span data-ttu-id="04541-356">**Example 1**</span><span class="sxs-lookup"><span data-stu-id="04541-356">**Example 1**</span></span>

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
<span data-ttu-id="04541-357">Shows weighted recommendation score for SQL Assessment recommendations.</span><span class="sxs-lookup"><span data-stu-id="04541-357">Shows weighted recommendation score for SQL Assessment recommendations.</span></span>

<span data-ttu-id="04541-358">**Example 2**</span><span class="sxs-lookup"><span data-stu-id="04541-358">**Example 2**</span></span>

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
<span data-ttu-id="04541-359">Shows counter value in KBs instead of bytes.</span><span class="sxs-lookup"><span data-stu-id="04541-359">Shows counter value in KBs instead of bytes.</span></span>

<span data-ttu-id="04541-360">**Example 3**</span><span class="sxs-lookup"><span data-stu-id="04541-360">**Example 3**</span></span>

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
<span data-ttu-id="04541-361">Scales the value of WireData TotalBytes, such that all results are between 0 and 100.</span><span class="sxs-lookup"><span data-stu-id="04541-361">Scales the value of WireData TotalBytes, such that all results are between 0 and 100.</span></span>

<span data-ttu-id="04541-362">**Example 4**</span><span class="sxs-lookup"><span data-stu-id="04541-362">**Example 4**</span></span>

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
<span data-ttu-id="04541-363">Tags Perf Counter Values less than 50 percent as LOW, and others as HIGH.</span><span class="sxs-lookup"><span data-stu-id="04541-363">Tags Perf Counter Values less than 50 percent as LOW, and others as HIGH.</span></span>

<span data-ttu-id="04541-364">**Example 5**</span><span class="sxs-lookup"><span data-stu-id="04541-364">**Example 5**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
<span data-ttu-id="04541-365">Calculates the maximum of disk writes per minute for every disk on your computer.</span><span class="sxs-lookup"><span data-stu-id="04541-365">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

<span data-ttu-id="04541-366">**Supported functions**</span><span class="sxs-lookup"><span data-stu-id="04541-366">**Supported functions**</span></span>

| <span data-ttu-id="04541-367">Function</span><span class="sxs-lookup"><span data-stu-id="04541-367">Function</span></span> | <span data-ttu-id="04541-368">Description</span><span class="sxs-lookup"><span data-stu-id="04541-368">Description</span></span> | <span data-ttu-id="04541-369">Syntax examples</span><span class="sxs-lookup"><span data-stu-id="04541-369">Syntax examples</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04541-370">abs</span><span class="sxs-lookup"><span data-stu-id="04541-370">abs</span></span> |<span data-ttu-id="04541-371">Returns the absolute value of the specified value or function.</span><span class="sxs-lookup"><span data-stu-id="04541-371">Returns the absolute value of the specified value or function.</span></span> |`abs(x)` <br> `abs(-5)` |
| <span data-ttu-id="04541-372">acos</span><span class="sxs-lookup"><span data-stu-id="04541-372">acos</span></span> |<span data-ttu-id="04541-373">Returns arc cosine of a value or a function.</span><span class="sxs-lookup"><span data-stu-id="04541-373">Returns arc cosine of a value or a function.</span></span> |`acos(x)` |
| <span data-ttu-id="04541-374">and</span><span class="sxs-lookup"><span data-stu-id="04541-374">and</span></span> |<span data-ttu-id="04541-375">Returns a value of true if and only if all of its operands evaluate to true.</span><span class="sxs-lookup"><span data-stu-id="04541-375">Returns a value of true if and only if all of its operands evaluate to true.</span></span> |`and(not(exists(popularity)),exists(price))` |
| <span data-ttu-id="04541-376">asin</span><span class="sxs-lookup"><span data-stu-id="04541-376">asin</span></span> |<span data-ttu-id="04541-377">Returns arc sine of a value or a function.</span><span class="sxs-lookup"><span data-stu-id="04541-377">Returns arc sine of a value or a function.</span></span> |`asin(x)` |
| <span data-ttu-id="04541-378">atan</span><span class="sxs-lookup"><span data-stu-id="04541-378">atan</span></span> |<span data-ttu-id="04541-379">Returns arc tangent of a value or a function.</span><span class="sxs-lookup"><span data-stu-id="04541-379">Returns arc tangent of a value or a function.</span></span> |`atan(x)` |
| <span data-ttu-id="04541-380">atan2</span><span class="sxs-lookup"><span data-stu-id="04541-380">atan2</span></span> |<span data-ttu-id="04541-381">Returns the angle resulting from the conversion of the rectangular coordinates x,y to polar coordinates.</span><span class="sxs-lookup"><span data-stu-id="04541-381">Returns the angle resulting from the conversion of the rectangular coordinates x,y to polar coordinates.</span></span> |`atan2(x,y)` |
| <span data-ttu-id="04541-382">cbrt</span><span class="sxs-lookup"><span data-stu-id="04541-382">cbrt</span></span> |<span data-ttu-id="04541-383">Cube root.</span><span class="sxs-lookup"><span data-stu-id="04541-383">Cube root.</span></span> |`cbrt(x)` |
| <span data-ttu-id="04541-384">ceil</span><span class="sxs-lookup"><span data-stu-id="04541-384">ceil</span></span> |<span data-ttu-id="04541-385">Rounds up to an integer.</span><span class="sxs-lookup"><span data-stu-id="04541-385">Rounds up to an integer.</span></span> |`ceil(x)`  <br> <span data-ttu-id="04541-386">`ceil(5.6)` Returns 6</span><span class="sxs-lookup"><span data-stu-id="04541-386">`ceil(5.6)` Returns 6</span></span> |
| <span data-ttu-id="04541-387">cos</span><span class="sxs-lookup"><span data-stu-id="04541-387">cos</span></span> |<span data-ttu-id="04541-388">Returns cosine of an angle.</span><span class="sxs-lookup"><span data-stu-id="04541-388">Returns cosine of an angle.</span></span> |`cos(x)` |
| <span data-ttu-id="04541-389">cosh</span><span class="sxs-lookup"><span data-stu-id="04541-389">cosh</span></span> |<span data-ttu-id="04541-390">Returns hyperbolic cosine of an angle.</span><span class="sxs-lookup"><span data-stu-id="04541-390">Returns hyperbolic cosine of an angle.</span></span> |`cosh(x)` |
| <span data-ttu-id="04541-391">def</span><span class="sxs-lookup"><span data-stu-id="04541-391">def</span></span> |<span data-ttu-id="04541-392">Abbreviation for default.</span><span class="sxs-lookup"><span data-stu-id="04541-392">Abbreviation for default.</span></span> <span data-ttu-id="04541-393">Returns the value of field "field".</span><span class="sxs-lookup"><span data-stu-id="04541-393">Returns the value of field "field".</span></span> <span data-ttu-id="04541-394">If the field does not exist, returns the default value specified and yields the first value where: `exists()==true`.</span><span class="sxs-lookup"><span data-stu-id="04541-394">If the field does not exist, returns the default value specified and yields the first value where: `exists()==true`.</span></span> |<span data-ttu-id="04541-395">`def(rating,5)`.</span><span class="sxs-lookup"><span data-stu-id="04541-395">`def(rating,5)`.</span></span> <span data-ttu-id="04541-396">This def() function returns the rating, or if no rating is specified in the document, returns 5.</span><span class="sxs-lookup"><span data-stu-id="04541-396">This def() function returns the rating, or if no rating is specified in the document, returns 5.</span></span> <br> <span data-ttu-id="04541-397">`def(myfield, 1.0)` is equivalent to `if(exists(myfield),myfield,1.0)`.</span><span class="sxs-lookup"><span data-stu-id="04541-397">`def(myfield, 1.0)` is equivalent to `if(exists(myfield),myfield,1.0)`.</span></span> |
| <span data-ttu-id="04541-398">deg</span><span class="sxs-lookup"><span data-stu-id="04541-398">deg</span></span> |<span data-ttu-id="04541-399">Converts radians to degrees.</span><span class="sxs-lookup"><span data-stu-id="04541-399">Converts radians to degrees.</span></span> |`deg(x)` |
| <span data-ttu-id="04541-400">div</span><span class="sxs-lookup"><span data-stu-id="04541-400">div</span></span> |<span data-ttu-id="04541-401">`div(x,y)` divides x by y.</span><span class="sxs-lookup"><span data-stu-id="04541-401">`div(x,y)` divides x by y.</span></span> |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| <span data-ttu-id="04541-402">dist</span><span class="sxs-lookup"><span data-stu-id="04541-402">dist</span></span> |<span data-ttu-id="04541-403">Returns the distance between two vectors, (points) in an n-dimensional space.</span><span class="sxs-lookup"><span data-stu-id="04541-403">Returns the distance between two vectors, (points) in an n-dimensional space.</span></span> <span data-ttu-id="04541-404">Takes in the power, plus two or more, ValueSource instances, and calculates the distances between the two vectors.</span><span class="sxs-lookup"><span data-stu-id="04541-404">Takes in the power, plus two or more, ValueSource instances, and calculates the distances between the two vectors.</span></span> <span data-ttu-id="04541-405">Each ValueSource must be a number.</span><span class="sxs-lookup"><span data-stu-id="04541-405">Each ValueSource must be a number.</span></span> <span data-ttu-id="04541-406">There must be an even number of ValueSource instances passed in, and the method assumes that the first half represent the first vector and the second half represent the second vector.</span><span class="sxs-lookup"><span data-stu-id="04541-406">There must be an even number of ValueSource instances passed in, and the method assumes that the first half represent the first vector and the second half represent the second vector.</span></span> |<span data-ttu-id="04541-407">`dist(2, x, y, 0, 0)` Calculates the Euclidean distance between (0,0) and (x,y) for each document.</span><span class="sxs-lookup"><span data-stu-id="04541-407">`dist(2, x, y, 0, 0)` Calculates the Euclidean distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="04541-408">`dist(1, x, y, 0, 0)` Calculates the Manhattan (taxicab) distance between (0,0) and (x,y) for each document.</span><span class="sxs-lookup"><span data-stu-id="04541-408">`dist(1, x, y, 0, 0)` Calculates the Manhattan (taxicab) distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="04541-409">`dist(2,,x,y,z,0,0,0)` Euclidean distance between (0,0,0) and (x,y,z) for each document.</span><span class="sxs-lookup"><span data-stu-id="04541-409">`dist(2,,x,y,z,0,0,0)` Euclidean distance between (0,0,0) and (x,y,z) for each document.</span></span><br><span data-ttu-id="04541-410">`dist(1,x,y,z,e,f,g)` Manhattan distance between (x,y,z) and (e,f,g), where each letter is a field name.</span><span class="sxs-lookup"><span data-stu-id="04541-410">`dist(1,x,y,z,e,f,g)` Manhattan distance between (x,y,z) and (e,f,g), where each letter is a field name.</span></span> |
| <span data-ttu-id="04541-411">exists</span><span class="sxs-lookup"><span data-stu-id="04541-411">exists</span></span> |<span data-ttu-id="04541-412">Returns TRUE if any member of the field exists.</span><span class="sxs-lookup"><span data-stu-id="04541-412">Returns TRUE if any member of the field exists.</span></span> |<span data-ttu-id="04541-413">`exists(author)` Returns TRUE for any document that has a value in the "author" field.</span><span class="sxs-lookup"><span data-stu-id="04541-413">`exists(author)` Returns TRUE for any document that has a value in the "author" field.</span></span><br><span data-ttu-id="04541-414">`exists(query(price:5.00))` Returns TRUE if "price" matches,"5.00".</span><span class="sxs-lookup"><span data-stu-id="04541-414">`exists(query(price:5.00))` Returns TRUE if "price" matches,"5.00".</span></span> |
| <span data-ttu-id="04541-415">exp</span><span class="sxs-lookup"><span data-stu-id="04541-415">exp</span></span> |<span data-ttu-id="04541-416">Returns Euler's number raised to power x.</span><span class="sxs-lookup"><span data-stu-id="04541-416">Returns Euler's number raised to power x.</span></span> |`exp(x)` |
| <span data-ttu-id="04541-417">floor</span><span class="sxs-lookup"><span data-stu-id="04541-417">floor</span></span> |<span data-ttu-id="04541-418">Rounds down to an integer.</span><span class="sxs-lookup"><span data-stu-id="04541-418">Rounds down to an integer.</span></span> |`floor(x)`  <br> <span data-ttu-id="04541-419">`floor(5.6)` Returns 5</span><span class="sxs-lookup"><span data-stu-id="04541-419">`floor(5.6)` Returns 5</span></span> |
| <span data-ttu-id="04541-420">hypo</span><span class="sxs-lookup"><span data-stu-id="04541-420">hypo</span></span> |<span data-ttu-id="04541-421">Returns sqrt(sum(pow(x,2),pow(y,2))) without intermediate overflow or underflow.</span><span class="sxs-lookup"><span data-stu-id="04541-421">Returns sqrt(sum(pow(x,2),pow(y,2))) without intermediate overflow or underflow.</span></span> |`hypo(x,y)`  <br> ` |
| <span data-ttu-id="04541-422">if</span><span class="sxs-lookup"><span data-stu-id="04541-422">if</span></span> |<span data-ttu-id="04541-423">Enables conditional function queries.</span><span class="sxs-lookup"><span data-stu-id="04541-423">Enables conditional function queries.</span></span> <span data-ttu-id="04541-424">In `if(test,value1,value2)`, test is or refers to a logical value or expression that returns a logical value (TRUE or FALSE).</span><span class="sxs-lookup"><span data-stu-id="04541-424">In `if(test,value1,value2)`, test is or refers to a logical value or expression that returns a logical value (TRUE or FALSE).</span></span> <span data-ttu-id="04541-425">`value1` is the value returned by the function if test yields TRUE.</span><span class="sxs-lookup"><span data-stu-id="04541-425">`value1` is the value returned by the function if test yields TRUE.</span></span> <span data-ttu-id="04541-426">`value2` is the value returned by the function if test yields FALSE.</span><span class="sxs-lookup"><span data-stu-id="04541-426">`value2` is the value returned by the function if test yields FALSE.</span></span> <span data-ttu-id="04541-427">An expression can be any function which outputs boolean values.</span><span class="sxs-lookup"><span data-stu-id="04541-427">An expression can be any function which outputs boolean values.</span></span> <span data-ttu-id="04541-428">It can also be a function returning numeric values, in which case value 0 is interpreted as false, or returning strings, in which case empty string is interpreted as false.</span><span class="sxs-lookup"><span data-stu-id="04541-428">It can also be a function returning numeric values, in which case value 0 is interpreted as false, or returning strings, in which case empty string is interpreted as false.</span></span> |<span data-ttu-id="04541-429">`if(termfreq(cat,'electronics'),popularity,42)` This function checks each document to see if it contains the term "electronics" in the cat field.</span><span class="sxs-lookup"><span data-stu-id="04541-429">`if(termfreq(cat,'electronics'),popularity,42)` This function checks each document to see if it contains the term "electronics" in the cat field.</span></span> <span data-ttu-id="04541-430">If it does, then the value of the popularity field is returned.</span><span class="sxs-lookup"><span data-stu-id="04541-430">If it does, then the value of the popularity field is returned.</span></span> <span data-ttu-id="04541-431">Otherwise, the value of 42 is returned.</span><span class="sxs-lookup"><span data-stu-id="04541-431">Otherwise, the value of 42 is returned.</span></span> |
| <span data-ttu-id="04541-432">linear</span><span class="sxs-lookup"><span data-stu-id="04541-432">linear</span></span> |<span data-ttu-id="04541-433">Implements `m*x+c`, where m and c are constants, and x is an arbitrary function.</span><span class="sxs-lookup"><span data-stu-id="04541-433">Implements `m*x+c`, where m and c are constants, and x is an arbitrary function.</span></span> <span data-ttu-id="04541-434">This is equivalent to `sum(product(m,x),c)`, but slightly more efficient as it is implemented as a single function.</span><span class="sxs-lookup"><span data-stu-id="04541-434">This is equivalent to `sum(product(m,x),c)`, but slightly more efficient as it is implemented as a single function.</span></span> |<span data-ttu-id="04541-435">`linear(x,m,c) linear(x,2,4)` returns `2*x+4`</span><span class="sxs-lookup"><span data-stu-id="04541-435">`linear(x,m,c) linear(x,2,4)` returns `2*x+4`</span></span> |
| <span data-ttu-id="04541-436">ln</span><span class="sxs-lookup"><span data-stu-id="04541-436">ln</span></span> |<span data-ttu-id="04541-437">Returns the natural log of the specified function.</span><span class="sxs-lookup"><span data-stu-id="04541-437">Returns the natural log of the specified function.</span></span> |`ln(x)` |
| <span data-ttu-id="04541-438">log</span><span class="sxs-lookup"><span data-stu-id="04541-438">log</span></span> |<span data-ttu-id="04541-439">Returns the log base 10 of the specified function.</span><span class="sxs-lookup"><span data-stu-id="04541-439">Returns the log base 10 of the specified function.</span></span> |`log(x)   log(sum(x,100))` |
| <span data-ttu-id="04541-440">map</span><span class="sxs-lookup"><span data-stu-id="04541-440">map</span></span> |<span data-ttu-id="04541-441">Maps any values of an input function x that fall within min and max, inclusive to the specified target.</span><span class="sxs-lookup"><span data-stu-id="04541-441">Maps any values of an input function x that fall within min and max, inclusive to the specified target.</span></span> <span data-ttu-id="04541-442">The arguments min and max must be constants.</span><span class="sxs-lookup"><span data-stu-id="04541-442">The arguments min and max must be constants.</span></span> <span data-ttu-id="04541-443">The arguments target and default can be constants or functions.</span><span class="sxs-lookup"><span data-stu-id="04541-443">The arguments target and default can be constants or functions.</span></span> <span data-ttu-id="04541-444">If the value of x does not fall between min and max, then either the value of x is returned, or a default value is returned if specified as a 5th argument.</span><span class="sxs-lookup"><span data-stu-id="04541-444">If the value of x does not fall between min and max, then either the value of x is returned, or a default value is returned if specified as a 5th argument.</span></span> |<span data-ttu-id="04541-445">`map(x,min,max,target) map(x,0,0,1)` Changes any values of 0 to 1.</span><span class="sxs-lookup"><span data-stu-id="04541-445">`map(x,min,max,target) map(x,0,0,1)` Changes any values of 0 to 1.</span></span> <span data-ttu-id="04541-446">This can be useful in handling default 0 values.</span><span class="sxs-lookup"><span data-stu-id="04541-446">This can be useful in handling default 0 values.</span></span><br> <span data-ttu-id="04541-447">`map(x,min,max,target,default)    map(x,0,100,1,-1)` Changes any values between 0 and 100 to 1, and all other values to -1.</span><span class="sxs-lookup"><span data-stu-id="04541-447">`map(x,min,max,target,default)    map(x,0,100,1,-1)` Changes any values between 0 and 100 to 1, and all other values to -1.</span></span><br>  <span data-ttu-id="04541-448">`map(x,0,100,sum(x,599),docfreq(text,solr))` Changes any values between 0 and 100 to x+599, and all other values to frequency of the term 'solr' in the field text.</span><span class="sxs-lookup"><span data-stu-id="04541-448">`map(x,0,100,sum(x,599),docfreq(text,solr))` Changes any values between 0 and 100 to x+599, and all other values to frequency of the term 'solr' in the field text.</span></span> |
| <span data-ttu-id="04541-449">max</span><span class="sxs-lookup"><span data-stu-id="04541-449">max</span></span> |<span data-ttu-id="04541-450">Returns the maximum numeric value of multiple nested functions or constants, which are specified as arguments: `max(x,y,...)`.</span><span class="sxs-lookup"><span data-stu-id="04541-450">Returns the maximum numeric value of multiple nested functions or constants, which are specified as arguments: `max(x,y,...)`.</span></span> <span data-ttu-id="04541-451">The max function can also be useful for "bottoming out" another function or field at some specified constant.</span><span class="sxs-lookup"><span data-stu-id="04541-451">The max function can also be useful for "bottoming out" another function or field at some specified constant.</span></span>  <span data-ttu-id="04541-452">Use the `field(myfield,max)` syntax for selecting the maximum value of a single multivalued field.</span><span class="sxs-lookup"><span data-stu-id="04541-452">Use the `field(myfield,max)` syntax for selecting the maximum value of a single multivalued field.</span></span> |`max(myfield,myotherfield,0)` |
| <span data-ttu-id="04541-453">min</span><span class="sxs-lookup"><span data-stu-id="04541-453">min</span></span> |<span data-ttu-id="04541-454">Returns the minimum numeric value of multiple nested functions of constants, which are specified as arguments: `min(x,y,...)`.</span><span class="sxs-lookup"><span data-stu-id="04541-454">Returns the minimum numeric value of multiple nested functions of constants, which are specified as arguments: `min(x,y,...)`.</span></span> <span data-ttu-id="04541-455">The min function can also be useful for providing an "upper bound" on a function using a constant.</span><span class="sxs-lookup"><span data-stu-id="04541-455">The min function can also be useful for providing an "upper bound" on a function using a constant.</span></span> <span data-ttu-id="04541-456">Use the `field(myfield,min)` syntax for selecting the minimum value of a single multivalued field.</span><span class="sxs-lookup"><span data-stu-id="04541-456">Use the `field(myfield,min)` syntax for selecting the minimum value of a single multivalued field.</span></span> |`min(myfield,myotherfield,0)` |
| <span data-ttu-id="04541-457">mod</span><span class="sxs-lookup"><span data-stu-id="04541-457">mod</span></span> |<span data-ttu-id="04541-458">Computes the modulus of the function x by the function y.</span><span class="sxs-lookup"><span data-stu-id="04541-458">Computes the modulus of the function x by the function y.</span></span> |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| <span data-ttu-id="04541-459">ms</span><span class="sxs-lookup"><span data-stu-id="04541-459">ms</span></span> |<span data-ttu-id="04541-460">Returns milliseconds of difference between its arguments.</span><span class="sxs-lookup"><span data-stu-id="04541-460">Returns milliseconds of difference between its arguments.</span></span> <span data-ttu-id="04541-461">Dates are relative to the Unix or POSIX time epoch, midnight, January 1, 1970 UTC.</span><span class="sxs-lookup"><span data-stu-id="04541-461">Dates are relative to the Unix or POSIX time epoch, midnight, January 1, 1970 UTC.</span></span> <span data-ttu-id="04541-462">Arguments may be the name of an indexed TrieDateField, or date math based on a constant date or NOW .</span><span class="sxs-lookup"><span data-stu-id="04541-462">Arguments may be the name of an indexed TrieDateField, or date math based on a constant date or NOW .</span></span> <span data-ttu-id="04541-463">`ms()` is equivalent to `ms(NOW)`, number of milliseconds since the epoch.</span><span class="sxs-lookup"><span data-stu-id="04541-463">`ms()` is equivalent to `ms(NOW)`, number of milliseconds since the epoch.</span></span> <span data-ttu-id="04541-464">`ms(a)` returns the number of milliseconds since the epoch that the argument represents.</span><span class="sxs-lookup"><span data-stu-id="04541-464">`ms(a)` returns the number of milliseconds since the epoch that the argument represents.</span></span> <span data-ttu-id="04541-465">`ms(a,b)` returns the number of milliseconds that b occurs before a, which is `a - b`.</span><span class="sxs-lookup"><span data-stu-id="04541-465">`ms(a,b)` returns the number of milliseconds that b occurs before a, which is `a - b`.</span></span> |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| <span data-ttu-id="04541-466">not</span><span class="sxs-lookup"><span data-stu-id="04541-466">not</span></span> |<span data-ttu-id="04541-467">The logically negated value of the wrapped function.</span><span class="sxs-lookup"><span data-stu-id="04541-467">The logically negated value of the wrapped function.</span></span> |<span data-ttu-id="04541-468">`not(exists(author))` TRUE only when `exists(author)` is false.</span><span class="sxs-lookup"><span data-stu-id="04541-468">`not(exists(author))` TRUE only when `exists(author)` is false.</span></span> |
| <span data-ttu-id="04541-469">or</span><span class="sxs-lookup"><span data-stu-id="04541-469">or</span></span> |<span data-ttu-id="04541-470">A logical disjunction.</span><span class="sxs-lookup"><span data-stu-id="04541-470">A logical disjunction.</span></span> |<span data-ttu-id="04541-471">`or(value1,value2)` TRUE if either value1 or value2 is true.</span><span class="sxs-lookup"><span data-stu-id="04541-471">`or(value1,value2)` TRUE if either value1 or value2 is true.</span></span> |
| <span data-ttu-id="04541-472">pow</span><span class="sxs-lookup"><span data-stu-id="04541-472">pow</span></span> |<span data-ttu-id="04541-473">Raises the specified base to the specified power.</span><span class="sxs-lookup"><span data-stu-id="04541-473">Raises the specified base to the specified power.</span></span> <span data-ttu-id="04541-474">`pow(x,y)` raises x to the power of y.</span><span class="sxs-lookup"><span data-stu-id="04541-474">`pow(x,y)` raises x to the power of y.</span></span> |`pow(x,y)`<br>`pow(x,log(y))`<br><span data-ttu-id="04541-475">`pow(x,0.5)` The same as sqrt.</span><span class="sxs-lookup"><span data-stu-id="04541-475">`pow(x,0.5)` The same as sqrt.</span></span> |
| <span data-ttu-id="04541-476">product</span><span class="sxs-lookup"><span data-stu-id="04541-476">product</span></span> |<span data-ttu-id="04541-477">Returns the product of multiple values or functions, which are specified in a comma-separated list.</span><span class="sxs-lookup"><span data-stu-id="04541-477">Returns the product of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="04541-478">`mul(...)` may also be used as an alias for this function.</span><span class="sxs-lookup"><span data-stu-id="04541-478">`mul(...)` may also be used as an alias for this function.</span></span> |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| <span data-ttu-id="04541-479">recip</span><span class="sxs-lookup"><span data-stu-id="04541-479">recip</span></span> |<span data-ttu-id="04541-480">Performs a reciprocal function with `recip(x,m,a,b)` implementing `a/(m*x+b)`, where m, a,and b are constants, and x is any arbitrarily complex function.</span><span class="sxs-lookup"><span data-stu-id="04541-480">Performs a reciprocal function with `recip(x,m,a,b)` implementing `a/(m*x+b)`, where m, a,and b are constants, and x is any arbitrarily complex function.</span></span> <span data-ttu-id="04541-481">When a and b are equal, and x>=0, this function has a maximum value of 1 that drops as x increases.</span><span class="sxs-lookup"><span data-stu-id="04541-481">When a and b are equal, and x>=0, this function has a maximum value of 1 that drops as x increases.</span></span> <span data-ttu-id="04541-482">Increasing the value of a and b together results in a movement of the entire function to a flatter part of the curve.</span><span class="sxs-lookup"><span data-stu-id="04541-482">Increasing the value of a and b together results in a movement of the entire function to a flatter part of the curve.</span></span> <span data-ttu-id="04541-483">These properties can make this an ideal function for boosting more recent documents when x is `rord(datefield)`.</span><span class="sxs-lookup"><span data-stu-id="04541-483">These properties can make this an ideal function for boosting more recent documents when x is `rord(datefield)`.</span></span> |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| <span data-ttu-id="04541-484">rad</span><span class="sxs-lookup"><span data-stu-id="04541-484">rad</span></span> |<span data-ttu-id="04541-485">Converts degrees to radians.</span><span class="sxs-lookup"><span data-stu-id="04541-485">Converts degrees to radians.</span></span> |`rad(x)` |
| <span data-ttu-id="04541-486">rint</span><span class="sxs-lookup"><span data-stu-id="04541-486">rint</span></span> |<span data-ttu-id="04541-487">Rounds to the nearest integer.</span><span class="sxs-lookup"><span data-stu-id="04541-487">Rounds to the nearest integer.</span></span> |`rint(x)`  <br> <span data-ttu-id="04541-488">`rint(5.6)` Returns 6</span><span class="sxs-lookup"><span data-stu-id="04541-488">`rint(5.6)` Returns 6</span></span> |
| <span data-ttu-id="04541-489">sin</span><span class="sxs-lookup"><span data-stu-id="04541-489">sin</span></span> |<span data-ttu-id="04541-490">Returns sine of an angle.</span><span class="sxs-lookup"><span data-stu-id="04541-490">Returns sine of an angle.</span></span> |`sin(x)` |
| <span data-ttu-id="04541-491">sinh</span><span class="sxs-lookup"><span data-stu-id="04541-491">sinh</span></span> |<span data-ttu-id="04541-492">Returns hyperbolic sine of an angle.</span><span class="sxs-lookup"><span data-stu-id="04541-492">Returns hyperbolic sine of an angle.</span></span> |`sinh(x)` |
| <span data-ttu-id="04541-493">scale</span><span class="sxs-lookup"><span data-stu-id="04541-493">scale</span></span> |<span data-ttu-id="04541-494">Scales values of the function x, such that they fall between the specified minTarget and maxTarget inclusive.</span><span class="sxs-lookup"><span data-stu-id="04541-494">Scales values of the function x, such that they fall between the specified minTarget and maxTarget inclusive.</span></span> <span data-ttu-id="04541-495">The current implementation traverses all of the function values to obtain the min and max, so it can pick the correct scale.</span><span class="sxs-lookup"><span data-stu-id="04541-495">The current implementation traverses all of the function values to obtain the min and max, so it can pick the correct scale.</span></span> <span data-ttu-id="04541-496">The current implementation cannot distinguish when documents have been deleted, or documents that have no value.</span><span class="sxs-lookup"><span data-stu-id="04541-496">The current implementation cannot distinguish when documents have been deleted, or documents that have no value.</span></span> <span data-ttu-id="04541-497">It uses 0.0 values for these cases.</span><span class="sxs-lookup"><span data-stu-id="04541-497">It uses 0.0 values for these cases.</span></span> <span data-ttu-id="04541-498">This means that if values are normally all greater than 0.0, one can still end up with 0.0 as the min value to map from.</span><span class="sxs-lookup"><span data-stu-id="04541-498">This means that if values are normally all greater than 0.0, one can still end up with 0.0 as the min value to map from.</span></span> <span data-ttu-id="04541-499">In these cases, an appropriate `map()` function could be used as a workaround to change 0.0 to a value in the real range, as shown here: `scale(map(x,0,0,5),1,2)`</span><span class="sxs-lookup"><span data-stu-id="04541-499">In these cases, an appropriate `map()` function could be used as a workaround to change 0.0 to a value in the real range, as shown here: `scale(map(x,0,0,5),1,2)`</span></span> |`scale(x,minTarget,maxTarget)`<br><span data-ttu-id="04541-500">`scale(x,1,2)` Scales the values of x, such that all values are between 1 and 2 inclusive.</span><span class="sxs-lookup"><span data-stu-id="04541-500">`scale(x,1,2)` Scales the values of x, such that all values are between 1 and 2 inclusive.</span></span> |
| <span data-ttu-id="04541-501">sqrt</span><span class="sxs-lookup"><span data-stu-id="04541-501">sqrt</span></span> |<span data-ttu-id="04541-502">Returns the square root of the specified value or function.</span><span class="sxs-lookup"><span data-stu-id="04541-502">Returns the square root of the specified value or function.</span></span> |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| <span data-ttu-id="04541-503">strdist</span><span class="sxs-lookup"><span data-stu-id="04541-503">strdist</span></span> |<span data-ttu-id="04541-504">Calculates the distance between two strings.</span><span class="sxs-lookup"><span data-stu-id="04541-504">Calculates the distance between two strings.</span></span> <span data-ttu-id="04541-505">Uses the Lucene spell checker StringDistance interface, and supports all of the implementations available in that package.</span><span class="sxs-lookup"><span data-stu-id="04541-505">Uses the Lucene spell checker StringDistance interface, and supports all of the implementations available in that package.</span></span> <span data-ttu-id="04541-506">Also allows applications to plug in their own, via Solr's resource loading capabilities.</span><span class="sxs-lookup"><span data-stu-id="04541-506">Also allows applications to plug in their own, via Solr's resource loading capabilities.</span></span> <span data-ttu-id="04541-507">strdist takes `(string1, string2, distance measure)`.</span><span class="sxs-lookup"><span data-stu-id="04541-507">strdist takes `(string1, string2, distance measure)`.</span></span> <span data-ttu-id="04541-508">Possible values for distance measure are:</span><span class="sxs-lookup"><span data-stu-id="04541-508">Possible values for distance measure are:</span></span><ul><li><span data-ttu-id="04541-509">jw: Jaro-Winkler</span><span class="sxs-lookup"><span data-stu-id="04541-509">jw: Jaro-Winkler</span></span></li><li><span data-ttu-id="04541-510">edit: Levenstein or Edit distance</span><span class="sxs-lookup"><span data-stu-id="04541-510">edit: Levenstein or Edit distance</span></span></li><li><span data-ttu-id="04541-511">ngram: The NGramDistance, if specified, can optionally pass in the ngram size too.</span><span class="sxs-lookup"><span data-stu-id="04541-511">ngram: The NGramDistance, if specified, can optionally pass in the ngram size too.</span></span> <span data-ttu-id="04541-512">Default is 2.</span><span class="sxs-lookup"><span data-stu-id="04541-512">Default is 2.</span></span></li><li><span data-ttu-id="04541-513">FQN: Fully Qualified class Name for an implementation of the StringDistance interface.</span><span class="sxs-lookup"><span data-stu-id="04541-513">FQN: Fully Qualified class Name for an implementation of the StringDistance interface.</span></span> <span data-ttu-id="04541-514">Must have a no-arg constructor.</span><span class="sxs-lookup"><span data-stu-id="04541-514">Must have a no-arg constructor.</span></span></li></ul> |`strdist("SOLR",id,edit)` |
| <span data-ttu-id="04541-515">sub</span><span class="sxs-lookup"><span data-stu-id="04541-515">sub</span></span> |<span data-ttu-id="04541-516">Returns x-y from `sub(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="04541-516">Returns x-y from `sub(x,y)`.</span></span> |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| <span data-ttu-id="04541-517">sum</span><span class="sxs-lookup"><span data-stu-id="04541-517">sum</span></span> |<span data-ttu-id="04541-518">Returns the sum of multiple values or functions, which are specified in a comma-separated list.</span><span class="sxs-lookup"><span data-stu-id="04541-518">Returns the sum of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="04541-519">`add(...)` may be used as an alias for this function.</span><span class="sxs-lookup"><span data-stu-id="04541-519">`add(...)` may be used as an alias for this function.</span></span> |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| <span data-ttu-id="04541-520">termfreq</span><span class="sxs-lookup"><span data-stu-id="04541-520">termfreq</span></span> |<span data-ttu-id="04541-521">Returns the number of times the term appears in the field for that document.</span><span class="sxs-lookup"><span data-stu-id="04541-521">Returns the number of times the term appears in the field for that document.</span></span> |<span data-ttu-id="04541-522">termfreq(text,'memory')</span><span class="sxs-lookup"><span data-stu-id="04541-522">termfreq(text,'memory')</span></span> |
| <span data-ttu-id="04541-523">tan</span><span class="sxs-lookup"><span data-stu-id="04541-523">tan</span></span> |<span data-ttu-id="04541-524">Returns tangent of an angle.</span><span class="sxs-lookup"><span data-stu-id="04541-524">Returns tangent of an angle.</span></span> |`tan(x)` |
| <span data-ttu-id="04541-525">tanh</span><span class="sxs-lookup"><span data-stu-id="04541-525">tanh</span></span> |<span data-ttu-id="04541-526">Returns hyperbolic tangent of an angle.</span><span class="sxs-lookup"><span data-stu-id="04541-526">Returns hyperbolic tangent of an angle.</span></span> |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a><span data-ttu-id="04541-527">Search field and facet reference</span><span class="sxs-lookup"><span data-stu-id="04541-527">Search field and facet reference</span></span>
<span data-ttu-id="04541-528">When you use Log Search to find data, results display various field and facets.</span><span class="sxs-lookup"><span data-stu-id="04541-528">When you use Log Search to find data, results display various field and facets.</span></span> <span data-ttu-id="04541-529">Some of the information might not appear very descriptive.</span><span class="sxs-lookup"><span data-stu-id="04541-529">Some of the information might not appear very descriptive.</span></span> <span data-ttu-id="04541-530">Use the following information to help you understand the results.</span><span class="sxs-lookup"><span data-stu-id="04541-530">Use the following information to help you understand the results.</span></span>

| <span data-ttu-id="04541-531">Field</span><span class="sxs-lookup"><span data-stu-id="04541-531">Field</span></span> | <span data-ttu-id="04541-532">Search type</span><span class="sxs-lookup"><span data-stu-id="04541-532">Search type</span></span> | <span data-ttu-id="04541-533">Description</span><span class="sxs-lookup"><span data-stu-id="04541-533">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04541-534">TenantId</span><span class="sxs-lookup"><span data-stu-id="04541-534">TenantId</span></span> |<span data-ttu-id="04541-535">All</span><span class="sxs-lookup"><span data-stu-id="04541-535">All</span></span> |<span data-ttu-id="04541-536">Used to partition data.</span><span class="sxs-lookup"><span data-stu-id="04541-536">Used to partition data.</span></span> |
| <span data-ttu-id="04541-537">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="04541-537">TimeGenerated</span></span> |<span data-ttu-id="04541-538">All</span><span class="sxs-lookup"><span data-stu-id="04541-538">All</span></span> |<span data-ttu-id="04541-539">Used to drive the timeline, timeselectors (in search and in other screens).</span><span class="sxs-lookup"><span data-stu-id="04541-539">Used to drive the timeline, timeselectors (in search and in other screens).</span></span> <span data-ttu-id="04541-540">It represents when the piece of data was generated (typically on the agent).</span><span class="sxs-lookup"><span data-stu-id="04541-540">It represents when the piece of data was generated (typically on the agent).</span></span> <span data-ttu-id="04541-541">The time is expressed in ISO format, and is always UTC.</span><span class="sxs-lookup"><span data-stu-id="04541-541">The time is expressed in ISO format, and is always UTC.</span></span> <span data-ttu-id="04541-542">In the case of types that are based on existing instrumentation (that is, events in a log), this is typically the real time that the log entry/line/record was logged.</span><span class="sxs-lookup"><span data-stu-id="04541-542">In the case of types that are based on existing instrumentation (that is, events in a log), this is typically the real time that the log entry/line/record was logged.</span></span> <span data-ttu-id="04541-543">For some of the other types that are produced either via management packs or in the cloud (for example, recommendations or alerts), the time represents something different.</span><span class="sxs-lookup"><span data-stu-id="04541-543">For some of the other types that are produced either via management packs or in the cloud (for example, recommendations or alerts), the time represents something different.</span></span> <span data-ttu-id="04541-544">This is the time when this new piece of data with a snapshot of a configuration of some sort was collected, or a recommendation/alert was produced based on it.</span><span class="sxs-lookup"><span data-stu-id="04541-544">This is the time when this new piece of data with a snapshot of a configuration of some sort was collected, or a recommendation/alert was produced based on it.</span></span> |
| <span data-ttu-id="04541-545">EventID</span><span class="sxs-lookup"><span data-stu-id="04541-545">EventID</span></span> |<span data-ttu-id="04541-546">Event</span><span class="sxs-lookup"><span data-stu-id="04541-546">Event</span></span> |<span data-ttu-id="04541-547">EventID in the Windows event log.</span><span class="sxs-lookup"><span data-stu-id="04541-547">EventID in the Windows event log.</span></span> |
| <span data-ttu-id="04541-548">EventLog</span><span class="sxs-lookup"><span data-stu-id="04541-548">EventLog</span></span> |<span data-ttu-id="04541-549">Event</span><span class="sxs-lookup"><span data-stu-id="04541-549">Event</span></span> |<span data-ttu-id="04541-550">Event log where the event was logged by Windows.</span><span class="sxs-lookup"><span data-stu-id="04541-550">Event log where the event was logged by Windows.</span></span> |
| <span data-ttu-id="04541-551">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="04541-551">EventLevelName</span></span> |<span data-ttu-id="04541-552">Event</span><span class="sxs-lookup"><span data-stu-id="04541-552">Event</span></span> |<span data-ttu-id="04541-553">Critical/warning/information/success</span><span class="sxs-lookup"><span data-stu-id="04541-553">Critical/warning/information/success</span></span> |
| <span data-ttu-id="04541-554">EventLevel</span><span class="sxs-lookup"><span data-stu-id="04541-554">EventLevel</span></span> |<span data-ttu-id="04541-555">Event</span><span class="sxs-lookup"><span data-stu-id="04541-555">Event</span></span> |<span data-ttu-id="04541-556">Numerical value for critical/warning/information/success (use EventLevelName instead for easier/more readable queries).</span><span class="sxs-lookup"><span data-stu-id="04541-556">Numerical value for critical/warning/information/success (use EventLevelName instead for easier/more readable queries).</span></span> |
| <span data-ttu-id="04541-557">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="04541-557">SourceSystem</span></span> |<span data-ttu-id="04541-558">All</span><span class="sxs-lookup"><span data-stu-id="04541-558">All</span></span> |<span data-ttu-id="04541-559">Where the data comes from (in terms of attach mode to the service).</span><span class="sxs-lookup"><span data-stu-id="04541-559">Where the data comes from (in terms of attach mode to the service).</span></span> <span data-ttu-id="04541-560">Examples include Microsoft System Center Operations Manager and Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="04541-560">Examples include Microsoft System Center Operations Manager and Azure Storage.</span></span> |
| <span data-ttu-id="04541-561">ObjectName</span><span class="sxs-lookup"><span data-stu-id="04541-561">ObjectName</span></span> |<span data-ttu-id="04541-562">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="04541-562">PerfHourly</span></span> |<span data-ttu-id="04541-563">Windows performance object name.</span><span class="sxs-lookup"><span data-stu-id="04541-563">Windows performance object name.</span></span> |
| <span data-ttu-id="04541-564">InstanceName</span><span class="sxs-lookup"><span data-stu-id="04541-564">InstanceName</span></span> |<span data-ttu-id="04541-565">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="04541-565">PerfHourly</span></span> |<span data-ttu-id="04541-566">Windows performance counter instance name.</span><span class="sxs-lookup"><span data-stu-id="04541-566">Windows performance counter instance name.</span></span> |
| <span data-ttu-id="04541-567">CounteName</span><span class="sxs-lookup"><span data-stu-id="04541-567">CounteName</span></span> |<span data-ttu-id="04541-568">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="04541-568">PerfHourly</span></span> |<span data-ttu-id="04541-569">Windows performance counter name.</span><span class="sxs-lookup"><span data-stu-id="04541-569">Windows performance counter name.</span></span> |
| <span data-ttu-id="04541-570">ObjectDisplayName</span><span class="sxs-lookup"><span data-stu-id="04541-570">ObjectDisplayName</span></span> |<span data-ttu-id="04541-571">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="04541-571">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="04541-572">Display name of the object targeted by a performance collection rule in Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="04541-572">Display name of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="04541-573">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span><span class="sxs-lookup"><span data-stu-id="04541-573">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="04541-574">RootObjectName</span><span class="sxs-lookup"><span data-stu-id="04541-574">RootObjectName</span></span> |<span data-ttu-id="04541-575">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="04541-575">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="04541-576">Display name of the parent of the parent (in a double hosting relationship) of the object targeted by a performance collection rule in Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="04541-576">Display name of the parent of the parent (in a double hosting relationship) of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="04541-577">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span><span class="sxs-lookup"><span data-stu-id="04541-577">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="04541-578">Computer</span><span class="sxs-lookup"><span data-stu-id="04541-578">Computer</span></span> |<span data-ttu-id="04541-579">Most types</span><span class="sxs-lookup"><span data-stu-id="04541-579">Most types</span></span> |<span data-ttu-id="04541-580">Computer name that the data belongs to.</span><span class="sxs-lookup"><span data-stu-id="04541-580">Computer name that the data belongs to.</span></span> |
| <span data-ttu-id="04541-581">DeviceName</span><span class="sxs-lookup"><span data-stu-id="04541-581">DeviceName</span></span> |<span data-ttu-id="04541-582">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="04541-582">ProtectionStatus</span></span> |<span data-ttu-id="04541-583">Computer name the data belongs to (same as "Computer").</span><span class="sxs-lookup"><span data-stu-id="04541-583">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="04541-584">DetectionId</span><span class="sxs-lookup"><span data-stu-id="04541-584">DetectionId</span></span> |<span data-ttu-id="04541-585">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="04541-585">ProtectionStatus</span></span> | |
| <span data-ttu-id="04541-586">ThreatStatusRank</span><span class="sxs-lookup"><span data-stu-id="04541-586">ThreatStatusRank</span></span> |<span data-ttu-id="04541-587">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="04541-587">ProtectionStatus</span></span> |<span data-ttu-id="04541-588">Threat status rank is a numerical representation of the threat status.</span><span class="sxs-lookup"><span data-stu-id="04541-588">Threat status rank is a numerical representation of the threat status.</span></span> <span data-ttu-id="04541-589">Similar to HTTP response codes, the ranking has gaps between the numbers (which is why no threats is 150 and not 100 or 0), leaving room to add new states.</span><span class="sxs-lookup"><span data-stu-id="04541-589">Similar to HTTP response codes, the ranking has gaps between the numbers (which is why no threats is 150 and not 100 or 0), leaving room to add new states.</span></span> <span data-ttu-id="04541-590">For a rollup of threat status and protection status, the intention is to show the worst state that the computer has been in during the selected time period.</span><span class="sxs-lookup"><span data-stu-id="04541-590">For a rollup of threat status and protection status, the intention is to show the worst state that the computer has been in during the selected time period.</span></span> <span data-ttu-id="04541-591">The numbers rank the different states, so you can look for the record with the highest number.</span><span class="sxs-lookup"><span data-stu-id="04541-591">The numbers rank the different states, so you can look for the record with the highest number.</span></span> |
| <span data-ttu-id="04541-592">ThreatStatus</span><span class="sxs-lookup"><span data-stu-id="04541-592">ThreatStatus</span></span> |<span data-ttu-id="04541-593">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="04541-593">ProtectionStatus</span></span> |<span data-ttu-id="04541-594">Description of ThreatStatus, maps 1:1 with ThreatStatusRank.</span><span class="sxs-lookup"><span data-stu-id="04541-594">Description of ThreatStatus, maps 1:1 with ThreatStatusRank.</span></span> |
| <span data-ttu-id="04541-595">TypeofProtection</span><span class="sxs-lookup"><span data-stu-id="04541-595">TypeofProtection</span></span> |<span data-ttu-id="04541-596">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="04541-596">ProtectionStatus</span></span> |<span data-ttu-id="04541-597">Antimalware product that is detected in the computer: none, Microsoft Malware Removal tool, Forefront, and so on.</span><span class="sxs-lookup"><span data-stu-id="04541-597">Antimalware product that is detected in the computer: none, Microsoft Malware Removal tool, Forefront, and so on.</span></span> |
| <span data-ttu-id="04541-598">ScanDate</span><span class="sxs-lookup"><span data-stu-id="04541-598">ScanDate</span></span> |<span data-ttu-id="04541-599">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="04541-599">ProtectionStatus</span></span> | |
| <span data-ttu-id="04541-600">SourceHealthServiceId</span><span class="sxs-lookup"><span data-stu-id="04541-600">SourceHealthServiceId</span></span> |<span data-ttu-id="04541-601">ProtectionStatus, RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="04541-601">ProtectionStatus, RequiredUpdate</span></span> |<span data-ttu-id="04541-602">HealthService ID for this computer's agent.</span><span class="sxs-lookup"><span data-stu-id="04541-602">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="04541-603">HealthServiceId</span><span class="sxs-lookup"><span data-stu-id="04541-603">HealthServiceId</span></span> |<span data-ttu-id="04541-604">Most types</span><span class="sxs-lookup"><span data-stu-id="04541-604">Most types</span></span> |<span data-ttu-id="04541-605">HealthService ID for this computer's agent.</span><span class="sxs-lookup"><span data-stu-id="04541-605">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="04541-606">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="04541-606">ManagementGroupName</span></span> |<span data-ttu-id="04541-607">Most types</span><span class="sxs-lookup"><span data-stu-id="04541-607">Most types</span></span> |<span data-ttu-id="04541-608">Management Group Name for Operations Manager-attached agents.</span><span class="sxs-lookup"><span data-stu-id="04541-608">Management Group Name for Operations Manager-attached agents.</span></span> <span data-ttu-id="04541-609">Otherwise, it is null/blank.</span><span class="sxs-lookup"><span data-stu-id="04541-609">Otherwise, it is null/blank.</span></span> |
| <span data-ttu-id="04541-610">ObjectType</span><span class="sxs-lookup"><span data-stu-id="04541-610">ObjectType</span></span> |<span data-ttu-id="04541-611">ConfigurationObject</span><span class="sxs-lookup"><span data-stu-id="04541-611">ConfigurationObject</span></span> |<span data-ttu-id="04541-612">Type (as in Operations Manager management pack's type/class) for this object, discovered by Log Analytics configuration assessment.</span><span class="sxs-lookup"><span data-stu-id="04541-612">Type (as in Operations Manager management pack's type/class) for this object, discovered by Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="04541-613">UpdateTitle</span><span class="sxs-lookup"><span data-stu-id="04541-613">UpdateTitle</span></span> |<span data-ttu-id="04541-614">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="04541-614">RequiredUpdate</span></span> |<span data-ttu-id="04541-615">Name of the update that was found not installed.</span><span class="sxs-lookup"><span data-stu-id="04541-615">Name of the update that was found not installed.</span></span> |
| <span data-ttu-id="04541-616">PublishDate</span><span class="sxs-lookup"><span data-stu-id="04541-616">PublishDate</span></span> |<span data-ttu-id="04541-617">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="04541-617">RequiredUpdate</span></span> |<span data-ttu-id="04541-618">When the update was published on Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="04541-618">When the update was published on Microsoft Update.</span></span> |
| <span data-ttu-id="04541-619">Server</span><span class="sxs-lookup"><span data-stu-id="04541-619">Server</span></span> |<span data-ttu-id="04541-620">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="04541-620">RequiredUpdate</span></span> |<span data-ttu-id="04541-621">Computer name the data belongs to (same as "Computer").</span><span class="sxs-lookup"><span data-stu-id="04541-621">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="04541-622">Product</span><span class="sxs-lookup"><span data-stu-id="04541-622">Product</span></span> |<span data-ttu-id="04541-623">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="04541-623">RequiredUpdate</span></span> |<span data-ttu-id="04541-624">Product that the update applies to.</span><span class="sxs-lookup"><span data-stu-id="04541-624">Product that the update applies to.</span></span> |
| <span data-ttu-id="04541-625">UpdateClassification</span><span class="sxs-lookup"><span data-stu-id="04541-625">UpdateClassification</span></span> |<span data-ttu-id="04541-626">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="04541-626">RequiredUpdate</span></span> |<span data-ttu-id="04541-627">Type of update (for example, update rollup or service pack).</span><span class="sxs-lookup"><span data-stu-id="04541-627">Type of update (for example, update rollup or service pack).</span></span> |
| <span data-ttu-id="04541-628">KBID</span><span class="sxs-lookup"><span data-stu-id="04541-628">KBID</span></span> |<span data-ttu-id="04541-629">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="04541-629">RequiredUpdate</span></span> |<span data-ttu-id="04541-630">KB article ID that describes this best practice or update.</span><span class="sxs-lookup"><span data-stu-id="04541-630">KB article ID that describes this best practice or update.</span></span> |
| <span data-ttu-id="04541-631">WorkflowName</span><span class="sxs-lookup"><span data-stu-id="04541-631">WorkflowName</span></span> |<span data-ttu-id="04541-632">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="04541-632">ConfigurationAlert</span></span> |<span data-ttu-id="04541-633">Name of the rule or monitor that produced the alert.</span><span class="sxs-lookup"><span data-stu-id="04541-633">Name of the rule or monitor that produced the alert.</span></span> |
| <span data-ttu-id="04541-634">Severity</span><span class="sxs-lookup"><span data-stu-id="04541-634">Severity</span></span> |<span data-ttu-id="04541-635">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="04541-635">ConfigurationAlert</span></span> |<span data-ttu-id="04541-636">Severity of the alert.</span><span class="sxs-lookup"><span data-stu-id="04541-636">Severity of the alert.</span></span> |
| <span data-ttu-id="04541-637">Priority</span><span class="sxs-lookup"><span data-stu-id="04541-637">Priority</span></span> |<span data-ttu-id="04541-638">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="04541-638">ConfigurationAlert</span></span> |<span data-ttu-id="04541-639">Priority of the alert.</span><span class="sxs-lookup"><span data-stu-id="04541-639">Priority of the alert.</span></span> |
| <span data-ttu-id="04541-640">IsMonitorAlert</span><span class="sxs-lookup"><span data-stu-id="04541-640">IsMonitorAlert</span></span> |<span data-ttu-id="04541-641">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="04541-641">ConfigurationAlert</span></span> |<span data-ttu-id="04541-642">Is this alert generated by a monitor (true) or a rule (false)?</span><span class="sxs-lookup"><span data-stu-id="04541-642">Is this alert generated by a monitor (true) or a rule (false)?</span></span> |
| <span data-ttu-id="04541-643">AlertParameters</span><span class="sxs-lookup"><span data-stu-id="04541-643">AlertParameters</span></span> |<span data-ttu-id="04541-644">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="04541-644">ConfigurationAlert</span></span> |<span data-ttu-id="04541-645">XML with the parameters of the Log Analytics alert.</span><span class="sxs-lookup"><span data-stu-id="04541-645">XML with the parameters of the Log Analytics alert.</span></span> |
| <span data-ttu-id="04541-646">Context</span><span class="sxs-lookup"><span data-stu-id="04541-646">Context</span></span> |<span data-ttu-id="04541-647">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="04541-647">ConfigurationAlert</span></span> |<span data-ttu-id="04541-648">XML with the context of the Log Analytics alert.</span><span class="sxs-lookup"><span data-stu-id="04541-648">XML with the context of the Log Analytics alert.</span></span> |
| <span data-ttu-id="04541-649">Workload</span><span class="sxs-lookup"><span data-stu-id="04541-649">Workload</span></span> |<span data-ttu-id="04541-650">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="04541-650">ConfigurationAlert</span></span> |<span data-ttu-id="04541-651">Technology or workload that the alert refers to.</span><span class="sxs-lookup"><span data-stu-id="04541-651">Technology or workload that the alert refers to.</span></span> |
| <span data-ttu-id="04541-652">AdvisorWorkload</span><span class="sxs-lookup"><span data-stu-id="04541-652">AdvisorWorkload</span></span> |<span data-ttu-id="04541-653">Recommendation</span><span class="sxs-lookup"><span data-stu-id="04541-653">Recommendation</span></span> |<span data-ttu-id="04541-654">Technology or workload that the recommendation refers to.</span><span class="sxs-lookup"><span data-stu-id="04541-654">Technology or workload that the recommendation refers to.</span></span> |
| <span data-ttu-id="04541-655">Description</span><span class="sxs-lookup"><span data-stu-id="04541-655">Description</span></span> |<span data-ttu-id="04541-656">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="04541-656">ConfigurationAlert</span></span> |<span data-ttu-id="04541-657">Alert description (short).</span><span class="sxs-lookup"><span data-stu-id="04541-657">Alert description (short).</span></span> |
| <span data-ttu-id="04541-658">DaysSinceLastUpdate</span><span class="sxs-lookup"><span data-stu-id="04541-658">DaysSinceLastUpdate</span></span> |<span data-ttu-id="04541-659">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="04541-659">UpdateAgent</span></span> |<span data-ttu-id="04541-660">How many days ago (relative to TimeGenerated of this record) did this agent install any update from Windows Server Update Service (WSUS) or Microsoft Update?</span><span class="sxs-lookup"><span data-stu-id="04541-660">How many days ago (relative to TimeGenerated of this record) did this agent install any update from Windows Server Update Service (WSUS) or Microsoft Update?</span></span> |
| <span data-ttu-id="04541-661">DaysSinceLastUpdateBucket</span><span class="sxs-lookup"><span data-stu-id="04541-661">DaysSinceLastUpdateBucket</span></span> |<span data-ttu-id="04541-662">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="04541-662">UpdateAgent</span></span> |<span data-ttu-id="04541-663">Based on DaysSinceLastUpdate, a categorization in time buckets of how long ago a computer last installed any update from WSUS/Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="04541-663">Based on DaysSinceLastUpdate, a categorization in time buckets of how long ago a computer last installed any update from WSUS/Microsoft Update.</span></span> |
| <span data-ttu-id="04541-664">AutomaticUpdateEnabled</span><span class="sxs-lookup"><span data-stu-id="04541-664">AutomaticUpdateEnabled</span></span> |<span data-ttu-id="04541-665">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="04541-665">UpdateAgent</span></span> |<span data-ttu-id="04541-666">Is automatic update checking enabled or disabled on this agent?</span><span class="sxs-lookup"><span data-stu-id="04541-666">Is automatic update checking enabled or disabled on this agent?</span></span> |
| <span data-ttu-id="04541-667">AutomaticUpdateValue</span><span class="sxs-lookup"><span data-stu-id="04541-667">AutomaticUpdateValue</span></span> |<span data-ttu-id="04541-668">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="04541-668">UpdateAgent</span></span> |<span data-ttu-id="04541-669">Is automatic update checking set to automatically download and install, only download, or only check?</span><span class="sxs-lookup"><span data-stu-id="04541-669">Is automatic update checking set to automatically download and install, only download, or only check?</span></span> |
| <span data-ttu-id="04541-670">WindowsUpdateAgentVersion</span><span class="sxs-lookup"><span data-stu-id="04541-670">WindowsUpdateAgentVersion</span></span> |<span data-ttu-id="04541-671">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="04541-671">UpdateAgent</span></span> |<span data-ttu-id="04541-672">Version number of the Microsoft Update agent.</span><span class="sxs-lookup"><span data-stu-id="04541-672">Version number of the Microsoft Update agent.</span></span> |
| <span data-ttu-id="04541-673">WSUSServer</span><span class="sxs-lookup"><span data-stu-id="04541-673">WSUSServer</span></span> |<span data-ttu-id="04541-674">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="04541-674">UpdateAgent</span></span> |<span data-ttu-id="04541-675">Which WSUS server is this update agent targeting?</span><span class="sxs-lookup"><span data-stu-id="04541-675">Which WSUS server is this update agent targeting?</span></span> |
| <span data-ttu-id="04541-676">OSVersion</span><span class="sxs-lookup"><span data-stu-id="04541-676">OSVersion</span></span> |<span data-ttu-id="04541-677">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="04541-677">UpdateAgent</span></span> |<span data-ttu-id="04541-678">Version of the operating system this update agent is running on.</span><span class="sxs-lookup"><span data-stu-id="04541-678">Version of the operating system this update agent is running on.</span></span> |
| <span data-ttu-id="04541-679">Name</span><span class="sxs-lookup"><span data-stu-id="04541-679">Name</span></span> |<span data-ttu-id="04541-680">Recommendation, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="04541-680">Recommendation, ConfigurationObjectProperty</span></span> |<span data-ttu-id="04541-681">Name/title of the recommendation, or name of the property from Log Analytics configuration assessment.</span><span class="sxs-lookup"><span data-stu-id="04541-681">Name/title of the recommendation, or name of the property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="04541-682">Value</span><span class="sxs-lookup"><span data-stu-id="04541-682">Value</span></span> |<span data-ttu-id="04541-683">ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="04541-683">ConfigurationObjectProperty</span></span> |<span data-ttu-id="04541-684">Value of a property from Log Analytics configuration assessment.</span><span class="sxs-lookup"><span data-stu-id="04541-684">Value of a property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="04541-685">KBLink</span><span class="sxs-lookup"><span data-stu-id="04541-685">KBLink</span></span> |<span data-ttu-id="04541-686">Recommendation</span><span class="sxs-lookup"><span data-stu-id="04541-686">Recommendation</span></span> |<span data-ttu-id="04541-687">URL to the KB article that describes this best practice or update.</span><span class="sxs-lookup"><span data-stu-id="04541-687">URL to the KB article that describes this best practice or update.</span></span> |
| <span data-ttu-id="04541-688">RecommendationStatus</span><span class="sxs-lookup"><span data-stu-id="04541-688">RecommendationStatus</span></span> |<span data-ttu-id="04541-689">Recommendation</span><span class="sxs-lookup"><span data-stu-id="04541-689">Recommendation</span></span> |<span data-ttu-id="04541-690">Recommendations are among the few types whose records get updated, not just added to the search index.</span><span class="sxs-lookup"><span data-stu-id="04541-690">Recommendations are among the few types whose records get updated, not just added to the search index.</span></span> <span data-ttu-id="04541-691">This status changes whether the recommendation is active/open, or if Log Analytics detects that it has been resolved.</span><span class="sxs-lookup"><span data-stu-id="04541-691">This status changes whether the recommendation is active/open, or if Log Analytics detects that it has been resolved.</span></span> |
| <span data-ttu-id="04541-692">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="04541-692">RenderedDescription</span></span> |<span data-ttu-id="04541-693">Event</span><span class="sxs-lookup"><span data-stu-id="04541-693">Event</span></span> |<span data-ttu-id="04541-694">Rendered description (reused text with populated parameters) of a Windows event.</span><span class="sxs-lookup"><span data-stu-id="04541-694">Rendered description (reused text with populated parameters) of a Windows event.</span></span> |
| <span data-ttu-id="04541-695">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="04541-695">ParameterXml</span></span> |<span data-ttu-id="04541-696">Event</span><span class="sxs-lookup"><span data-stu-id="04541-696">Event</span></span> |<span data-ttu-id="04541-697">XML with the parameters in the data section of a Windows Event (as seen in event viewer).</span><span class="sxs-lookup"><span data-stu-id="04541-697">XML with the parameters in the data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="04541-698">EventData</span><span class="sxs-lookup"><span data-stu-id="04541-698">EventData</span></span> |<span data-ttu-id="04541-699">Event</span><span class="sxs-lookup"><span data-stu-id="04541-699">Event</span></span> |<span data-ttu-id="04541-700">XML with the whole data section of a Windows Event (as seen in event viewer).</span><span class="sxs-lookup"><span data-stu-id="04541-700">XML with the whole data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="04541-701">Source</span><span class="sxs-lookup"><span data-stu-id="04541-701">Source</span></span> |<span data-ttu-id="04541-702">Event</span><span class="sxs-lookup"><span data-stu-id="04541-702">Event</span></span> |<span data-ttu-id="04541-703">Event log source that generated the event.</span><span class="sxs-lookup"><span data-stu-id="04541-703">Event log source that generated the event.</span></span> |
| <span data-ttu-id="04541-704">EventCategory</span><span class="sxs-lookup"><span data-stu-id="04541-704">EventCategory</span></span> |<span data-ttu-id="04541-705">Event</span><span class="sxs-lookup"><span data-stu-id="04541-705">Event</span></span> |<span data-ttu-id="04541-706">Category of the event, directly from the Windows event log.</span><span class="sxs-lookup"><span data-stu-id="04541-706">Category of the event, directly from the Windows event log.</span></span> |
| <span data-ttu-id="04541-707">UserName</span><span class="sxs-lookup"><span data-stu-id="04541-707">UserName</span></span> |<span data-ttu-id="04541-708">Event</span><span class="sxs-lookup"><span data-stu-id="04541-708">Event</span></span> |<span data-ttu-id="04541-709">User name of the Windows event (typically, NT AUTHORITY\LOCALSYSTEM).</span><span class="sxs-lookup"><span data-stu-id="04541-709">User name of the Windows event (typically, NT AUTHORITY\LOCALSYSTEM).</span></span> |
| <span data-ttu-id="04541-710">SampleValue</span><span class="sxs-lookup"><span data-stu-id="04541-710">SampleValue</span></span> |<span data-ttu-id="04541-711">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="04541-711">PerfHourly</span></span> |<span data-ttu-id="04541-712">Average value for the hourly aggregation of a performance counter.</span><span class="sxs-lookup"><span data-stu-id="04541-712">Average value for the hourly aggregation of a performance counter.</span></span> |
| <span data-ttu-id="04541-713">Min</span><span class="sxs-lookup"><span data-stu-id="04541-713">Min</span></span> |<span data-ttu-id="04541-714">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="04541-714">PerfHourly</span></span> |<span data-ttu-id="04541-715">Minimum value in the hourly interval of a performance counter hourly aggregate.</span><span class="sxs-lookup"><span data-stu-id="04541-715">Minimum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="04541-716">Max</span><span class="sxs-lookup"><span data-stu-id="04541-716">Max</span></span> |<span data-ttu-id="04541-717">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="04541-717">PerfHourly</span></span> |<span data-ttu-id="04541-718">Maximum value in the hourly interval of a performance counter hourly aggregate.</span><span class="sxs-lookup"><span data-stu-id="04541-718">Maximum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="04541-719">Percentile95</span><span class="sxs-lookup"><span data-stu-id="04541-719">Percentile95</span></span> |<span data-ttu-id="04541-720">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="04541-720">PerfHourly</span></span> |<span data-ttu-id="04541-721">The 95th percentile value for the hourly interval of a performance counter hourly aggregate.</span><span class="sxs-lookup"><span data-stu-id="04541-721">The 95th percentile value for the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="04541-722">SampleCount</span><span class="sxs-lookup"><span data-stu-id="04541-722">SampleCount</span></span> |<span data-ttu-id="04541-723">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="04541-723">PerfHourly</span></span> |<span data-ttu-id="04541-724">How many raw performance counter samples were used to produce this hourly aggregate record.</span><span class="sxs-lookup"><span data-stu-id="04541-724">How many raw performance counter samples were used to produce this hourly aggregate record.</span></span> |
| <span data-ttu-id="04541-725">Threat</span><span class="sxs-lookup"><span data-stu-id="04541-725">Threat</span></span> |<span data-ttu-id="04541-726">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="04541-726">ProtectionStatus</span></span> |<span data-ttu-id="04541-727">Name of malware found.</span><span class="sxs-lookup"><span data-stu-id="04541-727">Name of malware found.</span></span> |
| <span data-ttu-id="04541-728">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="04541-728">StorageAccount</span></span> |<span data-ttu-id="04541-729">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-729">W3CIISLog</span></span> |<span data-ttu-id="04541-730">Azure Storage account the log was read from.</span><span class="sxs-lookup"><span data-stu-id="04541-730">Azure Storage account the log was read from.</span></span> |
| <span data-ttu-id="04541-731">AzureDeploymentID</span><span class="sxs-lookup"><span data-stu-id="04541-731">AzureDeploymentID</span></span> |<span data-ttu-id="04541-732">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-732">W3CIISLog</span></span> |<span data-ttu-id="04541-733">Azure deployment ID of the cloud service the log belongs to.</span><span class="sxs-lookup"><span data-stu-id="04541-733">Azure deployment ID of the cloud service the log belongs to.</span></span> |
| <span data-ttu-id="04541-734">Role</span><span class="sxs-lookup"><span data-stu-id="04541-734">Role</span></span> |<span data-ttu-id="04541-735">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-735">W3CIISLog</span></span> |<span data-ttu-id="04541-736">Role of the Azure cloud service the log belongs to.</span><span class="sxs-lookup"><span data-stu-id="04541-736">Role of the Azure cloud service the log belongs to.</span></span> |
| <span data-ttu-id="04541-737">RoleInstance</span><span class="sxs-lookup"><span data-stu-id="04541-737">RoleInstance</span></span> |<span data-ttu-id="04541-738">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-738">W3CIISLog</span></span> |<span data-ttu-id="04541-739">RoleInstance of the Azure role that the log belongs to.</span><span class="sxs-lookup"><span data-stu-id="04541-739">RoleInstance of the Azure role that the log belongs to.</span></span> |
| <span data-ttu-id="04541-740">sSiteName</span><span class="sxs-lookup"><span data-stu-id="04541-740">sSiteName</span></span> |<span data-ttu-id="04541-741">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-741">W3CIISLog</span></span> |<span data-ttu-id="04541-742">IIS website that the log belongs to (metabase notation); the s-sitename field in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-742">IIS website that the log belongs to (metabase notation); the s-sitename field in the original log.</span></span> |
| <span data-ttu-id="04541-743">sComputerName</span><span class="sxs-lookup"><span data-stu-id="04541-743">sComputerName</span></span> |<span data-ttu-id="04541-744">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-744">W3CIISLog</span></span> |<span data-ttu-id="04541-745">The s-computername field in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-745">The s-computername field in the original log.</span></span> |
| <span data-ttu-id="04541-746">sIP</span><span class="sxs-lookup"><span data-stu-id="04541-746">sIP</span></span> |<span data-ttu-id="04541-747">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-747">W3CIISLog</span></span> |<span data-ttu-id="04541-748">Server IP address the HTTP request was addressed to.</span><span class="sxs-lookup"><span data-stu-id="04541-748">Server IP address the HTTP request was addressed to.</span></span> <span data-ttu-id="04541-749">The s-ip field in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-749">The s-ip field in the original log.</span></span> |
| <span data-ttu-id="04541-750">csMethod</span><span class="sxs-lookup"><span data-stu-id="04541-750">csMethod</span></span> |<span data-ttu-id="04541-751">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-751">W3CIISLog</span></span> |<span data-ttu-id="04541-752">HTTP method (for example, GET/POST) used by the client in the HTTP request.</span><span class="sxs-lookup"><span data-stu-id="04541-752">HTTP method (for example, GET/POST) used by the client in the HTTP request.</span></span> <span data-ttu-id="04541-753">The cs-method in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-753">The cs-method in the original log.</span></span> |
| <span data-ttu-id="04541-754">cIP</span><span class="sxs-lookup"><span data-stu-id="04541-754">cIP</span></span> |<span data-ttu-id="04541-755">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-755">W3CIISLog</span></span> |<span data-ttu-id="04541-756">Client IP address the HTTP request came from.</span><span class="sxs-lookup"><span data-stu-id="04541-756">Client IP address the HTTP request came from.</span></span> <span data-ttu-id="04541-757">The c-ip field in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-757">The c-ip field in the original log.</span></span> |
| <span data-ttu-id="04541-758">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="04541-758">csUserAgent</span></span> |<span data-ttu-id="04541-759">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-759">W3CIISLog</span></span> |<span data-ttu-id="04541-760">HTTP User-Agent declared by the client (browser or otherwise).</span><span class="sxs-lookup"><span data-stu-id="04541-760">HTTP User-Agent declared by the client (browser or otherwise).</span></span> <span data-ttu-id="04541-761">The cs-user-agent in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-761">The cs-user-agent in the original log.</span></span> |
| <span data-ttu-id="04541-762">scStatus</span><span class="sxs-lookup"><span data-stu-id="04541-762">scStatus</span></span> |<span data-ttu-id="04541-763">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-763">W3CIISLog</span></span> |<span data-ttu-id="04541-764">HTTP Status code (for example, 200/403/500) returned by the server to the client.</span><span class="sxs-lookup"><span data-stu-id="04541-764">HTTP Status code (for example, 200/403/500) returned by the server to the client.</span></span> <span data-ttu-id="04541-765">The cs-status in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-765">The cs-status in the original log.</span></span> |
| <span data-ttu-id="04541-766">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="04541-766">TimeTaken</span></span> |<span data-ttu-id="04541-767">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-767">W3CIISLog</span></span> |<span data-ttu-id="04541-768">How long (in milliseconds) that the request took to complete.</span><span class="sxs-lookup"><span data-stu-id="04541-768">How long (in milliseconds) that the request took to complete.</span></span> <span data-ttu-id="04541-769">The timetaken field in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-769">The timetaken field in the original log.</span></span> |
| <span data-ttu-id="04541-770">csUriStem</span><span class="sxs-lookup"><span data-stu-id="04541-770">csUriStem</span></span> |<span data-ttu-id="04541-771">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-771">W3CIISLog</span></span> |<span data-ttu-id="04541-772">Relative URI (without host address, that is, /search ) that was requested.</span><span class="sxs-lookup"><span data-stu-id="04541-772">Relative URI (without host address, that is, /search ) that was requested.</span></span> <span data-ttu-id="04541-773">The cs-uristem field in the original log.</span><span class="sxs-lookup"><span data-stu-id="04541-773">The cs-uristem field in the original log.</span></span> |
| <span data-ttu-id="04541-774">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="04541-774">csUriQuery</span></span> |<span data-ttu-id="04541-775">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-775">W3CIISLog</span></span> |<span data-ttu-id="04541-776">URI query.</span><span class="sxs-lookup"><span data-stu-id="04541-776">URI query.</span></span> <span data-ttu-id="04541-777">URI queries are necessary only for dynamic pages, such as ASP pages, so this field usually contains a hyphen for static pages.</span><span class="sxs-lookup"><span data-stu-id="04541-777">URI queries are necessary only for dynamic pages, such as ASP pages, so this field usually contains a hyphen for static pages.</span></span> |
| <span data-ttu-id="04541-778">sPort</span><span class="sxs-lookup"><span data-stu-id="04541-778">sPort</span></span> |<span data-ttu-id="04541-779">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-779">W3CIISLog</span></span> |<span data-ttu-id="04541-780">Server port that the HTTP request was sent to (and that IIS listens to, since it picked it up).</span><span class="sxs-lookup"><span data-stu-id="04541-780">Server port that the HTTP request was sent to (and that IIS listens to, since it picked it up).</span></span> |
| <span data-ttu-id="04541-781">csUserName</span><span class="sxs-lookup"><span data-stu-id="04541-781">csUserName</span></span> |<span data-ttu-id="04541-782">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-782">W3CIISLog</span></span> |<span data-ttu-id="04541-783">Authenticated user name, if the request is authenticated and not anonymous.</span><span class="sxs-lookup"><span data-stu-id="04541-783">Authenticated user name, if the request is authenticated and not anonymous.</span></span> |
| <span data-ttu-id="04541-784">csVersion</span><span class="sxs-lookup"><span data-stu-id="04541-784">csVersion</span></span> |<span data-ttu-id="04541-785">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-785">W3CIISLog</span></span> |<span data-ttu-id="04541-786">HTTP Protocol version used in the request (for example, HTTP/1.1).</span><span class="sxs-lookup"><span data-stu-id="04541-786">HTTP Protocol version used in the request (for example, HTTP/1.1).</span></span> |
| <span data-ttu-id="04541-787">csCookie</span><span class="sxs-lookup"><span data-stu-id="04541-787">csCookie</span></span> |<span data-ttu-id="04541-788">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-788">W3CIISLog</span></span> |<span data-ttu-id="04541-789">Cookie information.</span><span class="sxs-lookup"><span data-stu-id="04541-789">Cookie information.</span></span> |
| <span data-ttu-id="04541-790">csReferer</span><span class="sxs-lookup"><span data-stu-id="04541-790">csReferer</span></span> |<span data-ttu-id="04541-791">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-791">W3CIISLog</span></span> |<span data-ttu-id="04541-792">Site that the user last visited.</span><span class="sxs-lookup"><span data-stu-id="04541-792">Site that the user last visited.</span></span> <span data-ttu-id="04541-793">This site provided a link to the current site.</span><span class="sxs-lookup"><span data-stu-id="04541-793">This site provided a link to the current site.</span></span> |
| <span data-ttu-id="04541-794">csHost</span><span class="sxs-lookup"><span data-stu-id="04541-794">csHost</span></span> |<span data-ttu-id="04541-795">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-795">W3CIISLog</span></span> |<span data-ttu-id="04541-796">Host header (for example, www.mysite.com) that was requested.</span><span class="sxs-lookup"><span data-stu-id="04541-796">Host header (for example, www.mysite.com) that was requested.</span></span> |
| <span data-ttu-id="04541-797">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="04541-797">scSubStatus</span></span> |<span data-ttu-id="04541-798">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-798">W3CIISLog</span></span> |<span data-ttu-id="04541-799">Substatus error code.</span><span class="sxs-lookup"><span data-stu-id="04541-799">Substatus error code.</span></span> |
| <span data-ttu-id="04541-800">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="04541-800">scWin32Status</span></span> |<span data-ttu-id="04541-801">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-801">W3CIISLog</span></span> |<span data-ttu-id="04541-802">Windows status code.</span><span class="sxs-lookup"><span data-stu-id="04541-802">Windows status code.</span></span> |
| <span data-ttu-id="04541-803">csBytes</span><span class="sxs-lookup"><span data-stu-id="04541-803">csBytes</span></span> |<span data-ttu-id="04541-804">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-804">W3CIISLog</span></span> |<span data-ttu-id="04541-805">Bytes sent in the request from the client to the server.</span><span class="sxs-lookup"><span data-stu-id="04541-805">Bytes sent in the request from the client to the server.</span></span> |
| <span data-ttu-id="04541-806">scBytes</span><span class="sxs-lookup"><span data-stu-id="04541-806">scBytes</span></span> |<span data-ttu-id="04541-807">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="04541-807">W3CIISLog</span></span> |<span data-ttu-id="04541-808">Bytes returned back in the response from the server to the client.</span><span class="sxs-lookup"><span data-stu-id="04541-808">Bytes returned back in the response from the server to the client.</span></span> |
| <span data-ttu-id="04541-809">ConfigChangeType</span><span class="sxs-lookup"><span data-stu-id="04541-809">ConfigChangeType</span></span> |<span data-ttu-id="04541-810">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-810">ConfigurationChange</span></span> |<span data-ttu-id="04541-811">Type of change (for example, WindowsServices/Software).</span><span class="sxs-lookup"><span data-stu-id="04541-811">Type of change (for example, WindowsServices/Software).</span></span> |
| <span data-ttu-id="04541-812">ChangeCategory</span><span class="sxs-lookup"><span data-stu-id="04541-812">ChangeCategory</span></span> |<span data-ttu-id="04541-813">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-813">ConfigurationChange</span></span> |<span data-ttu-id="04541-814">Category of the change (Modified/Added/Removed).</span><span class="sxs-lookup"><span data-stu-id="04541-814">Category of the change (Modified/Added/Removed).</span></span> |
| <span data-ttu-id="04541-815">SoftwareType</span><span class="sxs-lookup"><span data-stu-id="04541-815">SoftwareType</span></span> |<span data-ttu-id="04541-816">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-816">ConfigurationChange</span></span> |<span data-ttu-id="04541-817">Type of software (Update/Application).</span><span class="sxs-lookup"><span data-stu-id="04541-817">Type of software (Update/Application).</span></span> |
| <span data-ttu-id="04541-818">SoftwareName</span><span class="sxs-lookup"><span data-stu-id="04541-818">SoftwareName</span></span> |<span data-ttu-id="04541-819">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-819">ConfigurationChange</span></span> |<span data-ttu-id="04541-820">Name of the software (only applicable to software changes).</span><span class="sxs-lookup"><span data-stu-id="04541-820">Name of the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="04541-821">Publisher</span><span class="sxs-lookup"><span data-stu-id="04541-821">Publisher</span></span> |<span data-ttu-id="04541-822">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-822">ConfigurationChange</span></span> |<span data-ttu-id="04541-823">Vendor who publishes the software (only applicable to software changes).</span><span class="sxs-lookup"><span data-stu-id="04541-823">Vendor who publishes the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="04541-824">SvcChangeType</span><span class="sxs-lookup"><span data-stu-id="04541-824">SvcChangeType</span></span> |<span data-ttu-id="04541-825">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-825">ConfigurationChange</span></span> |<span data-ttu-id="04541-826">Type of change that was applied on a Windows service (State/StartupType/Path/ServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="04541-826">Type of change that was applied on a Windows service (State/StartupType/Path/ServiceAccount).</span></span> <span data-ttu-id="04541-827">This is only applicable to Windows service changes.</span><span class="sxs-lookup"><span data-stu-id="04541-827">This is only applicable to Windows service changes.</span></span> |
| <span data-ttu-id="04541-828">SvcDisplayName</span><span class="sxs-lookup"><span data-stu-id="04541-828">SvcDisplayName</span></span> |<span data-ttu-id="04541-829">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-829">ConfigurationChange</span></span> |<span data-ttu-id="04541-830">Display name of the service that was changed.</span><span class="sxs-lookup"><span data-stu-id="04541-830">Display name of the service that was changed.</span></span> |
| <span data-ttu-id="04541-831">SvcName</span><span class="sxs-lookup"><span data-stu-id="04541-831">SvcName</span></span> |<span data-ttu-id="04541-832">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-832">ConfigurationChange</span></span> |<span data-ttu-id="04541-833">Name of the service that was changed.</span><span class="sxs-lookup"><span data-stu-id="04541-833">Name of the service that was changed.</span></span> |
| <span data-ttu-id="04541-834">SvcState</span><span class="sxs-lookup"><span data-stu-id="04541-834">SvcState</span></span> |<span data-ttu-id="04541-835">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-835">ConfigurationChange</span></span> |<span data-ttu-id="04541-836">New (current) state of the service.</span><span class="sxs-lookup"><span data-stu-id="04541-836">New (current) state of the service.</span></span> |
| <span data-ttu-id="04541-837">SvcPreviousState</span><span class="sxs-lookup"><span data-stu-id="04541-837">SvcPreviousState</span></span> |<span data-ttu-id="04541-838">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-838">ConfigurationChange</span></span> |<span data-ttu-id="04541-839">Previous known state of the service (only applicable if service state changed).</span><span class="sxs-lookup"><span data-stu-id="04541-839">Previous known state of the service (only applicable if service state changed).</span></span> |
| <span data-ttu-id="04541-840">SvcStartupType</span><span class="sxs-lookup"><span data-stu-id="04541-840">SvcStartupType</span></span> |<span data-ttu-id="04541-841">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-841">ConfigurationChange</span></span> |<span data-ttu-id="04541-842">Service startup type.</span><span class="sxs-lookup"><span data-stu-id="04541-842">Service startup type.</span></span> |
| <span data-ttu-id="04541-843">SvcPreviousStartupType</span><span class="sxs-lookup"><span data-stu-id="04541-843">SvcPreviousStartupType</span></span> |<span data-ttu-id="04541-844">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-844">ConfigurationChange</span></span> |<span data-ttu-id="04541-845">Previous service startup type (only applicable if service startup type changed).</span><span class="sxs-lookup"><span data-stu-id="04541-845">Previous service startup type (only applicable if service startup type changed).</span></span> |
| <span data-ttu-id="04541-846">SvcAccount</span><span class="sxs-lookup"><span data-stu-id="04541-846">SvcAccount</span></span> |<span data-ttu-id="04541-847">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-847">ConfigurationChange</span></span> |<span data-ttu-id="04541-848">Service account.</span><span class="sxs-lookup"><span data-stu-id="04541-848">Service account.</span></span> |
| <span data-ttu-id="04541-849">SvcPreviousAccount</span><span class="sxs-lookup"><span data-stu-id="04541-849">SvcPreviousAccount</span></span> |<span data-ttu-id="04541-850">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-850">ConfigurationChange</span></span> |<span data-ttu-id="04541-851">Previous service account (only applicable if service account changed).</span><span class="sxs-lookup"><span data-stu-id="04541-851">Previous service account (only applicable if service account changed).</span></span> |
| <span data-ttu-id="04541-852">SvcPath</span><span class="sxs-lookup"><span data-stu-id="04541-852">SvcPath</span></span> |<span data-ttu-id="04541-853">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-853">ConfigurationChange</span></span> |<span data-ttu-id="04541-854">Path to the executable of the Windows service.</span><span class="sxs-lookup"><span data-stu-id="04541-854">Path to the executable of the Windows service.</span></span> |
| <span data-ttu-id="04541-855">SvcPreviousPath</span><span class="sxs-lookup"><span data-stu-id="04541-855">SvcPreviousPath</span></span> |<span data-ttu-id="04541-856">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-856">ConfigurationChange</span></span> |<span data-ttu-id="04541-857">Previous path of the executable for the Windows service (only applicable if it changed).</span><span class="sxs-lookup"><span data-stu-id="04541-857">Previous path of the executable for the Windows service (only applicable if it changed).</span></span> |
| <span data-ttu-id="04541-858">SvcDescription</span><span class="sxs-lookup"><span data-stu-id="04541-858">SvcDescription</span></span> |<span data-ttu-id="04541-859">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-859">ConfigurationChange</span></span> |<span data-ttu-id="04541-860">Description of the service.</span><span class="sxs-lookup"><span data-stu-id="04541-860">Description of the service.</span></span> |
| <span data-ttu-id="04541-861">Previous</span><span class="sxs-lookup"><span data-stu-id="04541-861">Previous</span></span> |<span data-ttu-id="04541-862">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-862">ConfigurationChange</span></span> |<span data-ttu-id="04541-863">Previous state of this software (Installed/Not Installed/previous version).</span><span class="sxs-lookup"><span data-stu-id="04541-863">Previous state of this software (Installed/Not Installed/previous version).</span></span> |
| <span data-ttu-id="04541-864">Current</span><span class="sxs-lookup"><span data-stu-id="04541-864">Current</span></span> |<span data-ttu-id="04541-865">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="04541-865">ConfigurationChange</span></span> |<span data-ttu-id="04541-866">Latest state of this software (Installed/Not Installed/current version).</span><span class="sxs-lookup"><span data-stu-id="04541-866">Latest state of this software (Installed/Not Installed/current version).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="04541-867">Next steps</span><span class="sxs-lookup"><span data-stu-id="04541-867">Next steps</span></span>
<span data-ttu-id="04541-868">For additional information about log searches:</span><span class="sxs-lookup"><span data-stu-id="04541-868">For additional information about log searches:</span></span>

* <span data-ttu-id="04541-869">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span><span class="sxs-lookup"><span data-stu-id="04541-869">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="04541-870">Use [custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span><span class="sxs-lookup"><span data-stu-id="04541-870">Use [custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
