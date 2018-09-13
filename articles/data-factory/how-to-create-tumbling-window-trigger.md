---
title: Create tumbling window triggers in Azure Data Factory | Microsoft Docs
description: Learn how to create a trigger in Azure Data Factory that runs a pipeline on a tumbling window.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/27/2018
ms.author: shlo
ms.openlocfilehash: c42d6235af8a5ab27fbd550b63c301fd9c6f15b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865420"
---
# <a name="create-a-trigger-that-runs-a-pipeline-on-a-tumbling-window"></a><span data-ttu-id="c0feb-103">Create a trigger that runs a pipeline on a tumbling window</span><span class="sxs-lookup"><span data-stu-id="c0feb-103">Create a trigger that runs a pipeline on a tumbling window</span></span>
<span data-ttu-id="c0feb-104">This article provides steps to create, start, and monitor a tumbling window trigger.</span><span class="sxs-lookup"><span data-stu-id="c0feb-104">This article provides steps to create, start, and monitor a tumbling window trigger.</span></span> <span data-ttu-id="c0feb-105">For general information about triggers and the supported types, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md).</span><span class="sxs-lookup"><span data-stu-id="c0feb-105">For general information about triggers and the supported types, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md).</span></span>

<span data-ttu-id="c0feb-106">Tumbling window triggers are a type of trigger that fires at a periodic time interval from a specified start time, while retaining state.</span><span class="sxs-lookup"><span data-stu-id="c0feb-106">Tumbling window triggers are a type of trigger that fires at a periodic time interval from a specified start time, while retaining state.</span></span> <span data-ttu-id="c0feb-107">Tumbling windows are a series of fixed-sized, non-overlapping, and contiguous time intervals.</span><span class="sxs-lookup"><span data-stu-id="c0feb-107">Tumbling windows are a series of fixed-sized, non-overlapping, and contiguous time intervals.</span></span> <span data-ttu-id="c0feb-108">A tumbling window trigger has a one-to-one relationship with a pipeline and can only reference a singular pipeline.</span><span class="sxs-lookup"><span data-stu-id="c0feb-108">A tumbling window trigger has a one-to-one relationship with a pipeline and can only reference a singular pipeline.</span></span>

## <a name="data-factory-ui"></a><span data-ttu-id="c0feb-109">Data Factory UI</span><span class="sxs-lookup"><span data-stu-id="c0feb-109">Data Factory UI</span></span>

<span data-ttu-id="c0feb-110">To create a tumbling window trigger in the Azure portal, select **Trigger > Tumbling window > Next**, and then configure the properties that define the tumbling window.</span><span class="sxs-lookup"><span data-stu-id="c0feb-110">To create a tumbling window trigger in the Azure portal, select **Trigger > Tumbling window > Next**, and then configure the properties that define the tumbling window.</span></span>

![Create a tumbling window trigger in the Azure portal](media/how-to-create-tumbling-window-trigger/create-tumbling-window-trigger.png)

## <a name="tumbling-window-trigger-type-properties"></a><span data-ttu-id="c0feb-112">Tumbling window trigger type properties</span><span class="sxs-lookup"><span data-stu-id="c0feb-112">Tumbling window trigger type properties</span></span>
<span data-ttu-id="c0feb-113">A tumbling window has the following trigger type properties:</span><span class="sxs-lookup"><span data-stu-id="c0feb-113">A tumbling window has the following trigger type properties:</span></span>

```  
{
    "name": "MyTriggerName",
    "properties": {
        "type": "TumblingWindowTrigger",
        "runtimeState": "<<Started/Stopped/Disabled - readonly>>",
        "typeProperties": {
            "frequency": "<<Minute/Hour>>",
            "interval": <<int>>,
            "startTime": "<<datetime>>",
            "endTime: "<<datetime – optional>>"",
            "delay": "<<timespan – optional>>",
            “maxConcurrency”: <<int>> (required, max allowed: 50),
            "retryPolicy": {
                "count":  <<int - optional, default: 0>>,
                “intervalInSeconds”: <<int>>,
            }
        },
        "pipeline":
            {
                "pipelineReference": {
                    "type": "PipelineReference",
                    "referenceName": "MyPipelineName"
                },
                "parameters": {
                    "parameter1": {
                        "type": "Expression",
                        "value": "@{concat('output',formatDateTime(trigger().outputs.windowStartTime,'-dd-MM-yyyy-HH-mm-ss-ffff'))}"
                    },
                    "parameter2": {
                        "type": "Expression",
                        "value": "@{concat('output',formatDateTime(trigger().outputs.windowEndTime,'-dd-MM-yyyy-HH-mm-ss-ffff'))}"
                    },
                    "parameter3": "https://mydemo.azurewebsites.net/api/demoapi"
                }
            }
      }    
}
```  

