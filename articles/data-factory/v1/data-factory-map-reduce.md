---
title: Invoke MapReduce Program from Azure Data Factory
description: Learn how to process data by running MapReduce programs on an Azure HDInsight cluster from an Azure data factory.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: edbef08eaa100248368d7f0b23171f15b52ec56a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869231"
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="50ffc-103">Invoke MapReduce Programs from Data Factory</span><span class="sxs-lookup"><span data-stu-id="50ffc-103">Invoke MapReduce Programs from Data Factory</span></span>
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
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [transform data using MapReduce activity in Data Factory](../transform-data-using-hadoop-map-reduce.md).


<span data-ttu-id="50ffc-116">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="50ffc-116">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="50ffc-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="50ffc-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.  

## <a name="introduction"></a><span data-ttu-id="50ffc-119">Introduction</span><span class="sxs-lookup"><span data-stu-id="50ffc-119">Introduction</span></span>
<span data-ttu-id="50ffc-120">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span><span class="sxs-lookup"><span data-stu-id="50ffc-120">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="50ffc-121">It contains a sequence of activities where each activity performs a specific processing operation.</span><span class="sxs-lookup"><span data-stu-id="50ffc-121">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="50ffc-122">This article describes using the HDInsight MapReduce Activity.</span><span class="sxs-lookup"><span data-stu-id="50ffc-122">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="50ffc-123">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span><span class="sxs-lookup"><span data-stu-id="50ffc-123">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="50ffc-124">JSON for HDInsight MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="50ffc-124">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="50ffc-125">In the JSON definition for the HDInsight Activity:</span><span class="sxs-lookup"><span data-stu-id="50ffc-125">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="50ffc-126">Set the **type** of the **activity** to **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="50ffc-126">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="50ffc-127">Specify the name of the class for **className** property.</span><span class="sxs-lookup"><span data-stu-id="50ffc-127">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="50ffc-128">Specify the path to the JAR file including the file name for **jarFilePath** property.</span><span class="sxs-lookup"><span data-stu-id="50ffc-128">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="50ffc-129">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span><span class="sxs-lookup"><span data-stu-id="50ffc-129">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="50ffc-130">Specify any arguments for the MapReduce program in the **arguments** section.</span><span class="sxs-lookup"><span data-stu-id="50ffc-130">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="50ffc-131">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span><span class="sxs-lookup"><span data-stu-id="50ffc-131">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="50ffc-132">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span><span class="sxs-lookup"><span data-stu-id="50ffc-132">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
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
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="50ffc-133">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="50ffc-133">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="50ffc-134">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span><span class="sxs-lookup"><span data-stu-id="50ffc-134">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="50ffc-135">Sample on GitHub</span><span class="sxs-lookup"><span data-stu-id="50ffc-135">Sample on GitHub</span></span>
<span data-ttu-id="50ffc-136">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="50ffc-136">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="50ffc-137">Running the Word Count program</span><span class="sxs-lookup"><span data-stu-id="50ffc-137">Running the Word Count program</span></span>
<span data-ttu-id="50ffc-138">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="50ffc-138">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="50ffc-139">Linked Services</span><span class="sxs-lookup"><span data-stu-id="50ffc-139">Linked Services</span></span>
<span data-ttu-id="50ffc-140">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="50ffc-140">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="50ffc-141">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="50ffc-141">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="50ffc-142">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="50ffc-142">Azure Storage linked service</span></span>

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="50ffc-143">Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="50ffc-143">Azure HDInsight linked service</span></span>
<span data-ttu-id="50ffc-144">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="50ffc-144">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="50ffc-145">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span><span class="sxs-lookup"><span data-stu-id="50ffc-145">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a><span data-ttu-id="50ffc-146">Datasets</span><span class="sxs-lookup"><span data-stu-id="50ffc-146">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="50ffc-147">Output dataset</span><span class="sxs-lookup"><span data-stu-id="50ffc-147">Output dataset</span></span>
<span data-ttu-id="50ffc-148">The pipeline in this example does not take any inputs.</span><span class="sxs-lookup"><span data-stu-id="50ffc-148">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="50ffc-149">You specify an output dataset for the HDInsight MapReduce Activity.</span><span class="sxs-lookup"><span data-stu-id="50ffc-149">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="50ffc-150">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span><span class="sxs-lookup"><span data-stu-id="50ffc-150">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="50ffc-151">Pipeline</span><span class="sxs-lookup"><span data-stu-id="50ffc-151">Pipeline</span></span>
<span data-ttu-id="50ffc-152">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="50ffc-152">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="50ffc-153">Some of the important properties in the JSON are:</span><span class="sxs-lookup"><span data-stu-id="50ffc-153">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="50ffc-154">Property</span><span class="sxs-lookup"><span data-stu-id="50ffc-154">Property</span></span> | <span data-ttu-id="50ffc-155">Notes</span><span class="sxs-lookup"><span data-stu-id="50ffc-155">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="50ffc-156">type</span><span class="sxs-lookup"><span data-stu-id="50ffc-156">type</span></span> |<span data-ttu-id="50ffc-157">The type must be set to **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="50ffc-157">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="50ffc-158">className</span><span class="sxs-lookup"><span data-stu-id="50ffc-158">className</span></span> |<span data-ttu-id="50ffc-159">Name of the class is: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="50ffc-159">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="50ffc-160">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="50ffc-160">jarFilePath</span></span> |<span data-ttu-id="50ffc-161">Path to the jar file containing the class.</span><span class="sxs-lookup"><span data-stu-id="50ffc-161">Path to the jar file containing the class.</span></span> <span data-ttu-id="50ffc-162">If you copy/paste the following code, don't forget to change the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="50ffc-162">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="50ffc-163">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="50ffc-163">jarLinkedService</span></span> |<span data-ttu-id="50ffc-164">Azure Storage linked service that contains the jar file.</span><span class="sxs-lookup"><span data-stu-id="50ffc-164">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="50ffc-165">This linked service refers to the storage that is associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="50ffc-165">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="50ffc-166">arguments</span><span class="sxs-lookup"><span data-stu-id="50ffc-166">arguments</span></span> |<span data-ttu-id="50ffc-167">The wordcount program takes two arguments, an input and an output.</span><span class="sxs-lookup"><span data-stu-id="50ffc-167">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="50ffc-168">The input file is the davinci.txt file.</span><span class="sxs-lookup"><span data-stu-id="50ffc-168">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="50ffc-169">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="50ffc-169">frequency/interval</span></span> |<span data-ttu-id="50ffc-170">The values for these properties match the output dataset.</span><span class="sxs-lookup"><span data-stu-id="50ffc-170">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="50ffc-171">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="50ffc-171">linkedServiceName</span></span> |<span data-ttu-id="50ffc-172">refers to the HDInsight linked service you had created earlier.</span><span class="sxs-lookup"><span data-stu-id="50ffc-172">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a><span data-ttu-id="50ffc-173">Run Spark programs</span><span class="sxs-lookup"><span data-stu-id="50ffc-173">Run Spark programs</span></span>
<span data-ttu-id="50ffc-174">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="50ffc-174">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="50ffc-175">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span><span class="sxs-lookup"><span data-stu-id="50ffc-175">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="50ffc-176">See Also</span><span class="sxs-lookup"><span data-stu-id="50ffc-176">See Also</span></span>
* [<span data-ttu-id="50ffc-177">Hive Activity</span><span class="sxs-lookup"><span data-stu-id="50ffc-177">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="50ffc-178">Pig Activity</span><span class="sxs-lookup"><span data-stu-id="50ffc-178">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="50ffc-179">Hadoop Streaming Activity</span><span class="sxs-lookup"><span data-stu-id="50ffc-179">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="50ffc-180">Invoke Spark programs</span><span class="sxs-lookup"><span data-stu-id="50ffc-180">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="50ffc-181">Invoke R scripts</span><span class="sxs-lookup"><span data-stu-id="50ffc-181">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

