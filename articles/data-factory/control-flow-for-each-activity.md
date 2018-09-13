---
title: ForEach activity in Azure Data Factory | Microsoft Docs
description: The For Each Activity defines a repeating control flow in your pipeline. It is used for iterating over a collection and execute specified activities.
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
ms.openlocfilehash: 23f00280a69212b9e623ae1da16a681ca30c9d51
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867536"
---
# <a name="foreach-activity-in-azure-data-factory"></a><span data-ttu-id="962c0-104">ForEach activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="962c0-104">ForEach activity in Azure Data Factory</span></span>
<span data-ttu-id="962c0-105">The ForEach Activity defines a repeating control flow in your pipeline.</span><span class="sxs-lookup"><span data-stu-id="962c0-105">The ForEach Activity defines a repeating control flow in your pipeline.</span></span> <span data-ttu-id="962c0-106">This activity is used to iterate over a collection and executes specified activities in a loop.</span><span class="sxs-lookup"><span data-stu-id="962c0-106">This activity is used to iterate over a collection and executes specified activities in a loop.</span></span> <span data-ttu-id="962c0-107">The loop implementation of this activity is similar to Foreach looping structure in programming languages.</span><span class="sxs-lookup"><span data-stu-id="962c0-107">The loop implementation of this activity is similar to Foreach looping structure in programming languages.</span></span>

## <a name="syntax"></a><span data-ttu-id="962c0-108">Syntax</span><span class="sxs-lookup"><span data-stu-id="962c0-108">Syntax</span></span>
<span data-ttu-id="962c0-109">The properties are described later in this article.</span><span class="sxs-lookup"><span data-stu-id="962c0-109">The properties are described later in this article.</span></span> <span data-ttu-id="962c0-110">The items property is the collection and each item in the collection is referred to by using the `@item()` as shown in the following syntax:</span><span class="sxs-lookup"><span data-stu-id="962c0-110">The items property is the collection and each item in the collection is referred to by using the `@item()` as shown in the following syntax:</span></span>  

```json
{  
   "name":"MyForEachActivityName",
   "type":"ForEach",
   "typeProperties":{  
      "isSequential":"true",
        "items": {
            "value": "@pipeline().parameters.mySinkDatasetFolderPathCollection",
            "type": "Expression"
        },
      "activities":[  
         {  
            "name":"MyCopyActivity",
            "type":"Copy",
            "typeProperties":{  
               ...
            },
            "inputs":[  
               {  
                  "referenceName":"MyDataset",
                  "type":"DatasetReference",
                  "parameters":{  
                     "MyFolderPath":"@pipeline().parameters.mySourceDatasetFolderPath"
                  }
               }
            ],
            "outputs":[  
               {  
                  "referenceName":"MyDataset",
                  "type":"DatasetReference",
                  "parameters":{  
                     "MyFolderPath":"@item()"
                  }
               }
            ]
         }
      ]
   }
}

```

## <a name="type-properties"></a><span data-ttu-id="962c0-111">Type properties</span><span class="sxs-lookup"><span data-stu-id="962c0-111">Type properties</span></span>

