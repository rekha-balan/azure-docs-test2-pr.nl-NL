---
title: Azure Data Factory - JSON Scripting Reference | Microsoft Docs
description: Provides JSON schemas for Data Factory entities.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: spelluru
ms.openlocfilehash: 8b3007a4eb439d0dbbf24528c7ee4ac0f4d7cb4f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661462"
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="825eb-103">Azure Data Factory - JSON Scripting Reference</span><span class="sxs-lookup"><span data-stu-id="825eb-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="825eb-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span><span class="sxs-lookup"><span data-stu-id="825eb-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="825eb-105">Pipeline</span><span class="sxs-lookup"><span data-stu-id="825eb-105">Pipeline</span></span> 
<span data-ttu-id="825eb-106">The high-level structure for a pipeline definition is as follows:</span><span class="sxs-lookup"><span data-stu-id="825eb-106">The high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="825eb-107">Following table describes the properties within the pipeline JSON definition:</span><span class="sxs-lookup"><span data-stu-id="825eb-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="825eb-108">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-108">Property</span></span> | <span data-ttu-id="825eb-109">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-109">Description</span></span> | <span data-ttu-id="825eb-110">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="825eb-111">name</span><span class="sxs-lookup"><span data-stu-id="825eb-111">name</span></span> | <span data-ttu-id="825eb-112">Name of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-112">Name of the pipeline.</span></span> <span data-ttu-id="825eb-113">Specify a name that represents the action that the activity or pipeline is configured to do</span><span class="sxs-lookup"><span data-stu-id="825eb-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="825eb-114">Maximum number of characters: 260</span><span class="sxs-lookup"><span data-stu-id="825eb-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="825eb-115">Must start with a letter number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="825eb-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="825eb-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="825eb-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="825eb-117">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-117">Yes</span></span> |
| <span data-ttu-id="825eb-118">description</span><span class="sxs-lookup"><span data-stu-id="825eb-118">description</span></span> |<span data-ttu-id="825eb-119">Text describing what the activity or pipeline is used for</span><span class="sxs-lookup"><span data-stu-id="825eb-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="825eb-120">No</span><span class="sxs-lookup"><span data-stu-id="825eb-120">No</span></span> |
| <span data-ttu-id="825eb-121">activities</span><span class="sxs-lookup"><span data-stu-id="825eb-121">activities</span></span> | <span data-ttu-id="825eb-122">Contains a list of activities.</span><span class="sxs-lookup"><span data-stu-id="825eb-122">Contains a list of activities.</span></span> | <span data-ttu-id="825eb-123">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-123">Yes</span></span> |
| <span data-ttu-id="825eb-124">start</span><span class="sxs-lookup"><span data-stu-id="825eb-124">start</span></span> |<span data-ttu-id="825eb-125">Start date-time for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="825eb-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="825eb-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="825eb-127">For example: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="825eb-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="825eb-128">It is possible to specify a local time, for example an EST time.</span><span class="sxs-lookup"><span data-stu-id="825eb-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="825eb-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="825eb-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="825eb-130">The start and end properties together specify active period for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="825eb-131">Output slices are only produced with in this active period.</span><span class="sxs-lookup"><span data-stu-id="825eb-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="825eb-132">No</span><span class="sxs-lookup"><span data-stu-id="825eb-132">No</span></span><br/><br/><span data-ttu-id="825eb-133">If you specify a value for the end property, you must specify value for the start property.</span><span class="sxs-lookup"><span data-stu-id="825eb-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="825eb-134">The start and end times can both be empty to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="825eb-135">You must specify both values to set an active period for the pipeline to run.</span><span class="sxs-lookup"><span data-stu-id="825eb-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="825eb-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span><span class="sxs-lookup"><span data-stu-id="825eb-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="825eb-137">end</span><span class="sxs-lookup"><span data-stu-id="825eb-137">end</span></span> |<span data-ttu-id="825eb-138">End date-time for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-138">End date-time for the pipeline.</span></span> <span data-ttu-id="825eb-139">If specified must be in ISO format.</span><span class="sxs-lookup"><span data-stu-id="825eb-139">If specified must be in ISO format.</span></span> <span data-ttu-id="825eb-140">For example: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="825eb-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="825eb-141">It is possible to specify a local time, for example an EST time.</span><span class="sxs-lookup"><span data-stu-id="825eb-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="825eb-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="825eb-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="825eb-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span><span class="sxs-lookup"><span data-stu-id="825eb-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="825eb-144">No</span><span class="sxs-lookup"><span data-stu-id="825eb-144">No</span></span> <br/><br/><span data-ttu-id="825eb-145">If you specify a value for the start property, you must specify value for the end property.</span><span class="sxs-lookup"><span data-stu-id="825eb-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="825eb-146">See notes for the **start** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="825eb-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="825eb-147">isPaused</span></span> |<span data-ttu-id="825eb-148">If set to true the pipeline does not run.</span><span class="sxs-lookup"><span data-stu-id="825eb-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="825eb-149">Default value = false.</span><span class="sxs-lookup"><span data-stu-id="825eb-149">Default value = false.</span></span> <span data-ttu-id="825eb-150">You can use this property to enable or disable.</span><span class="sxs-lookup"><span data-stu-id="825eb-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="825eb-151">No</span><span class="sxs-lookup"><span data-stu-id="825eb-151">No</span></span> |
| <span data-ttu-id="825eb-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="825eb-152">pipelineMode</span></span> |<span data-ttu-id="825eb-153">The method for scheduling runs for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="825eb-154">Allowed values are: scheduled (default), onetime.</span><span class="sxs-lookup"><span data-stu-id="825eb-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="825eb-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span><span class="sxs-lookup"><span data-stu-id="825eb-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="825eb-156">‘Onetime’ indicates that the pipeline runs only once.</span><span class="sxs-lookup"><span data-stu-id="825eb-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="825eb-157">Onetime pipelines once created cannot be modified/updated currently.</span><span class="sxs-lookup"><span data-stu-id="825eb-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="825eb-158">See [Onetime pipeline](data-factory-scheduling-and-execution.md#onetime-pipeline) for details about onetime setting.</span><span class="sxs-lookup"><span data-stu-id="825eb-158">See [Onetime pipeline](data-factory-scheduling-and-execution.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="825eb-159">No</span><span class="sxs-lookup"><span data-stu-id="825eb-159">No</span></span> |
| <span data-ttu-id="825eb-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="825eb-160">expirationTime</span></span> |<span data-ttu-id="825eb-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span><span class="sxs-lookup"><span data-stu-id="825eb-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="825eb-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span><span class="sxs-lookup"><span data-stu-id="825eb-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="825eb-163">No</span><span class="sxs-lookup"><span data-stu-id="825eb-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="825eb-164">Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-164">Activity</span></span> 
<span data-ttu-id="825eb-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span><span class="sxs-lookup"><span data-stu-id="825eb-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="825eb-166">Following table describe the properties within the activity JSON definition:</span><span class="sxs-lookup"><span data-stu-id="825eb-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="825eb-167">Tag</span><span class="sxs-lookup"><span data-stu-id="825eb-167">Tag</span></span> | <span data-ttu-id="825eb-168">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-168">Description</span></span> | <span data-ttu-id="825eb-169">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-170">name</span><span class="sxs-lookup"><span data-stu-id="825eb-170">name</span></span> |<span data-ttu-id="825eb-171">Name of the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-171">Name of the activity.</span></span> <span data-ttu-id="825eb-172">Specify a name that represents the action that the activity is configured to do</span><span class="sxs-lookup"><span data-stu-id="825eb-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="825eb-173">Maximum number of characters: 260</span><span class="sxs-lookup"><span data-stu-id="825eb-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="825eb-174">Must start with a letter number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="825eb-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="825eb-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="825eb-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="825eb-176">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-176">Yes</span></span> |
| <span data-ttu-id="825eb-177">description</span><span class="sxs-lookup"><span data-stu-id="825eb-177">description</span></span> |<span data-ttu-id="825eb-178">Text describing what the activity is used for.</span><span class="sxs-lookup"><span data-stu-id="825eb-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="825eb-179">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-179">Yes</span></span> |
| <span data-ttu-id="825eb-180">type</span><span class="sxs-lookup"><span data-stu-id="825eb-180">type</span></span> |<span data-ttu-id="825eb-181">Specifies the type of the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-181">Specifies the type of the activity.</span></span> <span data-ttu-id="825eb-182">See the [DATA STORES](#data-stores) and [TRANSFORMATION ACTIVITIES](#transformation-activities) articles for different types of activities.</span><span class="sxs-lookup"><span data-stu-id="825eb-182">See the [DATA STORES](#data-stores) and [TRANSFORMATION ACTIVITIES](#transformation-activities) articles for different types of activities.</span></span> |<span data-ttu-id="825eb-183">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-183">Yes</span></span> |
| <span data-ttu-id="825eb-184">inputs</span><span class="sxs-lookup"><span data-stu-id="825eb-184">inputs</span></span> |<span data-ttu-id="825eb-185">Input tables used by the activity</span><span class="sxs-lookup"><span data-stu-id="825eb-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="825eb-186">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-186">Yes</span></span> |
| <span data-ttu-id="825eb-187">outputs</span><span class="sxs-lookup"><span data-stu-id="825eb-187">outputs</span></span> |<span data-ttu-id="825eb-188">Output tables used by the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="825eb-189">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-189">Yes</span></span> |
| <span data-ttu-id="825eb-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="825eb-190">linkedServiceName</span></span> |<span data-ttu-id="825eb-191">Name of the linked service used by the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="825eb-192">An activity may require that you specify the linked service that links to the required compute environment.</span><span class="sxs-lookup"><span data-stu-id="825eb-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="825eb-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="825eb-194">No for all others</span><span class="sxs-lookup"><span data-stu-id="825eb-194">No for all others</span></span> |
| <span data-ttu-id="825eb-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="825eb-195">typeProperties</span></span> |<span data-ttu-id="825eb-196">Properties in the typeProperties section depend on type of the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="825eb-197">No</span><span class="sxs-lookup"><span data-stu-id="825eb-197">No</span></span> |
| <span data-ttu-id="825eb-198">policy</span><span class="sxs-lookup"><span data-stu-id="825eb-198">policy</span></span> |<span data-ttu-id="825eb-199">Policies that affect the run-time behavior of the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="825eb-200">If it is not specified, default policies are used.</span><span class="sxs-lookup"><span data-stu-id="825eb-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="825eb-201">No</span><span class="sxs-lookup"><span data-stu-id="825eb-201">No</span></span> |
| <span data-ttu-id="825eb-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="825eb-202">scheduler</span></span> |<span data-ttu-id="825eb-203">“scheduler” property is used to define desired scheduling for the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="825eb-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#Availability).</span><span class="sxs-lookup"><span data-stu-id="825eb-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#Availability).</span></span> |<span data-ttu-id="825eb-205">No</span><span class="sxs-lookup"><span data-stu-id="825eb-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="825eb-206">Policies</span><span class="sxs-lookup"><span data-stu-id="825eb-206">Policies</span></span>
<span data-ttu-id="825eb-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span><span class="sxs-lookup"><span data-stu-id="825eb-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="825eb-208">The following table provides the details.</span><span class="sxs-lookup"><span data-stu-id="825eb-208">The following table provides the details.</span></span>

| <span data-ttu-id="825eb-209">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-209">Property</span></span> | <span data-ttu-id="825eb-210">Permitted values</span><span class="sxs-lookup"><span data-stu-id="825eb-210">Permitted values</span></span> | <span data-ttu-id="825eb-211">Default Value</span><span class="sxs-lookup"><span data-stu-id="825eb-211">Default Value</span></span> | <span data-ttu-id="825eb-212">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-213">concurrency</span><span class="sxs-lookup"><span data-stu-id="825eb-213">concurrency</span></span> |<span data-ttu-id="825eb-214">Integer</span><span class="sxs-lookup"><span data-stu-id="825eb-214">Integer</span></span> <br/><br/><span data-ttu-id="825eb-215">Max value: 10</span><span class="sxs-lookup"><span data-stu-id="825eb-215">Max value: 10</span></span> |<span data-ttu-id="825eb-216">1</span><span class="sxs-lookup"><span data-stu-id="825eb-216">1</span></span> |<span data-ttu-id="825eb-217">Number of concurrent executions of the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="825eb-218">It determines the number of parallel activity executions that can happen on different slices.</span><span class="sxs-lookup"><span data-stu-id="825eb-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="825eb-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span><span class="sxs-lookup"><span data-stu-id="825eb-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="825eb-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="825eb-220">executionPriorityOrder</span></span> |<span data-ttu-id="825eb-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="825eb-221">NewestFirst</span></span><br/><br/><span data-ttu-id="825eb-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="825eb-222">OldestFirst</span></span> |<span data-ttu-id="825eb-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="825eb-223">OldestFirst</span></span> |<span data-ttu-id="825eb-224">Determines the ordering of data slices that are being processed.</span><span class="sxs-lookup"><span data-stu-id="825eb-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="825eb-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span><span class="sxs-lookup"><span data-stu-id="825eb-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="825eb-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span><span class="sxs-lookup"><span data-stu-id="825eb-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="825eb-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span><span class="sxs-lookup"><span data-stu-id="825eb-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="825eb-228">retry</span><span class="sxs-lookup"><span data-stu-id="825eb-228">retry</span></span> |<span data-ttu-id="825eb-229">Integer</span><span class="sxs-lookup"><span data-stu-id="825eb-229">Integer</span></span><br/><br/><span data-ttu-id="825eb-230">Max value can be 10</span><span class="sxs-lookup"><span data-stu-id="825eb-230">Max value can be 10</span></span> |<span data-ttu-id="825eb-231">0</span><span class="sxs-lookup"><span data-stu-id="825eb-231">0</span></span> |<span data-ttu-id="825eb-232">Number of retries before the data processing for the slice is marked as Failure.</span><span class="sxs-lookup"><span data-stu-id="825eb-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="825eb-233">Activity execution for a data slice is retried up to the specified retry count.</span><span class="sxs-lookup"><span data-stu-id="825eb-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="825eb-234">The retry is done as soon as possible after the failure.</span><span class="sxs-lookup"><span data-stu-id="825eb-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="825eb-235">timeout</span><span class="sxs-lookup"><span data-stu-id="825eb-235">timeout</span></span> |<span data-ttu-id="825eb-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="825eb-236">TimeSpan</span></span> |<span data-ttu-id="825eb-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="825eb-237">00:00:00</span></span> |<span data-ttu-id="825eb-238">Timeout for the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-238">Timeout for the activity.</span></span> <span data-ttu-id="825eb-239">Example: 00:10:00 (implies timeout 10 mins)</span><span class="sxs-lookup"><span data-stu-id="825eb-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="825eb-240">If a value is not specified or is 0, the timeout is infinite.</span><span class="sxs-lookup"><span data-stu-id="825eb-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="825eb-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span><span class="sxs-lookup"><span data-stu-id="825eb-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="825eb-242">The number of retries depends on the retry property.</span><span class="sxs-lookup"><span data-stu-id="825eb-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="825eb-243">When timeout occurs, the status is set to TimedOut.</span><span class="sxs-lookup"><span data-stu-id="825eb-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="825eb-244">delay</span><span class="sxs-lookup"><span data-stu-id="825eb-244">delay</span></span> |<span data-ttu-id="825eb-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="825eb-245">TimeSpan</span></span> |<span data-ttu-id="825eb-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="825eb-246">00:00:00</span></span> |<span data-ttu-id="825eb-247">Specify the delay before data processing of the slice starts.</span><span class="sxs-lookup"><span data-stu-id="825eb-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="825eb-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span><span class="sxs-lookup"><span data-stu-id="825eb-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="825eb-249">Example: 00:10:00 (implies delay of 10 mins)</span><span class="sxs-lookup"><span data-stu-id="825eb-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="825eb-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="825eb-250">longRetry</span></span> |<span data-ttu-id="825eb-251">Integer</span><span class="sxs-lookup"><span data-stu-id="825eb-251">Integer</span></span><br/><br/><span data-ttu-id="825eb-252">Max value: 10</span><span class="sxs-lookup"><span data-stu-id="825eb-252">Max value: 10</span></span> |<span data-ttu-id="825eb-253">1</span><span class="sxs-lookup"><span data-stu-id="825eb-253">1</span></span> |<span data-ttu-id="825eb-254">The number of long retry attempts before the slice execution is failed.</span><span class="sxs-lookup"><span data-stu-id="825eb-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="825eb-255">longRetry attempts are spaced by longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="825eb-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="825eb-256">So if you need to specify a time between retry attempts, use longRetry.</span><span class="sxs-lookup"><span data-stu-id="825eb-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="825eb-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry \* longRetry.</span><span class="sxs-lookup"><span data-stu-id="825eb-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry \* longRetry.</span></span><br/><br/><span data-ttu-id="825eb-258">For example, if we have the following settings in the activity policy:</span><span class="sxs-lookup"><span data-stu-id="825eb-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="825eb-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="825eb-259">Retry: 3</span></span><br/><span data-ttu-id="825eb-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="825eb-260">longRetry: 2</span></span><br/><span data-ttu-id="825eb-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="825eb-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="825eb-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span><span class="sxs-lookup"><span data-stu-id="825eb-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="825eb-263">Initially there would be 3 consecutive execution attempts.</span><span class="sxs-lookup"><span data-stu-id="825eb-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="825eb-264">After each attempt, the slice status would be Retry.</span><span class="sxs-lookup"><span data-stu-id="825eb-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="825eb-265">After first 3 attempts are over, the slice status would be LongRetry.</span><span class="sxs-lookup"><span data-stu-id="825eb-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="825eb-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span><span class="sxs-lookup"><span data-stu-id="825eb-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="825eb-267">After that, the slice status would be Failed and no more retries would be attempted.</span><span class="sxs-lookup"><span data-stu-id="825eb-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="825eb-268">Hence overall 6 attempts were made.</span><span class="sxs-lookup"><span data-stu-id="825eb-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="825eb-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span><span class="sxs-lookup"><span data-stu-id="825eb-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="825eb-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span><span class="sxs-lookup"><span data-stu-id="825eb-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="825eb-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span><span class="sxs-lookup"><span data-stu-id="825eb-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="825eb-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="825eb-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="825eb-273">Typically, higher values imply other systemic issues.</span><span class="sxs-lookup"><span data-stu-id="825eb-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="825eb-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="825eb-274">longRetryInterval</span></span> |<span data-ttu-id="825eb-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="825eb-275">TimeSpan</span></span> |<span data-ttu-id="825eb-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="825eb-276">00:00:00</span></span> |<span data-ttu-id="825eb-277">The delay between long retry attempts</span><span class="sxs-lookup"><span data-stu-id="825eb-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="825eb-278">typeProperties section</span><span class="sxs-lookup"><span data-stu-id="825eb-278">typeProperties section</span></span>
<span data-ttu-id="825eb-279">The typeProperties section is different for each activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="825eb-280">Transformation activities have just the type properties.</span><span class="sxs-lookup"><span data-stu-id="825eb-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="825eb-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="825eb-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span><span class="sxs-lookup"><span data-stu-id="825eb-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="825eb-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span><span class="sxs-lookup"><span data-stu-id="825eb-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="825eb-284">Sample copy pipeline</span><span class="sxs-lookup"><span data-stu-id="825eb-284">Sample copy pipeline</span></span>
<span data-ttu-id="825eb-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span><span class="sxs-lookup"><span data-stu-id="825eb-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="825eb-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="825eb-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

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

<span data-ttu-id="825eb-287">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="825eb-287">Note the following points:</span></span>

* <span data-ttu-id="825eb-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="825eb-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="825eb-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="825eb-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="825eb-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="825eb-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="825eb-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span><span class="sxs-lookup"><span data-stu-id="825eb-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="825eb-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="825eb-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="825eb-293">Sample transformation pipeline</span><span class="sxs-lookup"><span data-stu-id="825eb-293">Sample transformation pipeline</span></span>
<span data-ttu-id="825eb-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span><span class="sxs-lookup"><span data-stu-id="825eb-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="825eb-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="825eb-296">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="825eb-296">Note the following points:</span></span> 

* <span data-ttu-id="825eb-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="825eb-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="825eb-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="825eb-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="825eb-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="825eb-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="825eb-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="825eb-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="825eb-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="825eb-302">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-302">Linked service</span></span>
<span data-ttu-id="825eb-303">The high-level structure for a linked service definition is as follows:</span><span class="sxs-lookup"><span data-stu-id="825eb-303">The high-level structure for a linked service definition is as follows:</span></span>

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

<span data-ttu-id="825eb-304">Following table describe the properties within the activity JSON definition:</span><span class="sxs-lookup"><span data-stu-id="825eb-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="825eb-305">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-305">Property</span></span> | <span data-ttu-id="825eb-306">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-306">Description</span></span> | <span data-ttu-id="825eb-307">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="825eb-308">name</span><span class="sxs-lookup"><span data-stu-id="825eb-308">name</span></span> | <span data-ttu-id="825eb-309">Name of the linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-309">Name of the linked service.</span></span> | <span data-ttu-id="825eb-310">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-310">Yes</span></span> | 
| <span data-ttu-id="825eb-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="825eb-311">properties - type</span></span> | <span data-ttu-id="825eb-312">Type of the linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-312">Type of the linked service.</span></span> <span data-ttu-id="825eb-313">For example: Azure Storage, Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="825eb-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="825eb-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="825eb-314">typeProperties</span></span> | <span data-ttu-id="825eb-315">The typeProperties section has elements that are different for each data store or compute environment.</span><span class="sxs-lookup"><span data-stu-id="825eb-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="825eb-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span><span class="sxs-lookup"><span data-stu-id="825eb-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="825eb-317">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-317">Dataset</span></span> 
<span data-ttu-id="825eb-318">A dataset in Azure Data Factory is defined as follows:</span><span class="sxs-lookup"><span data-stu-id="825eb-318">A dataset in Azure Data Factory is defined as follows:</span></span>

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

<span data-ttu-id="825eb-319">The following table describes properties in the above JSON:</span><span class="sxs-lookup"><span data-stu-id="825eb-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="825eb-320">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-320">Property</span></span> | <span data-ttu-id="825eb-321">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-321">Description</span></span> | <span data-ttu-id="825eb-322">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-322">Required</span></span> | <span data-ttu-id="825eb-323">Default</span><span class="sxs-lookup"><span data-stu-id="825eb-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-324">name</span><span class="sxs-lookup"><span data-stu-id="825eb-324">name</span></span> | <span data-ttu-id="825eb-325">Name of the dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-325">Name of the dataset.</span></span> <span data-ttu-id="825eb-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span><span class="sxs-lookup"><span data-stu-id="825eb-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="825eb-327">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-327">Yes</span></span> |<span data-ttu-id="825eb-328">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-328">NA</span></span> |
| <span data-ttu-id="825eb-329">type</span><span class="sxs-lookup"><span data-stu-id="825eb-329">type</span></span> | <span data-ttu-id="825eb-330">Type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-330">Type of the dataset.</span></span> <span data-ttu-id="825eb-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="825eb-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="825eb-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="825eb-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="825eb-333">structure</span><span class="sxs-lookup"><span data-stu-id="825eb-333">structure</span></span> | <span data-ttu-id="825eb-334">Schema of the dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-334">Schema of the dataset.</span></span> <span data-ttu-id="825eb-335">It contains columns, their types, etc.</span><span class="sxs-lookup"><span data-stu-id="825eb-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="825eb-336">No</span><span class="sxs-lookup"><span data-stu-id="825eb-336">No</span></span> |<span data-ttu-id="825eb-337">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-337">NA</span></span> |
| <span data-ttu-id="825eb-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="825eb-338">typeProperties</span></span> | <span data-ttu-id="825eb-339">Properties corresponding to the selected type.</span><span class="sxs-lookup"><span data-stu-id="825eb-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="825eb-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span><span class="sxs-lookup"><span data-stu-id="825eb-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="825eb-341">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-341">Yes</span></span> |<span data-ttu-id="825eb-342">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-342">NA</span></span> |
| <span data-ttu-id="825eb-343">external</span><span class="sxs-lookup"><span data-stu-id="825eb-343">external</span></span> | <span data-ttu-id="825eb-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span><span class="sxs-lookup"><span data-stu-id="825eb-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="825eb-345">No</span><span class="sxs-lookup"><span data-stu-id="825eb-345">No</span></span> |<span data-ttu-id="825eb-346">false</span><span class="sxs-lookup"><span data-stu-id="825eb-346">false</span></span> |
| <span data-ttu-id="825eb-347">availability</span><span class="sxs-lookup"><span data-stu-id="825eb-347">availability</span></span> | <span data-ttu-id="825eb-348">Defines the processing window or the slicing model for the dataset production.</span><span class="sxs-lookup"><span data-stu-id="825eb-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="825eb-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="825eb-350">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-350">Yes</span></span> |<span data-ttu-id="825eb-351">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-351">NA</span></span> |
| <span data-ttu-id="825eb-352">policy</span><span class="sxs-lookup"><span data-stu-id="825eb-352">policy</span></span> |<span data-ttu-id="825eb-353">Defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="825eb-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="825eb-354">For details, see [Dataset Policy](#Policy) section.</span><span class="sxs-lookup"><span data-stu-id="825eb-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="825eb-355">No</span><span class="sxs-lookup"><span data-stu-id="825eb-355">No</span></span> |<span data-ttu-id="825eb-356">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-356">NA</span></span> |

<span data-ttu-id="825eb-357">Each column in the **structure** section contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="825eb-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="825eb-358">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-358">Property</span></span> | <span data-ttu-id="825eb-359">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-359">Description</span></span> | <span data-ttu-id="825eb-360">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-361">name</span><span class="sxs-lookup"><span data-stu-id="825eb-361">name</span></span> |<span data-ttu-id="825eb-362">Name of the column.</span><span class="sxs-lookup"><span data-stu-id="825eb-362">Name of the column.</span></span> |<span data-ttu-id="825eb-363">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-363">Yes</span></span> |
| <span data-ttu-id="825eb-364">type</span><span class="sxs-lookup"><span data-stu-id="825eb-364">type</span></span> |<span data-ttu-id="825eb-365">Data type of the column.</span><span class="sxs-lookup"><span data-stu-id="825eb-365">Data type of the column.</span></span>  |<span data-ttu-id="825eb-366">No</span><span class="sxs-lookup"><span data-stu-id="825eb-366">No</span></span> |
| <span data-ttu-id="825eb-367">culture</span><span class="sxs-lookup"><span data-stu-id="825eb-367">culture</span></span> |<span data-ttu-id="825eb-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="825eb-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="825eb-369">Default is `en-us`.</span><span class="sxs-lookup"><span data-stu-id="825eb-369">Default is `en-us`.</span></span> |<span data-ttu-id="825eb-370">No</span><span class="sxs-lookup"><span data-stu-id="825eb-370">No</span></span> |
| <span data-ttu-id="825eb-371">format</span><span class="sxs-lookup"><span data-stu-id="825eb-371">format</span></span> |<span data-ttu-id="825eb-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="825eb-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="825eb-373">No</span><span class="sxs-lookup"><span data-stu-id="825eb-373">No</span></span> |

<span data-ttu-id="825eb-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span><span class="sxs-lookup"><span data-stu-id="825eb-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="825eb-375">The following table describes properties you can use in the **availability** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="825eb-376">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-376">Property</span></span> | <span data-ttu-id="825eb-377">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-377">Description</span></span> | <span data-ttu-id="825eb-378">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-378">Required</span></span> | <span data-ttu-id="825eb-379">Default</span><span class="sxs-lookup"><span data-stu-id="825eb-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-380">frequency</span><span class="sxs-lookup"><span data-stu-id="825eb-380">frequency</span></span> |<span data-ttu-id="825eb-381">Specifies the time unit for dataset slice production.</span><span class="sxs-lookup"><span data-stu-id="825eb-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="825eb-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span><span class="sxs-lookup"><span data-stu-id="825eb-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="825eb-383">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-383">Yes</span></span> |<span data-ttu-id="825eb-384">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-384">NA</span></span> |
| <span data-ttu-id="825eb-385">interval</span><span class="sxs-lookup"><span data-stu-id="825eb-385">interval</span></span> |<span data-ttu-id="825eb-386">Specifies a multiplier for frequency</span><span class="sxs-lookup"><span data-stu-id="825eb-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="825eb-387">”Frequency x interval” determines how often the slice is produced.</span><span class="sxs-lookup"><span data-stu-id="825eb-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="825eb-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="825eb-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="825eb-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span><span class="sxs-lookup"><span data-stu-id="825eb-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="825eb-390">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-390">Yes</span></span> |<span data-ttu-id="825eb-391">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-391">NA</span></span> |
| <span data-ttu-id="825eb-392">style</span><span class="sxs-lookup"><span data-stu-id="825eb-392">style</span></span> |<span data-ttu-id="825eb-393">Specifies whether the slice should be produced at the start/end of the interval.</span><span class="sxs-lookup"><span data-stu-id="825eb-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="825eb-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="825eb-394">StartOfInterval</span></span></li><li><span data-ttu-id="825eb-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="825eb-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="825eb-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span><span class="sxs-lookup"><span data-stu-id="825eb-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="825eb-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span><span class="sxs-lookup"><span data-stu-id="825eb-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="825eb-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span><span class="sxs-lookup"><span data-stu-id="825eb-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="825eb-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span><span class="sxs-lookup"><span data-stu-id="825eb-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="825eb-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span><span class="sxs-lookup"><span data-stu-id="825eb-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="825eb-401">No</span><span class="sxs-lookup"><span data-stu-id="825eb-401">No</span></span> |<span data-ttu-id="825eb-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="825eb-402">EndOfInterval</span></span> |
| <span data-ttu-id="825eb-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="825eb-403">anchorDateTime</span></span> |<span data-ttu-id="825eb-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span><span class="sxs-lookup"><span data-stu-id="825eb-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="825eb-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span><span class="sxs-lookup"><span data-stu-id="825eb-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="825eb-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span><span class="sxs-lookup"><span data-stu-id="825eb-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="825eb-407">No</span><span class="sxs-lookup"><span data-stu-id="825eb-407">No</span></span> |<span data-ttu-id="825eb-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="825eb-408">01/01/0001</span></span> |
| <span data-ttu-id="825eb-409">offset</span><span class="sxs-lookup"><span data-stu-id="825eb-409">offset</span></span> |<span data-ttu-id="825eb-410">Timespan by which the start and end of all dataset slices are shifted.</span><span class="sxs-lookup"><span data-stu-id="825eb-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="825eb-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span><span class="sxs-lookup"><span data-stu-id="825eb-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="825eb-412">No</span><span class="sxs-lookup"><span data-stu-id="825eb-412">No</span></span> |<span data-ttu-id="825eb-413">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-413">NA</span></span> |

<span data-ttu-id="825eb-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span><span class="sxs-lookup"><span data-stu-id="825eb-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="825eb-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="825eb-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="825eb-416">Policy Name</span><span class="sxs-lookup"><span data-stu-id="825eb-416">Policy Name</span></span> | <span data-ttu-id="825eb-417">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-417">Description</span></span> | <span data-ttu-id="825eb-418">Applied To</span><span class="sxs-lookup"><span data-stu-id="825eb-418">Applied To</span></span> | <span data-ttu-id="825eb-419">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-419">Required</span></span> | <span data-ttu-id="825eb-420">Default</span><span class="sxs-lookup"><span data-stu-id="825eb-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="825eb-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="825eb-421">minimumSizeMB</span></span> |<span data-ttu-id="825eb-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span><span class="sxs-lookup"><span data-stu-id="825eb-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="825eb-423">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="825eb-423">Azure Blob</span></span> |<span data-ttu-id="825eb-424">No</span><span class="sxs-lookup"><span data-stu-id="825eb-424">No</span></span> |<span data-ttu-id="825eb-425">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-425">NA</span></span> |
| <span data-ttu-id="825eb-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="825eb-426">minimumRows</span></span> |<span data-ttu-id="825eb-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span><span class="sxs-lookup"><span data-stu-id="825eb-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="825eb-428">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="825eb-428">Azure SQL Database</span></span></li><li><span data-ttu-id="825eb-429">Azure Table</span><span class="sxs-lookup"><span data-stu-id="825eb-429">Azure Table</span></span></li></ul> |<span data-ttu-id="825eb-430">No</span><span class="sxs-lookup"><span data-stu-id="825eb-430">No</span></span> |<span data-ttu-id="825eb-431">NA</span><span class="sxs-lookup"><span data-stu-id="825eb-431">NA</span></span> |

<span data-ttu-id="825eb-432">**Example:**</span><span class="sxs-lookup"><span data-stu-id="825eb-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="825eb-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span><span class="sxs-lookup"><span data-stu-id="825eb-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="825eb-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span><span class="sxs-lookup"><span data-stu-id="825eb-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="825eb-435">Name</span><span class="sxs-lookup"><span data-stu-id="825eb-435">Name</span></span> | <span data-ttu-id="825eb-436">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-436">Description</span></span> | <span data-ttu-id="825eb-437">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-437">Required</span></span> | <span data-ttu-id="825eb-438">Default Value</span><span class="sxs-lookup"><span data-stu-id="825eb-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="825eb-439">dataDelay</span></span> |<span data-ttu-id="825eb-440">Time to delay the check on the availability of the external data for the given slice.</span><span class="sxs-lookup"><span data-stu-id="825eb-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="825eb-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span><span class="sxs-lookup"><span data-stu-id="825eb-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="825eb-442">Only applies to the present time.</span><span class="sxs-lookup"><span data-stu-id="825eb-442">Only applies to the present time.</span></span>  <span data-ttu-id="825eb-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span><span class="sxs-lookup"><span data-stu-id="825eb-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="825eb-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span><span class="sxs-lookup"><span data-stu-id="825eb-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="825eb-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="825eb-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="825eb-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="825eb-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="825eb-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="825eb-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="825eb-448">For 1 day and 4 hours, specify 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="825eb-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="825eb-449">No</span><span class="sxs-lookup"><span data-stu-id="825eb-449">No</span></span> |<span data-ttu-id="825eb-450">0</span><span class="sxs-lookup"><span data-stu-id="825eb-450">0</span></span> |
| <span data-ttu-id="825eb-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="825eb-451">retryInterval</span></span> |<span data-ttu-id="825eb-452">The wait time between a failure and the next retry attempt.</span><span class="sxs-lookup"><span data-stu-id="825eb-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="825eb-453">If a try fails, the next try is after retryInterval.</span><span class="sxs-lookup"><span data-stu-id="825eb-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="825eb-454">If it is 1:00 PM right now, we begin the first try.</span><span class="sxs-lookup"><span data-stu-id="825eb-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="825eb-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="825eb-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="825eb-456">For slices in the past, there is no delay.</span><span class="sxs-lookup"><span data-stu-id="825eb-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="825eb-457">The retry happens immediately.</span><span class="sxs-lookup"><span data-stu-id="825eb-457">The retry happens immediately.</span></span> |<span data-ttu-id="825eb-458">No</span><span class="sxs-lookup"><span data-stu-id="825eb-458">No</span></span> |<span data-ttu-id="825eb-459">00:01:00 (1 minute)</span><span class="sxs-lookup"><span data-stu-id="825eb-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="825eb-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="825eb-460">retryTimeout</span></span> |<span data-ttu-id="825eb-461">The timeout for each retry attempt.</span><span class="sxs-lookup"><span data-stu-id="825eb-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="825eb-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="825eb-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="825eb-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span><span class="sxs-lookup"><span data-stu-id="825eb-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="825eb-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span><span class="sxs-lookup"><span data-stu-id="825eb-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="825eb-465">No</span><span class="sxs-lookup"><span data-stu-id="825eb-465">No</span></span> |<span data-ttu-id="825eb-466">00:10:00 (10 minutes)</span><span class="sxs-lookup"><span data-stu-id="825eb-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="825eb-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="825eb-467">maximumRetry</span></span> |<span data-ttu-id="825eb-468">Number of times to check for the availability of the external data.</span><span class="sxs-lookup"><span data-stu-id="825eb-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="825eb-469">The allowed maximum value is 10.</span><span class="sxs-lookup"><span data-stu-id="825eb-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="825eb-470">No</span><span class="sxs-lookup"><span data-stu-id="825eb-470">No</span></span> |<span data-ttu-id="825eb-471">3</span><span class="sxs-lookup"><span data-stu-id="825eb-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="825eb-472">DATA STORES</span><span class="sxs-lookup"><span data-stu-id="825eb-472">DATA STORES</span></span>
<span data-ttu-id="825eb-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span><span class="sxs-lookup"><span data-stu-id="825eb-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="825eb-474">This section provides details about JSON elements that are specific to each data store.</span><span class="sxs-lookup"><span data-stu-id="825eb-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="825eb-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span><span class="sxs-lookup"><span data-stu-id="825eb-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="825eb-476">This section provides details about JSON elements that are specific to each data store.</span><span class="sxs-lookup"><span data-stu-id="825eb-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="825eb-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span><span class="sxs-lookup"><span data-stu-id="825eb-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="825eb-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="825eb-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="825eb-480">Category</span><span class="sxs-lookup"><span data-stu-id="825eb-480">Category</span></span> | <span data-ttu-id="825eb-481">Data store</span><span class="sxs-lookup"><span data-stu-id="825eb-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="825eb-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="825eb-482">**Azure**</span></span> |[<span data-ttu-id="825eb-483">Azure Blob storage</span><span class="sxs-lookup"><span data-stu-id="825eb-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="825eb-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="825eb-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="825eb-485">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="825eb-485">Azure DocumentDB</span></span>](#azure-documentdb) |
| &nbsp; |[<span data-ttu-id="825eb-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="825eb-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="825eb-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="825eb-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="825eb-488">Azure Search</span><span class="sxs-lookup"><span data-stu-id="825eb-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="825eb-489">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="825eb-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="825eb-490">**Databases**</span><span class="sxs-lookup"><span data-stu-id="825eb-490">**Databases**</span></span> |[<span data-ttu-id="825eb-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="825eb-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="825eb-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="825eb-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="825eb-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="825eb-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="825eb-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="825eb-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="825eb-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="825eb-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="825eb-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="825eb-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="825eb-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="825eb-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="825eb-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="825eb-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="825eb-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="825eb-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="825eb-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="825eb-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="825eb-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="825eb-501">**NoSQL**</span></span> |[<span data-ttu-id="825eb-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="825eb-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="825eb-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="825eb-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="825eb-504">**File**</span><span class="sxs-lookup"><span data-stu-id="825eb-504">**File**</span></span> |[<span data-ttu-id="825eb-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="825eb-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="825eb-506">File System</span><span class="sxs-lookup"><span data-stu-id="825eb-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="825eb-507">FTP</span><span class="sxs-lookup"><span data-stu-id="825eb-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="825eb-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="825eb-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="825eb-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="825eb-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="825eb-510">**Others**</span><span class="sxs-lookup"><span data-stu-id="825eb-510">**Others**</span></span> |[<span data-ttu-id="825eb-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="825eb-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="825eb-512">OData</span><span class="sxs-lookup"><span data-stu-id="825eb-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="825eb-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="825eb-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="825eb-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="825eb-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="825eb-515">Web Table</span><span class="sxs-lookup"><span data-stu-id="825eb-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="825eb-516">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="825eb-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-517">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-517">Linked service</span></span>
<span data-ttu-id="825eb-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="825eb-519">Azure Storage Linked Service</span><span class="sxs-lookup"><span data-stu-id="825eb-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="825eb-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="825eb-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="825eb-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="825eb-522">Then, you can specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-523">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-523">Property</span></span> | <span data-ttu-id="825eb-524">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-524">Description</span></span> | <span data-ttu-id="825eb-525">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-526">connectionString</span></span> |<span data-ttu-id="825eb-527">Specify information needed to connect to Azure storage for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="825eb-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="825eb-528">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="825eb-529">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="825eb-530">Azure Storage SAS Linked Service</span><span class="sxs-lookup"><span data-stu-id="825eb-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="825eb-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="825eb-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="825eb-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span><span class="sxs-lookup"><span data-stu-id="825eb-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="825eb-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="825eb-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="825eb-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="825eb-535">Then, you can specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="825eb-536">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-536">Property</span></span> | <span data-ttu-id="825eb-537">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-537">Description</span></span> | <span data-ttu-id="825eb-538">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="825eb-539">sasUri</span></span> |<span data-ttu-id="825eb-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span><span class="sxs-lookup"><span data-stu-id="825eb-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="825eb-541">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="825eb-542">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-542">Example</span></span>

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

<span data-ttu-id="825eb-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-544">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-544">Dataset</span></span>
<span data-ttu-id="825eb-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="825eb-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="825eb-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-547">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-547">Property</span></span> | <span data-ttu-id="825eb-548">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-548">Description</span></span> | <span data-ttu-id="825eb-549">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="825eb-550">folderPath</span></span> |<span data-ttu-id="825eb-551">Path to the container and folder in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="825eb-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="825eb-552">Example: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="825eb-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="825eb-553">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-553">Yes</span></span> |
| <span data-ttu-id="825eb-554">fileName</span><span class="sxs-lookup"><span data-stu-id="825eb-554">fileName</span></span> |<span data-ttu-id="825eb-555">Name of the blob.</span><span class="sxs-lookup"><span data-stu-id="825eb-555">Name of the blob.</span></span> <span data-ttu-id="825eb-556">fileName is optional and case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="825eb-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span><span class="sxs-lookup"><span data-stu-id="825eb-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="825eb-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="825eb-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="825eb-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="825eb-560">No</span><span class="sxs-lookup"><span data-stu-id="825eb-560">No</span></span> |
| <span data-ttu-id="825eb-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="825eb-561">partitionedBy</span></span> |<span data-ttu-id="825eb-562">partitionedBy is an optional property.</span><span class="sxs-lookup"><span data-stu-id="825eb-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="825eb-563">You can use it to specify a dynamic folderPath and filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="825eb-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="825eb-564">For example, folderPath can be parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="825eb-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="825eb-565">No</span><span class="sxs-lookup"><span data-stu-id="825eb-565">No</span></span> |
| <span data-ttu-id="825eb-566">format</span><span class="sxs-lookup"><span data-stu-id="825eb-566">format</span></span> | <span data-ttu-id="825eb-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="825eb-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="825eb-568">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="825eb-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="825eb-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="825eb-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="825eb-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="825eb-571">No</span><span class="sxs-lookup"><span data-stu-id="825eb-571">No</span></span> |
| <span data-ttu-id="825eb-572">compression</span><span class="sxs-lookup"><span data-stu-id="825eb-572">compression</span></span> | <span data-ttu-id="825eb-573">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="825eb-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="825eb-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="825eb-575">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="825eb-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="825eb-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="825eb-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="825eb-577">No</span><span class="sxs-lookup"><span data-stu-id="825eb-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-578">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-578">Example</span></span>

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


<span data-ttu-id="825eb-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="825eb-580">BlobSource in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="825eb-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the \*\*source \*\*section:</span><span class="sxs-lookup"><span data-stu-id="825eb-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the \*\*source \*\*section:</span></span>

| <span data-ttu-id="825eb-582">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-582">Property</span></span> | <span data-ttu-id="825eb-583">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-583">Description</span></span> | <span data-ttu-id="825eb-584">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-584">Allowed values</span></span> | <span data-ttu-id="825eb-585">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-586">recursive</span><span class="sxs-lookup"><span data-stu-id="825eb-586">recursive</span></span> |<span data-ttu-id="825eb-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="825eb-588">True (default value), False</span><span class="sxs-lookup"><span data-stu-id="825eb-588">True (default value), False</span></span> |<span data-ttu-id="825eb-589">No</span><span class="sxs-lookup"><span data-stu-id="825eb-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="825eb-590">Example: BlobSource\*\*</span><span class="sxs-lookup"><span data-stu-id="825eb-590">Example: BlobSource\*\*</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="825eb-591">BlobSink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="825eb-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-593">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-593">Property</span></span> | <span data-ttu-id="825eb-594">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-594">Description</span></span> | <span data-ttu-id="825eb-595">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-595">Allowed values</span></span> | <span data-ttu-id="825eb-596">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="825eb-597">copyBehavior</span></span> |<span data-ttu-id="825eb-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span><span class="sxs-lookup"><span data-stu-id="825eb-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="825eb-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="825eb-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="825eb-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="825eb-602">The target files have auto generated name.</span><span class="sxs-lookup"><span data-stu-id="825eb-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="825eb-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="825eb-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="825eb-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="825eb-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="825eb-605">No</span><span class="sxs-lookup"><span data-stu-id="825eb-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="825eb-606">Example: BlobSink</span><span class="sxs-lookup"><span data-stu-id="825eb-606">Example: BlobSink</span></span>

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

<span data-ttu-id="825eb-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="825eb-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="825eb-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-609">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-609">Linked service</span></span>
<span data-ttu-id="825eb-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-611">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-611">Property</span></span> | <span data-ttu-id="825eb-612">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-612">Description</span></span> | <span data-ttu-id="825eb-613">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-614">type</span><span class="sxs-lookup"><span data-stu-id="825eb-614">type</span></span> | <span data-ttu-id="825eb-615">The type property must be set to: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="825eb-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="825eb-616">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-616">Yes</span></span> |
| <span data-ttu-id="825eb-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="825eb-617">dataLakeStoreUri</span></span> | <span data-ttu-id="825eb-618">Specify information about the Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="825eb-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="825eb-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="825eb-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="825eb-620">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-620">Yes</span></span> |
| <span data-ttu-id="825eb-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="825eb-621">subscriptionId</span></span> | <span data-ttu-id="825eb-622">Azure subscription Id to which Data Lake Store belongs.</span><span class="sxs-lookup"><span data-stu-id="825eb-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="825eb-623">Required for sink</span><span class="sxs-lookup"><span data-stu-id="825eb-623">Required for sink</span></span> |
| <span data-ttu-id="825eb-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="825eb-624">resourceGroupName</span></span> | <span data-ttu-id="825eb-625">Azure resource group name to which Data Lake Store belongs.</span><span class="sxs-lookup"><span data-stu-id="825eb-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="825eb-626">Required for sink</span><span class="sxs-lookup"><span data-stu-id="825eb-626">Required for sink</span></span> |
| <span data-ttu-id="825eb-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="825eb-627">servicePrincipalId</span></span> | <span data-ttu-id="825eb-628">Specify the application's client ID.</span><span class="sxs-lookup"><span data-stu-id="825eb-628">Specify the application's client ID.</span></span> | <span data-ttu-id="825eb-629">Yes (for service principal authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="825eb-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="825eb-630">servicePrincipalKey</span></span> | <span data-ttu-id="825eb-631">Specify the application's key.</span><span class="sxs-lookup"><span data-stu-id="825eb-631">Specify the application's key.</span></span> | <span data-ttu-id="825eb-632">Yes (for service principal authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="825eb-633">tenant</span><span class="sxs-lookup"><span data-stu-id="825eb-633">tenant</span></span> | <span data-ttu-id="825eb-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span><span class="sxs-lookup"><span data-stu-id="825eb-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="825eb-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="825eb-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="825eb-636">Yes (for service principal authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="825eb-637">authorization</span><span class="sxs-lookup"><span data-stu-id="825eb-637">authorization</span></span> | <span data-ttu-id="825eb-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span><span class="sxs-lookup"><span data-stu-id="825eb-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="825eb-639">Yes (for user credential authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="825eb-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="825eb-640">sessionId</span></span> | <span data-ttu-id="825eb-641">OAuth session id from the OAuth authorization session.</span><span class="sxs-lookup"><span data-stu-id="825eb-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="825eb-642">Each session id is unique and may only be used once.</span><span class="sxs-lookup"><span data-stu-id="825eb-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="825eb-643">This setting is automatically generated when you use Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="825eb-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="825eb-644">Yes (for user credential authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="825eb-645">Example: using service principal authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="825eb-646">Example: using user credential authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="825eb-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-648">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-648">Dataset</span></span>
<span data-ttu-id="825eb-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-650">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-650">Property</span></span> | <span data-ttu-id="825eb-651">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-651">Description</span></span> | <span data-ttu-id="825eb-652">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="825eb-653">folderPath</span></span> |<span data-ttu-id="825eb-654">Path to the container and folder in the Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="825eb-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="825eb-655">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-655">Yes</span></span> |
| <span data-ttu-id="825eb-656">fileName</span><span class="sxs-lookup"><span data-stu-id="825eb-656">fileName</span></span> |<span data-ttu-id="825eb-657">Name of the file in the Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="825eb-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="825eb-658">fileName is optional and case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="825eb-659">If you specify a filename, the activity (including Copy) works on the specific file.</span><span class="sxs-lookup"><span data-stu-id="825eb-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="825eb-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="825eb-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="825eb-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="825eb-662">No</span><span class="sxs-lookup"><span data-stu-id="825eb-662">No</span></span> |
| <span data-ttu-id="825eb-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="825eb-663">partitionedBy</span></span> |<span data-ttu-id="825eb-664">partitionedBy is an optional property.</span><span class="sxs-lookup"><span data-stu-id="825eb-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="825eb-665">You can use it to specify a dynamic folderPath and filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="825eb-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="825eb-666">For example, folderPath can be parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="825eb-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="825eb-667">No</span><span class="sxs-lookup"><span data-stu-id="825eb-667">No</span></span> |
| <span data-ttu-id="825eb-668">format</span><span class="sxs-lookup"><span data-stu-id="825eb-668">format</span></span> | <span data-ttu-id="825eb-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="825eb-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="825eb-670">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="825eb-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="825eb-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="825eb-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="825eb-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="825eb-673">No</span><span class="sxs-lookup"><span data-stu-id="825eb-673">No</span></span> |
| <span data-ttu-id="825eb-674">compression</span><span class="sxs-lookup"><span data-stu-id="825eb-674">compression</span></span> | <span data-ttu-id="825eb-675">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="825eb-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="825eb-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="825eb-677">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="825eb-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="825eb-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="825eb-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="825eb-679">No</span><span class="sxs-lookup"><span data-stu-id="825eb-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-680">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-680">Example</span></span>
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

<span data-ttu-id="825eb-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="825eb-682">Azure Data Lake Store Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="825eb-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="825eb-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="825eb-685">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-685">Property</span></span> | <span data-ttu-id="825eb-686">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-686">Description</span></span> | <span data-ttu-id="825eb-687">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-687">Allowed values</span></span> | <span data-ttu-id="825eb-688">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-689">recursive</span><span class="sxs-lookup"><span data-stu-id="825eb-689">recursive</span></span> |<span data-ttu-id="825eb-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="825eb-691">True (default value), False</span><span class="sxs-lookup"><span data-stu-id="825eb-691">True (default value), False</span></span> |<span data-ttu-id="825eb-692">No</span><span class="sxs-lookup"><span data-stu-id="825eb-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="825eb-693">Example: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="825eb-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="825eb-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="825eb-695">Azure Data Lake Store Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-697">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-697">Property</span></span> | <span data-ttu-id="825eb-698">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-698">Description</span></span> | <span data-ttu-id="825eb-699">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-699">Allowed values</span></span> | <span data-ttu-id="825eb-700">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="825eb-701">copyBehavior</span></span> |<span data-ttu-id="825eb-702">Specifies the copy behavior.</span><span class="sxs-lookup"><span data-stu-id="825eb-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="825eb-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="825eb-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="825eb-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="825eb-706">The target files are created with auto generated name.</span><span class="sxs-lookup"><span data-stu-id="825eb-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="825eb-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="825eb-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="825eb-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="825eb-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="825eb-709">No</span><span class="sxs-lookup"><span data-stu-id="825eb-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="825eb-710">Example: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="825eb-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="825eb-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-documentdb"></a><span data-ttu-id="825eb-712">Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="825eb-712">Azure DocumentDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-713">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-713">Linked service</span></span>
<span data-ttu-id="825eb-714">To define an Azure DocumentDB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-714">To define an Azure DocumentDB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-715">**Property**</span><span class="sxs-lookup"><span data-stu-id="825eb-715">**Property**</span></span> | <span data-ttu-id="825eb-716">**Description**</span><span class="sxs-lookup"><span data-stu-id="825eb-716">**Description**</span></span> | <span data-ttu-id="825eb-717">**Required**</span><span class="sxs-lookup"><span data-stu-id="825eb-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-718">connectionString</span></span> |<span data-ttu-id="825eb-719">Specify information needed to connect to Azure DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="825eb-719">Specify information needed to connect to Azure DocumentDB database.</span></span> |<span data-ttu-id="825eb-720">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-721">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-721">Example</span></span>

```json
{
    "name": "DocumentDbLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="825eb-722">For more information, see [DocumentDB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-722">For more information, see [DocumentDB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-723">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-723">Dataset</span></span>
<span data-ttu-id="825eb-724">To define an Azure DocumentDB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-724">To define an Azure DocumentDB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-725">**Property**</span><span class="sxs-lookup"><span data-stu-id="825eb-725">**Property**</span></span> | <span data-ttu-id="825eb-726">**Description**</span><span class="sxs-lookup"><span data-stu-id="825eb-726">**Description**</span></span> | <span data-ttu-id="825eb-727">**Required**</span><span class="sxs-lookup"><span data-stu-id="825eb-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="825eb-728">collectionName</span></span> |<span data-ttu-id="825eb-729">Name of the DocumentDB document collection.</span><span class="sxs-lookup"><span data-stu-id="825eb-729">Name of the DocumentDB document collection.</span></span> |<span data-ttu-id="825eb-730">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-731">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-731">Example</span></span>

```json
{
    "name": "PersonDocumentDbTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "DocumentDbLinkedService",
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
<span data-ttu-id="825eb-732">For more information, see [DocumentDB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-732">For more information, see [DocumentDB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="documentdb-collection-source-in-copy-activity"></a><span data-ttu-id="825eb-733">DocumentDB Collection Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-733">DocumentDB Collection Source in Copy Activity</span></span>
<span data-ttu-id="825eb-734">If you are copying data from an Azure DocumentDB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-734">If you are copying data from an Azure DocumentDB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-735">**Property**</span><span class="sxs-lookup"><span data-stu-id="825eb-735">**Property**</span></span> | <span data-ttu-id="825eb-736">**Description**</span><span class="sxs-lookup"><span data-stu-id="825eb-736">**Description**</span></span> | <span data-ttu-id="825eb-737">**Allowed values**</span><span class="sxs-lookup"><span data-stu-id="825eb-737">**Allowed values**</span></span> | <span data-ttu-id="825eb-738">**Required**</span><span class="sxs-lookup"><span data-stu-id="825eb-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-739">query</span><span class="sxs-lookup"><span data-stu-id="825eb-739">query</span></span> |<span data-ttu-id="825eb-740">Specify the query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-740">Specify the query to read data.</span></span> |<span data-ttu-id="825eb-741">Query string supported by DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="825eb-741">Query string supported by DocumentDB.</span></span> <br/><br/><span data-ttu-id="825eb-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="825eb-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="825eb-743">No</span><span class="sxs-lookup"><span data-stu-id="825eb-743">No</span></span> <br/><br/><span data-ttu-id="825eb-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="825eb-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="825eb-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="825eb-745">nestingSeparator</span></span> |<span data-ttu-id="825eb-746">Special character to indicate that the document is nested</span><span class="sxs-lookup"><span data-stu-id="825eb-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="825eb-747">Any character.</span><span class="sxs-lookup"><span data-stu-id="825eb-747">Any character.</span></span> <br/><br/><span data-ttu-id="825eb-748">DocumentDB is a NoSQL store for JSON documents, where nested structures are allowed.</span><span class="sxs-lookup"><span data-stu-id="825eb-748">DocumentDB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="825eb-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span><span class="sxs-lookup"><span data-stu-id="825eb-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="825eb-750">in the above examples.</span><span class="sxs-lookup"><span data-stu-id="825eb-750">in the above examples.</span></span> <span data-ttu-id="825eb-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="825eb-752">No</span><span class="sxs-lookup"><span data-stu-id="825eb-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-753">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-753">Example</span></span>

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
                "name": "PersonDocumentDbTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromDocDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="documentdb-collection-sink-in-copy-activity"></a><span data-ttu-id="825eb-754">DocumentDB Collection Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-754">DocumentDB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-755">If you are copying data to Azure DocumentDB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-755">If you are copying data to Azure DocumentDB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-756">**Property**</span><span class="sxs-lookup"><span data-stu-id="825eb-756">**Property**</span></span> | <span data-ttu-id="825eb-757">**Description**</span><span class="sxs-lookup"><span data-stu-id="825eb-757">**Description**</span></span> | <span data-ttu-id="825eb-758">**Allowed values**</span><span class="sxs-lookup"><span data-stu-id="825eb-758">**Allowed values**</span></span> | <span data-ttu-id="825eb-759">**Required**</span><span class="sxs-lookup"><span data-stu-id="825eb-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="825eb-760">nestingSeparator</span></span> |<span data-ttu-id="825eb-761">A special character in the source column name to indicate that nested document is needed.</span><span class="sxs-lookup"><span data-stu-id="825eb-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="825eb-762">For example above: `Name.First` in the output table produces the following JSON structure in the DocumentDB document:</span><span class="sxs-lookup"><span data-stu-id="825eb-762">For example above: `Name.First` in the output table produces the following JSON structure in the DocumentDB document:</span></span><br/><br/><span data-ttu-id="825eb-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="825eb-763">"Name": {</span></span><br/>    <span data-ttu-id="825eb-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="825eb-764">"First": "John"</span></span><br/><span data-ttu-id="825eb-765">},</span><span class="sxs-lookup"><span data-stu-id="825eb-765">},</span></span> |<span data-ttu-id="825eb-766">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="825eb-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="825eb-767">Default value is `.` (dot).</span><span class="sxs-lookup"><span data-stu-id="825eb-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="825eb-768">Character that is used to separate nesting levels.</span><span class="sxs-lookup"><span data-stu-id="825eb-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="825eb-769">Default value is `.` (dot).</span><span class="sxs-lookup"><span data-stu-id="825eb-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="825eb-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="825eb-770">writeBatchSize</span></span> |<span data-ttu-id="825eb-771">Number of parallel requests to DocumentDB service to create documents.</span><span class="sxs-lookup"><span data-stu-id="825eb-771">Number of parallel requests to DocumentDB service to create documents.</span></span><br/><br/><span data-ttu-id="825eb-772">You can fine-tune the performance when copying data to/from DocumentDB by using this property.</span><span class="sxs-lookup"><span data-stu-id="825eb-772">You can fine-tune the performance when copying data to/from DocumentDB by using this property.</span></span> <span data-ttu-id="825eb-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to DocumentDB are sent.</span><span class="sxs-lookup"><span data-stu-id="825eb-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to DocumentDB are sent.</span></span> <span data-ttu-id="825eb-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span><span class="sxs-lookup"><span data-stu-id="825eb-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="825eb-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span><span class="sxs-lookup"><span data-stu-id="825eb-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="825eb-776">Integer</span><span class="sxs-lookup"><span data-stu-id="825eb-776">Integer</span></span> |<span data-ttu-id="825eb-777">No (default: 5)</span><span class="sxs-lookup"><span data-stu-id="825eb-777">No (default: 5)</span></span> |
| <span data-ttu-id="825eb-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="825eb-778">writeBatchTimeout</span></span> |<span data-ttu-id="825eb-779">Wait time for the operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="825eb-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="825eb-780">timespan</span><span class="sxs-lookup"><span data-stu-id="825eb-780">timespan</span></span><br/><br/> <span data-ttu-id="825eb-781">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="825eb-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="825eb-782">No</span><span class="sxs-lookup"><span data-stu-id="825eb-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-783">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-783">Example</span></span>

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
                "name": "PersonDocumentDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToDocDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="825eb-784">For more information, see [DocumentDB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-784">For more information, see [DocumentDB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="825eb-785">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="825eb-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-786">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-786">Linked service</span></span>
<span data-ttu-id="825eb-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-788">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-788">Property</span></span> | <span data-ttu-id="825eb-789">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-789">Description</span></span> | <span data-ttu-id="825eb-790">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-791">connectionString</span></span> |<span data-ttu-id="825eb-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="825eb-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="825eb-793">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-794">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-794">Example</span></span>
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

<span data-ttu-id="825eb-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-796">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-796">Dataset</span></span>
<span data-ttu-id="825eb-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-798">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-798">Property</span></span> | <span data-ttu-id="825eb-799">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-799">Description</span></span> | <span data-ttu-id="825eb-800">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-801">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-801">tableName</span></span> |<span data-ttu-id="825eb-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="825eb-803">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-804">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-804">Example</span></span>

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
<span data-ttu-id="825eb-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="825eb-806">SQL Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="825eb-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-808">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-808">Property</span></span> | <span data-ttu-id="825eb-809">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-809">Description</span></span> | <span data-ttu-id="825eb-810">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-810">Allowed values</span></span> | <span data-ttu-id="825eb-811">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-812">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="825eb-812">sqlReaderQuery</span></span> |<span data-ttu-id="825eb-813">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-813">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-814">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-814">SQL query string.</span></span> <span data-ttu-id="825eb-815">Example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="825eb-816">No</span><span class="sxs-lookup"><span data-stu-id="825eb-816">No</span></span> |
| <span data-ttu-id="825eb-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="825eb-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="825eb-818">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="825eb-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="825eb-819">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-819">Name of the stored procedure.</span></span> |<span data-ttu-id="825eb-820">No</span><span class="sxs-lookup"><span data-stu-id="825eb-820">No</span></span> |
| <span data-ttu-id="825eb-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="825eb-821">storedProcedureParameters</span></span> |<span data-ttu-id="825eb-822">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="825eb-823">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="825eb-823">Name/value pairs.</span></span> <span data-ttu-id="825eb-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="825eb-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="825eb-825">No</span><span class="sxs-lookup"><span data-stu-id="825eb-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-826">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-826">Example</span></span>

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
<span data-ttu-id="825eb-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="825eb-828">SQL Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-830">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-830">Property</span></span> | <span data-ttu-id="825eb-831">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-831">Description</span></span> | <span data-ttu-id="825eb-832">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-832">Allowed values</span></span> | <span data-ttu-id="825eb-833">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="825eb-834">writeBatchTimeout</span></span> |<span data-ttu-id="825eb-835">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="825eb-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="825eb-836">timespan</span><span class="sxs-lookup"><span data-stu-id="825eb-836">timespan</span></span><br/><br/> <span data-ttu-id="825eb-837">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="825eb-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="825eb-838">No</span><span class="sxs-lookup"><span data-stu-id="825eb-838">No</span></span> |
| <span data-ttu-id="825eb-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="825eb-839">writeBatchSize</span></span> |<span data-ttu-id="825eb-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="825eb-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="825eb-841">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="825eb-841">Integer (number of rows)</span></span> |<span data-ttu-id="825eb-842">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="825eb-842">No (default: 10000)</span></span> |
| <span data-ttu-id="825eb-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="825eb-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="825eb-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="825eb-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="825eb-845">A query statement.</span><span class="sxs-lookup"><span data-stu-id="825eb-845">A query statement.</span></span> |<span data-ttu-id="825eb-846">No</span><span class="sxs-lookup"><span data-stu-id="825eb-846">No</span></span> |
| <span data-ttu-id="825eb-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="825eb-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="825eb-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="825eb-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="825eb-849">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="825eb-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="825eb-850">No</span><span class="sxs-lookup"><span data-stu-id="825eb-850">No</span></span> |
| <span data-ttu-id="825eb-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="825eb-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="825eb-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span><span class="sxs-lookup"><span data-stu-id="825eb-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="825eb-853">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-853">Name of the stored procedure.</span></span> |<span data-ttu-id="825eb-854">No</span><span class="sxs-lookup"><span data-stu-id="825eb-854">No</span></span> |
| <span data-ttu-id="825eb-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="825eb-855">storedProcedureParameters</span></span> |<span data-ttu-id="825eb-856">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="825eb-857">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="825eb-857">Name/value pairs.</span></span> <span data-ttu-id="825eb-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="825eb-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="825eb-859">No</span><span class="sxs-lookup"><span data-stu-id="825eb-859">No</span></span> |
| <span data-ttu-id="825eb-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="825eb-860">sqlWriterTableType</span></span> |<span data-ttu-id="825eb-861">Specify a table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="825eb-862">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="825eb-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="825eb-863">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="825eb-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="825eb-864">A table type name.</span><span class="sxs-lookup"><span data-stu-id="825eb-864">A table type name.</span></span> |<span data-ttu-id="825eb-865">No</span><span class="sxs-lookup"><span data-stu-id="825eb-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-866">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-866">Example</span></span>

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

<span data-ttu-id="825eb-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="825eb-868">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="825eb-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-869">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-869">Linked service</span></span>
<span data-ttu-id="825eb-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-871">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-871">Property</span></span> | <span data-ttu-id="825eb-872">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-872">Description</span></span> | <span data-ttu-id="825eb-873">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-874">connectionString</span></span> |<span data-ttu-id="825eb-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="825eb-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="825eb-876">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="825eb-877">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-877">Example</span></span>

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

<span data-ttu-id="825eb-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-879">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-879">Dataset</span></span>
<span data-ttu-id="825eb-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-881">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-881">Property</span></span> | <span data-ttu-id="825eb-882">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-882">Description</span></span> | <span data-ttu-id="825eb-883">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-884">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-884">tableName</span></span> |<span data-ttu-id="825eb-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="825eb-886">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-887">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-887">Example</span></span>

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

<span data-ttu-id="825eb-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="825eb-889">SQL DW Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="825eb-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-891">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-891">Property</span></span> | <span data-ttu-id="825eb-892">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-892">Description</span></span> | <span data-ttu-id="825eb-893">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-893">Allowed values</span></span> | <span data-ttu-id="825eb-894">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-895">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="825eb-895">sqlReaderQuery</span></span> |<span data-ttu-id="825eb-896">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-896">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-897">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-897">SQL query string.</span></span> <span data-ttu-id="825eb-898">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="825eb-899">No</span><span class="sxs-lookup"><span data-stu-id="825eb-899">No</span></span> |
| <span data-ttu-id="825eb-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="825eb-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="825eb-901">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="825eb-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="825eb-902">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-902">Name of the stored procedure.</span></span> |<span data-ttu-id="825eb-903">No</span><span class="sxs-lookup"><span data-stu-id="825eb-903">No</span></span> |
| <span data-ttu-id="825eb-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="825eb-904">storedProcedureParameters</span></span> |<span data-ttu-id="825eb-905">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="825eb-906">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="825eb-906">Name/value pairs.</span></span> <span data-ttu-id="825eb-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="825eb-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="825eb-908">No</span><span class="sxs-lookup"><span data-stu-id="825eb-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-909">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-909">Example</span></span>

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

<span data-ttu-id="825eb-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="825eb-911">SQL DW Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-913">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-913">Property</span></span> | <span data-ttu-id="825eb-914">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-914">Description</span></span> | <span data-ttu-id="825eb-915">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-915">Allowed values</span></span> | <span data-ttu-id="825eb-916">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="825eb-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="825eb-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="825eb-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="825eb-919">A query statement.</span><span class="sxs-lookup"><span data-stu-id="825eb-919">A query statement.</span></span> |<span data-ttu-id="825eb-920">No</span><span class="sxs-lookup"><span data-stu-id="825eb-920">No</span></span> |
| <span data-ttu-id="825eb-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="825eb-921">allowPolyBase</span></span> |<span data-ttu-id="825eb-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span><span class="sxs-lookup"><span data-stu-id="825eb-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="825eb-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="825eb-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="825eb-924">True</span><span class="sxs-lookup"><span data-stu-id="825eb-924">True</span></span> <br/><span data-ttu-id="825eb-925">False (default)</span><span class="sxs-lookup"><span data-stu-id="825eb-925">False (default)</span></span> |<span data-ttu-id="825eb-926">No</span><span class="sxs-lookup"><span data-stu-id="825eb-926">No</span></span> |
| <span data-ttu-id="825eb-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="825eb-927">polyBaseSettings</span></span> |<span data-ttu-id="825eb-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span><span class="sxs-lookup"><span data-stu-id="825eb-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="825eb-929">No</span><span class="sxs-lookup"><span data-stu-id="825eb-929">No</span></span> |
| <span data-ttu-id="825eb-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="825eb-930">rejectValue</span></span> |<span data-ttu-id="825eb-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span><span class="sxs-lookup"><span data-stu-id="825eb-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="825eb-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span><span class="sxs-lookup"><span data-stu-id="825eb-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="825eb-933">0 (default), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="825eb-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="825eb-934">No</span><span class="sxs-lookup"><span data-stu-id="825eb-934">No</span></span> |
| <span data-ttu-id="825eb-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="825eb-935">rejectType</span></span> |<span data-ttu-id="825eb-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span><span class="sxs-lookup"><span data-stu-id="825eb-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="825eb-937">Value (default), Percentage</span><span class="sxs-lookup"><span data-stu-id="825eb-937">Value (default), Percentage</span></span> |<span data-ttu-id="825eb-938">No</span><span class="sxs-lookup"><span data-stu-id="825eb-938">No</span></span> |
| <span data-ttu-id="825eb-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="825eb-939">rejectSampleValue</span></span> |<span data-ttu-id="825eb-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span><span class="sxs-lookup"><span data-stu-id="825eb-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="825eb-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="825eb-941">1, 2, …</span></span> |<span data-ttu-id="825eb-942">Yes, if **rejectType** is **percentage**</span><span class="sxs-lookup"><span data-stu-id="825eb-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="825eb-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="825eb-943">useTypeDefault</span></span> |<span data-ttu-id="825eb-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span><span class="sxs-lookup"><span data-stu-id="825eb-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="825eb-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="825eb-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="825eb-946">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="825eb-946">True, False (default)</span></span> |<span data-ttu-id="825eb-947">No</span><span class="sxs-lookup"><span data-stu-id="825eb-947">No</span></span> |
| <span data-ttu-id="825eb-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="825eb-948">writeBatchSize</span></span> |<span data-ttu-id="825eb-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="825eb-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="825eb-950">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="825eb-950">Integer (number of rows)</span></span> |<span data-ttu-id="825eb-951">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="825eb-951">No (default: 10000)</span></span> |
| <span data-ttu-id="825eb-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="825eb-952">writeBatchTimeout</span></span> |<span data-ttu-id="825eb-953">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="825eb-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="825eb-954">timespan</span><span class="sxs-lookup"><span data-stu-id="825eb-954">timespan</span></span><br/><br/> <span data-ttu-id="825eb-955">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="825eb-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="825eb-956">No</span><span class="sxs-lookup"><span data-stu-id="825eb-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-957">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-957">Example</span></span>

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

<span data-ttu-id="825eb-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="825eb-959">Azure Search</span><span class="sxs-lookup"><span data-stu-id="825eb-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-960">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-960">Linked service</span></span>
<span data-ttu-id="825eb-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-962">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-962">Property</span></span> | <span data-ttu-id="825eb-963">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-963">Description</span></span> | <span data-ttu-id="825eb-964">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="825eb-965">url</span><span class="sxs-lookup"><span data-stu-id="825eb-965">url</span></span> | <span data-ttu-id="825eb-966">URL for the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="825eb-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="825eb-967">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-967">Yes</span></span> |
| <span data-ttu-id="825eb-968">key</span><span class="sxs-lookup"><span data-stu-id="825eb-968">key</span></span> | <span data-ttu-id="825eb-969">Admin key for the Azure Search service.</span><span class="sxs-lookup"><span data-stu-id="825eb-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="825eb-970">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-971">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-971">Example</span></span>

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

<span data-ttu-id="825eb-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-973">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-973">Dataset</span></span>
<span data-ttu-id="825eb-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-975">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-975">Property</span></span> | <span data-ttu-id="825eb-976">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-976">Description</span></span> | <span data-ttu-id="825eb-977">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="825eb-978">type</span><span class="sxs-lookup"><span data-stu-id="825eb-978">type</span></span> | <span data-ttu-id="825eb-979">The type property must be set to **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="825eb-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="825eb-980">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-980">Yes</span></span> |
| <span data-ttu-id="825eb-981">indexName</span><span class="sxs-lookup"><span data-stu-id="825eb-981">indexName</span></span> | <span data-ttu-id="825eb-982">Name of the Azure Search index.</span><span class="sxs-lookup"><span data-stu-id="825eb-982">Name of the Azure Search index.</span></span> <span data-ttu-id="825eb-983">Data Factory does not create the index.</span><span class="sxs-lookup"><span data-stu-id="825eb-983">Data Factory does not create the index.</span></span> <span data-ttu-id="825eb-984">The index must exist in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="825eb-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="825eb-985">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-986">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-986">Example</span></span>

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

<span data-ttu-id="825eb-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="825eb-988">Azure Search Index Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-990">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-990">Property</span></span> | <span data-ttu-id="825eb-991">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-991">Description</span></span> | <span data-ttu-id="825eb-992">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-992">Allowed values</span></span> | <span data-ttu-id="825eb-993">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="825eb-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="825eb-994">WriteBehavior</span></span> | <span data-ttu-id="825eb-995">Specifies whether to merge or replace when a document already exists in the index.</span><span class="sxs-lookup"><span data-stu-id="825eb-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="825eb-996">Merge (default)</span><span class="sxs-lookup"><span data-stu-id="825eb-996">Merge (default)</span></span><br/><span data-ttu-id="825eb-997">Upload</span><span class="sxs-lookup"><span data-stu-id="825eb-997">Upload</span></span>| <span data-ttu-id="825eb-998">No</span><span class="sxs-lookup"><span data-stu-id="825eb-998">No</span></span> |
| <span data-ttu-id="825eb-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="825eb-999">WriteBatchSize</span></span> | <span data-ttu-id="825eb-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="825eb-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="825eb-1001">1 to 1,000.</span><span class="sxs-lookup"><span data-stu-id="825eb-1001">1 to 1,000.</span></span> <span data-ttu-id="825eb-1002">Default value is 1000.</span><span class="sxs-lookup"><span data-stu-id="825eb-1002">Default value is 1000.</span></span> | <span data-ttu-id="825eb-1003">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1004">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1004">Example</span></span>

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

<span data-ttu-id="825eb-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="825eb-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="825eb-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1007">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1007">Linked service</span></span>
<span data-ttu-id="825eb-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="825eb-1009">Azure Storage Linked Service</span><span class="sxs-lookup"><span data-stu-id="825eb-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="825eb-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="825eb-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="825eb-1012">Then, you can specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1013">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1013">Property</span></span> | <span data-ttu-id="825eb-1014">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1014">Description</span></span> | <span data-ttu-id="825eb-1015">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-1016">type</span><span class="sxs-lookup"><span data-stu-id="825eb-1016">type</span></span> |<span data-ttu-id="825eb-1017">The type property must be set to: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="825eb-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="825eb-1018">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1018">Yes</span></span> |
| <span data-ttu-id="825eb-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-1019">connectionString</span></span> |<span data-ttu-id="825eb-1020">Specify information needed to connect to Azure storage for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="825eb-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="825eb-1021">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1021">Yes</span></span> |

<span data-ttu-id="825eb-1022">**Example:**</span><span class="sxs-lookup"><span data-stu-id="825eb-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="825eb-1023">Azure Storage SAS Linked Service</span><span class="sxs-lookup"><span data-stu-id="825eb-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="825eb-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="825eb-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="825eb-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span><span class="sxs-lookup"><span data-stu-id="825eb-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="825eb-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="825eb-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="825eb-1028">Then, you can specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="825eb-1029">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1029">Property</span></span> | <span data-ttu-id="825eb-1030">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1030">Description</span></span> | <span data-ttu-id="825eb-1031">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-1032">type</span><span class="sxs-lookup"><span data-stu-id="825eb-1032">type</span></span> |<span data-ttu-id="825eb-1033">The type property must be set to: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="825eb-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="825eb-1034">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1034">Yes</span></span> |
| <span data-ttu-id="825eb-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="825eb-1035">sasUri</span></span> |<span data-ttu-id="825eb-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span><span class="sxs-lookup"><span data-stu-id="825eb-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="825eb-1037">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1037">Yes</span></span> |

<span data-ttu-id="825eb-1038">**Example:**</span><span class="sxs-lookup"><span data-stu-id="825eb-1038">**Example:**</span></span>

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

<span data-ttu-id="825eb-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-1040">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1040">Dataset</span></span>
<span data-ttu-id="825eb-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1042">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1042">Property</span></span> | <span data-ttu-id="825eb-1043">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1043">Description</span></span> | <span data-ttu-id="825eb-1044">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1045">tableName</span></span> |<span data-ttu-id="825eb-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="825eb-1047">Yes.</span><span class="sxs-lookup"><span data-stu-id="825eb-1047">Yes.</span></span> <span data-ttu-id="825eb-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="825eb-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="825eb-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="825eb-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1050">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1050">Example</span></span>

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

<span data-ttu-id="825eb-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="825eb-1052">Azure Table Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-1054">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1054">Property</span></span> | <span data-ttu-id="825eb-1055">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1055">Description</span></span> | <span data-ttu-id="825eb-1056">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1056">Allowed values</span></span> | <span data-ttu-id="825eb-1057">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1058">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="825eb-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="825eb-1059">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1060">Azure table query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1060">Azure table query string.</span></span> <span data-ttu-id="825eb-1061">See examples in the next section.</span><span class="sxs-lookup"><span data-stu-id="825eb-1061">See examples in the next section.</span></span> |<span data-ttu-id="825eb-1062">No.</span><span class="sxs-lookup"><span data-stu-id="825eb-1062">No.</span></span> <span data-ttu-id="825eb-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="825eb-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="825eb-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="825eb-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="825eb-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="825eb-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="825eb-1066">Indicate whether swallow the exception of table not exist.</span><span class="sxs-lookup"><span data-stu-id="825eb-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="825eb-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="825eb-1067">TRUE</span></span><br/><span data-ttu-id="825eb-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="825eb-1068">FALSE</span></span> |<span data-ttu-id="825eb-1069">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1070">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1070">Example</span></span>

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

<span data-ttu-id="825eb-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="825eb-1072">Azure Table Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-1074">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1074">Property</span></span> | <span data-ttu-id="825eb-1075">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1075">Description</span></span> | <span data-ttu-id="825eb-1076">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1076">Allowed values</span></span> | <span data-ttu-id="825eb-1077">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="825eb-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="825eb-1079">Default partition key value that can be used by the sink.</span><span class="sxs-lookup"><span data-stu-id="825eb-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="825eb-1080">A string value.</span><span class="sxs-lookup"><span data-stu-id="825eb-1080">A string value.</span></span> |<span data-ttu-id="825eb-1081">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1081">No</span></span> |
| <span data-ttu-id="825eb-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="825eb-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="825eb-1083">Specify name of the column whose values are used as partition keys.</span><span class="sxs-lookup"><span data-stu-id="825eb-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="825eb-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span><span class="sxs-lookup"><span data-stu-id="825eb-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="825eb-1085">A column name.</span><span class="sxs-lookup"><span data-stu-id="825eb-1085">A column name.</span></span> |<span data-ttu-id="825eb-1086">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1086">No</span></span> |
| <span data-ttu-id="825eb-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="825eb-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="825eb-1088">Specify name of the column whose column values are used as row key.</span><span class="sxs-lookup"><span data-stu-id="825eb-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="825eb-1089">If not specified, use a GUID for each row.</span><span class="sxs-lookup"><span data-stu-id="825eb-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="825eb-1090">A column name.</span><span class="sxs-lookup"><span data-stu-id="825eb-1090">A column name.</span></span> |<span data-ttu-id="825eb-1091">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1091">No</span></span> |
| <span data-ttu-id="825eb-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="825eb-1092">azureTableInsertType</span></span> |<span data-ttu-id="825eb-1093">The mode to insert data into Azure table.</span><span class="sxs-lookup"><span data-stu-id="825eb-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="825eb-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span><span class="sxs-lookup"><span data-stu-id="825eb-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="825eb-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span><span class="sxs-lookup"><span data-stu-id="825eb-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="825eb-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span><span class="sxs-lookup"><span data-stu-id="825eb-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="825eb-1097">merge (default)</span><span class="sxs-lookup"><span data-stu-id="825eb-1097">merge (default)</span></span><br/><span data-ttu-id="825eb-1098">replace</span><span class="sxs-lookup"><span data-stu-id="825eb-1098">replace</span></span> |<span data-ttu-id="825eb-1099">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1099">No</span></span> |
| <span data-ttu-id="825eb-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="825eb-1100">writeBatchSize</span></span> |<span data-ttu-id="825eb-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span><span class="sxs-lookup"><span data-stu-id="825eb-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="825eb-1102">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="825eb-1102">Integer (number of rows)</span></span> |<span data-ttu-id="825eb-1103">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="825eb-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="825eb-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="825eb-1104">writeBatchTimeout</span></span> |<span data-ttu-id="825eb-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span><span class="sxs-lookup"><span data-stu-id="825eb-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="825eb-1106">timespan</span><span class="sxs-lookup"><span data-stu-id="825eb-1106">timespan</span></span><br/><br/><span data-ttu-id="825eb-1107">Example: “00:20:00” (20 minutes)</span><span class="sxs-lookup"><span data-stu-id="825eb-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="825eb-1108">No (Default to storage client default timeout value 90 sec)</span><span class="sxs-lookup"><span data-stu-id="825eb-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1109">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1109">Example</span></span>

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
<span data-ttu-id="825eb-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="825eb-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="825eb-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1112">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1112">Linked service</span></span>
<span data-ttu-id="825eb-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1114">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1114">Property</span></span> | <span data-ttu-id="825eb-1115">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1115">Description</span></span> | <span data-ttu-id="825eb-1116">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1117">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1117">server</span></span> |<span data-ttu-id="825eb-1118">IP address or host name of the Amazon Redshift server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="825eb-1119">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1119">Yes</span></span> |
| <span data-ttu-id="825eb-1120">port</span><span class="sxs-lookup"><span data-stu-id="825eb-1120">port</span></span> |<span data-ttu-id="825eb-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="825eb-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="825eb-1122">No, default value: 5439</span><span class="sxs-lookup"><span data-stu-id="825eb-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="825eb-1123">database</span><span class="sxs-lookup"><span data-stu-id="825eb-1123">database</span></span> |<span data-ttu-id="825eb-1124">Name of the Amazon Redshift database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="825eb-1125">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1125">Yes</span></span> |
| <span data-ttu-id="825eb-1126">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1126">username</span></span> |<span data-ttu-id="825eb-1127">Name of user who has access to the database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="825eb-1128">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1128">Yes</span></span> |
| <span data-ttu-id="825eb-1129">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1129">password</span></span> |<span data-ttu-id="825eb-1130">Password for the user account.</span><span class="sxs-lookup"><span data-stu-id="825eb-1130">Password for the user account.</span></span> |<span data-ttu-id="825eb-1131">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1132">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1132">Example</span></span>

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

<span data-ttu-id="825eb-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-1134">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1134">Dataset</span></span>
<span data-ttu-id="825eb-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1136">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1136">Property</span></span> | <span data-ttu-id="825eb-1137">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1137">Description</span></span> | <span data-ttu-id="825eb-1138">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1139">tableName</span></span> |<span data-ttu-id="825eb-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="825eb-1141">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="825eb-1142">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1142">Example</span></span>

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
<span data-ttu-id="825eb-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-1144">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="825eb-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-1146">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1146">Property</span></span> | <span data-ttu-id="825eb-1147">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1147">Description</span></span> | <span data-ttu-id="825eb-1148">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1148">Allowed values</span></span> | <span data-ttu-id="825eb-1149">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1150">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1150">query</span></span> |<span data-ttu-id="825eb-1151">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1152">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1152">SQL query string.</span></span> <span data-ttu-id="825eb-1153">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="825eb-1154">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1155">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1155">Example</span></span>

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
<span data-ttu-id="825eb-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="825eb-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="825eb-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1158">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1158">Linked service</span></span>
<span data-ttu-id="825eb-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1160">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1160">Property</span></span> | <span data-ttu-id="825eb-1161">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1161">Description</span></span> | <span data-ttu-id="825eb-1162">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1163">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1163">server</span></span> |<span data-ttu-id="825eb-1164">Name of the DB2 server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="825eb-1165">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1165">Yes</span></span> |
| <span data-ttu-id="825eb-1166">database</span><span class="sxs-lookup"><span data-stu-id="825eb-1166">database</span></span> |<span data-ttu-id="825eb-1167">Name of the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="825eb-1168">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1168">Yes</span></span> |
| <span data-ttu-id="825eb-1169">schema</span><span class="sxs-lookup"><span data-stu-id="825eb-1169">schema</span></span> |<span data-ttu-id="825eb-1170">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1170">Name of the schema in the database.</span></span> <span data-ttu-id="825eb-1171">The schema name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="825eb-1172">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1172">No</span></span> |
| <span data-ttu-id="825eb-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-1173">authenticationType</span></span> |<span data-ttu-id="825eb-1174">Type of authentication used to connect to the DB2 database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="825eb-1175">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="825eb-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="825eb-1176">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1176">Yes</span></span> |
| <span data-ttu-id="825eb-1177">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1177">username</span></span> |<span data-ttu-id="825eb-1178">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="825eb-1179">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1179">No</span></span> |
| <span data-ttu-id="825eb-1180">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1180">password</span></span> |<span data-ttu-id="825eb-1181">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="825eb-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="825eb-1182">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1182">No</span></span> |
| <span data-ttu-id="825eb-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1183">gatewayName</span></span> |<span data-ttu-id="825eb-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="825eb-1185">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1186">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1186">Example</span></span>
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
<span data-ttu-id="825eb-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-1188">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1188">Dataset</span></span>
<span data-ttu-id="825eb-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="825eb-1190">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1190">Property</span></span> | <span data-ttu-id="825eb-1191">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1191">Description</span></span> | <span data-ttu-id="825eb-1192">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1193">tableName</span></span> |<span data-ttu-id="825eb-1194">Name of the table in the DB2 Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="825eb-1195">The tableName is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="825eb-1196">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="825eb-1197">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1197">Example</span></span>
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

<span data-ttu-id="825eb-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-1199">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-1201">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1201">Property</span></span> | <span data-ttu-id="825eb-1202">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1202">Description</span></span> | <span data-ttu-id="825eb-1203">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1203">Allowed values</span></span> | <span data-ttu-id="825eb-1204">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1205">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1205">query</span></span> |<span data-ttu-id="825eb-1206">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1207">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1207">SQL query string.</span></span> <span data-ttu-id="825eb-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="825eb-1209">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1210">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1210">Example</span></span>
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
<span data-ttu-id="825eb-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="825eb-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="825eb-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1213">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1213">Linked service</span></span>
<span data-ttu-id="825eb-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1215">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1215">Property</span></span> | <span data-ttu-id="825eb-1216">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1216">Description</span></span> | <span data-ttu-id="825eb-1217">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1218">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1218">server</span></span> |<span data-ttu-id="825eb-1219">Name of the MySQL server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="825eb-1220">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1220">Yes</span></span> |
| <span data-ttu-id="825eb-1221">database</span><span class="sxs-lookup"><span data-stu-id="825eb-1221">database</span></span> |<span data-ttu-id="825eb-1222">Name of the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="825eb-1223">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1223">Yes</span></span> |
| <span data-ttu-id="825eb-1224">schema</span><span class="sxs-lookup"><span data-stu-id="825eb-1224">schema</span></span> |<span data-ttu-id="825eb-1225">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="825eb-1226">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1226">No</span></span> |
| <span data-ttu-id="825eb-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-1227">authenticationType</span></span> |<span data-ttu-id="825eb-1228">Type of authentication used to connect to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="825eb-1229">Possible values are: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="825eb-1230">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1230">Yes</span></span> |
| <span data-ttu-id="825eb-1231">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1231">username</span></span> |<span data-ttu-id="825eb-1232">Specify user name to connect to the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="825eb-1233">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1233">Yes</span></span> |
| <span data-ttu-id="825eb-1234">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1234">password</span></span> |<span data-ttu-id="825eb-1235">Specify password for the user account you specified.</span><span class="sxs-lookup"><span data-stu-id="825eb-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="825eb-1236">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1236">Yes</span></span> |
| <span data-ttu-id="825eb-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1237">gatewayName</span></span> |<span data-ttu-id="825eb-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="825eb-1239">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1240">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1240">Example</span></span>

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

<span data-ttu-id="825eb-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-1242">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1242">Dataset</span></span>
<span data-ttu-id="825eb-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1244">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1244">Property</span></span> | <span data-ttu-id="825eb-1245">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1245">Description</span></span> | <span data-ttu-id="825eb-1246">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1247">tableName</span></span> |<span data-ttu-id="825eb-1248">Name of the table in the MySQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="825eb-1249">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1250">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1250">Example</span></span>

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
<span data-ttu-id="825eb-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-1252">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-1254">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1254">Property</span></span> | <span data-ttu-id="825eb-1255">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1255">Description</span></span> | <span data-ttu-id="825eb-1256">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1256">Allowed values</span></span> | <span data-ttu-id="825eb-1257">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1258">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1258">query</span></span> |<span data-ttu-id="825eb-1259">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1260">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1260">SQL query string.</span></span> <span data-ttu-id="825eb-1261">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="825eb-1262">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="825eb-1263">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1263">Example</span></span>
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

<span data-ttu-id="825eb-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="825eb-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="825eb-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-1266">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1266">Linked service</span></span>
<span data-ttu-id="825eb-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1268">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1268">Property</span></span> | <span data-ttu-id="825eb-1269">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1269">Description</span></span> | <span data-ttu-id="825eb-1270">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="825eb-1271">driverType</span></span> | <span data-ttu-id="825eb-1272">Specify which driver to use to copy data from/to Oracle Database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="825eb-1273">Allowed values are **Microsoft** or **ODP** (default).</span><span class="sxs-lookup"><span data-stu-id="825eb-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="825eb-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span><span class="sxs-lookup"><span data-stu-id="825eb-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="825eb-1275">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1275">No</span></span> |
| <span data-ttu-id="825eb-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-1276">connectionString</span></span> | <span data-ttu-id="825eb-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="825eb-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="825eb-1278">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1278">Yes</span></span> |
| <span data-ttu-id="825eb-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1279">gatewayName</span></span> | <span data-ttu-id="825eb-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span><span class="sxs-lookup"><span data-stu-id="825eb-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="825eb-1281">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1282">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1282">Example</span></span>
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

<span data-ttu-id="825eb-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-1284">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1284">Dataset</span></span>
<span data-ttu-id="825eb-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1286">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1286">Property</span></span> | <span data-ttu-id="825eb-1287">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1287">Description</span></span> | <span data-ttu-id="825eb-1288">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1289">tableName</span></span> |<span data-ttu-id="825eb-1290">Name of the table in the Oracle Database that the linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="825eb-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1292">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1292">Example</span></span>

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
<span data-ttu-id="825eb-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="825eb-1294">Oracle Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-1296">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1296">Property</span></span> | <span data-ttu-id="825eb-1297">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1297">Description</span></span> | <span data-ttu-id="825eb-1298">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1298">Allowed values</span></span> | <span data-ttu-id="825eb-1299">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="825eb-1300">oracleReaderQuery</span></span> |<span data-ttu-id="825eb-1301">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1302">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1302">SQL query string.</span></span> <span data-ttu-id="825eb-1303">For example: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="825eb-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="825eb-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="825eb-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="825eb-1305">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1306">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1306">Example</span></span>

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

<span data-ttu-id="825eb-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="825eb-1308">Oracle Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-1310">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1310">Property</span></span> | <span data-ttu-id="825eb-1311">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1311">Description</span></span> | <span data-ttu-id="825eb-1312">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1312">Allowed values</span></span> | <span data-ttu-id="825eb-1313">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="825eb-1314">writeBatchTimeout</span></span> |<span data-ttu-id="825eb-1315">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="825eb-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="825eb-1316">timespan</span><span class="sxs-lookup"><span data-stu-id="825eb-1316">timespan</span></span><br/><br/> <span data-ttu-id="825eb-1317">Example: 00:30:00 (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="825eb-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="825eb-1318">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1318">No</span></span> |
| <span data-ttu-id="825eb-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="825eb-1319">writeBatchSize</span></span> |<span data-ttu-id="825eb-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="825eb-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="825eb-1321">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="825eb-1321">Integer (number of rows)</span></span> |<span data-ttu-id="825eb-1322">No (default: 100)</span><span class="sxs-lookup"><span data-stu-id="825eb-1322">No (default: 100)</span></span> |
| <span data-ttu-id="825eb-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="825eb-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="825eb-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="825eb-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="825eb-1325">A query statement.</span><span class="sxs-lookup"><span data-stu-id="825eb-1325">A query statement.</span></span> |<span data-ttu-id="825eb-1326">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1326">No</span></span> |
| <span data-ttu-id="825eb-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="825eb-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="825eb-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="825eb-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="825eb-1329">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="825eb-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="825eb-1330">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1331">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1331">Example</span></span>
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
<span data-ttu-id="825eb-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="825eb-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="825eb-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1334">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1334">Linked service</span></span>
<span data-ttu-id="825eb-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1336">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1336">Property</span></span> | <span data-ttu-id="825eb-1337">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1337">Description</span></span> | <span data-ttu-id="825eb-1338">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1339">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1339">server</span></span> |<span data-ttu-id="825eb-1340">Name of the PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="825eb-1341">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1341">Yes</span></span> |
| <span data-ttu-id="825eb-1342">database</span><span class="sxs-lookup"><span data-stu-id="825eb-1342">database</span></span> |<span data-ttu-id="825eb-1343">Name of the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="825eb-1344">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1344">Yes</span></span> |
| <span data-ttu-id="825eb-1345">schema</span><span class="sxs-lookup"><span data-stu-id="825eb-1345">schema</span></span> |<span data-ttu-id="825eb-1346">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1346">Name of the schema in the database.</span></span> <span data-ttu-id="825eb-1347">The schema name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="825eb-1348">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1348">No</span></span> |
| <span data-ttu-id="825eb-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-1349">authenticationType</span></span> |<span data-ttu-id="825eb-1350">Type of authentication used to connect to the PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="825eb-1351">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="825eb-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="825eb-1352">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1352">Yes</span></span> |
| <span data-ttu-id="825eb-1353">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1353">username</span></span> |<span data-ttu-id="825eb-1354">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="825eb-1355">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1355">No</span></span> |
| <span data-ttu-id="825eb-1356">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1356">password</span></span> |<span data-ttu-id="825eb-1357">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="825eb-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="825eb-1358">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1358">No</span></span> |
| <span data-ttu-id="825eb-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1359">gatewayName</span></span> |<span data-ttu-id="825eb-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="825eb-1361">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1362">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1362">Example</span></span>

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
<span data-ttu-id="825eb-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-1364">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1364">Dataset</span></span>
<span data-ttu-id="825eb-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1366">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1366">Property</span></span> | <span data-ttu-id="825eb-1367">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1367">Description</span></span> | <span data-ttu-id="825eb-1368">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1369">tableName</span></span> |<span data-ttu-id="825eb-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="825eb-1371">The tableName is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="825eb-1372">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1373">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1373">Example</span></span>
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
<span data-ttu-id="825eb-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-1375">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-1377">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1377">Property</span></span> | <span data-ttu-id="825eb-1378">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1378">Description</span></span> | <span data-ttu-id="825eb-1379">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1379">Allowed values</span></span> | <span data-ttu-id="825eb-1380">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1381">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1381">query</span></span> |<span data-ttu-id="825eb-1382">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1383">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1383">SQL query string.</span></span> <span data-ttu-id="825eb-1384">For example: "query": "select \* from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="825eb-1384">For example: "query": "select \* from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="825eb-1385">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1386">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1386">Example</span></span>

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

<span data-ttu-id="825eb-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="825eb-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="825eb-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="825eb-1389">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1389">Linked service</span></span>
<span data-ttu-id="825eb-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="825eb-1391">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1391">Property</span></span> | <span data-ttu-id="825eb-1392">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1392">Description</span></span> | <span data-ttu-id="825eb-1393">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1393">Allowed values</span></span> | <span data-ttu-id="825eb-1394">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="825eb-1395">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1395">server</span></span> | <span data-ttu-id="825eb-1396">Name of the server on which the SAP BW instance resides.</span><span class="sxs-lookup"><span data-stu-id="825eb-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="825eb-1397">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1397">string</span></span> | <span data-ttu-id="825eb-1398">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1398">Yes</span></span>
<span data-ttu-id="825eb-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="825eb-1399">systemNumber</span></span> | <span data-ttu-id="825eb-1400">System number of the SAP BW system.</span><span class="sxs-lookup"><span data-stu-id="825eb-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="825eb-1401">Two-digit decimal number represented as a string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="825eb-1402">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1402">Yes</span></span>
<span data-ttu-id="825eb-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="825eb-1403">clientId</span></span> | <span data-ttu-id="825eb-1404">Client ID of the client in the SAP W system.</span><span class="sxs-lookup"><span data-stu-id="825eb-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="825eb-1405">Three-digit decimal number represented as a string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="825eb-1406">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1406">Yes</span></span>
<span data-ttu-id="825eb-1407">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1407">username</span></span> | <span data-ttu-id="825eb-1408">Name of the user who has access to the SAP server</span><span class="sxs-lookup"><span data-stu-id="825eb-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="825eb-1409">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1409">string</span></span> | <span data-ttu-id="825eb-1410">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1410">Yes</span></span>
<span data-ttu-id="825eb-1411">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1411">password</span></span> | <span data-ttu-id="825eb-1412">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="825eb-1412">Password for the user.</span></span> | <span data-ttu-id="825eb-1413">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1413">string</span></span> | <span data-ttu-id="825eb-1414">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1414">Yes</span></span>
<span data-ttu-id="825eb-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1415">gatewayName</span></span> | <span data-ttu-id="825eb-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="825eb-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="825eb-1417">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1417">string</span></span> | <span data-ttu-id="825eb-1418">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1418">Yes</span></span>
<span data-ttu-id="825eb-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-1419">encryptedCredential</span></span> | <span data-ttu-id="825eb-1420">The encrypted credential string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1420">The encrypted credential string.</span></span> | <span data-ttu-id="825eb-1421">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1421">string</span></span> | <span data-ttu-id="825eb-1422">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="825eb-1423">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1423">Example</span></span>

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

<span data-ttu-id="825eb-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-1425">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1425">Dataset</span></span>
<span data-ttu-id="825eb-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="825eb-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="825eb-1428">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1428">Example</span></span>

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
<span data-ttu-id="825eb-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-1430">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-1432">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1432">Property</span></span> | <span data-ttu-id="825eb-1433">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1433">Description</span></span> | <span data-ttu-id="825eb-1434">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1434">Allowed values</span></span> | <span data-ttu-id="825eb-1435">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1436">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1436">query</span></span> | <span data-ttu-id="825eb-1437">Specifies the MDX query to read data from the SAP BW instance.</span><span class="sxs-lookup"><span data-stu-id="825eb-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="825eb-1438">MDX query.</span><span class="sxs-lookup"><span data-stu-id="825eb-1438">MDX query.</span></span> | <span data-ttu-id="825eb-1439">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1440">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1440">Example</span></span>

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

<span data-ttu-id="825eb-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="825eb-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="825eb-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1443">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1443">Linked service</span></span>
<span data-ttu-id="825eb-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="825eb-1445">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1445">Property</span></span> | <span data-ttu-id="825eb-1446">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1446">Description</span></span> | <span data-ttu-id="825eb-1447">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1447">Allowed values</span></span> | <span data-ttu-id="825eb-1448">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="825eb-1449">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1449">server</span></span> | <span data-ttu-id="825eb-1450">Name of the server on which the SAP HANA instance resides.</span><span class="sxs-lookup"><span data-stu-id="825eb-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="825eb-1451">If your server is using a customized port, specify `server:port`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="825eb-1452">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1452">string</span></span> | <span data-ttu-id="825eb-1453">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1453">Yes</span></span>
<span data-ttu-id="825eb-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-1454">authenticationType</span></span> | <span data-ttu-id="825eb-1455">Type of authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-1455">Type of authentication.</span></span> | <span data-ttu-id="825eb-1456">string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1456">string.</span></span> <span data-ttu-id="825eb-1457">"Basic" or "Windows"</span><span class="sxs-lookup"><span data-stu-id="825eb-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="825eb-1458">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1458">Yes</span></span> 
<span data-ttu-id="825eb-1459">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1459">username</span></span> | <span data-ttu-id="825eb-1460">Name of the user who has access to the SAP server</span><span class="sxs-lookup"><span data-stu-id="825eb-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="825eb-1461">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1461">string</span></span> | <span data-ttu-id="825eb-1462">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1462">Yes</span></span>
<span data-ttu-id="825eb-1463">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1463">password</span></span> | <span data-ttu-id="825eb-1464">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="825eb-1464">Password for the user.</span></span> | <span data-ttu-id="825eb-1465">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1465">string</span></span> | <span data-ttu-id="825eb-1466">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1466">Yes</span></span>
<span data-ttu-id="825eb-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1467">gatewayName</span></span> | <span data-ttu-id="825eb-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="825eb-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="825eb-1469">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1469">string</span></span> | <span data-ttu-id="825eb-1470">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1470">Yes</span></span>
<span data-ttu-id="825eb-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-1471">encryptedCredential</span></span> | <span data-ttu-id="825eb-1472">The encrypted credential string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1472">The encrypted credential string.</span></span> | <span data-ttu-id="825eb-1473">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1473">string</span></span> | <span data-ttu-id="825eb-1474">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="825eb-1475">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1475">Example</span></span>

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
<span data-ttu-id="825eb-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="825eb-1477">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1477">Dataset</span></span>
<span data-ttu-id="825eb-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="825eb-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="825eb-1480">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1480">Example</span></span>

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
<span data-ttu-id="825eb-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-1482">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-1484">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1484">Property</span></span> | <span data-ttu-id="825eb-1485">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1485">Description</span></span> | <span data-ttu-id="825eb-1486">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1486">Allowed values</span></span> | <span data-ttu-id="825eb-1487">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1488">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1488">query</span></span> | <span data-ttu-id="825eb-1489">Specifies the SQL query to read data from the SAP HANA instance.</span><span class="sxs-lookup"><span data-stu-id="825eb-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="825eb-1490">SQL query.</span><span class="sxs-lookup"><span data-stu-id="825eb-1490">SQL query.</span></span> | <span data-ttu-id="825eb-1491">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="825eb-1492">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1492">Example</span></span>


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

<span data-ttu-id="825eb-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="825eb-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="825eb-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1495">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1495">Linked service</span></span>
<span data-ttu-id="825eb-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span><span class="sxs-lookup"><span data-stu-id="825eb-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="825eb-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="825eb-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="825eb-1499">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1499">Property</span></span> | <span data-ttu-id="825eb-1500">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1500">Description</span></span> | <span data-ttu-id="825eb-1501">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1502">type</span><span class="sxs-lookup"><span data-stu-id="825eb-1502">type</span></span> |<span data-ttu-id="825eb-1503">The type property should be set to: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="825eb-1504">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1504">Yes</span></span> |
| <span data-ttu-id="825eb-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-1505">connectionString</span></span> |<span data-ttu-id="825eb-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="825eb-1507">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1507">Yes</span></span> |
| <span data-ttu-id="825eb-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1508">gatewayName</span></span> |<span data-ttu-id="825eb-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="825eb-1510">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1510">Yes</span></span> |
| <span data-ttu-id="825eb-1511">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1511">username</span></span> |<span data-ttu-id="825eb-1512">Specify user name if you are using Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="825eb-1513">Example: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="825eb-1514">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1514">No</span></span> |
| <span data-ttu-id="825eb-1515">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1515">password</span></span> |<span data-ttu-id="825eb-1516">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="825eb-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="825eb-1517">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1517">No</span></span> |

<span data-ttu-id="825eb-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span><span class="sxs-lookup"><span data-stu-id="825eb-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="825eb-1519">Example: JSON for using SQL Authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="825eb-1520">Example: JSON for using Windows Authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="825eb-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="825eb-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span><span class="sxs-lookup"><span data-stu-id="825eb-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="825eb-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-1524">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1524">Dataset</span></span>
<span data-ttu-id="825eb-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1526">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1526">Property</span></span> | <span data-ttu-id="825eb-1527">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1527">Description</span></span> | <span data-ttu-id="825eb-1528">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1529">tableName</span></span> |<span data-ttu-id="825eb-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="825eb-1531">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1532">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1532">Example</span></span>
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

<span data-ttu-id="825eb-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="825eb-1534">Sql Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-1536">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1536">Property</span></span> | <span data-ttu-id="825eb-1537">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1537">Description</span></span> | <span data-ttu-id="825eb-1538">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1538">Allowed values</span></span> | <span data-ttu-id="825eb-1539">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1540">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="825eb-1540">sqlReaderQuery</span></span> |<span data-ttu-id="825eb-1541">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1542">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1542">SQL query string.</span></span> <span data-ttu-id="825eb-1543">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="825eb-1544">May reference multiple tables from the database referenced by the input dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="825eb-1545">If not specified, the SQL statement that is executed: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="825eb-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="825eb-1546">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1546">No</span></span> |
| <span data-ttu-id="825eb-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="825eb-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="825eb-1548">Name of the stored procedure that reads data from the source table.</span><span class="sxs-lookup"><span data-stu-id="825eb-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="825eb-1549">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="825eb-1550">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1550">No</span></span> |
| <span data-ttu-id="825eb-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="825eb-1551">storedProcedureParameters</span></span> |<span data-ttu-id="825eb-1552">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="825eb-1553">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="825eb-1553">Name/value pairs.</span></span> <span data-ttu-id="825eb-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="825eb-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="825eb-1555">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1555">No</span></span> |

<span data-ttu-id="825eb-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="825eb-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="825eb-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="825eb-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="825eb-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="825eb-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="825eb-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span><span class="sxs-lookup"><span data-stu-id="825eb-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="825eb-1561">There are no validations performed against this table though.</span><span class="sxs-lookup"><span data-stu-id="825eb-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="825eb-1562">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1562">Example</span></span>
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

<span data-ttu-id="825eb-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span><span class="sxs-lookup"><span data-stu-id="825eb-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="825eb-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="825eb-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span><span class="sxs-lookup"><span data-stu-id="825eb-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="825eb-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="825eb-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="825eb-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="825eb-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="825eb-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span><span class="sxs-lookup"><span data-stu-id="825eb-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="825eb-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="825eb-1571">Sql Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-1573">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1573">Property</span></span> | <span data-ttu-id="825eb-1574">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1574">Description</span></span> | <span data-ttu-id="825eb-1575">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1575">Allowed values</span></span> | <span data-ttu-id="825eb-1576">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="825eb-1577">writeBatchTimeout</span></span> |<span data-ttu-id="825eb-1578">Wait time for the batch insert operation to complete before it times out.</span><span class="sxs-lookup"><span data-stu-id="825eb-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="825eb-1579">timespan</span><span class="sxs-lookup"><span data-stu-id="825eb-1579">timespan</span></span><br/><br/> <span data-ttu-id="825eb-1580">Example: “00:30:00” (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="825eb-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="825eb-1581">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1581">No</span></span> |
| <span data-ttu-id="825eb-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="825eb-1582">writeBatchSize</span></span> |<span data-ttu-id="825eb-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="825eb-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="825eb-1584">Integer (number of rows)</span><span class="sxs-lookup"><span data-stu-id="825eb-1584">Integer (number of rows)</span></span> |<span data-ttu-id="825eb-1585">No (default: 10000)</span><span class="sxs-lookup"><span data-stu-id="825eb-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="825eb-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="825eb-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="825eb-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span><span class="sxs-lookup"><span data-stu-id="825eb-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="825eb-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span><span class="sxs-lookup"><span data-stu-id="825eb-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="825eb-1589">A query statement.</span><span class="sxs-lookup"><span data-stu-id="825eb-1589">A query statement.</span></span> |<span data-ttu-id="825eb-1590">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1590">No</span></span> |
| <span data-ttu-id="825eb-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="825eb-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="825eb-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span><span class="sxs-lookup"><span data-stu-id="825eb-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="825eb-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span><span class="sxs-lookup"><span data-stu-id="825eb-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="825eb-1594">Column name of a column with data type of binary(32).</span><span class="sxs-lookup"><span data-stu-id="825eb-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="825eb-1595">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1595">No</span></span> |
| <span data-ttu-id="825eb-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="825eb-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="825eb-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span><span class="sxs-lookup"><span data-stu-id="825eb-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="825eb-1598">Name of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="825eb-1599">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1599">No</span></span> |
| <span data-ttu-id="825eb-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="825eb-1600">storedProcedureParameters</span></span> |<span data-ttu-id="825eb-1601">Parameters for the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="825eb-1602">Name/value pairs.</span><span class="sxs-lookup"><span data-stu-id="825eb-1602">Name/value pairs.</span></span> <span data-ttu-id="825eb-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="825eb-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="825eb-1604">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1604">No</span></span> |
| <span data-ttu-id="825eb-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="825eb-1605">sqlWriterTableType</span></span> |<span data-ttu-id="825eb-1606">Specify table type name to be used in the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="825eb-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="825eb-1607">Copy activity makes the data being moved available in a temp table with this table type.</span><span class="sxs-lookup"><span data-stu-id="825eb-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="825eb-1608">Stored procedure code can then merge the data being copied with existing data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="825eb-1609">A table type name.</span><span class="sxs-lookup"><span data-stu-id="825eb-1609">A table type name.</span></span> |<span data-ttu-id="825eb-1610">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1611">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1611">Example</span></span>
<span data-ttu-id="825eb-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span><span class="sxs-lookup"><span data-stu-id="825eb-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="825eb-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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

<span data-ttu-id="825eb-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="825eb-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="825eb-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1616">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1616">Linked service</span></span>
<span data-ttu-id="825eb-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1618">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1618">Property</span></span> | <span data-ttu-id="825eb-1619">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1619">Description</span></span> | <span data-ttu-id="825eb-1620">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1621">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1621">server</span></span> |<span data-ttu-id="825eb-1622">Name of the Sybase server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="825eb-1623">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1623">Yes</span></span> |
| <span data-ttu-id="825eb-1624">database</span><span class="sxs-lookup"><span data-stu-id="825eb-1624">database</span></span> |<span data-ttu-id="825eb-1625">Name of the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="825eb-1626">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1626">Yes</span></span> |
| <span data-ttu-id="825eb-1627">schema</span><span class="sxs-lookup"><span data-stu-id="825eb-1627">schema</span></span> |<span data-ttu-id="825eb-1628">Name of the schema in the database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="825eb-1629">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1629">No</span></span> |
| <span data-ttu-id="825eb-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-1630">authenticationType</span></span> |<span data-ttu-id="825eb-1631">Type of authentication used to connect to the Sybase database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="825eb-1632">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="825eb-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="825eb-1633">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1633">Yes</span></span> |
| <span data-ttu-id="825eb-1634">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1634">username</span></span> |<span data-ttu-id="825eb-1635">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="825eb-1636">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1636">No</span></span> |
| <span data-ttu-id="825eb-1637">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1637">password</span></span> |<span data-ttu-id="825eb-1638">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="825eb-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="825eb-1639">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1639">No</span></span> |
| <span data-ttu-id="825eb-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1640">gatewayName</span></span> |<span data-ttu-id="825eb-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="825eb-1642">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1643">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1643">Example</span></span>
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

<span data-ttu-id="825eb-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-1645">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1645">Dataset</span></span>
<span data-ttu-id="825eb-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1647">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1647">Property</span></span> | <span data-ttu-id="825eb-1648">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1648">Description</span></span> | <span data-ttu-id="825eb-1649">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1650">tableName</span></span> |<span data-ttu-id="825eb-1651">Name of the table in the Sybase Database instance that linked service refers to.</span><span class="sxs-lookup"><span data-stu-id="825eb-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="825eb-1652">No (if **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1653">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1653">Example</span></span>

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

<span data-ttu-id="825eb-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-1655">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-1657">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1657">Property</span></span> | <span data-ttu-id="825eb-1658">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1658">Description</span></span> | <span data-ttu-id="825eb-1659">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1659">Allowed values</span></span> | <span data-ttu-id="825eb-1660">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1661">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1661">query</span></span> |<span data-ttu-id="825eb-1662">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1663">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1663">SQL query string.</span></span> <span data-ttu-id="825eb-1664">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="825eb-1665">No (if **tableName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1666">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1666">Example</span></span>

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

<span data-ttu-id="825eb-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="825eb-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="825eb-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1669">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1669">Linked service</span></span>
<span data-ttu-id="825eb-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1671">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1671">Property</span></span> | <span data-ttu-id="825eb-1672">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1672">Description</span></span> | <span data-ttu-id="825eb-1673">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1674">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1674">server</span></span> |<span data-ttu-id="825eb-1675">Name of the Teradata server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="825eb-1676">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1676">Yes</span></span> |
| <span data-ttu-id="825eb-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-1677">authenticationType</span></span> |<span data-ttu-id="825eb-1678">Type of authentication used to connect to the Teradata database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="825eb-1679">Possible values are: Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="825eb-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="825eb-1680">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1680">Yes</span></span> |
| <span data-ttu-id="825eb-1681">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1681">username</span></span> |<span data-ttu-id="825eb-1682">Specify user name if you are using Basic or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="825eb-1683">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1683">No</span></span> |
| <span data-ttu-id="825eb-1684">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1684">password</span></span> |<span data-ttu-id="825eb-1685">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="825eb-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="825eb-1686">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1686">No</span></span> |
| <span data-ttu-id="825eb-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1687">gatewayName</span></span> |<span data-ttu-id="825eb-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="825eb-1689">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1690">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1690">Example</span></span>
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

<span data-ttu-id="825eb-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-1692">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1692">Dataset</span></span>
<span data-ttu-id="825eb-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="825eb-1694">Currently, there are no type properties supported for the Teradata dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="825eb-1695">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1695">Example</span></span>
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

<span data-ttu-id="825eb-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-1697">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-1699">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1699">Property</span></span> | <span data-ttu-id="825eb-1700">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1700">Description</span></span> | <span data-ttu-id="825eb-1701">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1701">Allowed values</span></span> | <span data-ttu-id="825eb-1702">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1703">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1703">query</span></span> |<span data-ttu-id="825eb-1704">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1705">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1705">SQL query string.</span></span> <span data-ttu-id="825eb-1706">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="825eb-1707">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1708">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1708">Example</span></span>

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

<span data-ttu-id="825eb-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="825eb-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="825eb-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="825eb-1711">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1711">Linked service</span></span>
<span data-ttu-id="825eb-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1713">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1713">Property</span></span> | <span data-ttu-id="825eb-1714">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1714">Description</span></span> | <span data-ttu-id="825eb-1715">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1716">host</span><span class="sxs-lookup"><span data-stu-id="825eb-1716">host</span></span> |<span data-ttu-id="825eb-1717">One or more IP addresses or host names of Cassandra servers.</span><span class="sxs-lookup"><span data-stu-id="825eb-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="825eb-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span><span class="sxs-lookup"><span data-stu-id="825eb-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="825eb-1719">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1719">Yes</span></span> |
| <span data-ttu-id="825eb-1720">port</span><span class="sxs-lookup"><span data-stu-id="825eb-1720">port</span></span> |<span data-ttu-id="825eb-1721">The TCP port that the Cassandra server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="825eb-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="825eb-1722">No, default value: 9042</span><span class="sxs-lookup"><span data-stu-id="825eb-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="825eb-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-1723">authenticationType</span></span> |<span data-ttu-id="825eb-1724">Basic, or Anonymous</span><span class="sxs-lookup"><span data-stu-id="825eb-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="825eb-1725">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1725">Yes</span></span> |
| <span data-ttu-id="825eb-1726">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1726">username</span></span> |<span data-ttu-id="825eb-1727">Specify user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="825eb-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="825eb-1728">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="825eb-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="825eb-1729">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1729">password</span></span> |<span data-ttu-id="825eb-1730">Specify password for the user account.</span><span class="sxs-lookup"><span data-stu-id="825eb-1730">Specify password for the user account.</span></span> |<span data-ttu-id="825eb-1731">Yes, if authenticationType is set to Basic.</span><span class="sxs-lookup"><span data-stu-id="825eb-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="825eb-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1732">gatewayName</span></span> |<span data-ttu-id="825eb-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="825eb-1734">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1734">Yes</span></span> |
| <span data-ttu-id="825eb-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-1735">encryptedCredential</span></span> |<span data-ttu-id="825eb-1736">Credential encrypted by the gateway.</span><span class="sxs-lookup"><span data-stu-id="825eb-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="825eb-1737">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1738">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1738">Example</span></span>

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

<span data-ttu-id="825eb-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-1740">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1740">Dataset</span></span>
<span data-ttu-id="825eb-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1742">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1742">Property</span></span> | <span data-ttu-id="825eb-1743">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1743">Description</span></span> | <span data-ttu-id="825eb-1744">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="825eb-1745">keyspace</span></span> |<span data-ttu-id="825eb-1746">Name of the keyspace or schema in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="825eb-1747">Yes (If **query** for **CassandraSource** is not defined).</span><span class="sxs-lookup"><span data-stu-id="825eb-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="825eb-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-1748">tableName</span></span> |<span data-ttu-id="825eb-1749">Name of the table in Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="825eb-1750">Yes (If **query** for **CassandraSource** is not defined).</span><span class="sxs-lookup"><span data-stu-id="825eb-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1751">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1751">Example</span></span>

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

<span data-ttu-id="825eb-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="825eb-1753">Cassandra Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-1755">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1755">Property</span></span> | <span data-ttu-id="825eb-1756">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1756">Description</span></span> | <span data-ttu-id="825eb-1757">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1757">Allowed values</span></span> | <span data-ttu-id="825eb-1758">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1759">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1759">query</span></span> |<span data-ttu-id="825eb-1760">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1761">SQL-92 query or CQL query.</span><span class="sxs-lookup"><span data-stu-id="825eb-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="825eb-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="825eb-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="825eb-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span><span class="sxs-lookup"><span data-stu-id="825eb-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="825eb-1764">No (if tableName and keyspace on dataset are defined).</span><span class="sxs-lookup"><span data-stu-id="825eb-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="825eb-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="825eb-1765">consistencyLevel</span></span> |<span data-ttu-id="825eb-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span><span class="sxs-lookup"><span data-stu-id="825eb-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="825eb-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span><span class="sxs-lookup"><span data-stu-id="825eb-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="825eb-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="825eb-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="825eb-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span><span class="sxs-lookup"><span data-stu-id="825eb-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="825eb-1770">No.</span><span class="sxs-lookup"><span data-stu-id="825eb-1770">No.</span></span> <span data-ttu-id="825eb-1771">Default value is ONE.</span><span class="sxs-lookup"><span data-stu-id="825eb-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1772">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1772">Example</span></span>
  
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

<span data-ttu-id="825eb-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="825eb-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="825eb-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-1775">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1775">Linked service</span></span>
<span data-ttu-id="825eb-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1777">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1777">Property</span></span> | <span data-ttu-id="825eb-1778">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1778">Description</span></span> | <span data-ttu-id="825eb-1779">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1780">server</span><span class="sxs-lookup"><span data-stu-id="825eb-1780">server</span></span> |<span data-ttu-id="825eb-1781">IP address or host name of the MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="825eb-1782">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1782">Yes</span></span> |
| <span data-ttu-id="825eb-1783">port</span><span class="sxs-lookup"><span data-stu-id="825eb-1783">port</span></span> |<span data-ttu-id="825eb-1784">TCP port that the MongoDB server uses to listen for client connections.</span><span class="sxs-lookup"><span data-stu-id="825eb-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="825eb-1785">Optional, default value: 27017</span><span class="sxs-lookup"><span data-stu-id="825eb-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="825eb-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-1786">authenticationType</span></span> |<span data-ttu-id="825eb-1787">Basic, or Anonymous.</span><span class="sxs-lookup"><span data-stu-id="825eb-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="825eb-1788">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1788">Yes</span></span> |
| <span data-ttu-id="825eb-1789">username</span><span class="sxs-lookup"><span data-stu-id="825eb-1789">username</span></span> |<span data-ttu-id="825eb-1790">User account to access MongoDB.</span><span class="sxs-lookup"><span data-stu-id="825eb-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="825eb-1791">Yes (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="825eb-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="825eb-1792">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1792">password</span></span> |<span data-ttu-id="825eb-1793">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="825eb-1793">Password for the user.</span></span> |<span data-ttu-id="825eb-1794">Yes (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="825eb-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="825eb-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="825eb-1795">authSource</span></span> |<span data-ttu-id="825eb-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="825eb-1797">Optional (if basic authentication is used).</span><span class="sxs-lookup"><span data-stu-id="825eb-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="825eb-1798">default: uses the admin account and the database specified using databaseName property.</span><span class="sxs-lookup"><span data-stu-id="825eb-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="825eb-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="825eb-1799">databaseName</span></span> |<span data-ttu-id="825eb-1800">Name of the MongoDB database that you want to access.</span><span class="sxs-lookup"><span data-stu-id="825eb-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="825eb-1801">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1801">Yes</span></span> |
| <span data-ttu-id="825eb-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1802">gatewayName</span></span> |<span data-ttu-id="825eb-1803">Name of the gateway that accesses the data store.</span><span class="sxs-lookup"><span data-stu-id="825eb-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="825eb-1804">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1804">Yes</span></span> |
| <span data-ttu-id="825eb-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-1805">encryptedCredential</span></span> |<span data-ttu-id="825eb-1806">Credential encrypted by gateway.</span><span class="sxs-lookup"><span data-stu-id="825eb-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="825eb-1807">Optional</span><span class="sxs-lookup"><span data-stu-id="825eb-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1808">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1808">Example</span></span>

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

<span data-ttu-id="825eb-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="825eb-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-1810">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1810">Dataset</span></span>
<span data-ttu-id="825eb-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1812">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1812">Property</span></span> | <span data-ttu-id="825eb-1813">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1813">Description</span></span> | <span data-ttu-id="825eb-1814">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="825eb-1815">collectionName</span></span> |<span data-ttu-id="825eb-1816">Name of the collection in MongoDB database.</span><span class="sxs-lookup"><span data-stu-id="825eb-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="825eb-1817">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1818">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1818">Example</span></span>

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

<span data-ttu-id="825eb-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="825eb-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="825eb-1820">MongoDB Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-1822">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1822">Property</span></span> | <span data-ttu-id="825eb-1823">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1823">Description</span></span> | <span data-ttu-id="825eb-1824">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1824">Allowed values</span></span> | <span data-ttu-id="825eb-1825">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1826">query</span><span class="sxs-lookup"><span data-stu-id="825eb-1826">query</span></span> |<span data-ttu-id="825eb-1827">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-1828">SQL-92 query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1828">SQL-92 query string.</span></span> <span data-ttu-id="825eb-1829">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="825eb-1830">No (if **collectionName** of **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1831">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1831">Example</span></span>

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

<span data-ttu-id="825eb-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="825eb-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="825eb-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="825eb-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="825eb-1834">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1834">Linked service</span></span>
<span data-ttu-id="825eb-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-1836">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1836">Property</span></span> | <span data-ttu-id="825eb-1837">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1837">Description</span></span> | <span data-ttu-id="825eb-1838">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1838">Allowed values</span></span> | <span data-ttu-id="825eb-1839">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="825eb-1840">accessKeyID</span></span> |<span data-ttu-id="825eb-1841">ID of the secret access key.</span><span class="sxs-lookup"><span data-stu-id="825eb-1841">ID of the secret access key.</span></span> |<span data-ttu-id="825eb-1842">string</span><span class="sxs-lookup"><span data-stu-id="825eb-1842">string</span></span> |<span data-ttu-id="825eb-1843">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1843">Yes</span></span> |
| <span data-ttu-id="825eb-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="825eb-1844">secretAccessKey</span></span> |<span data-ttu-id="825eb-1845">The secret access key itself.</span><span class="sxs-lookup"><span data-stu-id="825eb-1845">The secret access key itself.</span></span> |<span data-ttu-id="825eb-1846">Encrypted secret string</span><span class="sxs-lookup"><span data-stu-id="825eb-1846">Encrypted secret string</span></span> |<span data-ttu-id="825eb-1847">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-1848">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1848">Example</span></span>
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

<span data-ttu-id="825eb-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="825eb-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-1850">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1850">Dataset</span></span>
<span data-ttu-id="825eb-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1852">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1852">Property</span></span> | <span data-ttu-id="825eb-1853">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1853">Description</span></span> | <span data-ttu-id="825eb-1854">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1854">Allowed values</span></span> | <span data-ttu-id="825eb-1855">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="825eb-1856">bucketName</span></span> |<span data-ttu-id="825eb-1857">The S3 bucket name.</span><span class="sxs-lookup"><span data-stu-id="825eb-1857">The S3 bucket name.</span></span> |<span data-ttu-id="825eb-1858">String</span><span class="sxs-lookup"><span data-stu-id="825eb-1858">String</span></span> |<span data-ttu-id="825eb-1859">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1859">Yes</span></span> |
| <span data-ttu-id="825eb-1860">key</span><span class="sxs-lookup"><span data-stu-id="825eb-1860">key</span></span> |<span data-ttu-id="825eb-1861">The S3 object key.</span><span class="sxs-lookup"><span data-stu-id="825eb-1861">The S3 object key.</span></span> |<span data-ttu-id="825eb-1862">String</span><span class="sxs-lookup"><span data-stu-id="825eb-1862">String</span></span> |<span data-ttu-id="825eb-1863">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1863">No</span></span> |
| <span data-ttu-id="825eb-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="825eb-1864">prefix</span></span> |<span data-ttu-id="825eb-1865">Prefix for the S3 object key.</span><span class="sxs-lookup"><span data-stu-id="825eb-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="825eb-1866">Objects whose keys start with this prefix are selected.</span><span class="sxs-lookup"><span data-stu-id="825eb-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="825eb-1867">Applies only when key is empty.</span><span class="sxs-lookup"><span data-stu-id="825eb-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="825eb-1868">String</span><span class="sxs-lookup"><span data-stu-id="825eb-1868">String</span></span> |<span data-ttu-id="825eb-1869">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1869">No</span></span> |
| <span data-ttu-id="825eb-1870">version</span><span class="sxs-lookup"><span data-stu-id="825eb-1870">version</span></span> |<span data-ttu-id="825eb-1871">The version of S3 object if S3 versioning is enabled.</span><span class="sxs-lookup"><span data-stu-id="825eb-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="825eb-1872">String</span><span class="sxs-lookup"><span data-stu-id="825eb-1872">String</span></span> |<span data-ttu-id="825eb-1873">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1873">No</span></span> |
| <span data-ttu-id="825eb-1874">format</span><span class="sxs-lookup"><span data-stu-id="825eb-1874">format</span></span> | <span data-ttu-id="825eb-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="825eb-1876">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="825eb-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="825eb-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="825eb-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="825eb-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="825eb-1879">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1879">No</span></span> | |
| <span data-ttu-id="825eb-1880">compression</span><span class="sxs-lookup"><span data-stu-id="825eb-1880">compression</span></span> | <span data-ttu-id="825eb-1881">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="825eb-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="825eb-1883">The supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="825eb-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="825eb-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="825eb-1885">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="825eb-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span><span class="sxs-lookup"><span data-stu-id="825eb-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="825eb-1887">Example: Sample dataset with prefix</span><span class="sxs-lookup"><span data-stu-id="825eb-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="825eb-1888">Example: Sample data set (with version)</span><span class="sxs-lookup"><span data-stu-id="825eb-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="825eb-1889">Example: Dynamic paths for S3</span><span class="sxs-lookup"><span data-stu-id="825eb-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="825eb-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="825eb-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span><span class="sxs-lookup"><span data-stu-id="825eb-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="825eb-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="825eb-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span><span class="sxs-lookup"><span data-stu-id="825eb-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="825eb-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="825eb-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="825eb-1895">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="825eb-1897">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1897">Property</span></span> | <span data-ttu-id="825eb-1898">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1898">Description</span></span> | <span data-ttu-id="825eb-1899">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1899">Allowed values</span></span> | <span data-ttu-id="825eb-1900">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="825eb-1901">recursive</span></span> |<span data-ttu-id="825eb-1902">Specifies whether to recursively list S3 objects under the directory.</span><span class="sxs-lookup"><span data-stu-id="825eb-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="825eb-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="825eb-1903">true/false</span></span> |<span data-ttu-id="825eb-1904">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="825eb-1905">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1905">Example</span></span>


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

<span data-ttu-id="825eb-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="825eb-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="825eb-1907">File System</span><span class="sxs-lookup"><span data-stu-id="825eb-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="825eb-1908">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-1908">Linked service</span></span>
<span data-ttu-id="825eb-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="825eb-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="825eb-1911">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1911">Property</span></span> | <span data-ttu-id="825eb-1912">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1912">Description</span></span> | <span data-ttu-id="825eb-1913">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1914">type</span><span class="sxs-lookup"><span data-stu-id="825eb-1914">type</span></span> |<span data-ttu-id="825eb-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="825eb-1916">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1916">Yes</span></span> |
| <span data-ttu-id="825eb-1917">host</span><span class="sxs-lookup"><span data-stu-id="825eb-1917">host</span></span> |<span data-ttu-id="825eb-1918">Specifies the root path of the folder that you want to copy.</span><span class="sxs-lookup"><span data-stu-id="825eb-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="825eb-1919">Use the escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="825eb-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="825eb-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="825eb-1921">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1921">Yes</span></span> |
| <span data-ttu-id="825eb-1922">userid</span><span class="sxs-lookup"><span data-stu-id="825eb-1922">userid</span></span> |<span data-ttu-id="825eb-1923">Specify the ID of the user who has access to the server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="825eb-1924">No (if you choose encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="825eb-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="825eb-1925">password</span><span class="sxs-lookup"><span data-stu-id="825eb-1925">password</span></span> |<span data-ttu-id="825eb-1926">Specify the password for the user (userid).</span><span class="sxs-lookup"><span data-stu-id="825eb-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="825eb-1927">No (if you choose encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="825eb-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-1928">encryptedCredential</span></span> |<span data-ttu-id="825eb-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="825eb-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="825eb-1930">No (if you choose to specify userid and password in plain text)</span><span class="sxs-lookup"><span data-stu-id="825eb-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="825eb-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-1931">gatewayName</span></span> |<span data-ttu-id="825eb-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span><span class="sxs-lookup"><span data-stu-id="825eb-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="825eb-1933">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="825eb-1934">Sample folder path definitions</span><span class="sxs-lookup"><span data-stu-id="825eb-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="825eb-1935">Scenario</span><span class="sxs-lookup"><span data-stu-id="825eb-1935">Scenario</span></span> | <span data-ttu-id="825eb-1936">Host in linked service definition</span><span class="sxs-lookup"><span data-stu-id="825eb-1936">Host in linked service definition</span></span> | <span data-ttu-id="825eb-1937">folderPath in dataset definition</span><span class="sxs-lookup"><span data-stu-id="825eb-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1938">Local folder on Data Management Gateway machine:</span><span class="sxs-lookup"><span data-stu-id="825eb-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="825eb-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="825eb-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="825eb-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span><span class="sxs-lookup"><span data-stu-id="825eb-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="825eb-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="825eb-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="825eb-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span><span class="sxs-lookup"><span data-stu-id="825eb-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="825eb-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span><span class="sxs-lookup"><span data-stu-id="825eb-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="825eb-1944">Remote shared folder:</span><span class="sxs-lookup"><span data-stu-id="825eb-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="825eb-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="825eb-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="825eb-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="825eb-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="825eb-1947">.\\\\ or folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="825eb-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="825eb-1948">Example: Using username and password in plain text</span><span class="sxs-lookup"><span data-stu-id="825eb-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="825eb-1949">Example: Using encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="825eb-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="825eb-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="825eb-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-1951">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-1951">Dataset</span></span>
<span data-ttu-id="825eb-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-1953">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1953">Property</span></span> | <span data-ttu-id="825eb-1954">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1954">Description</span></span> | <span data-ttu-id="825eb-1955">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="825eb-1956">folderPath</span></span> |<span data-ttu-id="825eb-1957">Specifies the subpath to the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="825eb-1958">Use the escape character ‘\’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="825eb-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="825eb-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="825eb-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="825eb-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="825eb-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="825eb-1961">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-1961">Yes</span></span> |
| <span data-ttu-id="825eb-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="825eb-1962">fileName</span></span> |<span data-ttu-id="825eb-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="825eb-1964">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="825eb-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span><span class="sxs-lookup"><span data-stu-id="825eb-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="825eb-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="825eb-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="825eb-1967">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1967">No</span></span> |
| <span data-ttu-id="825eb-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="825eb-1968">fileFilter</span></span> |<span data-ttu-id="825eb-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="825eb-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="825eb-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="825eb-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="825eb-1971">Example 1: "fileFilter": "\*.log"</span><span class="sxs-lookup"><span data-stu-id="825eb-1971">Example 1: "fileFilter": "\*.log"</span></span><br/><span data-ttu-id="825eb-1972">Example 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="825eb-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="825eb-1973">Note that fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="825eb-1974">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1974">No</span></span> |
| <span data-ttu-id="825eb-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="825eb-1975">partitionedBy</span></span> |<span data-ttu-id="825eb-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="825eb-1977">An example is folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="825eb-1978">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1978">No</span></span> |
| <span data-ttu-id="825eb-1979">format</span><span class="sxs-lookup"><span data-stu-id="825eb-1979">format</span></span> | <span data-ttu-id="825eb-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="825eb-1981">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="825eb-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="825eb-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="825eb-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="825eb-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="825eb-1984">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1984">No</span></span> |
| <span data-ttu-id="825eb-1985">compression</span><span class="sxs-lookup"><span data-stu-id="825eb-1985">compression</span></span> | <span data-ttu-id="825eb-1986">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="825eb-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="825eb-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="825eb-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="825eb-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="825eb-1989">No</span><span class="sxs-lookup"><span data-stu-id="825eb-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="825eb-1990">You cannot use fileName and fileFilter simultaneously.</span><span class="sxs-lookup"><span data-stu-id="825eb-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="825eb-1991">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-1991">Example</span></span>

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

<span data-ttu-id="825eb-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="825eb-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="825eb-1993">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="825eb-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-1995">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-1995">Property</span></span> | <span data-ttu-id="825eb-1996">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-1996">Description</span></span> | <span data-ttu-id="825eb-1997">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-1997">Allowed values</span></span> | <span data-ttu-id="825eb-1998">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="825eb-1999">recursive</span></span> |<span data-ttu-id="825eb-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="825eb-2001">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="825eb-2001">True, False (default)</span></span> |<span data-ttu-id="825eb-2002">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2003">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2003">Example</span></span>

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
<span data-ttu-id="825eb-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="825eb-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="825eb-2005">File System Sink in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="825eb-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="825eb-2007">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2007">Property</span></span> | <span data-ttu-id="825eb-2008">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2008">Description</span></span> | <span data-ttu-id="825eb-2009">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-2009">Allowed values</span></span> | <span data-ttu-id="825eb-2010">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="825eb-2011">copyBehavior</span></span> |<span data-ttu-id="825eb-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span><span class="sxs-lookup"><span data-stu-id="825eb-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="825eb-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="825eb-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="825eb-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="825eb-2016">The target files are created with an autogenerated name.</span><span class="sxs-lookup"><span data-stu-id="825eb-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="825eb-2017">**MergeFiles:** Merges all files from the source folder to one file.</span><span class="sxs-lookup"><span data-stu-id="825eb-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="825eb-2018">If the file name/blob name is specified, the merged file name is the specified name.</span><span class="sxs-lookup"><span data-stu-id="825eb-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="825eb-2019">Otherwise, it is an auto-generated file name.</span><span class="sxs-lookup"><span data-stu-id="825eb-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="825eb-2020">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2020">No</span></span> |
<span data-ttu-id="825eb-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="825eb-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="825eb-2022">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2022">Example</span></span>

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

<span data-ttu-id="825eb-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="825eb-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="825eb-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="825eb-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-2025">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2025">Linked service</span></span>
<span data-ttu-id="825eb-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2027">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2027">Property</span></span> | <span data-ttu-id="825eb-2028">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2028">Description</span></span> | <span data-ttu-id="825eb-2029">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2029">Required</span></span> | <span data-ttu-id="825eb-2030">Default</span><span class="sxs-lookup"><span data-stu-id="825eb-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2031">host</span><span class="sxs-lookup"><span data-stu-id="825eb-2031">host</span></span> |<span data-ttu-id="825eb-2032">Name or IP address of the FTP Server</span><span class="sxs-lookup"><span data-stu-id="825eb-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="825eb-2033">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="825eb-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-2034">authenticationType</span></span> |<span data-ttu-id="825eb-2035">Specify authentication type</span><span class="sxs-lookup"><span data-stu-id="825eb-2035">Specify authentication type</span></span> |<span data-ttu-id="825eb-2036">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2036">Yes</span></span> |<span data-ttu-id="825eb-2037">Basic, Anonymous</span><span class="sxs-lookup"><span data-stu-id="825eb-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="825eb-2038">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2038">username</span></span> |<span data-ttu-id="825eb-2039">User who has access to the FTP server</span><span class="sxs-lookup"><span data-stu-id="825eb-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="825eb-2040">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="825eb-2041">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2041">password</span></span> |<span data-ttu-id="825eb-2042">Password for the user (username)</span><span class="sxs-lookup"><span data-stu-id="825eb-2042">Password for the user (username)</span></span> |<span data-ttu-id="825eb-2043">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="825eb-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-2044">encryptedCredential</span></span> |<span data-ttu-id="825eb-2045">Encrypted credential to access the FTP server</span><span class="sxs-lookup"><span data-stu-id="825eb-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="825eb-2046">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="825eb-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-2047">gatewayName</span></span> |<span data-ttu-id="825eb-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span><span class="sxs-lookup"><span data-stu-id="825eb-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="825eb-2049">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="825eb-2050">port</span><span class="sxs-lookup"><span data-stu-id="825eb-2050">port</span></span> |<span data-ttu-id="825eb-2051">Port on which the FTP server is listening</span><span class="sxs-lookup"><span data-stu-id="825eb-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="825eb-2052">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2052">No</span></span> |<span data-ttu-id="825eb-2053">21</span><span class="sxs-lookup"><span data-stu-id="825eb-2053">21</span></span> |
| <span data-ttu-id="825eb-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="825eb-2054">enableSsl</span></span> |<span data-ttu-id="825eb-2055">Specify whether to use FTP over SSL/TLS channel</span><span class="sxs-lookup"><span data-stu-id="825eb-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="825eb-2056">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2056">No</span></span> |<span data-ttu-id="825eb-2057">true</span><span class="sxs-lookup"><span data-stu-id="825eb-2057">true</span></span> |
| <span data-ttu-id="825eb-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="825eb-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="825eb-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span><span class="sxs-lookup"><span data-stu-id="825eb-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="825eb-2060">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2060">No</span></span> |<span data-ttu-id="825eb-2061">true</span><span class="sxs-lookup"><span data-stu-id="825eb-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="825eb-2062">Example: Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="825eb-2063">Example: Using username and password in plain text for basic authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="825eb-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="825eb-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="825eb-2065">Example: Using encryptedCredential for authentication and gateway</span><span class="sxs-lookup"><span data-stu-id="825eb-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="825eb-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-2067">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-2067">Dataset</span></span>
<span data-ttu-id="825eb-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-2069">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2069">Property</span></span> | <span data-ttu-id="825eb-2070">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2070">Description</span></span> | <span data-ttu-id="825eb-2071">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="825eb-2072">folderPath</span></span> |<span data-ttu-id="825eb-2073">Sub path to the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2073">Sub path to the folder.</span></span> <span data-ttu-id="825eb-2074">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="825eb-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="825eb-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="825eb-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="825eb-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="825eb-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="825eb-2077">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2077">Yes</span></span> 
| <span data-ttu-id="825eb-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="825eb-2078">fileName</span></span> |<span data-ttu-id="825eb-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="825eb-2080">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="825eb-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span><span class="sxs-lookup"><span data-stu-id="825eb-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="825eb-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="825eb-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="825eb-2083">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2083">No</span></span> |
| <span data-ttu-id="825eb-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="825eb-2084">fileFilter</span></span> |<span data-ttu-id="825eb-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="825eb-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="825eb-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="825eb-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="825eb-2087">Examples 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="825eb-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="825eb-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="825eb-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="825eb-2089">fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="825eb-2090">This property is not supported with HDFS.</span><span class="sxs-lookup"><span data-stu-id="825eb-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="825eb-2091">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2091">No</span></span> |
| <span data-ttu-id="825eb-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="825eb-2092">partitionedBy</span></span> |<span data-ttu-id="825eb-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="825eb-2094">For example, folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="825eb-2095">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2095">No</span></span> |
| <span data-ttu-id="825eb-2096">format</span><span class="sxs-lookup"><span data-stu-id="825eb-2096">format</span></span> | <span data-ttu-id="825eb-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="825eb-2098">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="825eb-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="825eb-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="825eb-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="825eb-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="825eb-2101">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2101">No</span></span> |
| <span data-ttu-id="825eb-2102">compression</span><span class="sxs-lookup"><span data-stu-id="825eb-2102">compression</span></span> | <span data-ttu-id="825eb-2103">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="825eb-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="825eb-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="825eb-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="825eb-2106">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2106">No</span></span> |
| <span data-ttu-id="825eb-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="825eb-2107">useBinaryTransfer</span></span> |<span data-ttu-id="825eb-2108">Specify whether use Binary transfer mode.</span><span class="sxs-lookup"><span data-stu-id="825eb-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="825eb-2109">True for binary mode and false ASCII.</span><span class="sxs-lookup"><span data-stu-id="825eb-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="825eb-2110">Default value: True.</span><span class="sxs-lookup"><span data-stu-id="825eb-2110">Default value: True.</span></span> <span data-ttu-id="825eb-2111">This property can only be used when associated linked service type is of type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="825eb-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="825eb-2112">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="825eb-2113">filename and fileFilter cannot be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="825eb-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="825eb-2114">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2114">Example</span></span>

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

<span data-ttu-id="825eb-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="825eb-2116">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="825eb-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-2118">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2118">Property</span></span> | <span data-ttu-id="825eb-2119">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2119">Description</span></span> | <span data-ttu-id="825eb-2120">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-2120">Allowed values</span></span> | <span data-ttu-id="825eb-2121">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="825eb-2122">recursive</span></span> |<span data-ttu-id="825eb-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="825eb-2124">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="825eb-2124">True, False (default)</span></span> |<span data-ttu-id="825eb-2125">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2126">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2126">Example</span></span>

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

<span data-ttu-id="825eb-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="825eb-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="825eb-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-2129">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2129">Linked service</span></span>
<span data-ttu-id="825eb-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2131">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2131">Property</span></span> | <span data-ttu-id="825eb-2132">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2132">Description</span></span> | <span data-ttu-id="825eb-2133">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2134">type</span><span class="sxs-lookup"><span data-stu-id="825eb-2134">type</span></span> |<span data-ttu-id="825eb-2135">The type property must be set to: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="825eb-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="825eb-2136">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2136">Yes</span></span> |
| <span data-ttu-id="825eb-2137">Url</span><span class="sxs-lookup"><span data-stu-id="825eb-2137">Url</span></span> |<span data-ttu-id="825eb-2138">URL to the HDFS</span><span class="sxs-lookup"><span data-stu-id="825eb-2138">URL to the HDFS</span></span> |<span data-ttu-id="825eb-2139">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2139">Yes</span></span> |
| <span data-ttu-id="825eb-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-2140">authenticationType</span></span> |<span data-ttu-id="825eb-2141">Anonymous, or Windows.</span><span class="sxs-lookup"><span data-stu-id="825eb-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="825eb-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span><span class="sxs-lookup"><span data-stu-id="825eb-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="825eb-2143">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2143">Yes</span></span> |
| <span data-ttu-id="825eb-2144">userName</span><span class="sxs-lookup"><span data-stu-id="825eb-2144">userName</span></span> |<span data-ttu-id="825eb-2145">Username for Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="825eb-2146">Yes (for Windows Authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="825eb-2147">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2147">password</span></span> |<span data-ttu-id="825eb-2148">Password for Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="825eb-2149">Yes (for Windows Authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="825eb-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-2150">gatewayName</span></span> |<span data-ttu-id="825eb-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span><span class="sxs-lookup"><span data-stu-id="825eb-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="825eb-2152">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2152">Yes</span></span> |
| <span data-ttu-id="825eb-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-2153">encryptedCredential</span></span> |<span data-ttu-id="825eb-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span><span class="sxs-lookup"><span data-stu-id="825eb-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="825eb-2155">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="825eb-2156">Example: Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="825eb-2157">Example: Using Windows authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="825eb-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-2159">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-2159">Dataset</span></span>
<span data-ttu-id="825eb-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-2161">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2161">Property</span></span> | <span data-ttu-id="825eb-2162">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2162">Description</span></span> | <span data-ttu-id="825eb-2163">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="825eb-2164">folderPath</span></span> |<span data-ttu-id="825eb-2165">Path to the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2165">Path to the folder.</span></span> <span data-ttu-id="825eb-2166">Example: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="825eb-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="825eb-2167">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="825eb-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="825eb-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="825eb-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="825eb-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="825eb-2170">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2170">Yes</span></span> |
| <span data-ttu-id="825eb-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="825eb-2171">fileName</span></span> |<span data-ttu-id="825eb-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="825eb-2173">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="825eb-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span><span class="sxs-lookup"><span data-stu-id="825eb-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="825eb-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="825eb-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="825eb-2176">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2176">No</span></span> |
| <span data-ttu-id="825eb-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="825eb-2177">partitionedBy</span></span> |<span data-ttu-id="825eb-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="825eb-2179">Example: folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="825eb-2180">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2180">No</span></span> |
| <span data-ttu-id="825eb-2181">format</span><span class="sxs-lookup"><span data-stu-id="825eb-2181">format</span></span> | <span data-ttu-id="825eb-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="825eb-2183">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="825eb-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="825eb-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="825eb-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="825eb-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="825eb-2186">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2186">No</span></span> |
| <span data-ttu-id="825eb-2187">compression</span><span class="sxs-lookup"><span data-stu-id="825eb-2187">compression</span></span> | <span data-ttu-id="825eb-2188">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="825eb-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="825eb-2190">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="825eb-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="825eb-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="825eb-2192">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="825eb-2193">filename and fileFilter cannot be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="825eb-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="825eb-2194">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2194">Example</span></span>

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

<span data-ttu-id="825eb-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="825eb-2196">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="825eb-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="825eb-2198">**FileSystemSource** supports the following properties:</span><span class="sxs-lookup"><span data-stu-id="825eb-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="825eb-2199">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2199">Property</span></span> | <span data-ttu-id="825eb-2200">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2200">Description</span></span> | <span data-ttu-id="825eb-2201">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-2201">Allowed values</span></span> | <span data-ttu-id="825eb-2202">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="825eb-2203">recursive</span></span> |<span data-ttu-id="825eb-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="825eb-2205">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="825eb-2205">True, False (default)</span></span> |<span data-ttu-id="825eb-2206">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2207">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2207">Example</span></span>

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

<span data-ttu-id="825eb-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="825eb-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="825eb-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="825eb-2210">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2210">Linked service</span></span>
<span data-ttu-id="825eb-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2212">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2212">Property</span></span> | <span data-ttu-id="825eb-2213">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2213">Description</span></span> | <span data-ttu-id="825eb-2214">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2215">host</span><span class="sxs-lookup"><span data-stu-id="825eb-2215">host</span></span> | <span data-ttu-id="825eb-2216">Name or IP address of the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="825eb-2217">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2217">Yes</span></span> |
| <span data-ttu-id="825eb-2218">port</span><span class="sxs-lookup"><span data-stu-id="825eb-2218">port</span></span> |<span data-ttu-id="825eb-2219">Port on which the SFTP server is listening.</span><span class="sxs-lookup"><span data-stu-id="825eb-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="825eb-2220">The default value is: 21</span><span class="sxs-lookup"><span data-stu-id="825eb-2220">The default value is: 21</span></span> |<span data-ttu-id="825eb-2221">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2221">No</span></span> |
| <span data-ttu-id="825eb-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-2222">authenticationType</span></span> |<span data-ttu-id="825eb-2223">Specify authentication type.</span><span class="sxs-lookup"><span data-stu-id="825eb-2223">Specify authentication type.</span></span> <span data-ttu-id="825eb-2224">Allowed values: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="825eb-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span><span class="sxs-lookup"><span data-stu-id="825eb-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="825eb-2226">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2226">Yes</span></span> |
| <span data-ttu-id="825eb-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="825eb-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="825eb-2228">Specify whether to skip host key validation.</span><span class="sxs-lookup"><span data-stu-id="825eb-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="825eb-2229">No.</span><span class="sxs-lookup"><span data-stu-id="825eb-2229">No.</span></span> <span data-ttu-id="825eb-2230">The default value: false</span><span class="sxs-lookup"><span data-stu-id="825eb-2230">The default value: false</span></span> |
| <span data-ttu-id="825eb-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="825eb-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="825eb-2232">Specify the finger print of the host key.</span><span class="sxs-lookup"><span data-stu-id="825eb-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="825eb-2233">Yes if the `skipHostKeyValidation` is set to false.</span><span class="sxs-lookup"><span data-stu-id="825eb-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="825eb-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-2234">gatewayName</span></span> |<span data-ttu-id="825eb-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="825eb-2236">Yes if copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="825eb-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-2237">encryptedCredential</span></span> | <span data-ttu-id="825eb-2238">Encrypted credential to access the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="825eb-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span><span class="sxs-lookup"><span data-stu-id="825eb-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="825eb-2240">No.</span><span class="sxs-lookup"><span data-stu-id="825eb-2240">No.</span></span> <span data-ttu-id="825eb-2241">Apply only when copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="825eb-2242">Example: Using basic authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="825eb-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="825eb-2244">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2244">Property</span></span> | <span data-ttu-id="825eb-2245">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2245">Description</span></span> | <span data-ttu-id="825eb-2246">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2247">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2247">username</span></span> | <span data-ttu-id="825eb-2248">User who has access to the SFTP server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="825eb-2249">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2249">Yes</span></span> |
| <span data-ttu-id="825eb-2250">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2250">password</span></span> | <span data-ttu-id="825eb-2251">Password for the user (username).</span><span class="sxs-lookup"><span data-stu-id="825eb-2251">Password for the user (username).</span></span> | <span data-ttu-id="825eb-2252">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="825eb-2253">Example: Basic authentication with encrypted credential\*\*</span><span class="sxs-lookup"><span data-stu-id="825eb-2253">Example: Basic authentication with encrypted credential\*\*</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="825eb-2254">Using SSH public key authentication:\*\*</span><span class="sxs-lookup"><span data-stu-id="825eb-2254">Using SSH public key authentication:\*\*</span></span>

<span data-ttu-id="825eb-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="825eb-2256">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2256">Property</span></span> | <span data-ttu-id="825eb-2257">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2257">Description</span></span> | <span data-ttu-id="825eb-2258">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2259">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2259">username</span></span> |<span data-ttu-id="825eb-2260">User who has access to the SFTP server</span><span class="sxs-lookup"><span data-stu-id="825eb-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="825eb-2261">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2261">Yes</span></span> |
| <span data-ttu-id="825eb-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="825eb-2262">privateKeyPath</span></span> | <span data-ttu-id="825eb-2263">Specify absolute path to the private key file that gateway can access.</span><span class="sxs-lookup"><span data-stu-id="825eb-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="825eb-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="825eb-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="825eb-2265">Apply only when copying data from an on-premises SFTP server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="825eb-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="825eb-2266">privateKeyContent</span></span> | <span data-ttu-id="825eb-2267">A serialized string of the private key content.</span><span class="sxs-lookup"><span data-stu-id="825eb-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="825eb-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span><span class="sxs-lookup"><span data-stu-id="825eb-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="825eb-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span><span class="sxs-lookup"><span data-stu-id="825eb-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="825eb-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="825eb-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="825eb-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="825eb-2271">passPhrase</span></span> | <span data-ttu-id="825eb-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span><span class="sxs-lookup"><span data-stu-id="825eb-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="825eb-2273">Yes if the private key file is protected by a pass phrase.</span><span class="sxs-lookup"><span data-stu-id="825eb-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="825eb-2274">Example: SshPublicKey authentication using private key content\*\*</span><span class="sxs-lookup"><span data-stu-id="825eb-2274">Example: SshPublicKey authentication using private key content\*\*</span></span>

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

<span data-ttu-id="825eb-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-2276">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-2276">Dataset</span></span>
<span data-ttu-id="825eb-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-2278">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2278">Property</span></span> | <span data-ttu-id="825eb-2279">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2279">Description</span></span> | <span data-ttu-id="825eb-2280">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="825eb-2281">folderPath</span></span> |<span data-ttu-id="825eb-2282">Sub path to the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2282">Sub path to the folder.</span></span> <span data-ttu-id="825eb-2283">Use escape character ‘ \ ’ for special characters in the string.</span><span class="sxs-lookup"><span data-stu-id="825eb-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="825eb-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span><span class="sxs-lookup"><span data-stu-id="825eb-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="825eb-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span><span class="sxs-lookup"><span data-stu-id="825eb-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="825eb-2286">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2286">Yes</span></span> |
| <span data-ttu-id="825eb-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="825eb-2287">fileName</span></span> |<span data-ttu-id="825eb-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="825eb-2289">If you do not specify any value for this property, the table points to all files in the folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="825eb-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span><span class="sxs-lookup"><span data-stu-id="825eb-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="825eb-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="825eb-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="825eb-2292">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2292">No</span></span> |
| <span data-ttu-id="825eb-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="825eb-2293">fileFilter</span></span> |<span data-ttu-id="825eb-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span><span class="sxs-lookup"><span data-stu-id="825eb-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="825eb-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span><span class="sxs-lookup"><span data-stu-id="825eb-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="825eb-2296">Examples 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="825eb-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="825eb-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="825eb-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="825eb-2298">fileFilter is applicable for an input FileShare dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="825eb-2299">This property is not supported with HDFS.</span><span class="sxs-lookup"><span data-stu-id="825eb-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="825eb-2300">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2300">No</span></span> |
| <span data-ttu-id="825eb-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="825eb-2301">partitionedBy</span></span> |<span data-ttu-id="825eb-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="825eb-2303">For example, folderPath parameterized for every hour of data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="825eb-2304">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2304">No</span></span> |
| <span data-ttu-id="825eb-2305">format</span><span class="sxs-lookup"><span data-stu-id="825eb-2305">format</span></span> | <span data-ttu-id="825eb-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="825eb-2307">Set the **type** property under format to one of these values.</span><span class="sxs-lookup"><span data-stu-id="825eb-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="825eb-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="825eb-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="825eb-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="825eb-2310">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2310">No</span></span> |
| <span data-ttu-id="825eb-2311">compression</span><span class="sxs-lookup"><span data-stu-id="825eb-2311">compression</span></span> | <span data-ttu-id="825eb-2312">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="825eb-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="825eb-2314">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="825eb-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="825eb-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="825eb-2316">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2316">No</span></span> |
| <span data-ttu-id="825eb-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="825eb-2317">useBinaryTransfer</span></span> |<span data-ttu-id="825eb-2318">Specify whether use Binary transfer mode.</span><span class="sxs-lookup"><span data-stu-id="825eb-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="825eb-2319">True for binary mode and false ASCII.</span><span class="sxs-lookup"><span data-stu-id="825eb-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="825eb-2320">Default value: True.</span><span class="sxs-lookup"><span data-stu-id="825eb-2320">Default value: True.</span></span> <span data-ttu-id="825eb-2321">This property can only be used when associated linked service type is of type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="825eb-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="825eb-2322">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="825eb-2323">filename and fileFilter cannot be used simultaneously.</span><span class="sxs-lookup"><span data-stu-id="825eb-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="825eb-2324">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2324">Example</span></span>

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

<span data-ttu-id="825eb-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="825eb-2326">File System Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="825eb-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-2328">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2328">Property</span></span> | <span data-ttu-id="825eb-2329">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2329">Description</span></span> | <span data-ttu-id="825eb-2330">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-2330">Allowed values</span></span> | <span data-ttu-id="825eb-2331">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="825eb-2332">recursive</span></span> |<span data-ttu-id="825eb-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span><span class="sxs-lookup"><span data-stu-id="825eb-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="825eb-2334">True, False (default)</span><span class="sxs-lookup"><span data-stu-id="825eb-2334">True, False (default)</span></span> |<span data-ttu-id="825eb-2335">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="825eb-2336">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2336">Example</span></span>

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

<span data-ttu-id="825eb-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="825eb-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="825eb-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-2339">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2339">Linked service</span></span>
<span data-ttu-id="825eb-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2341">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2341">Property</span></span> | <span data-ttu-id="825eb-2342">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2342">Description</span></span> | <span data-ttu-id="825eb-2343">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2344">url</span><span class="sxs-lookup"><span data-stu-id="825eb-2344">url</span></span> | <span data-ttu-id="825eb-2345">Base URL to the Web Server</span><span class="sxs-lookup"><span data-stu-id="825eb-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="825eb-2346">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2346">Yes</span></span> |
| <span data-ttu-id="825eb-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-2347">authenticationType</span></span> | <span data-ttu-id="825eb-2348">Specifies the authentication type.</span><span class="sxs-lookup"><span data-stu-id="825eb-2348">Specifies the authentication type.</span></span> <span data-ttu-id="825eb-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="825eb-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span><span class="sxs-lookup"><span data-stu-id="825eb-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="825eb-2351">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2351">Yes</span></span> |
| <span data-ttu-id="825eb-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="825eb-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="825eb-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span><span class="sxs-lookup"><span data-stu-id="825eb-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="825eb-2354">No, default is true</span><span class="sxs-lookup"><span data-stu-id="825eb-2354">No, default is true</span></span> |
| <span data-ttu-id="825eb-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-2355">gatewayName</span></span> | <span data-ttu-id="825eb-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="825eb-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="825eb-2357">Yes if copying data from an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="825eb-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="825eb-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-2358">encryptedCredential</span></span> | <span data-ttu-id="825eb-2359">Encrypted credential to access the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="825eb-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="825eb-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span><span class="sxs-lookup"><span data-stu-id="825eb-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="825eb-2361">No.</span><span class="sxs-lookup"><span data-stu-id="825eb-2361">No.</span></span> <span data-ttu-id="825eb-2362">Apply only when copying data from an on-premises HTTP server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="825eb-2363">Example: Using Basic, Digest, or Windows authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="825eb-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span><span class="sxs-lookup"><span data-stu-id="825eb-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="825eb-2365">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2365">Property</span></span> | <span data-ttu-id="825eb-2366">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2366">Description</span></span> | <span data-ttu-id="825eb-2367">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2368">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2368">username</span></span> | <span data-ttu-id="825eb-2369">Username to access the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="825eb-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="825eb-2370">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2370">Yes</span></span> |
| <span data-ttu-id="825eb-2371">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2371">password</span></span> | <span data-ttu-id="825eb-2372">Password for the user (username).</span><span class="sxs-lookup"><span data-stu-id="825eb-2372">Password for the user (username).</span></span> | <span data-ttu-id="825eb-2373">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="825eb-2374">Example: Using ClientCertificate authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="825eb-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span><span class="sxs-lookup"><span data-stu-id="825eb-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="825eb-2376">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2376">Property</span></span> | <span data-ttu-id="825eb-2377">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2377">Description</span></span> | <span data-ttu-id="825eb-2378">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="825eb-2379">embeddedCertData</span></span> | <span data-ttu-id="825eb-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span><span class="sxs-lookup"><span data-stu-id="825eb-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="825eb-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="825eb-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="825eb-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="825eb-2382">certThumbprint</span></span> | <span data-ttu-id="825eb-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span><span class="sxs-lookup"><span data-stu-id="825eb-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="825eb-2384">Apply only when copying data from an on-premises HTTP source.</span><span class="sxs-lookup"><span data-stu-id="825eb-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="825eb-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="825eb-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="825eb-2386">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2386">password</span></span> | <span data-ttu-id="825eb-2387">Password associated with the certificate.</span><span class="sxs-lookup"><span data-stu-id="825eb-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="825eb-2388">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2388">No</span></span> |

<span data-ttu-id="825eb-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span><span class="sxs-lookup"><span data-stu-id="825eb-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="825eb-2390">Launch Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="825eb-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="825eb-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="825eb-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="825eb-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span><span class="sxs-lookup"><span data-stu-id="825eb-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="825eb-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span><span class="sxs-lookup"><span data-stu-id="825eb-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="825eb-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="825eb-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span><span class="sxs-lookup"><span data-stu-id="825eb-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="825eb-2397">Example: using client certificate in a file</span><span class="sxs-lookup"><span data-stu-id="825eb-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="825eb-2398">This linked service links your data factory to an on-premises HTTP web server.</span><span class="sxs-lookup"><span data-stu-id="825eb-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="825eb-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span><span class="sxs-lookup"><span data-stu-id="825eb-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="825eb-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-2401">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-2401">Dataset</span></span>
<span data-ttu-id="825eb-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-2403">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2403">Property</span></span> | <span data-ttu-id="825eb-2404">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2404">Description</span></span> | <span data-ttu-id="825eb-2405">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="825eb-2406">relativeUrl</span></span> | <span data-ttu-id="825eb-2407">A relative URL to the resource that contains the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="825eb-2408">When path is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="825eb-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="825eb-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="825eb-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="825eb-2410">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2410">No</span></span> |
| <span data-ttu-id="825eb-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="825eb-2411">requestMethod</span></span> | <span data-ttu-id="825eb-2412">Http method.</span><span class="sxs-lookup"><span data-stu-id="825eb-2412">Http method.</span></span> <span data-ttu-id="825eb-2413">Allowed values are **GET** or **POST**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="825eb-2414">No.</span><span class="sxs-lookup"><span data-stu-id="825eb-2414">No.</span></span> <span data-ttu-id="825eb-2415">Default is `GET`.</span><span class="sxs-lookup"><span data-stu-id="825eb-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="825eb-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="825eb-2416">additionalHeaders</span></span> | <span data-ttu-id="825eb-2417">Additional HTTP request headers.</span><span class="sxs-lookup"><span data-stu-id="825eb-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="825eb-2418">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2418">No</span></span> |
| <span data-ttu-id="825eb-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="825eb-2419">requestBody</span></span> | <span data-ttu-id="825eb-2420">Body for HTTP request.</span><span class="sxs-lookup"><span data-stu-id="825eb-2420">Body for HTTP request.</span></span> | <span data-ttu-id="825eb-2421">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2421">No</span></span> |
| <span data-ttu-id="825eb-2422">format</span><span class="sxs-lookup"><span data-stu-id="825eb-2422">format</span></span> | <span data-ttu-id="825eb-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span><span class="sxs-lookup"><span data-stu-id="825eb-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="825eb-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="825eb-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="825eb-2426">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2426">No</span></span> |
| <span data-ttu-id="825eb-2427">compression</span><span class="sxs-lookup"><span data-stu-id="825eb-2427">compression</span></span> | <span data-ttu-id="825eb-2428">Specify the type and level of compression for the data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="825eb-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="825eb-2430">Supported levels are: **Optimal** and **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="825eb-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="825eb-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="825eb-2432">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="825eb-2433">Example: using the GET (default) method</span><span class="sxs-lookup"><span data-stu-id="825eb-2433">Example: using the GET (default) method</span></span>

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

#### <a name="example-using-the-post-method"></a><span data-ttu-id="825eb-2434">Example: using the POST method</span><span class="sxs-lookup"><span data-stu-id="825eb-2434">Example: using the POST method</span></span>

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
<span data-ttu-id="825eb-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="825eb-2436">HTTP Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="825eb-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-2438">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2438">Property</span></span> | <span data-ttu-id="825eb-2439">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2439">Description</span></span> | <span data-ttu-id="825eb-2440">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="825eb-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="825eb-2441">httpRequestTimeout</span></span> | <span data-ttu-id="825eb-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span><span class="sxs-lookup"><span data-stu-id="825eb-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="825eb-2443">It is the timeout to get a response, not the timeout to read response data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="825eb-2444">No.</span><span class="sxs-lookup"><span data-stu-id="825eb-2444">No.</span></span> <span data-ttu-id="825eb-2445">Default value: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="825eb-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="825eb-2446">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2446">Example</span></span>

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

<span data-ttu-id="825eb-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="825eb-2448">OData</span><span class="sxs-lookup"><span data-stu-id="825eb-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-2449">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2449">Linked service</span></span>
<span data-ttu-id="825eb-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2451">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2451">Property</span></span> | <span data-ttu-id="825eb-2452">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2452">Description</span></span> | <span data-ttu-id="825eb-2453">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2454">url</span><span class="sxs-lookup"><span data-stu-id="825eb-2454">url</span></span> |<span data-ttu-id="825eb-2455">Url of the OData service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2455">Url of the OData service.</span></span> |<span data-ttu-id="825eb-2456">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2456">Yes</span></span> |
| <span data-ttu-id="825eb-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-2457">authenticationType</span></span> |<span data-ttu-id="825eb-2458">Type of authentication used to connect to the OData source.</span><span class="sxs-lookup"><span data-stu-id="825eb-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="825eb-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span><span class="sxs-lookup"><span data-stu-id="825eb-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="825eb-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span><span class="sxs-lookup"><span data-stu-id="825eb-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="825eb-2461">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2461">Yes</span></span> |
| <span data-ttu-id="825eb-2462">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2462">username</span></span> |<span data-ttu-id="825eb-2463">Specify user name if you are using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="825eb-2464">Yes (only if you are using Basic authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="825eb-2465">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2465">password</span></span> |<span data-ttu-id="825eb-2466">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="825eb-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="825eb-2467">Yes (only if you are using Basic authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="825eb-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="825eb-2468">authorizedCredential</span></span> |<span data-ttu-id="825eb-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span><span class="sxs-lookup"><span data-stu-id="825eb-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="825eb-2470">Yes (only if you are using OAuth authentication)</span><span class="sxs-lookup"><span data-stu-id="825eb-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="825eb-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-2471">gatewayName</span></span> |<span data-ttu-id="825eb-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="825eb-2473">Specify only if you are copying data from on-prem OData source.</span><span class="sxs-lookup"><span data-stu-id="825eb-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="825eb-2474">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="825eb-2475">Example - Using Basic authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="825eb-2476">Example - Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="825eb-2477">Example - Using Windows authentication accessing on-premises OData source</span><span class="sxs-lookup"><span data-stu-id="825eb-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="825eb-2478">Example - Using OAuth authentication accessing cloud OData source</span><span class="sxs-lookup"><span data-stu-id="825eb-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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

<span data-ttu-id="825eb-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="825eb-2480">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-2480">Dataset</span></span>
<span data-ttu-id="825eb-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-2482">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2482">Property</span></span> | <span data-ttu-id="825eb-2483">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2483">Description</span></span> | <span data-ttu-id="825eb-2484">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2485">path</span><span class="sxs-lookup"><span data-stu-id="825eb-2485">path</span></span> |<span data-ttu-id="825eb-2486">Path to the OData resource</span><span class="sxs-lookup"><span data-stu-id="825eb-2486">Path to the OData resource</span></span> |<span data-ttu-id="825eb-2487">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2488">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2488">Example</span></span>

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

<span data-ttu-id="825eb-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-2490">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-2492">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2492">Property</span></span> | <span data-ttu-id="825eb-2493">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2493">Description</span></span> | <span data-ttu-id="825eb-2494">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2494">Example</span></span> | <span data-ttu-id="825eb-2495">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2496">query</span><span class="sxs-lookup"><span data-stu-id="825eb-2496">query</span></span> |<span data-ttu-id="825eb-2497">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="825eb-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="825eb-2499">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2500">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2500">Example</span></span>

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

<span data-ttu-id="825eb-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="825eb-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="825eb-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="825eb-2503">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2503">Linked service</span></span>
<span data-ttu-id="825eb-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2505">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2505">Property</span></span> | <span data-ttu-id="825eb-2506">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2506">Description</span></span> | <span data-ttu-id="825eb-2507">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-2508">connectionString</span></span> |<span data-ttu-id="825eb-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span><span class="sxs-lookup"><span data-stu-id="825eb-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="825eb-2510">See examples in the following sections.</span><span class="sxs-lookup"><span data-stu-id="825eb-2510">See examples in the following sections.</span></span> |<span data-ttu-id="825eb-2511">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2511">Yes</span></span> |
| <span data-ttu-id="825eb-2512">credential</span><span class="sxs-lookup"><span data-stu-id="825eb-2512">credential</span></span> |<span data-ttu-id="825eb-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span><span class="sxs-lookup"><span data-stu-id="825eb-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="825eb-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="825eb-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="825eb-2515">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2515">No</span></span> |
| <span data-ttu-id="825eb-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-2516">authenticationType</span></span> |<span data-ttu-id="825eb-2517">Type of authentication used to connect to the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="825eb-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="825eb-2518">Possible values are: Anonymous and Basic.</span><span class="sxs-lookup"><span data-stu-id="825eb-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="825eb-2519">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2519">Yes</span></span> |
| <span data-ttu-id="825eb-2520">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2520">username</span></span> |<span data-ttu-id="825eb-2521">Specify user name if you are using Basic authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="825eb-2522">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2522">No</span></span> |
| <span data-ttu-id="825eb-2523">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2523">password</span></span> |<span data-ttu-id="825eb-2524">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="825eb-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="825eb-2525">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2525">No</span></span> |
| <span data-ttu-id="825eb-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-2526">gatewayName</span></span> |<span data-ttu-id="825eb-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="825eb-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="825eb-2528">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="825eb-2529">Example - Using Basic authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="825eb-2530">Example - Using Basic authentication with encrypted credentials</span><span class="sxs-lookup"><span data-stu-id="825eb-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="825eb-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="825eb-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="825eb-2532">Example: Using Anonymous authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="825eb-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-2534">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-2534">Dataset</span></span>
<span data-ttu-id="825eb-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-2536">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2536">Property</span></span> | <span data-ttu-id="825eb-2537">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2537">Description</span></span> | <span data-ttu-id="825eb-2538">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-2539">tableName</span></span> |<span data-ttu-id="825eb-2540">Name of the table in the ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="825eb-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="825eb-2541">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="825eb-2542">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2542">Example</span></span>

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

<span data-ttu-id="825eb-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-2544">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-2546">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2546">Property</span></span> | <span data-ttu-id="825eb-2547">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2547">Description</span></span> | <span data-ttu-id="825eb-2548">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-2548">Allowed values</span></span> | <span data-ttu-id="825eb-2549">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2550">query</span><span class="sxs-lookup"><span data-stu-id="825eb-2550">query</span></span> |<span data-ttu-id="825eb-2551">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-2552">SQL query string.</span><span class="sxs-lookup"><span data-stu-id="825eb-2552">SQL query string.</span></span> <span data-ttu-id="825eb-2553">For example: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="825eb-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="825eb-2554">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2555">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2555">Example</span></span>

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

<span data-ttu-id="825eb-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="825eb-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="825eb-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="825eb-2558">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2558">Linked service</span></span>
<span data-ttu-id="825eb-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2560">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2560">Property</span></span> | <span data-ttu-id="825eb-2561">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2561">Description</span></span> | <span data-ttu-id="825eb-2562">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="825eb-2563">environmentUrl</span></span> | <span data-ttu-id="825eb-2564">Specify the URL of Salesforce instance.</span><span class="sxs-lookup"><span data-stu-id="825eb-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="825eb-2565">- Default is "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="825eb-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="825eb-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="825eb-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="825eb-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="825eb-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="825eb-2568">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2568">No</span></span> |
| <span data-ttu-id="825eb-2569">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2569">username</span></span> |<span data-ttu-id="825eb-2570">Specify a user name for the user account.</span><span class="sxs-lookup"><span data-stu-id="825eb-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="825eb-2571">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2571">Yes</span></span> |
| <span data-ttu-id="825eb-2572">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2572">password</span></span> |<span data-ttu-id="825eb-2573">Specify a password for the user account.</span><span class="sxs-lookup"><span data-stu-id="825eb-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="825eb-2574">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2574">Yes</span></span> |
| <span data-ttu-id="825eb-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="825eb-2575">securityToken</span></span> |<span data-ttu-id="825eb-2576">Specify a security token for the user account.</span><span class="sxs-lookup"><span data-stu-id="825eb-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="825eb-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span><span class="sxs-lookup"><span data-stu-id="825eb-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="825eb-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="825eb-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="825eb-2579">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2580">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2580">Example</span></span>

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

<span data-ttu-id="825eb-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-2582">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-2582">Dataset</span></span>
<span data-ttu-id="825eb-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-2584">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2584">Property</span></span> | <span data-ttu-id="825eb-2585">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2585">Description</span></span> | <span data-ttu-id="825eb-2586">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="825eb-2587">tableName</span></span> |<span data-ttu-id="825eb-2588">Name of the table in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="825eb-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="825eb-2589">No (if a **query** of **RelationalSource** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2590">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2590">Example</span></span>

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

<span data-ttu-id="825eb-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="825eb-2592">Relational Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="825eb-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="825eb-2594">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2594">Property</span></span> | <span data-ttu-id="825eb-2595">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2595">Description</span></span> | <span data-ttu-id="825eb-2596">Allowed values</span><span class="sxs-lookup"><span data-stu-id="825eb-2596">Allowed values</span></span> | <span data-ttu-id="825eb-2597">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="825eb-2598">query</span><span class="sxs-lookup"><span data-stu-id="825eb-2598">query</span></span> |<span data-ttu-id="825eb-2599">Use the custom query to read data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="825eb-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span><span class="sxs-lookup"><span data-stu-id="825eb-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="825eb-2601">For example:  `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="825eb-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="825eb-2602">No (if the **tableName** of the **dataset** is specified)</span><span class="sxs-lookup"><span data-stu-id="825eb-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2603">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2603">Example</span></span>  



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
> <span data-ttu-id="825eb-2604">The "__c" part of the API Name is needed for any custom object.</span><span class="sxs-lookup"><span data-stu-id="825eb-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="825eb-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="825eb-2606">Web Data</span><span class="sxs-lookup"><span data-stu-id="825eb-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-2607">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2607">Linked service</span></span>
<span data-ttu-id="825eb-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2609">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2609">Property</span></span> | <span data-ttu-id="825eb-2610">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2610">Description</span></span> | <span data-ttu-id="825eb-2611">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2612">Url</span><span class="sxs-lookup"><span data-stu-id="825eb-2612">Url</span></span> |<span data-ttu-id="825eb-2613">URL to the Web source</span><span class="sxs-lookup"><span data-stu-id="825eb-2613">URL to the Web source</span></span> |<span data-ttu-id="825eb-2614">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2614">Yes</span></span> |
| <span data-ttu-id="825eb-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="825eb-2615">authenticationType</span></span> |<span data-ttu-id="825eb-2616">Anonymous.</span><span class="sxs-lookup"><span data-stu-id="825eb-2616">Anonymous.</span></span> |<span data-ttu-id="825eb-2617">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="825eb-2618">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2618">Example</span></span>


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

<span data-ttu-id="825eb-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="825eb-2620">Dataset</span><span class="sxs-lookup"><span data-stu-id="825eb-2620">Dataset</span></span>
<span data-ttu-id="825eb-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="825eb-2622">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2622">Property</span></span> | <span data-ttu-id="825eb-2623">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2623">Description</span></span> | <span data-ttu-id="825eb-2624">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-2625">type</span><span class="sxs-lookup"><span data-stu-id="825eb-2625">type</span></span> |<span data-ttu-id="825eb-2626">type of the dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-2626">type of the dataset.</span></span> <span data-ttu-id="825eb-2627">must be set to **WebTable**</span><span class="sxs-lookup"><span data-stu-id="825eb-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="825eb-2628">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2628">Yes</span></span> |
| <span data-ttu-id="825eb-2629">path</span><span class="sxs-lookup"><span data-stu-id="825eb-2629">path</span></span> |<span data-ttu-id="825eb-2630">A relative URL to the resource that contains the table.</span><span class="sxs-lookup"><span data-stu-id="825eb-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="825eb-2631">No.</span><span class="sxs-lookup"><span data-stu-id="825eb-2631">No.</span></span> <span data-ttu-id="825eb-2632">When path is not specified, only the URL specified in the linked service definition is used.</span><span class="sxs-lookup"><span data-stu-id="825eb-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="825eb-2633">index</span><span class="sxs-lookup"><span data-stu-id="825eb-2633">index</span></span> |<span data-ttu-id="825eb-2634">The index of the table in the resource.</span><span class="sxs-lookup"><span data-stu-id="825eb-2634">The index of the table in the resource.</span></span> <span data-ttu-id="825eb-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span><span class="sxs-lookup"><span data-stu-id="825eb-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="825eb-2636">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="825eb-2637">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2637">Example</span></span>

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

<span data-ttu-id="825eb-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="825eb-2639">Web Source in Copy Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="825eb-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="825eb-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span><span class="sxs-lookup"><span data-stu-id="825eb-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="825eb-2642">Example</span><span class="sxs-lookup"><span data-stu-id="825eb-2642">Example</span></span>

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

<span data-ttu-id="825eb-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="825eb-2644">COMPUTE ENVIRONMENTS</span><span class="sxs-lookup"><span data-stu-id="825eb-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="825eb-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span><span class="sxs-lookup"><span data-stu-id="825eb-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="825eb-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span><span class="sxs-lookup"><span data-stu-id="825eb-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="825eb-2647">Compute environment</span><span class="sxs-lookup"><span data-stu-id="825eb-2647">Compute environment</span></span> | <span data-ttu-id="825eb-2648">Activities</span><span class="sxs-lookup"><span data-stu-id="825eb-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="825eb-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="825eb-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="825eb-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="825eb-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="825eb-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="825eb-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="825eb-2652">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="825eb-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="825eb-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="825eb-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="825eb-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="825eb-2655">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="825eb-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="825eb-2656">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="825eb-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="825eb-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="825eb-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="825eb-2658">Stored Procedure</span><span class="sxs-lookup"><span data-stu-id="825eb-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="825eb-2659">On-demand Azure HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="825eb-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="825eb-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="825eb-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="825eb-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="825eb-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-2663">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2663">Linked service</span></span> 
<span data-ttu-id="825eb-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="825eb-2665">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2665">Property</span></span> | <span data-ttu-id="825eb-2666">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2666">Description</span></span> | <span data-ttu-id="825eb-2667">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2668">type</span><span class="sxs-lookup"><span data-stu-id="825eb-2668">type</span></span> |<span data-ttu-id="825eb-2669">The type property should be set to **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="825eb-2670">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2670">Yes</span></span> |
| <span data-ttu-id="825eb-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="825eb-2671">clusterSize</span></span> |<span data-ttu-id="825eb-2672">Number of worker/data nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="825eb-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="825eb-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span><span class="sxs-lookup"><span data-stu-id="825eb-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="825eb-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span><span class="sxs-lookup"><span data-stu-id="825eb-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="825eb-2676">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2676">Yes</span></span> |
| <span data-ttu-id="825eb-2677">timetolive</span><span class="sxs-lookup"><span data-stu-id="825eb-2677">timetolive</span></span> |<span data-ttu-id="825eb-2678">The allowed idle time for the on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="825eb-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="825eb-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span><span class="sxs-lookup"><span data-stu-id="825eb-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="825eb-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="825eb-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="825eb-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span><span class="sxs-lookup"><span data-stu-id="825eb-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="825eb-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span><span class="sxs-lookup"><span data-stu-id="825eb-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="825eb-2685">Therefore, it is important that you set the appropriate value based on your needs.</span><span class="sxs-lookup"><span data-stu-id="825eb-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="825eb-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span><span class="sxs-lookup"><span data-stu-id="825eb-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="825eb-2687">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2687">Yes</span></span> |
| <span data-ttu-id="825eb-2688">version</span><span class="sxs-lookup"><span data-stu-id="825eb-2688">version</span></span> |<span data-ttu-id="825eb-2689">Version of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="825eb-2690">The default value is 3.1 for Windows cluster and 3.2 for Linux cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2690">The default value is 3.1 for Windows cluster and 3.2 for Linux cluster.</span></span> |<span data-ttu-id="825eb-2691">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2691">No</span></span> |
| <span data-ttu-id="825eb-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="825eb-2692">linkedServiceName</span></span> |<span data-ttu-id="825eb-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span><span class="sxs-lookup"><span data-stu-id="825eb-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="825eb-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span><span class="sxs-lookup"><span data-stu-id="825eb-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="825eb-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="825eb-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="825eb-2696">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2696">Yes</span></span> |
| <span data-ttu-id="825eb-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="825eb-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="825eb-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span><span class="sxs-lookup"><span data-stu-id="825eb-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="825eb-2699">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2699">No</span></span> |
| <span data-ttu-id="825eb-2700">osType</span><span class="sxs-lookup"><span data-stu-id="825eb-2700">osType</span></span> |<span data-ttu-id="825eb-2701">Type of operating system.</span><span class="sxs-lookup"><span data-stu-id="825eb-2701">Type of operating system.</span></span> <span data-ttu-id="825eb-2702">Allowed values are: Windows (default) and Linux</span><span class="sxs-lookup"><span data-stu-id="825eb-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="825eb-2703">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2703">No</span></span> |
| <span data-ttu-id="825eb-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="825eb-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="825eb-2705">The name of Azure SQL linked service that point to the HCatalog database.</span><span class="sxs-lookup"><span data-stu-id="825eb-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="825eb-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span><span class="sxs-lookup"><span data-stu-id="825eb-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="825eb-2707">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="825eb-2708">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2708">JSON example</span></span>
<span data-ttu-id="825eb-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="825eb-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span><span class="sxs-lookup"><span data-stu-id="825eb-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "clusterSize": 4,
            "timeToLive": "00:05:00",
            "osType": "linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="825eb-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="825eb-2712">Existing Azure HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="825eb-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="825eb-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span><span class="sxs-lookup"><span data-stu-id="825eb-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="825eb-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="825eb-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-2715">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2715">Linked service</span></span>
<span data-ttu-id="825eb-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="825eb-2717">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2717">Property</span></span> | <span data-ttu-id="825eb-2718">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2718">Description</span></span> | <span data-ttu-id="825eb-2719">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2720">type</span><span class="sxs-lookup"><span data-stu-id="825eb-2720">type</span></span> |<span data-ttu-id="825eb-2721">The type property should be set to **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="825eb-2722">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2722">Yes</span></span> |
| <span data-ttu-id="825eb-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="825eb-2723">clusterUri</span></span> |<span data-ttu-id="825eb-2724">The URI of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="825eb-2725">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2725">Yes</span></span> |
| <span data-ttu-id="825eb-2726">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2726">username</span></span> |<span data-ttu-id="825eb-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="825eb-2728">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2728">Yes</span></span> |
| <span data-ttu-id="825eb-2729">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2729">password</span></span> |<span data-ttu-id="825eb-2730">Specify password for the user account.</span><span class="sxs-lookup"><span data-stu-id="825eb-2730">Specify password for the user account.</span></span> |<span data-ttu-id="825eb-2731">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2731">Yes</span></span> |
| <span data-ttu-id="825eb-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="825eb-2732">linkedServiceName</span></span> | <span data-ttu-id="825eb-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="825eb-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="825eb-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="825eb-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="825eb-2736">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2736">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="825eb-2737">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2737">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="825eb-2738">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="825eb-2738">Azure Batch</span></span>
<span data-ttu-id="825eb-2739">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span><span class="sxs-lookup"><span data-stu-id="825eb-2739">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="825eb-2740">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="825eb-2740">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="825eb-2741">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2741">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-2742">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2742">Linked service</span></span>
<span data-ttu-id="825eb-2743">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2743">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="825eb-2744">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2744">Property</span></span> | <span data-ttu-id="825eb-2745">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2745">Description</span></span> | <span data-ttu-id="825eb-2746">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2746">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2747">type</span><span class="sxs-lookup"><span data-stu-id="825eb-2747">type</span></span> |<span data-ttu-id="825eb-2748">The type property should be set to **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2748">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="825eb-2749">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2749">Yes</span></span> |
| <span data-ttu-id="825eb-2750">accountName</span><span class="sxs-lookup"><span data-stu-id="825eb-2750">accountName</span></span> |<span data-ttu-id="825eb-2751">Name of the Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="825eb-2751">Name of the Azure Batch account.</span></span> |<span data-ttu-id="825eb-2752">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2752">Yes</span></span> |
| <span data-ttu-id="825eb-2753">accessKey</span><span class="sxs-lookup"><span data-stu-id="825eb-2753">accessKey</span></span> |<span data-ttu-id="825eb-2754">Access key for the Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="825eb-2754">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="825eb-2755">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2755">Yes</span></span> |
| <span data-ttu-id="825eb-2756">poolName</span><span class="sxs-lookup"><span data-stu-id="825eb-2756">poolName</span></span> |<span data-ttu-id="825eb-2757">Name of the pool of virtual machines.</span><span class="sxs-lookup"><span data-stu-id="825eb-2757">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="825eb-2758">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2758">Yes</span></span> |
| <span data-ttu-id="825eb-2759">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="825eb-2759">linkedServiceName</span></span> |<span data-ttu-id="825eb-2760">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2760">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="825eb-2761">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span><span class="sxs-lookup"><span data-stu-id="825eb-2761">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="825eb-2762">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2762">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="825eb-2763">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2763">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="825eb-2764">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="825eb-2764">Azure Machine Learning</span></span>
<span data-ttu-id="825eb-2765">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span><span class="sxs-lookup"><span data-stu-id="825eb-2765">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="825eb-2766">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="825eb-2766">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-2767">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2767">Linked service</span></span>
<span data-ttu-id="825eb-2768">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2768">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="825eb-2769">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2769">Property</span></span> | <span data-ttu-id="825eb-2770">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2770">Description</span></span> | <span data-ttu-id="825eb-2771">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2771">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2772">Type</span><span class="sxs-lookup"><span data-stu-id="825eb-2772">Type</span></span> |<span data-ttu-id="825eb-2773">The type property should be set to: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2773">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="825eb-2774">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2774">Yes</span></span> |
| <span data-ttu-id="825eb-2775">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="825eb-2775">mlEndpoint</span></span> |<span data-ttu-id="825eb-2776">The batch scoring URL.</span><span class="sxs-lookup"><span data-stu-id="825eb-2776">The batch scoring URL.</span></span> |<span data-ttu-id="825eb-2777">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2777">Yes</span></span> |
| <span data-ttu-id="825eb-2778">apiKey</span><span class="sxs-lookup"><span data-stu-id="825eb-2778">apiKey</span></span> |<span data-ttu-id="825eb-2779">The published workspace model’s API.</span><span class="sxs-lookup"><span data-stu-id="825eb-2779">The published workspace model’s API.</span></span> |<span data-ttu-id="825eb-2780">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2780">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="825eb-2781">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2781">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="825eb-2782">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="825eb-2782">Azure Data Lake Analytics</span></span>
<span data-ttu-id="825eb-2783">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-2783">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="825eb-2784">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2784">Linked service</span></span>

<span data-ttu-id="825eb-2785">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2785">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="825eb-2786">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2786">Property</span></span> | <span data-ttu-id="825eb-2787">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2787">Description</span></span> | <span data-ttu-id="825eb-2788">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2788">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2789">Type</span><span class="sxs-lookup"><span data-stu-id="825eb-2789">Type</span></span> |<span data-ttu-id="825eb-2790">The type property should be set to: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2790">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="825eb-2791">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2791">Yes</span></span> |
| <span data-ttu-id="825eb-2792">accountName</span><span class="sxs-lookup"><span data-stu-id="825eb-2792">accountName</span></span> |<span data-ttu-id="825eb-2793">Azure Data Lake Analytics Account Name.</span><span class="sxs-lookup"><span data-stu-id="825eb-2793">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="825eb-2794">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2794">Yes</span></span> |
| <span data-ttu-id="825eb-2795">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="825eb-2795">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="825eb-2796">Azure Data Lake Analytics URI.</span><span class="sxs-lookup"><span data-stu-id="825eb-2796">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="825eb-2797">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2797">No</span></span> |
| <span data-ttu-id="825eb-2798">authorization</span><span class="sxs-lookup"><span data-stu-id="825eb-2798">authorization</span></span> |<span data-ttu-id="825eb-2799">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span><span class="sxs-lookup"><span data-stu-id="825eb-2799">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="825eb-2800">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2800">Yes</span></span> |
| <span data-ttu-id="825eb-2801">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="825eb-2801">subscriptionId</span></span> |<span data-ttu-id="825eb-2802">Azure subscription id</span><span class="sxs-lookup"><span data-stu-id="825eb-2802">Azure subscription id</span></span> |<span data-ttu-id="825eb-2803">No (If not specified, subscription of the data factory is used).</span><span class="sxs-lookup"><span data-stu-id="825eb-2803">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="825eb-2804">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="825eb-2804">resourceGroupName</span></span> |<span data-ttu-id="825eb-2805">Azure resource group name</span><span class="sxs-lookup"><span data-stu-id="825eb-2805">Azure resource group name</span></span> |<span data-ttu-id="825eb-2806">No (If not specified, resource group of the data factory is used).</span><span class="sxs-lookup"><span data-stu-id="825eb-2806">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="825eb-2807">sessionId</span><span class="sxs-lookup"><span data-stu-id="825eb-2807">sessionId</span></span> |<span data-ttu-id="825eb-2808">session id from the OAuth authorization session.</span><span class="sxs-lookup"><span data-stu-id="825eb-2808">session id from the OAuth authorization session.</span></span> <span data-ttu-id="825eb-2809">Each session id is unique and may only be used once.</span><span class="sxs-lookup"><span data-stu-id="825eb-2809">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="825eb-2810">When you use the Data Factory Editor, this ID is auto-generated.</span><span class="sxs-lookup"><span data-stu-id="825eb-2810">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="825eb-2811">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2811">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="825eb-2812">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2812">JSON example</span></span>
<span data-ttu-id="825eb-2813">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2813">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="825eb-2814">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="825eb-2814">Azure SQL Database</span></span>
<span data-ttu-id="825eb-2815">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-2815">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-2816">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2816">Linked service</span></span>
<span data-ttu-id="825eb-2817">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2817">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2818">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2818">Property</span></span> | <span data-ttu-id="825eb-2819">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2819">Description</span></span> | <span data-ttu-id="825eb-2820">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2820">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2821">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-2821">connectionString</span></span> |<span data-ttu-id="825eb-2822">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2822">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="825eb-2823">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2823">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="825eb-2824">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2824">JSON example</span></span>

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

<span data-ttu-id="825eb-2825">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2825">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="825eb-2826">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="825eb-2826">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="825eb-2827">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-2827">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-2828">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2828">Linked service</span></span>
<span data-ttu-id="825eb-2829">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span><span class="sxs-lookup"><span data-stu-id="825eb-2829">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="825eb-2830">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2830">Property</span></span> | <span data-ttu-id="825eb-2831">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2831">Description</span></span> | <span data-ttu-id="825eb-2832">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2832">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2833">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-2833">connectionString</span></span> |<span data-ttu-id="825eb-2834">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2834">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="825eb-2835">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2835">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="825eb-2836">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2836">JSON example</span></span>

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

<span data-ttu-id="825eb-2837">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2837">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="825eb-2838">SQL Server</span><span class="sxs-lookup"><span data-stu-id="825eb-2838">SQL Server</span></span> 
<span data-ttu-id="825eb-2839">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-2839">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="825eb-2840">Linked service</span><span class="sxs-lookup"><span data-stu-id="825eb-2840">Linked service</span></span>
<span data-ttu-id="825eb-2841">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span><span class="sxs-lookup"><span data-stu-id="825eb-2841">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="825eb-2842">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2842">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="825eb-2843">The following table provides description for JSON elements specific to SQL Server linked service.</span><span class="sxs-lookup"><span data-stu-id="825eb-2843">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="825eb-2844">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2844">Property</span></span> | <span data-ttu-id="825eb-2845">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2845">Description</span></span> | <span data-ttu-id="825eb-2846">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2846">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2847">type</span><span class="sxs-lookup"><span data-stu-id="825eb-2847">type</span></span> |<span data-ttu-id="825eb-2848">The type property should be set to: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2848">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="825eb-2849">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2849">Yes</span></span> |
| <span data-ttu-id="825eb-2850">connectionString</span><span class="sxs-lookup"><span data-stu-id="825eb-2850">connectionString</span></span> |<span data-ttu-id="825eb-2851">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-2851">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="825eb-2852">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2852">Yes</span></span> |
| <span data-ttu-id="825eb-2853">gatewayName</span><span class="sxs-lookup"><span data-stu-id="825eb-2853">gatewayName</span></span> |<span data-ttu-id="825eb-2854">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="825eb-2854">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="825eb-2855">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2855">Yes</span></span> |
| <span data-ttu-id="825eb-2856">username</span><span class="sxs-lookup"><span data-stu-id="825eb-2856">username</span></span> |<span data-ttu-id="825eb-2857">Specify user name if you are using Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="825eb-2857">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="825eb-2858">Example: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2858">Example: **domainname\\username**.</span></span> |<span data-ttu-id="825eb-2859">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2859">No</span></span> |
| <span data-ttu-id="825eb-2860">password</span><span class="sxs-lookup"><span data-stu-id="825eb-2860">password</span></span> |<span data-ttu-id="825eb-2861">Specify password for the user account you specified for the username.</span><span class="sxs-lookup"><span data-stu-id="825eb-2861">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="825eb-2862">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2862">No</span></span> |

<span data-ttu-id="825eb-2863">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span><span class="sxs-lookup"><span data-stu-id="825eb-2863">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="825eb-2864">Example: JSON for using SQL Authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2864">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="825eb-2865">Example: JSON for using Windows Authentication</span><span class="sxs-lookup"><span data-stu-id="825eb-2865">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="825eb-2866">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="825eb-2866">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="825eb-2867">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span><span class="sxs-lookup"><span data-stu-id="825eb-2867">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="825eb-2868">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2868">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="transformation-activites"></a><span data-ttu-id="825eb-2869">TRANSFORMATION ACTIVITES</span><span class="sxs-lookup"><span data-stu-id="825eb-2869">TRANSFORMATION ACTIVITES</span></span>

<span data-ttu-id="825eb-2870">Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2870">Activity</span></span> | <span data-ttu-id="825eb-2871">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2871">Description</span></span>
-------- | -----------
[<span data-ttu-id="825eb-2872">HDInsight Hive activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2872">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="825eb-2873">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2873">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="825eb-2874">HDInsight Pig activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2874">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="825eb-2875">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2875">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="825eb-2876">HDInsight MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2876">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="825eb-2877">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2877">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="825eb-2878">HDInsight Streaming Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2878">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="825eb-2879">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2879">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="825eb-2880">HDInsight Spark Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2880">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="825eb-2881">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2881">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="825eb-2882">Machine Learning Batch Execution Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2882">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="825eb-2883">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="825eb-2883">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="825eb-2884">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span><span class="sxs-lookup"><span data-stu-id="825eb-2884">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="825eb-2885">Machine Learning Update Resource Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2885">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="825eb-2886">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span><span class="sxs-lookup"><span data-stu-id="825eb-2886">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="825eb-2887">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span><span class="sxs-lookup"><span data-stu-id="825eb-2887">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="825eb-2888">You can use the Update Resource Activity to update the web service with the newly trained model.</span><span class="sxs-lookup"><span data-stu-id="825eb-2888">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="825eb-2889">Stored Procedure Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2889">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="825eb-2890">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="825eb-2890">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="825eb-2891">Data Lake Analytics U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2891">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="825eb-2892">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2892">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="825eb-2893">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2893">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="825eb-2894">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-2894">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="825eb-2895">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-2895">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="825eb-2896">HDInsight Hive Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2896">HDInsight Hive Activity</span></span>
<span data-ttu-id="825eb-2897">You can specify the following properties in a Hive Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-2897">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="825eb-2898">The type property for the activity must be: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2898">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="825eb-2899">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2899">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-2900">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span><span class="sxs-lookup"><span data-stu-id="825eb-2900">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="825eb-2901">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2901">Property</span></span> | <span data-ttu-id="825eb-2902">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2902">Description</span></span> | <span data-ttu-id="825eb-2903">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2903">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2904">script</span><span class="sxs-lookup"><span data-stu-id="825eb-2904">script</span></span> |<span data-ttu-id="825eb-2905">Specify the Hive script inline</span><span class="sxs-lookup"><span data-stu-id="825eb-2905">Specify the Hive script inline</span></span> |<span data-ttu-id="825eb-2906">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2906">No</span></span> |
| <span data-ttu-id="825eb-2907">script path</span><span class="sxs-lookup"><span data-stu-id="825eb-2907">script path</span></span> |<span data-ttu-id="825eb-2908">Store the Hive script in an Azure blob storage and provide the path to the file.</span><span class="sxs-lookup"><span data-stu-id="825eb-2908">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="825eb-2909">Use 'script' or 'scriptPath' property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2909">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="825eb-2910">Both cannot be used together.</span><span class="sxs-lookup"><span data-stu-id="825eb-2910">Both cannot be used together.</span></span> <span data-ttu-id="825eb-2911">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-2911">The file name is case-sensitive.</span></span> |<span data-ttu-id="825eb-2912">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2912">No</span></span> |
| <span data-ttu-id="825eb-2913">defines</span><span class="sxs-lookup"><span data-stu-id="825eb-2913">defines</span></span> |<span data-ttu-id="825eb-2914">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="825eb-2914">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="825eb-2915">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2915">No</span></span> |

<span data-ttu-id="825eb-2916">These type properties are specific to the Hive Activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-2916">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="825eb-2917">Other properties (outside the typeProperties section) are supported for all activities.</span><span class="sxs-lookup"><span data-stu-id="825eb-2917">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="825eb-2918">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2918">JSON example</span></span>
<span data-ttu-id="825eb-2919">The following JSON defines a HDInsight Hive activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-2919">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="825eb-2920">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2920">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="825eb-2921">HDInsight Pig Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2921">HDInsight Pig Activity</span></span>
<span data-ttu-id="825eb-2922">You can specify the following properties in a Pig Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-2922">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="825eb-2923">The type property for the activity must be: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2923">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="825eb-2924">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2924">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-2925">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span><span class="sxs-lookup"><span data-stu-id="825eb-2925">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="825eb-2926">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2926">Property</span></span> | <span data-ttu-id="825eb-2927">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2927">Description</span></span> | <span data-ttu-id="825eb-2928">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2928">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2929">script</span><span class="sxs-lookup"><span data-stu-id="825eb-2929">script</span></span> |<span data-ttu-id="825eb-2930">Specify the Pig script inline</span><span class="sxs-lookup"><span data-stu-id="825eb-2930">Specify the Pig script inline</span></span> |<span data-ttu-id="825eb-2931">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2931">No</span></span> |
| <span data-ttu-id="825eb-2932">script path</span><span class="sxs-lookup"><span data-stu-id="825eb-2932">script path</span></span> |<span data-ttu-id="825eb-2933">Store the Pig script in an Azure blob storage and provide the path to the file.</span><span class="sxs-lookup"><span data-stu-id="825eb-2933">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="825eb-2934">Use 'script' or 'scriptPath' property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2934">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="825eb-2935">Both cannot be used together.</span><span class="sxs-lookup"><span data-stu-id="825eb-2935">Both cannot be used together.</span></span> <span data-ttu-id="825eb-2936">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-2936">The file name is case-sensitive.</span></span> |<span data-ttu-id="825eb-2937">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2937">No</span></span> |
| <span data-ttu-id="825eb-2938">defines</span><span class="sxs-lookup"><span data-stu-id="825eb-2938">defines</span></span> |<span data-ttu-id="825eb-2939">Specify parameters as key/value pairs for referencing within the Pig script</span><span class="sxs-lookup"><span data-stu-id="825eb-2939">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="825eb-2940">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2940">No</span></span> |

<span data-ttu-id="825eb-2941">These type properties are specific to the Pig Activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-2941">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="825eb-2942">Other properties (outside the typeProperties section) are supported for all activities.</span><span class="sxs-lookup"><span data-stu-id="825eb-2942">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="825eb-2943">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2943">JSON example</span></span>

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

<span data-ttu-id="825eb-2944">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2944">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="825eb-2945">HDInsight MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2945">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="825eb-2946">You can specify the following properties in a MapReduce Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-2946">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="825eb-2947">The type property for the activity must be: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2947">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="825eb-2948">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2948">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-2949">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span><span class="sxs-lookup"><span data-stu-id="825eb-2949">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="825eb-2950">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2950">Property</span></span> | <span data-ttu-id="825eb-2951">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2951">Description</span></span> | <span data-ttu-id="825eb-2952">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-2952">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-2953">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="825eb-2953">jarLinkedService</span></span> | <span data-ttu-id="825eb-2954">Name of the linked service for the Azure Storage that contains the JAR file.</span><span class="sxs-lookup"><span data-stu-id="825eb-2954">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="825eb-2955">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2955">Yes</span></span> |
| <span data-ttu-id="825eb-2956">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="825eb-2956">jarFilePath</span></span> | <span data-ttu-id="825eb-2957">Path to the JAR file in the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="825eb-2957">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="825eb-2958">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2958">Yes</span></span> | 
| <span data-ttu-id="825eb-2959">className</span><span class="sxs-lookup"><span data-stu-id="825eb-2959">className</span></span> | <span data-ttu-id="825eb-2960">Name of the main class in the JAR file.</span><span class="sxs-lookup"><span data-stu-id="825eb-2960">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="825eb-2961">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-2961">Yes</span></span> | 
| <span data-ttu-id="825eb-2962">arguments</span><span class="sxs-lookup"><span data-stu-id="825eb-2962">arguments</span></span> | <span data-ttu-id="825eb-2963">A list of comma-separated arguments for the MapReduce program.</span><span class="sxs-lookup"><span data-stu-id="825eb-2963">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="825eb-2964">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span><span class="sxs-lookup"><span data-stu-id="825eb-2964">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="825eb-2965">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span><span class="sxs-lookup"><span data-stu-id="825eb-2965">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="825eb-2966">No</span><span class="sxs-lookup"><span data-stu-id="825eb-2966">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="825eb-2967">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-2967">JSON example</span></span>

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

<span data-ttu-id="825eb-2968">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-2968">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="825eb-2969">HDInsight Streaming Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-2969">HDInsight Streaming Activity</span></span>
<span data-ttu-id="825eb-2970">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-2970">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="825eb-2971">The type property for the activity must be: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="825eb-2971">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="825eb-2972">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2972">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-2973">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span><span class="sxs-lookup"><span data-stu-id="825eb-2973">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="825eb-2974">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-2974">Property</span></span> | <span data-ttu-id="825eb-2975">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-2975">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="825eb-2976">mapper</span><span class="sxs-lookup"><span data-stu-id="825eb-2976">mapper</span></span> | <span data-ttu-id="825eb-2977">Name of the mapper executable.</span><span class="sxs-lookup"><span data-stu-id="825eb-2977">Name of the mapper executable.</span></span> <span data-ttu-id="825eb-2978">In the example, cat.exe is the mapper executable.</span><span class="sxs-lookup"><span data-stu-id="825eb-2978">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="825eb-2979">reducer</span><span class="sxs-lookup"><span data-stu-id="825eb-2979">reducer</span></span> | <span data-ttu-id="825eb-2980">Name of the reducer executable.</span><span class="sxs-lookup"><span data-stu-id="825eb-2980">Name of the reducer executable.</span></span> <span data-ttu-id="825eb-2981">In the example, wc.exe is the reducer executable.</span><span class="sxs-lookup"><span data-stu-id="825eb-2981">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="825eb-2982">input</span><span class="sxs-lookup"><span data-stu-id="825eb-2982">input</span></span> | <span data-ttu-id="825eb-2983">Input file (including location) for the mapper.</span><span class="sxs-lookup"><span data-stu-id="825eb-2983">Input file (including location) for the mapper.</span></span> <span data-ttu-id="825eb-2984">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span><span class="sxs-lookup"><span data-stu-id="825eb-2984">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="825eb-2985">output</span><span class="sxs-lookup"><span data-stu-id="825eb-2985">output</span></span> | <span data-ttu-id="825eb-2986">Output file (including location) for the reducer.</span><span class="sxs-lookup"><span data-stu-id="825eb-2986">Output file (including location) for the reducer.</span></span> <span data-ttu-id="825eb-2987">The output of the Hadoop Streaming job is written to the location specified for this property.</span><span class="sxs-lookup"><span data-stu-id="825eb-2987">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="825eb-2988">filePaths</span><span class="sxs-lookup"><span data-stu-id="825eb-2988">filePaths</span></span> | <span data-ttu-id="825eb-2989">Paths for the mapper and reducer executables.</span><span class="sxs-lookup"><span data-stu-id="825eb-2989">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="825eb-2990">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span><span class="sxs-lookup"><span data-stu-id="825eb-2990">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="825eb-2991">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="825eb-2991">fileLinkedService</span></span> | <span data-ttu-id="825eb-2992">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span><span class="sxs-lookup"><span data-stu-id="825eb-2992">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="825eb-2993">arguments</span><span class="sxs-lookup"><span data-stu-id="825eb-2993">arguments</span></span> | <span data-ttu-id="825eb-2994">A list of comma-separated arguments for the MapReduce program.</span><span class="sxs-lookup"><span data-stu-id="825eb-2994">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="825eb-2995">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span><span class="sxs-lookup"><span data-stu-id="825eb-2995">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="825eb-2996">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span><span class="sxs-lookup"><span data-stu-id="825eb-2996">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="825eb-2997">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="825eb-2997">getDebugInfo</span></span> | <span data-ttu-id="825eb-2998">An optional element.</span><span class="sxs-lookup"><span data-stu-id="825eb-2998">An optional element.</span></span> <span data-ttu-id="825eb-2999">When it is set to Failure, the logs are downloaded only on failure.</span><span class="sxs-lookup"><span data-stu-id="825eb-2999">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="825eb-3000">When it is set to All, logs are always downloaded irrespective of the execution status.</span><span class="sxs-lookup"><span data-stu-id="825eb-3000">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="825eb-3001">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3001">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="825eb-3002">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="825eb-3002">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="825eb-3003">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3003">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="825eb-3004">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-3004">JSON example</span></span>

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

<span data-ttu-id="825eb-3005">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-3005">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="825eb-3006">HDInsight Spark Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-3006">HDInsight Spark Activity</span></span>
<span data-ttu-id="825eb-3007">You can specify the following properties in a Spark Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-3007">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="825eb-3008">The type property for the activity must be: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3008">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="825eb-3009">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3009">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-3010">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span><span class="sxs-lookup"><span data-stu-id="825eb-3010">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="825eb-3011">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-3011">Property</span></span> | <span data-ttu-id="825eb-3012">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-3012">Description</span></span> | <span data-ttu-id="825eb-3013">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-3013">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="825eb-3014">rootPath</span><span class="sxs-lookup"><span data-stu-id="825eb-3014">rootPath</span></span> | <span data-ttu-id="825eb-3015">The Azure Blob container and folder that contains the Spark file.</span><span class="sxs-lookup"><span data-stu-id="825eb-3015">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="825eb-3016">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-3016">The file name is case-sensitive.</span></span> | <span data-ttu-id="825eb-3017">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3017">Yes</span></span> |
| <span data-ttu-id="825eb-3018">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="825eb-3018">entryFilePath</span></span> | <span data-ttu-id="825eb-3019">Relative path to the root folder of the Spark code/package.</span><span class="sxs-lookup"><span data-stu-id="825eb-3019">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="825eb-3020">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3020">Yes</span></span> |
| <span data-ttu-id="825eb-3021">className</span><span class="sxs-lookup"><span data-stu-id="825eb-3021">className</span></span> | <span data-ttu-id="825eb-3022">Application's Java/Spark main class</span><span class="sxs-lookup"><span data-stu-id="825eb-3022">Application's Java/Spark main class</span></span> | <span data-ttu-id="825eb-3023">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3023">No</span></span> | 
| <span data-ttu-id="825eb-3024">arguments</span><span class="sxs-lookup"><span data-stu-id="825eb-3024">arguments</span></span> | <span data-ttu-id="825eb-3025">A list of command-line arguments to the Spark program.</span><span class="sxs-lookup"><span data-stu-id="825eb-3025">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="825eb-3026">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3026">No</span></span> | 
| <span data-ttu-id="825eb-3027">proxyUser</span><span class="sxs-lookup"><span data-stu-id="825eb-3027">proxyUser</span></span> | <span data-ttu-id="825eb-3028">The user account to impersonate to execute the Spark program</span><span class="sxs-lookup"><span data-stu-id="825eb-3028">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="825eb-3029">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3029">No</span></span> | 
| <span data-ttu-id="825eb-3030">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="825eb-3030">sparkConfig</span></span> | <span data-ttu-id="825eb-3031">Spark configuration properties.</span><span class="sxs-lookup"><span data-stu-id="825eb-3031">Spark configuration properties.</span></span> | <span data-ttu-id="825eb-3032">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3032">No</span></span> | 
| <span data-ttu-id="825eb-3033">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="825eb-3033">getDebugInfo</span></span> | <span data-ttu-id="825eb-3034">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="825eb-3034">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="825eb-3035">Allowed values: None, Always, or Failure.</span><span class="sxs-lookup"><span data-stu-id="825eb-3035">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="825eb-3036">Default value: None.</span><span class="sxs-lookup"><span data-stu-id="825eb-3036">Default value: None.</span></span> | <span data-ttu-id="825eb-3037">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3037">No</span></span> | 
| <span data-ttu-id="825eb-3038">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="825eb-3038">sparkJobLinkedService</span></span> | <span data-ttu-id="825eb-3039">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span><span class="sxs-lookup"><span data-stu-id="825eb-3039">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="825eb-3040">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span><span class="sxs-lookup"><span data-stu-id="825eb-3040">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="825eb-3041">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3041">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="825eb-3042">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-3042">JSON example</span></span>

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
<span data-ttu-id="825eb-3043">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="825eb-3043">Note the following points:</span></span> 

- <span data-ttu-id="825eb-3044">The **type** property is set to **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3044">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="825eb-3045">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span><span class="sxs-lookup"><span data-stu-id="825eb-3045">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="825eb-3046">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="825eb-3046">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="825eb-3047">You can upload the file to a different Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="825eb-3047">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="825eb-3048">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="825eb-3048">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="825eb-3049">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3049">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="825eb-3050">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-3050">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="825eb-3051">The **entryFilePath** is set to the **test.py**, which is the python file.</span><span class="sxs-lookup"><span data-stu-id="825eb-3051">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="825eb-3052">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span><span class="sxs-lookup"><span data-stu-id="825eb-3052">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="825eb-3053">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span><span class="sxs-lookup"><span data-stu-id="825eb-3053">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="825eb-3054">The **outputs** section has one output dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-3054">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="825eb-3055">You must specify an output dataset even if the spark program does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="825eb-3055">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="825eb-3056">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="825eb-3056">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="825eb-3057">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-3057">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="825eb-3058">Machine Learning Batch Execution Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-3058">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="825eb-3059">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-3059">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="825eb-3060">The type property for the activity must be: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3060">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="825eb-3061">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3061">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-3062">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span><span class="sxs-lookup"><span data-stu-id="825eb-3062">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="825eb-3063">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-3063">Property</span></span> | <span data-ttu-id="825eb-3064">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-3064">Description</span></span> | <span data-ttu-id="825eb-3065">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-3065">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="825eb-3066">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="825eb-3066">webServiceInput</span></span> | <span data-ttu-id="825eb-3067">The dataset to be passed as an input for the Azure ML web service.</span><span class="sxs-lookup"><span data-stu-id="825eb-3067">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="825eb-3068">This dataset must also be included in the inputs for the activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-3068">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="825eb-3069">Use either webServiceInput or webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="825eb-3069">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="825eb-3070">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="825eb-3070">webServiceInputs</span></span> | <span data-ttu-id="825eb-3071">Specify datasets to be passed as inputs for the Azure ML web service.</span><span class="sxs-lookup"><span data-stu-id="825eb-3071">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="825eb-3072">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3072">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="825eb-3073">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3073">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="825eb-3074">Use either webServiceInput or webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="825eb-3074">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="825eb-3075">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="825eb-3075">webServiceOutputs</span></span> | <span data-ttu-id="825eb-3076">The datasets that are assigned as outputs for the Azure ML web service.</span><span class="sxs-lookup"><span data-stu-id="825eb-3076">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="825eb-3077">The web service returns output data in this dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-3077">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="825eb-3078">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3078">Yes</span></span> | 
<span data-ttu-id="825eb-3079">globalParameters</span><span class="sxs-lookup"><span data-stu-id="825eb-3079">globalParameters</span></span> | <span data-ttu-id="825eb-3080">Specify values for the web service parameters in this section.</span><span class="sxs-lookup"><span data-stu-id="825eb-3080">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="825eb-3081">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3081">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="825eb-3082">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-3082">JSON example</span></span>
<span data-ttu-id="825eb-3083">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span><span class="sxs-lookup"><span data-stu-id="825eb-3083">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="825eb-3084">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3084">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="825eb-3085">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3085">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="825eb-3086">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="825eb-3086">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="825eb-3087">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span><span class="sxs-lookup"><span data-stu-id="825eb-3087">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="825eb-3088">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span><span class="sxs-lookup"><span data-stu-id="825eb-3088">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="825eb-3089">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span><span class="sxs-lookup"><span data-stu-id="825eb-3089">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="825eb-3090">Machine Learning Update Resource Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-3090">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="825eb-3091">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-3091">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="825eb-3092">The type property for the activity must be: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3092">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="825eb-3093">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3093">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-3094">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span><span class="sxs-lookup"><span data-stu-id="825eb-3094">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="825eb-3095">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-3095">Property</span></span> | <span data-ttu-id="825eb-3096">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-3096">Description</span></span> | <span data-ttu-id="825eb-3097">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-3097">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="825eb-3098">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="825eb-3098">trainedModelName</span></span> | <span data-ttu-id="825eb-3099">Name of the retrained model.</span><span class="sxs-lookup"><span data-stu-id="825eb-3099">Name of the retrained model.</span></span> | <span data-ttu-id="825eb-3100">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3100">Yes</span></span> |  
<span data-ttu-id="825eb-3101">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="825eb-3101">trainedModelDatasetName</span></span> | <span data-ttu-id="825eb-3102">Dataset pointing to the iLearner file returned by the retraining operation.</span><span class="sxs-lookup"><span data-stu-id="825eb-3102">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="825eb-3103">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3103">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="825eb-3104">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-3104">JSON example</span></span>
<span data-ttu-id="825eb-3105">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3105">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="825eb-3106">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span><span class="sxs-lookup"><span data-stu-id="825eb-3106">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="825eb-3107">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span><span class="sxs-lookup"><span data-stu-id="825eb-3107">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="825eb-3108">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-3108">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="825eb-3109">Data Lake Analytics U-SQL Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-3109">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="825eb-3110">You can specify the following properties in a U-SQL Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-3110">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="825eb-3111">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3111">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="825eb-3112">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3112">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-3113">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="825eb-3113">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="825eb-3114">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-3114">Property</span></span> | <span data-ttu-id="825eb-3115">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-3115">Description</span></span> | <span data-ttu-id="825eb-3116">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-3116">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-3117">scriptPath</span><span class="sxs-lookup"><span data-stu-id="825eb-3117">scriptPath</span></span> |<span data-ttu-id="825eb-3118">Path to folder that contains the U-SQL script.</span><span class="sxs-lookup"><span data-stu-id="825eb-3118">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="825eb-3119">Name of the file is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="825eb-3119">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="825eb-3120">No (if you use script)</span><span class="sxs-lookup"><span data-stu-id="825eb-3120">No (if you use script)</span></span> |
| <span data-ttu-id="825eb-3121">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="825eb-3121">scriptLinkedService</span></span> |<span data-ttu-id="825eb-3122">Linked service that links the storage that contains the script to the data factory</span><span class="sxs-lookup"><span data-stu-id="825eb-3122">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="825eb-3123">No (if you use script)</span><span class="sxs-lookup"><span data-stu-id="825eb-3123">No (if you use script)</span></span> |
| <span data-ttu-id="825eb-3124">script</span><span class="sxs-lookup"><span data-stu-id="825eb-3124">script</span></span> |<span data-ttu-id="825eb-3125">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="825eb-3125">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="825eb-3126">For example: "script": "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="825eb-3126">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="825eb-3127">No (if you use scriptPath and scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="825eb-3127">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="825eb-3128">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="825eb-3128">degreeOfParallelism</span></span> |<span data-ttu-id="825eb-3129">The maximum number of nodes simultaneously used to run the job.</span><span class="sxs-lookup"><span data-stu-id="825eb-3129">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="825eb-3130">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3130">No</span></span> |
| <span data-ttu-id="825eb-3131">priority</span><span class="sxs-lookup"><span data-stu-id="825eb-3131">priority</span></span> |<span data-ttu-id="825eb-3132">Determines which jobs out of all that are queued should be selected to run first.</span><span class="sxs-lookup"><span data-stu-id="825eb-3132">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="825eb-3133">The lower the number, the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="825eb-3133">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="825eb-3134">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3134">No</span></span> |
| <span data-ttu-id="825eb-3135">parameters</span><span class="sxs-lookup"><span data-stu-id="825eb-3135">parameters</span></span> |<span data-ttu-id="825eb-3136">Parameters for the U-SQL script</span><span class="sxs-lookup"><span data-stu-id="825eb-3136">Parameters for the U-SQL script</span></span> |<span data-ttu-id="825eb-3137">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3137">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="825eb-3138">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-3138">JSON example</span></span>

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

<span data-ttu-id="825eb-3139">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="825eb-3139">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="825eb-3140">Stored Procedure Activity</span><span class="sxs-lookup"><span data-stu-id="825eb-3140">Stored Procedure Activity</span></span>
<span data-ttu-id="825eb-3141">You can specify the following properties in a Stored Procedure Activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-3141">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="825eb-3142">The type property for the activity must be: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3142">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="825eb-3143">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span><span class="sxs-lookup"><span data-stu-id="825eb-3143">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="825eb-3144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="825eb-3144">SQL Server</span></span> 
- <span data-ttu-id="825eb-3145">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="825eb-3145">Azure SQL Database</span></span>
- <span data-ttu-id="825eb-3146">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="825eb-3146">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="825eb-3147">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span><span class="sxs-lookup"><span data-stu-id="825eb-3147">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="825eb-3148">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-3148">Property</span></span> | <span data-ttu-id="825eb-3149">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-3149">Description</span></span> | <span data-ttu-id="825eb-3150">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-3150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="825eb-3151">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="825eb-3151">storedProcedureName</span></span> |<span data-ttu-id="825eb-3152">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span><span class="sxs-lookup"><span data-stu-id="825eb-3152">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="825eb-3153">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3153">Yes</span></span> |
| <span data-ttu-id="825eb-3154">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="825eb-3154">storedProcedureParameters</span></span> |<span data-ttu-id="825eb-3155">Specify values for stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="825eb-3155">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="825eb-3156">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span><span class="sxs-lookup"><span data-stu-id="825eb-3156">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="825eb-3157">See the following sample to learn about using this property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3157">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="825eb-3158">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3158">No</span></span> |

<span data-ttu-id="825eb-3159">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span><span class="sxs-lookup"><span data-stu-id="825eb-3159">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="825eb-3160">The input dataset cannot be consumed in the stored procedure as a parameter.</span><span class="sxs-lookup"><span data-stu-id="825eb-3160">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="825eb-3161">It is only used to check the dependency before starting the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-3161">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="825eb-3162">You must specify an output dataset for a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-3162">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="825eb-3163">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span><span class="sxs-lookup"><span data-stu-id="825eb-3163">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="825eb-3164">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span><span class="sxs-lookup"><span data-stu-id="825eb-3164">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="825eb-3165">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#run-activities-in-a-sequence)) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="825eb-3165">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#run-activities-in-a-sequence)) in the pipeline.</span></span> <span data-ttu-id="825eb-3166">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span><span class="sxs-lookup"><span data-stu-id="825eb-3166">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="825eb-3167">It is the stored procedure that writes to a SQL table that the output dataset points to.</span><span class="sxs-lookup"><span data-stu-id="825eb-3167">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="825eb-3168">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="825eb-3168">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="825eb-3169">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-3169">JSON example</span></span>

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

<span data-ttu-id="825eb-3170">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-3170">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="825eb-3171">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="825eb-3171">.NET custom activity</span></span>
<span data-ttu-id="825eb-3172">You can specify the following properties in a .NET custom activity JSON definition.</span><span class="sxs-lookup"><span data-stu-id="825eb-3172">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="825eb-3173">The type property for the activity must be: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3173">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="825eb-3174">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="825eb-3174">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="825eb-3175">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span><span class="sxs-lookup"><span data-stu-id="825eb-3175">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="825eb-3176">Property</span><span class="sxs-lookup"><span data-stu-id="825eb-3176">Property</span></span> | <span data-ttu-id="825eb-3177">Description</span><span class="sxs-lookup"><span data-stu-id="825eb-3177">Description</span></span> | <span data-ttu-id="825eb-3178">Required</span><span class="sxs-lookup"><span data-stu-id="825eb-3178">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="825eb-3179">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="825eb-3179">AssemblyName</span></span> | <span data-ttu-id="825eb-3180">Name of the assembly.</span><span class="sxs-lookup"><span data-stu-id="825eb-3180">Name of the assembly.</span></span> <span data-ttu-id="825eb-3181">In the example, it is: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3181">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="825eb-3182">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3182">Yes</span></span> |
| <span data-ttu-id="825eb-3183">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="825eb-3183">EntryPoint</span></span> |<span data-ttu-id="825eb-3184">Name of the class that implements the IDotNetActivity interface.</span><span class="sxs-lookup"><span data-stu-id="825eb-3184">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="825eb-3185">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span><span class="sxs-lookup"><span data-stu-id="825eb-3185">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="825eb-3186">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3186">Yes</span></span> | 
| <span data-ttu-id="825eb-3187">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="825eb-3187">PackageLinkedService</span></span> | <span data-ttu-id="825eb-3188">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span><span class="sxs-lookup"><span data-stu-id="825eb-3188">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="825eb-3189">In the example, it is: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3189">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="825eb-3190">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3190">Yes</span></span> |
| <span data-ttu-id="825eb-3191">PackageFile</span><span class="sxs-lookup"><span data-stu-id="825eb-3191">PackageFile</span></span> | <span data-ttu-id="825eb-3192">Name of the zip file.</span><span class="sxs-lookup"><span data-stu-id="825eb-3192">Name of the zip file.</span></span> <span data-ttu-id="825eb-3193">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="825eb-3193">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="825eb-3194">Yes</span><span class="sxs-lookup"><span data-stu-id="825eb-3194">Yes</span></span> |
| <span data-ttu-id="825eb-3195">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="825eb-3195">extendedProperties</span></span> | <span data-ttu-id="825eb-3196">Extended properties that you can define and pass on to the .NET code.</span><span class="sxs-lookup"><span data-stu-id="825eb-3196">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="825eb-3197">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span><span class="sxs-lookup"><span data-stu-id="825eb-3197">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="825eb-3198">No</span><span class="sxs-lookup"><span data-stu-id="825eb-3198">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="825eb-3199">JSON example</span><span class="sxs-lookup"><span data-stu-id="825eb-3199">JSON example</span></span>

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

<span data-ttu-id="825eb-3200">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="825eb-3200">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="825eb-3201">Next Steps</span><span class="sxs-lookup"><span data-stu-id="825eb-3201">Next Steps</span></span>
<span data-ttu-id="825eb-3202">See the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="825eb-3202">See the following tutorials:</span></span> 

- [<span data-ttu-id="825eb-3203">Tutorial: create a pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="825eb-3203">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="825eb-3204">Tutorial: create a pipeline with a hive activity</span><span class="sxs-lookup"><span data-stu-id="825eb-3204">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)