---
title: 'Tutorial: Create a pipeline using Resource Manager Template | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using Azure Resource Manager template.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: spelluru
ms.openlocfilehash: b6fa00bc2638fef0902789bf76361da8cd137ce6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564611"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-azure-resource-manager-template"></a><span data-ttu-id="c52a9-103">Tutorial: Create a pipeline with Copy Activity using Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="c52a9-103">Tutorial: Create a pipeline with Copy Activity using Azure Resource Manager template</span></span>
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
> 

<span data-ttu-id="c52a9-112">This tutorial shows you how to create and monitor an Azure data factory using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="c52a9-112">This tutorial shows you how to create and monitor an Azure data factory using an Azure Resource Manager template.</span></span> <span data-ttu-id="c52a9-113">The pipeline in the data factory copies data from Azure Blob Storage to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c52a9-113">The pipeline in the data factory copies data from Azure Blob Storage to Azure SQL Database.</span></span>

> [!NOTE]
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 

## <a name="prerequisites"></a><span data-ttu-id="c52a9-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c52a9-119">Prerequisites</span></span>
* <span data-ttu-id="c52a9-120">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="c52a9-120">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="c52a9-121">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article to install latest version of Azure PowerShell on your computer.</span><span class="sxs-lookup"><span data-stu-id="c52a9-121">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="c52a9-122">In this tutorial, you use PowerShell to deploy Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="c52a9-122">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="c52a9-123">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="c52a9-123">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="c52a9-124">In this tutorial</span><span class="sxs-lookup"><span data-stu-id="c52a9-124">In this tutorial</span></span>
<span data-ttu-id="c52a9-125">In this tutorial, you create a data factory with the following Data Factory entities:</span><span class="sxs-lookup"><span data-stu-id="c52a9-125">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="c52a9-126">Entity</span><span class="sxs-lookup"><span data-stu-id="c52a9-126">Entity</span></span> | <span data-ttu-id="c52a9-127">Description</span><span class="sxs-lookup"><span data-stu-id="c52a9-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c52a9-128">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="c52a9-128">Azure Storage linked service</span></span> |<span data-ttu-id="c52a9-129">Links your Azure Storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="c52a9-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="c52a9-130">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="c52a9-130">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="c52a9-131">It specifies the storage account that contains the input data for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="c52a9-131">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="c52a9-132">Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="c52a9-132">Azure SQL Database linked service</span></span> |<span data-ttu-id="c52a9-133">Links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="c52a9-133">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="c52a9-134">It specifies the Azure SQL database that holds the output data for the copy activity.</span><span class="sxs-lookup"><span data-stu-id="c52a9-134">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="c52a9-135">Azure Blob input dataset</span><span class="sxs-lookup"><span data-stu-id="c52a9-135">Azure Blob input dataset</span></span> |<span data-ttu-id="c52a9-136">Refers to the Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="c52a9-136">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="c52a9-137">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span><span class="sxs-lookup"><span data-stu-id="c52a9-137">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="c52a9-138">Azure SQL output dataset</span><span class="sxs-lookup"><span data-stu-id="c52a9-138">Azure SQL output dataset</span></span> |<span data-ttu-id="c52a9-139">Refers to the Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="c52a9-139">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="c52a9-140">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="c52a9-140">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="c52a9-141">Data pipeline</span><span class="sxs-lookup"><span data-stu-id="c52a9-141">Data pipeline</span></span> |<span data-ttu-id="c52a9-142">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span><span class="sxs-lookup"><span data-stu-id="c52a9-142">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="c52a9-143">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c52a9-143">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="c52a9-144">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="c52a9-144">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c52a9-145">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="c52a9-145">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c52a9-146">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c52a9-146">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="c52a9-147">In this tutorial, you create a pipeline with one activity (copy activity).</span><span class="sxs-lookup"><span data-stu-id="c52a9-147">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Copy Azure Blob to Azure SQL Database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="c52a9-149">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span><span class="sxs-lookup"><span data-stu-id="c52a9-149">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="c52a9-150">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span><span class="sxs-lookup"><span data-stu-id="c52a9-150">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="c52a9-151">Data Factory JSON template</span><span class="sxs-lookup"><span data-stu-id="c52a9-151">Data Factory JSON template</span></span>
<span data-ttu-id="c52a9-152">The top-level Resource Manager template for defining a data factory is:</span><span class="sxs-lookup"><span data-stu-id="c52a9-152">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="c52a9-153">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span><span class="sxs-lookup"><span data-stu-id="c52a9-153">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

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
                "frequency": "Day",
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
                "frequency": "Day",
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
              "start": "2016-10-02T00:00:00Z",
              "end": "2016-10-03T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="c52a9-154">Parameters JSON</span><span class="sxs-lookup"><span data-stu-id="c52a9-154">Parameters JSON</span></span>
