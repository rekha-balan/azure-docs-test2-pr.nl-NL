---
title: Until activity in Azure Data Factory | Microsoft Docs
description: The Until activity executes a set of activities in a loop until the condition associated with the activity evaluates to true or it times out.
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
ms.date: 01/10/2018
ms.author: shlo
ms.openlocfilehash: cd4b58dea43e497a2d7a5b977379d95f7004af45
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870997"
---
# <a name="until-activity-in-azure-data-factory"></a><span data-ttu-id="ece1a-103">Until activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ece1a-103">Until activity in Azure Data Factory</span></span>
<span data-ttu-id="ece1a-104">The Until activity provides the same functionality that a do-until looping structure provides in programming languages.</span><span class="sxs-lookup"><span data-stu-id="ece1a-104">The Until activity provides the same functionality that a do-until looping structure provides in programming languages.</span></span> <span data-ttu-id="ece1a-105">It executes a set of activities in a loop until the condition associated with the activity evaluates to true.</span><span class="sxs-lookup"><span data-stu-id="ece1a-105">It executes a set of activities in a loop until the condition associated with the activity evaluates to true.</span></span> <span data-ttu-id="ece1a-106">You can specify a timeout value for the until activity in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ece1a-106">You can specify a timeout value for the until activity in Data Factory.</span></span> 

## <a name="syntax"></a><span data-ttu-id="ece1a-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="ece1a-107">Syntax</span></span>

```json
{
    "type": "Until",
    "typeProperties": {
        "expression":  {
            "value":  "<expression that evaluates to true or false>", 
            "type": "Expression"
        },
        "timeout": "<time out for the loop. for example: 00:01:00 (1 minute)>",
        "activities": [
            {
                "<Activity 1 definition>"
            },
            {
                "<Activity 2 definition>"
            },
            {
                "<Activity N definition>"
            }
        ]
    },
    "name": "MyUntilActivity"
}

```

## <a name="type-properties"></a><span data-ttu-id="ece1a-108">Type properties</span><span class="sxs-lookup"><span data-stu-id="ece1a-108">Type properties</span></span>

<span data-ttu-id="ece1a-109">Property</span><span class="sxs-lookup"><span data-stu-id="ece1a-109">Property</span></span> | <span data-ttu-id="ece1a-110">Description</span><span class="sxs-lookup"><span data-stu-id="ece1a-110">Description</span></span> | <span data-ttu-id="ece1a-111">Allowed values</span><span class="sxs-lookup"><span data-stu-id="ece1a-111">Allowed values</span></span> | <span data-ttu-id="ece1a-112">Required</span><span class="sxs-lookup"><span data-stu-id="ece1a-112">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="ece1a-113">name</span><span class="sxs-lookup"><span data-stu-id="ece1a-113">name</span></span> | <span data-ttu-id="ece1a-114">Name of the `Until` activity.</span><span class="sxs-lookup"><span data-stu-id="ece1a-114">Name of the `Until` activity.</span></span> | <span data-ttu-id="ece1a-115">String</span><span class="sxs-lookup"><span data-stu-id="ece1a-115">String</span></span> | <span data-ttu-id="ece1a-116">Yes</span><span class="sxs-lookup"><span data-stu-id="ece1a-116">Yes</span></span>
<span data-ttu-id="ece1a-117">type</span><span class="sxs-lookup"><span data-stu-id="ece1a-117">type</span></span> | <span data-ttu-id="ece1a-118">Must be set to **Until**.</span><span class="sxs-lookup"><span data-stu-id="ece1a-118">Must be set to **Until**.</span></span> | <span data-ttu-id="ece1a-119">String</span><span class="sxs-lookup"><span data-stu-id="ece1a-119">String</span></span> | <span data-ttu-id="ece1a-120">Yes</span><span class="sxs-lookup"><span data-stu-id="ece1a-120">Yes</span></span>
<span data-ttu-id="ece1a-121">expression</span><span class="sxs-lookup"><span data-stu-id="ece1a-121">expression</span></span> | <span data-ttu-id="ece1a-122">Expression that must evaluate to true or false</span><span class="sxs-lookup"><span data-stu-id="ece1a-122">Expression that must evaluate to true or false</span></span> | <span data-ttu-id="ece1a-123">Expression.</span><span class="sxs-lookup"><span data-stu-id="ece1a-123">Expression.</span></span>  | <span data-ttu-id="ece1a-124">Yes</span><span class="sxs-lookup"><span data-stu-id="ece1a-124">Yes</span></span>
<span data-ttu-id="ece1a-125">timeout</span><span class="sxs-lookup"><span data-stu-id="ece1a-125">timeout</span></span> | <span data-ttu-id="ece1a-126">The do-until loop times out after the specified time here.</span><span class="sxs-lookup"><span data-stu-id="ece1a-126">The do-until loop times out after the specified time here.</span></span> | <span data-ttu-id="ece1a-127">String.</span><span class="sxs-lookup"><span data-stu-id="ece1a-127">String.</span></span> <span data-ttu-id="ece1a-128">`d.hh:mm:ss` (or) `hh:mm:ss`.</span><span class="sxs-lookup"><span data-stu-id="ece1a-128">`d.hh:mm:ss` (or) `hh:mm:ss`.</span></span> <span data-ttu-id="ece1a-129">The default value is 7 days.</span><span class="sxs-lookup"><span data-stu-id="ece1a-129">The default value is 7 days.</span></span> <span data-ttu-id="ece1a-130">Maximum value is: 90 days.</span><span class="sxs-lookup"><span data-stu-id="ece1a-130">Maximum value is: 90 days.</span></span> | <span data-ttu-id="ece1a-131">No</span><span class="sxs-lookup"><span data-stu-id="ece1a-131">No</span></span>
<span data-ttu-id="ece1a-132">Activities</span><span class="sxs-lookup"><span data-stu-id="ece1a-132">Activities</span></span> | <span data-ttu-id="ece1a-133">Set of activities that are executed until expression evaluates to `true`.</span><span class="sxs-lookup"><span data-stu-id="ece1a-133">Set of activities that are executed until expression evaluates to `true`.</span></span> | <span data-ttu-id="ece1a-134">Array of activities.</span><span class="sxs-lookup"><span data-stu-id="ece1a-134">Array of activities.</span></span> |  <span data-ttu-id="ece1a-135">Yes</span><span class="sxs-lookup"><span data-stu-id="ece1a-135">Yes</span></span>