<span data-ttu-id="c0feb-114">The following table provides a high-level overview of the major JSON elements that are related to recurrence and scheduling of a tumbling window trigger:</span><span class="sxs-lookup"><span data-stu-id="c0feb-114">The following table provides a high-level overview of the major JSON elements that are related to recurrence and scheduling of a tumbling window trigger:</span></span>

| <span data-ttu-id="c0feb-115">JSON element</span><span class="sxs-lookup"><span data-stu-id="c0feb-115">JSON element</span></span> | <span data-ttu-id="c0feb-116">Description</span><span class="sxs-lookup"><span data-stu-id="c0feb-116">Description</span></span> | <span data-ttu-id="c0feb-117">Type</span><span class="sxs-lookup"><span data-stu-id="c0feb-117">Type</span></span> | <span data-ttu-id="c0feb-118">Allowed values</span><span class="sxs-lookup"><span data-stu-id="c0feb-118">Allowed values</span></span> | <span data-ttu-id="c0feb-119">Required</span><span class="sxs-lookup"><span data-stu-id="c0feb-119">Required</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="c0feb-120">**type**</span><span class="sxs-lookup"><span data-stu-id="c0feb-120">**type**</span></span> | <span data-ttu-id="c0feb-121">The type of the trigger.</span><span class="sxs-lookup"><span data-stu-id="c0feb-121">The type of the trigger.</span></span> <span data-ttu-id="c0feb-122">The type is the fixed value "TumblingWindowTrigger."</span><span class="sxs-lookup"><span data-stu-id="c0feb-122">The type is the fixed value "TumblingWindowTrigger."</span></span> | <span data-ttu-id="c0feb-123">String</span><span class="sxs-lookup"><span data-stu-id="c0feb-123">String</span></span> | <span data-ttu-id="c0feb-124">"TumblingWindowTrigger"</span><span class="sxs-lookup"><span data-stu-id="c0feb-124">"TumblingWindowTrigger"</span></span> | <span data-ttu-id="c0feb-125">Yes</span><span class="sxs-lookup"><span data-stu-id="c0feb-125">Yes</span></span> |
| <span data-ttu-id="c0feb-126">**runtimeState**</span><span class="sxs-lookup"><span data-stu-id="c0feb-126">**runtimeState**</span></span> | <span data-ttu-id="c0feb-127">The current state of the trigger run time.</span><span class="sxs-lookup"><span data-stu-id="c0feb-127">The current state of the trigger run time.</span></span><br/><span data-ttu-id="c0feb-128">**Note**: This element is \<readOnly>.</span><span class="sxs-lookup"><span data-stu-id="c0feb-128">**Note**: This element is \<readOnly>.</span></span> | <span data-ttu-id="c0feb-129">String</span><span class="sxs-lookup"><span data-stu-id="c0feb-129">String</span></span> | <span data-ttu-id="c0feb-130">"Started," "Stopped," "Disabled"</span><span class="sxs-lookup"><span data-stu-id="c0feb-130">"Started," "Stopped," "Disabled"</span></span> | <span data-ttu-id="c0feb-131">Yes</span><span class="sxs-lookup"><span data-stu-id="c0feb-131">Yes</span></span> |
| <span data-ttu-id="c0feb-132">**frequency**</span><span class="sxs-lookup"><span data-stu-id="c0feb-132">**frequency**</span></span> | <span data-ttu-id="c0feb-133">A string that represents the frequency unit (minutes or hours) at which the trigger recurs.</span><span class="sxs-lookup"><span data-stu-id="c0feb-133">A string that represents the frequency unit (minutes or hours) at which the trigger recurs.</span></span> <span data-ttu-id="c0feb-134">If the **startTime** date values are more granular than the **frequency** value, the **startTime** dates are considered when the window boundaries are computed.</span><span class="sxs-lookup"><span data-stu-id="c0feb-134">If the **startTime** date values are more granular than the **frequency** value, the **startTime** dates are considered when the window boundaries are computed.</span></span> <span data-ttu-id="c0feb-135">For example, if the **frequency** value is hourly and the **startTime** value is 2016-04-01T10:10:10Z, the first window is (2017-09-01T10:10:10Z, 2017-09-01T11:10:10Z).</span><span class="sxs-lookup"><span data-stu-id="c0feb-135">For example, if the **frequency** value is hourly and the **startTime** value is 2016-04-01T10:10:10Z, the first window is (2017-09-01T10:10:10Z, 2017-09-01T11:10:10Z).</span></span> | <span data-ttu-id="c0feb-136">String</span><span class="sxs-lookup"><span data-stu-id="c0feb-136">String</span></span> | <span data-ttu-id="c0feb-137">"minute," "hour"</span><span class="sxs-lookup"><span data-stu-id="c0feb-137">"minute," "hour"</span></span>  | <span data-ttu-id="c0feb-138">Yes</span><span class="sxs-lookup"><span data-stu-id="c0feb-138">Yes</span></span> |
| <span data-ttu-id="c0feb-139">**interval**</span><span class="sxs-lookup"><span data-stu-id="c0feb-139">**interval**</span></span> | <span data-ttu-id="c0feb-140">A positive integer that denotes the interval for the **frequency** value, which determines how often the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="c0feb-140">A positive integer that denotes the interval for the **frequency** value, which determines how often the trigger runs.</span></span> <span data-ttu-id="c0feb-141">For example, if the **interval** is 3 and the **frequency** is "hour," the trigger recurs every 3 hours.</span><span class="sxs-lookup"><span data-stu-id="c0feb-141">For example, if the **interval** is 3 and the **frequency** is "hour," the trigger recurs every 3 hours.</span></span> | <span data-ttu-id="c0feb-142">Integer</span><span class="sxs-lookup"><span data-stu-id="c0feb-142">Integer</span></span> | <span data-ttu-id="c0feb-143">A positive integer.</span><span class="sxs-lookup"><span data-stu-id="c0feb-143">A positive integer.</span></span> | <span data-ttu-id="c0feb-144">Yes</span><span class="sxs-lookup"><span data-stu-id="c0feb-144">Yes</span></span> |
| <span data-ttu-id="c0feb-145">**startTime**</span><span class="sxs-lookup"><span data-stu-id="c0feb-145">**startTime**</span></span>| <span data-ttu-id="c0feb-146">The first occurrence, which can be in the past.</span><span class="sxs-lookup"><span data-stu-id="c0feb-146">The first occurrence, which can be in the past.</span></span> <span data-ttu-id="c0feb-147">The first trigger interval is (**startTime**, **startTime** + **interval**).</span><span class="sxs-lookup"><span data-stu-id="c0feb-147">The first trigger interval is (**startTime**, **startTime** + **interval**).</span></span> | <span data-ttu-id="c0feb-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="c0feb-148">DateTime</span></span> | <span data-ttu-id="c0feb-149">A DateTime value.</span><span class="sxs-lookup"><span data-stu-id="c0feb-149">A DateTime value.</span></span> | <span data-ttu-id="c0feb-150">Yes</span><span class="sxs-lookup"><span data-stu-id="c0feb-150">Yes</span></span> |
| <span data-ttu-id="c0feb-151">**endTime**</span><span class="sxs-lookup"><span data-stu-id="c0feb-151">**endTime**</span></span>| <span data-ttu-id="c0feb-152">The last occurrence, which can be in the past.</span><span class="sxs-lookup"><span data-stu-id="c0feb-152">The last occurrence, which can be in the past.</span></span> | <span data-ttu-id="c0feb-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="c0feb-153">DateTime</span></span> | <span data-ttu-id="c0feb-154">A DateTime value.</span><span class="sxs-lookup"><span data-stu-id="c0feb-154">A DateTime value.</span></span> | <span data-ttu-id="c0feb-155">Yes</span><span class="sxs-lookup"><span data-stu-id="c0feb-155">Yes</span></span> |
| <span data-ttu-id="c0feb-156">**delay**</span><span class="sxs-lookup"><span data-stu-id="c0feb-156">**delay**</span></span> | <span data-ttu-id="c0feb-157">The amount of time to delay the start of data processing for the window.</span><span class="sxs-lookup"><span data-stu-id="c0feb-157">The amount of time to delay the start of data processing for the window.</span></span> <span data-ttu-id="c0feb-158">The pipeline run is started after the expected execution time plus the amount of **delay**.</span><span class="sxs-lookup"><span data-stu-id="c0feb-158">The pipeline run is started after the expected execution time plus the amount of **delay**.</span></span> <span data-ttu-id="c0feb-159">The **delay** defines how long the trigger waits past the due time before triggering a new run.</span><span class="sxs-lookup"><span data-stu-id="c0feb-159">The **delay** defines how long the trigger waits past the due time before triggering a new run.</span></span> <span data-ttu-id="c0feb-160">The **delay** doesn’t alter the window **startTime**.</span><span class="sxs-lookup"><span data-stu-id="c0feb-160">The **delay** doesn’t alter the window **startTime**.</span></span> <span data-ttu-id="c0feb-161">For example, a **delay** value of 00:10:00 implies a delay of 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="c0feb-161">For example, a **delay** value of 00:10:00 implies a delay of 10 minutes.</span></span> | <span data-ttu-id="c0feb-162">Timespan</span><span class="sxs-lookup"><span data-stu-id="c0feb-162">Timespan</span></span>  | <span data-ttu-id="c0feb-163">A time value where the default is 00:00:00.</span><span class="sxs-lookup"><span data-stu-id="c0feb-163">A time value where the default is 00:00:00.</span></span> | <span data-ttu-id="c0feb-164">No</span><span class="sxs-lookup"><span data-stu-id="c0feb-164">No</span></span> |
| <span data-ttu-id="c0feb-165">**maxConcurrency**</span><span class="sxs-lookup"><span data-stu-id="c0feb-165">**maxConcurrency**</span></span> | <span data-ttu-id="c0feb-166">The number of simultaneous trigger runs that are fired for windows that are ready.</span><span class="sxs-lookup"><span data-stu-id="c0feb-166">The number of simultaneous trigger runs that are fired for windows that are ready.</span></span> <span data-ttu-id="c0feb-167">For example, to back fill hourly runs for yesterday results in 24 windows.</span><span class="sxs-lookup"><span data-stu-id="c0feb-167">For example, to back fill hourly runs for yesterday results in 24 windows.</span></span> <span data-ttu-id="c0feb-168">If **maxConcurrency** = 10, trigger events are fired only for the first 10 windows (00:00-01:00 - 09:00-10:00).</span><span class="sxs-lookup"><span data-stu-id="c0feb-168">If **maxConcurrency** = 10, trigger events are fired only for the first 10 windows (00:00-01:00 - 09:00-10:00).</span></span> <span data-ttu-id="c0feb-169">After the first 10 triggered pipeline runs are complete, trigger runs are fired for the next 10 windows (10:00-11:00 - 19:00-20:00).</span><span class="sxs-lookup"><span data-stu-id="c0feb-169">After the first 10 triggered pipeline runs are complete, trigger runs are fired for the next 10 windows (10:00-11:00 - 19:00-20:00).</span></span> <span data-ttu-id="c0feb-170">Continuing with this example of **maxConcurrency** = 10, if there are 10 windows ready, there are 10 total pipeline runs.</span><span class="sxs-lookup"><span data-stu-id="c0feb-170">Continuing with this example of **maxConcurrency** = 10, if there are 10 windows ready, there are 10 total pipeline runs.</span></span> <span data-ttu-id="c0feb-171">If there's only 1 window ready, there's only 1 pipeline run.</span><span class="sxs-lookup"><span data-stu-id="c0feb-171">If there's only 1 window ready, there's only 1 pipeline run.</span></span> | <span data-ttu-id="c0feb-172">Integer</span><span class="sxs-lookup"><span data-stu-id="c0feb-172">Integer</span></span> | <span data-ttu-id="c0feb-173">An integer between 1 and 50.</span><span class="sxs-lookup"><span data-stu-id="c0feb-173">An integer between 1 and 50.</span></span> | <span data-ttu-id="c0feb-174">Yes</span><span class="sxs-lookup"><span data-stu-id="c0feb-174">Yes</span></span> |
| <span data-ttu-id="c0feb-175">**retryPolicy: Count**</span><span class="sxs-lookup"><span data-stu-id="c0feb-175">**retryPolicy: Count**</span></span> | <span data-ttu-id="c0feb-176">The number of retries before the pipeline run is marked as "Failed."</span><span class="sxs-lookup"><span data-stu-id="c0feb-176">The number of retries before the pipeline run is marked as "Failed."</span></span>  | <span data-ttu-id="c0feb-177">Integer</span><span class="sxs-lookup"><span data-stu-id="c0feb-177">Integer</span></span> | <span data-ttu-id="c0feb-178">An integer, where the default is 0 (no retries).</span><span class="sxs-lookup"><span data-stu-id="c0feb-178">An integer, where the default is 0 (no retries).</span></span> | <span data-ttu-id="c0feb-179">No</span><span class="sxs-lookup"><span data-stu-id="c0feb-179">No</span></span> |
| <span data-ttu-id="c0feb-180">**retryPolicy: intervalInSeconds**</span><span class="sxs-lookup"><span data-stu-id="c0feb-180">**retryPolicy: intervalInSeconds**</span></span> | <span data-ttu-id="c0feb-181">The delay between retry attempts specified in seconds.</span><span class="sxs-lookup"><span data-stu-id="c0feb-181">The delay between retry attempts specified in seconds.</span></span> | <span data-ttu-id="c0feb-182">Integer</span><span class="sxs-lookup"><span data-stu-id="c0feb-182">Integer</span></span> | <span data-ttu-id="c0feb-183">The number of seconds, where the default is 30.</span><span class="sxs-lookup"><span data-stu-id="c0feb-183">The number of seconds, where the default is 30.</span></span> | <span data-ttu-id="c0feb-184">No</span><span class="sxs-lookup"><span data-stu-id="c0feb-184">No</span></span> |

