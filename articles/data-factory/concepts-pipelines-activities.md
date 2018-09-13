---
title: Pipelines and activities in Azure Data Factory | Microsoft Docs
description: Learn about pipelines and activities in Azure Data Factory.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/12/2018
ms.author: shlo
ms.openlocfilehash: ca64c87a0211ae00218493fe7bfddcbbb81a032a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855695"
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a><span data-ttu-id="c65ce-103">Pipelines and activities in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c65ce-103">Pipelines and activities in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-create-pipelines.md)
> * [Current version](concepts-pipelines-activities.md)

<span data-ttu-id="c65ce-106">This article helps you understand pipelines and activities in Azure Data Factory and use them to construct end-to-end data-driven workflows for your data movement and data processing scenarios.</span><span class="sxs-lookup"><span data-stu-id="c65ce-106">This article helps you understand pipelines and activities in Azure Data Factory and use them to construct end-to-end data-driven workflows for your data movement and data processing scenarios.</span></span>

## <a name="overview"></a><span data-ttu-id="c65ce-107">Overview</span><span class="sxs-lookup"><span data-stu-id="c65ce-107">Overview</span></span>
<span data-ttu-id="c65ce-108">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="c65ce-108">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c65ce-109">A pipeline is a logical grouping of activities that together perform a task.</span><span class="sxs-lookup"><span data-stu-id="c65ce-109">A pipeline is a logical grouping of activities that together perform a task.</span></span> <span data-ttu-id="c65ce-110">For example, a pipeline could contain a set of activities that ingest and clean log data, and then kick off a Spark job on an HDInsight cluster to analyze the log data.</span><span class="sxs-lookup"><span data-stu-id="c65ce-110">For example, a pipeline could contain a set of activities that ingest and clean log data, and then kick off a Spark job on an HDInsight cluster to analyze the log data.</span></span> <span data-ttu-id="c65ce-111">The beauty of this is that the pipeline allows you to manage the activities as a set instead of each one individually.</span><span class="sxs-lookup"><span data-stu-id="c65ce-111">The beauty of this is that the pipeline allows you to manage the activities as a set instead of each one individually.</span></span> <span data-ttu-id="c65ce-112">For example, you can deploy and schedule the pipeline, instead of the activities independently.</span><span class="sxs-lookup"><span data-stu-id="c65ce-112">For example, you can deploy and schedule the pipeline, instead of the activities independently.</span></span>

<span data-ttu-id="c65ce-113">The activities in a pipeline define actions to perform on your data.</span><span class="sxs-lookup"><span data-stu-id="c65ce-113">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="c65ce-114">For example, you may use a copy activity to copy data from an on-premises SQL Server to an Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c65ce-114">For example, you may use a copy activity to copy data from an on-premises SQL Server to an Azure Blob Storage.</span></span> <span data-ttu-id="c65ce-115">Then, use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process/transform data from the blob storage to produce output data.</span><span class="sxs-lookup"><span data-stu-id="c65ce-115">Then, use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process/transform data from the blob storage to produce output data.</span></span> <span data-ttu-id="c65ce-116">Finally, use a second copy activity to copy the output data to an Azure SQL Data Warehouse on top of which business intelligence (BI) reporting solutions are built.</span><span class="sxs-lookup"><span data-stu-id="c65ce-116">Finally, use a second copy activity to copy the output data to an Azure SQL Data Warehouse on top of which business intelligence (BI) reporting solutions are built.</span></span>