## <a name="example-1"></a><span data-ttu-id="ece1a-136">Example 1</span><span class="sxs-lookup"><span data-stu-id="ece1a-136">Example 1</span></span>

> [!NOTE]
> <span data-ttu-id="ece1a-137">This section provides JSON definitions and sample PowerShell commands to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="ece1a-137">This section provides JSON definitions and sample PowerShell commands to run the pipeline.</span></span> <span data-ttu-id="ece1a-138">For a walkthrough with step-by-step instructions to create a Data Factory pipeline by using Azure PowerShell and JSON definitions, see [tutorial: create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ece1a-138">For a walkthrough with step-by-step instructions to create a Data Factory pipeline by using Azure PowerShell and JSON definitions, see [tutorial: create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span></span>

### <a name="pipeline-with-until-activity"></a><span data-ttu-id="ece1a-139">Pipeline with Until activity</span><span class="sxs-lookup"><span data-stu-id="ece1a-139">Pipeline with Until activity</span></span>
<span data-ttu-id="ece1a-140">In this example, the pipeline has two activities: **Until** and **Wait**.</span><span class="sxs-lookup"><span data-stu-id="ece1a-140">In this example, the pipeline has two activities: **Until** and **Wait**.</span></span> <span data-ttu-id="ece1a-141">The Wait activity waits for the specified period of time before running the Web activity in the loop.</span><span class="sxs-lookup"><span data-stu-id="ece1a-141">The Wait activity waits for the specified period of time before running the Web activity in the loop.</span></span> <span data-ttu-id="ece1a-142">To learn about expressions and functions in Data Factory, see [Expression language and functions](control-flow-expression-language-functions.md).</span><span class="sxs-lookup"><span data-stu-id="ece1a-142">To learn about expressions and functions in Data Factory, see [Expression language and functions](control-flow-expression-language-functions.md).</span></span> 

```json
{
    "name": "DoUntilPipeline",
    "properties": {
        "activities": [
            {
                "type": "Until",
                "typeProperties": {
                    "expression": {
                        "value": "@equals('Failed', coalesce(body('MyUnauthenticatedActivity')?.status, actions('MyUnauthenticatedActivity')?.status, 'null'))",
                        "type": "Expression"
                    },
                    "timeout": "00:00:01",
                    "activities": [
                        {
                            "name": "MyUnauthenticatedActivity",
                            "type": "WebActivity",
                            "typeProperties": {
                                "method": "get",
                                "url": "https://www.fake.com/",
                                "headers": {
                                    "Content-Type": "application/json"
                                }
                            },
                            "dependsOn": [
                                {
                                    "activity": "MyWaitActivity",
                                    "dependencyConditions": [ "Succeeded" ]
                                }
                            ]
                        },
                        {
                            "type": "Wait",
                            "typeProperties": {
                                "waitTimeInSeconds": 1
                            },
                            "name": "MyWaitActivity"
                        }
                    ]
                },
                "name": "MyUntilActivity"
            }
        ]
    }
}

```

## <a name="example-2"></a><span data-ttu-id="ece1a-143">Example 2</span><span class="sxs-lookup"><span data-stu-id="ece1a-143">Example 2</span></span> 
<span data-ttu-id="ece1a-144">The pipeline in this sample copies data from an input folder to an output folder in a loop.</span><span class="sxs-lookup"><span data-stu-id="ece1a-144">The pipeline in this sample copies data from an input folder to an output folder in a loop.</span></span> <span data-ttu-id="ece1a-145">The loop terminates when the value for the repeat parameter is set to false or it times out after one minute.</span><span class="sxs-lookup"><span data-stu-id="ece1a-145">The loop terminates when the value for the repeat parameter is set to false or it times out after one minute.</span></span>   

### <a name="pipeline-with-until-activity-adfv2quickstartpipelinejson"></a><span data-ttu-id="ece1a-146">Pipeline with Until activity (Adfv2QuickStartPipeline.json)</span><span class="sxs-lookup"><span data-stu-id="ece1a-146">Pipeline with Until activity (Adfv2QuickStartPipeline.json)</span></span>

```json
{
    "name": "Adfv2QuickStartPipeline",
    "properties": {
        "activities": [
            {
                "type": "Until",
                "typeProperties": {
                    "expression":  {
                        "value":  "@equals('false', pipeline().parameters.repeat)", 
                        "type": "Expression"
                    },
                    "timeout": "00:01:00",
                    "activities": [
                        {
                            "name": "CopyFromBlobToBlob",
                            "type": "Copy",
                            "inputs": [
                                {
                                    "referenceName": "BlobDataset",
                                    "parameters": {
                                        "path": "@pipeline().parameters.inputPath"
                                    },
                                    "type": "DatasetReference"
                                }
                            ],
                            "outputs": [
                                {
                                    "referenceName": "BlobDataset",
                                    "parameters": {
                                        "path": "@pipeline().parameters.outputPath"
                                    },
                                    "type": "DatasetReference"
                                }
                            ],
                            "typeProperties": {
                                "source": {
                                    "type": "BlobSource"
                                },
                                "sink": {
                                    "type": "BlobSink"
                                }
                            },
                            "policy": {
                                "retry": 1,
                                "timeout": "00:10:00",
                                "retryIntervalInSeconds": 60
                            }
                        }
                    ]
                },
                "name": "MyUntilActivity"
            }
        ],
        "parameters": {
            "inputPath": {
                "type": "String"
            },
            "outputPath": {
                "type": "String"
            },
            "repeat": {
                "type": "String"
            }                        
        }        
    }
}

```


### <a name="azure-storage-linked-service-azurestoragelinkedservicejson"></a><span data-ttu-id="ece1a-147">Azure Storage linked service (AzureStorageLinkedService.json)</span><span class="sxs-lookup"><span data-stu-id="ece1a-147">Azure Storage linked service (AzureStorageLinkedService.json)</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": {
                "value": "DefaultEndpointsProtocol=https;AccountName=<Azure Storage account name>;AccountKey=<Azure Storage account key>",
                "type": "SecureString"
            }
        }
    }
}
```

### <a name="parameterized-azure-blob-dataset-blobdatasetjson"></a><span data-ttu-id="ece1a-148">Parameterized Azure Blob dataset (BlobDataset.json)</span><span class="sxs-lookup"><span data-stu-id="ece1a-148">Parameterized Azure Blob dataset (BlobDataset.json)</span></span>
<span data-ttu-id="ece1a-149">The pipeline sets the **folderPath** to the value of either **outputPath1** or **outputPath2** parameter of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="ece1a-149">The pipeline sets the **folderPath** to the value of either **outputPath1** or **outputPath2** parameter of the pipeline.</span></span> 

```json
{
    "name": "BlobDataset",
    "properties": {
        "type": "AzureBlob",
        "typeProperties": {
            "folderPath": {
                "value": "@{dataset().path}",
                "type": "Expression"
            }
        },
        "linkedServiceName": {
            "referenceName": "AzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "parameters": {
            "path": {
                "type": "String"
            }
        }
    }
}
```

### <a name="pipeline-parameter-json-pipelineparametersjson"></a><span data-ttu-id="ece1a-150">Pipeline parameter JSON (PipelineParameters.json)</span><span class="sxs-lookup"><span data-stu-id="ece1a-150">Pipeline parameter JSON (PipelineParameters.json)</span></span>

```json
{
    "inputPath": "adftutorial/input",
    "outputPath": "adftutorial/outputUntil",
    "repeat": "true"
}
```

### <a name="powershell-commands"></a><span data-ttu-id="ece1a-151">PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="ece1a-151">PowerShell commands</span></span>
<span data-ttu-id="ece1a-152">These commands assume that you have saved the JSON files into the folder: C:\ADF.</span><span class="sxs-lookup"><span data-stu-id="ece1a-152">These commands assume that you have saved the JSON files into the folder: C:\ADF.</span></span> 

```powershell
Connect-AzureRmAccount
Select-AzureRmSubscription "<Your subscription name>"

