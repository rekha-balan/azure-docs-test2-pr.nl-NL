---
title: Execute Pipeline Activity in Azure Data Factory | Microsoft Docs
description: Learn how you can use the Execute Pipeline Activity to invoke one Data Factory pipeline from another Data Factory pipeline.
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
ms.date: 01/10/2018
ms.author: shlo
ms.openlocfilehash: 2aa25004fb9c2e914cd8c669095953e174686197
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866680"
---
# <a name="execute-pipeline-activity-in-azure-data-factory"></a><span data-ttu-id="1093e-103">Execute Pipeline activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1093e-103">Execute Pipeline activity in Azure Data Factory</span></span>
<span data-ttu-id="1093e-104">The Execute Pipeline activity allows a Data Factory pipeline to invoke another pipeline.</span><span class="sxs-lookup"><span data-stu-id="1093e-104">The Execute Pipeline activity allows a Data Factory pipeline to invoke another pipeline.</span></span>

## <a name="syntax"></a><span data-ttu-id="1093e-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="1093e-105">Syntax</span></span>

```json
{
    "name": "MyPipeline",
    "properties": {
        "activities": [
            {
                "name": "ExecutePipelineActivity",
                "type": "ExecutePipeline",
                "typeProperties": {
                    "parameters": {                        
                        "mySourceDatasetFolderPath": {
                            "value": "@pipeline().parameters.mySourceDatasetFolderPath",
                            "type": "Expression"
                        }
                    },
                    "pipeline": {
                        "referenceName": "<InvokedPipelineName>",
                        "type": "PipelineReference"
                    },
                    "waitOnCompletion": true
                 }
            }
        ],
        "parameters": [
            {
                "mySourceDatasetFolderPath": {
                    "type": "String"
                }
            }
        ]
    }
}
```

## <a name="type-properties"></a><span data-ttu-id="1093e-106">Type properties</span><span class="sxs-lookup"><span data-stu-id="1093e-106">Type properties</span></span>
<span data-ttu-id="1093e-107">Property</span><span class="sxs-lookup"><span data-stu-id="1093e-107">Property</span></span> | <span data-ttu-id="1093e-108">Description</span><span class="sxs-lookup"><span data-stu-id="1093e-108">Description</span></span> | <span data-ttu-id="1093e-109">Allowed values</span><span class="sxs-lookup"><span data-stu-id="1093e-109">Allowed values</span></span> | <span data-ttu-id="1093e-110">Required</span><span class="sxs-lookup"><span data-stu-id="1093e-110">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="1093e-111">name</span><span class="sxs-lookup"><span data-stu-id="1093e-111">name</span></span> | <span data-ttu-id="1093e-112">Name of the execute pipeline activity.</span><span class="sxs-lookup"><span data-stu-id="1093e-112">Name of the execute pipeline activity.</span></span> | <span data-ttu-id="1093e-113">String</span><span class="sxs-lookup"><span data-stu-id="1093e-113">String</span></span> | <span data-ttu-id="1093e-114">Yes</span><span class="sxs-lookup"><span data-stu-id="1093e-114">Yes</span></span>
<span data-ttu-id="1093e-115">type</span><span class="sxs-lookup"><span data-stu-id="1093e-115">type</span></span> | <span data-ttu-id="1093e-116">Must be set to: **ExecutePipeline**.</span><span class="sxs-lookup"><span data-stu-id="1093e-116">Must be set to: **ExecutePipeline**.</span></span> | <span data-ttu-id="1093e-117">String</span><span class="sxs-lookup"><span data-stu-id="1093e-117">String</span></span> | <span data-ttu-id="1093e-118">Yes</span><span class="sxs-lookup"><span data-stu-id="1093e-118">Yes</span></span>
<span data-ttu-id="1093e-119">pipeline</span><span class="sxs-lookup"><span data-stu-id="1093e-119">pipeline</span></span> | <span data-ttu-id="1093e-120">Pipeline reference to the dependent pipeline that this pipeline invokes.</span><span class="sxs-lookup"><span data-stu-id="1093e-120">Pipeline reference to the dependent pipeline that this pipeline invokes.</span></span> <span data-ttu-id="1093e-121">A pipeline reference object has two properties: **referenceName** and **type**.</span><span class="sxs-lookup"><span data-stu-id="1093e-121">A pipeline reference object has two properties: **referenceName** and **type**.</span></span> <span data-ttu-id="1093e-122">The referenceName property specifies the name of the reference pipeline.</span><span class="sxs-lookup"><span data-stu-id="1093e-122">The referenceName property specifies the name of the reference pipeline.</span></span> <span data-ttu-id="1093e-123">The type property must be set to PipelineReference.</span><span class="sxs-lookup"><span data-stu-id="1093e-123">The type property must be set to PipelineReference.</span></span> | <span data-ttu-id="1093e-124">PipelineReference</span><span class="sxs-lookup"><span data-stu-id="1093e-124">PipelineReference</span></span> | <span data-ttu-id="1093e-125">Yes</span><span class="sxs-lookup"><span data-stu-id="1093e-125">Yes</span></span>
<span data-ttu-id="1093e-126">parameters</span><span class="sxs-lookup"><span data-stu-id="1093e-126">parameters</span></span> | <span data-ttu-id="1093e-127">Parameters to be passed to the invoked pipeline</span><span class="sxs-lookup"><span data-stu-id="1093e-127">Parameters to be passed to the invoked pipeline</span></span> | <span data-ttu-id="1093e-128">A JSON object that maps parameter names to argument values</span><span class="sxs-lookup"><span data-stu-id="1093e-128">A JSON object that maps parameter names to argument values</span></span> | <span data-ttu-id="1093e-129">No</span><span class="sxs-lookup"><span data-stu-id="1093e-129">No</span></span>
<span data-ttu-id="1093e-130">waitOnCompletion</span><span class="sxs-lookup"><span data-stu-id="1093e-130">waitOnCompletion</span></span> | <span data-ttu-id="1093e-131">Defines whether activity execution waits for the dependent pipeline execution to finish.</span><span class="sxs-lookup"><span data-stu-id="1093e-131">Defines whether activity execution waits for the dependent pipeline execution to finish.</span></span> | <span data-ttu-id="1093e-132">Default is false.</span><span class="sxs-lookup"><span data-stu-id="1093e-132">Default is false.</span></span> | <span data-ttu-id="1093e-133">Boolean</span><span class="sxs-lookup"><span data-stu-id="1093e-133">Boolean</span></span> | <span data-ttu-id="1093e-134">No</span><span class="sxs-lookup"><span data-stu-id="1093e-134">No</span></span>

