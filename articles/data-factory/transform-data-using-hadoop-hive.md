---
title: Transform data using Hadoop Hive activity in Azure Data Factory | Microsoft Docs
description: Learn how you can use the Hive Activity in an Azure data factory to run Hive queries on an on-demand/your own HDInsight cluster.
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
ms.openlocfilehash: fc7c2c49de582a413b49d31c4b4e062d81e5e6ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968995"
---
# <a name="transform-data-using-hadoop-hive-activity-in-azure-data-factory"></a><span data-ttu-id="ea886-103">Transform data using Hadoop Hive activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ea886-103">Transform data using Hadoop Hive activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-hive-activity.md)
> * [Current version](transform-data-using-hadoop-hive.md)

<span data-ttu-id="ea886-106">The HDInsight Hive activity in a Data Factory [pipeline](concepts-pipelines-activities.md) executes Hive queries on [your own](compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)  HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ea886-106">The HDInsight Hive activity in a Data Factory [pipeline](concepts-pipelines-activities.md) executes Hive queries on [your own](compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)  HDInsight cluster.</span></span> <span data-ttu-id="ea886-107">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="ea886-107">This article builds on the [data transformation activities](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

<span data-ttu-id="ea886-108">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](introduction.md) and do the [Tutorial: transform data](tutorial-transform-data-spark-powershell.md) before reading this article.</span><span class="sxs-lookup"><span data-stu-id="ea886-108">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](introduction.md) and do the [Tutorial: transform data](tutorial-transform-data-spark-powershell.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="ea886-109">Syntax</span><span class="sxs-lookup"><span data-stu-id="ea886-109">Syntax</span></span>

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "linkedServiceName": {
        "referenceName": "MyHDInsightLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "scriptLinkedService": {
            "referenceName": "MyAzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "scriptPath": "MyAzureStorage\\HiveScripts\\MyHiveSript.hql",
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
## <a name="syntax-details"></a><span data-ttu-id="ea886-110">Syntax details</span><span class="sxs-lookup"><span data-stu-id="ea886-110">Syntax details</span></span>
| <span data-ttu-id="ea886-111">Property</span><span class="sxs-lookup"><span data-stu-id="ea886-111">Property</span></span>            | <span data-ttu-id="ea886-112">Description</span><span class="sxs-lookup"><span data-stu-id="ea886-112">Description</span></span>                              | <span data-ttu-id="ea886-113">Required</span><span class="sxs-lookup"><span data-stu-id="ea886-113">Required</span></span> |
| ------------------- | ---------------------------------------- | -------- |
| <span data-ttu-id="ea886-114">name</span><span class="sxs-lookup"><span data-stu-id="ea886-114">name</span></span>                | <span data-ttu-id="ea886-115">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="ea886-115">Name of the activity</span></span>                     | <span data-ttu-id="ea886-116">Yes</span><span class="sxs-lookup"><span data-stu-id="ea886-116">Yes</span></span>      |
| <span data-ttu-id="ea886-117">description</span><span class="sxs-lookup"><span data-stu-id="ea886-117">description</span></span>         | <span data-ttu-id="ea886-118">Text describing what the activity is used for</span><span class="sxs-lookup"><span data-stu-id="ea886-118">Text describing what the activity is used for</span></span> | <span data-ttu-id="ea886-119">No</span><span class="sxs-lookup"><span data-stu-id="ea886-119">No</span></span>       |
| <span data-ttu-id="ea886-120">type</span><span class="sxs-lookup"><span data-stu-id="ea886-120">type</span></span>                | <span data-ttu-id="ea886-121">For Hive Activity, the activity type is HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="ea886-121">For Hive Activity, the activity type is HDinsightHive</span></span> | <span data-ttu-id="ea886-122">Yes</span><span class="sxs-lookup"><span data-stu-id="ea886-122">Yes</span></span>      |
| <span data-ttu-id="ea886-123">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ea886-123">linkedServiceName</span></span>   | <span data-ttu-id="ea886-124">Reference to the HDInsight cluster registered as a linked service in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ea886-124">Reference to the HDInsight cluster registered as a linked service in Data Factory.</span></span> <span data-ttu-id="ea886-125">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="ea886-125">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span> | <span data-ttu-id="ea886-126">Yes</span><span class="sxs-lookup"><span data-stu-id="ea886-126">Yes</span></span>      |
| <span data-ttu-id="ea886-127">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="ea886-127">scriptLinkedService</span></span> | <span data-ttu-id="ea886-128">Reference to an Azure Storage Linked Service used to store the Hive script to be executed.</span><span class="sxs-lookup"><span data-stu-id="ea886-128">Reference to an Azure Storage Linked Service used to store the Hive script to be executed.</span></span> <span data-ttu-id="ea886-129">If you don't specify this Linked Service, the Azure Storage Linked Service defined in the HDInsight Linked Service is used.</span><span class="sxs-lookup"><span data-stu-id="ea886-129">If you don't specify this Linked Service, the Azure Storage Linked Service defined in the HDInsight Linked Service is used.</span></span> | <span data-ttu-id="ea886-130">No</span><span class="sxs-lookup"><span data-stu-id="ea886-130">No</span></span>       |
| <span data-ttu-id="ea886-131">scriptPath</span><span class="sxs-lookup"><span data-stu-id="ea886-131">scriptPath</span></span>          | <span data-ttu-id="ea886-132">Provide the path to the script file stored in the Azure Storage referred by scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ea886-132">Provide the path to the script file stored in the Azure Storage referred by scriptLinkedService.</span></span> <span data-ttu-id="ea886-133">The file name is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="ea886-133">The file name is case-sensitive.</span></span> | <span data-ttu-id="ea886-134">Yes</span><span class="sxs-lookup"><span data-stu-id="ea886-134">Yes</span></span>      |
| <span data-ttu-id="ea886-135">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="ea886-135">getDebugInfo</span></span>        | <span data-ttu-id="ea886-136">Specifies when the log files are copied to the Azure Storage used by HDInsight cluster (or) specified by scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ea886-136">Specifies when the log files are copied to the Azure Storage used by HDInsight cluster (or) specified by scriptLinkedService.</span></span> <span data-ttu-id="ea886-137">Allowed values: None, Always, or Failure.</span><span class="sxs-lookup"><span data-stu-id="ea886-137">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="ea886-138">Default value: None.</span><span class="sxs-lookup"><span data-stu-id="ea886-138">Default value: None.</span></span> | <span data-ttu-id="ea886-139">No</span><span class="sxs-lookup"><span data-stu-id="ea886-139">No</span></span>       |
| <span data-ttu-id="ea886-140">arguments</span><span class="sxs-lookup"><span data-stu-id="ea886-140">arguments</span></span>           | <span data-ttu-id="ea886-141">Specifies an array of arguments for a Hadoop job.</span><span class="sxs-lookup"><span data-stu-id="ea886-141">Specifies an array of arguments for a Hadoop job.</span></span> <span data-ttu-id="ea886-142">The arguments are passed as command-line arguments to each task.</span><span class="sxs-lookup"><span data-stu-id="ea886-142">The arguments are passed as command-line arguments to each task.</span></span> | <span data-ttu-id="ea886-143">No</span><span class="sxs-lookup"><span data-stu-id="ea886-143">No</span></span>       |
| <span data-ttu-id="ea886-144">defines</span><span class="sxs-lookup"><span data-stu-id="ea886-144">defines</span></span>             | <span data-ttu-id="ea886-145">Specify parameters as key/value pairs for referencing within the Hive script.</span><span class="sxs-lookup"><span data-stu-id="ea886-145">Specify parameters as key/value pairs for referencing within the Hive script.</span></span> | <span data-ttu-id="ea886-146">No</span><span class="sxs-lookup"><span data-stu-id="ea886-146">No</span></span>       |

## <a name="next-steps"></a><span data-ttu-id="ea886-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea886-147">Next steps</span></span>
<span data-ttu-id="ea886-148">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="ea886-148">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="ea886-149">U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="ea886-149">U-SQL activity</span></span>](transform-data-using-data-lake-analytics.md)
* [<span data-ttu-id="ea886-150">Pig activity</span><span class="sxs-lookup"><span data-stu-id="ea886-150">Pig activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="ea886-151">MapReduce activity</span><span class="sxs-lookup"><span data-stu-id="ea886-151">MapReduce activity</span></span>](transform-data-using-hadoop-map-reduce.md)
* [<span data-ttu-id="ea886-152">Hadoop Streaming activity</span><span class="sxs-lookup"><span data-stu-id="ea886-152">Hadoop Streaming activity</span></span>](transform-data-using-hadoop-streaming.md)
* [<span data-ttu-id="ea886-153">Spark activity</span><span class="sxs-lookup"><span data-stu-id="ea886-153">Spark activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="ea886-154">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="ea886-154">.NET custom activity</span></span>](transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="ea886-155">Machine Learning Batch Execution activity</span><span class="sxs-lookup"><span data-stu-id="ea886-155">Machine Learning Batch Execution activity</span></span>](transform-data-using-machine-learning.md)
* [<span data-ttu-id="ea886-156">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="ea886-156">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)

