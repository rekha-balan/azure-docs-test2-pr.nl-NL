---
title: 'Tutorial: Create a pipeline using Resource Manager Template | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline by using an Azure Resource Manager template. This pipeline copies data from an Azure blob storage to an Azure SQL database.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: ''
editor: ''
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 2b23239fd82198747980fd527c478647743028c4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869475"
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="dacec-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span><span class="sxs-lookup"><span data-stu-id="dacec-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
> * [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-dot-net.md). 

<span data-ttu-id="dacec-115">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="dacec-115">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="dacec-116">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span><span class="sxs-lookup"><span data-stu-id="dacec-116">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="dacec-117">It does not transform input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="dacec-117">It does not transform input data to produce output data.</span></span> <span data-ttu-id="dacec-118">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="dacec-118">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="dacec-119">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="dacec-119">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="dacec-120">The copy activity copies data from a supported data store to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="dacec-120">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="dacec-121">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="dacec-121">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="dacec-122">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="dacec-122">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="dacec-123">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="dacec-123">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="dacec-124">A pipeline can have more than one activity.</span><span class="sxs-lookup"><span data-stu-id="dacec-124">A pipeline can have more than one activity.</span></span> <span data-ttu-id="dacec-125">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="dacec-125">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="dacec-126">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="dacec-126">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> The data pipeline in this tutorial copies data from a source data store to a destination data store. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a><span data-ttu-id="dacec-129">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dacec-129">Prerequisites</span></span>
* <span data-ttu-id="dacec-130">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="dacec-130">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="dacec-131">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span><span class="sxs-lookup"><span data-stu-id="dacec-131">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="dacec-132">In this tutorial, you use PowerShell to deploy Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="dacec-132">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="dacec-133">(optional) See [Authoring Azure Resource Manager Templates](../../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="dacec-133">(optional) See [Authoring Azure Resource Manager Templates](../../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="dacec-134">In this tutorial</span><span class="sxs-lookup"><span data-stu-id="dacec-134">In this tutorial</span></span>
<span data-ttu-id="dacec-135">In this tutorial, you create a data factory with the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="dacec-135">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="dacec-136">Entity</span><span class="sxs-lookup"><span data-stu-id="dacec-136">Entity</span></span> | <span data-ttu-id="dacec-137">Description</span><span class="sxs-lookup"><span data-stu-id="dacec-137">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dacec-138">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="dacec-138">Azure Storage linked service</span></span> |<span data-ttu-id="dacec-139">Links your Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="dacec-139">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="dacec-140">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="dacec-140">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="dacec-141">It specifies the storage account that contains the input data for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="dacec-141">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="dacec-142">Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="dacec-142">Azure SQL Database linked service</span></span> |<span data-ttu-id="dacec-143">Links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="dacec-143">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="dacec-144">It specifies the Azure SQL database that holds the output data for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="dacec-144">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="dacec-145">Azure Blob input dataset</span><span class="sxs-lookup"><span data-stu-id="dacec-145">Azure Blob input dataset</span></span> |<span data-ttu-id="dacec-146">Refers to the Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="dacec-146">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="dacec-147">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span><span class="sxs-lookup"><span data-stu-id="dacec-147">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="dacec-148">Azure SQL output dataset</span><span class="sxs-lookup"><span data-stu-id="dacec-148">Azure SQL output dataset</span></span> |<span data-ttu-id="dacec-149">Refers to the Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="dacec-149">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="dacec-150">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="dacec-150">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="dacec-151">Data pipeline</span><span class="sxs-lookup"><span data-stu-id="dacec-151">Data pipeline</span></span> |<span data-ttu-id="dacec-152">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="dacec-152">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="dacec-153">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dacec-153">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="dacec-154">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="dacec-154">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="dacec-155">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="dacec-155">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="dacec-156">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="dacec-156">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="dacec-157">In this tutorial, you create a pipeline with one activity (copy activity).</span><span class="sxs-lookup"><span data-stu-id="dacec-157">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Copy Azure Blob to Azure SQL Database](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="dacec-159">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span><span class="sxs-lookup"><span data-stu-id="dacec-159">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="dacec-160">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span><span class="sxs-lookup"><span data-stu-id="dacec-160">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="dacec-161">Data Factory JSON template</span><span class="sxs-lookup"><span data-stu-id="dacec-161">Data Factory JSON template</span></span>
<span data-ttu-id="dacec-162">The top-level Resource Manager template for defining a data factory is:</span><span class="sxs-lookup"><span data-stu-id="dacec-162">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="dacec-163">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="dacec-163">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
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
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
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
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
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
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob to Azure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="dacec-164">Parameters JSON</span><span class="sxs-lookup"><span data-stu-id="dacec-164">Parameters JSON</span></span>
<span data-ttu-id="dacec-165">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="dacec-165">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.  
> 
> Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template. By using a Power Shell script, you can automate deploying Data Factory entities in these environments.  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="dacec-170">Create data factory</span><span class="sxs-lookup"><span data-stu-id="dacec-170">Create data factory</span></span>
1. <span data-ttu-id="dacec-171">Start **Azure PowerShell** and run the following command:</span><span class="sxs-lookup"><span data-stu-id="dacec-171">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="dacec-172">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dacec-172">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Connect-AzureRmAccount      
    ```  
   * <span data-ttu-id="dacec-173">Run the following command to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="dacec-173">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="dacec-174">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="dacec-174">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="dacec-175">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span><span class="sxs-lookup"><span data-stu-id="dacec-175">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="dacec-176">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="dacec-176">Monitor pipeline</span></span>

1. <span data-ttu-id="dacec-177">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span><span class="sxs-lookup"><span data-stu-id="dacec-177">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="dacec-178">Click **Data factories** on the left menu (or) click **All services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span><span class="sxs-lookup"><span data-stu-id="dacec-178">Click **Data factories** on the left menu (or) click **All services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Data factories menu](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="dacec-180">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="dacec-180">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Search for data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="dacec-182">Click your Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="dacec-182">Click your Azure data factory.</span></span> <span data-ttu-id="dacec-183">You see the home page for the data factory.</span><span class="sxs-lookup"><span data-stu-id="dacec-183">You see the home page for the data factory.</span></span>
   
    ![Home page for data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="dacec-185">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="dacec-185">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="dacec-186">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="dacec-186">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="dacec-187">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dacec-187">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="dacec-188">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="dacec-188">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="dacec-189">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="dacec-189">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="dacec-190">Data Factory entities in the template</span><span class="sxs-lookup"><span data-stu-id="dacec-190">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="dacec-191">Define data factory</span><span class="sxs-lookup"><span data-stu-id="dacec-191">Define data factory</span></span>
<span data-ttu-id="dacec-192">You define a data factory in the Resource Manager template as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="dacec-192">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="dacec-193">The dataFactoryName is defined as:</span><span class="sxs-lookup"><span data-stu-id="dacec-193">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="dacec-194">It is a unique string based on the resource group ID.</span><span class="sxs-lookup"><span data-stu-id="dacec-194">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="dacec-195">Defining Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="dacec-195">Defining Data Factory entities</span></span>
<span data-ttu-id="dacec-196">The following Data Factory entities are defined in the JSON template:</span><span class="sxs-lookup"><span data-stu-id="dacec-196">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="dacec-197">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="dacec-197">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="dacec-198">Azure SQL linked service</span><span class="sxs-lookup"><span data-stu-id="dacec-198">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="dacec-199">Azure blob dataset</span><span class="sxs-lookup"><span data-stu-id="dacec-199">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="dacec-200">Azure SQL dataset</span><span class="sxs-lookup"><span data-stu-id="dacec-200">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="dacec-201">Data pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="dacec-201">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="dacec-202">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="dacec-202">Azure Storage linked service</span></span>
<span data-ttu-id="dacec-203">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="dacec-203">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="dacec-204">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="dacec-204">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="dacec-205">You specify the name and key of your Azure storage account in this section.</span><span class="sxs-lookup"><span data-stu-id="dacec-205">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="dacec-206">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="dacec-206">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="dacec-207">The connectionString uses the storageAccountName and storageAccountKey parameters.</span><span class="sxs-lookup"><span data-stu-id="dacec-207">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="dacec-208">The values for these parameters passed by using a configuration file.</span><span class="sxs-lookup"><span data-stu-id="dacec-208">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="dacec-209">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span><span class="sxs-lookup"><span data-stu-id="dacec-209">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="dacec-210">Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="dacec-210">Azure SQL Database linked service</span></span>
<span data-ttu-id="dacec-211">AzureSqlLinkedService links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="dacec-211">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="dacec-212">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="dacec-212">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="dacec-213">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="dacec-213">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="dacec-214">You specify the Azure SQL server name, database name, user name, and user password in this section.</span><span class="sxs-lookup"><span data-stu-id="dacec-214">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="dacec-215">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="dacec-215">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="dacec-216">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span><span class="sxs-lookup"><span data-stu-id="dacec-216">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="dacec-217">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="dacec-217">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="dacec-218">Azure blob dataset</span><span class="sxs-lookup"><span data-stu-id="dacec-218">Azure blob dataset</span></span>
<span data-ttu-id="dacec-219">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="dacec-219">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="dacec-220">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="dacec-220">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="dacec-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="dacec-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="dacec-222">Azure SQL dataset</span><span class="sxs-lookup"><span data-stu-id="dacec-222">Azure SQL dataset</span></span>
<span data-ttu-id="dacec-223">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="dacec-223">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="dacec-224">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span><span class="sxs-lookup"><span data-stu-id="dacec-224">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="dacec-225">Data pipeline</span><span class="sxs-lookup"><span data-stu-id="dacec-225">Data pipeline</span></span>
<span data-ttu-id="dacec-226">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span><span class="sxs-lookup"><span data-stu-id="dacec-226">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="dacec-227">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span><span class="sxs-lookup"><span data-stu-id="dacec-227">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob to Azure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="dacec-228">Reuse the template</span><span class="sxs-lookup"><span data-stu-id="dacec-228">Reuse the template</span></span>
<span data-ttu-id="dacec-229">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span><span class="sxs-lookup"><span data-stu-id="dacec-229">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="dacec-230">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span><span class="sxs-lookup"><span data-stu-id="dacec-230">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="dacec-231">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span><span class="sxs-lookup"><span data-stu-id="dacec-231">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="dacec-232">Example:</span><span class="sxs-lookup"><span data-stu-id="dacec-232">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="dacec-233">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span><span class="sxs-lookup"><span data-stu-id="dacec-233">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="dacec-234">You can also reuse the template to perform repeated tasks.</span><span class="sxs-lookup"><span data-stu-id="dacec-234">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="dacec-235">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span><span class="sxs-lookup"><span data-stu-id="dacec-235">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="dacec-236">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span><span class="sxs-lookup"><span data-stu-id="dacec-236">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="dacec-237">Next steps</span><span class="sxs-lookup"><span data-stu-id="dacec-237">Next steps</span></span>
<span data-ttu-id="dacec-238">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="dacec-238">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="dacec-239">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span><span class="sxs-lookup"><span data-stu-id="dacec-239">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="dacec-240">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span><span class="sxs-lookup"><span data-stu-id="dacec-240">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
