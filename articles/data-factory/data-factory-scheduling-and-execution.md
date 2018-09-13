---
title: Scheduling and Execution with Data Factory | Microsoft Docs
description: Learn scheduling and execution aspects of Azure Data Factory application model.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: spelluru
ms.openlocfilehash: 696714755d79dafcf55ca9479610be01b539e786
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549182"
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="3911d-103">Data Factory scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="3911d-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="3911d-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="3911d-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3911d-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3911d-105">Prerequisites</span></span>
<span data-ttu-id="3911d-106">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span><span class="sxs-lookup"><span data-stu-id="3911d-106">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="3911d-107">For basic concepts of Azure Data Factory, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="3911d-107">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="3911d-108">Introduction to Data Factory</span><span class="sxs-lookup"><span data-stu-id="3911d-108">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="3911d-109">Pipelines</span><span class="sxs-lookup"><span data-stu-id="3911d-109">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="3911d-110">Datasets</span><span class="sxs-lookup"><span data-stu-id="3911d-110">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="schedule-an-activity"></a><span data-ttu-id="3911d-111">Schedule an activity</span><span class="sxs-lookup"><span data-stu-id="3911d-111">Schedule an activity</span></span>
<span data-ttu-id="3911d-112">With the scheduler section of the activity JSON, you can specify a recurring schedule for an activity.</span><span class="sxs-lookup"><span data-stu-id="3911d-112">With the scheduler section of the activity JSON, you can specify a recurring schedule for an activity.</span></span> <span data-ttu-id="3911d-113">For example, you can schedule an activity every hour as follows:</span><span class="sxs-lookup"><span data-stu-id="3911d-113">For example, you can schedule an activity every hour as follows:</span></span>

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},  
```

![Scheduler example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="3911d-115">As shown in the diagram, specifying a schedule for the activity creates a series of tumbling windows.</span><span class="sxs-lookup"><span data-stu-id="3911d-115">As shown in the diagram, specifying a schedule for the activity creates a series of tumbling windows.</span></span> <span data-ttu-id="3911d-116">Tumbling windows are a series of fixed-size, non-overlapping, contiguous time intervals.</span><span class="sxs-lookup"><span data-stu-id="3911d-116">Tumbling windows are a series of fixed-size, non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="3911d-117">These logical tumbling windows for the activity are called *activity windows*.</span><span class="sxs-lookup"><span data-stu-id="3911d-117">These logical tumbling windows for the activity are called *activity windows*.</span></span>

<span data-ttu-id="3911d-118">For the currently executing activity window, you can access the time interval associated with the activity window with [WindowStart](data-factory-functions-variables.md#data-factory-system-variables) and [WindowEnd](data-factory-functions-variables.md#data-factory-system-variables) system variables in the activity JSON.</span><span class="sxs-lookup"><span data-stu-id="3911d-118">For the currently executing activity window, you can access the time interval associated with the activity window with [WindowStart](data-factory-functions-variables.md#data-factory-system-variables) and [WindowEnd](data-factory-functions-variables.md#data-factory-system-variables) system variables in the activity JSON.</span></span> <span data-ttu-id="3911d-119">You can use these variables for different purposes in your activity JSON.</span><span class="sxs-lookup"><span data-stu-id="3911d-119">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="3911d-120">For example, you can use them to select data from input and output datasets representing time series data.</span><span class="sxs-lookup"><span data-stu-id="3911d-120">For example, you can use them to select data from input and output datasets representing time series data.</span></span>

<span data-ttu-id="3911d-121">The **scheduler** property supports the same subproperties as the **availability** property in a dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-121">The **scheduler** property supports the same subproperties as the **availability** property in a dataset.</span></span> <span data-ttu-id="3911d-122">See [Dataset availability](data-factory-create-datasets.md#Availability) for details.</span><span class="sxs-lookup"><span data-stu-id="3911d-122">See [Dataset availability](data-factory-create-datasets.md#Availability) for details.</span></span> <span data-ttu-id="3911d-123">Examples: scheduling at a specific time offset, or setting the mode to align processing at the beginning or end of the interval for the activity window.</span><span class="sxs-lookup"><span data-stu-id="3911d-123">Examples: scheduling at a specific time offset, or setting the mode to align processing at the beginning or end of the interval for the activity window.</span></span>

<span data-ttu-id="3911d-124">You can specify **scheduler** properties for an activity, but this property is **optional**.</span><span class="sxs-lookup"><span data-stu-id="3911d-124">You can specify **scheduler** properties for an activity, but this property is **optional**.</span></span> <span data-ttu-id="3911d-125">If you do specify a property, it must match the cadence you specify in the output dataset definition.</span><span class="sxs-lookup"><span data-stu-id="3911d-125">If you do specify a property, it must match the cadence you specify in the output dataset definition.</span></span> <span data-ttu-id="3911d-126">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="3911d-126">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="3911d-127">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-127">If the activity doesn't take any input, you can skip creating the input dataset.</span></span>

## <a name="time-series-datasets-and-data-slices"></a><span data-ttu-id="3911d-128">Time series datasets and data slices</span><span class="sxs-lookup"><span data-stu-id="3911d-128">Time series datasets and data slices</span></span>
<span data-ttu-id="3911d-129">Time series data is a continuous sequence of data points that typically consists of successive measurements made over a time interval.</span><span class="sxs-lookup"><span data-stu-id="3911d-129">Time series data is a continuous sequence of data points that typically consists of successive measurements made over a time interval.</span></span> <span data-ttu-id="3911d-130">Common examples of time series data include sensor data and application telemetry data.</span><span class="sxs-lookup"><span data-stu-id="3911d-130">Common examples of time series data include sensor data and application telemetry data.</span></span>

<span data-ttu-id="3911d-131">With Data Factory, you can process time series data in a batched fashion with activity runs.</span><span class="sxs-lookup"><span data-stu-id="3911d-131">With Data Factory, you can process time series data in a batched fashion with activity runs.</span></span> <span data-ttu-id="3911d-132">Typically, there is a recurring cadence at which input data arrives and output data needs to be produced.</span><span class="sxs-lookup"><span data-stu-id="3911d-132">Typically, there is a recurring cadence at which input data arrives and output data needs to be produced.</span></span> <span data-ttu-id="3911d-133">This cadence is modeled by specifying **availability** in the dataset as follows:</span><span class="sxs-lookup"><span data-stu-id="3911d-133">This cadence is modeled by specifying **availability** in the dataset as follows:</span></span>

```json
"availability": {
  "frequency": "Hour",
  "interval": 1
},
```

<span data-ttu-id="3911d-134">Each unit of data consumed and produced by an activity run is called a data slice.</span><span class="sxs-lookup"><span data-stu-id="3911d-134">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="3911d-135">The following diagram shows an example of an activity with one input dataset and one output dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-135">The following diagram shows an example of an activity with one input dataset and one output dataset.</span></span> <span data-ttu-id="3911d-136">These datasets have **availability** set to an hourly frequency.</span><span class="sxs-lookup"><span data-stu-id="3911d-136">These datasets have **availability** set to an hourly frequency.</span></span>

![Availability scheduler](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="3911d-138">The preceding diagram shows the hourly data slices for the input and output dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-138">The preceding diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="3911d-139">The diagram shows three input slices that are ready for processing.</span><span class="sxs-lookup"><span data-stu-id="3911d-139">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="3911d-140">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span><span class="sxs-lookup"><span data-stu-id="3911d-140">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span>

<span data-ttu-id="3911d-141">You can access the time interval associated with the current slice being produced in the dataset JSON with variables [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="3911d-141">You can access the time interval associated with the current slice being produced in the dataset JSON with variables [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span>

<span data-ttu-id="3911d-142">Currently, Data Factory requires that the schedule specified in the activity exactly matches the schedule specified in **availability** of the output dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-142">Currently, Data Factory requires that the schedule specified in the activity exactly matches the schedule specified in **availability** of the output dataset.</span></span> <span data-ttu-id="3911d-143">Therefore, **WindowStart**, **WindowEnd**, **SliceStart**, and **SliceEnd** always map to the same time period and a single output slice.</span><span class="sxs-lookup"><span data-stu-id="3911d-143">Therefore, **WindowStart**, **WindowEnd**, **SliceStart**, and **SliceEnd** always map to the same time period and a single output slice.</span></span>

<span data-ttu-id="3911d-144">For more information on different properties available for the availability section, see [Creating datasets](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="3911d-144">For more information on different properties available for the availability section, see [Creating datasets](data-factory-create-datasets.md).</span></span>

## <a name="move-data-from-sql-database-to-blob-storage"></a><span data-ttu-id="3911d-145">Move data from SQL Database to Blob storage</span><span class="sxs-lookup"><span data-stu-id="3911d-145">Move data from SQL Database to Blob storage</span></span>
<span data-ttu-id="3911d-146">Let’s put some things together and in action by creating a pipeline that copies data from an Azure SQL Database table to Azure Blob storage every hour.</span><span class="sxs-lookup"><span data-stu-id="3911d-146">Let’s put some things together and in action by creating a pipeline that copies data from an Azure SQL Database table to Azure Blob storage every hour.</span></span>

<span data-ttu-id="3911d-147">**Input: Azure SQL Database dataset**</span><span class="sxs-lookup"><span data-stu-id="3911d-147">**Input: Azure SQL Database dataset**</span></span>

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

<span data-ttu-id="3911d-148">**Frequency** is set to **Hour** and **interval** is set to **1** in the availability section.</span><span class="sxs-lookup"><span data-stu-id="3911d-148">**Frequency** is set to **Hour** and **interval** is set to **1** in the availability section.</span></span>

<span data-ttu-id="3911d-149">**Output: Azure Blob storage dataset**</span><span class="sxs-lookup"><span data-stu-id="3911d-149">**Output: Azure Blob storage dataset**</span></span>

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
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "%M"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "%d"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "%H"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="3911d-150">**Frequency** is set to **Hour** and **interval** is set to **1** in the availability section.</span><span class="sxs-lookup"><span data-stu-id="3911d-150">**Frequency** is set to **Hour** and **interval** is set to **1** in the availability section.</span></span>

<span data-ttu-id="3911d-151">**Activity: Copy Activity**</span><span class="sxs-lookup"><span data-stu-id="3911d-151">**Activity: Copy Activity**</span></span>

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
        "start": "2015-01-01T08:00:00Z",
        "end": "2015-01-01T11:00:00Z"
    }
}
```

