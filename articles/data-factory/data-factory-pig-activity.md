---
title: Transform data using Pig Activity in Azure Data Factory | Microsoft Docs
description: Learn how you can use the Pig Activity in an Azure data factory to run Pig scripts on an on-demand/your own HDInsight cluster.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: shlo
ms.openlocfilehash: 3c04cee00b7dc7c8833daf21cdbca11a065e9dae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540643"
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="03773-103">Transform data using Pig Activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="03773-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive Activity](data-factory-hive-activity.md) 
> * [Pig Activity](data-factory-pig-activity.md)
> * [MapReduce Activity](data-factory-map-reduce.md)
> * [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md)
> * [Spark Activity](data-factory-spark.md)
> * [Machine Learning Batch Execution Activity](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Update Resource Activity](data-factory-azure-ml-update-resource-activity.md)
> * [Stored Procedure Activity](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md)
> * [.NET Custom Activity](data-factory-use-custom-activities.md)

<span data-ttu-id="03773-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="03773-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="03773-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="03773-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

## <a name="syntax"></a><span data-ttu-id="03773-116">Syntax</span><span class="sxs-lookup"><span data-stu-id="03773-116">Syntax</span></span>

```JSON
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
## <a name="syntax-details"></a><span data-ttu-id="03773-117">Syntax details</span><span class="sxs-lookup"><span data-stu-id="03773-117">Syntax details</span></span>
| <span data-ttu-id="03773-118">Property</span><span class="sxs-lookup"><span data-stu-id="03773-118">Property</span></span> | <span data-ttu-id="03773-119">Description</span><span class="sxs-lookup"><span data-stu-id="03773-119">Description</span></span> | <span data-ttu-id="03773-120">Required</span><span class="sxs-lookup"><span data-stu-id="03773-120">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03773-121">name</span><span class="sxs-lookup"><span data-stu-id="03773-121">name</span></span> |<span data-ttu-id="03773-122">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="03773-122">Name of the activity</span></span> |<span data-ttu-id="03773-123">Yes</span><span class="sxs-lookup"><span data-stu-id="03773-123">Yes</span></span> |
| <span data-ttu-id="03773-124">description</span><span class="sxs-lookup"><span data-stu-id="03773-124">description</span></span> |<span data-ttu-id="03773-125">Text describing what the activity is used for</span><span class="sxs-lookup"><span data-stu-id="03773-125">Text describing what the activity is used for</span></span> |<span data-ttu-id="03773-126">No</span><span class="sxs-lookup"><span data-stu-id="03773-126">No</span></span> |
| <span data-ttu-id="03773-127">type</span><span class="sxs-lookup"><span data-stu-id="03773-127">type</span></span> |<span data-ttu-id="03773-128">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="03773-128">HDinsightPig</span></span> |<span data-ttu-id="03773-129">Yes</span><span class="sxs-lookup"><span data-stu-id="03773-129">Yes</span></span> |
| <span data-ttu-id="03773-130">inputs</span><span class="sxs-lookup"><span data-stu-id="03773-130">inputs</span></span> |<span data-ttu-id="03773-131">One or more inputs consumed by the Pig activity</span><span class="sxs-lookup"><span data-stu-id="03773-131">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="03773-132">No</span><span class="sxs-lookup"><span data-stu-id="03773-132">No</span></span> |
| <span data-ttu-id="03773-133">outputs</span><span class="sxs-lookup"><span data-stu-id="03773-133">outputs</span></span> |<span data-ttu-id="03773-134">One or more outputs produced by the Pig activity</span><span class="sxs-lookup"><span data-stu-id="03773-134">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="03773-135">Yes</span><span class="sxs-lookup"><span data-stu-id="03773-135">Yes</span></span> |
| <span data-ttu-id="03773-136">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="03773-136">linkedServiceName</span></span> |<span data-ttu-id="03773-137">Reference to the HDInsight cluster registered as a linked service in Data Factory</span><span class="sxs-lookup"><span data-stu-id="03773-137">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="03773-138">Yes</span><span class="sxs-lookup"><span data-stu-id="03773-138">Yes</span></span> |
| <span data-ttu-id="03773-139">script</span><span class="sxs-lookup"><span data-stu-id="03773-139">script</span></span> |<span data-ttu-id="03773-140">Specify the Pig script inline</span><span class="sxs-lookup"><span data-stu-id="03773-140">Specify the Pig script inline</span></span> |<span data-ttu-id="03773-141">No</span><span class="sxs-lookup"><span data-stu-id="03773-141">No</span></span> |
| <span data-ttu-id="03773-142">script path</span><span class="sxs-lookup"><span data-stu-id="03773-142">script path</span></span> |<span data-ttu-id="03773-143">Store the Pig script in an Azure blob storage and provide the path to the file.</span><span class="sxs-lookup"><span data-stu-id="03773-143">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="03773-144">Use 'script' or 'scriptPath' property.</span><span class="sxs-lookup"><span data-stu-id="03773-144">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="03773-145">Both cannot be used together.</span><span class="sxs-lookup"><span data-stu-id="03773-145">Both cannot be used together.</span></span> <span data-ttu-id="03773-146">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="03773-146">The file name is case-sensitive.</span></span> |<span data-ttu-id="03773-147">No</span><span class="sxs-lookup"><span data-stu-id="03773-147">No</span></span> |
| <span data-ttu-id="03773-148">defines</span><span class="sxs-lookup"><span data-stu-id="03773-148">defines</span></span> |<span data-ttu-id="03773-149">Specify parameters as key/value pairs for referencing within the Pig script</span><span class="sxs-lookup"><span data-stu-id="03773-149">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="03773-150">No</span><span class="sxs-lookup"><span data-stu-id="03773-150">No</span></span> |

## <a name="example"></a><span data-ttu-id="03773-151">Example</span><span class="sxs-lookup"><span data-stu-id="03773-151">Example</span></span>
<span data-ttu-id="03773-152">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span><span class="sxs-lookup"><span data-stu-id="03773-152">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="03773-153">The following sample game log is a comma (,) separated file.</span><span class="sxs-lookup"><span data-stu-id="03773-153">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="03773-154">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span><span class="sxs-lookup"><span data-stu-id="03773-154">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="03773-155">The **Pig script** to process this data:</span><span class="sxs-lookup"><span data-stu-id="03773-155">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="03773-156">To execute this Pig script in a Data Factory pipeline, do the following:</span><span class="sxs-lookup"><span data-stu-id="03773-156">To execute this Pig script in a Data Factory pipeline, do the following:</span></span>

1. <span data-ttu-id="03773-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="03773-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="03773-158">Let’s call this linked service **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="03773-158">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="03773-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span><span class="sxs-lookup"><span data-stu-id="03773-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="03773-160">Let’s call this linked service **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="03773-160">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="03773-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span><span class="sxs-lookup"><span data-stu-id="03773-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="03773-162">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="03773-162">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="03773-163">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span><span class="sxs-lookup"><span data-stu-id="03773-163">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="03773-164">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="03773-164">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="03773-165">Refer to the linked service in the activity configuration.</span><span class="sxs-lookup"><span data-stu-id="03773-165">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="03773-166">Use \*\*scriptPath \*\*to specify the path to pig script file and **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="03773-166">Use \*\*scriptPath \*\*to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > You can also provide the Pig script inline in the activity definition by using the **script** property. However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues. The best practice is to follow step #4.
   > 
   > 
5. <span data-ttu-id="03773-170">Create the pipeline with the HDInsightPig activity.</span><span class="sxs-lookup"><span data-stu-id="03773-170">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="03773-171">This activity processes the input data by running Pig script on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="03773-171">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
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
6. <span data-ttu-id="03773-172">Deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="03773-172">Deploy the pipeline.</span></span> <span data-ttu-id="03773-173">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="03773-173">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="03773-174">Monitor the pipeline using the data factory monitoring and management views.</span><span class="sxs-lookup"><span data-stu-id="03773-174">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="03773-175">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="03773-175">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="03773-176">Specifying parameters for a Pig script</span><span class="sxs-lookup"><span data-stu-id="03773-176">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="03773-177">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span><span class="sxs-lookup"><span data-stu-id="03773-177">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="03773-178">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span><span class="sxs-lookup"><span data-stu-id="03773-178">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="03773-179">To use parameterized Pig script, do the following:</span><span class="sxs-lookup"><span data-stu-id="03773-179">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="03773-180">Define the parameters in **defines**.</span><span class="sxs-lookup"><span data-stu-id="03773-180">Define the parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0: %M}/dayno={0: %d}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:%M}/dayno={0:%d}/', SliceStart)"
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
* <span data-ttu-id="03773-181">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="03773-181">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="03773-182">See Also</span><span class="sxs-lookup"><span data-stu-id="03773-182">See Also</span></span>
* [<span data-ttu-id="03773-183">Hive Activity</span><span class="sxs-lookup"><span data-stu-id="03773-183">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="03773-184">MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="03773-184">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="03773-185">Hadoop Streaming Activity</span><span class="sxs-lookup"><span data-stu-id="03773-185">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="03773-186">Invoke Spark programs</span><span class="sxs-lookup"><span data-stu-id="03773-186">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="03773-187">Invoke R scripts</span><span class="sxs-lookup"><span data-stu-id="03773-187">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

