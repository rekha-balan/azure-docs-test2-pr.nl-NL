---
title: Transform data using Hadoop Streaming activity in Azure Data Factory | Microsoft Docs
description: Explains how to use Hadoop Streaming Activity in Azure Data Factory to transform data by running Hadoop Streaming programs on a Hadoop cluster.
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
ms.openlocfilehash: 4c2bf83fec3d8f961a84523365e4a98fe3bf7603
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855840"
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="54d0a-103">Transform data using Hadoop Streaming activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="54d0a-103">Transform data using Hadoop Streaming activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-hadoop-streaming-activity.md)
> * [Current version](transform-data-using-hadoop-streaming.md)

<span data-ttu-id="54d0a-106">The HDInsight Streaming Activity in a Data Factory [pipeline](concepts-pipelines-activities.md) executes Hadoop Streaming programs on [your own](compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="54d0a-106">The HDInsight Streaming Activity in a Data Factory [pipeline](concepts-pipelines-activities.md) executes Hadoop Streaming programs on [your own](compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight cluster.</span></span> <span data-ttu-id="54d0a-107">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="54d0a-107">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

<span data-ttu-id="54d0a-108">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](introduction.md) and do the [Tutorial: transform data](tutorial-transform-data-spark-powershell.md) before reading this article.</span><span class="sxs-lookup"><span data-stu-id="54d0a-108">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](introduction.md) and do the [Tutorial: transform data](tutorial-transform-data-spark-powershell.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="54d0a-109">JSON sample</span><span class="sxs-lookup"><span data-stu-id="54d0a-109">JSON sample</span></span>
```json
{
    "name": "Streaming Activity",
    "description": "Description",
    "type": "HDInsightStreaming",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "mapper": "MyMapper.exe",
        "reducer": "MyReducer.exe",
        "combiner": "MyCombiner.exe",
        "fileLinkedService": {
            "referenceName": "MyAzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "filePaths": [
            "<containername>/example/apps/MyMapper.exe",
            "<containername>/example/apps/MyReducer.exe",
            "<containername>/example/apps/MyCombiner.exe"
        ],
        "input": "wasb://<containername>@<accountname>.blob.core.windows.net/example/input/MapperInput.txt",
        "output": "wasb://<containername>@<accountname>.blob.core.windows.net/example/output/ReducerOutput.txt",
        "commandEnvironment": [
            "CmdEnvVarName=CmdEnvVarValue"
        ],
        "getDebugInfo": "Failure",
        "arguments": [
            "SampleHadoopJobArgument1"
        ],
        "defines": {
            "param1": "param1Value"
        }
    }
}
```

## <a name="syntax-details"></a><span data-ttu-id="54d0a-110">Syntax details</span><span class="sxs-lookup"><span data-stu-id="54d0a-110">Syntax details</span></span>

| <span data-ttu-id="54d0a-111">Property</span><span class="sxs-lookup"><span data-stu-id="54d0a-111">Property</span></span>          | <span data-ttu-id="54d0a-112">Description</span><span class="sxs-lookup"><span data-stu-id="54d0a-112">Description</span></span>                              | <span data-ttu-id="54d0a-113">Required</span><span class="sxs-lookup"><span data-stu-id="54d0a-113">Required</span></span> |
| ----------------- | ---------------------------------------- | -------- |
| <span data-ttu-id="54d0a-114">name</span><span class="sxs-lookup"><span data-stu-id="54d0a-114">name</span></span>              | <span data-ttu-id="54d0a-115">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-115">Name of the activity</span></span>                     | <span data-ttu-id="54d0a-116">Yes</span><span class="sxs-lookup"><span data-stu-id="54d0a-116">Yes</span></span>      |
| <span data-ttu-id="54d0a-117">description</span><span class="sxs-lookup"><span data-stu-id="54d0a-117">description</span></span>       | <span data-ttu-id="54d0a-118">Text describing what the activity is used for</span><span class="sxs-lookup"><span data-stu-id="54d0a-118">Text describing what the activity is used for</span></span> | <span data-ttu-id="54d0a-119">No</span><span class="sxs-lookup"><span data-stu-id="54d0a-119">No</span></span>       |
| <span data-ttu-id="54d0a-120">type</span><span class="sxs-lookup"><span data-stu-id="54d0a-120">type</span></span>              | <span data-ttu-id="54d0a-121">For Hadoop Streaming Activity, the activity type is HDInsightStreaming</span><span class="sxs-lookup"><span data-stu-id="54d0a-121">For Hadoop Streaming Activity, the activity type is HDInsightStreaming</span></span> | <span data-ttu-id="54d0a-122">Yes</span><span class="sxs-lookup"><span data-stu-id="54d0a-122">Yes</span></span>      |
| <span data-ttu-id="54d0a-123">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="54d0a-123">linkedServiceName</span></span> | <span data-ttu-id="54d0a-124">Reference to the HDInsight cluster registered as a linked service in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54d0a-124">Reference to the HDInsight cluster registered as a linked service in Data Factory.</span></span> <span data-ttu-id="54d0a-125">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="54d0a-125">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span> | <span data-ttu-id="54d0a-126">Yes</span><span class="sxs-lookup"><span data-stu-id="54d0a-126">Yes</span></span>      |
| <span data-ttu-id="54d0a-127">mapper</span><span class="sxs-lookup"><span data-stu-id="54d0a-127">mapper</span></span>            | <span data-ttu-id="54d0a-128">Specifies the name of the mapper executable</span><span class="sxs-lookup"><span data-stu-id="54d0a-128">Specifies the name of the mapper executable</span></span> | <span data-ttu-id="54d0a-129">Yes</span><span class="sxs-lookup"><span data-stu-id="54d0a-129">Yes</span></span>      |
| <span data-ttu-id="54d0a-130">reducer</span><span class="sxs-lookup"><span data-stu-id="54d0a-130">reducer</span></span>           | <span data-ttu-id="54d0a-131">Specifies the name of the reducer executable</span><span class="sxs-lookup"><span data-stu-id="54d0a-131">Specifies the name of the reducer executable</span></span> | <span data-ttu-id="54d0a-132">Yes</span><span class="sxs-lookup"><span data-stu-id="54d0a-132">Yes</span></span>      |
| <span data-ttu-id="54d0a-133">combiner</span><span class="sxs-lookup"><span data-stu-id="54d0a-133">combiner</span></span>          | <span data-ttu-id="54d0a-134">Specifies the name of the combiner executable</span><span class="sxs-lookup"><span data-stu-id="54d0a-134">Specifies the name of the combiner executable</span></span> | <span data-ttu-id="54d0a-135">No</span><span class="sxs-lookup"><span data-stu-id="54d0a-135">No</span></span>       |
| <span data-ttu-id="54d0a-136">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="54d0a-136">fileLinkedService</span></span> | <span data-ttu-id="54d0a-137">Reference to an Azure Storage Linked Service used to store the Mapper, Combiner, and Reducer programs to be executed.</span><span class="sxs-lookup"><span data-stu-id="54d0a-137">Reference to an Azure Storage Linked Service used to store the Mapper, Combiner, and Reducer programs to be executed.</span></span> <span data-ttu-id="54d0a-138">If you don't specify this Linked Service, the Azure Storage Linked Service defined in the HDInsight Linked Service is used.</span><span class="sxs-lookup"><span data-stu-id="54d0a-138">If you don't specify this Linked Service, the Azure Storage Linked Service defined in the HDInsight Linked Service is used.</span></span> | <span data-ttu-id="54d0a-139">No</span><span class="sxs-lookup"><span data-stu-id="54d0a-139">No</span></span>       |
| <span data-ttu-id="54d0a-140">filePath</span><span class="sxs-lookup"><span data-stu-id="54d0a-140">filePath</span></span>          | <span data-ttu-id="54d0a-141">Provide an array of path to the Mapper, Combiner, and Reducer programs stored in the Azure Storage referred by fileLinkedService.</span><span class="sxs-lookup"><span data-stu-id="54d0a-141">Provide an array of path to the Mapper, Combiner, and Reducer programs stored in the Azure Storage referred by fileLinkedService.</span></span> <span data-ttu-id="54d0a-142">The path is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="54d0a-142">The path is case-sensitive.</span></span> | <span data-ttu-id="54d0a-143">Yes</span><span class="sxs-lookup"><span data-stu-id="54d0a-143">Yes</span></span>      |
| <span data-ttu-id="54d0a-144">input</span><span class="sxs-lookup"><span data-stu-id="54d0a-144">input</span></span>             | <span data-ttu-id="54d0a-145">Specifies the WASB path to the input file for the Mapper.</span><span class="sxs-lookup"><span data-stu-id="54d0a-145">Specifies the WASB path to the input file for the Mapper.</span></span> | <span data-ttu-id="54d0a-146">Yes</span><span class="sxs-lookup"><span data-stu-id="54d0a-146">Yes</span></span>      |
| <span data-ttu-id="54d0a-147">output</span><span class="sxs-lookup"><span data-stu-id="54d0a-147">output</span></span>            | <span data-ttu-id="54d0a-148">Specifies the WASB path to the output file for the Reducer.</span><span class="sxs-lookup"><span data-stu-id="54d0a-148">Specifies the WASB path to the output file for the Reducer.</span></span> | <span data-ttu-id="54d0a-149">Yes</span><span class="sxs-lookup"><span data-stu-id="54d0a-149">Yes</span></span>      |
| <span data-ttu-id="54d0a-150">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="54d0a-150">getDebugInfo</span></span>      | <span data-ttu-id="54d0a-151">Specifies when the log files are copied to the Azure Storage used by HDInsight cluster (or) specified by scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="54d0a-151">Specifies when the log files are copied to the Azure Storage used by HDInsight cluster (or) specified by scriptLinkedService.</span></span> <span data-ttu-id="54d0a-152">Allowed values: None, Always, or Failure.</span><span class="sxs-lookup"><span data-stu-id="54d0a-152">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="54d0a-153">Default value: None.</span><span class="sxs-lookup"><span data-stu-id="54d0a-153">Default value: None.</span></span> | <span data-ttu-id="54d0a-154">No</span><span class="sxs-lookup"><span data-stu-id="54d0a-154">No</span></span>       |
| <span data-ttu-id="54d0a-155">arguments</span><span class="sxs-lookup"><span data-stu-id="54d0a-155">arguments</span></span>         | <span data-ttu-id="54d0a-156">Specifies an array of arguments for a Hadoop job.</span><span class="sxs-lookup"><span data-stu-id="54d0a-156">Specifies an array of arguments for a Hadoop job.</span></span> <span data-ttu-id="54d0a-157">The arguments are passed as command-line arguments to each task.</span><span class="sxs-lookup"><span data-stu-id="54d0a-157">The arguments are passed as command-line arguments to each task.</span></span> | <span data-ttu-id="54d0a-158">No</span><span class="sxs-lookup"><span data-stu-id="54d0a-158">No</span></span>       |
| <span data-ttu-id="54d0a-159">defines</span><span class="sxs-lookup"><span data-stu-id="54d0a-159">defines</span></span>           | <span data-ttu-id="54d0a-160">Specify parameters as key/value pairs for referencing within the Hive script.</span><span class="sxs-lookup"><span data-stu-id="54d0a-160">Specify parameters as key/value pairs for referencing within the Hive script.</span></span> | <span data-ttu-id="54d0a-161">No</span><span class="sxs-lookup"><span data-stu-id="54d0a-161">No</span></span>       | 

## <a name="next-steps"></a><span data-ttu-id="54d0a-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="54d0a-162">Next steps</span></span>
<span data-ttu-id="54d0a-163">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="54d0a-163">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="54d0a-164">U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-164">U-SQL activity</span></span>](transform-data-using-data-lake-analytics.md)
* [<span data-ttu-id="54d0a-165">Hive activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-165">Hive activity</span></span>](transform-data-using-hadoop-hive.md)
* [<span data-ttu-id="54d0a-166">Pig activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-166">Pig activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="54d0a-167">MapReduce activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-167">MapReduce activity</span></span>](transform-data-using-hadoop-map-reduce.md)
* [<span data-ttu-id="54d0a-168">Spark activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-168">Spark activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="54d0a-169">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-169">.NET custom activity</span></span>](transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="54d0a-170">Machine Learning Batch Execution activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-170">Machine Learning Batch Execution activity</span></span>](transform-data-using-machine-learning.md)
* [<span data-ttu-id="54d0a-171">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="54d0a-171">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)
