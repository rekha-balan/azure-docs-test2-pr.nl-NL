---
title: Transform data using Spark activity in Azure Data Factory | Microsoft Docs
description: Learn how to transform data by running Spark programs from an Azure data factory pipeline using the Spark Activity.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/31/2018
ms.author: douglasl
ms.openlocfilehash: abe2fabc505f94f19d4b15a406fc59bf6d6e7ac1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864709"
---
# <a name="transform-data-using-spark-activity-in-azure-data-factory"></a><span data-ttu-id="ec036-103">Transform data using Spark activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ec036-103">Transform data using Spark activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-spark.md)
> * [Current version](transform-data-using-spark.md)

<span data-ttu-id="ec036-106">The Spark activity in a Data Factory [pipeline](concepts-pipelines-activities.md) executes a Spark program on [your own](compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)  HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ec036-106">The Spark activity in a Data Factory [pipeline](concepts-pipelines-activities.md) executes a Spark program on [your own](compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)  HDInsight cluster.</span></span> <span data-ttu-id="ec036-107">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="ec036-107">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span> <span data-ttu-id="ec036-108">When you use an on-demand Spark linked service, Data Factory automatically creates a Spark cluster for you just-in-time to process the data and then deletes the cluster once the processing is complete.</span><span class="sxs-lookup"><span data-stu-id="ec036-108">When you use an on-demand Spark linked service, Data Factory automatically creates a Spark cluster for you just-in-time to process the data and then deletes the cluster once the processing is complete.</span></span> 

> [!IMPORTANT]
> Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.

## <a name="spark-activity-properties"></a><span data-ttu-id="ec036-110">Spark activity properties</span><span class="sxs-lookup"><span data-stu-id="ec036-110">Spark activity properties</span></span>
<span data-ttu-id="ec036-111">Here is the sample JSON definition of a Spark Activity:</span><span class="sxs-lookup"><span data-stu-id="ec036-111">Here is the sample JSON definition of a Spark Activity:</span></span>    

```json
{
    "name": "Spark Activity",
    "description": "Description",
    "type": "HDInsightSpark",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "sparkJobLinkedService": {
            "referenceName": "MyAzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "rootPath": "adfspark\\pyFiles",
        "entryFilePath": "test.py",
        "sparkConfig": {
            "ConfigItem1": "Value"
        },
        "getDebugInfo": "Failure",
        "arguments": [
            "SampleHadoopJobArgument1"
        ]
    }
}
```