### <a name="windowstart-and-windowend-system-variables"></a><span data-ttu-id="c0feb-185">WindowStart and WindowEnd system variables</span><span class="sxs-lookup"><span data-stu-id="c0feb-185">WindowStart and WindowEnd system variables</span></span>

<span data-ttu-id="c0feb-186">You can use the **WindowStart** and **WindowEnd** system variables of the tumbling window trigger in your **pipeline** definition (that is, for part of a query).</span><span class="sxs-lookup"><span data-stu-id="c0feb-186">You can use the **WindowStart** and **WindowEnd** system variables of the tumbling window trigger in your **pipeline** definition (that is, for part of a query).</span></span> <span data-ttu-id="c0feb-187">Pass the system variables as parameters to your pipeline in the **trigger** definition.</span><span class="sxs-lookup"><span data-stu-id="c0feb-187">Pass the system variables as parameters to your pipeline in the **trigger** definition.</span></span> <span data-ttu-id="c0feb-188">The following example shows you how to pass these variables as parameters:</span><span class="sxs-lookup"><span data-stu-id="c0feb-188">The following example shows you how to pass these variables as parameters:</span></span>

```  
{
    "name": "MyTriggerName",
    "properties": {
        "type": "TumblingWindowTrigger",
            ...
        "pipeline":
            {
                "pipelineReference": {
                    "type": "PipelineReference",
                    "referenceName": "MyPipelineName"
                },
                "parameters": {
                    "MyWindowStart": {
                        "type": "Expression",
                        "value": "@{concat('output',formatDateTime(trigger().outputs.windowStartTime,'-dd-MM-yyyy-HH-mm-ss-ffff'))}"
                    },
                    "MyWindowEnd": {
                        "type": "Expression",
                        "value": "@{concat('output',formatDateTime(trigger().outputs.windowEndTime,'-dd-MM-yyyy-HH-mm-ss-ffff'))}"
                    }
                }
            }
      }    
}
```  

