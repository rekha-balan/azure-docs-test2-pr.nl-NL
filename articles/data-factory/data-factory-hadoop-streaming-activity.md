---
title: Transform data using Hadoop Streaming Activity - Azure | Microsoft Docs
description: Learn how you can use the Hadoop Streaming Activity in an Azure data factory to transform data by running Hadoop Streaming programs on an on-demand/your own HDInsight cluster.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/24/2017
ms.author: shlo
ms.openlocfilehash: 2748838279462a493983c397454cbcf13b2a82e6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564620"
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="d67f4-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d67f4-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
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

<span data-ttu-id="d67f4-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="d67f4-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="d67f4-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span><span class="sxs-lookup"><span data-stu-id="d67f4-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="d67f4-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d67f4-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d67f4-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="d67f4-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

## <a name="json-sample"></a><span data-ttu-id="d67f4-118">JSON sample</span><span class="sxs-lookup"><span data-stu-id="d67f4-118">JSON sample</span></span>
<span data-ttu-id="d67f4-119">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="d67f4-119">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="d67f4-120">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span><span class="sxs-lookup"><span data-stu-id="d67f4-120">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="d67f4-121">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="d67f4-121">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

```JSON
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
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
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
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

<span data-ttu-id="d67f4-122">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="d67f4-122">Note the following points:</span></span>

1. <span data-ttu-id="d67f4-123">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span><span class="sxs-lookup"><span data-stu-id="d67f4-123">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="d67f4-124">Set the type of the activity to **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="d67f4-124">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="d67f4-125">For the **mapper** property, specify the name of mapper executable.</span><span class="sxs-lookup"><span data-stu-id="d67f4-125">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="d67f4-126">In the example, cat.exe is the mapper executable.</span><span class="sxs-lookup"><span data-stu-id="d67f4-126">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="d67f4-127">For the **reducer** property, specify the name of reducer executable.</span><span class="sxs-lookup"><span data-stu-id="d67f4-127">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="d67f4-128">In the example, wc.exe is the reducer executable.</span><span class="sxs-lookup"><span data-stu-id="d67f4-128">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="d67f4-129">For the **input** type property, specify the input file (including the location) for the mapper.</span><span class="sxs-lookup"><span data-stu-id="d67f4-129">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="d67f4-130">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span><span class="sxs-lookup"><span data-stu-id="d67f4-130">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="d67f4-131">For the **output** type property, specify the output file (including the location) for the reducer.</span><span class="sxs-lookup"><span data-stu-id="d67f4-131">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="d67f4-132">The output of the Hadoop Streaming job is written to the location specified for this property.</span><span class="sxs-lookup"><span data-stu-id="d67f4-132">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="d67f4-133">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span><span class="sxs-lookup"><span data-stu-id="d67f4-133">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="d67f4-134">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span><span class="sxs-lookup"><span data-stu-id="d67f4-134">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="d67f4-135">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span><span class="sxs-lookup"><span data-stu-id="d67f4-135">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="d67f4-136">For the **arguments** property, specify the arguments for the streaming job.</span><span class="sxs-lookup"><span data-stu-id="d67f4-136">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="d67f4-137">The **getDebugInfo** property is an optional element.</span><span class="sxs-lookup"><span data-stu-id="d67f4-137">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="d67f4-138">When it is set to Failure, the logs are downloaded only on failure.</span><span class="sxs-lookup"><span data-stu-id="d67f4-138">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="d67f4-139">When it is set to All, logs are always downloaded irrespective of the execution status.</span><span class="sxs-lookup"><span data-stu-id="d67f4-139">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property. This dataset is just a dummy dataset that is required to drive the pipeline schedule. You do not need to specify any input dataset for the activity for the **inputs** property.  
> 
> 

## <a name="example"></a><span data-ttu-id="d67f4-143">Example</span><span class="sxs-lookup"><span data-stu-id="d67f4-143">Example</span></span>
<span data-ttu-id="d67f4-144">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d67f4-144">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="d67f4-145">Linked services</span><span class="sxs-lookup"><span data-stu-id="d67f4-145">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="d67f4-146">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="d67f4-146">Azure Storage linked service</span></span>
<span data-ttu-id="d67f4-147">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="d67f4-147">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="d67f4-148">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d67f4-148">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="d67f4-149">Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="d67f4-149">Azure HDInsight linked service</span></span>
<span data-ttu-id="d67f4-150">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="d67f4-150">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="d67f4-151">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span><span class="sxs-lookup"><span data-stu-id="d67f4-151">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="d67f4-152">Datasets</span><span class="sxs-lookup"><span data-stu-id="d67f4-152">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="d67f4-153">Output dataset</span><span class="sxs-lookup"><span data-stu-id="d67f4-153">Output dataset</span></span>
<span data-ttu-id="d67f4-154">The pipeline in this example does not take any inputs.</span><span class="sxs-lookup"><span data-stu-id="d67f4-154">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="d67f4-155">You specify an output dataset for the HDInsight Streaming Activity.</span><span class="sxs-lookup"><span data-stu-id="d67f4-155">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="d67f4-156">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span><span class="sxs-lookup"><span data-stu-id="d67f4-156">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="d67f4-157">Pipeline</span><span class="sxs-lookup"><span data-stu-id="d67f4-157">Pipeline</span></span>
<span data-ttu-id="d67f4-158">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="d67f4-158">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="d67f4-159">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="d67f4-159">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="d67f4-160">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span><span class="sxs-lookup"><span data-stu-id="d67f4-160">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="d67f4-161">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="d67f4-161">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

```JSON
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
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
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
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a><span data-ttu-id="d67f4-162">See Also</span><span class="sxs-lookup"><span data-stu-id="d67f4-162">See Also</span></span>
* [<span data-ttu-id="d67f4-163">Hive Activity</span><span class="sxs-lookup"><span data-stu-id="d67f4-163">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="d67f4-164">Pig Activity</span><span class="sxs-lookup"><span data-stu-id="d67f4-164">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="d67f4-165">MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="d67f4-165">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="d67f4-166">Invoke Spark programs</span><span class="sxs-lookup"><span data-stu-id="d67f4-166">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="d67f4-167">Invoke R scripts</span><span class="sxs-lookup"><span data-stu-id="d67f4-167">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

