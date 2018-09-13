---
title: Build your first data factory (Resource Manager template) | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline using an Azure Resource Manager template.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/17/2017
ms.author: spelluru
ms.openlocfilehash: f9b994164c7812f62401524c3d43390ecb8e136a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564628"
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="4ce22-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="4ce22-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="4ce22-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="4ce22-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="4ce22-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="4ce22-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

> [!NOTE]
> The data pipeline in this tutorial transforms input data to produce output data. It does not copy data from a source data store to a destination data store. For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 

## <a name="prerequisites"></a><span data-ttu-id="4ce22-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4ce22-117">Prerequisites</span></span>
* <span data-ttu-id="4ce22-118">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="4ce22-118">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="4ce22-119">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article to install latest version of Azure PowerShell on your computer.</span><span class="sxs-lookup"><span data-stu-id="4ce22-119">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="4ce22-120">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="4ce22-120">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="4ce22-121">In this tutorial</span><span class="sxs-lookup"><span data-stu-id="4ce22-121">In this tutorial</span></span>
| <span data-ttu-id="4ce22-122">Entity</span><span class="sxs-lookup"><span data-stu-id="4ce22-122">Entity</span></span> | <span data-ttu-id="4ce22-123">Description</span><span class="sxs-lookup"><span data-stu-id="4ce22-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4ce22-124">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="4ce22-124">Azure Storage linked service</span></span> |<span data-ttu-id="4ce22-125">Links your Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="4ce22-125">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="4ce22-126">The Azure Storage account holds the input and output data for the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="4ce22-126">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="4ce22-127">HDInsight on-demand linked service</span><span class="sxs-lookup"><span data-stu-id="4ce22-127">HDInsight on-demand linked service</span></span> |<span data-ttu-id="4ce22-128">Links an on-demand HDInsight cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="4ce22-128">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="4ce22-129">The cluster is automatically created for you to process data and is deleted after the processing is done.</span><span class="sxs-lookup"><span data-stu-id="4ce22-129">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="4ce22-130">Azure Blob input dataset</span><span class="sxs-lookup"><span data-stu-id="4ce22-130">Azure Blob input dataset</span></span> |<span data-ttu-id="4ce22-131">Refers to the Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="4ce22-131">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="4ce22-132">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span><span class="sxs-lookup"><span data-stu-id="4ce22-132">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="4ce22-133">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="4ce22-133">Azure Blob output dataset</span></span> |<span data-ttu-id="4ce22-134">Refers to the Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="4ce22-134">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="4ce22-135">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="4ce22-135">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="4ce22-136">Data pipeline</span><span class="sxs-lookup"><span data-stu-id="4ce22-136">Data pipeline</span></span> |<span data-ttu-id="4ce22-137">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span><span class="sxs-lookup"><span data-stu-id="4ce22-137">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="4ce22-138">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="4ce22-138">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4ce22-139">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="4ce22-139">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="4ce22-140">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4ce22-140">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="4ce22-141">In this tutorial, you create a pipeline with one activity (copy activity).</span><span class="sxs-lookup"><span data-stu-id="4ce22-141">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

<span data-ttu-id="4ce22-142">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span><span class="sxs-lookup"><span data-stu-id="4ce22-142">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="4ce22-143">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span><span class="sxs-lookup"><span data-stu-id="4ce22-143">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="4ce22-144">Data Factory JSON template</span><span class="sxs-lookup"><span data-stu-id="4ce22-144">Data Factory JSON template</span></span>
<span data-ttu-id="4ce22-145">The top-level Resource Manager template for defining a data factory is:</span><span class="sxs-lookup"><span data-stu-id="4ce22-145">The top-level Resource Manager template for defining a data factory is:</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
<span data-ttu-id="4ce22-146">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="4ce22-146">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "clusterSize": 1,
                    "version": "3.2",
                    "timeToLive": "00:05:00",
                    "osType": "windows",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2016-10-01T00:00:00Z",
                  "end": "2016-10-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="4ce22-148">Parameters JSON</span><span class="sxs-lookup"><span data-stu-id="4ce22-148">Parameters JSON</span></span>