<span data-ttu-id="c0feb-189">To use the **WindowStart** and **WindowEnd** system variable values in the pipeline definition, use your "MyWindowStart" and "MyWindowEnd" parameters, accordingly.</span><span class="sxs-lookup"><span data-stu-id="c0feb-189">To use the **WindowStart** and **WindowEnd** system variable values in the pipeline definition, use your "MyWindowStart" and "MyWindowEnd" parameters, accordingly.</span></span>

### <a name="execution-order-of-windows-in-a-backfill-scenario"></a><span data-ttu-id="c0feb-190">Execution order of windows in a backfill scenario</span><span class="sxs-lookup"><span data-stu-id="c0feb-190">Execution order of windows in a backfill scenario</span></span>
<span data-ttu-id="c0feb-191">When there are multiple windows up for execution (especially in a backfill scenario), the order of execution for windows is deterministic, from oldest to newest intervals.</span><span class="sxs-lookup"><span data-stu-id="c0feb-191">When there are multiple windows up for execution (especially in a backfill scenario), the order of execution for windows is deterministic, from oldest to newest intervals.</span></span> <span data-ttu-id="c0feb-192">Currently, this behavior can't be modified.</span><span class="sxs-lookup"><span data-stu-id="c0feb-192">Currently, this behavior can't be modified.</span></span>