$resourceGroupName = "<Resource Group Name>"
$dataFactoryName = "<Data Factory Name. Must be globally unique>";
Remove-AzureRmDataFactoryV2 $dataFactoryName -ResourceGroupName $resourceGroupName -force


Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location "East US" -Name $dataFactoryName
Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -DefinitionFile "C:\ADF\AzureStorageLinkedService.json"
Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "BlobDataset" -DefinitionFile "C:\ADF\BlobDataset.json"
Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "Adfv2QuickStartPipeline" -DefinitionFile "C:\ADF\Adfv2QuickStartPipeline.json"
$runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName "Adfv2QuickStartPipeline" -ParameterFile C:\ADF\PipelineParameters.json

while ($True) {
    $run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $resourceGroupName -DataFactoryName $DataFactoryName -PipelineRunId $runId

    if ($run) {
        if ($run.Status -ne 'InProgress') {
            Write-Host "Pipeline run finished. The status is: " $run.Status -foregroundcolor "Yellow"
            $run
            break
        }
        Write-Host  "Pipeline is running...status: InProgress" -foregroundcolor "Yellow"
        Write-Host "Activity run details:" -foregroundcolor "Yellow"
        $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
        $result

        Write-Host "Activity 'Output' section:" -foregroundcolor "Yellow"
        $result.Output -join "`r`n"
    }

    Start-Sleep -Seconds 15
}
```

## <a name="next-steps"></a><span data-ttu-id="ece1a-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="ece1a-153">Next steps</span></span>
<span data-ttu-id="ece1a-154">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="ece1a-154">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="ece1a-155">If Condition Activity</span><span class="sxs-lookup"><span data-stu-id="ece1a-155">If Condition Activity</span></span>](control-flow-if-condition-activity.md)
- [<span data-ttu-id="ece1a-156">Execute Pipeline Activity</span><span class="sxs-lookup"><span data-stu-id="ece1a-156">Execute Pipeline Activity</span></span>](control-flow-execute-pipeline-activity.md)
- [<span data-ttu-id="ece1a-157">For Each Activity</span><span class="sxs-lookup"><span data-stu-id="ece1a-157">For Each Activity</span></span>](control-flow-for-each-activity.md)
- [<span data-ttu-id="ece1a-158">Get Metadata Activity</span><span class="sxs-lookup"><span data-stu-id="ece1a-158">Get Metadata Activity</span></span>](control-flow-get-metadata-activity.md)
- [<span data-ttu-id="ece1a-159">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="ece1a-159">Lookup Activity</span></span>](control-flow-lookup-activity.md)
- [<span data-ttu-id="ece1a-160">Web Activity</span><span class="sxs-lookup"><span data-stu-id="ece1a-160">Web Activity</span></span>](control-flow-web-activity.md)
