---
title: Create/Schedule Pipelines, Chain Activities in Data Factory | Microsoft Docs
description: Learn to create a data pipeline in Azure Data Factory to move and transform data. Create a data driven workflow to produce ready to use information.
keywords: data pipeline, data driven workflow
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: shlo
ms.openlocfilehash: 32dbb53246f67b028da89c98a7fec22c6c4528d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564541"
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a><span data-ttu-id="011a9-105">Pipelines and Activities in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="011a9-105">Pipelines and Activities in Azure Data Factory</span></span>
<span data-ttu-id="011a9-106">This article helps you understand pipelines and activities in Azure Data Factory and use them to construct end-to-end data-driven workflows for your data movement and data processing scenarios.</span><span class="sxs-lookup"><span data-stu-id="011a9-106">This article helps you understand pipelines and activities in Azure Data Factory and use them to construct end-to-end data-driven workflows for your data movement and data processing scenarios.</span></span>  

> [!NOTE]
> <span data-ttu-id="011a9-107">This article assumes that you have gone through [Introduction to Azure Data Factory](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="011a9-107">This article assumes that you have gone through [Introduction to Azure Data Factory](data-factory-introduction.md).</span></span> <span data-ttu-id="011a9-108">If you do not have hands-on-experience with creating data factories, going through [data transformation tutorial](data-factory-build-your-first-pipeline.md) and/or [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) would help you understand this article better.</span><span class="sxs-lookup"><span data-stu-id="011a9-108">If you do not have hands-on-experience with creating data factories, going through [data transformation tutorial](data-factory-build-your-first-pipeline.md) and/or [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) would help you understand this article better.</span></span>  

## <a name="overview"></a><span data-ttu-id="011a9-109">Overview</span><span class="sxs-lookup"><span data-stu-id="011a9-109">Overview</span></span>
<span data-ttu-id="011a9-110">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="011a9-110">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="011a9-111">A pipeline is a logical grouping of activities that together perform a task.</span><span class="sxs-lookup"><span data-stu-id="011a9-111">A pipeline is a logical grouping of activities that together perform a task.</span></span> <span data-ttu-id="011a9-112">The activities in a pipeline define actions to perform on your data.</span><span class="sxs-lookup"><span data-stu-id="011a9-112">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="011a9-113">For example, you may use a copy activity to copy data from an on-premises SQL Server to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="011a9-113">For example, you may use a copy activity to copy data from an on-premises SQL Server to an Azure Blob Storage.</span></span> <span data-ttu-id="011a9-114">Then, use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process/transform data from the blob storage to produce output data.</span><span class="sxs-lookup"><span data-stu-id="011a9-114">Then, use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process/transform data from the blob storage to produce output data.</span></span> <span data-ttu-id="011a9-115">Finally, use a second copy activity to copy the output data to an Azure SQL Data Warehouse on top of which business intelligence (BI) reporting solutions are built.</span><span class="sxs-lookup"><span data-stu-id="011a9-115">Finally, use a second copy activity to copy the output data to an Azure SQL Data Warehouse on top of which business intelligence (BI) reporting solutions are built.</span></span> 

<span data-ttu-id="011a9-116">An activity can take zero or more input [datasets](data-factory-create-datasets.md) and produce one or more output [datasets](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="011a9-116">An activity can take zero or more input [datasets](data-factory-create-datasets.md) and produce one or more output [datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="011a9-117">The following diagram shows the relationship between pipeline, activity, and dataset in Data Factory:</span><span class="sxs-lookup"><span data-stu-id="011a9-117">The following diagram shows the relationship between pipeline, activity, and dataset in Data Factory:</span></span> 

![Relationship between pipeline, activity, and dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

<span data-ttu-id="011a9-119">A pipeline allows you to manage activities as a set instead of each one individually.</span><span class="sxs-lookup"><span data-stu-id="011a9-119">A pipeline allows you to manage activities as a set instead of each one individually.</span></span> <span data-ttu-id="011a9-120">For example, you can deploy, schedule, suspend, and resume a pipeline, instead of dealing with activities in the pipeline independently.</span><span class="sxs-lookup"><span data-stu-id="011a9-120">For example, you can deploy, schedule, suspend, and resume a pipeline, instead of dealing with activities in the pipeline independently.</span></span>

<span data-ttu-id="011a9-121">Data Factory supports two types of activities: data movement activities and data transformation activities.</span><span class="sxs-lookup"><span data-stu-id="011a9-121">Data Factory supports two types of activities: data movement activities and data transformation activities.</span></span> <span data-ttu-id="011a9-122">Each activity can have zero or more input [datasets](data-factory-create-datasets.md) and produce one or more output datasets.</span><span class="sxs-lookup"><span data-stu-id="011a9-122">Each activity can have zero or more input [datasets](data-factory-create-datasets.md) and produce one or more output datasets.</span></span>

<span data-ttu-id="011a9-123">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-123">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="011a9-124">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span><span class="sxs-lookup"><span data-stu-id="011a9-124">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="011a9-125">After you create a dataset, you can use it with activities in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-125">After you create a dataset, you can use it with activities in a pipeline.</span></span> <span data-ttu-id="011a9-126">For example, a dataset can be an input/output dataset of a Copy Activity or an HDInsightHive Activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-126">For example, a dataset can be an input/output dataset of a Copy Activity or an HDInsightHive Activity.</span></span> <span data-ttu-id="011a9-127">For more information about datasets, see [Datasets in Azure Data Factory](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="011a9-127">For more information about datasets, see [Datasets in Azure Data Factory](data-factory-create-datasets.md) article.</span></span>

### <a name="data-movement-activities"></a><span data-ttu-id="011a9-128">Data movement activities</span><span class="sxs-lookup"><span data-stu-id="011a9-128">Data movement activities</span></span>
<span data-ttu-id="011a9-129">Copy Activity in Data Factory copies data from a source data store to a sink data store.</span><span class="sxs-lookup"><span data-stu-id="011a9-129">Copy Activity in Data Factory copies data from a source data store to a sink data store.</span></span> <span data-ttu-id="011a9-130">Data Factory supports the following data stores.</span><span class="sxs-lookup"><span data-stu-id="011a9-130">Data Factory supports the following data stores.</span></span> <span data-ttu-id="011a9-131">Data from any source can be written to any sink.</span><span class="sxs-lookup"><span data-stu-id="011a9-131">Data from any source can be written to any sink.</span></span> <span data-ttu-id="011a9-132">Click a data store to learn how to copy data to and from that store.</span><span class="sxs-lookup"><span data-stu-id="011a9-132">Click a data store to learn how to copy data to and from that store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="011a9-133">Data stores with \* can be on-premises or on Azure IaaS, and require you to install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span><span class="sxs-lookup"><span data-stu-id="011a9-133">Data stores with \* can be on-premises or on Azure IaaS, and require you to install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

<span data-ttu-id="011a9-134">For more information, see [Data Movement Activities](data-factory-data-movement-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="011a9-134">For more information, see [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>

### <a name="data-transformation-activities"></a><span data-ttu-id="011a9-135">Data transformation activities</span><span class="sxs-lookup"><span data-stu-id="011a9-135">Data transformation activities</span></span>
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

<span data-ttu-id="011a9-136">For more information, see [Data Transformation Activities](data-factory-data-transformation-activities.md) article.</span><span class="sxs-lookup"><span data-stu-id="011a9-136">For more information, see [Data Transformation Activities](data-factory-data-transformation-activities.md) article.</span></span>

### <a name="custom-net-activities"></a><span data-ttu-id="011a9-137">Custom .NET activities</span><span class="sxs-lookup"><span data-stu-id="011a9-137">Custom .NET activities</span></span> 
<span data-ttu-id="011a9-138">If you need to move data to/from a data store that the Copy Activity doesn't support, or transform data using your own logic, create a **custom .NET activity**.</span><span class="sxs-lookup"><span data-stu-id="011a9-138">If you need to move data to/from a data store that the Copy Activity doesn't support, or transform data using your own logic, create a **custom .NET activity**.</span></span> <span data-ttu-id="011a9-139">For details on creating and using a custom activity, see [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="011a9-139">For details on creating and using a custom activity, see [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md).</span></span>

## <a name="pipeline-json"></a><span data-ttu-id="011a9-140">Pipeline JSON</span><span class="sxs-lookup"><span data-stu-id="011a9-140">Pipeline JSON</span></span>
<span data-ttu-id="011a9-141">Let us take a closer look on how a pipeline is defined in JSON format.</span><span class="sxs-lookup"><span data-stu-id="011a9-141">Let us take a closer look on how a pipeline is defined in JSON format.</span></span> <span data-ttu-id="011a9-142">The generic structure for a pipeline looks as follows:</span><span class="sxs-lookup"><span data-stu-id="011a9-142">The generic structure for a pipeline looks as follows:</span></span>

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| <span data-ttu-id="011a9-143">Tag</span><span class="sxs-lookup"><span data-stu-id="011a9-143">Tag</span></span> | <span data-ttu-id="011a9-144">Description</span><span class="sxs-lookup"><span data-stu-id="011a9-144">Description</span></span> | <span data-ttu-id="011a9-145">Required</span><span class="sxs-lookup"><span data-stu-id="011a9-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="011a9-146">name</span><span class="sxs-lookup"><span data-stu-id="011a9-146">name</span></span> |<span data-ttu-id="011a9-147">Name of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-147">Name of the pipeline.</span></span> <span data-ttu-id="011a9-148">Specify a name that represents the action that the pipeline performs.</span><span class="sxs-lookup"><span data-stu-id="011a9-148">Specify a name that represents the action that the pipeline performs.</span></span> <br/><ul><li><span data-ttu-id="011a9-149">Maximum number of characters: 260</span><span class="sxs-lookup"><span data-stu-id="011a9-149">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="011a9-150">Must start with a letter number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="011a9-150">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="011a9-151">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="011a9-151">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="011a9-152">Yes</span><span class="sxs-lookup"><span data-stu-id="011a9-152">Yes</span></span> |
| <span data-ttu-id="011a9-153">description</span><span class="sxs-lookup"><span data-stu-id="011a9-153">description</span></span> | <span data-ttu-id="011a9-154">Specify the text describing what the pipeline is used for.</span><span class="sxs-lookup"><span data-stu-id="011a9-154">Specify the text describing what the pipeline is used for.</span></span> |<span data-ttu-id="011a9-155">Yes</span><span class="sxs-lookup"><span data-stu-id="011a9-155">Yes</span></span> |
| <span data-ttu-id="011a9-156">activities</span><span class="sxs-lookup"><span data-stu-id="011a9-156">activities</span></span> | <span data-ttu-id="011a9-157">The **activities** section can have one or more activities defined within it.</span><span class="sxs-lookup"><span data-stu-id="011a9-157">The **activities** section can have one or more activities defined within it.</span></span> <span data-ttu-id="011a9-158">See the next section for details about the activities JSON element.</span><span class="sxs-lookup"><span data-stu-id="011a9-158">See the next section for details about the activities JSON element.</span></span> | <span data-ttu-id="011a9-159">Yes</span><span class="sxs-lookup"><span data-stu-id="011a9-159">Yes</span></span> |  
| <span data-ttu-id="011a9-160">start</span><span class="sxs-lookup"><span data-stu-id="011a9-160">start</span></span> | <span data-ttu-id="011a9-161">Start date-time for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-161">Start date-time for the pipeline.</span></span> <span data-ttu-id="011a9-162">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="011a9-162">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="011a9-163">For example: `2016-10-14T16:32:41Z`.</span><span class="sxs-lookup"><span data-stu-id="011a9-163">For example: `2016-10-14T16:32:41Z`.</span></span> <br/><br/><span data-ttu-id="011a9-164">It is possible to specify a local time, for example an EST time.</span><span class="sxs-lookup"><span data-stu-id="011a9-164">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="011a9-165">Here is an example: `2016-02-27T06:00:00-05:00`", which is 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="011a9-165">Here is an example: `2016-02-27T06:00:00-05:00`", which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="011a9-166">The start and end properties together specify active period for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-166">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="011a9-167">Output slices are only produced with in this active period.</span><span class="sxs-lookup"><span data-stu-id="011a9-167">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="011a9-168">No</span><span class="sxs-lookup"><span data-stu-id="011a9-168">No</span></span><br/><br/><span data-ttu-id="011a9-169">If you specify a value for the end property, you must specify value for the start property.</span><span class="sxs-lookup"><span data-stu-id="011a9-169">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="011a9-170">The start and end times can both be empty to create a pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-170">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="011a9-171">You must specify both values to set an active period for the pipeline to run.</span><span class="sxs-lookup"><span data-stu-id="011a9-171">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="011a9-172">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span><span class="sxs-lookup"><span data-stu-id="011a9-172">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="011a9-173">end</span><span class="sxs-lookup"><span data-stu-id="011a9-173">end</span></span> | <span data-ttu-id="011a9-174">End date-time for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-174">End date-time for the pipeline.</span></span> <span data-ttu-id="011a9-175">If specified must be in ISO format.</span><span class="sxs-lookup"><span data-stu-id="011a9-175">If specified must be in ISO format.</span></span> <span data-ttu-id="011a9-176">For example: `2016-10-14T17:32:41Z`</span><span class="sxs-lookup"><span data-stu-id="011a9-176">For example: `2016-10-14T17:32:41Z`</span></span> <br/><br/><span data-ttu-id="011a9-177">It is possible to specify a local time, for example an EST time.</span><span class="sxs-lookup"><span data-stu-id="011a9-177">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="011a9-178">Here is an example: `2016-02-27T06:00:00-05:00`, which is 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="011a9-178">Here is an example: `2016-02-27T06:00:00-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="011a9-179">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span><span class="sxs-lookup"><span data-stu-id="011a9-179">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="011a9-180">No</span><span class="sxs-lookup"><span data-stu-id="011a9-180">No</span></span> <br/><br/><span data-ttu-id="011a9-181">If you specify a value for the start property, you must specify value for the end property.</span><span class="sxs-lookup"><span data-stu-id="011a9-181">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="011a9-182">See notes for the **start** property.</span><span class="sxs-lookup"><span data-stu-id="011a9-182">See notes for the **start** property.</span></span> |
| <span data-ttu-id="011a9-183">isPaused</span><span class="sxs-lookup"><span data-stu-id="011a9-183">isPaused</span></span> | <span data-ttu-id="011a9-184">If set to true, the pipeline does not run.</span><span class="sxs-lookup"><span data-stu-id="011a9-184">If set to true, the pipeline does not run.</span></span> <span data-ttu-id="011a9-185">It's in the paused state.</span><span class="sxs-lookup"><span data-stu-id="011a9-185">It's in the paused state.</span></span> <span data-ttu-id="011a9-186">Default value = false.</span><span class="sxs-lookup"><span data-stu-id="011a9-186">Default value = false.</span></span> <span data-ttu-id="011a9-187">You can use this property to enable or disable a pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-187">You can use this property to enable or disable a pipeline.</span></span> |<span data-ttu-id="011a9-188">No</span><span class="sxs-lookup"><span data-stu-id="011a9-188">No</span></span> |
| <span data-ttu-id="011a9-189">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="011a9-189">pipelineMode</span></span> | <span data-ttu-id="011a9-190">The method for scheduling runs for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-190">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="011a9-191">Allowed values are: scheduled (default), onetime.</span><span class="sxs-lookup"><span data-stu-id="011a9-191">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="011a9-192">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span><span class="sxs-lookup"><span data-stu-id="011a9-192">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="011a9-193">‘Onetime’ indicates that the pipeline runs only once.</span><span class="sxs-lookup"><span data-stu-id="011a9-193">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="011a9-194">Onetime pipelines once created cannot be modified/updated currently.</span><span class="sxs-lookup"><span data-stu-id="011a9-194">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="011a9-195">See [Onetime pipeline](data-factory-scheduling-and-execution.md#onetime-pipeline) for details about onetime setting.</span><span class="sxs-lookup"><span data-stu-id="011a9-195">See [Onetime pipeline](data-factory-scheduling-and-execution.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="011a9-196">No</span><span class="sxs-lookup"><span data-stu-id="011a9-196">No</span></span> |
| <span data-ttu-id="011a9-197">expirationTime</span><span class="sxs-lookup"><span data-stu-id="011a9-197">expirationTime</span></span> | <span data-ttu-id="011a9-198">Duration of time after creation for which the [one-time pipeline](data-factory-scheduling-and-execution.md#onetime-pipeline) is valid and should remain provisioned.</span><span class="sxs-lookup"><span data-stu-id="011a9-198">Duration of time after creation for which the [one-time pipeline](data-factory-scheduling-and-execution.md#onetime-pipeline) is valid and should remain provisioned.</span></span> <span data-ttu-id="011a9-199">If it does not have any active, failed, or pending runs, the pipeline is automatically deleted once it reaches the expiration time.</span><span class="sxs-lookup"><span data-stu-id="011a9-199">If it does not have any active, failed, or pending runs, the pipeline is automatically deleted once it reaches the expiration time.</span></span> <span data-ttu-id="011a9-200">The default value: `"expirationTime": "3.00:00:00"`</span><span class="sxs-lookup"><span data-stu-id="011a9-200">The default value: `"expirationTime": "3.00:00:00"`</span></span>|<span data-ttu-id="011a9-201">No</span><span class="sxs-lookup"><span data-stu-id="011a9-201">No</span></span> |
| <span data-ttu-id="011a9-202">datasets</span><span class="sxs-lookup"><span data-stu-id="011a9-202">datasets</span></span> |<span data-ttu-id="011a9-203">List of datasets to be used by activities defined in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-203">List of datasets to be used by activities defined in the pipeline.</span></span> <span data-ttu-id="011a9-204">This property can be used to define datasets that are specific to this pipeline and not defined within the data factory.</span><span class="sxs-lookup"><span data-stu-id="011a9-204">This property can be used to define datasets that are specific to this pipeline and not defined within the data factory.</span></span> <span data-ttu-id="011a9-205">Datasets defined within this pipeline can only be used by this pipeline and cannot be shared.</span><span class="sxs-lookup"><span data-stu-id="011a9-205">Datasets defined within this pipeline can only be used by this pipeline and cannot be shared.</span></span> <span data-ttu-id="011a9-206">See [Scoped datasets](data-factory-create-datasets.md#scoped-datasets) for details.</span><span class="sxs-lookup"><span data-stu-id="011a9-206">See [Scoped datasets](data-factory-create-datasets.md#scoped-datasets) for details.</span></span> |<span data-ttu-id="011a9-207">No</span><span class="sxs-lookup"><span data-stu-id="011a9-207">No</span></span> |

## <a name="activity-json"></a><span data-ttu-id="011a9-208">Activity JSON</span><span class="sxs-lookup"><span data-stu-id="011a9-208">Activity JSON</span></span>
<span data-ttu-id="011a9-209">The **activities** section can have one or more activities defined within it.</span><span class="sxs-lookup"><span data-stu-id="011a9-209">The **activities** section can have one or more activities defined within it.</span></span> <span data-ttu-id="011a9-210">Each activity has the following top-level structure:</span><span class="sxs-lookup"><span data-stu-id="011a9-210">Each activity has the following top-level structure:</span></span>

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

<span data-ttu-id="011a9-211">Following table describe properties in the activity JSON definition:</span><span class="sxs-lookup"><span data-stu-id="011a9-211">Following table describe properties in the activity JSON definition:</span></span>

| <span data-ttu-id="011a9-212">Tag</span><span class="sxs-lookup"><span data-stu-id="011a9-212">Tag</span></span> | <span data-ttu-id="011a9-213">Description</span><span class="sxs-lookup"><span data-stu-id="011a9-213">Description</span></span> | <span data-ttu-id="011a9-214">Required</span><span class="sxs-lookup"><span data-stu-id="011a9-214">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="011a9-215">name</span><span class="sxs-lookup"><span data-stu-id="011a9-215">name</span></span> | <span data-ttu-id="011a9-216">Name of the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-216">Name of the activity.</span></span> <span data-ttu-id="011a9-217">Specify a name that represents the action that the activity performs.</span><span class="sxs-lookup"><span data-stu-id="011a9-217">Specify a name that represents the action that the activity performs.</span></span> <br/><ul><li><span data-ttu-id="011a9-218">Maximum number of characters: 260</span><span class="sxs-lookup"><span data-stu-id="011a9-218">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="011a9-219">Must start with a letter number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="011a9-219">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="011a9-220">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="011a9-220">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="011a9-221">Yes</span><span class="sxs-lookup"><span data-stu-id="011a9-221">Yes</span></span> |
| <span data-ttu-id="011a9-222">description</span><span class="sxs-lookup"><span data-stu-id="011a9-222">description</span></span> | <span data-ttu-id="011a9-223">Text describing what the activity or is used for</span><span class="sxs-lookup"><span data-stu-id="011a9-223">Text describing what the activity or is used for</span></span> |<span data-ttu-id="011a9-224">Yes</span><span class="sxs-lookup"><span data-stu-id="011a9-224">Yes</span></span> |
| <span data-ttu-id="011a9-225">type</span><span class="sxs-lookup"><span data-stu-id="011a9-225">type</span></span> | <span data-ttu-id="011a9-226">Type of the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-226">Type of the activity.</span></span> <span data-ttu-id="011a9-227">See the [Data Movement Activities](#data-movement-activities) and [Data Transformation Activities](#data-transformation-activities) sections for different types of activities.</span><span class="sxs-lookup"><span data-stu-id="011a9-227">See the [Data Movement Activities](#data-movement-activities) and [Data Transformation Activities](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="011a9-228">Yes</span><span class="sxs-lookup"><span data-stu-id="011a9-228">Yes</span></span> |
| <span data-ttu-id="011a9-229">inputs</span><span class="sxs-lookup"><span data-stu-id="011a9-229">inputs</span></span> |<span data-ttu-id="011a9-230">Input tables used by the activity</span><span class="sxs-lookup"><span data-stu-id="011a9-230">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="011a9-231">Yes</span><span class="sxs-lookup"><span data-stu-id="011a9-231">Yes</span></span> |
| <span data-ttu-id="011a9-232">outputs</span><span class="sxs-lookup"><span data-stu-id="011a9-232">outputs</span></span> |<span data-ttu-id="011a9-233">Output tables used by the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-233">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |<span data-ttu-id="011a9-234">Yes</span><span class="sxs-lookup"><span data-stu-id="011a9-234">Yes</span></span> |
| <span data-ttu-id="011a9-235">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="011a9-235">linkedServiceName</span></span> |<span data-ttu-id="011a9-236">Name of the linked service used by the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-236">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="011a9-237">An activity may require that you specify the linked service that links to the required compute environment.</span><span class="sxs-lookup"><span data-stu-id="011a9-237">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="011a9-238">Yes for HDInsight Activity and Azure Machine Learning Batch Scoring Activity</span><span class="sxs-lookup"><span data-stu-id="011a9-238">Yes for HDInsight Activity and Azure Machine Learning Batch Scoring Activity</span></span> <br/><br/><span data-ttu-id="011a9-239">No for all others</span><span class="sxs-lookup"><span data-stu-id="011a9-239">No for all others</span></span> |
| <span data-ttu-id="011a9-240">typeProperties</span><span class="sxs-lookup"><span data-stu-id="011a9-240">typeProperties</span></span> |<span data-ttu-id="011a9-241">Properties in the **typeProperties** section depend on type of the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-241">Properties in the **typeProperties** section depend on type of the activity.</span></span> <span data-ttu-id="011a9-242">To see type properties for an activity, click links to the activity in the previous section.</span><span class="sxs-lookup"><span data-stu-id="011a9-242">To see type properties for an activity, click links to the activity in the previous section.</span></span> | <span data-ttu-id="011a9-243">No</span><span class="sxs-lookup"><span data-stu-id="011a9-243">No</span></span> |
| <span data-ttu-id="011a9-244">policy</span><span class="sxs-lookup"><span data-stu-id="011a9-244">policy</span></span> |<span data-ttu-id="011a9-245">Policies that affect the run-time behavior of the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-245">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="011a9-246">If it is not specified, default policies are used.</span><span class="sxs-lookup"><span data-stu-id="011a9-246">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="011a9-247">No</span><span class="sxs-lookup"><span data-stu-id="011a9-247">No</span></span> |
| <span data-ttu-id="011a9-248">scheduler</span><span class="sxs-lookup"><span data-stu-id="011a9-248">scheduler</span></span> | <span data-ttu-id="011a9-249">“scheduler” property is used to define desired scheduling for the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-249">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="011a9-250">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#Availability).</span><span class="sxs-lookup"><span data-stu-id="011a9-250">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#Availability).</span></span> |<span data-ttu-id="011a9-251">No</span><span class="sxs-lookup"><span data-stu-id="011a9-251">No</span></span> |


### <a name="policies"></a><span data-ttu-id="011a9-252">Policies</span><span class="sxs-lookup"><span data-stu-id="011a9-252">Policies</span></span>
<span data-ttu-id="011a9-253">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span><span class="sxs-lookup"><span data-stu-id="011a9-253">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="011a9-254">The following table provides the details.</span><span class="sxs-lookup"><span data-stu-id="011a9-254">The following table provides the details.</span></span>

| <span data-ttu-id="011a9-255">Property</span><span class="sxs-lookup"><span data-stu-id="011a9-255">Property</span></span> | <span data-ttu-id="011a9-256">Permitted values</span><span class="sxs-lookup"><span data-stu-id="011a9-256">Permitted values</span></span> | <span data-ttu-id="011a9-257">Default Value</span><span class="sxs-lookup"><span data-stu-id="011a9-257">Default Value</span></span> | <span data-ttu-id="011a9-258">Description</span><span class="sxs-lookup"><span data-stu-id="011a9-258">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="011a9-259">concurrency</span><span class="sxs-lookup"><span data-stu-id="011a9-259">concurrency</span></span> |<span data-ttu-id="011a9-260">Integer</span><span class="sxs-lookup"><span data-stu-id="011a9-260">Integer</span></span> <br/><br/><span data-ttu-id="011a9-261">Max value: 10</span><span class="sxs-lookup"><span data-stu-id="011a9-261">Max value: 10</span></span> |<span data-ttu-id="011a9-262">1</span><span class="sxs-lookup"><span data-stu-id="011a9-262">1</span></span> |<span data-ttu-id="011a9-263">Number of concurrent executions of the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-263">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="011a9-264">It determines the number of parallel activity executions that can happen on different slices.</span><span class="sxs-lookup"><span data-stu-id="011a9-264">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="011a9-265">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span><span class="sxs-lookup"><span data-stu-id="011a9-265">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="011a9-266">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="011a9-266">executionPriorityOrder</span></span> |<span data-ttu-id="011a9-267">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="011a9-267">NewestFirst</span></span><br/><br/><span data-ttu-id="011a9-268">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="011a9-268">OldestFirst</span></span> |<span data-ttu-id="011a9-269">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="011a9-269">OldestFirst</span></span> |<span data-ttu-id="011a9-270">Determines the ordering of data slices that are being processed.</span><span class="sxs-lookup"><span data-stu-id="011a9-270">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="011a9-271">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span><span class="sxs-lookup"><span data-stu-id="011a9-271">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="011a9-272">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span><span class="sxs-lookup"><span data-stu-id="011a9-272">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="011a9-273">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span><span class="sxs-lookup"><span data-stu-id="011a9-273">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="011a9-274">retry</span><span class="sxs-lookup"><span data-stu-id="011a9-274">retry</span></span> |<span data-ttu-id="011a9-275">Integer</span><span class="sxs-lookup"><span data-stu-id="011a9-275">Integer</span></span><br/><br/><span data-ttu-id="011a9-276">Max value can be 10</span><span class="sxs-lookup"><span data-stu-id="011a9-276">Max value can be 10</span></span> |<span data-ttu-id="011a9-277">0</span><span class="sxs-lookup"><span data-stu-id="011a9-277">0</span></span> |<span data-ttu-id="011a9-278">Number of retries before the data processing for the slice is marked as Failure.</span><span class="sxs-lookup"><span data-stu-id="011a9-278">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="011a9-279">Activity execution for a data slice is retried up to the specified retry count.</span><span class="sxs-lookup"><span data-stu-id="011a9-279">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="011a9-280">The retry is done as soon as possible after the failure.</span><span class="sxs-lookup"><span data-stu-id="011a9-280">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="011a9-281">timeout</span><span class="sxs-lookup"><span data-stu-id="011a9-281">timeout</span></span> |<span data-ttu-id="011a9-282">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="011a9-282">TimeSpan</span></span> |<span data-ttu-id="011a9-283">00:00:00</span><span class="sxs-lookup"><span data-stu-id="011a9-283">00:00:00</span></span> |<span data-ttu-id="011a9-284">Timeout for the activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-284">Timeout for the activity.</span></span> <span data-ttu-id="011a9-285">Example: 00:10:00 (implies timeout 10 mins)</span><span class="sxs-lookup"><span data-stu-id="011a9-285">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="011a9-286">If a value is not specified or is 0, the timeout is infinite.</span><span class="sxs-lookup"><span data-stu-id="011a9-286">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="011a9-287">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span><span class="sxs-lookup"><span data-stu-id="011a9-287">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="011a9-288">The number of retries depends on the retry property.</span><span class="sxs-lookup"><span data-stu-id="011a9-288">The number of retries depends on the retry property.</span></span> <span data-ttu-id="011a9-289">When timeout occurs, the status is set to TimedOut.</span><span class="sxs-lookup"><span data-stu-id="011a9-289">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="011a9-290">delay</span><span class="sxs-lookup"><span data-stu-id="011a9-290">delay</span></span> |<span data-ttu-id="011a9-291">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="011a9-291">TimeSpan</span></span> |<span data-ttu-id="011a9-292">00:00:00</span><span class="sxs-lookup"><span data-stu-id="011a9-292">00:00:00</span></span> |<span data-ttu-id="011a9-293">Specify the delay before data processing of the slice starts.</span><span class="sxs-lookup"><span data-stu-id="011a9-293">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="011a9-294">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span><span class="sxs-lookup"><span data-stu-id="011a9-294">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="011a9-295">Example: 00:10:00 (implies delay of 10 mins)</span><span class="sxs-lookup"><span data-stu-id="011a9-295">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="011a9-296">longRetry</span><span class="sxs-lookup"><span data-stu-id="011a9-296">longRetry</span></span> |<span data-ttu-id="011a9-297">Integer</span><span class="sxs-lookup"><span data-stu-id="011a9-297">Integer</span></span><br/><br/><span data-ttu-id="011a9-298">Max value: 10</span><span class="sxs-lookup"><span data-stu-id="011a9-298">Max value: 10</span></span> |<span data-ttu-id="011a9-299">1</span><span class="sxs-lookup"><span data-stu-id="011a9-299">1</span></span> |<span data-ttu-id="011a9-300">The number of long retry attempts before the slice execution is failed.</span><span class="sxs-lookup"><span data-stu-id="011a9-300">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="011a9-301">longRetry attempts are spaced by longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="011a9-301">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="011a9-302">So if you need to specify a time between retry attempts, use longRetry.</span><span class="sxs-lookup"><span data-stu-id="011a9-302">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="011a9-303">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry \* longRetry.</span><span class="sxs-lookup"><span data-stu-id="011a9-303">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry \* longRetry.</span></span><br/><br/><span data-ttu-id="011a9-304">For example, if we have the following settings in the activity policy:</span><span class="sxs-lookup"><span data-stu-id="011a9-304">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="011a9-305">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="011a9-305">Retry: 3</span></span><br/><span data-ttu-id="011a9-306">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="011a9-306">longRetry: 2</span></span><br/><span data-ttu-id="011a9-307">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="011a9-307">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="011a9-308">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span><span class="sxs-lookup"><span data-stu-id="011a9-308">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="011a9-309">Initially there would be 3 consecutive execution attempts.</span><span class="sxs-lookup"><span data-stu-id="011a9-309">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="011a9-310">After each attempt, the slice status would be Retry.</span><span class="sxs-lookup"><span data-stu-id="011a9-310">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="011a9-311">After first 3 attempts are over, the slice status would be LongRetry.</span><span class="sxs-lookup"><span data-stu-id="011a9-311">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="011a9-312">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span><span class="sxs-lookup"><span data-stu-id="011a9-312">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="011a9-313">After that, the slice status would be Failed and no more retries would be attempted.</span><span class="sxs-lookup"><span data-stu-id="011a9-313">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="011a9-314">Hence overall 6 attempts were made.</span><span class="sxs-lookup"><span data-stu-id="011a9-314">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="011a9-315">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span><span class="sxs-lookup"><span data-stu-id="011a9-315">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="011a9-316">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span><span class="sxs-lookup"><span data-stu-id="011a9-316">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="011a9-317">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span><span class="sxs-lookup"><span data-stu-id="011a9-317">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="011a9-318">Word of caution: do not set high values for longRetry or longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="011a9-318">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="011a9-319">Typically, higher values imply other systemic issues.</span><span class="sxs-lookup"><span data-stu-id="011a9-319">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="011a9-320">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="011a9-320">longRetryInterval</span></span> |<span data-ttu-id="011a9-321">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="011a9-321">TimeSpan</span></span> |<span data-ttu-id="011a9-322">00:00:00</span><span class="sxs-lookup"><span data-stu-id="011a9-322">00:00:00</span></span> |<span data-ttu-id="011a9-323">The delay between long retry attempts</span><span class="sxs-lookup"><span data-stu-id="011a9-323">The delay between long retry attempts</span></span> |

## <a name="sample-copy-pipeline"></a><span data-ttu-id="011a9-324">Sample copy pipeline</span><span class="sxs-lookup"><span data-stu-id="011a9-324">Sample copy pipeline</span></span>
<span data-ttu-id="011a9-325">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span><span class="sxs-lookup"><span data-stu-id="011a9-325">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="011a9-326">In this sample, the [copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="011a9-326">In this sample, the [copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

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
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

<span data-ttu-id="011a9-327">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="011a9-327">Note the following points:</span></span>

* <span data-ttu-id="011a9-328">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="011a9-328">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="011a9-329">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="011a9-329">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> <span data-ttu-id="011a9-330">See [Datasets](data-factory-create-datasets.md) article for defining datasets in JSON.</span><span class="sxs-lookup"><span data-stu-id="011a9-330">See [Datasets](data-factory-create-datasets.md) article for defining datasets in JSON.</span></span> 
* <span data-ttu-id="011a9-331">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="011a9-331">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="011a9-332">In the [Data movement activities](#data-movement-activities) section, click the data store that you want to use as a source or a sink to learn more about moving data to/from that data store.</span><span class="sxs-lookup"><span data-stu-id="011a9-332">In the [Data movement activities](#data-movement-activities) section, click the data store that you want to use as a source or a sink to learn more about moving data to/from that data store.</span></span> 

<span data-ttu-id="011a9-333">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="011a9-333">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="sample-transformation-pipeline"></a><span data-ttu-id="011a9-334">Sample transformation pipeline</span><span class="sxs-lookup"><span data-stu-id="011a9-334">Sample transformation pipeline</span></span>
<span data-ttu-id="011a9-335">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span><span class="sxs-lookup"><span data-stu-id="011a9-335">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="011a9-336">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="011a9-336">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="011a9-337">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="011a9-337">Note the following points:</span></span> 

* <span data-ttu-id="011a9-338">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="011a9-338">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="011a9-339">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="011a9-339">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="011a9-340">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="011a9-340">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="011a9-341">The **typeProperties** section is different for each transformation activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-341">The **typeProperties** section is different for each transformation activity.</span></span> <span data-ttu-id="011a9-342">To learn about type properties supported for a transformation activity, click the transformation activity in the [Data transformation activities](#data-transformation-activities) table.</span><span class="sxs-lookup"><span data-stu-id="011a9-342">To learn about type properties supported for a transformation activity, click the transformation activity in the [Data transformation activities](#data-transformation-activities) table.</span></span> 

<span data-ttu-id="011a9-343">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="011a9-343">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="011a9-344">Multiple activities in a pipeline</span><span class="sxs-lookup"><span data-stu-id="011a9-344">Multiple activities in a pipeline</span></span>
<span data-ttu-id="011a9-345">The previous two sample pipelines have only one activity in them.</span><span class="sxs-lookup"><span data-stu-id="011a9-345">The previous two sample pipelines have only one activity in them.</span></span> <span data-ttu-id="011a9-346">You can have more than one activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-346">You can have more than one activity in a pipeline.</span></span>  

<span data-ttu-id="011a9-347">If you have multiple activities in a pipeline and output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span><span class="sxs-lookup"><span data-stu-id="011a9-347">If you have multiple activities in a pipeline and output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span> 

<span data-ttu-id="011a9-348">You can chain two activities by having the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-348">You can chain two activities by having the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="011a9-349">The second activity executes only when the first one completes successfully.</span><span class="sxs-lookup"><span data-stu-id="011a9-349">The second activity executes only when the first one completes successfully.</span></span>

![Chaining activities in the same pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-create-pipelines/chaining-one-pipeline.png)

<span data-ttu-id="011a9-351">In this sample, the pipeline has two activities: Activity1 and Activity2.</span><span class="sxs-lookup"><span data-stu-id="011a9-351">In this sample, the pipeline has two activities: Activity1 and Activity2.</span></span> <span data-ttu-id="011a9-352">The Activity1 takes Dataset1 as an input and produces an output Dataset2.</span><span class="sxs-lookup"><span data-stu-id="011a9-352">The Activity1 takes Dataset1 as an input and produces an output Dataset2.</span></span> <span data-ttu-id="011a9-353">The Activity takes Dataset2 as an input and produces an output Dataset3.</span><span class="sxs-lookup"><span data-stu-id="011a9-353">The Activity takes Dataset2 as an input and produces an output Dataset3.</span></span> <span data-ttu-id="011a9-354">Since the output of Activity1 (Dataset2) is the input of Activity2, the Activity2 runs only after the Activity completes successfully and produces the Dataset2 slice.</span><span class="sxs-lookup"><span data-stu-id="011a9-354">Since the output of Activity1 (Dataset2) is the input of Activity2, the Activity2 runs only after the Activity completes successfully and produces the Dataset2 slice.</span></span> <span data-ttu-id="011a9-355">If the Activity1 fails for some reason and does not produce the Dataset2 slice, the Activity 2 does not run for that slice (for example: 9 AM to 10 AM).</span><span class="sxs-lookup"><span data-stu-id="011a9-355">If the Activity1 fails for some reason and does not produce the Dataset2 slice, the Activity 2 does not run for that slice (for example: 9 AM to 10 AM).</span></span> 

<span data-ttu-id="011a9-356">You can also chain activities that are in different pipelines.</span><span class="sxs-lookup"><span data-stu-id="011a9-356">You can also chain activities that are in different pipelines.</span></span>

![Chaining activities in two pipelines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-create-pipelines/chaining-two-pipelines.png)

<span data-ttu-id="011a9-358">In this sample, Pipeline1 has only one activity that takes Dataset1 as an input and produces Dataset2 as an output.</span><span class="sxs-lookup"><span data-stu-id="011a9-358">In this sample, Pipeline1 has only one activity that takes Dataset1 as an input and produces Dataset2 as an output.</span></span> <span data-ttu-id="011a9-359">The Pipeline2 also has only one activity that takes Dataset2 as an input and Dataset3 as an output.</span><span class="sxs-lookup"><span data-stu-id="011a9-359">The Pipeline2 also has only one activity that takes Dataset2 as an input and Dataset3 as an output.</span></span> 

<span data-ttu-id="011a9-360">For more information, see [scheduling and execution](#chaining-activities).</span><span class="sxs-lookup"><span data-stu-id="011a9-360">For more information, see [scheduling and execution](#chaining-activities).</span></span> 

### <a name="json-example-for-chaining-two-copy-activity-in-a-pipeline"></a><span data-ttu-id="011a9-361">JSON example for chaining two copy activity in a pipeline</span><span class="sxs-lookup"><span data-stu-id="011a9-361">JSON example for chaining two copy activity in a pipeline</span></span>
<span data-ttu-id="011a9-362">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span><span class="sxs-lookup"><span data-stu-id="011a9-362">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="011a9-363">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span><span class="sxs-lookup"><span data-stu-id="011a9-363">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="011a9-364">**CopyActivity1**</span><span class="sxs-lookup"><span data-stu-id="011a9-364">**CopyActivity1**</span></span>

<span data-ttu-id="011a9-365">Input: Dataset.</span><span class="sxs-lookup"><span data-stu-id="011a9-365">Input: Dataset.</span></span> <span data-ttu-id="011a9-366">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="011a9-366">Output: Dataset2.</span></span>

<span data-ttu-id="011a9-367">**CopyActivity2**</span><span class="sxs-lookup"><span data-stu-id="011a9-367">**CopyActivity2**</span></span>

<span data-ttu-id="011a9-368">Input: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="011a9-368">Input: Dataset2.</span></span>  <span data-ttu-id="011a9-369">Output: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="011a9-369">Output: Dataset3.</span></span>

<span data-ttu-id="011a9-370">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span><span class="sxs-lookup"><span data-stu-id="011a9-370">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="011a9-371">Here is the sample pipeline JSON:</span><span class="sxs-lookup"><span data-stu-id="011a9-371">Here is the sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob to another"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T00:00:00Z",
        "end": "2016-08-25T05:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="011a9-372">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-372">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="011a9-373">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span><span class="sxs-lookup"><span data-stu-id="011a9-373">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="011a9-374">The output dataset is produced hourly within the pipeline start and end times.</span><span class="sxs-lookup"><span data-stu-id="011a9-374">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="011a9-375">Therefore, five dataset slices are produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span><span class="sxs-lookup"><span data-stu-id="011a9-375">Therefore, five dataset slices are produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 


<span data-ttu-id="011a9-376">In the example, CopyActivity2 can have an additional input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span><span class="sxs-lookup"><span data-stu-id="011a9-376">In the example, CopyActivity2 can have an additional input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="011a9-377">For example:</span><span class="sxs-lookup"><span data-stu-id="011a9-377">For example:</span></span>

<span data-ttu-id="011a9-378">**CopyActivity1**</span><span class="sxs-lookup"><span data-stu-id="011a9-378">**CopyActivity1**</span></span>

<span data-ttu-id="011a9-379">Input: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="011a9-379">Input: Dataset1.</span></span> <span data-ttu-id="011a9-380">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="011a9-380">Output: Dataset2.</span></span>

<span data-ttu-id="011a9-381">**CopyActivity2**</span><span class="sxs-lookup"><span data-stu-id="011a9-381">**CopyActivity2**</span></span>

<span data-ttu-id="011a9-382">Inputs: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="011a9-382">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="011a9-383">Output: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="011a9-383">Output: Dataset4.</span></span>

<span data-ttu-id="011a9-384">In this example, two input datasets are specified for the second copy activity.</span><span class="sxs-lookup"><span data-stu-id="011a9-384">In this example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="011a9-385">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span><span class="sxs-lookup"><span data-stu-id="011a9-385">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="011a9-386">CopyActivity2 would start only after the following conditions are met:</span><span class="sxs-lookup"><span data-stu-id="011a9-386">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="011a9-387">CopyActivity1 has successfully completed and Dataset2 is available.</span><span class="sxs-lookup"><span data-stu-id="011a9-387">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="011a9-388">This dataset is not used when copying data to Dataset4.</span><span class="sxs-lookup"><span data-stu-id="011a9-388">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="011a9-389">It only acts as a scheduling dependency for CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="011a9-389">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="011a9-390">Dataset3 is available.</span><span class="sxs-lookup"><span data-stu-id="011a9-390">Dataset3 is available.</span></span> <span data-ttu-id="011a9-391">This dataset represents the data that is copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="011a9-391">This dataset represents the data that is copied to the destination.</span></span> 

## <a name="scheduling-and-execution"></a><span data-ttu-id="011a9-392">Scheduling and Execution</span><span class="sxs-lookup"><span data-stu-id="011a9-392">Scheduling and Execution</span></span>
<span data-ttu-id="011a9-393">A pipeline is active only between its start time and end time.</span><span class="sxs-lookup"><span data-stu-id="011a9-393">A pipeline is active only between its start time and end time.</span></span> <span data-ttu-id="011a9-394">It is not executed before the start time or after the end time.</span><span class="sxs-lookup"><span data-stu-id="011a9-394">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="011a9-395">If the pipeline is paused, it does not get executed irrespective of its start and end time.</span><span class="sxs-lookup"><span data-stu-id="011a9-395">If the pipeline is paused, it does not get executed irrespective of its start and end time.</span></span> <span data-ttu-id="011a9-396">For a pipeline to run, it should not be paused.</span><span class="sxs-lookup"><span data-stu-id="011a9-396">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="011a9-397">In fact, it is not the pipeline that gets executed.</span><span class="sxs-lookup"><span data-stu-id="011a9-397">In fact, it is not the pipeline that gets executed.</span></span> <span data-ttu-id="011a9-398">It is the activities in the pipeline that get executed.</span><span class="sxs-lookup"><span data-stu-id="011a9-398">It is the activities in the pipeline that get executed.</span></span> <span data-ttu-id="011a9-399">However they do so in the overall context of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="011a9-399">However they do so in the overall context of the pipeline.</span></span> 

<span data-ttu-id="011a9-400">See [Scheduling and Execution](data-factory-scheduling-and-execution.md) to understand how scheduling and execution works in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="011a9-400">See [Scheduling and Execution](data-factory-scheduling-and-execution.md) to understand how scheduling and execution works in Azure Data Factory.</span></span>

## <a name="create-and-monitor-pipelines"></a><span data-ttu-id="011a9-401">Create and monitor pipelines</span><span class="sxs-lookup"><span data-stu-id="011a9-401">Create and monitor pipelines</span></span>
<span data-ttu-id="011a9-402">You can create pipelines by using one of these tools or SDKs.</span><span class="sxs-lookup"><span data-stu-id="011a9-402">You can create pipelines by using one of these tools or SDKs.</span></span> 

- <span data-ttu-id="011a9-403">Copy Wizard.</span><span class="sxs-lookup"><span data-stu-id="011a9-403">Copy Wizard.</span></span> 
- <span data-ttu-id="011a9-404">Azure portal</span><span class="sxs-lookup"><span data-stu-id="011a9-404">Azure portal</span></span>
- <span data-ttu-id="011a9-405">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="011a9-405">Visual Studio</span></span>
- <span data-ttu-id="011a9-406">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="011a9-406">Azure PowerShell</span></span>
- <span data-ttu-id="011a9-407">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="011a9-407">Azure Resource Manager template</span></span>
- <span data-ttu-id="011a9-408">REST API</span><span class="sxs-lookup"><span data-stu-id="011a9-408">REST API</span></span>
- <span data-ttu-id="011a9-409">.NET API</span><span class="sxs-lookup"><span data-stu-id="011a9-409">.NET API</span></span>

<span data-ttu-id="011a9-410">See the following tutorials for step-by-step instructions for creating pipelines by using one of these tools or SDKs.</span><span class="sxs-lookup"><span data-stu-id="011a9-410">See the following tutorials for step-by-step instructions for creating pipelines by using one of these tools or SDKs.</span></span>
 
- [<span data-ttu-id="011a9-411">Build a pipeline with a data transformation activity</span><span class="sxs-lookup"><span data-stu-id="011a9-411">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="011a9-412">Build a pipeline with a data movement activity</span><span class="sxs-lookup"><span data-stu-id="011a9-412">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="011a9-413">Once a pipeline is created/deployed, you can manage and monitor your pipelines by using the Azure portal blades or Monitor and Manage App.</span><span class="sxs-lookup"><span data-stu-id="011a9-413">Once a pipeline is created/deployed, you can manage and monitor your pipelines by using the Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="011a9-414">See the following topics for step-by-step instructions.</span><span class="sxs-lookup"><span data-stu-id="011a9-414">See the following topics for step-by-step instructions.</span></span> 

- <span data-ttu-id="011a9-415">[Monitor and manage pipelines by using Azure portal blades](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="011a9-415">[Monitor and manage pipelines by using Azure portal blades](data-factory-monitor-manage-pipelines.md).</span></span>
- [<span data-ttu-id="011a9-416">Monitor and manage pipelines by using Monitor and Manage App</span><span class="sxs-lookup"><span data-stu-id="011a9-416">Monitor and manage pipelines by using Monitor and Manage App</span></span>](data-factory-monitor-manage-app.md)


## <a name="next-steps"></a><span data-ttu-id="011a9-417">Next Steps</span><span class="sxs-lookup"><span data-stu-id="011a9-417">Next Steps</span></span>
- <span data-ttu-id="011a9-418">For more information about datasets, see [Create datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="011a9-418">For more information about datasets, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 
- <span data-ttu-id="011a9-419">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md) article.</span><span class="sxs-lookup"><span data-stu-id="011a9-419">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md) article.</span></span> 
  




