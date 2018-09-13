---
title: Transform data using Hive Activity - Azure | Microsoft Docs
description: Learn how you can use the Hive Activity in an Azure data factory to run Hive queries on an on-demand/your own HDInsight cluster.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: e8d3b83c8508ae5913975edcbf89f4e70a8b08be
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856984"
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="e4b1f-103">Transform data using Hive Activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e4b1f-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
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

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [transform data using Hive activity in Data Factory](../transform-data-using-hadoop-hive.md).

<span data-ttu-id="e4b1f-116">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-116">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e4b1f-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article. 

## <a name="syntax"></a><span data-ttu-id="e4b1f-119">Syntax</span><span class="sxs-lookup"><span data-stu-id="e4b1f-119">Syntax</span></span>

```JSON
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
## <a name="syntax-details"></a><span data-ttu-id="e4b1f-120">Syntax details</span><span class="sxs-lookup"><span data-stu-id="e4b1f-120">Syntax details</span></span>
| <span data-ttu-id="e4b1f-121">Property</span><span class="sxs-lookup"><span data-stu-id="e4b1f-121">Property</span></span> | <span data-ttu-id="e4b1f-122">Description</span><span class="sxs-lookup"><span data-stu-id="e4b1f-122">Description</span></span> | <span data-ttu-id="e4b1f-123">Required</span><span class="sxs-lookup"><span data-stu-id="e4b1f-123">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e4b1f-124">name</span><span class="sxs-lookup"><span data-stu-id="e4b1f-124">name</span></span> |<span data-ttu-id="e4b1f-125">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="e4b1f-125">Name of the activity</span></span> |<span data-ttu-id="e4b1f-126">Yes</span><span class="sxs-lookup"><span data-stu-id="e4b1f-126">Yes</span></span> |
| <span data-ttu-id="e4b1f-127">description</span><span class="sxs-lookup"><span data-stu-id="e4b1f-127">description</span></span> |<span data-ttu-id="e4b1f-128">Text describing what the activity is used for</span><span class="sxs-lookup"><span data-stu-id="e4b1f-128">Text describing what the activity is used for</span></span> |<span data-ttu-id="e4b1f-129">No</span><span class="sxs-lookup"><span data-stu-id="e4b1f-129">No</span></span> |
| <span data-ttu-id="e4b1f-130">type</span><span class="sxs-lookup"><span data-stu-id="e4b1f-130">type</span></span> |<span data-ttu-id="e4b1f-131">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="e4b1f-131">HDinsightHive</span></span> |<span data-ttu-id="e4b1f-132">Yes</span><span class="sxs-lookup"><span data-stu-id="e4b1f-132">Yes</span></span> |
| <span data-ttu-id="e4b1f-133">inputs</span><span class="sxs-lookup"><span data-stu-id="e4b1f-133">inputs</span></span> |<span data-ttu-id="e4b1f-134">Inputs consumed by the Hive activity</span><span class="sxs-lookup"><span data-stu-id="e4b1f-134">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="e4b1f-135">No</span><span class="sxs-lookup"><span data-stu-id="e4b1f-135">No</span></span> |
| <span data-ttu-id="e4b1f-136">outputs</span><span class="sxs-lookup"><span data-stu-id="e4b1f-136">outputs</span></span> |<span data-ttu-id="e4b1f-137">Outputs produced by the Hive activity</span><span class="sxs-lookup"><span data-stu-id="e4b1f-137">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="e4b1f-138">Yes</span><span class="sxs-lookup"><span data-stu-id="e4b1f-138">Yes</span></span> |
| <span data-ttu-id="e4b1f-139">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e4b1f-139">linkedServiceName</span></span> |<span data-ttu-id="e4b1f-140">Reference to the HDInsight cluster registered as a linked service in Data Factory</span><span class="sxs-lookup"><span data-stu-id="e4b1f-140">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="e4b1f-141">Yes</span><span class="sxs-lookup"><span data-stu-id="e4b1f-141">Yes</span></span> |
| <span data-ttu-id="e4b1f-142">script</span><span class="sxs-lookup"><span data-stu-id="e4b1f-142">script</span></span> |<span data-ttu-id="e4b1f-143">Specify the Hive script inline</span><span class="sxs-lookup"><span data-stu-id="e4b1f-143">Specify the Hive script inline</span></span> |<span data-ttu-id="e4b1f-144">No</span><span class="sxs-lookup"><span data-stu-id="e4b1f-144">No</span></span> |
| <span data-ttu-id="e4b1f-145">script path</span><span class="sxs-lookup"><span data-stu-id="e4b1f-145">script path</span></span> |<span data-ttu-id="e4b1f-146">Store the Hive script in an Azure blob storage and provide the path to the file.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-146">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="e4b1f-147">Use 'script' or 'scriptPath' property.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-147">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="e4b1f-148">Both cannot be used together.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-148">Both cannot be used together.</span></span> <span data-ttu-id="e4b1f-149">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-149">The file name is case-sensitive.</span></span> |<span data-ttu-id="e4b1f-150">No</span><span class="sxs-lookup"><span data-stu-id="e4b1f-150">No</span></span> |
| <span data-ttu-id="e4b1f-151">defines</span><span class="sxs-lookup"><span data-stu-id="e4b1f-151">defines</span></span> |<span data-ttu-id="e4b1f-152">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="e4b1f-152">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="e4b1f-153">No</span><span class="sxs-lookup"><span data-stu-id="e4b1f-153">No</span></span> |

## <a name="example"></a><span data-ttu-id="e4b1f-154">Example</span><span class="sxs-lookup"><span data-stu-id="e4b1f-154">Example</span></span>
<span data-ttu-id="e4b1f-155">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-155">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="e4b1f-156">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-156">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="e4b1f-157">The **Hive script** to process this data:</span><span class="sxs-lookup"><span data-stu-id="e4b1f-157">The **Hive script** to process this data:</span></span>

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

<span data-ttu-id="e4b1f-158">To execute this Hive script in a Data Factory pipeline, you need to do the following</span><span class="sxs-lookup"><span data-stu-id="e4b1f-158">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="e4b1f-159">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="e4b1f-159">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="e4b1f-160">Let’s call this linked service “HDInsightLinkedService”.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-160">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="e4b1f-161">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-161">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="e4b1f-162">Let’s call this linked service “StorageLinkedService”</span><span class="sxs-lookup"><span data-stu-id="e4b1f-162">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="e4b1f-163">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-163">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="e4b1f-164">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span><span class="sxs-lookup"><span data-stu-id="e4b1f-164">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="e4b1f-165">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-165">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="e4b1f-166">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-166">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="e4b1f-167">Use **scriptPath** to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-167">Use **scriptPath** to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > You can also provide the Hive script inline in the activity definition by using the **script** property. We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues. The best practice is to follow step #4.
   > 
   > 
5. <span data-ttu-id="e4b1f-171">Create a pipeline with the HDInsightHive activity.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-171">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="e4b1f-172">The activity processes/transforms the data.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-172">The activity processes/transforms the data.</span></span>

    ```JSON   
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
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. <span data-ttu-id="e4b1f-173">Deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-173">Deploy the pipeline.</span></span> <span data-ttu-id="e4b1f-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="e4b1f-175">Monitor the pipeline using the data factory monitoring and management views.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="e4b1f-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="e4b1f-177">Specifying parameters for a Hive script</span><span class="sxs-lookup"><span data-stu-id="e4b1f-177">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="e4b1f-178">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-178">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="e4b1f-179">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-179">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="e4b1f-180">To use parameterized Hive script, do the following</span><span class="sxs-lookup"><span data-stu-id="e4b1f-180">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="e4b1f-181">Define the parameters in **defines**.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-181">Define the parameters in **defines**.</span></span>

    ```JSON  
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
* <span data-ttu-id="e4b1f-182">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="e4b1f-182">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a><span data-ttu-id="e4b1f-183">See Also</span><span class="sxs-lookup"><span data-stu-id="e4b1f-183">See Also</span></span>
* [<span data-ttu-id="e4b1f-184">Pig Activity</span><span class="sxs-lookup"><span data-stu-id="e4b1f-184">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="e4b1f-185">MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="e4b1f-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="e4b1f-186">Hadoop Streaming Activity</span><span class="sxs-lookup"><span data-stu-id="e4b1f-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="e4b1f-187">Invoke Spark programs</span><span class="sxs-lookup"><span data-stu-id="e4b1f-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="e4b1f-188">Invoke R scripts</span><span class="sxs-lookup"><span data-stu-id="e4b1f-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

