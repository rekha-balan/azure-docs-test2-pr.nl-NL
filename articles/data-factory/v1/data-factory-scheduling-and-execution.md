---
title: Scheduling and Execution with Data Factory | Microsoft Docs
description: Learn scheduling and execution aspects of Azure Data Factory application model.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: bd8b682e073e86bb824d31d6ebab20a80f807730
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871720"
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="90b78-103">Data Factory scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="90b78-103">Data Factory scheduling and execution</span></span>
> [!NOTE]
> <span data-ttu-id="90b78-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="90b78-104">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="90b78-105">If you are using the current version of the Data Factory service, see [pipeline execution and triggers](../concepts-pipeline-execution-triggers.md) article.</span><span class="sxs-lookup"><span data-stu-id="90b78-105">If you are using the current version of the Data Factory service, see [pipeline execution and triggers](../concepts-pipeline-execution-triggers.md) article.</span></span>

<span data-ttu-id="90b78-106">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="90b78-106">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="90b78-107">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span><span class="sxs-lookup"><span data-stu-id="90b78-107">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="90b78-108">For basic concepts of Azure Data Factory, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="90b78-108">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="90b78-109">Introduction to Data Factory</span><span class="sxs-lookup"><span data-stu-id="90b78-109">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="90b78-110">Pipelines</span><span class="sxs-lookup"><span data-stu-id="90b78-110">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="90b78-111">Datasets</span><span class="sxs-lookup"><span data-stu-id="90b78-111">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="90b78-112">Start and end times of pipeline</span><span class="sxs-lookup"><span data-stu-id="90b78-112">Start and end times of pipeline</span></span>
<span data-ttu-id="90b78-113">A pipeline is active only between its **start** time and **end** time.</span><span class="sxs-lookup"><span data-stu-id="90b78-113">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="90b78-114">It is not executed before the start time or after the end time.</span><span class="sxs-lookup"><span data-stu-id="90b78-114">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="90b78-115">If the pipeline is paused, it is not executed irrespective of its start and end time.</span><span class="sxs-lookup"><span data-stu-id="90b78-115">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="90b78-116">For a pipeline to run, it should not be paused.</span><span class="sxs-lookup"><span data-stu-id="90b78-116">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="90b78-117">You find these settings (start, end, paused) in the pipeline definition:</span><span class="sxs-lookup"><span data-stu-id="90b78-117">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="90b78-118">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="90b78-118">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="90b78-119">Specify schedule for an activity</span><span class="sxs-lookup"><span data-stu-id="90b78-119">Specify schedule for an activity</span></span>
<span data-ttu-id="90b78-120">It is not the pipeline that is executed.</span><span class="sxs-lookup"><span data-stu-id="90b78-120">It is not the pipeline that is executed.</span></span> <span data-ttu-id="90b78-121">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="90b78-121">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="90b78-122">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span><span class="sxs-lookup"><span data-stu-id="90b78-122">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="90b78-123">For example, you can schedule an activity to run hourly as follows:</span><span class="sxs-lookup"><span data-stu-id="90b78-123">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="90b78-124">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span><span class="sxs-lookup"><span data-stu-id="90b78-124">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="90b78-125">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span><span class="sxs-lookup"><span data-stu-id="90b78-125">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="90b78-126">These logical tumbling windows for an activity are called **activity windows**.</span><span class="sxs-lookup"><span data-stu-id="90b78-126">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Activity scheduler example](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="90b78-128">The **scheduler** property for an activity is optional.</span><span class="sxs-lookup"><span data-stu-id="90b78-128">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="90b78-129">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-129">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="90b78-130">Currently, output dataset is what drives the schedule.</span><span class="sxs-lookup"><span data-stu-id="90b78-130">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="90b78-131">Therefore, you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="90b78-131">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="90b78-132">Specify schedule for a dataset</span><span class="sxs-lookup"><span data-stu-id="90b78-132">Specify schedule for a dataset</span></span>
<span data-ttu-id="90b78-133">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span><span class="sxs-lookup"><span data-stu-id="90b78-133">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="90b78-134">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="90b78-134">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="90b78-135">**Frequency** in the **availability** section specifies the time unit.</span><span class="sxs-lookup"><span data-stu-id="90b78-135">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="90b78-136">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span><span class="sxs-lookup"><span data-stu-id="90b78-136">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="90b78-137">The **interval** property in the availability section specifies a multiplier for frequency.</span><span class="sxs-lookup"><span data-stu-id="90b78-137">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="90b78-138">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span><span class="sxs-lookup"><span data-stu-id="90b78-138">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="90b78-139">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span><span class="sxs-lookup"><span data-stu-id="90b78-139">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="90b78-140">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="90b78-140">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="90b78-141">**Input dataset:**</span><span class="sxs-lookup"><span data-stu-id="90b78-141">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="90b78-142">**Output dataset**</span><span class="sxs-lookup"><span data-stu-id="90b78-142">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="90b78-143">Currently, **output dataset drives the schedule**.</span><span class="sxs-lookup"><span data-stu-id="90b78-143">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="90b78-144">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span><span class="sxs-lookup"><span data-stu-id="90b78-144">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="90b78-145">Therefore, you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="90b78-145">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="90b78-146">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-146">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="90b78-147">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-147">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="90b78-148">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="90b78-148">This property is optional.</span></span> <span data-ttu-id="90b78-149">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-149">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="90b78-150">In this example, the activity runs hourly between the start and end times of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="90b78-150">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="90b78-151">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span><span class="sxs-lookup"><span data-stu-id="90b78-151">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="90b78-152">Each unit of data consumed or produced by an activity run is called a **data slice**.</span><span class="sxs-lookup"><span data-stu-id="90b78-152">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="90b78-153">The following diagram shows an example of an activity with one input dataset and one output dataset:</span><span class="sxs-lookup"><span data-stu-id="90b78-153">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Availability scheduler](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="90b78-155">The diagram shows the hourly data slices for the input and output dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-155">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="90b78-156">The diagram shows three input slices that are ready for processing.</span><span class="sxs-lookup"><span data-stu-id="90b78-156">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="90b78-157">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span><span class="sxs-lookup"><span data-stu-id="90b78-157">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="90b78-158">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="90b78-158">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="90b78-159">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="90b78-159">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="90b78-160">The schedule of an activity must match the schedule of the output dataset for the activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-160">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="90b78-161">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span><span class="sxs-lookup"><span data-stu-id="90b78-161">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="90b78-162">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span><span class="sxs-lookup"><span data-stu-id="90b78-162">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="90b78-163">You can use these variables for different purposes in your activity JSON.</span><span class="sxs-lookup"><span data-stu-id="90b78-163">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="90b78-164">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span><span class="sxs-lookup"><span data-stu-id="90b78-164">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="90b78-165">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="90b78-165">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="90b78-166">The **folderPath** is parameterized to have a separate folder for every hour.</span><span class="sxs-lookup"><span data-stu-id="90b78-166">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="90b78-167">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span><span class="sxs-lookup"><span data-stu-id="90b78-167">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="90b78-168">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span><span class="sxs-lookup"><span data-stu-id="90b78-168">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="90b78-169">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="90b78-169">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="90b78-170">Dataset availability and policies</span><span class="sxs-lookup"><span data-stu-id="90b78-170">Dataset availability and policies</span></span>
<span data-ttu-id="90b78-171">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span><span class="sxs-lookup"><span data-stu-id="90b78-171">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="90b78-172">There are a few other properties that affect the scheduling and execution of an activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-172">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="90b78-173">Dataset availability</span><span class="sxs-lookup"><span data-stu-id="90b78-173">Dataset availability</span></span> 
<span data-ttu-id="90b78-174">The following table describes properties you can use in the **availability** section:</span><span class="sxs-lookup"><span data-stu-id="90b78-174">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="90b78-175">Property</span><span class="sxs-lookup"><span data-stu-id="90b78-175">Property</span></span> | <span data-ttu-id="90b78-176">Description</span><span class="sxs-lookup"><span data-stu-id="90b78-176">Description</span></span> | <span data-ttu-id="90b78-177">Required</span><span class="sxs-lookup"><span data-stu-id="90b78-177">Required</span></span> | <span data-ttu-id="90b78-178">Default</span><span class="sxs-lookup"><span data-stu-id="90b78-178">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="90b78-179">frequency</span><span class="sxs-lookup"><span data-stu-id="90b78-179">frequency</span></span> |<span data-ttu-id="90b78-180">Specifies the time unit for dataset slice production.</span><span class="sxs-lookup"><span data-stu-id="90b78-180">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="90b78-181"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span><span class="sxs-lookup"><span data-stu-id="90b78-181"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="90b78-182">Yes</span><span class="sxs-lookup"><span data-stu-id="90b78-182">Yes</span></span> |<span data-ttu-id="90b78-183">NA</span><span class="sxs-lookup"><span data-stu-id="90b78-183">NA</span></span> |
| <span data-ttu-id="90b78-184">interval</span><span class="sxs-lookup"><span data-stu-id="90b78-184">interval</span></span> |<span data-ttu-id="90b78-185">Specifies a multiplier for frequency</span><span class="sxs-lookup"><span data-stu-id="90b78-185">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="90b78-186">”Frequency x interval” determines how often the slice is produced.</span><span class="sxs-lookup"><span data-stu-id="90b78-186">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="90b78-187">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="90b78-187">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="90b78-188"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span><span class="sxs-lookup"><span data-stu-id="90b78-188"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="90b78-189">Yes</span><span class="sxs-lookup"><span data-stu-id="90b78-189">Yes</span></span> |<span data-ttu-id="90b78-190">NA</span><span class="sxs-lookup"><span data-stu-id="90b78-190">NA</span></span> |
| <span data-ttu-id="90b78-191">style</span><span class="sxs-lookup"><span data-stu-id="90b78-191">style</span></span> |<span data-ttu-id="90b78-192">Specifies whether the slice should be produced at the start/end of the interval.</span><span class="sxs-lookup"><span data-stu-id="90b78-192">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="90b78-193">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="90b78-193">StartOfInterval</span></span></li><li><span data-ttu-id="90b78-194">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="90b78-194">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="90b78-195">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span><span class="sxs-lookup"><span data-stu-id="90b78-195">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="90b78-196">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span><span class="sxs-lookup"><span data-stu-id="90b78-196">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="90b78-197">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span><span class="sxs-lookup"><span data-stu-id="90b78-197">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="90b78-198">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span><span class="sxs-lookup"><span data-stu-id="90b78-198">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="90b78-199">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span><span class="sxs-lookup"><span data-stu-id="90b78-199">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="90b78-200">No</span><span class="sxs-lookup"><span data-stu-id="90b78-200">No</span></span> |<span data-ttu-id="90b78-201">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="90b78-201">EndOfInterval</span></span> |
| <span data-ttu-id="90b78-202">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="90b78-202">anchorDateTime</span></span> |<span data-ttu-id="90b78-203">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span><span class="sxs-lookup"><span data-stu-id="90b78-203">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="90b78-204"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span><span class="sxs-lookup"><span data-stu-id="90b78-204"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="90b78-205">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span><span class="sxs-lookup"><span data-stu-id="90b78-205">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="90b78-206">No</span><span class="sxs-lookup"><span data-stu-id="90b78-206">No</span></span> |<span data-ttu-id="90b78-207">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="90b78-207">01/01/0001</span></span> |
| <span data-ttu-id="90b78-208">offset</span><span class="sxs-lookup"><span data-stu-id="90b78-208">offset</span></span> |<span data-ttu-id="90b78-209">Timespan by which the start and end of all dataset slices are shifted.</span><span class="sxs-lookup"><span data-stu-id="90b78-209">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="90b78-210"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span><span class="sxs-lookup"><span data-stu-id="90b78-210"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="90b78-211">No</span><span class="sxs-lookup"><span data-stu-id="90b78-211">No</span></span> |<span data-ttu-id="90b78-212">NA</span><span class="sxs-lookup"><span data-stu-id="90b78-212">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="90b78-213">offset example</span><span class="sxs-lookup"><span data-stu-id="90b78-213">offset example</span></span>
<span data-ttu-id="90b78-214">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span><span class="sxs-lookup"><span data-stu-id="90b78-214">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="90b78-215">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="90b78-215">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="90b78-216">anchorDateTime example</span><span class="sxs-lookup"><span data-stu-id="90b78-216">anchorDateTime example</span></span>
<span data-ttu-id="90b78-217">In the following example, the dataset is produced once every 23 hours.</span><span class="sxs-lookup"><span data-stu-id="90b78-217">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="90b78-218">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span><span class="sxs-lookup"><span data-stu-id="90b78-218">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="90b78-219">offset/style Example</span><span class="sxs-lookup"><span data-stu-id="90b78-219">offset/style Example</span></span>
<span data-ttu-id="90b78-220">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="90b78-220">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="90b78-221">Dataset policy</span><span class="sxs-lookup"><span data-stu-id="90b78-221">Dataset policy</span></span>
<span data-ttu-id="90b78-222">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span><span class="sxs-lookup"><span data-stu-id="90b78-222">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="90b78-223">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span><span class="sxs-lookup"><span data-stu-id="90b78-223">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="90b78-224">After the slices are validated, the slice status changes to **Ready**.</span><span class="sxs-lookup"><span data-stu-id="90b78-224">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="90b78-225">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span><span class="sxs-lookup"><span data-stu-id="90b78-225">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="90b78-226">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="90b78-226">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="90b78-227">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span><span class="sxs-lookup"><span data-stu-id="90b78-227">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="90b78-228">The following table describes properties you can use in the **policy** section:</span><span class="sxs-lookup"><span data-stu-id="90b78-228">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="90b78-229">Policy Name</span><span class="sxs-lookup"><span data-stu-id="90b78-229">Policy Name</span></span> | <span data-ttu-id="90b78-230">Description</span><span class="sxs-lookup"><span data-stu-id="90b78-230">Description</span></span> | <span data-ttu-id="90b78-231">Applied To</span><span class="sxs-lookup"><span data-stu-id="90b78-231">Applied To</span></span> | <span data-ttu-id="90b78-232">Required</span><span class="sxs-lookup"><span data-stu-id="90b78-232">Required</span></span> | <span data-ttu-id="90b78-233">Default</span><span class="sxs-lookup"><span data-stu-id="90b78-233">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="90b78-234">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="90b78-234">minimumSizeMB</span></span> | <span data-ttu-id="90b78-235">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span><span class="sxs-lookup"><span data-stu-id="90b78-235">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="90b78-236">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="90b78-236">Azure Blob</span></span> |<span data-ttu-id="90b78-237">No</span><span class="sxs-lookup"><span data-stu-id="90b78-237">No</span></span> |<span data-ttu-id="90b78-238">NA</span><span class="sxs-lookup"><span data-stu-id="90b78-238">NA</span></span> |
| <span data-ttu-id="90b78-239">minimumRows</span><span class="sxs-lookup"><span data-stu-id="90b78-239">minimumRows</span></span> | <span data-ttu-id="90b78-240">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span><span class="sxs-lookup"><span data-stu-id="90b78-240">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="90b78-241">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="90b78-241">Azure SQL Database</span></span></li><li><span data-ttu-id="90b78-242">Azure Table</span><span class="sxs-lookup"><span data-stu-id="90b78-242">Azure Table</span></span></li></ul> |<span data-ttu-id="90b78-243">No</span><span class="sxs-lookup"><span data-stu-id="90b78-243">No</span></span> |<span data-ttu-id="90b78-244">NA</span><span class="sxs-lookup"><span data-stu-id="90b78-244">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="90b78-245">Examples</span><span class="sxs-lookup"><span data-stu-id="90b78-245">Examples</span></span>
<span data-ttu-id="90b78-246">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="90b78-246">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="90b78-247">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="90b78-247">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="90b78-248">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span><span class="sxs-lookup"><span data-stu-id="90b78-248">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="90b78-249">Activity policies</span><span class="sxs-lookup"><span data-stu-id="90b78-249">Activity policies</span></span>
<span data-ttu-id="90b78-250">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span><span class="sxs-lookup"><span data-stu-id="90b78-250">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="90b78-251">The following table provides the details.</span><span class="sxs-lookup"><span data-stu-id="90b78-251">The following table provides the details.</span></span>

| <span data-ttu-id="90b78-252">Property</span><span class="sxs-lookup"><span data-stu-id="90b78-252">Property</span></span> | <span data-ttu-id="90b78-253">Permitted values</span><span class="sxs-lookup"><span data-stu-id="90b78-253">Permitted values</span></span> | <span data-ttu-id="90b78-254">Default Value</span><span class="sxs-lookup"><span data-stu-id="90b78-254">Default Value</span></span> | <span data-ttu-id="90b78-255">Description</span><span class="sxs-lookup"><span data-stu-id="90b78-255">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="90b78-256">concurrency</span><span class="sxs-lookup"><span data-stu-id="90b78-256">concurrency</span></span> |<span data-ttu-id="90b78-257">Integer</span><span class="sxs-lookup"><span data-stu-id="90b78-257">Integer</span></span> <br/><br/><span data-ttu-id="90b78-258">Max value: 10</span><span class="sxs-lookup"><span data-stu-id="90b78-258">Max value: 10</span></span> |<span data-ttu-id="90b78-259">1</span><span class="sxs-lookup"><span data-stu-id="90b78-259">1</span></span> |<span data-ttu-id="90b78-260">Number of concurrent executions of the activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-260">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="90b78-261">It determines the number of parallel activity executions that can happen on different slices.</span><span class="sxs-lookup"><span data-stu-id="90b78-261">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="90b78-262">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span><span class="sxs-lookup"><span data-stu-id="90b78-262">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="90b78-263">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="90b78-263">executionPriorityOrder</span></span> |<span data-ttu-id="90b78-264">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="90b78-264">NewestFirst</span></span><br/><br/><span data-ttu-id="90b78-265">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="90b78-265">OldestFirst</span></span> |<span data-ttu-id="90b78-266">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="90b78-266">OldestFirst</span></span> |<span data-ttu-id="90b78-267">Determines the ordering of data slices that are being processed.</span><span class="sxs-lookup"><span data-stu-id="90b78-267">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="90b78-268">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span><span class="sxs-lookup"><span data-stu-id="90b78-268">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="90b78-269">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span><span class="sxs-lookup"><span data-stu-id="90b78-269">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="90b78-270">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span><span class="sxs-lookup"><span data-stu-id="90b78-270">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="90b78-271">retry</span><span class="sxs-lookup"><span data-stu-id="90b78-271">retry</span></span> |<span data-ttu-id="90b78-272">Integer</span><span class="sxs-lookup"><span data-stu-id="90b78-272">Integer</span></span><br/><br/><span data-ttu-id="90b78-273">Max value can be 10</span><span class="sxs-lookup"><span data-stu-id="90b78-273">Max value can be 10</span></span> |<span data-ttu-id="90b78-274">0</span><span class="sxs-lookup"><span data-stu-id="90b78-274">0</span></span> |<span data-ttu-id="90b78-275">Number of retries before the data processing for the slice is marked as Failure.</span><span class="sxs-lookup"><span data-stu-id="90b78-275">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="90b78-276">Activity execution for a data slice is retried up to the specified retry count.</span><span class="sxs-lookup"><span data-stu-id="90b78-276">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="90b78-277">The retry is done as soon as possible after the failure.</span><span class="sxs-lookup"><span data-stu-id="90b78-277">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="90b78-278">timeout</span><span class="sxs-lookup"><span data-stu-id="90b78-278">timeout</span></span> |<span data-ttu-id="90b78-279">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="90b78-279">TimeSpan</span></span> |<span data-ttu-id="90b78-280">00:00:00</span><span class="sxs-lookup"><span data-stu-id="90b78-280">00:00:00</span></span> |<span data-ttu-id="90b78-281">Timeout for the activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-281">Timeout for the activity.</span></span> <span data-ttu-id="90b78-282">Example: 00:10:00 (implies timeout 10 mins)</span><span class="sxs-lookup"><span data-stu-id="90b78-282">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="90b78-283">If a value is not specified or is 0, the timeout is infinite.</span><span class="sxs-lookup"><span data-stu-id="90b78-283">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="90b78-284">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span><span class="sxs-lookup"><span data-stu-id="90b78-284">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="90b78-285">The number of retries depends on the retry property.</span><span class="sxs-lookup"><span data-stu-id="90b78-285">The number of retries depends on the retry property.</span></span> <span data-ttu-id="90b78-286">When timeout occurs, the status is set to TimedOut.</span><span class="sxs-lookup"><span data-stu-id="90b78-286">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="90b78-287">delay</span><span class="sxs-lookup"><span data-stu-id="90b78-287">delay</span></span> |<span data-ttu-id="90b78-288">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="90b78-288">TimeSpan</span></span> |<span data-ttu-id="90b78-289">00:00:00</span><span class="sxs-lookup"><span data-stu-id="90b78-289">00:00:00</span></span> |<span data-ttu-id="90b78-290">Specify the delay before data processing of the slice starts.</span><span class="sxs-lookup"><span data-stu-id="90b78-290">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="90b78-291">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span><span class="sxs-lookup"><span data-stu-id="90b78-291">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="90b78-292">Example: 00:10:00 (implies delay of 10 mins)</span><span class="sxs-lookup"><span data-stu-id="90b78-292">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="90b78-293">longRetry</span><span class="sxs-lookup"><span data-stu-id="90b78-293">longRetry</span></span> |<span data-ttu-id="90b78-294">Integer</span><span class="sxs-lookup"><span data-stu-id="90b78-294">Integer</span></span><br/><br/><span data-ttu-id="90b78-295">Max value: 10</span><span class="sxs-lookup"><span data-stu-id="90b78-295">Max value: 10</span></span> |<span data-ttu-id="90b78-296">1</span><span class="sxs-lookup"><span data-stu-id="90b78-296">1</span></span> |<span data-ttu-id="90b78-297">The number of long retry attempts before the slice execution is failed.</span><span class="sxs-lookup"><span data-stu-id="90b78-297">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="90b78-298">longRetry attempts are spaced by longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="90b78-298">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="90b78-299">So if you need to specify a time between retry attempts, use longRetry.</span><span class="sxs-lookup"><span data-stu-id="90b78-299">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="90b78-300">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry \* longRetry.</span><span class="sxs-lookup"><span data-stu-id="90b78-300">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry \* longRetry.</span></span><br/><br/><span data-ttu-id="90b78-301">For example, if we have the following settings in the activity policy:</span><span class="sxs-lookup"><span data-stu-id="90b78-301">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="90b78-302">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="90b78-302">Retry: 3</span></span><br/><span data-ttu-id="90b78-303">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="90b78-303">longRetry: 2</span></span><br/><span data-ttu-id="90b78-304">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="90b78-304">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="90b78-305">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span><span class="sxs-lookup"><span data-stu-id="90b78-305">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="90b78-306">Initially there would be 3 consecutive execution attempts.</span><span class="sxs-lookup"><span data-stu-id="90b78-306">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="90b78-307">After each attempt, the slice status would be Retry.</span><span class="sxs-lookup"><span data-stu-id="90b78-307">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="90b78-308">After first 3 attempts are over, the slice status would be LongRetry.</span><span class="sxs-lookup"><span data-stu-id="90b78-308">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="90b78-309">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span><span class="sxs-lookup"><span data-stu-id="90b78-309">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="90b78-310">After that, the slice status would be Failed and no more retries would be attempted.</span><span class="sxs-lookup"><span data-stu-id="90b78-310">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="90b78-311">Hence overall 6 attempts were made.</span><span class="sxs-lookup"><span data-stu-id="90b78-311">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="90b78-312">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span><span class="sxs-lookup"><span data-stu-id="90b78-312">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="90b78-313">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span><span class="sxs-lookup"><span data-stu-id="90b78-313">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="90b78-314">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span><span class="sxs-lookup"><span data-stu-id="90b78-314">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="90b78-315">Word of caution: do not set high values for longRetry or longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="90b78-315">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="90b78-316">Typically, higher values imply other systemic issues.</span><span class="sxs-lookup"><span data-stu-id="90b78-316">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="90b78-317">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="90b78-317">longRetryInterval</span></span> |<span data-ttu-id="90b78-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="90b78-318">TimeSpan</span></span> |<span data-ttu-id="90b78-319">00:00:00</span><span class="sxs-lookup"><span data-stu-id="90b78-319">00:00:00</span></span> |<span data-ttu-id="90b78-320">The delay between long retry attempts</span><span class="sxs-lookup"><span data-stu-id="90b78-320">The delay between long retry attempts</span></span> |

<span data-ttu-id="90b78-321">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="90b78-321">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="90b78-322">Parallel processing of data slices</span><span class="sxs-lookup"><span data-stu-id="90b78-322">Parallel processing of data slices</span></span>
<span data-ttu-id="90b78-323">You can set the start date for the pipeline in the past.</span><span class="sxs-lookup"><span data-stu-id="90b78-323">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="90b78-324">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span><span class="sxs-lookup"><span data-stu-id="90b78-324">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="90b78-325">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="90b78-325">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="90b78-326">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span><span class="sxs-lookup"><span data-stu-id="90b78-326">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="90b78-327">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span><span class="sxs-lookup"><span data-stu-id="90b78-327">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="90b78-328">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="90b78-328">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="90b78-329">For a description of the style property, see [dataset availability](#dataset-availability) section.</span><span class="sxs-lookup"><span data-stu-id="90b78-329">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="90b78-330">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span><span class="sxs-lookup"><span data-stu-id="90b78-330">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="90b78-331">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span><span class="sxs-lookup"><span data-stu-id="90b78-331">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="90b78-332">This property determines the number of parallel activity executions that can happen on different slices.</span><span class="sxs-lookup"><span data-stu-id="90b78-332">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="90b78-333">The default value for the concurrency property is 1.</span><span class="sxs-lookup"><span data-stu-id="90b78-333">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="90b78-334">Therefore, one slice is processed at a time by default.</span><span class="sxs-lookup"><span data-stu-id="90b78-334">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="90b78-335">The maximum value is 10.</span><span class="sxs-lookup"><span data-stu-id="90b78-335">The maximum value is 10.</span></span> <span data-ttu-id="90b78-336">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span><span class="sxs-lookup"><span data-stu-id="90b78-336">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="90b78-337">Rerun a failed data slice</span><span class="sxs-lookup"><span data-stu-id="90b78-337">Rerun a failed data slice</span></span>
<span data-ttu-id="90b78-338">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span><span class="sxs-lookup"><span data-stu-id="90b78-338">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="90b78-339">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span><span class="sxs-lookup"><span data-stu-id="90b78-339">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="90b78-340">Consider the following example, which shows two activities.</span><span class="sxs-lookup"><span data-stu-id="90b78-340">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="90b78-341">Activity1 and Activity 2.</span><span class="sxs-lookup"><span data-stu-id="90b78-341">Activity1 and Activity 2.</span></span> <span data-ttu-id="90b78-342">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-342">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![Failed slice](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="90b78-344">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span><span class="sxs-lookup"><span data-stu-id="90b78-344">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="90b78-345">Data Factory automatically tracks dependency for the time series dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-345">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="90b78-346">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span><span class="sxs-lookup"><span data-stu-id="90b78-346">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="90b78-347">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span><span class="sxs-lookup"><span data-stu-id="90b78-347">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="90b78-348">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span><span class="sxs-lookup"><span data-stu-id="90b78-348">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="90b78-349">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="90b78-349">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="90b78-350">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-350">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![Rerun failed slice](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="90b78-352">Multiple activities in a pipeline</span><span class="sxs-lookup"><span data-stu-id="90b78-352">Multiple activities in a pipeline</span></span>
<span data-ttu-id="90b78-353">You can have more than one activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="90b78-353">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="90b78-354">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span><span class="sxs-lookup"><span data-stu-id="90b78-354">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="90b78-355">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-355">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="90b78-356">The activities can be in the same pipeline or in different pipelines.</span><span class="sxs-lookup"><span data-stu-id="90b78-356">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="90b78-357">The second activity executes only when the first one finishes successfully.</span><span class="sxs-lookup"><span data-stu-id="90b78-357">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="90b78-358">For example, consider the following case where a pipeline has two activities:</span><span class="sxs-lookup"><span data-stu-id="90b78-358">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="90b78-359">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span><span class="sxs-lookup"><span data-stu-id="90b78-359">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="90b78-360">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span><span class="sxs-lookup"><span data-stu-id="90b78-360">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="90b78-361">In this scenario, activities A1 and A2 are in the same pipeline.</span><span class="sxs-lookup"><span data-stu-id="90b78-361">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="90b78-362">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span><span class="sxs-lookup"><span data-stu-id="90b78-362">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="90b78-363">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span><span class="sxs-lookup"><span data-stu-id="90b78-363">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="90b78-364">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span><span class="sxs-lookup"><span data-stu-id="90b78-364">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="90b78-365">The Diagram view with both activities in the same pipeline would look like the following diagram:</span><span class="sxs-lookup"><span data-stu-id="90b78-365">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![Chaining activities in the same pipeline](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="90b78-367">As mentioned earlier, the activities could be in different pipelines.</span><span class="sxs-lookup"><span data-stu-id="90b78-367">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="90b78-368">In such a scenario, the diagram view would look like the following diagram:</span><span class="sxs-lookup"><span data-stu-id="90b78-368">In such a scenario, the diagram view would look like the following diagram:</span></span>

![Chaining activities in two pipelines](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="90b78-370">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span><span class="sxs-lookup"><span data-stu-id="90b78-370">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="90b78-371">Model datasets with different frequencies</span><span class="sxs-lookup"><span data-stu-id="90b78-371">Model datasets with different frequencies</span></span>
<span data-ttu-id="90b78-372">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span><span class="sxs-lookup"><span data-stu-id="90b78-372">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="90b78-373">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span><span class="sxs-lookup"><span data-stu-id="90b78-373">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="90b78-374">Data Factory supports modeling these scenarios.</span><span class="sxs-lookup"><span data-stu-id="90b78-374">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="90b78-375">Sample 1: Produce a daily output report for input data that is available every hour</span><span class="sxs-lookup"><span data-stu-id="90b78-375">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="90b78-376">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="90b78-376">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="90b78-377">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="90b78-377">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="90b78-378">Here is how you can model this scenario with Data Factory:</span><span class="sxs-lookup"><span data-stu-id="90b78-378">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="90b78-379">**Input dataset**</span><span class="sxs-lookup"><span data-stu-id="90b78-379">**Input dataset**</span></span>

<span data-ttu-id="90b78-380">The hourly input files are dropped in the folder for the given day.</span><span class="sxs-lookup"><span data-stu-id="90b78-380">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="90b78-381">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="90b78-381">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="90b78-382">**Output dataset**</span><span class="sxs-lookup"><span data-stu-id="90b78-382">**Output dataset**</span></span>

<span data-ttu-id="90b78-383">One output file is created every day in the day's folder.</span><span class="sxs-lookup"><span data-stu-id="90b78-383">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="90b78-384">Availability of output is set at **Day** (frequency: Day and interval: 1).</span><span class="sxs-lookup"><span data-stu-id="90b78-384">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="90b78-385">**Activity: hive activity in a pipeline**</span><span class="sxs-lookup"><span data-stu-id="90b78-385">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="90b78-386">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="90b78-386">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="90b78-387">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span><span class="sxs-lookup"><span data-stu-id="90b78-387">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
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
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
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

<span data-ttu-id="90b78-388">The following diagram shows the scenario from a data-dependency point of view.</span><span class="sxs-lookup"><span data-stu-id="90b78-388">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![Data dependency](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="90b78-390">The output slice for every day depends on 24 hourly slices from an input dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-390">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="90b78-391">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span><span class="sxs-lookup"><span data-stu-id="90b78-391">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="90b78-392">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span><span class="sxs-lookup"><span data-stu-id="90b78-392">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="90b78-393">Sample 2: Specify dependency with expressions and Data Factory functions</span><span class="sxs-lookup"><span data-stu-id="90b78-393">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="90b78-394">Let’s consider another scenario.</span><span class="sxs-lookup"><span data-stu-id="90b78-394">Let’s consider another scenario.</span></span> <span data-ttu-id="90b78-395">Suppose you have a hive activity that processes two input datasets.</span><span class="sxs-lookup"><span data-stu-id="90b78-395">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="90b78-396">One of them has new data daily, but one of them gets new data every week.</span><span class="sxs-lookup"><span data-stu-id="90b78-396">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="90b78-397">Suppose you wanted to do a join across the two inputs and produce an output every day.</span><span class="sxs-lookup"><span data-stu-id="90b78-397">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="90b78-398">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span><span class="sxs-lookup"><span data-stu-id="90b78-398">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="90b78-399">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-399">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="90b78-400">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span><span class="sxs-lookup"><span data-stu-id="90b78-400">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="90b78-401">**Input1: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="90b78-401">**Input1: Azure blob**</span></span>

<span data-ttu-id="90b78-402">The first input is the Azure blob being updated daily.</span><span class="sxs-lookup"><span data-stu-id="90b78-402">The first input is the Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="90b78-403">**Input2: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="90b78-403">**Input2: Azure blob**</span></span>

<span data-ttu-id="90b78-404">Input2 is the Azure blob being updated weekly.</span><span class="sxs-lookup"><span data-stu-id="90b78-404">Input2 is the Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="90b78-405">**Output: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="90b78-405">**Output: Azure blob**</span></span>

<span data-ttu-id="90b78-406">One output file is created every day in the folder for the day.</span><span class="sxs-lookup"><span data-stu-id="90b78-406">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="90b78-407">Availability of output is set to **day** (frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="90b78-407">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="90b78-408">**Activity: hive activity in a pipeline**</span><span class="sxs-lookup"><span data-stu-id="90b78-408">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="90b78-409">The hive activity takes the two inputs and produces an output slice every day.</span><span class="sxs-lookup"><span data-stu-id="90b78-409">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="90b78-410">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span><span class="sxs-lookup"><span data-stu-id="90b78-410">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
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

<span data-ttu-id="90b78-411">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span><span class="sxs-lookup"><span data-stu-id="90b78-411">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="90b78-412">Appendix</span><span class="sxs-lookup"><span data-stu-id="90b78-412">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="90b78-413">Example: copy sequentially</span><span class="sxs-lookup"><span data-stu-id="90b78-413">Example: copy sequentially</span></span>
<span data-ttu-id="90b78-414">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span><span class="sxs-lookup"><span data-stu-id="90b78-414">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="90b78-415">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span><span class="sxs-lookup"><span data-stu-id="90b78-415">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="90b78-416">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="90b78-416">CopyActivity1</span></span>

<span data-ttu-id="90b78-417">Input: Dataset.</span><span class="sxs-lookup"><span data-stu-id="90b78-417">Input: Dataset.</span></span> <span data-ttu-id="90b78-418">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="90b78-418">Output: Dataset2.</span></span>

<span data-ttu-id="90b78-419">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="90b78-419">CopyActivity2</span></span>

<span data-ttu-id="90b78-420">Input: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="90b78-420">Input: Dataset2.</span></span>  <span data-ttu-id="90b78-421">Output: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="90b78-421">Output: Dataset3.</span></span>

<span data-ttu-id="90b78-422">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span><span class="sxs-lookup"><span data-stu-id="90b78-422">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="90b78-423">Here is the sample pipeline JSON:</span><span class="sxs-lookup"><span data-stu-id="90b78-423">Here is the sample pipeline JSON:</span></span>

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
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="90b78-424">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-424">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="90b78-425">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span><span class="sxs-lookup"><span data-stu-id="90b78-425">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="90b78-426">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span><span class="sxs-lookup"><span data-stu-id="90b78-426">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="90b78-427">For example:</span><span class="sxs-lookup"><span data-stu-id="90b78-427">For example:</span></span>

<span data-ttu-id="90b78-428">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="90b78-428">CopyActivity1</span></span>

<span data-ttu-id="90b78-429">Input: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="90b78-429">Input: Dataset1.</span></span> <span data-ttu-id="90b78-430">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="90b78-430">Output: Dataset2.</span></span>

<span data-ttu-id="90b78-431">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="90b78-431">CopyActivity2</span></span>

<span data-ttu-id="90b78-432">Inputs: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="90b78-432">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="90b78-433">Output: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="90b78-433">Output: Dataset4.</span></span>

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
                "name": "CopyFromBlobToBlob",
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
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="90b78-434">Notice that in the example, two input datasets are specified for the second copy activity.</span><span class="sxs-lookup"><span data-stu-id="90b78-434">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="90b78-435">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span><span class="sxs-lookup"><span data-stu-id="90b78-435">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="90b78-436">CopyActivity2 would start only after the following conditions are met:</span><span class="sxs-lookup"><span data-stu-id="90b78-436">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="90b78-437">CopyActivity1 has successfully completed and Dataset2 is available.</span><span class="sxs-lookup"><span data-stu-id="90b78-437">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="90b78-438">This dataset is not used when copying data to Dataset4.</span><span class="sxs-lookup"><span data-stu-id="90b78-438">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="90b78-439">It only acts as a scheduling dependency for CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="90b78-439">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="90b78-440">Dataset3 is available.</span><span class="sxs-lookup"><span data-stu-id="90b78-440">Dataset3 is available.</span></span> <span data-ttu-id="90b78-441">This dataset represents the data that is copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="90b78-441">This dataset represents the data that is copied to the destination.</span></span> 