<span data-ttu-id="ec036-112">The following table describes the JSON properties used in the JSON definition:</span><span class="sxs-lookup"><span data-stu-id="ec036-112">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="ec036-113">Property</span><span class="sxs-lookup"><span data-stu-id="ec036-113">Property</span></span>              | <span data-ttu-id="ec036-114">Description</span><span class="sxs-lookup"><span data-stu-id="ec036-114">Description</span></span>                              | <span data-ttu-id="ec036-115">Required</span><span class="sxs-lookup"><span data-stu-id="ec036-115">Required</span></span> |
| --------------------- | ---------------------------------------- | -------- |
| <span data-ttu-id="ec036-116">name</span><span class="sxs-lookup"><span data-stu-id="ec036-116">name</span></span>                  | <span data-ttu-id="ec036-117">Name of the activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="ec036-117">Name of the activity in the pipeline.</span></span>    | <span data-ttu-id="ec036-118">Yes</span><span class="sxs-lookup"><span data-stu-id="ec036-118">Yes</span></span>      |
| <span data-ttu-id="ec036-119">description</span><span class="sxs-lookup"><span data-stu-id="ec036-119">description</span></span>           | <span data-ttu-id="ec036-120">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="ec036-120">Text describing what the activity does.</span></span>  | <span data-ttu-id="ec036-121">No</span><span class="sxs-lookup"><span data-stu-id="ec036-121">No</span></span>       |
| <span data-ttu-id="ec036-122">type</span><span class="sxs-lookup"><span data-stu-id="ec036-122">type</span></span>                  | <span data-ttu-id="ec036-123">For Spark Activity, the activity type is HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="ec036-123">For Spark Activity, the activity type is HDInsightSpark.</span></span> | <span data-ttu-id="ec036-124">Yes</span><span class="sxs-lookup"><span data-stu-id="ec036-124">Yes</span></span>      |
| <span data-ttu-id="ec036-125">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ec036-125">linkedServiceName</span></span>     | <span data-ttu-id="ec036-126">Name of the HDInsight Spark Linked Service on which the Spark program runs.</span><span class="sxs-lookup"><span data-stu-id="ec036-126">Name of the HDInsight Spark Linked Service on which the Spark program runs.</span></span> <span data-ttu-id="ec036-127">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="ec036-127">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span> | <span data-ttu-id="ec036-128">Yes</span><span class="sxs-lookup"><span data-stu-id="ec036-128">Yes</span></span>      |
| <span data-ttu-id="ec036-129">SparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="ec036-129">SparkJobLinkedService</span></span> | <span data-ttu-id="ec036-130">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span><span class="sxs-lookup"><span data-stu-id="ec036-130">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="ec036-131">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span><span class="sxs-lookup"><span data-stu-id="ec036-131">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> <span data-ttu-id="ec036-132">The value of this property can only be an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="ec036-132">The value of this property can only be an Azure Storage linked service.</span></span> | <span data-ttu-id="ec036-133">No</span><span class="sxs-lookup"><span data-stu-id="ec036-133">No</span></span>       |
| <span data-ttu-id="ec036-134">rootPath</span><span class="sxs-lookup"><span data-stu-id="ec036-134">rootPath</span></span>              | <span data-ttu-id="ec036-135">The Azure Blob container and folder that contains the Spark file.</span><span class="sxs-lookup"><span data-stu-id="ec036-135">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="ec036-136">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="ec036-136">The file name is case-sensitive.</span></span> <span data-ttu-id="ec036-137">Refer to folder structure section (next section) for details about the structure of this folder.</span><span class="sxs-lookup"><span data-stu-id="ec036-137">Refer to folder structure section (next section) for details about the structure of this folder.</span></span> | <span data-ttu-id="ec036-138">Yes</span><span class="sxs-lookup"><span data-stu-id="ec036-138">Yes</span></span>      |
| <span data-ttu-id="ec036-139">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="ec036-139">entryFilePath</span></span>         | <span data-ttu-id="ec036-140">Relative path to the root folder of the Spark code/package.</span><span class="sxs-lookup"><span data-stu-id="ec036-140">Relative path to the root folder of the Spark code/package.</span></span> <span data-ttu-id="ec036-141">The entry file must be either a Python file or a .jar file.</span><span class="sxs-lookup"><span data-stu-id="ec036-141">The entry file must be either a Python file or a .jar file.</span></span> | <span data-ttu-id="ec036-142">Yes</span><span class="sxs-lookup"><span data-stu-id="ec036-142">Yes</span></span>      |
| <span data-ttu-id="ec036-143">className</span><span class="sxs-lookup"><span data-stu-id="ec036-143">className</span></span>             | <span data-ttu-id="ec036-144">Application's Java/Spark main class</span><span class="sxs-lookup"><span data-stu-id="ec036-144">Application's Java/Spark main class</span></span>      | <span data-ttu-id="ec036-145">No</span><span class="sxs-lookup"><span data-stu-id="ec036-145">No</span></span>       |
| <span data-ttu-id="ec036-146">arguments</span><span class="sxs-lookup"><span data-stu-id="ec036-146">arguments</span></span>             | <span data-ttu-id="ec036-147">A list of command-line arguments to the Spark program.</span><span class="sxs-lookup"><span data-stu-id="ec036-147">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="ec036-148">No</span><span class="sxs-lookup"><span data-stu-id="ec036-148">No</span></span>       |
| <span data-ttu-id="ec036-149">proxyUser</span><span class="sxs-lookup"><span data-stu-id="ec036-149">proxyUser</span></span>             | <span data-ttu-id="ec036-150">The user account to impersonate to execute the Spark program</span><span class="sxs-lookup"><span data-stu-id="ec036-150">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="ec036-151">No</span><span class="sxs-lookup"><span data-stu-id="ec036-151">No</span></span>       |
| <span data-ttu-id="ec036-152">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="ec036-152">sparkConfig</span></span>           | <span data-ttu-id="ec036-153">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="ec036-153">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="ec036-154">No</span><span class="sxs-lookup"><span data-stu-id="ec036-154">No</span></span>       |
| <span data-ttu-id="ec036-155">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="ec036-155">getDebugInfo</span></span>          | <span data-ttu-id="ec036-156">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ec036-156">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="ec036-157">Allowed values: None, Always, or Failure.</span><span class="sxs-lookup"><span data-stu-id="ec036-157">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="ec036-158">Default value: None.</span><span class="sxs-lookup"><span data-stu-id="ec036-158">Default value: None.</span></span> | <span data-ttu-id="ec036-159">No</span><span class="sxs-lookup"><span data-stu-id="ec036-159">No</span></span>       |