<span data-ttu-id="3911d-152">The sample shows the activity schedule and dataset availability sections set to an hourly frequency.</span><span class="sxs-lookup"><span data-stu-id="3911d-152">The sample shows the activity schedule and dataset availability sections set to an hourly frequency.</span></span> <span data-ttu-id="3911d-153">The sample shows how you can use **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="3911d-153">The sample shows how you can use **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="3911d-154">The **folderPath** is parameterized to have a separate folder for every hour.</span><span class="sxs-lookup"><span data-stu-id="3911d-154">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>

<span data-ttu-id="3911d-155">When three of the slices between 8–11 AM execute, the data in Azure SQL Database is as follows:</span><span class="sxs-lookup"><span data-stu-id="3911d-155">When three of the slices between 8–11 AM execute, the data in Azure SQL Database is as follows:</span></span>

![Sample input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-scheduling-and-execution/sample-input-data.png)

<span data-ttu-id="3911d-157">After the pipeline deploys, the Azure blob is populated as follows:</span><span class="sxs-lookup"><span data-stu-id="3911d-157">After the pipeline deploys, the Azure blob is populated as follows:</span></span>

* <span data-ttu-id="3911d-158">File mypath/2015/1/1/8/Data.&lt;Guid&gt;.txt with data</span><span class="sxs-lookup"><span data-stu-id="3911d-158">File mypath/2015/1/1/8/Data.&lt;Guid&gt;.txt with data</span></span>
    ```  
    10002345,334,2,2015-01-01 08:24:00.3130000
    10002345,347,15,2015-01-01 08:24:00.6570000
    10991568,2,7,2015-01-01 08:56:34.5300000
    ```
  
  > [!NOTE]
  > <span data-ttu-id="3911d-159">&lt;Guid&gt; is replaced with an actual guid.</span><span class="sxs-lookup"><span data-stu-id="3911d-159">&lt;Guid&gt; is replaced with an actual guid.</span></span> <span data-ttu-id="3911d-160">Example file name: Data.bcde1348-7620-4f93-bb89-0eed3455890b.txt</span><span class="sxs-lookup"><span data-stu-id="3911d-160">Example file name: Data.bcde1348-7620-4f93-bb89-0eed3455890b.txt</span></span>
  > 
  > 