<span data-ttu-id="4ce22-149">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="4ce22-149">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file. 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template. By using a Power Shell script, you can automate deploying Data Factory entities in these environments. 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="4ce22-153">Create data factory</span><span class="sxs-lookup"><span data-stu-id="4ce22-153">Create data factory</span></span>
1. <span data-ttu-id="4ce22-154">Start **Azure PowerShell** and run the following command:</span><span class="sxs-lookup"><span data-stu-id="4ce22-154">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="4ce22-155">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4ce22-155">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="4ce22-156">Run the following command to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="4ce22-156">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="4ce22-157">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="4ce22-157">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="4ce22-158">This subscription should be the same as the one you used in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4ce22-158">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="4ce22-159">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span><span class="sxs-lookup"><span data-stu-id="4ce22-159">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="4ce22-160">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="4ce22-160">Monitor pipeline</span></span>
1. <span data-ttu-id="4ce22-161">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="4ce22-161">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="4ce22-162">![Browse->Data factories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="4ce22-162">![Browse->Data factories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="4ce22-163">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span><span class="sxs-lookup"><span data-stu-id="4ce22-163">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="4ce22-164">In the **Data Factory** blade for your data factory, click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="4ce22-164">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Diagram Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="4ce22-166">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4ce22-166">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![Diagram View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="4ce22-168">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="4ce22-168">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="4ce22-169">You see that the slice that is currently being processed.</span><span class="sxs-lookup"><span data-stu-id="4ce22-169">You see that the slice that is currently being processed.</span></span>
   
    ![Dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="4ce22-171">When processing is done, you see the slice in **Ready** state.</span><span class="sxs-lookup"><span data-stu-id="4ce22-171">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="4ce22-172">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span><span class="sxs-lookup"><span data-stu-id="4ce22-172">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="4ce22-173">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span><span class="sxs-lookup"><span data-stu-id="4ce22-173">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Dataset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="4ce22-175">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span><span class="sxs-lookup"><span data-stu-id="4ce22-175">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="4ce22-176">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4ce22-176">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="4ce22-177">You can also use Monitor and Manage App to monitor your data pipelines.</span><span class="sxs-lookup"><span data-stu-id="4ce22-177">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="4ce22-178">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span><span class="sxs-lookup"><span data-stu-id="4ce22-178">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> The input file gets deleted when the slice is processed successfully. Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="4ce22-181">Data Factory entities in the template</span><span class="sxs-lookup"><span data-stu-id="4ce22-181">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="4ce22-182">Define data factory</span><span class="sxs-lookup"><span data-stu-id="4ce22-182">Define data factory</span></span>
<span data-ttu-id="4ce22-183">You define a data factory in the Resource Manager template as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="4ce22-183">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="4ce22-184">The dataFactoryName is defined as:</span><span class="sxs-lookup"><span data-stu-id="4ce22-184">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="4ce22-185">It is a unique string based on the resource group ID.</span><span class="sxs-lookup"><span data-stu-id="4ce22-185">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="4ce22-186">Defining Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="4ce22-186">Defining Data Factory entities</span></span>
<span data-ttu-id="4ce22-187">The following Data Factory entities are defined in the JSON template:</span><span class="sxs-lookup"><span data-stu-id="4ce22-187">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="4ce22-188">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="4ce22-188">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="4ce22-189">HDInsight on-demand linked service</span><span class="sxs-lookup"><span data-stu-id="4ce22-189">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="4ce22-190">Azure blob input dataset</span><span class="sxs-lookup"><span data-stu-id="4ce22-190">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="4ce22-191">Azure blob output dataset</span><span class="sxs-lookup"><span data-stu-id="4ce22-191">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="4ce22-192">Data pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="4ce22-192">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="4ce22-193">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="4ce22-193">Azure Storage linked service</span></span>
<span data-ttu-id="4ce22-194">You specify the name and key of your Azure storage account in this section.</span><span class="sxs-lookup"><span data-stu-id="4ce22-194">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="4ce22-195">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="4ce22-195">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="4ce22-196">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span><span class="sxs-lookup"><span data-stu-id="4ce22-196">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="4ce22-197">The values for these parameters passed by using a configuration file.</span><span class="sxs-lookup"><span data-stu-id="4ce22-197">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="4ce22-198">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span><span class="sxs-lookup"><span data-stu-id="4ce22-198">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="4ce22-199">HDInsight on-demand linked service</span><span class="sxs-lookup"><span data-stu-id="4ce22-199">HDInsight on-demand linked service</span></span>
<span data-ttu-id="4ce22-200">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span><span class="sxs-lookup"><span data-stu-id="4ce22-200">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "clusterSize": 1,
            "version": "3.2",
            "timeToLive": "00:05:00",
            "osType": "windows",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="4ce22-201">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="4ce22-201">Note the following points:</span></span> 

* <span data-ttu-id="4ce22-202">The Data Factory creates a **Windows-based** HDInsight cluster for you with the above JSON.</span><span class="sxs-lookup"><span data-stu-id="4ce22-202">The Data Factory creates a **Windows-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="4ce22-203">You could also have it create a **Linux-based** HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4ce22-203">You could also have it create a **Linux-based** HDInsight cluster.</span></span> <span data-ttu-id="4ce22-204">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="4ce22-204">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="4ce22-205">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4ce22-205">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="4ce22-206">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="4ce22-206">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="4ce22-207">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="4ce22-207">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="4ce22-208">HDInsight does not delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="4ce22-208">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="4ce22-209">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="4ce22-209">This behavior is by design.</span></span> <span data-ttu-id="4ce22-210">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="4ce22-210">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="4ce22-211">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4ce22-211">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="4ce22-212">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="4ce22-212">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="4ce22-213">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="4ce22-213">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="4ce22-214">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="4ce22-214">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="4ce22-215">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="4ce22-215">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="4ce22-216">Azure blob input dataset</span><span class="sxs-lookup"><span data-stu-id="4ce22-216">Azure blob input dataset</span></span>
<span data-ttu-id="4ce22-217">You specify the names of blob container, folder, and file that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="4ce22-217">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="4ce22-218">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="4ce22-218">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="4ce22-219">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="4ce22-219">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="4ce22-220">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="4ce22-220">Azure Blob output dataset</span></span>
<span data-ttu-id="4ce22-221">You specify the names of blob container and folder that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="4ce22-221">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="4ce22-222">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="4ce22-222">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="4ce22-223">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="4ce22-223">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="4ce22-224">Data pipeline</span><span class="sxs-lookup"><span data-stu-id="4ce22-224">Data pipeline</span></span>
<span data-ttu-id="4ce22-225">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4ce22-225">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="4ce22-226">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span><span class="sxs-lookup"><span data-stu-id="4ce22-226">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2016-10-01T00:00:00Z",
        "end": "2016-10-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="4ce22-227">Reuse the template</span><span class="sxs-lookup"><span data-stu-id="4ce22-227">Reuse the template</span></span>
<span data-ttu-id="4ce22-228">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span><span class="sxs-lookup"><span data-stu-id="4ce22-228">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="4ce22-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span><span class="sxs-lookup"><span data-stu-id="4ce22-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="4ce22-230">Example:</span><span class="sxs-lookup"><span data-stu-id="4ce22-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="4ce22-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span><span class="sxs-lookup"><span data-stu-id="4ce22-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="4ce22-232">You can also reuse the template to perform repeated tasks.</span><span class="sxs-lookup"><span data-stu-id="4ce22-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="4ce22-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span><span class="sxs-lookup"><span data-stu-id="4ce22-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="4ce22-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span><span class="sxs-lookup"><span data-stu-id="4ce22-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="4ce22-235">Resource Manager template for creating a gateway</span><span class="sxs-lookup"><span data-stu-id="4ce22-235">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="4ce22-236">Here is a sample Resource Manager template for creating a logical gateway in the back.</span><span class="sxs-lookup"><span data-stu-id="4ce22-236">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="4ce22-237">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span><span class="sxs-lookup"><span data-stu-id="4ce22-237">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="4ce22-238">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span><span class="sxs-lookup"><span data-stu-id="4ce22-238">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
<span data-ttu-id="4ce22-239">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="4ce22-239">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="4ce22-240">See Also</span><span class="sxs-lookup"><span data-stu-id="4ce22-240">See Also</span></span>
| <span data-ttu-id="4ce22-241">Topic</span><span class="sxs-lookup"><span data-stu-id="4ce22-241">Topic</span></span> | <span data-ttu-id="4ce22-242">Description</span><span class="sxs-lookup"><span data-stu-id="4ce22-242">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="4ce22-243">Pipelines</span><span class="sxs-lookup"><span data-stu-id="4ce22-243">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="4ce22-244">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="4ce22-244">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="4ce22-245">Datasets</span><span class="sxs-lookup"><span data-stu-id="4ce22-245">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="4ce22-246">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4ce22-246">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="4ce22-247">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="4ce22-247">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="4ce22-248">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="4ce22-248">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="4ce22-249">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="4ce22-249">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="4ce22-250">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="4ce22-250">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |






