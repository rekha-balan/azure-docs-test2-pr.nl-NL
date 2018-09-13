---
title: Transform data using Hadoop MapReduce activity in Azure Data Factory | Microsoft Docs
description: Learn how to process data by running Hadoop MapReduce programs on an Azure HDInsight cluster from an Azure data factory.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/16/2018
ms.author: douglasl
ms.openlocfilehash: cb7009d0e7f31b2f503ac51d378fd117fff9f9b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866589"
---
# <a name="transform-data-using-hadoop-mapreduce-activity-in-azure-data-factory"></a><span data-ttu-id="82e9c-103">Transform data using Hadoop MapReduce activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="82e9c-103">Transform data using Hadoop MapReduce activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-map-reduce.md)
> * [Current version](transform-data-using-hadoop-map-reduce.md)

<span data-ttu-id="82e9c-106">The HDInsight MapReduce activity in a Data Factory [pipeline](concepts-pipelines-activities.md) invokes MapReduce program on [your own](compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)  HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="82e9c-106">The HDInsight MapReduce activity in a Data Factory [pipeline](concepts-pipelines-activities.md) invokes MapReduce program on [your own](compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)  HDInsight cluster.</span></span> <span data-ttu-id="82e9c-107">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="82e9c-107">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

<span data-ttu-id="82e9c-108">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](introduction.md) and do the tutorial: [Tutorial: transform data](tutorial-transform-data-spark-powershell.md) before reading this article.</span><span class="sxs-lookup"><span data-stu-id="82e9c-108">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](introduction.md) and do the tutorial: [Tutorial: transform data](tutorial-transform-data-spark-powershell.md) before reading this article.</span></span> 

<span data-ttu-id="82e9c-109">See [Pig](transform-data-using-hadoop-pig.md) and [Hive](transform-data-using-hadoop-hive.md) for details about running Pig/Hive scripts on a HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span><span class="sxs-lookup"><span data-stu-id="82e9c-109">See [Pig](transform-data-using-hadoop-pig.md) and [Hive](transform-data-using-hadoop-hive.md) for details about running Pig/Hive scripts on a HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="syntax"></a><span data-ttu-id="82e9c-110">Syntax</span><span class="sxs-lookup"><span data-stu-id="82e9c-110">Syntax</span></span>

```json
{
    "name": "Map Reduce Activity",
    "description": "Description",
    "type": "HDInsightMapReduce",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "className": "org.myorg.SampleClass",
        "jarLinkedService": {
            "referenceName": "MyAzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "jarFilePath": "MyAzureStorage/jars/sample.jar",
        "getDebugInfo": "Failure",
        "arguments": [
          "-SampleHadoopJobArgument1"
        ],
        "defines": {
          "param1": "param1Value"
        }
    }
}
```

## <a name="syntax-details"></a><span data-ttu-id="82e9c-111">Syntax details</span><span class="sxs-lookup"><span data-stu-id="82e9c-111">Syntax details</span></span>