* <span data-ttu-id="3911d-161">File mypath/2015/1/1/9/Data.&lt;Guid&gt;.txt with data:</span><span class="sxs-lookup"><span data-stu-id="3911d-161">File mypath/2015/1/1/9/Data.&lt;Guid&gt;.txt with data:</span></span>

    ```json  
    10002345,334,1,2015-01-01 09:13:00.3900000
    24379245,569,23,2015-01-01 09:25:00.3130000
    16777799,21,115,2015-01-01 09:47:34.3130000
    ```
* <span data-ttu-id="3911d-162">File mypath/2015/1/1/10/Data.&lt;Guid&gt;.txt with no data.</span><span class="sxs-lookup"><span data-stu-id="3911d-162">File mypath/2015/1/1/10/Data.&lt;Guid&gt;.txt with no data.</span></span>

## <a name="active-period-for-pipeline"></a><span data-ttu-id="3911d-163">Active period for pipeline</span><span class="sxs-lookup"><span data-stu-id="3911d-163">Active period for pipeline</span></span>
<span data-ttu-id="3911d-164">[Creating pipelines](data-factory-create-pipelines.md) introduced the concept of an active period for a pipeline specified by setting the **start** and **end** properties.</span><span class="sxs-lookup"><span data-stu-id="3911d-164">[Creating pipelines](data-factory-create-pipelines.md) introduced the concept of an active period for a pipeline specified by setting the **start** and **end** properties.</span></span>

