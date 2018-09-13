---
title: Azure Data Factory - JSON Scripting Reference | Microsoft Docs
description: Provides JSON schemas for Data Factory entities.
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
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: c5909c1f511d3a7816ebafc3ea8b326edb7f14e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856870"
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="364d0-103">Azure Data Factory - JSON Scripting Reference</span><span class="sxs-lookup"><span data-stu-id="364d0-103">Azure Data Factory - JSON Scripting Reference</span></span>
> [!NOTE]
> <span data-ttu-id="364d0-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-104">This article applies to version 1 of Data Factory.</span></span>


<span data-ttu-id="364d0-105">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span><span class="sxs-lookup"><span data-stu-id="364d0-105">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="364d0-106">Pipeline</span><span class="sxs-lookup"><span data-stu-id="364d0-106">Pipeline</span></span> 
<span data-ttu-id="364d0-107">The high-level structure for a pipeline definition is as follows:</span><span class="sxs-lookup"><span data-stu-id="364d0-107">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="364d0-108">Following table describes the properties within the pipeline JSON definition:</span><span class="sxs-lookup"><span data-stu-id="364d0-108">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="364d0-109">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-109">Property</span></span> | <span data-ttu-id="364d0-110">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-110">Description</span></span> | <span data-ttu-id="364d0-111">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-111">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="364d0-112">name</span><span class="sxs-lookup"><span data-stu-id="364d0-112">name</span></span> | <span data-ttu-id="364d0-113">Name of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-113">Name of the pipeline.</span></span> <span data-ttu-id="364d0-114">Specify a name that represents the action that the activity or pipeline is configured to do</span><span class="sxs-lookup"><span data-stu-id="364d0-114">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="364d0-115">Maximum number of characters: 260</span><span class="sxs-lookup"><span data-stu-id="364d0-115">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="364d0-116">Must start with a letter number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="364d0-116">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="364d0-117">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="364d0-117">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="364d0-118">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-118">Yes</span></span> |
| <span data-ttu-id="364d0-119">description</span><span class="sxs-lookup"><span data-stu-id="364d0-119">description</span></span> |<span data-ttu-id="364d0-120">Text describing what the activity or pipeline is used for</span><span class="sxs-lookup"><span data-stu-id="364d0-120">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="364d0-121">No</span><span class="sxs-lookup"><span data-stu-id="364d0-121">No</span></span> |
| <span data-ttu-id="364d0-122">activities</span><span class="sxs-lookup"><span data-stu-id="364d0-122">activities</span></span> | <span data-ttu-id="364d0-123">Contains a list of activities.</span><span class="sxs-lookup"><span data-stu-id="364d0-123">Contains a list of activities.</span></span> | <span data-ttu-id="364d0-124">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-124">Yes</span></span> |
| <span data-ttu-id="364d0-125">start</span><span class="sxs-lookup"><span data-stu-id="364d0-125">start</span></span> |<span data-ttu-id="364d0-126">Start date-time for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-126">Start date-time for the pipeline.</span></span> <span data-ttu-id="364d0-127">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="364d0-127">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="364d0-128">For example: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="364d0-128">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="364d0-129">It is possible to specify a local time, for example an EST time.</span><span class="sxs-lookup"><span data-stu-id="364d0-129">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="364d0-130">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="364d0-130">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="364d0-131">The start and end properties together specify active period for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-131">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="364d0-132">Output slices are only produced with in this active period.</span><span class="sxs-lookup"><span data-stu-id="364d0-132">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="364d0-133">No</span><span class="sxs-lookup"><span data-stu-id="364d0-133">No</span></span><br/><br/><span data-ttu-id="364d0-134">If you specify a value for the end property, you must specify value for the start property.</span><span class="sxs-lookup"><span data-stu-id="364d0-134">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="364d0-135">The start and end times can both be empty to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-135">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="364d0-136">You must specify both values to set an active period for the pipeline to run.</span><span class="sxs-lookup"><span data-stu-id="364d0-136">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="364d0-137">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span><span class="sxs-lookup"><span data-stu-id="364d0-137">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="364d0-138">end</span><span class="sxs-lookup"><span data-stu-id="364d0-138">end</span></span> |<span data-ttu-id="364d0-139">End date-time for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-139">End date-time for the pipeline.</span></span> <span data-ttu-id="364d0-140">If specified must be in ISO format.</span><span class="sxs-lookup"><span data-stu-id="364d0-140">If specified must be in ISO format.</span></span> <span data-ttu-id="364d0-141">For example: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="364d0-141">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="364d0-142">It is possible to specify a local time, for example an EST time.</span><span class="sxs-lookup"><span data-stu-id="364d0-142">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="364d0-143">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="364d0-143">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="364d0-144">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span><span class="sxs-lookup"><span data-stu-id="364d0-144">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="364d0-145">No</span><span class="sxs-lookup"><span data-stu-id="364d0-145">No</span></span> <br/><br/><span data-ttu-id="364d0-146">If you specify a value for the start property, you must specify value for the end property.</span><span class="sxs-lookup"><span data-stu-id="364d0-146">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="364d0-147">See notes for the **start** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-147">See notes for the **start** property.</span></span> |
| <span data-ttu-id="364d0-148">isPaused</span><span class="sxs-lookup"><span data-stu-id="364d0-148">isPaused</span></span> |<span data-ttu-id="364d0-149">If set to true the pipeline does not run.</span><span class="sxs-lookup"><span data-stu-id="364d0-149">If set to true the pipeline does not run.</span></span> <span data-ttu-id="364d0-150">Default value = false.</span><span class="sxs-lookup"><span data-stu-id="364d0-150">Default value = false.</span></span> <span data-ttu-id="364d0-151">You can use this property to enable or disable.</span><span class="sxs-lookup"><span data-stu-id="364d0-151">You can use this property to enable or disable.</span></span> |<span data-ttu-id="364d0-152">No</span><span class="sxs-lookup"><span data-stu-id="364d0-152">No</span></span> |
| <span data-ttu-id="364d0-153">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="364d0-153">pipelineMode</span></span> |<span data-ttu-id="364d0-154">The method for scheduling runs for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-154">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="364d0-155">Allowed values are: scheduled (default), onetime.</span><span class="sxs-lookup"><span data-stu-id="364d0-155">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="364d0-156">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span><span class="sxs-lookup"><span data-stu-id="364d0-156">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="364d0-157">‘Onetime’ indicates that the pipeline runs only once.</span><span class="sxs-lookup"><span data-stu-id="364d0-157">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="364d0-158">Onetime pipelines once created cannot be modified/updated currently.</span><span class="sxs-lookup"><span data-stu-id="364d0-158">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="364d0-159">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span><span class="sxs-lookup"><span data-stu-id="364d0-159">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="364d0-160">No</span><span class="sxs-lookup"><span data-stu-id="364d0-160">No</span></span> |
| <span data-ttu-id="364d0-161">expirationTime</span><span class="sxs-lookup"><span data-stu-id="364d0-161">expirationTime</span></span> |<span data-ttu-id="364d0-162">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span><span class="sxs-lookup"><span data-stu-id="364d0-162">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="364d0-163">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span><span class="sxs-lookup"><span data-stu-id="364d0-163">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="364d0-164">No</span><span class="sxs-lookup"><span data-stu-id="364d0-164">No</span></span> |


## <a name="activity"></a><span data-ttu-id="364d0-165">Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-165">Activity</span></span> 
<span data-ttu-id="364d0-166">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span><span class="sxs-lookup"><span data-stu-id="364d0-166">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="364d0-167">Following table describe the properties within the activity JSON definition:</span><span class="sxs-lookup"><span data-stu-id="364d0-167">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="364d0-168">Tag</span><span class="sxs-lookup"><span data-stu-id="364d0-168">Tag</span></span> | <span data-ttu-id="364d0-169">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-169">Description</span></span> | <span data-ttu-id="364d0-170">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-171">name</span><span class="sxs-lookup"><span data-stu-id="364d0-171">name</span></span> |<span data-ttu-id="364d0-172">Name of the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-172">Name of the activity.</span></span> <span data-ttu-id="364d0-173">Specify a name that represents the action that the activity is configured to do</span><span class="sxs-lookup"><span data-stu-id="364d0-173">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="364d0-174">Maximum number of characters: 260</span><span class="sxs-lookup"><span data-stu-id="364d0-174">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="364d0-175">Must start with a letter number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="364d0-175">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="364d0-176">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="364d0-176">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="364d0-177">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-177">Yes</span></span> |
| <span data-ttu-id="364d0-178">description</span><span class="sxs-lookup"><span data-stu-id="364d0-178">description</span></span> |<span data-ttu-id="364d0-179">Text describing what the activity is used for.</span><span class="sxs-lookup"><span data-stu-id="364d0-179">Text describing what the activity is used for.</span></span> |<span data-ttu-id="364d0-180">No</span><span class="sxs-lookup"><span data-stu-id="364d0-180">No</span></span> |
| <span data-ttu-id="364d0-181">type</span><span class="sxs-lookup"><span data-stu-id="364d0-181">type</span></span> |<span data-ttu-id="364d0-182">Specifies the type of the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-182">Specifies the type of the activity.</span></span> <span data-ttu-id="364d0-183">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span><span class="sxs-lookup"><span data-stu-id="364d0-183">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="364d0-184">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-184">Yes</span></span> |
| <span data-ttu-id="364d0-185">inputs</span><span class="sxs-lookup"><span data-stu-id="364d0-185">inputs</span></span> |<span data-ttu-id="364d0-186">Input tables used by the activity</span><span class="sxs-lookup"><span data-stu-id="364d0-186">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="364d0-187">No for HDInsightStreaming and SqlServerStoredProcedure activities</span><span class="sxs-lookup"><span data-stu-id="364d0-187">No for HDInsightStreaming and SqlServerStoredProcedure activities</span></span> <br/> <br/> <span data-ttu-id="364d0-188">Yes for all others</span><span class="sxs-lookup"><span data-stu-id="364d0-188">Yes for all others</span></span> |
| <span data-ttu-id="364d0-189">outputs</span><span class="sxs-lookup"><span data-stu-id="364d0-189">outputs</span></span> |<span data-ttu-id="364d0-190">Output tables used by the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-190">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="364d0-191">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-191">Yes</span></span> |
| <span data-ttu-id="364d0-192">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="364d0-192">linkedServiceName</span></span> |<span data-ttu-id="364d0-193">Name of the linked service used by the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-193">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="364d0-194">An activity may require that you specify the linked service that links to the required compute environment.</span><span class="sxs-lookup"><span data-stu-id="364d0-194">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="364d0-195">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-195">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="364d0-196">No for all others</span><span class="sxs-lookup"><span data-stu-id="364d0-196">No for all others</span></span> |
| <span data-ttu-id="364d0-197">typeProperties</span><span class="sxs-lookup"><span data-stu-id="364d0-197">typeProperties</span></span> |<span data-ttu-id="364d0-198">Properties in the typeProperties section depend on type of the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-198">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="364d0-199">No</span><span class="sxs-lookup"><span data-stu-id="364d0-199">No</span></span> |
| <span data-ttu-id="364d0-200">policy</span><span class="sxs-lookup"><span data-stu-id="364d0-200">policy</span></span> |<span data-ttu-id="364d0-201">Policies that affect the run-time behavior of the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-201">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="364d0-202">If it is not specified, default policies are used.</span><span class="sxs-lookup"><span data-stu-id="364d0-202">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="364d0-203">No</span><span class="sxs-lookup"><span data-stu-id="364d0-203">No</span></span> |
| <span data-ttu-id="364d0-204">scheduler</span><span class="sxs-lookup"><span data-stu-id="364d0-204">scheduler</span></span> |<span data-ttu-id="364d0-205">“scheduler” property is used to define desired scheduling for the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-205">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="364d0-206">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="364d0-206">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="364d0-207">No</span><span class="sxs-lookup"><span data-stu-id="364d0-207">No</span></span> |

### <a name="policies"></a><span data-ttu-id="364d0-208">Policies</span><span class="sxs-lookup"><span data-stu-id="364d0-208">Policies</span></span>
<span data-ttu-id="364d0-209">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span><span class="sxs-lookup"><span data-stu-id="364d0-209">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="364d0-210">The following table provides the details.</span><span class="sxs-lookup"><span data-stu-id="364d0-210">The following table provides the details.</span></span>

| <span data-ttu-id="364d0-211">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-211">Property</span></span> | <span data-ttu-id="364d0-212">Permitted values</span><span class="sxs-lookup"><span data-stu-id="364d0-212">Permitted values</span></span> | <span data-ttu-id="364d0-213">Default Value</span><span class="sxs-lookup"><span data-stu-id="364d0-213">Default Value</span></span> | <span data-ttu-id="364d0-214">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-214">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-215">concurrency</span><span class="sxs-lookup"><span data-stu-id="364d0-215">concurrency</span></span> |<span data-ttu-id="364d0-216">Integer</span><span class="sxs-lookup"><span data-stu-id="364d0-216">Integer</span></span> <br/><br/><span data-ttu-id="364d0-217">Max value: 10</span><span class="sxs-lookup"><span data-stu-id="364d0-217">Max value: 10</span></span> |<span data-ttu-id="364d0-218">1</span><span class="sxs-lookup"><span data-stu-id="364d0-218">1</span></span> |<span data-ttu-id="364d0-219">Number of concurrent executions of the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-219">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="364d0-220">It determines the number of parallel activity executions that can happen on different slices.</span><span class="sxs-lookup"><span data-stu-id="364d0-220">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="364d0-221">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span><span class="sxs-lookup"><span data-stu-id="364d0-221">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="364d0-222">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="364d0-222">executionPriorityOrder</span></span> |<span data-ttu-id="364d0-223">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="364d0-223">NewestFirst</span></span><br/><br/><span data-ttu-id="364d0-224">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="364d0-224">OldestFirst</span></span> |<span data-ttu-id="364d0-225">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="364d0-225">OldestFirst</span></span> |<span data-ttu-id="364d0-226">Determines the ordering of data slices that are being processed.</span><span class="sxs-lookup"><span data-stu-id="364d0-226">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="364d0-227">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span><span class="sxs-lookup"><span data-stu-id="364d0-227">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="364d0-228">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span><span class="sxs-lookup"><span data-stu-id="364d0-228">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="364d0-229">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span><span class="sxs-lookup"><span data-stu-id="364d0-229">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="364d0-230">retry</span><span class="sxs-lookup"><span data-stu-id="364d0-230">retry</span></span> |<span data-ttu-id="364d0-231">Integer</span><span class="sxs-lookup"><span data-stu-id="364d0-231">Integer</span></span><br/><br/><span data-ttu-id="364d0-232">Max value can be 10</span><span class="sxs-lookup"><span data-stu-id="364d0-232">Max value can be 10</span></span> |<span data-ttu-id="364d0-233">0</span><span class="sxs-lookup"><span data-stu-id="364d0-233">0</span></span> |<span data-ttu-id="364d0-234">Number of retries before the data processing for the slice is marked as Failure.</span><span class="sxs-lookup"><span data-stu-id="364d0-234">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="364d0-235">Activity execution for a data slice is retried up to the specified retry count.</span><span class="sxs-lookup"><span data-stu-id="364d0-235">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="364d0-236">The retry is done as soon as possible after the failure.</span><span class="sxs-lookup"><span data-stu-id="364d0-236">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="364d0-237">timeout</span><span class="sxs-lookup"><span data-stu-id="364d0-237">timeout</span></span> |<span data-ttu-id="364d0-238">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="364d0-238">TimeSpan</span></span> |<span data-ttu-id="364d0-239">00:00:00</span><span class="sxs-lookup"><span data-stu-id="364d0-239">00:00:00</span></span> |<span data-ttu-id="364d0-240">Timeout for the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-240">Timeout for the activity.</span></span> <span data-ttu-id="364d0-241">Example: 00:10:00 (implies timeout 10 mins)</span><span class="sxs-lookup"><span data-stu-id="364d0-241">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="364d0-242">If a value is not specified or is 0, the timeout is infinite.</span><span class="sxs-lookup"><span data-stu-id="364d0-242">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="364d0-243">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span><span class="sxs-lookup"><span data-stu-id="364d0-243">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="364d0-244">The number of retries depends on the retry property.</span><span class="sxs-lookup"><span data-stu-id="364d0-244">The number of retries depends on the retry property.</span></span> <span data-ttu-id="364d0-245">When timeout occurs, the status is set to TimedOut.</span><span class="sxs-lookup"><span data-stu-id="364d0-245">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="364d0-246">delay</span><span class="sxs-lookup"><span data-stu-id="364d0-246">delay</span></span> |<span data-ttu-id="364d0-247">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="364d0-247">TimeSpan</span></span> |<span data-ttu-id="364d0-248">00:00:00</span><span class="sxs-lookup"><span data-stu-id="364d0-248">00:00:00</span></span> |<span data-ttu-id="364d0-249">Specify the delay before data processing of the slice starts.</span><span class="sxs-lookup"><span data-stu-id="364d0-249">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="364d0-250">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span><span class="sxs-lookup"><span data-stu-id="364d0-250">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="364d0-251">Example: 00:10:00 (implies delay of 10 mins)</span><span class="sxs-lookup"><span data-stu-id="364d0-251">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="364d0-252">longRetry</span><span class="sxs-lookup"><span data-stu-id="364d0-252">longRetry</span></span> |<span data-ttu-id="364d0-253">Integer</span><span class="sxs-lookup"><span data-stu-id="364d0-253">Integer</span></span><br/><br/><span data-ttu-id="364d0-254">Max value: 10</span><span class="sxs-lookup"><span data-stu-id="364d0-254">Max value: 10</span></span> |<span data-ttu-id="364d0-255">1</span><span class="sxs-lookup"><span data-stu-id="364d0-255">1</span></span> |<span data-ttu-id="364d0-256">The number of long retry attempts before the slice execution is failed.</span><span class="sxs-lookup"><span data-stu-id="364d0-256">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="364d0-257">longRetry attempts are spaced by longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="364d0-257">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="364d0-258">So if you need to specify a time between retry attempts, use longRetry.</span><span class="sxs-lookup"><span data-stu-id="364d0-258">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="364d0-259">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry \* longRetry.</span><span class="sxs-lookup"><span data-stu-id="364d0-259">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry \* longRetry.</span></span><br/><br/><span data-ttu-id="364d0-260">For example, if we have the following settings in the activity policy:</span><span class="sxs-lookup"><span data-stu-id="364d0-260">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="364d0-261">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="364d0-261">Retry: 3</span></span><br/><span data-ttu-id="364d0-262">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="364d0-262">longRetry: 2</span></span><br/><span data-ttu-id="364d0-263">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="364d0-263">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="364d0-264">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span><span class="sxs-lookup"><span data-stu-id="364d0-264">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="364d0-265">Initially there would be 3 consecutive execution attempts.</span><span class="sxs-lookup"><span data-stu-id="364d0-265">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="364d0-266">After each attempt, the slice status would be Retry.</span><span class="sxs-lookup"><span data-stu-id="364d0-266">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="364d0-267">After first 3 attempts are over, the slice status would be LongRetry.</span><span class="sxs-lookup"><span data-stu-id="364d0-267">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="364d0-268">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span><span class="sxs-lookup"><span data-stu-id="364d0-268">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="364d0-269">After that, the slice status would be Failed and no more retries would be attempted.</span><span class="sxs-lookup"><span data-stu-id="364d0-269">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="364d0-270">Hence overall 6 attempts were made.</span><span class="sxs-lookup"><span data-stu-id="364d0-270">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="364d0-271">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span><span class="sxs-lookup"><span data-stu-id="364d0-271">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="364d0-272">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span><span class="sxs-lookup"><span data-stu-id="364d0-272">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="364d0-273">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span><span class="sxs-lookup"><span data-stu-id="364d0-273">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="364d0-274">Word of caution: do not set high values for longRetry or longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="364d0-274">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="364d0-275">Typically, higher values imply other systemic issues.</span><span class="sxs-lookup"><span data-stu-id="364d0-275">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="364d0-276">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="364d0-276">longRetryInterval</span></span> |<span data-ttu-id="364d0-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="364d0-277">TimeSpan</span></span> |<span data-ttu-id="364d0-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="364d0-278">00:00:00</span></span> |<span data-ttu-id="364d0-279">The delay between long retry attempts</span><span class="sxs-lookup"><span data-stu-id="364d0-279">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="364d0-280">typeProperties section</span><span class="sxs-lookup"><span data-stu-id="364d0-280">typeProperties section</span></span>
<span data-ttu-id="364d0-281">The typeProperties section is different for each activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-281">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="364d0-282">Transformation activities have just the type properties.</span><span class="sxs-lookup"><span data-stu-id="364d0-282">Transformation activities have just the type properties.</span></span> <span data-ttu-id="364d0-283">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-283">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="364d0-284">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span><span class="sxs-lookup"><span data-stu-id="364d0-284">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="364d0-285">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span><span class="sxs-lookup"><span data-stu-id="364d0-285">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="364d0-286">Sample copy pipeline</span><span class="sxs-lookup"><span data-stu-id="364d0-286">Sample copy pipeline</span></span>
<span data-ttu-id="364d0-287">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span><span class="sxs-lookup"><span data-stu-id="364d0-287">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="364d0-288">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="364d0-288">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="364d0-289">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="364d0-289">Note the following points:</span></span>

* <span data-ttu-id="364d0-290">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="364d0-290">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="364d0-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="364d0-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="364d0-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="364d0-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="364d0-293">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span><span class="sxs-lookup"><span data-stu-id="364d0-293">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="364d0-294">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="364d0-294">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="364d0-295">Sample transformation pipeline</span><span class="sxs-lookup"><span data-stu-id="364d0-295">Sample transformation pipeline</span></span>
<span data-ttu-id="364d0-296">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span><span class="sxs-lookup"><span data-stu-id="364d0-296">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="364d0-297">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-297">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="364d0-298">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="364d0-298">Note the following points:</span></span> 