| <span data-ttu-id="82e9c-112">Property</span><span class="sxs-lookup"><span data-stu-id="82e9c-112">Property</span></span>          | <span data-ttu-id="82e9c-113">Description</span><span class="sxs-lookup"><span data-stu-id="82e9c-113">Description</span></span>                              | <span data-ttu-id="82e9c-114">Required</span><span class="sxs-lookup"><span data-stu-id="82e9c-114">Required</span></span> |
| ----------------- | ---------------------------------------- | -------- |
| <span data-ttu-id="82e9c-115">name</span><span class="sxs-lookup"><span data-stu-id="82e9c-115">name</span></span>              | <span data-ttu-id="82e9c-116">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-116">Name of the activity</span></span>                     | <span data-ttu-id="82e9c-117">Yes</span><span class="sxs-lookup"><span data-stu-id="82e9c-117">Yes</span></span>      |
| <span data-ttu-id="82e9c-118">description</span><span class="sxs-lookup"><span data-stu-id="82e9c-118">description</span></span>       | <span data-ttu-id="82e9c-119">Text describing what the activity is used for</span><span class="sxs-lookup"><span data-stu-id="82e9c-119">Text describing what the activity is used for</span></span> | <span data-ttu-id="82e9c-120">No</span><span class="sxs-lookup"><span data-stu-id="82e9c-120">No</span></span>       |
| <span data-ttu-id="82e9c-121">type</span><span class="sxs-lookup"><span data-stu-id="82e9c-121">type</span></span>              | <span data-ttu-id="82e9c-122">For MapReduce Activity, the activity type is HDinsightMapReduce</span><span class="sxs-lookup"><span data-stu-id="82e9c-122">For MapReduce Activity, the activity type is HDinsightMapReduce</span></span> | <span data-ttu-id="82e9c-123">Yes</span><span class="sxs-lookup"><span data-stu-id="82e9c-123">Yes</span></span>      |
| <span data-ttu-id="82e9c-124">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="82e9c-124">linkedServiceName</span></span> | <span data-ttu-id="82e9c-125">Reference to the HDInsight cluster registered as a linked service in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="82e9c-125">Reference to the HDInsight cluster registered as a linked service in Data Factory.</span></span> <span data-ttu-id="82e9c-126">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="82e9c-126">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span> | <span data-ttu-id="82e9c-127">Yes</span><span class="sxs-lookup"><span data-stu-id="82e9c-127">Yes</span></span>      |
| <span data-ttu-id="82e9c-128">className</span><span class="sxs-lookup"><span data-stu-id="82e9c-128">className</span></span>         | <span data-ttu-id="82e9c-129">Name of the Class to be executed</span><span class="sxs-lookup"><span data-stu-id="82e9c-129">Name of the Class to be executed</span></span>         | <span data-ttu-id="82e9c-130">Yes</span><span class="sxs-lookup"><span data-stu-id="82e9c-130">Yes</span></span>      |
| <span data-ttu-id="82e9c-131">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="82e9c-131">jarLinkedService</span></span>  | <span data-ttu-id="82e9c-132">Reference to an Azure Storage Linked Service used to store the Jar files.</span><span class="sxs-lookup"><span data-stu-id="82e9c-132">Reference to an Azure Storage Linked Service used to store the Jar files.</span></span> <span data-ttu-id="82e9c-133">If you don't specify this Linked Service, the Azure Storage Linked Service defined in the HDInsight Linked Service is used.</span><span class="sxs-lookup"><span data-stu-id="82e9c-133">If you don't specify this Linked Service, the Azure Storage Linked Service defined in the HDInsight Linked Service is used.</span></span> | <span data-ttu-id="82e9c-134">No</span><span class="sxs-lookup"><span data-stu-id="82e9c-134">No</span></span>       |
| <span data-ttu-id="82e9c-135">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="82e9c-135">jarFilePath</span></span>       | <span data-ttu-id="82e9c-136">Provide the path to the Jar files stored in the Azure Storage referred by jarLinkedService.</span><span class="sxs-lookup"><span data-stu-id="82e9c-136">Provide the path to the Jar files stored in the Azure Storage referred by jarLinkedService.</span></span> <span data-ttu-id="82e9c-137">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="82e9c-137">The file name is case-sensitive.</span></span> | <span data-ttu-id="82e9c-138">Yes</span><span class="sxs-lookup"><span data-stu-id="82e9c-138">Yes</span></span>      |
| <span data-ttu-id="82e9c-139">jarlibs</span><span class="sxs-lookup"><span data-stu-id="82e9c-139">jarlibs</span></span>           | <span data-ttu-id="82e9c-140">String array of the path to the Jar library files referenced by the job stored in the Azure Storage defined in jarLinkedService.</span><span class="sxs-lookup"><span data-stu-id="82e9c-140">String array of the path to the Jar library files referenced by the job stored in the Azure Storage defined in jarLinkedService.</span></span> <span data-ttu-id="82e9c-141">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="82e9c-141">The file name is case-sensitive.</span></span> | <span data-ttu-id="82e9c-142">No</span><span class="sxs-lookup"><span data-stu-id="82e9c-142">No</span></span>       |
| <span data-ttu-id="82e9c-143">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="82e9c-143">getDebugInfo</span></span>      | <span data-ttu-id="82e9c-144">Specifies when the log files are copied to the Azure Storage used by HDInsight cluster (or) specified by jarLinkedService.</span><span class="sxs-lookup"><span data-stu-id="82e9c-144">Specifies when the log files are copied to the Azure Storage used by HDInsight cluster (or) specified by jarLinkedService.</span></span> <span data-ttu-id="82e9c-145">Allowed values: None, Always, or Failure.</span><span class="sxs-lookup"><span data-stu-id="82e9c-145">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="82e9c-146">Default value: None.</span><span class="sxs-lookup"><span data-stu-id="82e9c-146">Default value: None.</span></span> | <span data-ttu-id="82e9c-147">No</span><span class="sxs-lookup"><span data-stu-id="82e9c-147">No</span></span>       |
| <span data-ttu-id="82e9c-148">arguments</span><span class="sxs-lookup"><span data-stu-id="82e9c-148">arguments</span></span>         | <span data-ttu-id="82e9c-149">Specifies an array of arguments for a Hadoop job.</span><span class="sxs-lookup"><span data-stu-id="82e9c-149">Specifies an array of arguments for a Hadoop job.</span></span> <span data-ttu-id="82e9c-150">The arguments are passed as command-line arguments to each task.</span><span class="sxs-lookup"><span data-stu-id="82e9c-150">The arguments are passed as command-line arguments to each task.</span></span> | <span data-ttu-id="82e9c-151">No</span><span class="sxs-lookup"><span data-stu-id="82e9c-151">No</span></span>       |
| <span data-ttu-id="82e9c-152">defines</span><span class="sxs-lookup"><span data-stu-id="82e9c-152">defines</span></span>           | <span data-ttu-id="82e9c-153">Specify parameters as key/value pairs for referencing within the Hive script.</span><span class="sxs-lookup"><span data-stu-id="82e9c-153">Specify parameters as key/value pairs for referencing within the Hive script.</span></span> | <span data-ttu-id="82e9c-154">No</span><span class="sxs-lookup"><span data-stu-id="82e9c-154">No</span></span>       |



