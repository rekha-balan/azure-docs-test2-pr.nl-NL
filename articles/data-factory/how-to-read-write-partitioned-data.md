---
title: How to read or write partitioned data in Azure Data Factory | Microsoft Docs
description: Learn how to read or write partitioned data in Azure Data Factory.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/15/2018
ms.author: shlo
ms.openlocfilehash: 59644f3318e2bf9c4f0ea6c3f5699fe1d19f2089
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864470"
---
# <a name="how-to-read-or-write-partitioned-data-in-azure-data-factory"></a><span data-ttu-id="7fa98-103">How to read or write partitioned data in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7fa98-103">How to read or write partitioned data in Azure Data Factory</span></span>
<span data-ttu-id="7fa98-104">In version 1, Azure Data Factory supported reading or writing partitioned data by using SliceStart/SliceEnd/WindowStart/WindowEnd system variables.</span><span class="sxs-lookup"><span data-stu-id="7fa98-104">In version 1, Azure Data Factory supported reading or writing partitioned data by using SliceStart/SliceEnd/WindowStart/WindowEnd system variables.</span></span> <span data-ttu-id="7fa98-105">In the current version of Data Factory, you can achieve this behavior by using a pipeline parameter and trigger's start time/scheduled time as a value of the parameter.</span><span class="sxs-lookup"><span data-stu-id="7fa98-105">In the current version of Data Factory, you can achieve this behavior by using a pipeline parameter and trigger's start time/scheduled time as a value of the parameter.</span></span> 

## <a name="use-a-pipeline-parameter"></a><span data-ttu-id="7fa98-106">Use a pipeline parameter</span><span class="sxs-lookup"><span data-stu-id="7fa98-106">Use a pipeline parameter</span></span> 
<span data-ttu-id="7fa98-107">In version 1, you could use the partitionedBy property and SliceStart system variable as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="7fa98-107">In version 1, you could use the partitionedBy property and SliceStart system variable as shown in the following example:</span></span> 

```json
"folderPath": "adfcustomerprofilingsample/logs/marketingcampaigneffectiveness/{Year}/{Month}/{Day}/",
"partitionedBy": [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "%M" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "%d" } }
],
```