<span data-ttu-id="3911d-165">You can set the start date for the pipeline active period in the past.</span><span class="sxs-lookup"><span data-stu-id="3911d-165">You can set the start date for the pipeline active period in the past.</span></span> <span data-ttu-id="3911d-166">Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span><span class="sxs-lookup"><span data-stu-id="3911d-166">Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span>

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="3911d-167">Parallel processing of data slices</span><span class="sxs-lookup"><span data-stu-id="3911d-167">Parallel processing of data slices</span></span>
<span data-ttu-id="3911d-168">You can configure back-filled data slices to be run in parallel by setting the **concurrency** property in the policy section of the activity JSON.</span><span class="sxs-lookup"><span data-stu-id="3911d-168">You can configure back-filled data slices to be run in parallel by setting the **concurrency** property in the policy section of the activity JSON.</span></span> <span data-ttu-id="3911d-169">For more information on this property, see [Creating pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="3911d-169">For more information on this property, see [Creating pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="3911d-170">Rerun a failed data slice</span><span class="sxs-lookup"><span data-stu-id="3911d-170">Rerun a failed data slice</span></span>
<span data-ttu-id="3911d-171">You can monitor execution of slices in a rich, visual way.</span><span class="sxs-lookup"><span data-stu-id="3911d-171">You can monitor execution of slices in a rich, visual way.</span></span> <span data-ttu-id="3911d-172">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span><span class="sxs-lookup"><span data-stu-id="3911d-172">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="3911d-173">Consider the following example, which shows two activities.</span><span class="sxs-lookup"><span data-stu-id="3911d-173">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="3911d-174">Activity1 produces a time series dataset with slices as output that is consumed as input by Activity2 to produce the final output time series dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-174">Activity1 produces a time series dataset with slices as output that is consumed as input by Activity2 to produce the final output time series dataset.</span></span>

![Failed slice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="3911d-176">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span><span class="sxs-lookup"><span data-stu-id="3911d-176">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="3911d-177">Data Factory automatically tracks dependency for the time series dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-177">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="3911d-178">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span><span class="sxs-lookup"><span data-stu-id="3911d-178">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="3911d-179">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span><span class="sxs-lookup"><span data-stu-id="3911d-179">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="3911d-180">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span><span class="sxs-lookup"><span data-stu-id="3911d-180">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="3911d-181">For more details on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="3911d-181">For more details on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="3911d-182">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-182">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![Rerun failed slice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="run-activities-in-a-sequence"></a><span data-ttu-id="3911d-184">Run activities in a sequence</span><span class="sxs-lookup"><span data-stu-id="3911d-184">Run activities in a sequence</span></span>
<span data-ttu-id="3911d-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="3911d-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="3911d-186">The activities can be in the same pipeline or in different pipelines.</span><span class="sxs-lookup"><span data-stu-id="3911d-186">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="3911d-187">The second activity executes only when the first one finishes successfully.</span><span class="sxs-lookup"><span data-stu-id="3911d-187">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="3911d-188">For example, consider the following case:</span><span class="sxs-lookup"><span data-stu-id="3911d-188">For example, consider the following case:</span></span>

1. <span data-ttu-id="3911d-189">Pipeline P1 has Activity A1 that requires external input dataset D1, and produces output dataset D2.</span><span class="sxs-lookup"><span data-stu-id="3911d-189">Pipeline P1 has Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="3911d-190">Pipeline P2 has Activity A2 that requires input from dataset D2, and produces output dataset D3.</span><span class="sxs-lookup"><span data-stu-id="3911d-190">Pipeline P2 has Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="3911d-191">In this scenario, activities A1 and A2 are in different pipelines.</span><span class="sxs-lookup"><span data-stu-id="3911d-191">In this scenario, activities A1 and A2 are in different pipelines.</span></span> <span data-ttu-id="3911d-192">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span><span class="sxs-lookup"><span data-stu-id="3911d-192">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="3911d-193">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span><span class="sxs-lookup"><span data-stu-id="3911d-193">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="3911d-194">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span><span class="sxs-lookup"><span data-stu-id="3911d-194">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="3911d-195">The Diagram view would look like the following diagram:</span><span class="sxs-lookup"><span data-stu-id="3911d-195">The Diagram view would look like the following diagram:</span></span>

![Chaining activities in two pipelines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="3911d-197">As mentioned earlier, the activities can be in the same pipeline.</span><span class="sxs-lookup"><span data-stu-id="3911d-197">As mentioned earlier, the activities can be in the same pipeline.</span></span> <span data-ttu-id="3911d-198">The Diagram view with both activities in the same pipeline would look like the following diagram:</span><span class="sxs-lookup"><span data-stu-id="3911d-198">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![Chaining activities in the same pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

### <a name="copy-sequentially"></a><span data-ttu-id="3911d-200">Copy sequentially</span><span class="sxs-lookup"><span data-stu-id="3911d-200">Copy sequentially</span></span>
<span data-ttu-id="3911d-201">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span><span class="sxs-lookup"><span data-stu-id="3911d-201">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="3911d-202">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span><span class="sxs-lookup"><span data-stu-id="3911d-202">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="3911d-203">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="3911d-203">CopyActivity1</span></span>

<span data-ttu-id="3911d-204">Input: Dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-204">Input: Dataset.</span></span> <span data-ttu-id="3911d-205">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="3911d-205">Output: Dataset2.</span></span>

<span data-ttu-id="3911d-206">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="3911d-206">CopyActivity2</span></span>

<span data-ttu-id="3911d-207">Input: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="3911d-207">Input: Dataset2.</span></span>  <span data-ttu-id="3911d-208">Output: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="3911d-208">Output: Dataset3.</span></span>

<span data-ttu-id="3911d-209">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span><span class="sxs-lookup"><span data-stu-id="3911d-209">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="3911d-210">Here is the sample pipeline JSON:</span><span class="sxs-lookup"><span data-stu-id="3911d-210">Here is the sample pipeline JSON:</span></span>

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

<span data-ttu-id="3911d-211">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span><span class="sxs-lookup"><span data-stu-id="3911d-211">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="3911d-212">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span><span class="sxs-lookup"><span data-stu-id="3911d-212">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="3911d-213">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span><span class="sxs-lookup"><span data-stu-id="3911d-213">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="3911d-214">For example:</span><span class="sxs-lookup"><span data-stu-id="3911d-214">For example:</span></span>

<span data-ttu-id="3911d-215">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="3911d-215">CopyActivity1</span></span>

<span data-ttu-id="3911d-216">Input: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="3911d-216">Input: Dataset1.</span></span> <span data-ttu-id="3911d-217">Output: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="3911d-217">Output: Dataset2.</span></span>

<span data-ttu-id="3911d-218">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="3911d-218">CopyActivity2</span></span>

<span data-ttu-id="3911d-219">Inputs: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="3911d-219">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="3911d-220">Output: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="3911d-220">Output: Dataset4.</span></span>

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

<span data-ttu-id="3911d-221">Notice that in the example, two input datasets are specified for the second copy activity.</span><span class="sxs-lookup"><span data-stu-id="3911d-221">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="3911d-222">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span><span class="sxs-lookup"><span data-stu-id="3911d-222">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="3911d-223">CopyActivity2 would start only after the following conditions are met:</span><span class="sxs-lookup"><span data-stu-id="3911d-223">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="3911d-224">CopyActivity1 has successfully completed and Dataset2 is available.</span><span class="sxs-lookup"><span data-stu-id="3911d-224">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="3911d-225">This dataset is not used when copying data to Dataset4.</span><span class="sxs-lookup"><span data-stu-id="3911d-225">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="3911d-226">It only acts as a scheduling dependency for CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="3911d-226">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="3911d-227">Dataset3 is available.</span><span class="sxs-lookup"><span data-stu-id="3911d-227">Dataset3 is available.</span></span> <span data-ttu-id="3911d-228">This dataset represents the data that is copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="3911d-228">This dataset represents the data that is copied to the destination.</span></span>  

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="3911d-229">Model datasets with different frequencies</span><span class="sxs-lookup"><span data-stu-id="3911d-229">Model datasets with different frequencies</span></span>
<span data-ttu-id="3911d-230">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span><span class="sxs-lookup"><span data-stu-id="3911d-230">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="3911d-231">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span><span class="sxs-lookup"><span data-stu-id="3911d-231">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="3911d-232">Data Factory supports modeling these scenarios.</span><span class="sxs-lookup"><span data-stu-id="3911d-232">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="3911d-233">Sample 1: Produce a daily output report for input data that is available every hour</span><span class="sxs-lookup"><span data-stu-id="3911d-233">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="3911d-234">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="3911d-234">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="3911d-235">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="3911d-235">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="3911d-236">Here is how you can model this scenario with Data Factory:</span><span class="sxs-lookup"><span data-stu-id="3911d-236">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="3911d-237">**Input dataset**</span><span class="sxs-lookup"><span data-stu-id="3911d-237">**Input dataset**</span></span>

<span data-ttu-id="3911d-238">The hourly input files are dropped in the folder for the given day.</span><span class="sxs-lookup"><span data-stu-id="3911d-238">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="3911d-239">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="3911d-239">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "%M"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "%d"}}
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
<span data-ttu-id="3911d-240">**Output dataset**</span><span class="sxs-lookup"><span data-stu-id="3911d-240">**Output dataset**</span></span>

<span data-ttu-id="3911d-241">One output file is created every day in the day's folder.</span><span class="sxs-lookup"><span data-stu-id="3911d-241">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="3911d-242">Availability of output is set at **Day** (frequency: Day and interval: 1).</span><span class="sxs-lookup"><span data-stu-id="3911d-242">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "%M"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "%d"}}
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

<span data-ttu-id="3911d-243">**Activity: hive activity in a pipeline**</span><span class="sxs-lookup"><span data-stu-id="3911d-243">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="3911d-244">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="3911d-244">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="3911d-245">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span><span class="sxs-lookup"><span data-stu-id="3911d-245">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

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

<span data-ttu-id="3911d-246">The following diagram shows the scenario from a data-dependency point of view.</span><span class="sxs-lookup"><span data-stu-id="3911d-246">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![Data dependency](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="3911d-248">The output slice for every day depends on 24 hourly slices from an input dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-248">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="3911d-249">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span><span class="sxs-lookup"><span data-stu-id="3911d-249">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="3911d-250">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span><span class="sxs-lookup"><span data-stu-id="3911d-250">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="3911d-251">Sample 2: Specify dependency with expressions and Data Factory functions</span><span class="sxs-lookup"><span data-stu-id="3911d-251">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="3911d-252">Let’s consider another scenario.</span><span class="sxs-lookup"><span data-stu-id="3911d-252">Let’s consider another scenario.</span></span> <span data-ttu-id="3911d-253">Suppose you have a hive activity that processes two input datasets.</span><span class="sxs-lookup"><span data-stu-id="3911d-253">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="3911d-254">One of them has new data daily, but one of them gets new data every week.</span><span class="sxs-lookup"><span data-stu-id="3911d-254">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="3911d-255">Suppose you wanted to do a join across the two inputs and produce an output every day.</span><span class="sxs-lookup"><span data-stu-id="3911d-255">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="3911d-256">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span><span class="sxs-lookup"><span data-stu-id="3911d-256">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="3911d-257">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-257">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="3911d-258">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span><span class="sxs-lookup"><span data-stu-id="3911d-258">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="3911d-259">**Input1: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="3911d-259">**Input1: Azure blob**</span></span>

<span data-ttu-id="3911d-260">The first input is the Azure blob being updated daily.</span><span class="sxs-lookup"><span data-stu-id="3911d-260">The first input is the Azure blob being updated daily.</span></span>

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
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "%M"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "%d"}}
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

<span data-ttu-id="3911d-261">**Input2: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="3911d-261">**Input2: Azure blob**</span></span>

<span data-ttu-id="3911d-262">Input2 is the Azure blob being updated weekly.</span><span class="sxs-lookup"><span data-stu-id="3911d-262">Input2 is the Azure blob being updated weekly.</span></span>

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
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "%M"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "%d"}}
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

<span data-ttu-id="3911d-263">**Output: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="3911d-263">**Output: Azure blob**</span></span>

<span data-ttu-id="3911d-264">One output file is created every day in the folder for the day.</span><span class="sxs-lookup"><span data-stu-id="3911d-264">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="3911d-265">Availability of output is set to **day** (frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="3911d-265">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

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
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "%M"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "%d"}}
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