## <a name="sample"></a><span data-ttu-id="1093e-135">Sample</span><span class="sxs-lookup"><span data-stu-id="1093e-135">Sample</span></span>
<span data-ttu-id="1093e-136">This scenario has two pipelines:</span><span class="sxs-lookup"><span data-stu-id="1093e-136">This scenario has two pipelines:</span></span>

- <span data-ttu-id="1093e-137">**Master pipeline** - This pipeline has one Execute Pipeline activity that calls the invoked pipeline.</span><span class="sxs-lookup"><span data-stu-id="1093e-137">**Master pipeline** - This pipeline has one Execute Pipeline activity that calls the invoked pipeline.</span></span> <span data-ttu-id="1093e-138">The master pipeline takes two parameters: `masterSourceBlobContainer`, `masterSinkBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="1093e-138">The master pipeline takes two parameters: `masterSourceBlobContainer`, `masterSinkBlobContainer`.</span></span>
- <span data-ttu-id="1093e-139">**Invoked pipeline** - This pipeline has one Copy activity that copies data from an Azure Blob source to Azure Blob sink.</span><span class="sxs-lookup"><span data-stu-id="1093e-139">**Invoked pipeline** - This pipeline has one Copy activity that copies data from an Azure Blob source to Azure Blob sink.</span></span> <span data-ttu-id="1093e-140">The invoked pipeline takes two parameters: `sourceBlobContainer`, `sinkBlobContainer`.</span><span class="sxs-lookup"><span data-stu-id="1093e-140">The invoked pipeline takes two parameters: `sourceBlobContainer`, `sinkBlobContainer`.</span></span>

### <a name="master-pipeline-definition"></a><span data-ttu-id="1093e-141">Master pipeline definition</span><span class="sxs-lookup"><span data-stu-id="1093e-141">Master pipeline definition</span></span>

```json
{
  "name": "masterPipeline",
  "properties": {
    "activities": [
      {
        "type": "ExecutePipeline",
        "typeProperties": {
          "pipeline": {
            "referenceName": "invokedPipeline",
            "type": "PipelineReference"
          },
          "parameters": {
            "sourceBlobContainer": {
              "value": "@pipeline().parameters.masterSourceBlobContainer",
              "type": "Expression"
            },
            "sinkBlobCountainer": {
              "value": "@pipeline().parameters.masterSinkBlobContainer",
              "type": "Expression"
            }
          },
          "waitOnCompletion": true
        },
        "name": "MyExecutePipelineActivity"
      }
    ],
    "parameters": {
      "masterSourceBlobContainer": {
        "type": "String"
      },
      "masterSinkBlobContainer": {
        "type": "String"
      }
    }
  }
}