### <a name="existing-triggerresource-elements"></a><span data-ttu-id="c0feb-193">Existing TriggerResource elements</span><span class="sxs-lookup"><span data-stu-id="c0feb-193">Existing TriggerResource elements</span></span>
<span data-ttu-id="c0feb-194">The following points apply to existing **TriggerResource** elements:</span><span class="sxs-lookup"><span data-stu-id="c0feb-194">The following points apply to existing **TriggerResource** elements:</span></span>

* <span data-ttu-id="c0feb-195">If the value for the **frequency** element (or window size) of the trigger changes, the state of the windows that are already processed is *not* reset.</span><span class="sxs-lookup"><span data-stu-id="c0feb-195">If the value for the **frequency** element (or window size) of the trigger changes, the state of the windows that are already processed is *not* reset.</span></span> <span data-ttu-id="c0feb-196">The trigger continues to fire for the windows from the last window that it executed by using the new window size.</span><span class="sxs-lookup"><span data-stu-id="c0feb-196">The trigger continues to fire for the windows from the last window that it executed by using the new window size.</span></span>
* <span data-ttu-id="c0feb-197">If the value for the **endTime** element of the trigger changes (added or updated), the state of the windows that are already processed is *not* reset.</span><span class="sxs-lookup"><span data-stu-id="c0feb-197">If the value for the **endTime** element of the trigger changes (added or updated), the state of the windows that are already processed is *not* reset.</span></span> <span data-ttu-id="c0feb-198">The trigger honors the new **endTime** value.</span><span class="sxs-lookup"><span data-stu-id="c0feb-198">The trigger honors the new **endTime** value.</span></span> <span data-ttu-id="c0feb-199">If the new **endTime** value is before the windows that are already executed, the trigger stops.</span><span class="sxs-lookup"><span data-stu-id="c0feb-199">If the new **endTime** value is before the windows that are already executed, the trigger stops.</span></span> <span data-ttu-id="c0feb-200">Otherwise, the trigger stops when the new **endTime** value is encountered.</span><span class="sxs-lookup"><span data-stu-id="c0feb-200">Otherwise, the trigger stops when the new **endTime** value is encountered.</span></span>