<span data-ttu-id="c65ce-117">Data Factory supports three types of activities: [data movement activities](copy-activity-overview.md), [data transformation activities](transform-data.md), and [control activities](control-flow-web-activity.md).</span><span class="sxs-lookup"><span data-stu-id="c65ce-117">Data Factory supports three types of activities: [data movement activities](copy-activity-overview.md), [data transformation activities](transform-data.md), and [control activities](control-flow-web-activity.md).</span></span> <span data-ttu-id="c65ce-118">An activity can take zero or more input [datasets](concepts-datasets-linked-services.md) and produce one or more output [datasets](concepts-datasets-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="c65ce-118">An activity can take zero or more input [datasets](concepts-datasets-linked-services.md) and produce one or more output [datasets](concepts-datasets-linked-services.md).</span></span> <span data-ttu-id="c65ce-119">The following diagram shows the relationship between pipeline, activity, and dataset in Data Factory:</span><span class="sxs-lookup"><span data-stu-id="c65ce-119">The following diagram shows the relationship between pipeline, activity, and dataset in Data Factory:</span></span>

![Relationship between dataset, activity, and pipeline](media/concepts-pipelines-activities/relationship-between-dataset-pipeline-activity.png)

<span data-ttu-id="c65ce-121">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-121">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="c65ce-122">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span><span class="sxs-lookup"><span data-stu-id="c65ce-122">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="c65ce-123">After you create a dataset, you can use it with activities in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c65ce-123">After you create a dataset, you can use it with activities in a pipeline.</span></span> <span data-ttu-id="c65ce-124">For example, a dataset can be an input/output dataset of a Copy Activity or an HDInsightHive Activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-124">For example, a dataset can be an input/output dataset of a Copy Activity or an HDInsightHive Activity.</span></span> <span data-ttu-id="c65ce-125">For more information about datasets, see [Datasets in Azure Data Factory](concepts-datasets-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="c65ce-125">For more information about datasets, see [Datasets in Azure Data Factory](concepts-datasets-linked-services.md) article.</span></span>

## <a name="data-movement-activities"></a><span data-ttu-id="c65ce-126">Data movement activities</span><span class="sxs-lookup"><span data-stu-id="c65ce-126">Data movement activities</span></span>
<span data-ttu-id="c65ce-127">Copy Activity in Data Factory copies data from a source data store to a sink data store.</span><span class="sxs-lookup"><span data-stu-id="c65ce-127">Copy Activity in Data Factory copies data from a source data store to a sink data store.</span></span> <span data-ttu-id="c65ce-128">Data Factory supports the data stores listed in the table in this section.</span><span class="sxs-lookup"><span data-stu-id="c65ce-128">Data Factory supports the data stores listed in the table in this section.</span></span> <span data-ttu-id="c65ce-129">Data from any source can be written to any sink.</span><span class="sxs-lookup"><span data-stu-id="c65ce-129">Data from any source can be written to any sink.</span></span> <span data-ttu-id="c65ce-130">Click a data store to learn how to copy data to and from that store.</span><span class="sxs-lookup"><span data-stu-id="c65ce-130">Click a data store to learn how to copy data to and from that store.</span></span>

[!INCLUDE [data-factory-v2-supported-data-stores](../../includes/data-factory-v2-supported-data-stores.md)]

<span data-ttu-id="c65ce-131">For more information, see [Copy Activity - Overview](copy-activity-overview.md) article.</span><span class="sxs-lookup"><span data-stu-id="c65ce-131">For more information, see [Copy Activity - Overview](copy-activity-overview.md) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="c65ce-132">Data transformation activities</span><span class="sxs-lookup"><span data-stu-id="c65ce-132">Data transformation activities</span></span>
<span data-ttu-id="c65ce-133">Azure Data Factory supports the following transformation activities that can be added to pipelines either individually or chained with another activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-133">Azure Data Factory supports the following transformation activities that can be added to pipelines either individually or chained with another activity.</span></span>

<span data-ttu-id="c65ce-134">Data transformation activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-134">Data transformation activity</span></span> | <span data-ttu-id="c65ce-135">Compute environment</span><span class="sxs-lookup"><span data-stu-id="c65ce-135">Compute environment</span></span>
---------------------------- | -------------------
[<span data-ttu-id="c65ce-136">Hive</span><span class="sxs-lookup"><span data-stu-id="c65ce-136">Hive</span></span>](transform-data-using-hadoop-hive.md) | <span data-ttu-id="c65ce-137">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="c65ce-137">HDInsight [Hadoop]</span></span>
[<span data-ttu-id="c65ce-138">Pig</span><span class="sxs-lookup"><span data-stu-id="c65ce-138">Pig</span></span>](transform-data-using-hadoop-pig.md) | <span data-ttu-id="c65ce-139">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="c65ce-139">HDInsight [Hadoop]</span></span>
[<span data-ttu-id="c65ce-140">MapReduce</span><span class="sxs-lookup"><span data-stu-id="c65ce-140">MapReduce</span></span>](transform-data-using-hadoop-map-reduce.md) | <span data-ttu-id="c65ce-141">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="c65ce-141">HDInsight [Hadoop]</span></span>
[<span data-ttu-id="c65ce-142">Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="c65ce-142">Hadoop Streaming</span></span>](transform-data-using-hadoop-streaming.md) | <span data-ttu-id="c65ce-143">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="c65ce-143">HDInsight [Hadoop]</span></span>
[<span data-ttu-id="c65ce-144">Spark</span><span class="sxs-lookup"><span data-stu-id="c65ce-144">Spark</span></span>](transform-data-using-spark.md) | <span data-ttu-id="c65ce-145">HDInsight [Hadoop]</span><span class="sxs-lookup"><span data-stu-id="c65ce-145">HDInsight [Hadoop]</span></span>
[<span data-ttu-id="c65ce-146">Machine Learning activities: Batch Execution and Update Resource</span><span class="sxs-lookup"><span data-stu-id="c65ce-146">Machine Learning activities: Batch Execution and Update Resource</span></span>](transform-data-using-machine-learning.md) | <span data-ttu-id="c65ce-147">Azure VM</span><span class="sxs-lookup"><span data-stu-id="c65ce-147">Azure VM</span></span>
[<span data-ttu-id="c65ce-148">Stored Procedure</span><span class="sxs-lookup"><span data-stu-id="c65ce-148">Stored Procedure</span></span>](transform-data-using-stored-procedure.md) | <span data-ttu-id="c65ce-149">Azure SQL, Azure SQL Data Warehouse, or SQL Server</span><span class="sxs-lookup"><span data-stu-id="c65ce-149">Azure SQL, Azure SQL Data Warehouse, or SQL Server</span></span>
[<span data-ttu-id="c65ce-150">U-SQL</span><span class="sxs-lookup"><span data-stu-id="c65ce-150">U-SQL</span></span>](transform-data-using-data-lake-analytics.md) | <span data-ttu-id="c65ce-151">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c65ce-151">Azure Data Lake Analytics</span></span>
[<span data-ttu-id="c65ce-152">Custom Code</span><span class="sxs-lookup"><span data-stu-id="c65ce-152">Custom Code</span></span>](transform-data-using-dotnet-custom-activity.md) | <span data-ttu-id="c65ce-153">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c65ce-153">Azure Batch</span></span>
[<span data-ttu-id="c65ce-154">Databricks Notebook</span><span class="sxs-lookup"><span data-stu-id="c65ce-154">Databricks Notebook</span></span>](transform-data-databricks-notebook.md) | <span data-ttu-id="c65ce-155">Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="c65ce-155">Azure Databricks</span></span>

<span data-ttu-id="c65ce-156">For more information, see the [data transformation activities](transform-data.md) article.</span><span class="sxs-lookup"><span data-stu-id="c65ce-156">For more information, see the [data transformation activities](transform-data.md) article.</span></span>

## <a name="control-activities"></a><span data-ttu-id="c65ce-157">Control activities</span><span class="sxs-lookup"><span data-stu-id="c65ce-157">Control activities</span></span>
<span data-ttu-id="c65ce-158">The following control flow activities are supported:</span><span class="sxs-lookup"><span data-stu-id="c65ce-158">The following control flow activities are supported:</span></span>

<span data-ttu-id="c65ce-159">Control activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-159">Control activity</span></span> | <span data-ttu-id="c65ce-160">Description</span><span class="sxs-lookup"><span data-stu-id="c65ce-160">Description</span></span>
---------------- | -----------
[<span data-ttu-id="c65ce-161">Execute Pipeline Activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-161">Execute Pipeline Activity</span></span>](control-flow-execute-pipeline-activity.md) | <span data-ttu-id="c65ce-162">Execute Pipeline activity allows a Data Factory pipeline to invoke another pipeline.</span><span class="sxs-lookup"><span data-stu-id="c65ce-162">Execute Pipeline activity allows a Data Factory pipeline to invoke another pipeline.</span></span>
[<span data-ttu-id="c65ce-163">ForEachActivity</span><span class="sxs-lookup"><span data-stu-id="c65ce-163">ForEachActivity</span></span>](control-flow-for-each-activity.md) | <span data-ttu-id="c65ce-164">ForEach Activity defines a repeating control flow in your pipeline.</span><span class="sxs-lookup"><span data-stu-id="c65ce-164">ForEach Activity defines a repeating control flow in your pipeline.</span></span> <span data-ttu-id="c65ce-165">This activity is used to iterate over a collection and executes specified activities in a loop.</span><span class="sxs-lookup"><span data-stu-id="c65ce-165">This activity is used to iterate over a collection and executes specified activities in a loop.</span></span> <span data-ttu-id="c65ce-166">The loop implementation of this activity is similar to Foreach looping structure in programming languages.</span><span class="sxs-lookup"><span data-stu-id="c65ce-166">The loop implementation of this activity is similar to Foreach looping structure in programming languages.</span></span>
[<span data-ttu-id="c65ce-167">WebActivity</span><span class="sxs-lookup"><span data-stu-id="c65ce-167">WebActivity</span></span>](control-flow-web-activity.md) | <span data-ttu-id="c65ce-168">Web Activity can be used to call a custom REST endpoint from a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="c65ce-168">Web Activity can be used to call a custom REST endpoint from a Data Factory pipeline.</span></span> <span data-ttu-id="c65ce-169">You can pass datasets and linked services to be consumed and accessed by the activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-169">You can pass datasets and linked services to be consumed and accessed by the activity.</span></span>
[<span data-ttu-id="c65ce-170">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-170">Lookup Activity</span></span>](control-flow-lookup-activity.md) | <span data-ttu-id="c65ce-171">Lookup Activity can be used to read or look up a record/ table name/ value from any external source.</span><span class="sxs-lookup"><span data-stu-id="c65ce-171">Lookup Activity can be used to read or look up a record/ table name/ value from any external source.</span></span> <span data-ttu-id="c65ce-172">This output can further be referenced by succeeding activities.</span><span class="sxs-lookup"><span data-stu-id="c65ce-172">This output can further be referenced by succeeding activities.</span></span>
[<span data-ttu-id="c65ce-173">Get Metadata Activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-173">Get Metadata Activity</span></span>](control-flow-get-metadata-activity.md) | <span data-ttu-id="c65ce-174">GetMetadata activity can be used to retrieve metadata of any data in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c65ce-174">GetMetadata activity can be used to retrieve metadata of any data in Azure Data Factory.</span></span>
[<span data-ttu-id="c65ce-175">Until Activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-175">Until Activity</span></span>](control-flow-until-activity.md) | <span data-ttu-id="c65ce-176">Implements Do-Until loop that is similar to Do-Until looping structure in programming languages.</span><span class="sxs-lookup"><span data-stu-id="c65ce-176">Implements Do-Until loop that is similar to Do-Until looping structure in programming languages.</span></span> <span data-ttu-id="c65ce-177">It executes a set of activities in a loop until the condition associated with the activity evaluates to true.</span><span class="sxs-lookup"><span data-stu-id="c65ce-177">It executes a set of activities in a loop until the condition associated with the activity evaluates to true.</span></span> <span data-ttu-id="c65ce-178">You can specify a timeout value for the until activity in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c65ce-178">You can specify a timeout value for the until activity in Data Factory.</span></span>
[<span data-ttu-id="c65ce-179">If Condition Activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-179">If Condition Activity</span></span>](control-flow-if-condition-activity.md) | <span data-ttu-id="c65ce-180">The If Condition can be used to branch based on condition that evaluates to true or false.</span><span class="sxs-lookup"><span data-stu-id="c65ce-180">The If Condition can be used to branch based on condition that evaluates to true or false.</span></span> <span data-ttu-id="c65ce-181">The If Condition activity provides the same functionality that an if statement provides in programming languages.</span><span class="sxs-lookup"><span data-stu-id="c65ce-181">The If Condition activity provides the same functionality that an if statement provides in programming languages.</span></span> <span data-ttu-id="c65ce-182">It evaluates a set of activities when the condition evaluates to `true` and another set of activities when the condition evaluates to `false`.</span><span class="sxs-lookup"><span data-stu-id="c65ce-182">It evaluates a set of activities when the condition evaluates to `true` and another set of activities when the condition evaluates to `false`.</span></span>
[<span data-ttu-id="c65ce-183">Wait Activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-183">Wait Activity</span></span>](control-flow-wait-activity.md) | <span data-ttu-id="c65ce-184">When you use a Wait activity in a pipeline, the pipeline waits for the specified period of time before continuing with execution of subsequent activities.</span><span class="sxs-lookup"><span data-stu-id="c65ce-184">When you use a Wait activity in a pipeline, the pipeline waits for the specified period of time before continuing with execution of subsequent activities.</span></span>

## <a name="pipeline-json"></a><span data-ttu-id="c65ce-185">Pipeline JSON</span><span class="sxs-lookup"><span data-stu-id="c65ce-185">Pipeline JSON</span></span>
<span data-ttu-id="c65ce-186">Here is how a pipeline is defined in JSON format:</span><span class="sxs-lookup"><span data-stu-id="c65ce-186">Here is how a pipeline is defined in JSON format:</span></span>

```json
{
    "name": "PipelineName",
    "properties":
    {
        "description": "pipeline description",
        "activities":
        [
        ],
        "parameters": {
         }
    }
}
```

<span data-ttu-id="c65ce-187">Tag</span><span class="sxs-lookup"><span data-stu-id="c65ce-187">Tag</span></span> | <span data-ttu-id="c65ce-188">Description</span><span class="sxs-lookup"><span data-stu-id="c65ce-188">Description</span></span> | <span data-ttu-id="c65ce-189">Type</span><span class="sxs-lookup"><span data-stu-id="c65ce-189">Type</span></span> | <span data-ttu-id="c65ce-190">Required</span><span class="sxs-lookup"><span data-stu-id="c65ce-190">Required</span></span>
--- | ----------- | ---- | --------
<span data-ttu-id="c65ce-191">name</span><span class="sxs-lookup"><span data-stu-id="c65ce-191">name</span></span> | <span data-ttu-id="c65ce-192">Name of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c65ce-192">Name of the pipeline.</span></span> <span data-ttu-id="c65ce-193">Specify a name that represents the action that the pipeline performs.</span><span class="sxs-lookup"><span data-stu-id="c65ce-193">Specify a name that represents the action that the pipeline performs.</span></span> <br/><ul><li><span data-ttu-id="c65ce-194">Maximum number of characters: 140</span><span class="sxs-lookup"><span data-stu-id="c65ce-194">Maximum number of characters: 140</span></span></li><li><span data-ttu-id="c65ce-195">Must start with a letter, number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="c65ce-195">Must start with a letter, number, or an underscore (_)</span></span></li><li><span data-ttu-id="c65ce-196">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\”</span><span class="sxs-lookup"><span data-stu-id="c65ce-196">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\”</span></span></li></ul> | <span data-ttu-id="c65ce-197">String</span><span class="sxs-lookup"><span data-stu-id="c65ce-197">String</span></span> | <span data-ttu-id="c65ce-198">Yes</span><span class="sxs-lookup"><span data-stu-id="c65ce-198">Yes</span></span>
<span data-ttu-id="c65ce-199">description</span><span class="sxs-lookup"><span data-stu-id="c65ce-199">description</span></span> | <span data-ttu-id="c65ce-200">Specify the text describing what the pipeline is used for.</span><span class="sxs-lookup"><span data-stu-id="c65ce-200">Specify the text describing what the pipeline is used for.</span></span> | <span data-ttu-id="c65ce-201">String</span><span class="sxs-lookup"><span data-stu-id="c65ce-201">String</span></span> | <span data-ttu-id="c65ce-202">No</span><span class="sxs-lookup"><span data-stu-id="c65ce-202">No</span></span>
<span data-ttu-id="c65ce-203">activities</span><span class="sxs-lookup"><span data-stu-id="c65ce-203">activities</span></span> | <span data-ttu-id="c65ce-204">The **activities** section can have one or more activities defined within it.</span><span class="sxs-lookup"><span data-stu-id="c65ce-204">The **activities** section can have one or more activities defined within it.</span></span> <span data-ttu-id="c65ce-205">See the [Activity JSON](#activity-json) section for details about the activities JSON element.</span><span class="sxs-lookup"><span data-stu-id="c65ce-205">See the [Activity JSON](#activity-json) section for details about the activities JSON element.</span></span> | <span data-ttu-id="c65ce-206">Array</span><span class="sxs-lookup"><span data-stu-id="c65ce-206">Array</span></span> | <span data-ttu-id="c65ce-207">Yes</span><span class="sxs-lookup"><span data-stu-id="c65ce-207">Yes</span></span>
<span data-ttu-id="c65ce-208">parameters</span><span class="sxs-lookup"><span data-stu-id="c65ce-208">parameters</span></span> | <span data-ttu-id="c65ce-209">The **parameters** section can have one or more parameters defined within the pipeline, making your pipeline flexible for reuse.</span><span class="sxs-lookup"><span data-stu-id="c65ce-209">The **parameters** section can have one or more parameters defined within the pipeline, making your pipeline flexible for reuse.</span></span> | <span data-ttu-id="c65ce-210">List</span><span class="sxs-lookup"><span data-stu-id="c65ce-210">List</span></span> | <span data-ttu-id="c65ce-211">No</span><span class="sxs-lookup"><span data-stu-id="c65ce-211">No</span></span>

## <a name="activity-json"></a><span data-ttu-id="c65ce-212">Activity JSON</span><span class="sxs-lookup"><span data-stu-id="c65ce-212">Activity JSON</span></span>
<span data-ttu-id="c65ce-213">The **activities** section can have one or more activities defined within it.</span><span class="sxs-lookup"><span data-stu-id="c65ce-213">The **activities** section can have one or more activities defined within it.</span></span> <span data-ttu-id="c65ce-214">There are two main types of activities: Execution and Control Activities.</span><span class="sxs-lookup"><span data-stu-id="c65ce-214">There are two main types of activities: Execution and Control Activities.</span></span>

### <a name="execution-activities"></a><span data-ttu-id="c65ce-215">Execution activities</span><span class="sxs-lookup"><span data-stu-id="c65ce-215">Execution activities</span></span>
<span data-ttu-id="c65ce-216">Execution activities include [data movement](#data-movement-activities) and [data transformation activities](#data-transformation-activities).</span><span class="sxs-lookup"><span data-stu-id="c65ce-216">Execution activities include [data movement](#data-movement-activities) and [data transformation activities](#data-transformation-activities).</span></span> <span data-ttu-id="c65ce-217">They have the following top-level structure:</span><span class="sxs-lookup"><span data-stu-id="c65ce-217">They have the following top-level structure:</span></span>

```json
{
    "name": "Execution Activity Name",
    "description": "description",
    "type": "<ActivityType>",
    "typeProperties":
    {
    },
    "linkedServiceName": "MyLinkedService",
    "policy":
    {
    },
    "dependsOn":
    {
    }
}
```

<span data-ttu-id="c65ce-218">Following table describes properties in the activity JSON definition:</span><span class="sxs-lookup"><span data-stu-id="c65ce-218">Following table describes properties in the activity JSON definition:</span></span>

<span data-ttu-id="c65ce-219">Tag</span><span class="sxs-lookup"><span data-stu-id="c65ce-219">Tag</span></span> | <span data-ttu-id="c65ce-220">Description</span><span class="sxs-lookup"><span data-stu-id="c65ce-220">Description</span></span> | <span data-ttu-id="c65ce-221">Required</span><span class="sxs-lookup"><span data-stu-id="c65ce-221">Required</span></span>
--- | ----------- | ---------
<span data-ttu-id="c65ce-222">name</span><span class="sxs-lookup"><span data-stu-id="c65ce-222">name</span></span> | <span data-ttu-id="c65ce-223">Name of the activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-223">Name of the activity.</span></span> <span data-ttu-id="c65ce-224">Specify a name that represents the action that the activity performs.</span><span class="sxs-lookup"><span data-stu-id="c65ce-224">Specify a name that represents the action that the activity performs.</span></span> <br/><ul><li><span data-ttu-id="c65ce-225">Maximum number of characters: 55</span><span class="sxs-lookup"><span data-stu-id="c65ce-225">Maximum number of characters: 55</span></span></li><li><span data-ttu-id="c65ce-226">Must start with a letter number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="c65ce-226">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="c65ce-227">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\”</span><span class="sxs-lookup"><span data-stu-id="c65ce-227">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\”</span></span> | <span data-ttu-id="c65ce-228">Yes</span><span class="sxs-lookup"><span data-stu-id="c65ce-228">Yes</span></span></li></ul>
<span data-ttu-id="c65ce-229">description</span><span class="sxs-lookup"><span data-stu-id="c65ce-229">description</span></span> | <span data-ttu-id="c65ce-230">Text describing what the activity or is used for</span><span class="sxs-lookup"><span data-stu-id="c65ce-230">Text describing what the activity or is used for</span></span> | <span data-ttu-id="c65ce-231">Yes</span><span class="sxs-lookup"><span data-stu-id="c65ce-231">Yes</span></span>
<span data-ttu-id="c65ce-232">type</span><span class="sxs-lookup"><span data-stu-id="c65ce-232">type</span></span> | <span data-ttu-id="c65ce-233">Type of the activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-233">Type of the activity.</span></span> <span data-ttu-id="c65ce-234">See the [Data Movement Activities](#data-movement-activities), [Data Transformation Activities](#data-transformation-activities), and [Control Activities](#control-activities) sections for different types of activities.</span><span class="sxs-lookup"><span data-stu-id="c65ce-234">See the [Data Movement Activities](#data-movement-activities), [Data Transformation Activities](#data-transformation-activities), and [Control Activities](#control-activities) sections for different types of activities.</span></span> | <span data-ttu-id="c65ce-235">Yes</span><span class="sxs-lookup"><span data-stu-id="c65ce-235">Yes</span></span>
<span data-ttu-id="c65ce-236">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c65ce-236">linkedServiceName</span></span> | <span data-ttu-id="c65ce-237">Name of the linked service used by the activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-237">Name of the linked service used by the activity.</span></span><br/><br/><span data-ttu-id="c65ce-238">An activity may require that you specify the linked service that links to the required compute environment.</span><span class="sxs-lookup"><span data-stu-id="c65ce-238">An activity may require that you specify the linked service that links to the required compute environment.</span></span> | <span data-ttu-id="c65ce-239">Yes for HDInsight Activity, Azure Machine Learning Batch Scoring Activity, Stored Procedure Activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-239">Yes for HDInsight Activity, Azure Machine Learning Batch Scoring Activity, Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="c65ce-240">No for all others</span><span class="sxs-lookup"><span data-stu-id="c65ce-240">No for all others</span></span>
<span data-ttu-id="c65ce-241">typeProperties</span><span class="sxs-lookup"><span data-stu-id="c65ce-241">typeProperties</span></span> | <span data-ttu-id="c65ce-242">Properties in the typeProperties section depend on each type of activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-242">Properties in the typeProperties section depend on each type of activity.</span></span> <span data-ttu-id="c65ce-243">To see type properties for an activity, click links to the activity in the previous section.</span><span class="sxs-lookup"><span data-stu-id="c65ce-243">To see type properties for an activity, click links to the activity in the previous section.</span></span> | <span data-ttu-id="c65ce-244">No</span><span class="sxs-lookup"><span data-stu-id="c65ce-244">No</span></span>
<span data-ttu-id="c65ce-245">policy</span><span class="sxs-lookup"><span data-stu-id="c65ce-245">policy</span></span> | <span data-ttu-id="c65ce-246">Policies that affect the run-time behavior of the activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-246">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="c65ce-247">This property includes timeout and retry behavior.</span><span class="sxs-lookup"><span data-stu-id="c65ce-247">This property includes timeout and retry behavior.</span></span> <span data-ttu-id="c65ce-248">If it is not specified, default values are used.</span><span class="sxs-lookup"><span data-stu-id="c65ce-248">If it is not specified, default values are used.</span></span> <span data-ttu-id="c65ce-249">For more information, see [Activity policy](#activity-policy) section.</span><span class="sxs-lookup"><span data-stu-id="c65ce-249">For more information, see [Activity policy](#activity-policy) section.</span></span> | <span data-ttu-id="c65ce-250">No</span><span class="sxs-lookup"><span data-stu-id="c65ce-250">No</span></span>
<span data-ttu-id="c65ce-251">dependsOn</span><span class="sxs-lookup"><span data-stu-id="c65ce-251">dependsOn</span></span> | <span data-ttu-id="c65ce-252">This property is used to define activity dependencies, and how subsequent activities depend on previous activities.</span><span class="sxs-lookup"><span data-stu-id="c65ce-252">This property is used to define activity dependencies, and how subsequent activities depend on previous activities.</span></span> <span data-ttu-id="c65ce-253">For more information, see [Activity dependency](#activity-dependency)</span><span class="sxs-lookup"><span data-stu-id="c65ce-253">For more information, see [Activity dependency](#activity-dependency)</span></span> | <span data-ttu-id="c65ce-254">No</span><span class="sxs-lookup"><span data-stu-id="c65ce-254">No</span></span>

### <a name="activity-policy"></a><span data-ttu-id="c65ce-255">Activity policy</span><span class="sxs-lookup"><span data-stu-id="c65ce-255">Activity policy</span></span>
<span data-ttu-id="c65ce-256">Policies affect the run-time behavior of an activity, giving configurability options.</span><span class="sxs-lookup"><span data-stu-id="c65ce-256">Policies affect the run-time behavior of an activity, giving configurability options.</span></span> <span data-ttu-id="c65ce-257">Activity Policies are only available for execution activities.</span><span class="sxs-lookup"><span data-stu-id="c65ce-257">Activity Policies are only available for execution activities.</span></span>

### <a name="activity-policy-json-definition"></a><span data-ttu-id="c65ce-258">Activity policy JSON definition</span><span class="sxs-lookup"><span data-stu-id="c65ce-258">Activity policy JSON definition</span></span>

```json
{
    "name": "MyPipelineName",
    "properties": {
      "activities": [
        {
          "name": "MyCopyBlobtoSqlActivity"
          "type": "Copy",
          "typeProperties": {
            ...
          },
         "policy": {
            "timeout": "00:10:00",
            "retry": 1,
            "retryIntervalInSeconds": 60,
            "secureOutput": true
         }
        }
      ],
        "parameters": {
           ...
        }
    }
}
```
<span data-ttu-id="c65ce-259">JSON name</span><span class="sxs-lookup"><span data-stu-id="c65ce-259">JSON name</span></span> | <span data-ttu-id="c65ce-260">Description</span><span class="sxs-lookup"><span data-stu-id="c65ce-260">Description</span></span> | <span data-ttu-id="c65ce-261">Allowed Values</span><span class="sxs-lookup"><span data-stu-id="c65ce-261">Allowed Values</span></span> | <span data-ttu-id="c65ce-262">Required</span><span class="sxs-lookup"><span data-stu-id="c65ce-262">Required</span></span>
--------- | ----------- | -------------- | --------
<span data-ttu-id="c65ce-263">timeout</span><span class="sxs-lookup"><span data-stu-id="c65ce-263">timeout</span></span> | <span data-ttu-id="c65ce-264">Specifies the timeout for the activity to run.</span><span class="sxs-lookup"><span data-stu-id="c65ce-264">Specifies the timeout for the activity to run.</span></span> | <span data-ttu-id="c65ce-265">Timespan</span><span class="sxs-lookup"><span data-stu-id="c65ce-265">Timespan</span></span> | <span data-ttu-id="c65ce-266">No.</span><span class="sxs-lookup"><span data-stu-id="c65ce-266">No.</span></span> <span data-ttu-id="c65ce-267">Default timeout is 7 days.</span><span class="sxs-lookup"><span data-stu-id="c65ce-267">Default timeout is 7 days.</span></span>
<span data-ttu-id="c65ce-268">retry</span><span class="sxs-lookup"><span data-stu-id="c65ce-268">retry</span></span> | <span data-ttu-id="c65ce-269">Maximum retry attempts</span><span class="sxs-lookup"><span data-stu-id="c65ce-269">Maximum retry attempts</span></span> | <span data-ttu-id="c65ce-270">Integer</span><span class="sxs-lookup"><span data-stu-id="c65ce-270">Integer</span></span> | <span data-ttu-id="c65ce-271">No.</span><span class="sxs-lookup"><span data-stu-id="c65ce-271">No.</span></span> <span data-ttu-id="c65ce-272">Default is 0</span><span class="sxs-lookup"><span data-stu-id="c65ce-272">Default is 0</span></span>
<span data-ttu-id="c65ce-273">retryIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="c65ce-273">retryIntervalInSeconds</span></span> | <span data-ttu-id="c65ce-274">The delay between retry attempts in seconds</span><span class="sxs-lookup"><span data-stu-id="c65ce-274">The delay between retry attempts in seconds</span></span> | <span data-ttu-id="c65ce-275">Integer</span><span class="sxs-lookup"><span data-stu-id="c65ce-275">Integer</span></span> | <span data-ttu-id="c65ce-276">No.</span><span class="sxs-lookup"><span data-stu-id="c65ce-276">No.</span></span> <span data-ttu-id="c65ce-277">Default is 20 seconds</span><span class="sxs-lookup"><span data-stu-id="c65ce-277">Default is 20 seconds</span></span>
<span data-ttu-id="c65ce-278">secureOutput</span><span class="sxs-lookup"><span data-stu-id="c65ce-278">secureOutput</span></span> | <span data-ttu-id="c65ce-279">When set to true, output from activity is considered as secure and will not be logged to monitoring.</span><span class="sxs-lookup"><span data-stu-id="c65ce-279">When set to true, output from activity is considered as secure and will not be logged to monitoring.</span></span> | <span data-ttu-id="c65ce-280">Boolean</span><span class="sxs-lookup"><span data-stu-id="c65ce-280">Boolean</span></span> | <span data-ttu-id="c65ce-281">No.</span><span class="sxs-lookup"><span data-stu-id="c65ce-281">No.</span></span> <span data-ttu-id="c65ce-282">Default is false.</span><span class="sxs-lookup"><span data-stu-id="c65ce-282">Default is false.</span></span>

### <a name="control-activity"></a><span data-ttu-id="c65ce-283">Control activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-283">Control activity</span></span>
<span data-ttu-id="c65ce-284">Control activities have the following top-level structure:</span><span class="sxs-lookup"><span data-stu-id="c65ce-284">Control activities have the following top-level structure:</span></span>

```json
{
    "name": "Control Activity Name",
    "description": "description",
    "type": "<ActivityType>",
    "typeProperties":
    {
    },
    "dependsOn":
    {
    }
}
```

<span data-ttu-id="c65ce-285">Tag</span><span class="sxs-lookup"><span data-stu-id="c65ce-285">Tag</span></span> | <span data-ttu-id="c65ce-286">Description</span><span class="sxs-lookup"><span data-stu-id="c65ce-286">Description</span></span> | <span data-ttu-id="c65ce-287">Required</span><span class="sxs-lookup"><span data-stu-id="c65ce-287">Required</span></span>
--- | ----------- | --------
<span data-ttu-id="c65ce-288">name</span><span class="sxs-lookup"><span data-stu-id="c65ce-288">name</span></span> | <span data-ttu-id="c65ce-289">Name of the activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-289">Name of the activity.</span></span> <span data-ttu-id="c65ce-290">Specify a name that represents the action that the activity performs.</span><span class="sxs-lookup"><span data-stu-id="c65ce-290">Specify a name that represents the action that the activity performs.</span></span><br/><ul><li><span data-ttu-id="c65ce-291">Maximum number of characters: 55</span><span class="sxs-lookup"><span data-stu-id="c65ce-291">Maximum number of characters: 55</span></span></li><li><span data-ttu-id="c65ce-292">Must start with a letter number, or an underscore (_)</span><span class="sxs-lookup"><span data-stu-id="c65ce-292">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="c65ce-293">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\”</span><span class="sxs-lookup"><span data-stu-id="c65ce-293">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”\*”,”%”,”&”,”:”,”\”</span></span> | <span data-ttu-id="c65ce-294">Yes</span><span class="sxs-lookup"><span data-stu-id="c65ce-294">Yes</span></span></li><ul>
<span data-ttu-id="c65ce-295">description</span><span class="sxs-lookup"><span data-stu-id="c65ce-295">description</span></span> | <span data-ttu-id="c65ce-296">Text describing what the activity or is used for</span><span class="sxs-lookup"><span data-stu-id="c65ce-296">Text describing what the activity or is used for</span></span> | <span data-ttu-id="c65ce-297">Yes</span><span class="sxs-lookup"><span data-stu-id="c65ce-297">Yes</span></span>
<span data-ttu-id="c65ce-298">type</span><span class="sxs-lookup"><span data-stu-id="c65ce-298">type</span></span> | <span data-ttu-id="c65ce-299">Type of the activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-299">Type of the activity.</span></span> <span data-ttu-id="c65ce-300">See the [data movement activities](#data-movement-activities), [data transformation activities](#data-transformation-activities), and [control activities](#control-activities) sections for different types of activities.</span><span class="sxs-lookup"><span data-stu-id="c65ce-300">See the [data movement activities](#data-movement-activities), [data transformation activities](#data-transformation-activities), and [control activities](#control-activities) sections for different types of activities.</span></span> | <span data-ttu-id="c65ce-301">Yes</span><span class="sxs-lookup"><span data-stu-id="c65ce-301">Yes</span></span>
<span data-ttu-id="c65ce-302">typeProperties</span><span class="sxs-lookup"><span data-stu-id="c65ce-302">typeProperties</span></span> | <span data-ttu-id="c65ce-303">Properties in the typeProperties section depend on each type of activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-303">Properties in the typeProperties section depend on each type of activity.</span></span> <span data-ttu-id="c65ce-304">To see type properties for an activity, click links to the activity in the previous section.</span><span class="sxs-lookup"><span data-stu-id="c65ce-304">To see type properties for an activity, click links to the activity in the previous section.</span></span> | <span data-ttu-id="c65ce-305">No</span><span class="sxs-lookup"><span data-stu-id="c65ce-305">No</span></span>
<span data-ttu-id="c65ce-306">dependsOn</span><span class="sxs-lookup"><span data-stu-id="c65ce-306">dependsOn</span></span> | <span data-ttu-id="c65ce-307">This property is used to define Activity Dependency, and how subsequent activities depend on previous activities.</span><span class="sxs-lookup"><span data-stu-id="c65ce-307">This property is used to define Activity Dependency, and how subsequent activities depend on previous activities.</span></span> <span data-ttu-id="c65ce-308">For more information, see [activity dependency](#activity-dependency).</span><span class="sxs-lookup"><span data-stu-id="c65ce-308">For more information, see [activity dependency](#activity-dependency).</span></span> | <span data-ttu-id="c65ce-309">No</span><span class="sxs-lookup"><span data-stu-id="c65ce-309">No</span></span>

### <a name="activity-dependency"></a><span data-ttu-id="c65ce-310">Activity dependency</span><span class="sxs-lookup"><span data-stu-id="c65ce-310">Activity dependency</span></span>
<span data-ttu-id="c65ce-311">Activity Dependency defines how subsequent activities depend on previous activities, determining the condition whether to continue executing the next task.</span><span class="sxs-lookup"><span data-stu-id="c65ce-311">Activity Dependency defines how subsequent activities depend on previous activities, determining the condition whether to continue executing the next task.</span></span> <span data-ttu-id="c65ce-312">An activity can depend on one or multiple previous activities with different dependency conditions.</span><span class="sxs-lookup"><span data-stu-id="c65ce-312">An activity can depend on one or multiple previous activities with different dependency conditions.</span></span>

<span data-ttu-id="c65ce-313">The different dependency conditions are: Succeeded, Failed, Skipped, Completed.</span><span class="sxs-lookup"><span data-stu-id="c65ce-313">The different dependency conditions are: Succeeded, Failed, Skipped, Completed.</span></span>

<span data-ttu-id="c65ce-314">For example, if a pipeline has Activity A -> Activity B, the different scenarios that can happen are:</span><span class="sxs-lookup"><span data-stu-id="c65ce-314">For example, if a pipeline has Activity A -> Activity B, the different scenarios that can happen are:</span></span>

- <span data-ttu-id="c65ce-315">Activity B has dependency condition on Activity A with **succeeded**: Activity B only runs if Activity A has a final status of succeeded</span><span class="sxs-lookup"><span data-stu-id="c65ce-315">Activity B has dependency condition on Activity A with **succeeded**: Activity B only runs if Activity A has a final status of succeeded</span></span>
- <span data-ttu-id="c65ce-316">Activity B has dependency condition on Activity A with **failed**: Activity B only runs if Activity A has a final status of failed</span><span class="sxs-lookup"><span data-stu-id="c65ce-316">Activity B has dependency condition on Activity A with **failed**: Activity B only runs if Activity A has a final status of failed</span></span>
- <span data-ttu-id="c65ce-317">Activity B has dependency condition on Activity A with **completed**: Activity B runs if Activity A has a final status of succeeded or failed</span><span class="sxs-lookup"><span data-stu-id="c65ce-317">Activity B has dependency condition on Activity A with **completed**: Activity B runs if Activity A has a final status of succeeded or failed</span></span>
- <span data-ttu-id="c65ce-318">Activity B has dependency condition on Activity A with **skipped**: Activity B runs if Activity A has a final status of skipped.</span><span class="sxs-lookup"><span data-stu-id="c65ce-318">Activity B has dependency condition on Activity A with **skipped**: Activity B runs if Activity A has a final status of skipped.</span></span> <span data-ttu-id="c65ce-319">Skipped occurs in the scenario of Activity X -> Activity Y -> Activity Z, where each activity runs only if the previous activity succeeds.</span><span class="sxs-lookup"><span data-stu-id="c65ce-319">Skipped occurs in the scenario of Activity X -> Activity Y -> Activity Z, where each activity runs only if the previous activity succeeds.</span></span> <span data-ttu-id="c65ce-320">If Activity X fails, then Activity Y has a status of “Skipped” because it never executes.</span><span class="sxs-lookup"><span data-stu-id="c65ce-320">If Activity X fails, then Activity Y has a status of “Skipped” because it never executes.</span></span> <span data-ttu-id="c65ce-321">Similarly, Activity Z has a status of “Skipped” as well.</span><span class="sxs-lookup"><span data-stu-id="c65ce-321">Similarly, Activity Z has a status of “Skipped” as well.</span></span>

#### <a name="example-activity-2-depends-on-the-activity-1-succeeding"></a><span data-ttu-id="c65ce-322">Example: Activity 2 depends on the Activity 1 succeeding</span><span class="sxs-lookup"><span data-stu-id="c65ce-322">Example: Activity 2 depends on the Activity 1 succeeding</span></span>

```json
{
    "name": "PipelineName",
    "properties":
    {
        "description": "pipeline description",
        "activities": [
         {
            "name": "MyFirstActivity",
            "type": "Copy",
            "typeProperties": {
            },
            "linkedServiceName": {
            }
        },
        {
            "name": "MySecondActivity",
            "type": "Copy",
            "typeProperties": {
            },
            "linkedServiceName": {
            },
            "dependsOn": [
            {
                "activity": "MyFirstActivity",
                "dependencyConditions": [
                    "Succeeded"
                ]
            }
          ]
        }
      ],
      "parameters": {
       }
    }
}

```

## <a name="sample-copy-pipeline"></a><span data-ttu-id="c65ce-323">Sample copy pipeline</span><span class="sxs-lookup"><span data-stu-id="c65ce-323">Sample copy pipeline</span></span>
<span data-ttu-id="c65ce-324">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span><span class="sxs-lookup"><span data-stu-id="c65ce-324">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="c65ce-325">In this sample, the [copy activity](copy-activity-overview.md) copies data from an Azure Blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c65ce-325">In this sample, the [copy activity](copy-activity-overview.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span>

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "policy": {
          "retry": 2,
          "timeout": "01:00:00"
        }
      }
    ]
  }
}
```
<span data-ttu-id="c65ce-326">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="c65ce-326">Note the following points:</span></span>

- <span data-ttu-id="c65ce-327">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="c65ce-327">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
- <span data-ttu-id="c65ce-328">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c65ce-328">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> <span data-ttu-id="c65ce-329">See [Datasets](concepts-datasets-linked-services.md) article for defining datasets in JSON.</span><span class="sxs-lookup"><span data-stu-id="c65ce-329">See [Datasets](concepts-datasets-linked-services.md) article for defining datasets in JSON.</span></span>
- <span data-ttu-id="c65ce-330">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="c65ce-330">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="c65ce-331">In the [data movement activities](#data-movement-activities) section, click the data store that you want to use as a source or a sink to learn more about moving data to/from that data store.</span><span class="sxs-lookup"><span data-stu-id="c65ce-331">In the [data movement activities](#data-movement-activities) section, click the data store that you want to use as a source or a sink to learn more about moving data to/from that data store.</span></span>

<span data-ttu-id="c65ce-332">For a complete walkthrough of creating this pipeline, see [Quickstart: create a data factory](quickstart-create-data-factory-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c65ce-332">For a complete walkthrough of creating this pipeline, see [Quickstart: create a data factory](quickstart-create-data-factory-powershell.md).</span></span>

## <a name="sample-transformation-pipeline"></a><span data-ttu-id="c65ce-333">Sample transformation pipeline</span><span class="sxs-lookup"><span data-stu-id="c65ce-333">Sample transformation pipeline</span></span>
<span data-ttu-id="c65ce-334">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span><span class="sxs-lookup"><span data-stu-id="c65ce-334">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="c65ce-335">In this sample, the [HDInsight Hive activity](transform-data-using-hadoop-hive.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="c65ce-335">In this sample, the [HDInsight Hive activity](transform-data-using-hadoop-hive.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span>

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
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
                "policy": {
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ]
    }
}
```
<span data-ttu-id="c65ce-336">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="c65ce-336">Note the following points:</span></span>

- <span data-ttu-id="c65ce-337">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="c65ce-337">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
- <span data-ttu-id="c65ce-338">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called AzureStorageLinkedService), and in script folder in the container `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="c65ce-338">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called AzureStorageLinkedService), and in script folder in the container `adfgetstarted`.</span></span>
- <span data-ttu-id="c65ce-339">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (for example, $`{hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="c65ce-339">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (for example, $`{hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="c65ce-340">The **typeProperties** section is different for each transformation activity.</span><span class="sxs-lookup"><span data-stu-id="c65ce-340">The **typeProperties** section is different for each transformation activity.</span></span> <span data-ttu-id="c65ce-341">To learn about type properties supported for a transformation activity, click the transformation activity in the [Data transformation activities](#data-transformation-activities).</span><span class="sxs-lookup"><span data-stu-id="c65ce-341">To learn about type properties supported for a transformation activity, click the transformation activity in the [Data transformation activities](#data-transformation-activities).</span></span>

<span data-ttu-id="c65ce-342">For a complete walkthrough of creating this pipeline, see [Tutorial: transform data using Spark](tutorial-transform-data-spark-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c65ce-342">For a complete walkthrough of creating this pipeline, see [Tutorial: transform data using Spark](tutorial-transform-data-spark-powershell.md).</span></span>

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="c65ce-343">Multiple activities in a pipeline</span><span class="sxs-lookup"><span data-stu-id="c65ce-343">Multiple activities in a pipeline</span></span>
<span data-ttu-id="c65ce-344">The previous two sample pipelines have only one activity in them.</span><span class="sxs-lookup"><span data-stu-id="c65ce-344">The previous two sample pipelines have only one activity in them.</span></span> <span data-ttu-id="c65ce-345">You can have more than one activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c65ce-345">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="c65ce-346">If you have multiple activities in a pipeline and subsequent activities are not dependent on previous activities, the activities may run in parallel.</span><span class="sxs-lookup"><span data-stu-id="c65ce-346">If you have multiple activities in a pipeline and subsequent activities are not dependent on previous activities, the activities may run in parallel.</span></span>

<span data-ttu-id="c65ce-347">You can chain two activities by using [activity dependency](#activity-dependency), which defines how subsequent activities depend on previous activities, determining the condition whether to continue executing the next task.</span><span class="sxs-lookup"><span data-stu-id="c65ce-347">You can chain two activities by using [activity dependency](#activity-dependency), which defines how subsequent activities depend on previous activities, determining the condition whether to continue executing the next task.</span></span> <span data-ttu-id="c65ce-348">An activity can depend on one or more previous activities with different dependency conditions.</span><span class="sxs-lookup"><span data-stu-id="c65ce-348">An activity can depend on one or more previous activities with different dependency conditions.</span></span>

## <a name="scheduling-pipelines"></a><span data-ttu-id="c65ce-349">Scheduling pipelines</span><span class="sxs-lookup"><span data-stu-id="c65ce-349">Scheduling pipelines</span></span>
<span data-ttu-id="c65ce-350">Pipelines are scheduled by triggers.</span><span class="sxs-lookup"><span data-stu-id="c65ce-350">Pipelines are scheduled by triggers.</span></span> <span data-ttu-id="c65ce-351">There are different types of triggers (scheduler trigger, which allows pipelines to be triggered on a wall-clock schedule, as well as manual trigger, which triggers pipelines on-demand).</span><span class="sxs-lookup"><span data-stu-id="c65ce-351">There are different types of triggers (scheduler trigger, which allows pipelines to be triggered on a wall-clock schedule, as well as manual trigger, which triggers pipelines on-demand).</span></span> <span data-ttu-id="c65ce-352">For more information about triggers, see [pipeline execution and triggers](concepts-pipeline-execution-triggers.md) article.</span><span class="sxs-lookup"><span data-stu-id="c65ce-352">For more information about triggers, see [pipeline execution and triggers](concepts-pipeline-execution-triggers.md) article.</span></span>

<span data-ttu-id="c65ce-353">To have your trigger kick off a pipeline run, you must include a pipeline reference of the particular pipeline in the trigger definition.</span><span class="sxs-lookup"><span data-stu-id="c65ce-353">To have your trigger kick off a pipeline run, you must include a pipeline reference of the particular pipeline in the trigger definition.</span></span> <span data-ttu-id="c65ce-354">Pipelines & triggers have an n-m relationship.</span><span class="sxs-lookup"><span data-stu-id="c65ce-354">Pipelines & triggers have an n-m relationship.</span></span> <span data-ttu-id="c65ce-355">Multiple triggers can kick off a single pipeline and the same trigger can kick off multiple pipelines.</span><span class="sxs-lookup"><span data-stu-id="c65ce-355">Multiple triggers can kick off a single pipeline and the same trigger can kick off multiple pipelines.</span></span> <span data-ttu-id="c65ce-356">Once the trigger is defined, you must start the trigger to have it start triggering the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c65ce-356">Once the trigger is defined, you must start the trigger to have it start triggering the pipeline.</span></span> <span data-ttu-id="c65ce-357">For more information about triggers, see [pipeline execution and triggers](concepts-pipeline-execution-triggers.md) article.</span><span class="sxs-lookup"><span data-stu-id="c65ce-357">For more information about triggers, see [pipeline execution and triggers](concepts-pipeline-execution-triggers.md) article.</span></span>

<span data-ttu-id="c65ce-358">For example, say you have a scheduler trigger, “Trigger A” that I wish to kick off my pipeline, “MyCopyPipeline.”</span><span class="sxs-lookup"><span data-stu-id="c65ce-358">For example, say you have a scheduler trigger, “Trigger A” that I wish to kick off my pipeline, “MyCopyPipeline.”</span></span> <span data-ttu-id="c65ce-359">You define the trigger as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c65ce-359">You define the trigger as shown in the following example:</span></span>

### <a name="trigger-a-definition"></a><span data-ttu-id="c65ce-360">Trigger A definition</span><span class="sxs-lookup"><span data-stu-id="c65ce-360">Trigger A definition</span></span>

```json
{
  "name": "TriggerA",
  "properties": {
    "type": "ScheduleTrigger",
    "typeProperties": {
      ...
      }
    },
    "pipeline": {
      "pipelineReference": {
        "type": "PipelineReference",
        "referenceName": "MyCopyPipeline"
      },
      "parameters": {
        "copySourceName": "FileSource"
      }
    }
  }
}
```



## <a name="next-steps"></a><span data-ttu-id="c65ce-361">Next steps</span><span class="sxs-lookup"><span data-stu-id="c65ce-361">Next steps</span></span>
<span data-ttu-id="c65ce-362">See the following tutorials for step-by-step instructions for creating pipelines with activities:</span><span class="sxs-lookup"><span data-stu-id="c65ce-362">See the following tutorials for step-by-step instructions for creating pipelines with activities:</span></span>

- [<span data-ttu-id="c65ce-363">Build a pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-363">Build a pipeline with a copy activity</span></span>](quickstart-create-data-factory-powershell.md)
- [<span data-ttu-id="c65ce-364">Build a pipeline with a data transformation activity</span><span class="sxs-lookup"><span data-stu-id="c65ce-364">Build a pipeline with a data transformation activity</span></span>](tutorial-transform-data-spark-powershell.md)
