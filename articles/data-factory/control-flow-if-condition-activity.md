---
title: If Condition activity in Azure Data Factory | Microsoft Docs
description: The If Condition activity allows you to control the processing flow based on a condition.
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
ms.openlocfilehash: 5077982bdef4d0e8fbf1ab485566909b4dc97a8a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966997"
---
# <a name="if-condition-activity-in-azure-data-factory"></a><span data-ttu-id="6efb1-103">If Condition activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6efb1-103">If Condition activity in Azure Data Factory</span></span>
<span data-ttu-id="6efb1-104">The If Condition activity provides the same functionality that an if statement provides in programming languages.</span><span class="sxs-lookup"><span data-stu-id="6efb1-104">The If Condition activity provides the same functionality that an if statement provides in programming languages.</span></span> <span data-ttu-id="6efb1-105">It evaluates a set of activities when the condition evaluates to `true` and another set of activities when the condition evaluates to `false`.</span><span class="sxs-lookup"><span data-stu-id="6efb1-105">It evaluates a set of activities when the condition evaluates to `true` and another set of activities when the condition evaluates to `false`.</span></span> 

## <a name="syntax"></a><span data-ttu-id="6efb1-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="6efb1-106">Syntax</span></span>

```json

{
    "name": "<Name of the activity>",
    "type": "IfCondition",
    "typeProperties": {
            "expression": {
            "value": "<expression that evaluates to true or false>",
            "type": "Expression"
            },

            "ifTrueActivities": [
            {
                "<Activity 1 definition>"
            },
            {
                "<Activity 2 definition>"
            },
            {
                "<Activity N definition>"
            }
        ],

        "ifFalseActivities": [
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
    }
}
```

## <a name="type-properties"></a><span data-ttu-id="6efb1-107">Type properties</span><span class="sxs-lookup"><span data-stu-id="6efb1-107">Type properties</span></span>

<span data-ttu-id="6efb1-108">Property</span><span class="sxs-lookup"><span data-stu-id="6efb1-108">Property</span></span> | <span data-ttu-id="6efb1-109">Description</span><span class="sxs-lookup"><span data-stu-id="6efb1-109">Description</span></span> | <span data-ttu-id="6efb1-110">Allowed values</span><span class="sxs-lookup"><span data-stu-id="6efb1-110">Allowed values</span></span> | <span data-ttu-id="6efb1-111">Required</span><span class="sxs-lookup"><span data-stu-id="6efb1-111">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="6efb1-112">name</span><span class="sxs-lookup"><span data-stu-id="6efb1-112">name</span></span> | <span data-ttu-id="6efb1-113">Name of the if-condition activity.</span><span class="sxs-lookup"><span data-stu-id="6efb1-113">Name of the if-condition activity.</span></span> | <span data-ttu-id="6efb1-114">String</span><span class="sxs-lookup"><span data-stu-id="6efb1-114">String</span></span> | <span data-ttu-id="6efb1-115">Yes</span><span class="sxs-lookup"><span data-stu-id="6efb1-115">Yes</span></span>
<span data-ttu-id="6efb1-116">type</span><span class="sxs-lookup"><span data-stu-id="6efb1-116">type</span></span> | <span data-ttu-id="6efb1-117">Must be set to **IfCondition**</span><span class="sxs-lookup"><span data-stu-id="6efb1-117">Must be set to **IfCondition**</span></span> | <span data-ttu-id="6efb1-118">String</span><span class="sxs-lookup"><span data-stu-id="6efb1-118">String</span></span> | <span data-ttu-id="6efb1-119">Yes</span><span class="sxs-lookup"><span data-stu-id="6efb1-119">Yes</span></span>
<span data-ttu-id="6efb1-120">expression</span><span class="sxs-lookup"><span data-stu-id="6efb1-120">expression</span></span> | <span data-ttu-id="6efb1-121">Expression that must evaluate to true or false</span><span class="sxs-lookup"><span data-stu-id="6efb1-121">Expression that must evaluate to true or false</span></span> | <span data-ttu-id="6efb1-122">Expression with result type boolean</span><span class="sxs-lookup"><span data-stu-id="6efb1-122">Expression with result type boolean</span></span> | <span data-ttu-id="6efb1-123">Yes</span><span class="sxs-lookup"><span data-stu-id="6efb1-123">Yes</span></span>
<span data-ttu-id="6efb1-124">ifTrueActivities</span><span class="sxs-lookup"><span data-stu-id="6efb1-124">ifTrueActivities</span></span> | <span data-ttu-id="6efb1-125">Set of activities that are executed when the expression evaluates to `true`.</span><span class="sxs-lookup"><span data-stu-id="6efb1-125">Set of activities that are executed when the expression evaluates to `true`.</span></span> | <span data-ttu-id="6efb1-126">Array</span><span class="sxs-lookup"><span data-stu-id="6efb1-126">Array</span></span> | <span data-ttu-id="6efb1-127">Yes</span><span class="sxs-lookup"><span data-stu-id="6efb1-127">Yes</span></span>
<span data-ttu-id="6efb1-128">ifFalseActivities</span><span class="sxs-lookup"><span data-stu-id="6efb1-128">ifFalseActivities</span></span> | <span data-ttu-id="6efb1-129">Set of activities that are executed when the expression evaluates to `false`.</span><span class="sxs-lookup"><span data-stu-id="6efb1-129">Set of activities that are executed when the expression evaluates to `false`.</span></span> | <span data-ttu-id="6efb1-130">Array</span><span class="sxs-lookup"><span data-stu-id="6efb1-130">Array</span></span> | <span data-ttu-id="6efb1-131">Yes</span><span class="sxs-lookup"><span data-stu-id="6efb1-131">Yes</span></span>

