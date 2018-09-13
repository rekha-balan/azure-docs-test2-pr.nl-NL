---
title: Data Factory Functions and System Variables | Microsoft Docs
description: Provides a list of Azure Data Factory functions and system variables
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2017
ms.author: shlo
ms.openlocfilehash: 74f2fafdf7355bbce37cf2bf98a6e709ebb7986e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563771"
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="4c444-103">Azure Data Factory - Functions and System Variables</span><span class="sxs-lookup"><span data-stu-id="4c444-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="4c444-104">This article provides information about functions and variables supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4c444-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="4c444-105">Data Factory system variables</span><span class="sxs-lookup"><span data-stu-id="4c444-105">Data Factory system variables</span></span>
| <span data-ttu-id="4c444-106">Variable Name</span><span class="sxs-lookup"><span data-stu-id="4c444-106">Variable Name</span></span> | <span data-ttu-id="4c444-107">Description</span><span class="sxs-lookup"><span data-stu-id="4c444-107">Description</span></span> | <span data-ttu-id="4c444-108">Object Scope</span><span class="sxs-lookup"><span data-stu-id="4c444-108">Object Scope</span></span> | <span data-ttu-id="4c444-109">JSON Scope and Use Cases</span><span class="sxs-lookup"><span data-stu-id="4c444-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4c444-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="4c444-110">WindowStart</span></span> |<span data-ttu-id="4c444-111">Start of time interval for current activity run window</span><span class="sxs-lookup"><span data-stu-id="4c444-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="4c444-112">activity</span><span class="sxs-lookup"><span data-stu-id="4c444-112">activity</span></span> |<ol><li><span data-ttu-id="4c444-113">Specify data selection queries.</span><span class="sxs-lookup"><span data-stu-id="4c444-113">Specify data selection queries.</span></span> <span data-ttu-id="4c444-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="4c444-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="4c444-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="4c444-115">WindowEnd</span></span> |<span data-ttu-id="4c444-116">End of time interval for current activity run window</span><span class="sxs-lookup"><span data-stu-id="4c444-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="4c444-117">activity</span><span class="sxs-lookup"><span data-stu-id="4c444-117">activity</span></span> |<span data-ttu-id="4c444-118">same as above</span><span class="sxs-lookup"><span data-stu-id="4c444-118">same as above</span></span> |
| <span data-ttu-id="4c444-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="4c444-119">SliceStart</span></span> |<span data-ttu-id="4c444-120">Start of time interval for data  slice being produced</span><span class="sxs-lookup"><span data-stu-id="4c444-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="4c444-121">activity</span><span class="sxs-lookup"><span data-stu-id="4c444-121">activity</span></span><br/><span data-ttu-id="4c444-122">dataset</span><span class="sxs-lookup"><span data-stu-id="4c444-122">dataset</span></span> |<ol><li><span data-ttu-id="4c444-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="4c444-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="4c444-124">Specify input dependencies with data factory functions in activity inputs collection.</span><span class="sxs-lookup"><span data-stu-id="4c444-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="4c444-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="4c444-125">SliceEnd</span></span> |<span data-ttu-id="4c444-126">End of time interval for current data slice being produced</span><span class="sxs-lookup"><span data-stu-id="4c444-126">End of time interval for current data slice being produced</span></span> |<span data-ttu-id="4c444-127">activity</span><span class="sxs-lookup"><span data-stu-id="4c444-127">activity</span></span><br/><span data-ttu-id="4c444-128">dataset</span><span class="sxs-lookup"><span data-stu-id="4c444-128">dataset</span></span> |<span data-ttu-id="4c444-129">same as SliceStart.</span><span class="sxs-lookup"><span data-stu-id="4c444-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="4c444-130">Currently data factory requires that the schedule specified in the activity exactly match the schedule specified in availability of the output dataset.</span><span class="sxs-lookup"><span data-stu-id="4c444-130">Currently data factory requires that the schedule specified in the activity exactly match the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="4c444-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span><span class="sxs-lookup"><span data-stu-id="4c444-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="4c444-132">Example for using a system variable</span><span class="sxs-lookup"><span data-stu-id="4c444-132">Example for using a system variable</span></span>
<span data-ttu-id="4c444-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate , which are used by **folderPath** and **fileName** properties.</span><span class="sxs-lookup"><span data-stu-id="4c444-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate , which are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="4c444-134">Data Factory functions</span><span class="sxs-lookup"><span data-stu-id="4c444-134">Data Factory functions</span></span>
<span data-ttu-id="4c444-135">You can use functions in data factory along with system variables for the following purposes:</span><span class="sxs-lookup"><span data-stu-id="4c444-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="4c444-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="4c444-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="4c444-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span><span class="sxs-lookup"><span data-stu-id="4c444-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="4c444-138">Specifying input dependencies with data factory functions in activity inputs collection.</span><span class="sxs-lookup"><span data-stu-id="4c444-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="4c444-139">$$ is not needed for specifying input dependency expressions.</span><span class="sxs-lookup"><span data-stu-id="4c444-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="4c444-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span><span class="sxs-lookup"><span data-stu-id="4c444-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="4c444-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span><span class="sxs-lookup"><span data-stu-id="4c444-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="4c444-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span><span class="sxs-lookup"><span data-stu-id="4c444-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="4c444-143">Functions</span><span class="sxs-lookup"><span data-stu-id="4c444-143">Functions</span></span>
<span data-ttu-id="4c444-144">The following tables list all the functions in Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="4c444-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="4c444-145">Category</span><span class="sxs-lookup"><span data-stu-id="4c444-145">Category</span></span> | <span data-ttu-id="4c444-146">Function</span><span class="sxs-lookup"><span data-stu-id="4c444-146">Function</span></span> | <span data-ttu-id="4c444-147">Parameters</span><span class="sxs-lookup"><span data-stu-id="4c444-147">Parameters</span></span> | <span data-ttu-id="4c444-148">Description</span><span class="sxs-lookup"><span data-stu-id="4c444-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4c444-149">Time</span><span class="sxs-lookup"><span data-stu-id="4c444-149">Time</span></span> |<span data-ttu-id="4c444-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="4c444-150">AddHours(X,Y)</span></span> |<span data-ttu-id="4c444-151">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="4c444-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="4c444-152">Y: int</span></span> |<span data-ttu-id="4c444-153">Adds Y hours to the given time X.</span><span class="sxs-lookup"><span data-stu-id="4c444-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="4c444-154">Example: 9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="4c444-154">Example: 9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM</span></span> |
| <span data-ttu-id="4c444-155">Time</span><span class="sxs-lookup"><span data-stu-id="4c444-155">Time</span></span> |<span data-ttu-id="4c444-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="4c444-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="4c444-157">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="4c444-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="4c444-158">Y: int</span></span> |<span data-ttu-id="4c444-159">Adds Y minutes to X.</span><span class="sxs-lookup"><span data-stu-id="4c444-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="4c444-160">Example: 9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM</span><span class="sxs-lookup"><span data-stu-id="4c444-160">Example: 9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM</span></span> |
| <span data-ttu-id="4c444-161">Time</span><span class="sxs-lookup"><span data-stu-id="4c444-161">Time</span></span> |<span data-ttu-id="4c444-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-162">StartOfHour(X)</span></span> |<span data-ttu-id="4c444-163">X: Datetime</span><span class="sxs-lookup"><span data-stu-id="4c444-163">X: Datetime</span></span> |<span data-ttu-id="4c444-164">Gets the starting time for the hour represented by the hour component of X.</span><span class="sxs-lookup"><span data-stu-id="4c444-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="4c444-165">Example: StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM</span><span class="sxs-lookup"><span data-stu-id="4c444-165">Example: StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM</span></span> |
| <span data-ttu-id="4c444-166">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-166">Date</span></span> |<span data-ttu-id="4c444-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="4c444-167">AddDays(X,Y)</span></span> |<span data-ttu-id="4c444-168">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-168">X: DateTime</span></span><br/><br/><span data-ttu-id="4c444-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="4c444-169">Y: int</span></span> |<span data-ttu-id="4c444-170">Adds Y days to X.</span><span class="sxs-lookup"><span data-stu-id="4c444-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="4c444-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="4c444-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="4c444-172">You can subtract days too by specifying Y as a negative number.</span><span class="sxs-lookup"><span data-stu-id="4c444-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="4c444-173">Example: 9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="4c444-173">Example: 9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM.</span></span> |
| <span data-ttu-id="4c444-174">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-174">Date</span></span> |<span data-ttu-id="4c444-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="4c444-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="4c444-176">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-176">X: DateTime</span></span><br/><br/><span data-ttu-id="4c444-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="4c444-177">Y: int</span></span> |<span data-ttu-id="4c444-178">Adds Y months to X.</span><span class="sxs-lookup"><span data-stu-id="4c444-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="4c444-179">Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="4c444-179">Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="4c444-180">You can subtract months too by specifying Y as a negative number.</span><span class="sxs-lookup"><span data-stu-id="4c444-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="4c444-181">Example: 9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="4c444-181">Example: 9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM.</span></span>|
| <span data-ttu-id="4c444-182">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-182">Date</span></span> |<span data-ttu-id="4c444-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="4c444-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="4c444-184">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="4c444-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="4c444-185">Y: int</span></span> |<span data-ttu-id="4c444-186">Adds Y \* 3 months to X.</span><span class="sxs-lookup"><span data-stu-id="4c444-186">Adds Y \* 3 months to X.</span></span><br/><br/><span data-ttu-id="4c444-187">Example: 9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="4c444-187">Example: 9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM</span></span> |
| <span data-ttu-id="4c444-188">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-188">Date</span></span> |<span data-ttu-id="4c444-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="4c444-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="4c444-190">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-190">X: DateTime</span></span><br/><br/><span data-ttu-id="4c444-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="4c444-191">Y: int</span></span> |<span data-ttu-id="4c444-192">Adds Y \* 7 days to X</span><span class="sxs-lookup"><span data-stu-id="4c444-192">Adds Y \* 7 days to X</span></span><br/><br/><span data-ttu-id="4c444-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="4c444-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="4c444-194">You can subtract weeks too by specifying Y as a negative number.</span><span class="sxs-lookup"><span data-stu-id="4c444-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="4c444-195">Example: 9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="4c444-195">Example: 9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM.</span></span> |
| <span data-ttu-id="4c444-196">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-196">Date</span></span> |<span data-ttu-id="4c444-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="4c444-197">AddYears(X,Y)</span></span> |<span data-ttu-id="4c444-198">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-198">X: DateTime</span></span><br/><br/><span data-ttu-id="4c444-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="4c444-199">Y: int</span></span> |<span data-ttu-id="4c444-200">Adds Y years to X.</span><span class="sxs-lookup"><span data-stu-id="4c444-200">Adds Y years to X.</span></span><br/><br/><span data-ttu-id="4c444-201">Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="4c444-201">Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM</span></span><br/><br/><span data-ttu-id="4c444-202">You can subtract years too by specifying Y as a negative number.</span><span class="sxs-lookup"><span data-stu-id="4c444-202">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="4c444-203">Example: 9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="4c444-203">Example: 9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM.</span></span> |
| <span data-ttu-id="4c444-204">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-204">Date</span></span> |<span data-ttu-id="4c444-205">Day(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-205">Day(X)</span></span> |<span data-ttu-id="4c444-206">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-206">X: DateTime</span></span> |<span data-ttu-id="4c444-207">Gets the day component of X.</span><span class="sxs-lookup"><span data-stu-id="4c444-207">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="4c444-208">Example: Day of 9/15/2013 12:00:00 PM is 9.</span><span class="sxs-lookup"><span data-stu-id="4c444-208">Example: Day of 9/15/2013 12:00:00 PM is 9.</span></span> |
| <span data-ttu-id="4c444-209">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-209">Date</span></span> |<span data-ttu-id="4c444-210">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-210">DayOfWeek(X)</span></span> |<span data-ttu-id="4c444-211">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-211">X: DateTime</span></span> |<span data-ttu-id="4c444-212">Gets the day of week component of X.</span><span class="sxs-lookup"><span data-stu-id="4c444-212">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="4c444-213">Example: DayOfWeek of 9/15/2013 12:00:00 PM is Sunday.</span><span class="sxs-lookup"><span data-stu-id="4c444-213">Example: DayOfWeek of 9/15/2013 12:00:00 PM is Sunday.</span></span> |
| <span data-ttu-id="4c444-214">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-214">Date</span></span> |<span data-ttu-id="4c444-215">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-215">DayOfYear(X)</span></span> |<span data-ttu-id="4c444-216">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-216">X: DateTime</span></span> |<span data-ttu-id="4c444-217">Gets the day in the year represented by the year component of X.</span><span class="sxs-lookup"><span data-stu-id="4c444-217">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="4c444-218">Examples:</span><span class="sxs-lookup"><span data-stu-id="4c444-218">Examples:</span></span><br/><span data-ttu-id="4c444-219">12/1/2015: day 335 of 2015</span><span class="sxs-lookup"><span data-stu-id="4c444-219">12/1/2015: day 335 of 2015</span></span><br/><span data-ttu-id="4c444-220">12/31/2015: day 365 of 2015</span><span class="sxs-lookup"><span data-stu-id="4c444-220">12/31/2015: day 365 of 2015</span></span><br/><span data-ttu-id="4c444-221">12/31/2016: day 366 of 2016 (Leap Year)</span><span class="sxs-lookup"><span data-stu-id="4c444-221">12/31/2016: day 366 of 2016 (Leap Year)</span></span> |
| <span data-ttu-id="4c444-222">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-222">Date</span></span> |<span data-ttu-id="4c444-223">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-223">DaysInMonth(X)</span></span> |<span data-ttu-id="4c444-224">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-224">X: DateTime</span></span> |<span data-ttu-id="4c444-225">Gets the days in the month represented by the month component of parameter X.</span><span class="sxs-lookup"><span data-stu-id="4c444-225">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="4c444-226">Example: DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month.</span><span class="sxs-lookup"><span data-stu-id="4c444-226">Example: DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month.</span></span> |
| <span data-ttu-id="4c444-227">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-227">Date</span></span> |<span data-ttu-id="4c444-228">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-228">EndOfDay(X)</span></span> |<span data-ttu-id="4c444-229">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-229">X: DateTime</span></span> |<span data-ttu-id="4c444-230">Gets the date-time that represents the end of the day (day component) of X.</span><span class="sxs-lookup"><span data-stu-id="4c444-230">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="4c444-231">Example: EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM.</span><span class="sxs-lookup"><span data-stu-id="4c444-231">Example: EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM.</span></span> |
| <span data-ttu-id="4c444-232">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-232">Date</span></span> |<span data-ttu-id="4c444-233">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-233">EndOfMonth(X)</span></span> |<span data-ttu-id="4c444-234">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-234">X: DateTime</span></span> |<span data-ttu-id="4c444-235">Gets the end of the month represented by month component of parameter X.</span><span class="sxs-lookup"><span data-stu-id="4c444-235">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="4c444-236">Example: EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM (date time that represents the end of September month)</span><span class="sxs-lookup"><span data-stu-id="4c444-236">Example: EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="4c444-237">Date</span><span class="sxs-lookup"><span data-stu-id="4c444-237">Date</span></span> |<span data-ttu-id="4c444-238">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-238">StartOfDay(X)</span></span> |<span data-ttu-id="4c444-239">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-239">X: DateTime</span></span> |<span data-ttu-id="4c444-240">Gets the start of the day represented by the day component of parameter X.</span><span class="sxs-lookup"><span data-stu-id="4c444-240">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="4c444-241">Example: StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM.</span><span class="sxs-lookup"><span data-stu-id="4c444-241">Example: StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM.</span></span> |
| <span data-ttu-id="4c444-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-242">DateTime</span></span> |<span data-ttu-id="4c444-243">From(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-243">From(X)</span></span> |<span data-ttu-id="4c444-244">X: String</span><span class="sxs-lookup"><span data-stu-id="4c444-244">X: String</span></span> |<span data-ttu-id="4c444-245">Parse string X to a date time.</span><span class="sxs-lookup"><span data-stu-id="4c444-245">Parse string X to a date time.</span></span> |
| <span data-ttu-id="4c444-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-246">DateTime</span></span> |<span data-ttu-id="4c444-247">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-247">Ticks(X)</span></span> |<span data-ttu-id="4c444-248">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="4c444-248">X: DateTime</span></span> |<span data-ttu-id="4c444-249">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span><span class="sxs-lookup"><span data-stu-id="4c444-249">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="4c444-250">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span><span class="sxs-lookup"><span data-stu-id="4c444-250">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="4c444-251">Text</span><span class="sxs-lookup"><span data-stu-id="4c444-251">Text</span></span> |<span data-ttu-id="4c444-252">Format(X)</span><span class="sxs-lookup"><span data-stu-id="4c444-252">Format(X)</span></span> |<span data-ttu-id="4c444-253">X: String variable</span><span class="sxs-lookup"><span data-stu-id="4c444-253">X: String variable</span></span> |<span data-ttu-id="4c444-254">Formats the text.</span><span class="sxs-lookup"><span data-stu-id="4c444-254">Formats the text.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="4c444-255">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span><span class="sxs-lookup"><span data-stu-id="4c444-255">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="4c444-256">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="4c444-256">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="4c444-257">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span><span class="sxs-lookup"><span data-stu-id="4c444-257">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="4c444-258">Example</span><span class="sxs-lookup"><span data-stu-id="4c444-258">Example</span></span>
<span data-ttu-id="4c444-259">In the following example, input and output parameters for the Hive activity are determined by using the Text.Format function and SliceStart system variable.</span><span class="sxs-lookup"><span data-stu-id="4c444-259">In the following example, input and output parameters for the Hive activity are determined by using the Text.Format function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:%M}/dayno={0:%d}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:%M}/dayno={0:%d}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="4c444-260">Example 2</span><span class="sxs-lookup"><span data-stu-id="4c444-260">Example 2</span></span>

<span data-ttu-id="4c444-261">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.Format function and the SliceStart variable.</span><span class="sxs-lookup"><span data-stu-id="4c444-261">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.Format function and the SliceStart variable.</span></span> 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="4c444-262">Example 3</span><span class="sxs-lookup"><span data-stu-id="4c444-262">Example 3</span></span>
<span data-ttu-id="4c444-263">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="4c444-263">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:%M}',WindowStart)",
                        "Day": "$$Text.Format('{0:%d}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="4c444-264">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span><span class="sxs-lookup"><span data-stu-id="4c444-264">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

