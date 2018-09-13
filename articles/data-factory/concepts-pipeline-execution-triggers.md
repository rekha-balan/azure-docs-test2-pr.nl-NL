---
title: Pipeline execution and triggers in Azure Data Factory | Microsoft Docs
description: This article provides information about how to execute a pipeline in Azure Data Factory, either on-demand or by creating a trigger.
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
ms.date: 07/05/2018
ms.author: shlo
ms.openlocfilehash: 8dfc2448861ca9b376246ac42f7563e44422d6de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869812"
---
# <a name="pipeline-execution-and-triggers-in-azure-data-factory"></a><span data-ttu-id="ffd72-103">Pipeline execution and triggers in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ffd72-103">Pipeline execution and triggers in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of the Data Factory service that you're using:"]
> * [Version 1](v1/data-factory-scheduling-and-execution.md)
> * [Current version](concepts-pipeline-execution-triggers.md)

<span data-ttu-id="ffd72-106">A _pipeline run_ in Azure Data Factory defines an instance of a pipeline execution.</span><span class="sxs-lookup"><span data-stu-id="ffd72-106">A _pipeline run_ in Azure Data Factory defines an instance of a pipeline execution.</span></span> <span data-ttu-id="ffd72-107">For example, say you have a pipeline that executes at 8:00 AM, 9:00 AM, and 10:00 AM.</span><span class="sxs-lookup"><span data-stu-id="ffd72-107">For example, say you have a pipeline that executes at 8:00 AM, 9:00 AM, and 10:00 AM.</span></span> <span data-ttu-id="ffd72-108">In this case, there are three separate runs of the pipeline, or pipeline runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-108">In this case, there are three separate runs of the pipeline, or pipeline runs.</span></span> <span data-ttu-id="ffd72-109">Each pipeline run has a unique pipeline run ID.</span><span class="sxs-lookup"><span data-stu-id="ffd72-109">Each pipeline run has a unique pipeline run ID.</span></span> <span data-ttu-id="ffd72-110">A run ID is a GUID that uniquely defines that particular pipeline run.</span><span class="sxs-lookup"><span data-stu-id="ffd72-110">A run ID is a GUID that uniquely defines that particular pipeline run.</span></span> 

<span data-ttu-id="ffd72-111">Pipeline runs are typically instantiated by passing arguments to parameters that you define in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="ffd72-111">Pipeline runs are typically instantiated by passing arguments to parameters that you define in the pipeline.</span></span> <span data-ttu-id="ffd72-112">You can execute a pipeline either manually or by using a _trigger_.</span><span class="sxs-lookup"><span data-stu-id="ffd72-112">You can execute a pipeline either manually or by using a _trigger_.</span></span> <span data-ttu-id="ffd72-113">This article provides details about both ways of executing a pipeline.</span><span class="sxs-lookup"><span data-stu-id="ffd72-113">This article provides details about both ways of executing a pipeline.</span></span>

## <a name="manual-execution-on-demand"></a><span data-ttu-id="ffd72-114">Manual execution (on-demand)</span><span class="sxs-lookup"><span data-stu-id="ffd72-114">Manual execution (on-demand)</span></span>
<span data-ttu-id="ffd72-115">The manual execution of a pipeline is also referred to as _on-demand_ execution.</span><span class="sxs-lookup"><span data-stu-id="ffd72-115">The manual execution of a pipeline is also referred to as _on-demand_ execution.</span></span>

<span data-ttu-id="ffd72-116">For example, say you have a basic pipeline named **copyPipeline** that you want to execute.</span><span class="sxs-lookup"><span data-stu-id="ffd72-116">For example, say you have a basic pipeline named **copyPipeline** that you want to execute.</span></span> <span data-ttu-id="ffd72-117">The pipeline has a single activity that copies from an Azure Blob storage source folder to a destination folder in the same storage.</span><span class="sxs-lookup"><span data-stu-id="ffd72-117">The pipeline has a single activity that copies from an Azure Blob storage source folder to a destination folder in the same storage.</span></span> <span data-ttu-id="ffd72-118">The following JSON definition shows this sample pipeline:</span><span class="sxs-lookup"><span data-stu-id="ffd72-118">The following JSON definition shows this sample pipeline:</span></span>

```json
{
  "name": "copyPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
        "name": "CopyBlobtoBlob",
        "inputs": [
          {
            "referenceName": "sourceBlobDataset",
            "type": "DatasetReference"
          }
        ],
        "outputs": [
          {
            "referenceName": "sinkBlobDataset",
            "type": "DatasetReference"
          }
        ]
      }
    ],
    "parameters": {
      "sourceBlobContainer": {
        "type": "String"
      },
      "sinkBlobContainer": {
        "type": "String"
      }
    }
  }
}
```

<span data-ttu-id="ffd72-119">In the JSON definition, the pipeline takes two parameters: **sourceBlobContainer** and **sinkBlobContainer**.</span><span class="sxs-lookup"><span data-stu-id="ffd72-119">In the JSON definition, the pipeline takes two parameters: **sourceBlobContainer** and **sinkBlobContainer**.</span></span> <span data-ttu-id="ffd72-120">You pass values to these parameters at runtime.</span><span class="sxs-lookup"><span data-stu-id="ffd72-120">You pass values to these parameters at runtime.</span></span>

<span data-ttu-id="ffd72-121">You can manually run your pipeline by using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="ffd72-121">You can manually run your pipeline by using one of the following methods:</span></span>
- <span data-ttu-id="ffd72-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="ffd72-122">.NET SDK</span></span>
- <span data-ttu-id="ffd72-123">Azure PowerShell module</span><span class="sxs-lookup"><span data-stu-id="ffd72-123">Azure PowerShell module</span></span>
- <span data-ttu-id="ffd72-124">REST API</span><span class="sxs-lookup"><span data-stu-id="ffd72-124">REST API</span></span>
- <span data-ttu-id="ffd72-125">Python SDK</span><span class="sxs-lookup"><span data-stu-id="ffd72-125">Python SDK</span></span>

### <a name="rest-api"></a><span data-ttu-id="ffd72-126">REST API</span><span class="sxs-lookup"><span data-stu-id="ffd72-126">REST API</span></span>
<span data-ttu-id="ffd72-127">The following sample command shows you how to manually run your pipeline by using the REST API:</span><span class="sxs-lookup"><span data-stu-id="ffd72-127">The following sample command shows you how to manually run your pipeline by using the REST API:</span></span>  

```
POST
https://management.azure.com/subscriptions/mySubId/resourceGroups/myResourceGroup/providers/Microsoft.DataFactory/factories/myDataFactory/pipelines/copyPipeline/createRun?api-version=2017-03-01-preview
```