## <a name="folder-structure"></a><span data-ttu-id="ec036-160">Folder structure</span><span class="sxs-lookup"><span data-stu-id="ec036-160">Folder structure</span></span>
<span data-ttu-id="ec036-161">Spark jobs are more extensible than Pig/Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="ec036-161">Spark jobs are more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="ec036-162">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span><span class="sxs-lookup"><span data-stu-id="ec036-162">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="ec036-163">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="ec036-163">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="ec036-164">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="ec036-164">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="ec036-165">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span><span class="sxs-lookup"><span data-stu-id="ec036-165">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="ec036-166">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="ec036-166">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="ec036-167">Path</span><span class="sxs-lookup"><span data-stu-id="ec036-167">Path</span></span>                  | <span data-ttu-id="ec036-168">Description</span><span class="sxs-lookup"><span data-stu-id="ec036-168">Description</span></span>                              | <span data-ttu-id="ec036-169">Required</span><span class="sxs-lookup"><span data-stu-id="ec036-169">Required</span></span> | <span data-ttu-id="ec036-170">Type</span><span class="sxs-lookup"><span data-stu-id="ec036-170">Type</span></span>   |
| --------------------- | ---------------------------------------- | -------- | ------ |
| <span data-ttu-id="ec036-171">`.` (root)</span><span class="sxs-lookup"><span data-stu-id="ec036-171">`.` (root)</span></span>            | <span data-ttu-id="ec036-172">The root path of the Spark job in the storage linked service</span><span class="sxs-lookup"><span data-stu-id="ec036-172">The root path of the Spark job in the storage linked service</span></span> | <span data-ttu-id="ec036-173">Yes</span><span class="sxs-lookup"><span data-stu-id="ec036-173">Yes</span></span>      | <span data-ttu-id="ec036-174">Folder</span><span class="sxs-lookup"><span data-stu-id="ec036-174">Folder</span></span> |
| <span data-ttu-id="ec036-175">&lt;user defined &gt;</span><span class="sxs-lookup"><span data-stu-id="ec036-175">&lt;user defined &gt;</span></span> | <span data-ttu-id="ec036-176">The path pointing to the entry file of the Spark job</span><span class="sxs-lookup"><span data-stu-id="ec036-176">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="ec036-177">Yes</span><span class="sxs-lookup"><span data-stu-id="ec036-177">Yes</span></span>      | <span data-ttu-id="ec036-178">File</span><span class="sxs-lookup"><span data-stu-id="ec036-178">File</span></span>   |
| <span data-ttu-id="ec036-179">./jars</span><span class="sxs-lookup"><span data-stu-id="ec036-179">./jars</span></span>                | <span data-ttu-id="ec036-180">All files under this folder are uploaded and placed on the java classpath of the cluster</span><span class="sxs-lookup"><span data-stu-id="ec036-180">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="ec036-181">No</span><span class="sxs-lookup"><span data-stu-id="ec036-181">No</span></span>       | <span data-ttu-id="ec036-182">Folder</span><span class="sxs-lookup"><span data-stu-id="ec036-182">Folder</span></span> |
| <span data-ttu-id="ec036-183">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="ec036-183">./pyFiles</span></span>             | <span data-ttu-id="ec036-184">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span><span class="sxs-lookup"><span data-stu-id="ec036-184">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="ec036-185">No</span><span class="sxs-lookup"><span data-stu-id="ec036-185">No</span></span>       | <span data-ttu-id="ec036-186">Folder</span><span class="sxs-lookup"><span data-stu-id="ec036-186">Folder</span></span> |
| <span data-ttu-id="ec036-187">./files</span><span class="sxs-lookup"><span data-stu-id="ec036-187">./files</span></span>               | <span data-ttu-id="ec036-188">All files under this folder are uploaded and placed on executor working directory</span><span class="sxs-lookup"><span data-stu-id="ec036-188">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="ec036-189">No</span><span class="sxs-lookup"><span data-stu-id="ec036-189">No</span></span>       | <span data-ttu-id="ec036-190">Folder</span><span class="sxs-lookup"><span data-stu-id="ec036-190">Folder</span></span> |
| <span data-ttu-id="ec036-191">./archives</span><span class="sxs-lookup"><span data-stu-id="ec036-191">./archives</span></span>            | <span data-ttu-id="ec036-192">All files under this folder are uncompressed</span><span class="sxs-lookup"><span data-stu-id="ec036-192">All files under this folder are uncompressed</span></span> | <span data-ttu-id="ec036-193">No</span><span class="sxs-lookup"><span data-stu-id="ec036-193">No</span></span>       | <span data-ttu-id="ec036-194">Folder</span><span class="sxs-lookup"><span data-stu-id="ec036-194">Folder</span></span> |
| <span data-ttu-id="ec036-195">./logs</span><span class="sxs-lookup"><span data-stu-id="ec036-195">./logs</span></span>                | <span data-ttu-id="ec036-196">The folder that contains logs from the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="ec036-196">The folder that contains logs from the Spark cluster.</span></span> | <span data-ttu-id="ec036-197">No</span><span class="sxs-lookup"><span data-stu-id="ec036-197">No</span></span>       | <span data-ttu-id="ec036-198">Folder</span><span class="sxs-lookup"><span data-stu-id="ec036-198">Folder</span></span> |