<span data-ttu-id="962c0-112">Property</span><span class="sxs-lookup"><span data-stu-id="962c0-112">Property</span></span> | <span data-ttu-id="962c0-113">Description</span><span class="sxs-lookup"><span data-stu-id="962c0-113">Description</span></span> | <span data-ttu-id="962c0-114">Allowed values</span><span class="sxs-lookup"><span data-stu-id="962c0-114">Allowed values</span></span> | <span data-ttu-id="962c0-115">Required</span><span class="sxs-lookup"><span data-stu-id="962c0-115">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="962c0-116">name</span><span class="sxs-lookup"><span data-stu-id="962c0-116">name</span></span> | <span data-ttu-id="962c0-117">Name of the for-each activity.</span><span class="sxs-lookup"><span data-stu-id="962c0-117">Name of the for-each activity.</span></span> | <span data-ttu-id="962c0-118">String</span><span class="sxs-lookup"><span data-stu-id="962c0-118">String</span></span> | <span data-ttu-id="962c0-119">Yes</span><span class="sxs-lookup"><span data-stu-id="962c0-119">Yes</span></span>
<span data-ttu-id="962c0-120">type</span><span class="sxs-lookup"><span data-stu-id="962c0-120">type</span></span> | <span data-ttu-id="962c0-121">Must be set to **ForEach**</span><span class="sxs-lookup"><span data-stu-id="962c0-121">Must be set to **ForEach**</span></span> | <span data-ttu-id="962c0-122">String</span><span class="sxs-lookup"><span data-stu-id="962c0-122">String</span></span> | <span data-ttu-id="962c0-123">Yes</span><span class="sxs-lookup"><span data-stu-id="962c0-123">Yes</span></span>
<span data-ttu-id="962c0-124">isSequential</span><span class="sxs-lookup"><span data-stu-id="962c0-124">isSequential</span></span> | <span data-ttu-id="962c0-125">Specifies whether the loop should be executed sequentially or in parallel.</span><span class="sxs-lookup"><span data-stu-id="962c0-125">Specifies whether the loop should be executed sequentially or in parallel.</span></span>  <span data-ttu-id="962c0-126">Maximum of 20 loop iterations can be executed at once in parallel).</span><span class="sxs-lookup"><span data-stu-id="962c0-126">Maximum of 20 loop iterations can be executed at once in parallel).</span></span> <span data-ttu-id="962c0-127">For example, if you have a ForEach activity iterating over a copy activity with 10 different source and sink datasets with **isSequential** set to False, all copies are executed at once.</span><span class="sxs-lookup"><span data-stu-id="962c0-127">For example, if you have a ForEach activity iterating over a copy activity with 10 different source and sink datasets with **isSequential** set to False, all copies are executed at once.</span></span> <span data-ttu-id="962c0-128">Default is False.</span><span class="sxs-lookup"><span data-stu-id="962c0-128">Default is False.</span></span> <br/><br/> <span data-ttu-id="962c0-129">If "isSequential" is set to False, ensure that there is a correct configuration to run multiple executables.</span><span class="sxs-lookup"><span data-stu-id="962c0-129">If "isSequential" is set to False, ensure that there is a correct configuration to run multiple executables.</span></span> <span data-ttu-id="962c0-130">Otherwise, this property should be used with caution to avoid incurring write conflicts.</span><span class="sxs-lookup"><span data-stu-id="962c0-130">Otherwise, this property should be used with caution to avoid incurring write conflicts.</span></span> <span data-ttu-id="962c0-131">For more information, see [Parallel execution](#parallel-execution) section.</span><span class="sxs-lookup"><span data-stu-id="962c0-131">For more information, see [Parallel execution](#parallel-execution) section.</span></span> | <span data-ttu-id="962c0-132">Boolean</span><span class="sxs-lookup"><span data-stu-id="962c0-132">Boolean</span></span> | <span data-ttu-id="962c0-133">No.</span><span class="sxs-lookup"><span data-stu-id="962c0-133">No.</span></span> <span data-ttu-id="962c0-134">Default is False.</span><span class="sxs-lookup"><span data-stu-id="962c0-134">Default is False.</span></span>
<span data-ttu-id="962c0-135">batchCount</span><span class="sxs-lookup"><span data-stu-id="962c0-135">batchCount</span></span> | <span data-ttu-id="962c0-136">Batch count to be used for controlling the number of parallel execution (when isSequential is set to false).</span><span class="sxs-lookup"><span data-stu-id="962c0-136">Batch count to be used for controlling the number of parallel execution (when isSequential is set to false).</span></span> | <span data-ttu-id="962c0-137">Integer (maximum 50)</span><span class="sxs-lookup"><span data-stu-id="962c0-137">Integer (maximum 50)</span></span> | <span data-ttu-id="962c0-138">No.</span><span class="sxs-lookup"><span data-stu-id="962c0-138">No.</span></span> <span data-ttu-id="962c0-139">Default is 20.</span><span class="sxs-lookup"><span data-stu-id="962c0-139">Default is 20.</span></span>
<span data-ttu-id="962c0-140">Items</span><span class="sxs-lookup"><span data-stu-id="962c0-140">Items</span></span> | <span data-ttu-id="962c0-141">An expression that returns a JSON Array to be iterated over.</span><span class="sxs-lookup"><span data-stu-id="962c0-141">An expression that returns a JSON Array to be iterated over.</span></span> | <span data-ttu-id="962c0-142">Expression (which returns a JSON Array)</span><span class="sxs-lookup"><span data-stu-id="962c0-142">Expression (which returns a JSON Array)</span></span> | <span data-ttu-id="962c0-143">Yes</span><span class="sxs-lookup"><span data-stu-id="962c0-143">Yes</span></span>
<span data-ttu-id="962c0-144">Activities</span><span class="sxs-lookup"><span data-stu-id="962c0-144">Activities</span></span> | <span data-ttu-id="962c0-145">The activities to be executed.</span><span class="sxs-lookup"><span data-stu-id="962c0-145">The activities to be executed.</span></span> | <span data-ttu-id="962c0-146">List of Activities</span><span class="sxs-lookup"><span data-stu-id="962c0-146">List of Activities</span></span> | <span data-ttu-id="962c0-147">Yes</span><span class="sxs-lookup"><span data-stu-id="962c0-147">Yes</span></span>

## <a name="parallel-execution"></a><span data-ttu-id="962c0-148">Parallel execution</span><span class="sxs-lookup"><span data-stu-id="962c0-148">Parallel execution</span></span>
<span data-ttu-id="962c0-149">If **isSequential** is set to false, the activity iterates in parallel with a maximum of 20 concurrent iterations.</span><span class="sxs-lookup"><span data-stu-id="962c0-149">If **isSequential** is set to false, the activity iterates in parallel with a maximum of 20 concurrent iterations.</span></span> <span data-ttu-id="962c0-150">This setting should be used with caution.</span><span class="sxs-lookup"><span data-stu-id="962c0-150">This setting should be used with caution.</span></span> <span data-ttu-id="962c0-151">If the concurrent iterations are writing to the same folder but to different files, this approach is fine.</span><span class="sxs-lookup"><span data-stu-id="962c0-151">If the concurrent iterations are writing to the same folder but to different files, this approach is fine.</span></span> <span data-ttu-id="962c0-152">If the concurrent iterations are writing concurrently to the exact same file, this approach most likely causes an error.</span><span class="sxs-lookup"><span data-stu-id="962c0-152">If the concurrent iterations are writing concurrently to the exact same file, this approach most likely causes an error.</span></span> 

## <a name="iteration-expression-language"></a><span data-ttu-id="962c0-153">Iteration expression language</span><span class="sxs-lookup"><span data-stu-id="962c0-153">Iteration expression language</span></span>
<span data-ttu-id="962c0-154">In the ForEach activity, provide an array to be iterated over for the property **items**."</span><span class="sxs-lookup"><span data-stu-id="962c0-154">In the ForEach activity, provide an array to be iterated over for the property **items**."</span></span> <span data-ttu-id="962c0-155">Use `@item()` to iterate over a single enumeration in ForEach activity.</span><span class="sxs-lookup"><span data-stu-id="962c0-155">Use `@item()` to iterate over a single enumeration in ForEach activity.</span></span> <span data-ttu-id="962c0-156">For example, if **items** is an array: [1, 2, 3], `@item()` returns 1 in the first iteration, 2 in the second iteration, and 3 in the third iteration.</span><span class="sxs-lookup"><span data-stu-id="962c0-156">For example, if **items** is an array: [1, 2, 3], `@item()` returns 1 in the first iteration, 2 in the second iteration, and 3 in the third iteration.</span></span>

## <a name="iterating-over-a-single-activity"></a><span data-ttu-id="962c0-157">Iterating over a single activity</span><span class="sxs-lookup"><span data-stu-id="962c0-157">Iterating over a single activity</span></span>
<span data-ttu-id="962c0-158">**Scenario:** Copy from the same source file in Azure Blob to multiple destination files in Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="962c0-158">**Scenario:** Copy from the same source file in Azure Blob to multiple destination files in Azure Blob.</span></span>

### <a name="pipeline-definition"></a><span data-ttu-id="962c0-159">Pipeline definition</span><span class="sxs-lookup"><span data-stu-id="962c0-159">Pipeline definition</span></span>

```json
{
    "name": "<MyForEachPipeline>",
    "properties": {
        "activities": [
            {
                "name": "<MyForEachActivity>",
                "type": "ForEach",
                "typeProperties": {
                    "isSequential": "true",
                    "items": {
                        "value": "@pipeline().parameters.mySinkDatasetFolderPath",
                        "type": "Expression"
                    },
                    "activities": [
                        {
                            "name": "MyCopyActivity",
                            "type": "Copy",
                            "typeProperties": {
                                "source": {
                                    "type": "BlobSource",
                                    "recursive": "false"
                                },
                                "sink": {
                                    "type": "BlobSink",
                                    "copyBehavior": "PreserveHierarchy"
                                }
                            },
                            "inputs": [
                                {
                                    "referenceName": "<MyDataset>",
                                    "type": "DatasetReference",
                                    "parameters": {
                                        "MyFolderPath": "@pipeline().parameters.mySourceDatasetFolderPath"
                                    }
                                }
                            ],
                            "outputs": [
                                {
                                    "referenceName": "MyDataset",
                                    "type": "DatasetReference",
                                    "parameters": {
                                        "MyFolderPath": "@item()"
                                    }
                                }
                            ]
                        }
                    ]
                }
            }
        ],
        "parameters": {
            "mySourceDatasetFolderPath": {
                "type": "String"
            },
            "mySinkDatasetFolderPath": {
                "type": "String"
            }
        }
    }
}

```

### <a name="blob-dataset-definition"></a><span data-ttu-id="962c0-160">Blob dataset definition</span><span class="sxs-lookup"><span data-stu-id="962c0-160">Blob dataset definition</span></span>

```json
{  
   "name":"<MyDataset>",
   "properties":{  
      "type":"AzureBlob",
      "typeProperties":{  
         "folderPath":{  
            "value":"@dataset().MyFolderPath",
            "type":"Expression"
         }
      },
      "linkedServiceName":{  
         "referenceName":"StorageLinkedService",
         "type":"LinkedServiceReference"
      },
      "parameters":{  
         "MyFolderPath":{  
            "type":"String"
         }
      }
   }
}

```

### <a name="run-parameter-values"></a><span data-ttu-id="962c0-161">Run parameter values</span><span class="sxs-lookup"><span data-stu-id="962c0-161">Run parameter values</span></span>

```json
{
    "mySourceDatasetFolderPath": "input/",
    "mySinkDatasetFolderPath": [ "outputs/file1", "outputs/file2" ]
}

```

## <a name="iterate-over-multiple-activities"></a><span data-ttu-id="962c0-162">Iterate over multiple activities</span><span class="sxs-lookup"><span data-stu-id="962c0-162">Iterate over multiple activities</span></span>
<span data-ttu-id="962c0-163">It's possible to iterate over multiple activities (for example: copy and web activities) in a ForEach activity.</span><span class="sxs-lookup"><span data-stu-id="962c0-163">It's possible to iterate over multiple activities (for example: copy and web activities) in a ForEach activity.</span></span> <span data-ttu-id="962c0-164">In this scenario, we recommend that you abstract out multiple activities into a separate pipeline.</span><span class="sxs-lookup"><span data-stu-id="962c0-164">In this scenario, we recommend that you abstract out multiple activities into a separate pipeline.</span></span> <span data-ttu-id="962c0-165">Then, you can use the [ExecutePipeline activity](control-flow-execute-pipeline-activity.md) in the pipeline with ForEach activity to invoke the separate pipeline with multiple activities.</span><span class="sxs-lookup"><span data-stu-id="962c0-165">Then, you can use the [ExecutePipeline activity](control-flow-execute-pipeline-activity.md) in the pipeline with ForEach activity to invoke the separate pipeline with multiple activities.</span></span> 


### <a name="syntax"></a><span data-ttu-id="962c0-166">Syntax</span><span class="sxs-lookup"><span data-stu-id="962c0-166">Syntax</span></span>

```json
{
  "name": "masterPipeline",
  "properties": {
    "activities": [
      {
        "type": "ForEach",
        "name": "<MyForEachMultipleActivities>"
        "typeProperties": {
          "isSequential": true,
          "items": {
            ...
          },
          "activities": [
            {
              "type": "ExecutePipeline",
              "name": "<MyInnerPipeline>"
              "typeProperties": {
                "pipeline": {
                  "referenceName": "<copyHttpPipeline>",
                  "type": "PipelineReference"
                },
                "parameters": {
                  ...
                },
                "waitOnCompletion": true
              }
            }
          ]
        }
      }
    ],
    "parameters": {
      ...
    }
  }
}

```
### <a name="example"></a><span data-ttu-id="962c0-167">Example</span><span class="sxs-lookup"><span data-stu-id="962c0-167">Example</span></span>
<span data-ttu-id="962c0-168">**Scenario:** Iterate over an InnerPipeline within a ForEach activity with Execute Pipeline activity.</span><span class="sxs-lookup"><span data-stu-id="962c0-168">**Scenario:** Iterate over an InnerPipeline within a ForEach activity with Execute Pipeline activity.</span></span> <span data-ttu-id="962c0-169">The inner pipeline copies with schema definitions parameterized.</span><span class="sxs-lookup"><span data-stu-id="962c0-169">The inner pipeline copies with schema definitions parameterized.</span></span>

#### <a name="master-pipeline-definition"></a><span data-ttu-id="962c0-170">Master Pipeline definition</span><span class="sxs-lookup"><span data-stu-id="962c0-170">Master Pipeline definition</span></span>

```json
{
  "name": "masterPipeline",
  "properties": {
    "activities": [
      {
        "type": "ForEach",
        "name": "MyForEachActivity",
        "typeProperties": {
          "isSequential": true,
          "items": {
            "value": "@pipeline().parameters.inputtables",
            "type": "Expression"
          },
          "activities": [
            {
              "type": "ExecutePipeline",
              "typeProperties": {
                "pipeline": {
                  "referenceName": "InnerCopyPipeline",
                  "type": "PipelineReference"
                },
                "parameters": {
                  "sourceTableName": {
                    "value": "@item().SourceTable",
                    "type": "Expression"
                  },
                  "sourceTableStructure": {
                    "value": "@item().SourceTableStructure",
                    "type": "Expression"
                  },
                  "sinkTableName": {
                    "value": "@item().DestTable",
                    "type": "Expression"
                  },
                  "sinkTableStructure": {
                    "value": "@item().DestTableStructure",
                    "type": "Expression"
                  }
                },
                "waitOnCompletion": true
              },
              "name": "ExecuteCopyPipeline"
            }
          ]
        }
      }
    ],
    "parameters": {
      "inputtables": {
        "type": "Array"
      }
    }
  }
}

```

#### <a name="inner-pipeline-definition"></a><span data-ttu-id="962c0-171">Inner pipeline definition</span><span class="sxs-lookup"><span data-stu-id="962c0-171">Inner pipeline definition</span></span>

```json
{
  "name": "InnerCopyPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            }
          },
          "sink": {
            "type": "SqlSink"
          }
        },
        "name": "CopyActivity",
        "inputs": [
          {
            "referenceName": "sqlSourceDataset",
            "parameters": {
              "SqlTableName": {
                "value": "@pipeline().parameters.sourceTableName",
                "type": "Expression"
              },
              "SqlTableStructure": {
                "value": "@pipeline().parameters.sourceTableStructure",
                "type": "Expression"
              }
            },
            "type": "DatasetReference"
          }
        ],
        "outputs": [
          {
            "referenceName": "sqlSinkDataset",
            "parameters": {
              "SqlTableName": {
                "value": "@pipeline().parameters.sinkTableName",
                "type": "Expression"
              },
              "SqlTableStructure": {
                "value": "@pipeline().parameters.sinkTableStructure",
                "type": "Expression"
              }
            },
            "type": "DatasetReference"
          }
        ]
      }
    ],
    "parameters": {
      "sourceTableName": {
        "type": "String"
      },
      "sourceTableStructure": {
        "type": "String"
      },
      "sinkTableName": {
        "type": "String"
      },
      "sinkTableStructure": {
        "type": "String"
      }
    }
  }
}

```

#### <a name="source-dataset-definition"></a><span data-ttu-id="962c0-172">Source dataset definition</span><span class="sxs-lookup"><span data-stu-id="962c0-172">Source dataset definition</span></span>

```json
{
  "name": "sqlSourceDataset",
  "properties": {
    "type": "SqlServerTable",
    "typeProperties": {
      "tableName": {
        "value": "@dataset().SqlTableName",
        "type": "Expression"
      }
    },
    "structure": {
      "value": "@dataset().SqlTableStructure",
      "type": "Expression"
    },
    "linkedServiceName": {
      "referenceName": "sqlserverLS",
      "type": "LinkedServiceReference"
    },
    "parameters": {
      "SqlTableName": {
        "type": "String"
      },
      "SqlTableStructure": {
        "type": "String"
      }
    }
  }
}

```

#### <a name="sink-dataset-definition"></a><span data-ttu-id="962c0-173">Sink dataset definition</span><span class="sxs-lookup"><span data-stu-id="962c0-173">Sink dataset definition</span></span>

```json
{
  "name": "sqlSinkDataSet",
  "properties": {
    "type": "AzureSqlTable",
    "typeProperties": {
      "tableName": {
        "value": "@dataset().SqlTableName",
        "type": "Expression"
      }
    },
    "structure": {
      "value": "@dataset().SqlTableStructure",
      "type": "Expression"
    },
    "linkedServiceName": {
      "referenceName": "azureSqlLS",
      "type": "LinkedServiceReference"
    },
    "parameters": {
      "SqlTableName": {
        "type": "String"
      },
      "SqlTableStructure": {
        "type": "String"
      }
    }
  }
}

```

#### <a name="master-pipeline-parameters"></a><span data-ttu-id="962c0-174">Master pipeline parameters</span><span class="sxs-lookup"><span data-stu-id="962c0-174">Master pipeline parameters</span></span>
```json
{
    "inputtables": [
        {
            "SourceTable": "department",
            "SourceTableStructure": [
              {
                "name": "departmentid",
                "type": "int"
              },
              {
                "name": "departmentname",
                "type": "string"
              }
            ],
            "DestTable": "department2",
            "DestTableStructure": [
              {
                "name": "departmentid",
                "type": "int"
              },
              {
                "name": "departmentname",
                "type": "string"
              }
            ]
        }
    ]
    
}

```
## <a name="aggregating-metric-output"></a><span data-ttu-id="962c0-175">Aggregating metric output</span><span class="sxs-lookup"><span data-stu-id="962c0-175">Aggregating metric output</span></span>
<span data-ttu-id="962c0-176">Expression for gathering the output of all the iterations of a ForEach is `@activity('NameofInnerActivity')`.</span><span class="sxs-lookup"><span data-stu-id="962c0-176">Expression for gathering the output of all the iterations of a ForEach is `@activity('NameofInnerActivity')`.</span></span> <span data-ttu-id="962c0-177">For example, if a ForEach Activity iterated over a "MyCopyActivity," the syntax would be: `@activity('MyCopyActivity')`.</span><span class="sxs-lookup"><span data-stu-id="962c0-177">For example, if a ForEach Activity iterated over a "MyCopyActivity," the syntax would be: `@activity('MyCopyActivity')`.</span></span> <span data-ttu-id="962c0-178">The output is an array, with each item giving details about a specific iteration.</span><span class="sxs-lookup"><span data-stu-id="962c0-178">The output is an array, with each item giving details about a specific iteration.</span></span>

> [!NOTE]
> <span data-ttu-id="962c0-179">If you want details about a specific iteration, the syntax would be: `@activity('NameofInnerActivity')[0]` for the latest iteration.</span><span class="sxs-lookup"><span data-stu-id="962c0-179">If you want details about a specific iteration, the syntax would be: `@activity('NameofInnerActivity')[0]` for the latest iteration.</span></span> <span data-ttu-id="962c0-180">Use the number in the brackets to access the specific iteration of the array.</span><span class="sxs-lookup"><span data-stu-id="962c0-180">Use the number in the brackets to access the specific iteration of the array.</span></span> <span data-ttu-id="962c0-181">To access a specific property of a specific iteration, you would use: `@activity('NameofInnerActivity')[0].output` or `@activity('NameofInnerActivity')[0].pipelineName`.</span><span class="sxs-lookup"><span data-stu-id="962c0-181">To access a specific property of a specific iteration, you would use: `@activity('NameofInnerActivity')[0].output` or `@activity('NameofInnerActivity')[0].pipelineName`.</span></span>

<span data-ttu-id="962c0-182">**Array output details of all Iterations:**</span><span class="sxs-lookup"><span data-stu-id="962c0-182">**Array output details of all Iterations:**</span></span>
```json
[    
    {      
        "pipelineName": "db1f7d2b-dbbd-4ea8-964e-0d9b2d3fe676",      
        "jobId": "a43766cb-ba13-4c68-923a-8349af9a76a3",      
        "activityRunId": "217526fa-0218-42f1-b85c-e0b4f7b170ce",      
        "linkedServiceName": "ADFService",      
        "status": "Succeeded",      
        "statusCode": null,      
        "output": 
            {        
                "progress": 100,        
                "loguri": null,        
                "dataRead": "6.00 Bytes",        
                "dataWritten": "6.00 Bytes",        
                "regionOrGateway": "West US",        
                "details": "Data Read: 6.00 Bytes, Written: 6.00 Bytes",        
                "copyDuration": "00:00:05",        
                "dataVolume": "6.00 Bytes",        
                "throughput": "1.16 Bytes/s",       
                 "totalDuration": "00:00:10"      
            },      
        "resumptionToken": 
            {       
                "ExecutionId": "217526fa-0218-42f1-b85c-e0b4f7b170ce",        
                "ResumptionToken": 
                    {          
                        "in progress": "217526fa-0218-42f1-b85c-e0b4f7b170ce/wu/cloud/"       
                    },        
                "ExtendedProperties": 
                    {          
                        "dataRead": "6.00 Bytes",          
                        "dataWritten": "6.00 Bytes",          
                        "regionOrGateway": "West US",          
                        "details": "Data Read: 6.00 Bytes, Written: 6.00 Bytes",          
                        "copyDuration": "00:00:05",          
                        "dataVolume": "6.00 Bytes",          
                        "throughput": "1.16 Bytes/s",          
                        "totalDuration": "00:00:10"        
                    }      
            },      
        "error": null,      
        "executionStartTime": "2017-08-01T04:17:27.5747275Z",      
        "executionEndTime": "2017-08-01T04:17:46.4224091Z",     
        "duration": "00:00:18.8476816"    
    },
    {      
        "pipelineName": "db1f7d2b-dbbd-4ea8-964e-0d9b2d3fe676",      
        "jobId": "54232-ba13-4c68-923a-8349af9a76a3",      
        "activityRunId": "217526fa-0218-42f1-b85c-e0b4f7b170ce",      
        "linkedServiceName": "ADFService",      
        "status": "Succeeded",      
        "statusCode": null,      
        "output": 
            {        
                "progress": 100,        
                "loguri": null,        
                "dataRead": "6.00 Bytes",        
                "dataWritten": "6.00 Bytes",        
                "regionOrGateway": "West US",        
                "details": "Data Read: 6.00 Bytes, Written: 6.00 Bytes",        
                "copyDuration": "00:00:05",        
                "dataVolume": "6.00 Bytes",        
                "throughput": "1.16 Bytes/s",       
                 "totalDuration": "00:00:10"      
            },      
        "resumptionToken": 
            {       
                "ExecutionId": "217526fa-0218-42f1-b85c-e0b4f7b170ce",        
                "ResumptionToken": 
                    {          
                        "in progress": "217526fa-0218-42f1-b85c-e0b4f7b170ce/wu/cloud/"       
                    },        
                "ExtendedProperties": 
                    {          
                        "dataRead": "6.00 Bytes",          
                        "dataWritten": "6.00 Bytes",          
                        "regionOrGateway": "West US",          
                        "details": "Data Read: 6.00 Bytes, Written: 6.00 Bytes",          
                        "copyDuration": "00:00:05",          
                        "dataVolume": "6.00 Bytes",          
                        "throughput": "1.16 Bytes/s",          
                        "totalDuration": "00:00:10"        
                    }      
            },      
        "error": null,      
        "executionStartTime": "2017-08-01T04:18:27.5747275Z",      
        "executionEndTime": "2017-08-01T04:18:46.4224091Z",     
        "duration": "00:00:18.8476816"    
    }
]

```
## <a name="next-steps"></a><span data-ttu-id="962c0-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="962c0-183">Next steps</span></span>
<span data-ttu-id="962c0-184">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="962c0-184">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="962c0-185">Execute Pipeline Activity</span><span class="sxs-lookup"><span data-stu-id="962c0-185">Execute Pipeline Activity</span></span>](control-flow-execute-pipeline-activity.md)
- [<span data-ttu-id="962c0-186">Get Metadata Activity</span><span class="sxs-lookup"><span data-stu-id="962c0-186">Get Metadata Activity</span></span>](control-flow-get-metadata-activity.md)
- [<span data-ttu-id="962c0-187">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="962c0-187">Lookup Activity</span></span>](control-flow-lookup-activity.md)
- [<span data-ttu-id="962c0-188">Web Activity</span><span class="sxs-lookup"><span data-stu-id="962c0-188">Web Activity</span></span>](control-flow-web-activity.md)