## <a name="example"></a><span data-ttu-id="6efb1-132">Example</span><span class="sxs-lookup"><span data-stu-id="6efb1-132">Example</span></span>
<span data-ttu-id="6efb1-133">The pipeline in this example copies data from an input folder to an output folder.</span><span class="sxs-lookup"><span data-stu-id="6efb1-133">The pipeline in this example copies data from an input folder to an output folder.</span></span> <span data-ttu-id="6efb1-134">The output folder is determined by the value of pipeline parameter: routeSelection.</span><span class="sxs-lookup"><span data-stu-id="6efb1-134">The output folder is determined by the value of pipeline parameter: routeSelection.</span></span> <span data-ttu-id="6efb1-135">If the value of routeSelection is true, the data is copied to outputPath1.</span><span class="sxs-lookup"><span data-stu-id="6efb1-135">If the value of routeSelection is true, the data is copied to outputPath1.</span></span> <span data-ttu-id="6efb1-136">And, if the value of routeSelection is false, the data is copied to outputPath2.</span><span class="sxs-lookup"><span data-stu-id="6efb1-136">And, if the value of routeSelection is false, the data is copied to outputPath2.</span></span> 

> [!NOTE]
> <span data-ttu-id="6efb1-137">This section provides JSON definitions and sample PowerShell commands to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="6efb1-137">This section provides JSON definitions and sample PowerShell commands to run the pipeline.</span></span> <span data-ttu-id="6efb1-138">For a walkthrough with step-by-step instructions to create a Data Factory pipeline by using Azure PowerShell and JSON definitions, see [tutorial: create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6efb1-138">For a walkthrough with step-by-step instructions to create a Data Factory pipeline by using Azure PowerShell and JSON definitions, see [tutorial: create a data factory by using Azure PowerShell](quickstart-create-data-factory-powershell.md).</span></span>

### <a name="pipeline-with-if-condition-activity-adfv2quickstartpipelinejson"></a><span data-ttu-id="6efb1-139">Pipeline with IF-Condition activity (Adfv2QuickStartPipeline.json)</span><span class="sxs-lookup"><span data-stu-id="6efb1-139">Pipeline with IF-Condition activity (Adfv2QuickStartPipeline.json)</span></span>

```json
{
    "name": "Adfv2QuickStartPipeline",
    "properties": {
        "activities": [
            {
                "name": "MyIfCondition",
                "type": "IfCondition",
                "typeProperties": {
                    "expression":  {
                        "value":  "@bool(pipeline().parameters.routeSelection)", 
                        "type": "Expression"
                     },
                                           
                    "ifTrueActivities": [
                        {
                            "name": "CopyFromBlobToBlob1",
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
                                        "path": "@pipeline().parameters.outputPath1"
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
                            }
                        }                                   
                    ],
                    "ifFalseActivities": [
                        {
                            "name": "CopyFromBlobToBlob2",
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
                                        "path": "@pipeline().parameters.outputPath2"
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
                            }
                        }
                    ]                    
                }
            }
        ],
        "parameters": {
            "inputPath": {
                "type": "String"
            },
            "outputPath1": {
                "type": "String"
            },
            "outputPath2": {
                "type": "String"
            },
            "routeSelection": {
                "type": "String"
            }                        
        }
    }
}
```

<span data-ttu-id="6efb1-140">Another example for expression is:</span><span class="sxs-lookup"><span data-stu-id="6efb1-140">Another example for expression is:</span></span> 

```json
"expression":  {
    "value":  "@pipeline().parameters.routeSelection == 1", 
    "type": "Expression"
}
```


### <a name="azure-storage-linked-service-azurestoragelinkedservicejson"></a><span data-ttu-id="6efb1-141">Azure Storage linked service (AzureStorageLinkedService.json)</span><span class="sxs-lookup"><span data-stu-id="6efb1-141">Azure Storage linked service (AzureStorageLinkedService.json)</span></span>

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

### <a name="parameterized-azure-blob-dataset-blobdatasetjson"></a><span data-ttu-id="6efb1-142">Parameterized Azure Blob dataset (BlobDataset.json)</span><span class="sxs-lookup"><span data-stu-id="6efb1-142">Parameterized Azure Blob dataset (BlobDataset.json)</span></span>
<span data-ttu-id="6efb1-143">The pipeline sets the **folderPath** to the value of either **outputPath1** or **outputPath2** parameter of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="6efb1-143">The pipeline sets the **folderPath** to the value of either **outputPath1** or **outputPath2** parameter of the pipeline.</span></span> 

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

### <a name="pipeline-parameter-json-pipelineparametersjson"></a><span data-ttu-id="6efb1-144">Pipeline parameter JSON (PipelineParameters.json)</span><span class="sxs-lookup"><span data-stu-id="6efb1-144">Pipeline parameter JSON (PipelineParameters.json)</span></span>

```json
{
    "inputPath": "adftutorial/input",
    "outputPath1": "adftutorial/outputIf",
    "outputPath2": "adftutorial/outputElse",
    "routeSelection": "false"
}
```

### <a name="powershell-commands"></a><span data-ttu-id="6efb1-145">PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="6efb1-145">PowerShell commands</span></span>
<span data-ttu-id="6efb1-146">These commands assume that you have saved the JSON files into the folder: C:\ADF.</span><span class="sxs-lookup"><span data-stu-id="6efb1-146">These commands assume that you have saved the JSON files into the folder: C:\ADF.</span></span> 

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
    }

    Start-Sleep -Seconds 30
}
Write-Host "Activity run details:" -foregroundcolor "Yellow"
$result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
$result