```

### <a name="invoked-pipeline-definition"></a><span data-ttu-id="1093e-142">Invoked pipeline definition</span><span class="sxs-lookup"><span data-stu-id="1093e-142">Invoked pipeline definition</span></span>

```json
{
  "name": "invokedPipeline",
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
            "referenceName": "SourceBlobDataset",
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

<span data-ttu-id="1093e-143">**Linked service**</span><span class="sxs-lookup"><span data-stu-id="1093e-143">**Linked service**</span></span>

```json
{
    "name": "BlobStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": {
        "value": "DefaultEndpointsProtocol=https;AccountName=*****",
        "type": "SecureString"
      }
    }
  }
}
```

<span data-ttu-id="1093e-144">**Source dataset**</span><span class="sxs-lookup"><span data-stu-id="1093e-144">**Source dataset**</span></span>
```json
{
    "name": "SourceBlobDataset",
    "properties": {
    "type": "AzureBlob",
    "typeProperties": {
      "folderPath": {
        "value": "@pipeline().parameters.sourceBlobContainer",
        "type": "Expression"
      },
      "fileName": "salesforce.txt"
    },
    "linkedServiceName": {
      "referenceName": "BlobStorageLinkedService",
      "type": "LinkedServiceReference"
    }
  }
}
```

<span data-ttu-id="1093e-145">**Sink dataset**</span><span class="sxs-lookup"><span data-stu-id="1093e-145">**Sink dataset**</span></span>
```json
{
    "name": "sinkBlobDataset",
    "properties": {
    "type": "AzureBlob",
    "typeProperties": {
      "folderPath": {
        "value": "@pipeline().parameters.sinkBlobContainer",
        "type": "Expression"
      }
    },
    "linkedServiceName": {
      "referenceName": "BlobStorageLinkedService",
      "type": "LinkedServiceReference"
    }
  }
}
```

### <a name="running-the-pipeline"></a><span data-ttu-id="1093e-146">Running the pipeline</span><span class="sxs-lookup"><span data-stu-id="1093e-146">Running the pipeline</span></span>

<span data-ttu-id="1093e-147">To run the master pipeline in this example, the following values are passed for the masterSourceBlobContainer and masterSinkBlobContainer parameters:</span><span class="sxs-lookup"><span data-stu-id="1093e-147">To run the master pipeline in this example, the following values are passed for the masterSourceBlobContainer and masterSinkBlobContainer parameters:</span></span> 

```json
{
  "masterSourceBlobContainer": "executetest",
  "masterSinkBlobContainer": "executesink"
}
```

<span data-ttu-id="1093e-148">The master pipeline forwards these values to the invoked pipeline as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1093e-148">The master pipeline forwards these values to the invoked pipeline as shown in the following example:</span></span> 

```json
{
    "type": "ExecutePipeline",
    "typeProperties": {
      "pipeline": {
        "referenceName": "invokedPipeline",
        "type": "PipelineReference"
      },
      "parameters": {
        "sourceBlobContainer": {
          "value": "@pipeline().parameters.masterSourceBlobContainer",
          "type": "Expression"
        },
        "sinkBlobCountainer": {
          "value": "@pipeline().parameters.masterSinkBlobContainer",
          "type": "Expression"
        }
      },

      ....
}

```
## <a name="next-steps"></a><span data-ttu-id="1093e-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="1093e-149">Next steps</span></span>
<span data-ttu-id="1093e-150">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="1093e-150">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="1093e-151">For Each Activity</span><span class="sxs-lookup"><span data-stu-id="1093e-151">For Each Activity</span></span>](control-flow-for-each-activity.md)
- [<span data-ttu-id="1093e-152">Get Metadata Activity</span><span class="sxs-lookup"><span data-stu-id="1093e-152">Get Metadata Activity</span></span>](control-flow-get-metadata-activity.md)
- [<span data-ttu-id="1093e-153">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="1093e-153">Lookup Activity</span></span>](control-flow-lookup-activity.md)
- [<span data-ttu-id="1093e-154">Web Activity</span><span class="sxs-lookup"><span data-stu-id="1093e-154">Web Activity</span></span>](control-flow-web-activity.md)