<span data-ttu-id="7fa98-108">For more information about the partitonedBy property, see [version 1 Azure Blob connector](v1/data-factory-azure-blob-connector.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="7fa98-108">For more information about the partitonedBy property, see [version 1 Azure Blob connector](v1/data-factory-azure-blob-connector.md#dataset-properties) article.</span></span> 

<span data-ttu-id="7fa98-109">In the current version of Data Factory, a way to achieve this behavior is to do the following actions:</span><span class="sxs-lookup"><span data-stu-id="7fa98-109">In the current version of Data Factory, a way to achieve this behavior is to do the following actions:</span></span> 

1. <span data-ttu-id="7fa98-110">Define a **pipeline parameter** of type string.</span><span class="sxs-lookup"><span data-stu-id="7fa98-110">Define a **pipeline parameter** of type string.</span></span> <span data-ttu-id="7fa98-111">In the following example, name of the pipeline parameter is **windowStartTime**.</span><span class="sxs-lookup"><span data-stu-id="7fa98-111">In the following example, name of the pipeline parameter is **windowStartTime**.</span></span> 
2. <span data-ttu-id="7fa98-112">Set **folderPath** in the dataset definition to reference the value of pipeline parameter.</span><span class="sxs-lookup"><span data-stu-id="7fa98-112">Set **folderPath** in the dataset definition to reference the value of pipeline parameter.</span></span> 
3. <span data-ttu-id="7fa98-113">Pass the actual value for the parameter when invoking the pipeline on-demand, or pass a trigger's start time/scheduled time dynamically at runtime.</span><span class="sxs-lookup"><span data-stu-id="7fa98-113">Pass the actual value for the parameter when invoking the pipeline on-demand, or pass a trigger's start time/scheduled time dynamically at runtime.</span></span> 

```json
"folderPath": {
      "value": "adfcustomerprofilingsample/logs/marketingcampaigneffectiveness/@{formatDateTime(pipeline().parameters.windowStartTime, 'yyyy/MM/dd')}/",
      "type": "Expression"
},
```

## <a name="pass-in-value-from-a-trigger"></a><span data-ttu-id="7fa98-114">Pass in value from a trigger</span><span class="sxs-lookup"><span data-stu-id="7fa98-114">Pass in value from a trigger</span></span>
<span data-ttu-id="7fa98-115">In the following tumbling window trigger definition, window start time of the trigger is passed as a value for the pipeline parameter  **windowStartTime**:</span><span class="sxs-lookup"><span data-stu-id="7fa98-115">In the following tumbling window trigger definition, window start time of the trigger is passed as a value for the pipeline parameter  **windowStartTime**:</span></span> 

```json
{
    "name": "MyTrigger",
    "properties": {
        "type": "TumblingWindowTrigger",
        "typeProperties": {
            "frequency": "Hour",
            "interval": "1",
            "startTime": "2018-05-15T00:00:00Z",
            "delay": "00:10:00",
            "maxConcurrency": 10
        },
        "pipeline": {
            "pipelineReference": {
                "type": "PipelineReference",
                "referenceName": "MyPipeline"
            },
            "parameters": {
                "windowStartTime": "@trigger().outputs.windowStartTime"
            }
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="7fa98-116">Example</span><span class="sxs-lookup"><span data-stu-id="7fa98-116">Example</span></span>

<span data-ttu-id="7fa98-117">Here is a sample dataset definition:</span><span class="sxs-lookup"><span data-stu-id="7fa98-117">Here is a sample dataset definition:</span></span>

```json
{
  "name": "SampleBlobDataset",
  "type": "AzureBlob",
  "typeProperties": {
    "folderPath": {
      "value": "adfcustomerprofilingsample/logs/marketingcampaigneffectiveness/@{formatDateTime(pipeline().parameters.windowStartTime, 'yyyy/MM/dd')}/",
      "type": "Expression"
    },
    "format": {
      "type": "TextFormat",
      "columnDelimiter": ","
    }
  },
  "structure": [
    { "name": "ProfileID", "type": "String" },
    { "name": "SessionStart", "type": "String" },
    { "name": "Duration", "type": "Int32" },
    { "name": "State", "type": "String" },
    { "name": "SrcIPAddress", "type": "String" },
    { "name": "GameType", "type": "String" },
    { "name": "Multiplayer", "type": "String" },
    { "name": "EndRank", "type": "String" },
    { "name": "WeaponsUsed", "type": "Int32" },
    { "name": "UsersInteractedWith", "type": "String" },
    { "name": "Impressions", "type": "String" }
  ],
  "linkedServiceName": {
    "referenceName": "churnStorageLinkedService",
    "type": "LinkedServiceReference"
  }
}
```

<span data-ttu-id="7fa98-118">Pipeline definition:</span><span class="sxs-lookup"><span data-stu-id="7fa98-118">Pipeline definition:</span></span> 

```json
{
    "properties": {
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": {
                    "value": "@concat(pipeline().parameters.blobContainer, '/scripts/', pipeline().parameters.partitionHiveScriptFile)",
                    "type": "Expression"
                },
                "scriptLinkedService": {
                    "referenceName": "churnStorageLinkedService",
                    "type": "LinkedServiceReference"
                },
                "defines": {
                    "RAWINPUT": {
                        "value": "@concat('wasb://', pipeline().parameters.blobContainer, '@', pipeline().parameters.blobStorageAccount, '.blob.core.windows.net/logs/', pipeline().parameters.inputRawLogsFolder, '/')",
                        "type": "Expression"
                    },
                    "Year": {
                        "value": "@formatDateTime(pipeline().parameters.windowStartTime, 'yyyy')",
                        "type": "Expression"
                    },
                    "Month": {
                        "value": "@formatDateTime(pipeline().parameters.windowStartTime, 'MM')",
                        "type": "Expression"
                    },
                    "Day": {
                        "value": "@formatDateTime(pipeline().parameters.windowStartTime, 'dd')",
                        "type": "Expression"
                    }
                }
            },
            "linkedServiceName": {
                "referenceName": "HdiLinkedService",
                "type": "LinkedServiceReference"
            },
            "name": "HivePartitionGameLogs"
        }],
        "parameters": {
            "windowStartTime": {
                "type": "String"
            },
            "blobStorageAccount": {
                "type": "String"
            },
            "blobContainer": {
                "type": "String"
            },
            "inputRawLogsFolder": {
                "type": "String"
            }
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="7fa98-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="7fa98-119">Next steps</span></span>
<span data-ttu-id="7fa98-120">For a complete walkthrough of creating a data factory with a pipeline, see [Quickstart: create a data factory](quickstart-create-data-factory-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7fa98-120">For a complete walkthrough of creating a data factory with a pipeline, see [Quickstart: create a data factory](quickstart-create-data-factory-powershell.md).</span></span> 