<span data-ttu-id="ffd72-128">For a complete sample, see [Quickstart: Create a data factory by using the REST API](quickstart-create-data-factory-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="ffd72-128">For a complete sample, see [Quickstart: Create a data factory by using the REST API](quickstart-create-data-factory-rest-api.md).</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="ffd72-129">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffd72-129">Azure PowerShell</span></span>
<span data-ttu-id="ffd72-130">The following sample command shows you how to manually run your pipeline by using Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ffd72-130">The following sample command shows you how to manually run your pipeline by using Azure PowerShell:</span></span>

```powershell
Invoke-AzureRmDataFactoryV2Pipeline -DataFactory $df -PipelineName "Adfv2QuickStartPipeline" -ParameterFile .\PipelineParameters.json
```

<span data-ttu-id="ffd72-131">You pass parameters in the body of the request payload.</span><span class="sxs-lookup"><span data-stu-id="ffd72-131">You pass parameters in the body of the request payload.</span></span> <span data-ttu-id="ffd72-132">In the .NET SDK, Azure PowerShell, and the Python SDK, you pass values in a dictionary that's passed as an argument to the call:</span><span class="sxs-lookup"><span data-stu-id="ffd72-132">In the .NET SDK, Azure PowerShell, and the Python SDK, you pass values in a dictionary that's passed as an argument to the call:</span></span>

```json
{
  "sourceBlobContainer": "MySourceFolder",
  "sinkBlobCountainer": "MySinkFolder"
}
```

<span data-ttu-id="ffd72-133">The response payload is a unique ID of the pipeline run:</span><span class="sxs-lookup"><span data-stu-id="ffd72-133">The response payload is a unique ID of the pipeline run:</span></span>

```json
{
  "runId": "0448d45a-a0bd-23f3-90a5-bfeea9264aed"
}
```

<span data-ttu-id="ffd72-134">For a complete sample, see [Quickstart: Create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ffd72-134">For a complete sample, see [Quickstart: Create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span></span>

### <a name="net-sdk"></a><span data-ttu-id="ffd72-135">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="ffd72-135">.NET SDK</span></span>
<span data-ttu-id="ffd72-136">The following sample call shows you how to manually run your pipeline by using the .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="ffd72-136">The following sample call shows you how to manually run your pipeline by using the .NET SDK:</span></span>

```csharp
client.Pipelines.CreateRunWithHttpMessagesAsync(resourceGroup, dataFactoryName, pipelineName, parameters)
```

<span data-ttu-id="ffd72-137">For a complete sample, see [Quickstart: Create a data factory by using the .NET SDK](quickstart-create-data-factory-dot-net.md).</span><span class="sxs-lookup"><span data-stu-id="ffd72-137">For a complete sample, see [Quickstart: Create a data factory by using the .NET SDK](quickstart-create-data-factory-dot-net.md).</span></span>

> [!NOTE]
> You can use the .NET SDK to invoke Data Factory pipelines from Azure Functions, from your own web services, and so on.

<h2 id="triggers"><span data-ttu-id="ffd72-139">Trigger execution</span><span class="sxs-lookup"><span data-stu-id="ffd72-139">Trigger execution</span></span></h2>
<span data-ttu-id="ffd72-140">Triggers are another way that you can execute a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="ffd72-140">Triggers are another way that you can execute a pipeline run.</span></span> <span data-ttu-id="ffd72-141">Triggers represent a unit of processing that determines when a pipeline execution needs to be kicked off.</span><span class="sxs-lookup"><span data-stu-id="ffd72-141">Triggers represent a unit of processing that determines when a pipeline execution needs to be kicked off.</span></span> <span data-ttu-id="ffd72-142">Currently, Data Factory supports three types of triggers:</span><span class="sxs-lookup"><span data-stu-id="ffd72-142">Currently, Data Factory supports three types of triggers:</span></span>

- <span data-ttu-id="ffd72-143">Schedule trigger: A trigger that invokes a pipeline on a wall-clock schedule.</span><span class="sxs-lookup"><span data-stu-id="ffd72-143">Schedule trigger: A trigger that invokes a pipeline on a wall-clock schedule.</span></span>

- <span data-ttu-id="ffd72-144">Tumbling window trigger: A trigger that operates on a periodic interval, while also retaining state.</span><span class="sxs-lookup"><span data-stu-id="ffd72-144">Tumbling window trigger: A trigger that operates on a periodic interval, while also retaining state.</span></span>

- <span data-ttu-id="ffd72-145">Event-based trigger: A trigger that responds to an event.</span><span class="sxs-lookup"><span data-stu-id="ffd72-145">Event-based trigger: A trigger that responds to an event.</span></span>

<span data-ttu-id="ffd72-146">Pipelines and triggers have a many-to-many relationship.</span><span class="sxs-lookup"><span data-stu-id="ffd72-146">Pipelines and triggers have a many-to-many relationship.</span></span> <span data-ttu-id="ffd72-147">Multiple triggers can kick off a single pipeline, or a single trigger can kick off multiple pipelines.</span><span class="sxs-lookup"><span data-stu-id="ffd72-147">Multiple triggers can kick off a single pipeline, or a single trigger can kick off multiple pipelines.</span></span> <span data-ttu-id="ffd72-148">In the following trigger definition, the **pipelines** property refers to a list of pipelines that are triggered by the particular trigger.</span><span class="sxs-lookup"><span data-stu-id="ffd72-148">In the following trigger definition, the **pipelines** property refers to a list of pipelines that are triggered by the particular trigger.</span></span> <span data-ttu-id="ffd72-149">The property definition includes values for the pipeline parameters.</span><span class="sxs-lookup"><span data-stu-id="ffd72-149">The property definition includes values for the pipeline parameters.</span></span>

### <a name="basic-trigger-definition"></a><span data-ttu-id="ffd72-150">Basic trigger definition</span><span class="sxs-lookup"><span data-stu-id="ffd72-150">Basic trigger definition</span></span>

```json
    "properties": {
        "name": "MyTrigger",
        "type": "<type of trigger>",
        "typeProperties": {
            …
        },
        "pipelines": [
            {
                "pipelineReference": {
                    "type": "PipelineReference",
                    "referenceName": "<Name of your pipeline>"
                },
                "parameters": {
                    "<parameter 1 Name>": {
                        "type": "Expression",
                          "value": "<parameter 1 Value>"
                    },
                    "<parameter 2 Name>" : "<parameter 2 Value>"
                }
            }
        ]
    }
```

## <a name="schedule-trigger"></a><span data-ttu-id="ffd72-151">Schedule trigger</span><span class="sxs-lookup"><span data-stu-id="ffd72-151">Schedule trigger</span></span>
<span data-ttu-id="ffd72-152">A schedule trigger runs pipelines on a wall-clock schedule.</span><span class="sxs-lookup"><span data-stu-id="ffd72-152">A schedule trigger runs pipelines on a wall-clock schedule.</span></span> <span data-ttu-id="ffd72-153">This trigger supports periodic and advanced calendar options.</span><span class="sxs-lookup"><span data-stu-id="ffd72-153">This trigger supports periodic and advanced calendar options.</span></span> <span data-ttu-id="ffd72-154">For example, the trigger supports intervals like "weekly" or "Monday at 5:00 PM and Thursday at 9:00 PM."</span><span class="sxs-lookup"><span data-stu-id="ffd72-154">For example, the trigger supports intervals like "weekly" or "Monday at 5:00 PM and Thursday at 9:00 PM."</span></span> <span data-ttu-id="ffd72-155">The schedule trigger is flexible because the dataset pattern is agnostic, and the trigger doesn't discern between time-series and non-time-series data.</span><span class="sxs-lookup"><span data-stu-id="ffd72-155">The schedule trigger is flexible because the dataset pattern is agnostic, and the trigger doesn't discern between time-series and non-time-series data.</span></span>

<span data-ttu-id="ffd72-156">For more information about schedule triggers and for examples, see [Create a schedule trigger](how-to-create-schedule-trigger.md).</span><span class="sxs-lookup"><span data-stu-id="ffd72-156">For more information about schedule triggers and for examples, see [Create a schedule trigger](how-to-create-schedule-trigger.md).</span></span>

## <a name="schedule-trigger-definition"></a><span data-ttu-id="ffd72-157">Schedule trigger definition</span><span class="sxs-lookup"><span data-stu-id="ffd72-157">Schedule trigger definition</span></span>
<span data-ttu-id="ffd72-158">When you create a schedule trigger, you specify scheduling and recurrence by using a JSON definition.</span><span class="sxs-lookup"><span data-stu-id="ffd72-158">When you create a schedule trigger, you specify scheduling and recurrence by using a JSON definition.</span></span> 

<span data-ttu-id="ffd72-159">To have your schedule trigger kick off a pipeline run, include a pipeline reference of the particular pipeline in the trigger definition.</span><span class="sxs-lookup"><span data-stu-id="ffd72-159">To have your schedule trigger kick off a pipeline run, include a pipeline reference of the particular pipeline in the trigger definition.</span></span> <span data-ttu-id="ffd72-160">Pipelines and triggers have a many-to-many relationship.</span><span class="sxs-lookup"><span data-stu-id="ffd72-160">Pipelines and triggers have a many-to-many relationship.</span></span> <span data-ttu-id="ffd72-161">Multiple triggers can kick off a single pipeline.</span><span class="sxs-lookup"><span data-stu-id="ffd72-161">Multiple triggers can kick off a single pipeline.</span></span> <span data-ttu-id="ffd72-162">A single trigger can kick off multiple pipelines.</span><span class="sxs-lookup"><span data-stu-id="ffd72-162">A single trigger can kick off multiple pipelines.</span></span>

```json
{
  "properties": {
    "type": "ScheduleTrigger",
    "typeProperties": {
      "recurrence": {
        "frequency": <<Minute, Hour, Day, Week, Year>>,
        "interval": <<int>>,             // How often to fire
        "startTime": <<datetime>>,
        "endTime": <<datetime>>,
        "timeZone": "UTC"
        "schedule": {                    // Optional (advanced scheduling specifics)
          "hours": [<<0-24>>],
          "weekDays": ": [<<Monday-Sunday>>],
          "minutes": [<<0-60>>],
          "monthDays": [<<1-31>>],
          "monthlyOccurences": [
               {
                    "day": <<Monday-Sunday>>,
                    "occurrence": <<1-5>>
               }
           ] 
        }
      }
    },
   "pipelines": [
            {
                "pipelineReference": {
                    "type": "PipelineReference",
                    "referenceName": "<Name of your pipeline>"
                },
                "parameters": {
                    "<parameter 1 Name>": {
                        "type": "Expression",
                        "value": "<parameter 1 Value>"
                    },
                    "<parameter 2 Name>" : "<parameter 2 Value>"
                }
           }
      ]
  }
}
```

> [!IMPORTANT]
> The **parameters** property is a mandatory property of the **pipelines** element. If your pipeline doesn't take any parameters, you must include an empty JSON definition for the **parameters** property.

### <a name="schema-overview"></a><span data-ttu-id="ffd72-165">Schema overview</span><span class="sxs-lookup"><span data-stu-id="ffd72-165">Schema overview</span></span>
<span data-ttu-id="ffd72-166">The following table provides a high-level overview of the major schema elements that are related to recurrence and scheduling a trigger:</span><span class="sxs-lookup"><span data-stu-id="ffd72-166">The following table provides a high-level overview of the major schema elements that are related to recurrence and scheduling a trigger:</span></span>

| <span data-ttu-id="ffd72-167">JSON property</span><span class="sxs-lookup"><span data-stu-id="ffd72-167">JSON property</span></span> | <span data-ttu-id="ffd72-168">Description</span><span class="sxs-lookup"><span data-stu-id="ffd72-168">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ffd72-169">**startTime**</span><span class="sxs-lookup"><span data-stu-id="ffd72-169">**startTime**</span></span> | <span data-ttu-id="ffd72-170">A date-time value.</span><span class="sxs-lookup"><span data-stu-id="ffd72-170">A date-time value.</span></span> <span data-ttu-id="ffd72-171">For basic schedules, the value of the **startTime** property applies to the first occurrence.</span><span class="sxs-lookup"><span data-stu-id="ffd72-171">For basic schedules, the value of the **startTime** property applies to the first occurrence.</span></span> <span data-ttu-id="ffd72-172">For complex schedules, the trigger starts no sooner than the specified **startTime** value.</span><span class="sxs-lookup"><span data-stu-id="ffd72-172">For complex schedules, the trigger starts no sooner than the specified **startTime** value.</span></span> |
| <span data-ttu-id="ffd72-173">**endTime**</span><span class="sxs-lookup"><span data-stu-id="ffd72-173">**endTime**</span></span> | <span data-ttu-id="ffd72-174">The end date and time for the trigger.</span><span class="sxs-lookup"><span data-stu-id="ffd72-174">The end date and time for the trigger.</span></span> <span data-ttu-id="ffd72-175">The trigger doesn't execute after the specified end date and time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-175">The trigger doesn't execute after the specified end date and time.</span></span> <span data-ttu-id="ffd72-176">The value for the property can't be in the past.</span><span class="sxs-lookup"><span data-stu-id="ffd72-176">The value for the property can't be in the past.</span></span> <!-- This property is optional. --> |
| <span data-ttu-id="ffd72-177">**timeZone**</span><span class="sxs-lookup"><span data-stu-id="ffd72-177">**timeZone**</span></span> | <span data-ttu-id="ffd72-178">The time zone.</span><span class="sxs-lookup"><span data-stu-id="ffd72-178">The time zone.</span></span> <span data-ttu-id="ffd72-179">Currently, only the UTC time zone is supported.</span><span class="sxs-lookup"><span data-stu-id="ffd72-179">Currently, only the UTC time zone is supported.</span></span> |
| <span data-ttu-id="ffd72-180">**recurrence**</span><span class="sxs-lookup"><span data-stu-id="ffd72-180">**recurrence**</span></span> | <span data-ttu-id="ffd72-181">A recurrence object that specifies the recurrence rules for the trigger.</span><span class="sxs-lookup"><span data-stu-id="ffd72-181">A recurrence object that specifies the recurrence rules for the trigger.</span></span> <span data-ttu-id="ffd72-182">The recurrence object supports the **frequency**, **interval**, **endTime**, **count**, and **schedule** elements.</span><span class="sxs-lookup"><span data-stu-id="ffd72-182">The recurrence object supports the **frequency**, **interval**, **endTime**, **count**, and **schedule** elements.</span></span> <span data-ttu-id="ffd72-183">When a recurrence object is defined, the **frequency** element is required.</span><span class="sxs-lookup"><span data-stu-id="ffd72-183">When a recurrence object is defined, the **frequency** element is required.</span></span> <span data-ttu-id="ffd72-184">The other elements of the recurrence object are optional.</span><span class="sxs-lookup"><span data-stu-id="ffd72-184">The other elements of the recurrence object are optional.</span></span> |
| <span data-ttu-id="ffd72-185">**frequency**</span><span class="sxs-lookup"><span data-stu-id="ffd72-185">**frequency**</span></span> | <span data-ttu-id="ffd72-186">The unit of frequency at which the trigger recurs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-186">The unit of frequency at which the trigger recurs.</span></span> <span data-ttu-id="ffd72-187">The supported values include "minute", "hour", "day", "week", and "month".</span><span class="sxs-lookup"><span data-stu-id="ffd72-187">The supported values include "minute", "hour", "day", "week", and "month".</span></span> |
| <span data-ttu-id="ffd72-188">**interval**</span><span class="sxs-lookup"><span data-stu-id="ffd72-188">**interval**</span></span> | <span data-ttu-id="ffd72-189">A positive integer that denotes the interval for the **frequency** value.</span><span class="sxs-lookup"><span data-stu-id="ffd72-189">A positive integer that denotes the interval for the **frequency** value.</span></span> <span data-ttu-id="ffd72-190">The **frequency** value determines how often the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-190">The **frequency** value determines how often the trigger runs.</span></span> <span data-ttu-id="ffd72-191">For example, if the **interval** is 3 and the **frequency** is "week", the trigger recurs every three weeks.</span><span class="sxs-lookup"><span data-stu-id="ffd72-191">For example, if the **interval** is 3 and the **frequency** is "week", the trigger recurs every three weeks.</span></span> |
| <span data-ttu-id="ffd72-192">**schedule**</span><span class="sxs-lookup"><span data-stu-id="ffd72-192">**schedule**</span></span> | <span data-ttu-id="ffd72-193">The recurrence schedule for the trigger.</span><span class="sxs-lookup"><span data-stu-id="ffd72-193">The recurrence schedule for the trigger.</span></span> <span data-ttu-id="ffd72-194">A trigger with a specified **frequency** value alters its recurrence based on a recurrence schedule.</span><span class="sxs-lookup"><span data-stu-id="ffd72-194">A trigger with a specified **frequency** value alters its recurrence based on a recurrence schedule.</span></span> <span data-ttu-id="ffd72-195">The **schedule** property contains modifications for the recurrence that are based on minutes, hours, week days, month days, and week number.</span><span class="sxs-lookup"><span data-stu-id="ffd72-195">The **schedule** property contains modifications for the recurrence that are based on minutes, hours, week days, month days, and week number.</span></span>

### <a name="schedule-trigger-example"></a><span data-ttu-id="ffd72-196">Schedule trigger example</span><span class="sxs-lookup"><span data-stu-id="ffd72-196">Schedule trigger example</span></span>

```json
{
    "properties": {
        "name": "MyTrigger",
        "type": "ScheduleTrigger",
        "typeProperties": {
            "recurrence": {
                "frequency": "Hour",
                "interval": 1,
                "startTime": "2017-11-01T09:00:00-08:00",
                "endTime": "2017-11-02T22:00:00-08:00"
            }
        },
        "pipelines": [{
                "pipelineReference": {
                    "type": "PipelineReference",
                    "referenceName": "SQLServerToBlobPipeline"
                },
                "parameters": {}
            },
            {
                "pipelineReference": {
                    "type": "PipelineReference",
                    "referenceName": "SQLServerToAzureSQLPipeline"
                },
                "parameters": {}
            }
        ]
    }
}
```

### <a name="schema-defaults-limits-and-examples"></a><span data-ttu-id="ffd72-197">Schema defaults, limits, and examples</span><span class="sxs-lookup"><span data-stu-id="ffd72-197">Schema defaults, limits, and examples</span></span>

| <span data-ttu-id="ffd72-198">JSON property</span><span class="sxs-lookup"><span data-stu-id="ffd72-198">JSON property</span></span> | <span data-ttu-id="ffd72-199">Type</span><span class="sxs-lookup"><span data-stu-id="ffd72-199">Type</span></span> | <span data-ttu-id="ffd72-200">Required</span><span class="sxs-lookup"><span data-stu-id="ffd72-200">Required</span></span> | <span data-ttu-id="ffd72-201">Default value</span><span class="sxs-lookup"><span data-stu-id="ffd72-201">Default value</span></span> | <span data-ttu-id="ffd72-202">Valid values</span><span class="sxs-lookup"><span data-stu-id="ffd72-202">Valid values</span></span> | <span data-ttu-id="ffd72-203">Example</span><span class="sxs-lookup"><span data-stu-id="ffd72-203">Example</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="ffd72-204">**startTime**</span><span class="sxs-lookup"><span data-stu-id="ffd72-204">**startTime**</span></span> | <span data-ttu-id="ffd72-205">string</span><span class="sxs-lookup"><span data-stu-id="ffd72-205">string</span></span> | <span data-ttu-id="ffd72-206">Yes</span><span class="sxs-lookup"><span data-stu-id="ffd72-206">Yes</span></span> | <span data-ttu-id="ffd72-207">None</span><span class="sxs-lookup"><span data-stu-id="ffd72-207">None</span></span> | <span data-ttu-id="ffd72-208">ISO 8601 date-times</span><span class="sxs-lookup"><span data-stu-id="ffd72-208">ISO 8601 date-times</span></span> | `"startTime" : "2013-01-09T09:30:00-08:00"` |
| <span data-ttu-id="ffd72-209">**recurrence**</span><span class="sxs-lookup"><span data-stu-id="ffd72-209">**recurrence**</span></span> | <span data-ttu-id="ffd72-210">object</span><span class="sxs-lookup"><span data-stu-id="ffd72-210">object</span></span> | <span data-ttu-id="ffd72-211">Yes</span><span class="sxs-lookup"><span data-stu-id="ffd72-211">Yes</span></span> | <span data-ttu-id="ffd72-212">None</span><span class="sxs-lookup"><span data-stu-id="ffd72-212">None</span></span> | <span data-ttu-id="ffd72-213">A recurrence object</span><span class="sxs-lookup"><span data-stu-id="ffd72-213">A recurrence object</span></span> | `"recurrence" : { "frequency" : "monthly", "interval" : 1 }` |
| <span data-ttu-id="ffd72-214">**interval**</span><span class="sxs-lookup"><span data-stu-id="ffd72-214">**interval**</span></span> | <span data-ttu-id="ffd72-215">number</span><span class="sxs-lookup"><span data-stu-id="ffd72-215">number</span></span> | <span data-ttu-id="ffd72-216">No</span><span class="sxs-lookup"><span data-stu-id="ffd72-216">No</span></span> | <span data-ttu-id="ffd72-217">1</span><span class="sxs-lookup"><span data-stu-id="ffd72-217">1</span></span> | <span data-ttu-id="ffd72-218">1 to 1000</span><span class="sxs-lookup"><span data-stu-id="ffd72-218">1 to 1000</span></span> | `"interval":10` |
| <span data-ttu-id="ffd72-219">**endTime**</span><span class="sxs-lookup"><span data-stu-id="ffd72-219">**endTime**</span></span> | <span data-ttu-id="ffd72-220">string</span><span class="sxs-lookup"><span data-stu-id="ffd72-220">string</span></span> | <span data-ttu-id="ffd72-221">Yes</span><span class="sxs-lookup"><span data-stu-id="ffd72-221">Yes</span></span> | <span data-ttu-id="ffd72-222">None</span><span class="sxs-lookup"><span data-stu-id="ffd72-222">None</span></span> | <span data-ttu-id="ffd72-223">A date-time value that represents a time in the future</span><span class="sxs-lookup"><span data-stu-id="ffd72-223">A date-time value that represents a time in the future</span></span> | `"endTime" : "2013-02-09T09:30:00-08:00"` |
| <span data-ttu-id="ffd72-224">**schedule**</span><span class="sxs-lookup"><span data-stu-id="ffd72-224">**schedule**</span></span> | <span data-ttu-id="ffd72-225">object</span><span class="sxs-lookup"><span data-stu-id="ffd72-225">object</span></span> | <span data-ttu-id="ffd72-226">No</span><span class="sxs-lookup"><span data-stu-id="ffd72-226">No</span></span> | <span data-ttu-id="ffd72-227">None</span><span class="sxs-lookup"><span data-stu-id="ffd72-227">None</span></span> | <span data-ttu-id="ffd72-228">A schedule object</span><span class="sxs-lookup"><span data-stu-id="ffd72-228">A schedule object</span></span> | `"schedule" : { "minute" : [30], "hour" : [8,17] }` |

### <a name="starttime-property"></a><span data-ttu-id="ffd72-229">startTime property</span><span class="sxs-lookup"><span data-stu-id="ffd72-229">startTime property</span></span>
<span data-ttu-id="ffd72-230">The following table shows you how the **startTime** property controls a trigger run:</span><span class="sxs-lookup"><span data-stu-id="ffd72-230">The following table shows you how the **startTime** property controls a trigger run:</span></span>

| <span data-ttu-id="ffd72-231">startTime value</span><span class="sxs-lookup"><span data-stu-id="ffd72-231">startTime value</span></span> | <span data-ttu-id="ffd72-232">Recurrence without schedule</span><span class="sxs-lookup"><span data-stu-id="ffd72-232">Recurrence without schedule</span></span> | <span data-ttu-id="ffd72-233">Recurrence with schedule</span><span class="sxs-lookup"><span data-stu-id="ffd72-233">Recurrence with schedule</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ffd72-234">**Start time is in the past**</span><span class="sxs-lookup"><span data-stu-id="ffd72-234">**Start time is in the past**</span></span> | <span data-ttu-id="ffd72-235">Calculates the first future execution time after the start time, and runs at that time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-235">Calculates the first future execution time after the start time, and runs at that time.</span></span><br /><br /><span data-ttu-id="ffd72-236">Runs subsequent executions calculated from the last execution time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-236">Runs subsequent executions calculated from the last execution time.</span></span><br /><br /><span data-ttu-id="ffd72-237">See the example that follows this table.</span><span class="sxs-lookup"><span data-stu-id="ffd72-237">See the example that follows this table.</span></span> | <span data-ttu-id="ffd72-238">The trigger starts _no sooner than_ the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-238">The trigger starts _no sooner than_ the specified start time.</span></span> <span data-ttu-id="ffd72-239">The first occurrence is based on the schedule,  calculated from the start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-239">The first occurrence is based on the schedule,  calculated from the start time.</span></span><br /><br /><span data-ttu-id="ffd72-240">Runs subsequent executions based on the recurrence schedule.</span><span class="sxs-lookup"><span data-stu-id="ffd72-240">Runs subsequent executions based on the recurrence schedule.</span></span> |
| <span data-ttu-id="ffd72-241">**Start time is in the future or the current time**</span><span class="sxs-lookup"><span data-stu-id="ffd72-241">**Start time is in the future or the current time**</span></span> | <span data-ttu-id="ffd72-242">Runs once at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-242">Runs once at the specified start time.</span></span><br /><br /><span data-ttu-id="ffd72-243">Runs subsequent executions calculated from the last execution time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-243">Runs subsequent executions calculated from the last execution time.</span></span> | <span data-ttu-id="ffd72-244">The trigger starts _no sooner_ than the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-244">The trigger starts _no sooner_ than the specified start time.</span></span> <span data-ttu-id="ffd72-245">The first occurrence is based on the schedule, calculated from the start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-245">The first occurrence is based on the schedule, calculated from the start time.</span></span><br /><br /><span data-ttu-id="ffd72-246">Runs subsequent executions based on the recurrence schedule.</span><span class="sxs-lookup"><span data-stu-id="ffd72-246">Runs subsequent executions based on the recurrence schedule.</span></span> |

<span data-ttu-id="ffd72-247">Let's look at an example of what happens when the start time is in the past, with a recurrence, but no schedule.</span><span class="sxs-lookup"><span data-stu-id="ffd72-247">Let's look at an example of what happens when the start time is in the past, with a recurrence, but no schedule.</span></span> <span data-ttu-id="ffd72-248">Assume that the current time is 2017-04-08 13:00, the start time is 2017-04-07 14:00, and the recurrence is every two days.</span><span class="sxs-lookup"><span data-stu-id="ffd72-248">Assume that the current time is 2017-04-08 13:00, the start time is 2017-04-07 14:00, and the recurrence is every two days.</span></span> <span data-ttu-id="ffd72-249">(The **recurrence** value is defined by setting the **frequency** property to "day" and the **interval** property to 2.) Notice that the **startTime** value is in the past and occurs before the current time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-249">(The **recurrence** value is defined by setting the **frequency** property to "day" and the **interval** property to 2.) Notice that the **startTime** value is in the past and occurs before the current time.</span></span>

<span data-ttu-id="ffd72-250">Under these conditions, the first execution is  2017-04-09 at 14:00.</span><span class="sxs-lookup"><span data-stu-id="ffd72-250">Under these conditions, the first execution is  2017-04-09 at 14:00.</span></span> <span data-ttu-id="ffd72-251">The Scheduler engine calculates execution occurrences from the start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-251">The Scheduler engine calculates execution occurrences from the start time.</span></span> <span data-ttu-id="ffd72-252">Any instances in the past are discarded.</span><span class="sxs-lookup"><span data-stu-id="ffd72-252">Any instances in the past are discarded.</span></span> <span data-ttu-id="ffd72-253">The engine uses the next instance that occurs in the future.</span><span class="sxs-lookup"><span data-stu-id="ffd72-253">The engine uses the next instance that occurs in the future.</span></span> <span data-ttu-id="ffd72-254">In this scenario, the start time is 2017-04-07 at 2:00 PM.</span><span class="sxs-lookup"><span data-stu-id="ffd72-254">In this scenario, the start time is 2017-04-07 at 2:00 PM.</span></span> <span data-ttu-id="ffd72-255">The next instance is two days from that time, which is on 2017-04-09 at 2:00 PM.</span><span class="sxs-lookup"><span data-stu-id="ffd72-255">The next instance is two days from that time, which is on 2017-04-09 at 2:00 PM.</span></span>

<span data-ttu-id="ffd72-256">The first execution time is the same even whether **startTime** is 2017-04-05 14:00 or 2017-04-01 14:00.</span><span class="sxs-lookup"><span data-stu-id="ffd72-256">The first execution time is the same even whether **startTime** is 2017-04-05 14:00 or 2017-04-01 14:00.</span></span> <span data-ttu-id="ffd72-257">After the first execution, subsequent executions are calculated by using the schedule.</span><span class="sxs-lookup"><span data-stu-id="ffd72-257">After the first execution, subsequent executions are calculated by using the schedule.</span></span> <span data-ttu-id="ffd72-258">Therefore, the subsequent executions are on 2017-04-11 at 2:00 PM, then on 2017-04-13 at 2:00 PM, then on 2017-04-15 at 2:00 PM, and so on.</span><span class="sxs-lookup"><span data-stu-id="ffd72-258">Therefore, the subsequent executions are on 2017-04-11 at 2:00 PM, then on 2017-04-13 at 2:00 PM, then on 2017-04-15 at 2:00 PM, and so on.</span></span>

<span data-ttu-id="ffd72-259">Finally, when hours or minutes aren’t set in the schedule for a trigger, the hours or minutes of the first execution are used as defaults.</span><span class="sxs-lookup"><span data-stu-id="ffd72-259">Finally, when hours or minutes aren’t set in the schedule for a trigger, the hours or minutes of the first execution are used as defaults.</span></span>

### <a name="schedule-property"></a><span data-ttu-id="ffd72-260">schedule property</span><span class="sxs-lookup"><span data-stu-id="ffd72-260">schedule property</span></span>
<span data-ttu-id="ffd72-261">You can use **schedule** to *limit* the number of trigger executions.</span><span class="sxs-lookup"><span data-stu-id="ffd72-261">You can use **schedule** to *limit* the number of trigger executions.</span></span> <span data-ttu-id="ffd72-262">For example, if a trigger with a monthly frequency is scheduled to run only on day 31, the trigger runs only in those months that have a thirty-first day.</span><span class="sxs-lookup"><span data-stu-id="ffd72-262">For example, if a trigger with a monthly frequency is scheduled to run only on day 31, the trigger runs only in those months that have a thirty-first day.</span></span>

<span data-ttu-id="ffd72-263">You can also use **schedule** to *expand* the number of trigger executions.</span><span class="sxs-lookup"><span data-stu-id="ffd72-263">You can also use **schedule** to *expand* the number of trigger executions.</span></span> <span data-ttu-id="ffd72-264">For example, a trigger with a monthly frequency that's scheduled to run on month days 1 and 2, runs on the first and second days of the month, rather than once a month.</span><span class="sxs-lookup"><span data-stu-id="ffd72-264">For example, a trigger with a monthly frequency that's scheduled to run on month days 1 and 2, runs on the first and second days of the month, rather than once a month.</span></span>

<span data-ttu-id="ffd72-265">If multiple **schedule** elements are specified, the order of evaluation is from the largest to the smallest schedule setting: week number, month day, week day, hour, minute.</span><span class="sxs-lookup"><span data-stu-id="ffd72-265">If multiple **schedule** elements are specified, the order of evaluation is from the largest to the smallest schedule setting: week number, month day, week day, hour, minute.</span></span>

<span data-ttu-id="ffd72-266">The following table describes the **schedule** elements in detail:</span><span class="sxs-lookup"><span data-stu-id="ffd72-266">The following table describes the **schedule** elements in detail:</span></span>

| <span data-ttu-id="ffd72-267">JSON element</span><span class="sxs-lookup"><span data-stu-id="ffd72-267">JSON element</span></span> | <span data-ttu-id="ffd72-268">Description</span><span class="sxs-lookup"><span data-stu-id="ffd72-268">Description</span></span> | <span data-ttu-id="ffd72-269">Valid values</span><span class="sxs-lookup"><span data-stu-id="ffd72-269">Valid values</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ffd72-270">**minutes**</span><span class="sxs-lookup"><span data-stu-id="ffd72-270">**minutes**</span></span> | <span data-ttu-id="ffd72-271">Minutes of the hour at which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-271">Minutes of the hour at which the trigger runs.</span></span> |<span data-ttu-id="ffd72-272">- Integer</span><span class="sxs-lookup"><span data-stu-id="ffd72-272">- Integer</span></span><br /><span data-ttu-id="ffd72-273">- Array of integers</span><span class="sxs-lookup"><span data-stu-id="ffd72-273">- Array of integers</span></span>|
| <span data-ttu-id="ffd72-274">**hours**</span><span class="sxs-lookup"><span data-stu-id="ffd72-274">**hours**</span></span> | <span data-ttu-id="ffd72-275">Hours of the day at which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-275">Hours of the day at which the trigger runs.</span></span> |<span data-ttu-id="ffd72-276">- Integer</span><span class="sxs-lookup"><span data-stu-id="ffd72-276">- Integer</span></span><br /><span data-ttu-id="ffd72-277">- Array of integers</span><span class="sxs-lookup"><span data-stu-id="ffd72-277">- Array of integers</span></span>|
| <span data-ttu-id="ffd72-278">**weekDays**</span><span class="sxs-lookup"><span data-stu-id="ffd72-278">**weekDays**</span></span> | <span data-ttu-id="ffd72-279">Days of the week the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-279">Days of the week the trigger runs.</span></span> <span data-ttu-id="ffd72-280">The value can be specified only with a weekly frequency.</span><span class="sxs-lookup"><span data-stu-id="ffd72-280">The value can be specified only with a weekly frequency.</span></span>|<br /><span data-ttu-id="ffd72-281">- Monday</span><span class="sxs-lookup"><span data-stu-id="ffd72-281">- Monday</span></span><br /><span data-ttu-id="ffd72-282">- Tuesday</span><span class="sxs-lookup"><span data-stu-id="ffd72-282">- Tuesday</span></span><br /><span data-ttu-id="ffd72-283">- Wednesday</span><span class="sxs-lookup"><span data-stu-id="ffd72-283">- Wednesday</span></span><br /><span data-ttu-id="ffd72-284">- Thursday</span><span class="sxs-lookup"><span data-stu-id="ffd72-284">- Thursday</span></span><br /><span data-ttu-id="ffd72-285">- Friday</span><span class="sxs-lookup"><span data-stu-id="ffd72-285">- Friday</span></span><br /><span data-ttu-id="ffd72-286">- Saturday</span><span class="sxs-lookup"><span data-stu-id="ffd72-286">- Saturday</span></span><br /><span data-ttu-id="ffd72-287">- Sunday</span><span class="sxs-lookup"><span data-stu-id="ffd72-287">- Sunday</span></span><br /><span data-ttu-id="ffd72-288">- Array of day values (maximum array size is 7)</span><span class="sxs-lookup"><span data-stu-id="ffd72-288">- Array of day values (maximum array size is 7)</span></span><br /><br /><span data-ttu-id="ffd72-289">Day values are not case-sensitive</span><span class="sxs-lookup"><span data-stu-id="ffd72-289">Day values are not case-sensitive</span></span>|
| <span data-ttu-id="ffd72-290">**monthlyOccurrences**</span><span class="sxs-lookup"><span data-stu-id="ffd72-290">**monthlyOccurrences**</span></span> | <span data-ttu-id="ffd72-291">Days of the month on which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-291">Days of the month on which the trigger runs.</span></span> <span data-ttu-id="ffd72-292">The value can be specified with a monthly frequency only.</span><span class="sxs-lookup"><span data-stu-id="ffd72-292">The value can be specified with a monthly frequency only.</span></span> |<span data-ttu-id="ffd72-293">- Array of **monthlyOccurence** objects: `{ "day": day,  "occurrence": occurence }`</span><span class="sxs-lookup"><span data-stu-id="ffd72-293">- Array of **monthlyOccurence** objects: `{ "day": day,  "occurrence": occurence }`</span></span><br /><span data-ttu-id="ffd72-294">- The **day** attribute is the day of the week on which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-294">- The **day** attribute is the day of the week on which the trigger runs.</span></span> <span data-ttu-id="ffd72-295">For example, a **monthlyOccurrences** property with a **day** value of `{Sunday}` means every Sunday of the month.</span><span class="sxs-lookup"><span data-stu-id="ffd72-295">For example, a **monthlyOccurrences** property with a **day** value of `{Sunday}` means every Sunday of the month.</span></span> <span data-ttu-id="ffd72-296">The **day** attribute is required.</span><span class="sxs-lookup"><span data-stu-id="ffd72-296">The **day** attribute is required.</span></span><br /><span data-ttu-id="ffd72-297">- The **occurrence** attribute is the occurrence of the specified **day** during the month.</span><span class="sxs-lookup"><span data-stu-id="ffd72-297">- The **occurrence** attribute is the occurrence of the specified **day** during the month.</span></span> <span data-ttu-id="ffd72-298">For example, a **monthlyOccurrences** property with **day** and **occurrence** values of `{Sunday, -1}` means the last Sunday of the month.</span><span class="sxs-lookup"><span data-stu-id="ffd72-298">For example, a **monthlyOccurrences** property with **day** and **occurrence** values of `{Sunday, -1}` means the last Sunday of the month.</span></span> <span data-ttu-id="ffd72-299">The **occurrence** attribute is optional.</span><span class="sxs-lookup"><span data-stu-id="ffd72-299">The **occurrence** attribute is optional.</span></span>|
| <span data-ttu-id="ffd72-300">**monthDays**</span><span class="sxs-lookup"><span data-stu-id="ffd72-300">**monthDays**</span></span> | <span data-ttu-id="ffd72-301">Day of the month on which the trigger runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-301">Day of the month on which the trigger runs.</span></span> <span data-ttu-id="ffd72-302">The value can be specified with a monthly frequency only.</span><span class="sxs-lookup"><span data-stu-id="ffd72-302">The value can be specified with a monthly frequency only.</span></span> |<span data-ttu-id="ffd72-303">- Any value <= -1 and >= -31</span><span class="sxs-lookup"><span data-stu-id="ffd72-303">- Any value <= -1 and >= -31</span></span><br /><span data-ttu-id="ffd72-304">- Any value >= 1 and <= 31</span><span class="sxs-lookup"><span data-stu-id="ffd72-304">- Any value >= 1 and <= 31</span></span><br /><span data-ttu-id="ffd72-305">- Array of values</span><span class="sxs-lookup"><span data-stu-id="ffd72-305">- Array of values</span></span>|

## <a name="tumbling-window-trigger"></a><span data-ttu-id="ffd72-306">Tumbling window trigger</span><span class="sxs-lookup"><span data-stu-id="ffd72-306">Tumbling window trigger</span></span>
<span data-ttu-id="ffd72-307">Tumbling window triggers are a type of trigger that fires at a periodic time interval from a specified start time, while retaining state.</span><span class="sxs-lookup"><span data-stu-id="ffd72-307">Tumbling window triggers are a type of trigger that fires at a periodic time interval from a specified start time, while retaining state.</span></span> <span data-ttu-id="ffd72-308">Tumbling windows are a series of fixed-sized, non-overlapping, and contiguous time intervals.</span><span class="sxs-lookup"><span data-stu-id="ffd72-308">Tumbling windows are a series of fixed-sized, non-overlapping, and contiguous time intervals.</span></span>

<span data-ttu-id="ffd72-309">For more information about tumbling window triggers and for examples, see [Create a tumbling window trigger](how-to-create-tumbling-window-trigger.md).</span><span class="sxs-lookup"><span data-stu-id="ffd72-309">For more information about tumbling window triggers and for examples, see [Create a tumbling window trigger](how-to-create-tumbling-window-trigger.md).</span></span>

## <a name="event-based-trigger"></a><span data-ttu-id="ffd72-310">Event-based trigger</span><span class="sxs-lookup"><span data-stu-id="ffd72-310">Event-based trigger</span></span>

<span data-ttu-id="ffd72-311">An event-based trigger runs pipelines in response to an event, such as the arrival of a file, or the deletion of a file, in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ffd72-311">An event-based trigger runs pipelines in response to an event, such as the arrival of a file, or the deletion of a file, in Azure Blob Storage.</span></span>

<span data-ttu-id="ffd72-312">For more information about event-based triggers, see [Create a trigger that runs a pipeline in response to an event](how-to-create-event-trigger.md).</span><span class="sxs-lookup"><span data-stu-id="ffd72-312">For more information about event-based triggers, see [Create a trigger that runs a pipeline in response to an event](how-to-create-event-trigger.md).</span></span>

## <a name="examples-of-trigger-recurrence-schedules"></a><span data-ttu-id="ffd72-313">Examples of trigger recurrence schedules</span><span class="sxs-lookup"><span data-stu-id="ffd72-313">Examples of trigger recurrence schedules</span></span>
<span data-ttu-id="ffd72-314">This section provides examples of recurrence schedules.</span><span class="sxs-lookup"><span data-stu-id="ffd72-314">This section provides examples of recurrence schedules.</span></span> <span data-ttu-id="ffd72-315">It focuses on the **schedule** object and its elements.</span><span class="sxs-lookup"><span data-stu-id="ffd72-315">It focuses on the **schedule** object and its elements.</span></span>

<span data-ttu-id="ffd72-316">The examples assume that the **interval** value is 1, and that the **frequency** value is correct according to the schedule definition.</span><span class="sxs-lookup"><span data-stu-id="ffd72-316">The examples assume that the **interval** value is 1, and that the **frequency** value is correct according to the schedule definition.</span></span> <span data-ttu-id="ffd72-317">For example, you can't have a **frequency** value of "day" and also have a **monthDays** modification in the **schedule** object.</span><span class="sxs-lookup"><span data-stu-id="ffd72-317">For example, you can't have a **frequency** value of "day" and also have a **monthDays** modification in the **schedule** object.</span></span> <span data-ttu-id="ffd72-318">These kinds of restrictions are described in the table in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="ffd72-318">These kinds of restrictions are described in the table in the preceding section.</span></span>

| <span data-ttu-id="ffd72-319">Example</span><span class="sxs-lookup"><span data-stu-id="ffd72-319">Example</span></span> | <span data-ttu-id="ffd72-320">Description</span><span class="sxs-lookup"><span data-stu-id="ffd72-320">Description</span></span> |
|:--- |:--- |
| `{"hours":[5]}` | <span data-ttu-id="ffd72-321">Run at 5:00 AM every day.</span><span class="sxs-lookup"><span data-stu-id="ffd72-321">Run at 5:00 AM every day.</span></span> |
| `{"minutes":[15], "hours":[5]}` | <span data-ttu-id="ffd72-322">Run at 5:15 AM every day.</span><span class="sxs-lookup"><span data-stu-id="ffd72-322">Run at 5:15 AM every day.</span></span> |
| `{"minutes":[15], "hours":[5,17]}` | <span data-ttu-id="ffd72-323">Run at 5:15 AM and 5:15 PM every day.</span><span class="sxs-lookup"><span data-stu-id="ffd72-323">Run at 5:15 AM and 5:15 PM every day.</span></span> |
| `{"minutes":[15,45], "hours":[5,17]}` | <span data-ttu-id="ffd72-324">Run at 5:15 AM, 5:45 AM, 5:15 PM, and 5:45 PM every day.</span><span class="sxs-lookup"><span data-stu-id="ffd72-324">Run at 5:15 AM, 5:45 AM, 5:15 PM, and 5:45 PM every day.</span></span> |
| `{"minutes":[0,15,30,45]}` | <span data-ttu-id="ffd72-325">Run every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="ffd72-325">Run every 15 minutes.</span></span> |
| `{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}` | <span data-ttu-id="ffd72-326">Run every hour.</span><span class="sxs-lookup"><span data-stu-id="ffd72-326">Run every hour.</span></span><br /><br /><span data-ttu-id="ffd72-327">This trigger runs every hour.</span><span class="sxs-lookup"><span data-stu-id="ffd72-327">This trigger runs every hour.</span></span> <span data-ttu-id="ffd72-328">The minutes are controlled by the **startTime** value, when a value is specified.</span><span class="sxs-lookup"><span data-stu-id="ffd72-328">The minutes are controlled by the **startTime** value, when a value is specified.</span></span> <span data-ttu-id="ffd72-329">If a value isn't specified, the minutes are controlled by the creation time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-329">If a value isn't specified, the minutes are controlled by the creation time.</span></span> <span data-ttu-id="ffd72-330">For example, if the start time or creation time (whichever applies) is 12:25 PM, the trigger runs at 00:25, 01:25, 02:25, ..., and 23:25.</span><span class="sxs-lookup"><span data-stu-id="ffd72-330">For example, if the start time or creation time (whichever applies) is 12:25 PM, the trigger runs at 00:25, 01:25, 02:25, ..., and 23:25.</span></span><br /><br /><span data-ttu-id="ffd72-331">This schedule is equivalent to having a trigger with a **frequency** value of "hour", an **interval** value of 1, and no **schedule**.</span><span class="sxs-lookup"><span data-stu-id="ffd72-331">This schedule is equivalent to having a trigger with a **frequency** value of "hour", an **interval** value of 1, and no **schedule**.</span></span> <span data-ttu-id="ffd72-332">This schedule can be used with different **frequency** and **interval** values to create other triggers.</span><span class="sxs-lookup"><span data-stu-id="ffd72-332">This schedule can be used with different **frequency** and **interval** values to create other triggers.</span></span> <span data-ttu-id="ffd72-333">For example, when the **frequency** value is "month", the schedule runs only once a month, rather than every day when the **frequency** value is "day".</span><span class="sxs-lookup"><span data-stu-id="ffd72-333">For example, when the **frequency** value is "month", the schedule runs only once a month, rather than every day when the **frequency** value is "day".</span></span> |
| `{"minutes":[0]}` | <span data-ttu-id="ffd72-334">Run every hour on the hour.</span><span class="sxs-lookup"><span data-stu-id="ffd72-334">Run every hour on the hour.</span></span><br /><br /><span data-ttu-id="ffd72-335">This trigger runs every hour on the hour starting at 12:00 AM, 1:00 AM, 2:00 AM, and so on.</span><span class="sxs-lookup"><span data-stu-id="ffd72-335">This trigger runs every hour on the hour starting at 12:00 AM, 1:00 AM, 2:00 AM, and so on.</span></span><br /><br /><span data-ttu-id="ffd72-336">This schedule is equivalent to a trigger with a **frequency** value of "hour" and a **startTime** value of zero minutes, and no **schedule** but a **frequency** value of "day".</span><span class="sxs-lookup"><span data-stu-id="ffd72-336">This schedule is equivalent to a trigger with a **frequency** value of "hour" and a **startTime** value of zero minutes, and no **schedule** but a **frequency** value of "day".</span></span> <span data-ttu-id="ffd72-337">If the **frequency** value is "week" or "month", the schedule executes one day a week or one day a month only, respectively.</span><span class="sxs-lookup"><span data-stu-id="ffd72-337">If the **frequency** value is "week" or "month", the schedule executes one day a week or one day a month only, respectively.</span></span> |
| `{"minutes":[15]}` | <span data-ttu-id="ffd72-338">Run at 15 minutes past every hour.</span><span class="sxs-lookup"><span data-stu-id="ffd72-338">Run at 15 minutes past every hour.</span></span><br /><br /><span data-ttu-id="ffd72-339">This trigger runs every hour at 15 minutes past the hour starting at 00:15 AM, 1:15 AM, 2:15 AM, and so on, and ending at 11:15 PM.</span><span class="sxs-lookup"><span data-stu-id="ffd72-339">This trigger runs every hour at 15 minutes past the hour starting at 00:15 AM, 1:15 AM, 2:15 AM, and so on, and ending at 11:15 PM.</span></span> |
| `{"hours":[17], "weekDays":["saturday"]}` | <span data-ttu-id="ffd72-340">Run at 5:00 PM on Saturdays every week.</span><span class="sxs-lookup"><span data-stu-id="ffd72-340">Run at 5:00 PM on Saturdays every week.</span></span> |
| `{"hours":[17], "weekDays":["monday", "wednesday", "friday"]}` | <span data-ttu-id="ffd72-341">Run at 5:00 PM on Monday, Wednesday, and Friday every week.</span><span class="sxs-lookup"><span data-stu-id="ffd72-341">Run at 5:00 PM on Monday, Wednesday, and Friday every week.</span></span> |
| `{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}` | <span data-ttu-id="ffd72-342">Run at 5:15 PM and 5:45 PM on Monday, Wednesday, and Friday every week.</span><span class="sxs-lookup"><span data-stu-id="ffd72-342">Run at 5:15 PM and 5:45 PM on Monday, Wednesday, and Friday every week.</span></span> |
| `{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}` | <span data-ttu-id="ffd72-343">Run every 15 minutes on weekdays.</span><span class="sxs-lookup"><span data-stu-id="ffd72-343">Run every 15 minutes on weekdays.</span></span> |
| `{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}` | <span data-ttu-id="ffd72-344">Run every 15 minutes on weekdays between 9:00 AM and 4:45 PM.</span><span class="sxs-lookup"><span data-stu-id="ffd72-344">Run every 15 minutes on weekdays between 9:00 AM and 4:45 PM.</span></span> |
| `{"weekDays":["tuesday", "thursday"]}` | <span data-ttu-id="ffd72-345">Run on Tuesdays and Thursdays at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-345">Run on Tuesdays and Thursdays at the specified start time.</span></span> |
| `{"minutes":[0], "hours":[6], "monthDays":[28]}` | <span data-ttu-id="ffd72-346">Run at 6:00 AM on the twenty-eighth day of every month (assuming a **frequency** value of "month").</span><span class="sxs-lookup"><span data-stu-id="ffd72-346">Run at 6:00 AM on the twenty-eighth day of every month (assuming a **frequency** value of "month").</span></span> |
| `{"minutes":[0], "hours":[6], "monthDays":[-1]}` | <span data-ttu-id="ffd72-347">Run at 6:00 AM on the last day of the month.</span><span class="sxs-lookup"><span data-stu-id="ffd72-347">Run at 6:00 AM on the last day of the month.</span></span><br /><br /><span data-ttu-id="ffd72-348">To run a trigger on the last day of a month, use -1 instead of day 28, 29, 30, or 31.</span><span class="sxs-lookup"><span data-stu-id="ffd72-348">To run a trigger on the last day of a month, use -1 instead of day 28, 29, 30, or 31.</span></span> |
| `{"minutes":[0], "hours":[6], "monthDays":[1,-1]}` | <span data-ttu-id="ffd72-349">Run at 6:00 AM on the first and last day of every month.</span><span class="sxs-lookup"><span data-stu-id="ffd72-349">Run at 6:00 AM on the first and last day of every month.</span></span> |
| `{monthDays":[1,14]}` | <span data-ttu-id="ffd72-350">Run on the first and fourteenth day of every month at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-350">Run on the first and fourteenth day of every month at the specified start time.</span></span> |
| `{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}` | <span data-ttu-id="ffd72-351">Run on the first Friday of every month at 5:00 AM.</span><span class="sxs-lookup"><span data-stu-id="ffd72-351">Run on the first Friday of every month at 5:00 AM.</span></span> |
| `{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}` | <span data-ttu-id="ffd72-352">Run on the first Friday of every month at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-352">Run on the first Friday of every month at the specified start time.</span></span> |
| `{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}` | <span data-ttu-id="ffd72-353">Run on the third Friday from the end of the month, every month, at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-353">Run on the third Friday from the end of the month, every month, at the specified start time.</span></span> |
| `{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}` | <span data-ttu-id="ffd72-354">Run on the first and last Friday of every month at 5:15 AM.</span><span class="sxs-lookup"><span data-stu-id="ffd72-354">Run on the first and last Friday of every month at 5:15 AM.</span></span> |
| `{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}` | <span data-ttu-id="ffd72-355">Run on the first and last Friday of every month at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-355">Run on the first and last Friday of every month at the specified start time.</span></span> |
| `{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}` | <span data-ttu-id="ffd72-356">Run on the fifth Friday of every month at the specified start time.</span><span class="sxs-lookup"><span data-stu-id="ffd72-356">Run on the fifth Friday of every month at the specified start time.</span></span><br /><br /><span data-ttu-id="ffd72-357">When there's no fifth Friday in a month, the pipeline doesn't run.</span><span class="sxs-lookup"><span data-stu-id="ffd72-357">When there's no fifth Friday in a month, the pipeline doesn't run.</span></span> <span data-ttu-id="ffd72-358">To run the trigger on the last occurring Friday of the month, consider using -1 instead of 5 for the **occurrence** value.</span><span class="sxs-lookup"><span data-stu-id="ffd72-358">To run the trigger on the last occurring Friday of the month, consider using -1 instead of 5 for the **occurrence** value.</span></span> |
| `{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}` | <span data-ttu-id="ffd72-359">Run every 15 minutes on the last Friday of the month.</span><span class="sxs-lookup"><span data-stu-id="ffd72-359">Run every 15 minutes on the last Friday of the month.</span></span> |
| `{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}` | <span data-ttu-id="ffd72-360">Run at 5:15 AM, 5:45 AM, 5:15 PM, and 5:45 PM on the third Wednesday of every month.</span><span class="sxs-lookup"><span data-stu-id="ffd72-360">Run at 5:15 AM, 5:45 AM, 5:15 PM, and 5:45 PM on the third Wednesday of every month.</span></span> |

## <a name="trigger-type-comparison"></a><span data-ttu-id="ffd72-361">Trigger type comparison</span><span class="sxs-lookup"><span data-stu-id="ffd72-361">Trigger type comparison</span></span>
<span data-ttu-id="ffd72-362">The tumbling window trigger and the schedule trigger both operate on time heartbeats.</span><span class="sxs-lookup"><span data-stu-id="ffd72-362">The tumbling window trigger and the schedule trigger both operate on time heartbeats.</span></span> <span data-ttu-id="ffd72-363">How are they different?</span><span class="sxs-lookup"><span data-stu-id="ffd72-363">How are they different?</span></span>

<span data-ttu-id="ffd72-364">The following table provides a comparison of the tumbling window trigger and schedule trigger:</span><span class="sxs-lookup"><span data-stu-id="ffd72-364">The following table provides a comparison of the tumbling window trigger and schedule trigger:</span></span>

|  | <span data-ttu-id="ffd72-365">Tumbling window trigger</span><span class="sxs-lookup"><span data-stu-id="ffd72-365">Tumbling window trigger</span></span> | <span data-ttu-id="ffd72-366">Schedule trigger</span><span class="sxs-lookup"><span data-stu-id="ffd72-366">Schedule trigger</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="ffd72-367">**Backfill scenarios**</span><span class="sxs-lookup"><span data-stu-id="ffd72-367">**Backfill scenarios**</span></span> | <span data-ttu-id="ffd72-368">Supported.</span><span class="sxs-lookup"><span data-stu-id="ffd72-368">Supported.</span></span> <span data-ttu-id="ffd72-369">Pipeline runs can be scheduled for windows in the past.</span><span class="sxs-lookup"><span data-stu-id="ffd72-369">Pipeline runs can be scheduled for windows in the past.</span></span> | <span data-ttu-id="ffd72-370">Not supported.</span><span class="sxs-lookup"><span data-stu-id="ffd72-370">Not supported.</span></span> <span data-ttu-id="ffd72-371">Pipeline runs can be executed only on time periods from the current time and the future.</span><span class="sxs-lookup"><span data-stu-id="ffd72-371">Pipeline runs can be executed only on time periods from the current time and the future.</span></span> |
| <span data-ttu-id="ffd72-372">**Reliability**</span><span class="sxs-lookup"><span data-stu-id="ffd72-372">**Reliability**</span></span> | <span data-ttu-id="ffd72-373">100% reliability.</span><span class="sxs-lookup"><span data-stu-id="ffd72-373">100% reliability.</span></span> <span data-ttu-id="ffd72-374">Pipeline runs can be scheduled for all windows from a specified start date without gaps.</span><span class="sxs-lookup"><span data-stu-id="ffd72-374">Pipeline runs can be scheduled for all windows from a specified start date without gaps.</span></span> | <span data-ttu-id="ffd72-375">Less reliable.</span><span class="sxs-lookup"><span data-stu-id="ffd72-375">Less reliable.</span></span> |
| <span data-ttu-id="ffd72-376">**Retry capability**</span><span class="sxs-lookup"><span data-stu-id="ffd72-376">**Retry capability**</span></span> | <span data-ttu-id="ffd72-377">Supported.</span><span class="sxs-lookup"><span data-stu-id="ffd72-377">Supported.</span></span> <span data-ttu-id="ffd72-378">Failed pipeline runs have a default retry policy of 0, or a policy that's specified by the user in the trigger definition.</span><span class="sxs-lookup"><span data-stu-id="ffd72-378">Failed pipeline runs have a default retry policy of 0, or a policy that's specified by the user in the trigger definition.</span></span> <span data-ttu-id="ffd72-379">Automatically retries when pipeline runs fail due to concurrency/server/throttling limits (that is, status codes 400: User Error, 429: Too many requests, and 500: Internal Server error).</span><span class="sxs-lookup"><span data-stu-id="ffd72-379">Automatically retries when pipeline runs fail due to concurrency/server/throttling limits (that is, status codes 400: User Error, 429: Too many requests, and 500: Internal Server error).</span></span> | <span data-ttu-id="ffd72-380">Not supported.</span><span class="sxs-lookup"><span data-stu-id="ffd72-380">Not supported.</span></span> |
| <span data-ttu-id="ffd72-381">**Concurrency**</span><span class="sxs-lookup"><span data-stu-id="ffd72-381">**Concurrency**</span></span> | <span data-ttu-id="ffd72-382">Supported.</span><span class="sxs-lookup"><span data-stu-id="ffd72-382">Supported.</span></span> <span data-ttu-id="ffd72-383">Users can explicitly set concurrency limits for the trigger.</span><span class="sxs-lookup"><span data-stu-id="ffd72-383">Users can explicitly set concurrency limits for the trigger.</span></span> <span data-ttu-id="ffd72-384">Allows between 1 and 50 concurrent triggered pipeline runs.</span><span class="sxs-lookup"><span data-stu-id="ffd72-384">Allows between 1 and 50 concurrent triggered pipeline runs.</span></span> | <span data-ttu-id="ffd72-385">Not supported.</span><span class="sxs-lookup"><span data-stu-id="ffd72-385">Not supported.</span></span> |
| <span data-ttu-id="ffd72-386">**System variables**</span><span class="sxs-lookup"><span data-stu-id="ffd72-386">**System variables**</span></span> | <span data-ttu-id="ffd72-387">Supports the use of the **WindowStart** and **WindowEnd** system variables.</span><span class="sxs-lookup"><span data-stu-id="ffd72-387">Supports the use of the **WindowStart** and **WindowEnd** system variables.</span></span> <span data-ttu-id="ffd72-388">Users can access `triggerOutputs().windowStartTime` and `triggerOutputs().windowEndTime` as trigger system variables in the trigger definition.</span><span class="sxs-lookup"><span data-stu-id="ffd72-388">Users can access `triggerOutputs().windowStartTime` and `triggerOutputs().windowEndTime` as trigger system variables in the trigger definition.</span></span> <span data-ttu-id="ffd72-389">The values are used as the window start time and window end time, respectively.</span><span class="sxs-lookup"><span data-stu-id="ffd72-389">The values are used as the window start time and window end time, respectively.</span></span> <span data-ttu-id="ffd72-390">For example, for a tumbling window trigger that runs every hour, for the window 1:00 AM to 2:00 AM, the definition is `triggerOutputs().WindowStartTime = 2017-09-01T01:00:00Z` and `triggerOutputs().WindowEndTime = 2017-09-01T02:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="ffd72-390">For example, for a tumbling window trigger that runs every hour, for the window 1:00 AM to 2:00 AM, the definition is `triggerOutputs().WindowStartTime = 2017-09-01T01:00:00Z` and `triggerOutputs().WindowEndTime = 2017-09-01T02:00:00Z`.</span></span> | <span data-ttu-id="ffd72-391">Not supported.</span><span class="sxs-lookup"><span data-stu-id="ffd72-391">Not supported.</span></span> |
| <span data-ttu-id="ffd72-392">**Pipeline-to-trigger relationship**</span><span class="sxs-lookup"><span data-stu-id="ffd72-392">**Pipeline-to-trigger relationship**</span></span> | <span data-ttu-id="ffd72-393">Supports a one-to-one relationship.</span><span class="sxs-lookup"><span data-stu-id="ffd72-393">Supports a one-to-one relationship.</span></span> <span data-ttu-id="ffd72-394">Only one pipeline can be triggered.</span><span class="sxs-lookup"><span data-stu-id="ffd72-394">Only one pipeline can be triggered.</span></span> | <span data-ttu-id="ffd72-395">Supports many-to-many relationships.</span><span class="sxs-lookup"><span data-stu-id="ffd72-395">Supports many-to-many relationships.</span></span> <span data-ttu-id="ffd72-396">Multiple triggers can kick off a single pipeline.</span><span class="sxs-lookup"><span data-stu-id="ffd72-396">Multiple triggers can kick off a single pipeline.</span></span> <span data-ttu-id="ffd72-397">A single trigger can kick off multiple pipelines.</span><span class="sxs-lookup"><span data-stu-id="ffd72-397">A single trigger can kick off multiple pipelines.</span></span> | 

## <a name="next-steps"></a><span data-ttu-id="ffd72-398">Next steps</span><span class="sxs-lookup"><span data-stu-id="ffd72-398">Next steps</span></span>
<span data-ttu-id="ffd72-399">See the following tutorials:</span><span class="sxs-lookup"><span data-stu-id="ffd72-399">See the following tutorials:</span></span>

- [<span data-ttu-id="ffd72-400">Quickstart: Create a data factory by using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ffd72-400">Quickstart: Create a data factory by using the .NET SDK</span></span>](quickstart-create-data-factory-dot-net.md)
- [<span data-ttu-id="ffd72-401">Create a schedule trigger</span><span class="sxs-lookup"><span data-stu-id="ffd72-401">Create a schedule trigger</span></span>](how-to-create-schedule-trigger.md)
- [<span data-ttu-id="ffd72-402">Create a tumbling window trigger</span><span class="sxs-lookup"><span data-stu-id="ffd72-402">Create a tumbling window trigger</span></span>](how-to-create-tumbling-window-trigger.md)