## <a name="sample-for-azure-powershell"></a><span data-ttu-id="c0feb-201">Sample for Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0feb-201">Sample for Azure PowerShell</span></span>
<span data-ttu-id="c0feb-202">This section shows you how to use Azure PowerShell to create, start, and monitor a trigger.</span><span class="sxs-lookup"><span data-stu-id="c0feb-202">This section shows you how to use Azure PowerShell to create, start, and monitor a trigger.</span></span>

1. <span data-ttu-id="c0feb-203">Create a JSON file named **MyTrigger.json** in the C:\ADFv2QuickStartPSH\ folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="c0feb-203">Create a JSON file named **MyTrigger.json** in the C:\ADFv2QuickStartPSH\ folder with the following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c0feb-204">Before you save the JSON file, set the value of the **startTime** element to the current UTC time.</span><span class="sxs-lookup"><span data-stu-id="c0feb-204">Before you save the JSON file, set the value of the **startTime** element to the current UTC time.</span></span> <span data-ttu-id="c0feb-205">Set the value of the **endTime** element to one hour past the current UTC time.</span><span class="sxs-lookup"><span data-stu-id="c0feb-205">Set the value of the **endTime** element to one hour past the current UTC time.</span></span>

    ```json   
    {
      "name": "PerfTWTrigger",
      "properties": {
        "type": "TumblingWindowTrigger",
        "typeProperties": {
          "frequency": "Minute",
          "interval": "15",
          "startTime": "2017-09-08T05:30:00Z",
          "delay": "00:00:01",
          "retryPolicy": {
            "count": 2,
            "intervalInSeconds": 30
          },
          "maxConcurrency": 50
        },
        "pipeline": {
          "pipelineReference": {
            "type": "PipelineReference",
            "referenceName": "DynamicsToBlobPerfPipeline"
          },
          "parameters": {
            "windowStart": "@trigger().outputs.windowStartTime",
            "windowEnd": "@trigger().outputs.windowEndTime"
          }
        },
        "runtimeState": "Started"
      }
    }
    ```  

