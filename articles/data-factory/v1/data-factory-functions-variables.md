---
title: Data Factory Functions and System Variables | Microsoft Docs
description: Provides a list of Azure Data Factory functions and system variables
documentationcenter: ''
author: sharonlo101
manager: craigg
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: b4d9a684c2c21ed9ec00b04963432f9ebcff7493
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864712"
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="76960-103">Azure Data Factory - Functions and System Variables</span><span class="sxs-lookup"><span data-stu-id="76960-103">Azure Data Factory - Functions and System Variables</span></span>
> [!NOTE]
> <span data-ttu-id="76960-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76960-104">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="76960-105">If you are using the current version of the Data Factory service, see [System variables in Data Factory](../control-flow-system-variables.md).</span><span class="sxs-lookup"><span data-stu-id="76960-105">If you are using the current version of the Data Factory service, see [System variables in Data Factory](../control-flow-system-variables.md).</span></span>

<span data-ttu-id="76960-106">This article provides information about functions and variables supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76960-106">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="76960-107">Data Factory system variables</span><span class="sxs-lookup"><span data-stu-id="76960-107">Data Factory system variables</span></span>
| <span data-ttu-id="76960-108">Variable Name</span><span class="sxs-lookup"><span data-stu-id="76960-108">Variable Name</span></span> | <span data-ttu-id="76960-109">Description</span><span class="sxs-lookup"><span data-stu-id="76960-109">Description</span></span> | <span data-ttu-id="76960-110">Object Scope</span><span class="sxs-lookup"><span data-stu-id="76960-110">Object Scope</span></span> | <span data-ttu-id="76960-111">JSON Scope and Use Cases</span><span class="sxs-lookup"><span data-stu-id="76960-111">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="76960-112">WindowStart</span><span class="sxs-lookup"><span data-stu-id="76960-112">WindowStart</span></span> |<span data-ttu-id="76960-113">Start of time interval for current activity run window</span><span class="sxs-lookup"><span data-stu-id="76960-113">Start of time interval for current activity run window</span></span> |<span data-ttu-id="76960-114">activity</span><span class="sxs-lookup"><span data-stu-id="76960-114">activity</span></span> |<ol><li><span data-ttu-id="76960-115">Specify data selection queries.</span><span class="sxs-lookup"><span data-stu-id="76960-115">Specify data selection queries.</span></span> <span data-ttu-id="76960-116">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="76960-116">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="76960-117">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="76960-117">WindowEnd</span></span> |<span data-ttu-id="76960-118">End of time interval for current activity run window</span><span class="sxs-lookup"><span data-stu-id="76960-118">End of time interval for current activity run window</span></span> |<span data-ttu-id="76960-119">activity</span><span class="sxs-lookup"><span data-stu-id="76960-119">activity</span></span> |<span data-ttu-id="76960-120">same as WindowStart.</span><span class="sxs-lookup"><span data-stu-id="76960-120">same as WindowStart.</span></span> |
| <span data-ttu-id="76960-121">SliceStart</span><span class="sxs-lookup"><span data-stu-id="76960-121">SliceStart</span></span> |<span data-ttu-id="76960-122">Start of time interval for data  slice being produced</span><span class="sxs-lookup"><span data-stu-id="76960-122">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="76960-123">activity</span><span class="sxs-lookup"><span data-stu-id="76960-123">activity</span></span><br/><span data-ttu-id="76960-124">dataset</span><span class="sxs-lookup"><span data-stu-id="76960-124">dataset</span></span> |<ol><li><span data-ttu-id="76960-125">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="76960-125">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="76960-126">Specify input dependencies with data factory functions in activity inputs collection.</span><span class="sxs-lookup"><span data-stu-id="76960-126">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="76960-127">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="76960-127">SliceEnd</span></span> |<span data-ttu-id="76960-128">End of time interval for current data slice.</span><span class="sxs-lookup"><span data-stu-id="76960-128">End of time interval for current data slice.</span></span> |<span data-ttu-id="76960-129">activity</span><span class="sxs-lookup"><span data-stu-id="76960-129">activity</span></span><br/><span data-ttu-id="76960-130">dataset</span><span class="sxs-lookup"><span data-stu-id="76960-130">dataset</span></span> |<span data-ttu-id="76960-131">same as SliceStart.</span><span class="sxs-lookup"><span data-stu-id="76960-131">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="76960-132">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span><span class="sxs-lookup"><span data-stu-id="76960-132">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="76960-133">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span><span class="sxs-lookup"><span data-stu-id="76960-133">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="76960-134">Example for using a system variable</span><span class="sxs-lookup"><span data-stu-id="76960-134">Example for using a system variable</span></span>
<span data-ttu-id="76960-135">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span><span class="sxs-lookup"><span data-stu-id="76960-135">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="76960-136">Data Factory functions</span><span class="sxs-lookup"><span data-stu-id="76960-136">Data Factory functions</span></span>
<span data-ttu-id="76960-137">You can use functions in data factory along with system variables for the following purposes:</span><span class="sxs-lookup"><span data-stu-id="76960-137">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="76960-138">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="76960-138">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="76960-139">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span><span class="sxs-lookup"><span data-stu-id="76960-139">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="76960-140">Specifying input dependencies with data factory functions in activity inputs collection.</span><span class="sxs-lookup"><span data-stu-id="76960-140">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="76960-141">$$ is not needed for specifying input dependency expressions.</span><span class="sxs-lookup"><span data-stu-id="76960-141">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="76960-142">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span><span class="sxs-lookup"><span data-stu-id="76960-142">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="76960-143">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span><span class="sxs-lookup"><span data-stu-id="76960-143">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="76960-144">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span><span class="sxs-lookup"><span data-stu-id="76960-144">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="76960-145">Functions</span><span class="sxs-lookup"><span data-stu-id="76960-145">Functions</span></span>
<span data-ttu-id="76960-146">The following tables list all the functions in Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="76960-146">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="76960-147">Category</span><span class="sxs-lookup"><span data-stu-id="76960-147">Category</span></span> | <span data-ttu-id="76960-148">Function</span><span class="sxs-lookup"><span data-stu-id="76960-148">Function</span></span> | <span data-ttu-id="76960-149">Parameters</span><span class="sxs-lookup"><span data-stu-id="76960-149">Parameters</span></span> | <span data-ttu-id="76960-150">Description</span><span class="sxs-lookup"><span data-stu-id="76960-150">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="76960-151">Time</span><span class="sxs-lookup"><span data-stu-id="76960-151">Time</span></span> |<span data-ttu-id="76960-152">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="76960-152">AddHours(X,Y)</span></span> |<span data-ttu-id="76960-153">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-153">X: DateTime</span></span> <br/><br/><span data-ttu-id="76960-154">Y: int</span><span class="sxs-lookup"><span data-stu-id="76960-154">Y: int</span></span> |<span data-ttu-id="76960-155">Adds Y hours to the given time X.</span><span class="sxs-lookup"><span data-stu-id="76960-155">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="76960-156">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="76960-156">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="76960-157">Time</span><span class="sxs-lookup"><span data-stu-id="76960-157">Time</span></span> |<span data-ttu-id="76960-158">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="76960-158">AddMinutes(X,Y)</span></span> |<span data-ttu-id="76960-159">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-159">X: DateTime</span></span> <br/><br/><span data-ttu-id="76960-160">Y: int</span><span class="sxs-lookup"><span data-stu-id="76960-160">Y: int</span></span> |<span data-ttu-id="76960-161">Adds Y minutes to X.</span><span class="sxs-lookup"><span data-stu-id="76960-161">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="76960-162">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="76960-162">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="76960-163">Time</span><span class="sxs-lookup"><span data-stu-id="76960-163">Time</span></span> |<span data-ttu-id="76960-164">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="76960-164">StartOfHour(X)</span></span> |<span data-ttu-id="76960-165">X: Datetime</span><span class="sxs-lookup"><span data-stu-id="76960-165">X: Datetime</span></span> |<span data-ttu-id="76960-166">Gets the starting time for the hour represented by the hour component of X.</span><span class="sxs-lookup"><span data-stu-id="76960-166">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="76960-167">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="76960-167">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="76960-168">Date</span><span class="sxs-lookup"><span data-stu-id="76960-168">Date</span></span> |<span data-ttu-id="76960-169">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="76960-169">AddDays(X,Y)</span></span> |<span data-ttu-id="76960-170">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-170">X: DateTime</span></span><br/><br/><span data-ttu-id="76960-171">Y: int</span><span class="sxs-lookup"><span data-stu-id="76960-171">Y: int</span></span> |<span data-ttu-id="76960-172">Adds Y days to X.</span><span class="sxs-lookup"><span data-stu-id="76960-172">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="76960-173">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="76960-173">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="76960-174">You can subtract days too by specifying Y as a negative number.</span><span class="sxs-lookup"><span data-stu-id="76960-174">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="76960-175">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="76960-175">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="76960-176">Date</span><span class="sxs-lookup"><span data-stu-id="76960-176">Date</span></span> |<span data-ttu-id="76960-177">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="76960-177">AddMonths(X,Y)</span></span> |<span data-ttu-id="76960-178">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-178">X: DateTime</span></span><br/><br/><span data-ttu-id="76960-179">Y: int</span><span class="sxs-lookup"><span data-stu-id="76960-179">Y: int</span></span> |<span data-ttu-id="76960-180">Adds Y months to X.</span><span class="sxs-lookup"><span data-stu-id="76960-180">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="76960-181">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="76960-181">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="76960-182">You can subtract months too by specifying Y as a negative number.</span><span class="sxs-lookup"><span data-stu-id="76960-182">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="76960-183">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="76960-183">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="76960-184">Date</span><span class="sxs-lookup"><span data-stu-id="76960-184">Date</span></span> |<span data-ttu-id="76960-185">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="76960-185">AddQuarters(X,Y)</span></span> |<span data-ttu-id="76960-186">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-186">X: DateTime</span></span> <br/><br/><span data-ttu-id="76960-187">Y: int</span><span class="sxs-lookup"><span data-stu-id="76960-187">Y: int</span></span> |<span data-ttu-id="76960-188">Adds Y \* 3 months to X.</span><span class="sxs-lookup"><span data-stu-id="76960-188">Adds Y \* 3 months to X.</span></span><br/><br/><span data-ttu-id="76960-189">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="76960-189">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="76960-190">Date</span><span class="sxs-lookup"><span data-stu-id="76960-190">Date</span></span> |<span data-ttu-id="76960-191">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="76960-191">AddWeeks(X,Y)</span></span> |<span data-ttu-id="76960-192">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-192">X: DateTime</span></span><br/><br/><span data-ttu-id="76960-193">Y: int</span><span class="sxs-lookup"><span data-stu-id="76960-193">Y: int</span></span> |<span data-ttu-id="76960-194">Adds Y \* 7 days to X</span><span class="sxs-lookup"><span data-stu-id="76960-194">Adds Y \* 7 days to X</span></span><br/><br/><span data-ttu-id="76960-195">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="76960-195">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="76960-196">You can subtract weeks too by specifying Y as a negative number.</span><span class="sxs-lookup"><span data-stu-id="76960-196">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="76960-197">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="76960-197">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="76960-198">Date</span><span class="sxs-lookup"><span data-stu-id="76960-198">Date</span></span> |<span data-ttu-id="76960-199">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="76960-199">AddYears(X,Y)</span></span> |<span data-ttu-id="76960-200">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-200">X: DateTime</span></span><br/><br/><span data-ttu-id="76960-201">Y: int</span><span class="sxs-lookup"><span data-stu-id="76960-201">Y: int</span></span> |<span data-ttu-id="76960-202">Adds Y years to X.</span><span class="sxs-lookup"><span data-stu-id="76960-202">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="76960-203">You can subtract years too by specifying Y as a negative number.</span><span class="sxs-lookup"><span data-stu-id="76960-203">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="76960-204">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="76960-204">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="76960-205">Date</span><span class="sxs-lookup"><span data-stu-id="76960-205">Date</span></span> |<span data-ttu-id="76960-206">Day(X)</span><span class="sxs-lookup"><span data-stu-id="76960-206">Day(X)</span></span> |<span data-ttu-id="76960-207">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-207">X: DateTime</span></span> |<span data-ttu-id="76960-208">Gets the day component of X.</span><span class="sxs-lookup"><span data-stu-id="76960-208">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="76960-209">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="76960-209">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="76960-210">Date</span><span class="sxs-lookup"><span data-stu-id="76960-210">Date</span></span> |<span data-ttu-id="76960-211">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="76960-211">DayOfWeek(X)</span></span> |<span data-ttu-id="76960-212">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-212">X: DateTime</span></span> |<span data-ttu-id="76960-213">Gets the day of week component of X.</span><span class="sxs-lookup"><span data-stu-id="76960-213">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="76960-214">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="76960-214">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="76960-215">Date</span><span class="sxs-lookup"><span data-stu-id="76960-215">Date</span></span> |<span data-ttu-id="76960-216">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="76960-216">DayOfYear(X)</span></span> |<span data-ttu-id="76960-217">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-217">X: DateTime</span></span> |<span data-ttu-id="76960-218">Gets the day in the year represented by the year component of X.</span><span class="sxs-lookup"><span data-stu-id="76960-218">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="76960-219">Examples:</span><span class="sxs-lookup"><span data-stu-id="76960-219">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="76960-220">Date</span><span class="sxs-lookup"><span data-stu-id="76960-220">Date</span></span> |<span data-ttu-id="76960-221">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="76960-221">DaysInMonth(X)</span></span> |<span data-ttu-id="76960-222">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-222">X: DateTime</span></span> |<span data-ttu-id="76960-223">Gets the days in the month represented by the month component of parameter X.</span><span class="sxs-lookup"><span data-stu-id="76960-223">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="76960-224">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="76960-224">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="76960-225">Date</span><span class="sxs-lookup"><span data-stu-id="76960-225">Date</span></span> |<span data-ttu-id="76960-226">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="76960-226">EndOfDay(X)</span></span> |<span data-ttu-id="76960-227">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-227">X: DateTime</span></span> |<span data-ttu-id="76960-228">Gets the date-time that represents the end of the day (day component) of X.</span><span class="sxs-lookup"><span data-stu-id="76960-228">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="76960-229">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="76960-229">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="76960-230">Date</span><span class="sxs-lookup"><span data-stu-id="76960-230">Date</span></span> |<span data-ttu-id="76960-231">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="76960-231">EndOfMonth(X)</span></span> |<span data-ttu-id="76960-232">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-232">X: DateTime</span></span> |<span data-ttu-id="76960-233">Gets the end of the month represented by month component of parameter X.</span><span class="sxs-lookup"><span data-stu-id="76960-233">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="76960-234">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span><span class="sxs-lookup"><span data-stu-id="76960-234">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="76960-235">Date</span><span class="sxs-lookup"><span data-stu-id="76960-235">Date</span></span> |<span data-ttu-id="76960-236">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="76960-236">StartOfDay(X)</span></span> |<span data-ttu-id="76960-237">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-237">X: DateTime</span></span> |<span data-ttu-id="76960-238">Gets the start of the day represented by the day component of parameter X.</span><span class="sxs-lookup"><span data-stu-id="76960-238">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="76960-239">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="76960-239">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="76960-240">DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-240">DateTime</span></span> |<span data-ttu-id="76960-241">From(X)</span><span class="sxs-lookup"><span data-stu-id="76960-241">From(X)</span></span> |<span data-ttu-id="76960-242">X: String</span><span class="sxs-lookup"><span data-stu-id="76960-242">X: String</span></span> |<span data-ttu-id="76960-243">Parse string X to a date time.</span><span class="sxs-lookup"><span data-stu-id="76960-243">Parse string X to a date time.</span></span> |
| <span data-ttu-id="76960-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-244">DateTime</span></span> |<span data-ttu-id="76960-245">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="76960-245">Ticks(X)</span></span> |<span data-ttu-id="76960-246">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="76960-246">X: DateTime</span></span> |<span data-ttu-id="76960-247">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span><span class="sxs-lookup"><span data-stu-id="76960-247">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="76960-248">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span><span class="sxs-lookup"><span data-stu-id="76960-248">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="76960-249">Text</span><span class="sxs-lookup"><span data-stu-id="76960-249">Text</span></span> |<span data-ttu-id="76960-250">Format(X)</span><span class="sxs-lookup"><span data-stu-id="76960-250">Format(X)</span></span> |<span data-ttu-id="76960-251">X: String variable</span><span class="sxs-lookup"><span data-stu-id="76960-251">X: String variable</span></span> |<span data-ttu-id="76960-252">Formats the text (use `\\'` combination to escape `'` character).</span><span class="sxs-lookup"><span data-stu-id="76960-252">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="76960-253">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span><span class="sxs-lookup"><span data-stu-id="76960-253">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="76960-254">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="76960-254">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="76960-255">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span><span class="sxs-lookup"><span data-stu-id="76960-255">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="76960-256">Example</span><span class="sxs-lookup"><span data-stu-id="76960-256">Example</span></span>
<span data-ttu-id="76960-257">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span><span class="sxs-lookup"><span data-stu-id="76960-257">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

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
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
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

### <a name="example-2"></a><span data-ttu-id="76960-258">Example 2</span><span class="sxs-lookup"><span data-stu-id="76960-258">Example 2</span></span>

<span data-ttu-id="76960-259">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span><span class="sxs-lookup"><span data-stu-id="76960-259">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="76960-260">Format function and the SliceStart variable.</span><span class="sxs-lookup"><span data-stu-id="76960-260">Format function and the SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="76960-261">Example 3</span><span class="sxs-lookup"><span data-stu-id="76960-261">Example 3</span></span>
<span data-ttu-id="76960-262">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="76960-262">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

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
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
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

<span data-ttu-id="76960-263">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span><span class="sxs-lookup"><span data-stu-id="76960-263">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