<span data-ttu-id="c52a9-155">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="c52a9-155">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> Specify the name and key of your Azure Storage account for **storageAccountName** and **storageAccountKey** parameters.  
> 
> 

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

## <a name="create-data-factory"></a><span data-ttu-id="c52a9-159">Create data factory</span><span class="sxs-lookup"><span data-stu-id="c52a9-159">Create data factory</span></span>
1. <span data-ttu-id="c52a9-160">Start **Azure PowerShell** and run the following command:</span><span class="sxs-lookup"><span data-stu-id="c52a9-160">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="c52a9-161">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c52a9-161">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="c52a9-162">Run the following command to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="c52a9-162">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="c52a9-163">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="c52a9-163">Run the following command to select the subscription that you want to work with.</span></span> 
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="c52a9-164">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span><span class="sxs-lookup"><span data-stu-id="c52a9-164">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="c52a9-165">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="c52a9-165">Monitor pipeline</span></span>

1. <span data-ttu-id="c52a9-166">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span><span class="sxs-lookup"><span data-stu-id="c52a9-166">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="c52a9-167">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span><span class="sxs-lookup"><span data-stu-id="c52a9-167">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Data factories menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="c52a9-169">In the **Data factories** page, search for and find your data factory.</span><span class="sxs-lookup"><span data-stu-id="c52a9-169">In the **Data factories** page, search for and find your data factory.</span></span> 
   
    ![Search for data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="c52a9-171">Click your Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="c52a9-171">Click your Azure data factory.</span></span> <span data-ttu-id="c52a9-172">You see the home page for the data factory.</span><span class="sxs-lookup"><span data-stu-id="c52a9-172">You see the home page for the data factory.</span></span>
   
    ![Home page for data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
5. <span data-ttu-id="c52a9-174">Click **Diagram** tile to see the diagram view of your data factory.</span><span class="sxs-lookup"><span data-stu-id="c52a9-174">Click **Diagram** tile to see the diagram view of your data factory.</span></span>
   
    ![Diagram view of data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-diagram-view.png)
6. <span data-ttu-id="c52a9-176">In the diagram view, double-click the dataset **SQLOutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c52a9-176">In the diagram view, double-click the dataset **SQLOutputDataset**.</span></span> <span data-ttu-id="c52a9-177">You see that status of the slice.</span><span class="sxs-lookup"><span data-stu-id="c52a9-177">You see that status of the slice.</span></span> <span data-ttu-id="c52a9-178">When the copy operation is done, you the status set to **Ready**.</span><span class="sxs-lookup"><span data-stu-id="c52a9-178">When the copy operation is done, you the status set to **Ready**.</span></span>
   
    ![Output slice in ready state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/output-slice-ready.png)
7. <span data-ttu-id="c52a9-180">When the slice is in **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c52a9-180">When the slice is in **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>

<span data-ttu-id="c52a9-181">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="c52a9-181">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="c52a9-182">You can also use Monitor and Manage App to monitor your data pipelines.</span><span class="sxs-lookup"><span data-stu-id="c52a9-182">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="c52a9-183">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span><span class="sxs-lookup"><span data-stu-id="c52a9-183">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="c52a9-184">Data Factory entities in the template</span><span class="sxs-lookup"><span data-stu-id="c52a9-184">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="c52a9-185">Define data factory</span><span class="sxs-lookup"><span data-stu-id="c52a9-185">Define data factory</span></span>
<span data-ttu-id="c52a9-186">You define a data factory in the Resource Manager template as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="c52a9-186">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="c52a9-187">The dataFactoryName is defined as:</span><span class="sxs-lookup"><span data-stu-id="c52a9-187">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="c52a9-188">It is a unique string based on the resource group ID.</span><span class="sxs-lookup"><span data-stu-id="c52a9-188">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="c52a9-189">Defining Data Factory entities</span><span class="sxs-lookup"><span data-stu-id="c52a9-189">Defining Data Factory entities</span></span>
<span data-ttu-id="c52a9-190">The following Data Factory entities are defined in the JSON template:</span><span class="sxs-lookup"><span data-stu-id="c52a9-190">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="c52a9-191">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="c52a9-191">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="c52a9-192">Azure SQL linked service</span><span class="sxs-lookup"><span data-stu-id="c52a9-192">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="c52a9-193">Azure blob dataset</span><span class="sxs-lookup"><span data-stu-id="c52a9-193">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="c52a9-194">Azure SQL dataset</span><span class="sxs-lookup"><span data-stu-id="c52a9-194">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="c52a9-195">Data pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="c52a9-195">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="c52a9-196">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="c52a9-196">Azure Storage linked service</span></span>
<span data-ttu-id="c52a9-197">You specify the name and key of your Azure storage account in this section.</span><span class="sxs-lookup"><span data-stu-id="c52a9-197">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="c52a9-198">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="c52a9-198">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="c52a9-199">The connectionString uses the storageAccountName and storageAccountKey parameters.</span><span class="sxs-lookup"><span data-stu-id="c52a9-199">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="c52a9-200">The values for these parameters passed by using a configuration file.</span><span class="sxs-lookup"><span data-stu-id="c52a9-200">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="c52a9-201">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span><span class="sxs-lookup"><span data-stu-id="c52a9-201">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="c52a9-202">Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="c52a9-202">Azure SQL Database linked service</span></span>
<span data-ttu-id="c52a9-203">You specify the Azure SQL server name, database name, user name, and user password in this section.</span><span class="sxs-lookup"><span data-stu-id="c52a9-203">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="c52a9-204">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="c52a9-204">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="c52a9-205">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span><span class="sxs-lookup"><span data-stu-id="c52a9-205">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="c52a9-206">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="c52a9-206">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="c52a9-207">Azure blob dataset</span><span class="sxs-lookup"><span data-stu-id="c52a9-207">Azure blob dataset</span></span>
<span data-ttu-id="c52a9-208">You specify the names of blob container, folder, and file that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="c52a9-208">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="c52a9-209">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="c52a9-209">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
            "frequency": "Day",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="c52a9-210">Azure SQL dataset</span><span class="sxs-lookup"><span data-stu-id="c52a9-210">Azure SQL dataset</span></span>
<span data-ttu-id="c52a9-211">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="c52a9-211">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="c52a9-212">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span><span class="sxs-lookup"><span data-stu-id="c52a9-212">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

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
            "frequency": "Day",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="c52a9-213">Data pipeline</span><span class="sxs-lookup"><span data-stu-id="c52a9-213">Data pipeline</span></span>
<span data-ttu-id="c52a9-214">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span><span class="sxs-lookup"><span data-stu-id="c52a9-214">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="c52a9-215">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span><span class="sxs-lookup"><span data-stu-id="c52a9-215">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

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
          "start": "2016-10-02T00:00:00Z",
          "end": "2016-10-03T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="c52a9-216">Reuse the template</span><span class="sxs-lookup"><span data-stu-id="c52a9-216">Reuse the template</span></span>
<span data-ttu-id="c52a9-217">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span><span class="sxs-lookup"><span data-stu-id="c52a9-217">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="c52a9-218">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span><span class="sxs-lookup"><span data-stu-id="c52a9-218">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="c52a9-219">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span><span class="sxs-lookup"><span data-stu-id="c52a9-219">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="c52a9-220">Example:</span><span class="sxs-lookup"><span data-stu-id="c52a9-220">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="c52a9-221">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span><span class="sxs-lookup"><span data-stu-id="c52a9-221">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="c52a9-222">You can also reuse the template to perform repeated tasks.</span><span class="sxs-lookup"><span data-stu-id="c52a9-222">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="c52a9-223">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span><span class="sxs-lookup"><span data-stu-id="c52a9-223">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="c52a9-224">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span><span class="sxs-lookup"><span data-stu-id="c52a9-224">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="see-also"></a><span data-ttu-id="c52a9-225">See Also</span><span class="sxs-lookup"><span data-stu-id="c52a9-225">See Also</span></span>
| <span data-ttu-id="c52a9-226">Topic</span><span class="sxs-lookup"><span data-stu-id="c52a9-226">Topic</span></span> | <span data-ttu-id="c52a9-227">Description</span><span class="sxs-lookup"><span data-stu-id="c52a9-227">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c52a9-228">Pipelines</span><span class="sxs-lookup"><span data-stu-id="c52a9-228">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c52a9-229">This article helps you understand pipelines and activities in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c52a9-229">This article helps you understand pipelines and activities in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c52a9-230">Datasets</span><span class="sxs-lookup"><span data-stu-id="c52a9-230">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c52a9-231">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c52a9-231">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c52a9-232">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="c52a9-232">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c52a9-233">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="c52a9-233">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |





