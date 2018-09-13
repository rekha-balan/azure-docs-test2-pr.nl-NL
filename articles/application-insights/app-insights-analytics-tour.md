---
title: A tour through Analytics in Azure Application Insights | Microsoft Docs
description: Short samples of all the main queries in Analytics, the powerful search tool of Application Insights.
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 39e6861afb8a9a78e3d1a0774d1ea467a7393b2c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553110"
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="f1511-103">A tour of Analytics in Application Insights</span><span class="sxs-lookup"><span data-stu-id="f1511-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="f1511-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1511-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f1511-105">These pages describe the Analytics query language.</span><span class="sxs-lookup"><span data-stu-id="f1511-105">These pages describe the Analytics query language.</span></span>

* <span data-ttu-id="f1511-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="f1511-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="f1511-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span><span class="sxs-lookup"><span data-stu-id="f1511-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="f1511-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span><span class="sxs-lookup"><span data-stu-id="f1511-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>

<span data-ttu-id="f1511-109">Let's take a walk through some basic queries to get you started.</span><span class="sxs-lookup"><span data-stu-id="f1511-109">Let's take a walk through some basic queries to get you started.</span></span>

## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="f1511-110">Connect to your Application Insights data</span><span class="sxs-lookup"><span data-stu-id="f1511-110">Connect to your Application Insights data</span></span>
<span data-ttu-id="f1511-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span><span class="sxs-lookup"><span data-stu-id="f1511-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Open portal.azure.com, open your Application Insights resource, and click Analytics.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/001.png)

## <a name="takeapp-insights-analytics-referencemdtake-operator-show-me-n-rows"></a><span data-ttu-id="f1511-113">[Take](app-insights-analytics-reference.md#take-operator): show me n rows</span><span class="sxs-lookup"><span data-stu-id="f1511-113">[Take](app-insights-analytics-reference.md#take-operator): show me n rows</span></span>
<span data-ttu-id="f1511-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span><span class="sxs-lookup"><span data-stu-id="f1511-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="f1511-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span><span class="sxs-lookup"><span data-stu-id="f1511-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span></span>

<span data-ttu-id="f1511-116">Let's start by examining a few sample rows of the table:</span><span class="sxs-lookup"><span data-stu-id="f1511-116">Let's start by examining a few sample rows of the table:</span></span>