<span data-ttu-id="3911d-266">**Activity: hive activity in a pipeline**</span><span class="sxs-lookup"><span data-stu-id="3911d-266">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="3911d-267">The hive activity takes the two inputs and produces an output slice every day.</span><span class="sxs-lookup"><span data-stu-id="3911d-267">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="3911d-268">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span><span class="sxs-lookup"><span data-stu-id="3911d-268">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

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

## <a name="data-factory-functions-and-system-variables"></a><span data-ttu-id="3911d-269">Data Factory functions and system variables</span><span class="sxs-lookup"><span data-stu-id="3911d-269">Data Factory functions and system variables</span></span>
<span data-ttu-id="3911d-270">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span><span class="sxs-lookup"><span data-stu-id="3911d-270">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="data-dependency-deep-dive"></a><span data-ttu-id="3911d-271">Data dependency deep dive</span><span class="sxs-lookup"><span data-stu-id="3911d-271">Data dependency deep dive</span></span>
<span data-ttu-id="3911d-272">To generate a dataset slice by an activity run, Data Factory uses the following *dependency model* to determine the relationships between datasets consumed and produced by an activity.</span><span class="sxs-lookup"><span data-stu-id="3911d-272">To generate a dataset slice by an activity run, Data Factory uses the following *dependency model* to determine the relationships between datasets consumed and produced by an activity.</span></span>