Write-Host "Activity 'Output' section:" -foregroundcolor "Yellow"
$result.Output -join "`r`n"

Write-Host "\nActivity 'Error' section:" -foregroundcolor "Yellow"
$result.Error -join "`r`n"
```

## <a name="next-steps"></a><span data-ttu-id="6efb1-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="6efb1-147">Next steps</span></span>
<span data-ttu-id="6efb1-148">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="6efb1-148">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="6efb1-149">Execute Pipeline Activity</span><span class="sxs-lookup"><span data-stu-id="6efb1-149">Execute Pipeline Activity</span></span>](control-flow-execute-pipeline-activity.md)
- [<span data-ttu-id="6efb1-150">For Each Activity</span><span class="sxs-lookup"><span data-stu-id="6efb1-150">For Each Activity</span></span>](control-flow-for-each-activity.md)
- [<span data-ttu-id="6efb1-151">Get Metadata Activity</span><span class="sxs-lookup"><span data-stu-id="6efb1-151">Get Metadata Activity</span></span>](control-flow-get-metadata-activity.md)
- [<span data-ttu-id="6efb1-152">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="6efb1-152">Lookup Activity</span></span>](control-flow-lookup-activity.md)
- [<span data-ttu-id="6efb1-153">Web Activity</span><span class="sxs-lookup"><span data-stu-id="6efb1-153">Web Activity</span></span>](control-flow-web-activity.md)