![results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="f1511-118">Put the cursor somewhere in the statement before you click Go.</span><span class="sxs-lookup"><span data-stu-id="f1511-118">Put the cursor somewhere in the statement before you click Go.</span></span> <span data-ttu-id="f1511-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span><span class="sxs-lookup"><span data-stu-id="f1511-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="f1511-120">Blank lines are a convenient way to keep several separate queries in the window.</span><span class="sxs-lookup"><span data-stu-id="f1511-120">Blank lines are a convenient way to keep several separate queries in the window.</span></span>
>
>

<span data-ttu-id="f1511-121">Choose columns, drag them, group by columns, and filter:</span><span class="sxs-lookup"><span data-stu-id="f1511-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Click column selection at upper right of results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/030.png)

<span data-ttu-id="f1511-123">Expand any item to see the detail:</span><span class="sxs-lookup"><span data-stu-id="f1511-123">Expand any item to see the detail:</span></span>

![Choose Table, and use Configure Columns](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="f1511-125">Click the head of a column to re-order the results available in the web browser.</span><span class="sxs-lookup"><span data-stu-id="f1511-125">Click the head of a column to re-order the results available in the web browser.</span></span> <span data-ttu-id="f1511-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span><span class="sxs-lookup"><span data-stu-id="f1511-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span></span> <span data-ttu-id="f1511-127">Sorting this way doesn't always show you the actual highest or lowest items.</span><span class="sxs-lookup"><span data-stu-id="f1511-127">Sorting this way doesn't always show you the actual highest or lowest items.</span></span> <span data-ttu-id="f1511-128">To sort items reliably, use the `top` or `sort` operator.</span><span class="sxs-lookup"><span data-stu-id="f1511-128">To sort items reliably, use the `top` or `sort` operator.</span></span>
>
>

## <a name="topapp-insights-analytics-referencemdtop-operator-and-sortapp-insights-analytics-referencemdsort-operator"></a><span data-ttu-id="f1511-129">[Top](app-insights-analytics-reference.md#top-operator) and [sort](app-insights-analytics-reference.md#sort-operator)</span><span class="sxs-lookup"><span data-stu-id="f1511-129">[Top](app-insights-analytics-reference.md#top-operator) and [sort](app-insights-analytics-reference.md#sort-operator)</span></span>
<span data-ttu-id="f1511-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span><span class="sxs-lookup"><span data-stu-id="f1511-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span></span> <span data-ttu-id="f1511-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span><span class="sxs-lookup"><span data-stu-id="f1511-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span></span>

<span data-ttu-id="f1511-132">Show me the first n rows, ordered by a particular column:</span><span class="sxs-lookup"><span data-stu-id="f1511-132">Show me the first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="f1511-133">*Syntax:* Most operators have keyword parameters such as `by`.</span><span class="sxs-lookup"><span data-stu-id="f1511-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="f1511-134">`desc` = descending order, `asc` = ascending.</span><span class="sxs-lookup"><span data-stu-id="f1511-134">`desc` = descending order, `asc` = ascending.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/260.png)

<span data-ttu-id="f1511-135">`top...` is a more performant way of saying `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="f1511-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="f1511-136">We could have written:</span><span class="sxs-lookup"><span data-stu-id="f1511-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="f1511-137">The result would be the same, but it would run a bit more slowly.</span><span class="sxs-lookup"><span data-stu-id="f1511-137">The result would be the same, but it would run a bit more slowly.</span></span> <span data-ttu-id="f1511-138">(You could also write `order`, which is an alias of `sort`.)</span><span class="sxs-lookup"><span data-stu-id="f1511-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="f1511-139">The column headers in the table view can also be used to sort the results on the screen.</span><span class="sxs-lookup"><span data-stu-id="f1511-139">The column headers in the table view can also be used to sort the results on the screen.</span></span> <span data-ttu-id="f1511-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span><span class="sxs-lookup"><span data-stu-id="f1511-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span></span>

## <a name="whereapp-insights-analytics-referencemdwhere-operator-filtering-on-a-condition"></a><span data-ttu-id="f1511-141">[Where](app-insights-analytics-reference.md#where-operator): filtering on a condition</span><span class="sxs-lookup"><span data-stu-id="f1511-141">[Where](app-insights-analytics-reference.md#where-operator): filtering on a condition</span></span>

<span data-ttu-id="f1511-142">Let's see just requests that returned a particular result code:</span><span class="sxs-lookup"><span data-stu-id="f1511-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/250.png)

<span data-ttu-id="f1511-143">The `where` operator takes a Boolean expression.</span><span class="sxs-lookup"><span data-stu-id="f1511-143">The `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="f1511-144">Here are some key points about them:</span><span class="sxs-lookup"><span data-stu-id="f1511-144">Here are some key points about them:</span></span>

* <span data-ttu-id="f1511-145">`and`, `or`: Boolean operators</span><span class="sxs-lookup"><span data-stu-id="f1511-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="f1511-146">`==`, `<>`, `!=` : equal and not equal</span><span class="sxs-lookup"><span data-stu-id="f1511-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="f1511-147">`=~`, `!~` : case-insensitive string equal and not equal.</span><span class="sxs-lookup"><span data-stu-id="f1511-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="f1511-148">There are lots more string comparison operators.</span><span class="sxs-lookup"><span data-stu-id="f1511-148">There are lots more string comparison operators.</span></span>

<span data-ttu-id="f1511-149">Read all about [scalar expressions](app-insights-analytics-reference.md#scalars).</span><span class="sxs-lookup"><span data-stu-id="f1511-149">Read all about [scalar expressions](app-insights-analytics-reference.md#scalars).</span></span>

### <a name="getting-the-right-type"></a><span data-ttu-id="f1511-150">Getting the right type</span><span class="sxs-lookup"><span data-stu-id="f1511-150">Getting the right type</span></span>
<span data-ttu-id="f1511-151">Find unsuccessful requests:</span><span class="sxs-lookup"><span data-stu-id="f1511-151">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```

<span data-ttu-id="f1511-152">`resultCode` has type string, so we must [cast it](app-insights-analytics-reference.md#casts) for a numeric comparison.</span><span class="sxs-lookup"><span data-stu-id="f1511-152">`resultCode` has type string, so we must [cast it](app-insights-analytics-reference.md#casts) for a numeric comparison.</span></span>

## <a name="time-range"></a><span data-ttu-id="f1511-153">Time range</span><span class="sxs-lookup"><span data-stu-id="f1511-153">Time range</span></span>

<span data-ttu-id="f1511-154">By default, your queries are restricted to the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="f1511-154">By default, your queries are restricted to the last 24 hours.</span></span> <span data-ttu-id="f1511-155">But you can change this range:</span><span class="sxs-lookup"><span data-stu-id="f1511-155">But you can change this range:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="f1511-156">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span><span class="sxs-lookup"><span data-stu-id="f1511-156">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="f1511-157">For example:</span><span class="sxs-lookup"><span data-stu-id="f1511-157">For example:</span></span>

```AIQL

    // What were the slowest requests over the past 3 days?
    requests
    | where timestamp > ago(3d)  // Override the time range
    | top 5 by duration
```

<span data-ttu-id="f1511-158">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span><span class="sxs-lookup"><span data-stu-id="f1511-158">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span></span>

<span data-ttu-id="f1511-159">`ago(3d)` means 'three days ago'.</span><span class="sxs-lookup"><span data-stu-id="f1511-159">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="f1511-160">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span><span class="sxs-lookup"><span data-stu-id="f1511-160">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="f1511-161">Other examples:</span><span class="sxs-lookup"><span data-stu-id="f1511-161">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="f1511-162">[Dates and times reference](app-insights-analytics-reference.md#date-and-time).</span><span class="sxs-lookup"><span data-stu-id="f1511-162">[Dates and times reference](app-insights-analytics-reference.md#date-and-time).</span></span>


## <a name="projectapp-insights-analytics-referencemdproject-operator-select-rename-and-compute-columns"></a><span data-ttu-id="f1511-163">[Project](app-insights-analytics-reference.md#project-operator): select, rename, and compute columns</span><span class="sxs-lookup"><span data-stu-id="f1511-163">[Project](app-insights-analytics-reference.md#project-operator): select, rename, and compute columns</span></span>
<span data-ttu-id="f1511-164">Use [`project`](app-insights-analytics-reference.md#project-operator) to pick out just the columns you want:</span><span class="sxs-lookup"><span data-stu-id="f1511-164">Use [`project`](app-insights-analytics-reference.md#project-operator) to pick out just the columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/240.png)

<span data-ttu-id="f1511-165">You can also rename columns and define new ones:</span><span class="sxs-lookup"><span data-stu-id="f1511-165">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="f1511-167">[Column names](app-insights-analytics-reference.md#names) can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span><span class="sxs-lookup"><span data-stu-id="f1511-167">[Column names](app-insights-analytics-reference.md#names) can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="f1511-168">`%` is the usual modulo operator.</span><span class="sxs-lookup"><span data-stu-id="f1511-168">`%` is the usual modulo operator.</span></span>
* <span data-ttu-id="f1511-169">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span><span class="sxs-lookup"><span data-stu-id="f1511-169">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="f1511-170">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="f1511-170">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="f1511-171">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span><span class="sxs-lookup"><span data-stu-id="f1511-171">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span></span> <span data-ttu-id="f1511-172">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span><span class="sxs-lookup"><span data-stu-id="f1511-172">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span></span>

<span data-ttu-id="f1511-173">[Expressions](app-insights-analytics-reference.md#scalars) can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span><span class="sxs-lookup"><span data-stu-id="f1511-173">[Expressions](app-insights-analytics-reference.md#scalars) can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extendapp-insights-analytics-referencemdextend-operator-compute-columns"></a><span data-ttu-id="f1511-174">[Extend](app-insights-analytics-reference.md#extend-operator): compute columns</span><span class="sxs-lookup"><span data-stu-id="f1511-174">[Extend](app-insights-analytics-reference.md#extend-operator): compute columns</span></span>
<span data-ttu-id="f1511-175">If you just want to add columns to the existing ones, use [`extend`](app-insights-analytics-reference.md#extend-operator):</span><span class="sxs-lookup"><span data-stu-id="f1511-175">If you just want to add columns to the existing ones, use [`extend`](app-insights-analytics-reference.md#extend-operator):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="f1511-176">Using [`extend`](app-insights-analytics-reference.md#extend-operator) is less verbose than [`project`](app-insights-analytics-reference.md#project-operator) if you want to keep all the existing columns.</span><span class="sxs-lookup"><span data-stu-id="f1511-176">Using [`extend`](app-insights-analytics-reference.md#extend-operator) is less verbose than [`project`](app-insights-analytics-reference.md#project-operator) if you want to keep all the existing columns.</span></span>

### <a name="convert-to-local-time"></a><span data-ttu-id="f1511-177">Convert to local time</span><span class="sxs-lookup"><span data-stu-id="f1511-177">Convert to local time</span></span>

<span data-ttu-id="f1511-178">Timestamps are always in UTC.</span><span class="sxs-lookup"><span data-stu-id="f1511-178">Timestamps are always in UTC.</span></span> <span data-ttu-id="f1511-179">So if you're on the US Pacific coast and it's winter, you might like this:</span><span class="sxs-lookup"><span data-stu-id="f1511-179">So if you're on the US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizeapp-insights-analytics-referencemdsummarize-operator-aggregate-groups-of-rows"></a><span data-ttu-id="f1511-180">[Summarize](app-insights-analytics-reference.md#summarize-operator): aggregate groups of rows</span><span class="sxs-lookup"><span data-stu-id="f1511-180">[Summarize](app-insights-analytics-reference.md#summarize-operator): aggregate groups of rows</span></span>
<span data-ttu-id="f1511-181">`Summarize` applies a specified *aggregation function* over groups of rows.</span><span class="sxs-lookup"><span data-stu-id="f1511-181">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="f1511-182">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span><span class="sxs-lookup"><span data-stu-id="f1511-182">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span></span> <span data-ttu-id="f1511-183">Let's see the average response time to all requests:</span><span class="sxs-lookup"><span data-stu-id="f1511-183">Let's see the average response time to all requests:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/410.png)

<span data-ttu-id="f1511-184">Or we could separate the result into requests of different names:</span><span class="sxs-lookup"><span data-stu-id="f1511-184">Or we could separate the result into requests of different names:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/420.png)

<span data-ttu-id="f1511-185">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span><span class="sxs-lookup"><span data-stu-id="f1511-185">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span></span> <span data-ttu-id="f1511-186">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span><span class="sxs-lookup"><span data-stu-id="f1511-186">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span></span>

<span data-ttu-id="f1511-187">Or we could group results by time of day:</span><span class="sxs-lookup"><span data-stu-id="f1511-187">Or we could group results by time of day:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/430.png)

<span data-ttu-id="f1511-188">Notice how we're using the `bin` function (aka `floor`).</span><span class="sxs-lookup"><span data-stu-id="f1511-188">Notice how we're using the `bin` function (aka `floor`).</span></span> <span data-ttu-id="f1511-189">If we just used `by timestamp`, every input row would end up in its own little group.</span><span class="sxs-lookup"><span data-stu-id="f1511-189">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="f1511-190">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span><span class="sxs-lookup"><span data-stu-id="f1511-190">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="f1511-191">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span><span class="sxs-lookup"><span data-stu-id="f1511-191">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span></span>

<span data-ttu-id="f1511-192">We can use the same technique to reduce ranges of strings:</span><span class="sxs-lookup"><span data-stu-id="f1511-192">We can use the same technique to reduce ranges of strings:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/440.png)

<span data-ttu-id="f1511-193">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span><span class="sxs-lookup"><span data-stu-id="f1511-193">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="f1511-194">Counting sampled data</span><span class="sxs-lookup"><span data-stu-id="f1511-194">Counting sampled data</span></span>
<span data-ttu-id="f1511-195">`sum(itemCount)` is the recommended aggregation to count events.</span><span class="sxs-lookup"><span data-stu-id="f1511-195">`sum(itemCount)` is the recommended aggregation to count events.</span></span> <span data-ttu-id="f1511-196">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span><span class="sxs-lookup"><span data-stu-id="f1511-196">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span></span> <span data-ttu-id="f1511-197">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span><span class="sxs-lookup"><span data-stu-id="f1511-197">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="f1511-198">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span><span class="sxs-lookup"><span data-stu-id="f1511-198">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="f1511-199">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span><span class="sxs-lookup"><span data-stu-id="f1511-199">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="f1511-200">Summing up itemCount therefore gives a good estimate of the original number of events.</span><span class="sxs-lookup"><span data-stu-id="f1511-200">Summing up itemCount therefore gives a good estimate of the original number of events.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/510.png)

<span data-ttu-id="f1511-201">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span><span class="sxs-lookup"><span data-stu-id="f1511-201">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span></span>

<span data-ttu-id="f1511-202">There's a range of [aggregation functions](app-insights-analytics-reference.md#aggregations).</span><span class="sxs-lookup"><span data-stu-id="f1511-202">There's a range of [aggregation functions](app-insights-analytics-reference.md#aggregations).</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="f1511-203">Charting the results</span><span class="sxs-lookup"><span data-stu-id="f1511-203">Charting the results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="f1511-204">By default, results display as a table:</span><span class="sxs-lookup"><span data-stu-id="f1511-204">By default, results display as a table:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/225.png)

<span data-ttu-id="f1511-205">We can do better than the table view.</span><span class="sxs-lookup"><span data-stu-id="f1511-205">We can do better than the table view.</span></span> <span data-ttu-id="f1511-206">Let's look at the results in the chart view with the vertical bar option:</span><span class="sxs-lookup"><span data-stu-id="f1511-206">Let's look at the results in the chart view with the vertical bar option:</span></span>

![Click Chart, then choose Vertical bar chart and assign x and y axes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/230.png)

<span data-ttu-id="f1511-208">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span><span class="sxs-lookup"><span data-stu-id="f1511-208">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="f1511-209">Timecharts</span><span class="sxs-lookup"><span data-stu-id="f1511-209">Timecharts</span></span>
<span data-ttu-id="f1511-210">Show how many events there are each hour:</span><span class="sxs-lookup"><span data-stu-id="f1511-210">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="f1511-211">Select the Chart display option:</span><span class="sxs-lookup"><span data-stu-id="f1511-211">Select the Chart display option:</span></span>

![timechart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="f1511-213">Multiple series</span><span class="sxs-lookup"><span data-stu-id="f1511-213">Multiple series</span></span>
<span data-ttu-id="f1511-214">Multiple expressions in the `summarize` clause creates multiple columns.</span><span class="sxs-lookup"><span data-stu-id="f1511-214">Multiple expressions in the `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="f1511-215">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span><span class="sxs-lookup"><span data-stu-id="f1511-215">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Table of requests by hour and location](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="f1511-217">Segment a chart by dimensions</span><span class="sxs-lookup"><span data-stu-id="f1511-217">Segment a chart by dimensions</span></span>
<span data-ttu-id="f1511-218">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span><span class="sxs-lookup"><span data-stu-id="f1511-218">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span></span> <span data-ttu-id="f1511-219">If there's more than one string column, you can choose which column to use as the discriminator.</span><span class="sxs-lookup"><span data-stu-id="f1511-219">If there's more than one string column, you can choose which column to use as the discriminator.</span></span>

![Segment an analytics chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="f1511-221">Bounce rate</span><span class="sxs-lookup"><span data-stu-id="f1511-221">Bounce rate</span></span>

<span data-ttu-id="f1511-222">Convert a boolean to a string to use it as a discriminator:</span><span class="sxs-lookup"><span data-stu-id="f1511-222">Convert a boolean to a string to use it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="f1511-223">Display multiple metrics</span><span class="sxs-lookup"><span data-stu-id="f1511-223">Display multiple metrics</span></span>
<span data-ttu-id="f1511-224">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span><span class="sxs-lookup"><span data-stu-id="f1511-224">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span></span>

![Segment an analytics chart](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/110.png)

<span data-ttu-id="f1511-226">You must select **Don't Split** before you can select multiple numeric columns.</span><span class="sxs-lookup"><span data-stu-id="f1511-226">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="f1511-227">You can't split by a string column at the same time as displaying more than one numeric column.</span><span class="sxs-lookup"><span data-stu-id="f1511-227">You can't split by a string column at the same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="f1511-228">Daily average cycle</span><span class="sxs-lookup"><span data-stu-id="f1511-228">Daily average cycle</span></span>
<span data-ttu-id="f1511-229">How does usage vary over the average day?</span><span class="sxs-lookup"><span data-stu-id="f1511-229">How does usage vary over the average day?</span></span>

<span data-ttu-id="f1511-230">Count requests by the time modulo one day, binned into hours:</span><span class="sxs-lookup"><span data-stu-id="f1511-230">Count requests by the time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Line chart of hours in an average day](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="f1511-232">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span><span class="sxs-lookup"><span data-stu-id="f1511-232">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="f1511-233">Compare multiple daily series</span><span class="sxs-lookup"><span data-stu-id="f1511-233">Compare multiple daily series</span></span>
<span data-ttu-id="f1511-234">How does usage vary over the time of day in different countries?</span><span class="sxs-lookup"><span data-stu-id="f1511-234">How does usage vary over the time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Split By client_CountryOrRegion](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="f1511-236">Plot a distribution</span><span class="sxs-lookup"><span data-stu-id="f1511-236">Plot a distribution</span></span>
<span data-ttu-id="f1511-237">How many sessions are there of different lengths?</span><span class="sxs-lookup"><span data-stu-id="f1511-237">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="f1511-238">The last line is required to convert to datetime.</span><span class="sxs-lookup"><span data-stu-id="f1511-238">The last line is required to convert to datetime.</span></span> <span data-ttu-id="f1511-239">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span><span class="sxs-lookup"><span data-stu-id="f1511-239">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="f1511-240">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span><span class="sxs-lookup"><span data-stu-id="f1511-240">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/290.png)

## <a name="percentilesapp-insights-analytics-referencemdpercentiles"></a>[<span data-ttu-id="f1511-241">Percentiles</span><span class="sxs-lookup"><span data-stu-id="f1511-241">Percentiles</span></span>](app-insights-analytics-reference.md#percentiles)
<span data-ttu-id="f1511-242">What ranges of durations cover different percentages of sessions?</span><span class="sxs-lookup"><span data-stu-id="f1511-242">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="f1511-243">Use the above query, but replace the last line:</span><span class="sxs-lookup"><span data-stu-id="f1511-243">Use the above query, but replace the last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="f1511-244">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span><span class="sxs-lookup"><span data-stu-id="f1511-244">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span></span>

![result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/180.png)

<span data-ttu-id="f1511-246">From which we can see that:</span><span class="sxs-lookup"><span data-stu-id="f1511-246">From which we can see that:</span></span>

* <span data-ttu-id="f1511-247">5% of sessions have a duration of less than 3 minutes 34s;</span><span class="sxs-lookup"><span data-stu-id="f1511-247">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="f1511-248">50% of sessions last less than 36 minutes;</span><span class="sxs-lookup"><span data-stu-id="f1511-248">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="f1511-249">5% of sessions last more than 7 days</span><span class="sxs-lookup"><span data-stu-id="f1511-249">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="f1511-250">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span><span class="sxs-lookup"><span data-stu-id="f1511-250">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="f1511-251">Join</span><span class="sxs-lookup"><span data-stu-id="f1511-251">Join</span></span>
<span data-ttu-id="f1511-252">We have access to several tables, including requests and exceptions.</span><span class="sxs-lookup"><span data-stu-id="f1511-252">We have access to several tables, including requests and exceptions.</span></span>

<span data-ttu-id="f1511-253">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="f1511-253">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="f1511-254">It's good practice to use `project` to select just the columns we need before performing the join.</span><span class="sxs-lookup"><span data-stu-id="f1511-254">It's good practice to use `project` to select just the columns we need before performing the join.</span></span>
<span data-ttu-id="f1511-255">In the same clauses, we rename the timestamp column.</span><span class="sxs-lookup"><span data-stu-id="f1511-255">In the same clauses, we rename the timestamp column.</span></span>

## <a name="letapp-insights-analytics-referencemdlet-clause-assign-a-result-to-a-variable"></a><span data-ttu-id="f1511-256">[Let](app-insights-analytics-reference.md#let-clause): Assign a result to a variable</span><span class="sxs-lookup"><span data-stu-id="f1511-256">[Let](app-insights-analytics-reference.md#let-clause): Assign a result to a variable</span></span>

<span data-ttu-id="f1511-257">Use `let` to separate out the parts of the previous expression.</span><span class="sxs-lookup"><span data-stu-id="f1511-257">Use `let` to separate out the parts of the previous expression.</span></span> <span data-ttu-id="f1511-258">The results are unchanged:</span><span class="sxs-lookup"><span data-stu-id="f1511-258">The results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="f1511-259">In the Analytics client, don't put blank lines between the parts of the query.</span><span class="sxs-lookup"><span data-stu-id="f1511-259">In the Analytics client, don't put blank lines between the parts of the query.</span></span> <span data-ttu-id="f1511-260">Make sure to execute all of it.</span><span class="sxs-lookup"><span data-stu-id="f1511-260">Make sure to execute all of it.</span></span>
>

<span data-ttu-id="f1511-261">Use `toscalar` to convert a single table cell to a value:</span><span class="sxs-lookup"><span data-stu-id="f1511-261">Use `toscalar` to convert a single table cell to a value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="f1511-262">Functions</span><span class="sxs-lookup"><span data-stu-id="f1511-262">Functions</span></span>

<span data-ttu-id="f1511-263">Use *Let* to define a function:</span><span class="sxs-lookup"><span data-stu-id="f1511-263">Use *Let* to define a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="f1511-264">Accessing nested objects</span><span class="sxs-lookup"><span data-stu-id="f1511-264">Accessing nested objects</span></span>
<span data-ttu-id="f1511-265">Nested objects can be accessed easily.</span><span class="sxs-lookup"><span data-stu-id="f1511-265">Nested objects can be accessed easily.</span></span> <span data-ttu-id="f1511-266">For example, in the exceptions stream you can see structured objects like this:</span><span class="sxs-lookup"><span data-stu-id="f1511-266">For example, in the exceptions stream you can see structured objects like this:</span></span>

![result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/520.png)

<span data-ttu-id="f1511-268">You can flatten it by choosing the properties you're interested in:</span><span class="sxs-lookup"><span data-stu-id="f1511-268">You can flatten it by choosing the properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="f1511-269">Note that you need to use a [cast](app-insights-analytics-reference.md#casts) to the appropriate type.</span><span class="sxs-lookup"><span data-stu-id="f1511-269">Note that you need to use a [cast](app-insights-analytics-reference.md#casts) to the appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="f1511-270">Custom properties and measurements</span><span class="sxs-lookup"><span data-stu-id="f1511-270">Custom properties and measurements</span></span>
<span data-ttu-id="f1511-271">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span><span class="sxs-lookup"><span data-stu-id="f1511-271">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="f1511-272">For example, if your app includes:</span><span class="sxs-lookup"><span data-stu-id="f1511-272">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="f1511-273">To extract these values in Analytics:</span><span class="sxs-lookup"><span data-stu-id="f1511-273">To extract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast to expected type

```

<span data-ttu-id="f1511-274">To verify whether a custom dimension is of a particular type:</span><span class="sxs-lookup"><span data-stu-id="f1511-274">To verify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="f1511-275">Dashboards</span><span class="sxs-lookup"><span data-stu-id="f1511-275">Dashboards</span></span>
<span data-ttu-id="f1511-276">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span><span class="sxs-lookup"><span data-stu-id="f1511-276">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span></span>

* <span data-ttu-id="f1511-277">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span><span class="sxs-lookup"><span data-stu-id="f1511-277">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span></span> <span data-ttu-id="f1511-278">Before you do this, you must have a shared dashboard.</span><span class="sxs-lookup"><span data-stu-id="f1511-278">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="f1511-279">In the Azure portal, open or create a dashboard and click Share.</span><span class="sxs-lookup"><span data-stu-id="f1511-279">In the Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="f1511-280">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span><span class="sxs-lookup"><span data-stu-id="f1511-280">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="f1511-281">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span><span class="sxs-lookup"><span data-stu-id="f1511-281">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="f1511-282">Combine with imported data</span><span class="sxs-lookup"><span data-stu-id="f1511-282">Combine with imported data</span></span>

<span data-ttu-id="f1511-283">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span><span class="sxs-lookup"><span data-stu-id="f1511-283">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span></span> <span data-ttu-id="f1511-284">For example, suppose your authenticated users are identified in the telemetry by an alias.</span><span class="sxs-lookup"><span data-stu-id="f1511-284">For example, suppose your authenticated users are identified in the telemetry by an alias.</span></span> <span data-ttu-id="f1511-285">You'd like to show their real names in your results.</span><span class="sxs-lookup"><span data-stu-id="f1511-285">You'd like to show their real names in your results.</span></span> <span data-ttu-id="f1511-286">To do this, you need a CSV file that maps from the aliases to the real names.</span><span class="sxs-lookup"><span data-stu-id="f1511-286">To do this, you need a CSV file that maps from the aliases to the real names.</span></span>

<span data-ttu-id="f1511-287">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span><span class="sxs-lookup"><span data-stu-id="f1511-287">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="f1511-288">Either query it on its own, or join it with other tables.</span><span class="sxs-lookup"><span data-stu-id="f1511-288">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="f1511-289">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span><span class="sxs-lookup"><span data-stu-id="f1511-289">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get the realName field from the usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="f1511-290">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span><span class="sxs-lookup"><span data-stu-id="f1511-290">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="f1511-291">Then you can use this definition to upload tables.</span><span class="sxs-lookup"><span data-stu-id="f1511-291">Then you can use this definition to upload tables.</span></span>

<span data-ttu-id="f1511-292">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span><span class="sxs-lookup"><span data-stu-id="f1511-292">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="f1511-293">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span><span class="sxs-lookup"><span data-stu-id="f1511-293">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="f1511-294">Tables</span><span class="sxs-lookup"><span data-stu-id="f1511-294">Tables</span></span>
<span data-ttu-id="f1511-295">The stream of telemetry received from your app is accessible through several tables.</span><span class="sxs-lookup"><span data-stu-id="f1511-295">The stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="f1511-296">The schema of properties available for each table is visible at the left of the window.</span><span class="sxs-lookup"><span data-stu-id="f1511-296">The schema of properties available for each table is visible at the left of the window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="f1511-297">Requests table</span><span class="sxs-lookup"><span data-stu-id="f1511-297">Requests table</span></span>
<span data-ttu-id="f1511-298">Count HTTP requests to your web app and segment by page name:</span><span class="sxs-lookup"><span data-stu-id="f1511-298">Count HTTP requests to your web app and segment by page name:</span></span>

![Count requests segmented by name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="f1511-300">Find the requests that fail most:</span><span class="sxs-lookup"><span data-stu-id="f1511-300">Find the requests that fail most:</span></span>

![Count requests segmented by name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="f1511-302">Custom events table</span><span class="sxs-lookup"><span data-stu-id="f1511-302">Custom events table</span></span>
<span data-ttu-id="f1511-303">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span><span class="sxs-lookup"><span data-stu-id="f1511-303">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span></span>

<span data-ttu-id="f1511-304">Let's take an example where your app code contains these lines:</span><span class="sxs-lookup"><span data-stu-id="f1511-304">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="f1511-305">Display the frequency of these events:</span><span class="sxs-lookup"><span data-stu-id="f1511-305">Display the frequency of these events:</span></span>

![Display rate of custom events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="f1511-307">Extract measurements and dimensions from the events:</span><span class="sxs-lookup"><span data-stu-id="f1511-307">Extract measurements and dimensions from the events:</span></span>

![Display rate of custom events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="f1511-309">Custom metrics table</span><span class="sxs-lookup"><span data-stu-id="f1511-309">Custom metrics table</span></span>
<span data-ttu-id="f1511-310">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span><span class="sxs-lookup"><span data-stu-id="f1511-310">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span></span> <span data-ttu-id="f1511-311">For example:</span><span class="sxs-lookup"><span data-stu-id="f1511-311">For example:</span></span>  

![Custom metrics in Application Insights analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="f1511-313">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="f1511-313">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="f1511-314">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span><span class="sxs-lookup"><span data-stu-id="f1511-314">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="f1511-315">Performance counters table</span><span class="sxs-lookup"><span data-stu-id="f1511-315">Performance counters table</span></span>
<span data-ttu-id="f1511-316">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span><span class="sxs-lookup"><span data-stu-id="f1511-316">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="f1511-317">You can configure the SDK to send additional counters, including your own custom counters.</span><span class="sxs-lookup"><span data-stu-id="f1511-317">You can configure the SDK to send additional counters, including your own custom counters.</span></span>

<span data-ttu-id="f1511-318">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span><span class="sxs-lookup"><span data-stu-id="f1511-318">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="f1511-319">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span><span class="sxs-lookup"><span data-stu-id="f1511-319">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span></span> <span data-ttu-id="f1511-320">In the telemetry for each application, you’ll see only the counters for that application.</span><span class="sxs-lookup"><span data-stu-id="f1511-320">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="f1511-321">For example, to see what counters are available:</span><span class="sxs-lookup"><span data-stu-id="f1511-321">For example, to see what counters are available:</span></span>

![Performance counters in Application Insights analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="f1511-323">To get a chart of available memory over the selected period:</span><span class="sxs-lookup"><span data-stu-id="f1511-323">To get a chart of available memory over the selected period:</span></span>

![Memory timechart in Application Insights analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="f1511-325">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span><span class="sxs-lookup"><span data-stu-id="f1511-325">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span></span> <span data-ttu-id="f1511-326">For example, to compare the performance of your app on the different machines:</span><span class="sxs-lookup"><span data-stu-id="f1511-326">For example, to compare the performance of your app on the different machines:</span></span>

![Performance segmented by role instance in Application Insights analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="f1511-328">Exceptions table</span><span class="sxs-lookup"><span data-stu-id="f1511-328">Exceptions table</span></span>
<span data-ttu-id="f1511-329">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span><span class="sxs-lookup"><span data-stu-id="f1511-329">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="f1511-330">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span><span class="sxs-lookup"><span data-stu-id="f1511-330">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span></span>

![Join exceptions with requests on operation_Id](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="f1511-332">Browser timings table</span><span class="sxs-lookup"><span data-stu-id="f1511-332">Browser timings table</span></span>
<span data-ttu-id="f1511-333">`browserTimings` shows page load data collected in your users' browsers.</span><span class="sxs-lookup"><span data-stu-id="f1511-333">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="f1511-334">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span><span class="sxs-lookup"><span data-stu-id="f1511-334">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span></span>

<span data-ttu-id="f1511-335">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="f1511-335">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="f1511-336">(They don’t indicate the length of time your users read a page.)</span><span class="sxs-lookup"><span data-stu-id="f1511-336">(They don’t indicate the length of time your users read a page.)</span></span>  

<span data-ttu-id="f1511-337">Show the popularities of different pages, and load times for each page:</span><span class="sxs-lookup"><span data-stu-id="f1511-337">Show the popularities of different pages, and load times for each page:</span></span>

![Page load times in Analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="f1511-339">Availability results table</span><span class="sxs-lookup"><span data-stu-id="f1511-339">Availability results table</span></span>
<span data-ttu-id="f1511-340">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="f1511-340">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="f1511-341">Each run of your tests from each test location is reported separately.</span><span class="sxs-lookup"><span data-stu-id="f1511-341">Each run of your tests from each test location is reported separately.</span></span>

![Page load times in Analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="f1511-343">Dependencies table</span><span class="sxs-lookup"><span data-stu-id="f1511-343">Dependencies table</span></span>
<span data-ttu-id="f1511-344">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span><span class="sxs-lookup"><span data-stu-id="f1511-344">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span></span> <span data-ttu-id="f1511-345">Also includes AJAX calls made from the browser.</span><span class="sxs-lookup"><span data-stu-id="f1511-345">Also includes AJAX calls made from the browser.</span></span>

<span data-ttu-id="f1511-346">AJAX calls from the browser:</span><span class="sxs-lookup"><span data-stu-id="f1511-346">AJAX calls from the browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="f1511-347">Dependency calls from the server:</span><span class="sxs-lookup"><span data-stu-id="f1511-347">Dependency calls from the server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="f1511-348">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span><span class="sxs-lookup"><span data-stu-id="f1511-348">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span></span> <span data-ttu-id="f1511-349">However, the other data are correct.</span><span class="sxs-lookup"><span data-stu-id="f1511-349">However, the other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="f1511-350">Traces table</span><span class="sxs-lookup"><span data-stu-id="f1511-350">Traces table</span></span>
<span data-ttu-id="f1511-351">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="f1511-351">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="f1511-352">Video</span><span class="sxs-lookup"><span data-stu-id="f1511-352">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="f1511-353">Advanced queries:</span><span class="sxs-lookup"><span data-stu-id="f1511-353">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="f1511-354">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1511-354">Next steps</span></span>
* [<span data-ttu-id="f1511-355">Analytics language reference</span><span class="sxs-lookup"><span data-stu-id="f1511-355">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="f1511-356">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span><span class="sxs-lookup"><span data-stu-id="f1511-356">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]





