## <a name="example"></a><span data-ttu-id="82e9c-155">Example</span><span class="sxs-lookup"><span data-stu-id="82e9c-155">Example</span></span>
<span data-ttu-id="82e9c-156">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="82e9c-156">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="82e9c-157">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span><span class="sxs-lookup"><span data-stu-id="82e9c-157">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

```json   
{
    "name": "MapReduce Activity for Mahout",
    "description": "Custom MapReduce to generate Mahout result",
    "type": "HDInsightMapReduce",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
        "jarLinkedService": {
            "referenceName": "MyStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
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
    }
}
```
<span data-ttu-id="82e9c-158">You can specify any arguments for the MapReduce program in the **arguments** section.</span><span class="sxs-lookup"><span data-stu-id="82e9c-158">You can specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="82e9c-159">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span><span class="sxs-lookup"><span data-stu-id="82e9c-159">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="82e9c-160">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span><span class="sxs-lookup"><span data-stu-id="82e9c-160">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82e9c-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="82e9c-161">Next steps</span></span>
<span data-ttu-id="82e9c-162">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="82e9c-162">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="82e9c-163">U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-163">U-SQL activity</span></span>](transform-data-using-data-lake-analytics.md)
* [<span data-ttu-id="82e9c-164">Hive activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-164">Hive activity</span></span>](transform-data-using-hadoop-hive.md)
* [<span data-ttu-id="82e9c-165">Pig activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-165">Pig activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="82e9c-166">Hadoop Streaming activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-166">Hadoop Streaming activity</span></span>](transform-data-using-hadoop-streaming.md)
* [<span data-ttu-id="82e9c-167">Spark activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-167">Spark activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="82e9c-168">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-168">.NET custom activity</span></span>](transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="82e9c-169">Machine Learning Batch Execution activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-169">Machine Learning Batch Execution activity</span></span>](transform-data-using-machine-learning.md)
* [<span data-ttu-id="82e9c-170">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="82e9c-170">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)