<span data-ttu-id="ec036-199">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span><span class="sxs-lookup"><span data-stu-id="ec036-199">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
## <a name="next-steps"></a><span data-ttu-id="ec036-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec036-200">Next steps</span></span>
<span data-ttu-id="ec036-201">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="ec036-201">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="ec036-202">U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="ec036-202">U-SQL activity</span></span>](transform-data-using-data-lake-analytics.md)
* [<span data-ttu-id="ec036-203">Hive activity</span><span class="sxs-lookup"><span data-stu-id="ec036-203">Hive activity</span></span>](transform-data-using-hadoop-hive.md)
* [<span data-ttu-id="ec036-204">Pig activity</span><span class="sxs-lookup"><span data-stu-id="ec036-204">Pig activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="ec036-205">MapReduce activity</span><span class="sxs-lookup"><span data-stu-id="ec036-205">MapReduce activity</span></span>](transform-data-using-hadoop-map-reduce.md)
* [<span data-ttu-id="ec036-206">Hadoop Streaming activity</span><span class="sxs-lookup"><span data-stu-id="ec036-206">Hadoop Streaming activity</span></span>](transform-data-using-hadoop-streaming.md)
* [<span data-ttu-id="ec036-207">Spark activity</span><span class="sxs-lookup"><span data-stu-id="ec036-207">Spark activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="ec036-208">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="ec036-208">.NET custom activity</span></span>](transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="ec036-209">Machine Learning Batch Execution activity</span><span class="sxs-lookup"><span data-stu-id="ec036-209">Machine Learning Batch Execution activity</span></span>](transform-data-using-machine-learning.md)
* [<span data-ttu-id="ec036-210">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="ec036-210">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)