<span data-ttu-id="3911d-273">The time range of the input datasets required to generate the output dataset slice is called the *dependency period*.</span><span class="sxs-lookup"><span data-stu-id="3911d-273">The time range of the input datasets required to generate the output dataset slice is called the *dependency period*.</span></span>

<span data-ttu-id="3911d-274">An activity run generates a dataset slice only after the data slices in input datasets within the dependency period are available.</span><span class="sxs-lookup"><span data-stu-id="3911d-274">An activity run generates a dataset slice only after the data slices in input datasets within the dependency period are available.</span></span> <span data-ttu-id="3911d-275">In other words, all the input slices comprising the dependency period must be in **Ready** state for the activity run to produce an output dataset slice.</span><span class="sxs-lookup"><span data-stu-id="3911d-275">In other words, all the input slices comprising the dependency period must be in **Ready** state for the activity run to produce an output dataset slice.</span></span>

<span data-ttu-id="3911d-276">To generate the dataset slice [**start**, **end**], a function must map the dataset slice to its dependency period.</span><span class="sxs-lookup"><span data-stu-id="3911d-276">To generate the dataset slice [**start**, **end**], a function must map the dataset slice to its dependency period.</span></span> <span data-ttu-id="3911d-277">This function is essentially a formula that converts the start and end of the dataset slice to the start and end of the dependency period.</span><span class="sxs-lookup"><span data-stu-id="3911d-277">This function is essentially a formula that converts the start and end of the dataset slice to the start and end of the dependency period.</span></span> <span data-ttu-id="3911d-278">More formally:</span><span class="sxs-lookup"><span data-stu-id="3911d-278">More formally:</span></span>