* <span data-ttu-id="364d0-299">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="364d0-299">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="364d0-300">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="364d0-300">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="364d0-301">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="364d0-301">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="364d0-302">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-302">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="364d0-303">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="364d0-303">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="364d0-304">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-304">Linked service</span></span>
<span data-ttu-id="364d0-305">The high-level structure for a linked service definition is as follows:</span><span class="sxs-lookup"><span data-stu-id="364d0-305">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="364d0-306">Following table describe the properties within the activity JSON definition:</span><span class="sxs-lookup"><span data-stu-id="364d0-306">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="364d0-307">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-307">Property</span></span> | <span data-ttu-id="364d0-308">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-308">Description</span></span> | <span data-ttu-id="364d0-309">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-309">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="364d0-310">name</span><span class="sxs-lookup"><span data-stu-id="364d0-310">name</span></span> | <span data-ttu-id="364d0-311">Name of the linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-311">Name of the linked service.</span></span> | <span data-ttu-id="364d0-312">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-312">Yes</span></span> | 
| <span data-ttu-id="364d0-313">properties - type</span><span class="sxs-lookup"><span data-stu-id="364d0-313">properties - type</span></span> | <span data-ttu-id="364d0-314">Type of the linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-314">Type of the linked service.</span></span> <span data-ttu-id="364d0-315">For example: Azure Storage, Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="364d0-315">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="364d0-316">typeProperties</span><span class="sxs-lookup"><span data-stu-id="364d0-316">typeProperties</span></span> | <span data-ttu-id="364d0-317">The typeProperties section has elements that are different for each data store or compute environment.</span><span class="sxs-lookup"><span data-stu-id="364d0-317">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="364d0-318">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span><span class="sxs-lookup"><span data-stu-id="364d0-318">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="364d0-319">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-319">Dataset</span></span> 
<span data-ttu-id="364d0-320">A dataset in Azure Data Factory is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="364d0-320">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="364d0-321">The following table describes properties in the above JSON:</span><span class="sxs-lookup"><span data-stu-id="364d0-321">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="364d0-322">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-322">Property</span></span> | <span data-ttu-id="364d0-323">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-323">Description</span></span> | <span data-ttu-id="364d0-324">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-324">Required</span></span> | <span data-ttu-id="364d0-325">Default</span><span class="sxs-lookup"><span data-stu-id="364d0-325">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-326">name</span><span class="sxs-lookup"><span data-stu-id="364d0-326">name</span></span> | <span data-ttu-id="364d0-327">Name of the dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-327">Name of the dataset.</span></span> <span data-ttu-id="364d0-328">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span><span class="sxs-lookup"><span data-stu-id="364d0-328">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="364d0-329">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-329">Yes</span></span> |<span data-ttu-id="364d0-330">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-330">NA</span></span> |
| <span data-ttu-id="364d0-331">type</span><span class="sxs-lookup"><span data-stu-id="364d0-331">type</span></span> | <span data-ttu-id="364d0-332">Type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-332">Type of the dataset.</span></span> <span data-ttu-id="364d0-333">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="364d0-333">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="364d0-334">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-334">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="364d0-335">structure</span><span class="sxs-lookup"><span data-stu-id="364d0-335">structure</span></span> | <span data-ttu-id="364d0-336">Schema of the dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-336">Schema of the dataset.</span></span> <span data-ttu-id="364d0-337">It contains columns, their types, etc.</span><span class="sxs-lookup"><span data-stu-id="364d0-337">It contains columns, their types, etc.</span></span> | <span data-ttu-id="364d0-338">No</span><span class="sxs-lookup"><span data-stu-id="364d0-338">No</span></span> |<span data-ttu-id="364d0-339">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-339">NA</span></span> |
| <span data-ttu-id="364d0-340">typeProperties</span><span class="sxs-lookup"><span data-stu-id="364d0-340">typeProperties</span></span> | <span data-ttu-id="364d0-341">Properties corresponding to the selected type.</span><span class="sxs-lookup"><span data-stu-id="364d0-341">Properties corresponding to the selected type.</span></span> <span data-ttu-id="364d0-342">See [DATA STORES](#data-stores) section for supported types and their properties.</span><span class="sxs-lookup"><span data-stu-id="364d0-342">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="364d0-343">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-343">Yes</span></span> |<span data-ttu-id="364d0-344">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-344">NA</span></span> |
| <span data-ttu-id="364d0-345">external</span><span class="sxs-lookup"><span data-stu-id="364d0-345">external</span></span> | <span data-ttu-id="364d0-346">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span><span class="sxs-lookup"><span data-stu-id="364d0-346">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="364d0-347">No</span><span class="sxs-lookup"><span data-stu-id="364d0-347">No</span></span> |<span data-ttu-id="364d0-348">false</span><span class="sxs-lookup"><span data-stu-id="364d0-348">false</span></span> |
| <span data-ttu-id="364d0-349">availability</span><span class="sxs-lookup"><span data-stu-id="364d0-349">availability</span></span> | <span data-ttu-id="364d0-350">Defines the processing window or the slicing model for the dataset production.</span><span class="sxs-lookup"><span data-stu-id="364d0-350">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="364d0-351">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-351">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="364d0-352">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-352">Yes</span></span> |<span data-ttu-id="364d0-353">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-353">NA</span></span> |
| <span data-ttu-id="364d0-354">policy</span><span class="sxs-lookup"><span data-stu-id="364d0-354">policy</span></span> |<span data-ttu-id="364d0-355">Defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="364d0-355">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="364d0-356">For details, see [Dataset Policy](#Policy) section.</span><span class="sxs-lookup"><span data-stu-id="364d0-356">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="364d0-357">No</span><span class="sxs-lookup"><span data-stu-id="364d0-357">No</span></span> |<span data-ttu-id="364d0-358">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-358">NA</span></span> |

<span data-ttu-id="364d0-359">Each column in the **structure** section contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="364d0-359">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="364d0-360">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-360">Property</span></span> | <span data-ttu-id="364d0-361">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-361">Description</span></span> | <span data-ttu-id="364d0-362">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-362">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-363">name</span><span class="sxs-lookup"><span data-stu-id="364d0-363">name</span></span> |<span data-ttu-id="364d0-364">Name of the column.</span><span class="sxs-lookup"><span data-stu-id="364d0-364">Name of the column.</span></span> |<span data-ttu-id="364d0-365">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-365">Yes</span></span> |
| <span data-ttu-id="364d0-366">type</span><span class="sxs-lookup"><span data-stu-id="364d0-366">type</span></span> |<span data-ttu-id="364d0-367">Data type of the column.</span><span class="sxs-lookup"><span data-stu-id="364d0-367">Data type of the column.</span></span>  |<span data-ttu-id="364d0-368">No</span><span class="sxs-lookup"><span data-stu-id="364d0-368">No</span></span> |
| <span data-ttu-id="364d0-369">culture</span><span class="sxs-lookup"><span data-stu-id="364d0-369">culture</span></span> |<span data-ttu-id="364d0-370">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="364d0-370">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="364d0-371">Default is `en-us`.</span><span class="sxs-lookup"><span data-stu-id="364d0-371">Default is `en-us`.</span></span> |<span data-ttu-id="364d0-372">No</span><span class="sxs-lookup"><span data-stu-id="364d0-372">No</span></span> |
| <span data-ttu-id="364d0-373">format</span><span class="sxs-lookup"><span data-stu-id="364d0-373">format</span></span> |<span data-ttu-id="364d0-374">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="364d0-374">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="364d0-375">No</span><span class="sxs-lookup"><span data-stu-id="364d0-375">No</span></span> |

<span data-ttu-id="364d0-376">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span><span class="sxs-lookup"><span data-stu-id="364d0-376">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="364d0-377">The following table describes properties you can use in the **availability** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-377">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="364d0-378">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-378">Property</span></span> | <span data-ttu-id="364d0-379">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-379">Description</span></span> | <span data-ttu-id="364d0-380">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-380">Required</span></span> | <span data-ttu-id="364d0-381">Default</span><span class="sxs-lookup"><span data-stu-id="364d0-381">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-382">frequency</span><span class="sxs-lookup"><span data-stu-id="364d0-382">frequency</span></span> |<span data-ttu-id="364d0-383">Specifies the time unit for dataset slice production.</span><span class="sxs-lookup"><span data-stu-id="364d0-383">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="364d0-384"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span><span class="sxs-lookup"><span data-stu-id="364d0-384"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="364d0-385">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-385">Yes</span></span> |<span data-ttu-id="364d0-386">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-386">NA</span></span> |
| <span data-ttu-id="364d0-387">interval</span><span class="sxs-lookup"><span data-stu-id="364d0-387">interval</span></span> |<span data-ttu-id="364d0-388">Specifies a multiplier for frequency</span><span class="sxs-lookup"><span data-stu-id="364d0-388">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="364d0-389">”Frequency x interval” determines how often the slice is produced.</span><span class="sxs-lookup"><span data-stu-id="364d0-389">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="364d0-390">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="364d0-390">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="364d0-391"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span><span class="sxs-lookup"><span data-stu-id="364d0-391"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="364d0-392">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-392">Yes</span></span> |<span data-ttu-id="364d0-393">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-393">NA</span></span> |
| <span data-ttu-id="364d0-394">style</span><span class="sxs-lookup"><span data-stu-id="364d0-394">style</span></span> |<span data-ttu-id="364d0-395">Specifies whether the slice should be produced at the start/end of the interval.</span><span class="sxs-lookup"><span data-stu-id="364d0-395">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="364d0-396">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="364d0-396">StartOfInterval</span></span></li><li><span data-ttu-id="364d0-397">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="364d0-397">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="364d0-398">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span><span class="sxs-lookup"><span data-stu-id="364d0-398">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="364d0-399">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span><span class="sxs-lookup"><span data-stu-id="364d0-399">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="364d0-400">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span><span class="sxs-lookup"><span data-stu-id="364d0-400">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="364d0-401">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span><span class="sxs-lookup"><span data-stu-id="364d0-401">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="364d0-402">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span><span class="sxs-lookup"><span data-stu-id="364d0-402">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="364d0-403">No</span><span class="sxs-lookup"><span data-stu-id="364d0-403">No</span></span> |<span data-ttu-id="364d0-404">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="364d0-404">EndOfInterval</span></span> |
| <span data-ttu-id="364d0-405">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="364d0-405">anchorDateTime</span></span> |<span data-ttu-id="364d0-406">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span><span class="sxs-lookup"><span data-stu-id="364d0-406">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="364d0-407"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span><span class="sxs-lookup"><span data-stu-id="364d0-407"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="364d0-408">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span><span class="sxs-lookup"><span data-stu-id="364d0-408">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="364d0-409">No</span><span class="sxs-lookup"><span data-stu-id="364d0-409">No</span></span> |<span data-ttu-id="364d0-410">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="364d0-410">01/01/0001</span></span> |
| <span data-ttu-id="364d0-411">offset</span><span class="sxs-lookup"><span data-stu-id="364d0-411">offset</span></span> |<span data-ttu-id="364d0-412">Timespan by which the start and end of all dataset slices are shifted.</span><span class="sxs-lookup"><span data-stu-id="364d0-412">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="364d0-413"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span><span class="sxs-lookup"><span data-stu-id="364d0-413"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="364d0-414">No</span><span class="sxs-lookup"><span data-stu-id="364d0-414">No</span></span> |<span data-ttu-id="364d0-415">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-415">NA</span></span> |

<span data-ttu-id="364d0-416">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span><span class="sxs-lookup"><span data-stu-id="364d0-416">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="364d0-417">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="364d0-417">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="364d0-418">Policy Name</span><span class="sxs-lookup"><span data-stu-id="364d0-418">Policy Name</span></span> | <span data-ttu-id="364d0-419">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-419">Description</span></span> | <span data-ttu-id="364d0-420">Applied To</span><span class="sxs-lookup"><span data-stu-id="364d0-420">Applied To</span></span> | <span data-ttu-id="364d0-421">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-421">Required</span></span> | <span data-ttu-id="364d0-422">Default</span><span class="sxs-lookup"><span data-stu-id="364d0-422">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="364d0-423">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="364d0-423">minimumSizeMB</span></span> |<span data-ttu-id="364d0-424">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span><span class="sxs-lookup"><span data-stu-id="364d0-424">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="364d0-425">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="364d0-425">Azure Blob</span></span> |<span data-ttu-id="364d0-426">No</span><span class="sxs-lookup"><span data-stu-id="364d0-426">No</span></span> |<span data-ttu-id="364d0-427">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-427">NA</span></span> |
| <span data-ttu-id="364d0-428">minimumRows</span><span class="sxs-lookup"><span data-stu-id="364d0-428">minimumRows</span></span> |<span data-ttu-id="364d0-429">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span><span class="sxs-lookup"><span data-stu-id="364d0-429">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="364d0-430">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="364d0-430">Azure SQL Database</span></span></li><li><span data-ttu-id="364d0-431">Azure Table</span><span class="sxs-lookup"><span data-stu-id="364d0-431">Azure Table</span></span></li></ul> |<span data-ttu-id="364d0-432">No</span><span class="sxs-lookup"><span data-stu-id="364d0-432">No</span></span> |<span data-ttu-id="364d0-433">NA</span><span class="sxs-lookup"><span data-stu-id="364d0-433">NA</span></span> |

<span data-ttu-id="364d0-434">**Example:**</span><span class="sxs-lookup"><span data-stu-id="364d0-434">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="364d0-435">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span><span class="sxs-lookup"><span data-stu-id="364d0-435">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="364d0-436">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span><span class="sxs-lookup"><span data-stu-id="364d0-436">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="364d0-437">Name</span><span class="sxs-lookup"><span data-stu-id="364d0-437">Name</span></span> | <span data-ttu-id="364d0-438">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-438">Description</span></span> | <span data-ttu-id="364d0-439">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-439">Required</span></span> | <span data-ttu-id="364d0-440">Default Value</span><span class="sxs-lookup"><span data-stu-id="364d0-440">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-441">dataDelay</span><span class="sxs-lookup"><span data-stu-id="364d0-441">dataDelay</span></span> |<span data-ttu-id="364d0-442">Time to delay the check on the availability of the external data for the given slice.</span><span class="sxs-lookup"><span data-stu-id="364d0-442">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="364d0-443">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span><span class="sxs-lookup"><span data-stu-id="364d0-443">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="364d0-444">Only applies to the present time.</span><span class="sxs-lookup"><span data-stu-id="364d0-444">Only applies to the present time.</span></span>  <span data-ttu-id="364d0-445">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span><span class="sxs-lookup"><span data-stu-id="364d0-445">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="364d0-446">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span><span class="sxs-lookup"><span data-stu-id="364d0-446">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="364d0-447">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="364d0-447">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="364d0-448">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="364d0-448">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="364d0-449">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="364d0-449">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="364d0-450">For 1 day and 4 hours, specify 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="364d0-450">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="364d0-451">No</span><span class="sxs-lookup"><span data-stu-id="364d0-451">No</span></span> |<span data-ttu-id="364d0-452">0</span><span class="sxs-lookup"><span data-stu-id="364d0-452">0</span></span> |
| <span data-ttu-id="364d0-453">retryInterval</span><span class="sxs-lookup"><span data-stu-id="364d0-453">retryInterval</span></span> |<span data-ttu-id="364d0-454">The wait time between a failure and the next retry attempt.</span><span class="sxs-lookup"><span data-stu-id="364d0-454">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="364d0-455">If a try fails, the next try is after retryInterval.</span><span class="sxs-lookup"><span data-stu-id="364d0-455">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="364d0-456">If it is 1:00 PM right now, we begin the first try.</span><span class="sxs-lookup"><span data-stu-id="364d0-456">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="364d0-457">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="364d0-457">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="364d0-458">For slices in the past, there is no delay.</span><span class="sxs-lookup"><span data-stu-id="364d0-458">For slices in the past, there is no delay.</span></span> <span data-ttu-id="364d0-459">The retry happens immediately.</span><span class="sxs-lookup"><span data-stu-id="364d0-459">The retry happens immediately.</span></span> |<span data-ttu-id="364d0-460">No</span><span class="sxs-lookup"><span data-stu-id="364d0-460">No</span></span> |<span data-ttu-id="364d0-461">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="364d0-461">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="364d0-462">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="364d0-462">retryTimeout</span></span> |<span data-ttu-id="364d0-463">The timeout for each retry attempt.</span><span class="sxs-lookup"><span data-stu-id="364d0-463">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="364d0-464">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="364d0-464">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="364d0-465">If it takes longer than 10 minutes to perform the validation, the retry times out.</span><span class="sxs-lookup"><span data-stu-id="364d0-465">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="364d0-466">If all attempts for the validation times out, the slice is marked as TimedOut.</span><span class="sxs-lookup"><span data-stu-id="364d0-466">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="364d0-467">No</span><span class="sxs-lookup"><span data-stu-id="364d0-467">No</span></span> |<span data-ttu-id="364d0-468">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="364d0-468">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="364d0-469">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="364d0-469">maximumRetry</span></span> |<span data-ttu-id="364d0-470">Number of times to check for the availability of the external data.</span><span class="sxs-lookup"><span data-stu-id="364d0-470">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="364d0-471">The allowed maximum value is 10.</span><span class="sxs-lookup"><span data-stu-id="364d0-471">The allowed maximum value is 10.</span></span> |<span data-ttu-id="364d0-472">No</span><span class="sxs-lookup"><span data-stu-id="364d0-472">No</span></span> |<span data-ttu-id="364d0-473">3</span><span class="sxs-lookup"><span data-stu-id="364d0-473">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="364d0-474">DATA STORES</span><span class="sxs-lookup"><span data-stu-id="364d0-474">DATA STORES</span></span>
<span data-ttu-id="364d0-475">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span><span class="sxs-lookup"><span data-stu-id="364d0-475">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="364d0-476">This section provides details about JSON elements that are specific to each data store.</span><span class="sxs-lookup"><span data-stu-id="364d0-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="364d0-477">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span><span class="sxs-lookup"><span data-stu-id="364d0-477">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="364d0-478">This section provides details about JSON elements that are specific to each data store.</span><span class="sxs-lookup"><span data-stu-id="364d0-478">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="364d0-479">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span><span class="sxs-lookup"><span data-stu-id="364d0-479">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="364d0-480">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-480">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="364d0-481">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-481">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="364d0-482">Category</span><span class="sxs-lookup"><span data-stu-id="364d0-482">Category</span></span> | <span data-ttu-id="364d0-483">Data store</span><span class="sxs-lookup"><span data-stu-id="364d0-483">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="364d0-484">**Azure**</span><span class="sxs-lookup"><span data-stu-id="364d0-484">**Azure**</span></span> |[<span data-ttu-id="364d0-485">Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="364d0-485">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="364d0-486">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="364d0-486">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="364d0-487">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="364d0-487">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="364d0-488">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="364d0-488">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="364d0-489">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="364d0-489">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="364d0-490">Azure Search</span><span class="sxs-lookup"><span data-stu-id="364d0-490">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="364d0-491">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="364d0-491">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="364d0-492">**Databases**</span><span class="sxs-lookup"><span data-stu-id="364d0-492">**Databases**</span></span> |[<span data-ttu-id="364d0-493">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="364d0-493">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="364d0-494">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="364d0-494">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="364d0-495">MySQL</span><span class="sxs-lookup"><span data-stu-id="364d0-495">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="364d0-496">Oracle</span><span class="sxs-lookup"><span data-stu-id="364d0-496">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="364d0-497">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="364d0-497">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="364d0-498">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="364d0-498">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="364d0-499">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="364d0-499">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="364d0-500">SQL Server</span><span class="sxs-lookup"><span data-stu-id="364d0-500">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="364d0-501">Sybase</span><span class="sxs-lookup"><span data-stu-id="364d0-501">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="364d0-502">Teradata</span><span class="sxs-lookup"><span data-stu-id="364d0-502">Teradata</span></span>](#teradata) |
| <span data-ttu-id="364d0-503">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="364d0-503">**NoSQL**</span></span> |[<span data-ttu-id="364d0-504">Cassandra</span><span class="sxs-lookup"><span data-stu-id="364d0-504">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="364d0-505">MongoDB</span><span class="sxs-lookup"><span data-stu-id="364d0-505">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="364d0-506">**File**</span><span class="sxs-lookup"><span data-stu-id="364d0-506">**File**</span></span> |[<span data-ttu-id="364d0-507">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="364d0-507">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="364d0-508">File System</span><span class="sxs-lookup"><span data-stu-id="364d0-508">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="364d0-509">FTP</span><span class="sxs-lookup"><span data-stu-id="364d0-509">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="364d0-510">HDFS</span><span class="sxs-lookup"><span data-stu-id="364d0-510">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="364d0-511">SFTP</span><span class="sxs-lookup"><span data-stu-id="364d0-511">SFTP</span></span>](#sftp) |
| <span data-ttu-id="364d0-512">**Others**</span><span class="sxs-lookup"><span data-stu-id="364d0-512">**Others**</span></span> |[<span data-ttu-id="364d0-513">HTTP</span><span class="sxs-lookup"><span data-stu-id="364d0-513">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="364d0-514">OData</span><span class="sxs-lookup"><span data-stu-id="364d0-514">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="364d0-515">ODBC</span><span class="sxs-lookup"><span data-stu-id="364d0-515">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="364d0-516">Salesforce</span><span class="sxs-lookup"><span data-stu-id="364d0-516">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="364d0-517">Web Table</span><span class="sxs-lookup"><span data-stu-id="364d0-517">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="364d0-518">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="364d0-518">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-519">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-519">Linked service</span></span>
<span data-ttu-id="364d0-520">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-520">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="364d0-521">Azure Storage Linked Service</span><span class="sxs-lookup"><span data-stu-id="364d0-521">Azure Storage Linked Service</span></span>
<span data-ttu-id="364d0-522">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-522">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="364d0-523">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="364d0-523">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="364d0-524">Then, you can specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-524">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-525">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-525">Property</span></span> | <span data-ttu-id="364d0-526">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-526">Description</span></span> | <span data-ttu-id="364d0-527">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-527">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-528">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-528">connectionString</span></span> |<span data-ttu-id="364d0-529">Specify information needed to connect to Azure storage for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="364d0-529">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="364d0-530">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-530">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="364d0-531">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-531">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="364d0-532">Azure Storage SAS Linked Service</span><span class="sxs-lookup"><span data-stu-id="364d0-532">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="364d0-533">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="364d0-533">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="364d0-534">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span><span class="sxs-lookup"><span data-stu-id="364d0-534">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="364d0-535">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-535">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="364d0-536">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="364d0-536">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="364d0-537">Then, you can specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-537">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="364d0-538">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-538">Property</span></span> | <span data-ttu-id="364d0-539">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-539">Description</span></span> | <span data-ttu-id="364d0-540">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-540">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-541">sasUri</span><span class="sxs-lookup"><span data-stu-id="364d0-541">sasUri</span></span> |<span data-ttu-id="364d0-542">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span><span class="sxs-lookup"><span data-stu-id="364d0-542">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="364d0-543">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-543">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="364d0-544">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-544">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="364d0-545">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-545">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-546">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-546">Dataset</span></span>
<span data-ttu-id="364d0-547">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="364d0-547">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="364d0-548">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-548">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-549">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-549">Property</span></span> | <span data-ttu-id="364d0-550">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-550">Description</span></span> | <span data-ttu-id="364d0-551">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-551">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-552">folderPath</span><span class="sxs-lookup"><span data-stu-id="364d0-552">folderPath</span></span> |<span data-ttu-id="364d0-553">Path to the container and folder in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="364d0-553">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="364d0-554">Example: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="364d0-554">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="364d0-555">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-555">Yes</span></span> |
| <span data-ttu-id="364d0-556">fileName</span><span class="sxs-lookup"><span data-stu-id="364d0-556">fileName</span></span> |<span data-ttu-id="364d0-557">Name of the blob.</span><span class="sxs-lookup"><span data-stu-id="364d0-557">Name of the blob.</span></span> <span data-ttu-id="364d0-558">fileName is optional and case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-558">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="364d0-559">If you specify a filename, the activity (including Copy) works on the specific Blob.</span><span class="sxs-lookup"><span data-stu-id="364d0-559">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="364d0-560">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-560">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="364d0-561">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="364d0-561">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="364d0-562">No</span><span class="sxs-lookup"><span data-stu-id="364d0-562">No</span></span> |
| <span data-ttu-id="364d0-563">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="364d0-563">partitionedBy</span></span> |<span data-ttu-id="364d0-564">partitionedBy is an optional property.</span><span class="sxs-lookup"><span data-stu-id="364d0-564">partitionedBy is an optional property.</span></span> <span data-ttu-id="364d0-565">You can use it to specify a dynamic folderPath and filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="364d0-565">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="364d0-566">For example, folderPath can be parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="364d0-566">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="364d0-567">No</span><span class="sxs-lookup"><span data-stu-id="364d0-567">No</span></span> |
| <span data-ttu-id="364d0-568">format</span><span class="sxs-lookup"><span data-stu-id="364d0-568">format</span></span> | <span data-ttu-id="364d0-569">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="364d0-569">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="364d0-570">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="364d0-570">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="364d0-571">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-571">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="364d0-572">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="364d0-572">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="364d0-573">No</span><span class="sxs-lookup"><span data-stu-id="364d0-573">No</span></span> |
| <span data-ttu-id="364d0-574">compression</span><span class="sxs-lookup"><span data-stu-id="364d0-574">compression</span></span> | <span data-ttu-id="364d0-575">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-575">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="364d0-576">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="364d0-576">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="364d0-577">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="364d0-577">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="364d0-578">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="364d0-578">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="364d0-579">No</span><span class="sxs-lookup"><span data-stu-id="364d0-579">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-580">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-580">Example</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


<span data-ttu-id="364d0-581">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-581">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="364d0-582">BlobSource in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-582">BlobSource in Copy Activity</span></span>
<span data-ttu-id="364d0-583">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-583">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-584">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-584">Property</span></span> | <span data-ttu-id="364d0-585">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-585">Description</span></span> | <span data-ttu-id="364d0-586">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-586">Allowed values</span></span> | <span data-ttu-id="364d0-587">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-587">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-588">recursive</span><span class="sxs-lookup"><span data-stu-id="364d0-588">recursive</span></span> |<span data-ttu-id="364d0-589">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-589">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="364d0-590">True (default value), False</span><span class="sxs-lookup"><span data-stu-id="364d0-590">True (default value), False</span></span> |<span data-ttu-id="364d0-591">No</span><span class="sxs-lookup"><span data-stu-id="364d0-591">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="364d0-592">Example: **BlobSource**</span><span class="sxs-lookup"><span data-stu-id="364d0-592">Example: **BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="364d0-593">BlobSink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-593">BlobSink in Copy Activity</span></span>
<span data-ttu-id="364d0-594">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-594">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-595">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-595">Property</span></span> | <span data-ttu-id="364d0-596">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-596">Description</span></span> | <span data-ttu-id="364d0-597">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-597">Allowed values</span></span> | <span data-ttu-id="364d0-598">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-598">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-599">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="364d0-599">copyBehavior</span></span> |<span data-ttu-id="364d0-600">Defines the copy behavior when the source is BlobSource or FileSystem.</span><span class="sxs-lookup"><span data-stu-id="364d0-600">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="364d0-601"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-601"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="364d0-602">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-602">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="364d0-603"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-603"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="364d0-604">The target files have auto generated name.</span><span class="sxs-lookup"><span data-stu-id="364d0-604">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="364d0-605"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="364d0-605"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="364d0-606">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="364d0-606">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="364d0-607">No</span><span class="sxs-lookup"><span data-stu-id="364d0-607">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="364d0-608">Example: BlobSink</span><span class="sxs-lookup"><span data-stu-id="364d0-608">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-609">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-609">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="364d0-610">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="364d0-610">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-611">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-611">Linked service</span></span>
<span data-ttu-id="364d0-612">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-612">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-613">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-613">Property</span></span> | <span data-ttu-id="364d0-614">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-614">Description</span></span> | <span data-ttu-id="364d0-615">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-615">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-616">type</span><span class="sxs-lookup"><span data-stu-id="364d0-616">type</span></span> | <span data-ttu-id="364d0-617">The type property must be set to: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="364d0-617">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="364d0-618">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-618">Yes</span></span> |
| <span data-ttu-id="364d0-619">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="364d0-619">dataLakeStoreUri</span></span> | <span data-ttu-id="364d0-620">Specify information about the Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="364d0-620">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="364d0-621">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="364d0-621">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="364d0-622">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-622">Yes</span></span> |
| <span data-ttu-id="364d0-623">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="364d0-623">subscriptionId</span></span> | <span data-ttu-id="364d0-624">Azure subscription Id to which Data Lake Store belongs.</span><span class="sxs-lookup"><span data-stu-id="364d0-624">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="364d0-625">Required for sink</span><span class="sxs-lookup"><span data-stu-id="364d0-625">Required for sink</span></span> |
| <span data-ttu-id="364d0-626">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="364d0-626">resourceGroupName</span></span> | <span data-ttu-id="364d0-627">Azure resource group name to which Data Lake Store belongs.</span><span class="sxs-lookup"><span data-stu-id="364d0-627">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="364d0-628">Required for sink</span><span class="sxs-lookup"><span data-stu-id="364d0-628">Required for sink</span></span> |
| <span data-ttu-id="364d0-629">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="364d0-629">servicePrincipalId</span></span> | <span data-ttu-id="364d0-630">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="364d0-630">Specify the application's client ID.</span></span> | <span data-ttu-id="364d0-631">Yes (for service principal authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-631">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="364d0-632">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="364d0-632">servicePrincipalKey</span></span> | <span data-ttu-id="364d0-633">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="364d0-633">Specify the application's key.</span></span> | <span data-ttu-id="364d0-634">Yes (for service principal authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-634">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="364d0-635">tenant</span><span class="sxs-lookup"><span data-stu-id="364d0-635">tenant</span></span> | <span data-ttu-id="364d0-636">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="364d0-636">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="364d0-637">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="364d0-637">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="364d0-638">Yes (for service principal authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-638">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="364d0-639">authorization</span><span class="sxs-lookup"><span data-stu-id="364d0-639">authorization</span></span> | <span data-ttu-id="364d0-640">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span><span class="sxs-lookup"><span data-stu-id="364d0-640">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="364d0-641">Yes (for user credential authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-641">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="364d0-642">sessionId</span><span class="sxs-lookup"><span data-stu-id="364d0-642">sessionId</span></span> | <span data-ttu-id="364d0-643">OAuth session id from the OAuth authorization session.</span><span class="sxs-lookup"><span data-stu-id="364d0-643">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="364d0-644">Each session id is unique and may only be used once.</span><span class="sxs-lookup"><span data-stu-id="364d0-644">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="364d0-645">This setting is automatically generated when you use Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="364d0-645">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="364d0-646">Yes (for user credential authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-646">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="364d0-647">Example: using service principal authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-647">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="364d0-648">Example: using user credential authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-648">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="364d0-649">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-649">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-650">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-650">Dataset</span></span>
<span data-ttu-id="364d0-651">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-651">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-652">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-652">Property</span></span> | <span data-ttu-id="364d0-653">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-653">Description</span></span> | <span data-ttu-id="364d0-654">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-654">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-655">folderPath</span><span class="sxs-lookup"><span data-stu-id="364d0-655">folderPath</span></span> |<span data-ttu-id="364d0-656">Path to the container and folder in the Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="364d0-656">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="364d0-657">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-657">Yes</span></span> |
| <span data-ttu-id="364d0-658">fileName</span><span class="sxs-lookup"><span data-stu-id="364d0-658">fileName</span></span> |<span data-ttu-id="364d0-659">Name of the file in the Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="364d0-659">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="364d0-660">fileName is optional and case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-660">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="364d0-661">If you specify a filename, the activity (including Copy) works on the specific file.</span><span class="sxs-lookup"><span data-stu-id="364d0-661">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="364d0-662">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-662">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="364d0-663">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="364d0-663">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="364d0-664">No</span><span class="sxs-lookup"><span data-stu-id="364d0-664">No</span></span> |
| <span data-ttu-id="364d0-665">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="364d0-665">partitionedBy</span></span> |<span data-ttu-id="364d0-666">partitionedBy is an optional property.</span><span class="sxs-lookup"><span data-stu-id="364d0-666">partitionedBy is an optional property.</span></span> <span data-ttu-id="364d0-667">You can use it to specify a dynamic folderPath and filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="364d0-667">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="364d0-668">For example, folderPath can be parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="364d0-668">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="364d0-669">No</span><span class="sxs-lookup"><span data-stu-id="364d0-669">No</span></span> |
| <span data-ttu-id="364d0-670">format</span><span class="sxs-lookup"><span data-stu-id="364d0-670">format</span></span> | <span data-ttu-id="364d0-671">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="364d0-671">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="364d0-672">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="364d0-672">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="364d0-673">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-673">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="364d0-674">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="364d0-674">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="364d0-675">No</span><span class="sxs-lookup"><span data-stu-id="364d0-675">No</span></span> |
| <span data-ttu-id="364d0-676">compression</span><span class="sxs-lookup"><span data-stu-id="364d0-676">compression</span></span> | <span data-ttu-id="364d0-677">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-677">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="364d0-678">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="364d0-678">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="364d0-679">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="364d0-679">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="364d0-680">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="364d0-680">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="364d0-681">No</span><span class="sxs-lookup"><span data-stu-id="364d0-681">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-682">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-682">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-683">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-683">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="364d0-684">Azure Data Lake Store Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-684">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="364d0-685">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-685">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="364d0-686">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-686">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="364d0-687">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-687">Property</span></span> | <span data-ttu-id="364d0-688">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-688">Description</span></span> | <span data-ttu-id="364d0-689">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-689">Allowed values</span></span> | <span data-ttu-id="364d0-690">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-690">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-691">recursive</span><span class="sxs-lookup"><span data-stu-id="364d0-691">recursive</span></span> |<span data-ttu-id="364d0-692">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-692">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="364d0-693">True (default value), False</span><span class="sxs-lookup"><span data-stu-id="364d0-693">True (default value), False</span></span> |<span data-ttu-id="364d0-694">No</span><span class="sxs-lookup"><span data-stu-id="364d0-694">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="364d0-695">Example: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="364d0-695">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-696">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-696">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="364d0-697">Azure Data Lake Store Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-697">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-698">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-698">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-699">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-699">Property</span></span> | <span data-ttu-id="364d0-700">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-700">Description</span></span> | <span data-ttu-id="364d0-701">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-701">Allowed values</span></span> | <span data-ttu-id="364d0-702">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-703">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="364d0-703">copyBehavior</span></span> |<span data-ttu-id="364d0-704">Specifies the copy behavior.</span><span class="sxs-lookup"><span data-stu-id="364d0-704">Specifies the copy behavior.</span></span> |<span data-ttu-id="364d0-705"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-705"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="364d0-706">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-706">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="364d0-707"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-707"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="364d0-708">The target files are created with auto generated name.</span><span class="sxs-lookup"><span data-stu-id="364d0-708">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="364d0-709"><b>MergeFiles</b>: merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="364d0-709"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="364d0-710">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="364d0-710">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="364d0-711">No</span><span class="sxs-lookup"><span data-stu-id="364d0-711">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="364d0-712">Example: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="364d0-712">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-713">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-713">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="364d0-714">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="364d0-714">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="364d0-715">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-715">Linked service</span></span>
<span data-ttu-id="364d0-716">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-716">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-717">**Property**</span><span class="sxs-lookup"><span data-stu-id="364d0-717">**Property**</span></span> | <span data-ttu-id="364d0-718">**Description**</span><span class="sxs-lookup"><span data-stu-id="364d0-718">**Description**</span></span> | <span data-ttu-id="364d0-719">**Required**</span><span class="sxs-lookup"><span data-stu-id="364d0-719">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-720">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-720">connectionString</span></span> |<span data-ttu-id="364d0-721">Specify information needed to connect to Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="364d0-721">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="364d0-722">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-722">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-723">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-723">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="364d0-724">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-724">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-725">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-725">Dataset</span></span>
<span data-ttu-id="364d0-726">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-726">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-727">**Property**</span><span class="sxs-lookup"><span data-stu-id="364d0-727">**Property**</span></span> | <span data-ttu-id="364d0-728">**Description**</span><span class="sxs-lookup"><span data-stu-id="364d0-728">**Description**</span></span> | <span data-ttu-id="364d0-729">**Required**</span><span class="sxs-lookup"><span data-stu-id="364d0-729">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-730">collectionName</span><span class="sxs-lookup"><span data-stu-id="364d0-730">collectionName</span></span> |<span data-ttu-id="364d0-731">Name of the Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="364d0-731">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="364d0-732">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-732">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-733">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-733">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="364d0-734">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-734">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="364d0-735">Azure Cosmos DB Collection Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-735">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="364d0-736">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-736">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-737">**Property**</span><span class="sxs-lookup"><span data-stu-id="364d0-737">**Property**</span></span> | <span data-ttu-id="364d0-738">**Description**</span><span class="sxs-lookup"><span data-stu-id="364d0-738">**Description**</span></span> | <span data-ttu-id="364d0-739">**Allowed values**</span><span class="sxs-lookup"><span data-stu-id="364d0-739">**Allowed values**</span></span> | <span data-ttu-id="364d0-740">**Required**</span><span class="sxs-lookup"><span data-stu-id="364d0-740">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-741">query</span><span class="sxs-lookup"><span data-stu-id="364d0-741">query</span></span> |<span data-ttu-id="364d0-742">Specify the query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-742">Specify the query to read data.</span></span> |<span data-ttu-id="364d0-743">Query string supported by Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="364d0-743">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="364d0-744">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="364d0-744">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="364d0-745">No</span><span class="sxs-lookup"><span data-stu-id="364d0-745">No</span></span> <br/><br/><span data-ttu-id="364d0-746">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="364d0-746">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="364d0-747">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="364d0-747">nestingSeparator</span></span> |<span data-ttu-id="364d0-748">Special character to indicate that the document is nested</span><span class="sxs-lookup"><span data-stu-id="364d0-748">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="364d0-749">Any character.</span><span class="sxs-lookup"><span data-stu-id="364d0-749">Any character.</span></span> <br/><br/><span data-ttu-id="364d0-750">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span><span class="sxs-lookup"><span data-stu-id="364d0-750">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="364d0-751">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span><span class="sxs-lookup"><span data-stu-id="364d0-751">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="364d0-752">in the above examples.</span><span class="sxs-lookup"><span data-stu-id="364d0-752">in the above examples.</span></span> <span data-ttu-id="364d0-753">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-753">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="364d0-754">No</span><span class="sxs-lookup"><span data-stu-id="364d0-754">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-755">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-755">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="364d0-756">Azure Cosmos DB Collection Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-756">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-757">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-757">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-758">**Property**</span><span class="sxs-lookup"><span data-stu-id="364d0-758">**Property**</span></span> | <span data-ttu-id="364d0-759">**Description**</span><span class="sxs-lookup"><span data-stu-id="364d0-759">**Description**</span></span> | <span data-ttu-id="364d0-760">**Allowed values**</span><span class="sxs-lookup"><span data-stu-id="364d0-760">**Allowed values**</span></span> | <span data-ttu-id="364d0-761">**Required**</span><span class="sxs-lookup"><span data-stu-id="364d0-761">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-762">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="364d0-762">nestingSeparator</span></span> |<span data-ttu-id="364d0-763">A special character in the source column name to indicate that nested document is needed.</span><span class="sxs-lookup"><span data-stu-id="364d0-763">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="364d0-764">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span><span class="sxs-lookup"><span data-stu-id="364d0-764">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="364d0-765">"Name": {</span><span class="sxs-lookup"><span data-stu-id="364d0-765">"Name": {</span></span><br/>    <span data-ttu-id="364d0-766">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="364d0-766">"First": "John"</span></span><br/><span data-ttu-id="364d0-767">},</span><span class="sxs-lookup"><span data-stu-id="364d0-767">},</span></span> |<span data-ttu-id="364d0-768">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="364d0-768">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="364d0-769">Default value is `.` (dot).</span><span class="sxs-lookup"><span data-stu-id="364d0-769">Default value is `.` (dot).</span></span> |<span data-ttu-id="364d0-770">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="364d0-770">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="364d0-771">Default value is `.` (dot).</span><span class="sxs-lookup"><span data-stu-id="364d0-771">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="364d0-772">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="364d0-772">writeBatchSize</span></span> |<span data-ttu-id="364d0-773">Number of parallel requests to Azure Cosmos DB service to create documents.</span><span class="sxs-lookup"><span data-stu-id="364d0-773">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="364d0-774">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span><span class="sxs-lookup"><span data-stu-id="364d0-774">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="364d0-775">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span><span class="sxs-lookup"><span data-stu-id="364d0-775">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="364d0-776">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span><span class="sxs-lookup"><span data-stu-id="364d0-776">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="364d0-777">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span><span class="sxs-lookup"><span data-stu-id="364d0-777">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="364d0-778">Integer</span><span class="sxs-lookup"><span data-stu-id="364d0-778">Integer</span></span> |<span data-ttu-id="364d0-779">No (default: 5)</span><span class="sxs-lookup"><span data-stu-id="364d0-779">No (default: 5)</span></span> |
| <span data-ttu-id="364d0-780">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="364d0-780">writeBatchTimeout</span></span> |<span data-ttu-id="364d0-781">Wait time for the operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="364d0-781">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="364d0-782">timespan</span><span class="sxs-lookup"><span data-stu-id="364d0-782">timespan</span></span><br/><br/> <span data-ttu-id="364d0-783">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="364d0-783">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="364d0-784">No</span><span class="sxs-lookup"><span data-stu-id="364d0-784">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-785">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-785">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="364d0-786">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-786">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="364d0-787">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="364d0-787">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-788">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-788">Linked service</span></span>
<span data-ttu-id="364d0-789">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-789">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-790">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-790">Property</span></span> | <span data-ttu-id="364d0-791">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-791">Description</span></span> | <span data-ttu-id="364d0-792">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-792">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-793">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-793">connectionString</span></span> |<span data-ttu-id="364d0-794">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="364d0-794">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="364d0-795">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-795">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-796">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-796">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="364d0-797">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-797">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-798">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-798">Dataset</span></span>
<span data-ttu-id="364d0-799">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-799">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-800">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-800">Property</span></span> | <span data-ttu-id="364d0-801">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-801">Description</span></span> | <span data-ttu-id="364d0-802">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-802">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-803">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-803">tableName</span></span> |<span data-ttu-id="364d0-804">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-804">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="364d0-805">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-805">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-806">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-806">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="364d0-807">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-807">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="364d0-808">SQL Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-808">SQL Source in Copy Activity</span></span>
<span data-ttu-id="364d0-809">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-809">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-810">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-810">Property</span></span> | <span data-ttu-id="364d0-811">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-811">Description</span></span> | <span data-ttu-id="364d0-812">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-812">Allowed values</span></span> | <span data-ttu-id="364d0-813">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-813">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-814">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="364d0-814">sqlReaderQuery</span></span> |<span data-ttu-id="364d0-815">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-815">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-816">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-816">SQL query string.</span></span> <span data-ttu-id="364d0-817">Example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-817">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="364d0-818">No</span><span class="sxs-lookup"><span data-stu-id="364d0-818">No</span></span> |
| <span data-ttu-id="364d0-819">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="364d0-819">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="364d0-820">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="364d0-820">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="364d0-821">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-821">Name of the stored procedure.</span></span> |<span data-ttu-id="364d0-822">No</span><span class="sxs-lookup"><span data-stu-id="364d0-822">No</span></span> |
| <span data-ttu-id="364d0-823">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="364d0-823">storedProcedureParameters</span></span> |<span data-ttu-id="364d0-824">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-824">Parameters for the stored procedure.</span></span> |<span data-ttu-id="364d0-825">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="364d0-825">Name/value pairs.</span></span> <span data-ttu-id="364d0-826">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="364d0-826">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="364d0-827">No</span><span class="sxs-lookup"><span data-stu-id="364d0-827">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-828">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-828">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="364d0-829">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-829">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="364d0-830">SQL Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-830">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-831">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-831">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-832">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-832">Property</span></span> | <span data-ttu-id="364d0-833">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-833">Description</span></span> | <span data-ttu-id="364d0-834">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-834">Allowed values</span></span> | <span data-ttu-id="364d0-835">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-835">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-836">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="364d0-836">writeBatchTimeout</span></span> |<span data-ttu-id="364d0-837">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="364d0-837">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="364d0-838">timespan</span><span class="sxs-lookup"><span data-stu-id="364d0-838">timespan</span></span><br/><br/> <span data-ttu-id="364d0-839">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="364d0-839">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="364d0-840">No</span><span class="sxs-lookup"><span data-stu-id="364d0-840">No</span></span> |
| <span data-ttu-id="364d0-841">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="364d0-841">writeBatchSize</span></span> |<span data-ttu-id="364d0-842">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="364d0-842">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="364d0-843">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="364d0-843">Integer (number of rows)</span></span> |<span data-ttu-id="364d0-844">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="364d0-844">No (default: 10000)</span></span> |
| <span data-ttu-id="364d0-845">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="364d0-845">sqlWriterCleanupScript</span></span> |<span data-ttu-id="364d0-846">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="364d0-846">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="364d0-847">A query statement.</span><span class="sxs-lookup"><span data-stu-id="364d0-847">A query statement.</span></span> |<span data-ttu-id="364d0-848">No</span><span class="sxs-lookup"><span data-stu-id="364d0-848">No</span></span> |
| <span data-ttu-id="364d0-849">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="364d0-849">sliceIdentifierColumnName</span></span> |<span data-ttu-id="364d0-850">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="364d0-850">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="364d0-851">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="364d0-851">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="364d0-852">No</span><span class="sxs-lookup"><span data-stu-id="364d0-852">No</span></span> |
| <span data-ttu-id="364d0-853">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="364d0-853">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="364d0-854">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span><span class="sxs-lookup"><span data-stu-id="364d0-854">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="364d0-855">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-855">Name of the stored procedure.</span></span> |<span data-ttu-id="364d0-856">No</span><span class="sxs-lookup"><span data-stu-id="364d0-856">No</span></span> |
| <span data-ttu-id="364d0-857">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="364d0-857">storedProcedureParameters</span></span> |<span data-ttu-id="364d0-858">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-858">Parameters for the stored procedure.</span></span> |<span data-ttu-id="364d0-859">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="364d0-859">Name/value pairs.</span></span> <span data-ttu-id="364d0-860">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="364d0-860">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="364d0-861">No</span><span class="sxs-lookup"><span data-stu-id="364d0-861">No</span></span> |
| <span data-ttu-id="364d0-862">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="364d0-862">sqlWriterTableType</span></span> |<span data-ttu-id="364d0-863">Specify a table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-863">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="364d0-864">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="364d0-864">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="364d0-865">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="364d0-865">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="364d0-866">A table type name.</span><span class="sxs-lookup"><span data-stu-id="364d0-866">A table type name.</span></span> |<span data-ttu-id="364d0-867">No</span><span class="sxs-lookup"><span data-stu-id="364d0-867">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-868">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-868">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-869">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-869">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="364d0-870">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="364d0-870">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-871">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-871">Linked service</span></span>
<span data-ttu-id="364d0-872">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-872">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-873">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-873">Property</span></span> | <span data-ttu-id="364d0-874">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-874">Description</span></span> | <span data-ttu-id="364d0-875">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-875">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-876">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-876">connectionString</span></span> |<span data-ttu-id="364d0-877">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="364d0-877">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="364d0-878">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-878">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="364d0-879">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-879">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="364d0-880">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-880">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-881">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-881">Dataset</span></span>
<span data-ttu-id="364d0-882">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-882">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-883">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-883">Property</span></span> | <span data-ttu-id="364d0-884">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-884">Description</span></span> | <span data-ttu-id="364d0-885">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-885">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-886">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-886">tableName</span></span> |<span data-ttu-id="364d0-887">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-887">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="364d0-888">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-888">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-889">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-889">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-890">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-890">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="364d0-891">SQL DW Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-891">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="364d0-892">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-892">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-893">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-893">Property</span></span> | <span data-ttu-id="364d0-894">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-894">Description</span></span> | <span data-ttu-id="364d0-895">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-895">Allowed values</span></span> | <span data-ttu-id="364d0-896">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-896">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-897">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="364d0-897">sqlReaderQuery</span></span> |<span data-ttu-id="364d0-898">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-898">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-899">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-899">SQL query string.</span></span> <span data-ttu-id="364d0-900">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-900">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="364d0-901">No</span><span class="sxs-lookup"><span data-stu-id="364d0-901">No</span></span> |
| <span data-ttu-id="364d0-902">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="364d0-902">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="364d0-903">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="364d0-903">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="364d0-904">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-904">Name of the stored procedure.</span></span> |<span data-ttu-id="364d0-905">No</span><span class="sxs-lookup"><span data-stu-id="364d0-905">No</span></span> |
| <span data-ttu-id="364d0-906">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="364d0-906">storedProcedureParameters</span></span> |<span data-ttu-id="364d0-907">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-907">Parameters for the stored procedure.</span></span> |<span data-ttu-id="364d0-908">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="364d0-908">Name/value pairs.</span></span> <span data-ttu-id="364d0-909">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="364d0-909">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="364d0-910">No</span><span class="sxs-lookup"><span data-stu-id="364d0-910">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-911">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-911">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-912">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-912">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="364d0-913">SQL DW Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-913">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-914">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-914">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-915">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-915">Property</span></span> | <span data-ttu-id="364d0-916">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-916">Description</span></span> | <span data-ttu-id="364d0-917">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-917">Allowed values</span></span> | <span data-ttu-id="364d0-918">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-918">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-919">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="364d0-919">sqlWriterCleanupScript</span></span> |<span data-ttu-id="364d0-920">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="364d0-920">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="364d0-921">A query statement.</span><span class="sxs-lookup"><span data-stu-id="364d0-921">A query statement.</span></span> |<span data-ttu-id="364d0-922">No</span><span class="sxs-lookup"><span data-stu-id="364d0-922">No</span></span> |
| <span data-ttu-id="364d0-923">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="364d0-923">allowPolyBase</span></span> |<span data-ttu-id="364d0-924">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span><span class="sxs-lookup"><span data-stu-id="364d0-924">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="364d0-925">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="364d0-925">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="364d0-926">True</span><span class="sxs-lookup"><span data-stu-id="364d0-926">True</span></span> <br/><span data-ttu-id="364d0-927">False (default)</span><span class="sxs-lookup"><span data-stu-id="364d0-927">False (default)</span></span> |<span data-ttu-id="364d0-928">No</span><span class="sxs-lookup"><span data-stu-id="364d0-928">No</span></span> |
| <span data-ttu-id="364d0-929">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="364d0-929">polyBaseSettings</span></span> |<span data-ttu-id="364d0-930">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="364d0-930">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="364d0-931">No</span><span class="sxs-lookup"><span data-stu-id="364d0-931">No</span></span> |
| <span data-ttu-id="364d0-932">rejectValue</span><span class="sxs-lookup"><span data-stu-id="364d0-932">rejectValue</span></span> |<span data-ttu-id="364d0-933">Specifies the number or percentage of rows that can be rejected before the query fails.</span><span class="sxs-lookup"><span data-stu-id="364d0-933">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="364d0-934">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="364d0-934">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="364d0-935">0 (default), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="364d0-935">0 (default), 1, 2, …</span></span> |<span data-ttu-id="364d0-936">No</span><span class="sxs-lookup"><span data-stu-id="364d0-936">No</span></span> |
| <span data-ttu-id="364d0-937">rejectType</span><span class="sxs-lookup"><span data-stu-id="364d0-937">rejectType</span></span> |<span data-ttu-id="364d0-938">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span><span class="sxs-lookup"><span data-stu-id="364d0-938">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="364d0-939">Value (default), Percentage</span><span class="sxs-lookup"><span data-stu-id="364d0-939">Value (default), Percentage</span></span> |<span data-ttu-id="364d0-940">No</span><span class="sxs-lookup"><span data-stu-id="364d0-940">No</span></span> |
| <span data-ttu-id="364d0-941">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="364d0-941">rejectSampleValue</span></span> |<span data-ttu-id="364d0-942">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span><span class="sxs-lookup"><span data-stu-id="364d0-942">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="364d0-943">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="364d0-943">1, 2, …</span></span> |<span data-ttu-id="364d0-944">Yes, if **rejectType** is **percentage**</span><span class="sxs-lookup"><span data-stu-id="364d0-944">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="364d0-945">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="364d0-945">useTypeDefault</span></span> |<span data-ttu-id="364d0-946">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span><span class="sxs-lookup"><span data-stu-id="364d0-946">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="364d0-947">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="364d0-947">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="364d0-948">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="364d0-948">True, False (default)</span></span> |<span data-ttu-id="364d0-949">No</span><span class="sxs-lookup"><span data-stu-id="364d0-949">No</span></span> |
| <span data-ttu-id="364d0-950">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="364d0-950">writeBatchSize</span></span> |<span data-ttu-id="364d0-951">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="364d0-951">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="364d0-952">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="364d0-952">Integer (number of rows)</span></span> |<span data-ttu-id="364d0-953">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="364d0-953">No (default: 10000)</span></span> |
| <span data-ttu-id="364d0-954">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="364d0-954">writeBatchTimeout</span></span> |<span data-ttu-id="364d0-955">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="364d0-955">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="364d0-956">timespan</span><span class="sxs-lookup"><span data-stu-id="364d0-956">timespan</span></span><br/><br/> <span data-ttu-id="364d0-957">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="364d0-957">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="364d0-958">No</span><span class="sxs-lookup"><span data-stu-id="364d0-958">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-959">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-959">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-960">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-960">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="364d0-961">Azure Search</span><span class="sxs-lookup"><span data-stu-id="364d0-961">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-962">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-962">Linked service</span></span>
<span data-ttu-id="364d0-963">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-963">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-964">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-964">Property</span></span> | <span data-ttu-id="364d0-965">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-965">Description</span></span> | <span data-ttu-id="364d0-966">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-966">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="364d0-967">url</span><span class="sxs-lookup"><span data-stu-id="364d0-967">url</span></span> | <span data-ttu-id="364d0-968">URL for the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="364d0-968">URL for the Azure Search service.</span></span> | <span data-ttu-id="364d0-969">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-969">Yes</span></span> |
| <span data-ttu-id="364d0-970">key</span><span class="sxs-lookup"><span data-stu-id="364d0-970">key</span></span> | <span data-ttu-id="364d0-971">Admin key for the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="364d0-971">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="364d0-972">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-972">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-973">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-973">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="364d0-974">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-974">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-975">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-975">Dataset</span></span>
<span data-ttu-id="364d0-976">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-976">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-977">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-977">Property</span></span> | <span data-ttu-id="364d0-978">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-978">Description</span></span> | <span data-ttu-id="364d0-979">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-979">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="364d0-980">type</span><span class="sxs-lookup"><span data-stu-id="364d0-980">type</span></span> | <span data-ttu-id="364d0-981">The type property must be set to **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="364d0-981">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="364d0-982">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-982">Yes</span></span> |
| <span data-ttu-id="364d0-983">indexName</span><span class="sxs-lookup"><span data-stu-id="364d0-983">indexName</span></span> | <span data-ttu-id="364d0-984">Name of the Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="364d0-984">Name of the Azure Search index.</span></span> <span data-ttu-id="364d0-985">Data Factory does not create the index.</span><span class="sxs-lookup"><span data-stu-id="364d0-985">Data Factory does not create the index.</span></span> <span data-ttu-id="364d0-986">The index must exist in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="364d0-986">The index must exist in Azure Search.</span></span> | <span data-ttu-id="364d0-987">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-987">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-988">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-988">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="364d0-989">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-989">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="364d0-990">Azure Search Index Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-990">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-991">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-991">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-992">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-992">Property</span></span> | <span data-ttu-id="364d0-993">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-993">Description</span></span> | <span data-ttu-id="364d0-994">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-994">Allowed values</span></span> | <span data-ttu-id="364d0-995">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-995">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="364d0-996">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="364d0-996">WriteBehavior</span></span> | <span data-ttu-id="364d0-997">Specifies whether to merge or replace when a document already exists in the index.</span><span class="sxs-lookup"><span data-stu-id="364d0-997">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="364d0-998">Merge (default)</span><span class="sxs-lookup"><span data-stu-id="364d0-998">Merge (default)</span></span><br/><span data-ttu-id="364d0-999">Upload</span><span class="sxs-lookup"><span data-stu-id="364d0-999">Upload</span></span>| <span data-ttu-id="364d0-1000">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1000">No</span></span> |
| <span data-ttu-id="364d0-1001">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="364d0-1001">WriteBatchSize</span></span> | <span data-ttu-id="364d0-1002">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="364d0-1002">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="364d0-1003">1 to 1,000.</span><span class="sxs-lookup"><span data-stu-id="364d0-1003">1 to 1,000.</span></span> <span data-ttu-id="364d0-1004">Default value is 1000.</span><span class="sxs-lookup"><span data-stu-id="364d0-1004">Default value is 1000.</span></span> | <span data-ttu-id="364d0-1005">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1005">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1006">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1006">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-1007">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1007">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="364d0-1008">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="364d0-1008">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1009">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1009">Linked service</span></span>
<span data-ttu-id="364d0-1010">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-1010">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="364d0-1011">Azure Storage Linked Service</span><span class="sxs-lookup"><span data-stu-id="364d0-1011">Azure Storage Linked Service</span></span>
<span data-ttu-id="364d0-1012">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-1012">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="364d0-1013">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1013">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="364d0-1014">Then, you can specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1014">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1015">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1015">Property</span></span> | <span data-ttu-id="364d0-1016">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1016">Description</span></span> | <span data-ttu-id="364d0-1017">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1017">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-1018">type</span><span class="sxs-lookup"><span data-stu-id="364d0-1018">type</span></span> |<span data-ttu-id="364d0-1019">The type property must be set to: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="364d0-1019">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="364d0-1020">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1020">Yes</span></span> |
| <span data-ttu-id="364d0-1021">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-1021">connectionString</span></span> |<span data-ttu-id="364d0-1022">Specify information needed to connect to Azure storage for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="364d0-1022">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="364d0-1023">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1023">Yes</span></span> |

<span data-ttu-id="364d0-1024">**Example:**</span><span class="sxs-lookup"><span data-stu-id="364d0-1024">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="364d0-1025">Azure Storage SAS Linked Service</span><span class="sxs-lookup"><span data-stu-id="364d0-1025">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="364d0-1026">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="364d0-1026">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="364d0-1027">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span><span class="sxs-lookup"><span data-stu-id="364d0-1027">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="364d0-1028">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-1028">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="364d0-1029">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1029">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="364d0-1030">Then, you can specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1030">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="364d0-1031">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1031">Property</span></span> | <span data-ttu-id="364d0-1032">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1032">Description</span></span> | <span data-ttu-id="364d0-1033">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1033">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-1034">type</span><span class="sxs-lookup"><span data-stu-id="364d0-1034">type</span></span> |<span data-ttu-id="364d0-1035">The type property must be set to: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="364d0-1035">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="364d0-1036">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1036">Yes</span></span> |
| <span data-ttu-id="364d0-1037">sasUri</span><span class="sxs-lookup"><span data-stu-id="364d0-1037">sasUri</span></span> |<span data-ttu-id="364d0-1038">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span><span class="sxs-lookup"><span data-stu-id="364d0-1038">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="364d0-1039">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1039">Yes</span></span> |

<span data-ttu-id="364d0-1040">**Example:**</span><span class="sxs-lookup"><span data-stu-id="364d0-1040">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="364d0-1041">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1041">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-1042">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1042">Dataset</span></span>
<span data-ttu-id="364d0-1043">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1043">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1044">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1044">Property</span></span> | <span data-ttu-id="364d0-1045">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1045">Description</span></span> | <span data-ttu-id="364d0-1046">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1046">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1047">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1047">tableName</span></span> |<span data-ttu-id="364d0-1048">Name of the table in the Azure Table Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-1048">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="364d0-1049">Yes.</span><span class="sxs-lookup"><span data-stu-id="364d0-1049">Yes.</span></span> <span data-ttu-id="364d0-1050">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="364d0-1050">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="364d0-1051">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="364d0-1051">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1052">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1052">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-1053">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1053">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="364d0-1054">Azure Table Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1054">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1055">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1055">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-1056">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1056">Property</span></span> | <span data-ttu-id="364d0-1057">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1057">Description</span></span> | <span data-ttu-id="364d0-1058">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1058">Allowed values</span></span> | <span data-ttu-id="364d0-1059">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1059">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1060">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="364d0-1060">azureTableSourceQuery</span></span> |<span data-ttu-id="364d0-1061">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1061">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1062">Azure table query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1062">Azure table query string.</span></span> <span data-ttu-id="364d0-1063">See examples in the next section.</span><span class="sxs-lookup"><span data-stu-id="364d0-1063">See examples in the next section.</span></span> |<span data-ttu-id="364d0-1064">No.</span><span class="sxs-lookup"><span data-stu-id="364d0-1064">No.</span></span> <span data-ttu-id="364d0-1065">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="364d0-1065">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="364d0-1066">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="364d0-1066">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="364d0-1067">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="364d0-1067">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="364d0-1068">Indicate whether swallow the exception of table not exist.</span><span class="sxs-lookup"><span data-stu-id="364d0-1068">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="364d0-1069">TRUE</span><span class="sxs-lookup"><span data-stu-id="364d0-1069">TRUE</span></span><br/><span data-ttu-id="364d0-1070">FALSE</span><span class="sxs-lookup"><span data-stu-id="364d0-1070">FALSE</span></span> |<span data-ttu-id="364d0-1071">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1071">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1072">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1072">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-1073">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1073">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="364d0-1074">Azure Table Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1074">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-1075">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1075">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-1076">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1076">Property</span></span> | <span data-ttu-id="364d0-1077">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1077">Description</span></span> | <span data-ttu-id="364d0-1078">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1078">Allowed values</span></span> | <span data-ttu-id="364d0-1079">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1079">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1080">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="364d0-1080">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="364d0-1081">Default partition key value that can be used by the sink.</span><span class="sxs-lookup"><span data-stu-id="364d0-1081">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="364d0-1082">A string value.</span><span class="sxs-lookup"><span data-stu-id="364d0-1082">A string value.</span></span> |<span data-ttu-id="364d0-1083">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1083">No</span></span> |
| <span data-ttu-id="364d0-1084">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="364d0-1084">azureTablePartitionKeyName</span></span> |<span data-ttu-id="364d0-1085">Specify name of the column whose values are used as partition keys.</span><span class="sxs-lookup"><span data-stu-id="364d0-1085">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="364d0-1086">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span><span class="sxs-lookup"><span data-stu-id="364d0-1086">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="364d0-1087">A column name.</span><span class="sxs-lookup"><span data-stu-id="364d0-1087">A column name.</span></span> |<span data-ttu-id="364d0-1088">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1088">No</span></span> |
| <span data-ttu-id="364d0-1089">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="364d0-1089">azureTableRowKeyName</span></span> |<span data-ttu-id="364d0-1090">Specify name of the column whose column values are used as row key.</span><span class="sxs-lookup"><span data-stu-id="364d0-1090">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="364d0-1091">If not specified, use a GUID for each row.</span><span class="sxs-lookup"><span data-stu-id="364d0-1091">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="364d0-1092">A column name.</span><span class="sxs-lookup"><span data-stu-id="364d0-1092">A column name.</span></span> |<span data-ttu-id="364d0-1093">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1093">No</span></span> |
| <span data-ttu-id="364d0-1094">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="364d0-1094">azureTableInsertType</span></span> |<span data-ttu-id="364d0-1095">The mode to insert data into Azure table.</span><span class="sxs-lookup"><span data-stu-id="364d0-1095">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="364d0-1096">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span><span class="sxs-lookup"><span data-stu-id="364d0-1096">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="364d0-1097">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span><span class="sxs-lookup"><span data-stu-id="364d0-1097">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="364d0-1098">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span><span class="sxs-lookup"><span data-stu-id="364d0-1098">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="364d0-1099">merge (default)</span><span class="sxs-lookup"><span data-stu-id="364d0-1099">merge (default)</span></span><br/><span data-ttu-id="364d0-1100">replace</span><span class="sxs-lookup"><span data-stu-id="364d0-1100">replace</span></span> |<span data-ttu-id="364d0-1101">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1101">No</span></span> |
| <span data-ttu-id="364d0-1102">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="364d0-1102">writeBatchSize</span></span> |<span data-ttu-id="364d0-1103">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span><span class="sxs-lookup"><span data-stu-id="364d0-1103">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="364d0-1104">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="364d0-1104">Integer (number of rows)</span></span> |<span data-ttu-id="364d0-1105">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="364d0-1105">No (default: 10000)</span></span> |
| <span data-ttu-id="364d0-1106">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="364d0-1106">writeBatchTimeout</span></span> |<span data-ttu-id="364d0-1107">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span><span class="sxs-lookup"><span data-stu-id="364d0-1107">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="364d0-1108">timespan</span><span class="sxs-lookup"><span data-stu-id="364d0-1108">timespan</span></span><br/><br/><span data-ttu-id="364d0-1109">Example: “00:20:00” (20 minutes)</span><span class="sxs-lookup"><span data-stu-id="364d0-1109">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="364d0-1110">No (Default to storage client default timeout value 90 sec)</span><span class="sxs-lookup"><span data-stu-id="364d0-1110">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1111">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1111">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="364d0-1112">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1112">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="364d0-1113">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="364d0-1113">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1114">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1114">Linked service</span></span>
<span data-ttu-id="364d0-1115">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1115">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1116">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1116">Property</span></span> | <span data-ttu-id="364d0-1117">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1117">Description</span></span> | <span data-ttu-id="364d0-1118">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1118">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1119">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1119">server</span></span> |<span data-ttu-id="364d0-1120">IP address or host name of the Amazon Redshift server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1120">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="364d0-1121">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1121">Yes</span></span> |
| <span data-ttu-id="364d0-1122">port</span><span class="sxs-lookup"><span data-stu-id="364d0-1122">port</span></span> |<span data-ttu-id="364d0-1123">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="364d0-1123">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="364d0-1124">No, default value: 5439</span><span class="sxs-lookup"><span data-stu-id="364d0-1124">No, default value: 5439</span></span> |
| <span data-ttu-id="364d0-1125">database</span><span class="sxs-lookup"><span data-stu-id="364d0-1125">database</span></span> |<span data-ttu-id="364d0-1126">Name of the Amazon Redshift database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1126">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="364d0-1127">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1127">Yes</span></span> |
| <span data-ttu-id="364d0-1128">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1128">username</span></span> |<span data-ttu-id="364d0-1129">Name of user who has access to the database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1129">Name of user who has access to the database.</span></span> |<span data-ttu-id="364d0-1130">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1130">Yes</span></span> |
| <span data-ttu-id="364d0-1131">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1131">password</span></span> |<span data-ttu-id="364d0-1132">Password for the user account.</span><span class="sxs-lookup"><span data-stu-id="364d0-1132">Password for the user account.</span></span> |<span data-ttu-id="364d0-1133">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1133">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1134">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1134">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="364d0-1135">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1135">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-1136">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1136">Dataset</span></span>
<span data-ttu-id="364d0-1137">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1137">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1138">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1138">Property</span></span> | <span data-ttu-id="364d0-1139">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1139">Description</span></span> | <span data-ttu-id="364d0-1140">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1141">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1141">tableName</span></span> |<span data-ttu-id="364d0-1142">Name of the table in the Amazon Redshift database that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-1142">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="364d0-1143">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1143">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="364d0-1144">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1144">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="364d0-1145">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1145">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-1146">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1146">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="364d0-1147">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1147">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-1148">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1148">Property</span></span> | <span data-ttu-id="364d0-1149">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1149">Description</span></span> | <span data-ttu-id="364d0-1150">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1150">Allowed values</span></span> | <span data-ttu-id="364d0-1151">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1151">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1152">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1152">query</span></span> |<span data-ttu-id="364d0-1153">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1153">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1154">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1154">SQL query string.</span></span> <span data-ttu-id="364d0-1155">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1155">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="364d0-1156">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1156">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1157">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1157">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="364d0-1158">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1158">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="364d0-1159">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="364d0-1159">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1160">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1160">Linked service</span></span>
<span data-ttu-id="364d0-1161">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1161">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1162">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1162">Property</span></span> | <span data-ttu-id="364d0-1163">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1163">Description</span></span> | <span data-ttu-id="364d0-1164">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1165">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1165">server</span></span> |<span data-ttu-id="364d0-1166">Name of the DB2 server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1166">Name of the DB2 server.</span></span> |<span data-ttu-id="364d0-1167">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1167">Yes</span></span> |
| <span data-ttu-id="364d0-1168">database</span><span class="sxs-lookup"><span data-stu-id="364d0-1168">database</span></span> |<span data-ttu-id="364d0-1169">Name of the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1169">Name of the DB2 database.</span></span> |<span data-ttu-id="364d0-1170">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1170">Yes</span></span> |
| <span data-ttu-id="364d0-1171">schema</span><span class="sxs-lookup"><span data-stu-id="364d0-1171">schema</span></span> |<span data-ttu-id="364d0-1172">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1172">Name of the schema in the database.</span></span> <span data-ttu-id="364d0-1173">The schema name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-1173">The schema name is case-sensitive.</span></span> |<span data-ttu-id="364d0-1174">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1174">No</span></span> |
| <span data-ttu-id="364d0-1175">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-1175">authenticationType</span></span> |<span data-ttu-id="364d0-1176">Type of authentication used to connect to the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1176">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="364d0-1177">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="364d0-1177">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="364d0-1178">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1178">Yes</span></span> |
| <span data-ttu-id="364d0-1179">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1179">username</span></span> |<span data-ttu-id="364d0-1180">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-1180">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="364d0-1181">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1181">No</span></span> |
| <span data-ttu-id="364d0-1182">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1182">password</span></span> |<span data-ttu-id="364d0-1183">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="364d0-1183">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="364d0-1184">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1184">No</span></span> |
| <span data-ttu-id="364d0-1185">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1185">gatewayName</span></span> |<span data-ttu-id="364d0-1186">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1186">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="364d0-1187">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1187">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1188">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1188">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="364d0-1189">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1189">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-1190">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1190">Dataset</span></span>
<span data-ttu-id="364d0-1191">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1191">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="364d0-1192">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1192">Property</span></span> | <span data-ttu-id="364d0-1193">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1193">Description</span></span> | <span data-ttu-id="364d0-1194">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1195">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1195">tableName</span></span> |<span data-ttu-id="364d0-1196">Name of the table in the DB2 Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-1196">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="364d0-1197">The tableName is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-1197">The tableName is case-sensitive.</span></span> |<span data-ttu-id="364d0-1198">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1198">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="364d0-1199">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1199">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-1200">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1200">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-1201">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1201">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1202">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1202">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-1203">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1203">Property</span></span> | <span data-ttu-id="364d0-1204">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1204">Description</span></span> | <span data-ttu-id="364d0-1205">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1205">Allowed values</span></span> | <span data-ttu-id="364d0-1206">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1206">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1207">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1207">query</span></span> |<span data-ttu-id="364d0-1208">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1208">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1209">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1209">SQL query string.</span></span> <span data-ttu-id="364d0-1210">For example: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1210">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="364d0-1211">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1211">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1212">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1212">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="364d0-1213">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1213">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="364d0-1214">MySQL</span><span class="sxs-lookup"><span data-stu-id="364d0-1214">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1215">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1215">Linked service</span></span>
<span data-ttu-id="364d0-1216">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1216">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1217">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1217">Property</span></span> | <span data-ttu-id="364d0-1218">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1218">Description</span></span> | <span data-ttu-id="364d0-1219">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1219">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1220">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1220">server</span></span> |<span data-ttu-id="364d0-1221">Name of the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1221">Name of the MySQL server.</span></span> |<span data-ttu-id="364d0-1222">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1222">Yes</span></span> |
| <span data-ttu-id="364d0-1223">database</span><span class="sxs-lookup"><span data-stu-id="364d0-1223">database</span></span> |<span data-ttu-id="364d0-1224">Name of the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1224">Name of the MySQL database.</span></span> |<span data-ttu-id="364d0-1225">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1225">Yes</span></span> |
| <span data-ttu-id="364d0-1226">schema</span><span class="sxs-lookup"><span data-stu-id="364d0-1226">schema</span></span> |<span data-ttu-id="364d0-1227">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1227">Name of the schema in the database.</span></span> |<span data-ttu-id="364d0-1228">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1228">No</span></span> |
| <span data-ttu-id="364d0-1229">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-1229">authenticationType</span></span> |<span data-ttu-id="364d0-1230">Type of authentication used to connect to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1230">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="364d0-1231">Possible values are: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1231">Possible values are: `Basic`.</span></span> |<span data-ttu-id="364d0-1232">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1232">Yes</span></span> |
| <span data-ttu-id="364d0-1233">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1233">username</span></span> |<span data-ttu-id="364d0-1234">Specify user name to connect to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1234">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="364d0-1235">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1235">Yes</span></span> |
| <span data-ttu-id="364d0-1236">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1236">password</span></span> |<span data-ttu-id="364d0-1237">Specify password for the user account you specified.</span><span class="sxs-lookup"><span data-stu-id="364d0-1237">Specify password for the user account you specified.</span></span> |<span data-ttu-id="364d0-1238">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1238">Yes</span></span> |
| <span data-ttu-id="364d0-1239">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1239">gatewayName</span></span> |<span data-ttu-id="364d0-1240">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1240">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="364d0-1241">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1241">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1242">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1242">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="364d0-1243">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1243">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-1244">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1244">Dataset</span></span>
<span data-ttu-id="364d0-1245">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1245">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1246">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1246">Property</span></span> | <span data-ttu-id="364d0-1247">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1247">Description</span></span> | <span data-ttu-id="364d0-1248">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1248">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1249">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1249">tableName</span></span> |<span data-ttu-id="364d0-1250">Name of the table in the MySQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-1250">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="364d0-1251">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1251">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1252">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1252">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="364d0-1253">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1253">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-1254">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1254">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1255">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1255">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-1256">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1256">Property</span></span> | <span data-ttu-id="364d0-1257">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1257">Description</span></span> | <span data-ttu-id="364d0-1258">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1258">Allowed values</span></span> | <span data-ttu-id="364d0-1259">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1259">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1260">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1260">query</span></span> |<span data-ttu-id="364d0-1261">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1261">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1262">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1262">SQL query string.</span></span> <span data-ttu-id="364d0-1263">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1263">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="364d0-1264">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1264">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="364d0-1265">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1265">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="364d0-1266">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1266">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="364d0-1267">Oracle</span><span class="sxs-lookup"><span data-stu-id="364d0-1267">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-1268">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1268">Linked service</span></span>
<span data-ttu-id="364d0-1269">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1269">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1270">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1270">Property</span></span> | <span data-ttu-id="364d0-1271">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1271">Description</span></span> | <span data-ttu-id="364d0-1272">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1272">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1273">driverType</span><span class="sxs-lookup"><span data-stu-id="364d0-1273">driverType</span></span> | <span data-ttu-id="364d0-1274">Specify which driver to use to copy data from/to Oracle Database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1274">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="364d0-1275">Allowed values are **Microsoft** or **ODP** (default).</span><span class="sxs-lookup"><span data-stu-id="364d0-1275">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="364d0-1276">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span><span class="sxs-lookup"><span data-stu-id="364d0-1276">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="364d0-1277">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1277">No</span></span> |
| <span data-ttu-id="364d0-1278">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-1278">connectionString</span></span> | <span data-ttu-id="364d0-1279">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="364d0-1279">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="364d0-1280">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1280">Yes</span></span> |
| <span data-ttu-id="364d0-1281">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1281">gatewayName</span></span> | <span data-ttu-id="364d0-1282">Name of the gateway that is used to connect to the on-premises Oracle server</span><span class="sxs-lookup"><span data-stu-id="364d0-1282">Name of the gateway that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="364d0-1283">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1283">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1284">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1284">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="364d0-1285">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1285">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-1286">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1286">Dataset</span></span>
<span data-ttu-id="364d0-1287">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1287">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1288">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1288">Property</span></span> | <span data-ttu-id="364d0-1289">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1289">Description</span></span> | <span data-ttu-id="364d0-1290">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1290">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1291">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1291">tableName</span></span> |<span data-ttu-id="364d0-1292">Name of the table in the Oracle Database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-1292">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="364d0-1293">No (if **oracleReaderQuery** of **OracleSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1293">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1294">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1294">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="364d0-1295">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1295">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="364d0-1296">Oracle Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1296">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1297">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1297">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-1298">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1298">Property</span></span> | <span data-ttu-id="364d0-1299">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1299">Description</span></span> | <span data-ttu-id="364d0-1300">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1300">Allowed values</span></span> | <span data-ttu-id="364d0-1301">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1301">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1302">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="364d0-1302">oracleReaderQuery</span></span> |<span data-ttu-id="364d0-1303">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1303">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1304">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1304">SQL query string.</span></span> <span data-ttu-id="364d0-1305">For example: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="364d0-1305">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="364d0-1306">If not specified, the SQL statement that is executed: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="364d0-1306">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="364d0-1307">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1307">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1308">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1308">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-1309">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1309">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="364d0-1310">Oracle Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1310">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-1311">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1311">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-1312">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1312">Property</span></span> | <span data-ttu-id="364d0-1313">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1313">Description</span></span> | <span data-ttu-id="364d0-1314">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1314">Allowed values</span></span> | <span data-ttu-id="364d0-1315">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1315">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1316">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="364d0-1316">writeBatchTimeout</span></span> |<span data-ttu-id="364d0-1317">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="364d0-1317">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="364d0-1318">timespan</span><span class="sxs-lookup"><span data-stu-id="364d0-1318">timespan</span></span><br/><br/> <span data-ttu-id="364d0-1319">Example: 00:30:00 (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="364d0-1319">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="364d0-1320">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1320">No</span></span> |
| <span data-ttu-id="364d0-1321">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="364d0-1321">writeBatchSize</span></span> |<span data-ttu-id="364d0-1322">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="364d0-1322">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="364d0-1323">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="364d0-1323">Integer (number of rows)</span></span> |<span data-ttu-id="364d0-1324">No (default: 100)</span><span class="sxs-lookup"><span data-stu-id="364d0-1324">No (default: 100)</span></span> |
| <span data-ttu-id="364d0-1325">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="364d0-1325">sqlWriterCleanupScript</span></span> |<span data-ttu-id="364d0-1326">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="364d0-1326">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="364d0-1327">A query statement.</span><span class="sxs-lookup"><span data-stu-id="364d0-1327">A query statement.</span></span> |<span data-ttu-id="364d0-1328">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1328">No</span></span> |
| <span data-ttu-id="364d0-1329">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="364d0-1329">sliceIdentifierColumnName</span></span> |<span data-ttu-id="364d0-1330">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="364d0-1330">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="364d0-1331">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="364d0-1331">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="364d0-1332">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1332">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1333">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1333">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="364d0-1334">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1334">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="364d0-1335">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="364d0-1335">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1336">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1336">Linked service</span></span>
<span data-ttu-id="364d0-1337">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1337">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1338">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1338">Property</span></span> | <span data-ttu-id="364d0-1339">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1339">Description</span></span> | <span data-ttu-id="364d0-1340">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1340">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1341">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1341">server</span></span> |<span data-ttu-id="364d0-1342">Name of the PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1342">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="364d0-1343">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1343">Yes</span></span> |
| <span data-ttu-id="364d0-1344">database</span><span class="sxs-lookup"><span data-stu-id="364d0-1344">database</span></span> |<span data-ttu-id="364d0-1345">Name of the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1345">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="364d0-1346">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1346">Yes</span></span> |
| <span data-ttu-id="364d0-1347">schema</span><span class="sxs-lookup"><span data-stu-id="364d0-1347">schema</span></span> |<span data-ttu-id="364d0-1348">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1348">Name of the schema in the database.</span></span> <span data-ttu-id="364d0-1349">The schema name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-1349">The schema name is case-sensitive.</span></span> |<span data-ttu-id="364d0-1350">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1350">No</span></span> |
| <span data-ttu-id="364d0-1351">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-1351">authenticationType</span></span> |<span data-ttu-id="364d0-1352">Type of authentication used to connect to the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1352">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="364d0-1353">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="364d0-1353">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="364d0-1354">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1354">Yes</span></span> |
| <span data-ttu-id="364d0-1355">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1355">username</span></span> |<span data-ttu-id="364d0-1356">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-1356">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="364d0-1357">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1357">No</span></span> |
| <span data-ttu-id="364d0-1358">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1358">password</span></span> |<span data-ttu-id="364d0-1359">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="364d0-1359">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="364d0-1360">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1360">No</span></span> |
| <span data-ttu-id="364d0-1361">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1361">gatewayName</span></span> |<span data-ttu-id="364d0-1362">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1362">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="364d0-1363">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1363">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1364">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1364">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="364d0-1365">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1365">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-1366">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1366">Dataset</span></span>
<span data-ttu-id="364d0-1367">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1367">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1368">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1368">Property</span></span> | <span data-ttu-id="364d0-1369">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1369">Description</span></span> | <span data-ttu-id="364d0-1370">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1370">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1371">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1371">tableName</span></span> |<span data-ttu-id="364d0-1372">Name of the table in the PostgreSQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-1372">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="364d0-1373">The tableName is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-1373">The tableName is case-sensitive.</span></span> |<span data-ttu-id="364d0-1374">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1374">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1375">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1375">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="364d0-1376">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1376">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-1377">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1377">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1378">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1378">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-1379">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1379">Property</span></span> | <span data-ttu-id="364d0-1380">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1380">Description</span></span> | <span data-ttu-id="364d0-1381">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1381">Allowed values</span></span> | <span data-ttu-id="364d0-1382">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1382">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1383">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1383">query</span></span> |<span data-ttu-id="364d0-1384">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1384">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1385">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1385">SQL query string.</span></span> <span data-ttu-id="364d0-1386">For example: "query": "select \* from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="364d0-1386">For example: "query": "select \* from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="364d0-1387">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1387">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1388">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1388">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="364d0-1389">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1389">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="364d0-1390">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="364d0-1390">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="364d0-1391">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1391">Linked service</span></span>
<span data-ttu-id="364d0-1392">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1392">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="364d0-1393">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1393">Property</span></span> | <span data-ttu-id="364d0-1394">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1394">Description</span></span> | <span data-ttu-id="364d0-1395">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1395">Allowed values</span></span> | <span data-ttu-id="364d0-1396">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1396">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="364d0-1397">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1397">server</span></span> | <span data-ttu-id="364d0-1398">Name of the server on which the SAP BW instance resides.</span><span class="sxs-lookup"><span data-stu-id="364d0-1398">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="364d0-1399">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1399">string</span></span> | <span data-ttu-id="364d0-1400">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1400">Yes</span></span>
<span data-ttu-id="364d0-1401">systemNumber</span><span class="sxs-lookup"><span data-stu-id="364d0-1401">systemNumber</span></span> | <span data-ttu-id="364d0-1402">System number of the SAP BW system.</span><span class="sxs-lookup"><span data-stu-id="364d0-1402">System number of the SAP BW system.</span></span> | <span data-ttu-id="364d0-1403">Two-digit decimal number represented as a string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1403">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="364d0-1404">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1404">Yes</span></span>
<span data-ttu-id="364d0-1405">clientId</span><span class="sxs-lookup"><span data-stu-id="364d0-1405">clientId</span></span> | <span data-ttu-id="364d0-1406">Client ID of the client in the SAP W system.</span><span class="sxs-lookup"><span data-stu-id="364d0-1406">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="364d0-1407">Three-digit decimal number represented as a string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1407">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="364d0-1408">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1408">Yes</span></span>
<span data-ttu-id="364d0-1409">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1409">username</span></span> | <span data-ttu-id="364d0-1410">Name of the user who has access to the SAP server</span><span class="sxs-lookup"><span data-stu-id="364d0-1410">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="364d0-1411">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1411">string</span></span> | <span data-ttu-id="364d0-1412">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1412">Yes</span></span>
<span data-ttu-id="364d0-1413">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1413">password</span></span> | <span data-ttu-id="364d0-1414">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="364d0-1414">Password for the user.</span></span> | <span data-ttu-id="364d0-1415">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1415">string</span></span> | <span data-ttu-id="364d0-1416">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1416">Yes</span></span>
<span data-ttu-id="364d0-1417">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1417">gatewayName</span></span> | <span data-ttu-id="364d0-1418">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="364d0-1418">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="364d0-1419">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1419">string</span></span> | <span data-ttu-id="364d0-1420">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1420">Yes</span></span>
<span data-ttu-id="364d0-1421">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-1421">encryptedCredential</span></span> | <span data-ttu-id="364d0-1422">The encrypted credential string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1422">The encrypted credential string.</span></span> | <span data-ttu-id="364d0-1423">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1423">string</span></span> | <span data-ttu-id="364d0-1424">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1424">No</span></span>

#### <a name="example"></a><span data-ttu-id="364d0-1425">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1425">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="364d0-1426">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1426">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-1427">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1427">Dataset</span></span>
<span data-ttu-id="364d0-1428">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1428">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="364d0-1429">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1429">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="364d0-1430">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1430">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="364d0-1431">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1431">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-1432">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1432">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1433">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1433">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-1434">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1434">Property</span></span> | <span data-ttu-id="364d0-1435">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1435">Description</span></span> | <span data-ttu-id="364d0-1436">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1436">Allowed values</span></span> | <span data-ttu-id="364d0-1437">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1437">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1438">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1438">query</span></span> | <span data-ttu-id="364d0-1439">Specifies the MDX query to read data from the SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="364d0-1439">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="364d0-1440">MDX query.</span><span class="sxs-lookup"><span data-stu-id="364d0-1440">MDX query.</span></span> | <span data-ttu-id="364d0-1441">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1441">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1442">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1442">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="364d0-1443">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1443">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="364d0-1444">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="364d0-1444">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1445">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1445">Linked service</span></span>
<span data-ttu-id="364d0-1446">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1446">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="364d0-1447">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1447">Property</span></span> | <span data-ttu-id="364d0-1448">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1448">Description</span></span> | <span data-ttu-id="364d0-1449">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1449">Allowed values</span></span> | <span data-ttu-id="364d0-1450">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1450">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="364d0-1451">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1451">server</span></span> | <span data-ttu-id="364d0-1452">Name of the server on which the SAP HANA instance resides.</span><span class="sxs-lookup"><span data-stu-id="364d0-1452">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="364d0-1453">If your server is using a customized port, specify `server:port`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1453">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="364d0-1454">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1454">string</span></span> | <span data-ttu-id="364d0-1455">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1455">Yes</span></span>
<span data-ttu-id="364d0-1456">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-1456">authenticationType</span></span> | <span data-ttu-id="364d0-1457">Type of authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-1457">Type of authentication.</span></span> | <span data-ttu-id="364d0-1458">string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1458">string.</span></span> <span data-ttu-id="364d0-1459">"Basic" or "Windows"</span><span class="sxs-lookup"><span data-stu-id="364d0-1459">"Basic" or "Windows"</span></span> | <span data-ttu-id="364d0-1460">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1460">Yes</span></span> 
<span data-ttu-id="364d0-1461">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1461">username</span></span> | <span data-ttu-id="364d0-1462">Name of the user who has access to the SAP server</span><span class="sxs-lookup"><span data-stu-id="364d0-1462">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="364d0-1463">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1463">string</span></span> | <span data-ttu-id="364d0-1464">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1464">Yes</span></span>
<span data-ttu-id="364d0-1465">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1465">password</span></span> | <span data-ttu-id="364d0-1466">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="364d0-1466">Password for the user.</span></span> | <span data-ttu-id="364d0-1467">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1467">string</span></span> | <span data-ttu-id="364d0-1468">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1468">Yes</span></span>
<span data-ttu-id="364d0-1469">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1469">gatewayName</span></span> | <span data-ttu-id="364d0-1470">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="364d0-1470">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="364d0-1471">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1471">string</span></span> | <span data-ttu-id="364d0-1472">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1472">Yes</span></span>
<span data-ttu-id="364d0-1473">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-1473">encryptedCredential</span></span> | <span data-ttu-id="364d0-1474">The encrypted credential string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1474">The encrypted credential string.</span></span> | <span data-ttu-id="364d0-1475">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1475">string</span></span> | <span data-ttu-id="364d0-1476">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1476">No</span></span>

#### <a name="example"></a><span data-ttu-id="364d0-1477">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1477">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="364d0-1478">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1478">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="364d0-1479">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1479">Dataset</span></span>
<span data-ttu-id="364d0-1480">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1480">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="364d0-1481">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1481">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="364d0-1482">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1482">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="364d0-1483">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1483">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-1484">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1484">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1485">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1485">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-1486">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1486">Property</span></span> | <span data-ttu-id="364d0-1487">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1487">Description</span></span> | <span data-ttu-id="364d0-1488">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1488">Allowed values</span></span> | <span data-ttu-id="364d0-1489">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1489">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1490">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1490">query</span></span> | <span data-ttu-id="364d0-1491">Specifies the SQL query to read data from the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="364d0-1491">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="364d0-1492">SQL query.</span><span class="sxs-lookup"><span data-stu-id="364d0-1492">SQL query.</span></span> | <span data-ttu-id="364d0-1493">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1493">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="364d0-1494">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1494">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="364d0-1495">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1495">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="364d0-1496">SQL Server</span><span class="sxs-lookup"><span data-stu-id="364d0-1496">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1497">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1497">Linked service</span></span>
<span data-ttu-id="364d0-1498">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-1498">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="364d0-1499">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-1499">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="364d0-1500">The following table provides description for JSON elements specific to SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-1500">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="364d0-1501">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1501">Property</span></span> | <span data-ttu-id="364d0-1502">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1502">Description</span></span> | <span data-ttu-id="364d0-1503">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1503">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1504">type</span><span class="sxs-lookup"><span data-stu-id="364d0-1504">type</span></span> |<span data-ttu-id="364d0-1505">The type property should be set to: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1505">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="364d0-1506">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1506">Yes</span></span> |
| <span data-ttu-id="364d0-1507">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-1507">connectionString</span></span> |<span data-ttu-id="364d0-1508">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-1508">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="364d0-1509">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1509">Yes</span></span> |
| <span data-ttu-id="364d0-1510">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1510">gatewayName</span></span> |<span data-ttu-id="364d0-1511">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1511">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="364d0-1512">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1512">Yes</span></span> |
| <span data-ttu-id="364d0-1513">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1513">username</span></span> |<span data-ttu-id="364d0-1514">Specify user name if you are using Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-1514">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="364d0-1515">Example: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1515">Example: **domainname\\username**.</span></span> |<span data-ttu-id="364d0-1516">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1516">No</span></span> |
| <span data-ttu-id="364d0-1517">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1517">password</span></span> |<span data-ttu-id="364d0-1518">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="364d0-1518">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="364d0-1519">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1519">No</span></span> |

<span data-ttu-id="364d0-1520">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span><span class="sxs-lookup"><span data-stu-id="364d0-1520">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="364d0-1521">Example: JSON for using SQL Authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-1521">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="364d0-1522">Example: JSON for using Windows Authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-1522">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="364d0-1523">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1523">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="364d0-1524">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span><span class="sxs-lookup"><span data-stu-id="364d0-1524">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="364d0-1525">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1525">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-1526">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1526">Dataset</span></span>
<span data-ttu-id="364d0-1527">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1527">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1528">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1528">Property</span></span> | <span data-ttu-id="364d0-1529">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1529">Description</span></span> | <span data-ttu-id="364d0-1530">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1530">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1531">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1531">tableName</span></span> |<span data-ttu-id="364d0-1532">Name of the table or view in the SQL Server Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-1532">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="364d0-1533">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1533">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1534">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1534">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-1535">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1535">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="364d0-1536">Sql Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1536">Sql Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1537">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1537">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-1538">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1538">Property</span></span> | <span data-ttu-id="364d0-1539">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1539">Description</span></span> | <span data-ttu-id="364d0-1540">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1540">Allowed values</span></span> | <span data-ttu-id="364d0-1541">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1541">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1542">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="364d0-1542">sqlReaderQuery</span></span> |<span data-ttu-id="364d0-1543">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1543">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1544">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1544">SQL query string.</span></span> <span data-ttu-id="364d0-1545">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1545">For example: `select * from MyTable`.</span></span> <span data-ttu-id="364d0-1546">May reference multiple tables from the database referenced by the input dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-1546">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="364d0-1547">If not specified, the SQL statement that is executed: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="364d0-1547">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="364d0-1548">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1548">No</span></span> |
| <span data-ttu-id="364d0-1549">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="364d0-1549">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="364d0-1550">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="364d0-1550">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="364d0-1551">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-1551">Name of the stored procedure.</span></span> |<span data-ttu-id="364d0-1552">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1552">No</span></span> |
| <span data-ttu-id="364d0-1553">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="364d0-1553">storedProcedureParameters</span></span> |<span data-ttu-id="364d0-1554">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-1554">Parameters for the stored procedure.</span></span> |<span data-ttu-id="364d0-1555">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="364d0-1555">Name/value pairs.</span></span> <span data-ttu-id="364d0-1556">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="364d0-1556">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="364d0-1557">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1557">No</span></span> |

<span data-ttu-id="364d0-1558">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1558">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="364d0-1559">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="364d0-1559">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="364d0-1560">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1560">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="364d0-1561">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="364d0-1561">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="364d0-1562">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span><span class="sxs-lookup"><span data-stu-id="364d0-1562">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="364d0-1563">There are no validations performed against this table though.</span><span class="sxs-lookup"><span data-stu-id="364d0-1563">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="364d0-1564">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1564">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-1565">In this example, **sqlReaderQuery** is specified for the SqlSource.</span><span class="sxs-lookup"><span data-stu-id="364d0-1565">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="364d0-1566">The Copy Activity runs this query against the SQL Server Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1566">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="364d0-1567">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="364d0-1567">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="364d0-1568">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-1568">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="364d0-1569">It is not limited to only the table set as the dataset's tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="364d0-1569">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="364d0-1570">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1570">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="364d0-1571">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="364d0-1571">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="364d0-1572">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1572">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="364d0-1573">Sql Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1573">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-1574">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1574">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-1575">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1575">Property</span></span> | <span data-ttu-id="364d0-1576">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1576">Description</span></span> | <span data-ttu-id="364d0-1577">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1577">Allowed values</span></span> | <span data-ttu-id="364d0-1578">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1578">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1579">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="364d0-1579">writeBatchTimeout</span></span> |<span data-ttu-id="364d0-1580">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="364d0-1580">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="364d0-1581">timespan</span><span class="sxs-lookup"><span data-stu-id="364d0-1581">timespan</span></span><br/><br/> <span data-ttu-id="364d0-1582">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="364d0-1582">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="364d0-1583">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1583">No</span></span> |
| <span data-ttu-id="364d0-1584">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="364d0-1584">writeBatchSize</span></span> |<span data-ttu-id="364d0-1585">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="364d0-1585">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="364d0-1586">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="364d0-1586">Integer (number of rows)</span></span> |<span data-ttu-id="364d0-1587">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="364d0-1587">No (default: 10000)</span></span> |
| <span data-ttu-id="364d0-1588">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="364d0-1588">sqlWriterCleanupScript</span></span> |<span data-ttu-id="364d0-1589">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="364d0-1589">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="364d0-1590">For more information, see [repeatability](#repeatability-during-copy) section.</span><span class="sxs-lookup"><span data-stu-id="364d0-1590">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="364d0-1591">A query statement.</span><span class="sxs-lookup"><span data-stu-id="364d0-1591">A query statement.</span></span> |<span data-ttu-id="364d0-1592">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1592">No</span></span> |
| <span data-ttu-id="364d0-1593">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="364d0-1593">sliceIdentifierColumnName</span></span> |<span data-ttu-id="364d0-1594">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="364d0-1594">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="364d0-1595">For more information, see [repeatability](#repeatability-during-copy) section.</span><span class="sxs-lookup"><span data-stu-id="364d0-1595">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="364d0-1596">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="364d0-1596">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="364d0-1597">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1597">No</span></span> |
| <span data-ttu-id="364d0-1598">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="364d0-1598">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="364d0-1599">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span><span class="sxs-lookup"><span data-stu-id="364d0-1599">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="364d0-1600">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-1600">Name of the stored procedure.</span></span> |<span data-ttu-id="364d0-1601">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1601">No</span></span> |
| <span data-ttu-id="364d0-1602">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="364d0-1602">storedProcedureParameters</span></span> |<span data-ttu-id="364d0-1603">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-1603">Parameters for the stored procedure.</span></span> |<span data-ttu-id="364d0-1604">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="364d0-1604">Name/value pairs.</span></span> <span data-ttu-id="364d0-1605">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="364d0-1605">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="364d0-1606">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1606">No</span></span> |
| <span data-ttu-id="364d0-1607">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="364d0-1607">sqlWriterTableType</span></span> |<span data-ttu-id="364d0-1608">Specify table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="364d0-1608">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="364d0-1609">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="364d0-1609">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="364d0-1610">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1610">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="364d0-1611">A table type name.</span><span class="sxs-lookup"><span data-stu-id="364d0-1611">A table type name.</span></span> |<span data-ttu-id="364d0-1612">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1612">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1613">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1613">Example</span></span>
<span data-ttu-id="364d0-1614">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="364d0-1614">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="364d0-1615">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1615">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-1616">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1616">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="364d0-1617">Sybase</span><span class="sxs-lookup"><span data-stu-id="364d0-1617">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1618">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1618">Linked service</span></span>
<span data-ttu-id="364d0-1619">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1619">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1620">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1620">Property</span></span> | <span data-ttu-id="364d0-1621">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1621">Description</span></span> | <span data-ttu-id="364d0-1622">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1622">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1623">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1623">server</span></span> |<span data-ttu-id="364d0-1624">Name of the Sybase server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1624">Name of the Sybase server.</span></span> |<span data-ttu-id="364d0-1625">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1625">Yes</span></span> |
| <span data-ttu-id="364d0-1626">database</span><span class="sxs-lookup"><span data-stu-id="364d0-1626">database</span></span> |<span data-ttu-id="364d0-1627">Name of the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1627">Name of the Sybase database.</span></span> |<span data-ttu-id="364d0-1628">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1628">Yes</span></span> |
| <span data-ttu-id="364d0-1629">schema</span><span class="sxs-lookup"><span data-stu-id="364d0-1629">schema</span></span> |<span data-ttu-id="364d0-1630">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1630">Name of the schema in the database.</span></span> |<span data-ttu-id="364d0-1631">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1631">No</span></span> |
| <span data-ttu-id="364d0-1632">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-1632">authenticationType</span></span> |<span data-ttu-id="364d0-1633">Type of authentication used to connect to the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1633">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="364d0-1634">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="364d0-1634">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="364d0-1635">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1635">Yes</span></span> |
| <span data-ttu-id="364d0-1636">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1636">username</span></span> |<span data-ttu-id="364d0-1637">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-1637">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="364d0-1638">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1638">No</span></span> |
| <span data-ttu-id="364d0-1639">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1639">password</span></span> |<span data-ttu-id="364d0-1640">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="364d0-1640">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="364d0-1641">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1641">No</span></span> |
| <span data-ttu-id="364d0-1642">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1642">gatewayName</span></span> |<span data-ttu-id="364d0-1643">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1643">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="364d0-1644">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1644">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1645">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1645">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="364d0-1646">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1646">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-1647">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1647">Dataset</span></span>
<span data-ttu-id="364d0-1648">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1648">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1649">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1649">Property</span></span> | <span data-ttu-id="364d0-1650">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1650">Description</span></span> | <span data-ttu-id="364d0-1651">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1651">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1652">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1652">tableName</span></span> |<span data-ttu-id="364d0-1653">Name of the table in the Sybase Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="364d0-1653">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="364d0-1654">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1654">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1655">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1655">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-1656">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1656">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-1657">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1657">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1658">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1658">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-1659">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1659">Property</span></span> | <span data-ttu-id="364d0-1660">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1660">Description</span></span> | <span data-ttu-id="364d0-1661">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1661">Allowed values</span></span> | <span data-ttu-id="364d0-1662">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1662">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1663">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1663">query</span></span> |<span data-ttu-id="364d0-1664">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1664">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1665">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1665">SQL query string.</span></span> <span data-ttu-id="364d0-1666">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1666">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="364d0-1667">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1667">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1668">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1668">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="364d0-1669">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1669">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="364d0-1670">Teradata</span><span class="sxs-lookup"><span data-stu-id="364d0-1670">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1671">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1671">Linked service</span></span>
<span data-ttu-id="364d0-1672">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1672">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1673">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1673">Property</span></span> | <span data-ttu-id="364d0-1674">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1674">Description</span></span> | <span data-ttu-id="364d0-1675">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1675">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1676">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1676">server</span></span> |<span data-ttu-id="364d0-1677">Name of the Teradata server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1677">Name of the Teradata server.</span></span> |<span data-ttu-id="364d0-1678">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1678">Yes</span></span> |
| <span data-ttu-id="364d0-1679">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-1679">authenticationType</span></span> |<span data-ttu-id="364d0-1680">Type of authentication used to connect to the Teradata database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1680">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="364d0-1681">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="364d0-1681">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="364d0-1682">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1682">Yes</span></span> |
| <span data-ttu-id="364d0-1683">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1683">username</span></span> |<span data-ttu-id="364d0-1684">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-1684">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="364d0-1685">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1685">No</span></span> |
| <span data-ttu-id="364d0-1686">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1686">password</span></span> |<span data-ttu-id="364d0-1687">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="364d0-1687">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="364d0-1688">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1688">No</span></span> |
| <span data-ttu-id="364d0-1689">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1689">gatewayName</span></span> |<span data-ttu-id="364d0-1690">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1690">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="364d0-1691">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1691">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1692">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1692">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="364d0-1693">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1693">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-1694">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1694">Dataset</span></span>
<span data-ttu-id="364d0-1695">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1695">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="364d0-1696">Currently, there are no type properties supported for the Teradata dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-1696">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="364d0-1697">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1697">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-1698">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1698">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-1699">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1699">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1700">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1700">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-1701">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1701">Property</span></span> | <span data-ttu-id="364d0-1702">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1702">Description</span></span> | <span data-ttu-id="364d0-1703">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1703">Allowed values</span></span> | <span data-ttu-id="364d0-1704">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1704">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1705">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1705">query</span></span> |<span data-ttu-id="364d0-1706">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1706">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1707">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1707">SQL query string.</span></span> <span data-ttu-id="364d0-1708">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1708">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="364d0-1709">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1709">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1710">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1710">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="364d0-1711">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1711">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="364d0-1712">Cassandra</span><span class="sxs-lookup"><span data-stu-id="364d0-1712">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="364d0-1713">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1713">Linked service</span></span>
<span data-ttu-id="364d0-1714">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1714">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1715">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1715">Property</span></span> | <span data-ttu-id="364d0-1716">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1716">Description</span></span> | <span data-ttu-id="364d0-1717">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1717">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1718">host</span><span class="sxs-lookup"><span data-stu-id="364d0-1718">host</span></span> |<span data-ttu-id="364d0-1719">One or more IP addresses or host names of Cassandra servers.</span><span class="sxs-lookup"><span data-stu-id="364d0-1719">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="364d0-1720">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span><span class="sxs-lookup"><span data-stu-id="364d0-1720">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="364d0-1721">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1721">Yes</span></span> |
| <span data-ttu-id="364d0-1722">port</span><span class="sxs-lookup"><span data-stu-id="364d0-1722">port</span></span> |<span data-ttu-id="364d0-1723">The TCP port that the Cassandra server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="364d0-1723">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="364d0-1724">No, default value: 9042</span><span class="sxs-lookup"><span data-stu-id="364d0-1724">No, default value: 9042</span></span> |
| <span data-ttu-id="364d0-1725">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-1725">authenticationType</span></span> |<span data-ttu-id="364d0-1726">Basic, or Anonymous</span><span class="sxs-lookup"><span data-stu-id="364d0-1726">Basic, or Anonymous</span></span> |<span data-ttu-id="364d0-1727">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1727">Yes</span></span> |
| <span data-ttu-id="364d0-1728">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1728">username</span></span> |<span data-ttu-id="364d0-1729">Specify user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="364d0-1729">Specify user name for the user account.</span></span> |<span data-ttu-id="364d0-1730">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="364d0-1730">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="364d0-1731">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1731">password</span></span> |<span data-ttu-id="364d0-1732">Specify password for the user account.</span><span class="sxs-lookup"><span data-stu-id="364d0-1732">Specify password for the user account.</span></span> |<span data-ttu-id="364d0-1733">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="364d0-1733">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="364d0-1734">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1734">gatewayName</span></span> |<span data-ttu-id="364d0-1735">The name of the gateway that is used to connect to the on-premises Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1735">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="364d0-1736">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1736">Yes</span></span> |
| <span data-ttu-id="364d0-1737">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-1737">encryptedCredential</span></span> |<span data-ttu-id="364d0-1738">Credential encrypted by the gateway.</span><span class="sxs-lookup"><span data-stu-id="364d0-1738">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="364d0-1739">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1739">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1740">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1740">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="364d0-1741">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1741">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-1742">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1742">Dataset</span></span>
<span data-ttu-id="364d0-1743">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1743">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1744">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1744">Property</span></span> | <span data-ttu-id="364d0-1745">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1745">Description</span></span> | <span data-ttu-id="364d0-1746">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1746">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1747">keyspace</span><span class="sxs-lookup"><span data-stu-id="364d0-1747">keyspace</span></span> |<span data-ttu-id="364d0-1748">Name of the keyspace or schema in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1748">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="364d0-1749">Yes (If **query** for **CassandraSource** is not defined).</span><span class="sxs-lookup"><span data-stu-id="364d0-1749">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="364d0-1750">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-1750">tableName</span></span> |<span data-ttu-id="364d0-1751">Name of the table in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1751">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="364d0-1752">Yes (If **query** for **CassandraSource** is not defined).</span><span class="sxs-lookup"><span data-stu-id="364d0-1752">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1753">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1753">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-1754">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1754">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="364d0-1755">Cassandra Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1755">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1756">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1756">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-1757">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1757">Property</span></span> | <span data-ttu-id="364d0-1758">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1758">Description</span></span> | <span data-ttu-id="364d0-1759">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1759">Allowed values</span></span> | <span data-ttu-id="364d0-1760">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1760">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1761">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1761">query</span></span> |<span data-ttu-id="364d0-1762">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1762">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1763">SQL-92 query or CQL query.</span><span class="sxs-lookup"><span data-stu-id="364d0-1763">SQL-92 query or CQL query.</span></span> <span data-ttu-id="364d0-1764">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="364d0-1764">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="364d0-1765">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span><span class="sxs-lookup"><span data-stu-id="364d0-1765">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="364d0-1766">No (if tableName and keyspace on dataset are defined).</span><span class="sxs-lookup"><span data-stu-id="364d0-1766">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="364d0-1767">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="364d0-1767">consistencyLevel</span></span> |<span data-ttu-id="364d0-1768">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span><span class="sxs-lookup"><span data-stu-id="364d0-1768">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="364d0-1769">Cassandra checks the specified number of replicas for data to satisfy the read request.</span><span class="sxs-lookup"><span data-stu-id="364d0-1769">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="364d0-1770">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="364d0-1770">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="364d0-1771">See [Configuring data consistency](https://docs.datastax.com/en/cassandra/2.1/cassandra/dml/dml_config_consistency_c.html) for details.</span><span class="sxs-lookup"><span data-stu-id="364d0-1771">See [Configuring data consistency](https://docs.datastax.com/en/cassandra/2.1/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="364d0-1772">No.</span><span class="sxs-lookup"><span data-stu-id="364d0-1772">No.</span></span> <span data-ttu-id="364d0-1773">Default value is ONE.</span><span class="sxs-lookup"><span data-stu-id="364d0-1773">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1774">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1774">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-1775">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-1775">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="364d0-1776">MongoDB</span><span class="sxs-lookup"><span data-stu-id="364d0-1776">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-1777">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1777">Linked service</span></span>
<span data-ttu-id="364d0-1778">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1778">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1779">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1779">Property</span></span> | <span data-ttu-id="364d0-1780">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1780">Description</span></span> | <span data-ttu-id="364d0-1781">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1781">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1782">server</span><span class="sxs-lookup"><span data-stu-id="364d0-1782">server</span></span> |<span data-ttu-id="364d0-1783">IP address or host name of the MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1783">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="364d0-1784">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1784">Yes</span></span> |
| <span data-ttu-id="364d0-1785">port</span><span class="sxs-lookup"><span data-stu-id="364d0-1785">port</span></span> |<span data-ttu-id="364d0-1786">TCP port that the MongoDB server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="364d0-1786">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="364d0-1787">Optional, default value: 27017</span><span class="sxs-lookup"><span data-stu-id="364d0-1787">Optional, default value: 27017</span></span> |
| <span data-ttu-id="364d0-1788">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-1788">authenticationType</span></span> |<span data-ttu-id="364d0-1789">Basic, or Anonymous.</span><span class="sxs-lookup"><span data-stu-id="364d0-1789">Basic, or Anonymous.</span></span> |<span data-ttu-id="364d0-1790">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1790">Yes</span></span> |
| <span data-ttu-id="364d0-1791">username</span><span class="sxs-lookup"><span data-stu-id="364d0-1791">username</span></span> |<span data-ttu-id="364d0-1792">User account to access MongoDB.</span><span class="sxs-lookup"><span data-stu-id="364d0-1792">User account to access MongoDB.</span></span> |<span data-ttu-id="364d0-1793">Yes (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="364d0-1793">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="364d0-1794">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1794">password</span></span> |<span data-ttu-id="364d0-1795">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="364d0-1795">Password for the user.</span></span> |<span data-ttu-id="364d0-1796">Yes (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="364d0-1796">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="364d0-1797">authSource</span><span class="sxs-lookup"><span data-stu-id="364d0-1797">authSource</span></span> |<span data-ttu-id="364d0-1798">Name of the MongoDB database that you want to use to check your credentials for authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-1798">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="364d0-1799">Optional (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="364d0-1799">Optional (if basic authentication is used).</span></span> <span data-ttu-id="364d0-1800">default: uses the admin account and the database specified using databaseName property.</span><span class="sxs-lookup"><span data-stu-id="364d0-1800">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="364d0-1801">databaseName</span><span class="sxs-lookup"><span data-stu-id="364d0-1801">databaseName</span></span> |<span data-ttu-id="364d0-1802">Name of the MongoDB database that you want to access.</span><span class="sxs-lookup"><span data-stu-id="364d0-1802">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="364d0-1803">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1803">Yes</span></span> |
| <span data-ttu-id="364d0-1804">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1804">gatewayName</span></span> |<span data-ttu-id="364d0-1805">Name of the gateway that accesses the data store.</span><span class="sxs-lookup"><span data-stu-id="364d0-1805">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="364d0-1806">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1806">Yes</span></span> |
| <span data-ttu-id="364d0-1807">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-1807">encryptedCredential</span></span> |<span data-ttu-id="364d0-1808">Credential encrypted by gateway.</span><span class="sxs-lookup"><span data-stu-id="364d0-1808">Credential encrypted by gateway.</span></span> |<span data-ttu-id="364d0-1809">Optional</span><span class="sxs-lookup"><span data-stu-id="364d0-1809">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1810">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1810">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="364d0-1811">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="364d0-1811">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-1812">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1812">Dataset</span></span>
<span data-ttu-id="364d0-1813">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1813">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1814">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1814">Property</span></span> | <span data-ttu-id="364d0-1815">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1815">Description</span></span> | <span data-ttu-id="364d0-1816">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1816">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1817">collectionName</span><span class="sxs-lookup"><span data-stu-id="364d0-1817">collectionName</span></span> |<span data-ttu-id="364d0-1818">Name of the collection in MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="364d0-1818">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="364d0-1819">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1819">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1820">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1820">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="364d0-1821">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="364d0-1821">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="364d0-1822">MongoDB Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1822">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1823">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1823">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-1824">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1824">Property</span></span> | <span data-ttu-id="364d0-1825">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1825">Description</span></span> | <span data-ttu-id="364d0-1826">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1826">Allowed values</span></span> | <span data-ttu-id="364d0-1827">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1827">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1828">query</span><span class="sxs-lookup"><span data-stu-id="364d0-1828">query</span></span> |<span data-ttu-id="364d0-1829">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1829">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-1830">SQL-92 query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1830">SQL-92 query string.</span></span> <span data-ttu-id="364d0-1831">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-1831">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="364d0-1832">No (if **collectionName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-1832">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1833">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1833">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="364d0-1834">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="364d0-1834">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="364d0-1835">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="364d0-1835">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="364d0-1836">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1836">Linked service</span></span>
<span data-ttu-id="364d0-1837">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1837">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-1838">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1838">Property</span></span> | <span data-ttu-id="364d0-1839">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1839">Description</span></span> | <span data-ttu-id="364d0-1840">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1840">Allowed values</span></span> | <span data-ttu-id="364d0-1841">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1841">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1842">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="364d0-1842">accessKeyID</span></span> |<span data-ttu-id="364d0-1843">ID of the secret access key.</span><span class="sxs-lookup"><span data-stu-id="364d0-1843">ID of the secret access key.</span></span> |<span data-ttu-id="364d0-1844">string</span><span class="sxs-lookup"><span data-stu-id="364d0-1844">string</span></span> |<span data-ttu-id="364d0-1845">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1845">Yes</span></span> |
| <span data-ttu-id="364d0-1846">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="364d0-1846">secretAccessKey</span></span> |<span data-ttu-id="364d0-1847">The secret access key itself.</span><span class="sxs-lookup"><span data-stu-id="364d0-1847">The secret access key itself.</span></span> |<span data-ttu-id="364d0-1848">Encrypted secret string</span><span class="sxs-lookup"><span data-stu-id="364d0-1848">Encrypted secret string</span></span> |<span data-ttu-id="364d0-1849">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1849">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-1850">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1850">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="364d0-1851">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="364d0-1851">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-1852">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1852">Dataset</span></span>
<span data-ttu-id="364d0-1853">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1853">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1854">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1854">Property</span></span> | <span data-ttu-id="364d0-1855">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1855">Description</span></span> | <span data-ttu-id="364d0-1856">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1856">Allowed values</span></span> | <span data-ttu-id="364d0-1857">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1857">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1858">bucketName</span><span class="sxs-lookup"><span data-stu-id="364d0-1858">bucketName</span></span> |<span data-ttu-id="364d0-1859">The S3 bucket name.</span><span class="sxs-lookup"><span data-stu-id="364d0-1859">The S3 bucket name.</span></span> |<span data-ttu-id="364d0-1860">String</span><span class="sxs-lookup"><span data-stu-id="364d0-1860">String</span></span> |<span data-ttu-id="364d0-1861">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1861">Yes</span></span> |
| <span data-ttu-id="364d0-1862">key</span><span class="sxs-lookup"><span data-stu-id="364d0-1862">key</span></span> |<span data-ttu-id="364d0-1863">The S3 object key.</span><span class="sxs-lookup"><span data-stu-id="364d0-1863">The S3 object key.</span></span> |<span data-ttu-id="364d0-1864">String</span><span class="sxs-lookup"><span data-stu-id="364d0-1864">String</span></span> |<span data-ttu-id="364d0-1865">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1865">No</span></span> |
| <span data-ttu-id="364d0-1866">prefix</span><span class="sxs-lookup"><span data-stu-id="364d0-1866">prefix</span></span> |<span data-ttu-id="364d0-1867">Prefix for the S3 object key.</span><span class="sxs-lookup"><span data-stu-id="364d0-1867">Prefix for the S3 object key.</span></span> <span data-ttu-id="364d0-1868">Objects whose keys start with this prefix are selected.</span><span class="sxs-lookup"><span data-stu-id="364d0-1868">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="364d0-1869">Applies only when key is empty.</span><span class="sxs-lookup"><span data-stu-id="364d0-1869">Applies only when key is empty.</span></span> |<span data-ttu-id="364d0-1870">String</span><span class="sxs-lookup"><span data-stu-id="364d0-1870">String</span></span> |<span data-ttu-id="364d0-1871">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1871">No</span></span> |
| <span data-ttu-id="364d0-1872">version</span><span class="sxs-lookup"><span data-stu-id="364d0-1872">version</span></span> |<span data-ttu-id="364d0-1873">The version of S3 object if S3 versioning is enabled.</span><span class="sxs-lookup"><span data-stu-id="364d0-1873">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="364d0-1874">String</span><span class="sxs-lookup"><span data-stu-id="364d0-1874">String</span></span> |<span data-ttu-id="364d0-1875">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1875">No</span></span> |
| <span data-ttu-id="364d0-1876">format</span><span class="sxs-lookup"><span data-stu-id="364d0-1876">format</span></span> | <span data-ttu-id="364d0-1877">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1877">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="364d0-1878">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="364d0-1878">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="364d0-1879">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-1879">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="364d0-1880">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="364d0-1880">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="364d0-1881">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1881">No</span></span> | |
| <span data-ttu-id="364d0-1882">compression</span><span class="sxs-lookup"><span data-stu-id="364d0-1882">compression</span></span> | <span data-ttu-id="364d0-1883">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1883">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="364d0-1884">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1884">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="364d0-1885">The supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1885">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="364d0-1886">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="364d0-1886">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="364d0-1887">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1887">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="364d0-1888">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span><span class="sxs-lookup"><span data-stu-id="364d0-1888">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="364d0-1889">Example: Sample dataset with prefix</span><span class="sxs-lookup"><span data-stu-id="364d0-1889">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="364d0-1890">Example: Sample data set (with version)</span><span class="sxs-lookup"><span data-stu-id="364d0-1890">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="364d0-1891">Example: Dynamic paths for S3</span><span class="sxs-lookup"><span data-stu-id="364d0-1891">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="364d0-1892">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-1892">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="364d0-1893">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span><span class="sxs-lookup"><span data-stu-id="364d0-1893">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="364d0-1894">You can do the same for the prefix property of an Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-1894">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="364d0-1895">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span><span class="sxs-lookup"><span data-stu-id="364d0-1895">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="364d0-1896">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="364d0-1896">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="364d0-1897">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1897">File System Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1898">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1898">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="364d0-1899">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1899">Property</span></span> | <span data-ttu-id="364d0-1900">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1900">Description</span></span> | <span data-ttu-id="364d0-1901">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1901">Allowed values</span></span> | <span data-ttu-id="364d0-1902">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1902">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-1903">recursive</span><span class="sxs-lookup"><span data-stu-id="364d0-1903">recursive</span></span> |<span data-ttu-id="364d0-1904">Specifies whether to recursively list S3 objects under the directory.</span><span class="sxs-lookup"><span data-stu-id="364d0-1904">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="364d0-1905">true/false</span><span class="sxs-lookup"><span data-stu-id="364d0-1905">true/false</span></span> |<span data-ttu-id="364d0-1906">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1906">No</span></span> |


#### <a name="example"></a><span data-ttu-id="364d0-1907">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1907">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="364d0-1908">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="364d0-1908">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="364d0-1909">File System</span><span class="sxs-lookup"><span data-stu-id="364d0-1909">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="364d0-1910">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-1910">Linked service</span></span>
<span data-ttu-id="364d0-1911">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-1911">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="364d0-1912">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-1912">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="364d0-1913">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1913">Property</span></span> | <span data-ttu-id="364d0-1914">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1914">Description</span></span> | <span data-ttu-id="364d0-1915">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1915">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1916">type</span><span class="sxs-lookup"><span data-stu-id="364d0-1916">type</span></span> |<span data-ttu-id="364d0-1917">Ensure that the type property is set to **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1917">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="364d0-1918">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1918">Yes</span></span> |
| <span data-ttu-id="364d0-1919">host</span><span class="sxs-lookup"><span data-stu-id="364d0-1919">host</span></span> |<span data-ttu-id="364d0-1920">Specifies the root path of the folder that you want to copy.</span><span class="sxs-lookup"><span data-stu-id="364d0-1920">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="364d0-1921">Use the escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1921">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="364d0-1922">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="364d0-1922">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="364d0-1923">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1923">Yes</span></span> |
| <span data-ttu-id="364d0-1924">userid</span><span class="sxs-lookup"><span data-stu-id="364d0-1924">userid</span></span> |<span data-ttu-id="364d0-1925">Specify the ID of the user who has access to the server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1925">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="364d0-1926">No (if you choose encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="364d0-1926">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="364d0-1927">password</span><span class="sxs-lookup"><span data-stu-id="364d0-1927">password</span></span> |<span data-ttu-id="364d0-1928">Specify the password for the user (userid).</span><span class="sxs-lookup"><span data-stu-id="364d0-1928">Specify the password for the user (userid).</span></span> |<span data-ttu-id="364d0-1929">No (if you choose encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-1929">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="364d0-1930">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-1930">encryptedCredential</span></span> |<span data-ttu-id="364d0-1931">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="364d0-1931">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="364d0-1932">No (if you choose to specify userid and password in plain text)</span><span class="sxs-lookup"><span data-stu-id="364d0-1932">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="364d0-1933">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-1933">gatewayName</span></span> |<span data-ttu-id="364d0-1934">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span><span class="sxs-lookup"><span data-stu-id="364d0-1934">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="364d0-1935">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1935">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="364d0-1936">Sample folder path definitions</span><span class="sxs-lookup"><span data-stu-id="364d0-1936">Sample folder path definitions</span></span> 
| <span data-ttu-id="364d0-1937">Scenario</span><span class="sxs-lookup"><span data-stu-id="364d0-1937">Scenario</span></span> | <span data-ttu-id="364d0-1938">Host in linked service definition</span><span class="sxs-lookup"><span data-stu-id="364d0-1938">Host in linked service definition</span></span> | <span data-ttu-id="364d0-1939">folderPath in dataset definition</span><span class="sxs-lookup"><span data-stu-id="364d0-1939">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1940">Local folder on Data Management Gateway machine:</span><span class="sxs-lookup"><span data-stu-id="364d0-1940">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="364d0-1941">Examples: D:\\\* or D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="364d0-1941">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="364d0-1942">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span><span class="sxs-lookup"><span data-stu-id="364d0-1942">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="364d0-1943">localhost (for earlier versions than Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="364d0-1943">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="364d0-1944">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span><span class="sxs-lookup"><span data-stu-id="364d0-1944">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="364d0-1945">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span><span class="sxs-lookup"><span data-stu-id="364d0-1945">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="364d0-1946">Remote shared folder:</span><span class="sxs-lookup"><span data-stu-id="364d0-1946">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="364d0-1947">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="364d0-1947">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="364d0-1948">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="364d0-1948">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="364d0-1949">.\\\\ or folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="364d0-1949">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="364d0-1950">Example: Using username and password in plain text</span><span class="sxs-lookup"><span data-stu-id="364d0-1950">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="364d0-1951">Example: Using encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="364d0-1951">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="364d0-1952">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="364d0-1952">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-1953">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-1953">Dataset</span></span>
<span data-ttu-id="364d0-1954">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1954">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-1955">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1955">Property</span></span> | <span data-ttu-id="364d0-1956">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1956">Description</span></span> | <span data-ttu-id="364d0-1957">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-1957">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-1958">folderPath</span><span class="sxs-lookup"><span data-stu-id="364d0-1958">folderPath</span></span> |<span data-ttu-id="364d0-1959">Specifies the subpath to the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-1959">Specifies the subpath to the folder.</span></span> <span data-ttu-id="364d0-1960">Use the escape character ‘\’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="364d0-1960">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="364d0-1961">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="364d0-1961">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="364d0-1962">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="364d0-1962">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="364d0-1963">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-1963">Yes</span></span> |
| <span data-ttu-id="364d0-1964">fileName</span><span class="sxs-lookup"><span data-stu-id="364d0-1964">fileName</span></span> |<span data-ttu-id="364d0-1965">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-1965">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="364d0-1966">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-1966">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="364d0-1967">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span><span class="sxs-lookup"><span data-stu-id="364d0-1967">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="364d0-1968">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="364d0-1968">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="364d0-1969">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1969">No</span></span> |
| <span data-ttu-id="364d0-1970">fileFilter</span><span class="sxs-lookup"><span data-stu-id="364d0-1970">fileFilter</span></span> |<span data-ttu-id="364d0-1971">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="364d0-1971">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="364d0-1972">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="364d0-1972">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="364d0-1973">Example 1: "fileFilter": "\*.log"</span><span class="sxs-lookup"><span data-stu-id="364d0-1973">Example 1: "fileFilter": "\*.log"</span></span><br/><span data-ttu-id="364d0-1974">Example 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="364d0-1974">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="364d0-1975">Note that fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-1975">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="364d0-1976">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1976">No</span></span> |
| <span data-ttu-id="364d0-1977">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="364d0-1977">partitionedBy</span></span> |<span data-ttu-id="364d0-1978">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1978">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="364d0-1979">An example is folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1979">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="364d0-1980">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1980">No</span></span> |
| <span data-ttu-id="364d0-1981">format</span><span class="sxs-lookup"><span data-stu-id="364d0-1981">format</span></span> | <span data-ttu-id="364d0-1982">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1982">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="364d0-1983">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="364d0-1983">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="364d0-1984">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-1984">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="364d0-1985">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="364d0-1985">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="364d0-1986">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1986">No</span></span> |
| <span data-ttu-id="364d0-1987">compression</span><span class="sxs-lookup"><span data-stu-id="364d0-1987">compression</span></span> | <span data-ttu-id="364d0-1988">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-1988">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="364d0-1989">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="364d0-1989">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="364d0-1990">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="364d0-1990">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="364d0-1991">No</span><span class="sxs-lookup"><span data-stu-id="364d0-1991">No</span></span> |

> [!NOTE]
> <span data-ttu-id="364d0-1992">You cannot use fileName and fileFilter simultaneously.</span><span class="sxs-lookup"><span data-stu-id="364d0-1992">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="364d0-1993">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-1993">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-1994">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="364d0-1994">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="364d0-1995">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-1995">File System Source in Copy Activity</span></span>
<span data-ttu-id="364d0-1996">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-1996">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-1997">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-1997">Property</span></span> | <span data-ttu-id="364d0-1998">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-1998">Description</span></span> | <span data-ttu-id="364d0-1999">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-1999">Allowed values</span></span> | <span data-ttu-id="364d0-2000">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2000">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2001">recursive</span><span class="sxs-lookup"><span data-stu-id="364d0-2001">recursive</span></span> |<span data-ttu-id="364d0-2002">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2002">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="364d0-2003">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="364d0-2003">True, False (default)</span></span> |<span data-ttu-id="364d0-2004">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2004">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2005">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2005">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="364d0-2006">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="364d0-2006">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="364d0-2007">File System Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2007">File System Sink in Copy Activity</span></span>
<span data-ttu-id="364d0-2008">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2008">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="364d0-2009">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2009">Property</span></span> | <span data-ttu-id="364d0-2010">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2010">Description</span></span> | <span data-ttu-id="364d0-2011">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-2011">Allowed values</span></span> | <span data-ttu-id="364d0-2012">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2012">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2013">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="364d0-2013">copyBehavior</span></span> |<span data-ttu-id="364d0-2014">Defines the copy behavior when the source is BlobSource or FileSystem.</span><span class="sxs-lookup"><span data-stu-id="364d0-2014">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="364d0-2015">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2015">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="364d0-2016">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2016">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="364d0-2017">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2017">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="364d0-2018">The target files are created with an autogenerated name.</span><span class="sxs-lookup"><span data-stu-id="364d0-2018">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="364d0-2019">**MergeFiles:** Merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="364d0-2019">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="364d0-2020">If the file name/blob name is specified, the merged file name is the specified name.</span><span class="sxs-lookup"><span data-stu-id="364d0-2020">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="364d0-2021">Otherwise, it is an auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="364d0-2021">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="364d0-2022">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2022">No</span></span> |
<span data-ttu-id="364d0-2023">auto-</span><span class="sxs-lookup"><span data-stu-id="364d0-2023">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="364d0-2024">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2024">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-2025">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="364d0-2025">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="364d0-2026">FTP</span><span class="sxs-lookup"><span data-stu-id="364d0-2026">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-2027">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2027">Linked service</span></span>
<span data-ttu-id="364d0-2028">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2028">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2029">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2029">Property</span></span> | <span data-ttu-id="364d0-2030">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2030">Description</span></span> | <span data-ttu-id="364d0-2031">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2031">Required</span></span> | <span data-ttu-id="364d0-2032">Default</span><span class="sxs-lookup"><span data-stu-id="364d0-2032">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2033">host</span><span class="sxs-lookup"><span data-stu-id="364d0-2033">host</span></span> |<span data-ttu-id="364d0-2034">Name or IP address of the FTP Server</span><span class="sxs-lookup"><span data-stu-id="364d0-2034">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="364d0-2035">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2035">Yes</span></span> |&nbsp; |
| <span data-ttu-id="364d0-2036">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-2036">authenticationType</span></span> |<span data-ttu-id="364d0-2037">Specify authentication type</span><span class="sxs-lookup"><span data-stu-id="364d0-2037">Specify authentication type</span></span> |<span data-ttu-id="364d0-2038">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2038">Yes</span></span> |<span data-ttu-id="364d0-2039">Basic, Anonymous</span><span class="sxs-lookup"><span data-stu-id="364d0-2039">Basic, Anonymous</span></span> |
| <span data-ttu-id="364d0-2040">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2040">username</span></span> |<span data-ttu-id="364d0-2041">User who has access to the FTP server</span><span class="sxs-lookup"><span data-stu-id="364d0-2041">User who has access to the FTP server</span></span> |<span data-ttu-id="364d0-2042">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2042">No</span></span> |&nbsp; |
| <span data-ttu-id="364d0-2043">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2043">password</span></span> |<span data-ttu-id="364d0-2044">Password for the user (username)</span><span class="sxs-lookup"><span data-stu-id="364d0-2044">Password for the user (username)</span></span> |<span data-ttu-id="364d0-2045">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2045">No</span></span> |&nbsp; |
| <span data-ttu-id="364d0-2046">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-2046">encryptedCredential</span></span> |<span data-ttu-id="364d0-2047">Encrypted credential to access the FTP server</span><span class="sxs-lookup"><span data-stu-id="364d0-2047">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="364d0-2048">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2048">No</span></span> |&nbsp; |
| <span data-ttu-id="364d0-2049">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-2049">gatewayName</span></span> |<span data-ttu-id="364d0-2050">Name of the Data Management Gateway to connect to an on-premises FTP server</span><span class="sxs-lookup"><span data-stu-id="364d0-2050">Name of the Data Management Gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="364d0-2051">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2051">No</span></span> |&nbsp; |
| <span data-ttu-id="364d0-2052">port</span><span class="sxs-lookup"><span data-stu-id="364d0-2052">port</span></span> |<span data-ttu-id="364d0-2053">Port on which the FTP server is listening</span><span class="sxs-lookup"><span data-stu-id="364d0-2053">Port on which the FTP server is listening</span></span> |<span data-ttu-id="364d0-2054">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2054">No</span></span> |<span data-ttu-id="364d0-2055">21</span><span class="sxs-lookup"><span data-stu-id="364d0-2055">21</span></span> |
| <span data-ttu-id="364d0-2056">enableSsl</span><span class="sxs-lookup"><span data-stu-id="364d0-2056">enableSsl</span></span> |<span data-ttu-id="364d0-2057">Specify whether to use FTP over SSL/TLS channel</span><span class="sxs-lookup"><span data-stu-id="364d0-2057">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="364d0-2058">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2058">No</span></span> |<span data-ttu-id="364d0-2059">true</span><span class="sxs-lookup"><span data-stu-id="364d0-2059">true</span></span> |
| <span data-ttu-id="364d0-2060">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="364d0-2060">enableServerCertificateValidation</span></span> |<span data-ttu-id="364d0-2061">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span><span class="sxs-lookup"><span data-stu-id="364d0-2061">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="364d0-2062">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2062">No</span></span> |<span data-ttu-id="364d0-2063">true</span><span class="sxs-lookup"><span data-stu-id="364d0-2063">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="364d0-2064">Example: Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2064">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="364d0-2065">Example: Using username and password in plain text for basic authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2065">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="364d0-2066">Example: Using port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="364d0-2066">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="364d0-2067">Example: Using encryptedCredential for authentication and gateway</span><span class="sxs-lookup"><span data-stu-id="364d0-2067">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="364d0-2068">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2068">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-2069">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-2069">Dataset</span></span>
<span data-ttu-id="364d0-2070">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2070">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-2071">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2071">Property</span></span> | <span data-ttu-id="364d0-2072">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2072">Description</span></span> | <span data-ttu-id="364d0-2073">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2073">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2074">folderPath</span><span class="sxs-lookup"><span data-stu-id="364d0-2074">folderPath</span></span> |<span data-ttu-id="364d0-2075">Sub path to the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2075">Sub path to the folder.</span></span> <span data-ttu-id="364d0-2076">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="364d0-2076">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="364d0-2077">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="364d0-2077">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="364d0-2078">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="364d0-2078">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="364d0-2079">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2079">Yes</span></span> 
| <span data-ttu-id="364d0-2080">fileName</span><span class="sxs-lookup"><span data-stu-id="364d0-2080">fileName</span></span> |<span data-ttu-id="364d0-2081">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2081">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="364d0-2082">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2082">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="364d0-2083">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span><span class="sxs-lookup"><span data-stu-id="364d0-2083">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="364d0-2084">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="364d0-2084">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="364d0-2085">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2085">No</span></span> |
| <span data-ttu-id="364d0-2086">fileFilter</span><span class="sxs-lookup"><span data-stu-id="364d0-2086">fileFilter</span></span> |<span data-ttu-id="364d0-2087">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="364d0-2087">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="364d0-2088">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="364d0-2088">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="364d0-2089">Examples 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="364d0-2089">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="364d0-2090">Example 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="364d0-2090">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="364d0-2091">fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-2091">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="364d0-2092">This property is not supported with HDFS.</span><span class="sxs-lookup"><span data-stu-id="364d0-2092">This property is not supported with HDFS.</span></span> |<span data-ttu-id="364d0-2093">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2093">No</span></span> |
| <span data-ttu-id="364d0-2094">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="364d0-2094">partitionedBy</span></span> |<span data-ttu-id="364d0-2095">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2095">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="364d0-2096">For example, folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2096">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="364d0-2097">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2097">No</span></span> |
| <span data-ttu-id="364d0-2098">format</span><span class="sxs-lookup"><span data-stu-id="364d0-2098">format</span></span> | <span data-ttu-id="364d0-2099">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2099">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="364d0-2100">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="364d0-2100">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="364d0-2101">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-2101">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="364d0-2102">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="364d0-2102">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="364d0-2103">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2103">No</span></span> |
| <span data-ttu-id="364d0-2104">compression</span><span class="sxs-lookup"><span data-stu-id="364d0-2104">compression</span></span> | <span data-ttu-id="364d0-2105">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2105">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="364d0-2106">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2106">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="364d0-2107">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="364d0-2107">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="364d0-2108">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2108">No</span></span> |
| <span data-ttu-id="364d0-2109">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="364d0-2109">useBinaryTransfer</span></span> |<span data-ttu-id="364d0-2110">Specify whether use Binary transfer mode.</span><span class="sxs-lookup"><span data-stu-id="364d0-2110">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="364d0-2111">True for binary mode and false ASCII.</span><span class="sxs-lookup"><span data-stu-id="364d0-2111">True for binary mode and false ASCII.</span></span> <span data-ttu-id="364d0-2112">Default value: True.</span><span class="sxs-lookup"><span data-stu-id="364d0-2112">Default value: True.</span></span> <span data-ttu-id="364d0-2113">This property can only be used when associated linked service type is of type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="364d0-2113">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="364d0-2114">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2114">No</span></span> |

> [!NOTE]
> <span data-ttu-id="364d0-2115">filename and fileFilter cannot be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="364d0-2115">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="364d0-2116">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2116">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="364d0-2117">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2117">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="364d0-2118">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2118">File System Source in Copy Activity</span></span>
<span data-ttu-id="364d0-2119">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2119">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-2120">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2120">Property</span></span> | <span data-ttu-id="364d0-2121">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2121">Description</span></span> | <span data-ttu-id="364d0-2122">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-2122">Allowed values</span></span> | <span data-ttu-id="364d0-2123">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2123">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2124">recursive</span><span class="sxs-lookup"><span data-stu-id="364d0-2124">recursive</span></span> |<span data-ttu-id="364d0-2125">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2125">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="364d0-2126">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="364d0-2126">True, False (default)</span></span> |<span data-ttu-id="364d0-2127">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2127">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2128">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2128">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="364d0-2129">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2129">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="364d0-2130">HDFS</span><span class="sxs-lookup"><span data-stu-id="364d0-2130">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-2131">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2131">Linked service</span></span>
<span data-ttu-id="364d0-2132">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2132">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2133">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2133">Property</span></span> | <span data-ttu-id="364d0-2134">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2134">Description</span></span> | <span data-ttu-id="364d0-2135">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2136">type</span><span class="sxs-lookup"><span data-stu-id="364d0-2136">type</span></span> |<span data-ttu-id="364d0-2137">The type property must be set to: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="364d0-2137">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="364d0-2138">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2138">Yes</span></span> |
| <span data-ttu-id="364d0-2139">Url</span><span class="sxs-lookup"><span data-stu-id="364d0-2139">Url</span></span> |<span data-ttu-id="364d0-2140">URL to the HDFS</span><span class="sxs-lookup"><span data-stu-id="364d0-2140">URL to the HDFS</span></span> |<span data-ttu-id="364d0-2141">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2141">Yes</span></span> |
| <span data-ttu-id="364d0-2142">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-2142">authenticationType</span></span> |<span data-ttu-id="364d0-2143">Anonymous, or Windows.</span><span class="sxs-lookup"><span data-stu-id="364d0-2143">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="364d0-2144">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span><span class="sxs-lookup"><span data-stu-id="364d0-2144">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="364d0-2145">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2145">Yes</span></span> |
| <span data-ttu-id="364d0-2146">userName</span><span class="sxs-lookup"><span data-stu-id="364d0-2146">userName</span></span> |<span data-ttu-id="364d0-2147">Username for Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-2147">Username for Windows authentication.</span></span> |<span data-ttu-id="364d0-2148">Yes (for Windows Authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-2148">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="364d0-2149">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2149">password</span></span> |<span data-ttu-id="364d0-2150">Password for Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-2150">Password for Windows authentication.</span></span> |<span data-ttu-id="364d0-2151">Yes (for Windows Authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-2151">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="364d0-2152">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-2152">gatewayName</span></span> |<span data-ttu-id="364d0-2153">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span><span class="sxs-lookup"><span data-stu-id="364d0-2153">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="364d0-2154">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2154">Yes</span></span> |
| <span data-ttu-id="364d0-2155">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-2155">encryptedCredential</span></span> |<span data-ttu-id="364d0-2156">[New-AzureRMDataFactoryEncryptValue](https://docs.microsoft.com/powershell/module/azurerm.datafactories/new-azurermdatafactoryencryptvalue) output of the access credential.</span><span class="sxs-lookup"><span data-stu-id="364d0-2156">[New-AzureRMDataFactoryEncryptValue](https://docs.microsoft.com/powershell/module/azurerm.datafactories/new-azurermdatafactoryencryptvalue) output of the access credential.</span></span> |<span data-ttu-id="364d0-2157">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2157">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="364d0-2158">Example: Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2158">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="364d0-2159">Example: Using Windows authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2159">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="364d0-2160">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2160">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-2161">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-2161">Dataset</span></span>
<span data-ttu-id="364d0-2162">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2162">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-2163">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2163">Property</span></span> | <span data-ttu-id="364d0-2164">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2164">Description</span></span> | <span data-ttu-id="364d0-2165">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2166">folderPath</span><span class="sxs-lookup"><span data-stu-id="364d0-2166">folderPath</span></span> |<span data-ttu-id="364d0-2167">Path to the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2167">Path to the folder.</span></span> <span data-ttu-id="364d0-2168">Example: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="364d0-2168">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="364d0-2169">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="364d0-2169">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="364d0-2170">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2170">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="364d0-2171">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="364d0-2171">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="364d0-2172">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2172">Yes</span></span> |
| <span data-ttu-id="364d0-2173">fileName</span><span class="sxs-lookup"><span data-stu-id="364d0-2173">fileName</span></span> |<span data-ttu-id="364d0-2174">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2174">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="364d0-2175">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2175">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="364d0-2176">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span><span class="sxs-lookup"><span data-stu-id="364d0-2176">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="364d0-2177">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="364d0-2177">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="364d0-2178">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2178">No</span></span> |
| <span data-ttu-id="364d0-2179">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="364d0-2179">partitionedBy</span></span> |<span data-ttu-id="364d0-2180">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2180">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="364d0-2181">Example: folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2181">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="364d0-2182">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2182">No</span></span> |
| <span data-ttu-id="364d0-2183">format</span><span class="sxs-lookup"><span data-stu-id="364d0-2183">format</span></span> | <span data-ttu-id="364d0-2184">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2184">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="364d0-2185">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="364d0-2185">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="364d0-2186">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-2186">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="364d0-2187">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="364d0-2187">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="364d0-2188">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2188">No</span></span> |
| <span data-ttu-id="364d0-2189">compression</span><span class="sxs-lookup"><span data-stu-id="364d0-2189">compression</span></span> | <span data-ttu-id="364d0-2190">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2190">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="364d0-2191">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2191">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="364d0-2192">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2192">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="364d0-2193">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="364d0-2193">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="364d0-2194">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2194">No</span></span> |

> [!NOTE]
> <span data-ttu-id="364d0-2195">filename and fileFilter cannot be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="364d0-2195">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="364d0-2196">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2196">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="364d0-2197">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2197">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="364d0-2198">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2198">File System Source in Copy Activity</span></span>
<span data-ttu-id="364d0-2199">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2199">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="364d0-2200">**FileSystemSource** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="364d0-2200">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="364d0-2201">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2201">Property</span></span> | <span data-ttu-id="364d0-2202">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2202">Description</span></span> | <span data-ttu-id="364d0-2203">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-2203">Allowed values</span></span> | <span data-ttu-id="364d0-2204">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2205">recursive</span><span class="sxs-lookup"><span data-stu-id="364d0-2205">recursive</span></span> |<span data-ttu-id="364d0-2206">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2206">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="364d0-2207">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="364d0-2207">True, False (default)</span></span> |<span data-ttu-id="364d0-2208">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2208">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2209">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2209">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="364d0-2210">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2210">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="364d0-2211">SFTP</span><span class="sxs-lookup"><span data-stu-id="364d0-2211">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="364d0-2212">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2212">Linked service</span></span>
<span data-ttu-id="364d0-2213">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2213">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2214">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2214">Property</span></span> | <span data-ttu-id="364d0-2215">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2215">Description</span></span> | <span data-ttu-id="364d0-2216">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2216">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2217">host</span><span class="sxs-lookup"><span data-stu-id="364d0-2217">host</span></span> | <span data-ttu-id="364d0-2218">Name or IP address of the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2218">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="364d0-2219">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2219">Yes</span></span> |
| <span data-ttu-id="364d0-2220">port</span><span class="sxs-lookup"><span data-stu-id="364d0-2220">port</span></span> |<span data-ttu-id="364d0-2221">Port on which the SFTP server is listening.</span><span class="sxs-lookup"><span data-stu-id="364d0-2221">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="364d0-2222">The default value is: 21</span><span class="sxs-lookup"><span data-stu-id="364d0-2222">The default value is: 21</span></span> |<span data-ttu-id="364d0-2223">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2223">No</span></span> |
| <span data-ttu-id="364d0-2224">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-2224">authenticationType</span></span> |<span data-ttu-id="364d0-2225">Specify authentication type.</span><span class="sxs-lookup"><span data-stu-id="364d0-2225">Specify authentication type.</span></span> <span data-ttu-id="364d0-2226">Allowed values: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2226">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="364d0-2227">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span><span class="sxs-lookup"><span data-stu-id="364d0-2227">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="364d0-2228">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2228">Yes</span></span> |
| <span data-ttu-id="364d0-2229">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="364d0-2229">skipHostKeyValidation</span></span> | <span data-ttu-id="364d0-2230">Specify whether to skip host key validation.</span><span class="sxs-lookup"><span data-stu-id="364d0-2230">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="364d0-2231">No.</span><span class="sxs-lookup"><span data-stu-id="364d0-2231">No.</span></span> <span data-ttu-id="364d0-2232">The default value: false</span><span class="sxs-lookup"><span data-stu-id="364d0-2232">The default value: false</span></span> |
| <span data-ttu-id="364d0-2233">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="364d0-2233">hostKeyFingerprint</span></span> | <span data-ttu-id="364d0-2234">Specify the finger print of the host key.</span><span class="sxs-lookup"><span data-stu-id="364d0-2234">Specify the finger print of the host key.</span></span> | <span data-ttu-id="364d0-2235">Yes if the `skipHostKeyValidation` is set to false.</span><span class="sxs-lookup"><span data-stu-id="364d0-2235">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="364d0-2236">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-2236">gatewayName</span></span> |<span data-ttu-id="364d0-2237">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2237">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="364d0-2238">Yes if copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2238">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="364d0-2239">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-2239">encryptedCredential</span></span> | <span data-ttu-id="364d0-2240">Encrypted credential to access the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2240">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="364d0-2241">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span><span class="sxs-lookup"><span data-stu-id="364d0-2241">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="364d0-2242">No.</span><span class="sxs-lookup"><span data-stu-id="364d0-2242">No.</span></span> <span data-ttu-id="364d0-2243">Apply only when copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2243">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="364d0-2244">Example: Using basic authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2244">Example: Using basic authentication</span></span>

<span data-ttu-id="364d0-2245">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2245">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="364d0-2246">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2246">Property</span></span> | <span data-ttu-id="364d0-2247">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2247">Description</span></span> | <span data-ttu-id="364d0-2248">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2248">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2249">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2249">username</span></span> | <span data-ttu-id="364d0-2250">User who has access to the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2250">User who has access to the SFTP server.</span></span> |<span data-ttu-id="364d0-2251">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2251">Yes</span></span> |
| <span data-ttu-id="364d0-2252">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2252">password</span></span> | <span data-ttu-id="364d0-2253">Password for the user (username).</span><span class="sxs-lookup"><span data-stu-id="364d0-2253">Password for the user (username).</span></span> | <span data-ttu-id="364d0-2254">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2254">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="364d0-2255">Example: **Basic authentication with encrypted credential**</span><span class="sxs-lookup"><span data-stu-id="364d0-2255">Example: **Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="364d0-2256">**Using SSH public key authentication:**</span><span class="sxs-lookup"><span data-stu-id="364d0-2256">**Using SSH public key authentication:**</span></span>

<span data-ttu-id="364d0-2257">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2257">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="364d0-2258">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2258">Property</span></span> | <span data-ttu-id="364d0-2259">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2259">Description</span></span> | <span data-ttu-id="364d0-2260">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2260">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2261">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2261">username</span></span> |<span data-ttu-id="364d0-2262">User who has access to the SFTP server</span><span class="sxs-lookup"><span data-stu-id="364d0-2262">User who has access to the SFTP server</span></span> |<span data-ttu-id="364d0-2263">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2263">Yes</span></span> |
| <span data-ttu-id="364d0-2264">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="364d0-2264">privateKeyPath</span></span> | <span data-ttu-id="364d0-2265">Specify absolute path to the private key file that gateway can access.</span><span class="sxs-lookup"><span data-stu-id="364d0-2265">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="364d0-2266">Specify either the `privateKeyPath` or `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="364d0-2266">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="364d0-2267">Apply only when copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2267">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="364d0-2268">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="364d0-2268">privateKeyContent</span></span> | <span data-ttu-id="364d0-2269">A serialized string of the private key content.</span><span class="sxs-lookup"><span data-stu-id="364d0-2269">A serialized string of the private key content.</span></span> <span data-ttu-id="364d0-2270">The Copy Wizard can read the private key file and extract the private key content automatically.</span><span class="sxs-lookup"><span data-stu-id="364d0-2270">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="364d0-2271">If you are using any other tool/SDK, use the privateKeyPath property instead.</span><span class="sxs-lookup"><span data-stu-id="364d0-2271">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="364d0-2272">Specify either the `privateKeyPath` or `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="364d0-2272">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="364d0-2273">passPhrase</span><span class="sxs-lookup"><span data-stu-id="364d0-2273">passPhrase</span></span> | <span data-ttu-id="364d0-2274">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span><span class="sxs-lookup"><span data-stu-id="364d0-2274">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="364d0-2275">Yes if the private key file is protected by a pass phrase.</span><span class="sxs-lookup"><span data-stu-id="364d0-2275">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="364d0-2276">Example: **SshPublicKey authentication using private key content**</span><span class="sxs-lookup"><span data-stu-id="364d0-2276">Example: **SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="364d0-2277">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2277">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-2278">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-2278">Dataset</span></span>
<span data-ttu-id="364d0-2279">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2279">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-2280">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2280">Property</span></span> | <span data-ttu-id="364d0-2281">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2281">Description</span></span> | <span data-ttu-id="364d0-2282">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2282">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2283">folderPath</span><span class="sxs-lookup"><span data-stu-id="364d0-2283">folderPath</span></span> |<span data-ttu-id="364d0-2284">Sub path to the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2284">Sub path to the folder.</span></span> <span data-ttu-id="364d0-2285">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="364d0-2285">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="364d0-2286">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="364d0-2286">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="364d0-2287">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="364d0-2287">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="364d0-2288">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2288">Yes</span></span> |
| <span data-ttu-id="364d0-2289">fileName</span><span class="sxs-lookup"><span data-stu-id="364d0-2289">fileName</span></span> |<span data-ttu-id="364d0-2290">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2290">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="364d0-2291">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2291">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="364d0-2292">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span><span class="sxs-lookup"><span data-stu-id="364d0-2292">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="364d0-2293">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="364d0-2293">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="364d0-2294">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2294">No</span></span> |
| <span data-ttu-id="364d0-2295">fileFilter</span><span class="sxs-lookup"><span data-stu-id="364d0-2295">fileFilter</span></span> |<span data-ttu-id="364d0-2296">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="364d0-2296">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="364d0-2297">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="364d0-2297">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="364d0-2298">Examples 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="364d0-2298">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="364d0-2299">Example 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="364d0-2299">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="364d0-2300">fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-2300">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="364d0-2301">This property is not supported with HDFS.</span><span class="sxs-lookup"><span data-stu-id="364d0-2301">This property is not supported with HDFS.</span></span> |<span data-ttu-id="364d0-2302">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2302">No</span></span> |
| <span data-ttu-id="364d0-2303">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="364d0-2303">partitionedBy</span></span> |<span data-ttu-id="364d0-2304">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2304">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="364d0-2305">For example, folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2305">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="364d0-2306">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2306">No</span></span> |
| <span data-ttu-id="364d0-2307">format</span><span class="sxs-lookup"><span data-stu-id="364d0-2307">format</span></span> | <span data-ttu-id="364d0-2308">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2308">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="364d0-2309">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="364d0-2309">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="364d0-2310">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-2310">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="364d0-2311">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="364d0-2311">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="364d0-2312">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2312">No</span></span> |
| <span data-ttu-id="364d0-2313">compression</span><span class="sxs-lookup"><span data-stu-id="364d0-2313">compression</span></span> | <span data-ttu-id="364d0-2314">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2314">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="364d0-2315">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2315">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="364d0-2316">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2316">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="364d0-2317">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="364d0-2317">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="364d0-2318">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2318">No</span></span> |
| <span data-ttu-id="364d0-2319">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="364d0-2319">useBinaryTransfer</span></span> |<span data-ttu-id="364d0-2320">Specify whether use Binary transfer mode.</span><span class="sxs-lookup"><span data-stu-id="364d0-2320">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="364d0-2321">True for binary mode and false ASCII.</span><span class="sxs-lookup"><span data-stu-id="364d0-2321">True for binary mode and false ASCII.</span></span> <span data-ttu-id="364d0-2322">Default value: True.</span><span class="sxs-lookup"><span data-stu-id="364d0-2322">Default value: True.</span></span> <span data-ttu-id="364d0-2323">This property can only be used when associated linked service type is of type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="364d0-2323">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="364d0-2324">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2324">No</span></span> |

> [!NOTE]
> <span data-ttu-id="364d0-2325">filename and fileFilter cannot be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="364d0-2325">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="364d0-2326">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2326">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="364d0-2327">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2327">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="364d0-2328">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2328">File System Source in Copy Activity</span></span>
<span data-ttu-id="364d0-2329">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2329">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-2330">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2330">Property</span></span> | <span data-ttu-id="364d0-2331">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2331">Description</span></span> | <span data-ttu-id="364d0-2332">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-2332">Allowed values</span></span> | <span data-ttu-id="364d0-2333">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2333">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2334">recursive</span><span class="sxs-lookup"><span data-stu-id="364d0-2334">recursive</span></span> |<span data-ttu-id="364d0-2335">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="364d0-2335">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="364d0-2336">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="364d0-2336">True, False (default)</span></span> |<span data-ttu-id="364d0-2337">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2337">No</span></span> |



#### <a name="example"></a><span data-ttu-id="364d0-2338">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2338">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="364d0-2339">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2339">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="364d0-2340">HTTP</span><span class="sxs-lookup"><span data-stu-id="364d0-2340">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-2341">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2341">Linked service</span></span>
<span data-ttu-id="364d0-2342">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2342">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2343">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2343">Property</span></span> | <span data-ttu-id="364d0-2344">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2344">Description</span></span> | <span data-ttu-id="364d0-2345">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2345">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2346">url</span><span class="sxs-lookup"><span data-stu-id="364d0-2346">url</span></span> | <span data-ttu-id="364d0-2347">Base URL to the Web Server</span><span class="sxs-lookup"><span data-stu-id="364d0-2347">Base URL to the Web Server</span></span> | <span data-ttu-id="364d0-2348">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2348">Yes</span></span> |
| <span data-ttu-id="364d0-2349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-2349">authenticationType</span></span> | <span data-ttu-id="364d0-2350">Specifies the authentication type.</span><span class="sxs-lookup"><span data-stu-id="364d0-2350">Specifies the authentication type.</span></span> <span data-ttu-id="364d0-2351">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2351">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="364d0-2352">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span><span class="sxs-lookup"><span data-stu-id="364d0-2352">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="364d0-2353">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2353">Yes</span></span> |
| <span data-ttu-id="364d0-2354">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="364d0-2354">enableServerCertificateValidation</span></span> | <span data-ttu-id="364d0-2355">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span><span class="sxs-lookup"><span data-stu-id="364d0-2355">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="364d0-2356">No, default is true</span><span class="sxs-lookup"><span data-stu-id="364d0-2356">No, default is true</span></span> |
| <span data-ttu-id="364d0-2357">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-2357">gatewayName</span></span> | <span data-ttu-id="364d0-2358">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="364d0-2358">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="364d0-2359">Yes if copying data from an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="364d0-2359">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="364d0-2360">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-2360">encryptedCredential</span></span> | <span data-ttu-id="364d0-2361">Encrypted credential to access the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="364d0-2361">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="364d0-2362">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span><span class="sxs-lookup"><span data-stu-id="364d0-2362">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="364d0-2363">No.</span><span class="sxs-lookup"><span data-stu-id="364d0-2363">No.</span></span> <span data-ttu-id="364d0-2364">Apply only when copying data from an on-premises HTTP server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2364">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="364d0-2365">Example: Using Basic, Digest, or Windows authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2365">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="364d0-2366">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span><span class="sxs-lookup"><span data-stu-id="364d0-2366">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="364d0-2367">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2367">Property</span></span> | <span data-ttu-id="364d0-2368">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2368">Description</span></span> | <span data-ttu-id="364d0-2369">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2369">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2370">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2370">username</span></span> | <span data-ttu-id="364d0-2371">Username to access the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="364d0-2371">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="364d0-2372">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2372">Yes</span></span> |
| <span data-ttu-id="364d0-2373">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2373">password</span></span> | <span data-ttu-id="364d0-2374">Password for the user (username).</span><span class="sxs-lookup"><span data-stu-id="364d0-2374">Password for the user (username).</span></span> | <span data-ttu-id="364d0-2375">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2375">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="364d0-2376">Example: Using ClientCertificate authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2376">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="364d0-2377">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span><span class="sxs-lookup"><span data-stu-id="364d0-2377">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="364d0-2378">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2378">Property</span></span> | <span data-ttu-id="364d0-2379">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2379">Description</span></span> | <span data-ttu-id="364d0-2380">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2380">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2381">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="364d0-2381">embeddedCertData</span></span> | <span data-ttu-id="364d0-2382">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span><span class="sxs-lookup"><span data-stu-id="364d0-2382">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="364d0-2383">Specify either the `embeddedCertData` or `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="364d0-2383">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="364d0-2384">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="364d0-2384">certThumbprint</span></span> | <span data-ttu-id="364d0-2385">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span><span class="sxs-lookup"><span data-stu-id="364d0-2385">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="364d0-2386">Apply only when copying data from an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="364d0-2386">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="364d0-2387">Specify either the `embeddedCertData` or `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="364d0-2387">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="364d0-2388">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2388">password</span></span> | <span data-ttu-id="364d0-2389">Password associated with the certificate.</span><span class="sxs-lookup"><span data-stu-id="364d0-2389">Password associated with the certificate.</span></span> | <span data-ttu-id="364d0-2390">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2390">No</span></span> |

<span data-ttu-id="364d0-2391">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span><span class="sxs-lookup"><span data-stu-id="364d0-2391">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="364d0-2392">Launch Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="364d0-2392">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="364d0-2393">Add the **Certificates** snap-in that targets the **Local Computer**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2393">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="364d0-2394">Expand **Certificates**, **Personal**, and click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2394">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="364d0-2395">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span><span class="sxs-lookup"><span data-stu-id="364d0-2395">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="364d0-2396">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span><span class="sxs-lookup"><span data-stu-id="364d0-2396">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="364d0-2397">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2397">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="364d0-2398">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span><span class="sxs-lookup"><span data-stu-id="364d0-2398">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="364d0-2399">Example: using client certificate in a file</span><span class="sxs-lookup"><span data-stu-id="364d0-2399">Example: using client certificate in a file</span></span>
<span data-ttu-id="364d0-2400">This linked service links your data factory to an on-premises HTTP web server.</span><span class="sxs-lookup"><span data-stu-id="364d0-2400">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="364d0-2401">It uses a client certificate file on the machine with Data Management Gateway installed.</span><span class="sxs-lookup"><span data-stu-id="364d0-2401">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="364d0-2402">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2402">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-2403">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-2403">Dataset</span></span>
<span data-ttu-id="364d0-2404">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2404">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-2405">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2405">Property</span></span> | <span data-ttu-id="364d0-2406">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2406">Description</span></span> | <span data-ttu-id="364d0-2407">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2407">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-2408">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="364d0-2408">relativeUrl</span></span> | <span data-ttu-id="364d0-2409">A relative URL to the resource that contains the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2409">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="364d0-2410">When path is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="364d0-2410">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="364d0-2411">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="364d0-2411">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="364d0-2412">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2412">No</span></span> |
| <span data-ttu-id="364d0-2413">requestMethod</span><span class="sxs-lookup"><span data-stu-id="364d0-2413">requestMethod</span></span> | <span data-ttu-id="364d0-2414">Http method.</span><span class="sxs-lookup"><span data-stu-id="364d0-2414">Http method.</span></span> <span data-ttu-id="364d0-2415">Allowed values are **GET** or **POST**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2415">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="364d0-2416">No.</span><span class="sxs-lookup"><span data-stu-id="364d0-2416">No.</span></span> <span data-ttu-id="364d0-2417">Default is `GET`.</span><span class="sxs-lookup"><span data-stu-id="364d0-2417">Default is `GET`.</span></span> |
| <span data-ttu-id="364d0-2418">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="364d0-2418">additionalHeaders</span></span> | <span data-ttu-id="364d0-2419">Additional HTTP request headers.</span><span class="sxs-lookup"><span data-stu-id="364d0-2419">Additional HTTP request headers.</span></span> | <span data-ttu-id="364d0-2420">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2420">No</span></span> |
| <span data-ttu-id="364d0-2421">requestBody</span><span class="sxs-lookup"><span data-stu-id="364d0-2421">requestBody</span></span> | <span data-ttu-id="364d0-2422">Body for HTTP request.</span><span class="sxs-lookup"><span data-stu-id="364d0-2422">Body for HTTP request.</span></span> | <span data-ttu-id="364d0-2423">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2423">No</span></span> |
| <span data-ttu-id="364d0-2424">format</span><span class="sxs-lookup"><span data-stu-id="364d0-2424">format</span></span> | <span data-ttu-id="364d0-2425">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span><span class="sxs-lookup"><span data-stu-id="364d0-2425">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="364d0-2426">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2426">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="364d0-2427">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-2427">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="364d0-2428">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2428">No</span></span> |
| <span data-ttu-id="364d0-2429">compression</span><span class="sxs-lookup"><span data-stu-id="364d0-2429">compression</span></span> | <span data-ttu-id="364d0-2430">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2430">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="364d0-2431">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2431">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="364d0-2432">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2432">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="364d0-2433">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="364d0-2433">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="364d0-2434">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2434">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="364d0-2435">Example: using the GET (default) method</span><span class="sxs-lookup"><span data-stu-id="364d0-2435">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="364d0-2436">Example: using the POST method</span><span class="sxs-lookup"><span data-stu-id="364d0-2436">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="364d0-2437">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2437">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="364d0-2438">HTTP Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2438">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="364d0-2439">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2439">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-2440">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2440">Property</span></span> | <span data-ttu-id="364d0-2441">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2441">Description</span></span> | <span data-ttu-id="364d0-2442">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2442">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="364d0-2443">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="364d0-2443">httpRequestTimeout</span></span> | <span data-ttu-id="364d0-2444">The timeout (TimeSpan) for the HTTP request to get a response.</span><span class="sxs-lookup"><span data-stu-id="364d0-2444">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="364d0-2445">It is the timeout to get a response, not the timeout to read response data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2445">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="364d0-2446">No.</span><span class="sxs-lookup"><span data-stu-id="364d0-2446">No.</span></span> <span data-ttu-id="364d0-2447">Default value: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="364d0-2447">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="364d0-2448">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2448">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-2449">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2449">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="364d0-2450">OData</span><span class="sxs-lookup"><span data-stu-id="364d0-2450">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-2451">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2451">Linked service</span></span>
<span data-ttu-id="364d0-2452">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2452">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2453">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2453">Property</span></span> | <span data-ttu-id="364d0-2454">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2454">Description</span></span> | <span data-ttu-id="364d0-2455">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2455">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2456">url</span><span class="sxs-lookup"><span data-stu-id="364d0-2456">url</span></span> |<span data-ttu-id="364d0-2457">Url of the OData service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2457">Url of the OData service.</span></span> |<span data-ttu-id="364d0-2458">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2458">Yes</span></span> |
| <span data-ttu-id="364d0-2459">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-2459">authenticationType</span></span> |<span data-ttu-id="364d0-2460">Type of authentication used to connect to the OData source.</span><span class="sxs-lookup"><span data-stu-id="364d0-2460">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="364d0-2461">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span><span class="sxs-lookup"><span data-stu-id="364d0-2461">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="364d0-2462">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="364d0-2462">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="364d0-2463">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2463">Yes</span></span> |
| <span data-ttu-id="364d0-2464">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2464">username</span></span> |<span data-ttu-id="364d0-2465">Specify user name if you are using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-2465">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="364d0-2466">Yes (only if you are using Basic authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-2466">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="364d0-2467">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2467">password</span></span> |<span data-ttu-id="364d0-2468">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="364d0-2468">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="364d0-2469">Yes (only if you are using Basic authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-2469">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="364d0-2470">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="364d0-2470">authorizedCredential</span></span> |<span data-ttu-id="364d0-2471">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span><span class="sxs-lookup"><span data-stu-id="364d0-2471">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="364d0-2472">Yes (only if you are using OAuth authentication)</span><span class="sxs-lookup"><span data-stu-id="364d0-2472">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="364d0-2473">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-2473">gatewayName</span></span> |<span data-ttu-id="364d0-2474">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2474">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="364d0-2475">Specify only if you are copying data from on-prem OData source.</span><span class="sxs-lookup"><span data-stu-id="364d0-2475">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="364d0-2476">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2476">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="364d0-2477">Example - Using Basic authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2477">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="364d0-2478">Example - Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2478">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="364d0-2479">Example - Using Windows authentication accessing on-premises OData source</span><span class="sxs-lookup"><span data-stu-id="364d0-2479">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="364d0-2480">Example - Using OAuth authentication accessing cloud OData source</span><span class="sxs-lookup"><span data-stu-id="364d0-2480">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="364d0-2481">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2481">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="364d0-2482">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-2482">Dataset</span></span>
<span data-ttu-id="364d0-2483">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2483">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-2484">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2484">Property</span></span> | <span data-ttu-id="364d0-2485">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2485">Description</span></span> | <span data-ttu-id="364d0-2486">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2486">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2487">path</span><span class="sxs-lookup"><span data-stu-id="364d0-2487">path</span></span> |<span data-ttu-id="364d0-2488">Path to the OData resource</span><span class="sxs-lookup"><span data-stu-id="364d0-2488">Path to the OData resource</span></span> |<span data-ttu-id="364d0-2489">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2489">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2490">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2490">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="364d0-2491">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2491">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-2492">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2492">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-2493">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2493">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-2494">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2494">Property</span></span> | <span data-ttu-id="364d0-2495">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2495">Description</span></span> | <span data-ttu-id="364d0-2496">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2496">Example</span></span> | <span data-ttu-id="364d0-2497">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2497">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2498">query</span><span class="sxs-lookup"><span data-stu-id="364d0-2498">query</span></span> |<span data-ttu-id="364d0-2499">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2499">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-2500">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="364d0-2500">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="364d0-2501">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2501">No</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2502">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2502">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="364d0-2503">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2503">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="364d0-2504">ODBC</span><span class="sxs-lookup"><span data-stu-id="364d0-2504">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="364d0-2505">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2505">Linked service</span></span>
<span data-ttu-id="364d0-2506">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2506">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2507">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2507">Property</span></span> | <span data-ttu-id="364d0-2508">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2508">Description</span></span> | <span data-ttu-id="364d0-2509">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2509">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2510">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-2510">connectionString</span></span> |<span data-ttu-id="364d0-2511">The non-access credential portion of the connection string and an optional encrypted credential.</span><span class="sxs-lookup"><span data-stu-id="364d0-2511">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="364d0-2512">See examples in the following sections.</span><span class="sxs-lookup"><span data-stu-id="364d0-2512">See examples in the following sections.</span></span> |<span data-ttu-id="364d0-2513">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2513">Yes</span></span> |
| <span data-ttu-id="364d0-2514">credential</span><span class="sxs-lookup"><span data-stu-id="364d0-2514">credential</span></span> |<span data-ttu-id="364d0-2515">The access credential portion of the connection string specified in driver-specific property-value format.</span><span class="sxs-lookup"><span data-stu-id="364d0-2515">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="364d0-2516">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="364d0-2516">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="364d0-2517">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2517">No</span></span> |
| <span data-ttu-id="364d0-2518">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-2518">authenticationType</span></span> |<span data-ttu-id="364d0-2519">Type of authentication used to connect to the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="364d0-2519">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="364d0-2520">Possible values are: Anonymous and Basic.</span><span class="sxs-lookup"><span data-stu-id="364d0-2520">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="364d0-2521">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2521">Yes</span></span> |
| <span data-ttu-id="364d0-2522">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2522">username</span></span> |<span data-ttu-id="364d0-2523">Specify user name if you are using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-2523">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="364d0-2524">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2524">No</span></span> |
| <span data-ttu-id="364d0-2525">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2525">password</span></span> |<span data-ttu-id="364d0-2526">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="364d0-2526">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="364d0-2527">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2527">No</span></span> |
| <span data-ttu-id="364d0-2528">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-2528">gatewayName</span></span> |<span data-ttu-id="364d0-2529">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="364d0-2529">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="364d0-2530">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2530">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="364d0-2531">Example - Using Basic authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2531">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="364d0-2532">Example - Using Basic authentication with encrypted credentials</span><span class="sxs-lookup"><span data-stu-id="364d0-2532">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="364d0-2533">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://docs.microsoft.com/powershell/module/azurerm.datafactories/new-azurermdatafactoryencryptvalue) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="364d0-2533">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://docs.microsoft.com/powershell/module/azurerm.datafactories/new-azurermdatafactoryencryptvalue) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="364d0-2534">Example: Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2534">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="364d0-2535">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2535">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-2536">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-2536">Dataset</span></span>
<span data-ttu-id="364d0-2537">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2537">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-2538">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2538">Property</span></span> | <span data-ttu-id="364d0-2539">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2539">Description</span></span> | <span data-ttu-id="364d0-2540">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2540">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2541">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-2541">tableName</span></span> |<span data-ttu-id="364d0-2542">Name of the table in the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="364d0-2542">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="364d0-2543">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2543">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="364d0-2544">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2544">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-2545">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2545">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-2546">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2546">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-2547">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2547">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-2548">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2548">Property</span></span> | <span data-ttu-id="364d0-2549">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2549">Description</span></span> | <span data-ttu-id="364d0-2550">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-2550">Allowed values</span></span> | <span data-ttu-id="364d0-2551">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2551">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2552">query</span><span class="sxs-lookup"><span data-stu-id="364d0-2552">query</span></span> |<span data-ttu-id="364d0-2553">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2553">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-2554">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="364d0-2554">SQL query string.</span></span> <span data-ttu-id="364d0-2555">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="364d0-2555">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="364d0-2556">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2556">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2557">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2557">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="364d0-2558">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2558">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="364d0-2559">Salesforce</span><span class="sxs-lookup"><span data-stu-id="364d0-2559">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="364d0-2560">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2560">Linked service</span></span>
<span data-ttu-id="364d0-2561">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2561">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2562">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2562">Property</span></span> | <span data-ttu-id="364d0-2563">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2563">Description</span></span> | <span data-ttu-id="364d0-2564">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2564">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2565">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="364d0-2565">environmentUrl</span></span> | <span data-ttu-id="364d0-2566">Specify the URL of Salesforce instance.</span><span class="sxs-lookup"><span data-stu-id="364d0-2566">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="364d0-2567">- Default is "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="364d0-2567">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="364d0-2568">- To copy data from sandbox, specify "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="364d0-2568">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="364d0-2569">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="364d0-2569">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="364d0-2570">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2570">No</span></span> |
| <span data-ttu-id="364d0-2571">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2571">username</span></span> |<span data-ttu-id="364d0-2572">Specify a user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="364d0-2572">Specify a user name for the user account.</span></span> |<span data-ttu-id="364d0-2573">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2573">Yes</span></span> |
| <span data-ttu-id="364d0-2574">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2574">password</span></span> |<span data-ttu-id="364d0-2575">Specify a password for the user account.</span><span class="sxs-lookup"><span data-stu-id="364d0-2575">Specify a password for the user account.</span></span> |<span data-ttu-id="364d0-2576">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2576">Yes</span></span> |
| <span data-ttu-id="364d0-2577">securityToken</span><span class="sxs-lookup"><span data-stu-id="364d0-2577">securityToken</span></span> |<span data-ttu-id="364d0-2578">Specify a security token for the user account.</span><span class="sxs-lookup"><span data-stu-id="364d0-2578">Specify a security token for the user account.</span></span> <span data-ttu-id="364d0-2579">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span><span class="sxs-lookup"><span data-stu-id="364d0-2579">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="364d0-2580">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="364d0-2580">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="364d0-2581">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2581">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2582">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2582">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="364d0-2583">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2583">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-2584">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-2584">Dataset</span></span>
<span data-ttu-id="364d0-2585">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2585">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-2586">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2586">Property</span></span> | <span data-ttu-id="364d0-2587">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2587">Description</span></span> | <span data-ttu-id="364d0-2588">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2588">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2589">tableName</span><span class="sxs-lookup"><span data-stu-id="364d0-2589">tableName</span></span> |<span data-ttu-id="364d0-2590">Name of the table in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="364d0-2590">Name of the table in Salesforce.</span></span> |<span data-ttu-id="364d0-2591">No (if a **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-2591">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2592">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2592">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="364d0-2593">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2593">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="364d0-2594">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2594">Relational Source in Copy Activity</span></span>
<span data-ttu-id="364d0-2595">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2595">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="364d0-2596">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2596">Property</span></span> | <span data-ttu-id="364d0-2597">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2597">Description</span></span> | <span data-ttu-id="364d0-2598">Allowed values</span><span class="sxs-lookup"><span data-stu-id="364d0-2598">Allowed values</span></span> | <span data-ttu-id="364d0-2599">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2599">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="364d0-2600">query</span><span class="sxs-lookup"><span data-stu-id="364d0-2600">query</span></span> |<span data-ttu-id="364d0-2601">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2601">Use the custom query to read data.</span></span> |<span data-ttu-id="364d0-2602">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span><span class="sxs-lookup"><span data-stu-id="364d0-2602">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="364d0-2603">For example:  `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="364d0-2603">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="364d0-2604">No (if the **tableName** of the **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="364d0-2604">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2605">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2605">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="364d0-2606">The "__c" part of the API Name is needed for any custom object.</span><span class="sxs-lookup"><span data-stu-id="364d0-2606">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="364d0-2607">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2607">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="364d0-2608">Web Data</span><span class="sxs-lookup"><span data-stu-id="364d0-2608">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-2609">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2609">Linked service</span></span>
<span data-ttu-id="364d0-2610">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2610">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2611">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2611">Property</span></span> | <span data-ttu-id="364d0-2612">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2612">Description</span></span> | <span data-ttu-id="364d0-2613">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2613">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2614">Url</span><span class="sxs-lookup"><span data-stu-id="364d0-2614">Url</span></span> |<span data-ttu-id="364d0-2615">URL to the Web source</span><span class="sxs-lookup"><span data-stu-id="364d0-2615">URL to the Web source</span></span> |<span data-ttu-id="364d0-2616">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2616">Yes</span></span> |
| <span data-ttu-id="364d0-2617">authenticationType</span><span class="sxs-lookup"><span data-stu-id="364d0-2617">authenticationType</span></span> |<span data-ttu-id="364d0-2618">Anonymous.</span><span class="sxs-lookup"><span data-stu-id="364d0-2618">Anonymous.</span></span> |<span data-ttu-id="364d0-2619">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2619">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="364d0-2620">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2620">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="364d0-2621">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2621">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="364d0-2622">Dataset</span><span class="sxs-lookup"><span data-stu-id="364d0-2622">Dataset</span></span>
<span data-ttu-id="364d0-2623">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2623">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="364d0-2624">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2624">Property</span></span> | <span data-ttu-id="364d0-2625">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2625">Description</span></span> | <span data-ttu-id="364d0-2626">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2626">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-2627">type</span><span class="sxs-lookup"><span data-stu-id="364d0-2627">type</span></span> |<span data-ttu-id="364d0-2628">type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-2628">type of the dataset.</span></span> <span data-ttu-id="364d0-2629">must be set to **WebTable**</span><span class="sxs-lookup"><span data-stu-id="364d0-2629">must be set to **WebTable**</span></span> |<span data-ttu-id="364d0-2630">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2630">Yes</span></span> |
| <span data-ttu-id="364d0-2631">path</span><span class="sxs-lookup"><span data-stu-id="364d0-2631">path</span></span> |<span data-ttu-id="364d0-2632">A relative URL to the resource that contains the table.</span><span class="sxs-lookup"><span data-stu-id="364d0-2632">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="364d0-2633">No.</span><span class="sxs-lookup"><span data-stu-id="364d0-2633">No.</span></span> <span data-ttu-id="364d0-2634">When path is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="364d0-2634">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="364d0-2635">index</span><span class="sxs-lookup"><span data-stu-id="364d0-2635">index</span></span> |<span data-ttu-id="364d0-2636">The index of the table in the resource.</span><span class="sxs-lookup"><span data-stu-id="364d0-2636">The index of the table in the resource.</span></span> <span data-ttu-id="364d0-2637">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span><span class="sxs-lookup"><span data-stu-id="364d0-2637">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="364d0-2638">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2638">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="364d0-2639">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2639">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="364d0-2640">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2640">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="364d0-2641">Web Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2641">Web Source in Copy Activity</span></span>
<span data-ttu-id="364d0-2642">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2642">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="364d0-2643">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span><span class="sxs-lookup"><span data-stu-id="364d0-2643">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="364d0-2644">Example</span><span class="sxs-lookup"><span data-stu-id="364d0-2644">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="364d0-2645">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2645">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="364d0-2646">COMPUTE ENVIRONMENTS</span><span class="sxs-lookup"><span data-stu-id="364d0-2646">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="364d0-2647">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span><span class="sxs-lookup"><span data-stu-id="364d0-2647">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="364d0-2648">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-2648">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="364d0-2649">Compute environment</span><span class="sxs-lookup"><span data-stu-id="364d0-2649">Compute environment</span></span> | <span data-ttu-id="364d0-2650">Activities</span><span class="sxs-lookup"><span data-stu-id="364d0-2650">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="364d0-2651">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="364d0-2651">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="364d0-2652">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity), [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="364d0-2652">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity), [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="364d0-2653">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="364d0-2653">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="364d0-2654">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2654">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="364d0-2655">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="364d0-2655">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="364d0-2656">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="364d0-2656">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="364d0-2657">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="364d0-2657">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="364d0-2658">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="364d0-2658">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="364d0-2659">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="364d0-2659">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="364d0-2660">Stored Procedure</span><span class="sxs-lookup"><span data-stu-id="364d0-2660">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="364d0-2661">On-demand Azure HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="364d0-2661">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="364d0-2662">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2662">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="364d0-2663">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2663">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="364d0-2664">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity), [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="364d0-2664">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity), [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-2665">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2665">Linked service</span></span> 
<span data-ttu-id="364d0-2666">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2666">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="364d0-2667">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2667">Property</span></span> | <span data-ttu-id="364d0-2668">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2668">Description</span></span> | <span data-ttu-id="364d0-2669">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2669">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2670">type</span><span class="sxs-lookup"><span data-stu-id="364d0-2670">type</span></span> |<span data-ttu-id="364d0-2671">The type property should be set to **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2671">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="364d0-2672">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2672">Yes</span></span> |
| <span data-ttu-id="364d0-2673">clusterSize</span><span class="sxs-lookup"><span data-stu-id="364d0-2673">clusterSize</span></span> |<span data-ttu-id="364d0-2674">Number of worker/data nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2674">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="364d0-2675">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2675">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="364d0-2676">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span><span class="sxs-lookup"><span data-stu-id="364d0-2676">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="364d0-2677">See [Create Linux-based Hadoop clusters in HDInsight](../../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span><span class="sxs-lookup"><span data-stu-id="364d0-2677">See [Create Linux-based Hadoop clusters in HDInsight](../../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="364d0-2678">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2678">Yes</span></span> |
| <span data-ttu-id="364d0-2679">timetolive</span><span class="sxs-lookup"><span data-stu-id="364d0-2679">timetolive</span></span> |<span data-ttu-id="364d0-2680">The allowed idle time for the on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2680">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="364d0-2681">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2681">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="364d0-2682">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span><span class="sxs-lookup"><span data-stu-id="364d0-2682">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="364d0-2683">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2683">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="364d0-2684">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2684">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="364d0-2685">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span><span class="sxs-lookup"><span data-stu-id="364d0-2685">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="364d0-2686">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span><span class="sxs-lookup"><span data-stu-id="364d0-2686">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="364d0-2687">Therefore, it is important that you set the appropriate value based on your needs.</span><span class="sxs-lookup"><span data-stu-id="364d0-2687">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="364d0-2688">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span><span class="sxs-lookup"><span data-stu-id="364d0-2688">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="364d0-2689">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2689">Yes</span></span> |
| <span data-ttu-id="364d0-2690">version</span><span class="sxs-lookup"><span data-stu-id="364d0-2690">version</span></span> |<span data-ttu-id="364d0-2691">Version of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2691">Version of the HDInsight cluster.</span></span> <span data-ttu-id="364d0-2692">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="364d0-2692">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="364d0-2693">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2693">No</span></span> |
| <span data-ttu-id="364d0-2694">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="364d0-2694">linkedServiceName</span></span> |<span data-ttu-id="364d0-2695">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span><span class="sxs-lookup"><span data-stu-id="364d0-2695">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="364d0-2696">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span><span class="sxs-lookup"><span data-stu-id="364d0-2696">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="364d0-2697">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="364d0-2697">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="364d0-2698">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2698">Yes</span></span> |
| <span data-ttu-id="364d0-2699">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="364d0-2699">additionalLinkedServiceNames</span></span> |<span data-ttu-id="364d0-2700">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span><span class="sxs-lookup"><span data-stu-id="364d0-2700">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="364d0-2701">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2701">No</span></span> |
| <span data-ttu-id="364d0-2702">osType</span><span class="sxs-lookup"><span data-stu-id="364d0-2702">osType</span></span> |<span data-ttu-id="364d0-2703">Type of operating system.</span><span class="sxs-lookup"><span data-stu-id="364d0-2703">Type of operating system.</span></span> <span data-ttu-id="364d0-2704">Allowed values are: Windows (default) and Linux</span><span class="sxs-lookup"><span data-stu-id="364d0-2704">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="364d0-2705">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2705">No</span></span> |
| <span data-ttu-id="364d0-2706">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="364d0-2706">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="364d0-2707">The name of Azure SQL linked service that point to the HCatalog database.</span><span class="sxs-lookup"><span data-stu-id="364d0-2707">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="364d0-2708">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span><span class="sxs-lookup"><span data-stu-id="364d0-2708">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="364d0-2709">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2709">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="364d0-2710">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2710">JSON example</span></span>
<span data-ttu-id="364d0-2711">The following JSON defines a Linux-based on-demand HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2711">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="364d0-2712">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span><span class="sxs-lookup"><span data-stu-id="364d0-2712">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="364d0-2713">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2713">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="364d0-2714">Existing Azure HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="364d0-2714">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="364d0-2715">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-2715">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="364d0-2716">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity), [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="364d0-2716">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity), [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-2717">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2717">Linked service</span></span>
<span data-ttu-id="364d0-2718">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2718">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="364d0-2719">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2719">Property</span></span> | <span data-ttu-id="364d0-2720">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2720">Description</span></span> | <span data-ttu-id="364d0-2721">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2721">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2722">type</span><span class="sxs-lookup"><span data-stu-id="364d0-2722">type</span></span> |<span data-ttu-id="364d0-2723">The type property should be set to **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2723">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="364d0-2724">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2724">Yes</span></span> |
| <span data-ttu-id="364d0-2725">clusterUri</span><span class="sxs-lookup"><span data-stu-id="364d0-2725">clusterUri</span></span> |<span data-ttu-id="364d0-2726">The URI of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2726">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="364d0-2727">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2727">Yes</span></span> |
| <span data-ttu-id="364d0-2728">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2728">username</span></span> |<span data-ttu-id="364d0-2729">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2729">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="364d0-2730">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2730">Yes</span></span> |
| <span data-ttu-id="364d0-2731">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2731">password</span></span> |<span data-ttu-id="364d0-2732">Specify password for the user account.</span><span class="sxs-lookup"><span data-stu-id="364d0-2732">Specify password for the user account.</span></span> |<span data-ttu-id="364d0-2733">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2733">Yes</span></span> |
| <span data-ttu-id="364d0-2734">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="364d0-2734">linkedServiceName</span></span> | <span data-ttu-id="364d0-2735">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2735">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="364d0-2736">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2736">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="364d0-2737">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="364d0-2737">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="364d0-2738">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2738">Yes</span></span> |

<span data-ttu-id="364d0-2739">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="364d0-2739">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="364d0-2740">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2740">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="364d0-2741">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="364d0-2741">Azure Batch</span></span>
<span data-ttu-id="364d0-2742">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-2742">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="364d0-2743">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="364d0-2743">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="364d0-2744">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2744">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-2745">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2745">Linked service</span></span>
<span data-ttu-id="364d0-2746">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2746">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="364d0-2747">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2747">Property</span></span> | <span data-ttu-id="364d0-2748">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2748">Description</span></span> | <span data-ttu-id="364d0-2749">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2749">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2750">type</span><span class="sxs-lookup"><span data-stu-id="364d0-2750">type</span></span> |<span data-ttu-id="364d0-2751">The type property should be set to **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2751">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="364d0-2752">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2752">Yes</span></span> |
| <span data-ttu-id="364d0-2753">accountName</span><span class="sxs-lookup"><span data-stu-id="364d0-2753">accountName</span></span> |<span data-ttu-id="364d0-2754">Name of the Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="364d0-2754">Name of the Azure Batch account.</span></span> |<span data-ttu-id="364d0-2755">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2755">Yes</span></span> |
| <span data-ttu-id="364d0-2756">accessKey</span><span class="sxs-lookup"><span data-stu-id="364d0-2756">accessKey</span></span> |<span data-ttu-id="364d0-2757">Access key for the Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="364d0-2757">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="364d0-2758">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2758">Yes</span></span> |
| <span data-ttu-id="364d0-2759">poolName</span><span class="sxs-lookup"><span data-stu-id="364d0-2759">poolName</span></span> |<span data-ttu-id="364d0-2760">Name of the pool of virtual machines.</span><span class="sxs-lookup"><span data-stu-id="364d0-2760">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="364d0-2761">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2761">Yes</span></span> |
| <span data-ttu-id="364d0-2762">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="364d0-2762">linkedServiceName</span></span> |<span data-ttu-id="364d0-2763">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2763">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="364d0-2764">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span><span class="sxs-lookup"><span data-stu-id="364d0-2764">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="364d0-2765">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2765">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="364d0-2766">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2766">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="364d0-2767">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="364d0-2767">Azure Machine Learning</span></span>
<span data-ttu-id="364d0-2768">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-2768">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="364d0-2769">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="364d0-2769">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-2770">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2770">Linked service</span></span>
<span data-ttu-id="364d0-2771">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2771">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="364d0-2772">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2772">Property</span></span> | <span data-ttu-id="364d0-2773">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2773">Description</span></span> | <span data-ttu-id="364d0-2774">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2774">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2775">Type</span><span class="sxs-lookup"><span data-stu-id="364d0-2775">Type</span></span> |<span data-ttu-id="364d0-2776">The type property should be set to: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2776">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="364d0-2777">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2777">Yes</span></span> |
| <span data-ttu-id="364d0-2778">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="364d0-2778">mlEndpoint</span></span> |<span data-ttu-id="364d0-2779">The batch scoring URL.</span><span class="sxs-lookup"><span data-stu-id="364d0-2779">The batch scoring URL.</span></span> |<span data-ttu-id="364d0-2780">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2780">Yes</span></span> |
| <span data-ttu-id="364d0-2781">apiKey</span><span class="sxs-lookup"><span data-stu-id="364d0-2781">apiKey</span></span> |<span data-ttu-id="364d0-2782">The published workspace model’s API.</span><span class="sxs-lookup"><span data-stu-id="364d0-2782">The published workspace model’s API.</span></span> |<span data-ttu-id="364d0-2783">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2783">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="364d0-2784">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2784">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="364d0-2785">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="364d0-2785">Azure Data Lake Analytics</span></span>
<span data-ttu-id="364d0-2786">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-2786">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="364d0-2787">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2787">Linked service</span></span>

<span data-ttu-id="364d0-2788">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2788">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="364d0-2789">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2789">Property</span></span> | <span data-ttu-id="364d0-2790">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2790">Description</span></span> | <span data-ttu-id="364d0-2791">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2791">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2792">Type</span><span class="sxs-lookup"><span data-stu-id="364d0-2792">Type</span></span> |<span data-ttu-id="364d0-2793">The type property should be set to: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2793">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="364d0-2794">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2794">Yes</span></span> |
| <span data-ttu-id="364d0-2795">accountName</span><span class="sxs-lookup"><span data-stu-id="364d0-2795">accountName</span></span> |<span data-ttu-id="364d0-2796">Azure Data Lake Analytics Account Name.</span><span class="sxs-lookup"><span data-stu-id="364d0-2796">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="364d0-2797">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2797">Yes</span></span> |
| <span data-ttu-id="364d0-2798">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="364d0-2798">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="364d0-2799">Azure Data Lake Analytics URI.</span><span class="sxs-lookup"><span data-stu-id="364d0-2799">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="364d0-2800">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2800">No</span></span> |
| <span data-ttu-id="364d0-2801">authorization</span><span class="sxs-lookup"><span data-stu-id="364d0-2801">authorization</span></span> |<span data-ttu-id="364d0-2802">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span><span class="sxs-lookup"><span data-stu-id="364d0-2802">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="364d0-2803">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2803">Yes</span></span> |
| <span data-ttu-id="364d0-2804">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="364d0-2804">subscriptionId</span></span> |<span data-ttu-id="364d0-2805">Azure subscription id</span><span class="sxs-lookup"><span data-stu-id="364d0-2805">Azure subscription id</span></span> |<span data-ttu-id="364d0-2806">No (If not specified, subscription of the data factory is used).</span><span class="sxs-lookup"><span data-stu-id="364d0-2806">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="364d0-2807">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="364d0-2807">resourceGroupName</span></span> |<span data-ttu-id="364d0-2808">Azure resource group name</span><span class="sxs-lookup"><span data-stu-id="364d0-2808">Azure resource group name</span></span> |<span data-ttu-id="364d0-2809">No (If not specified, resource group of the data factory is used).</span><span class="sxs-lookup"><span data-stu-id="364d0-2809">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="364d0-2810">sessionId</span><span class="sxs-lookup"><span data-stu-id="364d0-2810">sessionId</span></span> |<span data-ttu-id="364d0-2811">session id from the OAuth authorization session.</span><span class="sxs-lookup"><span data-stu-id="364d0-2811">session id from the OAuth authorization session.</span></span> <span data-ttu-id="364d0-2812">Each session id is unique and may only be used once.</span><span class="sxs-lookup"><span data-stu-id="364d0-2812">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="364d0-2813">When you use the Data Factory Editor, this ID is auto-generated.</span><span class="sxs-lookup"><span data-stu-id="364d0-2813">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="364d0-2814">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2814">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="364d0-2815">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2815">JSON example</span></span>
<span data-ttu-id="364d0-2816">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2816">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="364d0-2817">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="364d0-2817">Azure SQL Database</span></span>
<span data-ttu-id="364d0-2818">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-2818">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-2819">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2819">Linked service</span></span>
<span data-ttu-id="364d0-2820">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2820">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2821">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2821">Property</span></span> | <span data-ttu-id="364d0-2822">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2822">Description</span></span> | <span data-ttu-id="364d0-2823">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2823">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2824">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-2824">connectionString</span></span> |<span data-ttu-id="364d0-2825">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2825">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="364d0-2826">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2826">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="364d0-2827">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2827">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="364d0-2828">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2828">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="364d0-2829">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="364d0-2829">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="364d0-2830">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-2830">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-2831">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2831">Linked service</span></span>
<span data-ttu-id="364d0-2832">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="364d0-2832">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="364d0-2833">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2833">Property</span></span> | <span data-ttu-id="364d0-2834">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2834">Description</span></span> | <span data-ttu-id="364d0-2835">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2835">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2836">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-2836">connectionString</span></span> |<span data-ttu-id="364d0-2837">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2837">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="364d0-2838">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2838">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="364d0-2839">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2839">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="364d0-2840">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2840">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="364d0-2841">SQL Server</span><span class="sxs-lookup"><span data-stu-id="364d0-2841">SQL Server</span></span> 
<span data-ttu-id="364d0-2842">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-2842">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="364d0-2843">Linked service</span><span class="sxs-lookup"><span data-stu-id="364d0-2843">Linked service</span></span>
<span data-ttu-id="364d0-2844">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-2844">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="364d0-2845">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2845">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="364d0-2846">The following table provides description for JSON elements specific to SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="364d0-2846">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="364d0-2847">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2847">Property</span></span> | <span data-ttu-id="364d0-2848">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2848">Description</span></span> | <span data-ttu-id="364d0-2849">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2849">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2850">type</span><span class="sxs-lookup"><span data-stu-id="364d0-2850">type</span></span> |<span data-ttu-id="364d0-2851">The type property should be set to: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2851">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="364d0-2852">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2852">Yes</span></span> |
| <span data-ttu-id="364d0-2853">connectionString</span><span class="sxs-lookup"><span data-stu-id="364d0-2853">connectionString</span></span> |<span data-ttu-id="364d0-2854">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-2854">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="364d0-2855">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2855">Yes</span></span> |
| <span data-ttu-id="364d0-2856">gatewayName</span><span class="sxs-lookup"><span data-stu-id="364d0-2856">gatewayName</span></span> |<span data-ttu-id="364d0-2857">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="364d0-2857">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="364d0-2858">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2858">Yes</span></span> |
| <span data-ttu-id="364d0-2859">username</span><span class="sxs-lookup"><span data-stu-id="364d0-2859">username</span></span> |<span data-ttu-id="364d0-2860">Specify user name if you are using Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="364d0-2860">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="364d0-2861">Example: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2861">Example: **domainname\\username**.</span></span> |<span data-ttu-id="364d0-2862">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2862">No</span></span> |
| <span data-ttu-id="364d0-2863">password</span><span class="sxs-lookup"><span data-stu-id="364d0-2863">password</span></span> |<span data-ttu-id="364d0-2864">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="364d0-2864">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="364d0-2865">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2865">No</span></span> |

<span data-ttu-id="364d0-2866">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span><span class="sxs-lookup"><span data-stu-id="364d0-2866">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="364d0-2867">Example: JSON for using SQL Authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2867">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="364d0-2868">Example: JSON for using Windows Authentication</span><span class="sxs-lookup"><span data-stu-id="364d0-2868">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="364d0-2869">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="364d0-2869">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="364d0-2870">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span><span class="sxs-lookup"><span data-stu-id="364d0-2870">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="364d0-2871">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2871">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="364d0-2872">DATA TRANSFORMATION ACTIVITIES</span><span class="sxs-lookup"><span data-stu-id="364d0-2872">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="364d0-2873">Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2873">Activity</span></span> | <span data-ttu-id="364d0-2874">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2874">Description</span></span>
-------- | -----------
[<span data-ttu-id="364d0-2875">HDInsight Hive activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2875">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="364d0-2876">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2876">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="364d0-2877">HDInsight Pig activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2877">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="364d0-2878">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2878">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="364d0-2879">HDInsight MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2879">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="364d0-2880">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2880">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="364d0-2881">HDInsight Streaming Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2881">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="364d0-2882">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2882">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="364d0-2883">HDInsight Spark Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2883">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="364d0-2884">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2884">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="364d0-2885">Machine Learning Batch Execution Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2885">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="364d0-2886">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="364d0-2886">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="364d0-2887">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span><span class="sxs-lookup"><span data-stu-id="364d0-2887">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="364d0-2888">Machine Learning Update Resource Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2888">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="364d0-2889">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span><span class="sxs-lookup"><span data-stu-id="364d0-2889">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="364d0-2890">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span><span class="sxs-lookup"><span data-stu-id="364d0-2890">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="364d0-2891">You can use the Update Resource Activity to update the web service with the newly trained model.</span><span class="sxs-lookup"><span data-stu-id="364d0-2891">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="364d0-2892">Stored Procedure Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2892">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="364d0-2893">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="364d0-2893">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="364d0-2894">Data Lake Analytics U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2894">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="364d0-2895">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2895">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="364d0-2896">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2896">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="364d0-2897">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-2897">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="364d0-2898">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-2898">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="364d0-2899">HDInsight Hive Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2899">HDInsight Hive Activity</span></span>
<span data-ttu-id="364d0-2900">You can specify the following properties in a Hive Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-2900">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="364d0-2901">The type property for the activity must be: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2901">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="364d0-2902">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2902">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-2903">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span><span class="sxs-lookup"><span data-stu-id="364d0-2903">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="364d0-2904">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2904">Property</span></span> | <span data-ttu-id="364d0-2905">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2905">Description</span></span> | <span data-ttu-id="364d0-2906">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2906">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2907">script</span><span class="sxs-lookup"><span data-stu-id="364d0-2907">script</span></span> |<span data-ttu-id="364d0-2908">Specify the Hive script inline</span><span class="sxs-lookup"><span data-stu-id="364d0-2908">Specify the Hive script inline</span></span> |<span data-ttu-id="364d0-2909">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2909">No</span></span> |
| <span data-ttu-id="364d0-2910">script path</span><span class="sxs-lookup"><span data-stu-id="364d0-2910">script path</span></span> |<span data-ttu-id="364d0-2911">Store the Hive script in an Azure blob storage and provide the path to the file.</span><span class="sxs-lookup"><span data-stu-id="364d0-2911">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="364d0-2912">Use 'script' or 'scriptPath' property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2912">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="364d0-2913">Both cannot be used together.</span><span class="sxs-lookup"><span data-stu-id="364d0-2913">Both cannot be used together.</span></span> <span data-ttu-id="364d0-2914">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-2914">The file name is case-sensitive.</span></span> |<span data-ttu-id="364d0-2915">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2915">No</span></span> |
| <span data-ttu-id="364d0-2916">defines</span><span class="sxs-lookup"><span data-stu-id="364d0-2916">defines</span></span> |<span data-ttu-id="364d0-2917">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="364d0-2917">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="364d0-2918">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2918">No</span></span> |

<span data-ttu-id="364d0-2919">These type properties are specific to the Hive Activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-2919">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="364d0-2920">Other properties (outside the typeProperties section) are supported for all activities.</span><span class="sxs-lookup"><span data-stu-id="364d0-2920">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="364d0-2921">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2921">JSON example</span></span>
<span data-ttu-id="364d0-2922">The following JSON defines a HDInsight Hive activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-2922">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

<span data-ttu-id="364d0-2923">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2923">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="364d0-2924">HDInsight Pig Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2924">HDInsight Pig Activity</span></span>
<span data-ttu-id="364d0-2925">You can specify the following properties in a Pig Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-2925">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="364d0-2926">The type property for the activity must be: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2926">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="364d0-2927">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2927">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-2928">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span><span class="sxs-lookup"><span data-stu-id="364d0-2928">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="364d0-2929">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2929">Property</span></span> | <span data-ttu-id="364d0-2930">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2930">Description</span></span> | <span data-ttu-id="364d0-2931">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2931">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2932">script</span><span class="sxs-lookup"><span data-stu-id="364d0-2932">script</span></span> |<span data-ttu-id="364d0-2933">Specify the Pig script inline</span><span class="sxs-lookup"><span data-stu-id="364d0-2933">Specify the Pig script inline</span></span> |<span data-ttu-id="364d0-2934">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2934">No</span></span> |
| <span data-ttu-id="364d0-2935">script path</span><span class="sxs-lookup"><span data-stu-id="364d0-2935">script path</span></span> |<span data-ttu-id="364d0-2936">Store the Pig script in an Azure blob storage and provide the path to the file.</span><span class="sxs-lookup"><span data-stu-id="364d0-2936">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="364d0-2937">Use 'script' or 'scriptPath' property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2937">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="364d0-2938">Both cannot be used together.</span><span class="sxs-lookup"><span data-stu-id="364d0-2938">Both cannot be used together.</span></span> <span data-ttu-id="364d0-2939">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-2939">The file name is case-sensitive.</span></span> |<span data-ttu-id="364d0-2940">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2940">No</span></span> |
| <span data-ttu-id="364d0-2941">defines</span><span class="sxs-lookup"><span data-stu-id="364d0-2941">defines</span></span> |<span data-ttu-id="364d0-2942">Specify parameters as key/value pairs for referencing within the Pig script</span><span class="sxs-lookup"><span data-stu-id="364d0-2942">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="364d0-2943">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2943">No</span></span> |

<span data-ttu-id="364d0-2944">These type properties are specific to the Pig Activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-2944">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="364d0-2945">Other properties (outside the typeProperties section) are supported for all activities.</span><span class="sxs-lookup"><span data-stu-id="364d0-2945">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="364d0-2946">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2946">JSON example</span></span>

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

<span data-ttu-id="364d0-2947">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2947">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="364d0-2948">HDInsight MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2948">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="364d0-2949">You can specify the following properties in a MapReduce Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-2949">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="364d0-2950">The type property for the activity must be: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2950">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="364d0-2951">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2951">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-2952">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span><span class="sxs-lookup"><span data-stu-id="364d0-2952">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="364d0-2953">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2953">Property</span></span> | <span data-ttu-id="364d0-2954">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2954">Description</span></span> | <span data-ttu-id="364d0-2955">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-2955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-2956">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="364d0-2956">jarLinkedService</span></span> | <span data-ttu-id="364d0-2957">Name of the linked service for the Azure Storage that contains the JAR file.</span><span class="sxs-lookup"><span data-stu-id="364d0-2957">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="364d0-2958">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2958">Yes</span></span> |
| <span data-ttu-id="364d0-2959">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="364d0-2959">jarFilePath</span></span> | <span data-ttu-id="364d0-2960">Path to the JAR file in the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="364d0-2960">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="364d0-2961">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2961">Yes</span></span> | 
| <span data-ttu-id="364d0-2962">className</span><span class="sxs-lookup"><span data-stu-id="364d0-2962">className</span></span> | <span data-ttu-id="364d0-2963">Name of the main class in the JAR file.</span><span class="sxs-lookup"><span data-stu-id="364d0-2963">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="364d0-2964">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-2964">Yes</span></span> | 
| <span data-ttu-id="364d0-2965">arguments</span><span class="sxs-lookup"><span data-stu-id="364d0-2965">arguments</span></span> | <span data-ttu-id="364d0-2966">A list of comma-separated arguments for the MapReduce program.</span><span class="sxs-lookup"><span data-stu-id="364d0-2966">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="364d0-2967">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span><span class="sxs-lookup"><span data-stu-id="364d0-2967">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="364d0-2968">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span><span class="sxs-lookup"><span data-stu-id="364d0-2968">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="364d0-2969">No</span><span class="sxs-lookup"><span data-stu-id="364d0-2969">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="364d0-2970">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-2970">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="364d0-2971">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-2971">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="364d0-2972">HDInsight Streaming Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-2972">HDInsight Streaming Activity</span></span>
<span data-ttu-id="364d0-2973">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-2973">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="364d0-2974">The type property for the activity must be: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="364d0-2974">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="364d0-2975">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2975">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-2976">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span><span class="sxs-lookup"><span data-stu-id="364d0-2976">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="364d0-2977">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-2977">Property</span></span> | <span data-ttu-id="364d0-2978">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-2978">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="364d0-2979">mapper</span><span class="sxs-lookup"><span data-stu-id="364d0-2979">mapper</span></span> | <span data-ttu-id="364d0-2980">Name of the mapper executable.</span><span class="sxs-lookup"><span data-stu-id="364d0-2980">Name of the mapper executable.</span></span> <span data-ttu-id="364d0-2981">In the example, cat.exe is the mapper executable.</span><span class="sxs-lookup"><span data-stu-id="364d0-2981">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="364d0-2982">reducer</span><span class="sxs-lookup"><span data-stu-id="364d0-2982">reducer</span></span> | <span data-ttu-id="364d0-2983">Name of the reducer executable.</span><span class="sxs-lookup"><span data-stu-id="364d0-2983">Name of the reducer executable.</span></span> <span data-ttu-id="364d0-2984">In the example, wc.exe is the reducer executable.</span><span class="sxs-lookup"><span data-stu-id="364d0-2984">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="364d0-2985">input</span><span class="sxs-lookup"><span data-stu-id="364d0-2985">input</span></span> | <span data-ttu-id="364d0-2986">Input file (including location) for the mapper.</span><span class="sxs-lookup"><span data-stu-id="364d0-2986">Input file (including location) for the mapper.</span></span> <span data-ttu-id="364d0-2987">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span><span class="sxs-lookup"><span data-stu-id="364d0-2987">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="364d0-2988">output</span><span class="sxs-lookup"><span data-stu-id="364d0-2988">output</span></span> | <span data-ttu-id="364d0-2989">Output file (including location) for the reducer.</span><span class="sxs-lookup"><span data-stu-id="364d0-2989">Output file (including location) for the reducer.</span></span> <span data-ttu-id="364d0-2990">The output of the Hadoop Streaming job is written to the location specified for this property.</span><span class="sxs-lookup"><span data-stu-id="364d0-2990">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="364d0-2991">filePaths</span><span class="sxs-lookup"><span data-stu-id="364d0-2991">filePaths</span></span> | <span data-ttu-id="364d0-2992">Paths for the mapper and reducer executables.</span><span class="sxs-lookup"><span data-stu-id="364d0-2992">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="364d0-2993">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span><span class="sxs-lookup"><span data-stu-id="364d0-2993">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="364d0-2994">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="364d0-2994">fileLinkedService</span></span> | <span data-ttu-id="364d0-2995">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span><span class="sxs-lookup"><span data-stu-id="364d0-2995">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="364d0-2996">arguments</span><span class="sxs-lookup"><span data-stu-id="364d0-2996">arguments</span></span> | <span data-ttu-id="364d0-2997">A list of comma-separated arguments for the MapReduce program.</span><span class="sxs-lookup"><span data-stu-id="364d0-2997">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="364d0-2998">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span><span class="sxs-lookup"><span data-stu-id="364d0-2998">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="364d0-2999">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span><span class="sxs-lookup"><span data-stu-id="364d0-2999">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="364d0-3000">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="364d0-3000">getDebugInfo</span></span> | <span data-ttu-id="364d0-3001">An optional element.</span><span class="sxs-lookup"><span data-stu-id="364d0-3001">An optional element.</span></span> <span data-ttu-id="364d0-3002">When it is set to Failure, the logs are downloaded only on failure.</span><span class="sxs-lookup"><span data-stu-id="364d0-3002">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="364d0-3003">When it is set to All, logs are always downloaded irrespective of the execution status.</span><span class="sxs-lookup"><span data-stu-id="364d0-3003">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="364d0-3004">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3004">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="364d0-3005">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="364d0-3005">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="364d0-3006">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3006">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="364d0-3007">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-3007">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="364d0-3008">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-3008">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="364d0-3009">HDInsight Spark Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-3009">HDInsight Spark Activity</span></span>
<span data-ttu-id="364d0-3010">You can specify the following properties in a Spark Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-3010">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="364d0-3011">The type property for the activity must be: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3011">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="364d0-3012">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3012">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-3013">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span><span class="sxs-lookup"><span data-stu-id="364d0-3013">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="364d0-3014">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-3014">Property</span></span> | <span data-ttu-id="364d0-3015">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-3015">Description</span></span> | <span data-ttu-id="364d0-3016">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-3016">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="364d0-3017">rootPath</span><span class="sxs-lookup"><span data-stu-id="364d0-3017">rootPath</span></span> | <span data-ttu-id="364d0-3018">The Azure Blob container and folder that contains the Spark file.</span><span class="sxs-lookup"><span data-stu-id="364d0-3018">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="364d0-3019">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-3019">The file name is case-sensitive.</span></span> | <span data-ttu-id="364d0-3020">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3020">Yes</span></span> |
| <span data-ttu-id="364d0-3021">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="364d0-3021">entryFilePath</span></span> | <span data-ttu-id="364d0-3022">Relative path to the root folder of the Spark code/package.</span><span class="sxs-lookup"><span data-stu-id="364d0-3022">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="364d0-3023">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3023">Yes</span></span> |
| <span data-ttu-id="364d0-3024">className</span><span class="sxs-lookup"><span data-stu-id="364d0-3024">className</span></span> | <span data-ttu-id="364d0-3025">Application's Java/Spark main class</span><span class="sxs-lookup"><span data-stu-id="364d0-3025">Application's Java/Spark main class</span></span> | <span data-ttu-id="364d0-3026">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3026">No</span></span> | 
| <span data-ttu-id="364d0-3027">arguments</span><span class="sxs-lookup"><span data-stu-id="364d0-3027">arguments</span></span> | <span data-ttu-id="364d0-3028">A list of command-line arguments to the Spark program.</span><span class="sxs-lookup"><span data-stu-id="364d0-3028">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="364d0-3029">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3029">No</span></span> | 
| <span data-ttu-id="364d0-3030">proxyUser</span><span class="sxs-lookup"><span data-stu-id="364d0-3030">proxyUser</span></span> | <span data-ttu-id="364d0-3031">The user account to impersonate to execute the Spark program</span><span class="sxs-lookup"><span data-stu-id="364d0-3031">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="364d0-3032">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3032">No</span></span> | 
| <span data-ttu-id="364d0-3033">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="364d0-3033">sparkConfig</span></span> | <span data-ttu-id="364d0-3034">Spark configuration properties.</span><span class="sxs-lookup"><span data-stu-id="364d0-3034">Spark configuration properties.</span></span> | <span data-ttu-id="364d0-3035">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3035">No</span></span> | 
| <span data-ttu-id="364d0-3036">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="364d0-3036">getDebugInfo</span></span> | <span data-ttu-id="364d0-3037">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="364d0-3037">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="364d0-3038">Allowed values: None, Always, or Failure.</span><span class="sxs-lookup"><span data-stu-id="364d0-3038">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="364d0-3039">Default value: None.</span><span class="sxs-lookup"><span data-stu-id="364d0-3039">Default value: None.</span></span> | <span data-ttu-id="364d0-3040">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3040">No</span></span> | 
| <span data-ttu-id="364d0-3041">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="364d0-3041">sparkJobLinkedService</span></span> | <span data-ttu-id="364d0-3042">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span><span class="sxs-lookup"><span data-stu-id="364d0-3042">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="364d0-3043">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span><span class="sxs-lookup"><span data-stu-id="364d0-3043">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="364d0-3044">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3044">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="364d0-3045">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-3045">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="364d0-3046">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="364d0-3046">Note the following points:</span></span> 

- <span data-ttu-id="364d0-3047">The **type** property is set to **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3047">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="364d0-3048">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span><span class="sxs-lookup"><span data-stu-id="364d0-3048">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="364d0-3049">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="364d0-3049">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="364d0-3050">You can upload the file to a different Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="364d0-3050">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="364d0-3051">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="364d0-3051">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="364d0-3052">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3052">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="364d0-3053">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-3053">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="364d0-3054">The **entryFilePath** is set to the **test.py**, which is the python file.</span><span class="sxs-lookup"><span data-stu-id="364d0-3054">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="364d0-3055">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span><span class="sxs-lookup"><span data-stu-id="364d0-3055">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="364d0-3056">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span><span class="sxs-lookup"><span data-stu-id="364d0-3056">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="364d0-3057">The **outputs** section has one output dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-3057">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="364d0-3058">You must specify an output dataset even if the spark program does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="364d0-3058">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="364d0-3059">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="364d0-3059">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="364d0-3060">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-3060">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="364d0-3061">Machine Learning Batch Execution Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-3061">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="364d0-3062">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-3062">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="364d0-3063">The type property for the activity must be: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3063">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="364d0-3064">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3064">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-3065">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span><span class="sxs-lookup"><span data-stu-id="364d0-3065">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="364d0-3066">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-3066">Property</span></span> | <span data-ttu-id="364d0-3067">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-3067">Description</span></span> | <span data-ttu-id="364d0-3068">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-3068">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="364d0-3069">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="364d0-3069">webServiceInput</span></span> | <span data-ttu-id="364d0-3070">The dataset to be passed as an input for the Azure ML web service.</span><span class="sxs-lookup"><span data-stu-id="364d0-3070">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="364d0-3071">This dataset must also be included in the inputs for the activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-3071">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="364d0-3072">Use either webServiceInput or webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="364d0-3072">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="364d0-3073">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="364d0-3073">webServiceInputs</span></span> | <span data-ttu-id="364d0-3074">Specify datasets to be passed as inputs for the Azure ML web service.</span><span class="sxs-lookup"><span data-stu-id="364d0-3074">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="364d0-3075">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3075">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="364d0-3076">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3076">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="364d0-3077">Use either webServiceInput or webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="364d0-3077">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="364d0-3078">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="364d0-3078">webServiceOutputs</span></span> | <span data-ttu-id="364d0-3079">The datasets that are assigned as outputs for the Azure ML web service.</span><span class="sxs-lookup"><span data-stu-id="364d0-3079">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="364d0-3080">The web service returns output data in this dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-3080">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="364d0-3081">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3081">Yes</span></span> | 
<span data-ttu-id="364d0-3082">globalParameters</span><span class="sxs-lookup"><span data-stu-id="364d0-3082">globalParameters</span></span> | <span data-ttu-id="364d0-3083">Specify values for the web service parameters in this section.</span><span class="sxs-lookup"><span data-stu-id="364d0-3083">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="364d0-3084">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3084">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="364d0-3085">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-3085">JSON example</span></span>
<span data-ttu-id="364d0-3086">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span><span class="sxs-lookup"><span data-stu-id="364d0-3086">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="364d0-3087">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3087">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="364d0-3088">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3088">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="364d0-3089">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="364d0-3089">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="364d0-3090">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span><span class="sxs-lookup"><span data-stu-id="364d0-3090">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="364d0-3091">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span><span class="sxs-lookup"><span data-stu-id="364d0-3091">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="364d0-3092">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span><span class="sxs-lookup"><span data-stu-id="364d0-3092">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="364d0-3093">Machine Learning Update Resource Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-3093">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="364d0-3094">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-3094">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="364d0-3095">The type property for the activity must be: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3095">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="364d0-3096">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3096">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-3097">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span><span class="sxs-lookup"><span data-stu-id="364d0-3097">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="364d0-3098">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-3098">Property</span></span> | <span data-ttu-id="364d0-3099">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-3099">Description</span></span> | <span data-ttu-id="364d0-3100">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-3100">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="364d0-3101">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="364d0-3101">trainedModelName</span></span> | <span data-ttu-id="364d0-3102">Name of the retrained model.</span><span class="sxs-lookup"><span data-stu-id="364d0-3102">Name of the retrained model.</span></span> | <span data-ttu-id="364d0-3103">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3103">Yes</span></span> |  
<span data-ttu-id="364d0-3104">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="364d0-3104">trainedModelDatasetName</span></span> | <span data-ttu-id="364d0-3105">Dataset pointing to the iLearner file returned by the retraining operation.</span><span class="sxs-lookup"><span data-stu-id="364d0-3105">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="364d0-3106">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3106">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="364d0-3107">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-3107">JSON example</span></span>
<span data-ttu-id="364d0-3108">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3108">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="364d0-3109">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span><span class="sxs-lookup"><span data-stu-id="364d0-3109">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="364d0-3110">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span><span class="sxs-lookup"><span data-stu-id="364d0-3110">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="364d0-3111">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-3111">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="364d0-3112">Data Lake Analytics U-SQL Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-3112">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="364d0-3113">You can specify the following properties in a U-SQL Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-3113">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="364d0-3114">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3114">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="364d0-3115">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3115">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-3116">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="364d0-3116">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="364d0-3117">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-3117">Property</span></span> | <span data-ttu-id="364d0-3118">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-3118">Description</span></span> | <span data-ttu-id="364d0-3119">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-3119">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-3120">scriptPath</span><span class="sxs-lookup"><span data-stu-id="364d0-3120">scriptPath</span></span> |<span data-ttu-id="364d0-3121">Path to folder that contains the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="364d0-3121">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="364d0-3122">Name of the file is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="364d0-3122">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="364d0-3123">No (if you use script)</span><span class="sxs-lookup"><span data-stu-id="364d0-3123">No (if you use script)</span></span> |
| <span data-ttu-id="364d0-3124">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="364d0-3124">scriptLinkedService</span></span> |<span data-ttu-id="364d0-3125">Linked service that links the storage that contains the script to the data factory</span><span class="sxs-lookup"><span data-stu-id="364d0-3125">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="364d0-3126">No (if you use script)</span><span class="sxs-lookup"><span data-stu-id="364d0-3126">No (if you use script)</span></span> |
| <span data-ttu-id="364d0-3127">script</span><span class="sxs-lookup"><span data-stu-id="364d0-3127">script</span></span> |<span data-ttu-id="364d0-3128">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="364d0-3128">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="364d0-3129">For example: "script": "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="364d0-3129">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="364d0-3130">No (if you use scriptPath and scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="364d0-3130">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="364d0-3131">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="364d0-3131">degreeOfParallelism</span></span> |<span data-ttu-id="364d0-3132">The maximum number of nodes simultaneously used to run the job.</span><span class="sxs-lookup"><span data-stu-id="364d0-3132">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="364d0-3133">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3133">No</span></span> |
| <span data-ttu-id="364d0-3134">priority</span><span class="sxs-lookup"><span data-stu-id="364d0-3134">priority</span></span> |<span data-ttu-id="364d0-3135">Determines which jobs out of all that are queued should be selected to run first.</span><span class="sxs-lookup"><span data-stu-id="364d0-3135">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="364d0-3136">The lower the number, the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="364d0-3136">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="364d0-3137">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3137">No</span></span> |
| <span data-ttu-id="364d0-3138">parameters</span><span class="sxs-lookup"><span data-stu-id="364d0-3138">parameters</span></span> |<span data-ttu-id="364d0-3139">Parameters for the U-SQL script</span><span class="sxs-lookup"><span data-stu-id="364d0-3139">Parameters for the U-SQL script</span></span> |<span data-ttu-id="364d0-3140">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3140">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="364d0-3141">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-3141">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="364d0-3142">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="364d0-3142">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="364d0-3143">Stored Procedure Activity</span><span class="sxs-lookup"><span data-stu-id="364d0-3143">Stored Procedure Activity</span></span>
<span data-ttu-id="364d0-3144">You can specify the following properties in a Stored Procedure Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-3144">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="364d0-3145">The type property for the activity must be: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3145">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="364d0-3146">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span><span class="sxs-lookup"><span data-stu-id="364d0-3146">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="364d0-3147">SQL Server</span><span class="sxs-lookup"><span data-stu-id="364d0-3147">SQL Server</span></span> 
- <span data-ttu-id="364d0-3148">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="364d0-3148">Azure SQL Database</span></span>
- <span data-ttu-id="364d0-3149">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="364d0-3149">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="364d0-3150">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span><span class="sxs-lookup"><span data-stu-id="364d0-3150">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="364d0-3151">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-3151">Property</span></span> | <span data-ttu-id="364d0-3152">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-3152">Description</span></span> | <span data-ttu-id="364d0-3153">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-3153">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="364d0-3154">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="364d0-3154">storedProcedureName</span></span> |<span data-ttu-id="364d0-3155">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span><span class="sxs-lookup"><span data-stu-id="364d0-3155">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="364d0-3156">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3156">Yes</span></span> |
| <span data-ttu-id="364d0-3157">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="364d0-3157">storedProcedureParameters</span></span> |<span data-ttu-id="364d0-3158">Specify values for stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="364d0-3158">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="364d0-3159">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span><span class="sxs-lookup"><span data-stu-id="364d0-3159">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="364d0-3160">See the following sample to learn about using this property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3160">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="364d0-3161">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3161">No</span></span> |

<span data-ttu-id="364d0-3162">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span><span class="sxs-lookup"><span data-stu-id="364d0-3162">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="364d0-3163">The input dataset cannot be consumed in the stored procedure as a parameter.</span><span class="sxs-lookup"><span data-stu-id="364d0-3163">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="364d0-3164">It is only used to check the dependency before starting the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-3164">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="364d0-3165">You must specify an output dataset for a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-3165">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="364d0-3166">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span><span class="sxs-lookup"><span data-stu-id="364d0-3166">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="364d0-3167">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span><span class="sxs-lookup"><span data-stu-id="364d0-3167">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="364d0-3168">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="364d0-3168">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="364d0-3169">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span><span class="sxs-lookup"><span data-stu-id="364d0-3169">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="364d0-3170">It is the stored procedure that writes to a SQL table that the output dataset points to.</span><span class="sxs-lookup"><span data-stu-id="364d0-3170">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="364d0-3171">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="364d0-3171">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="364d0-3172">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-3172">JSON example</span></span>

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
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="364d0-3173">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-3173">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="364d0-3174">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="364d0-3174">.NET custom activity</span></span>
<span data-ttu-id="364d0-3175">You can specify the following properties in a .NET custom activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="364d0-3175">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="364d0-3176">The type property for the activity must be: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3176">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="364d0-3177">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="364d0-3177">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="364d0-3178">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span><span class="sxs-lookup"><span data-stu-id="364d0-3178">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="364d0-3179">Property</span><span class="sxs-lookup"><span data-stu-id="364d0-3179">Property</span></span> | <span data-ttu-id="364d0-3180">Description</span><span class="sxs-lookup"><span data-stu-id="364d0-3180">Description</span></span> | <span data-ttu-id="364d0-3181">Required</span><span class="sxs-lookup"><span data-stu-id="364d0-3181">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="364d0-3182">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="364d0-3182">AssemblyName</span></span> | <span data-ttu-id="364d0-3183">Name of the assembly.</span><span class="sxs-lookup"><span data-stu-id="364d0-3183">Name of the assembly.</span></span> <span data-ttu-id="364d0-3184">In the example, it is: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3184">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="364d0-3185">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3185">Yes</span></span> |
| <span data-ttu-id="364d0-3186">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="364d0-3186">EntryPoint</span></span> |<span data-ttu-id="364d0-3187">Name of the class that implements the IDotNetActivity interface.</span><span class="sxs-lookup"><span data-stu-id="364d0-3187">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="364d0-3188">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span><span class="sxs-lookup"><span data-stu-id="364d0-3188">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="364d0-3189">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3189">Yes</span></span> | 
| <span data-ttu-id="364d0-3190">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="364d0-3190">PackageLinkedService</span></span> | <span data-ttu-id="364d0-3191">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span><span class="sxs-lookup"><span data-stu-id="364d0-3191">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="364d0-3192">In the example, it is: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3192">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="364d0-3193">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3193">Yes</span></span> |
| <span data-ttu-id="364d0-3194">PackageFile</span><span class="sxs-lookup"><span data-stu-id="364d0-3194">PackageFile</span></span> | <span data-ttu-id="364d0-3195">Name of the zip file.</span><span class="sxs-lookup"><span data-stu-id="364d0-3195">Name of the zip file.</span></span> <span data-ttu-id="364d0-3196">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="364d0-3196">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="364d0-3197">Yes</span><span class="sxs-lookup"><span data-stu-id="364d0-3197">Yes</span></span> |
| <span data-ttu-id="364d0-3198">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="364d0-3198">extendedProperties</span></span> | <span data-ttu-id="364d0-3199">Extended properties that you can define and pass on to the .NET code.</span><span class="sxs-lookup"><span data-stu-id="364d0-3199">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="364d0-3200">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span><span class="sxs-lookup"><span data-stu-id="364d0-3200">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="364d0-3201">No</span><span class="sxs-lookup"><span data-stu-id="364d0-3201">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="364d0-3202">JSON example</span><span class="sxs-lookup"><span data-stu-id="364d0-3202">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="364d0-3203">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="364d0-3203">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="364d0-3204">Next Steps</span><span class="sxs-lookup"><span data-stu-id="364d0-3204">Next Steps</span></span>
<span data-ttu-id="364d0-3205">See the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="364d0-3205">See the following tutorials:</span></span> 

- [<span data-ttu-id="364d0-3206">Tutorial: create a pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="364d0-3206">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="364d0-3207">Tutorial: create a pipeline with a hive activity</span><span class="sxs-lookup"><span data-stu-id="364d0-3207">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