2. <span data-ttu-id="c0feb-206">Create a trigger by using the **Set-AzureRmDataFactoryV2Trigger** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c0feb-206">Create a trigger by using the **Set-AzureRmDataFactoryV2Trigger** cmdlet:</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger" -DefinitionFile "C:\ADFv2QuickStartPSH\MyTrigger.json"
    ```
    
3. <span data-ttu-id="c0feb-207">Confirm that the status of the trigger is **Stopped** by using the **Get-AzureRmDataFactoryV2Trigger** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c0feb-207">Confirm that the status of the trigger is **Stopped** by using the **Get-AzureRmDataFactoryV2Trigger** cmdlet:</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger"
    ```

4. <span data-ttu-id="c0feb-208">Start the trigger by using the **Start-AzureRmDataFactoryV2Trigger** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c0feb-208">Start the trigger by using the **Start-AzureRmDataFactoryV2Trigger** cmdlet:</span></span>

    ```powershell
    Start-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger"
    ```

5. <span data-ttu-id="c0feb-209">Confirm that the status of the trigger is **Started** by using the **Get-AzureRmDataFactoryV2Trigger** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c0feb-209">Confirm that the status of the trigger is **Started** by using the **Get-AzureRmDataFactoryV2Trigger** cmdlet:</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2Trigger -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -Name "MyTrigger"
    ```

6. <span data-ttu-id="c0feb-210">Get the trigger runs in Azure PowerShell by using the **Get-AzureRmDataFactoryV2TriggerRun** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c0feb-210">Get the trigger runs in Azure PowerShell by using the **Get-AzureRmDataFactoryV2TriggerRun** cmdlet.</span></span> <span data-ttu-id="c0feb-211">To get information about the trigger runs, execute the following command periodically.</span><span class="sxs-lookup"><span data-stu-id="c0feb-211">To get information about the trigger runs, execute the following command periodically.</span></span> <span data-ttu-id="c0feb-212">Update the **TriggerRunStartedAfter** and **TriggerRunStartedBefore** values to match the values in your trigger definition:</span><span class="sxs-lookup"><span data-stu-id="c0feb-212">Update the **TriggerRunStartedAfter** and **TriggerRunStartedBefore** values to match the values in your trigger definition:</span></span>

    ```powershell
    Get-AzureRmDataFactoryV2TriggerRun -ResourceGroupName $ResourceGroupName -DataFactoryName $DataFactoryName -TriggerName "MyTrigger" -TriggerRunStartedAfter "2017-12-08T00:00:00" -TriggerRunStartedBefore "2017-12-08T01:00:00"
    ```
    
<span data-ttu-id="c0feb-213">To monitor trigger runs and pipeline runs in the Azure portal, see [Monitor pipeline runs](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c0feb-213">To monitor trigger runs and pipeline runs in the Azure portal, see [Monitor pipeline runs](quickstart-create-data-factory-resource-manager-template.md#monitor-the-pipeline).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0feb-214">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0feb-214">Next steps</span></span>
<span data-ttu-id="c0feb-215">For detailed information about triggers, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md#triggers).</span><span class="sxs-lookup"><span data-stu-id="c0feb-215">For detailed information about triggers, see [Pipeline execution and triggers](concepts-pipeline-execution-triggers.md#triggers).</span></span>