```
DatasetSlice = [start, end]
DependencyPeriod = [f(start, end), g(start, end)]
```

<span data-ttu-id="3911d-279">**F** and **g** are mapping functions that calculate the start and end of the dependency period for each activity input.</span><span class="sxs-lookup"><span data-stu-id="3911d-279">**F** and **g** are mapping functions that calculate the start and end of the dependency period for each activity input.</span></span>

<span data-ttu-id="3911d-280">As seen in samples, the dependency period is same as the period for the data slice that is produced.</span><span class="sxs-lookup"><span data-stu-id="3911d-280">As seen in samples, the dependency period is same as the period for the data slice that is produced.</span></span> <span data-ttu-id="3911d-281">In these cases, Data Factory automatically computes the input slices that fall in the dependency period.</span><span class="sxs-lookup"><span data-stu-id="3911d-281">In these cases, Data Factory automatically computes the input slices that fall in the dependency period.</span></span>  

<span data-ttu-id="3911d-282">For example, in the aggregation sample where output is produced daily and input data is available every hour, the data slice period is 24 hours.</span><span class="sxs-lookup"><span data-stu-id="3911d-282">For example, in the aggregation sample where output is produced daily and input data is available every hour, the data slice period is 24 hours.</span></span> <span data-ttu-id="3911d-283">Data Factory finds the relevant hourly input slices for this time period and makes the output slice dependent on the input slice.</span><span class="sxs-lookup"><span data-stu-id="3911d-283">Data Factory finds the relevant hourly input slices for this time period and makes the output slice dependent on the input slice.</span></span>

<span data-ttu-id="3911d-284">You can also provide your own mapping for the dependency period as shown in the sample, where one of the inputs is weekly and the output slice is produced daily.</span><span class="sxs-lookup"><span data-stu-id="3911d-284">You can also provide your own mapping for the dependency period as shown in the sample, where one of the inputs is weekly and the output slice is produced daily.</span></span>

## <a name="data-dependency-and-validation"></a><span data-ttu-id="3911d-285">Data dependency and validation</span><span class="sxs-lookup"><span data-stu-id="3911d-285">Data dependency and validation</span></span>
<span data-ttu-id="3911d-286">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span><span class="sxs-lookup"><span data-stu-id="3911d-286">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="3911d-287">See [Creating datasets](data-factory-create-datasets.md) for details.</span><span class="sxs-lookup"><span data-stu-id="3911d-287">See [Creating datasets](data-factory-create-datasets.md) for details.</span></span>

<span data-ttu-id="3911d-288">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span><span class="sxs-lookup"><span data-stu-id="3911d-288">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="3911d-289">After the slices are validated, the slice status changes to **Ready**.</span><span class="sxs-lookup"><span data-stu-id="3911d-289">After the slices are validated, the slice status changes to **Ready**.</span></span>

<span data-ttu-id="3911d-290">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span><span class="sxs-lookup"><span data-stu-id="3911d-290">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span>

<span data-ttu-id="3911d-291">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3911d-291">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

## <a name="external-data"></a><span data-ttu-id="3911d-292">External data</span><span class="sxs-lookup"><span data-stu-id="3911d-292">External data</span></span>
<span data-ttu-id="3911d-293">A dataset can be marked as external (as shown in the following JSON snippet), implying it was not generated with Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3911d-293">A dataset can be marked as external (as shown in the following JSON snippet), implying it was not generated with Data Factory.</span></span> <span data-ttu-id="3911d-294">In such a case, the Dataset policy can have an additional set of parameters describing validation and retry policy for the dataset.</span><span class="sxs-lookup"><span data-stu-id="3911d-294">In such a case, the Dataset policy can have an additional set of parameters describing validation and retry policy for the dataset.</span></span> <span data-ttu-id="3911d-295">See [Creating pipelines](data-factory-create-pipelines.md) for a description of all the properties.</span><span class="sxs-lookup"><span data-stu-id="3911d-295">See [Creating pipelines](data-factory-create-pipelines.md) for a description of all the properties.</span></span>

<span data-ttu-id="3911d-296">Similar to datasets that are produced by Data Factory, the data slices for external data need to be ready before dependent slices can be processed.</span><span class="sxs-lookup"><span data-stu-id="3911d-296">Similar to datasets that are produced by Data Factory, the data slices for external data need to be ready before dependent slices can be processed.</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties":
    {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1     
        },
        "external": true,
        "policy":
        {
            "externalData":
            {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }  
    }
}
```
## <a name="onetime-pipeline"></a><span data-ttu-id="3911d-297">Onetime pipeline</span><span class="sxs-lookup"><span data-stu-id="3911d-297">Onetime pipeline</span></span>
<span data-ttu-id="3911d-298">You can create and schedule a pipeline to run periodically (for example: hourly or daily) within the start and end times you specify in the pipeline definition.</span><span class="sxs-lookup"><span data-stu-id="3911d-298">You can create and schedule a pipeline to run periodically (for example: hourly or daily) within the start and end times you specify in the pipeline definition.</span></span> <span data-ttu-id="3911d-299">See [Scheduling activities](#scheduling-and-execution) for details.</span><span class="sxs-lookup"><span data-stu-id="3911d-299">See [Scheduling activities](#scheduling-and-execution) for details.</span></span> <span data-ttu-id="3911d-300">You can also create a pipeline that runs only once.</span><span class="sxs-lookup"><span data-stu-id="3911d-300">You can also create a pipeline that runs only once.</span></span> <span data-ttu-id="3911d-301">To do so, you set the **pipelineMode** property in the pipeline definition to **onetime** as shown in the following JSON sample.</span><span class="sxs-lookup"><span data-stu-id="3911d-301">To do so, you set the **pipelineMode** property in the pipeline definition to **onetime** as shown in the following JSON sample.</span></span> <span data-ttu-id="3911d-302">The default value for this property is **scheduled**.</span><span class="sxs-lookup"><span data-stu-id="3911d-302">The default value for this property is **scheduled**.</span></span>

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

<span data-ttu-id="3911d-303">Note the following:</span><span class="sxs-lookup"><span data-stu-id="3911d-303">Note the following:</span></span>

* <span data-ttu-id="3911d-304">**Start** and **end** times for the pipeline are not specified.</span><span class="sxs-lookup"><span data-stu-id="3911d-304">**Start** and **end** times for the pipeline are not specified.</span></span>
* <span data-ttu-id="3911d-305">**Availability** of input and output datasets is specified (**frequency** and **interval**), even though Data Factory does not use the values.</span><span class="sxs-lookup"><span data-stu-id="3911d-305">**Availability** of input and output datasets is specified (**frequency** and **interval**), even though Data Factory does not use the values.</span></span>  
* <span data-ttu-id="3911d-306">Diagram view does not show one-time pipelines.</span><span class="sxs-lookup"><span data-stu-id="3911d-306">Diagram view does not show one-time pipelines.</span></span> <span data-ttu-id="3911d-307">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="3911d-307">This behavior is by design.</span></span>
* <span data-ttu-id="3911d-308">One-time pipelines cannot be updated.</span><span class="sxs-lookup"><span data-stu-id="3911d-308">One-time pipelines cannot be updated.</span></span> <span data-ttu-id="3911d-309">You can clone a one-time pipeline, rename it, update properties, and deploy it to create another one.</span><span class="sxs-lookup"><span data-stu-id="3911d-309">You can clone a one-time pipeline, rename it, update properties, and deploy it to create another one.</span></span>









